---
title: 通话和联机会议机器人
description: 了解 Microsoft Teams 应用如何使用语音和视频与用户交互，使用 Microsoft Graph API 进行通话和联机会议。
ms.topic: conceptual
localization_priority: Normal
keywords: 呼叫呼叫 音频视频 IVR 语音联机会议
ms.openlocfilehash: 52a7e1e24fdc0a2c17264087e4f4461b7c43a50a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020167"
---
# <a name="calls-and-online-meetings-bots"></a><span data-ttu-id="09c62-104">通话和联机会议机器人</span><span class="sxs-lookup"><span data-stu-id="09c62-104">Calls and online meetings bots</span></span>

> [!NOTE]
> <span data-ttu-id="09c62-105">Microsoft Teams 移动平台当前不支持对呼叫和联机会议机器人的支持。</span><span class="sxs-lookup"><span data-stu-id="09c62-105">Support for calls and online meeting bots is currently not supported on the Microsoft Teams mobile platform.</span></span>

<span data-ttu-id="09c62-106">机器人可以使用实时语音、视频和屏幕共享与 Teams 通话和会议交互。</span><span class="sxs-lookup"><span data-stu-id="09c62-106">Bots can interact with Teams calls and meetings using real-time voice, video, and screen sharing.</span></span> <span data-ttu-id="09c62-107">借助 [用于通话和联机](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)会议的 Microsoft Graph API，Teams 应用现在可以使用语音和视频与用户交互，以增强体验。</span><span class="sxs-lookup"><span data-stu-id="09c62-107">With [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true), Teams apps can now interact with users using voice and video to enhance the experience.</span></span> <span data-ttu-id="09c62-108">这些 API 允许你添加以下新功能：</span><span class="sxs-lookup"><span data-stu-id="09c62-108">These APIs allow you to add the following new features:</span></span>

* <span data-ttu-id="09c62-109">IVR (互动语音) 。</span><span class="sxs-lookup"><span data-stu-id="09c62-109">Interactive voice response (IVR).</span></span>
* <span data-ttu-id="09c62-110">呼叫控制。</span><span class="sxs-lookup"><span data-stu-id="09c62-110">Call control.</span></span>
* <span data-ttu-id="09c62-111">访问实时音频和视频流，包括桌面应用共享。</span><span class="sxs-lookup"><span data-stu-id="09c62-111">Access to real-time audio and video streams, including desktop and app sharing.</span></span>

<span data-ttu-id="09c62-112">若要在 Teams 应用中使用这些 Graph API，请创建一个自动程序并指定其他一些信息和权限。</span><span class="sxs-lookup"><span data-stu-id="09c62-112">To use these Graph APIs in a Teams app, you create a bot and specify some additional information and permissions.</span></span>

<span data-ttu-id="09c62-113">此外，实时媒体平台使机器人能够使用实时语音、视频和屏幕共享与 Teams 通话和会议进行交互。</span><span class="sxs-lookup"><span data-stu-id="09c62-113">In addition, the Real-time Media Platform enables bots to interact with Teams calls and meetings using real-time voice, video, and screen sharing.</span></span> <span data-ttu-id="09c62-114">参与音频或视频通话和联机会议的机器人是一个普通的 Microsoft Teams 机器人，具有用于注册机器人的一些额外功能。</span><span class="sxs-lookup"><span data-stu-id="09c62-114">A bot that participates in audio or video calls and online meetings is a regular Microsoft Teams bot with few extra features used to register the bot.</span></span>

