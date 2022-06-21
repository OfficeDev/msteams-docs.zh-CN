---
title: 使用 Microsoft Graph 在 Teams 中授权主动机器人安装和消息传递
description: 本文介绍Teams中的主动消息传送以及如何实现它。 了解如何使用代码示例启用主动应用安装和消息传递。
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: Overview
ms.openlocfilehash: 832dfe6ddce7710d506c480fc1195c426b8da0df
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189583"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a>使用 Graph API 发送邮件的应用主动安装

## <a name="proactive-messaging-in-teams"></a>Teams 中的主动消息传递

由机器人发起主动消息，从而开始与用户对话。 它们提供多种用途，包括发送欢迎消息、进行调查或投票，以及广播组织范围内的通知。 Teams 中的主动消息可以作为 **临时** 或 **基于对话** 的对话传递:

|消息类型 | 说明 |
|----------------|-------------- |
|临时主动消息| 机器人在不中断对话流的情况下插入消息。|
|基于对话的主动消息 | 机器人会新建对话线程、控制对话、传递主动消息、关闭控制并将控制返回给前一个对话。|

## <a name="proactive-app-installation-in-teams"></a>Teams 中的主动应用安装

在机器人可以主动向用户发送消息之前，必须将其安装为个人应用，或安装在用户所属的团队中。 有时，需要主动向尚未安装或以前与应用交互的用户发送消息。 例如，如果需要向组织中的每个人发送重要信息，则可以使用 Microsoft 图形 API 为用户主动安装机器人。

## <a name="permissions"></a>权限

Microsoft Graph [teamsAppInstallation 资源类型](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) 权限有助于管理 Microsoft Teams 平台内所有用户(个人)或团队(频道)作用域的应用安装生命周期:

|应用权限 | 说明|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|允许 Teams 应用为任何 *用户* 读取、安装、升级并卸载自身，无需事先登录或使用。|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|允许 Teams 应用在任何 *团队* 中读取、安装、升级并卸载自身，无需事先登录或使用。|

要使用这些权限，必须向应用清单添加包含以下值的 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥:

* **ID**: Azure Active Directory 应用 ID。
* **资源**: 应用的资源 URL。

