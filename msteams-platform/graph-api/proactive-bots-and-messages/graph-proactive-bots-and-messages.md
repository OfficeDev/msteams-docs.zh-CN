---
title: 使用 Microsoft Graph授权主动自动程序安装和邮件Teams
description: 介绍企业中的主动Teams以及如何实现。
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: teams 主动消息聊天安装Graph
ms.openlocfilehash: 0f59a74cc24b7d80dd3afd4aa4369a47d56e4d59
ms.sourcegitcommit: a6253e89cb8c8c34d45b06e08c9668daeebc30a3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2021
ms.locfileid: "53300303"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a><span data-ttu-id="c3815-104">使用 Graph API 发送邮件的应用主动安装</span><span class="sxs-lookup"><span data-stu-id="c3815-104">Proactive installation of apps using Graph API to send messages</span></span>

>[!IMPORTANT]
> <span data-ttu-id="c3815-105">Microsoft Graph公共Microsoft Teams预览版可供早期访问和反馈使用。</span><span class="sxs-lookup"><span data-stu-id="c3815-105">Microsoft Graph and Microsoft Teams public previews are available for early access and feedback.</span></span> <span data-ttu-id="c3815-106">尽管此版本已经过大量测试，但不适合在生产中使用。</span><span class="sxs-lookup"><span data-stu-id="c3815-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="c3815-107">邮件中的主动Teams</span><span class="sxs-lookup"><span data-stu-id="c3815-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="c3815-108">主动消息由机器人启动，以开始与用户的对话。</span><span class="sxs-lookup"><span data-stu-id="c3815-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="c3815-109">它们用于多种用途，包括发送欢迎消息、开展调查或投票以及广播组织范围内的通知。</span><span class="sxs-lookup"><span data-stu-id="c3815-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span> <span data-ttu-id="c3815-110">邮件中的Teams消息 **可以临时对话** 或基于对话 **的对话传递：**</span><span class="sxs-lookup"><span data-stu-id="c3815-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="c3815-111">消息类型</span><span class="sxs-lookup"><span data-stu-id="c3815-111">Message type</span></span> | <span data-ttu-id="c3815-112">说明</span><span class="sxs-lookup"><span data-stu-id="c3815-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="c3815-113">临时主动邮件</span><span class="sxs-lookup"><span data-stu-id="c3815-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="c3815-114">机器人在不中断对话流的情况下与消息进行交互。</span><span class="sxs-lookup"><span data-stu-id="c3815-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="c3815-115">基于对话框的主动消息</span><span class="sxs-lookup"><span data-stu-id="c3815-115">Dialog-based proactive message</span></span> | <span data-ttu-id="c3815-116">机器人创建新的对话线程、控制对话、传递主动消息、关闭并返回对上一对话框的控制。</span><span class="sxs-lookup"><span data-stu-id="c3815-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="c3815-117">在应用中主动安装Teams</span><span class="sxs-lookup"><span data-stu-id="c3815-117">Proactive app installation in Teams</span></span>

<span data-ttu-id="c3815-118">在自动程序可以主动向用户发送消息之前，它必须作为个人应用或用户是成员的团队进行安装。</span><span class="sxs-lookup"><span data-stu-id="c3815-118">Before your bot can proactively message a user, it must be installed either as a personal app or in a team where the user is a member.</span></span> <span data-ttu-id="c3815-119">有时，你需要主动向尚未安装或之前与你的应用交互的用户发送消息。</span><span class="sxs-lookup"><span data-stu-id="c3815-119">At times, you need to proactively message users that have not installed or previously interacted with your app.</span></span> <span data-ttu-id="c3815-120">例如，需要向组织中的每个人发送重要信息。</span><span class="sxs-lookup"><span data-stu-id="c3815-120">For example, the need to message important information to everyone in your organization.</span></span> <span data-ttu-id="c3815-121">对于此类方案，可以使用 Microsoft Graph API 主动为用户安装自动程序。</span><span class="sxs-lookup"><span data-stu-id="c3815-121">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="c3815-122">权限</span><span class="sxs-lookup"><span data-stu-id="c3815-122">Permissions</span></span>

