---
title: 通话和联机会议机器人
description: 了解你的Microsoft Teams应用如何使用语音和视频与用户使用 Microsoft Graph API 进行通话和联机会议交互。
ms.topic: conceptual
localization_priority: Normal
keywords: 呼叫呼叫 音频视频 IVR 语音联机会议
ms.openlocfilehash: d4cec30e110eed5f73929305cc43b84eed4d7524
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058311"
---
# <a name="calls-and-online-meetings-bots"></a><span data-ttu-id="5893e-104">通话和联机会议机器人</span><span class="sxs-lookup"><span data-stu-id="5893e-104">Calls and online meetings bots</span></span>

> [!NOTE]
> <span data-ttu-id="5893e-105">当前不支持在移动平台上支持Microsoft Teams聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="5893e-105">Support for calls and online meeting bots is currently not supported on the Microsoft Teams mobile platform.</span></span>

<span data-ttu-id="5893e-106">机器人可以使用实时Teams、视频和屏幕共享与呼叫和会议进行交互。</span><span class="sxs-lookup"><span data-stu-id="5893e-106">Bots can interact with Teams calls and meetings using real-time voice, video, and screen sharing.</span></span> <span data-ttu-id="5893e-107">借助[Microsoft Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)API 进行呼叫和联机会议，Teams应用现在可以使用语音和视频与用户进行交互，以增强体验。</span><span class="sxs-lookup"><span data-stu-id="5893e-107">With [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true), Teams apps can now interact with users using voice and video to enhance the experience.</span></span> <span data-ttu-id="5893e-108">这些 API 允许你添加以下新功能：</span><span class="sxs-lookup"><span data-stu-id="5893e-108">These APIs allow you to add the following new features:</span></span>

* <span data-ttu-id="5893e-109">IVR (互动语音) 。</span><span class="sxs-lookup"><span data-stu-id="5893e-109">Interactive voice response (IVR).</span></span>
* <span data-ttu-id="5893e-110">呼叫控制。</span><span class="sxs-lookup"><span data-stu-id="5893e-110">Call control.</span></span>
* <span data-ttu-id="5893e-111">访问实时音频和视频流，包括桌面应用共享。</span><span class="sxs-lookup"><span data-stu-id="5893e-111">Access to real-time audio and video streams, including desktop and app sharing.</span></span>

<span data-ttu-id="5893e-112">若要在 Graph应用中使用这些 Teams API，请创建一个自动程序并指定其他一些信息和权限。</span><span class="sxs-lookup"><span data-stu-id="5893e-112">To use these Graph APIs in a Teams app, you create a bot and specify some additional information and permissions.</span></span>

<span data-ttu-id="5893e-113">此外，实时媒体平台还允许机器人使用实时Teams、视频和屏幕共享与通话和会议进行交互。</span><span class="sxs-lookup"><span data-stu-id="5893e-113">In addition, the Real-time Media Platform enables bots to interact with Teams calls and meetings using real-time voice, video, and screen sharing.</span></span> <span data-ttu-id="5893e-114">参与音频或视频呼叫和联机会议的机器人是一种Microsoft Teams聊天机器人，具有用于注册机器人的一些额外功能。</span><span class="sxs-lookup"><span data-stu-id="5893e-114">A bot that participates in audio or video calls and online meetings is a regular Microsoft Teams bot with few extra features used to register the bot.</span></span>

