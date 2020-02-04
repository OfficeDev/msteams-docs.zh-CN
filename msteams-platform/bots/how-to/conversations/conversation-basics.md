---
title: 对话基础知识
author: clearab
description: 如何与 Microsoft 团队 bot 进行对话
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2d241ad04509c596e97647138bab2a749fa0f74c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673139"
---
# <a name="conversation-basics"></a><span data-ttu-id="9dc7a-103">对话基础知识</span><span class="sxs-lookup"><span data-stu-id="9dc7a-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="9dc7a-104">对话是在你的 bot 和一个或多个用户之间发送的一系列邮件。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-104">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="9dc7a-105">团队中有三种对话（也称为 "作用域"）：</span><span class="sxs-lookup"><span data-stu-id="9dc7a-105">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="9dc7a-106">`teams`也称为频道对话，对频道的所有成员可见。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-106">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="9dc7a-107">`personal`Bot 和单个用户之间的对话。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-107">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="9dc7a-108">`groupChat`在 bot 和两个或更多用户之间聊天。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-108">`groupChat` Chat between a bot and two or more users.</span></span> <span data-ttu-id="9dc7a-109">此外，还可以在会议聊天中启用你的 bot。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-109">Also enables your bot in meeting chats.</span></span>

<span data-ttu-id="9dc7a-110">Bot 的行为略有不同，具体取决于它涉及的对话类型：</span><span class="sxs-lookup"><span data-stu-id="9dc7a-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="9dc7a-111">频道和分组聊天对话中的 bot 要求用户在频道中提及机器人以调用它。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-111">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="9dc7a-112">一对一对话中的 bot 不需要 @ 提及。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-112">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="9dc7a-113">用户发送的所有邮件都将被路由到你的 bot。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-113">All messages sent by the user will be routed to your bot.</span></span>

