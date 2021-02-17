---
ms.openlocfilehash: ade142f1518d9bd56fa1472889721a4c8995bc3c
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274185"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="8242b-101">Neste exercício, você incorporará o Microsoft Graph ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8242b-101">In this exercise you will incorporate Microsoft Graph into the application.</span></span> <span data-ttu-id="8242b-102">Para este aplicativo, você usará a biblioteca [microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) para fazer chamadas para o Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="8242b-102">For this application, you will use the [microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) library to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="8242b-103">Obter eventos de calendário do Outlook</span><span class="sxs-lookup"><span data-stu-id="8242b-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="8242b-104">Comece adicionando uma API para obter uma [exibição de](https://docs.microsoft.com/graph/api/user-list-calendarview) calendário do calendário do usuário.</span><span class="sxs-lookup"><span data-stu-id="8242b-104">Start by adding an API to get a [calendar view](https://docs.microsoft.com/graph/api/user-list-calendarview) from the user's calendar.</span></span>

1. <span data-ttu-id="8242b-105">Abra **./src/api/graph.ts** e adicione as instruções a `import` seguir na parte superior do arquivo.</span><span class="sxs-lookup"><span data-stu-id="8242b-105">Open **./src/api/graph.ts** and add the following `import` statements to the top of the file.</span></span>

    ```typescript
    import { zonedTimeToUtc } from 'date-fns-tz';
    import { findOneIana } from 'windows-iana';
    import * as graph from '@microsoft/microsoft-graph-client';
    import { Event, MailboxSettings } from 'microsoft-graph';
    import 'isomorphic-fetch';
    import { getTokenOnBehalfOf } from './auth';
    ```

1. <span data-ttu-id="8242b-106">Adicione a função a seguir para inicializar o SDK do Microsoft Graph e retornar um **Cliente.**</span><span class="sxs-lookup"><span data-stu-id="8242b-106">Add the following function to initialize the Microsoft Graph SDK and return a **Client**.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="GetClientSnippet":::

1. <span data-ttu-id="8242b-107">Adicione a função a seguir para obter o fuso horário do usuário a partir de suas configurações de caixa de correio e converter esse valor em um identificador de fuso horário IANA.</span><span class="sxs-lookup"><span data-stu-id="8242b-107">Add the following function to get the user's time zone from their mailbox settings, and to convert that value to an IANA time zone identifier.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="GetTimeZonesSnippet":::

