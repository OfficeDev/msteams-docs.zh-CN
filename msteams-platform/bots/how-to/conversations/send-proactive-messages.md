---
title: 发送主动邮件
author: clearab
description: 如何使用 Microsoft 团队 bot 发送主动消息。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2dfb8e18243079ca38d505f4b80deb7abf2de32f
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874847"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="ec0fd-103">发送主动邮件</span><span class="sxs-lookup"><span data-stu-id="ec0fd-103">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="ec0fd-104">主动消息是由自动程序发送的无直接响应来自用户的请求的任何消息。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-104">A proactive message is any message sent by a bot that is not in direct response to a request from a user.</span></span> <span data-ttu-id="ec0fd-105">这可能包括如下邮件：</span><span class="sxs-lookup"><span data-stu-id="ec0fd-105">This can include messages like:</span></span>

* <span data-ttu-id="ec0fd-106">欢迎邮件</span><span class="sxs-lookup"><span data-stu-id="ec0fd-106">Welcome messages</span></span>
* <span data-ttu-id="ec0fd-107">通知</span><span class="sxs-lookup"><span data-stu-id="ec0fd-107">Notifications</span></span>
* <span data-ttu-id="ec0fd-108">计划的邮件</span><span class="sxs-lookup"><span data-stu-id="ec0fd-108">Scheduled messages</span></span>

