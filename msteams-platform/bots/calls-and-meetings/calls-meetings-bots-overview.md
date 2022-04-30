---
title: 呼叫和联机会议机器人
description: 了解 Microsoft Teams 应用如何使用语音和视频与用户交互、如何将 Microsoft Graph API 用于呼叫和联机会议，并了解实时媒体流
ms.topic: conceptual
ms.localizationpriority: high
keywords: 通话呼叫音频视频 IVR 语音联机会议实时媒体流机器人
ms.openlocfilehash: 1e719a60c1b14b6651c852ad0eae791e96fa8cc6
ms.sourcegitcommit: 591bab4c7e01ac9099b9a540f149b64e6e31e6e8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2022
ms.locfileid: "65135680"
---
# <a name="calls-and-online-meetings-bots"></a>呼叫和联机会议机器人

机器人可以使用实时语音、视频和屏幕共享与 Teams 呼叫和会议交互。 借助[适用于呼叫和联机会议的 Microsoft Graph API](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)，Teams 应用现在可以使用语音和视频与用户交互，从而改进体验。 这些 API 允许添加以下新功能:

* 互动语音响应 (IVR)。
* 呼叫控制。
* 访问实时音频和视频流，包括桌面和应用共享。

若要在 Teams 应用中使用这些 Graph API，需创建机器人并指定一些附加信息和权限。

此外，实时媒体平台允许机器人使用实时语音、视频和屏幕共享与 Teams 呼叫和会议交互。 参与音频或视频通话和联机会议的机器人为常规 Microsoft Teams 机器人，它具有一些用于注册机器人的额外功能。

具有两个附加设置 `supportsCalling` 和 `supportsVideo` 的 Teams 应用清单、适用于机器人 Microsoft 应用 ID 的 Grapgh 权限以及租户管理员同意使你能够注册机器人。 在为 Teams 注册呼叫和会议机器人时，会提到 Webhook URL，它是机器人所有来电的 Webhook 终结点。 应用程序托管媒体机器人需要 Microsoft.Graph.Communications.Calls.Media .NET 库来访问音频和视频媒体流，并且机器人必须部署在 Azure 中的 Windows Server 计算机或 Windows Server 来宾操作系统 (OS) 上。 Teams 上的机器人仅支持一组特定的音频和视频内容媒体格式。

现在，你必须了解一些核心概念、术语和约定。

## <a name="terminologies"></a>术语

以下核心概念、术语和约定会指导你使用呼叫和联机会议机器人:

* 音频或视频通话
* 呼叫类型
* 信号
* 呼叫和联机会议
* 实时媒体

### <a name="audio-or-video-calls"></a>音频或视频通话

Teams 中的通话可以是纯音频或音频和视频。 使用的术语是“呼叫”，而非音频或视频通话。

### <a name="call-types"></a>呼叫类型

通话是人员与机器人之间的对等通话，或机器人与群组通话中的两人或更多人之间的多方通话。

:::image type="content" source="~/assets/images/calls-and-meetings/call-types.png" alt-text="通话类型"border="true":::

以下是通话所需的不同通话类型和权限:

* 用户可以发起与机器人的对等通话，或邀请机器人加入现有多方通话。 Teams 用户界面中尚未启用多方通话。

    > [!NOTE]
    > Microsoft Teams 移动平台当前不支持用户向机器人发起通话。

* 用户无需 Graph 权限即可发起与机器人的对等通话。 机器人需要其他权限才可参与多方通话，或者机器人需要其他权限才可发起与用户的对等通话。
* 通话可以以对等方式开始，并在最后成为多方通话。 如果机器人具有适当权限，则可邀请他人发起多方通话。 如果机器人没有参与群组通话的权限，并且如果参与者将另一名参与者添加到通话中，则将从通话中删除机器人。

### <a name="signals"></a>信号

有两种类型的信号: 来电和通话中。 以下是信号的不同功能:

* 若要接听来电，请在机器人设置中输入终结点。 发起来电时，此终结点会收到通知。 可以应答呼叫、拒绝呼叫或将其重定向到其他人员。

     :::image type="content" source="~/assets/images/calls-and-meetings/call-handling.png" alt-text="呼叫处理"border="true":::

