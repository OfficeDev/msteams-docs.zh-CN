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
# <a name="send-proactive-messages"></a>发送主动邮件

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

主动消息是自动程序发送的任何不响应用户请求的消息。 这可能包括邮件，例如：

* 欢迎消息
* 通知
* 计划邮件

若要让机器人向用户、群聊或团队发送主动消息，它必须具有发送消息的访问权限。 对于群聊或团队，必须先将包含机器人的应用安装在该位置。 如果需要[，可在团队](#proactively-install-your-app-using-graph)中主动使用 Microsoft Graph 安装应用，或使用应用策略将应用[](/microsoftteams/teams-custom-app-policies-and-settings)推送到租户中的团队和用户。 对于用户，必须为用户安装你的应用，或者用户必须是安装应用的团队的一部分。

发送主动邮件与发送常规邮件不同。 没有用于 `turnContext` 答复的活动。 在发送邮件之前，必须创建对话。 例如，频道中的新一对一聊天或新对话线程。 不能在具有主动消息的团队中创建新的群聊或新频道。

**发送主动邮件**

1. [如果需要，获取用户 ID、团队 ID 或频道 ID。](#get-the-user-id-team-id-or-channel-id)
1. [创建对话](#create-the-conversation)（如果需要）。
1. [获取对话 ID](#get-the-conversation-id)。
1. [发送邮件](#send-the-message)。

示例部分的代码段用于创建一[](#samples)对一对话。 有关一对一对话和组或频道的完整工作示例的链接，请参阅 [代码示例](#code-sample)。

要有效地使用主动邮件，请参阅 [主动邮件的最佳实践](#best-practices-for-proactive-messaging)。 对于某些方案，你必须使用 Graph 主动 [安装应用](#proactively-install-your-app-using-graph)。 示例部分的代码段用于创建一[](#samples)对一对话。 有关一对一对话以及组或频道的完整工作示例，请参阅 [代码示例](#code-sample)。

## <a name="get-the-user-id-team-id-or-channel-id"></a>获取用户 ID、团队 ID 或频道 ID

若要在频道中创建新对话或对话线程，必须具有正确的 ID。 可以使用以下任一项接收或检索此 ID：

* 当你的应用安装在任何特定上下文中时，你会收到一个[ `onMembersAdded` 活动](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
* 将新用户添加到安装你的应用的上下文中时，你会收到一个[ `onMembersAdded` 活动](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
* 你可以检索 [安装了应用的](~/bots/how-to/get-teams-context.md) 团队中的频道列表。
* 你可以检索 [安装了应用的](~/bots/how-to/get-teams-context.md) 团队成员列表。
* 机器人收到的每个活动都必须包含所需信息。

无论如何获取信息，都必须存储 和 或 `tenantId` `userId` `channelId` 以创建新对话。 您还可以使用 在团队的常规频道或默认频道中创建新的 `teamId` 对话线程。

`userId`是自动程序 ID 和特定用户所特有的。 您不能在自动程序 `userId` 之间重复使用。 `channelId`是全局的。 但是，必须先在团队中安装自动程序，然后才能向频道发送主动消息。

获得用户或频道信息后，必须创建对话。

## <a name="create-the-conversation"></a>创建对话

如果对话不存在或您不知道 ，则必须创建 `conversationId` 对话。 只能创建一次对话并存储 `conversationId` 值或 `conversationReference` 对象。

创建对话后，必须获取对话 ID。

## <a name="get-the-conversation-id"></a>获取对话 ID

使用 `conversationReference` 对象或 `conversationId` 和 `tenantId` 发送邮件。 可以通过创建对话或从该上下文发送给你的任何活动存储此 ID 来获取此 ID。 存储此 ID 供参考。

获取相应的地址信息后，可以发送邮件。

## <a name="send-the-message"></a>发送邮件

现在，您具有正确的地址信息，您可以发送邮件。 如果你使用的是 SDK，你将使用 方法以及 和 进行直接 `continueConversation` `conversationId` API `tenantId` 调用。 必须正确设置 `conversationParameters` ，以成功发送邮件。 请参阅 [示例](#samples) 部分或使用代码示例部分中列出的示例 [之](#code-sample) 一。

如果使用的是 SDK，则必须使用 和 方法，并直接 `continueConversation` `conversationId` 调用 `tenantId` API 来发送消息。 必须正确设置 `conversationParameters` ，以成功发送邮件。

现在，你已发送主动邮件，在发送主动邮件时必须遵循这些最佳做法，以便用户和机器人之间更好地交换信息。

## <a name="best-practices-for-proactive-messaging"></a>主动邮件最佳做法

向用户发送主动邮件是一种与用户通信的有效方式。 但是，从他们的角度来看，此消息可能完全不提示，对于欢迎消息，这是他们第一次与你的应用交互。 因此，请谨慎使用主动邮件，而不是向用户发送垃圾邮件，并提供足够信息让用户了解接收邮件的原因，这一点非常重要。

### <a name="welcome-messages"></a>欢迎消息

当主动消息用于向用户发送欢迎消息时，用户收到邮件的原因没有上下文。 这也是用户第一次与你的应用交互。 这是创造良好的第一印象的机会。 最佳欢迎消息必须包括：

* 用户为什么收到邮件：用户必须非常清楚地了解他们接收邮件的原因。 如果你的机器人安装在频道中，并且你向所有用户发送了欢迎消息，请让他们知道它安装在什么频道以及谁安装了它。
* 你提供什么：用户必须能够确定他们可以对你的应用执行哪些操作，以及你可以为用户带来什么价值。
* 接下来应做什么：邀请用户试用命令，或与你的应用交互。

较差的欢迎消息可能会导致用户阻止机器人。 写入要点并清除欢迎消息。 如果欢迎消息没有达到预期效果，则对欢迎消息进行 Iterate。

### <a name="notification-messages"></a>通知消息

若要使用主动消息发送通知，请确保你的用户有一个清晰的路径，可以基于你的通知采取常见操作。 确保用户清楚地了解他们为何收到通知。 良好的通知消息通常包括以下内容：

* 发生的情况：关于导致通知发生的情况的清晰指示。
* 结果是什么：必须清楚更新了哪些项，以引发通知。
* 触发它的人或原因：导致发送通知的操作者或行为。
* 用户可在响应中执行哪些操作：使用户能够轻松根据通知采取操作。
* 用户如何选择退出：你必须为用户提供选择退出其他通知的路径。

若要向一大组用户发送消息（例如，发送到组织）请主动使用 Graph 安装应用。

### <a name="scheduled-messages"></a>计划邮件

使用主动消息向用户发送计划邮件时，请验证时区已更新到其时区。 这可确保在相关时间将邮件传递给用户。 计划邮件通常包括：

* 用户为什么收到邮件：让用户轻松了解收到邮件的原因。
* 用户接下来可以做什么：用户可以根据邮件内容采取所需操作。

## <a name="proactively-install-your-app-using-graph"></a>使用 Graph 主动安装应用

> [!Note]
> 使用 Graph 主动安装应用目前处于 beta 阶段。

主动向之前未安装或与你的应用交互的用户发送消息。 例如，您希望使用公司通信 [程序](~/samples/app-templates.md#company-communicator) 向整个组织发送邮件。 在这种情况下，可以使用 Graph API 主动为用户安装应用。 缓存应用在安装 `conversationUpdate` 时收到的事件所需的值。

只能安装组织应用目录或 Teams 应用商店中的应用。

请参阅 [Graph 文档中的为用户](/graph/api/userteamwork-post-installedapps) 安装应用，以及使用 Graph 在 Teams 中主动安装机器人 [和消息传递](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)。 GitHub 平台上还有一个 [Microsoft .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) 框架示例。

## <a name="samples"></a>示例

以下代码显示了一个简单的代码示例，该示例使用 Graph 主动安装你的应用：

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

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

# <a name="json"></a>[JSON](#tab/json)

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

必须提供用户 ID 和租户 ID。 如果调用成功，API 将返回以下 response 对象：

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-sample"></a>代码示例

下表提供了一个简单的代码示例，该示例将基本对话流合并到 Teams 应用程序中，以及如何在 Teams 中的频道中创建新的对话线程：

| **示例名称** | **描述** | **.NET** | **Node.js** | **Python** |
|---------------|--------------|--------|-------------|--------|
| Teams 对话基础知识  | 演示 Teams 中对话的基础知识，包括发送一对一主动消息。| [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| 在频道中启动新线程 | 演示在频道中创建新线程。 | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

### <a name="additional-code-sample"></a>其他代码示例

> [!div class="nextstepaction"]
> [Teams 主动邮件代码示例](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [**Teams 主动邮件代码示例**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp) 
> [设置自动程序消息的格式](~/bots/how-to/format-your-bot-messages.md)