<span data-ttu-id="09c62-115">Teams 应用清单具有两个附加设置和 、自动程序 Microsoft 应用 ID 的 Graph 权限和租户管理员同意，可 `supportsCalling` `supportsVideo` 让你注册机器人。</span><span class="sxs-lookup"><span data-stu-id="09c62-115">The Teams app manifest with two additional settings `supportsCalling` and `supportsVideo`, Graph permissions for your bot's Microsoft App ID, and tenant admin consent enable you to register the bot.</span></span> <span data-ttu-id="09c62-116">在注册 Teams 的呼叫和会议机器人时，会提到 Webhook URL，它是对自动程序的所有传入呼叫的 webhook 终结点。</span><span class="sxs-lookup"><span data-stu-id="09c62-116">In registering a calls and meetings bot for Teams, the Webhook URL is mentioned, which is the webhook endpoint for all incoming calls to your bot.</span></span> <span data-ttu-id="09c62-117">应用程序托管的媒体机器人需要 Microsoft.Graph.Communications.Calls.Media .NET 库来访问音频和视频媒体流，并且必须在 Azure 中的 Windows Server 计算机或 Windows Server 来宾操作系统 (操作系统) 上部署该机器人。</span><span class="sxs-lookup"><span data-stu-id="09c62-117">An application-hosted media bot requires the Microsoft.Graph.Communications.Calls.Media .NET library to access the audio and video media streams, and the bot must be deployed on a Windows Server machine or Windows Server guest Operating System (OS) in Azure.</span></span> <span data-ttu-id="09c62-118">Teams 上的机器人仅支持音频和视频内容的一组特定的媒体格式。</span><span class="sxs-lookup"><span data-stu-id="09c62-118">Bots on Teams supports only a specific set of media formats for audio and video content.</span></span>

<span data-ttu-id="09c62-119">现在，您必须了解一些核心概念、术语和约定。</span><span class="sxs-lookup"><span data-stu-id="09c62-119">Now, you must understand some core concepts, terminology, and conventions.</span></span>

## <a name="terminologies"></a><span data-ttu-id="09c62-120">术语</span><span class="sxs-lookup"><span data-stu-id="09c62-120">Terminologies</span></span>

<span data-ttu-id="09c62-121">以下核心概念、术语和约定指导你使用呼叫和联机会议机器人：</span><span class="sxs-lookup"><span data-stu-id="09c62-121">The following core concepts, terminology, and conventions guide you through the use of calls and online meetings bots:</span></span>

* <span data-ttu-id="09c62-122">音频或视频呼叫</span><span class="sxs-lookup"><span data-stu-id="09c62-122">Audio or video calls</span></span>
* <span data-ttu-id="09c62-123">呼叫类型</span><span class="sxs-lookup"><span data-stu-id="09c62-123">Call types</span></span>
* <span data-ttu-id="09c62-124">信号</span><span class="sxs-lookup"><span data-stu-id="09c62-124">Signals</span></span>
* <span data-ttu-id="09c62-125">呼叫和联机会议</span><span class="sxs-lookup"><span data-stu-id="09c62-125">Calls and online meetings</span></span>
* <span data-ttu-id="09c62-126">实时媒体</span><span class="sxs-lookup"><span data-stu-id="09c62-126">Real-time media</span></span>

### <a name="audio-or-video-calls"></a><span data-ttu-id="09c62-127">音频或视频呼叫</span><span class="sxs-lookup"><span data-stu-id="09c62-127">Audio or video calls</span></span>

<span data-ttu-id="09c62-128">Teams 中的通话可以纯音频或音频和视频。</span><span class="sxs-lookup"><span data-stu-id="09c62-128">Calls in Teams can be purely audio or audio and video.</span></span> <span data-ttu-id="09c62-129">使用术语呼叫代替音频或视频呼叫。</span><span class="sxs-lookup"><span data-stu-id="09c62-129">Instead of audio or video call, the term call is used.</span></span>

### <a name="call-types"></a><span data-ttu-id="09c62-130">呼叫类型</span><span class="sxs-lookup"><span data-stu-id="09c62-130">Call types</span></span>

<span data-ttu-id="09c62-131">呼叫可以是人员与机器人之间的对等呼叫，或者是机器人与组通话中的两个或多个人员之间的多方呼叫。</span><span class="sxs-lookup"><span data-stu-id="09c62-131">Calls are either peer-to-peer between a person and your bot, or multiparty between your bot and two or more people in a group call.</span></span>

![调用类型](~/assets/images/calls-and-meetings/call-types.png)

