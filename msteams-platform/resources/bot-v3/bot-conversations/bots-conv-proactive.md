---
title: 主动邮件
description: 描述机器人可以在 Microsoft Teams 中启动对话
keywords: 团队方案主动消息传递对话机器人
ms.openlocfilehash: 8c93696f79b5d99c32162a7374c7d9adccacb984
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231622"
---
# <a name="proactive-messaging-for-bots"></a>自动程序主动消息传递

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

主动消息是由机器人发送以启动对话的消息。 你可能希望机器人启动对话的原因有很多，包括：

* 个人机器人对话的欢迎消息
* 轮询响应
* 外部事件通知

发送邮件以启动新对话线程与发送消息以响应现有对话不同：当机器人启动新对话时，没有将邮件张贴到的预先存在的对话。 若要发送主动邮件，需要：

1. [决定你要说出什么](#best-practices-for-proactive-messaging)
1. [获取用户的唯一 ID 和租户 ID](#obtain-necessary-user-information)
1. [发送邮件](#examples)

创建主动邮件时 **，必须** 调用 `MicrosoftAppCredentials.TrustServiceUrl` 服务 URL，然后创建用于 `ConnectorClient` 发送邮件的服务 URL。 如果不这样做，你的应用将收到 `401: Unauthorized` 响应。 请参阅 [下面的示例](#net-example-from-this-sample)。

## <a name="best-practices-for-proactive-messaging"></a>主动消息传递的最佳实践

向用户发送主动消息是一种与用户通信的非常有效的方式。 但是，从他们的角度来看，此消息可能看起来完全不一样，在欢迎消息的情况下，他们将是首次与你的应用交互。 因此，请慎用此功能 (不要向用户发送) ，并为用户提供足够的信息，让他们了解为何收到邮件。

主动邮件通常分为两类之一：欢迎消息或通知。

### <a name="welcome-messages"></a>欢迎消息

使用主动消息向用户发送欢迎消息时，必须记住，对于大多数接收邮件的用户，他们对于接收邮件的原因没有上下文。 这也是他们第一次与你的应用交互;这是创造良好第一印象的机会。 最佳的欢迎消息包括：

* **他们为什么收到此消息。** 用户应非常清楚地了解他们接收邮件的原因。 如果你的机器人安装在频道中，并且你向所有用户发送了欢迎消息，请让他们知道它安装在哪些频道中以及可能安装它的人。
* **你提供什么。** 他们可以对你的应用执行哪些操作？ 你可以为它们带来什么价值？
* **接下来，他们应该怎么办。** 邀请他们试用命令，或以某种方式与你的应用交互。

### <a name="notification-messages"></a>通知邮件

使用主动消息发送通知时，需要确保用户有一个明确路径，可以基于通知采取常见操作，并明确了解通知发生的原因。 良好的通知消息通常包括：

* **发生了什么事。** 导致通知发生的情况的清晰指示。
* **它发生了什么。** 应清楚哪些项目/内容已更新以引起通知。
* **谁这样做了。** 谁采取导致发送通知的操作。
* **他们可以对它执行哪些工作。** 使用户能够轻松根据通知采取操作。
* **如何选择退出。** 你需要为用户提供选择退出其他通知的路径。

## <a name="obtain-necessary-user-information"></a>获取必要的用户信息

机器人可以通过获取用户的唯一 ID 和租户 *ID* 来与单个 Microsoft Teams 用户创建新 *对话。* 可以使用下列方法之一获取这些值：

* 通过 [从安装你的应用](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) 的频道获取团队名单。
* 在用户与频道中的机器人交互时 [缓存它们](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)。
* 当用户在频道 [@mentioned聊天时，](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) 自动程序是其中一部分。
* 当你在[个人范围内 `conversationUpdate` 安装](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)应用时收到事件时缓存它们，或者将新成员添加到频道或群聊中，

### <a name="proactively-install-your-app-using-graph"></a>使用 Graph 主动安装应用

> [!Note]
> 使用 graph 主动安装应用目前处于 beta 阶段。

有时，可能需要主动向之前未安装或与你的应用交互的用户发送消息。 例如，您希望使用公司 [通信程序](~/samples/app-templates.md#company-communicator) 向整个组织发送邮件。 对于此方案，可以使用 Graph API 主动为用户安装应用，然后缓存应用在安装时收到的事件 `conversationUpdate` 所需的值。

只能安装组织应用目录或 Teams 应用商店中的应用。

有关 [完整详细信息，请参阅](/graph/teams-proactive-messaging) Graph 文档中的"为用户安装应用"。 .NET 中 [还有一个示例](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)。

## <a name="examples"></a>示例

在使用 REST API 创建新对话之前，请确保你进行身份验证并拥有一个记名令牌。

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

此 ID 是个人聊天的唯一对话 ID。 请存储此值，并重复使用它以便将来与用户交互。

### <a name="using-net"></a>使用 .NET

此示例使用 [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet 程序包。

```csharp
// Create or get existing chat conversation with user
var response = client.Conversations.CreateOrGetDirectConversation(activity.Recipient, activity.From, activity.GetTenantId());

// Construct the message to post to conversation
Activity newActivity = new Activity()
{
    Text = "Hello",
    Type = ActivityTypes.Message,
    Conversation = new ConversationAccount
    {
        Id = response.Id
    },
};

// Post the message to chat conversation with user
await client.Conversations.SendToConversationAsync(newActivity, response.Id);
```

### <a name="using-nodejs"></a>使用Node.js

```javascript
var address =
{
    channelId: 'msteams',
    user: { id: userId },
    channelData: {
        tenant: {
            id: tenantId
        }
    },
    bot:
    {
        id: appId,
        name: appName
    },
    serviceUrl: session.message.address.serviceUrl,
    useAuth: true
}

var msg = new builder.Message().address(address);
msg.text('Hello, this is a notification');
bot.send(msg);
```

*另请参阅 Bot* [Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。

## <a name="creating-a-channel-conversation"></a>创建频道对话

团队添加的机器人可以发布至频道以创建新的回复链。 如果你使用的是 Node.js Teams SDK，请使用它为你提供具有正确活动 ID 和对话 ID 的完全填充 `startReplyChain()` 的地址。如果使用的是 C#，请参阅下面的示例。

或者，您可以使用 REST API 向资源发出 POST [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) 请求。

### <a name="net-example-from-this-sample"></a>此示例 (.NET[示例) ](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)

```csharp
using Microsoft.Bot.Builder.Dialogs;
using Microsoft.Bot.Connector;
using Microsoft.Bot.Connector.Teams.Models;
using Microsoft.Teams.TemplateBotCSharp.Properties;
using System;
using System.Threading.Tasks;

namespace Microsoft.Teams.TemplateBotCSharp.Dialogs
{
    [Serializable]
    public class ProactiveMsgTo1to1Dialog : IDialog<object>
    {
        public async Task StartAsync(IDialogContext context)
        {
            if (context == null)
            {
                throw new ArgumentNullException(nameof(context));
            }

            var channelData = context.Activity.GetChannelData<TeamsChannelData>();
            var message = Activity.CreateMessageActivity();
            message.Text = "Hello World";

            var conversationParameters = new ConversationParameters
            {
                  IsGroup = true,
                  ChannelData = new TeamsChannelData
                  {
                      Channel = new ChannelInfo(channelData.Channel.Id),
                  },
                  Activity = (Activity) message
            };

            MicrosoftAppCredentials.TrustServiceUrl(serviceUrl, DateTime.MaxValue);
            var connectorClient = new ConnectorClient(new Uri(activity.ServiceUrl));
            var response = await connectorClient.Conversations.CreateConversationAsync(conversationParameters);

            context.Done<object>(null);
        }
    }
}
```