<span data-ttu-id="5893e-115">The Teams app manifest with two additional settings `supportsCalling` and `supportsVideo` ， Graph permissions for your bot's Microsoft App ID， and tenant admin consent enable you to register the bot.</span><span class="sxs-lookup"><span data-stu-id="5893e-115">The Teams app manifest with two additional settings `supportsCalling` and `supportsVideo`, Graph permissions for your bot's Microsoft App ID, and tenant admin consent enable you to register the bot.</span></span> <span data-ttu-id="5893e-116">为聊天机器人注册Teams时，会提到 Webhook URL，它是对自动程序的所有传入呼叫的 webhook 终结点。</span><span class="sxs-lookup"><span data-stu-id="5893e-116">In registering a calls and meetings bot for Teams, the Webhook URL is mentioned, which is the webhook endpoint for all incoming calls to your bot.</span></span> <span data-ttu-id="5893e-117">应用程序托管的媒体机器人需要 Microsoft。Graph。Communications.Calls.Media .NET 库，用于访问音频和视频媒体流，机器人必须部署在 Azure 中的 Windows Server 计算机或 Windows Server 来宾操作系统 (OS) 上。</span><span class="sxs-lookup"><span data-stu-id="5893e-117">An application-hosted media bot requires the Microsoft.Graph.Communications.Calls.Media .NET library to access the audio and video media streams, and the bot must be deployed on a Windows Server machine or Windows Server guest Operating System (OS) in Azure.</span></span> <span data-ttu-id="5893e-118">自动程序Teams音频和视频内容仅支持一组特定的媒体格式。</span><span class="sxs-lookup"><span data-stu-id="5893e-118">Bots on Teams supports only a specific set of media formats for audio and video content.</span></span>

<span data-ttu-id="5893e-119">现在，您必须了解一些核心概念、术语和约定。</span><span class="sxs-lookup"><span data-stu-id="5893e-119">Now, you must understand some core concepts, terminology, and conventions.</span></span>

## <a name="terminologies"></a><span data-ttu-id="5893e-120">术语</span><span class="sxs-lookup"><span data-stu-id="5893e-120">Terminologies</span></span>

<span data-ttu-id="5893e-121">以下核心概念、术语和约定指导你使用呼叫和联机会议机器人：</span><span class="sxs-lookup"><span data-stu-id="5893e-121">The following core concepts, terminology, and conventions guide you through the use of calls and online meetings bots:</span></span>

* <span data-ttu-id="5893e-122">音频或视频呼叫</span><span class="sxs-lookup"><span data-stu-id="5893e-122">Audio or video calls</span></span>
* <span data-ttu-id="5893e-123">呼叫类型</span><span class="sxs-lookup"><span data-stu-id="5893e-123">Call types</span></span>
* <span data-ttu-id="5893e-124">信号</span><span class="sxs-lookup"><span data-stu-id="5893e-124">Signals</span></span>
* <span data-ttu-id="5893e-125">呼叫和联机会议</span><span class="sxs-lookup"><span data-stu-id="5893e-125">Calls and online meetings</span></span>
* <span data-ttu-id="5893e-126">实时媒体</span><span class="sxs-lookup"><span data-stu-id="5893e-126">Real-time media</span></span>

### <a name="audio-or-video-calls"></a><span data-ttu-id="5893e-127">音频或视频呼叫</span><span class="sxs-lookup"><span data-stu-id="5893e-127">Audio or video calls</span></span>

<span data-ttu-id="5893e-128">呼叫Teams可以是纯音频或音频和视频。</span><span class="sxs-lookup"><span data-stu-id="5893e-128">Calls in Teams can be purely audio or audio and video.</span></span> <span data-ttu-id="5893e-129">使用术语呼叫代替音频或视频呼叫。</span><span class="sxs-lookup"><span data-stu-id="5893e-129">Instead of audio or video call, the term call is used.</span></span>

### <a name="call-types"></a><span data-ttu-id="5893e-130">呼叫类型</span><span class="sxs-lookup"><span data-stu-id="5893e-130">Call types</span></span>

<span data-ttu-id="5893e-131">呼叫可以是人员与机器人之间的对等呼叫，或者是机器人与组通话中的两个或多个人员之间的多方呼叫。</span><span class="sxs-lookup"><span data-stu-id="5893e-131">Calls are either peer-to-peer between a person and your bot, or multiparty between your bot and two or more people in a group call.</span></span>

![调用类型](~/assets/images/calls-and-meetings/call-types.png)

<span data-ttu-id="5893e-133">以下是调用所需的不同呼叫类型和权限：</span><span class="sxs-lookup"><span data-stu-id="5893e-133">Following are the different call types and permissions required for the call:</span></span>

