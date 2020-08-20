---
title: 使用 Microsoft Graph 支持 Teams 中的主动机器人安装和消息传递
description: 介绍 Teams 中的主动消息传递以及如何实现。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams 主动消息聊天安装图形
ms.openlocfilehash: b601c5858e5141ce81985dca62968b1713e1d2ba
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819159"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a>使用 Microsoft Graph 公共预览版启用 Teams 中的主动机器人安装 (主动) 

>[!IMPORTANT]
> Microsoft Graph 和 Microsoft Teams 公共预览版可提供快速访问权限和反馈。 虽然此版本已经进行了大的测试，但它不适合用于生产。

## <a name="proactive-messaging-in-teams"></a>Teams 中的主动消息传递

主动邮件由机器人启动，以与用户开始对话。 它们用于许多目的，包括发送欢迎邮件、进行调查或投票，以及广播组织范围内的通知。  Teams 中的主动消息可以作为临**时对话或基于对话框****的对话**传递：

|消息类型 | 说明 |
|----------------|-------------- |
|临时主动邮件| 机器人将截获一条消息，而不会中断对话流。|
|基于对话框的主动邮件 | 机器人会创建新的对话框线程，控制对话，传递主动消息，关闭，然后将控件返回到上一个对话。|

*请参阅*、 [向用户 SDK v4 发送主动通知](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)

## <a name="proactive-app-installation-in-teams"></a>Teams 中的主动应用安装

在自动程序可主动向用户传出消息之前，需要将其作为个人应用或用户所在团队进行安装。 有时，你可能需要主动向尚未 _安装或之前_ 未与应用进行交互的消息用户。 例如，需要向组织中的所有人显示至其他所有人的信息。 对于此类应用场景，可使用 Microsoft Graph API 主动为用户安装自动程序。

## <a name="permissions"></a>权限

使用 Microsoft Graph [teamsAppInstallation 资源类型](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) 权限，可管理 Microsoft Teams 平台内 (个人) 或团队 (频道) 的应用安装生命周期：

|应用权限 | 说明|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|允许 Teams 应用针对任何用户自己读取、安装 **、升级和**卸载其自身，而无需在登录或使用之前。|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|允许 Teams 应用在任何团队中自行读取、安装、升级和 **卸载其自**身，而无需先登录或使用。|

若要使用这些权限，必须使用以下 [值将 webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到应用部件清单：
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id**  — 你的 Azure AD 应用 ID。
> * **资源** — 应用程序的资源 URL。
>

>[!NOTE]
>
> * 自动程序不需要_具有非__用户委派权限_的应用程序，因为安装对用户来来并不是用户。
>
> * Azure AD 租户管理员必须 [对应用程序显式授予权限](/graph/security-authorization#grant-permissions-to-an-application)。 授权应用程序后 _，Azure_ AD 租户的所有成员都将获取已授予的权限。

## <a name="enable-proactive-app-installation-and-messaging"></a>启用主动应用安装和消息

 > [!IMPORTANT]
>Microsoft Graph 仅将安装在组织的应用程序目录或 [AppSource](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) [中发布的应用](https://appsource.microsoft.com/)。

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔为 Teams 创建和发布主动邮件传递自动程序

若要开始使用，需要具有主动[邮件](../../bots/how-to/create-a-bot-for-teams.md)功能的 Teams[proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md)自动程序，并[发布](../../concepts/deploy-and-publish/overview.md)在组织的应用目录[或](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) [AppSource 中](https://appsource.microsoft.com/)。

>[!TIP]
> 生产就绪 [**型公司Communicator**](../..//samples/app-templates.md#company-communicator) 公司模板支持广播消息，并且是构建主动机器人应用程序的很好基础。

### <a name="-get-the-teamsappid-for-your-app"></a>✔为 `teamsAppId` 你的应用获取

**1.** 后续步骤 `teamsAppId`  中将需要您。

可以 `teamsAppId` 从组织的应用程序目录检索到：

**Microsoft Graph 页参考**[：teamsApp 资源类型](/graph/api/resources/teamsapp?view=graph-rest-1.0)

**HTTP GET** 请求：

```http
GET https://graph.microsoft.com/beta/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

请求将返回 `teamsApp`  对象。 返回的对象是 `id`  应用的目录生成的应用 ID，与在 Teams 应用清单中提供的"id："不同：

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

**2.**  如果已为个人范围内的用户上传/旁加载应用，你可以如下所示 `teamsAppId` 进行检索：

**Microsoft Graph 页参考：**[列出为用户安装的应用](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)

**HTTP GET** 请求：

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** 如果已为团队范围内的频道上传/旁加载应用，可以按如下所示 `teamsAppId` 检索：

**Microsoft Graph 页参考：**[列出团队中的应用](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)

**HTTP GET** 请求：

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> 可以筛选 [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0) 对象的任何字段来缩小结果列表。

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔确定当前是否为邮件收件人安装了机器人

**Microsoft Graph 页参考：**[列出为用户安装的应用](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)

**HTTP GET** 请求：

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

如果未安装应用，则此请求将返回空数组，或者返回包含单个 [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) 对象的数组（如果已安装）。

### <a name="-install-your-app"></a>✔安装应用

**Microsoft Graph 参考：**[为用户安装应用](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)

**HTTP POST** 请求：

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

如果用户运行 Microsoft Teams，可能会立即看到应用安装。 或者，可能需要重新启动才能查看已安装的应用。

### <a name="-retrieve-the-conversation-chatid"></a>✔检索对话 **chatId**

为用户安装应用后，机器人将收到 `conversationUpdate` [事件通知](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) ，其中包含发送主动消息所需的信息。

`chatId`也可以按如下方式检索：

**Microsoft Graph 参考：**[获取聊天](/graph/api/chat-get?view=graph-rest-beta&tabs=http)

**1.** 您将需要您的应用程序 `{teamsAppInstallationId}` 。 如果没有，请使用以下名称：

**HTTP GET** 请求：

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

响应的 **id** 属性为 `teamsAppInstallationId` .

**2.** 发出以下请求可提取 `chatId` ：

**HTTP GET** 请求 (权限 — `TeamsAppInstallation.ReadWriteSelfForUser.All`) ：  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

响应的 **id** 属性为 `chatId` .

或者，你也可以根据 `chatId`  下面请求检索请求，但需要更广泛 `Chat.Read.All` 的权限：

**HTTP GET** 请求 (权限 — `Chat.Read.All`) ：

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔动发送主动邮件

为用户或团队添加了机器人并获取必要的用户信息后，可以开始 [发送主动邮件](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)。

# <a name="c--net"></a>[C# / .NET](#tab/csharp)

以下代码段来自 [于 C# 的 Microsoft Bot Framework 示例。](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)

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

以下代码段来自 [Microsoft Bot Framework JavaScript 示例](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages)。

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

## <a name="related-topic-for-teams-administrators"></a>有关 Teams 管理员的相关主题
>
> [!div class="nextstepaction"]
> [**在 Microsoft Teams 中管理应用设置策略**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a>查看其他代码示例
>
> [!div class="nextstepaction"]
> [**Teams 主动消息传递代码示例**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