<span data-ttu-id="09c62-133">以下是调用所需的不同呼叫类型和权限：</span><span class="sxs-lookup"><span data-stu-id="09c62-133">Following are the different call types and permissions required for the call:</span></span>

* <span data-ttu-id="09c62-134">用户可以使用机器人发起对等呼叫或邀请机器人加入现有的多方呼叫。</span><span class="sxs-lookup"><span data-stu-id="09c62-134">A user can initiate a peer-to-peer call with your bot or invite your bot into an existing multiparty call.</span></span> <span data-ttu-id="09c62-135">Teams 用户界面中尚未启用多方呼叫。</span><span class="sxs-lookup"><span data-stu-id="09c62-135">The multiparty call is not enabled yet in the Teams user interface.</span></span>
* <span data-ttu-id="09c62-136">用户通过自动程序发起对等呼叫不需要 Graph 权限。</span><span class="sxs-lookup"><span data-stu-id="09c62-136">Graph permissions are not necessary for a user to initiate a peer-to-peer call with your bot.</span></span> <span data-ttu-id="09c62-137">机器人需要其他权限才能参与多方呼叫，或者机器人需要其他权限来发起与用户的对等呼叫。</span><span class="sxs-lookup"><span data-stu-id="09c62-137">Additional permissions are needed for your bot to participate in a multiparty call, or for your bot to initiate a peer-to-peer call with a user.</span></span>
* <span data-ttu-id="09c62-138">呼叫可以对等启动，并最终成为多方呼叫。</span><span class="sxs-lookup"><span data-stu-id="09c62-138">A call can start as peer-to-peer and eventually become a multiparty call.</span></span> <span data-ttu-id="09c62-139">如果你的机器人拥有适当的权限，则机器人可以通过邀请其他人来发起多方呼叫。</span><span class="sxs-lookup"><span data-stu-id="09c62-139">Your bot can initiate multiparty calls by inviting others, provided your bot has the proper permissions.</span></span> <span data-ttu-id="09c62-140">如果你的机器人无权参与组通话，并且某位参与者向该呼叫添加了另一个参与者，则你的机器人会从通话中丢弃。</span><span class="sxs-lookup"><span data-stu-id="09c62-140">If your bot does not have permissions to participate in group calls and if a participant adds another participant to the call, your bot is dropped from the call.</span></span>

### <a name="signals"></a><span data-ttu-id="09c62-141">信号</span><span class="sxs-lookup"><span data-stu-id="09c62-141">Signals</span></span>

<span data-ttu-id="09c62-142">有两种类型的信号：传入呼叫和呼叫内。</span><span class="sxs-lookup"><span data-stu-id="09c62-142">There are two types of signals, incoming call and in-call.</span></span> <span data-ttu-id="09c62-143">以下是信号的不同功能：</span><span class="sxs-lookup"><span data-stu-id="09c62-143">Following are the different features of signals:</span></span>

* <span data-ttu-id="09c62-144">若要接收传入呼叫，请在自动程序设置中输入终结点。</span><span class="sxs-lookup"><span data-stu-id="09c62-144">To receive an incoming call, you enter an endpoint in your bot settings.</span></span> <span data-ttu-id="09c62-145">启动传入呼叫时，此终结点将收到通知。</span><span class="sxs-lookup"><span data-stu-id="09c62-145">This endpoint receives a notification when an incoming call is initiated.</span></span> <span data-ttu-id="09c62-146">可以应答呼叫、拒绝呼叫或将其重定向到其他人。</span><span class="sxs-lookup"><span data-stu-id="09c62-146">You can answer the call, reject it, or redirect it to someone else.</span></span>

    ![呼叫处理](~/assets/images/calls-and-meetings/call-handling.png)