* <span data-ttu-id="5893e-134">用户可以使用机器人发起对等呼叫或邀请机器人加入现有的多方呼叫。</span><span class="sxs-lookup"><span data-stu-id="5893e-134">A user can initiate a peer-to-peer call with your bot or invite your bot into an existing multiparty call.</span></span> <span data-ttu-id="5893e-135">多部分调用尚未在 Teams用户界面中启用。</span><span class="sxs-lookup"><span data-stu-id="5893e-135">The multiparty call is not enabled yet in the Teams user interface.</span></span>
* <span data-ttu-id="5893e-136">Graph自动程序发起对等呼叫不需要权限。</span><span class="sxs-lookup"><span data-stu-id="5893e-136">Graph permissions are not necessary for a user to initiate a peer-to-peer call with your bot.</span></span> <span data-ttu-id="5893e-137">机器人需要其他权限才能参与多方呼叫，或者机器人需要其他权限来发起与用户的对等呼叫。</span><span class="sxs-lookup"><span data-stu-id="5893e-137">Additional permissions are needed for your bot to participate in a multiparty call, or for your bot to initiate a peer-to-peer call with a user.</span></span>
* <span data-ttu-id="5893e-138">呼叫可以对等启动，并最终成为多方呼叫。</span><span class="sxs-lookup"><span data-stu-id="5893e-138">A call can start as peer-to-peer and eventually become a multiparty call.</span></span> <span data-ttu-id="5893e-139">如果你的机器人拥有适当的权限，则机器人可以通过邀请其他人来发起多方呼叫。</span><span class="sxs-lookup"><span data-stu-id="5893e-139">Your bot can initiate multiparty calls by inviting others, provided your bot has the proper permissions.</span></span> <span data-ttu-id="5893e-140">如果你的机器人无权参与组通话，并且某位参与者向该呼叫添加了另一个参与者，则你的机器人会从通话中丢弃。</span><span class="sxs-lookup"><span data-stu-id="5893e-140">If your bot does not have permissions to participate in group calls and if a participant adds another participant to the call, your bot is dropped from the call.</span></span>

### <a name="signals"></a><span data-ttu-id="5893e-141">信号</span><span class="sxs-lookup"><span data-stu-id="5893e-141">Signals</span></span>

<span data-ttu-id="5893e-142">有两种类型的信号：传入呼叫和呼叫内。</span><span class="sxs-lookup"><span data-stu-id="5893e-142">There are two types of signals, incoming call and in-call.</span></span> <span data-ttu-id="5893e-143">以下是信号的不同功能：</span><span class="sxs-lookup"><span data-stu-id="5893e-143">Following are the different features of signals:</span></span>

* <span data-ttu-id="5893e-144">若要接收传入呼叫，请在自动程序设置中输入终结点。</span><span class="sxs-lookup"><span data-stu-id="5893e-144">To receive an incoming call, you enter an endpoint in your bot settings.</span></span> <span data-ttu-id="5893e-145">启动传入呼叫时，此终结点将收到通知。</span><span class="sxs-lookup"><span data-stu-id="5893e-145">This endpoint receives a notification when an incoming call is initiated.</span></span> <span data-ttu-id="5893e-146">可以应答呼叫、拒绝呼叫或将其重定向到其他人。</span><span class="sxs-lookup"><span data-stu-id="5893e-146">You can answer the call, reject it, or redirect it to someone else.</span></span>

    ![呼叫处理](~/assets/images/calls-and-meetings/call-handling.png)

* <span data-ttu-id="5893e-148">当机器人正在通话中时，有一些 API 用于将机器人静音和取消静音，以及启动或停止与其他参与者共享视频或桌面内容。</span><span class="sxs-lookup"><span data-stu-id="5893e-148">When a bot is in a call, there are APIs for muting and unmuting the bot and to start or stop sharing video or desktop content with other participants.</span></span>
* <span data-ttu-id="5893e-149">机器人还可以访问参与者列表、邀请新参与者并将其静音。</span><span class="sxs-lookup"><span data-stu-id="5893e-149">The bot can also access the list of participants, invite new participants, and mute them.</span></span>

