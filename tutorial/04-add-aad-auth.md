---
ms.openlocfilehash: 69d77c19cb2c589086df2b4bf19eeadf41aad58a
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274208"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="d7315-101">Neste exercício, você habilita o [SSO (single sign-on)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins) do Complemento do Office no complemento e estende a API Web para dar suporte ao fluxo em nome [de.](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)</span><span class="sxs-lookup"><span data-stu-id="d7315-101">In this exercise you will enable [Office Add-in single sign-on (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins) in the add-in, and extend the web API to support [on-behalf-of flow](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow).</span></span> <span data-ttu-id="d7315-102">Isso é necessário para obter o token de acesso OAuth necessário para chamar o Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="d7315-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span>

## <a name="overview"></a><span data-ttu-id="d7315-103">Visão Geral</span><span class="sxs-lookup"><span data-stu-id="d7315-103">Overview</span></span>

<span data-ttu-id="d7315-104">O SSO do Complemento do Office fornece um token de acesso, mas esse token só permite que o complemento chame sua própria API Web.</span><span class="sxs-lookup"><span data-stu-id="d7315-104">Office Add-in SSO provides an access token, but that token is only enables the add-in to call it's own web API.</span></span> <span data-ttu-id="d7315-105">Ele não habilita o acesso direto ao Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="d7315-105">It does not enable direct access to the Microsoft Graph.</span></span> <span data-ttu-id="d7315-106">O processo funciona da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="d7315-106">The process works as follows.</span></span>

