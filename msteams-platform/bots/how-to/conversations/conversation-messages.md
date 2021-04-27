---
title: 智能机器人对话中的邮件
description: 介绍与 Microsoft Teams 机器人对话的方法
ms.topic: overview
ms.author: anclear
localization_priority: Normal
keyword: receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 5944cc299a8ad4bebdaf034d803919a54868e41f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020924"
---
# <a name="messages-in-bot-conversations"></a><span data-ttu-id="875fe-103">智能机器人对话中的邮件</span><span class="sxs-lookup"><span data-stu-id="875fe-103">Messages in bot conversations</span></span>

<span data-ttu-id="875fe-104">对话中每条消息都是一 `Activity` 个类型 为 的对象 `messageType: message` 。</span><span class="sxs-lookup"><span data-stu-id="875fe-104">Each message in a conversation is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="875fe-105">当用户发送消息时，Teams 会向自动程序发布消息。</span><span class="sxs-lookup"><span data-stu-id="875fe-105">When a user sends a message, Teams posts the message to your bot.</span></span> <span data-ttu-id="875fe-106">Teams 将 JSON 对象发送到机器人的消息终结点。</span><span class="sxs-lookup"><span data-stu-id="875fe-106">Teams sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="875fe-107">自动程序将检查消息以确定其类型并相应地做出响应。</span><span class="sxs-lookup"><span data-stu-id="875fe-107">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="875fe-108">基本对话通过 Bot Framework 连接器（一个 REST API）进行处理。</span><span class="sxs-lookup"><span data-stu-id="875fe-108">Basic conversations are handled through the Bot Framework connector, a single REST API.</span></span> <span data-ttu-id="875fe-109">此 API 使机器人能够与 Teams 和其他频道进行通信。</span><span class="sxs-lookup"><span data-stu-id="875fe-109">This API enables your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="875fe-110">Bot Builder SDK 提供以下功能：</span><span class="sxs-lookup"><span data-stu-id="875fe-110">The Bot Builder SDK provides the following features:</span></span>

* <span data-ttu-id="875fe-111">轻松访问 Bot Framework 连接器。</span><span class="sxs-lookup"><span data-stu-id="875fe-111">Easy access to the Bot Framework connector.</span></span>
* <span data-ttu-id="875fe-112">用于管理对话流和状态的其他功能。</span><span class="sxs-lookup"><span data-stu-id="875fe-112">Additional functionality to manage conversation flow and state.</span></span>
* <span data-ttu-id="875fe-113">合并认知服务的简单方法，如自然语言处理 (NLP) 。</span><span class="sxs-lookup"><span data-stu-id="875fe-113">Simple ways to incorporate cognitive services, such as natural language processing (NLP).</span></span>

<span data-ttu-id="875fe-114">自动程序使用 属性接收来自 Teams 的消息， `Text` 并且它会向用户发送一个或多个消息响应。</span><span class="sxs-lookup"><span data-stu-id="875fe-114">Your bot receives messages from Teams using the `Text` property and it sends single or multiple message responses to the users.</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="875fe-115">接收消息</span><span class="sxs-lookup"><span data-stu-id="875fe-115">Receive a message</span></span>

<span data-ttu-id="875fe-116">若要接收短信，请使用 `Activity` 对象的 `Text` 属性。</span><span class="sxs-lookup"><span data-stu-id="875fe-116">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="875fe-117">在机器人的活动处理程序中，使用圈上下文对象的 `Activity` 来读取单一消息请求。</span><span class="sxs-lookup"><span data-stu-id="875fe-117">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="875fe-118">以下代码显示了一个接收邮件的示例：</span><span class="sxs-lookup"><span data-stu-id="875fe-118">The following code shows an example of receiving a message:</span></span>

# <a name="c"></a>[<span data-ttu-id="875fe-119">C#</span><span class="sxs-lookup"><span data-stu-id="875fe-119">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="875fe-120">TypeScript</span><span class="sxs-lookup"><span data-stu-id="875fe-120">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="875fe-121">Python</span><span class="sxs-lookup"><span data-stu-id="875fe-121">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="875fe-122">JSON</span><span class="sxs-lookup"><span data-stu-id="875fe-122">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="875fe-123">发送消息</span><span class="sxs-lookup"><span data-stu-id="875fe-123">Send a message</span></span>

