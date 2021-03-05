---
title: 对话基础知识
description: 介绍与 Microsoft Teams 机器人对话的方法
ms.topic: overview
ms.author: anclear
keyword: conversations basics receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 4eba22e9b29f5378dc03480ba5f6ba421f816eb3
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449505"
---
# <a name="conversation-basics"></a><span data-ttu-id="e25b6-103">对话基础知识</span><span class="sxs-lookup"><span data-stu-id="e25b6-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="e25b6-104">对话是在自动程序与一个或多个用户之间发送的一系列消息。</span><span class="sxs-lookup"><span data-stu-id="e25b6-104">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="e25b6-105">有三种类型的对话，在 Teams 中也称为范围：</span><span class="sxs-lookup"><span data-stu-id="e25b6-105">There are three types of conversations, also called scopes in Teams:</span></span>

| <span data-ttu-id="e25b6-106">对话类型</span><span class="sxs-lookup"><span data-stu-id="e25b6-106">Conversation type</span></span> | <span data-ttu-id="e25b6-107">说明</span><span class="sxs-lookup"><span data-stu-id="e25b6-107">Description</span></span> |
| ------- | ----------- |
|  `teams` | <span data-ttu-id="e25b6-108">也称为频道对话，对频道的所有成员可见。</span><span class="sxs-lookup"><span data-stu-id="e25b6-108">Also called channel conversations, visible to all members of the channel.</span></span> |
| `personal` | <span data-ttu-id="e25b6-109">机器人和单个用户之间的对话。</span><span class="sxs-lookup"><span data-stu-id="e25b6-109">Conversations between bots and a single user.</span></span> |
| `groupChat` | <span data-ttu-id="e25b6-110">机器人与两个或多个用户之间的聊天。</span><span class="sxs-lookup"><span data-stu-id="e25b6-110">Chat between a bot and two or more users.</span></span> <span data-ttu-id="e25b6-111">此外，还可以在会议聊天中启用机器人。</span><span class="sxs-lookup"><span data-stu-id="e25b6-111">Also enables your bot in meeting chats.</span></span> |

<span data-ttu-id="e25b6-112">自动程序的行为稍有不同，具体取决于它涉及的对话类型：</span><span class="sxs-lookup"><span data-stu-id="e25b6-112">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="e25b6-113">频道和群聊对话中的聊天机器人要求用户 @ 提及机器人，以在频道中调用它。</span><span class="sxs-lookup"><span data-stu-id="e25b6-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="e25b6-114">一对一对话中的机器人不需要 @ 提及。</span><span class="sxs-lookup"><span data-stu-id="e25b6-114">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="e25b6-115">用户发送的所有消息将路由到机器人。</span><span class="sxs-lookup"><span data-stu-id="e25b6-115">All messages sent by the user routes to your bot.</span></span>

