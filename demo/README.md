---
ms.openlocfilehash: fed56663591ac36e4defcae3a8d0a222f86e3026
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274201"
---
# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="e200e-101">Como executar o projeto concluído</span><span class="sxs-lookup"><span data-stu-id="e200e-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e200e-102">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e200e-102">Prerequisites</span></span>

<span data-ttu-id="e200e-103">Para executar o projeto concluído nessa pasta, você precisa do seguinte:</span><span class="sxs-lookup"><span data-stu-id="e200e-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="e200e-104">[Node.js](https://nodejs.org) e [o Yarn](https://yarnpkg.com/) instalados em sua máquina de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="e200e-104">[Node.js](https://nodejs.org) and [Yarn](https://yarnpkg.com/) installed on your development machine.</span></span> <span data-ttu-id="e200e-105">(**Observação:** Este tutorial foi escrito com o Node versão 14.15.0 e o Yarn versão 1.22.0.</span><span class="sxs-lookup"><span data-stu-id="e200e-105">(**Note:** This tutorial was written with Node version 14.15.0 and Yarn version 1.22.0.</span></span> <span data-ttu-id="e200e-106">As etapas neste guia podem funcionar com outras versões, mas que não foram testadas.)</span><span class="sxs-lookup"><span data-stu-id="e200e-106">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="e200e-107">Uma conta pessoal da Microsoft com uma caixa de correio Outlook.com uma conta de trabalho ou de estudante da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e200e-107">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="e200e-108">Se você não tiver uma conta da Microsoft, há algumas opções para obter uma conta gratuita:</span><span class="sxs-lookup"><span data-stu-id="e200e-108">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="e200e-109">Você pode [se inscrever para uma nova conta pessoal da Microsoft.](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)</span><span class="sxs-lookup"><span data-stu-id="e200e-109">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="e200e-110">Você pode se inscrever no Programa para Desenvolvedores do [Office 365](https://developer.microsoft.com/office/dev-program) para obter uma assinatura gratuita do Office 365.</span><span class="sxs-lookup"><span data-stu-id="e200e-110">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="e200e-111">Registrar um aplicativo Web com o centro de administração do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e200e-111">Register a web application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="e200e-112">Abra um navegador e navegue até o [centro de administração do Azure Active Directory](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e200e-112">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="e200e-113">Faça logon usando uma **conta pessoal** (também conhecida como Conta da Microsoft) ou **Conta Corporativa ou de Estudante**.</span><span class="sxs-lookup"><span data-stu-id="e200e-113">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="e200e-114">Selecione **Azure Active Directory** na navegação esquerda e selecione **Registros de aplicativos** em **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="e200e-114">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="e200e-115">Uma captura de tela dos registros do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e200e-115">A screenshot of the App registrations</span></span> ](/tutorial/images/app-registrations.png)

1. <span data-ttu-id="e200e-116">Selecione **Novo registro**.</span><span class="sxs-lookup"><span data-stu-id="e200e-116">Select **New registration**.</span></span> <span data-ttu-id="e200e-117">Na página **Registrar um aplicativo**, defina os valores da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="e200e-117">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="e200e-118">Defina **Nome** para `Office Add-in Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="e200e-118">Set **Name** to `Office Add-in Graph Tutorial`.</span></span>
    - <span data-ttu-id="e200e-119">Defina **Tipos de conta com suporte** para **Contas em qualquer diretório organizacional e contas pessoais da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="e200e-119">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="e200e-120">Em **URI de Redirecionamento**, defina o primeiro menu suspenso para `Single-page application (SPA)` e defina o valor como `https://localhost:3000/consent.html`.</span><span class="sxs-lookup"><span data-stu-id="e200e-120">Under **Redirect URI**, set the first drop-down to `Single-page application (SPA)` and set the value to `https://localhost:3000/consent.html`.</span></span>

    ![Uma captura de tela da página Registrar um aplicativo](/tutorial/images/register-an-app.png)

1. <span data-ttu-id="e200e-122">Selecione **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="e200e-122">Select **Register**.</span></span> <span data-ttu-id="e200e-123">Na página do Tutorial do Graph do Complemento do Office, copie o valor da ID do Aplicativo **(cliente)** e **salve-o,** você precisará dele na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="e200e-123">On the **Office Add-in Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Uma captura de tela da ID do aplicativo do novo registro de aplicativo](/tutorial/images/application-id.png)