<span data-ttu-id="875fe-124">若要发送短信，请指定你想要作为活动发送的字符串。</span><span class="sxs-lookup"><span data-stu-id="875fe-124">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="875fe-125">在机器人的活动处理程序中，使用 turn context 对象的方法发送 `SendActivityAsync` 单个消息响应。</span><span class="sxs-lookup"><span data-stu-id="875fe-125">In the bot's activity handler, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="875fe-126">使用 对象的 `SendActivitiesAsync` 方法一次发送多个响应。</span><span class="sxs-lookup"><span data-stu-id="875fe-126">Use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span>

<span data-ttu-id="875fe-127">以下代码显示向对话中添加用户时发送邮件的示例：</span><span class="sxs-lookup"><span data-stu-id="875fe-127">The following code shows an example of sending a message when a user is added to a conversation:</span></span>

# <a name="c"></a>[<span data-ttu-id="875fe-128">C#</span><span class="sxs-lookup"><span data-stu-id="875fe-128">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="875fe-129">TypeScript</span><span class="sxs-lookup"><span data-stu-id="875fe-129">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="875fe-130">Python</span><span class="sxs-lookup"><span data-stu-id="875fe-130">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="875fe-131">JSON</span><span class="sxs-lookup"><span data-stu-id="875fe-131">JSON</span></span>](#tab/json)

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
> <span data-ttu-id="875fe-132">在同一活动有效负载中发送短信和附件时，将发生邮件拆分。</span><span class="sxs-lookup"><span data-stu-id="875fe-132">Message splitting occurs when a text message and an attachment are sent in the same activity payload.</span></span> <span data-ttu-id="875fe-133">此活动由 Microsoft Teams 拆分为单独的活动，一个仅包含一条短信，另一个包含附件。</span><span class="sxs-lookup"><span data-stu-id="875fe-133">This activity is split into separate activities by Microsoft Teams, one with just a text message and the other with an attachment.</span></span> <span data-ttu-id="875fe-134">拆分活动时，您不会收到响应消息 ID，该 ID 用于主动更新或删除[](~/bots/how-to/update-and-delete-bot-messages.md)邮件。</span><span class="sxs-lookup"><span data-stu-id="875fe-134">As the activity is split, you do not receive the message ID in response, which is used to [update or delete](~/bots/how-to/update-and-delete-bot-messages.md) the message proactively.</span></span> <span data-ttu-id="875fe-135">建议发送单独的活动，而不是根据邮件拆分。</span><span class="sxs-lookup"><span data-stu-id="875fe-135">It is recommended to send separate activities instead of depending on message splitting.</span></span>

<span data-ttu-id="875fe-136">在用户和机器人之间发送的消息包含邮件中的内部通道数据。</span><span class="sxs-lookup"><span data-stu-id="875fe-136">Messages sent between users and bots include internal channel data within the message.</span></span> <span data-ttu-id="875fe-137">此数据允许机器人在此频道上正常通信。</span><span class="sxs-lookup"><span data-stu-id="875fe-137">This data allows the bot to communicate properly on that channel.</span></span> <span data-ttu-id="875fe-138">Bot Builder SDK 允许你修改消息结构。</span><span class="sxs-lookup"><span data-stu-id="875fe-138">The Bot Builder SDK allows you to modify the message structure.</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="875fe-139">Teams 频道数据</span><span class="sxs-lookup"><span data-stu-id="875fe-139">Teams channel data</span></span>

