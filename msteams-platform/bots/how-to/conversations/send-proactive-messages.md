---
title: 发送主动消息
author: clearab
description: 如何使用 Microsoft 团队 bot 发送主动消息。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2821e4d7ddeb74b3921be792cc55a136ab4ac5e4
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228078"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="f62b1-103">发送主动消息</span><span class="sxs-lookup"><span data-stu-id="f62b1-103">Send proactive messages</span></span>

> [!Note]
> <span data-ttu-id="f62b1-104">本文中的代码示例使用的是 v3 Bot 框架 SDK 和 v3 团队 Bot 生成器 SDK 扩展。</span><span class="sxs-lookup"><span data-stu-id="f62b1-104">The code samples in this article make use of the v3 Bot Framework SDK, and v3 Teams Bot Builder SDK extensions.</span></span> <span data-ttu-id="f62b1-105">从概念上讲，此信息适用于使用该 SDK 的 v4 版本，但代码略有不同。</span><span class="sxs-lookup"><span data-stu-id="f62b1-105">Conceptually, the information applies when using the v4 versions of the SDK, but the code is slightly different.</span></span>

<span data-ttu-id="f62b1-106">[！注意] 主动消息是由 bot 发送的用于启动对话的邮件。</span><span class="sxs-lookup"><span data-stu-id="f62b1-106">A proactive message is a message that is sent by a bot to start a conversation.</span></span> <span data-ttu-id="f62b1-107">出于多种原因，您可能希望机器人启动对话，其中包括：</span><span class="sxs-lookup"><span data-stu-id="f62b1-107">You may want your bot to start a conversation for a number of reasons, including:</span></span>

* <span data-ttu-id="f62b1-108">个人 bot 对话的欢迎邮件</span><span class="sxs-lookup"><span data-stu-id="f62b1-108">Welcome messages for personal bot conversations</span></span>
* <span data-ttu-id="f62b1-109">轮询响应</span><span class="sxs-lookup"><span data-stu-id="f62b1-109">Poll responses</span></span>
* <span data-ttu-id="f62b1-110">外部事件通知</span><span class="sxs-lookup"><span data-stu-id="f62b1-110">External event notifications</span></span>

<span data-ttu-id="f62b1-111">发送邮件以启动新的对话线程与发送邮件以响应现有对话不同：当你的 bot 启动新的对话时，没有要将邮件发布到的预先存在的会话。</span><span class="sxs-lookup"><span data-stu-id="f62b1-111">Sending a message to start a new conversation thread is different than sending a message in response to an existing conversation: when your bot starts a new a conversation, there is no pre-existing conversation to post the message to.</span></span> <span data-ttu-id="f62b1-112">若要发送一封主动消息，您需要执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="f62b1-112">In order to send a proactive message you need to:</span></span>