<span data-ttu-id="9dc7a-114">若要在特定范围内启用你的 bot，请将该作用域添加到你的[应用程序清单](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-114">To enable your bot in a particular scope, add that scope to your [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="activities"></a><span data-ttu-id="9dc7a-115">活动</span><span class="sxs-lookup"><span data-stu-id="9dc7a-115">Activities</span></span>

<span data-ttu-id="9dc7a-116">每封邮件都`Activity`是一种`messageType: message`类型的对象。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-116">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="9dc7a-117">当用户发送邮件时，工作组会将邮件发送到你的 bot。具体来说，它会将 JSON 对象发送到你的 bot 的邮件终结点。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-117">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="9dc7a-118">你的 bot 将检查邮件以确定其类型并相应地做出响应。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-118">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="9dc7a-119">基本对话通过 Bot 框架连接器（单个 REST API）处理，使你的 bot 能够与团队和其他频道进行通信。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-119">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="9dc7a-120">机器人生成器 SDK 提供了轻松访问此 API 的功能、用于管理对话流和状态的附加功能，以及用于集成认知服务（如自然语言处理（NLP））的简单方法。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-120">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="9dc7a-121">接收邮件</span><span class="sxs-lookup"><span data-stu-id="9dc7a-121">Receive a message</span></span>

<span data-ttu-id="9dc7a-122">若要接收短信，请使用`Text` `Activity`对象的属性。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-122">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="9dc7a-123">在 bot 的活动处理程序中，使用 turn context 对象`Activity`读取单个邮件请求。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-123">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="9dc7a-124">下面的代码显示了一个示例。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-124">The code below shows an example.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="9dc7a-125">C #/.NET</span><span class="sxs-lookup"><span data-stu-id="9dc7a-125">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="9dc7a-126">TypeScript/node.js</span><span class="sxs-lookup"><span data-stu-id="9dc7a-126">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="pythontabpython"></a>[<span data-ttu-id="9dc7a-127">Python</span><span class="sxs-lookup"><span data-stu-id="9dc7a-127">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="jsontabjson"></a>[<span data-ttu-id="9dc7a-128">JSON</span><span class="sxs-lookup"><span data-stu-id="9dc7a-128">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="9dc7a-129">发送邮件</span><span class="sxs-lookup"><span data-stu-id="9dc7a-129">Send a message</span></span>

<span data-ttu-id="9dc7a-130">若要发送短信，请指定要作为活动发送的字符串。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-130">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="9dc7a-131">在 bot 的活动处理程序中，使用 turn context 对象的`SendActivityAsync`方法发送单个邮件响应。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-131">In the bot's activity handlers, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="9dc7a-132">您还可以使用对象的`SendActivitiesAsync`方法一次发送多个响应。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-132">You can also use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="9dc7a-133">下面的代码展示了在将某人添加到对话中时发送邮件的示例</span><span class="sxs-lookup"><span data-stu-id="9dc7a-133">The code below shows an example of sending a message when someone is added to a conversation</span></span>  

# <a name="cnettabdotnet"></a>[<span data-ttu-id="9dc7a-134">C #/.NET</span><span class="sxs-lookup"><span data-stu-id="9dc7a-134">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="9dc7a-135">TypeScript/node.js</span><span class="sxs-lookup"><span data-stu-id="9dc7a-135">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="pythontabpython"></a>[<span data-ttu-id="9dc7a-136">Python</span><span class="sxs-lookup"><span data-stu-id="9dc7a-136">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="jsontabjson"></a>[<span data-ttu-id="9dc7a-137">JSON</span><span class="sxs-lookup"><span data-stu-id="9dc7a-137">JSON</span></span>](#tab/json)

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

## <a name="teams-channel-data"></a><span data-ttu-id="9dc7a-138">团队频道数据</span><span class="sxs-lookup"><span data-stu-id="9dc7a-138">Teams channel data</span></span>

<span data-ttu-id="9dc7a-139">该`channelData`对象包含特定于团队的信息，是团队和通道 id 的权威源。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-139">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="9dc7a-140">您可能需要缓存这些 id 并将其用作本地存储的键。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-140">You may need to cache and use these ids as keys for local storage.</span></span> <span data-ttu-id="9dc7a-141">SDK `TeamsActivityHandler`中的通常会从`channelData`对象中提取重要信息，以使其更易于访问，但您始终可以访问`turnContext`对象中的原始信息。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-141">The `TeamsActivityHandler` in the SDK will typically pull out important information from the `channelData` object to make it more easily accessible, however you can always access the original information from the `turnContext` object.</span></span>

<span data-ttu-id="9dc7a-142">在`channelData`个人对话的邮件中不包含该对象，因为它们在任何频道之外发生。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-142">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="9dc7a-143">发送到你的 bot 的活动中的典型 channelData 对象包含以下信息：</span><span class="sxs-lookup"><span data-stu-id="9dc7a-143">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="9dc7a-144">`eventType`团队事件类型;仅在[频道修改事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)的情况下传递</span><span class="sxs-lookup"><span data-stu-id="9dc7a-144">`eventType` Teams event type; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="9dc7a-145">`tenant.id`Azure Active Directory 租户 ID;在所有上下文中传递</span><span class="sxs-lookup"><span data-stu-id="9dc7a-145">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="9dc7a-146">`team`仅在通道上下文中传递，而不是在个人聊天中传递。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-146">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="9dc7a-147">`id`通道的 GUID</span><span class="sxs-lookup"><span data-stu-id="9dc7a-147">`id` GUID for the channel</span></span>
  * <span data-ttu-id="9dc7a-148">`name`团队的名称;仅在[团队重命名事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)的情况下传递</span><span class="sxs-lookup"><span data-stu-id="9dc7a-148">`name` Name of the team; passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="9dc7a-149">`channel`当提及 bot 时，仅在通道上下文中传递，或在已添加机器人的团队中的频道中传递事件</span><span class="sxs-lookup"><span data-stu-id="9dc7a-149">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="9dc7a-150">`id`通道的 GUID</span><span class="sxs-lookup"><span data-stu-id="9dc7a-150">`id` GUID for the channel</span></span>
  * <span data-ttu-id="9dc7a-151">`name`通道名称;仅在[频道修改事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)的情况下传递。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-151">`name` Channel name; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="9dc7a-152">`channelData.teamsTeamId`被.</span><span class="sxs-lookup"><span data-stu-id="9dc7a-152">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="9dc7a-153">包含此属性只是为了向后兼容。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-153">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="9dc7a-154">`channelData.teamsChannelId`被.</span><span class="sxs-lookup"><span data-stu-id="9dc7a-154">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="9dc7a-155">包含此属性只是为了向后兼容。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-155">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="9dc7a-156">示例 channelData 对象（channelCreated 事件）</span><span class="sxs-lookup"><span data-stu-id="9dc7a-156">Example channelData object (channelCreated event)</span></span>

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

## <a name="message-content"></a><span data-ttu-id="9dc7a-157">邮件内容</span><span class="sxs-lookup"><span data-stu-id="9dc7a-157">Message content</span></span>

<span data-ttu-id="9dc7a-158">你的 bot 可以发送多信息文本、图片和卡片。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-158">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="9dc7a-159">用户可以向你的 bot 发送丰富的文本和图片。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-159">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="9dc7a-160">Format</span><span class="sxs-lookup"><span data-stu-id="9dc7a-160">Format</span></span>    | <span data-ttu-id="9dc7a-161">从用户到 bot</span><span class="sxs-lookup"><span data-stu-id="9dc7a-161">From user to bot</span></span> | <span data-ttu-id="9dc7a-162">从 bot 到用户</span><span class="sxs-lookup"><span data-stu-id="9dc7a-162">From bot to user</span></span> | <span data-ttu-id="9dc7a-163">注释</span><span class="sxs-lookup"><span data-stu-id="9dc7a-163">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="9dc7a-164">格式文本 </span><span class="sxs-lookup"><span data-stu-id="9dc7a-164">Rich text</span></span> | <span data-ttu-id="9dc7a-165">✔</span><span class="sxs-lookup"><span data-stu-id="9dc7a-165">✔</span></span>                | <span data-ttu-id="9dc7a-166">✔</span><span class="sxs-lookup"><span data-stu-id="9dc7a-166">✔</span></span>                |                                                                                         |
| <span data-ttu-id="9dc7a-167">图片</span><span class="sxs-lookup"><span data-stu-id="9dc7a-167">Pictures</span></span>  | <span data-ttu-id="9dc7a-168">✔</span><span class="sxs-lookup"><span data-stu-id="9dc7a-168">✔</span></span>                | <span data-ttu-id="9dc7a-169">✔</span><span class="sxs-lookup"><span data-stu-id="9dc7a-169">✔</span></span>                | <span data-ttu-id="9dc7a-170">最大1024×1024和 1 MB，PNG、JPEG 或 GIF 格式;不支持动态 GIF</span><span class="sxs-lookup"><span data-stu-id="9dc7a-170">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span>  |
| <span data-ttu-id="9dc7a-171">圣诞卡</span><span class="sxs-lookup"><span data-stu-id="9dc7a-171">Cards</span></span>     | <span data-ttu-id="9dc7a-172">✖</span><span class="sxs-lookup"><span data-stu-id="9dc7a-172">✖</span></span>                | <span data-ttu-id="9dc7a-173">✔</span><span class="sxs-lookup"><span data-stu-id="9dc7a-173">✔</span></span>                | <span data-ttu-id="9dc7a-174">有关支持的卡片，请参阅[团队卡片参考](~/task-modules-and-cards/cards/cards-reference.md)</span><span class="sxs-lookup"><span data-stu-id="9dc7a-174">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="9dc7a-175">表情符号</span><span class="sxs-lookup"><span data-stu-id="9dc7a-175">Emojis</span></span>    | <span data-ttu-id="9dc7a-176">✖</span><span class="sxs-lookup"><span data-stu-id="9dc7a-176">✖</span></span>                | <span data-ttu-id="9dc7a-177">✔</span><span class="sxs-lookup"><span data-stu-id="9dc7a-177">✔</span></span>                | <span data-ttu-id="9dc7a-178">团队目前支持通过 UTF-16 进行的表情符号（例如，U + 1F600 for grinning 脸）</span><span class="sxs-lookup"><span data-stu-id="9dc7a-178">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span>          |

## <a name="adding-notifications-to-your-message"></a><span data-ttu-id="9dc7a-179">向邮件中添加通知</span><span class="sxs-lookup"><span data-stu-id="9dc7a-179">Adding notifications to your message</span></span>

<span data-ttu-id="9dc7a-180">通知会提醒用户有关新任务、提及和注释（与他们的工作方式相关），或者需要将通知插入到其活动源中来查看。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-180">Notifications alert users about new tasks, mentions and comments related to what they are working on, or need to look at by inserting a notice into their Activity Feed.</span></span> <span data-ttu-id="9dc7a-181">您可以通过将`TeamsChannelData`对象`Notification.Alert`属性设置为 true，将通知设置为触发来自 bot 邮件。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-181">You can set notifications to trigger from your bot message by setting the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="9dc7a-182">是否引发通知将最终取决于单个用户的团队设置，并且无法以编程方式重写这些设置。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-182">Whether or not a notification is raised will ultimately depend on the individual user's Teams settings and you cannot programmatically override these settings.</span></span> <span data-ttu-id="9dc7a-183">通知类型可以是横幅，也可以同时是横幅和电子邮件。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-183">The type of notification will be either a banner or both a banner and an email.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="9dc7a-184">C #/.NET</span><span class="sxs-lookup"><span data-stu-id="9dc7a-184">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="9dc7a-185">TypeScript/node.js</span><span class="sxs-lookup"><span data-stu-id="9dc7a-185">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="pythontabpython"></a>[<span data-ttu-id="9dc7a-186">Python</span><span class="sxs-lookup"><span data-stu-id="9dc7a-186">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="jsontabjson"></a>[<span data-ttu-id="9dc7a-187">JSON</span><span class="sxs-lookup"><span data-stu-id="9dc7a-187">JSON</span></span>](#tab/json)

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

## <a name="picture-messages"></a><span data-ttu-id="9dc7a-188">图片邮件</span><span class="sxs-lookup"><span data-stu-id="9dc7a-188">Picture messages</span></span>

<span data-ttu-id="9dc7a-189">通过将附件添加到邮件来发送图片。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-189">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="9dc7a-190">您可以在[Bot 框架文档](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0)中找到有关附件的详细信息。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-190">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span></span>

<span data-ttu-id="9dc7a-191">图片最多可以为1024×1024和 1 MB （PNG、JPEG 或 GIF 格式）;不支持动态 GIF。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-191">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="9dc7a-192">建议使用 XML 指定每个图像的高度和宽度。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-192">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="9dc7a-193">如果使用 Markdown，则图像大小默认为256×256。</span><span class="sxs-lookup"><span data-stu-id="9dc7a-193">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="9dc7a-194">例如：</span><span class="sxs-lookup"><span data-stu-id="9dc7a-194">For example:</span></span>

* <span data-ttu-id="9dc7a-195">改用`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="9dc7a-195">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="9dc7a-196">请勿使用-`![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="9dc7a-196">Don't use - `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="next-steps"></a><span data-ttu-id="9dc7a-197">后续步骤</span><span class="sxs-lookup"><span data-stu-id="9dc7a-197">Next steps</span></span>

* [<span data-ttu-id="9dc7a-198">发送主动消息</span><span class="sxs-lookup"><span data-stu-id="9dc7a-198">Sending proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
* [<span data-ttu-id="9dc7a-199">订阅对话事件</span><span class="sxs-lookup"><span data-stu-id="9dc7a-199">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
