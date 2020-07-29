---
title: 使用 Microsoft Graph 在团队中启用主动备机器人安装和邮件功能
description: 介绍了如何在团队中进行主动消息传递以及如何实现。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: 团队前瞻性消息聊天安装图
ms.openlocfilehash: 735dbfa39222f312b4f3714b5c009dfd1bf28b05
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434494"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a>在使用 Microsoft Graph 的团队中启用主动备机器人安装和主动消息（公共预览）

>[!IMPORTANT]
> Microsoft Graph 公共预览版适用于早期访问和反馈。 尽管此版本已经历大量测试，但不适合在生产中使用。

## <a name="proactive-messaging-in-teams"></a>团队中的主动消息

启动由 bot 启动与用户的对话的主动消息。 它们可用于多种用途，包括发送欢迎邮件、执行调查或投票以及广播组织范围内的通知。  可以将团队**中的主动**消息作为临时或**基于对话框的**对话进行传递：

|消息类型 | 说明 |
|----------------|-------------- |
|临时的主动消息| Bot 在不中断对话流的情况下 interjects 邮件。|
|基于对话框的主动消息 | Bot 将创建一个新的对话线程，控制对话，传递主动消息，关闭并将控制返回到上一个对话框。|

*请参阅*[向用户 SDK v4 发送主动通知](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)

## <a name="proactive-app-installation-in-teams"></a>团队中的主动应用安装

在你的 bot 可以主动向用户发送邮件之前，它需要安装为个人应用程序，或者安装在用户所属的团队中。 有时，您可能需要主动向_尚未_安装或之前与您的应用程序交互的用户发送邮件。 例如，需要向组织中的每个人发送重要信息。 在这种情况下，您可以使用 Microsoft Graph API 为用户主动安装机器人。

## <a name="permissions"></a>权限

Microsoft Graph [teamsAppInstallation 资源类型](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0)权限允许您管理应用程序在 Microsoft 团队平台中的所有用户（个人）或团队（频道）作用域的安装生命周期：

|应用权限 | 说明|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|允许工作组应用在未登录或使用之前为任何**用户**读取、安装、升级和卸载自己。|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|允许团队应用在未登录或使用之前，在任何**团队**中读取、安装、升级和卸载自己。|

若要使用这些权限，您必须将[webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo)密钥添加到您的应用程序清单中，其中包含以下值：
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id** —您的 Azure AD 应用程序 id。
> * **资源**—应用程序的资源 URL。
>

>[!NOTE]
>
> * 你的 bot 需要_应用程序_不是_用户委派_的权限，因为安装不是你自己的，而是供其他人访问。
>
> * Azure AD 租户管理员必须[显式授予对应用程序的权限](/graph/security-authorization#grant-permissions-to-an-application)。 在向应用程序授予权限后，Azure AD 租户的_所有_成员都将获得已授予的权限。

## <a name="enable-proactive-app-installation-and-messaging"></a>启用主动应用安装和邮件传递

 > [!IMPORTANT]
>Microsoft Graph 将仅安装在组织的[应用程序目录](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)或[AppSource](https://appsource.microsoft.com/)中发布的应用程序。

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔为团队创建和发布主动消息机器人

若要开始，你将需要具有[主动消息](../../concepts/bots/bot-conversations/bots-conv-proactive.md)功能且在组织的[应用程序目录](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)或[AppSource](https://appsource.microsoft.com/)中[发布](../../concepts/deploy-and-publish/overview.md)的[团队的 bot](../../bots/how-to/create-a-bot-for-teams.md) 。

>[!TIP]
> 生产就绪的[**公司 Communicator**](../..//samples/app-templates.md#company-communicator)应用模板支持广播消息传递，是构建主动机器人应用程序的良好基础。

### <a name="-get-the-teamsappid-for-your-app"></a>`teamsAppId`为您的应用程序✔获取

**1.** 你将需要 `teamsAppId` 执行后续步骤。

`teamsAppId`可以从组织的应用程序目录中检索：

**Microsoft Graph 页面参考：** [teamsApp 资源类型](/graph/api/resources/teamsapp?view=graph-rest-1.0)

**HTTP GET**请求：

```http
GET https://graph.microsoft.com/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

请求将返回一个 `teamsApp` 对象。 返回的对象 `id` 是应用程序的目录生成的应用程序 id，与您在团队应用程序清单中提供的 "id：" 不同：

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

**2.** 如果您的应用程序已为个人范围内的用户上载/旁加载，则可以按如下所示检索 `teamsAppId` ：

**Microsoft Graph 页面参考：** [列出为用户安装的应用程序](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)

**HTTP GET**请求：

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

**3.** 如果您的应用程序已在团队作用域中的某个频道上传/旁加载，则可以 `teamsAppId` 按如下所示检索：

**Microsoft Graph 页面参考：** [列出团队中的应用程序](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)

**HTTP GET**请求：

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{manifestId}'
```

>[!TIP]
> 您可以对[**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0)对象的任何字段进行筛选以缩小结果列表的范围。

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔确定当前是否为邮件收件人安装了你的 bot

**Microsoft Graph 页面参考：** [列出为用户安装的应用程序](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)

**HTTP GET**请求：

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

如果未安装应用程序，则此请求将返回一个空数组; 如果已安装，则返回一个包含一个[teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta)对象的数组。

### <a name="-install-your-app"></a>✔安装您的应用程序

**Microsoft Graph 参考：** [为用户安装应用程序](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)

**HTTP POST**请求：

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

如果用户运行的是 Microsoft 团队，他们可能会立即看到应用安装。 或者，可能需要重新启动才能查看已安装的应用程序。

### <a name="-retrieve-the-conversation-chatid"></a>✔检索对话**chatId**

为用户安装您的应用程序时，bot 将收到 `conversationUpdate` [事件通知](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)，其中包含发送主动消息所需的信息。

`chatId`也可以按如下所示检索：

**Microsoft Graph 参考：** [获取聊天](/graph/api/chat-get?view=graph-rest-beta&tabs=http)

**1.** 你将需要你的应用程序 `{teamsAppInstallationId}` ，如果你没有它，请使用以下命令：

**HTTP GET**请求：

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

响应的**id**属性是 `teamsAppInstallationId` 。

**2.** 发出以下请求以获取 `chatId` ：

**HTTP GET**请求（权限 `TeamsAppInstallation.ReadWriteSelfForUser.All` ）：  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

响应的**id**属性是 `chatId` 。

或者，您可以 `chatId` 使用下面的请求检索，但它将需要更广泛的 `Chat.Read.All` 权限：

**HTTP GET**请求（权限 `Chat.Read.All` ）：

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔发送主动消息

为用户或团队添加了你的 bot 并获取了必要的用户信息后，即可开始[发送主动消息](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)。

# <a name="c--net"></a>[C #/.NET](#tab/csharp)

下面的代码片段来自[c # 的 Microsoft Bot 框架示例。](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)

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

下面的代码片段来自适用于[JavaScript 的 Microsoft Bot 框架示例](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages)。

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

## <a name="related-topic-for-teams-administrators"></a>团队管理员的相关主题
>
> [!div class="nextstepaction"]
> [**在 Microsoft 团队中管理应用程序安装策略**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a>查看其他代码示例
>
> [!div class="nextstepaction"]
> [**团队主动消息代码示例**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>