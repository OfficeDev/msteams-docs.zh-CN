---
title: 使用 Microsoft Graph 在 Teams 中启用主动机器人安装和消息传递
description: 介绍 Teams 中的主动消息传递以及如何实现。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams 主动消息聊天安装图
ms.openlocfilehash: 4f26b4d2f4e82fcf50b7a35c46bcd07e5afecf19
ms.sourcegitcommit: b99ed616db734371e4af4594b7e895c5b05737c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2021
ms.locfileid: "50162892"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a>使用 Microsoft Graph 公共预览版在 Teams 中启用主动自动 (和主动) 

>[!IMPORTANT]
> Microsoft Graph 和 Microsoft Teams 公共预览版可用于早期访问和反馈。 尽管此版本已经过大量测试，但不适合在生产中使用。

## <a name="proactive-messaging-in-teams"></a>Teams 中的主动消息传递

主动消息由机器人启动，以开始与用户的对话。 它们用于多种用途，包括发送欢迎消息、开展调查或投票以及广播组织范围内的通知。  Teams 中的主动消息可以作为临时对话 **或** 基于对话 **的对话** 传递：

|消息类型 | 说明 |
|----------------|-------------- |
|临时主动消息| 自动程序在未中断对话流的情况下干扰消息。|
|基于对话框的主动消息 | 机器人创建新的对话框线程、控制对话、传递主动消息、关闭并返回对上一对话框的控制。|

*请参阅*， [向用户 SDK v4 发送主动通知](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="proactive-app-installation-in-teams"></a>Teams 中的主动应用安装

在自动程序可以主动向用户发送消息之前，需要以个人应用或用户为成员的团队进行安装。 有时，你可能需要主动向尚未安装或之前与你的应用交互的用户发送消息。 例如，需要向组织中的每个人发送重要信息。 对于此类方案，可以使用 Microsoft Graph API 主动为用户安装自动程序。

## <a name="permissions"></a>权限

通过 Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) 资源类型权限，你可以管理 Microsoft Teams 平台内所有 (个人) 或团队 (频道) 范围的应用的安装生命周期：

|应用权限 | 说明|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|允许 Teams 应用为任何用户读取、安装、升级和卸载自身，而无需事先登录或使用。|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|允许 Teams 应用在任何团队中读取、安装、升级和卸载自身，而无需事先登录或使用。|

若要使用这些权限，必须将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id**  — Azure AD 应用 ID。
> * **资源** — 应用的资源 URL。
>

