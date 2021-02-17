---
ms.openlocfilehash: facdbb5c42e60e5bb0ee98b06ef68939a6010a67
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274184"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="1acd3-101">Nesta seção, você adicionará a capacidade de criar eventos no calendário do usuário.</span><span class="sxs-lookup"><span data-stu-id="1acd3-101">In this section you will add the ability to create events on the user's calendar.</span></span>

## <a name="implement-the-api"></a><span data-ttu-id="1acd3-102">Implementar a API</span><span class="sxs-lookup"><span data-stu-id="1acd3-102">Implement the API</span></span>

1. <span data-ttu-id="1acd3-103">Abra **./src/api/graph.ts** e adicione o seguinte código para implementar uma nova API de evento ( `POST /graph/newevent` ).</span><span class="sxs-lookup"><span data-stu-id="1acd3-103">Open **./src/api/graph.ts** and add the following code to implement a new event API (`POST /graph/newevent`).</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="CreateEventSnippet":::

1. <span data-ttu-id="1acd3-104">Abra **./src/addin/taskpane.js** e adicione a função a seguir para chamar a nova API de evento.</span><span class="sxs-lookup"><span data-stu-id="1acd3-104">Open **./src/addin/taskpane.js** and add the following function to call the new event API.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="CreateEventSnippet":::

1. <span data-ttu-id="1acd3-105">Salve todas as suas alterações, reinicie o servidor e atualize o painel de tarefas no Excel (feche todos os painéis de tarefas abertos e reaberto).</span><span class="sxs-lookup"><span data-stu-id="1acd3-105">Save all of your changes, restart the server, and refresh the task pane in Excel (close any open task panes and re-open).</span></span>

    ![Uma captura de tela do formulário criar evento](images/create-event-ui.png)

1. <span data-ttu-id="1acd3-107">Preencha o formulário e escolha **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1acd3-107">Fill in the form and choose **Create**.</span></span> <span data-ttu-id="1acd3-108">Verifique se o evento foi adicionado ao calendário do usuário.</span><span class="sxs-lookup"><span data-stu-id="1acd3-108">Verify that the event is added to the user's calendar.</span></span>