<span data-ttu-id="c3815-123">Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true)资源类型权限可帮助你管理 Microsoft Teams 平台内所有 (个人) 或团队 () 范围的应用的安装生命周期：</span><span class="sxs-lookup"><span data-stu-id="c3815-123">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions help you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="c3815-124">应用权限</span><span class="sxs-lookup"><span data-stu-id="c3815-124">Application permission</span></span> | <span data-ttu-id="c3815-125">说明</span><span class="sxs-lookup"><span data-stu-id="c3815-125">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="c3815-126">允许Teams应用为任何用户读取、安装、升级和卸载自身，而无需事先登录或使用。</span><span class="sxs-lookup"><span data-stu-id="c3815-126">Allows a Teams app to read, install, upgrade, and uninstall itself for any *user*, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="c3815-127">允许Teams应用在任何团队中读取、安装、升级和卸载自身，而无需事先登录或使用。</span><span class="sxs-lookup"><span data-stu-id="c3815-127">Allows a Teams app to read, install, upgrade, and uninstall itself in any *team*, without prior sign in or use.</span></span>|

<span data-ttu-id="c3815-128">若要使用这些权限，必须将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：</span><span class="sxs-lookup"><span data-stu-id="c3815-128">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

* <span data-ttu-id="c3815-129">**id**：你的Azure Active Directory (AAD) 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="c3815-129">**id**: Your Azure Active Directory (AAD) app ID.</span></span>
* <span data-ttu-id="c3815-130">**resource：** 应用的资源 URL。</span><span class="sxs-lookup"><span data-stu-id="c3815-130">**resource**: The resource URL for the app.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="c3815-131">自动程序需要应用程序权限，而不是用户委派权限，因为安装适用于其他人。</span><span class="sxs-lookup"><span data-stu-id="c3815-131">Your bot requires application and not user delegated permissions because the installation is for others.</span></span>
>
> * <span data-ttu-id="c3815-132">AAD 租户管理员 [必须对应用程序显式授予权限](/graph/security-authorization#grant-permissions-to-an-application)。</span><span class="sxs-lookup"><span data-stu-id="c3815-132">An AAD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="c3815-133">向应用程序授予权限后，AAD 租户的所有成员都获得已授予的权限。</span><span class="sxs-lookup"><span data-stu-id="c3815-133">After the application is granted permissions, all members of the AAD tenant get the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="c3815-134">启用主动应用安装和消息传递</span><span class="sxs-lookup"><span data-stu-id="c3815-134">Enable proactive app installation and messaging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3815-135">Microsoft Graph只能安装发布到组织的应用商店或应用商店Teams应用。</span><span class="sxs-lookup"><span data-stu-id="c3815-135">Microsoft Graph can only install apps published to your organization's app store or the Teams store.</span></span>

### <a name="create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="c3815-136">为用户创建和发布主动消息Teams</span><span class="sxs-lookup"><span data-stu-id="c3815-136">Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="c3815-137">若要开始，你需要一个自动[](../../bots/how-to/create-a-bot-for-teams.md)程序Teams组织应用商店或应用商店中的[](../../concepts/bots/bot-conversations/bots-conv-proactive.md)主动邮件Teams[功能](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)。 [](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org)</span><span class="sxs-lookup"><span data-stu-id="c3815-137">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that is in your [organization's app store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) or the [Teams store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span></span>

> [!TIP]
> <span data-ttu-id="c3815-138">生产就绪型 [*公司Communicator*](../..//samples/app-templates.md#company-communicator)模板允许广播消息，是构建主动式机器人应用程序的良好开始。</span><span class="sxs-lookup"><span data-stu-id="c3815-138">The production-ready [*Company Communicator*](../..//samples/app-templates.md#company-communicator) app template permits broadcast messaging and is a good start to build your proactive bot application.</span></span>

### <a name="get-the-teamsappid-for-your-app"></a><span data-ttu-id="c3815-139">获取 `teamsAppId` 应用的</span><span class="sxs-lookup"><span data-stu-id="c3815-139">Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="c3815-140">可以通过以下 `teamsAppId` 方法检索 ：</span><span class="sxs-lookup"><span data-stu-id="c3815-140">You can retrieve the `teamsAppId` in the following ways:</span></span>

* <span data-ttu-id="c3815-141">从组织的应用程序目录中：</span><span class="sxs-lookup"><span data-stu-id="c3815-141">From your organization's app catalog:</span></span>

    <span data-ttu-id="c3815-142">**Microsoft Graph 页面参考**[：teamsApp 资源类型](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c3815-142">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

    <span data-ttu-id="c3815-143">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="c3815-143">**HTTP GET** request:</span></span>

    ```http
        GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
    ```

    <span data-ttu-id="c3815-144">请求必须返回对象 `teamsApp` `id` ，即应用的目录生成的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="c3815-144">The request must return a `teamsApp` object `id`, which is the app's catalog generated app ID.</span></span> <span data-ttu-id="c3815-145">这不同于在应用清单中Teams ID：</span><span class="sxs-lookup"><span data-stu-id="c3815-145">This is different from the ID that you provided in your Teams app manifest:</span></span>

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

* <span data-ttu-id="c3815-146">如果你的应用已在个人范围内为用户上载或旁加载：</span><span class="sxs-lookup"><span data-stu-id="c3815-146">If your app has already been uploaded or sideloaded for a user in personal scope:</span></span>

    <span data-ttu-id="c3815-147">**Microsoft Graph页面参考：**[列出为用户安装的应用](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c3815-147">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

    <span data-ttu-id="c3815-148">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="c3815-148">**HTTP GET** request:</span></span>

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

* <span data-ttu-id="c3815-149">如果你的应用已在团队范围内上传或旁加载频道：</span><span class="sxs-lookup"><span data-stu-id="c3815-149">If your app has already been uploaded or sideloaded for a channel in team scope:</span></span>

    <span data-ttu-id="c3815-150">**Microsoft Graph页面参考：**[列出团队中的应用](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c3815-150">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

    <span data-ttu-id="c3815-151">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="c3815-151">**HTTP GET** request:</span></span>

    ```http
    GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

    > [!TIP]
    > <span data-ttu-id="c3815-152">若要缩小结果列表，可以筛选 [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) 对象的任何字段。</span><span class="sxs-lookup"><span data-stu-id="c3815-152">To narrow the list of results, you can filter any of the fields of the [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object.</span></span>

### <a name="determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="c3815-153">确定当前是否为邮件收件人安装了自动程序</span><span class="sxs-lookup"><span data-stu-id="c3815-153">Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="c3815-154">您可以确定当前是否已为邮件收件人安装自动程序，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c3815-154">You can determine whether your bot is currently installed for a message recipient as follows:</span></span>

<span data-ttu-id="c3815-155">**Microsoft Graph页面参考：**[列出为用户安装的应用](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c3815-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="c3815-156">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="c3815-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="c3815-157">请求返回：</span><span class="sxs-lookup"><span data-stu-id="c3815-157">The request returns:</span></span>

* <span data-ttu-id="c3815-158">如果未安装应用，则为空数组。</span><span class="sxs-lookup"><span data-stu-id="c3815-158">An empty array if the app is not installed.</span></span>
* <span data-ttu-id="c3815-159">包含单个 [teamsAppInstallation 对象的](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) 数组（如果已安装应用）。</span><span class="sxs-lookup"><span data-stu-id="c3815-159">An array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if the app is installed.</span></span>

### <a name="install-your-app"></a><span data-ttu-id="c3815-160">安装应用</span><span class="sxs-lookup"><span data-stu-id="c3815-160">Install your app</span></span>

<span data-ttu-id="c3815-161">可以按如下方式安装应用：</span><span class="sxs-lookup"><span data-stu-id="c3815-161">You can install your app as follows:</span></span>

<span data-ttu-id="c3815-162">**Microsoft Graph页面参考：**[为用户安装应用](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c3815-162">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="c3815-163">**HTTP POST** 请求：</span><span class="sxs-lookup"><span data-stu-id="c3815-163">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="c3815-164">如果用户已运行Microsoft Teams，则立即安装应用。</span><span class="sxs-lookup"><span data-stu-id="c3815-164">If the user has Microsoft Teams running, app installation occurs immediately.</span></span> <span data-ttu-id="c3815-165">若要查看已安装的应用，可能需要重新启动。</span><span class="sxs-lookup"><span data-stu-id="c3815-165">A restart may be required to view the installed app.</span></span>

### <a name="retrieve-the-conversation-chatid"></a><span data-ttu-id="c3815-166">检索对话 `chatId`</span><span class="sxs-lookup"><span data-stu-id="c3815-166">Retrieve the conversation `chatId`</span></span>

<span data-ttu-id="c3815-167">为用户安装应用时，机器人将收到一个事件通知，其中包含发送主动消息 `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)的必要信息。</span><span class="sxs-lookup"><span data-stu-id="c3815-167">When your app is installed for the user, the bot receives a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that contains the necessary information to send the proactive message.</span></span>

<span data-ttu-id="c3815-168">**Microsoft Graph页面参考：**[获取聊天](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c3815-168">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

1. <span data-ttu-id="c3815-169">必须具有应用的 `{teamsAppInstallationId}` 。</span><span class="sxs-lookup"><span data-stu-id="c3815-169">You must have your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="c3815-170">如果没有，请使用以下内容：</span><span class="sxs-lookup"><span data-stu-id="c3815-170">If you do not have it, use the following:</span></span>

    <span data-ttu-id="c3815-171">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="c3815-171">**HTTP GET** request:</span></span>

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
    ```

    <span data-ttu-id="c3815-172">响应 **的 id** 属性为 `teamsAppInstallationId` 。</span><span class="sxs-lookup"><span data-stu-id="c3815-172">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

1. <span data-ttu-id="c3815-173">提出以下请求以提取 `chatId` ：</span><span class="sxs-lookup"><span data-stu-id="c3815-173">Make the following request to fetch the `chatId`:</span></span>

    <span data-ttu-id="c3815-174">**HTTP GET** 请求 (权限 — `TeamsAppInstallation.ReadWriteSelfForUser.All`) ：</span><span class="sxs-lookup"><span data-stu-id="c3815-174">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
    ```

    <span data-ttu-id="c3815-175">响应 **的 id** 属性为 `chatId` 。</span><span class="sxs-lookup"><span data-stu-id="c3815-175">The **id** property of the response is the `chatId`.</span></span>

    <span data-ttu-id="c3815-176">还可以检索具有以下 `chatId` 请求的 ，但需要更广泛的 `Chat.Read.All` 权限：</span><span class="sxs-lookup"><span data-stu-id="c3815-176">You can also retrieve the `chatId` with the following request but it requires the broader `Chat.Read.All` permission:</span></span>

    <span data-ttu-id="c3815-177">**HTTP GET** 请求 (权限 — `Chat.Read.All`) ：</span><span class="sxs-lookup"><span data-stu-id="c3815-177">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
    ```

### <a name="send-proactive-messages"></a><span data-ttu-id="c3815-178">发送主动邮件</span><span class="sxs-lookup"><span data-stu-id="c3815-178">Send proactive messages</span></span>

<span data-ttu-id="c3815-179">自动程序 [可以在为用户或](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) 团队添加自动程序并接收所有用户信息后发送主动消息。</span><span class="sxs-lookup"><span data-stu-id="c3815-179">Your bot can [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) after the bot has been added for a user or a team, and has received all the user information.</span></span>

## <a name="code-sample"></a><span data-ttu-id="c3815-180">代码示例</span><span class="sxs-lookup"><span data-stu-id="c3815-180">Code sample</span></span>

| <span data-ttu-id="c3815-181">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="c3815-181">**Sample Name**</span></span> | <span data-ttu-id="c3815-182">**说明**</span><span class="sxs-lookup"><span data-stu-id="c3815-182">**Description**</span></span> | <span data-ttu-id="c3815-183">**.NET**</span><span class="sxs-lookup"><span data-stu-id="c3815-183">**.NET**</span></span> | <span data-ttu-id="c3815-184">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="c3815-184">**Node.js**</span></span> |
|---------------|--------------|--------|-------------|--------|
| <span data-ttu-id="c3815-185">主动安装应用并发送主动通知</span><span class="sxs-lookup"><span data-stu-id="c3815-185">Proactive installation of app and sending proactive notifications</span></span> | <span data-ttu-id="c3815-186">此示例演示如何使用用户主动安装应用，以及如何通过调用 Microsoft Graph发送主动通知。</span><span class="sxs-lookup"><span data-stu-id="c3815-186">This sample shows how you can use proactive installation of app for users and send proactive notifications by calling Microsoft Graph APIs.</span></span> | [<span data-ttu-id="c3815-187">View</span><span class="sxs-lookup"><span data-stu-id="c3815-187">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [<span data-ttu-id="c3815-188">View</span><span class="sxs-lookup"><span data-stu-id="c3815-188">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) |

## <a name="see-also"></a><span data-ttu-id="c3815-189">另请参阅</span><span class="sxs-lookup"><span data-stu-id="c3815-189">See also</span></span>

* [<span data-ttu-id="c3815-190">**在应用中管理应用Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="c3815-190">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [<span data-ttu-id="c3815-191">向用户发送主动通知 SDK v4</span><span class="sxs-lookup"><span data-stu-id="c3815-191">Send proactive notifications to users SDK v4</span></span>](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="additional-code-samples"></a><span data-ttu-id="c3815-192">其他代码示例</span><span class="sxs-lookup"><span data-stu-id="c3815-192">Additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="c3815-193">**Teams主动邮件代码示例**</span><span class="sxs-lookup"><span data-stu-id="c3815-193">**Teams proactive messaging code samples**</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)