<span data-ttu-id="ec0fd-109">为了让你的 bot 发送一封主动消息，它必须具有对要向其发送邮件的用户、组聊天或团队的访问权限。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-109">In order for your bot to send a proactive message, it must have access to the user, group chat, or team that you wish to send the message to.</span></span> <span data-ttu-id="ec0fd-110">对于组聊天或团队，这意味着必须首先将包含你的 bot 的应用安装到该位置。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-110">For a group chat or team, this means the app that contains your bot must first be installed to that location.</span></span> <span data-ttu-id="ec0fd-111">如有必要，可以在团队中使用 Graph （如有必要） [主动安装应用](#proactively-install-your-app-using-graph) ，或使用 [应用策略](/microsoftteams/teams-custom-app-policies-and-settings) 将应用推送到租户中的团队和用户。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-111">You can [proactively install your app using Graph](#proactively-install-your-app-using-graph) in a team if necessary, or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="ec0fd-112">对于用户，需要为该用户安装您的应用程序，或者您的用户需要是安装应用程序的团队的一部分。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-112">For users, your app either needs to be installed for that user, or your user needs to be part of a team where your app is installed.</span></span>

<span data-ttu-id="ec0fd-113">发送主动消息与发送常规邮件不同，因为您没有可用于答复的活动状态 `turnContext` 。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-113">Sending a proactive message is different than sending a regular message in that you won't have an active `turnContext` to use for a reply.</span></span> <span data-ttu-id="ec0fd-114">您可能还需要在发送邮件之前，先创建一个新的会话 (，例如新的一对一聊天或在频道) 中的新对话线程。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-114">You may also need to create the conversation (for example a new one-to-one chat, or a new conversation thread in a channel) before sending the message.</span></span> <span data-ttu-id="ec0fd-115">您不能通过主动消息在团队中创建新组聊天或新频道。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-115">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="ec0fd-116">在较高级别上，您需要完成的步骤才能发送一封主动消息：</span><span class="sxs-lookup"><span data-stu-id="ec0fd-116">At a high level the steps you'll need to complete to send a proactive message are:</span></span>

1. <span data-ttu-id="ec0fd-117">[获取用户 ID 或团队/通道 ID](#get-the-user-id-or-teamchannel-id) (如果需要) 。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-117">[Get the user ID or team/channel ID](#get-the-user-id-or-teamchannel-id) (if needed).</span></span>
1. <span data-ttu-id="ec0fd-118">如有必要[，创建会话或对话线索](#create-the-conversation) () 。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-118">[Create the conversation or conversation thread](#create-the-conversation) (if needed).</span></span>
1. <span data-ttu-id="ec0fd-119">[获取会话 ID](#get-the-conversation-id)。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-119">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="ec0fd-120">[发送邮件](#send-the-message)。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-120">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="ec0fd-121">下面的 [示例](#examples) 部分中的代码段用于创建一对一对话，请参阅 " [参考](#references) " 部分，以获取用于一次性对话和组/频道的完整工作示例的链接。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-121">The code snippets in the [examples](#examples) section below are for creating a one-to-one conversation, see the [references](#references) section for links to complete working samples for both one-to-once conversations and group/channels.</span></span>

## <a name="get-the-user-id-or-teamchannel-id"></a><span data-ttu-id="ec0fd-122">获取用户 ID 或团队/通道 ID</span><span class="sxs-lookup"><span data-stu-id="ec0fd-122">Get the user ID or team/channel ID</span></span>

<span data-ttu-id="ec0fd-123">如果需要在频道中创建新对话或对话线程，则首先需要使用正确的 ID 来创建对话。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-123">If you need to create a new conversation or conversation thread in a channel you'll first need the right ID to create the conversation.</span></span> <span data-ttu-id="ec0fd-124">您可以通过多种方式接收/检索此 ID：</span><span class="sxs-lookup"><span data-stu-id="ec0fd-124">You can receive/retrieve this ID in multiple ways:</span></span>

1. <span data-ttu-id="ec0fd-125">当您的应用程序安装在任何特定上下文中时，您将收到一个[ `onMembersAdded` 活动](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-125">When your app is installed in any particular context, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="ec0fd-126">将新用户添加到安装了应用程序的上下文中时，您将收到[ `onMembersAdded` 活动](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-126">When a new user is added to a context where your app is installed, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="ec0fd-127">您可以在已安装应用程序的团队中检索 [频道列表](~/bots/how-to/get-teams-context.md) 。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-127">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team your app is installed.</span></span>
1. <span data-ttu-id="ec0fd-128">您可以检索您的应用程序已安装的团队 [成员的列表](~/bots/how-to/get-teams-context.md) 。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-128">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team your app is installed.</span></span>
1. <span data-ttu-id="ec0fd-129">你的 bot 接收的每个活动将包含所需的信息。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-129">Every Activity your bot receives will contain the necessary information.</span></span>

<span data-ttu-id="ec0fd-130">无论您如何获取这些信息，您都需要存储 `tenantId` 和或的，以便 `userId` `channelId` 创建新对话。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-130">Regardless of how you gain the information, you'll need to store the `tenantId` and either the `userId` or `channelId` in order to create a new conversation.</span></span> <span data-ttu-id="ec0fd-131">您还可以使用在 `teamId` 团队的常规/默认通道中创建新的对话线程。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-131">You can also use the `teamId` to create a new conversation thread in the general/default channel of a team.</span></span>

<span data-ttu-id="ec0fd-132">`userId`对于你的 Bot Id 和特定用户而言是唯一的，无法在 bot 之间重新使用它们。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-132">The `userId` is unique to your bot Id and a particular user, you cannot re-use them between bots.</span></span> <span data-ttu-id="ec0fd-133">`channelId`这是全局性的，但是你的 bot_必须_安装在团队中，然后才能向通道发送主动消息。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-133">The `channelId` is global, however your bot _must_ be installed in the team before you can send a proactive message to a channel.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="ec0fd-134">创建对话</span><span class="sxs-lookup"><span data-stu-id="ec0fd-134">Create the conversation</span></span>

<span data-ttu-id="ec0fd-135">拥有用户/频道信息后，如果会话尚不存在，则需要创建会话 (或者不知道 `conversationId`) 。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-135">Once you have the user/channel information, you'll need to create the conversation if it doesn't already exist (or you don't know the `conversationId`).</span></span> <span data-ttu-id="ec0fd-136">只应创建对话一次;请确保存储 `conversationId` `conversationReference` 要在将来使用的值或对象。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-136">You should only create the conversation once; make sure you store the `conversationId` value or `conversationReference` object to use in the future.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="ec0fd-137">获取会话 ID</span><span class="sxs-lookup"><span data-stu-id="ec0fd-137">Get the conversation ID</span></span>

<span data-ttu-id="ec0fd-138">一旦创建了对话，您就可以使用 `conversationReference` 对象或 `conversationId` 和 `tenantId` 来发送邮件。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-138">Once the conversation has been created, you will use either the `conversationReference` object or the `conversationId` and the `tenantId` to send the message.</span></span> <span data-ttu-id="ec0fd-139">您可以通过创建对话来获取此 Id，也可以在从该上下文发送给您的任何活动中存储此 Id。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-139">You can get this Id by either creating the conversation, or storing it from any Activity sent to you from that context.</span></span> <span data-ttu-id="ec0fd-140">确保存储此 Id。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-140">Make certain that you store this Id.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="ec0fd-141">发送邮件</span><span class="sxs-lookup"><span data-stu-id="ec0fd-141">Send the message</span></span>

<span data-ttu-id="ec0fd-142">现在你已拥有正确的地址信息，你可以发送邮件了。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-142">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="ec0fd-143">如果您使用的是 SDK，您将使用 `continueConversation` 方法，以及 `conversationId` 并执行 `tenantId` 直接 API 调用。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-143">If you're using the SDK, you'll do so using the `continueConversation` method,and the `conversationId` and `tenantId` to make a direct API call.</span></span>  <span data-ttu-id="ec0fd-144">您需要设置 `conversationParameters` 正确的以成功发送邮件-请参阅下面的 [示例](#examples) 或使用 " [参考](#references) " 部分中列出的示例之一。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-144">You'll need to set the `conversationParameters` correctly to successfully send your message - see the [examples](#examples) below or use one of the samples listed in the [references](#references) section.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="ec0fd-145">主动消息传递的最佳做法</span><span class="sxs-lookup"><span data-stu-id="ec0fd-145">Best practices for proactive messaging</span></span>

<span data-ttu-id="ec0fd-146">向用户发送主动消息是与用户进行通信的一种非常有效的方式。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-146">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="ec0fd-147">但是，从其角度来看，此消息可以完全自发，在欢迎消息的情况下，它将在第一次与您的应用程序进行交互时显示。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-147">However, from their perspective this message can appear completely unprompted and, in the case of welcome messages, it will be the first time they've interacted with your app.</span></span> <span data-ttu-id="ec0fd-148">因此，谨慎使用此功能非常重要 (不要对用户) 垃圾邮件，并提供足够的信息，让用户了解推广的原因。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-148">As such, it is very important to use this functionality sparingly (don't spam your users) and to provide enough information to let users understand why they are being messaged.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="ec0fd-149">欢迎邮件</span><span class="sxs-lookup"><span data-stu-id="ec0fd-149">Welcome messages</span></span>

<span data-ttu-id="ec0fd-150">使用前瞻性消息向用户发送欢迎邮件时，必须记住，对于大多数接收邮件的人，将没有上下文了解他们接收邮件的原因。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-150">When using proactive messaging to send a welcome message to a user you must keep in mind that, for most people receiving the message, there will be no context for why they are receiving it.</span></span> <span data-ttu-id="ec0fd-151">这也是第一次将与您的应用程序进行交互。你有机会创建一个理想的首印象。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-151">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="ec0fd-152">最佳欢迎消息将包括：</span><span class="sxs-lookup"><span data-stu-id="ec0fd-152">The best welcome messages will include:</span></span>

* <span data-ttu-id="ec0fd-153">**用户接收邮件的原因。**</span><span class="sxs-lookup"><span data-stu-id="ec0fd-153">**Why a user is receiving the message.**</span></span> <span data-ttu-id="ec0fd-154">应非常清楚用户接收邮件的原因。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-154">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="ec0fd-155">如果你的 bot 已安装在频道中，并且你向所有用户发送了欢迎消息，请让他们知道它安装在什么频道并有权安装它。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-155">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="ec0fd-156">**你提供的内容。**</span><span class="sxs-lookup"><span data-stu-id="ec0fd-156">**What do you offer.**</span></span> <span data-ttu-id="ec0fd-157">他们可以对你的应用程序做些什么？</span><span class="sxs-lookup"><span data-stu-id="ec0fd-157">What can they do with your app?</span></span> <span data-ttu-id="ec0fd-158">您可以为它们引入什么值？</span><span class="sxs-lookup"><span data-stu-id="ec0fd-158">What value can you bring to them?</span></span>
* <span data-ttu-id="ec0fd-159">**接下来应做些什么。**</span><span class="sxs-lookup"><span data-stu-id="ec0fd-159">**What should they do next.**</span></span> <span data-ttu-id="ec0fd-160">邀请他们试用某个命令，或以某种方式与您的应用程序进行交互。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-160">Invite them to try out a command, or interact with your app in some way.</span></span>

<span data-ttu-id="ec0fd-161">请记住，欢迎邮件较差可能会导致用户阻止你的 bot。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-161">Remember, poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="ec0fd-162">应花费大量时间来起草欢迎消息，并在用户没有所需的效果的情况下对其进行迭代。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-162">You should spend plenty of time crafting your welcome messages, and iterate on them if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="ec0fd-163">通知邮件</span><span class="sxs-lookup"><span data-stu-id="ec0fd-163">Notification messages</span></span>

<span data-ttu-id="ec0fd-164">使用主动消息发送通知时，您需要确保您的用户有一个明确的路径，以根据您的通知执行常见操作，并清楚地了解通知发生的原因。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-164">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="ec0fd-165">正常的通知消息通常包括：</span><span class="sxs-lookup"><span data-stu-id="ec0fd-165">Good notification messages will generally include:</span></span>

* <span data-ttu-id="ec0fd-166">**发生了什么事。**</span><span class="sxs-lookup"><span data-stu-id="ec0fd-166">**What happened.**</span></span> <span data-ttu-id="ec0fd-167">可以清楚地指示导致通知发生了什么情况。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-167">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="ec0fd-168">**结果是什么。**</span><span class="sxs-lookup"><span data-stu-id="ec0fd-168">**What was the result.**</span></span> <span data-ttu-id="ec0fd-169">应清楚是什么项目/内容已更新，从而导致通知。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-169">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="ec0fd-170">**触发它的执行者。**</span><span class="sxs-lookup"><span data-stu-id="ec0fd-170">**Who/what triggered it.**</span></span> <span data-ttu-id="ec0fd-171">导致通知被发送的操作或采取的操作。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-171">Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="ec0fd-172">**用户可以采取何种响应。**</span><span class="sxs-lookup"><span data-stu-id="ec0fd-172">**What can users do in response.**</span></span> <span data-ttu-id="ec0fd-173">使您的用户可以轻松地根据您的通知执行操作。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-173">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="ec0fd-174">**用户可以选择退出的方式。** 您需要为用户提供一个路径，以供用户退出其他通知。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-174">**How can users opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="ec0fd-175">使用 Graph 主动安装您的应用程序</span><span class="sxs-lookup"><span data-stu-id="ec0fd-175">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="ec0fd-176">使用 Microsoft Graph 主动安装应用目前在 beta 中。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-176">Proactively installing apps using the Microsoft Graph is currently in beta.</span></span>

<span data-ttu-id="ec0fd-177">有时，可能有必要主动向尚未安装或与您的应用程序进行交互的邮件用户进行处理。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-177">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="ec0fd-178">例如，您希望使用 [公司 communicator](~/samples/app-templates.md#company-communicator) 向整个组织发送邮件。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-178">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="ec0fd-179">在这种情况下，您可以使用 Graph API 主动为您的用户安装您的应用程序，然后从 `conversationUpdate` 应用程序安装时收到的事件中缓存必要的值。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-179">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="ec0fd-180">您只能安装组织应用程序目录或团队应用商店中的应用程序。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-180">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="ec0fd-181">请参阅在 Microsoft Graph 的团队文档中 [为用户安装应用程序](/graph/teams-proactive-messaging) 和 [主动机器人安装和消息](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-181">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation and [Proactive bot installation and messaging in Teams with Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="ec0fd-182">GitHub 平台上也有 [Microsoft .net framework 示例](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)  。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-182">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)  on the GitHub platform.</span></span>

## <a name="examples"></a><span data-ttu-id="ec0fd-183">示例</span><span class="sxs-lookup"><span data-stu-id="ec0fd-183">Examples</span></span>

# <a name="cnet"></a>[<span data-ttu-id="ec0fd-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ec0fd-184">C#/.NET</span></span>](#tab/dotnet)

```csharp
private async Task MessageAllMembersAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var teamsChannelId = turnContext.Activity.TeamsGetChannelId();
    var serviceUrl = turnContext.Activity.ServiceUrl;
    var credentials = new MicrosoftAppCredentials(_appId, _appPassword);
    ConversationReference conversationReference = null;

    //Get the set of member IDs to send the message to
    var members = await GetPagedMembers(turnContext, cancellationToken);

    foreach (var teamMember in members)
    {
        var proactiveMessage = MessageFactory.Text($"Hello {teamMember.GivenName} {teamMember.Surname}. I'm a Teams conversation bot.");

        var conversationParameters = new ConversationParameters
        {
            IsGroup = false,
            Bot = turnContext.Activity.Recipient,
            Members = new ChannelAccount[] { teamMember },
            TenantId = turnContext.Activity.Conversation.TenantId,
        };
        //create the new one-to-one conversations
        await ((BotFrameworkAdapter)turnContext.Adapter).CreateConversationAsync(
            teamsChannelId,
            serviceUrl,
            credentials,
            conversationParameters,
            async (t1, c1) =>
            {
                //Get the conversationReference
                conversationReference = t1.Activity.GetConversationReference();
                //Send the proactive message
                await ((BotFrameworkAdapter)turnContext.Adapter).ContinueConversationAsync(
                    _appId,
                    conversationReference,
                    async (t2, c2) =>
                    {
                        await t2.SendActivityAsync(proactiveMessage, c2);
                    },
                    cancellationToken);
            },
            cancellationToken);
    }

    await turnContext.SendActivityAsync(MessageFactory.Text("All messages have been sent."), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="ec0fd-185">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="ec0fd-185">TypeScript/Node.js</span></span>](#tab/typescript)

```javascript

async messageAllMembersAsync(context) {
    const members = await this.getPagedMembers(context);

    members.forEach(async (teamMember) => {
        const message = MessageFactory.text('Hello ${ teamMember.givenName } ${ teamMember.surname }. I\'m a Teams conversation bot.');

        var ref = TurnContext.getConversationReference(context.activity);
        ref.user = teamMember;

        await context.adapter.createConversation(ref,
            async (t1) => {
                const ref2 = TurnContext.getConversationReference(t1.activity);
                await t1.adapter.continueConversation(ref2, async (t2) => {
                    await t2.sendActivity(message);
                });
            });
    });

    await context.sendActivity(MessageFactory.text('All messages have been sent.'));
}
```

# <a name="python"></a>[<span data-ttu-id="ec0fd-186">Python</span><span class="sxs-lookup"><span data-stu-id="ec0fd-186">Python</span></span>](#tab/python)

```python
async def _message_all_members(self, turn_context: TurnContext):
    team_members = await self._get_paged_members(turn_context)

    for member in team_members:
        conversation_reference = TurnContext.get_conversation_reference(
            turn_context.activity
        )

        conversation_parameters = ConversationParameters(
            is_group=False,
            bot=turn_context.activity.recipient,
            members=[member],
            tenant_id=turn_context.activity.conversation.tenant_id,
        )

        async def get_ref(tc1):
            conversation_reference_inner = TurnContext.get_conversation_reference(
                tc1.activity
            )
            return await tc1.adapter.continue_conversation(
                conversation_reference_inner, send_message, self._app_id
            )

        async def send_message(tc2: TurnContext):
            return await tc2.send_activity(
                f"Hello {member.name}. I'm a Teams conversation bot."
            )

        await turn_context.adapter.create_conversation(
            conversation_reference, get_ref, conversation_parameters
        )

    await turn_context.send_activity(
        MessageFactory.text("All messages have been sent")
    )

```

# <a name="json"></a>[<span data-ttu-id="ec0fd-187">JSON</span><span class="sxs-lookup"><span data-stu-id="ec0fd-187">JSON</span></span>](#tab/json)

```json
POST /v3/conversations
{
  "bot": {
    "id": "28:10j12ou0d812-2o1098-c1mjojzldxcj-1098028n ",
    "name": "The Bot"
  },
  "members": [
    {
      "id": "29:012d20j1cjo20211"
    }
  ],
  "channelData": {
    "tenant": {
      "id": "197231joe-1209j01821-012kdjoj"
    }
  }
}
```

<span data-ttu-id="ec0fd-188">您必须提供用户 ID 和租户 ID。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-188">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="ec0fd-189">如果调用成功，API 将返回以下响应对象。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-189">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="references"></a><span data-ttu-id="ec0fd-190">参考</span><span class="sxs-lookup"><span data-stu-id="ec0fd-190">References</span></span>

<span data-ttu-id="ec0fd-191">下面列出了官方的主动消息示例。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-191">The official proactive messaging samples are listed below.</span></span>

|  <span data-ttu-id="ec0fd-192">不正确。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-192">No.</span></span>  | <span data-ttu-id="ec0fd-193">示例名称</span><span class="sxs-lookup"><span data-stu-id="ec0fd-193">Sample Name</span></span>           | <span data-ttu-id="ec0fd-194">说明</span><span class="sxs-lookup"><span data-stu-id="ec0fd-194">Description</span></span>                                                                      | <span data-ttu-id="ec0fd-195">.NET</span><span class="sxs-lookup"><span data-stu-id="ec0fd-195">.NET</span></span>    | <span data-ttu-id="ec0fd-196">JavaScript</span><span class="sxs-lookup"><span data-stu-id="ec0fd-196">JavaScript</span></span>   | <span data-ttu-id="ec0fd-197">Python</span><span class="sxs-lookup"><span data-stu-id="ec0fd-197">Python</span></span>  |
|:--:|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="ec0fd-198">57</span><span class="sxs-lookup"><span data-stu-id="ec0fd-198">57</span></span>|<span data-ttu-id="ec0fd-199">团队对话基础知识</span><span class="sxs-lookup"><span data-stu-id="ec0fd-199">Teams Conversation Basics</span></span>  | <span data-ttu-id="ec0fd-200">演示团队中的对话的基础知识，包括发送一对一的主动消息。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-200">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>|[<span data-ttu-id="ec0fd-201">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="ec0fd-201">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="ec0fd-202">JavaScript</span><span class="sxs-lookup"><span data-stu-id="ec0fd-202">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="ec0fd-203">Python</span><span class="sxs-lookup"><span data-stu-id="ec0fd-203">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|<span data-ttu-id="ec0fd-204">58</span><span class="sxs-lookup"><span data-stu-id="ec0fd-204">58</span></span>|<span data-ttu-id="ec0fd-205">在频道中启动新线程</span><span class="sxs-lookup"><span data-stu-id="ec0fd-205">Start new thread in a channel</span></span>     | <span data-ttu-id="ec0fd-206">演示如何在通道中创建新线程。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-206">Demonstrates creating a new thread in a channel.</span></span> |[<span data-ttu-id="ec0fd-207">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="ec0fd-207">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="ec0fd-208">JavaScript</span><span class="sxs-lookup"><span data-stu-id="ec0fd-208">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="ec0fd-209">Python</span><span class="sxs-lookup"><span data-stu-id="ec0fd-209">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

<span data-ttu-id="ec0fd-210">下面的示例演示了在不使用对象) 的情况下发送主动消息所需的最少量信息 (`conversationReference` 。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-210">The sample below demonstrates the minimal amount of information needed to send a proactive message (without using a `conversationReference` object).</span></span> <span data-ttu-id="ec0fd-211">如果您直接使用 REST API 调用，或者尚未存储完全对象，则此示例可能很有用 `conversationReference` 。</span><span class="sxs-lookup"><span data-stu-id="ec0fd-211">This sample can be useful if you're using REST API calls directly, or haven't been storing full `conversationReference` objects.</span></span>

* [<span data-ttu-id="ec0fd-212">团队主动消息传递</span><span class="sxs-lookup"><span data-stu-id="ec0fd-212">Teams Proactive Messaging</span></span>](https://github.com/clearab/teamsProactiveMessaging)

## <a name="view-additional-code"></a><span data-ttu-id="ec0fd-213">查看其他代码</span><span class="sxs-lookup"><span data-stu-id="ec0fd-213">View additional code</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ec0fd-214">**团队主动消息代码示例**</span><span class="sxs-lookup"><span data-stu-id="ec0fd-214">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>