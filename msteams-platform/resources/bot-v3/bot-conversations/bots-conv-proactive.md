---
title: 主动邮件
description: 描述机器人可以在 Microsoft Teams 中启动对话
keywords: 团队方案主动消息传递对话机器人
ms.openlocfilehash: 8c93696f79b5d99c32162a7374c7d9adccacb984
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231622"
---
# <a name="proactive-messaging-for-bots"></a><span data-ttu-id="69293-104">自动程序主动消息传递</span><span class="sxs-lookup"><span data-stu-id="69293-104">Proactive messaging for bots</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="69293-105">主动消息是由机器人发送以启动对话的消息。</span><span class="sxs-lookup"><span data-stu-id="69293-105">A proactive message is a message that is sent by a bot to start a conversation.</span></span> <span data-ttu-id="69293-106">你可能希望机器人启动对话的原因有很多，包括：</span><span class="sxs-lookup"><span data-stu-id="69293-106">You may want your bot to start a conversation for a number of reasons, including:</span></span>

* <span data-ttu-id="69293-107">个人机器人对话的欢迎消息</span><span class="sxs-lookup"><span data-stu-id="69293-107">Welcome messages for personal bot conversations</span></span>
* <span data-ttu-id="69293-108">轮询响应</span><span class="sxs-lookup"><span data-stu-id="69293-108">Poll responses</span></span>
* <span data-ttu-id="69293-109">外部事件通知</span><span class="sxs-lookup"><span data-stu-id="69293-109">External event notifications</span></span>

<span data-ttu-id="69293-110">发送邮件以启动新对话线程与发送消息以响应现有对话不同：当机器人启动新对话时，没有将邮件张贴到的预先存在的对话。</span><span class="sxs-lookup"><span data-stu-id="69293-110">Sending a message to start a new conversation thread is different than sending a message in response to an existing conversation: when your bot starts a new a conversation, there is no pre-existing conversation to post the message to.</span></span> <span data-ttu-id="69293-111">若要发送主动邮件，需要：</span><span class="sxs-lookup"><span data-stu-id="69293-111">In order to send a proactive message you need to:</span></span>

