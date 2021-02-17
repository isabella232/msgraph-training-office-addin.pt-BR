---
ms.openlocfilehash: a336095a238eefeae22dac86d29e3140e8d94bf1
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274190"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="338f1-101">Neste exercício, você criará um novo registro de aplicativo Web do Azure AD usando o centro de administração do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="338f1-101">In this exercise, you will create a new Azure AD web application registration using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="338f1-102">Abra um navegador e navegue até o [centro de administração do Azure Active Directory](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="338f1-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="338f1-103">Faça logon usando uma **conta pessoal** (também conhecida como Conta da Microsoft) ou **Conta Corporativa ou de Estudante**.</span><span class="sxs-lookup"><span data-stu-id="338f1-103">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="338f1-104">Selecione **Azure Active Directory** na navegação esquerda e selecione **Registros de aplicativos** em **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="338f1-104">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="338f1-105">Uma captura de tela dos registros do aplicativo</span><span class="sxs-lookup"><span data-stu-id="338f1-105">A screenshot of the App registrations</span></span> ](images/app-registrations.png)

1. <span data-ttu-id="338f1-106">Selecione **Novo registro**.</span><span class="sxs-lookup"><span data-stu-id="338f1-106">Select **New registration**.</span></span> <span data-ttu-id="338f1-107">Na página **Registrar um aplicativo**, defina os valores da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="338f1-107">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="338f1-108">Defina **Nome** para `Office Add-in Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="338f1-108">Set **Name** to `Office Add-in Graph Tutorial`.</span></span>
    - <span data-ttu-id="338f1-109">Defina **Tipos de conta com suporte** para **Contas em qualquer diretório organizacional e contas pessoais da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="338f1-109">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="338f1-110">Em **URI de Redirecionamento**, defina o primeiro menu suspenso para `Single-page application (SPA)` e defina o valor como `https://localhost:3000/consent.html`.</span><span class="sxs-lookup"><span data-stu-id="338f1-110">Under **Redirect URI**, set the first drop-down to `Single-page application (SPA)` and set the value to `https://localhost:3000/consent.html`.</span></span>

    ![Uma captura de tela da página Registrar um aplicativo](images/register-an-app.png)

1. <span data-ttu-id="338f1-112">Selecione **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="338f1-112">Select **Register**.</span></span> <span data-ttu-id="338f1-113">Na página do Tutorial do Graph do Complemento do Office, copie o valor da ID do Aplicativo **(cliente)** e **salve-o,** você precisará dele na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="338f1-113">On the **Office Add-in Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Uma captura de tela da ID do aplicativo do novo registro de aplicativo](images/application-id.png)

1. <span data-ttu-id="338f1-115">Selecione **Certificados e segredos** sob **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="338f1-115">Select **Certificates & secrets** under **Manage**.</span></span> <span data-ttu-id="338f1-116">Selecione o botão **Novo segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="338f1-116">Select the **New client secret** button.</span></span> <span data-ttu-id="338f1-117">Insira um valor em **Descrição** e selecione uma das opções para **Expirar** e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="338f1-117">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

1. <span data-ttu-id="338f1-118">Copie o valor secreto do cliente antes de sair desta página.</span><span class="sxs-lookup"><span data-stu-id="338f1-118">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="338f1-119">Você precisará dele na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="338f1-119">You will need it in the next step.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="338f1-120">Este segredo do cliente nunca é mostrado novamente, portanto, copie-o agora.</span><span class="sxs-lookup"><span data-stu-id="338f1-120">This client secret is never shown again, so make sure you copy it now.</span></span>

1. <span data-ttu-id="338f1-121">Selecione **permissões de API em** **Gerenciar** e, em **seguida, selecione Adicionar uma permissão.**</span><span class="sxs-lookup"><span data-stu-id="338f1-121">Select **API permissions** under **Manage**, then select **Add a permission**.</span></span>

1. <span data-ttu-id="338f1-122">Selecione **o Microsoft Graph** e, em **seguida, permissões delegadas.**</span><span class="sxs-lookup"><span data-stu-id="338f1-122">Select **Microsoft Graph**, then **Delegated permissions**.</span></span>

1. <span data-ttu-id="338f1-123">Selecione as seguintes permissões e, em seguida, **selecione Adicionar permissões.**</span><span class="sxs-lookup"><span data-stu-id="338f1-123">Select the following permissions, then select **Add permissions**.</span></span>

    - <span data-ttu-id="338f1-124">**offline_access** - isso permitirá que o aplicativo atualize tokens de acesso quando expirarem.</span><span class="sxs-lookup"><span data-stu-id="338f1-124">**offline_access** - this will allow the app to refresh access tokens when they expire.</span></span>
    - <span data-ttu-id="338f1-125">**Calendars.ReadWrite** - isso permitirá que o aplicativo leia e escreva no calendário do usuário.</span><span class="sxs-lookup"><span data-stu-id="338f1-125">**Calendars.ReadWrite** - this will allow the app to read and write to the user's calendar.</span></span>
    - <span data-ttu-id="338f1-126">**MailboxSettings.Read** - isso permitirá que o aplicativo receba o fuso horário do usuário nas configurações da caixa de correio.</span><span class="sxs-lookup"><span data-stu-id="338f1-126">**MailboxSettings.Read** - this will allow the app to get the user's time zone from their mailbox settings.</span></span>

    ![Uma captura de tela das permissões configuradas](images/configured-permissions.png)

