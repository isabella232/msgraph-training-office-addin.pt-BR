---
ms.openlocfilehash: 2c323d61632c62c82af0561536656f1d68fe8938
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274203"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="44b59-101">Este tutorial ensina a criar um Complemento do Office para Excel que usa a API do Microsoft Graph para recuperar informações de calendário para um usuário.</span><span class="sxs-lookup"><span data-stu-id="44b59-101">This tutorial teaches you how to build an Office Add-in for Excel that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="44b59-102">Se preferir apenas baixar o tutorial concluído, você pode baixar ou clonar o [repositório do GitHub.](https://github.com/microsoftgraph/msgraph-training-office-addin)</span><span class="sxs-lookup"><span data-stu-id="44b59-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-office-addin).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44b59-103">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="44b59-103">Prerequisites</span></span>

<span data-ttu-id="44b59-104">Antes de iniciar essa demonstração, você deve [ ter ](https://nodejs.org)Node.js[e o Yarn](https://yarnpkg.com/) instalados em sua máquina de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="44b59-104">Before you start this demo, you should have [Node.js](https://nodejs.org) and [Yarn](https://yarnpkg.com/) installed on your development machine.</span></span> <span data-ttu-id="44b59-105">Se você não tiver o Node.js ou o Yarn, visite o link anterior para opções de download.</span><span class="sxs-lookup"><span data-stu-id="44b59-105">If you do not have Node.js or Yarn, visit the previous link for download options.</span></span>

> [!NOTE]
> <span data-ttu-id="44b59-106">Talvez os usuários do Windows precisem instalar o Python e o Visual Studio Build Tools para dar suporte a módulos NPM que precisam ser compilados a partir do C/C++.</span><span class="sxs-lookup"><span data-stu-id="44b59-106">Windows users may need to install Python and Visual Studio Build Tools to support NPM modules that need to be compiled from C/C++.</span></span> <span data-ttu-id="44b59-107">O Node.js instalador no Windows oferece uma opção para instalar automaticamente essas ferramentas.</span><span class="sxs-lookup"><span data-stu-id="44b59-107">The Node.js installer on Windows gives an option to automatically install these tools.</span></span> <span data-ttu-id="44b59-108">Como alternativa, você pode seguir instruções em [https://github.com/nodejs/node-gyp#on-windows](https://github.com/nodejs/node-gyp#on-windows) .</span><span class="sxs-lookup"><span data-stu-id="44b59-108">Alternatively, you can follow instructions at [https://github.com/nodejs/node-gyp#on-windows](https://github.com/nodejs/node-gyp#on-windows).</span></span>

<span data-ttu-id="44b59-109">Você também deve ter uma conta pessoal da Microsoft com uma caixa de correio no Outlook.com ou uma conta de trabalho ou de estudante da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="44b59-109">You should also have either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span> <span data-ttu-id="44b59-110">Se você não tiver uma conta da Microsoft, há algumas opções para obter uma conta gratuita:</span><span class="sxs-lookup"><span data-stu-id="44b59-110">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="44b59-111">Você pode [se inscrever para uma nova conta pessoal da Microsoft.](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)</span><span class="sxs-lookup"><span data-stu-id="44b59-111">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="44b59-112">Você pode se inscrever no Programa para Desenvolvedores do [Office 365](https://developer.microsoft.com/office/dev-program) para obter uma assinatura gratuita do Office 365.</span><span class="sxs-lookup"><span data-stu-id="44b59-112">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="44b59-113">Este tutorial foi escrito com o Node versão 14.15.0 e o Yarn versão 1.22.0.</span><span class="sxs-lookup"><span data-stu-id="44b59-113">This tutorial was written with Node version 14.15.0 and Yarn version 1.22.0.</span></span> <span data-ttu-id="44b59-114">As etapas neste guia podem funcionar com outras versões, mas que não foram testadas.</span><span class="sxs-lookup"><span data-stu-id="44b59-114">The steps in this guide may work with other versions, but that has not been tested.</span></span>

## <a name="feedback"></a><span data-ttu-id="44b59-115">Comentários</span><span class="sxs-lookup"><span data-stu-id="44b59-115">Feedback</span></span>

<span data-ttu-id="44b59-116">Faça comentários sobre este tutorial no repositório [do GitHub.](https://github.com/microsoftgraph/msgraph-training-office-addin)</span><span class="sxs-lookup"><span data-stu-id="44b59-116">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-office-addin).</span></span>