1. [<span data-ttu-id="69293-112">决定你要说出什么</span><span class="sxs-lookup"><span data-stu-id="69293-112">Decide what you're going to say</span></span>](#best-practices-for-proactive-messaging)
1. [<span data-ttu-id="69293-113">获取用户的唯一 ID 和租户 ID</span><span class="sxs-lookup"><span data-stu-id="69293-113">Obtain the user's unique Id and tenant Id</span></span>](#obtain-necessary-user-information)
1. [<span data-ttu-id="69293-114">发送邮件</span><span class="sxs-lookup"><span data-stu-id="69293-114">Send the message</span></span>](#examples)

<span data-ttu-id="69293-115">创建主动邮件时 **，必须** 调用 `MicrosoftAppCredentials.TrustServiceUrl` 服务 URL，然后创建用于 `ConnectorClient` 发送邮件的服务 URL。</span><span class="sxs-lookup"><span data-stu-id="69293-115">When creating proactive messages you **must** call `MicrosoftAppCredentials.TrustServiceUrl`, and pass in the service URL before creating the `ConnectorClient` you will use to send the message.</span></span> <span data-ttu-id="69293-116">如果不这样做，你的应用将收到 `401: Unauthorized` 响应。</span><span class="sxs-lookup"><span data-stu-id="69293-116">If you do not, your app will receive a `401: Unauthorized` response.</span></span> <span data-ttu-id="69293-117">请参阅 [下面的示例](#net-example-from-this-sample)。</span><span class="sxs-lookup"><span data-stu-id="69293-117">See [the samples below](#net-example-from-this-sample).</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="69293-118">主动消息传递的最佳实践</span><span class="sxs-lookup"><span data-stu-id="69293-118">Best practices for proactive messaging</span></span>

<span data-ttu-id="69293-119">向用户发送主动消息是一种与用户通信的非常有效的方式。</span><span class="sxs-lookup"><span data-stu-id="69293-119">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="69293-120">但是，从他们的角度来看，此消息可能看起来完全不一样，在欢迎消息的情况下，他们将是首次与你的应用交互。</span><span class="sxs-lookup"><span data-stu-id="69293-120">However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app.</span></span> <span data-ttu-id="69293-121">因此，请慎用此功能 (不要向用户发送) ，并为用户提供足够的信息，让他们了解为何收到邮件。</span><span class="sxs-lookup"><span data-stu-id="69293-121">As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.</span></span>

<span data-ttu-id="69293-122">主动邮件通常分为两类之一：欢迎消息或通知。</span><span class="sxs-lookup"><span data-stu-id="69293-122">Proactive messages generally fall into one of two categories, welcome messages or notifications.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="69293-123">欢迎消息</span><span class="sxs-lookup"><span data-stu-id="69293-123">Welcome messages</span></span>

<span data-ttu-id="69293-124">使用主动消息向用户发送欢迎消息时，必须记住，对于大多数接收邮件的用户，他们对于接收邮件的原因没有上下文。</span><span class="sxs-lookup"><span data-stu-id="69293-124">When using proactive messaging to send a welcome message to a user you must keep in mind that for most people receiving the message they will have no context for why they are receiving it.</span></span> <span data-ttu-id="69293-125">这也是他们第一次与你的应用交互;这是创造良好第一印象的机会。</span><span class="sxs-lookup"><span data-stu-id="69293-125">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="69293-126">最佳的欢迎消息包括：</span><span class="sxs-lookup"><span data-stu-id="69293-126">The best welcome messages will include:</span></span>

* <span data-ttu-id="69293-127">**他们为什么收到此消息。**</span><span class="sxs-lookup"><span data-stu-id="69293-127">**Why are they receiving this message.**</span></span> <span data-ttu-id="69293-128">用户应非常清楚地了解他们接收邮件的原因。</span><span class="sxs-lookup"><span data-stu-id="69293-128">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="69293-129">如果你的机器人安装在频道中，并且你向所有用户发送了欢迎消息，请让他们知道它安装在哪些频道中以及可能安装它的人。</span><span class="sxs-lookup"><span data-stu-id="69293-129">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="69293-130">**你提供什么。**</span><span class="sxs-lookup"><span data-stu-id="69293-130">**What do you offer.**</span></span> <span data-ttu-id="69293-131">他们可以对你的应用执行哪些操作？</span><span class="sxs-lookup"><span data-stu-id="69293-131">What can they do with your app?</span></span> <span data-ttu-id="69293-132">你可以为它们带来什么价值？</span><span class="sxs-lookup"><span data-stu-id="69293-132">What value can you bring to them?</span></span>
* <span data-ttu-id="69293-133">**接下来，他们应该怎么办。**</span><span class="sxs-lookup"><span data-stu-id="69293-133">**What should they do next.**</span></span> <span data-ttu-id="69293-134">邀请他们试用命令，或以某种方式与你的应用交互。</span><span class="sxs-lookup"><span data-stu-id="69293-134">Invite them to try out a command, or interact with your app in some way.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="69293-135">通知邮件</span><span class="sxs-lookup"><span data-stu-id="69293-135">Notification messages</span></span>

<span data-ttu-id="69293-136">使用主动消息发送通知时，需要确保用户有一个明确路径，可以基于通知采取常见操作，并明确了解通知发生的原因。</span><span class="sxs-lookup"><span data-stu-id="69293-136">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification, and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="69293-137">良好的通知消息通常包括：</span><span class="sxs-lookup"><span data-stu-id="69293-137">Good notification messages will generally include:</span></span>

* <span data-ttu-id="69293-138">**发生了什么事。**</span><span class="sxs-lookup"><span data-stu-id="69293-138">**What happened.**</span></span> <span data-ttu-id="69293-139">导致通知发生的情况的清晰指示。</span><span class="sxs-lookup"><span data-stu-id="69293-139">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="69293-140">**它发生了什么。**</span><span class="sxs-lookup"><span data-stu-id="69293-140">**What it happened to.**</span></span> <span data-ttu-id="69293-141">应清楚哪些项目/内容已更新以引起通知。</span><span class="sxs-lookup"><span data-stu-id="69293-141">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="69293-142">**谁这样做了。**</span><span class="sxs-lookup"><span data-stu-id="69293-142">**Who did it.**</span></span> <span data-ttu-id="69293-143">谁采取导致发送通知的操作。</span><span class="sxs-lookup"><span data-stu-id="69293-143">Who took the action that caused the notification to be sent.</span></span>
* <span data-ttu-id="69293-144">**他们可以对它执行哪些工作。**</span><span class="sxs-lookup"><span data-stu-id="69293-144">**What they can do about it.**</span></span> <span data-ttu-id="69293-145">使用户能够轻松根据通知采取操作。</span><span class="sxs-lookup"><span data-stu-id="69293-145">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="69293-146">**如何选择退出。** 你需要为用户提供选择退出其他通知的路径。</span><span class="sxs-lookup"><span data-stu-id="69293-146">**How they can opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="obtain-necessary-user-information"></a><span data-ttu-id="69293-147">获取必要的用户信息</span><span class="sxs-lookup"><span data-stu-id="69293-147">Obtain necessary user information</span></span>

<span data-ttu-id="69293-148">机器人可以通过获取用户的唯一 ID 和租户 *ID* 来与单个 Microsoft Teams 用户创建新 *对话。*</span><span class="sxs-lookup"><span data-stu-id="69293-148">Bots can create new conversations with an individual Microsoft Teams user by obtaining the user's *unique ID* and *tenant ID.*</span></span> <span data-ttu-id="69293-149">可以使用下列方法之一获取这些值：</span><span class="sxs-lookup"><span data-stu-id="69293-149">You can obtain these values using one of the following methods:</span></span>

* <span data-ttu-id="69293-150">通过 [从安装你的应用](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) 的频道获取团队名单。</span><span class="sxs-lookup"><span data-stu-id="69293-150">By [fetching the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) from a channel your app is installed in.</span></span>
* <span data-ttu-id="69293-151">在用户与频道中的机器人交互时 [缓存它们](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)。</span><span class="sxs-lookup"><span data-stu-id="69293-151">By caching them when a user [interacts with your bot in a channel](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).</span></span>
* <span data-ttu-id="69293-152">当用户在频道 [@mentioned聊天时，](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) 自动程序是其中一部分。</span><span class="sxs-lookup"><span data-stu-id="69293-152">When a users is [@mentioned in a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) the bot is a part of.</span></span>
* <span data-ttu-id="69293-153">当你在[个人范围内 `conversationUpdate` 安装](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)应用时收到事件时缓存它们，或者将新成员添加到频道或群聊中，</span><span class="sxs-lookup"><span data-stu-id="69293-153">By caching them when you [receive the `conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) event when your app is installed in a personal scope, or new members are added to a channel or group chat that</span></span>

### <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="69293-154">使用 Graph 主动安装应用</span><span class="sxs-lookup"><span data-stu-id="69293-154">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="69293-155">使用 graph 主动安装应用目前处于 beta 阶段。</span><span class="sxs-lookup"><span data-stu-id="69293-155">Proactively installing apps using graph is currently in beta.</span></span>

<span data-ttu-id="69293-156">有时，可能需要主动向之前未安装或与你的应用交互的用户发送消息。</span><span class="sxs-lookup"><span data-stu-id="69293-156">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="69293-157">例如，您希望使用公司 [通信程序](~/samples/app-templates.md#company-communicator) 向整个组织发送邮件。</span><span class="sxs-lookup"><span data-stu-id="69293-157">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="69293-158">对于此方案，可以使用 Graph API 主动为用户安装应用，然后缓存应用在安装时收到的事件 `conversationUpdate` 所需的值。</span><span class="sxs-lookup"><span data-stu-id="69293-158">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="69293-159">只能安装组织应用目录或 Teams 应用商店中的应用。</span><span class="sxs-lookup"><span data-stu-id="69293-159">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="69293-160">有关 [完整详细信息，请参阅](/graph/teams-proactive-messaging) Graph 文档中的"为用户安装应用"。</span><span class="sxs-lookup"><span data-stu-id="69293-160">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation for complete details.</span></span> <span data-ttu-id="69293-161">.NET 中 [还有一个示例](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)。</span><span class="sxs-lookup"><span data-stu-id="69293-161">There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span></span>

## <a name="examples"></a><span data-ttu-id="69293-162">示例</span><span class="sxs-lookup"><span data-stu-id="69293-162">Examples</span></span>

<span data-ttu-id="69293-163">在使用 REST API 创建新对话之前，请确保你进行身份验证并拥有一个记名令牌。</span><span class="sxs-lookup"><span data-stu-id="69293-163">Be sure that you authenticate and have a bearer token before creating a new conversation using the REST API.</span></span>

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

<span data-ttu-id="69293-164">必须提供用户 ID 和租户 ID。</span><span class="sxs-lookup"><span data-stu-id="69293-164">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="69293-165">如果调用成功，API 将返回以下响应对象。</span><span class="sxs-lookup"><span data-stu-id="69293-165">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

<span data-ttu-id="69293-166">此 ID 是个人聊天的唯一对话 ID。</span><span class="sxs-lookup"><span data-stu-id="69293-166">This ID is the personal chat's unique conversation ID.</span></span> <span data-ttu-id="69293-167">请存储此值，并重复使用它以便将来与用户交互。</span><span class="sxs-lookup"><span data-stu-id="69293-167">Please store this value and reuse it for future interactions with the user.</span></span>

### <a name="using-net"></a><span data-ttu-id="69293-168">使用 .NET</span><span class="sxs-lookup"><span data-stu-id="69293-168">Using .NET</span></span>

<span data-ttu-id="69293-169">此示例使用 [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet 程序包。</span><span class="sxs-lookup"><span data-stu-id="69293-169">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

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

### <a name="using-nodejs"></a><span data-ttu-id="69293-170">使用Node.js</span><span class="sxs-lookup"><span data-stu-id="69293-170">Using Node.js</span></span>

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

<span data-ttu-id="69293-171">*另请参阅 Bot* [Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="69293-171">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="creating-a-channel-conversation"></a><span data-ttu-id="69293-172">创建频道对话</span><span class="sxs-lookup"><span data-stu-id="69293-172">Creating a channel conversation</span></span>

<span data-ttu-id="69293-173">团队添加的机器人可以发布至频道以创建新的回复链。</span><span class="sxs-lookup"><span data-stu-id="69293-173">Your team-added bot can post into a channel to create a new reply chain.</span></span> <span data-ttu-id="69293-174">如果你使用的是 Node.js Teams SDK，请使用它为你提供具有正确活动 ID 和对话 ID 的完全填充 `startReplyChain()` 的地址。如果使用的是 C#，请参阅下面的示例。</span><span class="sxs-lookup"><span data-stu-id="69293-174">If you're using the Node.js Teams SDK, use `startReplyChain()` which gives you a fully-populated address with the correct activity id and conversation id. If you are using C#, see the example below.</span></span>

<span data-ttu-id="69293-175">或者，您可以使用 REST API 向资源发出 POST [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) 请求。</span><span class="sxs-lookup"><span data-stu-id="69293-175">Alternatively, you can use the REST API and issue a POST request to [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) resource.</span></span>

### <a name="net-example-from-this-sample"></a><span data-ttu-id="69293-176">此示例 (.NET[示例) ](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)</span><span class="sxs-lookup"><span data-stu-id="69293-176">.NET example (from [this sample](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))</span></span>

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