1. <span data-ttu-id="e200e-125">Selecione **Certificados e segredos** sob **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="e200e-125">Select **Certificates & secrets** under **Manage**.</span></span> <span data-ttu-id="e200e-126">Selecione o botão **Novo segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="e200e-126">Select the **New client secret** button.</span></span> <span data-ttu-id="e200e-127">Insira um valor em **Descrição** e selecione uma das opções para **Expirar** e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e200e-127">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

1. <span data-ttu-id="e200e-128">Copie o valor secreto do cliente antes de sair desta página.</span><span class="sxs-lookup"><span data-stu-id="e200e-128">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="e200e-129">Você precisará dele na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="e200e-129">You will need it in the next step.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e200e-130">Este segredo do cliente nunca é mostrado novamente, portanto, copie-o agora.</span><span class="sxs-lookup"><span data-stu-id="e200e-130">This client secret is never shown again, so make sure you copy it now.</span></span>

1. <span data-ttu-id="e200e-131">Selecione **permissões de API em** **Gerenciar** e, em **seguida, selecione Adicionar uma permissão.**</span><span class="sxs-lookup"><span data-stu-id="e200e-131">Select **API permissions** under **Manage**, then select **Add a permission**.</span></span>

1. <span data-ttu-id="e200e-132">Selecione **o Microsoft Graph** e, em **seguida, permissões delegadas.**</span><span class="sxs-lookup"><span data-stu-id="e200e-132">Select **Microsoft Graph**, then **Delegated permissions**.</span></span>

1. <span data-ttu-id="e200e-133">Selecione as seguintes permissões e, em seguida, **selecione Adicionar permissões.**</span><span class="sxs-lookup"><span data-stu-id="e200e-133">Select the following permissions, then select **Add permissions**.</span></span>

    - <span data-ttu-id="e200e-134">**Calendars.ReadWrite** - isso permitirá que o aplicativo leia e escreva no calendário do usuário.</span><span class="sxs-lookup"><span data-stu-id="e200e-134">**Calendars.ReadWrite** - this will allow the app to read and write to the user's calendar.</span></span>
    - <span data-ttu-id="e200e-135">**MailboxSettings.Read** - isso permitirá que o aplicativo receba o fuso horário do usuário nas configurações da caixa de correio.</span><span class="sxs-lookup"><span data-stu-id="e200e-135">**MailboxSettings.Read** - this will allow the app to get the user's time zone from their mailbox settings.</span></span>

    ![Uma captura de tela das permissões configuradas](/tutorial/images/configured-permissions.png)

## <a name="configure-office-add-in-single-sign-on"></a><span data-ttu-id="e200e-137">Configurar o single sign-on do Office Add-in</span><span class="sxs-lookup"><span data-stu-id="e200e-137">Configure Office Add-in single sign-on</span></span>