1. [<span data-ttu-id="f62b1-113">决定要说出的内容</span><span class="sxs-lookup"><span data-stu-id="f62b1-113">Decide what you're going to say</span></span>](#best-practices-for-proactive-messaging)
1. [<span data-ttu-id="f62b1-114">获取用户的唯一 Id 和租户 Id</span><span class="sxs-lookup"><span data-stu-id="f62b1-114">Obtain the user's unique Id and tenant Id</span></span>](#obtain-necessary-user-information)
1. [<span data-ttu-id="f62b1-115">发送邮件</span><span class="sxs-lookup"><span data-stu-id="f62b1-115">Send the message</span></span>](#examples)

<span data-ttu-id="f62b1-116">创建主动预防性邮件\*\*\*\* 时， `MicrosoftAppCredentials.TrustServiceUrl`必须调用并传入服务 URL，然后才能创建`ConnectorClient`将用于发送邮件的。</span><span class="sxs-lookup"><span data-stu-id="f62b1-116">When creating proactive messages you **must** call `MicrosoftAppCredentials.TrustServiceUrl`, and pass in the service URL before creating the `ConnectorClient` you will use to send the message.</span></span> <span data-ttu-id="f62b1-117">如果不这样做，您的应用程序将`401: Unauthorized`收到响应。</span><span class="sxs-lookup"><span data-stu-id="f62b1-117">If you do not, your app will receive a `401: Unauthorized` response.</span></span> 

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="f62b1-118">主动消息传递的最佳做法</span><span class="sxs-lookup"><span data-stu-id="f62b1-118">Best practices for proactive messaging</span></span>

<span data-ttu-id="f62b1-119">向用户发送主动消息是与用户进行通信的一种非常有效的方式。</span><span class="sxs-lookup"><span data-stu-id="f62b1-119">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="f62b1-120">但是，从其角度看，此消息似乎完全自发，而欢迎消息则是第一次与您的应用程序进行交互的情况。</span><span class="sxs-lookup"><span data-stu-id="f62b1-120">However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app.</span></span> <span data-ttu-id="f62b1-121">因此，谨慎使用此功能非常重要（不要向用户发送垃圾邮件），并为他们提供足够的信息，让他们了解为什么要推广。</span><span class="sxs-lookup"><span data-stu-id="f62b1-121">As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.</span></span>

<span data-ttu-id="f62b1-122">主动消息通常分为两类：欢迎消息或通知中的一种。</span><span class="sxs-lookup"><span data-stu-id="f62b1-122">Proactive messages generally fall into one of two categories, welcome messages or notifications.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="f62b1-123">欢迎邮件</span><span class="sxs-lookup"><span data-stu-id="f62b1-123">Welcome messages</span></span>

<span data-ttu-id="f62b1-124">使用前瞻性消息向用户发送欢迎邮件时，必须注意，对于大多数接收邮件的用户，他们在接收邮件时将没有上下文。</span><span class="sxs-lookup"><span data-stu-id="f62b1-124">When using proactive messaging to send a welcome message to a user you must keep in mind that for most people receiving the message they will have no context for why they are receiving it.</span></span> <span data-ttu-id="f62b1-125">这也是第一次将与您的应用程序进行交互。你有机会创建一个理想的首印象。</span><span class="sxs-lookup"><span data-stu-id="f62b1-125">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="f62b1-126">最佳欢迎消息将包括：</span><span class="sxs-lookup"><span data-stu-id="f62b1-126">The best welcome messages will include:</span></span>

* <span data-ttu-id="f62b1-127">**为什么他们收到此邮件。**</span><span class="sxs-lookup"><span data-stu-id="f62b1-127">**Why are they receiving this message.**</span></span> <span data-ttu-id="f62b1-128">应非常清楚用户接收邮件的原因。</span><span class="sxs-lookup"><span data-stu-id="f62b1-128">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="f62b1-129">如果你的 bot 已安装在频道中，并且你向所有用户发送了欢迎消息，请让他们知道它安装在什么频道并有权安装它。</span><span class="sxs-lookup"><span data-stu-id="f62b1-129">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="f62b1-130">**你提供的内容。**</span><span class="sxs-lookup"><span data-stu-id="f62b1-130">**What do you offer.**</span></span> <span data-ttu-id="f62b1-131">他们可以对你的应用程序做些什么？</span><span class="sxs-lookup"><span data-stu-id="f62b1-131">What can they do with your app?</span></span> <span data-ttu-id="f62b1-132">您可以为它们引入什么值？</span><span class="sxs-lookup"><span data-stu-id="f62b1-132">What value can you bring to them?</span></span>
* <span data-ttu-id="f62b1-133">**接下来应做些什么。**</span><span class="sxs-lookup"><span data-stu-id="f62b1-133">**What should they do next.**</span></span> <span data-ttu-id="f62b1-134">邀请他们试用某个命令，或以某种方式与您的应用程序进行交互。</span><span class="sxs-lookup"><span data-stu-id="f62b1-134">Invite them to try out a command, or interact with your app in some way.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="f62b1-135">通知邮件</span><span class="sxs-lookup"><span data-stu-id="f62b1-135">Notification messages</span></span>

<span data-ttu-id="f62b1-136">使用主动消息发送通知时，您需要确保您的用户有一个明确的路径，以根据您的通知执行常见操作，并清楚地了解通知发生的原因。</span><span class="sxs-lookup"><span data-stu-id="f62b1-136">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification, and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="f62b1-137">正常的通知消息通常包括：</span><span class="sxs-lookup"><span data-stu-id="f62b1-137">Good notification messages will generally include:</span></span>

* <span data-ttu-id="f62b1-138">**发生了什么事。**</span><span class="sxs-lookup"><span data-stu-id="f62b1-138">**What happened.**</span></span> <span data-ttu-id="f62b1-139">可以清楚地指示导致通知发生了什么情况。</span><span class="sxs-lookup"><span data-stu-id="f62b1-139">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="f62b1-140">**它发生的变化。**</span><span class="sxs-lookup"><span data-stu-id="f62b1-140">**What it happened to.**</span></span> <span data-ttu-id="f62b1-141">应清楚是什么项目/内容已更新，从而导致通知。</span><span class="sxs-lookup"><span data-stu-id="f62b1-141">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="f62b1-142">**已完成的操作。**</span><span class="sxs-lookup"><span data-stu-id="f62b1-142">**Who did it.**</span></span> <span data-ttu-id="f62b1-143">谁采取了导致通知发送的操作。</span><span class="sxs-lookup"><span data-stu-id="f62b1-143">Who took the action that caused the notification to be sent.</span></span>
* <span data-ttu-id="f62b1-144">**他们可以执行的操作。**</span><span class="sxs-lookup"><span data-stu-id="f62b1-144">**What they can do about it.**</span></span> <span data-ttu-id="f62b1-145">使您的用户可以轻松地根据您的通知执行操作。</span><span class="sxs-lookup"><span data-stu-id="f62b1-145">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="f62b1-146">**他们可以选择退出。** 您需要为用户提供一个路径，以供用户退出其他通知。</span><span class="sxs-lookup"><span data-stu-id="f62b1-146">**How they can opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="obtain-necessary-user-information"></a><span data-ttu-id="f62b1-147">获取必要的用户信息</span><span class="sxs-lookup"><span data-stu-id="f62b1-147">Obtain necessary user information</span></span>

<span data-ttu-id="f62b1-148">Bot 可以通过获取用户的*唯一 ID*和*租户 id* ，创建与单个 Microsoft 团队用户的新对话。</span><span class="sxs-lookup"><span data-stu-id="f62b1-148">Bots can create new conversations with an individual Microsoft Teams user by obtaining the user’s *unique ID* and *tenant ID.*</span></span> <span data-ttu-id="f62b1-149">您可以使用下列方法之一获取这些值：</span><span class="sxs-lookup"><span data-stu-id="f62b1-149">You can obtain these values using one of the following methods:</span></span>

* <span data-ttu-id="f62b1-150">通过从频道中[提取团队名单，](../get-teams-context.md#fetching-the-roster-or-user-profile)您的应用程序已安装在中。</span><span class="sxs-lookup"><span data-stu-id="f62b1-150">By [fetching the team roster](../get-teams-context.md#fetching-the-roster-or-user-profile) from a channel your app is installed in.</span></span>
* <span data-ttu-id="f62b1-151">通过在用户[与频道中的 bot 交互](./channel-and-group-conversations.md)时缓存这些文件。</span><span class="sxs-lookup"><span data-stu-id="f62b1-151">By caching them when a user [interacts with your bot in a channel](./channel-and-group-conversations.md).</span></span>
* <span data-ttu-id="f62b1-152">当用户[在频道对话中 @mentioned](./channel-and-group-conversations.md#retrieving-mentions)时，bot 是的一部分。</span><span class="sxs-lookup"><span data-stu-id="f62b1-152">When a users is [@mentioned in a channel conversation](./channel-and-group-conversations.md#retrieving-mentions) the bot is a part of.</span></span>
* <span data-ttu-id="f62b1-153">当您的应用程序安装在个人作用域中时，当您[收到`conversationUpdate` ](./subscribe-to-conversation-events.md#team-members-added)事件时缓存它们，或将新成员添加到频道或组聊天</span><span class="sxs-lookup"><span data-stu-id="f62b1-153">By caching them when you [receive the `conversationUpdate`](./subscribe-to-conversation-events.md#team-members-added) event when your app is installed in a personal scope, or new members are added to a channel or group chat that</span></span>

### <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="f62b1-154">使用 Graph 主动安装您的应用程序</span><span class="sxs-lookup"><span data-stu-id="f62b1-154">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="f62b1-155">使用 graph 主动安装应用当前处于 beta 中。</span><span class="sxs-lookup"><span data-stu-id="f62b1-155">Proactively installing apps using graph is currently in beta.</span></span>

<span data-ttu-id="f62b1-156">有时，可能有必要主动向尚未安装或与您的应用程序进行交互的邮件用户进行处理。</span><span class="sxs-lookup"><span data-stu-id="f62b1-156">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="f62b1-157">例如，您希望使用[公司 communicator](~/samples/app-templates.md#company-communicator)向整个组织发送邮件。</span><span class="sxs-lookup"><span data-stu-id="f62b1-157">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="f62b1-158">在这种情况下，您可以使用 Graph API 主动为您的用户安装您的应用程序，然后从应用`conversationUpdate`程序安装时收到的事件中缓存必要的值。</span><span class="sxs-lookup"><span data-stu-id="f62b1-158">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="f62b1-159">您只能安装组织应用程序目录或团队应用商店中的应用程序。</span><span class="sxs-lookup"><span data-stu-id="f62b1-159">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="f62b1-160">有关完整的详细信息，请参阅在 Graph 文档中[安装用户的应用程序](/graph/teams-proactive-messaging)。</span><span class="sxs-lookup"><span data-stu-id="f62b1-160">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation for complete details.</span></span> <span data-ttu-id="f62b1-161">[.Net 中](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)也有一个示例。</span><span class="sxs-lookup"><span data-stu-id="f62b1-161">There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span></span>

## <a name="examples"></a><span data-ttu-id="f62b1-162">示例</span><span class="sxs-lookup"><span data-stu-id="f62b1-162">Examples</span></span>

<span data-ttu-id="f62b1-163">在使用 REST API 创建新对话之前，请务必对持有者令牌进行身份验证并拥有持有者令牌。</span><span class="sxs-lookup"><span data-stu-id="f62b1-163">Be sure that you authenticate and have a bearer token before creating a new conversation using the REST API.</span></span> <span data-ttu-id="f62b1-164">下面`members.id`的对象中的字段对你的 bot 和用户的组合是唯一的。</span><span class="sxs-lookup"><span data-stu-id="f62b1-164">The `members.id` field in the object below is unique to the combination of your bot and a user.</span></span> <span data-ttu-id="f62b1-165">您不能通过任何其他方法获取它，而不是以上所述。</span><span class="sxs-lookup"><span data-stu-id="f62b1-165">You cannot obtain it via any other method than those outlined above.</span></span>

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

<span data-ttu-id="f62b1-166">您必须提供用户 ID 和租户 ID。</span><span class="sxs-lookup"><span data-stu-id="f62b1-166">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="f62b1-167">如果调用成功，API 将返回以下响应对象。</span><span class="sxs-lookup"><span data-stu-id="f62b1-167">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

<span data-ttu-id="f62b1-168">此 ID 是个人聊天的唯一会话 ID。</span><span class="sxs-lookup"><span data-stu-id="f62b1-168">This ID is the personal chat's unique conversation ID.</span></span> <span data-ttu-id="f62b1-169">请存储此值并重用它以供用户将来交互。</span><span class="sxs-lookup"><span data-stu-id="f62b1-169">Please store this value and reuse it for future interactions with the user.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f62b1-170">C #/.NET</span><span class="sxs-lookup"><span data-stu-id="f62b1-170">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="f62b1-171">本示例使用的是 ".[团队](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)" NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="f62b1-171">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="f62b1-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="f62b1-172">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="f62b1-173">*另请参阅* [Bot 框架示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="f62b1-173">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

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

# <a name="python"></a>[<span data-ttu-id="f62b1-174">Python</span><span class="sxs-lookup"><span data-stu-id="f62b1-174">Python</span></span>](#tab/python)

```python
async def _send_proactive_message():
  for conversation_reference in CONVERSATION_REFERENCES.values():
    return await ADAPTER.continue_conversation(APP_ID, conversation_reference,
      lambda turn_context: turn_context.send_activity("proactive hello")
    )

```

---

## <a name="creating-a-channel-conversation"></a><span data-ttu-id="f62b1-175">创建频道对话</span><span class="sxs-lookup"><span data-stu-id="f62b1-175">Creating a channel conversation</span></span>

<span data-ttu-id="f62b1-176">您的团队添加的 bot 可以发布到通道中，以创建新的答复链。</span><span class="sxs-lookup"><span data-stu-id="f62b1-176">Your team-added bot can post into a channel to create a new reply chain.</span></span> <span data-ttu-id="f62b1-177">如果您使用的是 node.js 团队 SDK，则使用`startReplyChain()`可为您提供一个具有正确的活动 id 和会话 id 的完全填充的地址。如果使用的是 c #，请参阅下面的示例。</span><span class="sxs-lookup"><span data-stu-id="f62b1-177">If you're using the Node.js Teams SDK, use `startReplyChain()` which gives you a fully-populated address with the correct activity id and conversation id. If you are using C#, see the example below.</span></span>

<span data-ttu-id="f62b1-178">或者，也可以使用 REST API 并向[`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) RESOURCE 发出 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="f62b1-178">Alternatively, you can use the REST API and issue a POST request to [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) resource.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f62b1-179">C #/.NET</span><span class="sxs-lookup"><span data-stu-id="f62b1-179">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="f62b1-180">下面的代码段来自[此示例](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)。</span><span class="sxs-lookup"><span data-stu-id="f62b1-180">The following code snippet is from [this sample](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs).</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="f62b1-181">JavaScript</span><span class="sxs-lookup"><span data-stu-id="f62b1-181">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="f62b1-182">下面的代码片段来自[teamsConversationBot](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js)。</span><span class="sxs-lookup"><span data-stu-id="f62b1-182">The following code snippet is from [teamsConversationBot.js](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js).</span></span>

[!code-javascript[messageAllMembersAsync](~/../botbuilder-samples/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js?range=115-134&highlight=13-15)]

# <a name="python"></a>[<span data-ttu-id="f62b1-183">Python</span><span class="sxs-lookup"><span data-stu-id="f62b1-183">Python</span></span>](#tab/python)

[!code-python[message-all-members](~/../botbuilder-samples/samples/python/57.teams-conversation-bot/bots/teams_conversation_bot.py?range=101-135)]

---
