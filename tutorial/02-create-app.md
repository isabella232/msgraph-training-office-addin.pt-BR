---
ms.openlocfilehash: 70df2dfceb1d2df527acfecab894b28019c6febb
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274205"
---
<!-- markdownlint-disable MD002 MD041 -->

Neste exercício, você criará uma solução de add-in do Office usando [o Express.](http://expressjs.com/) A solução consistirá em duas partes.

- O complemento, implementado como arquivos HTML e JavaScript estáticos.
- Um Node.js/Express que serve o complemento e implementa uma API Web para recuperar dados para o complemento.

## <a name="create-the-server"></a>Criar o servidor

1. Abra sua CLI (interface de linha de comando), navegue até um diretório onde você deseja criar seu projeto e execute o seguinte comando para gerar um package.jsno arquivo.

    ```Shell
    yarn init
    ```

    Insira valores para os prompts conforme apropriado. Se você não tiver certeza, os valores padrão serão bons.

1. Execute os seguintes comandos para instalar dependências.

    ```Shell
    yarn add express@4.17.1 express-promise-router@4.0.1 dotenv@8.2.0 node-fetch@2.6.1 jsonwebtoken@8.5.1@
    yarn add jwks-rsa@1.11.0 @azure/msal-node@1.0.0-beta.1 @microsoft/microsoft-graph-client@2.1.1
    yarn add date-fns@2.16.1 date-fns-tz@1.0.12 isomorphic-fetch@3.0.0 windows-iana@4.2.1
    yarn add -D typescript@4.0.5 ts-node@9.0.0 nodemon@2.0.6 @types/node@14.14.7 @types/express@4.17.9
    yarn add -D @types/node-fetch@2.5.7 @types/jsonwebtoken@8.5.0 @types/microsoft-graph@1.26.0
    yarn add -D @types/office-js@1.0.147 @types/jquery@3.5.4 @types/isomorphic-fetch@0.0.35
    ```

1. Execute o seguinte comando para gerar um tsconfig.jsno arquivo.

    ```Shell
    tsc --init
    ```

1. Abra **./tsconfig.jsem** um editor de texto e faça as seguintes alterações.

    - Altere `target` o valor para `es6` .
    - Uncomment the `outDir` value and set it to `./dist` .
    - Uncomment the `rootDir` value and set it to `./src` .

1. Abra **./package.jse** adicione a propriedade a seguir ao JSON.

    ```json
    "scripts": {
      "start": "nodemon ./src/server.ts",
      "build": "tsc --project ./"
    },
    ```

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

1. Crie um novo arquivo chamado **.env** na raiz do projeto e adicione o código a seguir.

    :::code language="ini" source="../demo/graph-tutorial/example.env":::

    Substitua pelo caminho para localhost.crt e pelo caminho `PATH_TO_LOCALHOST.CRT` `PATH_TO_LOCALHOST.KEY` para localhost.key output pelo comando anterior.

1. Crie um novo diretório na raiz do seu projeto chamado **src**.

1. Crie dois diretórios no **diretório ./src:** **addin** e **api.**

1. Crie um novo arquivo chamado **auth.ts** no diretório **./src/api** e adicione o código a seguir.

    ```typescript
    import Router from 'express-promise-router';

    const authRouter = Router();

    // TODO: Implement this router

    export default authRouter;
    ```

1. Crie um novo arquivo chamado **graph.ts** no diretório **./src/api** e adicione o código a seguir.

    ```typescript
    import Router from 'express-promise-router';

    const graphRouter = Router();

    // TODO: Implement this router

    export default graphRouter;
    ```

1. Crie um novo arquivo chamado **server.ts** no diretório **./src** e adicione o código a seguir.

    :::code language="typescript" source="../demo/graph-tutorial/src/server.ts" id="ServerSnippet":::

## <a name="create-the-add-in"></a>Criar o suplemento

1. Crie um novo arquivo **taskpane.html** no diretório **./src/addin** e adicione o código a seguir.

    :::code language="html" source="../demo/graph-tutorial/src/addin/taskpane.html" id="TaskPaneHtmlSnippet":::

1. Crie um novo arquivo denominado **taskpane.css** no diretório **./src/addin** e adicione o código a seguir.

    :::code language="css" source="../demo/graph-tutorial/src/addin/taskpane.css":::

1. Crie um novo arquivo **taskpane.js** no diretório **./src/addin** e adicione o código a seguir.

    ```javascript
    // TEMPORARY CODE TO VERIFY ADD-IN LOADS
    'use strict';

    Office.onReady(info => {
      if (info.host === Office.HostType.Excel) {
        $(function() {
          $('p').text('Hello World!!');
        });
      }
    });
    ```

1. Crie um novo diretório no diretório **.src/addin denominado** **ativos.**

1. Adicione três arquivos PNG neste diretório de acordo com a tabela a seguir.

    | Nome do arquivo   | Tamanho em pixels |
    |-------------|----------------|
    | icon-80.png | 80x80          |
    | icon-32.png | 32x32          |
    | icon-16.png | 16 x 16          |

    > [!NOTE]
    > Você pode usar qualquer imagem que quiser para esta etapa. Você também pode baixar as imagens usadas neste exemplo diretamente do [GitHub.](https://github.com/microsoftgraph/msgraph-training-office-addin/demo/graph-tutorial/src/addin/assets)

1. Crie um novo diretório na raiz do manifesto nomeado do **projeto.**

1. Crie um novo arquivo **manifest.xml** na pasta **./manifest** e adicione o código a seguir. Substitua `NEW_GUID_HERE` por um novo GUID, como `b4fa03b8-1eb6-4e8b-a380-e0476be9e019` .

    :::code language="xml" source="../demo/graph-tutorial/manifest/manifest.xml":::

## <a name="side-load-the-add-in-in-excel"></a>Side load the add-in in Excel

1. Inicie o servidor executando o seguinte comando.

    ```Shell
    yarn start
    ```

1. Abra seu navegador e navegue `https://localhost:3000/taskpane.html` até. Você verá uma `Not loaded` mensagem.

1. No navegador, vá para o [Office.com](https://www.office.com/) e entre. Selecione **Criar** na barra de ferramentas à esquerda e selecione **Planilha.**

    ![Uma captura de tela do menu Criar no Office.com](images/office-select-excel.png)

1. Selecione a **guia** Inserir e, em **seguida, selecione Os Complementos do Office.**

1. Selecione **Carregar Meu Complemento e,** em seguida, **Procurar.** Carregue seu **arquivo ./manifest/manifest.xml.**

1. Selecione o **botão Importar Calendário** na guia **Página** Início para abrir o taskpane.

    ![Uma captura de tela do botão Importar Calendário na guia Página Inicial](images/get-started.png)

1. Depois que o taskpane abrir, você deverá ver uma `Hello World!` mensagem.

    ![Uma captura de tela da mensagem Hello World](images/hello-world.png)