1. <span data-ttu-id="d7315-107">O complemento obtém um token chamando [getAccessToken](https://docs.microsoft.com/javascript/api/office-runtime/officeruntime.auth?view=common-js#getaccesstoken-options-).</span><span class="sxs-lookup"><span data-stu-id="d7315-107">The add-in gets a token by calling [getAccessToken](https://docs.microsoft.com/javascript/api/office-runtime/officeruntime.auth?view=common-js#getaccesstoken-options-).</span></span> <span data-ttu-id="d7315-108">A audiência desse token (a declaração) é a ID do aplicativo do `aud` registro de aplicativo do complemento.</span><span class="sxs-lookup"><span data-stu-id="d7315-108">This token's audience (the `aud` claim) is the application ID of the add-in's app registration.</span></span>
1. <span data-ttu-id="d7315-109">O complemento envia esse token no título `Authorization` quando faz uma chamada para a API da Web.</span><span class="sxs-lookup"><span data-stu-id="d7315-109">The add-in sends this token in the `Authorization` header when it makes a call to the web API.</span></span>
1. <span data-ttu-id="d7315-110">A API Web valida o token e usa o fluxo em nome de para trocar esse token por um token do Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="d7315-110">The web API validates the token, then uses the on-behalf-of flow to exchange this token for a Microsoft Graph token.</span></span> <span data-ttu-id="d7315-111">O público-alvo desse novo token é `https://graph.microsoft.com` .</span><span class="sxs-lookup"><span data-stu-id="d7315-111">This new token's audience is `https://graph.microsoft.com`.</span></span>
1. <span data-ttu-id="d7315-112">A API Web usa o novo token para fazer chamadas para o Microsoft Graph e retorna os resultados para o complemento.</span><span class="sxs-lookup"><span data-stu-id="d7315-112">The web API uses the new token to make calls to the Microsoft Graph, and returns the results back to the add-in.</span></span>

## <a name="configure-the-solution"></a><span data-ttu-id="d7315-113">Configurar a solução</span><span class="sxs-lookup"><span data-stu-id="d7315-113">Configure the solution</span></span>

1. <span data-ttu-id="d7315-114">Abra **./.env e** atualize a ID do aplicativo e o segredo do cliente `AZURE_APP_ID` do registro do `AZURE_CLIENT_SECRET` aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d7315-114">Open **./.env** and update the `AZURE_APP_ID` and `AZURE_CLIENT_SECRET` with the application ID and client secret from your app registration.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d7315-115">Se você estiver usando o controle de código-fonte, como git, agora seria um bom momento para excluir o arquivo **.env** do controle de código-fonte para evitar o vazamento inadvertida da ID do aplicativo e do segredo do cliente.</span><span class="sxs-lookup"><span data-stu-id="d7315-115">If you're using source control such as git, now would be a good time to exclude the **.env** file from source control to avoid inadvertently leaking your app ID and client secret.</span></span>

1. <span data-ttu-id="d7315-116">Abra **./manifest/manifest.xml** e substitua todas as instâncias `YOUR_APP_ID_HERE` pela ID do aplicativo do registro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d7315-116">Open **./manifest/manifest.xml** and replace all instances of `YOUR_APP_ID_HERE` with the application ID from your app registration.</span></span>

1. <span data-ttu-id="d7315-117">Crie um novo arquivo no diretório **./src/addin** chamado **config.js** e adicione o código a seguir, substituindo pela ID do aplicativo do `YOUR_APP_ID_HERE` registro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d7315-117">Create a new file in the **./src/addin** directory named **config.js** and add the following code, replacing `YOUR_APP_ID_HERE` with the application ID from your app registration.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/config.example.js":::

## <a name="implement-sign-in"></a><span data-ttu-id="d7315-118">Implementar a login</span><span class="sxs-lookup"><span data-stu-id="d7315-118">Implement sign-in</span></span>

1. <span data-ttu-id="d7315-119">Abra **./src/api/auth.ts** e adicione as instruções a seguir `import` na parte superior do arquivo.</span><span class="sxs-lookup"><span data-stu-id="d7315-119">Open **./src/api/auth.ts** and add the following `import` statements at the top of the file.</span></span>

    ```typescript
    import jwt, { SigningKeyCallback, JwtHeader } from 'jsonwebtoken';
    import jwksClient from 'jwks-rsa';
    import * as msal from '@azure/msal-node';
    ```

1. <span data-ttu-id="d7315-120">Adicione o código a seguir após as `import` instruções.</span><span class="sxs-lookup"><span data-stu-id="d7315-120">Add the following code after the `import` statements.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/api/auth.ts" id="TokenExchangeSnippet":::

    <span data-ttu-id="d7315-121">Esse código inicializa um cliente [confidencial da MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/initialize-confidential-client-application.md)e exporta uma função para obter um token do Graph do token enviado pelo complemento.</span><span class="sxs-lookup"><span data-stu-id="d7315-121">This code [initializes an MSAL confidential client](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/initialize-confidential-client-application.md), and exports a function to get a Graph token from the token sent by the add-in.</span></span>

1. <span data-ttu-id="d7315-122">Adicione o seguinte código antes da `export default authRouter;` linha.</span><span class="sxs-lookup"><span data-stu-id="d7315-122">Add the following code before the `export default authRouter;` line.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/api/auth.ts" id="GetAuthStatusSnippet":::

    <span data-ttu-id="d7315-123">Esse código implementa uma API ( ) que verifica se o token do complemento pode ser trocado silenciosamente `GET /auth/status` por um token do Graph.</span><span class="sxs-lookup"><span data-stu-id="d7315-123">This code implements an API (`GET /auth/status`) that checks if the add-in token can be silently exchanged for a Graph token.</span></span> <span data-ttu-id="d7315-124">O add-in usará essa API para determinar se ele precisa apresentar um logon interativo para o usuário.</span><span class="sxs-lookup"><span data-stu-id="d7315-124">The add-in will use this API to determine if it needs to present an interactive login to the user.</span></span>

1. <span data-ttu-id="d7315-125">Abra **./src/addin/taskpane.js** e adicione o seguinte código ao arquivo.</span><span class="sxs-lookup"><span data-stu-id="d7315-125">Open **./src/addin/taskpane.js** and add the following code to the file.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="AuthUiSnippet":::

    <span data-ttu-id="d7315-126">Este código adiciona funções para atualizar a interface do usuário e usar a API da Caixa de Diálogo do [Office](https://docs.microsoft.com/office/dev/add-ins/develop/dialog-api-in-office-add-ins) para iniciar um fluxo de autenticação interativa.</span><span class="sxs-lookup"><span data-stu-id="d7315-126">This code adds functions to update the UI, and to use the [Office Dialog API](https://docs.microsoft.com/office/dev/add-ins/develop/dialog-api-in-office-add-ins) to initiate an interactive authentication flow.</span></span>

1. <span data-ttu-id="d7315-127">Adicione a função a seguir para implementar uma interface do usuário principal temporária.</span><span class="sxs-lookup"><span data-stu-id="d7315-127">Add the following function to implement a temporary main UI.</span></span>

    ```javascript
    function showMainUi() {
      $('.container').empty();
      $('<p/>', {
        class: 'ms-fontSize-24 ms-fontWeight-bold',
        text: 'Authenticated!'
      }).appendTo('.container');
    }
    ```

1. <span data-ttu-id="d7315-128">Substitua a chamada `Office.onReady` existente pelo seguinte.</span><span class="sxs-lookup"><span data-stu-id="d7315-128">Replace the existing `Office.onReady` call with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="OfficeReadySnippet":::

    <span data-ttu-id="d7315-129">Considere o que esse código faz.</span><span class="sxs-lookup"><span data-stu-id="d7315-129">Consider what this code does.</span></span>

    - <span data-ttu-id="d7315-130">Quando o painel de tarefas é carregado pela primeira vez, ele chama para obter um token com escopo para `getAccessToken` a API Web do complemento.</span><span class="sxs-lookup"><span data-stu-id="d7315-130">When the task pane first loads, it calls `getAccessToken` to get a token scoped for the add-in's web API.</span></span>
    - <span data-ttu-id="d7315-131">Ele usa esse token para chamar a API para verificar se o usuário `/auth/status` deu consentimento para os escopos do Microsoft Graph ainda.</span><span class="sxs-lookup"><span data-stu-id="d7315-131">It uses that token to call the `/auth/status` API to check if the user has given consent to the Microsoft Graph scopes yet.</span></span>
        - <span data-ttu-id="d7315-132">Se o usuário não tiver consentido, ele usará uma janela pop-up para obter o consentimento do usuário por meio de um logon interativo.</span><span class="sxs-lookup"><span data-stu-id="d7315-132">If the user has not consented, it uses a pop-up window to get the user's consent through an interactive login.</span></span>
        - <span data-ttu-id="d7315-133">Se o usuário tiver consentido, ele carregará a interface do usuário principal.</span><span class="sxs-lookup"><span data-stu-id="d7315-133">If the user has consented, it loads the main UI.</span></span>

### <a name="getting-user-consent"></a><span data-ttu-id="d7315-134">Obter consentimento do usuário</span><span class="sxs-lookup"><span data-stu-id="d7315-134">Getting user consent</span></span>

<span data-ttu-id="d7315-135">Mesmo que o complemento esteja usando o SSO, o usuário ainda precisa consentir com o complemento acessando seus dados por meio do Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="d7315-135">Even though the add-in is using SSO, the user still has to consent to the add-in accessing their data via Microsoft Graph.</span></span> <span data-ttu-id="d7315-136">Obter consentimento é um processo único.</span><span class="sxs-lookup"><span data-stu-id="d7315-136">Getting consent is a one-time process.</span></span> <span data-ttu-id="d7315-137">Depois que o usuário conceder consentimento, o token SSO poderá ser trocado por um token do Graph sem qualquer interação do usuário.</span><span class="sxs-lookup"><span data-stu-id="d7315-137">Once the user has granted consent, the SSO token can be exchanged for a Graph token without any user interaction.</span></span> <span data-ttu-id="d7315-138">Nesta seção, você implementará a experiência de consentimento no complemento usando [msal-browser.](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser)</span><span class="sxs-lookup"><span data-stu-id="d7315-138">In this section you'll implement the consent experience in the add-in using [msal-browser](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser).</span></span>

1. <span data-ttu-id="d7315-139">Crie um novo arquivo no **diretório ./src/addin** chamado **consent.js** e adicione o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="d7315-139">Create a new file in the **./src/addin** directory named **consent.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/consent.js" id="ConsentJsSnippet":::

    <span data-ttu-id="d7315-140">Esse código faz logon para o usuário, solicitando o conjunto de permissões do Microsoft Graph que estão configuradas no registro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d7315-140">This code does login for the user, requesting the set of Microsoft Graph permissions that are configured on the app registration.</span></span>

1. <span data-ttu-id="d7315-141">Crie um novo arquivo no **diretório ./src/addin** **chamadoconsent.html** e adicione o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="d7315-141">Create a new file in the **./src/addin** directory named **consent.html** and add the following code.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/addin/consent.html" id="ConsentHtmlSnippet":::

    <span data-ttu-id="d7315-142">Este código implementa uma página HTML básica para carregar o **consent.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="d7315-142">This code implements a basic HTML page to load the **consent.js** file.</span></span> <span data-ttu-id="d7315-143">Esta página será carregada em uma caixa de diálogo pop-up.</span><span class="sxs-lookup"><span data-stu-id="d7315-143">This page will be loaded in a pop-up dialog.</span></span>

1. <span data-ttu-id="d7315-144">Salve todas as suas alterações e reinicie o servidor.</span><span class="sxs-lookup"><span data-stu-id="d7315-144">Save all of your changes and restart the server.</span></span>

1. <span data-ttu-id="d7315-145">Carregue seu arquivo **manifest.xml** usando as mesmas etapas em [Side-load do complemento no Excel.](02-create-app.md#side-load-the-add-in-in-excel)</span><span class="sxs-lookup"><span data-stu-id="d7315-145">Re-upload your **manifest.xml** file using the same steps in [Side-load the add-in in Excel](02-create-app.md#side-load-the-add-in-in-excel).</span></span>

1. <span data-ttu-id="d7315-146">Selecione o **botão Importar Calendário** na guia **Página** Início para abrir o painel de tarefas.</span><span class="sxs-lookup"><span data-stu-id="d7315-146">Select the **Import Calendar** button on the **Home** tab to open the task pane.</span></span>

1. <span data-ttu-id="d7315-147">Selecione o **botão Dar permissão** no painel de tarefas para iniciar a caixa de diálogo de consentimento em uma janela pop-up.</span><span class="sxs-lookup"><span data-stu-id="d7315-147">Select the **Give permission** button in the task pane to launch the consent dialog in a pop-up window.</span></span> <span data-ttu-id="d7315-148">Entre e conceda consentimento.</span><span class="sxs-lookup"><span data-stu-id="d7315-148">Sign in and grant consent.</span></span>

1. <span data-ttu-id="d7315-149">O painel de tarefas é atualizado com um "Autenticado!"</span><span class="sxs-lookup"><span data-stu-id="d7315-149">The task pane updates with an "Authenticated!"</span></span> <span data-ttu-id="d7315-150">message.</span><span class="sxs-lookup"><span data-stu-id="d7315-150">message.</span></span> <span data-ttu-id="d7315-151">Você pode verificar os tokens da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="d7315-151">You can check the tokens as follows.</span></span>

    - <span data-ttu-id="d7315-152">Nas ferramentas de desenvolvedor do seu navegador, o token de API é mostrado no Console.</span><span class="sxs-lookup"><span data-stu-id="d7315-152">In your brower's developer tools, the API token is shown in the Console.</span></span>
    - <span data-ttu-id="d7315-153">Na CLI em que você está executando o servidor Node.js, o token do Graph é impresso.</span><span class="sxs-lookup"><span data-stu-id="d7315-153">In your CLI where you are running the Node.js server, the Graph token is printed.</span></span>

    <span data-ttu-id="d7315-154">Você pode comparar esses tokens em [https://jwt.ms](https://jwt.ms) .</span><span class="sxs-lookup"><span data-stu-id="d7315-154">You can compare these token at [https://jwt.ms](https://jwt.ms).</span></span> <span data-ttu-id="d7315-155">Observe que o público do token de API ( ) é definido como a ID do aplicativo do registro do seu aplicativo, e o escopo `aud` ( `scp` ) é `access_as_user` .</span><span class="sxs-lookup"><span data-stu-id="d7315-155">Notice that the API token's audience (`aud`) is set to the application ID of your app registration, and the scope (`scp`) is `access_as_user`.</span></span>
