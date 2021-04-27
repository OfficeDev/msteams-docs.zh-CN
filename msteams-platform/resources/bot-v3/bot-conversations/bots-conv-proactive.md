---
title: 主动邮件
description: 描述机器人可以在 Microsoft Teams 中启动对话
ms.topic: conceptual
localization_priority: Normal
keywords: 团队方案主动消息对话机器人
ms.openlocfilehash: a13c565c8abe8c78fe6402d76796381b6a837393
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019788"
---
# <a name="proactive-messaging-for-bots"></a><span data-ttu-id="6a08c-104">自动程序主动消息传递</span><span class="sxs-lookup"><span data-stu-id="6a08c-104">Proactive messaging for bots</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="6a08c-105">主动消息是由机器人发送以开始对话的消息。</span><span class="sxs-lookup"><span data-stu-id="6a08c-105">A proactive message is a message that is sent by a bot to start a conversation.</span></span> <span data-ttu-id="6a08c-106">希望机器人开始对话的原因可能有很多，其中包括:</span><span class="sxs-lookup"><span data-stu-id="6a08c-106">You may want your bot to start a conversation for a number of reasons, including:</span></span>

* <span data-ttu-id="6a08c-107">个人机器人对话的欢迎消息</span><span class="sxs-lookup"><span data-stu-id="6a08c-107">Welcome messages for personal bot conversations</span></span>
* <span data-ttu-id="6a08c-108">投票回复</span><span class="sxs-lookup"><span data-stu-id="6a08c-108">Poll responses</span></span>
* <span data-ttu-id="6a08c-109">外部事件通知</span><span class="sxs-lookup"><span data-stu-id="6a08c-109">External event notifications</span></span>

<span data-ttu-id="6a08c-110">发送消息以启动新对话线程与在响应现有对话时发送消息不同：当机器人启动新对话时，没有将邮件张贴到的预先存在的会话。</span><span class="sxs-lookup"><span data-stu-id="6a08c-110">Sending a message to start a new conversation thread is different than sending a message in response to an existing conversation: when your bot starts a new a conversation, there is no pre-existing conversation to post the message to.</span></span> <span data-ttu-id="6a08c-111">为了发送主动邮件，你需要：</span><span class="sxs-lookup"><span data-stu-id="6a08c-111">In order to send a proactive message you need to:</span></span>