<span data-ttu-id="875fe-140">对象 `channelData` 包含特定于 Teams 的信息，是团队和频道 ID 的权威性来源。</span><span class="sxs-lookup"><span data-stu-id="875fe-140">The `channelData` object contains Teams-specific information and is a definitive source for team and channel IDs.</span></span> <span data-ttu-id="875fe-141">（可选）你可以缓存这些 ID 并用作本地存储的密钥。</span><span class="sxs-lookup"><span data-stu-id="875fe-141">Optionally, you can cache and use these IDs as keys for local storage.</span></span> <span data-ttu-id="875fe-142">`TeamsActivityHandler`SDK 中的 从 对象提取重要信息 `channelData` ，使其易于访问。</span><span class="sxs-lookup"><span data-stu-id="875fe-142">The `TeamsActivityHandler` in the SDK pulls out important information from the `channelData` object to make it easily accessible.</span></span> <span data-ttu-id="875fe-143">但是，您始终可以从对象访问 `turnContext` 原始数据。</span><span class="sxs-lookup"><span data-stu-id="875fe-143">However, you can always access the original data from the `turnContext` object.</span></span>

<span data-ttu-id="875fe-144">`channelData`对象不包含在个人对话中的邮件中，因为邮件在频道外发生。</span><span class="sxs-lookup"><span data-stu-id="875fe-144">The `channelData` object is not included in messages in personal conversations, as these take place outside of a channel.</span></span>