<span data-ttu-id="e25b6-116">若要启用特定作用域中的自动程序，请将此范围添加到[应用清单。](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="e25b6-116">To enable your bot in a particular scope, add that scope to your [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="activities"></a><span data-ttu-id="e25b6-117">活动</span><span class="sxs-lookup"><span data-stu-id="e25b6-117">Activities</span></span>

<span data-ttu-id="e25b6-118">每封邮件都是 `Activity` 一个类型对象 `messageType: message` 。</span><span class="sxs-lookup"><span data-stu-id="e25b6-118">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="e25b6-119">当用户发送消息时，Teams 会向机器人发布消息;具体而言，它会将 JSON 对象发送到机器人的消息终结点。</span><span class="sxs-lookup"><span data-stu-id="e25b6-119">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="e25b6-120">机器人会检查邮件以确定其类型并相应地做出响应。</span><span class="sxs-lookup"><span data-stu-id="e25b6-120">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="e25b6-121">基本对话通过自动程序框架连接器（一个 REST API）进行处理。</span><span class="sxs-lookup"><span data-stu-id="e25b6-121">Basic conversations are handled through the Bot Framework Connector, a single REST API.</span></span> <span data-ttu-id="e25b6-122">此 API 使机器人能够与 Teams 和其他频道进行通信。</span><span class="sxs-lookup"><span data-stu-id="e25b6-122">This API enables your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="e25b6-123">Bot Builder SDK 提供对此 API 的轻松访问、用于管理对话流和状态的其他功能，以及合并认知服务的简单方法，如自然语言处理 (NLP) 。</span><span class="sxs-lookup"><span data-stu-id="e25b6-123">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as Natural Language Processing (NLP).</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="e25b6-124">接收邮件</span><span class="sxs-lookup"><span data-stu-id="e25b6-124">Receive a message</span></span>

<span data-ttu-id="e25b6-125">若要接收短信，请使用 `Text` 对象 `Activity` 的属性。</span><span class="sxs-lookup"><span data-stu-id="e25b6-125">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="e25b6-126">在自动程序的活动处理程序中，使用 turn context 对象读取 `Activity` 单个邮件请求。</span><span class="sxs-lookup"><span data-stu-id="e25b6-126">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="e25b6-127">以下代码是一个示例。</span><span class="sxs-lookup"><span data-stu-id="e25b6-127">The following code shows an example.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e25b6-128">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e25b6-128">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e25b6-129">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e25b6-129">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity(`Echo: '${context.activity.text}'`);
            await next();
        });
    }
}

