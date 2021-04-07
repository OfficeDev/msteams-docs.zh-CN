---
title: 对话基础知识
description: 介绍与 Microsoft Teams 自动程序对话的方法
ms.topic: overview
ms.author: anclear
keyword: conversations basics receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 193a93dbf775389383e0385207fa4112440bffe5
ms.sourcegitcommit: 82bda0599ba2676ab9348c2f4284f73c7dad0838
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596672"
---
# <a name="conversation-basics"></a><span data-ttu-id="aa4a3-103">对话基础知识</span><span class="sxs-lookup"><span data-stu-id="aa4a3-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="aa4a3-104">对话是在 Microsoft Teams 自动程序与一个或多个用户之间发送的一系列消息。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-104">A conversation is a series of messages sent between your Microsoft Teams bot and one or more users.</span></span> <span data-ttu-id="aa4a3-105">有三种类型的对话，在 Teams 中也称为范围：</span><span class="sxs-lookup"><span data-stu-id="aa4a3-105">There are three types of conversations, also called scopes in Teams:</span></span>

| <span data-ttu-id="aa4a3-106">对话类型</span><span class="sxs-lookup"><span data-stu-id="aa4a3-106">Conversation type</span></span> | <span data-ttu-id="aa4a3-107">Description</span><span class="sxs-lookup"><span data-stu-id="aa4a3-107">Description</span></span> |
| ------- | ----------- |
| `channel` | <span data-ttu-id="aa4a3-108">此对话类型对频道的所有成员可见。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-108">This conversation type is visible to all members of the channel.</span></span> |
| `personal` | <span data-ttu-id="aa4a3-109">此对话类型包括机器人和单个用户之间的对话。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-109">This conversation type includes conversations between bots and a single user.</span></span> |
| `groupChat` | <span data-ttu-id="aa4a3-110">此对话类型包括机器人与两个或多个用户之间的聊天。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-110">This conversation type includes chat between a bot and two or more users.</span></span> <span data-ttu-id="aa4a3-111">它还可在会议聊天中启用机器人。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-111">It also enables your bot in meeting chats.</span></span> |

<span data-ttu-id="aa4a3-112">自动程序的行为方式有所不同，具体取决于它涉及的对话：</span><span class="sxs-lookup"><span data-stu-id="aa4a3-112">A bot behaves differently depending on the conversation it is involved in:</span></span>

* <span data-ttu-id="aa4a3-113">频道和群聊对话中的聊天机器人要求用户 @ 提及机器人，以在频道中调用它。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="aa4a3-114">一对一对话中的机器人不需要 @ 提及。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-114">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="aa4a3-115">用户发送的所有消息将路由到自动程序。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-115">All messages sent by the user routes to your bot.</span></span>

