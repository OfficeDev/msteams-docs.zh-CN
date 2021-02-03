---
title: 对话基础知识
author: clearab
description: 如何与 Microsoft Teams 机器人对话
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 6f7e7a4d1be08126c96dff07ddbc3e1156700a90
ms.sourcegitcommit: 94ad961ecd002805b4e0424601d1c0ec191ff376
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2021
ms.locfileid: "50075691"
---
# <a name="conversation-basics"></a><span data-ttu-id="42c51-103">对话基础知识</span><span class="sxs-lookup"><span data-stu-id="42c51-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="42c51-104">对话是在机器人与一个或多个用户之间发送的一系列消息。</span><span class="sxs-lookup"><span data-stu-id="42c51-104">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="42c51-105">有三种类型的对话 (Teams 中称为) 范围：</span><span class="sxs-lookup"><span data-stu-id="42c51-105">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="42c51-106">`teams` 也称为频道对话，对频道的所有成员可见。</span><span class="sxs-lookup"><span data-stu-id="42c51-106">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="42c51-107">`personal` 机器人与单个用户之间的对话。</span><span class="sxs-lookup"><span data-stu-id="42c51-107">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="42c51-108">`groupChat` 机器人与两个或多个用户之间的聊天。</span><span class="sxs-lookup"><span data-stu-id="42c51-108">`groupChat` Chat between a bot and two or more users.</span></span> <span data-ttu-id="42c51-109">此外，还可以在会议聊天中启用机器人。</span><span class="sxs-lookup"><span data-stu-id="42c51-109">Also enables your bot in meeting chats.</span></span>

<span data-ttu-id="42c51-110">自动程序的行为略有不同，具体取决于它涉及的对话类型：</span><span class="sxs-lookup"><span data-stu-id="42c51-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="42c51-111">频道和群聊对话中的聊天机器人要求用户 @ 提及机器人，以在频道中调用它。</span><span class="sxs-lookup"><span data-stu-id="42c51-111">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="42c51-112">一对一对话中的机器人不需要 @ 提及。</span><span class="sxs-lookup"><span data-stu-id="42c51-112">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="42c51-113">用户发送的所有邮件都将路由到自动程序。</span><span class="sxs-lookup"><span data-stu-id="42c51-113">All messages sent by the user will be routed to your bot.</span></span>