### <a name="calls-and-online-meetings"></a><span data-ttu-id="5893e-150">呼叫和联机会议</span><span class="sxs-lookup"><span data-stu-id="5893e-150">Calls and online meetings</span></span>

<span data-ttu-id="5893e-151">从Teams的角度来看，有两种类型的联机会议，即临时会议和计划会议。</span><span class="sxs-lookup"><span data-stu-id="5893e-151">From a Teams user's perspective, there are two kinds of online meetings, ad hoc and scheduled.</span></span> <span data-ttu-id="5893e-152">从机器人的角度来看，这两个联机会议是相同的。</span><span class="sxs-lookup"><span data-stu-id="5893e-152">From a bot's perspective, both online meetings are the same.</span></span> <span data-ttu-id="5893e-153">对于机器人，联机会议是一组参与者之间的多方呼叫，包括会议坐标。</span><span class="sxs-lookup"><span data-stu-id="5893e-153">To a bot, an online meeting is a multiparty call between a set of participants and includes meeting coordinates.</span></span> <span data-ttu-id="5893e-154">会议坐标是会议元数据，包括与会议关联的 `botId` 、 `chatId` `joinUrl` 或 `startTime` `endTime` 等。</span><span class="sxs-lookup"><span data-stu-id="5893e-154">Meeting coordinates are the metadata for the meeting including `botId`, `chatId` associated with the meeting, `joinUrl`, `startTime` or `endTime`, and so on.</span></span>

### <a name="real-time-media"></a><span data-ttu-id="5893e-155">实时媒体</span><span class="sxs-lookup"><span data-stu-id="5893e-155">Real-time media</span></span>

<span data-ttu-id="5893e-156">当机器人参与呼叫或联机会议时，它必须处理音频和视频流。</span><span class="sxs-lookup"><span data-stu-id="5893e-156">When a bot is participating in a call or online meeting, it must deal with audio and video streams.</span></span> <span data-ttu-id="5893e-157">当用户在通话中通话、在摄像头上显示自己或在会议中演示屏幕时，机器人会显示为音频和视频流。</span><span class="sxs-lookup"><span data-stu-id="5893e-157">When users talk on a call, show themselves on a webcam, or present their screens in a meeting, to a bot it is shown as audio and video streams.</span></span> <span data-ttu-id="5893e-158">如果机器人想要说出一些简单的内容，请按 **0** 以在 IVR (交互语音响应中) 接线员，则需要播放 。WAV 文件。</span><span class="sxs-lookup"><span data-stu-id="5893e-158">If a bot wants to say something as simple as, **press 0 to reach the operator** in an interactive voice response (IVR) scenario, it requires playing a .WAV file.</span></span> <span data-ttu-id="5893e-159">这统称为媒体或实时媒体。</span><span class="sxs-lookup"><span data-stu-id="5893e-159">Collectively, this is referred to as media or real-time media.</span></span>

