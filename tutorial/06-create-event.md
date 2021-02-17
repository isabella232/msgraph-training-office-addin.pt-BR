---
ms.openlocfilehash: facdbb5c42e60e5bb0ee98b06ef68939a6010a67
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274184"
---
<!-- markdownlint-disable MD002 MD041 -->

Nesta seção, você adicionará a capacidade de criar eventos no calendário do usuário.

## <a name="implement-the-api"></a>Implementar a API

1. Abra **./src/api/graph.ts** e adicione o seguinte código para implementar uma nova API de evento ( `POST /graph/newevent` ).

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="CreateEventSnippet":::

1. Abra **./src/addin/taskpane.js** e adicione a função a seguir para chamar a nova API de evento.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="CreateEventSnippet":::

1. Salve todas as suas alterações, reinicie o servidor e atualize o painel de tarefas no Excel (feche todos os painéis de tarefas abertos e reaberto).

    ![Uma captura de tela do formulário criar evento](images/create-event-ui.png)

1. Preencha o formulário e escolha **Criar**. Verifique se o evento foi adicionado ao calendário do usuário.