1. [<span data-ttu-id="6a08c-112">决定要说出什么</span><span class="sxs-lookup"><span data-stu-id="6a08c-112">Decide what you're going to say</span></span>](#best-practices-for-proactive-messaging)
1. [<span data-ttu-id="6a08c-113">获取用户的唯一 ID 和租户 ID</span><span class="sxs-lookup"><span data-stu-id="6a08c-113">Obtain the user's unique Id and tenant Id</span></span>](#obtain-necessary-user-information)
1. [<span data-ttu-id="6a08c-114">发送邮件</span><span class="sxs-lookup"><span data-stu-id="6a08c-114">Send the message</span></span>](#examples)

<span data-ttu-id="6a08c-115">创建主动邮件时 **，必须** 调用 ，并传递服务 URL，然后再创建 ，以 `MicrosoftAppCredentials.TrustServiceUrl` `ConnectorClient` 用于发送邮件。</span><span class="sxs-lookup"><span data-stu-id="6a08c-115">When creating proactive messages you **must** call `MicrosoftAppCredentials.TrustServiceUrl`, and pass in the service URL before creating the `ConnectorClient` you will use to send the message.</span></span> <span data-ttu-id="6a08c-116">如果不这样做，你的应用将收到 `401: Unauthorized` 响应。</span><span class="sxs-lookup"><span data-stu-id="6a08c-116">If you do not, your app will receive a `401: Unauthorized` response.</span></span> <span data-ttu-id="6a08c-117">请参阅 [下面的示例](#net-example-from-this-sample)。</span><span class="sxs-lookup"><span data-stu-id="6a08c-117">See [the samples below](#net-example-from-this-sample).</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="6a08c-118">主动邮件最佳做法</span><span class="sxs-lookup"><span data-stu-id="6a08c-118">Best practices for proactive messaging</span></span>

<span data-ttu-id="6a08c-119">向用户发送主动邮件是一种与用户通信的有效方式。</span><span class="sxs-lookup"><span data-stu-id="6a08c-119">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="6a08c-120">但是，从他们的角度来看，此消息可能看起来完全不一样，在欢迎消息的情况下，他们将第一次与你的应用交互。</span><span class="sxs-lookup"><span data-stu-id="6a08c-120">However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app.</span></span> <span data-ttu-id="6a08c-121">因此，请慎用此功能， (不要向用户发送) ，并为用户提供足够的信息，让他们了解邮件发送的原因。</span><span class="sxs-lookup"><span data-stu-id="6a08c-121">As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.</span></span>

<span data-ttu-id="6a08c-122">主动消息一般分为两类: 欢迎消息或通知。</span><span class="sxs-lookup"><span data-stu-id="6a08c-122">Proactive messages generally fall into one of two categories, welcome messages or notifications.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="6a08c-123">欢迎消息</span><span class="sxs-lookup"><span data-stu-id="6a08c-123">Welcome messages</span></span>

<span data-ttu-id="6a08c-124">使用主动消息向用户发送欢迎消息时，必须记住，对于大多数接收邮件的人，他们对于接收邮件的原因没有上下文。</span><span class="sxs-lookup"><span data-stu-id="6a08c-124">When using proactive messaging to send a welcome message to a user you must keep in mind that for most people receiving the message they will have no context for why they are receiving it.</span></span> <span data-ttu-id="6a08c-125">这也是他们第一次与你的应用交互;可以创造良好的第一印象。</span><span class="sxs-lookup"><span data-stu-id="6a08c-125">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="6a08c-126">最佳的欢迎消息包括：</span><span class="sxs-lookup"><span data-stu-id="6a08c-126">The best welcome messages will include:</span></span>

* <span data-ttu-id="6a08c-127">**他们为什么收到此消息。**</span><span class="sxs-lookup"><span data-stu-id="6a08c-127">**Why are they receiving this message.**</span></span> <span data-ttu-id="6a08c-128">用户应该非常清楚地了解他们接收邮件的原因。</span><span class="sxs-lookup"><span data-stu-id="6a08c-128">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="6a08c-129">如果你的自动程序安装在频道中，并且你向所有用户发送了欢迎消息，请让他们知道它安装在什么频道以及可能安装它的人。</span><span class="sxs-lookup"><span data-stu-id="6a08c-129">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="6a08c-130">**你提供什么功能。**</span><span class="sxs-lookup"><span data-stu-id="6a08c-130">**What do you offer.**</span></span> <span data-ttu-id="6a08c-131">他们可以对你的应用执行哪些操作？</span><span class="sxs-lookup"><span data-stu-id="6a08c-131">What can they do with your app?</span></span> <span data-ttu-id="6a08c-132">您可以为它们带来什么价值？</span><span class="sxs-lookup"><span data-stu-id="6a08c-132">What value can you bring to them?</span></span>
* <span data-ttu-id="6a08c-133">**接下来应执行哪些步骤。**</span><span class="sxs-lookup"><span data-stu-id="6a08c-133">**What should they do next.**</span></span> <span data-ttu-id="6a08c-134">邀请他们试用命令，或以某种方式与你的应用交互。</span><span class="sxs-lookup"><span data-stu-id="6a08c-134">Invite them to try out a command, or interact with your app in some way.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="6a08c-135">通知消息</span><span class="sxs-lookup"><span data-stu-id="6a08c-135">Notification messages</span></span>

<span data-ttu-id="6a08c-136">使用主动消息发送通知时，需要确保用户有一个清晰的路径，可以基于通知采取常见操作，并明确了解通知发生的原因。</span><span class="sxs-lookup"><span data-stu-id="6a08c-136">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification, and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="6a08c-137">良好的通知消息通常包括：</span><span class="sxs-lookup"><span data-stu-id="6a08c-137">Good notification messages will generally include:</span></span>

* <span data-ttu-id="6a08c-138">**发生了什么事。**</span><span class="sxs-lookup"><span data-stu-id="6a08c-138">**What happened.**</span></span> <span data-ttu-id="6a08c-139">关于导致通知发生的情况的清晰指示。</span><span class="sxs-lookup"><span data-stu-id="6a08c-139">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="6a08c-140">**它发生了什么。**</span><span class="sxs-lookup"><span data-stu-id="6a08c-140">**What it happened to.**</span></span> <span data-ttu-id="6a08c-141">应清楚哪些项/内容已更新，以引发通知。</span><span class="sxs-lookup"><span data-stu-id="6a08c-141">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="6a08c-142">**谁在做。**</span><span class="sxs-lookup"><span data-stu-id="6a08c-142">**Who did it.**</span></span> <span data-ttu-id="6a08c-143">谁采取导致发送通知的操作。</span><span class="sxs-lookup"><span data-stu-id="6a08c-143">Who took the action that caused the notification to be sent.</span></span>
* <span data-ttu-id="6a08c-144">**他们可以对它做什么。**</span><span class="sxs-lookup"><span data-stu-id="6a08c-144">**What they can do about it.**</span></span> <span data-ttu-id="6a08c-145">让用户能够轻松根据通知采取操作。</span><span class="sxs-lookup"><span data-stu-id="6a08c-145">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="6a08c-146">**如何选择退出。** 你需要为用户提供选择退出其他通知的路径。</span><span class="sxs-lookup"><span data-stu-id="6a08c-146">**How they can opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="obtain-necessary-user-information"></a><span data-ttu-id="6a08c-147">获取必要的用户信息</span><span class="sxs-lookup"><span data-stu-id="6a08c-147">Obtain necessary user information</span></span>

<span data-ttu-id="6a08c-148">机器人可以通过获取用户的唯一 ID 和租户 *ID* 来与单个 Microsoft Teams 用户创建新 *对话。*</span><span class="sxs-lookup"><span data-stu-id="6a08c-148">Bots can create new conversations with an individual Microsoft Teams user by obtaining the user's *unique ID* and *tenant ID.*</span></span> <span data-ttu-id="6a08c-149">可以使用以下方法之一获取这些值：</span><span class="sxs-lookup"><span data-stu-id="6a08c-149">You can obtain these values using one of the following methods:</span></span>

* <span data-ttu-id="6a08c-150">通过 [从应用安装通道](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) 获取团队名单。</span><span class="sxs-lookup"><span data-stu-id="6a08c-150">By [fetching the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) from a channel your app is installed in.</span></span>
* <span data-ttu-id="6a08c-151">在用户与频道中的机器人交互时 [缓存它们](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)。</span><span class="sxs-lookup"><span data-stu-id="6a08c-151">By caching them when a user [interacts with your bot in a channel](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).</span></span>
* <span data-ttu-id="6a08c-152">当用户在频道 [@mentioned聊天时，](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) 机器人是其中一部分。</span><span class="sxs-lookup"><span data-stu-id="6a08c-152">When a users is [@mentioned in a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) the bot is a part of.</span></span>
* <span data-ttu-id="6a08c-153">当你在[个人范围内安装 `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)应用或将新成员添加到频道或群聊时，通过缓存它们</span><span class="sxs-lookup"><span data-stu-id="6a08c-153">By caching them when you [receive the `conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) event when your app is installed in a personal scope, or new members are added to a channel or group chat that</span></span>

### <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="6a08c-154">使用 Graph 主动安装应用</span><span class="sxs-lookup"><span data-stu-id="6a08c-154">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="6a08c-155">使用 graph 主动安装应用目前处于 beta 阶段。</span><span class="sxs-lookup"><span data-stu-id="6a08c-155">Proactively installing apps using graph is currently in beta.</span></span>

<span data-ttu-id="6a08c-156">有时，可能需要主动向之前未安装或与你的应用交互的用户发送消息。</span><span class="sxs-lookup"><span data-stu-id="6a08c-156">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="6a08c-157">例如，您希望使用公司通信 [程序](~/samples/app-templates.md#company-communicator) 向整个组织发送邮件。</span><span class="sxs-lookup"><span data-stu-id="6a08c-157">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="6a08c-158">对于此方案，可以使用 Graph API 主动为用户安装应用，然后根据应用在安装时收到的事件缓存 `conversationUpdate` 必要的值。</span><span class="sxs-lookup"><span data-stu-id="6a08c-158">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="6a08c-159">只能安装组织应用目录中的应用或 Teams 应用商店。</span><span class="sxs-lookup"><span data-stu-id="6a08c-159">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="6a08c-160">有关 [完整详细信息，请参阅](/graph/teams-proactive-messaging) Graph 文档中的安装用户应用。</span><span class="sxs-lookup"><span data-stu-id="6a08c-160">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation for complete details.</span></span> <span data-ttu-id="6a08c-161">.NET 中 [还有一个示例](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)。</span><span class="sxs-lookup"><span data-stu-id="6a08c-161">There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span></span>

## <a name="examples"></a><span data-ttu-id="6a08c-162">示例</span><span class="sxs-lookup"><span data-stu-id="6a08c-162">Examples</span></span>

<span data-ttu-id="6a08c-163">在使用 REST API 创建新对话之前，请确保你进行身份验证并拥有一个记分令牌。</span><span class="sxs-lookup"><span data-stu-id="6a08c-163">Be sure that you authenticate and have a bearer token before creating a new conversation using the REST API.</span></span>

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

<span data-ttu-id="6a08c-164">必须提供用户 ID 和租户 ID。</span><span class="sxs-lookup"><span data-stu-id="6a08c-164">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="6a08c-165">如果调用成功，API 将返回以下 response 对象。</span><span class="sxs-lookup"><span data-stu-id="6a08c-165">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

<span data-ttu-id="6a08c-166">此 ID 是个人聊天的唯一对话 ID。</span><span class="sxs-lookup"><span data-stu-id="6a08c-166">This ID is the personal chat's unique conversation ID.</span></span> <span data-ttu-id="6a08c-167">请存储此值，并重复使用它以便以后与用户交互。</span><span class="sxs-lookup"><span data-stu-id="6a08c-167">Please store this value and reuse it for future interactions with the user.</span></span>

### <a name="using-net"></a><span data-ttu-id="6a08c-168">使用 .NET</span><span class="sxs-lookup"><span data-stu-id="6a08c-168">Using .NET</span></span>

<span data-ttu-id="6a08c-169">此示例使用 [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet 程序包。</span><span class="sxs-lookup"><span data-stu-id="6a08c-169">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create or get existing chat conversation with user
var response = client.Conversations.CreateOrGetDirectConversation(activity.Recipient, activity.From, activity.GetTenantId());

// Construct the message to post to conversation
Activity newActivity = new Activity()
{
    Text = "Hello",
    Type = ActivityTypes.Message,
    Conversation = new ConversationAccount
    {
        Id = response.Id
    },
};

// Post the message to chat conversation with user
await client.Conversations.SendToConversationAsync(newActivity, response.Id);
```

### <a name="using-nodejs"></a><span data-ttu-id="6a08c-170">使用 Node.js</span><span class="sxs-lookup"><span data-stu-id="6a08c-170">Using Node.js</span></span>

```javascript
var address =
{
    channelId: 'msteams',
    user: { id: userId },
    channelData: {
        tenant: {
            id: tenantId
        }
    },
    bot:
    {
        id: appId,
        name: appName
    },
    serviceUrl: session.message.address.serviceUrl,
    useAuth: true
}

var msg = new builder.Message().address(address);
msg.text('Hello, this is a notification');
bot.send(msg);
```

<span data-ttu-id="6a08c-171">*另请参阅* [Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="6a08c-171">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="creating-a-channel-conversation"></a><span data-ttu-id="6a08c-172">创建频道对话</span><span class="sxs-lookup"><span data-stu-id="6a08c-172">Creating a channel conversation</span></span>

<span data-ttu-id="6a08c-173">团队添加的机器人可以发布到频道中，以创建新的回复链。</span><span class="sxs-lookup"><span data-stu-id="6a08c-173">Your team-added bot can post into a channel to create a new reply chain.</span></span> <span data-ttu-id="6a08c-174">如果你使用的是 teams SDK Node.js，请使用 它为你提供具有正确活动 ID 和对话 ID 的完全 `startReplyChain()` 填充的地址。如果你使用的是C#，请参阅下面的示例。</span><span class="sxs-lookup"><span data-stu-id="6a08c-174">If you're using the Node.js Teams SDK, use `startReplyChain()` which gives you a fully-populated address with the correct activity id and conversation id. If you are using C#, see the example below.</span></span>

<span data-ttu-id="6a08c-175">或者，您可以使用 REST API 向资源发出 POST [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) 请求。</span><span class="sxs-lookup"><span data-stu-id="6a08c-175">Alternatively, you can use the REST API and issue a POST request to [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) resource.</span></span>

### <a name="net-example-from-this-sample"></a><span data-ttu-id="6a08c-176">此示例示例中 (.NET [) ](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)</span><span class="sxs-lookup"><span data-stu-id="6a08c-176">.NET example (from [this sample](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))</span></span>

```csharp
using Microsoft.Bot.Builder.Dialogs;
using Microsoft.Bot.Connector;
using Microsoft.Bot.Connector.Teams.Models;
using Microsoft.Teams.TemplateBotCSharp.Properties;
using System;
using System.Threading.Tasks;

namespace Microsoft.Teams.TemplateBotCSharp.Dialogs
{
    [Serializable]
    public class ProactiveMsgTo1to1Dialog : IDialog<object>
    {
        public async Task StartAsync(IDialogContext context)
        {
            if (context == null)
            {
                throw new ArgumentNullException(nameof(context));
            }

            var channelData = context.Activity.GetChannelData<TeamsChannelData>();
            var message = Activity.CreateMessageActivity();
            message.Text = "Hello World";

            var conversationParameters = new ConversationParameters
            {
                  IsGroup = true,
                  ChannelData = new TeamsChannelData
                  {
                      Channel = new ChannelInfo(channelData.Channel.Id),
                  },
                  Activity = (Activity) message
            };

            MicrosoftAppCredentials.TrustServiceUrl(serviceUrl, DateTime.MaxValue);
            var connectorClient = new ConnectorClient(new Uri(activity.ServiceUrl));
            var response = await connectorClient.Conversations.CreateConversationAsync(conversationParameters);

            context.Done<object>(null);
        }
    }
}
```