<span data-ttu-id="aa4a3-116">若要使机器人能够处理特定对话或范围，在应用清单 中添加对此 [范围的支持](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-116">For the bot to work in a particular conversation or scope, add support to that scope in the [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="messages-in-bot-conversations"></a><span data-ttu-id="aa4a3-117">机器人对话中的消息</span><span class="sxs-lookup"><span data-stu-id="aa4a3-117">Messages in bot conversations</span></span>

<span data-ttu-id="aa4a3-118">对话中每条消息都是一 `Activity` 个类型 为 的对象 `messageType: message` 。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-118">Each message in a conversation is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="aa4a3-119">当用户发送消息时，Teams 会向自动程序发布消息。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-119">When a user sends a message, Teams posts the message to your bot.</span></span> <span data-ttu-id="aa4a3-120">Teams 将 JSON 对象发送到机器人的消息终结点。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-120">Teams sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="aa4a3-121">自动程序将检查消息以确定其类型并相应地做出响应。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-121">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="aa4a3-122">基本对话通过 Bot Framework 连接器（一个 REST API）进行处理。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-122">Basic conversations are handled through the Bot Framework connector, a single REST API.</span></span> <span data-ttu-id="aa4a3-123">此 API 使机器人能够与 Teams 和其他频道进行通信。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-123">This API enables your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="aa4a3-124">Bot Builder SDK 提供以下内容：</span><span class="sxs-lookup"><span data-stu-id="aa4a3-124">The Bot Builder SDK provides the following:</span></span>

* <span data-ttu-id="aa4a3-125">轻松访问 Bot Framework 连接器。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-125">Easy access to the Bot Framework connector.</span></span>
* <span data-ttu-id="aa4a3-126">用于管理对话流和状态的其他功能。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-126">Additional functionality to manage conversation flow and state.</span></span>
* <span data-ttu-id="aa4a3-127">合并认知服务（如自然语言处理和 NLP (）) 。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-127">Simple ways to incorporate cognitive services such as Natural Language Processing (NLP).</span></span>

<span data-ttu-id="aa4a3-128">自动程序使用 属性接收来自 Teams 的消息， `Text` 并且它会向用户发送一个或多个消息响应。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-128">Your bot receives messages from Teams using the `Text` property and it sends single or multiple message responses to the users.</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="aa4a3-129">接收消息</span><span class="sxs-lookup"><span data-stu-id="aa4a3-129">Receive a message</span></span>

<span data-ttu-id="aa4a3-130">若要接收短信，请使用 `Activity` 对象的 `Text` 属性。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-130">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="aa4a3-131">在机器人的活动处理程序中，使用圈上下文对象的 `Activity` 来读取单一消息请求。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-131">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="aa4a3-132">以下代码显示了一个接收邮件的示例：</span><span class="sxs-lookup"><span data-stu-id="aa4a3-132">The following code shows an example of receiving a message:</span></span>

# <a name="c"></a>[<span data-ttu-id="aa4a3-133">C#</span><span class="sxs-lookup"><span data-stu-id="aa4a3-133">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="aa4a3-134">TypeScript</span><span class="sxs-lookup"><span data-stu-id="aa4a3-134">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="aa4a3-135">Python</span><span class="sxs-lookup"><span data-stu-id="aa4a3-135">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="aa4a3-136">JSON</span><span class="sxs-lookup"><span data-stu-id="aa4a3-136">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="aa4a3-137">发送消息</span><span class="sxs-lookup"><span data-stu-id="aa4a3-137">Send a message</span></span>

<span data-ttu-id="aa4a3-138">若要发送短信，请指定你想要作为活动发送的字符串。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-138">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="aa4a3-139">在机器人的活动处理程序中，使用 turn context 对象的方法发送 `SendActivityAsync` 单个消息响应。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-139">In the bot's activity handler, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="aa4a3-140">使用 对象的 `SendActivitiesAsync` 方法一次发送多个响应。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-140">Use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="aa4a3-141">以下代码显示向对话中添加用户时发送邮件的示例：</span><span class="sxs-lookup"><span data-stu-id="aa4a3-141">The following code shows an example of sending a message when a user is added to a conversation:</span></span>

<span data-ttu-id="aa4a3-142">以下代码显示发送邮件的示例：</span><span class="sxs-lookup"><span data-stu-id="aa4a3-142">The following code shows an example of sending a message:</span></span>

# <a name="c"></a>[<span data-ttu-id="aa4a3-143">C#</span><span class="sxs-lookup"><span data-stu-id="aa4a3-143">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="aa4a3-144">TypeScript</span><span class="sxs-lookup"><span data-stu-id="aa4a3-144">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="aa4a3-145">Python</span><span class="sxs-lookup"><span data-stu-id="aa4a3-145">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="aa4a3-146">JSON</span><span class="sxs-lookup"><span data-stu-id="aa4a3-146">JSON</span></span>](#tab/json)

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
> <span data-ttu-id="aa4a3-147">在同一活动有效负载中发送短信和附件时，将发生邮件拆分。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-147">Message splitting occurs when a text message and an attachment are sent in the same activity payload.</span></span> <span data-ttu-id="aa4a3-148">此活动由 Microsoft Teams 拆分为单独的活动，一个仅包含一条短信，另一个包含附件。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-148">This activity is split into separate activities by Microsoft Teams, one with just a text message and the other with an attachment.</span></span> <span data-ttu-id="aa4a3-149">拆分活动时，您不会收到响应消息 ID，该 ID 用于主动更新或删除[](~/bots/how-to/update-and-delete-bot-messages.md)邮件。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-149">As the activity is split, you do not receive the message ID in response, which is used to [update or delete](~/bots/how-to/update-and-delete-bot-messages.md) the message proactively.</span></span> <span data-ttu-id="aa4a3-150">建议发送单独的活动，而不是根据邮件拆分。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-150">It is recommended to send separate activities instead of depending on message splitting.</span></span>

<span data-ttu-id="aa4a3-151">在用户和机器人之间发送的消息包含邮件中的内部通道数据。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-151">Messages sent between users and bots include internal channel data within the message.</span></span> <span data-ttu-id="aa4a3-152">此数据允许机器人在此频道上正常通信。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-152">This data allows the bot to communicate properly on that channel.</span></span> <span data-ttu-id="aa4a3-153">Bot Builder SDK 允许你修改消息结构。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-153">The Bot Builder SDK allows you to modify the message structure.</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="aa4a3-154">Teams 频道数据</span><span class="sxs-lookup"><span data-stu-id="aa4a3-154">Teams channel data</span></span>

<span data-ttu-id="aa4a3-155">对象 `channelData` 包含特定于 Teams 的信息，是团队和频道 ID 的权威性来源。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-155">The `channelData` object contains Teams-specific information and is a definitive source for team and channel IDs.</span></span> <span data-ttu-id="aa4a3-156">（可选）你可以缓存这些 ID 并用作本地存储的密钥。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-156">Optionally, you can cache and use these IDs as keys for local storage.</span></span> <span data-ttu-id="aa4a3-157">SDK 中的 通常从 对象提取重要信息， `TeamsActivityHandler` `channelData` 使其易于访问。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-157">The `TeamsActivityHandler` in the SDK typically pulls out important information from the `channelData` object to make it easily accessible.</span></span> <span data-ttu-id="aa4a3-158">但是，您始终可以从对象访问 `turnContext` 原始数据。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-158">However, you can always access the original data from the `turnContext` object.</span></span>

<span data-ttu-id="aa4a3-159">`channelData`对象不包含在个人对话中的邮件中，因为邮件在频道外发生。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-159">The `channelData` object is not included in messages in personal conversations, as these take place outside of a channel.</span></span>

<span data-ttu-id="aa4a3-160">发送给 `channelData` 自动程序的活动中的典型对象包含以下信息：</span><span class="sxs-lookup"><span data-stu-id="aa4a3-160">A typical `channelData` object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="aa4a3-161">`eventType`：仅在频道修改事件的情况下传递的 Teams [事件类型](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-161">`eventType`: Teams event type passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="aa4a3-162">`tenant.id`：在所有上下文中传递的 Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-162">`tenant.id`: Azure Active Directory tenant ID passed in all contexts.</span></span>
* <span data-ttu-id="aa4a3-163">`team`：仅在频道上下文中传递，而不是在个人聊天中传递。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-163">`team`: Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="aa4a3-164">`id`：通道的 GUID。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-164">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="aa4a3-165">`name`：仅在团队重命名事件的情况下传递 [的团队名称](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-165">`name`: Name of the team passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="aa4a3-166">`channel`：仅在提到自动程序时在频道上下文中传递，或针对团队中已添加自动程序的团队中的事件传递。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-166">`channel`: Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="aa4a3-167">`id`：通道的 GUID。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-167">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="aa4a3-168">`name`：仅在通道修改事件的情况下传递 [的频道名称](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-168">`name`: Channel name passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="aa4a3-169">`channelData.teamsTeamId`：已弃用。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-169">`channelData.teamsTeamId`: Deprecated.</span></span> <span data-ttu-id="aa4a3-170">此属性仅包含用于向后兼容。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-170">This property is only included for backward compatibility.</span></span>
* <span data-ttu-id="aa4a3-171">`channelData.teamsChannelId`：已弃用。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-171">`channelData.teamsChannelId`: Deprecated.</span></span> <span data-ttu-id="aa4a3-172">此属性仅包含用于向后兼容。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-172">This property is only included for backward compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="aa4a3-173">channelCreated 事件 (channelCreated 事件示例) </span><span class="sxs-lookup"><span data-stu-id="aa4a3-173">Example channelData object (channelCreated event)</span></span>

<span data-ttu-id="aa4a3-174">以下代码显示了 channelData 对象的示例：</span><span class="sxs-lookup"><span data-stu-id="aa4a3-174">The following code shows an example of channelData object:</span></span>

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

<span data-ttu-id="aa4a3-175">从自动程序接收或发送到自动程序的邮件可以包括不同类型的邮件内容。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-175">Messages received from or sent to your bot can include different types of message content.</span></span>

## <a name="message-content"></a><span data-ttu-id="aa4a3-176">邮件内容</span><span class="sxs-lookup"><span data-stu-id="aa4a3-176">Message content</span></span>

<span data-ttu-id="aa4a3-177">机器人可以发送格式文本、图片和卡片。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-177">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="aa4a3-178">用户可以向自动程序发送格式文本和图片。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-178">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="aa4a3-179">格式</span><span class="sxs-lookup"><span data-stu-id="aa4a3-179">Format</span></span>    | <span data-ttu-id="aa4a3-180">从用户到机器人</span><span class="sxs-lookup"><span data-stu-id="aa4a3-180">From user to bot</span></span> | <span data-ttu-id="aa4a3-181">从自动程序到用户</span><span class="sxs-lookup"><span data-stu-id="aa4a3-181">From bot to user</span></span> | <span data-ttu-id="aa4a3-182">注释</span><span class="sxs-lookup"><span data-stu-id="aa4a3-182">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="aa4a3-183">格式文本 </span><span class="sxs-lookup"><span data-stu-id="aa4a3-183">Rich text</span></span> | <span data-ttu-id="aa4a3-184">✔</span><span class="sxs-lookup"><span data-stu-id="aa4a3-184">✔</span></span>                | <span data-ttu-id="aa4a3-185">✔</span><span class="sxs-lookup"><span data-stu-id="aa4a3-185">✔</span></span>                |                                                                                         |
| <span data-ttu-id="aa4a3-186">图片</span><span class="sxs-lookup"><span data-stu-id="aa4a3-186">Pictures</span></span>  | <span data-ttu-id="aa4a3-187">✔</span><span class="sxs-lookup"><span data-stu-id="aa4a3-187">✔</span></span>                | <span data-ttu-id="aa4a3-188">✔</span><span class="sxs-lookup"><span data-stu-id="aa4a3-188">✔</span></span>                | <span data-ttu-id="aa4a3-189">PNG、JPEG 或 GIF 格式×最大为 1024×1024 和 1 MB。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-189">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="aa4a3-190">不支持动态 GIF。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-190">Animated GIF is not supported.</span></span>  |
| <span data-ttu-id="aa4a3-191">卡</span><span class="sxs-lookup"><span data-stu-id="aa4a3-191">Cards</span></span>     | <span data-ttu-id="aa4a3-192">✖</span><span class="sxs-lookup"><span data-stu-id="aa4a3-192">✖</span></span>                | <span data-ttu-id="aa4a3-193">✔</span><span class="sxs-lookup"><span data-stu-id="aa4a3-193">✔</span></span>                | <span data-ttu-id="aa4a3-194">有关受支持的 [卡片，](~/task-modules-and-cards/cards/cards-reference.md) 请参阅 Teams 卡参考。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-194">See the [Teams card reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards.</span></span> |
| <span data-ttu-id="aa4a3-195">表情符号</span><span class="sxs-lookup"><span data-stu-id="aa4a3-195">Emojis</span></span>    | <span data-ttu-id="aa4a3-196">✖</span><span class="sxs-lookup"><span data-stu-id="aa4a3-196">✖</span></span>                | <span data-ttu-id="aa4a3-197">✔</span><span class="sxs-lookup"><span data-stu-id="aa4a3-197">✔</span></span>                | <span data-ttu-id="aa4a3-198">Teams 当前支持通过 UTF-16 使用表情符号，例如 U+1F600，用于表情符号。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-198">Teams currently supports emojis through UTF-16, such as U+1F600 for grinning face.</span></span> |

<span data-ttu-id="aa4a3-199">您还可以使用 属性向邮件添加 `Notification.Alert` 通知。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-199">You can also add notifications to your message using the `Notification.Alert` property.</span></span>

## <a name="notifications-to-your-message"></a><span data-ttu-id="aa4a3-200">邮件通知</span><span class="sxs-lookup"><span data-stu-id="aa4a3-200">Notifications to your message</span></span>

<span data-ttu-id="aa4a3-201">通知会提醒用户有关新任务、提及和评论。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-201">Notifications alert users about new tasks, mentions, and comments.</span></span> <span data-ttu-id="aa4a3-202">这些警报与用户正在处理或必须通过向活动源中插入通知来查看内容相关。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-202">These alerts are related to what users are working on or what they must look at by inserting a notice into their activity feed.</span></span> <span data-ttu-id="aa4a3-203">对于从自动程序消息触发的通知，将 `TeamsChannelData` objects `Notification.Alert` 属性设置为 true。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-203">For notifications to trigger from your bot message, set the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="aa4a3-204">是否引发通知取决于单个用户的 Teams 设置，你无法替代这些设置。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-204">Whether or not a notification is raised depends on the individual user's Teams settings and you cannot override these settings.</span></span> <span data-ttu-id="aa4a3-205">通知类型是横幅或横幅和电子邮件。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-205">The notification type is either a banner or both a banner and an email.</span></span>

> [!NOTE]
> <span data-ttu-id="aa4a3-206">" **摘要"** 字段将来自用户的任何文本显示为源中的通知消息。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-206">The **Summary** field displays any text from the user as a notification message in the feed.</span></span>

<span data-ttu-id="aa4a3-207">以下代码显示向邮件添加通知的示例：</span><span class="sxs-lookup"><span data-stu-id="aa4a3-207">The following code shows an example of adding notifications to your message:</span></span>

# <a name="c"></a>[<span data-ttu-id="aa4a3-208">C#</span><span class="sxs-lookup"><span data-stu-id="aa4a3-208">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescript"></a>[<span data-ttu-id="aa4a3-209">TypeScript</span><span class="sxs-lookup"><span data-stu-id="aa4a3-209">TypeScript</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="aa4a3-210">Python</span><span class="sxs-lookup"><span data-stu-id="aa4a3-210">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="aa4a3-211">JSON</span><span class="sxs-lookup"><span data-stu-id="aa4a3-211">JSON</span></span>](#tab/json)

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

<span data-ttu-id="aa4a3-212">若要增强邮件功能，可以将图片作为邮件附件进行添加。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-212">To enhance your message, you can include pictures as attachments to that message.</span></span>

## <a name="picture-messages"></a><span data-ttu-id="aa4a3-213">图片消息</span><span class="sxs-lookup"><span data-stu-id="aa4a3-213">Picture messages</span></span>

<span data-ttu-id="aa4a3-214">图片通过向邮件添加附件来发送。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-214">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="aa4a3-215">有关附件详细信息，请参阅 [Bot Framework 文档](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-215">For more information on attachments, see [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).</span></span>

<span data-ttu-id="aa4a3-216">图片可以是最多 1024×1024 和 1 MB PNG、 JPEG 或 GIF 格式。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-216">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="aa4a3-217">不支持动态 GIF。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-217">Animated GIF is not supported.</span></span>

<span data-ttu-id="aa4a3-218">使用 XML 指定每个图像的高度和宽度。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-218">Specify the height and width of each image by using XML.</span></span> <span data-ttu-id="aa4a3-219">在 markdown 中，图像大小默认为 256×256。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-219">In markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="aa4a3-220">例如：</span><span class="sxs-lookup"><span data-stu-id="aa4a3-220">For example:</span></span>

* <span data-ttu-id="aa4a3-221">使用 `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` ：。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-221">Use: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.</span></span>
* <span data-ttu-id="aa4a3-222">请勿使用 `![Duck on a rock](http://aka.ms/Fo983c)` ：。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-222">Do not use: `![Duck on a rock](http://aka.ms/Fo983c)`.</span></span>

<span data-ttu-id="aa4a3-223">对话机器人可以包含可简化业务工作流的自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-223">A conversational bot can include adaptive cards that simplify business workflows.</span></span> <span data-ttu-id="aa4a3-224">自适应卡片提供丰富的可自定义文本、语音、图像、按钮和输入字段。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-224">Adaptive cards offer rich customizable text, speech, images, buttons, and input fields.</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="aa4a3-225">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="aa4a3-225">Adaptive cards</span></span>

<span data-ttu-id="aa4a3-226">自适应卡片可以在机器人中创作，并可在多个应用（如 Teams、网站等）中显示。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-226">Adaptive cards can be authored in a bot and shown in multiple apps such as Teams, your website, and so on.</span></span> <span data-ttu-id="aa4a3-227">有关详细信息，请参阅 [自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-227">For more information, see [adaptive cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>

<span data-ttu-id="aa4a3-228">以下代码显示发送简单自适应卡片的示例：</span><span class="sxs-lookup"><span data-stu-id="aa4a3-228">The following code shows an example of sending a simple adaptive card:</span></span>

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

<span data-ttu-id="aa4a3-229">若要了解有关机器人中的卡和卡的更多信息，请参阅 [卡片文档](~/task-modules-and-cards/what-are-cards.md)。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-229">To know more about cards and cards in bots, see [cards documentation](~/task-modules-and-cards/what-are-cards.md).</span></span>

<span data-ttu-id="aa4a3-230">下一节提供自动程序 API 生成的错误的状态代码响应。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-230">The next section provides status code responses for errors generated from Bot APIs.</span></span>

## <a name="status-code-responses"></a><span data-ttu-id="aa4a3-231">状态代码响应</span><span class="sxs-lookup"><span data-stu-id="aa4a3-231">Status code responses</span></span>

<span data-ttu-id="aa4a3-232">以下是状态代码及其错误代码和消息值：</span><span class="sxs-lookup"><span data-stu-id="aa4a3-232">Following are the status codes and their error code and message values:</span></span>

| <span data-ttu-id="aa4a3-233">状态代码</span><span class="sxs-lookup"><span data-stu-id="aa4a3-233">Status code</span></span> | <span data-ttu-id="aa4a3-234">错误代码和消息值</span><span class="sxs-lookup"><span data-stu-id="aa4a3-234">Error code and message values</span></span> | <span data-ttu-id="aa4a3-235">Description</span><span class="sxs-lookup"><span data-stu-id="aa4a3-235">Description</span></span> |
|----------------|-----------------|-----------------|
| <span data-ttu-id="aa4a3-236">403</span><span class="sxs-lookup"><span data-stu-id="aa4a3-236">403</span></span> | <span data-ttu-id="aa4a3-237">**代码**： `ConversationBlockedByUser`</span><span class="sxs-lookup"><span data-stu-id="aa4a3-237">**Code**: `ConversationBlockedByUser`</span></span> <br/> <span data-ttu-id="aa4a3-238">**消息**："用户阻止了与机器人的对话。"</span><span class="sxs-lookup"><span data-stu-id="aa4a3-238">**Message**: "User blocked the conversation with the bot."</span></span> | <span data-ttu-id="aa4a3-239">用户通过审核设置在一对一聊天或频道中阻止机器人。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-239">User blocked the bot in 1:1 chat or a channel through moderation settings.</span></span> |
| <span data-ttu-id="aa4a3-240">403</span><span class="sxs-lookup"><span data-stu-id="aa4a3-240">403</span></span> | <span data-ttu-id="aa4a3-241">**代码**： `BotNotInConversationRoster`</span><span class="sxs-lookup"><span data-stu-id="aa4a3-241">**Code**: `BotNotInConversationRoster`</span></span> <br/> <span data-ttu-id="aa4a3-242">**消息**："机器人不是对话名单中的一部分。"</span><span class="sxs-lookup"><span data-stu-id="aa4a3-242">**Message**: "The bot is not part of the conversation roster."</span></span> | <span data-ttu-id="aa4a3-243">机器人不是对话的一部分。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-243">The bot is not part of the conversation.</span></span> |
| <span data-ttu-id="aa4a3-244">403</span><span class="sxs-lookup"><span data-stu-id="aa4a3-244">403</span></span> | <span data-ttu-id="aa4a3-245">**代码**： `BotDisabledByAdmin`</span><span class="sxs-lookup"><span data-stu-id="aa4a3-245">**Code**: `BotDisabledByAdmin`</span></span> <br/> <span data-ttu-id="aa4a3-246">**消息**："租户管理员已禁用此机器人。"</span><span class="sxs-lookup"><span data-stu-id="aa4a3-246">**Message**: "The tenant admin disabled this bot."</span></span> | <span data-ttu-id="aa4a3-247">租户阻止了机器人。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-247">Tenant blocked the bot.</span></span> |
| <span data-ttu-id="aa4a3-248">401</span><span class="sxs-lookup"><span data-stu-id="aa4a3-248">401</span></span> | <span data-ttu-id="aa4a3-249">**代码**： `BotNotRegistered`</span><span class="sxs-lookup"><span data-stu-id="aa4a3-249">**Code**: `BotNotRegistered`</span></span> <br/> <span data-ttu-id="aa4a3-250">**消息**："未找到此自动程序注册。"</span><span class="sxs-lookup"><span data-stu-id="aa4a3-250">**Message**: “No registration found for this bot.”</span></span> | <span data-ttu-id="aa4a3-251">未找到此自动程序注册。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-251">The registration for this bot was not found.</span></span> |
| <span data-ttu-id="aa4a3-252">412</span><span class="sxs-lookup"><span data-stu-id="aa4a3-252">412</span></span> | <span data-ttu-id="aa4a3-253">**代码**： `PreconditionFailed`</span><span class="sxs-lookup"><span data-stu-id="aa4a3-253">**Code**: `PreconditionFailed`</span></span> <br/> <span data-ttu-id="aa4a3-254">**消息**："先决条件失败，请重试。"</span><span class="sxs-lookup"><span data-stu-id="aa4a3-254">**Message**: “Precondition failed, please try again.”</span></span> | <span data-ttu-id="aa4a3-255">由于同一对话上的多个并发操作，某一依赖项的前提条件失败。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-255">A precondition failed on one of our dependencies due to multiple concurrent operations on the same conversation.</span></span> |
| <span data-ttu-id="aa4a3-256">404</span><span class="sxs-lookup"><span data-stu-id="aa4a3-256">404</span></span> | <span data-ttu-id="aa4a3-257">**代码**： `ConversationNotFound`</span><span class="sxs-lookup"><span data-stu-id="aa4a3-257">**Code**: `ConversationNotFound`</span></span> <br/> <span data-ttu-id="aa4a3-258">**消息**："未找到对话"。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-258">**Message**: “Conversation not found.”</span></span> | <span data-ttu-id="aa4a3-259">未找到对话。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-259">The conversation was not found.</span></span> |
| <span data-ttu-id="aa4a3-260">413</span><span class="sxs-lookup"><span data-stu-id="aa4a3-260">413</span></span> | <span data-ttu-id="aa4a3-261">**代码**： `MessageSizeTooBig`</span><span class="sxs-lookup"><span data-stu-id="aa4a3-261">**Code**: `MessageSizeTooBig`</span></span> <br/> <span data-ttu-id="aa4a3-262">**邮件**："邮件大小太大。"</span><span class="sxs-lookup"><span data-stu-id="aa4a3-262">**Message**: “Message size too large.”</span></span> | <span data-ttu-id="aa4a3-263">传入请求的大小太大。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-263">The size on the incoming request was too large.</span></span> |
| <span data-ttu-id="aa4a3-264">429</span><span class="sxs-lookup"><span data-stu-id="aa4a3-264">429</span></span> | <span data-ttu-id="aa4a3-265">**代码**： `Throttled`</span><span class="sxs-lookup"><span data-stu-id="aa4a3-265">**Code**: `Throttled`</span></span> <br/> <span data-ttu-id="aa4a3-266">**消息**："请求过多。"</span><span class="sxs-lookup"><span data-stu-id="aa4a3-266">**Message**: “Too many requests.”</span></span> <span data-ttu-id="aa4a3-267">还返回在之后重试时间。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-267">Also returns when to retry after.</span></span> | <span data-ttu-id="aa4a3-268">机器人发送的请求过多。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-268">Too many requests were sent by the bot.</span></span> <span data-ttu-id="aa4a3-269">有关详细信息，请参阅速率 [限制](~/bots/how-to/rate-limit.md)。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-269">For more information, see [rate limit](~/bots/how-to/rate-limit.md).</span></span> |

<span data-ttu-id="aa4a3-270">下一节演示了一个简单的代码示例，该示例将基本对话流合并到 Teams 应用程序中。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-270">The next section illustrates a simple code sample that incorporates basic conversational flow into a Teams application.</span></span>

## <a name="code-sample"></a><span data-ttu-id="aa4a3-271">代码示例</span><span class="sxs-lookup"><span data-stu-id="aa4a3-271">Code sample</span></span>

<span data-ttu-id="aa4a3-272">以下是 Teams 对话机器人的代码示例：</span><span class="sxs-lookup"><span data-stu-id="aa4a3-272">Following are the code samples for Teams conversation bot:</span></span>

|<span data-ttu-id="aa4a3-273">示例名称</span><span class="sxs-lookup"><span data-stu-id="aa4a3-273">Sample name</span></span> | <span data-ttu-id="aa4a3-274">Description</span><span class="sxs-lookup"><span data-stu-id="aa4a3-274">Description</span></span> | <span data-ttu-id="aa4a3-275">.NETCore</span><span class="sxs-lookup"><span data-stu-id="aa4a3-275">.NETCore</span></span> | <span data-ttu-id="aa4a3-276">Node.js</span><span class="sxs-lookup"><span data-stu-id="aa4a3-276">Node.js</span></span> | <span data-ttu-id="aa4a3-277">Python</span><span class="sxs-lookup"><span data-stu-id="aa4a3-277">Python</span></span> |
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="aa4a3-278">Teams 对话自动程序</span><span class="sxs-lookup"><span data-stu-id="aa4a3-278">Teams conversation bot</span></span> | <span data-ttu-id="aa4a3-279">消息和对话事件处理。</span><span class="sxs-lookup"><span data-stu-id="aa4a3-279">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="aa4a3-280">View</span><span class="sxs-lookup"><span data-stu-id="aa4a3-280">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="aa4a3-281">View</span><span class="sxs-lookup"><span data-stu-id="aa4a3-281">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="aa4a3-282">View</span><span class="sxs-lookup"><span data-stu-id="aa4a3-282">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="see-also"></a><span data-ttu-id="aa4a3-283">另请参阅</span><span class="sxs-lookup"><span data-stu-id="aa4a3-283">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa4a3-284">发送主动邮件</span><span class="sxs-lookup"><span data-stu-id="aa4a3-284">Send proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="aa4a3-285">订阅对话事件</span><span class="sxs-lookup"><span data-stu-id="aa4a3-285">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="next-step"></a><span data-ttu-id="aa4a3-286">后续步骤</span><span class="sxs-lookup"><span data-stu-id="aa4a3-286">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa4a3-287">自动程序命令菜单</span><span class="sxs-lookup"><span data-stu-id="aa4a3-287">Bot command menus</span></span>](~/bots/how-to/create-a-bot-commands-menu.md)
