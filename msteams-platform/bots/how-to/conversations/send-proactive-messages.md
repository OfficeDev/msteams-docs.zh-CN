---
title: 发送主动邮件
description: 介绍如何使用 Microsoft Teams 自动程序发送主动消息。
ms.topic: overview
ms.author: anclear
Keywords: 发送消息获取用户 ID 通道 ID 对话 ID
ms.openlocfilehash: 2d7ff10469a181bb06fda5029c8f6b2725b0402d
ms.sourcegitcommit: 7db6eabe3ef128ac7f14b32d07e9e86c995d187f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/04/2021
ms.locfileid: "50103603"
---
# <a name="send-proactive-messages"></a>发送主动邮件

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

主动消息是自动程序发送的任何消息，不直接响应用户的请求。 这可能包括如下消息：

* 欢迎消息
* 通知
* 计划邮件

若要让机器人发送主动消息，它必须有权访问要发送消息的用户、群聊或团队。 对于群聊或团队，这意味着必须先将包含机器人的应用安装到该位置。 如果需要[，可以在](#proactively-install-your-app-using-graph)团队中主动使用 Graph 安装应用，或使用应用策略将应用[](/microsoftteams/teams-custom-app-policies-and-settings)推送到租户中的团队和用户。 对于用户，必须为用户安装你的应用，或者用户必须是安装了应用的团队的一部分。

发送主动邮件与发送常规邮件不同。 在这一方面，没有用于 `turnContext` 答复的活动。 在发送邮件之前，您可能还需要创建对话。 例如，频道中的新一对一聊天或新对话线程。 无法在具有主动消息的团队中创建新的群聊或新频道。

在高级别上，发送主动消息需要完成的步骤包括：

1. [如果需要，请](#get-the-user-id-or-teamchannel-id) 获取用户 ID 或团队/ (id) 。
1. [根据需要创建对话或 (](#create-the-conversation) 线程) 。
1. [获取对话 ID。](#get-the-conversation-id)
1. [发送邮件](#send-the-message)。

示例部分的代码段用于创建一[](#examples)对一对话。 有关一对一对话和组或频道的完整工作示例的链接，请参阅 [代码示例](#code-samples)。

## <a name="get-the-user-id-or-teamchannel-id"></a>获取用户 ID 或团队/频道 ID

若要在频道中创建新对话或对话线程，你需要正确的 ID。 可以通过多种方式接收或检索此 ID：

1. 当你的应用安装在任何特定上下文中时，你将收到一个[ `onMembersAdded` 活动](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
1. 将新用户添加到安装你的应用的上下文中时，你将收到[ `onMembersAdded` 一个活动](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
1. 你可以检索 [已安装应用的](~/bots/how-to/get-teams-context.md) 团队中的频道列表。
1. 你可以检索 [已安装应用的](~/bots/how-to/get-teams-context.md) 团队成员列表。
1. 机器人收到的每个活动都必须包含所需信息。

无论你如何获取信息，你都需要存储和 `tenantId` / `userId` 或 `channelId` 创建新对话。 您还可以使用 在团队的常规频道或默认频道中 `teamId` 创建新的对话线程。

它是你的机器人 ID 和特定用户所特有的， `userId` 你无法在机器人之间重新使用它们。 这是全局的，但是，必须先在团队中安装自动程序 `channelId` ，然后才能向频道发送主动消息。

## <a name="create-the-conversation"></a>创建对话

获得用户或频道信息后，如果对话不存在或不知道对话，则需要创建 `conversationId` 对话。 只能创建对话一次，并确保存储要 `conversationId` 在将来使用 `conversationReference` 的值或对象。

## <a name="get-the-conversation-id"></a>获取对话 ID

创建对话后，使用 `conversationReference` 对象或 `conversationId` `tenantId` 发送邮件。 可以通过创建对话或从该上下文发送给你的任何活动存储此 ID。 确保存储此 ID。

## <a name="send-the-message"></a>发送邮件

现在，您具有正确的地址信息，您可以发送邮件。 如果你使用的是 SDK，你将使用该方法以及进行直接 `continueConversation` `conversationId` API `tenantId` 调用。 必须正确 `conversationParameters` 设置，以成功发送邮件。 请参阅 [示例](#examples) 部分或使用代码示例部分中列出的示例 [之一](#code-samples) 。

## <a name="best-practices-for-proactive-messaging"></a>主动消息传递的最佳实践

向用户发送主动邮件是一种与用户通信的有效方式。 但是，从他们的角度来看，此消息可能看起来完全不一样，对于欢迎消息，这是他们第一次与你的应用交互。 因此，请谨慎使用此功能，不要向用户发送垃圾邮件，并提供足够信息，让用户了解为何收到邮件，这一点非常重要。

### <a name="welcome-messages"></a>欢迎消息

使用主动消息向用户发送欢迎消息时，必须记住，对于大多数接收邮件的人，他们接收邮件的原因没有上下文。 这也是他们第一次与你的应用交互。 可以创造良好的第一印象。 最佳欢迎消息必须包括：

* **用户接收邮件的原因。** 用户必须非常清楚地了解他们接收邮件的原因。 如果你的自动程序安装在频道中，并且你向所有用户发送了欢迎消息，请让他们知道它安装在什么频道中以及可能安装它的人。
* **你提供什么。** 他们可以对你的应用做什么？ 你可以为它们带来什么价值？
* **接下来，他们该怎么办。** 邀请他们试用命令，或以某种方式与你的应用交互。

请记住，较差的欢迎消息可能会导致用户阻止机器人。 花费大量时间精心制作欢迎消息，如果它们没有达到预期效果，请对它们进行一次访问。

### <a name="notification-messages"></a>通知邮件

使用主动消息发送通知时，必须确保用户有一个清晰的路径，可以基于你的通知采取常见操作，并明确了解通知发生的原因。 良好的通知消息通常包括：

* **发生了什么事。** 导致通知发生的原因的清晰指示。
* **结果是什么。** 必须清楚哪些项或内容已更新，以引发通知。
* **触发它的人/人。** 导致发送通知的谁或采取什么操作。
* **用户可以在响应中执行哪些功能。** 让用户能够轻松根据通知采取操作。
* **用户如何选择退出。** 你必须为用户提供选择退出其他通知的路径。

## <a name="proactively-install-your-app-using-graph"></a>使用 Graph 主动安装应用

> [!Note]
> 目前，使用 Microsoft Graph 主动安装应用处于 beta 阶段。

有时，可能需要主动向之前未安装或与你的应用交互的用户发送消息。 例如，您希望使用公司通信 [器向](~/samples/app-templates.md#company-communicator) 整个组织发送邮件。 对于此方案，可以使用 Graph API 主动为用户安装应用，然后缓存应用在安装时收到 `conversationUpdate` 的事件所需的值。

只能安装组织应用目录或 Teams 应用商店中的应用。

请参阅 [Graph 文档中的用户应用](/graph/api/userteamwork-post-installedapps) ，以及使用 Microsoft Graph 在 Teams 中主动安装 [机器人和消息传递](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)。 GitHub 平台上还有一个 [Microsoft .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) 框架示例。

## <a name="examples"></a>示例

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

必须提供用户 ID 和租户 ID。 如果调用成功，API 将返回以下响应对象。

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-samples"></a>代码示例

官方主动消息示例如下所示：

| 示例名称           | 说明                                                                      | .NET    | JavaScript   | Python  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|Teams 对话基础知识  | 演示 Teams 中对话的基础知识，包括发送一对一主动消息。|[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|在频道中启动新线程     | 演示在频道中创建新线程。 |[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a>查看其他代码示例
>
> [!div class="nextstepaction"]
> [**Teams 主动邮件代码示例**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
