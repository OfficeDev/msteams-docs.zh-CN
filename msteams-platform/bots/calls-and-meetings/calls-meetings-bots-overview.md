---
title: 通话和联机会议机器人
description: 了解你的 Microsoft Teams 应用如何使用语音和视频与用户使用 Microsoft Graph API 进行通话和联机会议交互。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: 呼叫呼叫 音频视频 IVR 语音联机会议
ms.openlocfilehash: e94cb425f7931582067bc3439e890b74b64e0f51
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155969"
---
# <a name="calls-and-online-meetings-bots"></a>通话和联机会议机器人

机器人可以使用实时Teams、视频和屏幕共享与呼叫和会议进行交互。 借助[Microsoft Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)API 进行呼叫和联机会议，Teams应用现在可以使用语音和视频与用户交互，以增强体验。 这些 API 允许你添加以下新功能：

* IVR (互动语音) 。
* 呼叫控制。
* 访问实时音频和视频流，包括桌面应用共享。

若要在 Graph应用中使用这些 Teams API，请创建一个自动程序并指定一些其他信息和权限。

此外，实时媒体平台允许机器人使用实时Teams、视频和屏幕共享与通话和会议进行交互。 参与音频或视频通话和联机会议的机器人是一种Microsoft Teams聊天机器人，具有用于注册机器人的一些额外功能。

The Teams app manifest with two additional settings `supportsCalling` and `supportsVideo` ， Graph permissions for your bot's Microsoft App ID， and tenant admin consent enable you to register the bot. 在注册呼叫和会议机器人Teams时，会提到 Webhook URL，它是对自动程序的所有传入呼叫的 webhook 终结点。 应用程序托管的媒体机器人需要 Microsoft。Graph。Communications.Calls.Media .NET 库，用于访问音频和视频媒体流，机器人必须部署在 Azure 中的 Windows Server 计算机或 Windows Server 来宾操作系统 (操作系统) 上。 自动程序Teams音频和视频内容仅支持一组特定的媒体格式。

现在，您必须了解一些核心概念、术语和约定。

## <a name="terminologies"></a>术语

以下核心概念、术语和约定指导你使用呼叫和联机会议机器人：

* 音频或视频呼叫
* 呼叫类型
* 信号
* 呼叫和联机会议
* 实时媒体

### <a name="audio-or-video-calls"></a>音频或视频呼叫

呼叫Teams可以是纯音频或音频和视频。 使用术语呼叫代替音频或视频呼叫。

### <a name="call-types"></a>呼叫类型

呼叫可以是人员与机器人之间的对等呼叫，或者是机器人与组通话中的两个或多个人员之间的多方呼叫。

![调用类型](~/assets/images/calls-and-meetings/call-types.png)

以下是调用所需的不同呼叫类型和权限：

* 用户可以使用机器人发起对等呼叫或邀请机器人加入现有的多方呼叫。 多部分调用尚未在 Teams用户界面中启用。

    > [!NOTE]
    > 用户向自动程序发起的呼叫当前在移动Microsoft Teams不受支持。

* Graph自动程序发起对等呼叫不需要权限。 机器人需要其他权限才能参与多方呼叫，或者机器人需要其他权限来发起与用户的对等呼叫。
* 呼叫可以对等启动，并最终成为多方呼叫。 如果你的机器人拥有适当的权限，则机器人可以通过邀请其他人来发起多方呼叫。 如果你的机器人无权参与组通话，并且某位参与者向该呼叫添加了另一个参与者，则你的机器人会从通话中丢弃。

### <a name="signals"></a>信号

有两种类型的信号：传入呼叫和呼叫内。 以下是信号的不同功能：

* 若要接收传入呼叫，请在自动程序设置中输入终结点。 启动传入呼叫时，此终结点将收到通知。 可以应答呼叫、拒绝呼叫或将其重定向到其他人。

    ![呼叫处理](~/assets/images/calls-and-meetings/call-handling.png)

