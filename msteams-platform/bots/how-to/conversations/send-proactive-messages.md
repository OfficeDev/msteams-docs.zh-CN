---
title: 发送主动邮件
description: 了解如何向 Microsoft Teams 机器人发送主动消息，使用 Microsoft Graph 主动安装应用，并根据 Bot Framework SDK v4 检查代码示例。
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: high
Keywords: 发送消息, 获取用户 ID、频道 ID、对话 ID
ms.openlocfilehash: fd3ed48022239aaa84e00c8b3b59701970d9a0af
ms.sourcegitcommit: aa95313cdab4fbf0a9f62a047ebbe6a5f1fbbf5d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2022
ms.locfileid: "65602269"
---
# <a name="proactive-messages"></a>主动邮件

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

主动消息是由机器人发送的、不响应用户请求的任何消息。可以包含多种消息，例如:

* 欢迎消息
* Notifications
* 计划的消息

> [!IMPORTANT]
> 目前，机器人在政府社区云（GCC）和 GCC-High 中可用，但在国防部（DOD）中不可用。
>
> 对于主动消息，机器人应将以下终结点用于政府云环境：
>    * GCC: `https://smba.infra.gcc.teams.microsoft.com/gcc`。
>    * GCCH: `https://smba.infra.gov.teams.microsoft.us/gcch`。

