---
ms.openlocfilehash: 89bc4baff47ae895c7c0dfd34a8f8d4d0da091f5
ms.sourcegitcommit: 8a65c826f6b229c287a782d784b6d9629aa5a3d0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/20/2021
ms.locfileid: "51899427"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="e81a8-101">Neste exercício, você criará um novo registro de aplicativo Web do Azure AD usando o Centro de administração do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e81a8-101">In this exercise, you will create a new Azure AD web application registration using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="e81a8-102">Abra um navegador e navegue até o [centro de administração do Azure Active Directory](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e81a8-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="e81a8-103">Faça logon usando uma **conta pessoal** (também conhecida como Conta da Microsoft) ou **Conta Corporativa ou de Estudante**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-103">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="e81a8-104">Selecione **Azure Active Directory** na navegação esquerda e selecione **Registros de aplicativos** em **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-104">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="e81a8-105">Uma captura de tela dos registros do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e81a8-105">A screenshot of the App registrations</span></span> ](images/app-registrations.png)

1. <span data-ttu-id="e81a8-106">Selecione **Novo registro**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-106">Select **New registration**.</span></span> <span data-ttu-id="e81a8-107">Na página **Registrar um aplicativo**, defina os valores da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="e81a8-107">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="e81a8-108">Defina **Nome** para `Office Add-in Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="e81a8-108">Set **Name** to `Office Add-in Graph Tutorial`.</span></span>
    - <span data-ttu-id="e81a8-109">Defina **Tipos de conta com suporte** para **Contas em qualquer diretório organizacional e contas pessoais da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-109">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="e81a8-110">Em **URI de Redirecionamento**, defina o primeiro menu suspenso para `Single-page application (SPA)` e defina o valor como `https://localhost:3000/consent.html`.</span><span class="sxs-lookup"><span data-stu-id="e81a8-110">Under **Redirect URI**, set the first drop-down to `Single-page application (SPA)` and set the value to `https://localhost:3000/consent.html`.</span></span>

    ![Captura de tela da página Registrar um aplicativo](images/register-an-app.png)

1. <span data-ttu-id="e81a8-112">Selecione **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-112">Select **Register**.</span></span> <span data-ttu-id="e81a8-113">Na página Tutorial do Gráfico de Complementos do **Office,** copie o valor da ID do Aplicativo **(cliente)** e salve-a, você precisará dele na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="e81a8-113">On the **Office Add-in Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Captura de tela da ID do aplicativo do novo registro do aplicativo](images/application-id.png)

1. <span data-ttu-id="e81a8-115">Selecione **Autenticação** em **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-115">Select **Authentication** under **Manage**.</span></span> <span data-ttu-id="e81a8-116">Localize **a seção Concessão Implícita** e habilita **tokens de Acesso** e **tokens de ID**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-116">Locate the **Implicit grant** section and enable **Access tokens** and **ID tokens**.</span></span> <span data-ttu-id="e81a8-117">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-117">Select **Save**.</span></span>

    ![Uma captura de tela da seção Concessão Implícita](./images/aad-implicit-grant.png)

1. <span data-ttu-id="e81a8-119">Selecione **Certificados e segredos** sob **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-119">Select **Certificates & secrets** under **Manage**.</span></span> <span data-ttu-id="e81a8-120">Selecione o botão **Novo segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-120">Select the **New client secret** button.</span></span> <span data-ttu-id="e81a8-121">Insira um valor em **Descrição** e selecione uma das opções para **Expira** em e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-121">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

1. <span data-ttu-id="e81a8-122">Copie o valor secreto do cliente antes de sair desta página.</span><span class="sxs-lookup"><span data-stu-id="e81a8-122">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="e81a8-123">Você precisará dele na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="e81a8-123">You will need it in the next step.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e81a8-124">Este segredo do cliente nunca é mostrado novamente, portanto, copie-o agora.</span><span class="sxs-lookup"><span data-stu-id="e81a8-124">This client secret is never shown again, so make sure you copy it now.</span></span>

1. <span data-ttu-id="e81a8-125">Selecione **permissões de API** em **Gerenciar**, em seguida, selecione Adicionar **uma permissão**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-125">Select **API permissions** under **Manage**, then select **Add a permission**.</span></span>

1. <span data-ttu-id="e81a8-126">Selecione **Microsoft Graph**, em **seguida, Permissões delegadas**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-126">Select **Microsoft Graph**, then **Delegated permissions**.</span></span>

1. <span data-ttu-id="e81a8-127">Selecione as seguintes permissões e selecione **Adicionar permissões**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-127">Select the following permissions, then select **Add permissions**.</span></span>

    - <span data-ttu-id="e81a8-128">**offline_access** - isso permitirá que o aplicativo atualize tokens de acesso quando eles expirarem.</span><span class="sxs-lookup"><span data-stu-id="e81a8-128">**offline_access** - this will allow the app to refresh access tokens when they expire.</span></span>
    - <span data-ttu-id="e81a8-129">**Calendars.ReadWrite** - isso permitirá que o aplicativo leia e escreva no calendário do usuário.</span><span class="sxs-lookup"><span data-stu-id="e81a8-129">**Calendars.ReadWrite** - this will allow the app to read and write to the user's calendar.</span></span>
    - <span data-ttu-id="e81a8-130">**MailboxSettings.Read** - isso permitirá que o aplicativo receba o fuso horário do usuário a partir de suas configurações de caixa de correio.</span><span class="sxs-lookup"><span data-stu-id="e81a8-130">**MailboxSettings.Read** - this will allow the app to get the user's time zone from their mailbox settings.</span></span>

    ![Uma captura de tela das permissões configuradas](images/configured-permissions.png)