<span data-ttu-id="5893e-160">实时媒体是指必须实时处理媒体（而不是播放以前录制的音频或视频）的方案。</span><span class="sxs-lookup"><span data-stu-id="5893e-160">Real-time media refers to scenarios where media must be processed in real-time, as opposed to playback of previously recorded audio or video.</span></span> <span data-ttu-id="5893e-161">处理媒体流（尤其是实时媒体流）非常复杂。</span><span class="sxs-lookup"><span data-stu-id="5893e-161">Dealing with media streams, particularly real-time media streams, is extremely complex.</span></span> <span data-ttu-id="5893e-162">Microsoft 已创建实时媒体平台来处理这些方案，并尽可能卸载传统繁重的媒体处理工作。</span><span class="sxs-lookup"><span data-stu-id="5893e-162">Microsoft has created the Real-time Media Platform to handle these scenarios and to offload as much of the traditional heavy lifting of real-time media processing as possible.</span></span> <span data-ttu-id="5893e-163">当机器人应答传入呼叫或加入新呼叫或现有呼叫时，需要告诉实时媒体平台如何处理媒体。</span><span class="sxs-lookup"><span data-stu-id="5893e-163">When the bot answers an incoming call or joins a new or existing call, it needs to tell the Real-time Media Platform how media is handled.</span></span> <span data-ttu-id="5893e-164">如果要构建 IVR 应用程序，可以将昂贵的音频处理卸载到 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="5893e-164">If you are building an IVR application, you can offload the expensive audio processing to Microsoft.</span></span> <span data-ttu-id="5893e-165">或者，如果你的机器人需要直接访问媒体流，则也支持该方案。</span><span class="sxs-lookup"><span data-stu-id="5893e-165">Alternately, if your bot requires direct access to media streams, that scenario is also supported.</span></span> <span data-ttu-id="5893e-166">有两种类型的媒体处理：</span><span class="sxs-lookup"><span data-stu-id="5893e-166">There are two types of media processing:</span></span>

* <span data-ttu-id="5893e-167">**服务托管的媒体**：机器人专注于管理应用程序工作流，例如将呼叫路由和将音频处理卸载到 Microsoft 实时媒体平台。</span><span class="sxs-lookup"><span data-stu-id="5893e-167">**Service-hosted media**: Bots focus on managing application workflow, such as routing calls and offload audio processing to the Microsoft Real-time Media Platform.</span></span> <span data-ttu-id="5893e-168">借助服务托管的媒体，有几种实现和托管机器人的选项。</span><span class="sxs-lookup"><span data-stu-id="5893e-168">With service-hosted media, you have several options to implement and host your bot.</span></span> <span data-ttu-id="5893e-169">服务托管的媒体机器人可以作为无状态服务进行实施，因为它不在本地处理媒体。</span><span class="sxs-lookup"><span data-stu-id="5893e-169">A service-hosted media bot can be implemented as a stateless service as it does not process media locally.</span></span> <span data-ttu-id="5893e-170">服务托管的媒体机器人可以使用以下 API：</span><span class="sxs-lookup"><span data-stu-id="5893e-170">Service-hosted media bots can use the following APIs:</span></span>

    * <span data-ttu-id="5893e-171">`PlayPrompt` 用于播放音频剪辑。</span><span class="sxs-lookup"><span data-stu-id="5893e-171">`PlayPrompt` for playing an audio clip.</span></span>
    * <span data-ttu-id="5893e-172">`Record` 用于录制音频剪辑。</span><span class="sxs-lookup"><span data-stu-id="5893e-172">`Record` for recording audio clips.</span></span>
    * <span data-ttu-id="5893e-173">`SubscribeToTone` 用于订阅双音多频 (DTMF) 音。</span><span class="sxs-lookup"><span data-stu-id="5893e-173">`SubscribeToTone` for subscribing to dual tone multiple frequency (DTMF) tones.</span></span>

    <span data-ttu-id="5893e-174">例如，知道用户何时按 **0** 到达接线员。</span><span class="sxs-lookup"><span data-stu-id="5893e-174">For example, knowing when a user has pressed **0** to reach the operator.</span></span>