<span data-ttu-id="e200e-138">Atualize o registro do aplicativo para dar suporte ao [SSO (single sign-on) do Complemento](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins)do Office.</span><span class="sxs-lookup"><span data-stu-id="e200e-138">Update the app registration to support [Office Add-in single sign-on (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins).</span></span>

1. <span data-ttu-id="e200e-139">Selecione **Expor uma API.**</span><span class="sxs-lookup"><span data-stu-id="e200e-139">Select **Expose an API**.</span></span> <span data-ttu-id="e200e-140">Nos **Escopos definidos por esta seção da API,** selecione **Adicionar um escopo.**</span><span class="sxs-lookup"><span data-stu-id="e200e-140">In the **Scopes defined by this API** section, select **Add a scope**.</span></span> <span data-ttu-id="e200e-141">Quando solicitado a definir um **URI da ID** do Aplicativo, de definida o valor como `api://localhost:3000/YOUR_APP_ID_HERE` , `YOUR_APP_ID_HERE` substituindo pela ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e200e-141">When prompted to set an **Application ID URI**, set the value to `api://localhost:3000/YOUR_APP_ID_HERE`, replacing `YOUR_APP_ID_HERE` with the application ID.</span></span> <span data-ttu-id="e200e-142">Escolha **Salvar e continuar.**</span><span class="sxs-lookup"><span data-stu-id="e200e-142">Choose **Save and continue**.</span></span>

1. <span data-ttu-id="e200e-143">Preencha os campos da seguinte forma e selecione **Adicionar escopo.**</span><span class="sxs-lookup"><span data-stu-id="e200e-143">Fill in the fields as follows and select **Add scope**.</span></span>

    - <span data-ttu-id="e200e-144">**Nome do escopo:**`access_as_user`</span><span class="sxs-lookup"><span data-stu-id="e200e-144">**Scope name:** `access_as_user`</span></span>
    - <span data-ttu-id="e200e-145">**Quem pode consentir?: Administradores e usuários**</span><span class="sxs-lookup"><span data-stu-id="e200e-145">**Who can consent?: Admins and users**</span></span>
    - <span data-ttu-id="e200e-146">**Nome de exibição do consentimento do administrador:**`Access the app as the user`</span><span class="sxs-lookup"><span data-stu-id="e200e-146">**Admin consent display name:** `Access the app as the user`</span></span>
    - <span data-ttu-id="e200e-147">**Descrição do consentimento do administrador:**`Allows Office Add-ins to call the app's web APIs as the current user.`</span><span class="sxs-lookup"><span data-stu-id="e200e-147">**Admin consent description:** `Allows Office Add-ins to call the app's web APIs as the current user.`</span></span>
    - <span data-ttu-id="e200e-148">**Nome de exibição do consentimento do usuário:**`Access the app as you`</span><span class="sxs-lookup"><span data-stu-id="e200e-148">**User consent display name:** `Access the app as you`</span></span>
    - <span data-ttu-id="e200e-149">**Descrição do consentimento do usuário:**`Allows Office Add-ins to call the app's web APIs as you.`</span><span class="sxs-lookup"><span data-stu-id="e200e-149">**User consent description:** `Allows Office Add-ins to call the app's web APIs as you.`</span></span>
    - <span data-ttu-id="e200e-150">**Estado: Habilitado**</span><span class="sxs-lookup"><span data-stu-id="e200e-150">**State: Enabled**</span></span>

    ![Uma captura de tela do formulário Adicionar um escopo](/tutorial/images/add-scope.png)

1. <span data-ttu-id="e200e-152">Na seção **Aplicativos cliente autorizados,** selecione **Adicionar um aplicativo cliente**.</span><span class="sxs-lookup"><span data-stu-id="e200e-152">In the **Authorized client applications** section, select **Add a client application**.</span></span> <span data-ttu-id="e200e-153">Insira uma ID de cliente na lista a seguir, habilita o escopo em **Escopos autorizados** e selecione **Adicionar aplicativo.**</span><span class="sxs-lookup"><span data-stu-id="e200e-153">Enter a client ID from the following list, enable the scope under **Authorized scopes**, and select **Add application**.</span></span> <span data-ttu-id="e200e-154">Repita esse processo para cada uma das IDs de cliente na lista.</span><span class="sxs-lookup"><span data-stu-id="e200e-154">Repeat this process for each of the client IDs in the list.</span></span>

    - <span data-ttu-id="e200e-155">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="e200e-155">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span></span>
    - <span data-ttu-id="e200e-156">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="e200e-156">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span></span>
    - <span data-ttu-id="e200e-157">`57fb890c-0dab-4253-a5e0-7188c88b2bb4`(Office na Web)</span><span class="sxs-lookup"><span data-stu-id="e200e-157">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office on the web)</span></span>
    - <span data-ttu-id="e200e-158">`08e18876-6177-487e-b8b5-cf950c1e598c`(Office na Web)</span><span class="sxs-lookup"><span data-stu-id="e200e-158">`08e18876-6177-487e-b8b5-cf950c1e598c` (Office on the web)</span></span>

