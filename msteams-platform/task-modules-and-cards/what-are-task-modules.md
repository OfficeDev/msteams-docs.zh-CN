---
title: 什么是任务模块？
author: clearab
description: 添加模式弹出窗口体验，以收集 Microsoft Teams 应用中的信息或向用户显示信息。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: d92da7e6def6d66efd2f94600b7b8f8847553701
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231657"
---
# <a name="what-are-task-modules"></a>什么是任务模块？

任务模块允许你在 Teams 应用程序中创建模式弹出体验。 在弹出窗口中，你可以运行自己的自定义 HTML/JavaScript 代码，显示基于小部件（如 YouTube 或 Microsoft Stream 视频）或 `<iframe>` 显示 [自适应卡片](/adaptive-cards/)。 它们对于启动和完成任务或显示丰富的信息（如视频或 Power BI 仪表板）特别有用。 与选项卡或基于对话的自动程序体验相比，弹出式体验对于用户启动和完成任务通常更自然。

任务模块基于 Microsoft Teams 选项卡构建;它们实质上是弹出窗口中的一个选项卡。 它们使用相同的 SDK，因此，如果你已生成选项卡，则 90% 已能够创建任务模块。

可以通过三种方式调用任务模块：

* **频道或个人选项卡。** 使用 Microsoft Teams 选项卡 SDK，可以从选项卡上的按钮、链接或菜单调用任务模块。此处详细介绍 [了这一点。](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* **机器人。** 从自动程序 [发送的](~/task-modules-and-cards/cards/cards-reference.md) 卡片上的按钮。 当你不需要频道中的每个人查看你使用机器人执行什么时，这尤其有用。 例如，当用户在频道中回复轮询时，查看所创建的轮询记录并不实用。 [此处详细介绍了这一点。](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* **来自深层链接的 Teams 外部。** 还可以创建 URL 以从任何位置调用任务模块。 [此处详细介绍了这一点。](#task-module-deep-link-syntax)

## <a name="what-a-task-module-looks-like"></a>任务模块的外观

下面是从没有彩色矩形和编号的圆圈的自动程序 (调用任务模块时的外观，当然) ：

![任务模块示例](~/assets/images/task-module/task-module-example.png)

让我们演练一下：

1. 应用的[ `color` 图标](~/resources/schema/manifest-schema.md#icons)。
2. 应用[ `short` 的名称](~/resources/schema/manifest-schema.md#name)。
3. 任务模块的标题在 `title` [TaskInfo 对象的属性中指定](#the-taskinfo-object)。
4. 任务模块的关闭/取消按钮。 如果用户按此键，你的应用将收到 `err` 一个事件，如下 [所述](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)。  (**注意：** 当前无法从 bot.) 
5. 如果使用 TaskInfo 对象的属性加载自己的网页，则蓝色矩形是网页的 `url` [显示位置](#the-taskinfo-object)。 下面的任务模块 [大小调整部分中提供了更多详细信息](#task-module-sizing) 。
6. 如果通过 TaskInfo 对象的属性显示自适应卡片，则添加填充，否则需要自己 `card` [处理。](#task-module-css-for-htmljavascript-task-modules) [](#the-taskinfo-object)
7. 自适应卡片按钮将在此处呈现。 如果你使用的是自己的页面，则必须创建自己的按钮。

## <a name="overview-of-invoking-and-dismissing-task-modules"></a>调用和消除任务模块概述

可以从选项卡、自动程序或深层链接调用任务模块，其中显示的内容可以是 HTML 或自适应卡片，因此在如何调用任务模块以及如何处理用户交互的结果方面有很多灵活性。 下表总结了此操作的工作原理：

| **通过...** | **任务模块为 HTML/JavaScript** | **任务模块为自适应卡片** |
| --- | --- | --- |
| **选项卡中的 JavaScript** | 1. 将 Teams 客户端 SDK 函数与 `tasks.startTask()` 可选回调 `submitHandler(err, result)` 函数一同使用 <br/><br/> 2. 在任务模块代码中，当用户完成时，使用对象作为参数调用 Teams SDK `tasks.submitTask()` `result` 函数。 如果在 `submitHandler` 中指定了回调 `tasks.startTask()` ，Teams 会使用参数 `result` 调用它。<br/><br/> 3. 如果在调用时出错，则改为 `tasks.startTask()` `submitHandler` 使用字符串 `err` 调用函数。 <br/><br/> 4. 还可以指定呼叫 `completionBotId` 时 - 在这种情况下，改为发送到 `teams.startTask()` `result` 自动程序。 | 1. 使用 TaskInfo 对象并包含要显示在任务模块弹出窗口中的自适应卡片的 JSON 调用 Teams 客户端 SDK `tasks.startTask()` [](#the-taskinfo-object) `TaskInfo.card` 函数。 <br/><br/> 2. 如果在调用时出现错误，或者用户使用右上角的 X 关闭任务模块弹出窗口，则 Teams 会使用字符串调用 `submitHandler` `tasks.startTask()` `err` `tasks.startTask()` 它。 <br/><br/> 3. 如果用户按下 Action.Submit 按钮，则其对象作为 `data` `result` 值返回。 |
| **自动程序卡片按钮** | 1. 自动程序卡片按钮（具体取决于按钮类型）可以通过两种方式调用任务模块：深层链接 URL 或 `task/fetch` 发送消息。 请参阅下文，了解链接 URL 的深入工作。 <br/><br/> 2. 如果按钮的操作是自适应卡片) 的 (按钮类型，则 (会向自动程序发送一个事件) 下的 HTTP POST，机器人使用 `type` `task/fetch` HTTP `Action.Submit` 200 响应 POST，响应正文包含 `task/fetch invoke` [TaskInfo](#the-taskinfo-object)对象周围的包装器。 这将详细介绍通过任务/提取[调用任务模块。](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch)<br/><br/> 3. Teams 显示任务模块;用户完成后，使用对象作为参数调用 Teams SDK `tasks.submitTask()` `result` 函数。 <br/><br/> 4. 自动程序收到 `task/submit invoke` 包含该对象 `result` 的消息。 有三种不同的方法来响应消息：不执行任何操作 (任务成功完成) ，在弹出窗口中向用户显示消息，或调用另一个任务模块窗口 (例如创建类似向导的体验 `task/submit`) 。 在有关任务 [/提交的详细讨论中，将详细讨论这三个选项](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 | 1. 与 Bot Framework 卡上的按钮类似，自适应卡片上的按钮支持两种调用任务模块的方法：包含按钮的深层链接 URL 以及 `Action.openUrl` `task/fetch` 通过使用 `Action.Submit` 按钮。 <br/><br/> 2. 具有自适应卡片的任务模块的运行方式与 HTML/JavaScript 用例 (左) 。 主要区别在于，由于在使用自适应卡片时没有 JavaScript，因此无法调用 `tasks.submitTask()` 。 相反，Teams 会从对象中取值，并返回该对象作为事件的有效负载， `data` `Action.Submit` `task/submit` 如此处 [所述](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 |
| **深层链接 URL** <br/>[URL 语法](#task-module-deep-link-syntax) | 1. Teams 调用任务模块;在深层链接的参数 `<iframe>` 中指定的内部出现的 `url` URL。 没有 `submitHandler` 回调。 <br/><br/> 2. 在任务模块中页面的 JavaScript 中，调用以将对象作为参数关闭它，与从选项卡或自动程序卡按钮调用对象 `tasks.submitTask()` `result` 时相同。 但是，完成逻辑略有不同。 如果完成逻辑驻留在客户端 (即如果没有自动程序) 则没有回调，因此任何完成逻辑都必须位于调用 `submitHandler` 之前的代码。 `tasks.submitTask()` 仅通过控制台报告调用错误。 如果你有自动程序，可以在深层链接中指定参数以 `completionBotId` 通过事件 `result` 发送 `task/submit` 对象。 | 1. Teams 调用任务模块;自适应卡片的 JSON 卡正文指定为深层链接参数的 URL `card` 编码值。 <br/><br/> 2. 用户通过单击任务模块右上角的 X 或按卡片上的按钮来关闭任务 `Action.Submit` 模块。 由于没有要调用的字段，因此你必须有一个自动程序将自适应 `submitHandler` 卡片字段的值发送到。 使用深层链接中的参数指定通过事件将数据 `completionBotId` 发送到的 `task/submit invoke` 自动程序。 |

> [!NOTE]
> 移动版不支持从 JavaScript 调用任务模块。

## <a name="the-taskinfo-object"></a>TaskInfo 对象

该对象 `TaskInfo` 包含任务模块的元数据。 对象定义如下所示。 你必须 **为** 嵌入 `url` 的 iFrame (定义) ， (为自适应卡片 `card`) 。

| 属性 | 类型 | 说明 |
| --- | --- | --- |
| `title` | string | 显示在应用名称下方，并出现在应用图标的右侧 |
| `height` | number or string | 它可以是表示任务模块的高度（以像素为单位）或 `small` ， `medium` 或 `large` 。 [请参阅下文，了解如何处理高度和宽度](#task-module-sizing)。 |
| `width` | number or string | 它可以是表示任务模块的宽度（以像素为单位）或 `small` ， `medium` 或 `large` 。 [请参阅下文，了解如何处理高度和宽度](#task-module-sizing)。 |
| `url` | string | 作为任务模块内部加载 `<iframe>` 的页面的 URL。 URL 的域必须在你的应用清单 [中的应用的 validDomains](~/resources/schema/manifest-schema.md#validdomains) 数组中。 |
| `card` | 自适应卡片或自适应卡片自动程序卡附件 | 要显示在任务模块中的自适应卡片的 JSON。 如果从机器人调用，则需要在 Bot Framework 对象中使用自适应卡片 `attachment` JSON。 从选项卡中，你只需使用自适应卡片。 [下面是一个示例。](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | 如果客户端不支持任务模块功能，则此 URL 在浏览器选项卡中打开。 |
| `completionBotId` | string | 指定要发送用户与任务模块交互结果的自动程序应用 ID。 如果指定，机器人将在事件有效负载中接收 `task/submit invoke` 包含 JSON 对象的事件。 |

> [!NOTE]
> 任务模块功能要求要加载的任何 URL 的域包含在应用清单的数组 `validDomains` 中。

## <a name="task-module-sizing"></a>任务模块大小调整

使用整数 `TaskInfo.width` 和 `TaskInfo.height` 将设置高度和宽度（以像素为单位）。 但是，根据团队窗口的大小和屏幕分辨率，它们将会按比例减少，同时保持纵横比 (宽度/高度) 。

If and are ， or the size of the red rectangle in the above is a proportion of the available `TaskInfo.width` `TaskInfo.height` `"small"` `"medium"` `"large"` space： 20%， 50%， 60% for `width` and 20%， 50%， 66% for `height` .

从选项卡调用的任务模块可以动态调整大小。 调用后 `tasks.startTask()` ，可以调用 newSize 对象的高度和宽度属性符合 `tasks.updateTask(newSize)` TaskInfo 规范 (位置。 `{ height: 'medium', width: 'medium' }`).

## <a name="task-module-css-for-htmljavascript-task-modules"></a>HTML/JavaScript 任务模块的任务模块 CSS

基于 HTML/JavaScript 的任务模块可以访问标题下的任务模块的整个区域。 虽然这提供了极大的灵活性，但如果希望边缘周围的填充与页眉元素对齐，并避免不必要的滚动条，则需要提供正确的 CSS。 下面是几个用例的一些示例。

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

您也可以使用相同的方法嵌入 PowerApp。 由于任何单个 PowerApp 的高度/宽度都是可自定义的，因此可能需要调整高度和宽度才能实现所需的演示文稿。

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

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>自适应卡或自适应卡片自动程序卡附件

如上所述，根据调用方式，你将需要使用自适应卡片或自适应卡片自动程序卡附件 (该附件只是包装在附件对象) 中的自适应卡片。 `card`

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

当你从机器人调用时，你将需要使用自适应卡片自动程序卡附件，如以下示例所示：

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

## <a name="task-module-deep-link-syntax"></a>任务模块深层链接语法

任务模块深层链接只是包含其他两条信息的[TaskInfo](#the-taskinfo-object)对象的序列化，并且 `APP_ID` 可选： `BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

有关[数据类型和允许](#the-taskinfo-object)的值，请参阅 TaskInfo 对象，以及 `<TaskInfo.url>` 。 `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>`

> [!TIP]
> 请确保 URL 对深层链接进行编码，尤其是在使用参数 (`card` 例如，JavaScript[ `encodeURI()` 的函数) 。](https://www.w3schools.com/jsref/jsref_encodeURI.asp)

以下是有关和 `APP_ID` `BOT_APP_ID` 的信息：

| 值 | 类型 | 是否必需？ | 说明 |
| --- | --- | --- | --- |
| `APP_ID` | string | 是 | [调用](~/resources/schema/manifest-schema.md#id)任务模块的应用的 ID。 [清单中的 validDomains](~/resources/schema/manifest-schema.md#validdomains)数组 `APP_ID` 必须包含 if `url` `url` 的域。  (从选项卡或自动程序调用任务模块时，应用 ID 已已知，这就是它未包含在 `TaskInfo` .)  |
| `BOT_APP_ID` | string | 否 | 如果指定了值 `completionBotId` ，则对象通过消息发送给 `result` `task/submit invoke` 指定的自动程序。 `BOT_APP_ID` 必须指定为应用清单中的自动程序，即不能只将其发送到任何自动程序。 |

请注意，它有效且相同，并且在许多情况下，如果应用具有自动程序，因为建议在有自动程序时将该应用用作 `APP_ID` `BOT_APP_ID` 应用的 ID。

## <a name="keyboard-and-accessibility-guidelines"></a>键盘和辅助功能指南

对于基于 HTML/JavaScript 的任务模块，你有责任确保应用的任务模块可以与键盘一同使用。 屏幕阅读器程序还取决于使用键盘导航的能力。 从实践上说，这意味着两点：

1. 使用 HTML 标记中的[tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex)属性控制哪些元素可以聚焦以及是否/在何处参与顺序键盘导航 (通常使用 Tab 键和<kbd>Shift-Tab</kbd>键) 。 <kbd></kbd>
2. 处理任务模块的 JavaScript 中的 <kbd>Esc</kbd> 键。 下面是显示如何执行此操作的代码示例：

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

Microsoft Teams 将确保键盘导航从任务模块标头正常转换为 HTML，反之亦然。

## <a name="task-module-samples"></a>任务模块示例

* [Node.js/TypeScript 示例](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs)
* [C#/.NET 示例](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp)

> [!div class="nextstepaction"]
> [了解更多信息：请求设备权限](../concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
> [了解更多信息：集成媒体功能](../concepts/device-capabilities/mobile-camera-image-permissions.md)
