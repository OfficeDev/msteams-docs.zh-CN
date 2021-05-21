---
title: 主动邮件
description: 描述机器人可以在聊天机器人中启动Microsoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: 团队方案主动消息对话机器人
ms.openlocfilehash: baf148d0f4d0a669de582dfca70ed5d5bed0274c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566787"
---
# <a name="proactive-messaging-for-bots"></a>自动程序主动消息传递

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

主动消息是由机器人发送以开始对话的消息。 希望机器人开始对话的原因可能有很多，其中包括:

* 个人机器人对话的欢迎消息。
* 投票响应。
* 外部事件通知。

发送消息以启动新对话线程与在响应现有对话时发送消息不同：当机器人启动新对话时，没有将邮件张贴到的预先存在的会话。 为了发送主动邮件，你需要：

1. [决定要说出什么](#best-practices-for-proactive-messaging)
1. [获取用户的唯一 ID 和租户 ID](#obtain-necessary-user-information)
1. [发送邮件](#examples)

创建主动邮件时 **，必须** 调用 ，并传递服务 URL，然后再创建 ，以 `MicrosoftAppCredentials.TrustServiceUrl` `ConnectorClient` 用于发送邮件。 如果不这样做，你的应用将收到 `401: Unauthorized` 响应。 有关详细信息，请参阅 [下面的示例](#net-example-from-this-sample)。

## <a name="best-practices-for-proactive-messaging"></a>主动邮件最佳做法

向用户发送主动邮件是一种与用户通信的有效方式。 但是，从他们的角度来看，此消息可能看起来完全不一样，在欢迎消息的情况下，他们将第一次与你的应用交互。 因此，请慎用此功能， (不要向用户发送) ，并为用户提供足够的信息，让他们了解邮件发送的原因。

主动消息一般分为两类: 欢迎消息或通知。

### <a name="welcome-messages"></a>欢迎消息

使用主动消息向用户发送欢迎消息时，必须记住，对于大多数接收邮件的人，他们对于接收邮件的原因没有上下文。 这也是他们第一次与你的应用交互;可以创造良好的第一印象。 最佳的欢迎消息包括：

* **他们为什么收到此消息。** 用户应该非常清楚地了解他们接收邮件的原因。 如果你的自动程序安装在频道中，并且你向所有用户发送了欢迎消息，请让他们知道它安装在什么频道以及可能安装它的人。
* **你提供什么功能。** 他们可以对你的应用执行哪些操作？ 您可以为它们带来什么价值？
* **接下来应执行哪些步骤。** 邀请他们试用命令，或以某种方式与你的应用交互。

### <a name="notification-messages"></a>通知消息

使用主动消息发送通知时，需要确保用户有一个清晰的路径，可以基于通知采取常见操作，并明确了解通知发生的原因。 良好的通知消息通常包括：

* **发生了什么事。** 关于导致通知发生的情况的清晰指示。
* **它发生了什么。** 应清楚哪些项/内容已更新，以引发通知。
* **Who已这样做。** Who已执行导致发送通知的操作。
* **他们可以对它做什么。** 让用户能够轻松根据通知采取操作。
* **如何选择退出。** 你需要为用户提供选择退出其他通知的路径。

## <a name="obtain-necessary-user-information"></a>获取必要的用户信息

机器人可以通过获取用户的唯一 ID Microsoft Teams租户 *ID，* 与单个用户创建新 *对话。* 可以使用以下方法之一获取这些值：

* 通过 [从应用安装通道](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) 获取团队名单。
* 在用户与频道中的机器人交互时 [缓存它们](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)。
* 当用户在频道 [@mentioned聊天时，](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) 机器人是其中一部分。
* 当你在[个人范围内安装 `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)应用或将新成员添加到该频道或群聊时，通过缓存它们来接收事件。

### <a name="proactively-install-your-app-using-graph"></a>使用安装程序主动安装Graph

> [!Note]
> 使用 graph 主动安装应用目前处于 beta 阶段。

有时，可能需要主动向之前未安装或与你的应用交互的用户发送消息。 例如，您希望使用公司通信 [程序](~/samples/app-templates.md#company-communicator) 向整个组织发送邮件。 对于此方案，可以使用 Graph API 主动为用户安装应用，然后从应用安装时收到的事件缓存 `conversationUpdate` 必要的值。

只能安装组织应用目录中的应用，或Teams应用商店。

有关[完整详细信息，](/graph/teams-proactive-messaging)请参阅Graph安装用户应用。 .NET 中 [还有一个示例](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)。

## <a name="examples"></a>示例

在使用 REST API 创建新对话之前，请确保你进行身份验证并拥有一个记分令牌。

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

此 ID 是个人聊天的唯一对话 ID。 请存储此值，并重复使用它以便以后与用户交互。

### <a name="using-net"></a>使用 .NET

此示例使用[Microsoft.Bot.Connector.Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)包。

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

### <a name="using-nodejs"></a>使用 Node.js

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

## <a name="creating-a-channel-conversation"></a>创建频道对话

团队添加的机器人可以发布到频道中，以创建新的回复链。 如果你使用的是 Node.js Teams SDK，请使用 它为你提供具有正确活动 ID 和对话 ID 的完全 `startReplyChain()` 填充的地址。如果你使用的是C#，请参阅下面的示例。

或者，您可以使用 REST API 向资源发出 POST [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) 请求。

### <a name="net-example-from-this-sample"></a>此示例示例中 (.NET [) ](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)

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

## <a name="see-also"></a>另请参阅

[Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)