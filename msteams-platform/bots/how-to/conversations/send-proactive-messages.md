---
title: 发送主动邮件
description: 介绍如何使用 Microsoft Teams 自动程序发送主动邮件。
ms.topic: overview
ms.author: anclear
Keywords: 发送消息获取用户 ID 通道 ID 对话 ID
ms.openlocfilehash: 7da470eaba6ae9ecb82c9a7ba04d69b2f196a9d7
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654291"
---
# <a name="send-proactive-messages"></a>发送主动邮件

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

主动消息是自动程序发送的任何消息，不直接响应来自用户的请求。 这可能包括如下消息：

* 欢迎消息
* 通知
* 计划邮件

若要让机器人发送主动消息，它必须有权访问要发送消息的用户、群聊或团队。 对于群聊或团队，这意味着必须先将包含机器人的应用安装到该位置。 如果需要[，可以在团队](#proactively-install-your-app-using-graph)中主动使用 Graph 安装应用，或使用应用策略将应用[](/microsoftteams/teams-custom-app-policies-and-settings)推送到租户中的团队和用户。 对于用户，必须为用户安装你的应用，或者用户必须是安装应用的团队的一部分。

发送主动邮件与发送常规邮件不同。 在这种情况下，没有用于 `turnContext` 回复的活动。 在发送邮件之前，可能还需要创建对话。 例如，频道中的新一对一聊天或新对话线程。 不能在具有主动消息的团队中创建新的群聊或新频道。

在高级别上，发送主动消息需要完成的步骤包括：

1. [如果需要，请获取用户 ID 或团队/ (](#get-the-user-id-or-teamchannel-id) id) 。
1. [如果需要，请创建对话 (](#create-the-conversation) 对话线程) 。
1. [获取对话 ID](#get-the-conversation-id)。
1. [发送邮件](#send-the-message)。

示例部分的代码段用于创建一[](#examples)对一对话。 有关一对一对话和组或频道的完整工作示例的链接，请参阅 [代码示例](#code-samples)。

## <a name="get-the-user-id-or-teamchannel-id"></a>获取用户 ID 或团队/频道 ID

若要在频道中创建新对话或对话线程，你需要正确的 ID。 可以通过多种方式接收或检索此 ID：

1. 当你的应用安装在任何特定上下文中时，你将收到活动[ `onMembersAdded` 。](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
1. 将新用户添加到安装应用的上下文时，你将收到"活动[ `onMembersAdded` "。](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
1. 你可以检索 [已安装应用的](~/bots/how-to/get-teams-context.md) 团队中的频道列表。
1. 你可以检索 [已安装应用的](~/bots/how-to/get-teams-context.md) 团队成员列表。
1. 自动程序收到的每个活动都必须包含所需信息。

无论如何获取信息，都需要存储 和 或 `tenantId` `userId` `channelId` 以创建新对话。 您还可以使用 在团队的常规频道或默认频道中创建新的 `teamId` 对话线程。

对于自动程序 ID 和特定用户来说是唯一的，你无法在机器人之间 `userId` 重新使用它们。 是全局的，但是，必须先在团队中安装自动程序 `channelId` ，然后才能向频道发送主动消息。

## <a name="create-the-conversation"></a>创建对话

获得用户或频道信息后，如果对话不存在或不知道 ，则需要创建 `conversationId` 对话。 只能创建一次对话，并确保存储要在将来 `conversationId` `conversationReference` 使用的值或对象。

## <a name="get-the-conversation-id"></a>获取对话 ID

创建对话后，使用 `conversationReference` 对象 或 `conversationId` `tenantId` 发送邮件。 可以通过创建对话或从该上下文发送给你的任何活动存储此 ID 来获取此 ID。 确保存储此 ID。

## <a name="send-the-message"></a>发送邮件

现在，您具有正确的地址信息，您可以发送邮件。 如果你使用的是 SDK，你将使用 方法以及 和 进行直接 `continueConversation` `conversationId` API `tenantId` 调用。 必须正确设置 `conversationParameters` ，以成功发送邮件。 请参阅 [示例](#examples) 部分或使用代码示例部分中列出的示例 [之一](#code-samples) 。

## <a name="best-practices-for-proactive-messaging"></a>主动邮件最佳做法

向用户发送主动邮件是一种与用户通信的有效方式。 但是，从他们的角度来看，此消息可能完全不提示，对于欢迎消息，这是他们第一次与你的应用交互。 因此，请慎用此功能，不要向用户发送垃圾邮件，并提供足够信息让用户了解邮件的原因，这一点非常重要。

### <a name="welcome-messages"></a>欢迎消息

使用主动消息向用户发送欢迎消息时，必须记住，对于大多数接收邮件的人，他们接收邮件的原因没有上下文。 这也是他们第一次与你的应用交互。 可以创造良好的第一印象。 最佳欢迎消息必须包括：

* **用户为什么收到邮件。** 用户必须非常清楚地了解他们接收邮件的原因。 如果你的自动程序安装在频道中，并且你向所有用户发送了欢迎消息，请让他们知道它安装在什么频道以及可能安装它的人。
* **你提供什么功能。** 他们可以对你的应用执行哪些操作？ 您可以为它们带来什么价值？
* **接下来应执行哪些步骤。** 邀请他们试用命令，或以某种方式与你的应用交互。

请记住，较差的欢迎消息可能会导致用户阻止机器人。 花费大量时间精心制作欢迎消息，如果消息没有达到预期效果，请对消息进行一次访问。

### <a name="notification-messages"></a>通知消息

使用主动消息发送通知时，必须确保用户有一个清晰的路径，可以基于通知采取常见操作，并清楚了解通知发生的原因。 良好的通知消息通常包括：

* **发生了什么事。** 关于导致通知发生的情况的清晰指示。
* **结果是什么。** 必须清楚哪些项或内容已更新，以引发通知。
* **触发它的人/人。** 导致发送通知的操作人或执行什么操作。
* **用户可以在响应中做什么。** 让用户能够轻松根据通知采取操作。
* **用户如何选择退出。** 你必须为用户提供选择退出其他通知的路径。

### <a name="scheduled-messages"></a>计划邮件

使用主动消息向用户发送计划邮件时，请验证时区已更新到其时区。 这可确保在相关时间将邮件传递给用户。 计划邮件通常包括：

* **用户为什么收到邮件**：让用户轻松了解收到邮件的原因。
* **用户接下来可以做什么**：用户可以根据邮件内容采取所需操作。

## <a name="proactively-install-your-app-using-graph"></a>使用 Graph 主动安装应用

> [!Note]
> 使用 Microsoft Graph 主动安装应用目前处于 beta 阶段。

有时，可能需要主动向之前未安装或与你的应用交互的用户发送消息。 例如，您希望使用公司通信 [程序](~/samples/app-templates.md#company-communicator) 向整个组织发送邮件。 对于此方案，可以使用 Graph API 主动为用户安装应用，然后根据应用在安装时收到的事件缓存 `conversationUpdate` 必要的值。

只能安装组织应用目录或 Teams 应用商店中的应用。

请参阅 [Graph 文档中的为用户](/graph/api/userteamwork-post-installedapps) 安装应用，以及使用 Microsoft Graph 在 Teams 中主动安装 [机器人和消息传递](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)。 GitHub 平台上还有一个 [Microsoft .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) 框架示例。

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

必须提供用户 ID 和租户 ID。 如果调用成功，API 将返回以下 response 对象。

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-samples"></a>代码示例

官方主动邮件示例如下所示：

| 示例名称           | Description                                                                      | .NET    | JavaScript   | Python  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|Teams 对话基础知识  | 演示 Teams 中对话的基础知识，包括发送一对一主动消息。|[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|在频道中启动新线程     | 演示在频道中创建新线程。 |[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a>查看其他代码示例
>
> [!div class="nextstepaction"]
> [**Teams 主动邮件代码示例**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
