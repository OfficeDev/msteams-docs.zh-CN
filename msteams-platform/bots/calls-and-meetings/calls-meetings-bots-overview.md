---
title: 呼叫和联机会议机器人
description: 了解Microsoft Teams应用如何使用 Microsoft Graph API 进行呼叫和联机会议的语音和视频与用户交互，并了解实时媒体流
ms.topic: conceptual
ms.localizationpriority: medium
keywords: 调用音频视频 IVR 语音联机会议实时媒体流机器人
ms.openlocfilehash: e17d0c18bfb3f751a11e43780dba9f0f85441a96
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073821"
---
# <a name="calls-and-online-meetings-bots"></a>呼叫和联机会议机器人

机器人可以使用实时语音、视频和屏幕共享与Teams呼叫和会议交互。 使用 [Microsoft Graph API 进行通话和联机会议](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)，Teams应用现在可以使用语音和视频与用户进行交互，以增强体验。 使用这些 API 可以添加以下新功能：

* IVR)  (交互式语音响应。
* 呼叫控制。
* 访问实时音频和视频流，包括桌面和应用共享。

若要在Teams应用中使用这些Graph API，请创建一个机器人并指定一些其他信息和权限。

此外，通过实时媒体平台，机器人可以使用实时语音、视频和屏幕共享与Teams呼叫和会议进行交互。 参与音频或视频通话和联机会议的机器人是常规Microsoft Teams机器人，几乎没有额外的功能用于注册机器人。

Teams应用清单具有两个附加设置`supportsCalling``supportsVideo`，以及机器人的 Microsoft 应用 ID 的Graph权限以及租户管理员同意，可以注册机器人。 在为Teams注册呼叫和会议机器人时，会提到 Webhook URL，它是所有传入机器人的调用的 Webhook 终结点。 应用程序托管的媒体机器人需要 Microsoft。Graph。Communications.Calls.Media .NET 库用于访问音频和视频媒体流，并且机器人必须部署在 Windows 服务器计算机上，或者Windows服务器来宾操作系统 (Azure 中的 OS) 。 Teams上的机器人仅支持音频和视频内容的特定媒体格式集。

现在，必须了解一些核心概念、术语和约定。

## <a name="terminologies"></a>术语

以下核心概念、术语和约定指导你使用呼叫和联机会议机器人：

* 音频或视频通话
* 呼叫类型
* 信号
* 呼叫和联机会议
* 实时媒体

### <a name="audio-or-video-calls"></a>音频或视频通话

Teams中的呼叫可以是纯音频或音频和视频。 使用术语调用，而不是音频或视频呼叫。

### <a name="call-types"></a>呼叫类型

呼叫是人员与机器人之间的对等呼叫，或是机器人与组呼叫中的两个或更多人之间的多方。

![呼叫类型](~/assets/images/calls-and-meetings/call-types.png)

下面是调用所需的不同调用类型和权限：

* 用户可以与机器人启动对等呼叫，或邀请机器人加入现有的多方呼叫。 尚未在Teams用户界面中启用多方调用。

    > [!NOTE]
    > Microsoft Teams移动平台目前不支持用户发起的对机器人的调用。

* 用户无需Graph权限即可启动与机器人的对等调用。 机器人需要其他权限才能参与多方调用，或者机器人需要其他权限才能与用户启动对等呼叫。
* 呼叫可以以对等方式开始，并最终成为多方调用。 机器人可以通过邀请他人来启动多方调用，前提是机器人具有适当的权限。 如果你的机器人没有参与组呼叫的权限，并且如果参与者将另一个参与者添加到呼叫中，则机器人将从呼叫中删除。

### <a name="signals"></a>信号

有两种类型的信号，即传入呼叫和呼叫中。 以下是信号的不同功能：

* 若要接收传入呼叫，请在机器人设置中输入终结点。 启动传入调用时，此终结点将收到通知。 可以接听呼叫、拒绝呼叫或将其重定向到其他人。

    ![呼叫处理](~/assets/images/calls-and-meetings/call-handling.png)

* 当机器人处于呼叫状态时，有用于静音和解构机器人以及开始或停止与其他参与者共享视频或桌面内容的 API。
* 机器人还可以访问参与者列表、邀请新参与者并将其静音。

### <a name="calls-and-online-meetings"></a>呼叫和联机会议

从Teams用户的角度来看，有两种类型的联机会议，即席会议和计划会议。 从机器人的角度来看，这两个在线会议都是相同的。 对于机器人，联机会议是一组参与者之间的多方调用，包括会议坐标。 会议坐标是会议的元数据，包括`botId`与会议 `startTime` `joinUrl`关联的、或`endTime``chatId`等。

### <a name="real-time-media"></a>实时媒体

当机器人参与通话或联机会议时，它必须处理音频和视频流。 当用户在通话中交谈、在网络摄像头上显示自己或在会议中显示屏幕时，向机器人显示为音频和视频流。 如果机器人想说一些简单的话， **按 0 以在** IVR) 方案 (交互式语音响应中访问操作员，则需要播放一个。WAV 文件。 这统称为媒体或实时媒体。

实时媒体是指必须实时处理媒体，而不是播放以前录制的音频或视频的情况。 处理媒体流（尤其是实时媒体流）极其复杂。 Microsoft 创建了实时媒体平台来处理这些方案，并尽可能卸载尽可能多的传统重载实时媒体处理。 当机器人接听传入呼叫或加入新的或现有的呼叫时，它需要告诉实时媒体平台如何处理媒体。 如果要生成 IVR 应用程序，可以将昂贵的音频处理卸载到 Microsoft。 或者，如果机器人需要直接访问媒体流，则也支持此方案。 媒体处理有两种类型：

* **服务托管媒体**：机器人专注于管理应用程序工作流，例如路由呼叫和将音频处理卸载到 Microsoft 实时媒体平台。 使用服务托管媒体，可以使用多个选项来实现和托管机器人。 服务托管的媒体机器人可以作为无状态服务进行实施，因为它不在本地处理媒体。 服务托管媒体机器人可以使用以下 API：

  * `PlayPrompt` 用于播放音频剪辑。
  * `Record` 用于录制音频剪辑。
  * `SubscribeToTone` 用于订阅双音多频 (DTMF) 音。

    例如，知道用户何时按下 **0** 来访问操作员。

* **应用程序托管媒体**：机器人要直接访问媒体，需要特定的Graph权限。 机器人拥有权限后，[实时媒体库](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)和[调用 SDK 的Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder)可帮助你构建丰富的实时媒体和调用机器人。 必须在 Windows 环境中托管应用程序托管的机器人。 有关详细信息，请参阅 [应用程序托管的媒体机器人](./requirements-considerations-application-hosted-media-bots.md)。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **Graph** |
|---------------|----------|--------|
| Graph通信 | Graph与 Microsoft 通信平台交互的通信。 | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [实时媒体通话与会议](~/bots/calls-and-meetings/real-time-media-concepts.md)

## <a name="see-also"></a>另请参阅

* [图形 API参考](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
* [示例应用](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
* [注册支持通话和联机会议的机器人](./registering-calling-bot.md)
* [Graph呼叫和联机会议机器人的权限](./registering-calling-bot.md#add-graph-permissions)
* [如何在计算机上开发呼叫和联机会议机器人](./debugging-local-testing-calling-meeting-bots.md)
* [应用程序托管媒体机器人的要求和注意事项](./requirements-considerations-application-hosted-media-bots.md)
* [有关处理传入呼叫通知的技术信息](./call-notifications.md)
* [设置自动助理](/microsoftteams/create-a-phone-system-auto-attendant)
* [在 Android 和视频电话设备上为 Teams Microsoft Teams 会议室设置自动应答](/microsoftteams/set-up-auto-answer-on-teams-android)
* [Teams记录策略](/MicrosoftTeams/teams-recording-policy)