<span data-ttu-id="42c51-114">若要启用特定作用域中的自动程序，请将此范围添加到[应用清单。](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="42c51-114">To enable your bot in a particular scope, add that scope to your [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="activities"></a><span data-ttu-id="42c51-115">活动</span><span class="sxs-lookup"><span data-stu-id="42c51-115">Activities</span></span>

<span data-ttu-id="42c51-116">每封邮件都是 `Activity` 一个类型对象 `messageType: message` 。</span><span class="sxs-lookup"><span data-stu-id="42c51-116">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="42c51-117">当用户发送消息时，Teams 会向自动程序发布消息;具体来说，它会将 JSON 对象发送到机器人的消息终结点。</span><span class="sxs-lookup"><span data-stu-id="42c51-117">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="42c51-118">机器人会检查消息以确定其类型并相应地做出响应。</span><span class="sxs-lookup"><span data-stu-id="42c51-118">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="42c51-119">基本对话通过 Bot Framework 连接器（一个 REST API）进行处理，使机器人能够与 Teams 和其他频道进行通信。</span><span class="sxs-lookup"><span data-stu-id="42c51-119">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="42c51-120">Bot Builder SDK 提供对此 API 的轻松访问、用于管理对话流和状态的其他功能，以及合并认知服务（如自然语言处理 (NLP) ）。</span><span class="sxs-lookup"><span data-stu-id="42c51-120">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="42c51-121">接收邮件</span><span class="sxs-lookup"><span data-stu-id="42c51-121">Receive a message</span></span>

<span data-ttu-id="42c51-122">若要接收短信，请使用 `Text` 对象 `Activity` 的属性。</span><span class="sxs-lookup"><span data-stu-id="42c51-122">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="42c51-123">在机器人的活动处理程序中，使用 turn context 对象读取 `Activity` 单个消息请求。</span><span class="sxs-lookup"><span data-stu-id="42c51-123">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="42c51-124">下面的代码显示了一个示例。</span><span class="sxs-lookup"><span data-stu-id="42c51-124">The code below shows an example.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="42c51-125">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="42c51-125">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="42c51-126">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="42c51-126">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="42c51-127">Python</span><span class="sxs-lookup"><span data-stu-id="42c51-127">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="42c51-128">JSON</span><span class="sxs-lookup"><span data-stu-id="42c51-128">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="42c51-129">发送邮件</span><span class="sxs-lookup"><span data-stu-id="42c51-129">Send a message</span></span>

<span data-ttu-id="42c51-130">若要发送短信，请指定要作为活动发送的字符串。</span><span class="sxs-lookup"><span data-stu-id="42c51-130">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="42c51-131">在机器人的活动处理程序中，使用 turn context 对象的方法发送 `SendActivityAsync` 单个消息响应。</span><span class="sxs-lookup"><span data-stu-id="42c51-131">In the bot's activity handlers, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="42c51-132">您还可以使用对象的方法 `SendActivitiesAsync` 一次发送多个响应。</span><span class="sxs-lookup"><span data-stu-id="42c51-132">You can also use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="42c51-133">下面的代码显示了将某人添加到对话时发送邮件的示例</span><span class="sxs-lookup"><span data-stu-id="42c51-133">The code below shows an example of sending a message when someone is added to a conversation</span></span>  

# <a name="cnet"></a>[<span data-ttu-id="42c51-134">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="42c51-134">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="42c51-135">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="42c51-135">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="42c51-136">Python</span><span class="sxs-lookup"><span data-stu-id="42c51-136">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="42c51-137">JSON</span><span class="sxs-lookup"><span data-stu-id="42c51-137">JSON</span></span>](#tab/json)

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

## <a name="teams-channel-data"></a><span data-ttu-id="42c51-138">Teams 频道数据</span><span class="sxs-lookup"><span data-stu-id="42c51-138">Teams channel data</span></span>

<span data-ttu-id="42c51-139">该对象 `channelData` 包含特定于 Teams 的信息，是团队和频道 ID 的最终来源。</span><span class="sxs-lookup"><span data-stu-id="42c51-139">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="42c51-140">您可能需要缓存这些 ID，并使用这些 ID 作为本地存储的密钥。</span><span class="sxs-lookup"><span data-stu-id="42c51-140">You may need to cache and use these ids as keys for local storage.</span></span> <span data-ttu-id="42c51-141">SDK 中的内容通常会从对象中拉出重要信息，使其更易于访问，但始终可以从对象访问 `TeamsActivityHandler` `channelData` 原始 `turnContext` 信息。</span><span class="sxs-lookup"><span data-stu-id="42c51-141">The `TeamsActivityHandler` in the SDK will typically pull out important information from the `channelData` object to make it more easily accessible, however you can always access the original information from the `turnContext` object.</span></span>

<span data-ttu-id="42c51-142">对象 `channelData` 不包含在个人对话中的邮件中，因为这些事件发生在任何频道之外。</span><span class="sxs-lookup"><span data-stu-id="42c51-142">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="42c51-143">发送给自动程序的活动中的典型 channelData 对象包含以下信息：</span><span class="sxs-lookup"><span data-stu-id="42c51-143">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="42c51-144">`eventType` Teams 事件类型;仅在通道修改 [事件的情况下传递](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="42c51-144">`eventType` Teams event type; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="42c51-145">`tenant.id` Azure Active Directory 租户 ID;在所有上下文中传递</span><span class="sxs-lookup"><span data-stu-id="42c51-145">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="42c51-146">`team` 仅在频道上下文中传递，而不是在个人聊天中传递。</span><span class="sxs-lookup"><span data-stu-id="42c51-146">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="42c51-147">`id` 频道的 GUID</span><span class="sxs-lookup"><span data-stu-id="42c51-147">`id` GUID for the channel</span></span>
  * <span data-ttu-id="42c51-148">`name` 团队名称;仅在团队重命名 [事件的情况下传递](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="42c51-148">`name` Name of the team; passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="42c51-149">`channel` 仅在提及自动程序时或在团队中添加了自动程序的团队中的频道中为事件传递</span><span class="sxs-lookup"><span data-stu-id="42c51-149">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="42c51-150">`id` 频道的 GUID</span><span class="sxs-lookup"><span data-stu-id="42c51-150">`id` GUID for the channel</span></span>
  * <span data-ttu-id="42c51-151">`name` 频道名称;仅在通道修改 [事件的情况下传递](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="42c51-151">`name` Channel name; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="42c51-152">`channelData.teamsTeamId` 已弃用。</span><span class="sxs-lookup"><span data-stu-id="42c51-152">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="42c51-153">包含此属性仅仅是为了向后兼容。</span><span class="sxs-lookup"><span data-stu-id="42c51-153">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="42c51-154">`channelData.teamsChannelId` 已弃用。</span><span class="sxs-lookup"><span data-stu-id="42c51-154">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="42c51-155">包含此属性仅仅是为了向后兼容。</span><span class="sxs-lookup"><span data-stu-id="42c51-155">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="42c51-156">channelCreated 事件 (的 channelData 对象) </span><span class="sxs-lookup"><span data-stu-id="42c51-156">Example channelData object (channelCreated event)</span></span>

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

## <a name="message-content"></a><span data-ttu-id="42c51-157">邮件内容</span><span class="sxs-lookup"><span data-stu-id="42c51-157">Message content</span></span>

<span data-ttu-id="42c51-158">机器人可以发送格式文本、图片和卡片。</span><span class="sxs-lookup"><span data-stu-id="42c51-158">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="42c51-159">用户可以将格式文本和图片发送到机器人。</span><span class="sxs-lookup"><span data-stu-id="42c51-159">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="42c51-160">Format</span><span class="sxs-lookup"><span data-stu-id="42c51-160">Format</span></span>    | <span data-ttu-id="42c51-161">从用户到机器人</span><span class="sxs-lookup"><span data-stu-id="42c51-161">From user to bot</span></span> | <span data-ttu-id="42c51-162">从自动程序到用户</span><span class="sxs-lookup"><span data-stu-id="42c51-162">From bot to user</span></span> | <span data-ttu-id="42c51-163">注释</span><span class="sxs-lookup"><span data-stu-id="42c51-163">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="42c51-164">格式文本 </span><span class="sxs-lookup"><span data-stu-id="42c51-164">Rich text</span></span> | <span data-ttu-id="42c51-165">✔</span><span class="sxs-lookup"><span data-stu-id="42c51-165">✔</span></span>                | <span data-ttu-id="42c51-166">✔</span><span class="sxs-lookup"><span data-stu-id="42c51-166">✔</span></span>                |                                                                                         |
| <span data-ttu-id="42c51-167">图片</span><span class="sxs-lookup"><span data-stu-id="42c51-167">Pictures</span></span>  | <span data-ttu-id="42c51-168">✔</span><span class="sxs-lookup"><span data-stu-id="42c51-168">✔</span></span>                | <span data-ttu-id="42c51-169">✔</span><span class="sxs-lookup"><span data-stu-id="42c51-169">✔</span></span>                | <span data-ttu-id="42c51-170">PNG、JPEG 或 GIF 格式的最大大小为 1024×1024 和 1 MB;不支持动态 GIF</span><span class="sxs-lookup"><span data-stu-id="42c51-170">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span>  |
| <span data-ttu-id="42c51-171">卡</span><span class="sxs-lookup"><span data-stu-id="42c51-171">Cards</span></span>     | <span data-ttu-id="42c51-172">✖</span><span class="sxs-lookup"><span data-stu-id="42c51-172">✖</span></span>                | <span data-ttu-id="42c51-173">✔</span><span class="sxs-lookup"><span data-stu-id="42c51-173">✔</span></span>                | <span data-ttu-id="42c51-174">有关受支持的 [卡，](~/task-modules-and-cards/cards/cards-reference.md) 请参阅 Teams 卡参考</span><span class="sxs-lookup"><span data-stu-id="42c51-174">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="42c51-175">表情符号</span><span class="sxs-lookup"><span data-stu-id="42c51-175">Emojis</span></span>    | <span data-ttu-id="42c51-176">✖</span><span class="sxs-lookup"><span data-stu-id="42c51-176">✖</span></span>                | <span data-ttu-id="42c51-177">✔</span><span class="sxs-lookup"><span data-stu-id="42c51-177">✔</span></span>                | <span data-ttu-id="42c51-178">Teams 当前支持通过 UTF-16 (表情符号，例如 U+1F600，用于面部) </span><span class="sxs-lookup"><span data-stu-id="42c51-178">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span>          |

## <a name="adding-notifications-to-your-message"></a><span data-ttu-id="42c51-179">向邮件添加通知</span><span class="sxs-lookup"><span data-stu-id="42c51-179">Adding notifications to your message</span></span>

<span data-ttu-id="42c51-180">通知会提醒用户有关他们正在处理的新任务、提及和注释，或者需要通过向活动源中插入通知来查看。</span><span class="sxs-lookup"><span data-stu-id="42c51-180">Notifications alert users about new tasks, mentions and comments related to what they are working on, or need to look at by inserting a notice into their Activity Feed.</span></span> <span data-ttu-id="42c51-181">可以通过将 objects 属性设置为 true，将通知设置为从自动 `TeamsChannelData` 程序 `Notification.Alert` 消息中触发。</span><span class="sxs-lookup"><span data-stu-id="42c51-181">You can set notifications to trigger from your bot message by setting the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="42c51-182">是否引发通知最终将取决于单个用户的 Teams 设置，并且你无法以编程方式覆盖这些设置。</span><span class="sxs-lookup"><span data-stu-id="42c51-182">Whether or not a notification is raised will ultimately depend on the individual user's Teams settings and you cannot programmatically override these settings.</span></span> <span data-ttu-id="42c51-183">通知类型将为横幅或横幅和电子邮件。</span><span class="sxs-lookup"><span data-stu-id="42c51-183">The type of notification will be either a banner or both a banner and an email.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="42c51-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="42c51-184">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="42c51-185">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="42c51-185">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="42c51-186">Python</span><span class="sxs-lookup"><span data-stu-id="42c51-186">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="42c51-187">JSON</span><span class="sxs-lookup"><span data-stu-id="42c51-187">JSON</span></span>](#tab/json)

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

## <a name="picture-messages"></a><span data-ttu-id="42c51-188">图片消息</span><span class="sxs-lookup"><span data-stu-id="42c51-188">Picture messages</span></span>

<span data-ttu-id="42c51-189">图片通过向邮件添加附件来发送。</span><span class="sxs-lookup"><span data-stu-id="42c51-189">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="42c51-190">您可以在 Bot Framework 文档中找到有关 [附件的更多信息](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="42c51-190">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).</span></span>

<span data-ttu-id="42c51-191">图片最多为 1024×1024 和 1 MB（采用 PNG、JPEG 或 GIF 格式）;不支持动态 GIF。</span><span class="sxs-lookup"><span data-stu-id="42c51-191">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="42c51-192">建议您使用 XML 指定每个图像的高度和宽度。</span><span class="sxs-lookup"><span data-stu-id="42c51-192">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="42c51-193">如果使用 Markdown，图像大小默认为 256×256。</span><span class="sxs-lookup"><span data-stu-id="42c51-193">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="42c51-194">例如：</span><span class="sxs-lookup"><span data-stu-id="42c51-194">For example:</span></span>

* <span data-ttu-id="42c51-195">使用 - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="42c51-195">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="42c51-196">请勿使用 - `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="42c51-196">Don't use - `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="code-sample"></a><span data-ttu-id="42c51-197">代码示例</span><span class="sxs-lookup"><span data-stu-id="42c51-197">Code sample</span></span>
|<span data-ttu-id="42c51-198">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="42c51-198">**Sample name**</span></span> | <span data-ttu-id="42c51-199">**说明**</span><span class="sxs-lookup"><span data-stu-id="42c51-199">**Description**</span></span> | <span data-ttu-id="42c51-200">**.NETCore**</span><span class="sxs-lookup"><span data-stu-id="42c51-200">**.NETCore**</span></span> | <span data-ttu-id="42c51-201">**Javascript**</span><span class="sxs-lookup"><span data-stu-id="42c51-201">**Javascript**</span></span> | <span data-ttu-id="42c51-202">**Python**</span><span class="sxs-lookup"><span data-stu-id="42c51-202">**Python**</span></span>|
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="42c51-203">Teams 对话机器人</span><span class="sxs-lookup"><span data-stu-id="42c51-203">Teams Conversation Bot</span></span> | <span data-ttu-id="42c51-204">消息和对话事件处理。</span><span class="sxs-lookup"><span data-stu-id="42c51-204">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="42c51-205">View</span><span class="sxs-lookup"><span data-stu-id="42c51-205">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="42c51-206">View</span><span class="sxs-lookup"><span data-stu-id="42c51-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="42c51-207">View</span><span class="sxs-lookup"><span data-stu-id="42c51-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-steps"></a><span data-ttu-id="42c51-208">后续步骤</span><span class="sxs-lookup"><span data-stu-id="42c51-208">Next steps</span></span>

* [<span data-ttu-id="42c51-209">发送主动邮件</span><span class="sxs-lookup"><span data-stu-id="42c51-209">Sending proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
* [<span data-ttu-id="42c51-210">订阅对话事件</span><span class="sxs-lookup"><span data-stu-id="42c51-210">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
