---
title: 发送主动邮件
description: 介绍如何使用 Microsoft Teams 自动程序发送主动邮件。
ms.topic: conceptual
ms.author: anclear
localization_priority: Normal
Keywords: 发送消息获取用户 ID 通道 ID 对话 ID
ms.openlocfilehash: ae651ac94b1b092374f6fae284b67070036b561f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020917"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="98ceb-104">发送主动邮件</span><span class="sxs-lookup"><span data-stu-id="98ceb-104">Send proactive messages</span></span>

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="98ceb-105">主动消息是自动程序发送的任何不响应用户请求的消息。</span><span class="sxs-lookup"><span data-stu-id="98ceb-105">A proactive message is any message sent by a bot that is not in response to a request from a user.</span></span> <span data-ttu-id="98ceb-106">这可能包括邮件，例如：</span><span class="sxs-lookup"><span data-stu-id="98ceb-106">This can include messages, such as:</span></span>

* <span data-ttu-id="98ceb-107">欢迎消息</span><span class="sxs-lookup"><span data-stu-id="98ceb-107">Welcome messages</span></span>
* <span data-ttu-id="98ceb-108">通知</span><span class="sxs-lookup"><span data-stu-id="98ceb-108">Notifications</span></span>
* <span data-ttu-id="98ceb-109">计划邮件</span><span class="sxs-lookup"><span data-stu-id="98ceb-109">Scheduled messages</span></span>

