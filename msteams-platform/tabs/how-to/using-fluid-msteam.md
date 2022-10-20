---
title: 将 Fluid 与 Teams 配合使用
author: timtwang
ms.author: mobajemu
description: 有关将 Fluid 支持的实时协作功能集成到 Microsoft Teams 选项卡应用程序的教程
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: 620e2150ca6300fb8d37bc7c68b965aacb19700b
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615382"
---
# <a name="use-fluid-with-teams"></a>将 Fluid 与 Teams 配合使用

本教程结束时，可以将任何 Fluid 支持的应用程序集成到 Teams 中，并实时与其他人协作。

在本部分中，可以了解以下概念：

1. 将 Fluid 客户端集成到 Teams 选项卡应用程序中。
1. 在 Azure Fluid Relay)  (运行 Teams 应用程序并将其连接到 Fluid 服务。
1. 创建并获取 Fluid 容器，并将其传递给React组件。

有关生成复杂应用程序的详细信息，请参阅 FluidExamples 存储库中的 [Teams Fluid Hello World](https://github.com/microsoft/FluidExamples/tree/main/teams-fluid-hello-world) 示例。

## <a name="prerequisites"></a>先决条件

本教程需要熟悉以下概念和资源：

- [Fluid Framework 概述](https://fluidframework.com/docs/)
- [Fluid Framework 快速入门](https://fluidframework.com/docs/start/quick-start/)
- [React](https://reactjs.org/)和[React挂钩的基础知识](https://reactjs.org/docs/hooks-intro.html)
- 如何生成 [Microsoft Teams 选项卡](/microsoftteams/platform/tabs/what-are-tabs)

> [!div class="nextstepaction"]
> [安装先决条件](tab-requirements.md)

## <a name="create-the-project"></a>创建项目

1. 打开命令提示符并导航到要在其中创建项目的父文件夹，例如， `/My Microsoft Teams Projects`
1. 通过运行以下命令并 [创建通道选项卡来创建](create-channel-group-tab.md#create-a-custom-channel-or-group-tab-with-nodejs) Teams 选项卡应用程序：

    ```cmd
    yo teams
    ```

1. 创建后，使用以下命令 `cd <your project name>`导航到项目。
1. 该项目使用以下库：

    |库 |说明 |
    |---|---|
    | `fluid-framework`    |包含 IFluidContainer 和其他跨客户端同步数据的 [分布式数据结构](https://fluidframework.com/docs/build/dds/) 。|
    | `@fluidframework/azure-client`   |定义 [Fluid 容器](https://fluidframework.com/docs/build/containers/)的起始架构。|
    | `@fluidframework/test-client-utils` |`InsecureTokenProvider`定义创建到 Fluid 服务的连接所需的条件。|

    运行以下命令以安装库：

    ```cmd
    npm install @fluidframework/azure-client fluid-framework @fluidframework/test-client-utils
    ```

## <a name="code-the-project"></a>对项目进行编码

1. 在代码编辑器中打开该文件 `/src/client/<your tab name>` 。
1. 创建新文件并 `Util.ts` 添加以下 import 语句：

    ```ts
    //`Util.ts

    import { IFluidContainer } from "fluid-framework";
    import { AzureClient, AzureClientProps } from "@fluidframework/azure-client";
    import { InsecureTokenProvider } from "@fluidframework/test-client-utils";
    ```

### <a name="defining-fluid-functions-and-parameters"></a>定义 Fluid 函数和参数

此应用旨在用于 Microsoft Teams 的上下文，以及所有与 Fluid 相关的导入、初始化和函数。 这提供了增强的体验，并使将来更易于使用。 可以将以下代码添加到 import 语句：

```ts
// TODO 1: Define the parameter key(s).
// TODO 2: Define container schema.
// TODO 3: Define connectionConfig (AzureClientProps).
// TODO 4: Create Azure client.
// TODO 5: Define create container function.
// TODO 6: Define get container function.
```

> [!NOTE]
> 注释定义与 Fluid 服务和容器交互所需的所有函数和常量。

1. 将 `TODO 1:` 替换为下面的代码：

    ```ts
    export const containerIdQueryParamKey = "containerId";
    ```

    该常量在追加到 `contentUrl` Microsoft Teams 设置中时导出，稍后将用于分析内容页中的容器 ID。 这是一种常见的模式，可将重要的查询参数键存储为常量，而不是每次键入原始字符串。

    客户端必须先 `containerSchema` 定义此应用程序中使用的共享对象，然后客户端才能创建任何容器。 此示例使用 SharedMap 作为 `initialObjects`，但可以使用任何共享对象。

    > [!NOTE]
    > 是 `map` 对象的 `SharedMap` ID，并且它在容器中必须与任何其他 DDSes 一样唯一。

1. 将 `TODO: 2` 替换为下面的代码：

    ```ts
    const containerSchema = {
        initialObjects: { map: SharedMap }
    };
    ```

1. 将 `TODO: 3` 替换为下面的代码：

    ```ts
    const connectionConfig : AzureClientProps =
    {
        connection: {
            type: "local",
            tokenProvider: new InsecureTokenProvider("foobar", { id: "user" }),
            endpoint: "http://localhost:7070"
        }
    };
    ```

    在使用客户端之前，它需要定义 `AzureClientProps` 客户端使用的连接类型。 连接到服务需要该 `connectionConfig` 属性。 使用 Azure 客户端的本地模式。 若要在所有客户端之间启用协作，请将其替换为 Fluid Relay Service 凭据。 有关详细信息，请参阅如何 [设置 Azure Fluid Relay 服务](/azure/azure-fluid-relay/how-tos/provision-fluid-azure-portal)。

1. 将 `TODO: 4` 替换为下面的代码：

    ```ts
    const client = new AzureClient(connectionConfig);
    ```

1. 将 `TODO: 5` 替换为下面的代码：

    ```ts
    export async function createContainer() : Promise<string> {
        const { container } = await client.createContainer(containerSchema);
        const containerId = await container.attach();
        return containerId;
    };
    ```

    在配置页中创建容器并将其追加到 `contentUrl` Teams 设置时，必须在附加容器后返回容器 ID。

1. 将 `TODO: 6` 替换为下面的代码：

    ```ts
    export async function getContainer(id : string) : Promise<IFluidContainer> {
        const { container } = await client.getContainer(id, containerSchema);
        return container;
    };
    ```

    提取 Fluid 容器时，需要返回容器，因为应用程序必须在内容页中与容器及其内部的 DDS 进行交互。

### <a name="create-fluid-container-in-the-configuration-page"></a>在配置页中创建 Fluid 容器

1. 在代码编辑器中打开该文件 `src/client/<your tab name>/<your tab name>Config.tsx` 。

    标准 Teams 选项卡应用程序流从配置转到内容页。 若要启用协作，在加载到内容页时保留容器至关重要。 保存容器的最佳解决方案是将容器 ID 作为查询参数附加到 `contentUrl` 内容页的 URL 和 `websiteUrl`URL 上。 Teams 配置页中的“保存”按钮是配置页和内容页之间的网关。 这是一个创建容器并在设置中追加容器 ID 的位置。

1. 添加下列导入语句：

    ```ts
    import { createContainer, containerIdQueryParamKey } from "./Util";
    ```

1. 使用以下代码替换 `onSaveHandler` 方法。 此处添加的唯一行是调用前面定义的`Utils.ts`创建容器方法，然后将返回的容器 ID 追加到`contentUrl`查询参数中。`websiteUrl`

    ```ts {linenos=inline,hl_lines=[134,136,137]}
    const onSaveHandler = async (saveEvent: microsoftTeams.settings.SaveEvent) => {
        const host = "https://" + window.location.host;
        const containerId = await createContainer();
        microsoftTeams.settings.setSettings({
            contentUrl: host + "/<your tab name>/?" + containerIdQueryParamKey + "=" + containerId + "&name={loginHint}&tenant={tid}&group={groupId}&theme={theme}",
            websiteUrl: host + "/<your tab name>/?" + containerIdQueryParamKey + "=" + containerId + "&name={loginHint}&tenant={tid}&group={groupId}&theme={theme}",
            suggestedDisplayName: "<your tab name>",
            removeUrl: host + "/<your tab name>/remove.html?theme={theme}",
            entityId: entityId.current
        });
        saveEvent.notifySuccess();
    };
    ```

    请确保替换 `<your tab name>` 为项目中的选项卡名称。

    > [!WARNING]
    > 由于内容页 URL 用于存储容器 ID，因此在删除 Teams 选项卡时会删除此记录。
    > 此外，每个内容页面只能支持一个容器 ID。

### <a name="refactor-content-page-to-reflect-fluid-application"></a>重构内容页以反映 Fluid 应用程序

1. 在代码编辑器中打开该文件 `src/client/<your tab name>/<your tab name>.tsx` 。 典型的 Fluid 驱动应用程序由视图和 Fluid 数据结构组成。 专注于获取/加载 Fluid 容器，并将所有与 Fluid 相关的交互保留在React组件中。

1. 在内容页中添加以下 import 语句：

    ```ts
    import { IFluidContainer } from "fluid-framework";
    import { getContainer, containerIdQueryParamKey } from "./Util";
    ```

1. 删除内容页中 import 语句下的所有代码，并将其替换为以下代码：

    ```ts
    export const <your tab name> = () => {
      // TODO 1: Initialize Microsoft Teams.
      // TODO 2: Initialize inTeams boolean.
      // TODO 3: Define container as a React state.
      // TODO 4: Define a method that gets the Fluid container
      // TODO 5: Get Fluid container on content page startup.
      // TODO 6: Pass the container to the React component as argument.
    }
    ```

    请确保替换 `<your tab name>` 为为项目定义的选项卡名称。

1. 将 `TODO 1` 替换为下面的代码：

    ```ts
    microsoftTeams.initialize();
    ```

    若要在 Teams 中显示内容页，必须包含 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) ，并在页面加载后包含初始化它的调用。

1. 将 `TODO 2` 替换为下面的代码：

    ```ts
    const [{ inTeams }] = useTeams();
    ```

    由于 Teams 应用程序只是网页的 IFrame 注入，因此需要初始化 `inTeams` 布尔常量，以便知道应用程序是否在 Teams 内部，以及 Teams 资源（如 Teams 资源） `contentUrl`是否可用。

1. 将 `TODO 3` 替换为下面的代码：

    ```ts
    const [fluidContainer, setFluidContainer] = useState<IFluidContainer | undefined>(undefined);
    ```

    对容器使用React状态，因为它能够动态更新容器及其中的数据对象。

1. 将 `TODO 4` 替换为下面的代码：

    ```ts
    const getFluidContainer = async (url : URLSearchParams) => {
        const containerId = url.get(containerIdQueryParamKey);
        if (!containerId) {
            throw Error("containerId not found in the URL");
        }
        const container = await getContainer(containerId);
        setFluidContainer(container);
    };
    ```

    分析 URL 以获取由 `containerIdQueryParamKey`其定义的查询参数字符串，并检索容器 ID。 使用容器 ID 可以加载容器。 拥有容器后，请设置`fluidContainer`React状态，请参阅上一步。

1. 将 `TODO 5` 替换为下面的代码：

    ```ts
    useEffect(() => {
        if (inTeams === true) {
            microsoftTeams.settings.getSettings(async (instanceSettings) => {
                const url = new URL(instanceSettings.contentUrl);
                getFluidContainer(url.searchParams);
            });
            microsoftTeams.appInitialization.notifySuccess();
        }
    }, [inTeams]);
    ```

    定义如何获取 Fluid 容器后，需要告知React在加载时调用`getFluidContainer`，然后根据应用程序是否在 Teams 中将结果存储在状态。
    React的 [useState 挂钩](https://reactjs.org/docs/hooks-state.html)提供所需的存储，[UseEffect](https://reactjs.org/docs/hooks-effect.html) 允许你调用`getFluidContainer`呈现，将返回的值传递到`setFluidContainer`中。

    通过在依赖项数组末`useEffect`尾添加`inTeams`，应用可确保仅在内容页加载时调用此函数。

1. 将 `TODO 6` 替换为下面的代码：

    ```ts
    if (inTeams === false) {
      return (
          <div>This application only works in the context of Microsoft Teams</div>
      );
    }

    if (fluidContainer !== undefined) {
      return (
          <FluidComponent fluidContainer={fluidContainer} />
      );
    }

    return (
      <div>Loading FluidComponent...</div>
    );
    ```

    > [!NOTE]
    > 请务必确保在 Teams 中加载内容页面，并在将 Fluid 容器传递到定义`FluidComponent` (React组件之前定义 Fluid 容器，请参阅以下) 。

### <a name="create-react-component-for-fluid-view-and-data"></a>为 Fluid 视图和数据创建React组件

你已集成了 Teams 和 Fluid 的基本创建流。 现在可以创建自己的React组件来处理应用程序视图与 Fluid 数据之间的交互。 从现在起，逻辑和流的行为与其他 Fluid 驱动的应用程序一样。 设置基本结构后，可以通过更改和应用程序`ContainerSchema`视图与内容页中的 DDSes/数据对象的交互，将任何 [Fluid 示例](https://github.com/microsoft/FluidExamples)创建为 Teams 应用程序。

## <a name="start-the-fluid-server-and-run-the-application"></a>启动 Fluid 服务器并运行应用程序

如果使用 Azure 客户端本地模式在本地运行 Teams 应用程序，请确保在命令提示符中运行以下命令以启动 Fluid 服务：

```cmd
npx @fluidframework/azure-local-service@latest
```

若要运行并启动 Teams 应用程序，请打开另一个终端，并按照 [说明运行应用程序服务器](create-channel-group-tab.md#upload-your-application-to-teams)。

> [!WARNING]
> 不保留具有 `ngrok`免费隧道的 HostNames。 每次运行都会生成不同的 URL。 创建新 `ngrok` 隧道后，旧容器将不再可供访问。 有关生产方案，请参阅 [将 AzureClient 与 Azure Fluid Relay 配合使用](#use-azureclient-with-azure-fluid-relay)。

> [!NOTE]
> 安装其他依赖项，使此演示与 Webpack 5 兼容。 如果收到与“缓冲区”包相关的编译错误，请运行 `npm install -D buffer` 并重试。 这将在 Fluid Framework 的未来版本中解决。

## <a name="next-steps"></a>后续步骤

### <a name="use-azureclient-with-azure-fluid-relay"></a>将 AzureClient 与 Azure Fluid Relay 配合使用

由于这是 Teams 选项卡应用程序，因此协作和交互是主要焦点。 将之前提供的本地模式 `AzureClientProps` 替换为 Azure 服务实例中的非本地凭据，以便其他人可以加入应用程序并与你交互。 了解 [如何预配 Azure Fluid Relay 服务](/azure/azure-fluid-relay/how-tos/provision-fluid-azure-portal)。

> [!IMPORTANT]
> 必须隐藏传入 `AzureClientProps` 的凭据，避免意外提交到源代码管理。 Teams 项目附带一个 `.env` 文件，可将凭据存储为环境变量，并且文件本身已包含在其中 `.gitignore`。 若要在 Teams 中使用环境变量，请参阅 [“设置”并获取环境变量](#set-and-get-environment-variable)。

> [!WARNING]
> `InsecureTokenProvider` 是一种在本地测试应用程序的便捷方法。 你有责任处理任何用户身份验证，并为任何生产环境使用 [安全令牌](/azure/azure-fluid-relay/how-tos/connect-fluid-azure-service) 。

### <a name="set-and-get-environment-variable"></a>设置和获取环境变量

若要设置环境变量并在 Teams 中检索它，可以利用内置 `.env` 文件。 以下代码用于在 `.env`以下情况下设置环境变量：

```
# .env

TENANT_KEY=foobar
```

若要将文件内容 `.env` 传递到客户端应用，需要将其配置为 `webpack.config.js` 以便 `webpack` 在运行时提供对它们的访问权限。 使用以下代码从 `.env`以下代码添加环境变量：

```js
// webpack,config.js

webpack.EnvironmentPlugin({
    PUBLIC_HOSTNAME: undefined,
    TAB_APP_ID: null,
    TAB_APP_URI: null,
    REACT_APP_TENANT_KEY: JSON.stringify(process.env.TENANT_KEY) // Add environment variable here
}),
```

可以在其中访问环境变量 `Util.ts`

```ts
// Util.ts

tokenProvider: new InsecureTokenProvider(JSON.parse(process.env.REACT_APP_TENANT_KEY!), { id: "user" }),
```

> [!TIP]
> 对代码进行更改时，项目会自动重新生成并重新加载应用程序服务器。 但是，如果对容器架构进行更改，它们只会在关闭并重新启动应用程序服务器时生效。 为此，请转到命令提示符并按 Ctrl-C 两次。 然后运行或`gulp ngrok-serve`再次运行`gulp serve`。

## <a name="see-also"></a>另请参阅

- [Azure Fluid Relay 文档](/azure/azure-fluid-relay)

- [Fluid Framework 文档](https://fluidframework.com/docs/)
- [流体示例 GitHub 存储库](https://github.com/microsoft/FluidExamples)
