---
title: 发送主动邮件
author: clearab
description: 如何使用 Microsoft 团队 bot 发送主动消息。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2dfb8e18243079ca38d505f4b80deb7abf2de32f
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874847"
---
# <a name="send-proactive-messages"></a>发送主动邮件

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

主动消息是由自动程序发送的无直接响应来自用户的请求的任何消息。 这可能包括如下邮件：

* 欢迎邮件
* 通知
* 计划的邮件

为了让你的 bot 发送一封主动消息，它必须具有对要向其发送邮件的用户、组聊天或团队的访问权限。 对于组聊天或团队，这意味着必须首先将包含你的 bot 的应用安装到该位置。 如有必要，可以在团队中使用 Graph （如有必要） [主动安装应用](#proactively-install-your-app-using-graph) ，或使用 [应用策略](/microsoftteams/teams-custom-app-policies-and-settings) 将应用推送到租户中的团队和用户。 对于用户，需要为该用户安装您的应用程序，或者您的用户需要是安装应用程序的团队的一部分。

发送主动消息与发送常规邮件不同，因为您没有可用于答复的活动状态 `turnContext` 。 您可能还需要在发送邮件之前，先创建一个新的会话 (，例如新的一对一聊天或在频道) 中的新对话线程。 您不能通过主动消息在团队中创建新组聊天或新频道。

在较高级别上，您需要完成的步骤才能发送一封主动消息：

1. [获取用户 ID 或团队/通道 ID](#get-the-user-id-or-teamchannel-id) (如果需要) 。
1. 如有必要[，创建会话或对话线索](#create-the-conversation) () 。
1. [获取会话 ID](#get-the-conversation-id)。
1. [发送邮件](#send-the-message)。

下面的 [示例](#examples) 部分中的代码段用于创建一对一对话，请参阅 " [参考](#references) " 部分，以获取用于一次性对话和组/频道的完整工作示例的链接。

## <a name="get-the-user-id-or-teamchannel-id"></a>获取用户 ID 或团队/通道 ID

如果需要在频道中创建新对话或对话线程，则首先需要使用正确的 ID 来创建对话。 您可以通过多种方式接收/检索此 ID：

1. 当您的应用程序安装在任何特定上下文中时，您将收到一个[ `onMembersAdded` 活动](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
1. 将新用户添加到安装了应用程序的上下文中时，您将收到[ `onMembersAdded` 活动](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
1. 您可以在已安装应用程序的团队中检索 [频道列表](~/bots/how-to/get-teams-context.md) 。
1. 您可以检索您的应用程序已安装的团队 [成员的列表](~/bots/how-to/get-teams-context.md) 。
1. 你的 bot 接收的每个活动将包含所需的信息。

无论您如何获取这些信息，您都需要存储 `tenantId` 和或的，以便 `userId` `channelId` 创建新对话。 您还可以使用在 `teamId` 团队的常规/默认通道中创建新的对话线程。

`userId`对于你的 Bot Id 和特定用户而言是唯一的，无法在 bot 之间重新使用它们。 `channelId`这是全局性的，但是你的 bot_必须_安装在团队中，然后才能向通道发送主动消息。

## <a name="create-the-conversation"></a>创建对话

拥有用户/频道信息后，如果会话尚不存在，则需要创建会话 (或者不知道 `conversationId`) 。 只应创建对话一次;请确保存储 `conversationId` `conversationReference` 要在将来使用的值或对象。

## <a name="get-the-conversation-id"></a>获取会话 ID

一旦创建了对话，您就可以使用 `conversationReference` 对象或 `conversationId` 和 `tenantId` 来发送邮件。 您可以通过创建对话来获取此 Id，也可以在从该上下文发送给您的任何活动中存储此 Id。 确保存储此 Id。

## <a name="send-the-message"></a>发送邮件

现在你已拥有正确的地址信息，你可以发送邮件了。 如果您使用的是 SDK，您将使用 `continueConversation` 方法，以及 `conversationId` 并执行 `tenantId` 直接 API 调用。  您需要设置 `conversationParameters` 正确的以成功发送邮件-请参阅下面的 [示例](#examples) 或使用 " [参考](#references) " 部分中列出的示例之一。

## <a name="best-practices-for-proactive-messaging"></a>主动消息传递的最佳做法

向用户发送主动消息是与用户进行通信的一种非常有效的方式。 但是，从其角度来看，此消息可以完全自发，在欢迎消息的情况下，它将在第一次与您的应用程序进行交互时显示。 因此，谨慎使用此功能非常重要 (不要对用户) 垃圾邮件，并提供足够的信息，让用户了解推广的原因。

### <a name="welcome-messages"></a>欢迎邮件

使用前瞻性消息向用户发送欢迎邮件时，必须记住，对于大多数接收邮件的人，将没有上下文了解他们接收邮件的原因。 这也是第一次将与您的应用程序进行交互。你有机会创建一个理想的首印象。 最佳欢迎消息将包括：

* **用户接收邮件的原因。** 应非常清楚用户接收邮件的原因。 如果你的 bot 已安装在频道中，并且你向所有用户发送了欢迎消息，请让他们知道它安装在什么频道并有权安装它。
* **你提供的内容。** 他们可以对你的应用程序做些什么？ 您可以为它们引入什么值？
* **接下来应做些什么。** 邀请他们试用某个命令，或以某种方式与您的应用程序进行交互。

请记住，欢迎邮件较差可能会导致用户阻止你的 bot。 应花费大量时间来起草欢迎消息，并在用户没有所需的效果的情况下对其进行迭代。

### <a name="notification-messages"></a>通知邮件

使用主动消息发送通知时，您需要确保您的用户有一个明确的路径，以根据您的通知执行常见操作，并清楚地了解通知发生的原因。 正常的通知消息通常包括：

* **发生了什么事。** 可以清楚地指示导致通知发生了什么情况。
* **结果是什么。** 应清楚是什么项目/内容已更新，从而导致通知。
* **触发它的执行者。** 导致通知被发送的操作或采取的操作。
* **用户可以采取何种响应。** 使您的用户可以轻松地根据您的通知执行操作。
* **用户可以选择退出的方式。** 您需要为用户提供一个路径，以供用户退出其他通知。

## <a name="proactively-install-your-app-using-graph"></a>使用 Graph 主动安装您的应用程序

> [!Note]
> 使用 Microsoft Graph 主动安装应用目前在 beta 中。

有时，可能有必要主动向尚未安装或与您的应用程序进行交互的邮件用户进行处理。 例如，您希望使用 [公司 communicator](~/samples/app-templates.md#company-communicator) 向整个组织发送邮件。 在这种情况下，您可以使用 Graph API 主动为您的用户安装您的应用程序，然后从 `conversationUpdate` 应用程序安装时收到的事件中缓存必要的值。

您只能安装组织应用程序目录或团队应用商店中的应用程序。

请参阅在 Microsoft Graph 的团队文档中 [为用户安装应用程序](/graph/teams-proactive-messaging) 和 [主动机器人安装和消息](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)。 GitHub 平台上也有 [Microsoft .net framework 示例](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)  。

## <a name="examples"></a>示例

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
private async Task MessageAllMembersAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var teamsChannelId = turnContext.Activity.TeamsGetChannelId();
    var serviceUrl = turnContext.Activity.ServiceUrl;
    var credentials = new MicrosoftAppCredentials(_appId, _appPassword);
    ConversationReference conversationReference = null;

    //Get the set of member IDs to send the message to
    var members = await GetPagedMembers(turnContext, cancellationToken);

    foreach (var teamMember in members)
    {
        var proactiveMessage = MessageFactory.Text($"Hello {teamMember.GivenName} {teamMember.Surname}. I'm a Teams conversation bot.");

        var conversationParameters = new ConversationParameters
        {
            IsGroup = false,
            Bot = turnContext.Activity.Recipient,
            Members = new ChannelAccount[] { teamMember },
            TenantId = turnContext.Activity.Conversation.TenantId,
        };
        //create the new one-to-one conversations
        await ((BotFrameworkAdapter)turnContext.Adapter).CreateConversationAsync(
            teamsChannelId,
            serviceUrl,
            credentials,
            conversationParameters,
            async (t1, c1) =>
            {
                //Get the conversationReference
                conversationReference = t1.Activity.GetConversationReference();
                //Send the proactive message
                await ((BotFrameworkAdapter)turnContext.Adapter).ContinueConversationAsync(
                    _appId,
                    conversationReference,
                    async (t2, c2) =>
                    {
                        await t2.SendActivityAsync(proactiveMessage, c2);
                    },
                    cancellationToken);
            },
            cancellationToken);
    }

    await turnContext.SendActivityAsync(MessageFactory.Text("All messages have been sent."), cancellationToken);
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

您必须提供用户 ID 和租户 ID。 如果调用成功，API 将返回以下响应对象。

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="references"></a>参考

下面列出了官方的主动消息示例。

|  不正确。  | 示例名称           | 说明                                                                      | .NET    | JavaScript   | Python  |
|:--:|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|57|团队对话基础知识  | 演示团队中的对话的基础知识，包括发送一对一的主动消息。|[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|58|在频道中启动新线程     | 演示如何在通道中创建新线程。 |[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

下面的示例演示了在不使用对象) 的情况下发送主动消息所需的最少量信息 (`conversationReference` 。 如果您直接使用 REST API 调用，或者尚未存储完全对象，则此示例可能很有用 `conversationReference` 。

* [团队主动消息传递](https://github.com/clearab/teamsProactiveMessaging)

## <a name="view-additional-code"></a>查看其他代码
>
> [!div class="nextstepaction"]
> [**团队主动消息代码示例**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>