<span data-ttu-id="98ceb-110">若要让机器人向用户、群聊或团队发送主动消息，它必须具有发送消息的访问权限。</span><span class="sxs-lookup"><span data-stu-id="98ceb-110">For your bot to send a proactive message to a user, group chat, or team, it must have access to send the message.</span></span> <span data-ttu-id="98ceb-111">对于群聊或团队，必须先将包含机器人的应用安装在该位置。</span><span class="sxs-lookup"><span data-stu-id="98ceb-111">For a group chat or team, the app that contains your bot must be first installed in that location.</span></span> <span data-ttu-id="98ceb-112">如果需要[，可在团队](#proactively-install-your-app-using-graph)中主动使用 Microsoft Graph 安装应用，或使用应用策略将应用[](/microsoftteams/teams-custom-app-policies-and-settings)推送到租户中的团队和用户。</span><span class="sxs-lookup"><span data-stu-id="98ceb-112">You can [proactively install your app using Microsoft Graph](#proactively-install-your-app-using-graph) in a team, if required, or use an [app policy](/microsoftteams/teams-custom-app-policies-and-settings) to push apps out to teams and users in your tenant.</span></span> <span data-ttu-id="98ceb-113">对于用户，必须为用户安装你的应用，或者用户必须是安装应用的团队的一部分。</span><span class="sxs-lookup"><span data-stu-id="98ceb-113">For users, your app either must be installed for the user or your user must be part of a team where your app is installed.</span></span>

<span data-ttu-id="98ceb-114">发送主动邮件与发送常规邮件不同。</span><span class="sxs-lookup"><span data-stu-id="98ceb-114">Sending a proactive message is different from sending a regular message.</span></span> <span data-ttu-id="98ceb-115">没有用于 `turnContext` 答复的活动。</span><span class="sxs-lookup"><span data-stu-id="98ceb-115">There is no active `turnContext` to use for a reply.</span></span> <span data-ttu-id="98ceb-116">在发送邮件之前，必须创建对话。</span><span class="sxs-lookup"><span data-stu-id="98ceb-116">You must create the conversation before sending the message.</span></span> <span data-ttu-id="98ceb-117">例如，频道中的新一对一聊天或新对话线程。</span><span class="sxs-lookup"><span data-stu-id="98ceb-117">For example, a new one-to-one chat or a new conversation thread in a channel.</span></span> <span data-ttu-id="98ceb-118">不能在具有主动消息的团队中创建新的群聊或新频道。</span><span class="sxs-lookup"><span data-stu-id="98ceb-118">You cannot create a new group chat or a new channel in a team with proactive messaging.</span></span>

<span data-ttu-id="98ceb-119">**发送主动邮件**</span><span class="sxs-lookup"><span data-stu-id="98ceb-119">**To send a proactive message**</span></span>

1. <span data-ttu-id="98ceb-120">[如果需要，获取用户 ID、团队 ID 或频道 ID。](#get-the-user-id-team-id-or-channel-id)</span><span class="sxs-lookup"><span data-stu-id="98ceb-120">[Get the user ID, team ID, or channel ID](#get-the-user-id-team-id-or-channel-id), if required.</span></span>
1. <span data-ttu-id="98ceb-121">[创建对话](#create-the-conversation)（如果需要）。</span><span class="sxs-lookup"><span data-stu-id="98ceb-121">[Create the conversation](#create-the-conversation), if required.</span></span>
1. <span data-ttu-id="98ceb-122">[获取对话 ID](#get-the-conversation-id)。</span><span class="sxs-lookup"><span data-stu-id="98ceb-122">[Get the conversation ID](#get-the-conversation-id).</span></span>
1. <span data-ttu-id="98ceb-123">[发送邮件](#send-the-message)。</span><span class="sxs-lookup"><span data-stu-id="98ceb-123">[Send the message](#send-the-message).</span></span>

<span data-ttu-id="98ceb-124">示例部分的代码段用于创建一[](#samples)对一对话。</span><span class="sxs-lookup"><span data-stu-id="98ceb-124">The code snippets in the [samples](#samples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="98ceb-125">有关一对一对话和组或频道的完整工作示例的链接，请参阅 [代码示例](#code-sample)。</span><span class="sxs-lookup"><span data-stu-id="98ceb-125">For links to complete working samples for both one-to-one conversations and group or channels , see [code sample](#code-sample).</span></span>

<span data-ttu-id="98ceb-126">要有效地使用主动邮件，请参阅 [主动邮件的最佳实践](#best-practices-for-proactive-messaging)。</span><span class="sxs-lookup"><span data-stu-id="98ceb-126">For using proactive messages effectively, see [best practices for proactive messaging](#best-practices-for-proactive-messaging).</span></span> <span data-ttu-id="98ceb-127">对于某些方案，你必须使用 Graph 主动 [安装应用](#proactively-install-your-app-using-graph)。</span><span class="sxs-lookup"><span data-stu-id="98ceb-127">For certain scenarios, you must [proactively install your app using Graph](#proactively-install-your-app-using-graph).</span></span> <span data-ttu-id="98ceb-128">示例部分的代码段用于创建一[](#samples)对一对话。</span><span class="sxs-lookup"><span data-stu-id="98ceb-128">The code snippets in the [samples](#samples) section are for creating a one-to-one conversation.</span></span> <span data-ttu-id="98ceb-129">有关一对一对话以及组或频道的完整工作示例，请参阅 [代码示例](#code-sample)。</span><span class="sxs-lookup"><span data-stu-id="98ceb-129">For complete working samples for both one-to-one conversations and groups or channels, see [code sample](#code-sample).</span></span>

## <a name="get-the-user-id-team-id-or-channel-id"></a><span data-ttu-id="98ceb-130">获取用户 ID、团队 ID 或频道 ID</span><span class="sxs-lookup"><span data-stu-id="98ceb-130">Get the user ID, team ID or channel ID</span></span>

<span data-ttu-id="98ceb-131">若要在频道中创建新对话或对话线程，必须具有正确的 ID。</span><span class="sxs-lookup"><span data-stu-id="98ceb-131">To create a new conversation or conversation thread in a channel, you must have the correct ID.</span></span> <span data-ttu-id="98ceb-132">可以使用以下任一项接收或检索此 ID：</span><span class="sxs-lookup"><span data-stu-id="98ceb-132">You can receive or retrieve this ID using any of the following:</span></span>

* <span data-ttu-id="98ceb-133">当你的应用安装在任何特定上下文中时，你会收到一个[ `onMembersAdded` 活动](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="98ceb-133">When your app is installed in any particular context, you receive an [`onMembersAdded` activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="98ceb-134">将新用户添加到安装你的应用的上下文中时，你会收到一个[ `onMembersAdded` 活动](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="98ceb-134">When a new user is added to a context where your app is installed, you receive an [`onMembersAdded` activity](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="98ceb-135">你可以检索 [安装了应用的](~/bots/how-to/get-teams-context.md) 团队中的频道列表。</span><span class="sxs-lookup"><span data-stu-id="98ceb-135">You can retrieve the [list of channels](~/bots/how-to/get-teams-context.md) in a team where your app is installed.</span></span>
* <span data-ttu-id="98ceb-136">你可以检索 [安装了应用的](~/bots/how-to/get-teams-context.md) 团队成员列表。</span><span class="sxs-lookup"><span data-stu-id="98ceb-136">You can retrieve the [list of members](~/bots/how-to/get-teams-context.md) of a team where your app is installed.</span></span>
* <span data-ttu-id="98ceb-137">机器人收到的每个活动都必须包含所需信息。</span><span class="sxs-lookup"><span data-stu-id="98ceb-137">Every activity your bot receives must contain the required information.</span></span>

<span data-ttu-id="98ceb-138">无论如何获取信息，都必须存储 和 或 `tenantId` `userId` `channelId` 以创建新对话。</span><span class="sxs-lookup"><span data-stu-id="98ceb-138">Regardless of how you get the information, you must store the `tenantId` and either the `userId` or `channelId` to create a new conversation.</span></span> <span data-ttu-id="98ceb-139">您还可以使用 在团队的常规频道或默认频道中创建新的 `teamId` 对话线程。</span><span class="sxs-lookup"><span data-stu-id="98ceb-139">You can also use the `teamId` to create a new conversation thread in the general or default channel of a team.</span></span>

<span data-ttu-id="98ceb-140">`userId`是自动程序 ID 和特定用户所特有的。</span><span class="sxs-lookup"><span data-stu-id="98ceb-140">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="98ceb-141">您不能在自动程序 `userId` 之间重复使用。</span><span class="sxs-lookup"><span data-stu-id="98ceb-141">You cannot reuse the `userId` between bots.</span></span> <span data-ttu-id="98ceb-142">`channelId`是全局的。</span><span class="sxs-lookup"><span data-stu-id="98ceb-142">The `channelId` is global.</span></span> <span data-ttu-id="98ceb-143">但是，必须先在团队中安装自动程序，然后才能向频道发送主动消息。</span><span class="sxs-lookup"><span data-stu-id="98ceb-143">However, your bot must be installed in the team before you can send a proactive message to a channel.</span></span>

<span data-ttu-id="98ceb-144">获得用户或频道信息后，必须创建对话。</span><span class="sxs-lookup"><span data-stu-id="98ceb-144">After you have the user or channel information, you must create the conversation.</span></span>

## <a name="create-the-conversation"></a><span data-ttu-id="98ceb-145">创建对话</span><span class="sxs-lookup"><span data-stu-id="98ceb-145">Create the conversation</span></span>

<span data-ttu-id="98ceb-146">如果对话不存在或您不知道 ，则必须创建 `conversationId` 对话。</span><span class="sxs-lookup"><span data-stu-id="98ceb-146">You must create the conversation if it does not exist or you do not know the `conversationId`.</span></span> <span data-ttu-id="98ceb-147">只能创建一次对话并存储 `conversationId` 值或 `conversationReference` 对象。</span><span class="sxs-lookup"><span data-stu-id="98ceb-147">You must only create the conversation once and store the `conversationId` value or `conversationReference` object.</span></span>

<span data-ttu-id="98ceb-148">创建对话后，必须获取对话 ID。</span><span class="sxs-lookup"><span data-stu-id="98ceb-148">After the conversation is created, you must get the conversation ID.</span></span>

## <a name="get-the-conversation-id"></a><span data-ttu-id="98ceb-149">获取对话 ID</span><span class="sxs-lookup"><span data-stu-id="98ceb-149">Get the conversation ID</span></span>

<span data-ttu-id="98ceb-150">使用 `conversationReference` 对象或 `conversationId` 和 `tenantId` 发送邮件。</span><span class="sxs-lookup"><span data-stu-id="98ceb-150">Use either the `conversationReference` object or `conversationId` and `tenantId` to send the message.</span></span> <span data-ttu-id="98ceb-151">可以通过创建对话或从该上下文发送给你的任何活动存储此 ID 来获取此 ID。</span><span class="sxs-lookup"><span data-stu-id="98ceb-151">You can get this ID by either creating the conversation or storing it from any activity sent to you from that context.</span></span> <span data-ttu-id="98ceb-152">存储此 ID 供参考。</span><span class="sxs-lookup"><span data-stu-id="98ceb-152">Store this ID for reference.</span></span>

<span data-ttu-id="98ceb-153">获取相应的地址信息后，可以发送邮件。</span><span class="sxs-lookup"><span data-stu-id="98ceb-153">After you get the appropriate address information, you can send your message.</span></span>

## <a name="send-the-message"></a><span data-ttu-id="98ceb-154">发送邮件</span><span class="sxs-lookup"><span data-stu-id="98ceb-154">Send the message</span></span>

<span data-ttu-id="98ceb-155">现在，您具有正确的地址信息，您可以发送邮件。</span><span class="sxs-lookup"><span data-stu-id="98ceb-155">Now that you have the right address information, you can send your message.</span></span> <span data-ttu-id="98ceb-156">如果你使用的是 SDK，你将使用 方法以及 和 进行直接 `continueConversation` `conversationId` API `tenantId` 调用。</span><span class="sxs-lookup"><span data-stu-id="98ceb-156">If you're using the SDK, you'll do so using the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call.</span></span> <span data-ttu-id="98ceb-157">必须正确设置 `conversationParameters` ，以成功发送邮件。</span><span class="sxs-lookup"><span data-stu-id="98ceb-157">You must set the `conversationParameters` correctly to successfully send your message.</span></span> <span data-ttu-id="98ceb-158">请参阅 [示例](#samples) 部分或使用代码示例部分中列出的示例 [之](#code-sample) 一。</span><span class="sxs-lookup"><span data-stu-id="98ceb-158">See the [samples](#samples) section or use one of the samples listed in the [code sample](#code-sample) section.</span></span>

<span data-ttu-id="98ceb-159">如果使用的是 SDK，则必须使用 和 方法，并直接 `continueConversation` `conversationId` 调用 `tenantId` API 来发送消息。</span><span class="sxs-lookup"><span data-stu-id="98ceb-159">If you are using the SDK, you must use the `continueConversation` method, and the `conversationId` and `tenantId` to make a direct API call to send the message.</span></span> <span data-ttu-id="98ceb-160">必须正确设置 `conversationParameters` ，以成功发送邮件。</span><span class="sxs-lookup"><span data-stu-id="98ceb-160">You must set the `conversationParameters` correctly to successfully send your message.</span></span>

<span data-ttu-id="98ceb-161">现在，你已发送主动邮件，在发送主动邮件时必须遵循这些最佳做法，以便用户和机器人之间更好地交换信息。</span><span class="sxs-lookup"><span data-stu-id="98ceb-161">Now that you have sent the proactive message, you must follow these best practices while sending proactive messages for better information exchange between users and the bot.</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="98ceb-162">主动邮件最佳做法</span><span class="sxs-lookup"><span data-stu-id="98ceb-162">Best practices for proactive messaging</span></span>

<span data-ttu-id="98ceb-163">向用户发送主动邮件是一种与用户通信的有效方式。</span><span class="sxs-lookup"><span data-stu-id="98ceb-163">Sending proactive messages to users is a very effective way to communicate with your users.</span></span> <span data-ttu-id="98ceb-164">但是，从他们的角度来看，此消息可能完全不提示，对于欢迎消息，这是他们第一次与你的应用交互。</span><span class="sxs-lookup"><span data-stu-id="98ceb-164">However, from their perspective, this message can appear completely unprompted, and in the case of welcome messages, it is the first time they have interacted with your app.</span></span> <span data-ttu-id="98ceb-165">因此，请谨慎使用主动邮件，而不是向用户发送垃圾邮件，并提供足够信息让用户了解接收邮件的原因，这一点非常重要。</span><span class="sxs-lookup"><span data-stu-id="98ceb-165">Therefore, it is very important to use proactive messaging sparingly, not spam your users, and provide enough information to let users understand why they are receiving the messages.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="98ceb-166">欢迎消息</span><span class="sxs-lookup"><span data-stu-id="98ceb-166">Welcome messages</span></span>

<span data-ttu-id="98ceb-167">当主动消息用于向用户发送欢迎消息时，用户收到邮件的原因没有上下文。</span><span class="sxs-lookup"><span data-stu-id="98ceb-167">When proactive messaging is used to send a welcome message to a user, there is no context for why the users receive the message.</span></span> <span data-ttu-id="98ceb-168">这也是用户第一次与你的应用交互。</span><span class="sxs-lookup"><span data-stu-id="98ceb-168">This is also the first time users interact with your app.</span></span> <span data-ttu-id="98ceb-169">这是创造良好的第一印象的机会。</span><span class="sxs-lookup"><span data-stu-id="98ceb-169">It is an opportunity to create a good first impression.</span></span> <span data-ttu-id="98ceb-170">最佳欢迎消息必须包括：</span><span class="sxs-lookup"><span data-stu-id="98ceb-170">The best welcome messages must include:</span></span>

* <span data-ttu-id="98ceb-171">用户为什么收到邮件：用户必须非常清楚地了解他们接收邮件的原因。</span><span class="sxs-lookup"><span data-stu-id="98ceb-171">Why a user is receiving the message: It must be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="98ceb-172">如果你的机器人安装在频道中，并且你向所有用户发送了欢迎消息，请让他们知道它安装在什么频道以及谁安装了它。</span><span class="sxs-lookup"><span data-stu-id="98ceb-172">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and who installed it.</span></span>
* <span data-ttu-id="98ceb-173">你提供什么：用户必须能够确定他们可以对你的应用执行哪些操作，以及你可以为用户带来什么价值。</span><span class="sxs-lookup"><span data-stu-id="98ceb-173">What do you offer: Users must be able to identify what they can do with your app and what value can you bring to them.</span></span>
* <span data-ttu-id="98ceb-174">接下来应做什么：邀请用户试用命令，或与你的应用交互。</span><span class="sxs-lookup"><span data-stu-id="98ceb-174">What should they do next: Invite users to try out a command, or interact with your app.</span></span>

<span data-ttu-id="98ceb-175">较差的欢迎消息可能会导致用户阻止机器人。</span><span class="sxs-lookup"><span data-stu-id="98ceb-175">Poor welcome messages can lead to users blocking your bot.</span></span> <span data-ttu-id="98ceb-176">写入要点并清除欢迎消息。</span><span class="sxs-lookup"><span data-stu-id="98ceb-176">Write to the point and clear welcome messages.</span></span> <span data-ttu-id="98ceb-177">如果欢迎消息没有达到预期效果，则对欢迎消息进行 Iterate。</span><span class="sxs-lookup"><span data-stu-id="98ceb-177">Iterate on the welcome messages if they are not having the desired effect.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="98ceb-178">通知消息</span><span class="sxs-lookup"><span data-stu-id="98ceb-178">Notification messages</span></span>

<span data-ttu-id="98ceb-179">若要使用主动消息发送通知，请确保你的用户有一个清晰的路径，可以基于你的通知采取常见操作。</span><span class="sxs-lookup"><span data-stu-id="98ceb-179">To send notifications using proactive messaging, ensure your users have a clear path to take common actions based on your notification.</span></span> <span data-ttu-id="98ceb-180">确保用户清楚地了解他们为何收到通知。</span><span class="sxs-lookup"><span data-stu-id="98ceb-180">Ensure users have a clear understanding of why they have received a notification.</span></span> <span data-ttu-id="98ceb-181">良好的通知消息通常包括以下内容：</span><span class="sxs-lookup"><span data-stu-id="98ceb-181">Good notification messages generally include the following:</span></span>

* <span data-ttu-id="98ceb-182">发生的情况：关于导致通知发生的情况的清晰指示。</span><span class="sxs-lookup"><span data-stu-id="98ceb-182">What happened: A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="98ceb-183">结果是什么：必须清楚更新了哪些项，以引发通知。</span><span class="sxs-lookup"><span data-stu-id="98ceb-183">What was the result: It must be clear what item was updated to cause the notification.</span></span>
* <span data-ttu-id="98ceb-184">触发它的人或原因：导致发送通知的操作者或行为。</span><span class="sxs-lookup"><span data-stu-id="98ceb-184">Who or what triggered it: Who or what took action that caused the notification to be sent.</span></span>
* <span data-ttu-id="98ceb-185">用户可在响应中执行哪些操作：使用户能够轻松根据通知采取操作。</span><span class="sxs-lookup"><span data-stu-id="98ceb-185">What can users do in response: Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="98ceb-186">用户如何选择退出：你必须为用户提供选择退出其他通知的路径。</span><span class="sxs-lookup"><span data-stu-id="98ceb-186">How can users opt-out: You must provide a path for users to opt-out of additional notifications.</span></span>

<span data-ttu-id="98ceb-187">若要向一大组用户发送消息（例如，发送到组织）请主动使用 Graph 安装应用。</span><span class="sxs-lookup"><span data-stu-id="98ceb-187">To send messages to a large group of users, for example to your organization, proactively install your app using Graph.</span></span>

### <a name="scheduled-messages"></a><span data-ttu-id="98ceb-188">计划邮件</span><span class="sxs-lookup"><span data-stu-id="98ceb-188">Scheduled messages</span></span>

<span data-ttu-id="98ceb-189">使用主动消息向用户发送计划邮件时，请验证时区已更新到其时区。</span><span class="sxs-lookup"><span data-stu-id="98ceb-189">When using proactive messaging to send scheduled messages to users, verify that your time zone is updated to their time zone.</span></span> <span data-ttu-id="98ceb-190">这可确保在相关时间将邮件传递给用户。</span><span class="sxs-lookup"><span data-stu-id="98ceb-190">This ensures that the messages are delivered to the users at the relevant time.</span></span> <span data-ttu-id="98ceb-191">计划邮件通常包括：</span><span class="sxs-lookup"><span data-stu-id="98ceb-191">Schedule messages generally include:</span></span>

* <span data-ttu-id="98ceb-192">用户为什么收到邮件：让用户轻松了解收到邮件的原因。</span><span class="sxs-lookup"><span data-stu-id="98ceb-192">Why is the user receiving the message: Make it easy for your users to understand the reason for which they are receiving the message.</span></span>
* <span data-ttu-id="98ceb-193">用户接下来可以做什么：用户可以根据邮件内容采取所需操作。</span><span class="sxs-lookup"><span data-stu-id="98ceb-193">What can user do next: Users can take the required action based on the message content.</span></span>

## <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="98ceb-194">使用 Graph 主动安装应用</span><span class="sxs-lookup"><span data-stu-id="98ceb-194">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="98ceb-195">使用 Graph 主动安装应用目前处于 beta 阶段。</span><span class="sxs-lookup"><span data-stu-id="98ceb-195">Proactively installing apps using Graph is currently in beta.</span></span>

<span data-ttu-id="98ceb-196">主动向之前未安装或与你的应用交互的用户发送消息。</span><span class="sxs-lookup"><span data-stu-id="98ceb-196">Proactively message users that have previously not installed or interacted with your app.</span></span> <span data-ttu-id="98ceb-197">例如，您希望使用公司通信 [程序](~/samples/app-templates.md#company-communicator) 向整个组织发送邮件。</span><span class="sxs-lookup"><span data-stu-id="98ceb-197">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="98ceb-198">在这种情况下，可以使用 Graph API 主动为用户安装应用。</span><span class="sxs-lookup"><span data-stu-id="98ceb-198">In this case, you can use the Graph API to proactively install your app for your users.</span></span> <span data-ttu-id="98ceb-199">缓存应用在安装 `conversationUpdate` 时收到的事件所需的值。</span><span class="sxs-lookup"><span data-stu-id="98ceb-199">Cache the necessary values from the `conversationUpdate` event your app receives upon installation.</span></span>

<span data-ttu-id="98ceb-200">只能安装组织应用目录或 Teams 应用商店中的应用。</span><span class="sxs-lookup"><span data-stu-id="98ceb-200">You can only install apps that are in your organizational app catalog or the Teams App Store.</span></span>

<span data-ttu-id="98ceb-201">请参阅 [Graph 文档中的为用户](/graph/api/userteamwork-post-installedapps) 安装应用，以及使用 Graph 在 Teams 中主动安装机器人 [和消息传递](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="98ceb-201">See [install apps for users](/graph/api/userteamwork-post-installedapps) in the Graph documentation and [proactive bot installation and messaging in Teams with Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md).</span></span> <span data-ttu-id="98ceb-202">GitHub 平台上还有一个 [Microsoft .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) 框架示例。</span><span class="sxs-lookup"><span data-stu-id="98ceb-202">There is also a [Microsoft .NET framework sample](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) on the GitHub platform.</span></span>

## <a name="samples"></a><span data-ttu-id="98ceb-203">示例</span><span class="sxs-lookup"><span data-stu-id="98ceb-203">Samples</span></span>

<span data-ttu-id="98ceb-204">以下代码显示了一个简单的代码示例，该示例使用 Graph 主动安装你的应用：</span><span class="sxs-lookup"><span data-stu-id="98ceb-204">The following code shows a simple code sample that proactively installs your app using Graph:</span></span>

# <a name="c"></a>[<span data-ttu-id="98ceb-205">C#</span><span class="sxs-lookup"><span data-stu-id="98ceb-205">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="98ceb-206">TypeScript</span><span class="sxs-lookup"><span data-stu-id="98ceb-206">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="98ceb-207">Python</span><span class="sxs-lookup"><span data-stu-id="98ceb-207">Python</span></span>](#tab/python)

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

# <a name="json"></a>[<span data-ttu-id="98ceb-208">JSON</span><span class="sxs-lookup"><span data-stu-id="98ceb-208">JSON</span></span>](#tab/json)

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

<span data-ttu-id="98ceb-209">必须提供用户 ID 和租户 ID。</span><span class="sxs-lookup"><span data-stu-id="98ceb-209">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="98ceb-210">如果调用成功，API 将返回以下 response 对象：</span><span class="sxs-lookup"><span data-stu-id="98ceb-210">If the call succeeds, the API returns the following response object:</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-sample"></a><span data-ttu-id="98ceb-211">代码示例</span><span class="sxs-lookup"><span data-stu-id="98ceb-211">Code sample</span></span>

<span data-ttu-id="98ceb-212">下表提供了一个简单的代码示例，该示例将基本对话流合并到 Teams 应用程序中，以及如何在 Teams 中的频道中创建新的对话线程：</span><span class="sxs-lookup"><span data-stu-id="98ceb-212">The following table provides a simple code sample that incorporate basic conversation flow into a Teams application and how to create a new conversation thread in a channel in Teams:</span></span>

| <span data-ttu-id="98ceb-213">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="98ceb-213">**Sample Name**</span></span> | <span data-ttu-id="98ceb-214">**描述**</span><span class="sxs-lookup"><span data-stu-id="98ceb-214">**Description**</span></span> | <span data-ttu-id="98ceb-215">**.NET**</span><span class="sxs-lookup"><span data-stu-id="98ceb-215">**.NET**</span></span> | <span data-ttu-id="98ceb-216">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="98ceb-216">**Node.js**</span></span> | <span data-ttu-id="98ceb-217">**Python**</span><span class="sxs-lookup"><span data-stu-id="98ceb-217">**Python**</span></span> |
|---------------|--------------|--------|-------------|--------|
| <span data-ttu-id="98ceb-218">Teams 对话基础知识</span><span class="sxs-lookup"><span data-stu-id="98ceb-218">Teams Conversation Basics</span></span>  | <span data-ttu-id="98ceb-219">演示 Teams 中对话的基础知识，包括发送一对一主动消息。</span><span class="sxs-lookup"><span data-stu-id="98ceb-219">Demonstrates basics of conversations in Teams, including sending one-to-one proactive messages.</span></span>| [<span data-ttu-id="98ceb-220">View</span><span class="sxs-lookup"><span data-stu-id="98ceb-220">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [<span data-ttu-id="98ceb-221">View</span><span class="sxs-lookup"><span data-stu-id="98ceb-221">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="98ceb-222">View</span><span class="sxs-lookup"><span data-stu-id="98ceb-222">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| <span data-ttu-id="98ceb-223">在频道中启动新线程</span><span class="sxs-lookup"><span data-stu-id="98ceb-223">Start new thread in a channel</span></span> | <span data-ttu-id="98ceb-224">演示在频道中创建新线程。</span><span class="sxs-lookup"><span data-stu-id="98ceb-224">Demonstrates creating a new thread in a channel.</span></span> | [<span data-ttu-id="98ceb-225">View</span><span class="sxs-lookup"><span data-stu-id="98ceb-225">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [<span data-ttu-id="98ceb-226">View</span><span class="sxs-lookup"><span data-stu-id="98ceb-226">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [<span data-ttu-id="98ceb-227">View</span><span class="sxs-lookup"><span data-stu-id="98ceb-227">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

### <a name="additional-code-sample"></a><span data-ttu-id="98ceb-228">其他代码示例</span><span class="sxs-lookup"><span data-stu-id="98ceb-228">Additional code sample</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="98ceb-229">Teams 主动邮件代码示例</span><span class="sxs-lookup"><span data-stu-id="98ceb-229">Teams proactive messaging code samples</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="next-step"></a><span data-ttu-id="98ceb-230">后续步骤</span><span class="sxs-lookup"><span data-stu-id="98ceb-230">Next step</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="98ceb-231">[**Teams 主动邮件代码示例**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp) 
> [设置自动程序消息的格式](~/bots/how-to/format-your-bot-messages.md)</span><span class="sxs-lookup"><span data-stu-id="98ceb-231">[**Teams proactive messaging code samples**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)
[Format your bot messages](~/bots/how-to/format-your-bot-messages.md)</span></span>
