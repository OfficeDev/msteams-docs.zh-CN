---
title: 发送主动邮件
description: 介绍如何使用 Microsoft Teams 自动程序发送主动邮件。
ms.topic: overview
ms.author: anclear
Keywords: 发送消息获取用户 ID 通道 ID 对话 ID
ms.openlocfilehash: 7da470eaba6ae9ecb82c9a7ba04d69b2f196a9d7
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654291"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="919c8-104">发送主动邮件</span><span class="sxs-lookup"><span data-stu-id="919c8-104">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="919c8-105">主动消息是自动程序发送的任何消息，不直接响应来自用户的请求。</span><span class="sxs-lookup"><span data-stu-id="919c8-105">A proactive message is any message sent by a bot that is not in direct response to a request from a user.</span></span> <span data-ttu-id="919c8-106">这可能包括如下消息：</span><span class="sxs-lookup"><span data-stu-id="919c8-106">This can include messages like:</span></span>

* <span data-ttu-id="919c8-107">欢迎消息</span><span class="sxs-lookup"><span data-stu-id="919c8-107">Welcome messages</span></span>
* <span data-ttu-id="919c8-108">通知</span><span class="sxs-lookup"><span data-stu-id="919c8-108">Notifications</span></span>
* <span data-ttu-id="919c8-109">计划邮件</span><span class="sxs-lookup"><span data-stu-id="919c8-109">Scheduled messages</span></span>