> [!NOTE]
>
> * 由于是为他人进行安装，因此机器人需要应用程序，而非用户委派的权限。
>
> * Azure AD 租户管理员必须 [向应用程序显式授予权限](/graph/security-authorization#grant-permissions-to-an-application)。 向应用程序授予权限后，Azure AD 租户的所有成员都将获得授予的权限。

## <a name="enable-proactive-app-installation-and-messaging"></a>启用主动应用安装和消息传递

> [!IMPORTANT]
> Microsoft Graph 只能安装发布到组织的应用商店或 Teams 应用商店的应用。

### <a name="create-and-publish-your-proactive-messaging-bot-for-teams"></a>为 Teams 创建并发布主动消息传递机器人

要开始，需要 [适用于 Teams 的机器人](../../bots/how-to/create-a-bot-for-teams.md)，其中具有[组织的应用商店](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) 或 [Teams 应用商店](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store) 中的[主动消息传递](../../concepts/bots/bot-conversations/bots-conv-proactive.md) 功能。

> [!TIP]
> 生产就绪 [*公司 Communicator*](../..//samples/app-templates.md#company-communicator) 应用模板允许广播消息传递，且是生成主动机器人应用程序的良好起点。

### <a name="get-the-teamsappid-for-your-app"></a>获取应用的 `teamsAppId`

可以通过以下方式检索 `teamsAppId`:

* 从组织的应用目录:

    **Microsoft Graph 页面参考:** [teamsApp 资源类型](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

    **HTTP GET** 请求:

    ```http
    GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
    ```

    请求必须返回 `teamsApp` 对象 `id`，即应用目录生成的应用 ID。 这不同于你在 Teams 应用清单中提供的 ID:

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

* 如果已为个人范围内的用户上传或旁加载应用:

    **Microsoft Graph 页面参考:** [列出为用户安装的应用](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    **HTTP GET** 请求:

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

* 如果已为团队范围内的频道上传或旁加载应用:

    **Microsoft Graph 页面参考:** [列出团队中的应用](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    **HTTP GET** 请求:

    ```http
    GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

    > [!TIP]
    > 要压缩结果列表，可以筛选 [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) 对象的字段。

### <a name="determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>确定当前是否已为消息收件人安装机器人

可以确定当前是否已为消息收件人安装机器人，如下所示:

**Microsoft Graph 页面参考:** [列出为用户安装的应用](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 请求:

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

请求返回:

* 如果未安装应用，则为空数组。
* 具有单一 [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) 对象的数组(如果已安装应用)。

### <a name="install-your-app"></a>安装应用

可以安装应用，如下所示:

**Microsoft Graph 页面参考:** [为用户安装应用](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP POST** 请求:

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

如果用户正在运行 Microsoft Teams，则会立即安装应用。 可能需要重启才可查看已安装的应用。

### <a name="retrieve-the-conversation-chatid"></a>检索对话 `chatId`

为用户安装应用后，机器人会收到 `conversationUpdate` [事件通知](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)，其中包含发送主动消息所需的信息。

**Microsoft Graph 页面参考:** [获取聊天](/graph/api/chat-get?view=graph-rest-v1.0&tabs=http&preserve-view=true)

1. 必须具有应用的 `{teamsAppInstallationId}`。 如果没有，请使用以下命令：

    **HTTP GET** 请求:

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
    ```

    响应的 **ID** 属性为 `teamsAppInstallationId`。

1. 发出以下请求以提取 `chatId`:

    **HTTP GET** 请求 (权限 -`TeamsAppInstallation.ReadWriteSelfForUser.All`) ：  

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
    ```

    响应的 **ID** 属性为 `chatId`。

    还可以使用以下请求检索 `chatId`，但需要更广泛的 `Chat.Read.All` 权限:

    **HTTP GET** 请求 (权限 -`Chat.Read.All`) ：

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
    ```

### <a name="send-proactive-messages"></a>发送主动邮件

在已为用户或团队添加机器人且已收到所有用户信息后，机器人可以 [发送主动消息](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)。

## <a name="code-snippets"></a>代码段

以下代码提供了发送主动消息的示例:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
public async Task<int> SendNotificationToAllUsersAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
   int msgSentCount = 0;

   // Send notification to all the members
   foreach (var conversationReference in _conversationReferences.Values)
   {
       await turnContext.Adapter.ContinueConversationAsync(_configuration["MicrosoftAppId"], conversationReference, BotCallback, cancellationToken);
       msgSentCount++;
   }

   return msgSentCount;
}

private async Task BotCallback(ITurnContext turnContext, CancellationToken cancellationToken)
{
   await turnContext.SendActivityAsync("Proactive hello.");
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
server.get('/api/notify', async (req, res) => {
    for (const conversationReference of Object.values(conversationReferences)) {
        await adapter.continueConversationAsync(process.env.MicrosoftAppId, conversationReference, async context => {
            await context.sendActivity('proactive hello');
        });
    }

    res.setHeader('Content-Type', 'text/html');
    res.writeHead(200);
    res.write('<html><body><h1>Proactive messages have been sent.</h1></body></html>');
    res.end();
});
```

---

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **.NET** | **Node.js** |
|---------------|--------------|--------|-------------|
| 主动安装应用并发送主动通知 | 此示例演示如何通过调用 Microsoft Graph API 为用户使用主动安装应用并发送主动通知。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) |

## <a name="additional-code-samples"></a>其他代码示例
>
> [!div class="nextstepaction"]
> [**Teams 主动消息传递代码示例**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)

## <a name="see-also"></a>另请参阅

* [在 Teams 中管理应用设置策略](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [向用户 SDK v4 发送主动通知](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)