1. <span data-ttu-id="8242b-108">Adicione a seguinte função (abaixo da `const graphRouter = Router();` linha) para implementar um ponto de extremidade de API ( `GET /graph/calendarview` ).</span><span class="sxs-lookup"><span data-stu-id="8242b-108">Add the following function (below the `const graphRouter = Router();` line) to implement an API endpoint (`GET /graph/calendarview`).</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="GetCalendarViewSnippet":::

    <span data-ttu-id="8242b-109">Considere o que esse código faz.</span><span class="sxs-lookup"><span data-stu-id="8242b-109">Consider what this code does.</span></span>

    - <span data-ttu-id="8242b-110">Ele obtém o fuso horário do usuário e o usa para converter o início e o fim da exibição de calendário solicitada em valores UTC.</span><span class="sxs-lookup"><span data-stu-id="8242b-110">It gets the user's time zone and uses that to convert the start and end of the requested calendar view into UTC values.</span></span>
    - <span data-ttu-id="8242b-111">Ele faz um `GET` para o ponto de extremidade da API do `/me/calendarview` Graph.</span><span class="sxs-lookup"><span data-stu-id="8242b-111">It does a `GET` to the `/me/calendarview` Graph API endpoint.</span></span>
        - <span data-ttu-id="8242b-112">Ele usa a função para definir o header, fazendo com que as horas de início e término dos eventos retornados sejam ajustadas para o `header` `Prefer: outlook.timezone` fuso horário do usuário.</span><span class="sxs-lookup"><span data-stu-id="8242b-112">It uses the `header` function to set the `Prefer: outlook.timezone` header, causing the start and end times of the returned events to be adjusted to the user's time zone.</span></span>
        - <span data-ttu-id="8242b-113">Ele usa a `query` função para adicionar os `startDateTime` `endDateTime` parâmetros, definindo o início e o fim do ponto de vista de calendário.</span><span class="sxs-lookup"><span data-stu-id="8242b-113">It uses the `query` function to add the `startDateTime` and `endDateTime` parameters, setting the start and end of the calendar view.</span></span>
        - <span data-ttu-id="8242b-114">Ele usa `select` a função para solicitar apenas os campos usados pelo complemento.</span><span class="sxs-lookup"><span data-stu-id="8242b-114">It uses the `select` function to request only the fields used by the add-in.</span></span>
        - <span data-ttu-id="8242b-115">Ela usa `orderby` a função para classificar os resultados pela hora de início.</span><span class="sxs-lookup"><span data-stu-id="8242b-115">It uses the `orderby` function to sort the results by the start time.</span></span>
        - <span data-ttu-id="8242b-116">Ela usa `top` a função para limitar os resultados em uma única solicitação a 25.</span><span class="sxs-lookup"><span data-stu-id="8242b-116">It uses the `top` function to limit the results in a single request to 25.</span></span>
    - <span data-ttu-id="8242b-117">Ele usa um **objeto PageIteratorCallback** para [iterar](https://docs.microsoft.com/graph/sdks/paging) pelos resultados e para fazer solicitações adicionais se mais páginas de resultados estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="8242b-117">It uses a **PageIteratorCallback** object to [iterate through the results](https://docs.microsoft.com/graph/sdks/paging) and to make additional requests if more pages of results are available.</span></span>

## <a name="update-the-ui"></a><span data-ttu-id="8242b-118">Atualizar a interface do usuário</span><span class="sxs-lookup"><span data-stu-id="8242b-118">Update the UI</span></span>

<span data-ttu-id="8242b-119">Agora vamos atualizar o painel de tarefas para permitir que o usuário especifique uma data de início e de término para a exibição de calendário.</span><span class="sxs-lookup"><span data-stu-id="8242b-119">Now let's update the task pane to allow the user to specify a start and end date for the calendar view.</span></span>

1. <span data-ttu-id="8242b-120">Abra **./src/addin/taskpane.js** e substitua a função `showMainUi` existente pelo seguinte.</span><span class="sxs-lookup"><span data-stu-id="8242b-120">Open **./src/addin/taskpane.js** and replace the existing `showMainUi` function with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="MainUiSnippet":::

    <span data-ttu-id="8242b-121">Este código adiciona um formulário simples para que o usuário possa especificar uma data de início e de término.</span><span class="sxs-lookup"><span data-stu-id="8242b-121">This code adds a simple form so the user can specify a start and end date.</span></span> <span data-ttu-id="8242b-122">Ele também implementa um segundo formulário para criar um novo evento.</span><span class="sxs-lookup"><span data-stu-id="8242b-122">It also implements a second form for creating a new event.</span></span> <span data-ttu-id="8242b-123">Esse formulário não faz nada por enquanto, você implementará esse recurso na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="8242b-123">That form doesn't do anything for now, you'll implement that feature in the next section.</span></span>

1. <span data-ttu-id="8242b-124">Adicione o código a seguir ao arquivo para criar uma tabela na planilha ativa contendo os eventos recuperados da exibição de calendário.</span><span class="sxs-lookup"><span data-stu-id="8242b-124">Add the following code to the file to create a table in the active worksheet containing the events retrieved from the calendar view.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="WriteToSheetSnippet":::

1. <span data-ttu-id="8242b-125">Adicione a função a seguir para chamar a API de exibição de calendário.</span><span class="sxs-lookup"><span data-stu-id="8242b-125">Add the following function to call the calendar view API.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="GetCalendarSnippet":::

1. <span data-ttu-id="8242b-126">Salve todas as suas alterações, reinicie o servidor e atualize o painel de tarefas no Excel (feche todos os painéis de tarefas abertos e reaberto).</span><span class="sxs-lookup"><span data-stu-id="8242b-126">Save all of your changes, restart the server, and refresh the task pane in Excel (close any open task panes and re-open).</span></span>

    ![Uma captura de tela do formulário de importação](images/get-calendar-view-ui.png)

1. <span data-ttu-id="8242b-128">Escolha as datas de início e término e escolha **Importar**.</span><span class="sxs-lookup"><span data-stu-id="8242b-128">Choose start and end dates and choose **Import**.</span></span>

    ![Uma captura de tela da tabela de eventos](images/calendar-view-table.png)
