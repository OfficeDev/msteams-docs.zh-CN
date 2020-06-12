---
title: 发送主动邮件
author: clearab
description: 如何使用 Microsoft 团队 bot 发送主动消息。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 6e387dcf0e73124d57996a56c835f5a99fc6f1c6
ms.sourcegitcommit: b822584b643e003d12d2e9b5b02a0534b2d57d71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2020
ms.locfileid: "44704458"
---
# <a name="send-proactive-messages"></a><span data-ttu-id="2a5fa-103">发送主动邮件</span><span class="sxs-lookup"><span data-stu-id="2a5fa-103">Send proactive messages</span></span>

> [!Note]
> <span data-ttu-id="2a5fa-104">本文中的代码示例使用的是 v3 Bot 框架 SDK 和 v3 团队 Bot 生成器 SDK 扩展。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-104">The code samples in this article make use of the v3 Bot Framework SDK, and v3 Teams Bot Builder SDK extensions.</span></span> <span data-ttu-id="2a5fa-105">从概念上讲，此信息适用于使用该 SDK 的 v4 版本，但代码略有不同。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-105">Conceptually, the information applies when using the v4 versions of the SDK, but the code is slightly different.</span></span>

<span data-ttu-id="2a5fa-106">[！注意] 主动消息是由 bot 发送的用于启动对话的邮件。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-106">A proactive message is a message that is sent by a bot to start a conversation.</span></span> <span data-ttu-id="2a5fa-107">出于多种原因，您可能希望机器人启动对话，其中包括：</span><span class="sxs-lookup"><span data-stu-id="2a5fa-107">You may want your bot to start a conversation for a number of reasons, including:</span></span>

* <span data-ttu-id="2a5fa-108">个人 bot 对话的欢迎邮件</span><span class="sxs-lookup"><span data-stu-id="2a5fa-108">Welcome messages for personal bot conversations</span></span>
* <span data-ttu-id="2a5fa-109">轮询响应</span><span class="sxs-lookup"><span data-stu-id="2a5fa-109">Poll responses</span></span>
* <span data-ttu-id="2a5fa-110">外部事件通知</span><span class="sxs-lookup"><span data-stu-id="2a5fa-110">External event notifications</span></span>

<span data-ttu-id="2a5fa-111">发送邮件以启动新的对话线程与发送邮件以响应现有对话不同：当你的 bot 启动新的对话时，没有要将邮件发布到的预先存在的会话。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-111">Sending a message to start a new conversation thread is different than sending a message in response to an existing conversation: when your bot starts a new a conversation, there is no pre-existing conversation to post the message to.</span></span> <span data-ttu-id="2a5fa-112">若要发送一封主动消息，您需要执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="2a5fa-112">In order to send a proactive message you need to:</span></span>