* <span data-ttu-id="09c62-148">当机器人正在通话中时，有一些 API 用于将机器人静音和取消静音，以及启动或停止与其他参与者共享视频或桌面内容。</span><span class="sxs-lookup"><span data-stu-id="09c62-148">When a bot is in a call, there are APIs for muting and unmuting the bot and to start or stop sharing video or desktop content with other participants.</span></span>
* <span data-ttu-id="09c62-149">机器人还可以访问参与者列表、邀请新参与者并将其静音。</span><span class="sxs-lookup"><span data-stu-id="09c62-149">The bot can also access the list of participants, invite new participants, and mute them.</span></span>

### <a name="calls-and-online-meetings"></a><span data-ttu-id="09c62-150">呼叫和联机会议</span><span class="sxs-lookup"><span data-stu-id="09c62-150">Calls and online meetings</span></span>

<span data-ttu-id="09c62-151">从 Teams 用户的角度来看，有两种类型的联机会议，即临时会议和计划会议。</span><span class="sxs-lookup"><span data-stu-id="09c62-151">From a Teams user's perspective, there are two kinds of online meetings, ad hoc and scheduled.</span></span> <span data-ttu-id="09c62-152">从机器人的角度来看，这两个联机会议是相同的。</span><span class="sxs-lookup"><span data-stu-id="09c62-152">From a bot's perspective, both online meetings are the same.</span></span> <span data-ttu-id="09c62-153">对于机器人，联机会议是一组参与者之间的多方呼叫，包括会议坐标。</span><span class="sxs-lookup"><span data-stu-id="09c62-153">To a bot, an online meeting is a multiparty call between a set of participants and includes meeting coordinates.</span></span> <span data-ttu-id="09c62-154">会议坐标是会议元数据，包括与会议关联的 `botId` 、 `chatId` `joinUrl` 或 `startTime` `endTime` 等。</span><span class="sxs-lookup"><span data-stu-id="09c62-154">Meeting coordinates are the metadata for the meeting including `botId`, `chatId` associated with the meeting, `joinUrl`, `startTime` or `endTime`, and so on.</span></span>

### <a name="real-time-media"></a><span data-ttu-id="09c62-155">实时媒体</span><span class="sxs-lookup"><span data-stu-id="09c62-155">Real-time media</span></span>

<span data-ttu-id="09c62-156">当机器人参与呼叫或联机会议时，它必须处理音频和视频流。</span><span class="sxs-lookup"><span data-stu-id="09c62-156">When a bot is participating in a call or online meeting, it must deal with audio and video streams.</span></span> <span data-ttu-id="09c62-157">当用户在通话中通话、在摄像头上显示自己或在会议中演示屏幕时，机器人会显示为音频和视频流。</span><span class="sxs-lookup"><span data-stu-id="09c62-157">When users talk on a call, show themselves on a webcam, or present their screens in a meeting, to a bot it is shown as audio and video streams.</span></span> <span data-ttu-id="09c62-158">如果机器人想要说出一些简单的内容，请按 **0** 以在 IVR (交互语音响应中) 接线员，则需要播放 。WAV 文件。</span><span class="sxs-lookup"><span data-stu-id="09c62-158">If a bot wants to say something as simple as, **press 0 to reach the operator** in an interactive voice response (IVR) scenario, it requires playing a .WAV file.</span></span> <span data-ttu-id="09c62-159">这统称为媒体或实时媒体。</span><span class="sxs-lookup"><span data-stu-id="09c62-159">Collectively, this is referred to as media or real-time media.</span></span>