<span data-ttu-id="875fe-145">发送给 `channelData` 自动程序的活动中的典型对象包含以下信息：</span><span class="sxs-lookup"><span data-stu-id="875fe-145">A typical `channelData` object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="875fe-146">`eventType`：仅在频道修改事件的情况下传递的 Teams [事件类型](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="875fe-146">`eventType`: Teams event type passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="875fe-147">`tenant.id`：在所有上下文中传递的 Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="875fe-147">`tenant.id`: Azure Active Directory tenant ID passed in all contexts.</span></span>
* <span data-ttu-id="875fe-148">`team`：仅在频道上下文中传递，而不是在个人聊天中传递。</span><span class="sxs-lookup"><span data-stu-id="875fe-148">`team`: Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="875fe-149">`id`：通道的 GUID。</span><span class="sxs-lookup"><span data-stu-id="875fe-149">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="875fe-150">`name`：仅在团队重命名事件的情况下传递 [的团队名称](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="875fe-150">`name`: Name of the team passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="875fe-151">`channel`：仅在提到自动程序时在频道上下文中传递，或针对团队中已添加自动程序的团队中的事件传递。</span><span class="sxs-lookup"><span data-stu-id="875fe-151">`channel`: Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="875fe-152">`id`：通道的 GUID。</span><span class="sxs-lookup"><span data-stu-id="875fe-152">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="875fe-153">`name`：仅在通道修改事件的情况下传递 [的频道名称](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="875fe-153">`name`: Channel name passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="875fe-154">`channelData.teamsTeamId`：已弃用。</span><span class="sxs-lookup"><span data-stu-id="875fe-154">`channelData.teamsTeamId`: Deprecated.</span></span> <span data-ttu-id="875fe-155">此属性仅包含用于向后兼容。</span><span class="sxs-lookup"><span data-stu-id="875fe-155">This property is only included for backward compatibility.</span></span>
* <span data-ttu-id="875fe-156">`channelData.teamsChannelId`：已弃用。</span><span class="sxs-lookup"><span data-stu-id="875fe-156">`channelData.teamsChannelId`: Deprecated.</span></span> <span data-ttu-id="875fe-157">此属性仅包含用于向后兼容。</span><span class="sxs-lookup"><span data-stu-id="875fe-157">This property is only included for backward compatibility.</span></span>

### <a name="example-channeldata-object-or-channelcreated-event"></a><span data-ttu-id="875fe-158">channelData 对象或 channelCreated 事件示例</span><span class="sxs-lookup"><span data-stu-id="875fe-158">Example channelData object or channelCreated event</span></span>

<span data-ttu-id="875fe-159">以下代码显示了 channelData 对象的示例：</span><span class="sxs-lookup"><span data-stu-id="875fe-159">The following code shows an example of channelData object:</span></span>

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

<span data-ttu-id="875fe-160">从自动程序接收或发送到自动程序的邮件可以包括不同类型的邮件内容。</span><span class="sxs-lookup"><span data-stu-id="875fe-160">Messages received from or sent to your bot can include different types of message content.</span></span>

## <a name="message-content"></a><span data-ttu-id="875fe-161">邮件内容</span><span class="sxs-lookup"><span data-stu-id="875fe-161">Message content</span></span>

| <span data-ttu-id="875fe-162">格式</span><span class="sxs-lookup"><span data-stu-id="875fe-162">Format</span></span>    | <span data-ttu-id="875fe-163">从用户到机器人</span><span class="sxs-lookup"><span data-stu-id="875fe-163">From user to bot</span></span> | <span data-ttu-id="875fe-164">从自动程序到用户</span><span class="sxs-lookup"><span data-stu-id="875fe-164">From bot to user</span></span> | <span data-ttu-id="875fe-165">注意</span><span class="sxs-lookup"><span data-stu-id="875fe-165">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="875fe-166">格式文本 </span><span class="sxs-lookup"><span data-stu-id="875fe-166">Rich text</span></span> | <span data-ttu-id="875fe-167">✔</span><span class="sxs-lookup"><span data-stu-id="875fe-167">✔</span></span>                | <span data-ttu-id="875fe-168">✔</span><span class="sxs-lookup"><span data-stu-id="875fe-168">✔</span></span>                | <span data-ttu-id="875fe-169">机器人可以发送格式文本、图片和卡片。</span><span class="sxs-lookup"><span data-stu-id="875fe-169">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="875fe-170">用户可以向自动程序发送格式文本和图片。</span><span class="sxs-lookup"><span data-stu-id="875fe-170">Users can send rich text and pictures to your bot.</span></span>                                                                                        |
| <span data-ttu-id="875fe-171">图片</span><span class="sxs-lookup"><span data-stu-id="875fe-171">Pictures</span></span>  | <span data-ttu-id="875fe-172">✔</span><span class="sxs-lookup"><span data-stu-id="875fe-172">✔</span></span>                | <span data-ttu-id="875fe-173">✔</span><span class="sxs-lookup"><span data-stu-id="875fe-173">✔</span></span>                | <span data-ttu-id="875fe-174">PNG、JPEG 或 GIF 格式×最大为 1024×1024 和 1 MB。</span><span class="sxs-lookup"><span data-stu-id="875fe-174">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="875fe-175">不支持动态 GIF。</span><span class="sxs-lookup"><span data-stu-id="875fe-175">Animated GIF is not supported.</span></span>  |
| <span data-ttu-id="875fe-176">卡</span><span class="sxs-lookup"><span data-stu-id="875fe-176">Cards</span></span>     | <span data-ttu-id="875fe-177">✖</span><span class="sxs-lookup"><span data-stu-id="875fe-177">✖</span></span>                | <span data-ttu-id="875fe-178">✔</span><span class="sxs-lookup"><span data-stu-id="875fe-178">✔</span></span>                | <span data-ttu-id="875fe-179">有关受支持的 [卡片，](~/task-modules-and-cards/cards/cards-reference.md) 请参阅 Teams 卡参考。</span><span class="sxs-lookup"><span data-stu-id="875fe-179">See the [Teams card reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards.</span></span> |
| <span data-ttu-id="875fe-180">表情符号</span><span class="sxs-lookup"><span data-stu-id="875fe-180">Emojis</span></span>    | <span data-ttu-id="875fe-181">✖</span><span class="sxs-lookup"><span data-stu-id="875fe-181">✖</span></span>                | <span data-ttu-id="875fe-182">✔</span><span class="sxs-lookup"><span data-stu-id="875fe-182">✔</span></span>                | <span data-ttu-id="875fe-183">Teams 当前支持通过 UTF-16 使用表情符号，例如 U+1F600，用于表情符号。</span><span class="sxs-lookup"><span data-stu-id="875fe-183">Teams currently supports emojis through UTF-16, such as U+1F600 for grinning face.</span></span> |

<span data-ttu-id="875fe-184">您还可以使用 属性向邮件添加 `Notification.Alert` 通知。</span><span class="sxs-lookup"><span data-stu-id="875fe-184">You can also add notifications to your message using the `Notification.Alert` property.</span></span>

## <a name="notifications-to-your-message"></a><span data-ttu-id="875fe-185">邮件通知</span><span class="sxs-lookup"><span data-stu-id="875fe-185">Notifications to your message</span></span>

<span data-ttu-id="875fe-186">通知会提醒用户有关新任务、提及和评论。</span><span class="sxs-lookup"><span data-stu-id="875fe-186">Notifications alert users about new tasks, mentions, and comments.</span></span> <span data-ttu-id="875fe-187">这些警报与用户正在处理或必须通过向活动源中插入通知来查看内容相关。</span><span class="sxs-lookup"><span data-stu-id="875fe-187">These alerts are related to what users are working on or what they must look at by inserting a notice into their activity feed.</span></span> <span data-ttu-id="875fe-188">对于从自动程序消息触发的通知，将 `TeamsChannelData` objects `Notification.Alert` 属性设置为 *true*。</span><span class="sxs-lookup"><span data-stu-id="875fe-188">For notifications to trigger from your bot message, set the `TeamsChannelData` objects `Notification.Alert` property to *true*.</span></span> <span data-ttu-id="875fe-189">是否引发通知取决于单个用户的 Teams 设置，你无法替代这些设置。</span><span class="sxs-lookup"><span data-stu-id="875fe-189">Whether or not a notification is raised depends on the individual user's Teams settings and you cannot override these settings.</span></span> <span data-ttu-id="875fe-190">通知类型可以是横幅，也可以同时为横幅和电子邮件。</span><span class="sxs-lookup"><span data-stu-id="875fe-190">The notification type is either a banner, or both a banner and an email.</span></span>

> [!NOTE]
> <span data-ttu-id="875fe-191">" **摘要"** 字段将来自用户的任何文本显示为源中的通知消息。</span><span class="sxs-lookup"><span data-stu-id="875fe-191">The **Summary** field displays any text from the user as a notification message in the feed.</span></span>

<span data-ttu-id="875fe-192">以下代码显示向邮件添加通知的示例：</span><span class="sxs-lookup"><span data-stu-id="875fe-192">The following code shows an example of adding notifications to your message:</span></span>

# <a name="c"></a>[<span data-ttu-id="875fe-193">C#</span><span class="sxs-lookup"><span data-stu-id="875fe-193">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescript"></a>[<span data-ttu-id="875fe-194">TypeScript</span><span class="sxs-lookup"><span data-stu-id="875fe-194">TypeScript</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="875fe-195">Python</span><span class="sxs-lookup"><span data-stu-id="875fe-195">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="875fe-196">JSON</span><span class="sxs-lookup"><span data-stu-id="875fe-196">JSON</span></span>](#tab/json)

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

<span data-ttu-id="875fe-197">若要增强邮件功能，可以将图片作为邮件附件进行添加。</span><span class="sxs-lookup"><span data-stu-id="875fe-197">To enhance your message, you can include pictures as attachments to that message.</span></span>

## <a name="picture-messages"></a><span data-ttu-id="875fe-198">图片消息</span><span class="sxs-lookup"><span data-stu-id="875fe-198">Picture messages</span></span>

<span data-ttu-id="875fe-199">图片通过向邮件添加附件来发送。</span><span class="sxs-lookup"><span data-stu-id="875fe-199">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="875fe-200">有关附件详细信息，请参阅 [Bot Framework 文档](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)。</span><span class="sxs-lookup"><span data-stu-id="875fe-200">For more information on attachments, see [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).</span></span>

<span data-ttu-id="875fe-201">图片可以是最多 1024×1024 和 1 MB PNG、 JPEG 或 GIF 格式。</span><span class="sxs-lookup"><span data-stu-id="875fe-201">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="875fe-202">不支持动态 GIF。</span><span class="sxs-lookup"><span data-stu-id="875fe-202">Animated GIF is not supported.</span></span>

<span data-ttu-id="875fe-203">使用 XML 指定每个图像的高度和宽度。</span><span class="sxs-lookup"><span data-stu-id="875fe-203">Specify the height and width of each image by using XML.</span></span> <span data-ttu-id="875fe-204">在 markdown 中，图像大小默认为 256×256。</span><span class="sxs-lookup"><span data-stu-id="875fe-204">In markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="875fe-205">例如：</span><span class="sxs-lookup"><span data-stu-id="875fe-205">For example:</span></span>

* <span data-ttu-id="875fe-206">使用 `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` ：。</span><span class="sxs-lookup"><span data-stu-id="875fe-206">Use: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.</span></span>
* <span data-ttu-id="875fe-207">请勿使用 `![Duck on a rock](http://aka.ms/Fo983c)` ：。</span><span class="sxs-lookup"><span data-stu-id="875fe-207">Do not use: `![Duck on a rock](http://aka.ms/Fo983c)`.</span></span>

<span data-ttu-id="875fe-208">对话机器人可以包含可简化业务工作流的自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="875fe-208">A conversational bot can include Adaptive Cards that simplify business workflows.</span></span> <span data-ttu-id="875fe-209">自适应卡片提供丰富的可自定义文本、语音、图像、按钮和输入字段。</span><span class="sxs-lookup"><span data-stu-id="875fe-209">Adaptive Cards offer rich customizable text, speech, images, buttons, and input fields.</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="875fe-210">自适应卡</span><span class="sxs-lookup"><span data-stu-id="875fe-210">Adaptive Cards</span></span>

<span data-ttu-id="875fe-211">自适应卡片可以在机器人中创作，并可在多个应用（如 Teams、网站等）中显示。</span><span class="sxs-lookup"><span data-stu-id="875fe-211">Adaptive Cards can be authored in a bot and shown in multiple apps such as Teams, your website, and so on.</span></span> <span data-ttu-id="875fe-212">有关详细信息，请参阅自适应 [卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)。</span><span class="sxs-lookup"><span data-stu-id="875fe-212">For more information, see [Adaptive Cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>

<span data-ttu-id="875fe-213">以下代码显示发送简单自适应卡片的示例：</span><span class="sxs-lookup"><span data-stu-id="875fe-213">The following code shows an example of sending a simple Adaptive Card:</span></span>

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

<span data-ttu-id="875fe-214">若要了解有关机器人中的卡和卡的更多信息，请参阅 [卡片文档](~/task-modules-and-cards/what-are-cards.md)。</span><span class="sxs-lookup"><span data-stu-id="875fe-214">To know more about cards and cards in bots, see [cards documentation](~/task-modules-and-cards/what-are-cards.md).</span></span>

## <a name="status-code-responses"></a><span data-ttu-id="875fe-215">状态代码响应</span><span class="sxs-lookup"><span data-stu-id="875fe-215">Status code responses</span></span>

<span data-ttu-id="875fe-216">以下是状态代码及其错误代码和消息值：</span><span class="sxs-lookup"><span data-stu-id="875fe-216">Following are the status codes and their error code and message values:</span></span>

| <span data-ttu-id="875fe-217">状态代码</span><span class="sxs-lookup"><span data-stu-id="875fe-217">Status code</span></span> | <span data-ttu-id="875fe-218">错误代码和消息值</span><span class="sxs-lookup"><span data-stu-id="875fe-218">Error code and message values</span></span> | <span data-ttu-id="875fe-219">说明</span><span class="sxs-lookup"><span data-stu-id="875fe-219">Description</span></span> |
|----------------|-----------------|-----------------|
| <span data-ttu-id="875fe-220">403</span><span class="sxs-lookup"><span data-stu-id="875fe-220">403</span></span> | <span data-ttu-id="875fe-221">**代码**： `ConversationBlockedByUser`</span><span class="sxs-lookup"><span data-stu-id="875fe-221">**Code**: `ConversationBlockedByUser`</span></span> <br/> <span data-ttu-id="875fe-222">**消息**：用户阻止了与机器人的对话。</span><span class="sxs-lookup"><span data-stu-id="875fe-222">**Message**: User blocked the conversation with the bot.</span></span> | <span data-ttu-id="875fe-223">用户通过审核设置在一对一聊天或频道中阻止机器人。</span><span class="sxs-lookup"><span data-stu-id="875fe-223">User blocked the bot in 1:1 chat or a channel through moderation settings.</span></span> |
| <span data-ttu-id="875fe-224">403</span><span class="sxs-lookup"><span data-stu-id="875fe-224">403</span></span> | <span data-ttu-id="875fe-225">**代码**： `BotNotInConversationRoster`</span><span class="sxs-lookup"><span data-stu-id="875fe-225">**Code**: `BotNotInConversationRoster`</span></span> <br/> <span data-ttu-id="875fe-226">**消息**：机器人不是对话名单中的一部分。</span><span class="sxs-lookup"><span data-stu-id="875fe-226">**Message**: The bot is not part of the conversation roster.</span></span> | <span data-ttu-id="875fe-227">机器人不是对话的一部分。</span><span class="sxs-lookup"><span data-stu-id="875fe-227">The bot is not part of the conversation.</span></span> |
| <span data-ttu-id="875fe-228">403</span><span class="sxs-lookup"><span data-stu-id="875fe-228">403</span></span> | <span data-ttu-id="875fe-229">**代码**： `BotDisabledByAdmin`</span><span class="sxs-lookup"><span data-stu-id="875fe-229">**Code**: `BotDisabledByAdmin`</span></span> <br/> <span data-ttu-id="875fe-230">**消息**：租户管理员已禁用此自动程序。</span><span class="sxs-lookup"><span data-stu-id="875fe-230">**Message**: The tenant admin disabled this bot.</span></span> | <span data-ttu-id="875fe-231">租户阻止了机器人。</span><span class="sxs-lookup"><span data-stu-id="875fe-231">Tenant blocked the bot.</span></span> |
| <span data-ttu-id="875fe-232">401</span><span class="sxs-lookup"><span data-stu-id="875fe-232">401</span></span> | <span data-ttu-id="875fe-233">**代码**： `BotNotRegistered`</span><span class="sxs-lookup"><span data-stu-id="875fe-233">**Code**: `BotNotRegistered`</span></span> <br/> <span data-ttu-id="875fe-234">**消息**：未找到此自动程序注册。</span><span class="sxs-lookup"><span data-stu-id="875fe-234">**Message**: No registration found for this bot.</span></span> | <span data-ttu-id="875fe-235">未找到此自动程序注册。</span><span class="sxs-lookup"><span data-stu-id="875fe-235">The registration for this bot was not found.</span></span> |
| <span data-ttu-id="875fe-236">412</span><span class="sxs-lookup"><span data-stu-id="875fe-236">412</span></span> | <span data-ttu-id="875fe-237">**代码**： `PreconditionFailed`</span><span class="sxs-lookup"><span data-stu-id="875fe-237">**Code**: `PreconditionFailed`</span></span> <br/> <span data-ttu-id="875fe-238">**消息**：先决条件失败，请重试。</span><span class="sxs-lookup"><span data-stu-id="875fe-238">**Message**: Precondition failed, please try again.</span></span> | <span data-ttu-id="875fe-239">由于同一对话上的多个并发操作，某一依赖项的前提条件失败。</span><span class="sxs-lookup"><span data-stu-id="875fe-239">A precondition failed on one of our dependencies due to multiple concurrent operations on the same conversation.</span></span> |
| <span data-ttu-id="875fe-240">404</span><span class="sxs-lookup"><span data-stu-id="875fe-240">404</span></span> | <span data-ttu-id="875fe-241">**代码**： `ConversationNotFound`</span><span class="sxs-lookup"><span data-stu-id="875fe-241">**Code**: `ConversationNotFound`</span></span> <br/> <span data-ttu-id="875fe-242">**消息**：未找到对话。</span><span class="sxs-lookup"><span data-stu-id="875fe-242">**Message**: Conversation not found.</span></span> | <span data-ttu-id="875fe-243">未找到对话。</span><span class="sxs-lookup"><span data-stu-id="875fe-243">The conversation was not found.</span></span> |
| <span data-ttu-id="875fe-244">413</span><span class="sxs-lookup"><span data-stu-id="875fe-244">413</span></span> | <span data-ttu-id="875fe-245">**代码**： `MessageSizeTooBig`</span><span class="sxs-lookup"><span data-stu-id="875fe-245">**Code**: `MessageSizeTooBig`</span></span> <br/> <span data-ttu-id="875fe-246">**邮件**：邮件大小过大。</span><span class="sxs-lookup"><span data-stu-id="875fe-246">**Message**: Message size too large.</span></span> | <span data-ttu-id="875fe-247">传入请求的大小太大。</span><span class="sxs-lookup"><span data-stu-id="875fe-247">The size on the incoming request was too large.</span></span> |
| <span data-ttu-id="875fe-248">429</span><span class="sxs-lookup"><span data-stu-id="875fe-248">429</span></span> | <span data-ttu-id="875fe-249">**代码**： `Throttled`</span><span class="sxs-lookup"><span data-stu-id="875fe-249">**Code**: `Throttled`</span></span> <br/> <span data-ttu-id="875fe-250">**消息**：请求过多。</span><span class="sxs-lookup"><span data-stu-id="875fe-250">**Message**: Too many requests.</span></span> <span data-ttu-id="875fe-251">还返回在之后重试时间。</span><span class="sxs-lookup"><span data-stu-id="875fe-251">Also returns when to retry after.</span></span> | <span data-ttu-id="875fe-252">机器人发送的请求过多。</span><span class="sxs-lookup"><span data-stu-id="875fe-252">Too many requests were sent by the bot.</span></span> <span data-ttu-id="875fe-253">有关详细信息，请参阅速率 [限制](~/bots/how-to/rate-limit.md)。</span><span class="sxs-lookup"><span data-stu-id="875fe-253">For more information, see [rate limit](~/bots/how-to/rate-limit.md).</span></span> |

## <a name="code-sample"></a><span data-ttu-id="875fe-254">代码示例</span><span class="sxs-lookup"><span data-stu-id="875fe-254">Code sample</span></span>

|<span data-ttu-id="875fe-255">示例名称</span><span class="sxs-lookup"><span data-stu-id="875fe-255">Sample name</span></span> | <span data-ttu-id="875fe-256">说明</span><span class="sxs-lookup"><span data-stu-id="875fe-256">Description</span></span> | <span data-ttu-id="875fe-257">.NETCore</span><span class="sxs-lookup"><span data-stu-id="875fe-257">.NETCore</span></span> | <span data-ttu-id="875fe-258">Node.js</span><span class="sxs-lookup"><span data-stu-id="875fe-258">Node.js</span></span> | <span data-ttu-id="875fe-259">Python</span><span class="sxs-lookup"><span data-stu-id="875fe-259">Python</span></span> |
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="875fe-260">Teams 对话自动程序</span><span class="sxs-lookup"><span data-stu-id="875fe-260">Teams conversation bot</span></span> | <span data-ttu-id="875fe-261">消息和对话事件处理。</span><span class="sxs-lookup"><span data-stu-id="875fe-261">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="875fe-262">View</span><span class="sxs-lookup"><span data-stu-id="875fe-262">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="875fe-263">View</span><span class="sxs-lookup"><span data-stu-id="875fe-263">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="875fe-264">View</span><span class="sxs-lookup"><span data-stu-id="875fe-264">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="see-also"></a><span data-ttu-id="875fe-265">另请参阅</span><span class="sxs-lookup"><span data-stu-id="875fe-265">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="875fe-266">发送主动邮件</span><span class="sxs-lookup"><span data-stu-id="875fe-266">Send proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="875fe-267">订阅对话事件</span><span class="sxs-lookup"><span data-stu-id="875fe-267">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="next-step"></a><span data-ttu-id="875fe-268">后续步骤</span><span class="sxs-lookup"><span data-stu-id="875fe-268">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="875fe-269">自动程序命令菜单</span><span class="sxs-lookup"><span data-stu-id="875fe-269">Bot command menus</span></span>](~/bots/how-to/create-a-bot-commands-menu.md)
