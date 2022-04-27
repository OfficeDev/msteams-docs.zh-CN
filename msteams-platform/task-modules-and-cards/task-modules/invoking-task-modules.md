---
title: 调用和关闭任务模块
description: 了解如何使用代码示例调用和消除任务模块、任务信息对象、任务模块大小、任务模块深度链接语法
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 5685e789dd6f4ad7cc39173e11af15dd9f7360fe
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073687"
---
# <a name="invoke-and-dismiss-task-modules"></a>调用和关闭任务模块

可以从选项卡、机器人或深层链接调用任务模块。 响应可以是 HTML、JavaScript 或自适应卡片。 在如何调用任务模块以及如何处理用户交互的响应方面有很多灵活性。 下表总结了此工作原理：

| 使用调用 | 使用 HTML 或 JavaScript 的任务模块 | 使用自适应卡片的任务模块 |
| --- | --- | --- |
| 选项卡中的 JavaScript | 1.将Teams客户端 SDK 函`tasks.startTask()`数与可选`submitHandler(err, result)`回调函数配合使用。 <br/><br/> 2. 在任务模块代码中，当用户执行操作时，使用对象作为参数调用`result`Teams SDK 函`tasks.submitTask()`数。 `submitHandler`如果在`tasks.startTask()`其中指定了回调，Teams将其作为参数调用`result`。 如果调用 `tasks.startTask()`时出错，则 `submitHandler` 用字符串调用 `err` 该函数。 <br/><br/> 3. 还可以指定 `completionBotId` 调用 `teams.startTask()`时。 然后，将 `result` 该文件发送到机器人。 | 1. 使用 [TaskInfo 对象](#the-taskinfo-object)调用Teams客户端 SDK `tasks.startTask()` 函数，并`TaskInfo.card`包含要在任务模块弹出窗口中显示的自适应卡片的 JSON。 <br/><br/> 2. 如果`submitHandler`在`tasks.startTask()`其中指定了回调，Teams使用字符串调用`err`它，如果调用`tasks.startTask()`时出错，或者用户使用右上角的 X 关闭任务模块弹出窗口。 <br/><br/> 3. 如果用户按下按 `Action.Submit` 钮，则返回其 `data` 对象作为值 `result`。 |
| 机器人卡按钮 | 1. 机器人卡按钮（具体取决于按钮的类型）可以通过两种方式（深层链接 URL 或通过发送消息） `task/fetch` 调用任务模块。 <br/><br/> 2. 如果按钮的操作`type`是`task/fetch``Action.Submit`自适应卡片的按钮类型，`task/fetch invoke`则会将 HTTP POST 事件发送到机器人。 机器人使用 HTTP 200 响应 POST，响应正文包含 [TaskInfo 对象](#the-taskinfo-object)周围的包装器。 有关详细信息，请参阅[使用`task/fetch`调用任务模块](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch)。 Teams显示任务模块。 <br/><br/> 3. 用户执行操作后，使用对象作为参数调用`result`Teams SDK 函`tasks.submitTask()`数。 机器人接收包含`task/submit invoke``result`该对象的消息。 <br/><br/> 4. 通过在弹出窗口中向用户显示消息或调用另一个任务模块窗口，你可以通过三种不同的方式来响应 `task/submit` 消息、不执行成功完成的任务。 有关详细信息，请参阅 [有关详细讨论的信息 `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 | <ul><li> 与 Bot Framework 卡上的按钮一样，自适应卡片上的按钮支持调用任务模块的两种方法：使用按钮的深度链接 URL `Action.openUrl` 和 `task/fetch` 按 `Action.Submit` 钮。 </li></ul> <br/><br/> <ul><li> 使用自适应卡片的任务模块的工作方式与 HTML 或 JavaScript 大小写非常相似。 主要区别在于，由于使用自适应卡片时没有 JavaScript，因此无法调用 `tasks.submitTask()`。 相反，Teams从`Action.Submit`中`data`获取对象，并将其作为事件的`task/submit`有效负载返回。 有关详细信息，请参阅 [灵活性 `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。 </li></ul> |
| 深层链接 URL <br/>[URL 语法](#task-module-deep-link-syntax) | 1. Teams调用任务模块，该任务模块是在深层链接的参数中`url`指定的 URL 中显示`<iframe>`的。 没有 `submitHandler` 回调。 <br/><br/> 2. 在任务模块中页面的 JavaScript 中，调用`tasks.submitTask()``result`以对象作为参数将其关闭，与从选项卡或机器人卡按钮调用对象时相同。 但是，完成逻辑略有不同。 如果完成逻辑位于没有机器人的客户端上，则没有 `submitHandler` 回调，因此任何完成逻辑都必须位于调用 `tasks.submitTask()`之前的代码中。 调用错误仅通过控制台报告。 如果有机器人，则可以在深层链接中指定`completionBotId`参数以通过`task/submit`事件发送`result`对象。 | 1. Teams调用任务模块，该模块是自适应卡片的 JSON 卡体，指定为深层链接参数的 `card` URL 编码值。 <br/><br/> 2. 用户通过选择任务模块右上角的 X 或按 `Action.Submit` 卡上的按钮来关闭任务模块。 由于没有 `submitHandler` 调用，因此用户必须有一个机器人才能发送自适应卡片字段的值。 用户必须使用 `completionBotId` 深层链接中的参数来指定机器人以将数据发送到使用 `task/submit invoke` 事件。 |

下一部分指定 `TaskInfo` 为任务模块定义某些属性的对象。

## <a name="the-taskinfo-object"></a>TaskInfo 对象

该 `TaskInfo` 对象包含任务模块的元数据。 `url`定义嵌入式 iFrame 或`card`自适应卡片。 下表提供了对象定义：

| 属性 | 类型 | 说明 |
| --- | --- | --- |
| `title` | string | 此属性显示在应用名称下方和应用图标右侧。 |
| `height` | number or string | 此属性可以是一个数字，表示任务模块的高度（以像素为单位）或`small``medium``large`或 。 有关详细信息，请参阅 [任务模块大小](#task-module-sizing)调整。 |
| `width` | number or string | 此属性可以是一个数字，表示任务模块的宽度（以像素为单位）或 `small``medium``large`。 有关详细信息，请参阅 [任务模块大小](#task-module-sizing)调整。 |
| `url` | string | 此属性是作为 `<iframe>` 任务模块内部加载的页面的 URL。 URL 的域必须位于应用清单中的 [validDomains 数组](~/resources/schema/manifest-schema.md#validdomains) 中。 |
| `card` | 自适应卡片或自适应卡片机器人卡附件 | 此属性是自适应卡片在任务模块中显示的 JSON。 如果用户从机器人调用，请在 Bot Framework `attachment` 对象中使用自适应卡片 JSON。 在选项卡中，用户必须使用自适应卡片。 有关详细信息，请参阅 [自适应卡片或自适应卡机器人卡附件](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | string | 如果客户端不支持任务模块功能，则此属性会在浏览器选项卡中打开 URL。 |
| `completionBotId` | string | 此属性指定一个机器人应用 ID，用于发送用户与任务模块交互的结果。 如果指定，机器人将接收 `task/submit invoke` 事件有效负载中包含 JSON 对象的事件。 |

> [!NOTE]
> 任务模块功能要求要加载的任何 URL 的域都包含在应用清单的数组中 `validDomains` 。

下一部分指定任务模块大小，使用户能够设置任务模块的高度和宽度。

## <a name="task-module-sizing"></a>任务模块大小调整

使用整数来`TaskInfo.width``TaskInfo.height`设置任务模块的高度和宽度（以像素为单位）。 但是，根据团队的窗口大小和屏幕分辨率，它们会按比例减少，同时保持宽度或高度的纵横比。

如果`TaskInfo.width`是（`"small"``TaskInfo.height``"medium"`或`"large"`）下图中红色矩形的大小占可用空间的比例，则为 `width` 20%、50% 和 60%，20%、50% 和 66%。`height`

:::image type="content" source="../../assets/images/task-module/task-module-example.png" alt-text="任务模块示例":::

可以动态调整从选项卡调用的任务模块的大小。 调用 `tasks.startTask()` 后，可以调用 `tasks.updateTask(newSize)` newSize 对象的高度和宽度属性符合 TaskInfo 规范的位置，例如 `{ height: 'medium', width: 'medium' }`。

下一部分提供了在 YouTube 视频和 PowerApp 中嵌入任务模块的示例。

## <a name="task-module-css-for-html-or-javascript-task-modules"></a>适用于 HTML 或 JavaScript 任务模块的任务模块 CSS

HTML 或基于 JavaScript 的任务模块有权访问标头下的任务模块的整个区域。 虽然这提供了很大的灵活性，但如果希望在边缘周围填充以与标头元素保持一致并避免不必要的滚动条，则用户必须提供正确的 CSS。 下一部分提供了一些示例，说明一些用例。

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

### <a name="example-2-powerapp"></a>示例 2：PowerApp

用户也可以使用相同的方法嵌入 PowerApp。 由于任何单个 PowerApp 的高度或宽度都是可自定义的，因此用户可以调整高度和宽度以实现所需的演示文稿。

:::image type="content" source="../../assets/images/task-module/powerapp-example.png" alt-text="powerapp":::

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

下一部分提供有关使用自适应卡片或自适应卡片机器人卡附件调用卡的详细信息。

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a>自适应卡片或自适应卡片机器人卡附件

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

下一部分提供有关任务模块深层链接语法的详细信息， `TaskInfo` 包括对象和 `APP_ID` `BOT_APP_ID`。

## <a name="task-module-deep-link-syntax"></a>任务模块深层链接语法

任务模块深度链接是使用以下两个其他详细信息对 TaskInfo 对象进行序列化， `APP_ID` 并可选 `BOT_APP_ID`地执行以下操作：

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

有关数据类型和允许的值`<TaskInfo.url>``<TaskInfo.width>``<TaskInfo.title>``<TaskInfo.card>``<TaskInfo.height>`，请参阅 [TaskInfo 对象](#the-taskinfo-object)。

> [!TIP]
> 使用 `card` 参数（例如 JavaScript 的 [`encodeURI()` 函](https://www.w3schools.com/jsref/jsref_encodeURI.asp)数）时，URL 会对深层链接进行编码。

下表提供了有关 `APP_ID` 以下 `BOT_APP_ID`内容的信息：

| 值 | 类型 | 必需 | 说明 |
| --- | --- | --- | --- |
| `APP_ID` | string | 是 | 调用任务模块的应用的 [ID](~/resources/schema/manifest-schema.md#id) 。 清单`APP_ID`中的 [validDomains 数组](~/resources/schema/manifest-schema.md#validdomains)必须包含 URL 中的域`url``url`。 当从选项卡或机器人调用任务模块时，应用 ID 已经知道，这就是为什么它不包含在其中 `TaskInfo`的原因。 |
| `BOT_APP_ID` | string | 否 | 如果指定了值 `completionBotId` ， `result` 则使用 `task/submit invoke` 消息将对象发送到指定的机器人。 `BOT_APP_ID` 必须在应用清单中指定为机器人，即不能将其发送到任何机器人。 |

> [!NOTE]
> `APP_ID``BOT_APP_ID`在许多情况下，如果应用有建议的机器人用作应用的 ID（如果有），则可以是一样的。

下一部分提供有关在应用的任务模块中使用键盘的详细信息。

## <a name="keyboard-and-accessibility-guidelines"></a>键盘和辅助功能指南

使用基于 HTML 或 JavaScript 的任务模块，必须确保应用的任务模块可以与键盘一起使用。 屏幕阅读器程序还取决于使用键盘导航的功能。 这包括以下两个事项：

* 在 HTML 标记中使用 [tabindex 属性](https://developer.mozilla.org/docs/Web/HTML/Global_attributes/tabindex) 来控制哪些元素可以聚焦。 此外，使用 tabindex 属性来标识它通常使用 <kbd>Tab</kbd> 和 <kbd>Shift-Tab</kbd> 键参与顺序键盘导航的位置。
* 处理任务模块的 JavaScript 中的 <kbd>Esc</kbd> 密钥。 以下代码提供了如何处理 <kbd>Esc</kbd> 密钥的示例：

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

Microsoft Teams可确保键盘导航从任务模块标头正常工作到 HTML，反之亦然。

## <a name="code-sample"></a>代码示例

|示例名称 | Description | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|任务模块示例 bots-V4 | 用于创建任务模块的示例。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|任务模块示例选项卡和 bots-V3 | 用于创建任务模块的示例。 |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [在选项卡中使用任务模块](~/task-modules-and-cards/task-modules/task-modules-tabs.md)

## <a name="see-also"></a>另请参阅

* [请求设备权限](~/concepts/device-capabilities/native-device-permissions.md)
* [集成媒体功能](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [在 Teams 中集成 QR 或条形码扫描程序功能](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [在 Teams 中集成位置功能](~/concepts/device-capabilities/location-capability.md)
