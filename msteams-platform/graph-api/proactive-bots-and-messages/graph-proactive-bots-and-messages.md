---
title: 使用 Microsoft Graph授权主动自动程序安装和邮件Teams
description: 介绍邮件中的主动Teams以及如何实现它。 了解如何使用代码示例启用主动应用安装和消息传递。
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: teams 主动消息聊天安装Graph
ms.openlocfilehash: a52d36150ee384841cde73e9a00510cabc31f144
ms.sourcegitcommit: 58fe8a87b988850ae6219c55062ac34cd8bdbf66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2021
ms.locfileid: "60949577"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a>使用 Graph API 发送邮件的应用主动安装

>[!IMPORTANT]
> Microsoft Graph公共Microsoft Teams预览版可供早期访问和反馈。 尽管此版本已经过大量测试，但不适合在生产中使用。

## <a name="proactive-messaging-in-teams"></a>邮件中的主动Teams

主动消息由机器人启动，以开始与用户的对话。 它们用于多种用途，包括发送欢迎消息、开展调查或投票以及广播组织范围内的通知。 邮件中的Teams **可以临时对话** 或基于对话 **的对话传递：**

|消息类型 | 说明 |
|----------------|-------------- |
|临时主动邮件| 机器人在不中断对话流的情况下与消息进行交互。|
|基于对话框的主动消息 | 机器人创建新的对话框线程、控制对话、传递主动消息、关闭控件，以及将控制权返回到上一个对话框。|

## <a name="proactive-app-installation-in-teams"></a>在应用中主动安装Teams

在自动程序可以主动向用户发送消息之前，它必须作为个人应用或用户是成员的团队进行安装。 有时，你需要主动向尚未安装或之前未与你的应用交互的用户发送消息。 例如，需要向组织中的每个人发送重要信息。 对于此类方案，可以使用 Microsoft Graph API 主动为用户安装自动程序。

## <a name="permissions"></a>权限

Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true)资源类型权限可帮助你管理 Microsoft Teams 平台内所有 (个人) 或团队 () 范围的应用的安装生命周期：

|应用权限 | 说明|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|允许Teams应用为任何用户读取、安装、升级和卸载自身，而无需事先登录或使用。|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|允许Teams应用在任何团队中读取、安装、升级和卸载自身，而无需事先登录或使用。|

若要使用这些权限，必须将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：

* **id**：Azure Active Directory (AAD) 应用 ID。
* **resource：** 应用的资源 URL。

> [!NOTE]
>
> * 自动程序需要应用程序权限，而不是用户委派权限，因为安装适用于其他人。
>
> * 租户AAD必须[显式授予对应用程序的权限](/graph/security-authorization#grant-permissions-to-an-application)。 在向应用程序授予权限后，AAD的所有成员都获得已授予的权限。

## <a name="enable-proactive-app-installation-and-messaging"></a>启用主动应用安装和消息传递

> [!IMPORTANT]
> Microsoft Graph只能安装发布到组织的应用商店或应用商店Teams应用。

### <a name="create-and-publish-your-proactive-messaging-bot-for-teams"></a>为用户创建和发布主动消息Teams

若要开始，你需要一个自动[](../../bots/how-to/create-a-bot-for-teams.md)程序Teams组织应用商店或应用商店中的[](../../concepts/bots/bot-conversations/bots-conv-proactive.md)主动邮件Teams[功能](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)。 [](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org)

> [!TIP]
> 生产就绪型 [*公司Communicator*](../..//samples/app-templates.md#company-communicator)模板允许广播消息，是构建主动式机器人应用程序的良好开始。

### <a name="get-the-teamsappid-for-your-app"></a>获取 `teamsAppId` 应用的

可以通过以下 `teamsAppId` 方法检索 ：

* 从组织的应用程序目录中：

    **Microsoft Graph页面参考**[：teamsApp 资源类型](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

    **HTTP GET** 请求：

    ```http
    GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
    ```

    请求必须返回对象 `teamsApp` `id` ，即应用的目录生成的应用程序 ID。 这不同于在应用清单中Teams ID：

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

* 如果你的应用已在个人范围内为用户上载或旁加载：

    **Microsoft Graph页参考：**[列出为用户安装的应用](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    **HTTP GET** 请求：

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

* 如果你的应用已在团队范围内上传或旁加载频道：

    **Microsoft Graph页面参考：**[列出团队中的应用](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    **HTTP GET** 请求：

    ```http
    GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

    > [!TIP]
    > 若要缩小结果列表，可以筛选 [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) 对象的任何字段。

### <a name="determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>确定当前是否为邮件收件人安装了自动程序

您可以确定当前是否已为邮件收件人安装自动程序，如下所示：

**Microsoft Graph页参考：**[列出为用户安装的应用](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 请求：

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

请求返回：

* 如果未安装应用，则为空数组。
* 包含单个 [teamsAppInstallation 对象的](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) 数组（如果已安装应用）。

### <a name="install-your-app"></a>安装应用

可以按如下方式安装应用：

**Microsoft Graph页面参考：**[为用户安装应用](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP POST** 请求：

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

如果用户已运行Microsoft Teams，则立即安装应用。 若要查看已安装的应用，可能需要重新启动。

### <a name="retrieve-the-conversation-chatid"></a>检索对话 `chatId`

为用户安装应用时，机器人将收到一个事件通知，其中包含发送主动消息 `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)的必要信息。

**Microsoft Graph页面参考：**[获取聊天](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

1. 必须具有应用的 `{teamsAppInstallationId}` 。 如果没有，请使用以下内容：

    **HTTP GET** 请求：

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
    ```

    响应 **的 id** 属性为 `teamsAppInstallationId` 。

1. 提出以下请求以提取 `chatId` ：

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

### <a name="send-proactive-messages"></a>发送主动邮件

自动程序 [可以在为用户或](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) 团队添加自动程序并接收所有用户信息后发送主动消息。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **.NET** | **Node.js** |
|---------------|--------------|--------|-------------|
| 主动安装应用并发送主动通知 | 此示例演示如何使用用户主动安装应用，以及如何通过调用 Microsoft Graph发送主动通知。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) |

## <a name="additional-code-samples"></a>其他代码示例
>
> [!div class="nextstepaction"]
> [**Teams主动邮件代码示例**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)

## <a name="see-also"></a>另请参阅

* [在 Teams 中管理应用设置策略](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [向用户发送主动通知 SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)