```

# <a name="python"></a>[<span data-ttu-id="e25b6-130">Python</span><span class="sxs-lookup"><span data-stu-id="e25b6-130">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="e25b6-131">JSON</span><span class="sxs-lookup"><span data-stu-id="e25b6-131">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot",
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

---

## <a name="send-a-message"></a><span data-ttu-id="e25b6-132">发送邮件</span><span class="sxs-lookup"><span data-stu-id="e25b6-132">Send a message</span></span>

<span data-ttu-id="e25b6-133">若要发送短信，请指定要作为活动发送的字符串。</span><span class="sxs-lookup"><span data-stu-id="e25b6-133">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="e25b6-134">在机器人的活动处理程序中，使用 turn context 对象的方法 `SendActivityAsync` 发送单个消息响应。</span><span class="sxs-lookup"><span data-stu-id="e25b6-134">In the bot's activity handler, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="e25b6-135">使用对象的方法 `SendActivitiesAsync` 一次发送多个响应。</span><span class="sxs-lookup"><span data-stu-id="e25b6-135">Use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="e25b6-136">以下代码显示了将某人添加到对话时发送邮件的示例。</span><span class="sxs-lookup"><span data-stu-id="e25b6-136">The following code shows an example of sending a message when someone is added to a conversation.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e25b6-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e25b6-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e25b6-138">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e25b6-138">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity('Hello and welcome!');
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="e25b6-139">Python</span><span class="sxs-lookup"><span data-stu-id="e25b6-139">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="e25b6-140">JSON</span><span class="sxs-lookup"><span data-stu-id="e25b6-140">JSON</span></span>](#tab/json)

```json
{
    "text": "hi",
    "textFormat": "plain",
    "type": "message",
    "timestamp": "2019-10-31T20:57:27.2347285Z",
    "localTimestamp": "2019-10-31T13:57:27.2347285-07:00",
    "id": "1572555447214",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "from": {
        "id": "29:1Xv-kvy4dKirR0rZfSF_kAVUzotoT1SXuEzkC9XGkuZng8YBw8qyu5uh4128fQRjlGgvEiRLx-0XP4KYMwcgdZw",
        "name": "Jane Doe",
        "aadObjectId": "df486eae-88fd-42a5-b45e-c581588186db"
    },
    "conversation": {
        "conversationType": "personal",
        "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "id": "a:1oAmWTVBBe9E0JrpGxauqNyx4CCE_iQf2ZuWon9D42722Fon3wYIpbhgbRChE3wgVS1Gwl9zS1pZy4FSu6-x1vGEq5KBQK-EbBgyPyeP_C-lbLBY3vxnGk9m9D_282jbg"
    },
    "recipient": {
        "id": "28:5baea8d1-d4ea-43a1-b101-882f4c8d9cb4",
        "name": "Imported Bot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Windows",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

---

> [!NOTE]
> <span data-ttu-id="e25b6-141">在同一活动有效负载中发送短信和附件时，将发生邮件拆分。</span><span class="sxs-lookup"><span data-stu-id="e25b6-141">Message splitting occurs when a text message and an attachment are sent in the same activity payload.</span></span> <span data-ttu-id="e25b6-142">Microsoft Teams 将此活动拆分为单独的活动，一个活动仅包含一条短信，另一个包含附件。</span><span class="sxs-lookup"><span data-stu-id="e25b6-142">This activity is split into separate activities by Microsoft Teams, one activity with just a text message and the other with an attachment.</span></span> <span data-ttu-id="e25b6-143">拆分活动时，您不会收到响应消息 ID，该 ID 用于主动更新或删除[](~/bots/how-to/update-and-delete-bot-messages.md)邮件。</span><span class="sxs-lookup"><span data-stu-id="e25b6-143">As the activity is split, you do not receive the message ID in response, which is used to [update or delete](~/bots/how-to/update-and-delete-bot-messages.md) the message proactively.</span></span> <span data-ttu-id="e25b6-144">建议发送单独的活动，而不是根据邮件拆分。</span><span class="sxs-lookup"><span data-stu-id="e25b6-144">It is recommended to send separate activities instead of depending on message splitting.</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="e25b6-145">Teams 频道数据</span><span class="sxs-lookup"><span data-stu-id="e25b6-145">Teams channel data</span></span>

<span data-ttu-id="e25b6-146">该对象 `channelData` 包含特定于 Teams 的信息，是团队和频道的一个明确来源。</span><span class="sxs-lookup"><span data-stu-id="e25b6-146">The `channelData` object contains Teams-specific information and is a definitive source for team and channel IDs.</span></span> <span data-ttu-id="e25b6-147">您可能需要缓存这些 ID 并用作本地存储的密钥。</span><span class="sxs-lookup"><span data-stu-id="e25b6-147">You may need to cache and use these IDs as keys for local storage.</span></span> <span data-ttu-id="e25b6-148">SDK 中通常从对象提取重要信息 `TeamsActivityHandler` `channelData` ，使其易于访问。</span><span class="sxs-lookup"><span data-stu-id="e25b6-148">The `TeamsActivityHandler` in the SDK, typically pulls out important information from the `channelData` object to make it easily accessible.</span></span> <span data-ttu-id="e25b6-149">但是，您始终可以从对象访问 `turnContext` 原始数据。</span><span class="sxs-lookup"><span data-stu-id="e25b6-149">However, you can always access the original data from the `turnContext` object.</span></span>

<span data-ttu-id="e25b6-150">`channelData`对象不包含在个人对话中的邮件中，因为邮件发生在任何频道之外。</span><span class="sxs-lookup"><span data-stu-id="e25b6-150">The `channelData` object is not included in messages in personal conversations, as these take place outside of any channel.</span></span>

<span data-ttu-id="e25b6-151">发送给自动程序的活动中的典型 channelData 对象包含以下信息：</span><span class="sxs-lookup"><span data-stu-id="e25b6-151">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="e25b6-152">`eventType` Teams 事件类型;仅在通道修改 [事件的情况下传递](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="e25b6-152">`eventType` Teams event type; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="e25b6-153">`tenant.id` 在所有上下文中传递的 Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="e25b6-153">`tenant.id` Azure Active Directory tenant ID, passed in all contexts.</span></span>
* <span data-ttu-id="e25b6-154">`team` 仅在频道上下文中传递，而不是在个人聊天中传递。</span><span class="sxs-lookup"><span data-stu-id="e25b6-154">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="e25b6-155">`id` 通道的 GUID。</span><span class="sxs-lookup"><span data-stu-id="e25b6-155">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="e25b6-156">`name` 团队名称;仅在团队重命名 [事件的情况下传递](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="e25b6-156">`name` Name of the team; passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="e25b6-157">`channel` 仅在提及自动程序时在频道上下文中传递，或针对已添加自动程序的团队中的频道中的事件传递。</span><span class="sxs-lookup"><span data-stu-id="e25b6-157">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="e25b6-158">`id` 通道的 GUID。</span><span class="sxs-lookup"><span data-stu-id="e25b6-158">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="e25b6-159">`name` 频道名称;仅在通道修改 [事件的情况下传递](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="e25b6-159">`name` Channel name; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="e25b6-160">`channelData.teamsTeamId` 已弃用。</span><span class="sxs-lookup"><span data-stu-id="e25b6-160">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="e25b6-161">此属性仅包含用于向后兼容性。</span><span class="sxs-lookup"><span data-stu-id="e25b6-161">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="e25b6-162">`channelData.teamsChannelId` 已弃用。</span><span class="sxs-lookup"><span data-stu-id="e25b6-162">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="e25b6-163">此属性仅包含用于向后兼容性。</span><span class="sxs-lookup"><span data-stu-id="e25b6-163">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="e25b6-164">channelCreated 事件 (的 channelData 对象) </span><span class="sxs-lookup"><span data-stu-id="e25b6-164">Example channelData object (channelCreated event)</span></span>

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

## <a name="message-content"></a><span data-ttu-id="e25b6-165">邮件内容</span><span class="sxs-lookup"><span data-stu-id="e25b6-165">Message content</span></span>

<span data-ttu-id="e25b6-166">机器人可以发送格式文本、图片和卡片。</span><span class="sxs-lookup"><span data-stu-id="e25b6-166">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="e25b6-167">用户可以向自动程序发送格式文本和图片。</span><span class="sxs-lookup"><span data-stu-id="e25b6-167">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="e25b6-168">Format</span><span class="sxs-lookup"><span data-stu-id="e25b6-168">Format</span></span>    | <span data-ttu-id="e25b6-169">从用户到机器人</span><span class="sxs-lookup"><span data-stu-id="e25b6-169">From user to bot</span></span> | <span data-ttu-id="e25b6-170">从自动程序到用户</span><span class="sxs-lookup"><span data-stu-id="e25b6-170">From bot to user</span></span> | <span data-ttu-id="e25b6-171">注释</span><span class="sxs-lookup"><span data-stu-id="e25b6-171">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="e25b6-172">格式文本 </span><span class="sxs-lookup"><span data-stu-id="e25b6-172">Rich text</span></span> | <span data-ttu-id="e25b6-173">✔</span><span class="sxs-lookup"><span data-stu-id="e25b6-173">✔</span></span>                | <span data-ttu-id="e25b6-174">✔</span><span class="sxs-lookup"><span data-stu-id="e25b6-174">✔</span></span>                |                                                                                         |
| <span data-ttu-id="e25b6-175">图片</span><span class="sxs-lookup"><span data-stu-id="e25b6-175">Pictures</span></span>  | <span data-ttu-id="e25b6-176">✔</span><span class="sxs-lookup"><span data-stu-id="e25b6-176">✔</span></span>                | <span data-ttu-id="e25b6-177">✔</span><span class="sxs-lookup"><span data-stu-id="e25b6-177">✔</span></span>                | <span data-ttu-id="e25b6-178">PNG、JPEG 或 GIF 格式的最大大小为 1024×1024 和 1 MB;不支持动态 GIF</span><span class="sxs-lookup"><span data-stu-id="e25b6-178">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span>  |
| <span data-ttu-id="e25b6-179">卡</span><span class="sxs-lookup"><span data-stu-id="e25b6-179">Cards</span></span>     | <span data-ttu-id="e25b6-180">✖</span><span class="sxs-lookup"><span data-stu-id="e25b6-180">✖</span></span>                | <span data-ttu-id="e25b6-181">✔</span><span class="sxs-lookup"><span data-stu-id="e25b6-181">✔</span></span>                | <span data-ttu-id="e25b6-182">有关受支持的 [卡片，](~/task-modules-and-cards/cards/cards-reference.md) 请参阅 Teams 卡片参考</span><span class="sxs-lookup"><span data-stu-id="e25b6-182">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="e25b6-183">表情符号</span><span class="sxs-lookup"><span data-stu-id="e25b6-183">Emojis</span></span>    | <span data-ttu-id="e25b6-184">✖</span><span class="sxs-lookup"><span data-stu-id="e25b6-184">✖</span></span>                | <span data-ttu-id="e25b6-185">✔</span><span class="sxs-lookup"><span data-stu-id="e25b6-185">✔</span></span>                | <span data-ttu-id="e25b6-186">Teams 当前支持通过 UTF-16 (表情符号，例如 U+1F600，用于面部) </span><span class="sxs-lookup"><span data-stu-id="e25b6-186">Teams currently supports emojis through UTF-16 (such as U+1F600 for grinning face)</span></span>          |

## <a name="adding-notifications-to-your-message"></a><span data-ttu-id="e25b6-187">向邮件添加通知</span><span class="sxs-lookup"><span data-stu-id="e25b6-187">Adding notifications to your message</span></span>

<span data-ttu-id="e25b6-188">通知会提醒用户与正在处理或需要查看的任务相关的新任务、提及和注释，只需在活动源中插入通知。</span><span class="sxs-lookup"><span data-stu-id="e25b6-188">Notifications alert users about new tasks, mentions, and comments related to what they are working on or need to look at by inserting a notice into their activity feed.</span></span> <span data-ttu-id="e25b6-189">可以通过将 objects 属性设置为 true，将通知设置为从自动 `TeamsChannelData` 程序 `Notification.Alert` 消息触发。</span><span class="sxs-lookup"><span data-stu-id="e25b6-189">You can set notifications to trigger from your bot-message by setting the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="e25b6-190">是否引发通知最终取决于单个用户的 Teams 设置，你无法以编程方式覆盖这些设置。</span><span class="sxs-lookup"><span data-stu-id="e25b6-190">Whether or not a notification is raised ultimately depends on the individual user's Teams settings and you cannot programmatically override these settings.</span></span> <span data-ttu-id="e25b6-191">通知类型为横幅或横幅和电子邮件。</span><span class="sxs-lookup"><span data-stu-id="e25b6-191">The type of notification is either a banner or both a banner and an email.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e25b6-192">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e25b6-192">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e25b6-193">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e25b6-193">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="e25b6-194">Python</span><span class="sxs-lookup"><span data-stu-id="e25b6-194">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="e25b6-195">JSON</span><span class="sxs-lookup"><span data-stu-id="e25b6-195">JSON</span></span>](#tab/json)

```json
{
  "type": "message",
  "timestamp": "2017-04-24T21:46:00.9663655Z",
  "localTimestamp": "2017-04-24T14:46:00.9663655-07:00",
  "serviceUrl": "https://callback.com",
  "channelId": "msteams",
  "from": {
    "id": "28:e4fda94a-4b80-40eb-9bf0-6314491bc793",
    "name": "The bot"
  },
  "conversation": {
    "id": "a:1pL6i0oY3C0K8oAj8"
  },
  "recipient": {
    "id": "29:1rsVJmSSFMScF0YFyCXpvNWlo",
    "name": "User"
  },
  "text": "John Phillips assigned you a weekly todo",
  "summary": "Don't forget to meet with Marketing next week",
  "channelData": {
    "notification": {
      "alert": true
    }
  },
  "replyToId": "1493070356924"
}
```

---

## <a name="picture-messages"></a><span data-ttu-id="e25b6-196">图片消息</span><span class="sxs-lookup"><span data-stu-id="e25b6-196">Picture messages</span></span>

<span data-ttu-id="e25b6-197">图片通过向邮件添加附件来发送。</span><span class="sxs-lookup"><span data-stu-id="e25b6-197">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="e25b6-198">您可以在 Bot Framework 文档中找到有关 [附件详细信息](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)。</span><span class="sxs-lookup"><span data-stu-id="e25b6-198">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).</span></span>

<span data-ttu-id="e25b6-199">图片最多为 1024×1024 和 1 MB（采用 PNG、JPEG 或 GIF 格式）。</span><span class="sxs-lookup"><span data-stu-id="e25b6-199">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="e25b6-200">不支持动态 GIF。</span><span class="sxs-lookup"><span data-stu-id="e25b6-200">Animated GIF is not supported.</span></span>

<span data-ttu-id="e25b6-201">始终使用 XML 指定每个图像的高度和宽度。</span><span class="sxs-lookup"><span data-stu-id="e25b6-201">Always specify the height and width of each image by using XML.</span></span> <span data-ttu-id="e25b6-202">在 Markdown 中，图像大小默认为 256×256。</span><span class="sxs-lookup"><span data-stu-id="e25b6-202">In Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="e25b6-203">例如：</span><span class="sxs-lookup"><span data-stu-id="e25b6-203">For example:</span></span>

* <span data-ttu-id="e25b6-204">使用 - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="e25b6-204">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="e25b6-205">请勿使用 - `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="e25b6-205">Don't use - `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="e25b6-206">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="e25b6-206">Adaptive cards</span></span>

<span data-ttu-id="e25b6-207">使用以下代码发送简单的自适应卡片：</span><span class="sxs-lookup"><span data-stu-id="e25b6-207">Use the following code to send a simple adaptive card:</span></span>

```json
{
    "type": "AdaptiveCard",
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.5",
    "body": [
    {
        "items": [
        {
            "size": "large",
            "text": " Simple Adaptivecard Example with a Textbox",
            "type": "TextBlock",
            "weight": "bolder",
            "wrap": true
        },
        ],
        "spacing": "extraLarge",
        "type": "Container",
        "verticalContentAlignment": "center"
    }
    ]
}
```

<span data-ttu-id="e25b6-208">若要了解有关机器人中的卡和卡的更多信息，请参阅 [卡片文档](~/task-modules-and-cards/what-are-cards.md)。</span><span class="sxs-lookup"><span data-stu-id="e25b6-208">To know more about cards and cards in bots, see [cards documentation](~/task-modules-and-cards/what-are-cards.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="e25b6-209">代码示例</span><span class="sxs-lookup"><span data-stu-id="e25b6-209">Code sample</span></span>

|<span data-ttu-id="e25b6-210">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="e25b6-210">**Sample name**</span></span> | <span data-ttu-id="e25b6-211">**说明**</span><span class="sxs-lookup"><span data-stu-id="e25b6-211">**Description**</span></span> | <span data-ttu-id="e25b6-212">**.NETCore**</span><span class="sxs-lookup"><span data-stu-id="e25b6-212">**.NETCore**</span></span> | <span data-ttu-id="e25b6-213">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="e25b6-213">**JavaScript**</span></span> | <span data-ttu-id="e25b6-214">**Python**</span><span class="sxs-lookup"><span data-stu-id="e25b6-214">**Python**</span></span>|
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="e25b6-215">Teams 对话机器人</span><span class="sxs-lookup"><span data-stu-id="e25b6-215">Teams Conversation Bot</span></span> | <span data-ttu-id="e25b6-216">消息和对话事件处理。</span><span class="sxs-lookup"><span data-stu-id="e25b6-216">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="e25b6-217">View</span><span class="sxs-lookup"><span data-stu-id="e25b6-217">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="e25b6-218">View</span><span class="sxs-lookup"><span data-stu-id="e25b6-218">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="e25b6-219">View</span><span class="sxs-lookup"><span data-stu-id="e25b6-219">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-steps"></a><span data-ttu-id="e25b6-220">后续步骤</span><span class="sxs-lookup"><span data-stu-id="e25b6-220">Next steps</span></span>

* [<span data-ttu-id="e25b6-221">发送主动邮件</span><span class="sxs-lookup"><span data-stu-id="e25b6-221">Sending proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
* [<span data-ttu-id="e25b6-222">订阅对话事件</span><span class="sxs-lookup"><span data-stu-id="e25b6-222">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