<span data-ttu-id="09c62-160">实时媒体是指必须实时处理媒体（而不是播放以前录制的音频或视频）的方案。</span><span class="sxs-lookup"><span data-stu-id="09c62-160">Real-time media refers to scenarios where media must be processed in real-time, as opposed to playback of previously recorded audio or video.</span></span> <span data-ttu-id="09c62-161">处理媒体流（尤其是实时媒体流）非常复杂。</span><span class="sxs-lookup"><span data-stu-id="09c62-161">Dealing with media streams, particularly real-time media streams, is extremely complex.</span></span> <span data-ttu-id="09c62-162">Microsoft 已创建实时媒体平台来处理这些方案，并尽可能卸载传统繁重的媒体处理工作。</span><span class="sxs-lookup"><span data-stu-id="09c62-162">Microsoft has created the Real-time Media Platform to handle these scenarios and to offload as much of the traditional heavy lifting of real-time media processing as possible.</span></span> <span data-ttu-id="09c62-163">当机器人应答传入呼叫或加入新呼叫或现有呼叫时，需要告诉实时媒体平台如何处理媒体。</span><span class="sxs-lookup"><span data-stu-id="09c62-163">When the bot answers an incoming call or joins a new or existing call, it needs to tell the Real-time Media Platform how media is handled.</span></span> <span data-ttu-id="09c62-164">如果要构建 IVR 应用程序，可以将昂贵的音频处理卸载到 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="09c62-164">If you are building an IVR application, you can offload the expensive audio processing to Microsoft.</span></span> <span data-ttu-id="09c62-165">或者，如果你的机器人需要直接访问媒体流，则也支持该方案。</span><span class="sxs-lookup"><span data-stu-id="09c62-165">Alternately, if your bot requires direct access to media streams, that scenario is also supported.</span></span> <span data-ttu-id="09c62-166">有两种类型的媒体处理：</span><span class="sxs-lookup"><span data-stu-id="09c62-166">There are two types of media processing:</span></span>

* <span data-ttu-id="09c62-167">**服务托管的媒体**：机器人专注于管理应用程序工作流，例如将呼叫路由和将音频处理卸载到 Microsoft 实时媒体平台。</span><span class="sxs-lookup"><span data-stu-id="09c62-167">**Service-hosted media**: Bots focus on managing application workflow, such as routing calls and offload audio processing to the Microsoft Real-time Media Platform.</span></span> <span data-ttu-id="09c62-168">借助服务托管的媒体，有几种实现和托管机器人的选项。</span><span class="sxs-lookup"><span data-stu-id="09c62-168">With service-hosted media, you have several options to implement and host your bot.</span></span> <span data-ttu-id="09c62-169">服务托管的媒体机器人可以作为无状态服务进行实施，因为它不在本地处理媒体。</span><span class="sxs-lookup"><span data-stu-id="09c62-169">A service-hosted media bot can be implemented as a stateless service as it does not process media locally.</span></span> <span data-ttu-id="09c62-170">服务托管的媒体机器人可以使用以下 API：</span><span class="sxs-lookup"><span data-stu-id="09c62-170">Service-hosted media bots can use the following APIs:</span></span>

    * <span data-ttu-id="09c62-171">`PlayPrompt` 用于播放音频剪辑。</span><span class="sxs-lookup"><span data-stu-id="09c62-171">`PlayPrompt` for playing an audio clip.</span></span>
    * <span data-ttu-id="09c62-172">`Record` 用于录制音频剪辑。</span><span class="sxs-lookup"><span data-stu-id="09c62-172">`Record` for recording audio clips.</span></span>
    * <span data-ttu-id="09c62-173">`SubscribeToTone` 用于订阅双音多频 (DTMF) 音。</span><span class="sxs-lookup"><span data-stu-id="09c62-173">`SubscribeToTone` for subscribing to dual tone multiple frequency (DTMF) tones.</span></span>

    <span data-ttu-id="09c62-174">例如，知道用户何时按 **0** 到达接线员。</span><span class="sxs-lookup"><span data-stu-id="09c62-174">For example, knowing when a user has pressed **0** to reach the operator.</span></span>

