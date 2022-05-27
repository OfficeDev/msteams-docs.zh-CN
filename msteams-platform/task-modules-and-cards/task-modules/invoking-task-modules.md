---
title: 调用和关闭任务模块
description: 了解如何使用代码示例调用和关闭任务模块、任务信息对象、任务模块大小调整、任务模块深层链接语法
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 3b33d553849376da73b3269ac9a5c0a551d6074d
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757302"
---
# <a name="invoke-and-dismiss-task-modules"></a>调用和关闭任务模块

可以从选项卡、机器人或深层链接调用任务模块。 响应可以是 HTML、JavaScript 或自适应卡片。 在如何调用任务模块以及如何处理用户交互的响应方面有许多灵活性。 下表总结了其工作原理：

| 调用方式 | 具有 HTML 或 JavaScript 的任务模块 | 具有自适应卡片的任务模块 |
| --- | --- | --- |
| 选项卡中的 JavaScript | 1. 将 Teams 客户端 SDK 函数 `tasks.startTask()` 与可选 `submitHandler(err, result)` 回调函数一起使用。 <br/><br/> 2. 在任务模块代码中，当用户已执行操作时，使用 `result` 对象作为参数调用 Teams SDK 函数`tasks.submitTask()`。 如果在 `tasks.startTask()` 中指定了 `submitHandler` 回调，Teams 会使用 `result` 作为参数调用它。 如果调用 `tasks.startTask()` 时出错，则使用 `err` 字符串调用 `submitHandler` 函数。 <br/><br/> 3. 也可以在调用 `teams.startTask()` 时指定 `completionBotId`。 然后将 `result` 发送到机器人。 | 1. 使用 [TaskInfo 对象](#the-taskinfo-object) 和 `TaskInfo.card` 调用 Teams 客户端 SDK 函数 `tasks.startTask()`，其中包含要在任务模块弹出窗口中显示的自适应卡片的 JSON。 <br/><br/> 2. 如果在 `tasks.startTask()` 中指定了 `submitHandler` 回调，调用 `tasks.startTask()` 时出现错误，或者用户使用右上角的 X 关闭任务模块弹出窗口，Teams 会使用 `err` 字符串调用它。 <br/><br/> 3. 如果用户按下 `Action.Submit` 按钮，则其 `data` 对象将作为 `result` 的值返回。 |
| 机器人卡片按钮 | 1. 机器人卡片按钮（具体取决于按钮的类型）可以通过两种方式调用任务模块：深层链接 URL 或发送 `task/fetch` 消息。 <br/><br/> 2. 如果按钮的操作 `type` 是 `task/fetch`，即自适应卡片的 `Action.Submit` 按钮类型，则会将为 HTTP POST 的 `task/fetch invoke` 事件发送到机器人。 机器人使用 HTTP 200 响应 POST，响应正文包含围绕 [TaskInfo 对象](#the-taskinfo-object)的包装器。 有关详细信息，请参阅[使用 `task/fetch` 调用任务模块](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch)。 Teams 将显示任务模块。 <br/><br/> 3. 用户执行操作后，使用 `result` 对象作为参数调用 Teams SDK 函数`tasks.submitTask()`。 机器人接收包含 `result` 对象的 `task/submit invoke` 消息。 <br/><br/> 4. 可通过三种不同的方式来响应 `task/submit` 消息：不执行任何操作，成功已完成任务；在弹出窗口中向用户显示消息；或者调用另一个任务模块窗口。 有关详细信息，请参阅[有关 `task/submit` 的详细讨论](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 | <ul><li> 与 Bot Framework 卡片上的按钮一样，自适应卡片上的按钮支持两种调用任务模块的方式：使用 `Action.openUrl` 按钮通过深层链接 URL，以及使用 `Action.Submit` 按钮通过 `task/fetch`。 </li></ul> <br/><br/> <ul><li> 使用自适应卡片的任务模块的工作方式与 HTML 或 JavaScript 大小写类似。 主要区别在于，由于使用自适应卡片时没有 JavaScript，因此无法调用 `tasks.submitTask()`。 相反，Teams 从 `Action.Submit` 获取 `data` 对象并将其作为 `task/submit` 事件的有效负载返回。 有关详细信息，请参阅 [`task/submit` 的灵活性](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 </li></ul> |
| 深层链接 URL <br/>[URL 语法](#task-module-deep-link-syntax) | 1. Teams 调用任务模块，该模块是出现在深层链接的 `url` 参数中指定的 `<iframe>` 内的 URL。 没有 `submitHandler` 回调。 <br/><br/> 2. 在任务模块中页面的 JavaScript 中，调用 `tasks.submitTask()` 以使用 `result` 对象作为参数来关闭它，与从选项卡或机器人卡片按钮调用它时相同。 但是，完成逻辑略有不同。 如果完成逻辑位于没有机器人的客户端上，则没有 `submitHandler` 回调，因此任何完成逻辑都必须位于调用 `tasks.submitTask()`之前的代码中。 调用错误仅通过控制台报告。 如果有机器人，则可以在深层链接中指定 `completionBotId` 参数以通过 `task/submit` 事件发送 `result` 对象。 | 1. Teams 调用任务模块，该模块是自适应卡片的 JSON 卡片正文，被指定为深度链接的 `card` 参数的 URL 编码值。 <br/><br/> 2. 用户通过选择任务模块右上角的 X 或按卡片上的 `Action.Submit` 按钮来关闭任务模块。 由于无法 `submitHandler` 调用，因此用户必须有一个机器人才能发送自适应卡片字段的值。 用户必须使用深层链接中的 `completionBotId` 参数来指定要使用 `task/submit invoke` 事件向其发送数据的机器人。 |

下一部分指定为任务模块定义某些属性的 `TaskInfo` 对象。

## <a name="the-taskinfo-object"></a>TaskInfo 对象

`TaskInfo` 对象包含任务模块的元数据。 为嵌入式 iFrame 定义 `url` 或为自适应卡片定义 `card`。 下表提供了对象定义：

| 属性 | 类型 | 说明 |
| --- | --- | --- |
| `title` | string | 此属性显示在应用名称下方和应用图标右侧。 |
| `height` | number or string | 此属性可以是一个数字，表示任务模块的高度（以像素为单位），也可以是 `small`、`medium` 或 `large`。 有关详细信息，请参阅[任务模块大小调整](#task-module-sizing)。 |
| `width` | number or string | 此属性可以是一个数字，表示任务模块的宽度（以像素为单位），也可以是 `small`、`medium` 或 `large`。 有关详细信息，请参阅[任务模块大小调整](#task-module-sizing)。 |
| `url` | string | 此属性是在任务模块内作为 `<iframe>` 加载的页面的 URL。 URL 的域必须位于应用清单中应用的 [validDomains 数组](~/resources/schema/manifest-schema.md#validdomains)中。 |
| `card` | 自适应卡片或自适应卡片机器人卡片附件 | 此属性是要在任务模块中显示的自适应卡片的 JSON。 如果用户从机器人调用，请在 Bot Framework `attachment` 对象中使用自适应卡片 JSON。 在选项卡中，用户必须使用自适应卡片。 有关详细信息，请参阅[自适应卡片或自适应卡片机器人卡片附件](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | 如果客户端不支持任务模块功能，此属性将在浏览器选项卡中打开 URL。 |
| `completionBotId` | string | 此属性指定机器人应用 ID，用于发送用户与任务模块交互的结果。 如果指定，机器人将接收事件有效负载中包含 JSON 对象的 `task/submit invoke` 事件。 |

> [!NOTE]
> 任务模块功能要求要加载的任何 URL 的域都包含在应用清单的 `validDomains` 数组中。

下一部分指定任务模块大小，使用户能够设置任务模块的高度和宽度。

## <a name="task-module-sizing"></a>任务模块大小调整

对 `TaskInfo.width` 和 `TaskInfo.height` 使用整数，以像素为单位设置任务模块的高度和宽度。 但是，根据团队的窗口大小和屏幕分辨率，它们会按比例减少，同时保持宽度或高度的纵横比。

如果 `TaskInfo.width` 和 `TaskInfo.height` 为 `"small"`、`"medium"` 或 `"large"`，则下图中红色矩形的大小是可用空间的比例，`width` 分别为 20%、50% 和 60%，`height` 分别为 20%、50% 和 66%：

:::image type="content" source="../../assets/images/task-module/task-module-example.png" alt-text="任务模块示例":::

可以动态调整从选项卡调用的任务模块的大小。 调用 `tasks.startTask()` 后，可以调用 `tasks.updateTask(newSize)`，其中 newSize 对象的 height 和 width 属性符合 TaskInfo 规范，例如 `{ height: 'medium', width: 'medium' }`。

下一部分提供了在 YouTube 视频和 PowerApp 中嵌入任务模块的示例。

## <a name="task-module-css-for-html-or-javascript-task-modules"></a>HTML 或 JavaScript 任务模块的任务模块 CSS

基于 HTML 或 JavaScript 的任务模块可以访问标题下方任务模块的整个区域。 虽然这提供了很大的灵活性，但如果希望在边缘周围填充以与标题元素对齐并避免不必要的滚动条，则用户必须提供正确的 CSS。 接下来的部分为一些用例提供了一些示例。

### <a name="example-1-youtube-video"></a>示例 1：YouTube 视频

YouTube 提供在网页上嵌入视频的功能。 使用简单的存根网页在任务模块中的网页上嵌入视频很容易。

:::image type="content" source="../../assets/images/task-module/youtube-example.png" alt-text="Youtube 示例":::

以下代码提供了没有 CSS 的网页的 HTML 示例：

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

以下代码提供了 CSS 示例：

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

### <a name="example-2-powerapp"></a>示例 2：PowerApp

用户也可以使用相同的方法来嵌入 PowerApp。 由于任何单个 PowerApp 的高度或宽度都是可自定义的，因此用户可以调整高度和宽度来实现所需的演示。

:::image type="content" source="../../assets/images/task-module/powerapp-example.png" alt-text="powerapp":::

以下代码提供了 PowerApp 的 HTML 示例：

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

以下代码提供了 CSS 示例：

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

下一部分提供有关使用自适应卡片或自适应卡片机器人卡片附件调用卡片的详细信息。

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>自适应卡片或自适应卡片机器人卡片附件

根据调用 `card`方式，必须使用自适应卡片或自适应卡片机器人卡附件，即包装在附件对象中的自适应卡片。

从选项卡调用时，用户必须使用自适应卡片。

以下代码提供了自适应卡片的示例：

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

以下代码提供了从机器人调用自适应卡片机器人卡附件的示例：

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

下一部分提供有关任务模块深层链接语法的详细信息，包括 `TaskInfo` 对象以及 `APP_ID` 和 `BOT_APP_ID`。

## <a name="task-module-deep-link-syntax"></a>任务模块深层链接语法

任务模块深层链接是 TaskInfo 对象的序列化，具有以下两个其他详细信息：`APP_ID` 和 `BOT_APP_ID`（可选）：

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

有关 `<TaskInfo.url>`、`<TaskInfo.card>`、`<TaskInfo.height>`、`<TaskInfo.width>` 和 `<TaskInfo.title>` 的数据类型和允许的值，请参阅 [TaskInfo 对象](#the-taskinfo-object)。

> [!TIP]
> 使用 `card` 参数时对深层链接进行 URL 编码，例如 JavaScript 的 [`encodeURI()` 函数](https://www.w3schools.com/jsref/jsref_encodeURI.asp)。

下表提供了有关 `APP_ID` 和 `BOT_APP_ID` 的信息：

| 值 | 类型 | 必需 | 说明 |
| --- | --- | --- | --- |
| `APP_ID` | string | 是 | 调用任务模块的应用的 [ID](~/resources/schema/manifest-schema.md#id)。 如果 `url` 在 URL 中，则 `APP_ID` 清单中的 [validDomains 数组](~/resources/schema/manifest-schema.md#validdomains)必须包含 `url` 的域。 当从选项卡或机器人调用任务模块时，应用 ID 已经知道，这就是为什么它不包含在其中 `TaskInfo`的原因。 |
| `BOT_APP_ID` | string | 否 | 如果指定了 `completionBotId` 的值，则使用 `task/submit invoke` 消息将 `result` 对象发送到指定的机器人。 `BOT_APP_ID` 必须在应用清单中指定为机器人，即不能将其发送到任何机器人。 |

> [!NOTE]
> 如果应用有建议的机器人用作应用的 ID（如果有），`APP_ID` 和 `BOT_APP_ID` 在许多情况下可以是相同的。

下一部分提供有关将键盘与应用的任务模块配合使用的详细信息。

## <a name="keyboard-and-accessibility-guidelines"></a>键盘和辅助功能指南

对于基于 HTML 或 JavaScript 的任务模块，必须确保应用的任务模块可以与键盘一起使用。 屏幕阅读器程序还依赖于使用键盘进行导航的能力。 这包括以下两个事项：

* 在 HTML 标记中使用 [tabindex 属性](https://developer.mozilla.org/docs/Web/HTML/Global_attributes/tabindex)来控制可以聚焦的元素。 此外，使用 tabindex 属性来标识它通常使用 <kbd>Tab</kbd> 和 <kbd>Shift-Tab</kbd> 键参与顺序键盘导航的位置。
* 在任务模块的 JavaScript 中处理 <kbd>Esc</kbd> 键。 以下代码提供了如何处理 <kbd>Esc</kbd> 键的示例：

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

Microsoft Teams 可确保键盘导航从任务模块标题到 HTML 中正常工作，反之亦然。

## <a name="code-sample"></a>代码示例

|示例名称 | Description | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|任务模块示例机器人-V4 | 用于创建任务模块的示例。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|任务模块示例选项卡和机器人 V3 | 用于创建任务模块的示例。 |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [在选项卡中使用任务模块](~/task-modules-and-cards/task-modules/task-modules-tabs.md)

## <a name="see-also"></a>另请参阅

* [请求设备权限](~/concepts/device-capabilities/native-device-permissions.md)
* [集成媒体功能](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [在 Teams 中集成 QR 或条形码扫描程序功能](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [在 Teams 中集成位置功能](~/concepts/device-capabilities/location-capability.md)
