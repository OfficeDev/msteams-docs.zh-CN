---
title: 通话和联机会议机器人
description: 了解 Microsoft Teams 应用如何使用语音和视频与用户交互，使用 Microsoft Graph API 进行通话和联机会议。
keywords: 呼叫呼叫 音频视频 IVR 语音联机会议
ms.openlocfilehash: 0fcf420ba8d698404d00bb2cab3d61cab2245f40
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034640"
---
# <a name="calls-and-online-meetings-bots"></a>通话和联机会议机器人

通过添加用于通话和联机会议的 [Microsoft Graph API，Microsoft](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)Teams 应用现在可以通过多种使用语音和视频的方式与用户进行交互。 这些 API 允许你添加新功能，例如交互式语音响应 (IVR) 、呼叫控制，以及访问通话和会议实时音频流和/或视频流，包括桌面应用共享。

若要在 Microsoft Teams 应用中使用这些 Microsoft Graph API，你可以创建一个自动程序并指定一些附加信息和权限，我们将在其他地方介绍这些信息和权限，但首先，了解一些核心概念、术语和约定非常重要：

* **音频/视频呼叫。** Teams 中的通话可以纯音频或音频+视频。 为简单起见，我们不会在任何地方都说"音频/视频呼叫";我们只需说"呼叫"。
* **呼叫类型。** 呼叫是一个人与机器人 (之间的对等呼叫) 或多方 (机器人和两个或多个群组通话) 。
  ![CallingTypes ](~/assets/images/calls-and-meetings/call-types.png) ：
  * 用户可以使用机器人发起对等呼叫，或邀请机器人加入现有多方呼叫 (尽管 Microsoft Teams UI 服务中尚未启用后者) 。
  
  > [!NOTE]
  > Microsoft Teams 移动平台当前不支持用户发起的机器人呼叫。 
  
  * 用户无需使用 Microsoft Graph 权限通过机器人发起对等呼叫，但机器人需要其他权限才能参与多方呼叫，或者自动程序需要其他权限才能与用户发起对等呼叫。
  * 呼叫可以点对点开始并升级为多方。 如果你的机器人拥有适当的权限，则机器人可以通过邀请其他人来发起此升级。 如果你的机器人没有参与组呼叫的权限，并且一个参与者添加了另一方，则你的机器人会从通话中被删除。
* **信号。** 有两种类型的信号 - 传入呼叫和呼叫内信号：
  * 若要接收传入呼叫，您可以在自动程序设置中指定终结点;传入呼叫到达时，此终结点将收到通知。 可以应答呼叫、拒绝呼叫或将其重定向到其他位置或其他人。
  ![呼叫类型](~/assets/images/calls-and-meetings/call-handling.png)
  * 当机器人在通话中时，存在用于将自身静音和取消静音以及开始/停止与其他参与者共享视频/桌面内容的 API。
  * 机器人还可以访问参与者列表、邀请新参与者并将其静音。
* **通话和联机会议。** 从 Teams 用户的角度来看，有两种类型的联机会议— 临时和计划。 但是，从自动程序的角度来看，这两者是相同的。 对于机器人，联机会议只是多方呼叫 (一组参与者) 加上"会议坐标"，你可以将这些呼叫视为会议元数据：、与会议关联的、 、 等。 `botId` `chatId` `joinUrl` `startTime` / `endTime`
* **实时媒体。** 当机器人参与呼叫或联机会议时，它必须处理音频和视频流。 当用户在通话中通话、在摄像头上显示自己或在会议中显示其屏幕时，机器人会"看到"这一点作为音频流和/或视频流。 如果机器人想要说出内容或显示屏幕内容，则需要音频或视频流。 甚至像机器人在 IVR 中说"按 0 到达接线员"一样简单 (互动语音响应) 播放 。WAV 文件。 我们统称为媒体或实时媒体 (是指必须实时处理媒体的方案，而不是播放以前录制的音频/视频) 。 过去，处理媒体流（尤其是实时媒体流）对于开发人员来说非常复杂。 Microsoft 已创建 _实时媒体_ 平台来处理这些用例，并尽可能卸载传统"繁重"实时媒体处理。  当机器人接听来电或加入新呼叫或现有呼叫时，需要告诉实时媒体平台如何处理媒体。 如果要构建 IVR 应用程序，可以将昂贵的音频处理卸载到 Microsoft。 或者，如果你的机器人需要直接访问媒体流，我们也支持该方案。 有两种类型的媒体处理：
  * **服务托管的媒体。** 机器人专注于管理应用程序工作流 (例如，将呼叫路由到) ，以及将音频处理卸载到 Microsoft 实时媒体平台。 借助服务托管的媒体，有几种实现和托管机器人的选项。 服务托管的媒体自动程序可以实施为无状态服务，因为它不在本地处理媒体。 服务托管的媒体机器人可以使用 API，例如播放音频剪辑、录制音频剪辑或订阅 DTMF 音调 (例如，知道用户何时按 0 到达话务员 `PlayPrompt` `Record` `SubscribeToTone`) 。
  * **应用程序托管的媒体。** 若要让机器人直接访问媒体，它需要特定的 Graph 权限，但一旦机器人拥有该权限，实时媒体库和[](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)Graph 调用[SDK](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder)可帮助你生成丰富的实时媒体，调用机器人。 应用程序托管的自动程序必须托管在 Windows 环境中，如此处所 [介绍的更多详细信息](./requirements-considerations-application-hosted-media-bots.md)。

## <a name="further-reading"></a>进一步阅读

下面详细了解如何创建和测试通话和联机会议机器人：

* [图形 API 参考](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
* [示例应用](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
* [注册支持通话和联机](./registering-calling-bot.md) 会议的机器人，以及针对通话和联机会议机器人的 [Microsoft Graph 权限](./registering-calling-bot.md#add-microsoft-graph-permissions)
* [如何在本地电脑上开发通话和联机会议机器人](./debugging-local-testing-calling-meeting-bots.md)
* [有关实时媒体处理以及](./real-time-media-concepts.md)支持应用程序托管媒体 [所需的内容详细信息](./requirements-considerations-application-hosted-media-bots.md)
* [有关处理传入呼叫通知的技术信息](./call-notifications.md)