## <a name="install-development-certificates"></a><span data-ttu-id="e200e-159">Instalar certificados de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="e200e-159">Install development certificates</span></span>

1. <span data-ttu-id="e200e-160">Execute o seguinte comando para gerar e instalar certificados de desenvolvimento para o seu complemento.</span><span class="sxs-lookup"><span data-stu-id="e200e-160">Run the following command to generate and install development certificates for your add-in.</span></span>

    ```Shell
    npx office-addin-dev-certs install
    ```

    <span data-ttu-id="e200e-161">Se for solicitado a confirmar, confirme as ações.</span><span class="sxs-lookup"><span data-stu-id="e200e-161">If prompted for confirmation, confirm the actions.</span></span> <span data-ttu-id="e200e-162">Depois que o comando é concluído, você verá uma saída semelhante à seguinte.</span><span class="sxs-lookup"><span data-stu-id="e200e-162">Once the command completes, you will see output similar to the following.</span></span>

    ```Shell
    You now have trusted access to https://localhost.
    Certificate: <path>\localhost.crt
    Key: <path>\localhost.key
    ```

1. <span data-ttu-id="e200e-163">Copie os caminhos para localhost.crt e localhost.key, você precisará deles na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="e200e-163">Copy the paths to localhost.crt and localhost.key, you'll need them in the next step.</span></span>

## <a name="update-the-manifest"></a><span data-ttu-id="e200e-164">Atualizar o manifesto</span><span class="sxs-lookup"><span data-stu-id="e200e-164">Update the manifest</span></span>

1. <span data-ttu-id="e200e-165">Abra o **manifest.xml** arquivo e faça as seguintes alterações.</span><span class="sxs-lookup"><span data-stu-id="e200e-165">Open the **manifest.xml** file and make the following changes.</span></span>
    1. <span data-ttu-id="e200e-166">Substitua `NEW_GUID_HERE` por um novo GUID, como `b4fa03b8-1eb6-4e8b-a380-e0476be9e019` .</span><span class="sxs-lookup"><span data-stu-id="e200e-166">Replace `NEW_GUID_HERE` with a new GUID, like `b4fa03b8-1eb6-4e8b-a380-e0476be9e019`.</span></span>
    1. <span data-ttu-id="e200e-167">Substitua todas as instâncias `YOUR_APP_ID_HERE` pela ID do aplicativo do registro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e200e-167">Replace all instances of `YOUR_APP_ID_HERE` with the application ID from your app registration.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="e200e-168">Configurar o exemplo</span><span class="sxs-lookup"><span data-stu-id="e200e-168">Configure the sample</span></span>

1. <span data-ttu-id="e200e-169">Renomeie o `example.env` arquivo para `.env` .</span><span class="sxs-lookup"><span data-stu-id="e200e-169">Rename the `example.env` file to `.env`.</span></span>
1. <span data-ttu-id="e200e-170">Edite `.env` o arquivo e faça as seguintes alterações.</span><span class="sxs-lookup"><span data-stu-id="e200e-170">Edit the `.env` file and make the following changes.</span></span>
    1. <span data-ttu-id="e200e-171">Substitua `YOUR_APP_ID_HERE` pela **ID do Aplicativo que** você recebeu do Portal de Registro de Aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e200e-171">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>
    1. <span data-ttu-id="e200e-172">Substitua `YOUR_CLIENT_SECRET_HERE` pelo segredo do cliente que você recebeu do Portal de Registro de Aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e200e-172">Replace `YOUR_CLIENT_SECRET_HERE` with the client secret you got from the App Registration Portal.</span></span>
    1. <span data-ttu-id="e200e-173">Substitua `PATH_TO_LOCALHOST.CRT` pelo caminho para o arquivo localhost.crt a partir da saída do `npx office-addin-dev-certs install` comando.</span><span class="sxs-lookup"><span data-stu-id="e200e-173">Replace `PATH_TO_LOCALHOST.CRT` with the path to your localhost.crt file from the output of the `npx office-addin-dev-certs install` command.</span></span>
    1. <span data-ttu-id="e200e-174">Substitua `PATH_TO_LOCALHOST.KEY` pelo caminho para o arquivo localhost.key da saída do `npx office-addin-dev-certs install` comando.</span><span class="sxs-lookup"><span data-stu-id="e200e-174">Replace `PATH_TO_LOCALHOST.KEY` with the path to your localhost.key file from the output of the `npx office-addin-dev-certs install` command.</span></span>