<span data-ttu-id="919c8-110">若要让机器人发送主动消息，它必须有权访问要发送消息的用户、群聊或团队。</span><span class="sxs-lookup"><span data-stu-id="919c8-110">For your bot to send a proactive message, it must have access to the user, group chat, or team that you want to send the message to.</span></span> <span data-ttu-id="919c8-111">对于群聊或团队，这意味着必须先将包含机器人的应用安装到该位置。</span><span class="sxs-lookup"><span data-stu-id="919c8-111">For a group chat or team, this means the app that contains your bot must be installed to that location first.</span></span> <span data-ttu-id="919c8-112">如果需要[，可以在团队](#proactively-install-your-app-using-graph)中主动使用 Graph 安装应用，或使用应用策略将应用[](/microsoftteams/teams-custom-app-policies-and-settings)推送到租户中的团队和用户。</span><span class="sxs-lookup"><span data-stu-id="919c8-112">You can [proactively install your app using Graph](#proactively-install-your-app-using-graph) in a team, if required or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="919c8-113">对于用户，必须为用户安装你的应用，或者用户必须是安装应用的团队的一部分。</span><span class="sxs-lookup"><span data-stu-id="919c8-113">For users, your app either must be installed for the user or your user must be part of a team where your app is installed.</span></span>

<span data-ttu-id="919c8-114">发送主动邮件与发送常规邮件不同。</span><span class="sxs-lookup"><span data-stu-id="919c8-114">Sending a proactive message is different than sending a regular message.</span></span> <span data-ttu-id="919c8-115">在这种情况下，没有用于 `turnContext` 回复的活动。</span><span class="sxs-lookup"><span data-stu-id="919c8-115">In that, there is no active `turnContext` to use for a reply.</span></span> <span data-ttu-id="919c8-116">在发送邮件之前，可能还需要创建对话。</span><span class="sxs-lookup"><span data-stu-id="919c8-116">You may also need to create the conversation before sending the message.</span></span> <span data-ttu-id="919c8-117">例如，频道中的新一对一聊天或新对话线程。</span><span class="sxs-lookup"><span data-stu-id="919c8-117">For example, a new one-to-one chat or a new conversation thread in a channel.</span></span> <span data-ttu-id="919c8-118">不能在具有主动消息的团队中创建新的群聊或新频道。</span><span class="sxs-lookup"><span data-stu-id="919c8-118">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="919c8-119">在高级别上，发送主动消息需要完成的步骤包括：</span><span class="sxs-lookup"><span data-stu-id="919c8-119">At a high level the steps you'll need to complete to send a proactive message are:</span></span>

1. <span data-ttu-id="919c8-120">[如果需要，请获取用户 ID 或团队/ (](#get-the-user-id-or-teamchannel-id) id) 。</span><span class="sxs-lookup"><span data-stu-id="919c8-120">[Get the user ID or team/channel ID](#get-the-user-id-or-teamchannel-id) (if needed).</span></span>
1. <span data-ttu-id="919c8-121">[如果需要，请创建对话 (](#create-the-conversation) 对话线程) 。</span><span class="sxs-lookup"><span data-stu-id="919c8-121">[Create the conversation or conversation thread](#create-the-conversation) (if needed).</span></span>
1. <span data-ttu-id="919c8-122">[获取对话 ID](#get-the-conversation-id)。</span><span class="sxs-lookup"><span data-stu-id="919c8-122">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="919c8-123">[发送邮件](#send-the-message)。</span><span class="sxs-lookup"><span data-stu-id="919c8-123">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="919c8-124">示例部分的代码段用于创建一[](#examples)对一对话。</span><span class="sxs-lookup"><span data-stu-id="919c8-124">The code snippets in the [examples](#examples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="919c8-125">有关一对一对话和组或频道的完整工作示例的链接，请参阅 [代码示例](#code-samples)。</span><span class="sxs-lookup"><span data-stu-id="919c8-125">For links to complete working samples for both one-to-one conversations and group or channels , see [code samples](#code-samples).</span></span>

## <a name="get-the-user-id-or-teamchannel-id"></a><span data-ttu-id="919c8-126">获取用户 ID 或团队/频道 ID</span><span class="sxs-lookup"><span data-stu-id="919c8-126">Get the user ID or team/channel ID</span></span>

<span data-ttu-id="919c8-127">若要在频道中创建新对话或对话线程，你需要正确的 ID。</span><span class="sxs-lookup"><span data-stu-id="919c8-127">To create a new conversation or conversation thread in a channel, you need the correct ID.</span></span> <span data-ttu-id="919c8-128">可以通过多种方式接收或检索此 ID：</span><span class="sxs-lookup"><span data-stu-id="919c8-128">You can receive or retrieve this ID in multiple ways:</span></span>

1. <span data-ttu-id="919c8-129">当你的应用安装在任何特定上下文中时，你将收到活动[ `onMembersAdded` 。](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="919c8-129">When your app is installed in any particular context, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="919c8-130">将新用户添加到安装应用的上下文时，你将收到"活动[ `onMembersAdded` "。](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="919c8-130">When a new user is added to a context where your app is installed, you'll receive a [`onMembersAdded` Activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
1. <span data-ttu-id="919c8-131">你可以检索 [已安装应用的](~/bots/how-to/get-teams-context.md) 团队中的频道列表。</span><span class="sxs-lookup"><span data-stu-id="919c8-131">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team your app is installed.</span></span>
1. <span data-ttu-id="919c8-132">你可以检索 [已安装应用的](~/bots/how-to/get-teams-context.md) 团队成员列表。</span><span class="sxs-lookup"><span data-stu-id="919c8-132">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team your app is installed.</span></span>
1. <span data-ttu-id="919c8-133">自动程序收到的每个活动都必须包含所需信息。</span><span class="sxs-lookup"><span data-stu-id="919c8-133">Every Activity your bot receives must contain the required information.</span></span>

<span data-ttu-id="919c8-134">无论如何获取信息，都需要存储 和 或 `tenantId` `userId` `channelId` 以创建新对话。</span><span class="sxs-lookup"><span data-stu-id="919c8-134">Regardless of how you gain the information, you'll need to store the `tenantId` and either the `userId` or `channelId` to create a new conversation.</span></span> <span data-ttu-id="919c8-135">您还可以使用 在团队的常规频道或默认频道中创建新的 `teamId` 对话线程。</span><span class="sxs-lookup"><span data-stu-id="919c8-135">You can also use the `teamId` to create a new conversation thread in the general or default channel of a team.</span></span>

<span data-ttu-id="919c8-136">对于自动程序 ID 和特定用户来说是唯一的，你无法在机器人之间 `userId` 重新使用它们。</span><span class="sxs-lookup"><span data-stu-id="919c8-136">The `userId` is unique to your bot Id and a particular user, you cannot re-use them between bots.</span></span> <span data-ttu-id="919c8-137">是全局的，但是，必须先在团队中安装自动程序 `channelId` ，然后才能向频道发送主动消息。</span><span class="sxs-lookup"><span data-stu-id="919c8-137">The `channelId` is global, however, your bot must be installed in the team before you can send a proactive message to a channel.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="919c8-138">创建对话</span><span class="sxs-lookup"><span data-stu-id="919c8-138">Create the conversation</span></span>

<span data-ttu-id="919c8-139">获得用户或频道信息后，如果对话不存在或不知道 ，则需要创建 `conversationId` 对话。</span><span class="sxs-lookup"><span data-stu-id="919c8-139">After you have the user or channel information, you need to create the conversation if it doesn't already exist or you don't know the `conversationId`.</span></span> <span data-ttu-id="919c8-140">只能创建一次对话，并确保存储要在将来 `conversationId` `conversationReference` 使用的值或对象。</span><span class="sxs-lookup"><span data-stu-id="919c8-140">You must only create the conversation once and make sure you store the `conversationId` value or `conversationReference` object to use in the future.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="919c8-141">获取对话 ID</span><span class="sxs-lookup"><span data-stu-id="919c8-141">Get the conversation ID</span></span>

<span data-ttu-id="919c8-142">创建对话后，使用 `conversationReference` 对象 或 `conversationId` `tenantId` 发送邮件。</span><span class="sxs-lookup"><span data-stu-id="919c8-142">After the conversation is created, use either the `conversationReference` object or `conversationId` and `tenantId` to send the message.</span></span> <span data-ttu-id="919c8-143">可以通过创建对话或从该上下文发送给你的任何活动存储此 ID 来获取此 ID。</span><span class="sxs-lookup"><span data-stu-id="919c8-143">You can get this ID by either creating the conversation or storing it from any Activity sent to you from that context.</span></span> <span data-ttu-id="919c8-144">确保存储此 ID。</span><span class="sxs-lookup"><span data-stu-id="919c8-144">Make certain that you store this ID.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="919c8-145">发送邮件</span><span class="sxs-lookup"><span data-stu-id="919c8-145">Send the message</span></span>

<span data-ttu-id="919c8-146">现在，您具有正确的地址信息，您可以发送邮件。</span><span class="sxs-lookup"><span data-stu-id="919c8-146">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="919c8-147">如果你使用的是 SDK，你将使用 方法以及 和 进行直接 `continueConversation` `conversationId` API `tenantId` 调用。</span><span class="sxs-lookup"><span data-stu-id="919c8-147">If you're using the SDK, you'll do so using the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call.</span></span> <span data-ttu-id="919c8-148">必须正确设置 `conversationParameters` ，以成功发送邮件。</span><span class="sxs-lookup"><span data-stu-id="919c8-148">You must set the `conversationParameters` correctly to successfully send your message.</span></span> <span data-ttu-id="919c8-149">请参阅 [示例](#examples) 部分或使用代码示例部分中列出的示例 [之一](#code-samples) 。</span><span class="sxs-lookup"><span data-stu-id="919c8-149">See the [examples](#examples) section or use one of the samples listed in the [code samples](#code-samples) section.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="919c8-150">主动邮件最佳做法</span><span class="sxs-lookup"><span data-stu-id="919c8-150">Best practices for proactive messaging</span></span>

<span data-ttu-id="919c8-151">向用户发送主动邮件是一种与用户通信的有效方式。</span><span class="sxs-lookup"><span data-stu-id="919c8-151">Sending proactive messages to users is a very effective way to communicate with your users.</span></span> <span data-ttu-id="919c8-152">但是，从他们的角度来看，此消息可能完全不提示，对于欢迎消息，这是他们第一次与你的应用交互。</span><span class="sxs-lookup"><span data-stu-id="919c8-152">However, from their perspective, this message can appear completely unprompted, and in the case of welcome messages, it is the first time they have interacted with your app.</span></span> <span data-ttu-id="919c8-153">因此，请慎用此功能，不要向用户发送垃圾邮件，并提供足够信息让用户了解邮件的原因，这一点非常重要。</span><span class="sxs-lookup"><span data-stu-id="919c8-153">Therefore, it is very important to use this functionality sparingly, don't spam your users, and to provide enough information to let users understand why they are being messaged.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="919c8-154">欢迎消息</span><span class="sxs-lookup"><span data-stu-id="919c8-154">Welcome messages</span></span>

<span data-ttu-id="919c8-155">使用主动消息向用户发送欢迎消息时，必须记住，对于大多数接收邮件的人，他们接收邮件的原因没有上下文。</span><span class="sxs-lookup"><span data-stu-id="919c8-155">When using proactive messaging to send a welcome message to a user you must keep in mind that, for most people receiving the message, there is no context for why they are receiving it.</span></span> <span data-ttu-id="919c8-156">这也是他们第一次与你的应用交互。</span><span class="sxs-lookup"><span data-stu-id="919c8-156">This is also the first time they have interacted with your app.</span></span> <span data-ttu-id="919c8-157">可以创造良好的第一印象。</span><span class="sxs-lookup"><span data-stu-id="919c8-157">It is your opportunity to create a good first impression.</span></span> <span data-ttu-id="919c8-158">最佳欢迎消息必须包括：</span><span class="sxs-lookup"><span data-stu-id="919c8-158">The best welcome messages must include:</span></span>

* <span data-ttu-id="919c8-159">**用户为什么收到邮件。**</span><span class="sxs-lookup"><span data-stu-id="919c8-159">**Why a user is receiving the message.**</span></span> <span data-ttu-id="919c8-160">用户必须非常清楚地了解他们接收邮件的原因。</span><span class="sxs-lookup"><span data-stu-id="919c8-160">It must be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="919c8-161">如果你的自动程序安装在频道中，并且你向所有用户发送了欢迎消息，请让他们知道它安装在什么频道以及可能安装它的人。</span><span class="sxs-lookup"><span data-stu-id="919c8-161">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="919c8-162">**你提供什么功能。**</span><span class="sxs-lookup"><span data-stu-id="919c8-162">**What do you offer.**</span></span> <span data-ttu-id="919c8-163">他们可以对你的应用执行哪些操作？</span><span class="sxs-lookup"><span data-stu-id="919c8-163">What can they do with your app?</span></span> <span data-ttu-id="919c8-164">您可以为它们带来什么价值？</span><span class="sxs-lookup"><span data-stu-id="919c8-164">What value can you bring to them?</span></span>
* <span data-ttu-id="919c8-165">**接下来应执行哪些步骤。**</span><span class="sxs-lookup"><span data-stu-id="919c8-165">**What should they do next.**</span></span> <span data-ttu-id="919c8-166">邀请他们试用命令，或以某种方式与你的应用交互。</span><span class="sxs-lookup"><span data-stu-id="919c8-166">Invite them to try out a command, or interact with your app in some way.</span></span>

<span data-ttu-id="919c8-167">请记住，较差的欢迎消息可能会导致用户阻止机器人。</span><span class="sxs-lookup"><span data-stu-id="919c8-167">Remember, poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="919c8-168">花费大量时间精心制作欢迎消息，如果消息没有达到预期效果，请对消息进行一次访问。</span><span class="sxs-lookup"><span data-stu-id="919c8-168">Spend plenty of time crafting your welcome messages, and iterate on them if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="919c8-169">通知消息</span><span class="sxs-lookup"><span data-stu-id="919c8-169">Notification messages</span></span>

<span data-ttu-id="919c8-170">使用主动消息发送通知时，必须确保用户有一个清晰的路径，可以基于通知采取常见操作，并清楚了解通知发生的原因。</span><span class="sxs-lookup"><span data-stu-id="919c8-170">When using proactive messaging to send notifications you must ensure your users have a clear path to take common actions based on your notification and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="919c8-171">良好的通知消息通常包括：</span><span class="sxs-lookup"><span data-stu-id="919c8-171">Good notification messages generally include:</span></span>

* <span data-ttu-id="919c8-172">**发生了什么事。**</span><span class="sxs-lookup"><span data-stu-id="919c8-172">**What happened.**</span></span> <span data-ttu-id="919c8-173">关于导致通知发生的情况的清晰指示。</span><span class="sxs-lookup"><span data-stu-id="919c8-173">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="919c8-174">**结果是什么。**</span><span class="sxs-lookup"><span data-stu-id="919c8-174">**What was the result.**</span></span> <span data-ttu-id="919c8-175">必须清楚哪些项或内容已更新，以引发通知。</span><span class="sxs-lookup"><span data-stu-id="919c8-175">It must be clear what item or thing was updated to cause the notification.</span></span>
* <span data-ttu-id="919c8-176">**触发它的人/人。**</span><span class="sxs-lookup"><span data-stu-id="919c8-176">**Who/what triggered it.**</span></span> <span data-ttu-id="919c8-177">导致发送通知的操作人或执行什么操作。</span><span class="sxs-lookup"><span data-stu-id="919c8-177">Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="919c8-178">**用户可以在响应中做什么。**</span><span class="sxs-lookup"><span data-stu-id="919c8-178">**What can users do in response.**</span></span> <span data-ttu-id="919c8-179">让用户能够轻松根据通知采取操作。</span><span class="sxs-lookup"><span data-stu-id="919c8-179">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="919c8-180">**用户如何选择退出。** 你必须为用户提供选择退出其他通知的路径。</span><span class="sxs-lookup"><span data-stu-id="919c8-180">**How can users opt out.** You must provide a path for users to opt out of additional notifications.</span></span>

### <a name="scheduled-messages"></a><span data-ttu-id="919c8-181">计划邮件</span><span class="sxs-lookup"><span data-stu-id="919c8-181">Scheduled messages</span></span>

<span data-ttu-id="919c8-182">使用主动消息向用户发送计划邮件时，请验证时区已更新到其时区。</span><span class="sxs-lookup"><span data-stu-id="919c8-182">When using proactive messaging to send scheduled messages to users, verify that your time zone is updated to their time zone.</span></span> <span data-ttu-id="919c8-183">这可确保在相关时间将邮件传递给用户。</span><span class="sxs-lookup"><span data-stu-id="919c8-183">This ensures that the messages are delivered to the users at the relevant time.</span></span> <span data-ttu-id="919c8-184">计划邮件通常包括：</span><span class="sxs-lookup"><span data-stu-id="919c8-184">Schedule messages generally include:</span></span>

* <span data-ttu-id="919c8-185">**用户为什么收到邮件**：让用户轻松了解收到邮件的原因。</span><span class="sxs-lookup"><span data-stu-id="919c8-185">**Why is the user receiving the message**: Make it easy for your users to understand the reason for which they are receiving the message.</span></span>
* <span data-ttu-id="919c8-186">**用户接下来可以做什么**：用户可以根据邮件内容采取所需操作。</span><span class="sxs-lookup"><span data-stu-id="919c8-186">**What can user do next**: Users can take the required action based on the message content.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="919c8-187">使用 Graph 主动安装应用</span><span class="sxs-lookup"><span data-stu-id="919c8-187">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="919c8-188">使用 Microsoft Graph 主动安装应用目前处于 beta 阶段。</span><span class="sxs-lookup"><span data-stu-id="919c8-188">Proactively installing apps using the Microsoft Graph is currently in beta.</span></span>

<span data-ttu-id="919c8-189">有时，可能需要主动向之前未安装或与你的应用交互的用户发送消息。</span><span class="sxs-lookup"><span data-stu-id="919c8-189">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="919c8-190">例如，您希望使用公司通信 [程序](~/samples/app-templates.md#company-communicator) 向整个组织发送邮件。</span><span class="sxs-lookup"><span data-stu-id="919c8-190">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="919c8-191">对于此方案，可以使用 Graph API 主动为用户安装应用，然后根据应用在安装时收到的事件缓存 `conversationUpdate` 必要的值。</span><span class="sxs-lookup"><span data-stu-id="919c8-191">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app receives upon installation.</span></span>

<span data-ttu-id="919c8-192">只能安装组织应用目录或 Teams 应用商店中的应用。</span><span class="sxs-lookup"><span data-stu-id="919c8-192">You can only install apps that are in your organizational app catalog or the Teams app store.</span></span>

<span data-ttu-id="919c8-193">请参阅 [Graph 文档中的为用户](/graph/api/userteamwork-post-installedapps) 安装应用，以及使用 Microsoft Graph 在 Teams 中主动安装 [机器人和消息传递](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="919c8-193">See [Install apps for users](/graph/api/userteamwork-post-installedapps) in the Graph documentation and [Proactive bot installation and messaging in Teams with Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="919c8-194">GitHub 平台上还有一个 [Microsoft .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) 框架示例。</span><span class="sxs-lookup"><span data-stu-id="919c8-194">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) on the GitHub platform.</span></span>

## <a name="examples"></a><span data-ttu-id="919c8-195">示例</span><span class="sxs-lookup"><span data-stu-id="919c8-195">Examples</span></span>

# <a name="cnet"></a>[<span data-ttu-id="919c8-196">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="919c8-196">C#/.NET</span></span>](#tab/dotnet)

```csharp
[Route("api/notify")]
[ApiController]
public class NotifyController : ControllerBase
{
    private readonly IBotFrameworkHttpAdapter _adapter;
    private readonly string _appId;
    private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

    public NotifyController(IBotFrameworkHttpAdapter adapter, IConfiguration configuration, ConcurrentDictionary<string, ConversationReference> conversationReferences)
    {
        _adapter = adapter;
        _conversationReferences = conversationReferences;
        _appId = configuration["MicrosoftAppId"] ?? string.Empty;
    }

    public async Task<IActionResult> Get()
    {
        foreach (var conversationReference in _conversationReferences.Values)
        {
            await ((BotAdapter)_adapter).ContinueConversationAsync(_appId, conversationReference, BotCallback, default(CancellationToken));
        }
        
        // Let the caller know proactive messages have been sent
        return new ContentResult()
        {
            Content = "<html><body><h1>Proactive messages have been sent.</h1></body></html>",
            ContentType = "text/html",
            StatusCode = (int)HttpStatusCode.OK,
        };
    }

    private async Task BotCallback(ITurnContext turnContext, CancellationToken cancellationToken)
    {
        // If you encounter permission-related errors when sending this message, see
        // https://aka.ms/BotTrustServiceUrl
        await turnContext.SendActivityAsync("proactive hello");
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="919c8-197">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="919c8-197">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="919c8-198">Python</span><span class="sxs-lookup"><span data-stu-id="919c8-198">Python</span></span>](#tab/python)

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

# <a name="json"></a>[<span data-ttu-id="919c8-199">JSON</span><span class="sxs-lookup"><span data-stu-id="919c8-199">JSON</span></span>](#tab/json)

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

<span data-ttu-id="919c8-200">必须提供用户 ID 和租户 ID。</span><span class="sxs-lookup"><span data-stu-id="919c8-200">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="919c8-201">如果调用成功，API 将返回以下 response 对象。</span><span class="sxs-lookup"><span data-stu-id="919c8-201">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-samples"></a><span data-ttu-id="919c8-202">代码示例</span><span class="sxs-lookup"><span data-stu-id="919c8-202">Code samples</span></span>

<span data-ttu-id="919c8-203">官方主动邮件示例如下所示：</span><span class="sxs-lookup"><span data-stu-id="919c8-203">The official proactive messaging samples are as follows:</span></span>

| <span data-ttu-id="919c8-204">示例名称</span><span class="sxs-lookup"><span data-stu-id="919c8-204">Sample Name</span></span>           | <span data-ttu-id="919c8-205">Description</span><span class="sxs-lookup"><span data-stu-id="919c8-205">Description</span></span>                                                                      | <span data-ttu-id="919c8-206">.NET</span><span class="sxs-lookup"><span data-stu-id="919c8-206">.NET</span></span>    | <span data-ttu-id="919c8-207">JavaScript</span><span class="sxs-lookup"><span data-stu-id="919c8-207">JavaScript</span></span>   | <span data-ttu-id="919c8-208">Python</span><span class="sxs-lookup"><span data-stu-id="919c8-208">Python</span></span>  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="919c8-209">Teams 对话基础知识</span><span class="sxs-lookup"><span data-stu-id="919c8-209">Teams Conversation Basics</span></span>  | <span data-ttu-id="919c8-210">演示 Teams 中对话的基础知识，包括发送一对一主动消息。</span><span class="sxs-lookup"><span data-stu-id="919c8-210">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>|[<span data-ttu-id="919c8-211">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="919c8-211">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="919c8-212">JavaScript</span><span class="sxs-lookup"><span data-stu-id="919c8-212">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="919c8-213">Python</span><span class="sxs-lookup"><span data-stu-id="919c8-213">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|<span data-ttu-id="919c8-214">在频道中启动新线程</span><span class="sxs-lookup"><span data-stu-id="919c8-214">Start new thread in a channel</span></span>     | <span data-ttu-id="919c8-215">演示在频道中创建新线程。</span><span class="sxs-lookup"><span data-stu-id="919c8-215">Demonstrates creating a new thread in a channel.</span></span> |[<span data-ttu-id="919c8-216">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="919c8-216">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="919c8-217">JavaScript</span><span class="sxs-lookup"><span data-stu-id="919c8-217">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[<span data-ttu-id="919c8-218">Python</span><span class="sxs-lookup"><span data-stu-id="919c8-218">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a><span data-ttu-id="919c8-219">查看其他代码示例</span><span class="sxs-lookup"><span data-stu-id="919c8-219">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="919c8-220">**Teams 主动邮件代码示例**</span><span class="sxs-lookup"><span data-stu-id="919c8-220">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