## <a name="configure-office-add-in-single-sign-on"></a><span data-ttu-id="338f1-128">Configurar o single sign-on do Office Add-in</span><span class="sxs-lookup"><span data-stu-id="338f1-128">Configure Office Add-in single sign-on</span></span>

<span data-ttu-id="338f1-129">Nesta seção, você atualizará o registro do aplicativo para dar suporte ao [SSO (single sign-on)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins)do Complemento do Office.</span><span class="sxs-lookup"><span data-stu-id="338f1-129">In this section you'll update the app registration to support [Office Add-in single sign-on (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins).</span></span>

1. <span data-ttu-id="338f1-130">Selecione **Expor uma API.**</span><span class="sxs-lookup"><span data-stu-id="338f1-130">Select **Expose an API**.</span></span> <span data-ttu-id="338f1-131">Nos **Escopos definidos por esta seção da API,** selecione **Adicionar um escopo.**</span><span class="sxs-lookup"><span data-stu-id="338f1-131">In the **Scopes defined by this API** section, select **Add a scope**.</span></span> <span data-ttu-id="338f1-132">Quando solicitado a definir um **URI da ID** do Aplicativo, de definida o valor como `api://localhost:3000/YOUR_APP_ID_HERE` , `YOUR_APP_ID_HERE` substituindo pela ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="338f1-132">When prompted to set an **Application ID URI**, set the value to `api://localhost:3000/YOUR_APP_ID_HERE`, replacing `YOUR_APP_ID_HERE` with the application ID.</span></span> <span data-ttu-id="338f1-133">Escolha **Salvar e continuar.**</span><span class="sxs-lookup"><span data-stu-id="338f1-133">Choose **Save and continue**.</span></span>

1. <span data-ttu-id="338f1-134">Preencha os campos da seguinte forma e selecione **Adicionar escopo.**</span><span class="sxs-lookup"><span data-stu-id="338f1-134">Fill in the fields as follows and select **Add scope**.</span></span>

    - <span data-ttu-id="338f1-135">**Nome do escopo:**`access_as_user`</span><span class="sxs-lookup"><span data-stu-id="338f1-135">**Scope name:** `access_as_user`</span></span>
    - <span data-ttu-id="338f1-136">**Quem pode consentir?: Administradores e usuários**</span><span class="sxs-lookup"><span data-stu-id="338f1-136">**Who can consent?: Admins and users**</span></span>
    - <span data-ttu-id="338f1-137">**Nome de exibição do consentimento do administrador:**`Access the app as the user`</span><span class="sxs-lookup"><span data-stu-id="338f1-137">**Admin consent display name:** `Access the app as the user`</span></span>
    - <span data-ttu-id="338f1-138">**Descrição do consentimento do administrador:**`Allows Office Add-ins to call the app's web APIs as the current user.`</span><span class="sxs-lookup"><span data-stu-id="338f1-138">**Admin consent description:** `Allows Office Add-ins to call the app's web APIs as the current user.`</span></span>
    - <span data-ttu-id="338f1-139">**Nome de exibição do consentimento do usuário:**`Access the app as you`</span><span class="sxs-lookup"><span data-stu-id="338f1-139">**User consent display name:** `Access the app as you`</span></span>
    - <span data-ttu-id="338f1-140">**Descrição do consentimento do usuário:**`Allows Office Add-ins to call the app's web APIs as you.`</span><span class="sxs-lookup"><span data-stu-id="338f1-140">**User consent description:** `Allows Office Add-ins to call the app's web APIs as you.`</span></span>
    - <span data-ttu-id="338f1-141">**Estado: Habilitado**</span><span class="sxs-lookup"><span data-stu-id="338f1-141">**State: Enabled**</span></span>

    ![Uma captura de tela do formulário Adicionar um escopo](images/add-scope.png)

1. <span data-ttu-id="338f1-143">Na seção **Aplicativos cliente autorizados,** selecione **Adicionar um aplicativo cliente**.</span><span class="sxs-lookup"><span data-stu-id="338f1-143">In the **Authorized client applications** section, select **Add a client application**.</span></span> <span data-ttu-id="338f1-144">Insira uma ID de cliente na lista a seguir, habilita o escopo em **Escopos autorizados** e selecione **Adicionar aplicativo.**</span><span class="sxs-lookup"><span data-stu-id="338f1-144">Enter a client ID from the following list, enable the scope under **Authorized scopes**, and select **Add application**.</span></span> <span data-ttu-id="338f1-145">Repita esse processo para cada uma das IDs de cliente na lista.</span><span class="sxs-lookup"><span data-stu-id="338f1-145">Repeat this process for each of the client IDs in the list.</span></span>

    - <span data-ttu-id="338f1-146">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="338f1-146">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span></span>
    - <span data-ttu-id="338f1-147">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="338f1-147">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span></span>
    - <span data-ttu-id="338f1-148">`57fb890c-0dab-4253-a5e0-7188c88b2bb4`(Office na Web)</span><span class="sxs-lookup"><span data-stu-id="338f1-148">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office on the web)</span></span>
    - <span data-ttu-id="338f1-149">`08e18876-6177-487e-b8b5-cf950c1e598c`(Office na Web)</span><span class="sxs-lookup"><span data-stu-id="338f1-149">`08e18876-6177-487e-b8b5-cf950c1e598c` (Office on the web)</span></span>