* 当机器人接听电话时，有 API 可用于静音和取消静音该机器人，以及开始或停止与其他参与者共享视频或桌面内容。
* 机器人还可以访问参与者列表、邀请新的参与者并将其静音。

### <a name="calls-and-online-meetings"></a>呼叫和联机会议

从 Teams 用户的角度来看，有两种类型的联机会议: 临时会议和计划的会议。 从机器人的角度来看，这两种联机会议并无差别。 对机器人而言，联机会议是一组参与者之间的多方通话，包括会议坐标。 会议坐标为会议的元数据，包括 `botId`、与会议关联的 `chatId`、`joinUrl`、`startTime` 或 `endTime` 等。

### <a name="real-time-media"></a>实时媒体

当机器人参与通话或联机会议时，它必须处理音频和视频流。 当用户在通话中交谈、在网络摄像头中露面或在会议中展示屏幕时，会以音频和视频流的形式显示给机器人。 如果机器人想要在互动语音响应 (IVR) 场景中说出“**按 0 联系话务员**”等简单的话，需要播放 .WAV 文件。 这统称为媒体或实时媒体。

实时媒体是指必须实时处理媒体的场景，而不是播放之前录制的音频或视频。 处理媒体流 (尤其是实时媒体流) 极其复杂。 Microsoft 已创建实时媒体平台以应对这些场景，并尽可能减轻实时媒体处理的传统繁重工作。 当机器人接听来电或加入新的或现有通话时，它需要告知实时媒体平台如何处理媒体。 如果正在构建 IVR 应用程序，可以将昂贵的音频处理工作交给 Microsoft。 或者，如果机器人需要直接访问媒体流，也支持该方案。 媒体处理有两种类型：

* **服务托管媒体**: 机器人专注于管理应用程序工作流，例如呼叫路由并将音频处理工作交给 Microsoft 实时媒体平台。 借助服务托管媒体，可以通过多个选项来实现并托管机器人。 服务托管的媒体机器人可以作为无状态服务进行实施，因为它不在本地处理媒体。 服务托管媒体机器人可以使用以下 API:

  * `PlayPrompt` 用于播放音频剪辑。
  * `Record` 用于录制音频剪辑。
  * `SubscribeToTone` 用于订阅双音多频 (DTMF) 音。

    例如，了解用户按“**0**”联系话务员的时间。

* **应用程序托管媒体**: 要让机器人直接访问媒体，它需要特定的 Graph 权限。 机器人拥有权限后，[实时媒体库](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)和 [Graph 通话 SDK](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder) 可帮助你构建丰富的实时媒体和通话机器人。 必须在 Windows 环境中托管应用程序托管的机器人。 有关详细信息，请参阅 [应用程序托管媒体机器人](./requirements-considerations-application-hosted-media-bots.md)。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **Graph** |
|---------------|----------|--------|
| Graph 通信 | 用于与 Microsoft 通信平台交互的 Graph 通信。 | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [实时媒体通话与会议](~/bots/calls-and-meetings/real-time-media-concepts.md)

## <a name="see-also"></a>另请参阅

* [Graph API 参考](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
* [示例应用](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
* [注册支持呼叫和联机会议的机器人](./registering-calling-bot.md)
* [适用于呼叫和联机会议机器人的 Graph 权限](./registering-calling-bot.md#add-graph-permissions)
* [如何在计算机上开发呼叫和联机会议机器人](./debugging-local-testing-calling-meeting-bots.md)
* [应用程序托管的媒体机器人的要求和注意事项](./requirements-considerations-application-hosted-media-bots.md)
* [有关处理来电通知的技术信息](./call-notifications.md)
* [设置自动助理](/microsoftteams/create-a-phone-system-auto-attendant)
* [在 Android 和 Teams 视频电话设备上为 Microsoft Teams 会议室设置自动应答](/microsoftteams/set-up-auto-answer-on-teams-android)
* [Teams 录制策略](/MicrosoftTeams/teams-recording-policy)
* [在 Microsoft Graph 中使用通信 API](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
