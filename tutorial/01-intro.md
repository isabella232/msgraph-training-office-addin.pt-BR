---
ms.openlocfilehash: 2c323d61632c62c82af0561536656f1d68fe8938
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274203"
---
<!-- markdownlint-disable MD002 MD041 -->

Este tutorial ensina a criar um Complemento do Office para Excel que usa a API do Microsoft Graph para recuperar informações de calendário para um usuário.

> [!TIP]
> Se preferir apenas baixar o tutorial concluído, você pode baixar ou clonar o [repositório do GitHub.](https://github.com/microsoftgraph/msgraph-training-office-addin)

## <a name="prerequisites"></a>Pré-requisitos

Antes de iniciar essa demonstração, você deve [ ter ](https://nodejs.org)Node.js[e o Yarn](https://yarnpkg.com/) instalados em sua máquina de desenvolvimento. Se você não tiver o Node.js ou o Yarn, visite o link anterior para opções de download.

> [!NOTE]
> Talvez os usuários do Windows precisem instalar o Python e o Visual Studio Build Tools para dar suporte a módulos NPM que precisam ser compilados a partir do C/C++. O Node.js instalador no Windows oferece uma opção para instalar automaticamente essas ferramentas. Como alternativa, você pode seguir instruções em [https://github.com/nodejs/node-gyp#on-windows](https://github.com/nodejs/node-gyp#on-windows) .

Você também deve ter uma conta pessoal da Microsoft com uma caixa de correio no Outlook.com ou uma conta de trabalho ou de estudante da Microsoft. Se você não tiver uma conta da Microsoft, há algumas opções para obter uma conta gratuita:

- Você pode [se inscrever para uma nova conta pessoal da Microsoft.](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)
- Você pode se inscrever no Programa para Desenvolvedores do [Office 365](https://developer.microsoft.com/office/dev-program) para obter uma assinatura gratuita do Office 365.

> [!NOTE]
> Este tutorial foi escrito com o Node versão 14.15.0 e o Yarn versão 1.22.0. As etapas neste guia podem funcionar com outras versões, mas que não foram testadas.

## <a name="feedback"></a>Comentários

Faça comentários sobre este tutorial no repositório [do GitHub.](https://github.com/microsoftgraph/msgraph-training-office-addin)