>[!NOTE]
>
> * 您的自动 _程序需要_ 应用程序而不是用户 _委派_ 的权限，因为安装并非针对自己，而对于其他人。
>
> * Azure AD 租户管理员必须 [明确授予对应用程序的权限](/graph/security-authorization#grant-permissions-to-an-application)。 向应用程序授予权限后，Azure AD 租户的所有成员都将获得授予的权限。 

## <a name="enable-proactive-app-installation-and-messaging"></a>启用主动应用安装和消息传递

 > [!IMPORTANT]
>Microsoft Graph 将仅安装在组织的应用目录或[](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) [AppSource 中发布的应用](https://appsource.microsoft.com/)。

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔为 Teams 创建和发布主动消息自动程序

若要开始，你需要一个 Teams 自动程序，[](../../concepts/bots/bot-conversations/bots-conv-proactive.md)具有主动消息传递功能，并[](../../concepts/deploy-and-publish/overview.md)发布在组织的应用目录或[](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) [AppSource 中](https://appsource.microsoft.com/)。 [](../../bots/how-to/create-a-bot-for-teams.md)

>[!TIP]
> 生产就绪型 [**公司Communicator**](../..//samples/app-templates.md#company-communicator) 模板支持广播消息，是构建主动式机器人应用程序的良好基础。

### <a name="-get-the-teamsappid-for-your-app"></a>✔获取 `teamsAppId` 应用

**1.** 你将需要执行 `teamsAppId`  以下步骤。

`teamsAppId`可以从组织的应用程序目录中检索：

**Microsoft Graph 页面参考**[：teamsApp 资源类型](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

**HTTP GET** 请求：

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

请求将返回一 `teamsApp`  个对象。 返回的对象是应用的目录生成的应用 ID，不同于你在 Teams 应用清单中提供的 `id`  "id："：

```json
{
  "value": [
    {
      "id": "b1c5353a-7aca-41b3-830f-27d5218fe0e5",
      "externalId": "f31b1263-ba99-435a-a679-911d24850d7c",
      "name": "Test App",
      "version": "1.0.1",
      "distributionMethod": "Organization"
    }
  ]
}
```

**2.**  如果你的应用已在个人范围内为用户上载或旁加载，你可以按 `teamsAppId` 如下方式检索：

**Microsoft Graph 页面参考：**[列出为用户安装的应用](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 请求：

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** 如果你的应用已在团队范围内为频道上载/旁加载，你可以按 `teamsAppId` 如下方式检索：

**Microsoft Graph 页面参考：**[列出团队中的应用](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 请求：

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> 可以筛选 [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) 对象的任何字段以缩小结果列表。

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔确定当前是否已为邮件收件人安装自动程序

**Microsoft Graph 页面参考：**[列出为用户安装的应用](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 请求：

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

如果未安装应用，此请求将返回空数组;如果已安装，则返回包含单个 [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) 对象的数组。

### <a name="-install-your-app"></a>✔安装应用

**Microsoft Graph 页面参考：**[为用户安装应用](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP POST** 请求：

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

如果用户正在运行 Microsoft Teams，他们可能会立即看到应用安装。 或者，可能需要重新启动才能看到已安装的应用。

### <a name="-retrieve-the-conversation-chatid"></a>✔检索 **对话 chatId**

为用户安装应用时，自动程序将收到一个事件通知，其中包含发送主动消息 `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)的必要信息。

`chatId`也可以按如下方式检索：

**Microsoft Graph 页面参考：**[获取聊天](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

**1.** 你将需要你的应用 `{teamsAppInstallationId}` 。 如果没有，请使用以下内容：

**HTTP GET** 请求：

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

响应 **的 id** 属性为 `teamsAppInstallationId` 。

**2.** 提出以下请求以提取 `chatId` ：

**HTTP GET** 请求 (权限 — `TeamsAppInstallation.ReadWriteSelfForUser.All`) ：  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

响应 **的 id** 属性为 `chatId` 。

或者，您可以使用下面的请求检索， `chatId`  但需要更广泛的 `Chat.Read.All` 权限：

**HTTP GET** 请求 (权限 — `Chat.Read.All`) ：

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔发送主动邮件

为用户或团队添加自动程序并获取必要的用户信息后，它就可以开始发送 [主动消息](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)。

# <a name="c--net"></a>[C# / .NET](#tab/csharp)

以下代码段来自适用于 C# 的 [Microsoft Bot Framework 示例。](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)

```csharp
using System.Collections.Concurrent;
using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Bot.Builder;
using Microsoft.Bot.Schema;

namespace Microsoft.BotBuilderSamples
{
    public class ProactiveBot : ActivityHandler
    {
        // Message to send to users when the bot receives a Conversation Update event
        private const string WelcomeMessage = "Welcome to the Proactive Bot sample.  Navigate to http://localhost:3978/api/notify to proactively message everyone who has previously messaged this bot.";

        // Dependency injected dictionary for storing ConversationReference objects used in NotifyController to proactively message users
        private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

        public ProactiveBot(ConcurrentDictionary<string, ConversationReference> conversationReferences)
        {
            _conversationReferences = conversationReferences;
        }

        private void AddConversationReference(Activity activity)
        {
            var conversationReference = activity.GetConversationReference();
            _conversationReferences.AddOrUpdate(conversationReference.User.Id, conversationReference, (key, newValue) => conversationReference);
        }

        protected override Task OnConversationUpdateActivityAsync(ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            AddConversationReference(turnContext.Activity as Activity);

            return base.OnConversationUpdateActivityAsync(turnContext, cancellationToken);
        }

        protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            foreach (var member in membersAdded)
            {
                // Greet anyone that was not the target (recipient) of this message.
                if (member.Id != turnContext.Activity.Recipient.Id)
                {
                    await turnContext.SendActivityAsync(MessageFactory.Text(WelcomeMessage), cancellationToken);
                }
            }
        }

        protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
        {
            AddConversationReference(turnContext.Activity as Activity);

            // Echo back what the user said
            await turnContext.SendActivityAsync(MessageFactory.Text($"You sent '{turnContext.Activity.Text}'"), cancellationToken);
        }
    }
}
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

以下代码段来自 [适用于 JavaScript 的 Microsoft Bot Framework 示例](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages)。

```javascript
const { ActivityHandler, TurnContext } = require('botbuilder');

class ProactiveBot extends ActivityHandler {
    constructor(conversationReferences) {
        super();

        // Dependency injected dictionary for storing ConversationReference objects used in NotifyController to proactively message users
        this.conversationReferences = conversationReferences;

        this.onConversationUpdate(async (context, next) => {
            this.addConversationReference(context.activity);

            await next();
        });

        this.onMembersAdded(async (context, next) => {
            const membersAdded = context.activity.membersAdded;
            for (let cnt = 0; cnt < membersAdded.length; cnt++) {
                if (membersAdded[cnt].id !== context.activity.recipient.id) {
                    const welcomeMessage = 'Welcome to the Proactive Bot sample.  Navigate to http://localhost:3978/api/notify to proactively message everyone who has previously messaged this bot.';
                    await context.sendActivity(welcomeMessage);
                }
            }

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });

        this.onMessage(async (context, next) => {
            this.addConversationReference(context.activity);

            // Echo back what the user said
            await context.sendActivity(`You sent '${ context.activity.text }'`);
            await next();
        });
    }

    addConversationReference(activity) {
        const conversationReference = TurnContext.getConversationReference(activity);
        this.conversationReferences[conversationReference.conversation.id] = conversationReference;
    }
}

module.exports.ProactiveBot = ProactiveBot;

```
---

## <a name="related-topic-for-teams-administrators"></a>适用于 Teams 管理员的相关主题
>
> [!div class="nextstepaction"]
> [**在 Teams 中管理应用设置策略**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a>查看其他代码示例
>
> [!div class="nextstepaction"]
> [**Teams 主动邮件代码示例**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
