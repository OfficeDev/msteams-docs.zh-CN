---
title: 机器人的主动消息传递
description: 了解如何在 Microsoft Teams 中对机器人使用主动消息传递
ms.topic: conceptual
ms.localizationpriority: high
keywords: Teams, 方案, 主动消息传递, 对话机器人
ms.openlocfilehash: 12c6f9ad79d7e28f31e3985930557339e75ccbbf
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111484"
---
# <a name="proactive-messaging-for-bots"></a>机器人的主动消息传递

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

主动消息是由机器人发送以启动对话的消息。 希望机器人开始对话的原因可能有很多，其中包括:

* 个人机器人对话的欢迎消息
* 投票回复
* 外部事件通知

发送消息来启动新对话线程不同于发送消息来响应现有对话：机器人启动新对话时，没有要将消息发布到的预先存在的对话。 若要发送主动消息，需要：

1. [决定要说的内容](#best-practices-for-proactive-messaging)
1. [获取用户的唯一 ID 和租户 ID](#obtain-necessary-user-information)
1. [发送邮件](#examples)

创建主动消息时，**必须** 调用 `MicrosoftAppCredentials.TrustServiceUrl`，并在创建用于发送消息的 `ConnectorClient` 之前传入服务 URL。 如果没有，应用会收到 `401: Unauthorized` 响应。 有关详细信息，请参阅[下面的示例](#net-example-from-this-sample)。

## <a name="best-practices-for-proactive-messaging"></a>主动消息传递的最佳做法

发送主动消息是一种与用户沟通的有效方式。 但是，从用户的角度来看，该消息似乎是未经提示的。 如果有欢迎消息，这将是他们第一次与应用交互。 使用此功能并向用户提供完整信息以了解该消息的用途非常重要。

主动消息一般分为两类: 欢迎消息或通知。

### <a name="welcome-messages"></a>欢迎消息

使用主动消息传递向用户发送欢迎消息时，请确保从用户的角度来看，该消息不会出现提示。 如果有欢迎消息，这将是他们第一次与应用交互。 最佳欢迎消息包括：

* **为什么他们收到此消息**：用户应该清楚他们收到此消息的原因。 如果机器人安装在频道中，并且你向所有用户发送了欢迎消息，请让他们知道它安装在哪个频道中以及可能谁安装了它。
* **你提供什么**：它们可以对你的应用执行哪些操作？ 可以为他们带来什么价值？
* **他们接下来应该做什么**：邀请用户尝试某个命令，或者以某种方式与应用交互。

### <a name="notification-messages"></a>通知消息

在使用主动消息传递发送通知时，需要确保用户有清晰的路径根据通知采取常见操作，并清楚地了解通知发生的原因。好的通知消息通常包括：

* **发生了什么**：明确指出发生了什么情况才导致发送通知。
* **它发生了什么**：应该清楚更新了哪些项目/内容来引起通知。
* **谁做的**：谁执行了导致发送通知的操作？
* **他们可以对其执行的操作**：使用户能够轻松地根据通知执行操作。
* **如何选择退出**：为用户提供选择退出其他通知的路径。

## <a name="obtain-necessary-user-information"></a>获取必要的用户信息

机器人可以通过获取用户的 *唯一 ID* 和 *租户 ID* 来创建与单个 Microsoft Teams 用户的新对话。 可以使用以下方法之一获取这些值：

* 从安装应用的频道[提取团队名单](~/resources/bot-v3/bots-context.md#fetch-the-team-roster)。
* 当用户[在频道中与机器人交互](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)时缓存它们。
* 当在机器人所属的[频道对话中 @提及](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)用户时。
* 当在个人范围内安装应用或将新成员添加到频道或群组聊天时，[收到 `conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) 事件时则缓存它们。

### <a name="proactively-install-your-app-using-graph"></a>使用 Graph 主动安装应用

> [!Note]
> 目前，使用 Graph 主动安装应用处于 beta 阶段。

有时，可能需要主动向之前未安装或与应用交互的用户发送消息。 例如，你希望使用[公司通信器](~/samples/app-templates.md#company-communicator)向整个组织发送消息。 对于这种情况，可以使用 Graph API 主动为用户安装应用，然后缓存应用在安装时将收到的 `conversationUpdate` 事件中的必要值。

只能安装组织应用目录或 Teams 应用商店中的应用。

有关完整详细信息，请参阅 Graph 文档中的[为用户安装应用](/graph/api/userteamwork-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)。 [.NET 中也有一个示例](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)。

## <a name="examples"></a>示例

在使用 REST API 创建新对话之前，请确保进行身份验证并拥有持有者令牌。

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

你必须提供用户 ID 和租户 ID。 如果调用成功，API 将返回以下响应对象。

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

此 ID 是个人聊天的唯一对话 ID。 请存储此值，并将其重复用于将来与用户的交互。

### <a name="using-net"></a>使用 .NET

此示例使用 [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet 包。

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

团队添加的机器人可以发布到频道中，以创建新的回复链。 如果使用的是 Node.js Teams SDK，请使用 `startReplyChain()`，它会提供一个完全填充的地址，其中包含正确的活动 ID 和对话 ID。 如果使用的是 C#，请参阅下面的示例。

或者，可以使用 REST API 并向 [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) 资源发出 POST 请求。

### <a name="net-example-from-this-sample"></a>.NET 示例（来自[此示例](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)）

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
