---
ms.openlocfilehash: 69d77c19cb2c589086df2b4bf19eeadf41aad58a
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274208"
---
<!-- markdownlint-disable MD002 MD041 -->

Neste exercício, você habilita o [SSO (single sign-on)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins) do Complemento do Office no complemento e estende a API Web para dar suporte ao fluxo em nome [de.](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) Isso é necessário para obter o token de acesso OAuth necessário para chamar o Microsoft Graph.

## <a name="overview"></a>Visão Geral

O SSO do Complemento do Office fornece um token de acesso, mas esse token só permite que o complemento chame sua própria API Web. Ele não habilita o acesso direto ao Microsoft Graph. O processo funciona da seguinte forma.

1. O complemento obtém um token chamando [getAccessToken](https://docs.microsoft.com/javascript/api/office-runtime/officeruntime.auth?view=common-js#getaccesstoken-options-). A audiência desse token (a declaração) é a ID do aplicativo do `aud` registro de aplicativo do complemento.
1. O complemento envia esse token no título `Authorization` quando faz uma chamada para a API da Web.
1. A API Web valida o token e usa o fluxo em nome de para trocar esse token por um token do Microsoft Graph. O público-alvo desse novo token é `https://graph.microsoft.com` .
1. A API Web usa o novo token para fazer chamadas para o Microsoft Graph e retorna os resultados para o complemento.

## <a name="configure-the-solution"></a>Configurar a solução

1. Abra **./.env e** atualize a ID do aplicativo e o segredo do cliente `AZURE_APP_ID` do registro do `AZURE_CLIENT_SECRET` aplicativo.

    > [!IMPORTANT]
    > Se você estiver usando o controle de código-fonte, como git, agora seria um bom momento para excluir o arquivo **.env** do controle de código-fonte para evitar o vazamento inadvertida da ID do aplicativo e do segredo do cliente.

1. Abra **./manifest/manifest.xml** e substitua todas as instâncias `YOUR_APP_ID_HERE` pela ID do aplicativo do registro do aplicativo.

1. Crie um novo arquivo no diretório **./src/addin** chamado **config.js** e adicione o código a seguir, substituindo pela ID do aplicativo do `YOUR_APP_ID_HERE` registro do aplicativo.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/config.example.js":::

## <a name="implement-sign-in"></a>Implementar a login

1. Abra **./src/api/auth.ts** e adicione as instruções a seguir `import` na parte superior do arquivo.

    ```typescript
    import jwt, { SigningKeyCallback, JwtHeader } from 'jsonwebtoken';
    import jwksClient from 'jwks-rsa';
    import * as msal from '@azure/msal-node';
    ```

1. Adicione o código a seguir após as `import` instruções.

    :::code language="typescript" source="../demo/graph-tutorial/src/api/auth.ts" id="TokenExchangeSnippet":::

    Esse código inicializa um cliente [confidencial da MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/initialize-confidential-client-application.md)e exporta uma função para obter um token do Graph do token enviado pelo complemento.

1. Adicione o seguinte código antes da `export default authRouter;` linha.

    :::code language="typescript" source="../demo/graph-tutorial/src/api/auth.ts" id="GetAuthStatusSnippet":::

    Esse código implementa uma API ( ) que verifica se o token do complemento pode ser trocado silenciosamente `GET /auth/status` por um token do Graph. O add-in usará essa API para determinar se ele precisa apresentar um logon interativo para o usuário.

1. Abra **./src/addin/taskpane.js** e adicione o seguinte código ao arquivo.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="AuthUiSnippet":::

    Este código adiciona funções para atualizar a interface do usuário e usar a API da Caixa de Diálogo do [Office](https://docs.microsoft.com/office/dev/add-ins/develop/dialog-api-in-office-add-ins) para iniciar um fluxo de autenticação interativa.

1. Adicione a função a seguir para implementar uma interface do usuário principal temporária.

    ```javascript
    function showMainUi() {
      $('.container').empty();
      $('<p/>', {
        class: 'ms-fontSize-24 ms-fontWeight-bold',
        text: 'Authenticated!'
      }).appendTo('.container');
    }
    ```

1. Substitua a chamada `Office.onReady` existente pelo seguinte.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="OfficeReadySnippet":::

    Considere o que esse código faz.

    - Quando o painel de tarefas é carregado pela primeira vez, ele chama para obter um token com escopo para `getAccessToken` a API Web do complemento.
    - Ele usa esse token para chamar a API para verificar se o usuário `/auth/status` deu consentimento para os escopos do Microsoft Graph ainda.
        - Se o usuário não tiver consentido, ele usará uma janela pop-up para obter o consentimento do usuário por meio de um logon interativo.
        - Se o usuário tiver consentido, ele carregará a interface do usuário principal.

### <a name="getting-user-consent"></a>Obter consentimento do usuário

Mesmo que o complemento esteja usando o SSO, o usuário ainda precisa consentir com o complemento acessando seus dados por meio do Microsoft Graph. Obter consentimento é um processo único. Depois que o usuário conceder consentimento, o token SSO poderá ser trocado por um token do Graph sem qualquer interação do usuário. Nesta seção, você implementará a experiência de consentimento no complemento usando [msal-browser.](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser)

1. Crie um novo arquivo no **diretório ./src/addin** chamado **consent.js** e adicione o código a seguir.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/consent.js" id="ConsentJsSnippet":::

    Esse código faz logon para o usuário, solicitando o conjunto de permissões do Microsoft Graph que estão configuradas no registro do aplicativo.

1. Crie um novo arquivo no **diretório ./src/addin** **chamadoconsent.html** e adicione o código a seguir.

    :::code language="html" source="../demo/graph-tutorial/src/addin/consent.html" id="ConsentHtmlSnippet":::

    Este código implementa uma página HTML básica para carregar o **consent.js** arquivo. Esta página será carregada em uma caixa de diálogo pop-up.

1. Salve todas as suas alterações e reinicie o servidor.

1. Carregue seu arquivo **manifest.xml** usando as mesmas etapas em [Side-load do complemento no Excel.](02-create-app.md#side-load-the-add-in-in-excel)

1. Selecione o **botão Importar Calendário** na guia **Página** Início para abrir o painel de tarefas.

1. Selecione o **botão Dar permissão** no painel de tarefas para iniciar a caixa de diálogo de consentimento em uma janela pop-up. Entre e conceda consentimento.

1. O painel de tarefas é atualizado com um "Autenticado!" message. Você pode verificar os tokens da seguinte forma.

    - Nas ferramentas de desenvolvedor do seu navegador, o token de API é mostrado no Console.
    - Na CLI em que você está executando o servidor Node.js, o token do Graph é impresso.

    Você pode comparar esses tokens em [https://jwt.ms](https://jwt.ms) . Observe que o público do token de API ( ) é definido como a ID do aplicativo do registro do seu aplicativo, e o escopo `aud` ( `scp` ) é `access_as_user` .
