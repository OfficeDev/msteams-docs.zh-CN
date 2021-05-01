---
title: 使用 Microsoft Graph授权主动自动程序安装和邮件Teams
description: 介绍企业中的主动Teams以及如何实现。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams 主动消息聊天安装Graph
ms.openlocfilehash: 62974f6f3b26e53558658f0b6cfda815dee1de8a
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101798"
---
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a>使用 Graph API 以及发送邮件主动安装应用

>[!IMPORTANT]
> Microsoft Graph公共Microsoft Teams预览版可供早期访问和反馈使用。 尽管此版本已经过大量测试，但不适合在生产中使用。

## <a name="proactive-messaging-in-teams"></a>邮件中的主动Teams

主动消息由机器人启动，以开始与用户的对话。 它们用于多种用途，包括发送欢迎消息、开展调查或投票以及广播组织范围内的通知。 邮件中的Teams消息 **可以临时对话** 或基于对话 **的对话传递：**

|消息类型 | 说明 |
|----------------|-------------- |
|临时主动邮件| 机器人在不中断对话流的情况下与消息进行交互。|
|基于对话框的主动消息 | 机器人创建新的对话线程、控制对话、传递主动消息、关闭并返回对上一对话框的控制。|

请参阅向[用户发送主动通知 SDK v4。](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="proactive-app-installation-in-teams"></a>在应用中主动安装Teams

在自动程序可以主动向用户发送消息之前，它必须作为个人应用或用户是成员的团队进行安装。 有时，你需要主动向尚未安装或之前与你的应用交互的用户发送消息。 例如，需要向组织中的每个人发送重要信息。 对于此类方案，可以使用 Microsoft Graph API 主动为用户安装自动程序。

## <a name="permissions"></a>权限

Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true)资源类型权限可帮助你管理 Microsoft Teams 平台内所有 (个人) 或团队 (频道) 范围的应用的安装生命周期：

|应用权限 | 说明|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|允许Teams应用为任何用户读取、安装、升级和卸载自身，而无需事先登录或使用。|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|允许Teams应用在任何团队中读取、安装、升级和卸载自身，而无需事先登录或使用。|

若要使用这些权限，必须将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id** — 你的 Azure AD 应用 ID。
> * **resource** — 应用的资源 URL。
>
>[!NOTE]
>
> * 自动程序需要应用程序权限，而不是用户委派权限，因为安装适用于其他人。
>
> * Azure AD 租户管理员 [必须明确授予对应用程序的权限](/graph/security-authorization#grant-permissions-to-an-application)。 向应用程序授予权限后，Azure AD 租户的所有成员都将获得已授予的权限。

## <a name="enable-proactive-app-installation-and-messaging"></a>启用主动应用安装和消息传递

> [!IMPORTANT]
>Microsoft Graph只能安装发布到组织的应用商店或应用商店Teams应用。

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔创建并发布主动邮件自动程序Teams

若要开始，你需要一个自动[](../../bots/how-to/create-a-bot-for-teams.md)程序Teams组织应用商店或应用商店中的[](../../concepts/bots/bot-conversations/bots-conv-proactive.md)主动邮件Teams[功能](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)。 [](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org)

>[!TIP]
> 生产就绪型 [**公司Communicator**](../..//samples/app-templates.md#company-communicator)模板允许广播消息，它是构建主动式机器人应用程序的良好基础。

### <a name="-get-the-teamsappid-for-your-app"></a>✔获取 `teamsAppId` 应用的

**1。** 需要 执行 `teamsAppId` 以下步骤。

`teamsAppId`可以从组织的应用程序目录中检索：

**Microsoft Graph 页面参考**[：teamsApp 资源类型](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

**HTTP GET** 请求：

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

请求必须返回 `teamsApp` 对象。 返回的对象是应用的目录生成的应用程序 ID，并且不同于在应用程序清单中Teams `id` ID：

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

**2.**  如果你的应用已在个人范围内为用户上载或旁加载，可以按 `teamsAppId` 如下方式检索：

**Microsoft Graph页面参考：**[列出为用户安装的应用](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 请求：

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** 如果你的应用已针对团队作用域中的频道上载或旁加载，可以按 `teamsAppId` 如下方式检索：

**Microsoft Graph页面参考：**[列出团队中的应用](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 请求：

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> 若要缩小结果列表，可以筛选 [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) 对象的任何字段。

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔确定当前是否已为邮件收件人安装自动程序

**Microsoft Graph页面参考：**[列出为用户安装的应用](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 请求：

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

如果未安装应用，此请求将返回空数组;如果已安装应用，则返回包含单个 [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) 对象的数组。

### <a name="-install-your-app"></a>✔安装应用

**Microsoft Graph页面参考：**[为用户安装应用](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP POST** 请求：

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

如果用户已运行Microsoft Teams，将立即看到应用安装。 若要查看已安装的应用，可能需要重新启动。

### <a name="-retrieve-the-conversation-chatid"></a>✔检索对话 **chatId**

为用户安装应用时，机器人将收到一个事件通知，其中包含发送主动消息 `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)的必要信息。

`chatId`也可以按如下方式检索：

**Microsoft Graph页面参考：**[获取聊天](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

**1。** 你必须需要你的应用 `{teamsAppInstallationId}` 的 。 如果没有，请使用以下内容：

**HTTP GET** 请求：

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

响应 **的 id** 属性为 `teamsAppInstallationId` 。

**2.** 提出以下请求来获取 `chatId` ：

**HTTP GET** 请求 (权限 — `TeamsAppInstallation.ReadWriteSelfForUser.All`) ：  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

响应 **的 id** 属性为 `chatId` 。

还可以检索具有以下 `chatId` 请求的 ，但需要更广泛的 `Chat.Read.All` 权限：

**HTTP GET** 请求 (权限 — `Chat.Read.All`) ：

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔发送主动邮件

自动程序 [可以在为用户或](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) 团队添加自动程序并接收所有用户信息后发送主动消息。

## <a name="related-topic-for-teams-administrators"></a>有关管理员Teams主题
>
> [!div class="nextstepaction"]
> [**在应用中管理应用Microsoft Teams**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a>查看其他代码示例
>
> [!div class="nextstepaction"]
> [**Teams主动邮件代码示例**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