1. <span data-ttu-id="e200e-175">Renomeie `config.example.js` o arquivo para `config.js` .</span><span class="sxs-lookup"><span data-stu-id="e200e-175">Rename the `config.example.js` file to `config.js`.</span></span>
1. <span data-ttu-id="e200e-176">Edite `config.js` o arquivo e faça as seguintes alterações.</span><span class="sxs-lookup"><span data-stu-id="e200e-176">Edit the `config.js` file and make the following changes.</span></span>
    1. <span data-ttu-id="e200e-177">Substitua `YOUR_APP_ID_HERE` pela **ID do Aplicativo que** você recebeu do Portal de Registro de Aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e200e-177">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>
1. <span data-ttu-id="e200e-178">Em sua CLI (interface de linha de comando), navegue até esse diretório e execute o seguinte comando para instalar os requisitos.</span><span class="sxs-lookup"><span data-stu-id="e200e-178">In your command-line interface (CLI), navigate to this directory and run the following command to install requirements.</span></span>

    ```Shell
    yarn install
    ```

## <a name="run-the-sample"></a><span data-ttu-id="e200e-179">Executar o exemplo</span><span class="sxs-lookup"><span data-stu-id="e200e-179">Run the sample</span></span>

1. <span data-ttu-id="e200e-180">Execute o seguinte comando em sua CLI para iniciar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e200e-180">Run the following command in your CLI to start the application.</span></span>

    ```Shell
    yarn start
    ```

1. <span data-ttu-id="e200e-181">No navegador, vá para o [Office.com](https://www.office.com/) e entre.</span><span class="sxs-lookup"><span data-stu-id="e200e-181">In your browser, go to [Office.com](https://www.office.com/) and sign in.</span></span> <span data-ttu-id="e200e-182">Selecione **Criar** na barra de ferramentas à esquerda e selecione **Planilha.**</span><span class="sxs-lookup"><span data-stu-id="e200e-182">Select **Create** in the left-hand toolbar, then select **Spreadsheet**.</span></span>

    ![Uma captura de tela do menu Criar no Office.com](/tutorial/images/office-select-excel.png)

1. <span data-ttu-id="e200e-184">Selecione a **guia** Inserir e, em **seguida, selecione Os Complementos do Office.**</span><span class="sxs-lookup"><span data-stu-id="e200e-184">Select the **Insert** tab, then select **Office Add-ins**.</span></span>

1. <span data-ttu-id="e200e-185">Selecione **Carregar Meu Complemento e,** em seguida, **Procurar.**</span><span class="sxs-lookup"><span data-stu-id="e200e-185">Select **Upload My Add-in**, then select **Browse**.</span></span> <span data-ttu-id="e200e-186">Carregue seu **manifest.xml** arquivo.</span><span class="sxs-lookup"><span data-stu-id="e200e-186">Upload your **manifest.xml** file.</span></span>

1. <span data-ttu-id="e200e-187">Selecione o **botão Importar Calendário** na guia **Página** Início para abrir o taskpane.</span><span class="sxs-lookup"><span data-stu-id="e200e-187">Select the **Import Calendar** button on the **Home** tab to open the taskpane.</span></span>

    ![Uma captura de tela do botão Importar Calendário na guia Página Inicial](/tutorial/images/get-started.png)
