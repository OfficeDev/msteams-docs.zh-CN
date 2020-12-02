---
title: 呼叫和联机会议 Bot
description: 了解如何使用 Microsoft Graph Api 对呼叫和联机会议使用语音和视频与用户进行交互。
keywords: 呼叫音频视频 IVR 语音联机会议
ms.openlocfilehash: fa31bc55221befab1ac1b6b77e116f3fc2e1a935
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552428"
---
# <a name="calls-and-online-meetings-bots"></a>呼叫和联机会议 bot

> [!NOTE]
> Microsoft 团队移动平台目前不支持呼叫和联机会议 bot 支持。 

通过添加 [用于呼叫和联机会议的 Microsoft Graph api](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)，microsoft 团队应用现在可以使用语音和视频以丰富的方式与用户进行交互。 这些 Api 允许您添加新功能，如交互式语音响应 (IVR) 、呼叫控制以及对呼叫和会议（包括桌面和应用程序共享）的实时音频和/或视频流的访问。

若要在 Microsoft 团队应用程序中使用这些 Microsoft Graph Api，请创建一个 bot 并指定一些其他信息和权限，这些信息和权限将在其他地方介绍，但首先，了解一些核心概念、术语和约定非常重要：

* **音频/视频呼叫。** 团队中的呼叫可以是纯音频或音频 + 视频。 为简洁起见，我们并不说 "音频/视频呼叫" 无处不在。我们只是说 "通话"。
* **呼叫类型。** 呼叫可以是用户和你的 bot 之间的对等 () 或多方 (你的 bot 和组中的两个或更多人) 调用。
  ![CallingTypes ](~/assets/images/calls-and-meetings/call-types.png) ：
  * 用户可以使用你的 bot 启动对等呼叫，或邀请你的 bot 加入现有的多方呼叫 (尽管在 Microsoft 团队 UI) 中尚未启用后者。
  * 用户无需使用 Microsoft Graph 权限来启动与你的 bot 的对等呼叫，但你的 bot 需要其他权限来参与多方呼叫，或者你的 bot 启动与用户的对等呼叫。
  * 呼叫可以作为对等启动，并升级到多方。 你的 bot 可以通过邀请其他人来启动此升级，前提是你的 bot 具有适当的权限。 如果你的 bot 没有参与组呼叫的权限，并且一个参与者添加了另一方，则你的 bot 将从呼叫中删除。
* **令.** 有两种类型的信号：传入呼叫和待命：
  * 若要接收传入呼叫，请在你的 bot 设置中指定终结点;传入呼叫到达时，此终结点收到通知。 您可以应答呼叫、拒绝呼叫，或将其重定向到某个位置或其他人。
  ![呼叫类型](~/assets/images/calls-and-meetings/call-handling.png)
  * 当 bot 在呼叫中时，会有用于静音和观众本身的 Api，并可启动/停止与其他参与者共享视频/桌面内容。
  * Bot 还可以访问参与者列表、邀请新参与者并将其静音。
* **呼叫和联机会议。** 从团队用户的角度来看，有两种类型的在线会议—临时和计划的。 但是，从 bot 的角度来看，两者都是相同的。 对于 bot，联机会议只是一个多方呼叫 (一组参与者) 加上 "会议协调"，您可以将其视为会议的元数据： `botId` 、 `chatId` 与会议、、等相关联 `joinUrl` `startTime` / `endTime` 。
* **实时媒体。** 当机器人参与呼叫或联机会议时，它必须处理音频和视频流。 当用户在通话中进行通话、在网络摄像机上显示自己或在会议中显示其屏幕时，bot 会 "将" 视为音频和/或视频流。 如果你的 bot 想要说出某个内容或呈现屏幕内容，则需要音频或视频流。 甚至像 bot 这样简单的东西，在 IVR (交互式语音响应中 "按0进入操作员") 方案意味着播放 a。WAV 文件。 我们将此情况称为 _媒体_ 或 _实时媒体_ (。在引用媒体必须实时处理（而不是之前录制的音频/视频) 播放）的情况下。 过去，处理媒体流（尤其是实时媒体流）对于开发人员来说非常复杂。 Microsoft 已经创建了 _实时媒体平台_ 来处理这些用例，并尽可能多地分担实时 "大量提升" 的实时媒体处理。  当机器人接听来电或加入新呼叫或现有呼叫时，需要告诉实时媒体平台如何处理媒体。 如果您正在构建 IVR 应用程序，则可以将昂贵的音频处理卸载给 Microsoft。 或者，如果你的 bot 需要直接访问媒体流，我们也支持此方案。 有两种类型的媒体处理：
  * **服务承载的媒体。** Bot 将重点放在管理应用程序工作流 (例如，路由呼叫) 并将音频处理转移到 Microsoft 实时媒体平台。 使用服务托管媒体，可以通过多种方式来实施和托管你的 bot。 服务托管的媒体 bot 可以作为无状态服务实现，因为它不会在本地处理媒体。 服务承载的媒体 bot 可以使用 Api，如 `PlayPrompt` 播放音频剪辑、 `Record` 录制音频剪辑或 `SubscribeToTone` 订阅 DTMF 声音 (例如，了解用户已按0进入操作员) 。
  * **应用程序托管的媒体。** 为了让机器人能够直接访问媒体，它需要特定的图形权限，但在你的 bot 提供程序后， [实时媒体库](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) 和 [图形呼叫 SDK](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder) 可帮助你构建丰富的实时媒体和呼叫机器人。 应用程序托管的 bot 必须托管在 Windows 环境中，如下文中对 [此](./requirements-considerations-application-hosted-media-bots.md)进行了详细介绍。

## <a name="further-reading"></a>进一步阅读

以下是有关如何创建和测试呼叫和联机会议 bot 的详细信息：

* [Graph API 参考](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
* [示例应用](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
* [为呼叫和联机会议 Bot](./registering-calling-bot.md#add-microsoft-graph-permissions) [注册支持呼叫和联机会议](./registering-calling-bot.md)以及 Microsoft Graph 权限的 bot
* [如何在本地电脑上开发呼叫和联机会议 bot](./debugging-local-testing-calling-meeting-bots.md)
* 有关[实时媒体处理的详细信息](./real-time-media-concepts.md)，以及[支持应用程序承载的媒体所需的内容](./requirements-considerations-application-hosted-media-bots.md)
* [有关处理传入呼叫通知的技术信息](./call-notifications.md)
