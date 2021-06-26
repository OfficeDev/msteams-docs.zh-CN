---
title: 调用和消除任务模块
description: 调用和消除任务模块。
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: a23d5cee3f13967772a4b58ed973bf08906e36a6
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140767"
---
# <a name="invoke-and-dismiss-task-modules"></a>调用和消除任务模块

可以从选项卡、自动程序或深层链接调用任务模块。 响应可以是 HTML、JavaScript 或自适应卡片。 在如何调用任务模块以及如何处理用户交互的响应方面，存在很多灵活性。 下表总结了此操作的工作原理：

| 使用 调用 | 包含 HTML 或 JavaScript 的任务模块 | 具有自适应卡片的任务模块 |
| --- | --- | --- |
| 选项卡中的 JavaScript | 1. 将 Teams客户端 SDK 函数 `tasks.startTask()` 与可选回调 `submitHandler(err, result)` 函数一同使用。 <br/><br/> 2. 在任务模块代码中，当用户已执行这些操作时，Teams对象作为参数调用 SDK `tasks.submitTask()` `result` 函数。 如果在 `submitHandler` 中指定了回调 `tasks.startTask()` ，Teams使用 作为 `result` 参数调用它。 如果在调用 时出错，则 `tasks.startTask()` `submitHandler` 改为使用字符串调用 `err` 函数。 <br/><br/> 3.还可以在调用 时 `completionBotId` 指定 `teams.startTask()` 。 然后 `result` ，将 改为发送到自动程序。 | 1. 使用 TaskInfo Teams包含要显示在任务模块弹出窗口中的自适应卡片的 JSON 来调用客户端 SDK `tasks.startTask()` [](#the-taskinfo-object) `TaskInfo.card` 函数。 <br/><br/> 2. 如果在 中指定了回调，Teams如果调用时出错或者用户关闭任务模块弹出窗口（使用右上角的 `submitHandler` `tasks.startTask()` `err` X）以字符串调用它 `tasks.startTask()` 。 <br/><br/> 3. 如果用户按下某个 `Action.Submit` 按钮，则其 `data` 对象将返回为 的值 `result` 。 |
| 自动程序卡按钮 | 1. 自动程序卡片按钮可以通过两种方式（深度链接 URL 或发送消息）调用任务模块，具体取决于按钮 `task/fetch` 的类型。 <br/><br/> 2. 如果按钮的操作是自适应卡片的按钮类型，则 HTTP POST 事件 `type` `task/fetch` 将发送给 `Action.Submit` `task/fetch invoke` 机器人。 机器人使用 HTTP 200 响应 POST，响应正文包含 [TaskInfo 对象周围的包装](#the-taskinfo-object)器。 有关详细信息，请参阅使用[调用任务模块 `task/fetch` ](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch)。 Teams任务模块。 <br/><br/> 3. 用户执行这些操作后，Teams对象作为参数调用 sdk `tasks.submitTask()` `result` 函数。 机器人会收到 `task/submit invoke` 一条消息，其中包含 `result` 对象。 <br/><br/> 4. 通过不执行任何操作（即任务成功完成、在弹出窗口中向用户显示消息或调用另一个任务模块窗口）来响应邮件，你有三种不同的方法。 `task/submit` 有关详细信息，请参阅[上的详细说明 `task/submit` ](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 | <ul><li> 与 Bot Framework 卡上的按钮类似，自适应卡片上的按钮支持两种调用任务模块的方法、包含按钮的深层链接 URL `Action.openUrl` `task/fetch` 和使用 `Action.Submit` 按钮。 </li></ul> <br/><br/> <ul><li> 具有自适应卡片的任务模块与 HTML 或 JavaScript 的情况非常类似。 主要区别在于，由于在使用自适应卡片时没有 JavaScript，因此无法调用 `tasks.submitTask()` 。 相反，Teams对象， `data` `Action.Submit` 并返回该对象作为事件 `task/submit` 的有效负载。 有关详细信息，请参阅[的灵活性 `task/submit` ](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 </li></ul> |
| 深层链接 URL <br/>[URL 语法](#task-module-deep-link-syntax) | 1. Teams调用任务模块，该模块是显示在深层链接的参数中指定的内的 `<iframe>` `url` URL。 没有 `submitHandler` 回调。 <br/><br/> 2. 在任务模块中页面的 JavaScript 内，调用 以使用对象作为参数关闭它，就像从选项卡或自动程序卡按钮调用它一 `tasks.submitTask()` `result` 样。 但是，完成逻辑略有不同。 如果完成逻辑驻留在没有自动程序的客户端上，则没有回调，因此任何完成逻辑都必须位于 调用 之前 `submitHandler` 的代码 `tasks.submitTask()` 。 调用错误仅通过控制台报告。 如果你有自动程序，可以在深度链接中指定参数以 `completionBotId` 通过事件 `result` 发送 `task/submit` 对象。 | 1. Teams调用任务模块，该任务模块是自适应卡片的 JSON 卡片正文，指定为深层链接参数的 URL 编码 `card` 值。 <br/><br/> 2. 用户通过选择任务模块右上角的 X 或按卡片上的按钮来 `Action.Submit` 关闭任务模块。 由于没有要调用的项，因此用户必须具有自动程序来发送自适应卡片 `submitHandler` 字段的值。 用户必须使用深层链接中的 参数指定使用事件 `completionBotId` 将数据发送到的 `task/submit invoke` 自动程序。 |

> [!NOTE]
> 移动版不支持从 JavaScript 调用任务模块。

下一节指定定义任务模块 `TaskInfo` 的某些属性的对象。

## <a name="the-taskinfo-object"></a>TaskInfo 对象

`TaskInfo`对象包含任务模块的元数据。 为 `url` 嵌入的 iFrame 或 `card` 自适应卡片定义 。 下表提供了对象定义：

| 属性 | 类型 | 说明 |
| --- | --- | --- |
| `title` | string | 此属性显示在应用名称下方和应用图标右侧。 |
| `height` | number or string | 此属性可以是一个数字，表示任务模块的高度，以像素为单位，或 `small` 、 或 `medium` `large` 。 有关详细信息，请参阅任务 [模块大小调整](#task-module-sizing)。 |
| `width` | number or string | 此属性可以是一个数字，表示任务模块的宽度，以像素为单位，或 `small` 、 或 `medium` `large` 。 有关详细信息，请参阅任务 [模块大小调整](#task-module-sizing)。 |
| `url` | string | 此属性是作为任务模块内部加载的页面 `<iframe>` 的 URL。 URL 的域必须在你的应用清单中的 [应用的 validDomains](~/resources/schema/manifest-schema.md#validdomains) 数组中。 |
| `card` | 自适应卡片或自适应卡片自动程序卡附件 | 此属性是要显示在任务模块中的自适应卡片的 JSON。 如果用户从自动程序调用，请使用 Bot Framework 对象中的自适应卡片 `attachment` JSON。 在选项卡中，用户必须使用自适应卡片。 有关详细信息，请参阅自适应 [卡片或自适应卡片自动程序卡附件](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | 如果客户端不支持任务模块功能，则此属性将在浏览器选项卡中打开 URL。 |
| `completionBotId` | string | 此属性指定要发送用户与任务模块交互结果的自动程序应用 ID。 如果指定，机器人将接收事件负载 `task/submit invoke` 中具有 JSON 对象的事件。 |

> [!NOTE]
> 任务模块功能要求要加载的任何 URL 的域包含在应用清单的数组 `validDomains` 中。

下一节指定允许用户设置任务模块的高度和宽度的任务模块大小。

## <a name="task-module-sizing"></a>任务模块大小调整

使用 和 的整数设置任务模块的高度和宽度 `TaskInfo.width` `TaskInfo.height` （以像素为单位）。 但是，根据团队窗口的大小和屏幕分辨率，它们按比例减少，同时保持宽度或高度的纵横比。

如果 和 为 、 或 ，则以下图像中红色矩形的大小与可用空间的比例为 `TaskInfo.width` `TaskInfo.height` `"small"` `"medium"` `"large"` 20%、50% 和 60%，对于 `width` `height` ：

![任务模块示例](~/assets/images/task-module/task-module-example.png)

从选项卡调用的任务模块可以动态调整大小。 调用后 `tasks.startTask()` ，可以调用 newSize 对象的高度和宽度属性符合 `tasks.updateTask(newSize)` TaskInfo 规范，例如 `{ height: 'medium', width: 'medium' }` 。

下一节提供了在 YouTube 视频和 PowerApp 中嵌入任务模块的示例。

## <a name="task-module-css-for-html-or-javascript-task-modules"></a>HTML 或 JavaScript 任务模块的任务模块 CSS

基于 HTML 或 JavaScript 的任务模块可以访问标题下方的整个任务模块区域。 虽然这提供了极大的灵活性，但如果您希望边缘的填充与页眉元素对齐并避免不必要的滚动条，则用户必须提供正确的 CSS。 以下各节提供了一些用例示例。

**示例 1：YouTube 视频**

YouTube 提供在网页上嵌入视频的能力。 使用简单的存根网页在任务模块中的网页上嵌入视频很简单。

![YouTube 视频](~/assets/images/task-module/youtube-example.png)

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

以下代码提供了 CSS 的示例：

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

**示例 2：PowerApp**

用户也可以使用相同的方法嵌入 PowerApp。 由于任何单个 PowerApp 的高度或宽度都是可自定义的，因此用户可以调整高度和宽度以实现所需的演示文稿。

![资产管理 PowerApp](~/assets/images/task-module/powerapp-example.png)

以下代码提供了 PowerApp 的 HTML 示例：

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

以下代码提供了 CSS 的示例：

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

下一节提供有关使用自适应卡片或自适应卡片自动程序卡附件调用卡片的详细信息。

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>自适应卡片或自适应卡片自动程序卡附件

根据调用你的 方式，你必须使用自适应卡片或自适应卡片自动程序卡附件，它是一个封装在附件对象中的自适应 `card` 卡片。

当你从选项卡调用时，用户必须使用自适应卡片。

以下代码提供自适应卡片的示例：

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

以下代码提供了从自动程序调用时自适应卡片自动程序卡附件的示例：

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

下一节提供有关任务模块深层链接语法的详细信息，包括 `TaskInfo` 对象 和 `APP_ID` `BOT_APP_ID` 。

## <a name="task-module-deep-link-syntax"></a>任务模块深度链接语法

任务模块深层链接是具有以下两个其他详细信息（可选）的 TaskInfo 对象的 `APP_ID` 序列化 `BOT_APP_ID` ：

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

有关 、 和 的数据类型和允许的值 `<TaskInfo.url>` `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` ，请参阅 [TaskInfo 对象](#the-taskinfo-object)。

> [!TIP]
> URL 在使用 参数时对深度链接进行 `card` 编码，例如 JavaScript[ `encodeURI()` ](https://www.w3schools.com/jsref/jsref_encodeURI.asp)的函数 。

下表提供了有关 和 `APP_ID` 的信息 `BOT_APP_ID` ：

| 值 | 类型 | 必需 | 说明 |
| --- | --- | --- | --- |
| `APP_ID` | string | 是 | 调用任务模块的应用的[ID。](~/resources/schema/manifest-schema.md#id) 的 [清单中的 validDomains](~/resources/schema/manifest-schema.md#validdomains) `APP_ID` 数组必须包含 `url` 的域的 if 位于 URL `url` 中。 从选项卡或自动程序调用任务模块时，应用 ID 已已知，这就是它未包含在 中的原因 `TaskInfo` 。 |
| `BOT_APP_ID` | string | 否 | 如果指定了 `completionBotId` 的值，则使用消息将对象 `result` `task/submit invoke` 发送到指定的自动程序。 `BOT_APP_ID` 必须在应用清单中指定为自动程序，即不能将其发送到任何自动程序。 |

> [!NOTE]
> `APP_ID` 如果应用有建议自动程序用作应用 ID（如果存在的话）。在许多情况下，和 可能 `BOT_APP_ID` 相同。

下一节提供有关将键盘与应用的任务模块一同使用的详细信息。

## <a name="keyboard-and-accessibility-guidelines"></a>键盘和辅助功能指南

对于基于 HTML 或 JavaScript 的任务模块，必须确保应用的任务模块可以与键盘一同使用。 屏幕阅读器程序还取决于使用键盘进行导航的能力。 这包括以下两项：

* 使用 [HTML 标记中的 tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) 属性控制可以聚焦的元素。 另外，使用 tabindex 属性确定它通常使用 <kbd>Tab</kbd> 键和 <kbd>Shift-Tab</kbd> 键参与顺序键盘导航的地方。
* 在 <kbd>JavaScript</kbd> 中为任务模块处理 Esc 键。 以下代码提供了如何处理 <kbd>Esc</kbd> 键的示例：

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

Microsoft Teams确保键盘导航从任务模块标头正常进入 HTML，反之亦然。

## <a name="code-sample"></a>代码示例

|示例名称 | 说明 | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|任务模块示例 bots-V4 | 用于创建任务模块的示例。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|任务模块示例选项卡和 bots-V3 | 用于创建任务模块的示例。 |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a>另请参阅

* [请求设备权限](~/concepts/device-capabilities/native-device-permissions.md)
* [集成媒体功能](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [将 QR 或条形码扫描仪功能集成到 Teams](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [在 Teams 中集成位置Teams](~/concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [在选项卡中使用任务模块](~/task-modules-and-cards/task-modules/task-modules-tabs.md)