* <span data-ttu-id="5893e-175">**应用程序托管的媒体**：若要使机器人直接访问媒体，它需要特定的Graph权限。</span><span class="sxs-lookup"><span data-stu-id="5893e-175">**Application-hosted media**: For a bot to get direct access to the media, it needs a specific Graph permission.</span></span> <span data-ttu-id="5893e-176">在机器人拥有权限后，实时媒体[](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)库和 Graph[调用 SDK](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder)可帮助你生成丰富的实时媒体和通话机器人。</span><span class="sxs-lookup"><span data-stu-id="5893e-176">After your bot has the permission, the [Real-time Media Library](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/), and the [Graph calling SDK](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder) helps you build rich, real-time media, and calling bots.</span></span> <span data-ttu-id="5893e-177">必须在 Windows 环境中托管应用程序托管的机器人。</span><span class="sxs-lookup"><span data-stu-id="5893e-177">An application-hosted bot must be hosted in a Windows environment.</span></span> <span data-ttu-id="5893e-178">有关详细信息，请参阅 [应用程序托管的媒体机器人](./requirements-considerations-application-hosted-media-bots.md)。</span><span class="sxs-lookup"><span data-stu-id="5893e-178">For more information, see [application-hosted media bots](./requirements-considerations-application-hosted-media-bots.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="5893e-179">代码示例</span><span class="sxs-lookup"><span data-stu-id="5893e-179">Code sample</span></span>

| <span data-ttu-id="5893e-180">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="5893e-180">**Sample name**</span></span> | <span data-ttu-id="5893e-181">**说明**</span><span class="sxs-lookup"><span data-stu-id="5893e-181">**Description**</span></span> | <span data-ttu-id="5893e-182">**Graph**</span><span class="sxs-lookup"><span data-stu-id="5893e-182">**Graph**</span></span> |
|---------------|----------|--------|
| <span data-ttu-id="5893e-183">Graph通信</span><span class="sxs-lookup"><span data-stu-id="5893e-183">Graph communication</span></span> | <span data-ttu-id="5893e-184">Graph与 Microsoft 的通信平台进行交互。</span><span class="sxs-lookup"><span data-stu-id="5893e-184">Graph communications to interact with Microsoft's communications platform.</span></span> | [<span data-ttu-id="5893e-185">View</span><span class="sxs-lookup"><span data-stu-id="5893e-185">View</span></span>](https://github.com/microsoftgraph/microsoft-graph-comms-samples) |

## <a name="see-also"></a><span data-ttu-id="5893e-186">另请参阅</span><span class="sxs-lookup"><span data-stu-id="5893e-186">See also</span></span>

- [<span data-ttu-id="5893e-187">GraphAPI 参考</span><span class="sxs-lookup"><span data-stu-id="5893e-187">Graph API reference</span></span>](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)

- [<span data-ttu-id="5893e-188">示例应用</span><span class="sxs-lookup"><span data-stu-id="5893e-188">Sample apps</span></span>](https://github.com/microsoftgraph/microsoft-graph-comms-samples)

- [<span data-ttu-id="5893e-189">注册支持通话和联机会议的机器人</span><span class="sxs-lookup"><span data-stu-id="5893e-189">Registering a bot that supports calls and online meetings</span></span>](./registering-calling-bot.md)

- [<span data-ttu-id="5893e-190">Graph聊天机器人的联机会议权限</span><span class="sxs-lookup"><span data-stu-id="5893e-190">Graph permissions for calls and online meetings bots</span></span>](./registering-calling-bot.md#add-graph-permissions)

- [<span data-ttu-id="5893e-191">如何在计算机上开发通话和联机会议机器人</span><span class="sxs-lookup"><span data-stu-id="5893e-191">How to develop calling and online meeting bots on your computer</span></span>](./debugging-local-testing-calling-meeting-bots.md)

- [<span data-ttu-id="5893e-192">应用程序托管的媒体机器人的要求和注意事项</span><span class="sxs-lookup"><span data-stu-id="5893e-192">Requirements and considerations for application-hosted media bots</span></span>](./requirements-considerations-application-hosted-media-bots.md)

- [<span data-ttu-id="5893e-193">有关处理传入呼叫通知的技术信息</span><span class="sxs-lookup"><span data-stu-id="5893e-193">Technical information on handling incoming call notifications</span></span>](./call-notifications.md)

## <a name="next-step"></a><span data-ttu-id="5893e-194">后续步骤</span><span class="sxs-lookup"><span data-stu-id="5893e-194">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5893e-195">实时媒体通话与会议</span><span class="sxs-lookup"><span data-stu-id="5893e-195">Real-time media calls and meetings</span></span>](~/bots/calls-and-meetings/real-time-media-concepts.md)