若要让机器人向用户、群聊或团队发送主动消息，它必须具有发送消息的权限。 对于群聊或团队，必须先将包含机器人的应用安装在该位置。
如果需要，你可以在团队中[使用 Microsoft Graph 主动安装应用](#proactively-install-your-app-using-graph)，或使用[应用策略](/microsoftteams/teams-custom-app-policies-and-settings)将应用推送给租户中的团队和用户。 对于用户，必须为你的用户安装应用，或者该用户必须是安装应用的团队的成员。

发送主动消息与发送常规消息不同。 没有用于回复的活动 `turnContext`。 在发送消息之前，你必须先创建对话。 例如，频道中的新一对一聊天或新对话线程。 你不能在具有主动消息传递的团队中创建新的群聊或新频道。

若要发送主动邮件，请按照以下步骤操作:

1. [获取用户 ID、团队 ID 或频道 ID](#get-the-user-id-team-id-or-channel-id) (如果需要)。
1. [创建对话](#create-the-conversation)(如果需要)。
1. [获取对话 ID](#get-the-conversation-id)。
1. [发送消息](#send-the-message).

[示例](#samples)部分中的代码片段用于创建一对一对话。 有关一对一对话和群聊或频道的完整工作示例的链接，请参阅[代码示例](#code-sample)。

若要有效地使用主动消息，请参阅[主动消息传递的最佳做法](#best-practices-for-proactive-messaging)。 对于某些方案，你必须[使用 Graph 主动安装应用](#proactively-install-your-app-using-graph)。 [示例](#samples)部分中的代码片段用于创建一对一对话。 有关一对一对话以及群聊或频道的完整工作示例，请参阅[代码示例](#code-sample)。

## <a name="get-the-user-id-team-id-or-channel-id"></a>获取用户 ID、团队 ID 或频道 ID

若要在频道中创建新对话或对话线程，你必须具有正确的 ID。 你可以使用以下任何方式接收或检索此 ID：

* 当你的应用安装在任何特定上下文中时，你会收到一个 [`onMembersAdded` 活动](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
* 将新用户添加到安装应用的上下文时，你会收到一个 [`onMembersAdded` 活动](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
* 你可以在已安装应用的团队中检索[频道列表](~/bots/how-to/get-teams-context.md)。
* 你可以检索已安装应用的团队的[成员列表](~/bots/how-to/get-teams-context.md)。
* 机器人收到的每个活动都必须包含所需信息。

无论你通过何种方式获取信息，都必须存储 `tenantId` 以及 `userId` 或 `channelId` 才能创建新对话。 你还可以使用 `teamId` 在团队的常规频道或默认频道中创建新的对话线程。

`userId` 对于机器人 ID 和特定用户是唯一的。 你不能在机器人之间重复使用 `userId`。 `channelId` 是全局 ID。 但是，必须先在团队中安装机器人，然后才能向频道发送主动消息。

获取用户或频道信息后，你必须创建对话。

## <a name="create-the-conversation"></a>创建对话

如果对话不存在或者你不知道 `conversationId`，则必须创建对话。 只能创建一次对话并存储 `conversationId` 值或 `conversationReference` 对象。

创建对话后，你必须获取对话 ID。

## <a name="get-the-conversation-id"></a>获取对话 ID

使用 `conversationReference` 对象或 `conversationId` 和 `tenantId` 发送消息。 你可以通过以下方式获取此 ID，即通过从该上下文发送给你的任何活动创建对话或存储对话。 存储此 ID 以供参考。

获取相应的地址信息后，你可以发送消息。

## <a name="send-the-message"></a>发送邮件

现在，你已拥有正确的地址信息，因此可以发送消息。 如果你使用的是 SDK，则必须使用 `continueConversation` 方法以及 `conversationId` 和 `tenantId` 进行直接 API 调用。 必须正确设置 `conversationParameters` 才能成功发送消息。 请参阅[示例](#samples)部分，或使用[代码示例](#code-sample)部分中列出的其中一个示例。

现在，你已发送主动消息，你必须在发送主动消息时遵循这些最佳做法，以便更好地在用户和机器人之间交换信息。

## <a name="best-practices-for-proactive-messaging"></a>主动消息传递的最佳做法

向用户发送主动消息是一种与用户沟通的有效方式。 但是，从用户的角度来看，该消息似乎是未经提示的。 如果有欢迎消息，这将是他们第一次与应用交互。 使用此功能并向用户提供完整信息以了解该消息的用途非常重要。

### <a name="welcome-messages"></a>欢迎消息

当使用主动消息传递向用户发送欢迎消息时，用户收到消息的原因将没有上下文。 这也是用户第一次与你的应用交互。 这是创造良好第一印象的好机会。 最佳欢迎消息必须包括：

* 用户收到消息的原因：用户必须非常清楚他们收到消息的原因。 如果你的机器人序安装在频道中，并且向所有用户发送了欢迎消息，请让他们知道它安装在哪个频道中以及谁安装了它。
* 你提供的内容：用户必须了解他们可以使用你的应用做什么，以及你可以为他们带来什么价值。
* 他们接下来应该做什么：邀请用户尝试某个命令，或者与你的应用交互。
糟糕的欢迎消息可能会导致用户阻止你的机器人。 言简意赅地写下欢迎消息。 如果欢迎消息没有达到预期效果，则对欢迎消息进行迭代。

### <a name="notification-messages"></a>通知消息

若要使用主动消息传递发送通知，请确保用户具有清晰的路径来根据你的通知执行常见操作。 确保用户清楚地了解他们收到通知的原因。 良好的通知消息通常包括以下内容：

* 发生了什么：明确指出发生了什么情况才导致发送通知。
* 结果是什么：必须明确指出哪些项目更新导致发送通知。
* 谁或哪些操作触发了通知：谁或执行了哪些操作导致发送通知。
* 用户可以执行哪些操作来响应：让用户能够轻松根据你的通知执行相关操作。
* 用户如何选择退出：你必须为用户提供选择退出其他通知的路径。

若向大量用户发送消息，例如向你的组织发送消息，请使用 Graph 主动安装你的应用。

### <a name="scheduled-messages"></a>计划的消息

使用主动消息传递向用户发送计划的消息时，请验证你的时区是否已更新为其所在的时区。 这可确保在相关时间将消息传递给用户。 计划的消息通常包括：

* 用户收到消息的原因：让用户轻松了解收到消息的原因。
* 用户接下来可以做什么：用户可以根据消息内容执行所需的操作。

## <a name="proactively-install-your-app-using-graph"></a>使用 Graph 主动安装应用

主动向以前未安装或未与应用交互的用户发送消息。 例如，你希望使用[公司通信器](~/samples/app-templates.md#company-communicator)向整个组织发送消息。 在这种情况下，可以使用 Graph API 主动为用户安装应用。 缓存应用在安装时收到的 `conversationUpdate` 事件中的必要值。

你只能安装组织应用目录或 Teams 应用商店中的应用。

请参阅 Graph 文档中的[为用户安装应用](/graph/api/userteamwork-post-installedapps)以及[使用 Graph 在 Teams 中进行主动型机器人安装和消息传递](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)。 此外，GitHub 平台上还提供了 [Microsoft .NET Framework 示例](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)。

## <a name="samples"></a>示例

以下代码显示如何发送主动消息：

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

你必须提供用户 ID 和租户 ID。 如果调用成功，则 API 将返回以下响应对象：

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-sample"></a>代码示例

下表提供了一个用于将基本对话流合并到 Teams 应用程序中的简单代码示例，并介绍了如何在 Teams 的频道中创建新的对话线程：

| **示例名称** | **说明** | **.NET** | **Node.js** | **Python** |
|---------------|--------------|--------|-------------|--------|
| Teams 对话基础知识  | 演示 Teams 中对话的基础知识，包括发送一对一的主动消息。| [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| 在频道中启动新线程 | 演示在频道中创建新线程。 | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |
| 主动安装应用并发送主动通知 | 此示例演示如何通过调用 Microsoft Graph API 为用户使用主动安装应用并发送主动通知。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) | |

### <a name="additional-code-sample"></a>其他代码示例

> [!div class="nextstepaction"]
> [Teams 主动消息传递代码示例](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="step-by-step-guide"></a>分步指南

按照[分步指南](../../../sbs-send-proactive.yml)执行操作，它可帮助你从机器人发送主动消息。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [设置你的智能机器人邮件格式](~/bots/how-to/format-your-bot-messages.md)

## <a name="see-also"></a>另请参阅

* [**Teams 主动消息传递代码示例**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)
* [使用机器人进行频道和群组对话](~/bots/how-to/conversations/channel-and-group-conversations.md)
* [响应任务模块提交操作](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
* [向用户发送主动通知](/azure/bot-service/bot-builder-howto-proactive-message)