## <a name="configure-office-add-in-single-sign-on"></a><span data-ttu-id="e81a8-132">Configurar o login único do Office Add-in</span><span class="sxs-lookup"><span data-stu-id="e81a8-132">Configure Office Add-in single sign-on</span></span>

<span data-ttu-id="e81a8-133">Nesta seção, você atualizará o registro do aplicativo para dar suporte ao [SSO (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins).</span><span class="sxs-lookup"><span data-stu-id="e81a8-133">In this section you'll update the app registration to support [Office Add-in single sign-on (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins).</span></span>

1. <span data-ttu-id="e81a8-134">Selecione **Expor uma API**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-134">Select **Expose an API**.</span></span> <span data-ttu-id="e81a8-135">Na seção **Escopos definidos por esta API,** selecione **Adicionar um escopo**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-135">In the **Scopes defined by this API** section, select **Add a scope**.</span></span> <span data-ttu-id="e81a8-136">Quando solicitado a definir um **URI de ID** do aplicativo, de definir o valor como `api://localhost:3000/YOUR_APP_ID_HERE` , `YOUR_APP_ID_HERE` substituindo pela ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e81a8-136">When prompted to set an **Application ID URI**, set the value to `api://localhost:3000/YOUR_APP_ID_HERE`, replacing `YOUR_APP_ID_HERE` with the application ID.</span></span> <span data-ttu-id="e81a8-137">Escolha **Salvar e continuar**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-137">Choose **Save and continue**.</span></span>

1. <span data-ttu-id="e81a8-138">Preencha os campos da seguinte forma e selecione **Adicionar escopo**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-138">Fill in the fields as follows and select **Add scope**.</span></span>

    - <span data-ttu-id="e81a8-139">**Nome do escopo:**`access_as_user`</span><span class="sxs-lookup"><span data-stu-id="e81a8-139">**Scope name:** `access_as_user`</span></span>
    - <span data-ttu-id="e81a8-140">**Quem pode consentir?: Administradores e usuários**</span><span class="sxs-lookup"><span data-stu-id="e81a8-140">**Who can consent?: Admins and users**</span></span>
    - <span data-ttu-id="e81a8-141">**Nome de exibição de consentimento do administrador:**`Access the app as the user`</span><span class="sxs-lookup"><span data-stu-id="e81a8-141">**Admin consent display name:** `Access the app as the user`</span></span>
    - <span data-ttu-id="e81a8-142">**Descrição do consentimento do administrador:**`Allows Office Add-ins to call the app's web APIs as the current user.`</span><span class="sxs-lookup"><span data-stu-id="e81a8-142">**Admin consent description:** `Allows Office Add-ins to call the app's web APIs as the current user.`</span></span>
    - <span data-ttu-id="e81a8-143">**Nome de exibição de consentimento do usuário:**`Access the app as you`</span><span class="sxs-lookup"><span data-stu-id="e81a8-143">**User consent display name:** `Access the app as you`</span></span>
    - <span data-ttu-id="e81a8-144">**Descrição do consentimento do usuário:**`Allows Office Add-ins to call the app's web APIs as you.`</span><span class="sxs-lookup"><span data-stu-id="e81a8-144">**User consent description:** `Allows Office Add-ins to call the app's web APIs as you.`</span></span>
    - <span data-ttu-id="e81a8-145">**Estado: Habilitado**</span><span class="sxs-lookup"><span data-stu-id="e81a8-145">**State: Enabled**</span></span>

    ![Uma captura de tela do formulário Adicionar um escopo](images/add-scope.png)

1. <span data-ttu-id="e81a8-147">Na seção **Aplicativos cliente autorizados,** selecione **Adicionar um aplicativo cliente**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-147">In the **Authorized client applications** section, select **Add a client application**.</span></span> <span data-ttu-id="e81a8-148">Insira uma ID do cliente na lista a seguir, habilita o escopo em **Escopos Autorizados** e selecione **Adicionar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="e81a8-148">Enter a client ID from the following list, enable the scope under **Authorized scopes**, and select **Add application**.</span></span> <span data-ttu-id="e81a8-149">Repita esse processo para cada uma das IDs do cliente na lista.</span><span class="sxs-lookup"><span data-stu-id="e81a8-149">Repeat this process for each of the client IDs in the list.</span></span>

    - <span data-ttu-id="e81a8-150">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="e81a8-150">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span></span>
    - <span data-ttu-id="e81a8-151">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="e81a8-151">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span></span>
    - <span data-ttu-id="e81a8-152">`57fb890c-0dab-4253-a5e0-7188c88b2bb4`(Office na Web)</span><span class="sxs-lookup"><span data-stu-id="e81a8-152">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office on the web)</span></span>
    - <span data-ttu-id="e81a8-153">`08e18876-6177-487e-b8b5-cf950c1e598c`(Office na Web)</span><span class="sxs-lookup"><span data-stu-id="e81a8-153">`08e18876-6177-487e-b8b5-cf950c1e598c` (Office on the web)</span></span>
