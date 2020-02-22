---
title: 主动消息
description: 描述 bot 可以在 Microsoft 团队中开始对话
keywords: 团队方案主动消息对话机器人
ms.openlocfilehash: 2f644820da33acc885a7972b13a1f61c167d6d8f
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228064"
---
# <a name="proactive-messaging-for-bots"></a>针对 bot 的主动消息

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

[！注意] 主动消息是由 bot 发送的用于启动对话的邮件。 出于多种原因，您可能希望机器人启动对话，其中包括：

* 个人 bot 对话的欢迎邮件
* 轮询响应
* 外部事件通知

发送邮件以启动新的对话线程与发送邮件以响应现有对话不同：当你的 bot 启动新的对话时，没有要将邮件发布到的预先存在的会话。 若要发送一封主动消息，您需要执行以下操作：

1. [决定要说出的内容](#best-practices-for-proactive-messaging)
1. [获取用户的唯一 Id 和租户 Id](#obtain-necessary-user-information)
1. [发送邮件](#examples)

创建主动预防性邮件**** 时， `MicrosoftAppCredentials.TrustServiceUrl`必须调用并传入服务 URL，然后才能创建`ConnectorClient`将用于发送邮件的。 如果不这样做，您的应用程序将`401: Unauthorized`收到响应。 请参阅[下面的示例](#net-example-from-this-sample)。

## <a name="best-practices-for-proactive-messaging"></a>主动消息传递的最佳做法

向用户发送主动消息是与用户进行通信的一种非常有效的方式。 但是，从其角度看，此消息似乎完全自发，而欢迎消息则是第一次与您的应用程序进行交互的情况。 因此，谨慎使用此功能非常重要（不要向用户发送垃圾邮件），并为他们提供足够的信息，让他们了解为什么要推广。

主动消息通常分为两类：欢迎消息或通知中的一种。

### <a name="welcome-messages"></a>欢迎邮件

使用前瞻性消息向用户发送欢迎邮件时，必须注意，对于大多数接收邮件的用户，他们在接收邮件时将没有上下文。 这也是第一次将与您的应用程序进行交互。你有机会创建一个理想的首印象。 最佳欢迎消息将包括：

* **为什么他们收到此邮件。** 应非常清楚用户接收邮件的原因。 如果你的 bot 已安装在频道中，并且你向所有用户发送了欢迎消息，请让他们知道它安装在什么频道并有权安装它。
* **你提供的内容。** 他们可以对你的应用程序做些什么？ 您可以为它们引入什么值？
* **接下来应做些什么。** 邀请他们试用某个命令，或以某种方式与您的应用程序进行交互。

### <a name="notification-messages"></a>通知邮件

使用主动消息发送通知时，您需要确保您的用户有一个明确的路径，以根据您的通知执行常见操作，并清楚地了解通知发生的原因。 正常的通知消息通常包括：

* **发生了什么事。** 可以清楚地指示导致通知发生了什么情况。
* **它发生的变化。** 应清楚是什么项目/内容已更新，从而导致通知。
* **已完成的操作。** 谁采取了导致通知发送的操作。
* **他们可以执行的操作。** 使您的用户可以轻松地根据您的通知执行操作。
* **他们可以选择退出。** 您需要为用户提供一个路径，以供用户退出其他通知。

## <a name="obtain-necessary-user-information"></a>获取必要的用户信息

Bot 可以通过获取用户的*唯一 ID*和*租户 id* ，创建与单个 Microsoft 团队用户的新对话。 您可以使用下列方法之一获取这些值：

* 通过从频道中[提取团队名单，](~/resources/bot-v3/bots-context.md#fetching-the-team-roster)您的应用程序已安装在中。
* 通过在用户[与频道中的 bot 交互](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)时缓存这些文件。
* 当用户[在频道对话中 @mentioned](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)时，bot 是的一部分。
* 当您的应用程序安装在个人作用域中时，当您[收到`conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)事件时缓存它们，或将新成员添加到频道或组聊天

### <a name="proactively-install-your-app-using-graph"></a>使用 Graph 主动安装您的应用程序

> [!Note]
> 使用 graph 主动安装应用当前处于 beta 中。

有时，可能有必要主动向尚未安装或与您的应用程序进行交互的邮件用户进行处理。 例如，您希望使用[公司 communicator](~/samples/app-templates.md#company-communicator)向整个组织发送邮件。 在这种情况下，您可以使用 Graph API 主动为您的用户安装您的应用程序，然后从应用`conversationUpdate`程序安装时收到的事件中缓存必要的值。

您只能安装组织应用程序目录或团队应用商店中的应用程序。

有关完整的详细信息，请参阅在 Graph 文档中[安装用户的应用程序](/graph/teams-proactive-messaging)。 [.Net 中](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)也有一个示例。

## <a name="examples"></a>示例

在使用 REST API 创建新对话之前，请务必对持有者令牌进行身份验证并拥有持有者令牌。

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

此 ID 是个人聊天的唯一会话 ID。 请存储此值并重用它以供用户将来交互。

### <a name="using-net"></a>使用 .NET

本示例使用的是 ".[团队](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)" NuGet 包。

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

### <a name="using-nodejs"></a>使用 node.js

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

*另请参阅* [Bot 框架示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。

## <a name="creating-a-channel-conversation"></a>创建频道对话

您的团队添加的 bot 可以发布到通道中，以创建新的答复链。 如果您使用的是 node.js 团队 SDK，则使用`startReplyChain()`可为您提供一个具有正确的活动 id 和会话 id 的完全填充的地址。如果使用的是 c #，请参阅下面的示例。

或者，也可以使用 REST API 并向[`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) RESOURCE 发出 POST 请求。

### <a name="net-example-from-this-sample"></a>.NET 示例（[本示例](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)中）

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
