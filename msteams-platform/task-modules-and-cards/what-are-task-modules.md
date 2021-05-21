---
title: 什么是任务模块？
author: clearab
description: 添加模式弹出窗口体验，以从你的应用收集信息或向用户Microsoft Teams信息
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 23157e30ce25c2dfa1c21e7f5c4ddd4f735b660f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566837"
---
# <a name="task-modules"></a>任务模块

任务模块允许你在 Teams 应用程序中创建模式弹出体验。 在弹出窗口中，可以运行自己的自定义 HTML/JavaScript 代码，显示基于小部件（如 YouTube 或 Microsoft Stream 视频）或 `<iframe>` 显示 [自适应卡片](/adaptive-cards/)。 它们对于启动和完成任务或显示丰富的信息（如视频或仪表板）Power BI非常有用。 与选项卡或基于对话的自动程序体验相比，用户启动和完成任务通常更自然。

任务模块基于选项卡Microsoft Teams构建;它们实质上是弹出窗口中的一个选项卡。 它们使用相同的 SDK，因此如果你已生成选项卡，则你已经 90% 能够创建任务模块。

可通过 3 种方式调用任务模块：

* **频道或个人选项卡**：使用 Microsoft Teams Tabs SDK，可以从选项卡上的按钮、链接或菜单调用任务模块。此处详细介绍 [了这一点。](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* **自动程序**：从自动 [程序发送](~/task-modules-and-cards/cards/cards-reference.md) 的卡片上的按钮。 当你不需要频道中的每个人查看你正在使用机器人做什么时，这尤其有用。 例如，让用户在频道中回复投票时，看到创建该投票的记录并没有多大用处。 [此处详细介绍了这一点。](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* **在Teams** 链接之外：还可以创建 URL 以从任何位置调用任务模块。 [此处详细介绍了这一点。](#task-module-deep-link-syntax)

## <a name="task-module-looks-like"></a>任务模块类似于

下面是从没有彩色矩形和带编号的圆圈的自动程序 (调用任务模块时的外观，当然) ：

![任务模块示例](~/assets/images/task-module/task-module-example.png)

让我们演练一下：

1. 应用的[ `color` 图标](~/resources/schema/manifest-schema.md#icons)。
1. 应用[ `short` 的名称](~/resources/schema/manifest-schema.md#name)。
1. 任务模块的标题在 `title` [TaskInfo](#the-taskinfo-object)对象的 属性中指定。
1. 任务模块的关闭/取消按钮。 如果用户按此键，你的应用将收到一 `err` 个事件，如此处 [所述](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)。
    > [!Note]
    > 从自动程序调用任务模块时，当前无法检测此事件。
1. 如果正在使用 TaskInfo 对象的 属性加载自己的网页，则蓝色矩形是显示 `url` [网页的位置](#the-taskinfo-object)。 下面的任务模块 [大小调整部分提供了更多详细信息](#task-module-sizing) 。
1. 如果你要通过 TaskInfo 对象的 属性显示自适应卡片，则添加填充，否则你需要自己 `card` [处理。](#task-module-css-for-htmljavascript-task-modules) [](#the-taskinfo-object)
1. 自适应卡片按钮将在此处呈现。 如果正在使用自己的页面，则必须创建自己的按钮。

## <a name="overview-of-invoking-and-dismissing-task-modules"></a>调用和消除任务模块概述

可以从选项卡、聊天机器人或深层链接调用任务模块，其中显示的内容可以是 HTML 或自适应卡片，因此在如何调用任务模块以及如何处理用户交互的结果方面，存在很多灵活性。 下表总结了此操作的工作原理：

| **通过...** | **任务模块为 HTML/JavaScript** | **任务模块是自适应卡片** |
| --- | --- | --- |
| **选项卡中的 JavaScript** | 1. 将 Teams客户端 SDK 函数 `tasks.startTask()` 与可选回调 `submitHandler(err, result)` 函数一同使用。 <br/><br/> 2. 在任务模块代码中，当用户完成时，使用对象作为参数Teams SDK `tasks.submitTask()` `result` 函数。 如果在 `submitHandler` 中指定了回调 `tasks.startTask()` ，Teams使用 作为 `result` 参数调用它。<br/><br/> 3. 如果在调用 时出错，则改为 `tasks.startTask()` `submitHandler` 使用字符串调用 `err` 函数。 <br/><br/> 4. 还可以在呼叫 `completionBotId` 时指定 `teams.startTask()` - 在这种情况下 `result` ，会改为发送到机器人。 | 1. 使用 TaskInfo Teams并包含要显示在任务模块弹出窗口中的自适应卡片的 JSON 来调用客户端 SDK `tasks.startTask()` [](#the-taskinfo-object) `TaskInfo.card` 函数。 <br/><br/> 2. 如果在 中指定了回调，Teams如果调用时出错或用户关闭任务模块弹出窗口（使用右上角的 X）则使用字符串 `submitHandler` `tasks.startTask()` `err` `tasks.startTask()` 调用它。 <br/><br/> 3. 如果用户按下 Action.Submit 按钮，则其 `data` 对象将返回为 的值 `result` 。 |
| **自动程序卡按钮** | 1. 自动程序卡片按钮可以通过两种方式调用任务模块，具体取决于按钮的类型：深层链接 URL 或 `task/fetch` 发送消息。 有关链接 URL 工作深度的详细信息，请参阅下文。 <br/><br/> 2. 如果按钮的操作是自适应卡片) 的 (按钮类型，) 下的事件 (HTTP POST 将发送给机器人，机器人使用 `type` `task/fetch` HTTP `Action.Submit` 200 响应 POST，响应正文包含 `task/fetch invoke` [TaskInfo](#the-taskinfo-object)对象周围的包装器。 在通过 [task/fetch 调用任务模块时对此进行了详细说明](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-through-taskfetch)。<br/><br/> 3. Teams任务模块;用户完成后，调用 Teams SDK `tasks.submitTask()` 函数，将 对象 `result` 作为参数。 <br/><br/> 4. 机器人会收到 `task/submit invoke` 包含对象 `result` 的消息。 有三种不同的方法来响应消息：不执行任何操作 (任务成功完成) 、在弹出窗口中向用户显示消息，或调用另一个任务模块窗口 (即创建类似向导的体验 `task/submit`) 。 有关任务/提交 [的详细讨论中将详细讨论这三个选项](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 | 1. 与 Bot Framework 卡上的按钮类似，自适应卡片上的按钮支持两种调用任务模块的方法：带按钮的深层链接 URL 和使用 `Action.openUrl` `task/fetch` `Action.Submit` 按钮。 <br/><br/> 2. 具有自适应卡片的任务模块与 HTML/JavaScript 用例 (请参阅左侧) 。 主要区别在于，由于在使用自适应卡片时没有 JavaScript，因此无法调用 `tasks.submitTask()` 。 相反，Teams 对象，并返回作为 事件的有效负载， `data` `Action.Submit` 如此处 `task/submit` [所述](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 |
| **深层链接 URL** <br/>[URL 语法](#task-module-deep-link-syntax) | 1. Teams调用任务模块;在深层链接 `<iframe>` 的参数中指定的 内 `url` 出现的 URL。 没有 `submitHandler` 回调。 <br/><br/> 2. 在任务模块中页面的 JavaScript 内，调用 以使用对象作为参数关闭它，就像从选项卡或自动程序卡按钮调用它一 `tasks.submitTask()` `result` 样。 不过，完成逻辑略有不同。 如果你的完成逻辑驻留在客户端 (即如果没有自动程序) 则没有回调，因此任何完成逻辑都必须位于 调用 之前 `submitHandler` 的代码 `tasks.submitTask()` 。 调用错误仅通过控制台报告。 如果你有自动程序，可以在深层链接中指定参数，以 `completionBotId` 通过事件 `result` 发送 `task/submit` 对象。 | 1. Teams调用任务模块;自适应卡片的 JSON 卡正文指定为深层链接参数的 URL `card` 编码值。 <br/><br/> 2. 用户通过单击任务模块右上角的 X 或按卡片上的按钮来 `Action.Submit` 关闭任务模块。 由于没有要调用的，因此你必须有一个自动程序将自适应卡片 `submitHandler` 字段的值发送到。 使用深层 `completionBotId` 链接中的 参数指定通过事件将数据发送到的 `task/submit invoke` 自动程序。 |

## <a name="the-taskinfo-object"></a>TaskInfo 对象

`TaskInfo`对象包含任务模块的元数据。 对象定义如下所示。 你必须 **为** 嵌入 `url` 的 iFrame 或 `card` 自适应卡片定义 。

| 属性 | 类型 | 说明 |
| --- | --- | --- |
| `title` | string | 显示在应用程序名称下方以及应用程序图标的右侧。 |
| `height` | number or string | 它可以是表示任务模块的高度（以像素为单位）或 `small` 、 `medium` 或 `large` 。 [请参阅下文，了解如何处理高度和宽度](#task-module-sizing)。 |
| `width` | number or string | 它可以是表示任务模块的宽度（以像素为单位）或 `small` 、 `medium` 或 `large` 的数。 [请参阅下文，了解如何处理高度和宽度](#task-module-sizing)。 |
| `url` | 字符串 | 作为任务模块内部加载 `<iframe>` 的页面的 URL。 URL 的域必须在你的应用清单中的 [应用的 validDomains](~/resources/schema/manifest-schema.md#validdomains) 数组中。 |
| `card` | 自适应卡片或自适应卡片自动程序卡附件 | 要显示在任务模块中的自适应卡片的 JSON。 如果你从自动程序调用，则需要在 Bot Framework 对象中使用自适应卡片 `attachment` JSON。 从选项卡中，你只需使用自适应卡片。 [下面是一个示例。](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | 字符串 | 如果客户端不支持任务模块功能，此 URL 在浏览器选项卡中打开。 |
| `completionBotId` | 字符串 | 指定要发送用户与任务模块交互结果的自动程序应用 ID。 如果指定，机器人将收到事件负载中具有 `task/submit invoke` JSON 对象的事件。 |

> [!NOTE]
> 任务模块功能要求要加载的任何 URL 的域包含在应用清单的数组 `validDomains` 中。

## <a name="task-module-sizing"></a>任务模块大小调整

使用 和 `TaskInfo.width` 的 `TaskInfo.height` 整数将设置高度和宽度（以像素为单位）。 但是，根据团队窗口的大小和屏幕分辨率，在保持纵横比和宽度/高度比例 (按比例) 。

如果 和 为 ，或者上图中红色矩形的大小与可用空间的比例为 `TaskInfo.width` `TaskInfo.height` `"small"` `"medium"` `"large"` ：20%、50%、60%、20%、50%、66%。 `width` `height`

从选项卡调用的任务模块可以动态调整大小。 调用后 `tasks.startTask()` ，可以调用 newSize 对象的高度和宽度属性符合 `tasks.updateTask(newSize)` TaskInfo 规范（例如 (要求）。 `{ height: 'medium', width: 'medium' }`).

## <a name="task-module-css-for-htmljavascript-task-modules"></a>HTML/JavaScript 任务模块的任务模块 CSS

基于 HTML/JavaScript 的任务模块可以访问标题下方的整个任务模块区域。 虽然这提供了极大的灵活性，但如果你想要在边缘周围填充以与标头元素对齐，并避免不必要的滚动条，则需要提供正确的 CSS。 下面是几个用例的一些示例。

### <a name="example-1---youtube-video"></a>示例 1 - YouTube 视频

YouTube 提供在网页上嵌入视频的能力。 使用简单的存根网页很容易在任务模块中显示：

![YouTube 视频](~/assets/images/task-module/youtube-example.png)

下面是此页面的 HTML，不含 CSS：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  ⋮
</head>
<body>
  <div id="embed-container">
    <iframe width="1000" height="700" src="https://www.youtube.com/embed/rd0Rd8w3FZ0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen=""></iframe>
  </div>
</body>
</html>
```

CSS 如下所示：

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 95%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

### <a name="example-2---powerapp"></a>示例 2 - PowerApp

也可以使用相同的方法嵌入 PowerApp。 由于任何单个 PowerApp 的高度/宽度都是可自定义的，因此可能需要调整高度和宽度才能实现所需的演示文稿。

![资产管理 PowerApp](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

CSS 为：

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 94%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>自适应卡片或自适应卡片自动程序卡附件

如上所述，根据调用方式，你将需要使用自适应卡片或自适应卡片自动程序卡附件 (该附件只是包装在附件对象) `card` 中的自适应卡片。

从选项卡调用时，将需要使用自适应卡片。 下面是一个非常简单的示例：

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "text": "Here is a ninja cat:"
        },
        {
            "type": "Image",
            "url": "http://adaptivecards.io/content/cats/1.png",
            "size": "Medium"
        }
    ],
    "version": "1.0"
}
```

从自动程序调用时，将需要使用自适应卡片自动程序卡附件，如以下示例所示：

```json
{
    "contentType": "application/vnd.microsoft.card.adaptive",
    "content": {
        "type": "AdaptiveCard",
        "body": [
            {
                "type": "TextBlock",
                "text": "Here is a ninja cat:"
            },
            {
                "type": "Image",
                "url": "http://adaptivecards.io/content/cats/1.png",
                "size": "Medium"
            }
        ],
        "version": "1.0"
    }
}
```

你将需要记住是调用包含自动程序或选项卡中的自适应卡片的任务模块。

## <a name="task-module-deep-link-syntax"></a>任务模块深度链接语法

任务模块深层链接只是 [TaskInfo](#the-taskinfo-object) 对象的序列化，包含两条其他信息，以及可选的 `APP_ID` `BOT_APP_ID` ：

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

请参阅 [TaskInfo 对象](#the-taskinfo-object) ，了解数据类型以及 、 、 和 的允许 `<TaskInfo.url>` `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` 值 `<TaskInfo.title>` 。

> [!TIP]
> 请确保 URL 对深层链接进行编码，尤其是在使用参数 (`card` 例如，JavaScript[ `encodeURI()` 的 function) 。](https://www.w3schools.com/jsref/jsref_encodeURI.asp)

以下是 和 `APP_ID` 的信息 `BOT_APP_ID` ：

| 值 | 类型 | 是否必需？ | 说明 |
| --- | --- | --- | --- |
| `APP_ID` | string | 是 | [调用](~/resources/schema/manifest-schema.md#id)任务模块的应用的 ID。 的 [清单中的 validDomains](~/resources/schema/manifest-schema.md#validdomains) `APP_ID` 数组必须包含 `url` 的域的 if 位于 URL `url` 中。  (从选项卡或自动程序调用任务模块时，应用 ID 已已知，这就是它未包含在 `TaskInfo` .)  |
| `BOT_APP_ID` | string | 否 | 如果指定了 值，则对象通过消息 `completionBotId` `result` `task/submit invoke` 发送给指定的自动程序。 `BOT_APP_ID` 必须在应用清单中指定为自动程序，即不能只将其发送到任何自动程序。 |

请注意，它对于 和 相同有效，并且在许多情况下，如果应用有自动程序，因为建议将该应用用作应用的 `APP_ID` `BOT_APP_ID` ID（如果有）。

## <a name="keyboard-and-accessibility-guidelines"></a>键盘和辅助功能指南

对于基于 HTML/JavaScript 的任务模块，你有责任确保应用的任务模块可以与键盘一同使用。 屏幕阅读器程序还取决于使用键盘进行导航的能力。 从实际上说，这有两点意义：

1. 使用 HTML 标记中的 [tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) 属性控制哪些元素可以聚焦以及是否/在哪里参与顺序键盘导航 (通常使用 <kbd>Tab</kbd> 和 <kbd>Shift-Tab</kbd> 键) 。
2. 在 <kbd>JavaScript</kbd> 中为任务模块处理 Esc 键。 下面是一个显示如何执行此操作的代码示例：

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

Microsoft Teams可确保键盘导航从任务模块标头正常进入 HTML，反之亦然。

## <a name="code-sample"></a>代码示例
|**示例名称** | **说明** | **.NET** | **Node.js**|
|----------------|-----------------|--------------|----------------|
|Bots-V4 (任务模块)  | 用于创建任务模块的示例。 |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 
|任务模块示例 (选项卡 + Bots-V3)  | 用于创建任务模块的示例。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a>另请参阅

* [请求设备权限](../concepts/device-capabilities/native-device-permissions.md)
* [集成媒体功能](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [将 QR 或条形码扫描仪功能集成到 Teams](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [在 Teams 中集成位置Teams](../concepts/device-capabilities/location-capability.md)