* 当机器人正在通话中时，有一些 API 用于将机器人静音和取消静音，以及启动或停止与其他参与者共享视频或桌面内容。
* 机器人还可以访问参与者列表、邀请新参与者并将其静音。

### <a name="calls-and-online-meetings"></a>呼叫和联机会议

从Teams的角度来看，有两种类型的联机会议，即临时会议和计划会议。 从机器人的角度来看，这两个联机会议是相同的。 对于机器人，联机会议是一组参与者之间的多方呼叫，包括会议坐标。 会议坐标是会议元数据，包括与会议关联的 `botId` 、 `chatId` `joinUrl` 或 `startTime` `endTime` 等。

### <a name="real-time-media"></a>实时媒体

当机器人参与呼叫或联机会议时，它必须处理音频和视频流。 当用户在通话中通话、在摄像头上显示自己或在会议中演示屏幕时，机器人会显示为音频和视频流。 如果机器人想要说出一些非常简单的话，请按 **0** 以在 IVR (交互语音响应中) 接线员，则需要播放 。WAV 文件。 这统称为媒体或实时媒体。

实时媒体是指必须实时处理媒体（而不是播放以前录制的音频或视频）的方案。 处理媒体流（尤其是实时媒体流）非常复杂。 Microsoft 已创建实时媒体平台来处理这些方案，并尽可能卸载传统繁重的媒体处理工作。 当机器人应答传入呼叫或加入新呼叫或现有呼叫时，需要告诉实时媒体平台如何处理媒体。 如果要构建 IVR 应用程序，可以将昂贵的音频处理卸载到 Microsoft。 或者，如果你的机器人需要直接访问媒体流，则也支持该方案。 有两种类型的媒体处理：

* **服务托管的媒体**：机器人专注于管理应用程序工作流，例如将呼叫路由和将音频处理卸载到 Microsoft 实时媒体平台。 借助服务托管的媒体，有几种实现和托管机器人的选项。 服务托管的媒体机器人可以作为无状态服务进行实施，因为它不在本地处理媒体。 服务托管的媒体机器人可以使用以下 API：

    * `PlayPrompt` 用于播放音频剪辑。
    * `Record` 用于录制音频剪辑。
    * `SubscribeToTone` 用于订阅双音多频 (DTMF) 音。

    例如，知道用户何时按 **0** 到达接线员。

* **应用程序托管的媒体**：若要使机器人直接访问媒体，它需要特定的Graph权限。 在机器人拥有权限后，实时媒体[](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)库和 Graph[调用 SDK](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder)可帮助你生成丰富的实时媒体和通话机器人。 必须在 Windows 环境中托管应用程序托管的机器人。 有关详细信息，请参阅 [应用程序托管的媒体机器人](./requirements-considerations-application-hosted-media-bots.md)。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **Graph** |
|---------------|----------|--------|
| Graph通信 | Graph与 Microsoft 的通信平台进行交互。 | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples) |
| 通话和会议机器人 | 示例应用将启动机器人如何创建呼叫、加入会议以及转接呼叫。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-calling-meeting/csharp) |

## <a name="see-also"></a>另请参阅

- [GraphAPI 参考](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)

- [示例应用](https://github.com/microsoftgraph/microsoft-graph-comms-samples)

- [注册支持通话和联机会议的机器人](./registering-calling-bot.md)

- [Graph联机会议自动程序的权限](./registering-calling-bot.md#add-graph-permissions)

- [如何在计算机上开发通话和联机会议机器人](./debugging-local-testing-calling-meeting-bots.md)

- [应用程序托管的媒体机器人的要求和注意事项](./requirements-considerations-application-hosted-media-bots.md)

- [有关处理传入呼叫通知的技术信息](./call-notifications.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [实时媒体通话与会议](~/bots/calls-and-meetings/real-time-media-concepts.md)