1. [<span data-ttu-id="2a5fa-113">决定要说出的内容</span><span class="sxs-lookup"><span data-stu-id="2a5fa-113">Decide what you're going to say</span></span>](#best-practices-for-proactive-messaging)
1. [<span data-ttu-id="2a5fa-114">获取用户的唯一 Id 和租户 Id</span><span class="sxs-lookup"><span data-stu-id="2a5fa-114">Obtain the user's unique Id and tenant Id</span></span>](#obtain-necessary-user-information)
1. [<span data-ttu-id="2a5fa-115">发送邮件</span><span class="sxs-lookup"><span data-stu-id="2a5fa-115">Send the message</span></span>](#examples)

<span data-ttu-id="2a5fa-116">创建主动预防性邮件时，**必须**调用 `MicrosoftAppCredentials.TrustServiceUrl` 并传入服务 URL，然后才能创建 [`ConnectorClient`](/azure/bot-service/dotnet/bot-builder-dotnet-connector) 将用于发送邮件的。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-116">When creating proactive messages you **must** call `MicrosoftAppCredentials.TrustServiceUrl`, and pass in the service URL before creating the [`ConnectorClient`](/azure/bot-service/dotnet/bot-builder-dotnet-connector) you will use to send the message.</span></span> <span data-ttu-id="2a5fa-117">如果不这样做，您的应用程序将收到 `401: Unauthorized` 响应。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-117">If you do not, your app will receive a `401: Unauthorized` response.</span></span>

> [!Tip]
> <span data-ttu-id="2a5fa-118">有关为 .NET 客户端设置的更多详细信息 `ConnectorClient` ，请参阅 "[发送和接收活动](/azure/bot-service/dotnet/bot-builder-dotnet-connector#create-a-connector-client)" 主题</span><span class="sxs-lookup"><span data-stu-id="2a5fa-118">For more details on setting up the `ConnectorClient` for .NET clients, see the [Send and receive activities](/azure/bot-service/dotnet/bot-builder-dotnet-connector#create-a-connector-client) topic</span></span>
>
> <span data-ttu-id="2a5fa-119">有关发送前瞻性消息的更多示例，可参阅 Azure Bot Service [.net](/azure/bot-service/dotnet/bot-builder-dotnet-proactive-messages)和[Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-proactive-messages)文档</span><span class="sxs-lookup"><span data-stu-id="2a5fa-119">More examples for sending proactive messages can be found in the Azure Bot Service [.NET](/azure/bot-service/dotnet/bot-builder-dotnet-proactive-messages) and [Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-proactive-messages) documentation</span></span>

## <a name="best-practices-for-proactive-messaging"></a><span data-ttu-id="2a5fa-120">主动消息传递的最佳做法</span><span class="sxs-lookup"><span data-stu-id="2a5fa-120">Best practices for proactive messaging</span></span>

<span data-ttu-id="2a5fa-121">向用户发送主动消息是与用户进行通信的一种非常有效的方式。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-121">Sending proactive messages to users can be a very effective way to communicate with your users.</span></span> <span data-ttu-id="2a5fa-122">但是，从其角度看，此消息似乎完全自发，而欢迎消息则是第一次与您的应用程序进行交互的情况。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-122">However, from their perspective this message can appear to come to them completely unprompted, and in the case of welcome messages will be the first time they've interacted with your app.</span></span> <span data-ttu-id="2a5fa-123">因此，谨慎使用此功能非常重要（不要向用户发送垃圾邮件），并为他们提供足够的信息，让他们了解为什么要推广。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-123">As such, it is very important to use this functionality sparingly (don't spam your users), and to provide them with enough information to let them understand why they are being messaged.</span></span>

<span data-ttu-id="2a5fa-124">主动消息通常分为两类：欢迎消息或通知中的一种。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-124">Proactive messages generally fall into one of two categories, welcome messages or notifications.</span></span>

### <a name="welcome-messages"></a><span data-ttu-id="2a5fa-125">欢迎邮件</span><span class="sxs-lookup"><span data-stu-id="2a5fa-125">Welcome messages</span></span>

<span data-ttu-id="2a5fa-126">使用前瞻性消息向用户发送欢迎邮件时，必须注意，对于大多数接收邮件的用户，他们在接收邮件时将没有上下文。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-126">When using proactive messaging to send a welcome message to a user you must keep in mind that for most people receiving the message they will have no context for why they are receiving it.</span></span> <span data-ttu-id="2a5fa-127">这也是第一次将与您的应用程序进行交互。你有机会创建一个理想的首印象。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-127">This is also the first time they will have interacted with your app; it is your opportunity to create a good first impression.</span></span> <span data-ttu-id="2a5fa-128">最佳欢迎消息将包括：</span><span class="sxs-lookup"><span data-stu-id="2a5fa-128">The best welcome messages will include:</span></span>

* <span data-ttu-id="2a5fa-129">**为什么他们收到此邮件。**</span><span class="sxs-lookup"><span data-stu-id="2a5fa-129">**Why are they receiving this message.**</span></span> <span data-ttu-id="2a5fa-130">应非常清楚用户接收邮件的原因。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-130">It should be very clear to the user why they are receiving the message.</span></span> <span data-ttu-id="2a5fa-131">如果你的 bot 已安装在频道中，并且你向所有用户发送了欢迎消息，请让他们知道它安装在什么频道并有权安装它。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-131">If your bot was installed in a channel and you sent a welcome message to all users, let them know what channel it was installed in and potentially who installed it.</span></span>
* <span data-ttu-id="2a5fa-132">**你提供的内容。**</span><span class="sxs-lookup"><span data-stu-id="2a5fa-132">**What do you offer.**</span></span> <span data-ttu-id="2a5fa-133">他们可以对你的应用程序做些什么？</span><span class="sxs-lookup"><span data-stu-id="2a5fa-133">What can they do with your app?</span></span> <span data-ttu-id="2a5fa-134">您可以为它们引入什么值？</span><span class="sxs-lookup"><span data-stu-id="2a5fa-134">What value can you bring to them?</span></span>
* <span data-ttu-id="2a5fa-135">**接下来应做些什么。**</span><span class="sxs-lookup"><span data-stu-id="2a5fa-135">**What should they do next.**</span></span> <span data-ttu-id="2a5fa-136">邀请他们试用某个命令，或以某种方式与您的应用程序进行交互。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-136">Invite them to try out a command, or interact with your app in some way.</span></span>

### <a name="notification-messages"></a><span data-ttu-id="2a5fa-137">通知邮件</span><span class="sxs-lookup"><span data-stu-id="2a5fa-137">Notification messages</span></span>

<span data-ttu-id="2a5fa-138">使用主动消息发送通知时，您需要确保您的用户有一个明确的路径，以根据您的通知执行常见操作，并清楚地了解通知发生的原因。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-138">When using proactive messaging to send notifications you need to make sure your users have a clear path to take common actions based on your notification, and a clear understanding of why the notification occurred.</span></span> <span data-ttu-id="2a5fa-139">正常的通知消息通常包括：</span><span class="sxs-lookup"><span data-stu-id="2a5fa-139">Good notification messages will generally include:</span></span>

* <span data-ttu-id="2a5fa-140">**发生了什么事。**</span><span class="sxs-lookup"><span data-stu-id="2a5fa-140">**What happened.**</span></span> <span data-ttu-id="2a5fa-141">可以清楚地指示导致通知发生了什么情况。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-141">A clear indication of what happened to cause the notification.</span></span>
* <span data-ttu-id="2a5fa-142">**它发生的变化。**</span><span class="sxs-lookup"><span data-stu-id="2a5fa-142">**What it happened to.**</span></span> <span data-ttu-id="2a5fa-143">应清楚是什么项目/内容已更新，从而导致通知。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-143">It should be clear what item/thing was updated to cause the notification.</span></span>
* <span data-ttu-id="2a5fa-144">**已完成的操作。**</span><span class="sxs-lookup"><span data-stu-id="2a5fa-144">**Who did it.**</span></span> <span data-ttu-id="2a5fa-145">谁采取了导致通知发送的操作。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-145">Who took the action that caused the notification to be sent.</span></span>
* <span data-ttu-id="2a5fa-146">**他们可以执行的操作。**</span><span class="sxs-lookup"><span data-stu-id="2a5fa-146">**What they can do about it.**</span></span> <span data-ttu-id="2a5fa-147">使您的用户可以轻松地根据您的通知执行操作。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-147">Make it easy for your users to take actions based on your notifications.</span></span>
* <span data-ttu-id="2a5fa-148">**他们可以选择退出。** 您需要为用户提供一个路径，以供用户退出其他通知。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-148">**How they can opt out.** You need to provide a path for users to opt out of additional notifications.</span></span>

## <a name="obtain-necessary-user-information"></a><span data-ttu-id="2a5fa-149">获取必要的用户信息</span><span class="sxs-lookup"><span data-stu-id="2a5fa-149">Obtain necessary user information</span></span>

<span data-ttu-id="2a5fa-150">Bot 可以通过获取用户的*唯一 ID*和*租户 id* ，创建与单个 Microsoft 团队用户的新对话。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-150">Bots can create new conversations with an individual Microsoft Teams user by obtaining the user's *unique ID* and *tenant ID.*</span></span> <span data-ttu-id="2a5fa-151">您可以使用下列方法之一获取这些值：</span><span class="sxs-lookup"><span data-stu-id="2a5fa-151">You can obtain these values using one of the following methods:</span></span>

* <span data-ttu-id="2a5fa-152">通过从频道中[提取团队名单，](../get-teams-context.md#fetching-the-roster-or-user-profile)您的应用程序已安装在中。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-152">By [fetching the team roster](../get-teams-context.md#fetching-the-roster-or-user-profile) from a channel your app is installed in.</span></span>
* <span data-ttu-id="2a5fa-153">通过在用户[与频道中的 bot 交互](./channel-and-group-conversations.md)时缓存这些文件。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-153">By caching them when a user [interacts with your bot in a channel](./channel-and-group-conversations.md).</span></span>
* <span data-ttu-id="2a5fa-154">当用户[在频道对话中 @mentioned](./channel-and-group-conversations.md#retrieving-mentions)时，bot 是的一部分。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-154">When a users is [@mentioned in a channel conversation](./channel-and-group-conversations.md#retrieving-mentions) the bot is a part of.</span></span>
* <span data-ttu-id="2a5fa-155">当您的应用程序安装在个人作用域中时，当您[收到 `conversationUpdate` ](./subscribe-to-conversation-events.md#team-members-added)事件时缓存它们，或将新成员添加到频道或组聊天</span><span class="sxs-lookup"><span data-stu-id="2a5fa-155">By caching them when you [receive the `conversationUpdate`](./subscribe-to-conversation-events.md#team-members-added) event when your app is installed in a personal scope, or new members are added to a channel or group chat that</span></span>

### <a name="proactively-install-your-app-using-graph"></a><span data-ttu-id="2a5fa-156">使用 Graph 主动安装您的应用程序</span><span class="sxs-lookup"><span data-stu-id="2a5fa-156">Proactively install your app using Graph</span></span>

> [!Note]
> <span data-ttu-id="2a5fa-157">使用 graph 主动安装应用当前处于 beta 中。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-157">Proactively installing apps using graph is currently in beta.</span></span>

<span data-ttu-id="2a5fa-158">有时，可能有必要主动向尚未安装或与您的应用程序进行交互的邮件用户进行处理。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-158">Occasionally it may be necessary to proactively message users that have not installed or interacted with your app previously.</span></span> <span data-ttu-id="2a5fa-159">例如，您希望使用[公司 communicator](~/samples/app-templates.md#company-communicator)向整个组织发送邮件。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-159">For example, you want to use the [company communicator](~/samples/app-templates.md#company-communicator) to send messages to your entire organization.</span></span> <span data-ttu-id="2a5fa-160">在这种情况下，您可以使用 Graph API 主动为您的用户安装您的应用程序，然后从 `conversationUpdate` 应用程序安装时收到的事件中缓存必要的值。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-160">For this scenario you can use the Graph API to proactively install your app for your users, then cache the necessary values from the `conversationUpdate` event your app will receive upon install.</span></span>

<span data-ttu-id="2a5fa-161">您只能安装组织应用程序目录或团队应用商店中的应用程序。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-161">You can only install apps that are in your organizational app catalogue, or the Teams app store.</span></span>

<span data-ttu-id="2a5fa-162">有关完整的详细信息，请参阅在 Graph 文档中[安装用户的应用程序](/graph/teams-proactive-messaging)。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-162">See [Install apps for users](/graph/teams-proactive-messaging) in the Graph documentation for complete details.</span></span> <span data-ttu-id="2a5fa-163">[.Net 中](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)也有一个示例。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-163">There is also a [sample in .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).</span></span>

## <a name="examples"></a><span data-ttu-id="2a5fa-164">示例</span><span class="sxs-lookup"><span data-stu-id="2a5fa-164">Examples</span></span>

<span data-ttu-id="2a5fa-165">在使用 REST API 创建新对话之前，请务必对持有者令牌进行身份验证并拥有持有者令牌。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-165">Be sure that you authenticate and have a bearer token before creating a new conversation using the REST API.</span></span> <span data-ttu-id="2a5fa-166">`members.id`下面的对象中的字段对你的 bot 和用户的组合是唯一的。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-166">The `members.id` field in the object below is unique to the combination of your bot and a user.</span></span> <span data-ttu-id="2a5fa-167">您不能通过任何其他方法获取它，而不是以上所述。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-167">You cannot obtain it via any other method than those outlined above.</span></span>

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

<span data-ttu-id="2a5fa-168">您必须提供用户 ID 和租户 ID。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-168">You must supply the user ID and the tenant ID.</span></span> <span data-ttu-id="2a5fa-169">如果调用成功，API 将返回以下响应对象。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-169">If the call succeeds, the API returns with the following response object.</span></span>

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

<span data-ttu-id="2a5fa-170">此 ID 是个人聊天的唯一会话 ID。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-170">This ID is the personal chat's unique conversation ID.</span></span> <span data-ttu-id="2a5fa-171">请存储此值并重用它以供用户将来交互。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-171">Please store this value and reuse it for future interactions with the user.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="2a5fa-172">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="2a5fa-172">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="2a5fa-173">本示例使用的是 ".[团队](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)" NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-173">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span> <span data-ttu-id="2a5fa-174">在此示例中， `client` 是已 `ConnectorClient` 按照[发送和接收活动](/azure/bot-service/dotnet/bot-builder-dotnet-connector)中所述创建和验证的实例</span><span class="sxs-lookup"><span data-stu-id="2a5fa-174">In this example, `client` is a `ConnectorClient` instance that has already been created and authenticated as described in [Send and receive activities](/azure/bot-service/dotnet/bot-builder-dotnet-connector)</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="2a5fa-175">JavaScript</span><span class="sxs-lookup"><span data-stu-id="2a5fa-175">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="2a5fa-176">*另请参阅* [Bot 框架示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-176">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

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

# <a name="python"></a>[<span data-ttu-id="2a5fa-177">Python</span><span class="sxs-lookup"><span data-stu-id="2a5fa-177">Python</span></span>](#tab/python)

```python
async def _send_proactive_message():
  for conversation_reference in CONVERSATION_REFERENCES.values():
    return await ADAPTER.continue_conversation(APP_ID, conversation_reference,
      lambda turn_context: turn_context.send_activity("proactive hello")
    )

```

---

## <a name="creating-a-channel-conversation"></a><span data-ttu-id="2a5fa-178">创建频道对话</span><span class="sxs-lookup"><span data-stu-id="2a5fa-178">Creating a channel conversation</span></span>

<span data-ttu-id="2a5fa-179">您的团队添加的 bot 可以发布到通道中，以创建新的答复链。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-179">Your team-added bot can post into a channel to create a new reply chain.</span></span> <span data-ttu-id="2a5fa-180">如果您使用的是 Node.js 团队 SDK，请使用以 `startReplyChain()` 正确的活动 id 和会话 id 为您提供完全填充的地址。如果使用的是 c #，请参阅下面的示例。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-180">If you're using the Node.js Teams SDK, use `startReplyChain()` which gives you a fully-populated address with the correct activity id and conversation id. If you are using C#, see the example below.</span></span>

<span data-ttu-id="2a5fa-181">或者，也可以使用 REST API 并向 resource 发出 POST 请求 [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) 。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-181">Alternatively, you can use the REST API and issue a POST request to [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) resource.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="2a5fa-182">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="2a5fa-182">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="2a5fa-183">下面的代码段来自[此示例](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-183">The following code snippet is from [this sample](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs).</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="2a5fa-184">JavaScript</span><span class="sxs-lookup"><span data-stu-id="2a5fa-184">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="2a5fa-185">下面的代码片段来自[teamsConversationBot.js](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js)。</span><span class="sxs-lookup"><span data-stu-id="2a5fa-185">The following code snippet is from [teamsConversationBot.js](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js).</span></span>

[!code-javascript[messageAllMembersAsync](~/../botbuilder-samples/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js?range=115-134&highlight=13-15)]

# <a name="python"></a>[<span data-ttu-id="2a5fa-186">Python</span><span class="sxs-lookup"><span data-stu-id="2a5fa-186">Python</span></span>](#tab/python)

[!code-python[message-all-members](~/../botbuilder-samples/samples/python/57.teams-conversation-bot/bots/teams_conversation_bot.py?range=101-135)]

---
