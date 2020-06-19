---
title: 什么是任务模块？
author: clearab
description: 添加模式弹出窗口体验，以便从 Microsoft 团队应用程序向用户收集或显示信息。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 22fdc7a9dab1ff6f27e2b0d144e54676b6cca50e
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801024"
---
# <a name="what-are-task-modules"></a>什么是任务模块？

任务模块使您能够在团队应用程序中创建模式弹出窗口体验。 在弹出式菜单中，您可以运行自己的自定义 HTML/JavaScript 代码，显示基于某个的 `<iframe>` 小组件（如 YouTube 或 Microsoft Stream 视频）或显示[自适应卡片](/adaptive-cards/)。 它们在启动和完成任务或显示丰富的信息（如视频或 Power BI 仪表板）时尤其有用。 与选项卡或基于对话的 bot 体验相比，启动和完成任务的用户的弹出体验通常更为自然。

任务模块是在 Microsoft 团队选项卡的基础上构建的;它们实质上是一个处于弹出窗口中的选项卡。 它们使用相同的 SDK，因此，如果您已经构建了一个选项卡，则您已经是能够创建任务模块的90%。

可以通过三种方式调用任务模块：

* **频道或个人选项卡。** 使用 Microsoft 团队选项卡 SDK，可以从选项卡上的按钮、链接或菜单调用任务模块。[此处将详细介绍这一点。](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* **Bot.** 从你的 bot 发送的[卡片](~/task-modules-and-cards/cards/cards-reference.md)上的按钮。 当你不需要频道中的每个人查看你使用机器人的内容时，这一点尤其有用。 例如，当用户在频道中响应轮询时，查看正在创建的轮询的记录是非常有用的。 [这里将对此进行详细介绍。](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* **来自深层链接的团队外部。** 您还可以创建 Url，从任何位置调用任务模块。 [这里将对此进行详细介绍。](#task-module-deep-link-syntax)

## <a name="what-a-task-module-looks-like"></a>任务模块的外观

下面是从 bot （当然不带彩色矩形和带编号的圆）调用时，任务模块的外观：

![任务模块示例](~/assets/images/task-module/task-module-example.png)

让我们浏览一下：

1. 您的应用程序[ `color` 图标](~/resources/schema/manifest-schema.md#icons)。
2. 您的应用程序的[ `short` 名称](~/resources/schema/manifest-schema.md#name)。
3. 在 `title` [TaskInfo 对象](#the-taskinfo-object)的属性中指定的任务模块的标题。
4. 任务模块的 "关闭/取消" 按钮。 如果用户按此方式，您的应用程序将 `err` 按[此处](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)所述接收事件。 （**注意：** 当从 bot 调用任务模块时，当前无法检测到此事件。）
5. 当您使用 `url` [TaskInfo 对象](#the-taskinfo-object)的属性加载自己的网页时，蓝色矩形是您的网页的显示位置。 下面的[任务模块 "调整大小](#task-module-sizing)" 部分中有更多详细信息。
6. 如果您通过 TaskInfo 对象的属性显示自适应卡片 `card` ， [TaskInfo object](#the-taskinfo-object)则会为您添加填充，否则您将需要[自己处理这](#task-module-css-for-htmljavascript-task-modules)种情况。
7. 自适应卡片按钮将呈现在此处。 如果您使用的是自己的页面，则必须创建自己的按钮。

## <a name="overview-of-invoking-and-dismissing-task-modules"></a>调用和解除关闭任务模块的概述

可以从选项卡、bot 或深层链接中调用任务模块，并且其中显示的内容可以是 HTML，也可以是自适应卡片，因此在如何调用它们以及如何处理用户交互的结果方面有很大的灵活性。 下表总结了这是如何工作的：

| **通过调用的 .。。** | **任务模块为 HTML/JavaScript** | **任务模块为自适应卡片** |
| --- | --- | --- |
| **选项卡中的 JavaScript** | 1. 将团队客户端 SDK 函数 `tasks.startTask()` 与可选 `submitHandler(err, result)` 回调函数结合使用 <br/><br/> 2. 在任务模块代码中，当用户完成时，调用团队 SDK 函数， `tasks.submitTask()` 并将 `result` 对象作为参数。 如果 `submitHandler` 在中指定了回调 `tasks.startTask()` ，则团队将使用 `result` 作为参数调用它。<br/><br/> 3. 如果调用时出现错误，则 `tasks.startTask()` `submitHandler` 使用字符串调用函数 `err` 。 <br/><br/> 4. 您还可以指定在 `completionBotId` 调用时 `teams.startTask()` `result` 改为发送到 bot 的条件。 | 1. 使用 TaskInfo 对象调用团队客户端 SDK 函数 `tasks.startTask()` ， [TaskInfo object](#the-taskinfo-object)并 `TaskInfo.card` 包含要在任务模块弹出菜单中显示的自适应卡片的 JSON。 <br/><br/> 2. 如果 `submitHandler` 在中指定了回调 `tasks.startTask()` ，则团队会在 `err` 调用时出现错误， `tasks.startTask()` 或者用户使用右上角的 X 关闭任务模块弹出菜单时，将调用该字符串。 <br/><br/> 3. 如果用户按下某个操作。 "提交" 按钮 `data` ，然后其对象将作为的值返回 `result` 。 |
| **Bot 卡按钮** | 1. Bot 卡片按钮（具体取决于按钮的类型）可以通过两种方式调用任务模块：深层链接 URL 或通过发送 `task/fetch` 邮件。 有关深层链接 Url 的工作原理，请参阅下文。 <br/><br/> 2. 如果按钮的操作 `type` 为 `task/fetch` （ `Action.Submit` 自适应卡片的按钮类型），则 `task/fetch invoke` 会将事件（封面下的 HTTP POST）发送到 bot，然后，bot 将使用 HTTP 200 和包含[TaskInfo 对象](#the-taskinfo-object)包装的响应正文对 POST 做出响应。 这将在[通过任务/提取调用任务模块](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch)中详细说明。<br/><br/> 3. 团队显示任务模块;当用户完成时，调用团队 SDK 函数， `tasks.submitTask()` 并将 `result` 对象作为参数。 <br/><br/> 4. 机器人 `task/submit invoke` 会收到包含该对象的邮件 `result` 。 您可以使用三种不同的方法来响应 `task/submit` 邮件：通过不执行任何操作（任务已成功完成）、在弹出窗口中向用户显示一条消息，或调用另一个任务模块窗口（如创建类似于向导的体验）。 [有关任务/提交的详细讨论中](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)详细介绍了这三个选项。 | 1. 与 Bot 框架卡上的按钮类似，自适应卡片上的按钮支持两种调用任务模块的方法：带有按钮的深层链接 Url `Action.openUrl` ，以及通过 `task/fetch` 使用 `Action.Submit` 按钮。 <br/><br/> 2. 具有自适应卡片的任务模块的工作方式与 HTML/JavaScript 情况非常相似（请参阅左图）。 主要区别在于，由于在使用自适应卡时没有 JavaScript，因此没有办法呼叫 `tasks.submitTask()` 。 相反，团队将获取 `data` 对象 `Action.Submit` ，并将其作为事件中的有效负载返回 `task/submit` ，如下所[here](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)述。 |
| **深层链接 URL** <br/>[URL 语法](#task-module-deep-link-syntax) | 1. 团队调用任务模块;在 `<iframe>` 深层链接的参数中指定的 URL 中显示的 URL `url` 。 没有 `submitHandler` 回调。 <br/><br/> 2. 在任务模块中的页面的 JavaScript 中，调用 `tasks.submitTask()` 以将 `result` 对象作为参数关闭，与从选项卡或机器人卡按钮调用它时相同。 但是，完成逻辑稍有不同。 如果完成逻辑驻留在客户端上（即没有 bot），则没有 `submitHandler` 回调，因此任何完成逻辑都必须位于调用前的代码中 `tasks.submitTask()` 。 仅通过控制台报告调用错误。 如果你有机器人，则可以 `completionBotId` 在 deep link 中指定用于通过事件发送对象的参数 `result` `task/submit` 。 | 1. 团队调用任务模块;将自适应卡片的 JSON 卡片正文指定为深层链接的参数的 URL 编码值 `card` 。 <br/><br/> 2. 用户通过单击任务模块右上角的 X 或按卡片上的按钮关闭任务模块 `Action.Submit` 。 由于没有 `submitHandler` 呼叫，您必须有用于将自适应卡片字段的值发送到的 bot。 您可以使用 `completionBotId` 深层链接中的参数指定通过事件将数据发送到的 bot `task/submit invoke` 。 |

> [!NOTE]
> 移动时不支持从 JavaScript 调用任务模块。

## <a name="the-taskinfo-object"></a>TaskInfo 对象

`TaskInfo`对象包含任务模块的元数据。 对象定义如下所示。 您**必须**定义 `url` （对于 en 嵌入 iFrame）或 `card` （对于自适应卡片）。

| 属性 | 类型 | 说明 |
| --- | --- | --- |
| `title` | string | 显示在应用程序名称下方和应用图标的右侧 |
| `height` | number or string | 该值可以是表示任务模块的高度（以像素为单位）或、或的数字 `small` `medium` `large` 。 [请参阅以下有关如何处理高度和宽度的说明](#task-module-sizing)。 |
| `width` | number or string | 该值可以是表示任务模块的宽度（以像素为单位）的数字，或者 `small` 、 `medium` 或 `large` 。 [请参阅以下有关如何处理高度和宽度的说明](#task-module-sizing)。 |
| `url` | string | 加载为任务模块内的页面的 URL `<iframe>` 。 URL 的域必须位于应用程序清单中的应用程序的[validDomains 数组](~/resources/schema/manifest-schema.md#validdomains)中。 |
| `card` | 自适应卡片或自适应卡片 bot 卡片附件 | 要显示在任务模块中的自适应卡片的 JSON。 如果您正在从 bot 进行调用，则需要在 Bot 框架对象中使用自适应卡 JSON `attachment` 。 在选项卡上，您只需使用自适应卡片。 [下面是一个示例。](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | 如果客户端不支持任务模块功能，则在浏览器选项卡中打开此 URL。 |
| `completionBotId` | string | 指定机器人应用程序 ID，以将用户与任务模块的交互结果发送到。 如果指定，则 bot 将 `task/submit invoke` 在事件负载中接收具有 JSON 对象的事件。 |

> [!NOTE]
> 任务模块功能要求您要加载的任何 Url 的域都包含在 `validDomains` 应用程序清单中的数组中。

## <a name="task-module-sizing"></a>任务模块大小调整

对使用的整数 `TaskInfo.width` 和 `TaskInfo.height` 将设置以像素为单位的高度和宽度。 但是，根据工作组窗口和屏幕分辨率的大小，它们将按比例缩小，同时保持纵横比（宽度/高度）。

如果 `TaskInfo.width` 和 `TaskInfo.height` 是 `"small"` ， `"medium"` 或者 `"large"` 上图中的红色矩形的大小是可用空间的比例：20%、50%、60% `width` 、20%、50%、66% `height` 。

从选项卡调用的任务模块可以动态调整大小。 调用后 `tasks.startTask()` ，您可以调用 `tasks.updateTask(newSize)` newSize 对象上的 height 和 width 属性符合 TaskInfo 规范（ex）。 `{ height: 'medium', width: 'medium' }`).

## <a name="task-module-css-for-htmljavascript-task-modules"></a>HTML/JavaScript 任务模块的任务模块 CSS

基于 HTML/JavaScript 的任务模块可以访问标题下的任务模块的整个区域。 虽然这提供了极大的灵活性，但如果您想要在边缘周围填充以与标头元素对齐并避免不必要的滚动条，则需要提供正确的 CSS。 下面是几个用例的一些示例。

### <a name="example-1---youtube-video"></a>示例 1-YouTube 视频

YouTube 提供了在网页上嵌入视频的功能。 使用简单的存根网页，可以很容易地在任务模块中显示此内容：

![YouTube 视频](~/assets/images/task-module/youtube-example.png)

以下是此页面的 HTML，不含 CSS：

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

### <a name="example-2---powerapp"></a>示例 2-PowerApp

也可以使用相同的方法嵌入 PowerApp。 由于任何单个 PowerApp 的高度/宽度都是可自定义的，因此您可能需要调整 "高度" 和 "宽度" 以实现所需的演示文稿。

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

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>自适应卡片或自适应卡片 bot 卡片附件

正如我们上面所述，根据您的调用方式， `card` 需要使用自适应卡片或自适应卡片 bot 卡片附件（只是包装在附件对象中的自适应卡）。

从选项卡调用时，需要使用自适应卡片。 下面是一个非常简单的示例：

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

当您从 bot 进行调用时，需要使用自适应卡 bot 卡片附件，如下例所示：

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

您需要记住是否要从 bot 或选项卡调用包含自适应卡片的任务模块。

## <a name="task-module-deep-link-syntax"></a>任务模块深层链接语法

Task module deep 链接只是对包含其他两条信息的[TaskInfo 对象](#the-taskinfo-object)进行序列化， `APP_ID` 也可以选择 `BOT_APP_ID` ：

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

有关[TaskInfo object](#the-taskinfo-object)数据类型以及、、、 `<TaskInfo.url>` `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` 和 `<TaskInfo.title>` 的允许值，请参阅 TaskInfo 对象。

> [!TIP]
> 确保 URL 对深层链接进行编码，尤其是在使用 `card` 参数时（例如，JavaScript 的[ `encodeURI()` 函数](https://www.w3schools.com/jsref/jsref_encodeURI.asp)）。

以下是有关和的 `APP_ID` 信息 `BOT_APP_ID` ：

| 值 | 类型 | 是否必需？ | 说明 |
| --- | --- | --- | --- |
| `APP_ID` | string | 是 | 调用任务模块的应用程序的[id](~/resources/schema/manifest-schema.md#id) 。 的清单中的[validDomains 数组](~/resources/schema/manifest-schema.md#validdomains) `APP_ID` 必须包含的域位于 `url` `url` URL 中。 （在从选项卡或 bot 中调用任务模块时，应用程序 ID 已已知，这就是不包含在中的原因 `TaskInfo` 。） |
| `BOT_APP_ID` | string | 否 | 如果 `completionBotId` 指定了一个值，则 `result` 会通过一封邮件将该对象发送 `task/submit invoke` 到指定的 bot。 `BOT_APP_ID`必须在应用程序清单中指定为 bot，即，不能仅将其发送到任何机器人。 |

请注意，它的有效期 `APP_ID` 和 `BOT_APP_ID` 相同，在许多情况下，如果应用程序中有自动程序的 ID，则会出现这种情况，如果存在，则使用该应用程序的 ID。

## <a name="keyboard-and-accessibility-guidelines"></a>键盘和辅助功能指南

使用基于 HTML/JavaScript 的任务模块，您有责任确保您的应用程序的任务模块可与键盘配合使用。 屏幕阅读器程序还取决于使用键盘导航的功能。 实际而言，这意味着两个问题：

1. 在 HTML 标记中使用[tabindex 属性](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex)来控制哪些元素可以获得焦点，以及它在顺序键盘导航（通常与<kbd>Tab</kbd>键和<kbd>Shift-tab</kbd>键）中参与的位置。
2. 处理任务模块的 JavaScript 中的<kbd>Esc</kbd>键。 下面的代码示例展示了如何执行此操作：

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

Microsoft 团队将确保键盘导航能够正常地从任务模块标题到 HTML，反之亦然。

## <a name="task-module-samples"></a>任务模块示例

* [Node.js/TypeScript 示例](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs)
* [C #/.NET 示例](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp)