* <span data-ttu-id="09c62-175">**应用程序托管的媒体**：若要让机器人直接访问媒体，它需要特定的 Graph 权限。</span><span class="sxs-lookup"><span data-stu-id="09c62-175">**Application-hosted media**: For a bot to get direct access to the media, it needs a specific Graph permission.</span></span> <span data-ttu-id="09c62-176">在机器人拥有权限后，实时媒体[](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)库和 Graph 调用[SDK](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder)可帮助你生成丰富的实时媒体和通话机器人。</span><span class="sxs-lookup"><span data-stu-id="09c62-176">After your bot has the permission, the [Real-time Media Library](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/), and the [Graph calling SDK](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder) helps you build rich, real-time media, and calling bots.</span></span> <span data-ttu-id="09c62-177">必须在 Windows 环境中托管应用程序托管的机器人。</span><span class="sxs-lookup"><span data-stu-id="09c62-177">An application-hosted bot must be hosted in a Windows environment.</span></span> <span data-ttu-id="09c62-178">有关详细信息，请参阅 [应用程序托管的媒体机器人](./requirements-considerations-application-hosted-media-bots.md)。</span><span class="sxs-lookup"><span data-stu-id="09c62-178">For more information, see [application-hosted media bots](./requirements-considerations-application-hosted-media-bots.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="09c62-179">代码示例</span><span class="sxs-lookup"><span data-stu-id="09c62-179">Code sample</span></span>

| <span data-ttu-id="09c62-180">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="09c62-180">**Sample name**</span></span> | <span data-ttu-id="09c62-181">**描述**</span><span class="sxs-lookup"><span data-stu-id="09c62-181">**Description**</span></span> | <span data-ttu-id="09c62-182">**Graph**</span><span class="sxs-lookup"><span data-stu-id="09c62-182">**Graph**</span></span> |
|---------------|----------|--------|
| <span data-ttu-id="09c62-183">图形通信</span><span class="sxs-lookup"><span data-stu-id="09c62-183">Graph communication</span></span> | <span data-ttu-id="09c62-184">图形通信以与 Microsoft 的通信平台交互。</span><span class="sxs-lookup"><span data-stu-id="09c62-184">Graph communications to interact with Microsoft's communications platform.</span></span> | [<span data-ttu-id="09c62-185">View</span><span class="sxs-lookup"><span data-stu-id="09c62-185">View</span></span>](https://github.com/microsoftgraph/microsoft-graph-comms-samples) |

## <a name="see-also"></a><span data-ttu-id="09c62-186">另请参阅</span><span class="sxs-lookup"><span data-stu-id="09c62-186">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="09c62-187">图形 API 参考</span><span class="sxs-lookup"><span data-stu-id="09c62-187">Graph API reference</span></span>](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
> [!div class="nextstepaction"]
> [<span data-ttu-id="09c62-188">示例应用</span><span class="sxs-lookup"><span data-stu-id="09c62-188">Sample apps</span></span>](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
> [!div class="nextstepaction"]
> [<span data-ttu-id="09c62-189">注册支持通话和联机会议的机器人</span><span class="sxs-lookup"><span data-stu-id="09c62-189">Registering a bot that supports calls and online meetings</span></span>](./registering-calling-bot.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="09c62-190">呼叫和联机会议机器人的图形权限</span><span class="sxs-lookup"><span data-stu-id="09c62-190">Graph permissions for calls and online meetings bots</span></span>](./registering-calling-bot.md#add-graph-permissions)
> [!div class="nextstepaction"]
> [<span data-ttu-id="09c62-191">如何在计算机上开发通话和联机会议机器人</span><span class="sxs-lookup"><span data-stu-id="09c62-191">How to develop calling and online meeting bots on your computer</span></span>](./debugging-local-testing-calling-meeting-bots.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="09c62-192">应用程序托管的媒体机器人的要求和注意事项</span><span class="sxs-lookup"><span data-stu-id="09c62-192">Requirements and considerations for application-hosted media bots</span></span>](./requirements-considerations-application-hosted-media-bots.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="09c62-193">有关处理传入呼叫通知的技术信息</span><span class="sxs-lookup"><span data-stu-id="09c62-193">Technical information on handling incoming call notifications</span></span>](./call-notifications.md)

## <a name="next-step"></a><span data-ttu-id="09c62-194">后续步骤</span><span class="sxs-lookup"><span data-stu-id="09c62-194">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="09c62-195">实时媒体通话与会议</span><span class="sxs-lookup"><span data-stu-id="09c62-195">Real-time media calls and meetings</span></span>](~/bots/calls-and-meetings/real-time-media-concepts.md)
