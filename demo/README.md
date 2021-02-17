---
ms.openlocfilehash: fed56663591ac36e4defcae3a8d0a222f86e3026
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274201"
---
# <a name="how-to-run-the-completed-project"></a>Como executar o projeto concluído

## <a name="prerequisites"></a>Pré-requisitos

Para executar o projeto concluído nessa pasta, você precisa do seguinte:

- [Node.js](https://nodejs.org) e [o Yarn](https://yarnpkg.com/) instalados em sua máquina de desenvolvimento. (**Observação:** Este tutorial foi escrito com o Node versão 14.15.0 e o Yarn versão 1.22.0. As etapas neste guia podem funcionar com outras versões, mas que não foram testadas.)
- Uma conta pessoal da Microsoft com uma caixa de correio Outlook.com uma conta de trabalho ou de estudante da Microsoft.

Se você não tiver uma conta da Microsoft, há algumas opções para obter uma conta gratuita:

- Você pode [se inscrever para uma nova conta pessoal da Microsoft.](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)
- Você pode se inscrever no Programa para Desenvolvedores do [Office 365](https://developer.microsoft.com/office/dev-program) para obter uma assinatura gratuita do Office 365.

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a>Registrar um aplicativo Web com o centro de administração do Azure Active Directory

1. Abra um navegador e navegue até o [centro de administração do Azure Active Directory](https://aad.portal.azure.com). Faça logon usando uma **conta pessoal** (também conhecida como Conta da Microsoft) ou **Conta Corporativa ou de Estudante**.

1. Selecione **Azure Active Directory** na navegação esquerda e selecione **Registros de aplicativos** em **Gerenciar**.

    ![Uma captura de tela dos registros do aplicativo ](/tutorial/images/app-registrations.png)

1. Selecione **Novo registro**. Na página **Registrar um aplicativo**, defina os valores da seguinte forma.

    - Defina **Nome** para `Office Add-in Graph Tutorial`.
    - Defina **Tipos de conta com suporte** para **Contas em qualquer diretório organizacional e contas pessoais da Microsoft**.
    - Em **URI de Redirecionamento**, defina o primeiro menu suspenso para `Single-page application (SPA)` e defina o valor como `https://localhost:3000/consent.html`.

    ![Uma captura de tela da página Registrar um aplicativo](/tutorial/images/register-an-app.png)

1. Selecione **Registrar**. Na página do Tutorial do Graph do Complemento do Office, copie o valor da ID do Aplicativo **(cliente)** e **salve-o,** você precisará dele na próxima etapa.

    ![Uma captura de tela da ID do aplicativo do novo registro de aplicativo](/tutorial/images/application-id.png)

1. Selecione **Certificados e segredos** sob **Gerenciar**. Selecione o botão **Novo segredo do cliente**. Insira um valor em **Descrição** e selecione uma das opções para **Expirar** e selecione **Adicionar**.

1. Copie o valor secreto do cliente antes de sair desta página. Você precisará dele na próxima etapa.

    > [!IMPORTANT]
    > Este segredo do cliente nunca é mostrado novamente, portanto, copie-o agora.

1. Selecione **permissões de API em** **Gerenciar** e, em **seguida, selecione Adicionar uma permissão.**

1. Selecione **o Microsoft Graph** e, em **seguida, permissões delegadas.**

1. Selecione as seguintes permissões e, em seguida, **selecione Adicionar permissões.**

    - **Calendars.ReadWrite** - isso permitirá que o aplicativo leia e escreva no calendário do usuário.
    - **MailboxSettings.Read** - isso permitirá que o aplicativo receba o fuso horário do usuário nas configurações da caixa de correio.

    ![Uma captura de tela das permissões configuradas](/tutorial/images/configured-permissions.png)

## <a name="configure-office-add-in-single-sign-on"></a>Configurar o single sign-on do Office Add-in

Atualize o registro do aplicativo para dar suporte ao [SSO (single sign-on) do Complemento](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins)do Office.

1. Selecione **Expor uma API.** Nos **Escopos definidos por esta seção da API,** selecione **Adicionar um escopo.** Quando solicitado a definir um **URI da ID** do Aplicativo, de definida o valor como `api://localhost:3000/YOUR_APP_ID_HERE` , `YOUR_APP_ID_HERE` substituindo pela ID do aplicativo. Escolha **Salvar e continuar.**

1. Preencha os campos da seguinte forma e selecione **Adicionar escopo.**

    - **Nome do escopo:**`access_as_user`
    - **Quem pode consentir?: Administradores e usuários**
    - **Nome de exibição do consentimento do administrador:**`Access the app as the user`
    - **Descrição do consentimento do administrador:**`Allows Office Add-ins to call the app's web APIs as the current user.`
    - **Nome de exibição do consentimento do usuário:**`Access the app as you`
    - **Descrição do consentimento do usuário:**`Allows Office Add-ins to call the app's web APIs as you.`
    - **Estado: Habilitado**

    ![Uma captura de tela do formulário Adicionar um escopo](/tutorial/images/add-scope.png)

1. Na seção **Aplicativos cliente autorizados,** selecione **Adicionar um aplicativo cliente**. Insira uma ID de cliente na lista a seguir, habilita o escopo em **Escopos autorizados** e selecione **Adicionar aplicativo.** Repita esse processo para cada uma das IDs de cliente na lista.

    - `d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)
    - `ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)
    - `57fb890c-0dab-4253-a5e0-7188c88b2bb4`(Office na Web)
    - `08e18876-6177-487e-b8b5-cf950c1e598c`(Office na Web)

## <a name="install-development-certificates"></a>Instalar certificados de desenvolvimento

1. Execute o seguinte comando para gerar e instalar certificados de desenvolvimento para o seu complemento.

    ```Shell
    npx office-addin-dev-certs install
    ```

    Se for solicitado a confirmar, confirme as ações. Depois que o comando é concluído, você verá uma saída semelhante à seguinte.

    ```Shell
    You now have trusted access to https://localhost.
    Certificate: <path>\localhost.crt
    Key: <path>\localhost.key
    ```

1. Copie os caminhos para localhost.crt e localhost.key, você precisará deles na próxima etapa.

## <a name="update-the-manifest"></a>Atualizar o manifesto

1. Abra o **manifest.xml** arquivo e faça as seguintes alterações.
    1. Substitua `NEW_GUID_HERE` por um novo GUID, como `b4fa03b8-1eb6-4e8b-a380-e0476be9e019` .
    1. Substitua todas as instâncias `YOUR_APP_ID_HERE` pela ID do aplicativo do registro do aplicativo.

## <a name="configure-the-sample"></a>Configurar o exemplo

1. Renomeie o `example.env` arquivo para `.env` .
1. Edite `.env` o arquivo e faça as seguintes alterações.
    1. Substitua `YOUR_APP_ID_HERE` pela **ID do Aplicativo que** você recebeu do Portal de Registro de Aplicativos.
    1. Substitua `YOUR_CLIENT_SECRET_HERE` pelo segredo do cliente que você recebeu do Portal de Registro de Aplicativos.
    1. Substitua `PATH_TO_LOCALHOST.CRT` pelo caminho para o arquivo localhost.crt a partir da saída do `npx office-addin-dev-certs install` comando.
    1. Substitua `PATH_TO_LOCALHOST.KEY` pelo caminho para o arquivo localhost.key da saída do `npx office-addin-dev-certs install` comando.

1. Renomeie `config.example.js` o arquivo para `config.js` .
1. Edite `config.js` o arquivo e faça as seguintes alterações.
    1. Substitua `YOUR_APP_ID_HERE` pela **ID do Aplicativo que** você recebeu do Portal de Registro de Aplicativos.
1. Em sua CLI (interface de linha de comando), navegue até esse diretório e execute o seguinte comando para instalar os requisitos.

    ```Shell
    yarn install
    ```

## <a name="run-the-sample"></a>Executar o exemplo

1. Execute o seguinte comando em sua CLI para iniciar o aplicativo.

    ```Shell
    yarn start
    ```

1. No navegador, vá para o [Office.com](https://www.office.com/) e entre. Selecione **Criar** na barra de ferramentas à esquerda e selecione **Planilha.**

    ![Uma captura de tela do menu Criar no Office.com](/tutorial/images/office-select-excel.png)

1. Selecione a **guia** Inserir e, em **seguida, selecione Os Complementos do Office.**

1. Selecione **Carregar Meu Complemento e,** em seguida, **Procurar.** Carregue seu **manifest.xml** arquivo.

1. Selecione o **botão Importar Calendário** na guia **Página** Início para abrir o taskpane.

    ![Uma captura de tela do botão Importar Calendário na guia Página Inicial](/tutorial/images/get-started.png)
