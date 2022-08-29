---
title: Live Share 代码教程
author: surbhigupta
description: 在本模块中，了解如何开始使用 Live Share SDK，以及如何使用 Live Share SDK 生成 Dice Roller 示例
ms.topic: conceptual
ms.localizationpriority: high
ms.author: stevenic
ms.date: 04/07/2022
ms.openlocfilehash: 511083fea77c40cec0134e6620c741c3c4da8829
ms.sourcegitcommit: 134ce9381891e51e6327f1f611fdfd60c90cca18
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2022
ms.locfileid: "67425615"
---
# <a name="dice-roller-code-tutorial"></a>Dice Roller 代码教程

在 Dice Roller 示例应用中，用户会看到一个带有按钮的骰子来掷出它。 投掷骰子时，Live Share SDK 使用 Fluid Framework 跨客户端同步数据，因此每个人都可以看到相同的结果。 若要同步数据，请在 [app.js](https://github.com/microsoft/live-share-sdk/blob/main/samples/01.dice-roller/src/app.js) 文件中执行以下步骤：

1. [设置应用程序](#set-up-the-application)
2. [加入 Fluid 容器](#join-a-fluid-container)
3. [编写阶段视图](#write-the-stage-view)
4. [将阶段视图连接到 Fluid 数据](#connect-stage-view-to-fluid-data)
5. [编写侧面板视图](#write-the-side-panel-view)
6. [编写设置视图](#write-the-settings-view)

:::image type="content" source="../assets/images/teams-live-share/dice-roller.png" alt-text="DiceRoller 示例":::

## <a name="set-up-the-application"></a>设置应用程序

首先导入所需的模块。 该示例使用 Fluid Framework 中的 [SharedMap DDS](https://fluidframework.com/docs/data-structures/map/) 和 Live Share SDK 中的 [TeamsFluidClient](/javascript/api/@microsoft/live-share/teamsfluidclient)。 此示例支持 Teams 会议扩展性，因此我们需要包括 [Teams 客户端 SDK](https://github.com/OfficeDev/microsoft-teams-library-js)。 最后，该示例设计为在本地和 Teams 会议中运行，因此我们需要包括一些在 [本地测试示例](https://fluidframework.com/docs/testing/testing/#azure-fluid-relay-as-an-abstraction-for-tinylicious) 所需的其他 Fluid Framework 部分。

应用程序使用一个架构创建 Fluid 容器，该架构定义一组可供容器使用的 _初始对象_。 该示例使用 SharedMap 存储已投掷的最新骰子数值。 有关详细信息，请参阅 [数据建模](https://fluidframework.com/docs/build/data-modeling/)。

Teams 会议应用需要多个视图（内容、配置和阶段）。 我们将创建一个 `start()` 函数，以帮助标识要呈现的视图并执行所需的任何初始化。 我们希望应用支持在 Web 浏览器和 Teams 会议中本地运行，以便 `start()` 函数查找 `inTeams=true` 查询参数以确定它是否在 Teams 中运行。 在 Teams 中运行时，应用程序需要在调用任何其他 teams-js 方法之前调用 `app.initialize()`。

除了 `inTeams=true` 查询参数，我们还可以使用 `view=content|config|stage` 查询参数来确定需要呈现的视图。

```js
import { SharedMap } from "fluid-framework";
import { TeamsFluidClient } from "@microsoft/live-share";
import { app, pages } from "@microsoft/teams-js";
import { LOCAL_MODE_TENANT_ID } from "@fluidframework/azure-client";
import { InsecureTokenProvider } from "@fluidframework/test-client-utils";

const searchParams = new URL(window.location).searchParams;
const root = document.getElementById("content");

// Define container schema

const diceValueKey = "dice-value-key";

const containerSchema = {
  initialObjects: { diceMap: SharedMap },
};

function onContainerFirstCreated(container) {
  // Set initial state of the rolled dice to 1.
  container.initialObjects.diceMap.set(diceValueKey, 1);
}

// STARTUP LOGIC

async function start() {
  // Check for page to display
  let view = searchParams.get("view") || "stage";

  // Check if we are running on stage.
  if (!!searchParams.get("inTeams")) {
    // Initialize teams app
    await app.initialize();

    // Get our frameContext from context of our app in Teams
    const context = await app.getContext();
    if (context.page.frameContext == "meetingStage") {
      view = "stage";
    }
  }

  // Load the requested view
  switch (view) {
    case "content":
      renderSidePanel(root);
      break;
    case "config":
      renderSettings(root);
      break;
    case "stage":
    default:
      const { container } = await joinContainer();
      renderStage(container.initialObjects.diceMap, root);
      break;
  }
}

start().catch((error) => console.error(error));
```

## <a name="join-a-fluid-container"></a>加入 Fluid 容器

并非所有应用视图都需要协作。 `stage`视图 _始终_ 需要协作功能，`content`视图 _可能需要_ 协作功能，`config`视图 _不应_ 需要协作功能。 对于需要协作功能的视图，需要加入与当前会议关联的 Fluid 容器。

加入会议容器与创建新的 [TeamsFluidClient](/javascript/api/@microsoft/live-share/teamsfluidclient) ，然后调用 [JoinContainer()](/javascript/api/@microsoft/live-share/teamsfluidclient#@microsoft-live-share-teamsfluidclient-joincontainer) 方法一样简单。 在本地运行时，需要传入具有特殊 `LOCAL_MODE_TENANT_ID` 的自定义连接配置，否则，加入本地容器与在 Teams 中加入容器相同。

```js
async function joinContainer() {
  // Are we running in teams?
  let client;
  if (!!searchParams.get("inTeams")) {
    // Create client
    client = new TeamsFluidClient();
  } else {
    // Create client and configure for testing
    client = new TeamsFluidClient({
      connection: {
        type: "local",
        tokenProvider: new InsecureTokenProvider("", {
          id: "123",
          name: "Test User",
        }),
        endpoint: "http://localhost:7070",
      },
    });
  }

  // Join container
  return await client.joinContainer(containerSchema, onContainerFirstCreated);
}
```

> [!NOTE]
> 在本地测试时，TeamsFluidClient 会更新浏览器 URL，以包含已创建的测试容器的 ID。 将该链接复制到其他浏览器选项卡会导致 TeamsFluidClient 加入已创建的测试容器。 如果修改应用程序 URL 干扰应用程序操作，则可以使用传递给 TeamsFluidClient 的 [setLocalTestContainerId](/javascript/api/@microsoft/live-share/iteamsfluidclientoptions#@microsoft-live-share-iteamsfluidclientoptions-setlocaltestcontainerid) 和 [getLocalTestContainerId](/javascript/api/@microsoft/live-share/iteamsfluidclientoptions#@microsoft-live-share-iteamsfluidclientoptions-getlocaltestcontainerid) 选项自定义用于存储测试容器 ID 的策略。

## <a name="write-the-stage-view"></a>编写阶段视图

许多 Teams 会议扩展性应用程序旨在将 React 用于其视图框架，但这不是必需的。 例如，此示例使用标准 HTML/DOM 方法来呈现视图。

### <a name="start-with-a-static-view"></a>从静态视图开始

使用不带任何 Fluid 功能的本地数据轻松创建视图，然后通过更改应用的某些关键部分来添加 Fluid。

`renderStage` 函数在传递的 HTML 元素上添加了 `stageTemplate`，并在每次选择 **Roll** 按钮时创建一个工作的投掷骰子，并有一个随机的骰子值。 在接下来的几个步骤中将使用 `diceMap`。

```js
const stageTemplate = document.createElement("template");

stageTemplate["innerHTML"] = `
  <div class="wrapper">
    <div class="dice"></div>
    <button class="roll"> Roll </button>
  </div>
`;
function renderStage(diceMap, elem) {
  elem.appendChild(stageTemplate.content.cloneNode(true));
  const rollButton = elem.querySelector(".roll");
  const dice = elem.querySelector(".dice");

  rollButton.onclick = () => updateDice(Math.floor(Math.random() * 6) + 1);

  const updateDice = (value) => {
    // Unicode 0x2680-0x2685 are the sides of a die (⚀⚁⚂⚃⚄⚅).
    dice.textContent = String.fromCodePoint(0x267f + value);
  };
  updateDice(1);
}
```

## <a name="connect-stage-view-to-fluid-data"></a>将阶段视图连接到数据

### <a name="modify-fluid-data"></a>修改 Fluid 数据

若要开始在应用程序中使用 Fluid，首先要更改的是用户选择 `rollButton` 时发生的情况。 按钮不直接更新本地状态，而是更新 `diceMap` 中传入的 `value` 键中存储的数字。 由于 `diceMap` 是 Fluid `SharedMap`，因此更改将分发给所有客户端。 对 `diceMap` 的任何更改都将导致发出 `valueChanged` 事件，并且事件处理程序可以触发视图的更新。

此模式在 Fluid 中很常见，因为它使视图能够对本地和远程更改采用相同的行为方式。

```js
rollButton.onclick = () =>
  diceMap.set("dice-value-key", Math.floor(Math.random() * 6) + 1);
```

### <a name="rely-on-fluid-data"></a>依赖 Fluid 数据

需要进行的下一个更改是更改 `updateDice` 函数，使其不再接受任意值。 这意味着应用无法再直接修改本地骰子值。 而是在每次调用 `updateDice` 时从 `SharedMap` 检索值。

```js
const updateDice = () => {
  const diceValue = diceMap.get("dice-value-key");
  dice.textContent = String.fromCodePoint(0x267f + diceValue);
};
updateDice();
```

### <a name="handle-remote-changes"></a>处理远程更改

从 `diceMap` 返回的值只是时间快照。 若要使数据在更改时保持最新，必须在 `diceMap` 上设置事件处理程序，以便在每次发送 `valueChanged` 事件时调用 `updateDice`。 若要获取触发的事件列表以及传递给这些事件的值，请参阅 [SharedMap](https://fluidframework.com/docs/data-structures/map/)。

```js
diceMap.on("valueChanged", updateDice);
```

## <a name="write-the-side-panel-view"></a>编写侧面板视图

当用户在会议中打开应用时，会在侧面板中向用户显示侧面板视图，该视图通过选项卡 `contentUrl` 加载 `sidePanel` 帧上下文。 此视图的目标是让用户在将应用共享到会议阶段之前选择应用的内容。 对于 Live Share SDK 应用，侧面板视图也可用作应用的配套体验。 从侧面板视图调用 [ joinContainer()](/javascript/api/@microsoft/live-share/teamsfluidclient#@microsoft-live-share-teamsfluidclient-joincontainer) 将连接到阶段视图连接到的同一 Fluid 容器。 然后，此容器可用于与阶段视图通信。 确保与每个人的阶段视图 _和_ 侧面板视图通信。

示例的侧面板视图提示用户选择要暂存的共享按钮。

```js
const sidePanelTemplate = document.createElement("template");

sidePanelTemplate["innerHTML"] = `
  <style>
    .wrapper { text-align: center }
    .title { font-size: large; font-weight: bolder; }
    .text { font-size: medium; }
  </style>
  <div class="wrapper">
    <p class="title">Lets get started</p>
    <p class="text">Press the share to stage button to share Dice Roller to the meeting stage.</p>
  </div>
`;

function renderSidePanel(elem) {
  elem.appendChild(sidePanelTemplate.content.cloneNode(true));
}
```

## <a name="write-the-settings-view"></a>编写设置视图

通过应用清单中的 `configurationUrl` 加载的设置视图会在用户首次将应用添加到 Teams 会议时向用户显示。 此视图允许开发人员根据用户输入配置固定到会议的选项卡的 `contentUrl`。 即使不需要用户输入来设置 `contentUrl`，当前也需要此页。

> [!IMPORTANT]
> 选项卡 `settings` 上下文中不支持 Live Share SDK 的 [joinContainer()](/javascript/api/@microsoft/live-share/teamsfluidclient#@microsoft-live-share-teamsfluidclient-joincontainer)。

示例的设置视图提示用户选择保存按钮。

```js
const settingsTemplate = document.createElement("template");

settingsTemplate["innerHTML"] = `
  <style>
    .wrapper { text-align: center }
    .title { font-size: large; font-weight: bolder; }
    .text { font-size: medium; }
  </style>
  <div class="wrapper">
    <p class="title">Welcome to Dice Roller!</p>
    <p class="text">Press the save button to continue.</p>
  </div>
`;

function renderSettings(elem) {
  elem.appendChild(settingsTemplate.content.cloneNode(true));

  // Save the configurable tab
  pages.config.registerOnSaveHandler((saveEvent) => {
    pages.config.setConfig({
      websiteUrl: window.location.origin,
      contentUrl: window.location.origin + "?inTeams=1&view=content",
      entityId: "DiceRollerFluidLiveShare",
      suggestedDisplayName: "DiceRollerFluidLiveShare",
    });
    saveEvent.notifySuccess();
  });

  // Enable the Save button in config dialog
  pages.config.setValidityState(true);
}
```

## <a name="test-locally"></a>在本地测试

可以使用 `npm run start` 在本地测试应用。 有关详细信息，请参阅 [快速入门指南](./teams-live-share-quick-start.md)。

## <a name="test-in-teams"></a>在 Teams 中测试

使用 `npm run start` 开始在本地运行应用后，可以在 Teams 上测试应用。 若要在不部署的情况下测试应用，请下载并使用 [`ngrok`](https://ngrok.com/) 隧道服务。

### <a name="create-a-ngrok-tunnel-to-allow-teams-to-reach-your-app"></a>创建 ngrok 隧道以允许 Teams 访问你的应用

1. [下载 ngrok](https://ngrok.com/download)。

1. 使用 ngrok 创建具有端口 8080 的隧道。 运行以下命令：

   ```bash
    ngrok http 8080 --host-header=localhost
   ```

   将打开一个新的 ngrok 终端，其中包含一个新 URL，例如 `https:...ngrok.io`。 新 URL 是指向应用的隧道，需要在应用 `manifest.json` 中更新。

### <a name="create-the-app-package-to-sideload-into-teams"></a>创建应用包以旁加载到 Teams 中

1. 转到计算机上 `\live-share-sdk\samples\01.dice-roller` 的 Dice Roller 示例文件夹。 还可以从 GitHub 上的 Dice Roller 示例检查 [`.\manifest\manifest.json`](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller/manifest)。

1. 打开 manifest.json 并更新配置 URL。

   将 `https://<<BASE_URI_DOMAIN>>` 替换为 ngrok 中的 http 终结点。

1. 可以更新以下字段：

   - 将 `developer.name` 设置为你的姓名。
   - 使用网站更新 `developer.websiteUrl`。
   - 使用隐私策略更新 `developer.privacyUrl`。
   - 使用使用条款更新 `developer.termsOfUseUrl`。

1. 压缩清单文件夹的内容以创建 `manifest.zip`。 确保 `manifest.zip` 仅包含 `manifest.json` 源文件、 `color` 图标和 `outline` 图标。

   1. 在 Windows 上，选择 `.\manifest` 目录中的所有文件并对其进行压缩。

   > [!NOTE]
   >
   > - 不要压缩包含文件夹。
   > - 为 zip 文件提供描述性名称。 例如，`DiceRollerLiveShare`。

   有关清单的详细信息，请访问 [Teams 清单文档](../resources/schema/manifest-schema.md)

### <a name="sideload-your-app-into-a-meeting"></a>将应用旁加载到会议中

1. 打开 Teams。

1. 在 Teams 中从日历安排会议。 请确保至少邀请一位与会者参加会议。

1. 加入会议。

1. 在顶部的会议窗口中，选择“**+ 应用**” > “**管理应用**”。

1. 在“**管理应用**”窗格中，选择“**上传自定义应用**”。

   1. 如果看不到“**上传自定义应用**”选项，请按照 [说明](/microsoftteams/teams-custom-app-policies-and-settings) 在租户中启用自定义应用。

1. 从计算机中选择并上传 `manifest.zip` 文件。

1. 选择“**添加**”以将示例应用添加到会议中。

1. 选择“**+ 应用**”，在“**查找应用**”搜索框中键入 "Dice Roller"。

1. 选择应用以在会议中激活它。

1. 选择“保存”。

   Dice Roller 应用将添加到 Teams 会议面板。

1. 在侧面板中，选择要暂存的共享图标。 Teams 开始与会议阶段的用户进行实时同步。

   :::image type="content" source="../assets/images/teams-live-share/teams-live-share-to-stage.png" alt-text="共享到阶段图标":::

   你现在应该会在会议阶段看到骰子投掷。

   :::image type="content" source="../assets/images/teams-live-share/teams-live-share-meeting-stage.png" alt-text="会议阶段图像":::

受邀加入会议的用户可以在加入会议时在台上查看你的应用。

## <a name="deployment"></a>部署

准备好部署代码后，可以使用 [Teams 工具包](../toolkit/provision.md#provision-using-teams-toolkit) 或 [Teams 开发人员门户](https://dev.teams.microsoft.com/apps) 来预配和上传应用的 zip 文件。

> [!NOTE]
> 在上传或分发应用之前，需要将预配的 appId 添加到 `manifest.json`。

## <a name="code-samples"></a>代码示例

| 示例名称 | Description                                                     | JavaScript                                                                           |
| :---------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| 投掷骰子 | 启用所有连接的客户端以投掷骰子并查看结果。 | [View](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [核心功能](teams-live-share-capabilities.md)

## <a name="see-also"></a>另请参阅

- [GitHub 存储库](https://github.com/microsoft/live-share-sdk)
- [Live Share SDK 参考文档](/javascript/api/@microsoft/live-share/)
- [Live Share 媒体 SDK 参考文档](/javascript/api/@microsoft/live-share-media/)
- [Live Share 常见问题解答](teams-live-share-faq.md)
- [会议中的 Teams 应用](teams-apps-in-meetings.md)
