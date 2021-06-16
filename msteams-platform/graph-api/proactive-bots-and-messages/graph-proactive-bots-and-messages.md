---
title: 使用 Microsoft Graph授权主动自动程序安装和邮件Teams
description: 介绍企业中的主动Teams以及如何实现。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams 主动消息聊天安装Graph
ms.openlocfilehash: db36c64e557b90699bb09e77dc67ca4c9a8e5853
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949663"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a><span data-ttu-id="5c9c2-104">使用 Graph API 主动安装应用以发送消息</span><span class="sxs-lookup"><span data-stu-id="5c9c2-104">Proactive installation of apps using Graph API to send messages</span></span>

>[!IMPORTANT]
> <span data-ttu-id="5c9c2-105">Microsoft Graph公共Microsoft Teams预览版可供早期访问和反馈使用。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-105">Microsoft Graph and Microsoft Teams public previews are available for early access and feedback.</span></span> <span data-ttu-id="5c9c2-106">尽管此版本已经过大量测试，但不适合在生产中使用。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="5c9c2-107">邮件中的主动Teams</span><span class="sxs-lookup"><span data-stu-id="5c9c2-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="5c9c2-108">主动消息由机器人启动，以开始与用户的对话。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="5c9c2-109">它们用于多种用途，包括发送欢迎消息、开展调查或投票以及广播组织范围内的通知。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span> <span data-ttu-id="5c9c2-110">邮件中的Teams消息 **可以临时对话** 或基于对话 **的对话传递：**</span><span class="sxs-lookup"><span data-stu-id="5c9c2-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="5c9c2-111">消息类型</span><span class="sxs-lookup"><span data-stu-id="5c9c2-111">Message Type</span></span> | <span data-ttu-id="5c9c2-112">说明</span><span class="sxs-lookup"><span data-stu-id="5c9c2-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="5c9c2-113">临时主动邮件</span><span class="sxs-lookup"><span data-stu-id="5c9c2-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="5c9c2-114">机器人在不中断对话流的情况下与消息进行交互。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="5c9c2-115">基于对话框的主动消息</span><span class="sxs-lookup"><span data-stu-id="5c9c2-115">Dialog-based proactive message</span></span> | <span data-ttu-id="5c9c2-116">机器人创建新的对话线程、控制对话、传递主动消息、关闭并返回对上一对话框的控制。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="5c9c2-117">在应用中主动安装Teams</span><span class="sxs-lookup"><span data-stu-id="5c9c2-117">Proactive app installation in Teams</span></span>

<span data-ttu-id="5c9c2-118">在自动程序可以主动向用户发送消息之前，它必须作为个人应用或用户是成员的团队进行安装。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-118">Before your bot can proactively message a user, it must be installed either as a personal app or in a team where the user is a member.</span></span> <span data-ttu-id="5c9c2-119">有时，你需要主动向尚未安装或之前与你的应用交互的用户发送消息。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-119">At times, you need to proactively message users that have not installed or previously interacted with your app.</span></span> <span data-ttu-id="5c9c2-120">例如，需要向组织中的每个人发送重要信息。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-120">For example, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="5c9c2-121">对于此类方案，可以使用 Microsoft Graph API 主动为用户安装自动程序。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-121">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="5c9c2-122">权限</span><span class="sxs-lookup"><span data-stu-id="5c9c2-122">Permissions</span></span>

<span data-ttu-id="5c9c2-123">Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true)资源类型权限可帮助你管理 Microsoft Teams 平台内所有 (个人) 或团队 (频道) 范围的应用的安装生命周期：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-123">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions helps you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="5c9c2-124">应用权限</span><span class="sxs-lookup"><span data-stu-id="5c9c2-124">Application permission</span></span> | <span data-ttu-id="5c9c2-125">说明</span><span class="sxs-lookup"><span data-stu-id="5c9c2-125">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="5c9c2-126">允许Teams应用为任何用户读取、安装、升级和卸载自身，而无需事先登录或使用。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-126">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="5c9c2-127">允许Teams应用在任何团队中读取、安装、升级和卸载自身，而无需事先登录或使用。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-127">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="5c9c2-128">若要使用这些权限，必须将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-128">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="5c9c2-129">**id** — 你的 Azure AD 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-129">**id** — your Azure AD app ID.</span></span>
> * <span data-ttu-id="5c9c2-130">**resource** — 应用的资源 URL。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-130">**resource** — the resource URL for the app.</span></span>
>
>[!NOTE]
>
> * <span data-ttu-id="5c9c2-131">自动程序需要应用程序权限，而不是用户委派权限，因为安装适用于其他人。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-131">Your bot requires application and not user delegated permissions because the installation is for others.</span></span>
>
> * <span data-ttu-id="5c9c2-132">Azure AD 租户管理员 [必须明确授予对应用程序的权限](/graph/security-authorization#grant-permissions-to-an-application)。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-132">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="5c9c2-133">向应用程序授予权限后，Azure AD 租户的所有成员都将获得已授予的权限。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-133">After an application is granted permissions, all members of the Azure AD tenant gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="5c9c2-134">启用主动应用安装和消息传递</span><span class="sxs-lookup"><span data-stu-id="5c9c2-134">Enable proactive app installation and messaging</span></span>

> [!IMPORTANT]
><span data-ttu-id="5c9c2-135">Microsoft Graph只能安装发布到组织的应用商店或应用商店Teams应用。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-135">Microsoft Graph can only install apps published to your organization's app store or the Teams store.</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="5c9c2-136">✔创建并发布主动邮件自动程序Teams</span><span class="sxs-lookup"><span data-stu-id="5c9c2-136">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="5c9c2-137">若要开始，你需要一个自动[](../../bots/how-to/create-a-bot-for-teams.md)程序Teams组织应用商店或应用商店中的[](../../concepts/bots/bot-conversations/bots-conv-proactive.md)主动邮件Teams[功能](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)。 [](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org)</span><span class="sxs-lookup"><span data-stu-id="5c9c2-137">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that's in your [organization's app store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) or the [Teams store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span></span>

>[!TIP]
> <span data-ttu-id="5c9c2-138">生产就绪型 [**公司Communicator**](../..//samples/app-templates.md#company-communicator)模板允许广播消息，它是构建主动式机器人应用程序的良好基础。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-138">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template permits broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="5c9c2-139">✔获取 `teamsAppId` 应用的</span><span class="sxs-lookup"><span data-stu-id="5c9c2-139">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="5c9c2-140">**1。** 需要 执行 `teamsAppId` 以下步骤。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-140">**1.** You need the `teamsAppId` for the next steps.</span></span>

<span data-ttu-id="5c9c2-141">`teamsAppId`可以从组织的应用程序目录中检索：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-141">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="5c9c2-142">**Microsoft Graph 页面参考**[：teamsApp 资源类型](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="5c9c2-142">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

<span data-ttu-id="5c9c2-143">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-143">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="5c9c2-144">请求必须返回 `teamsApp` 对象。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-144">The request must return a `teamsApp` object.</span></span> <span data-ttu-id="5c9c2-145">返回的对象是应用的目录生成的应用程序 ID，并且不同于在应用程序清单中Teams `id` ID：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-145">The returned object `id` is the app's catalog generated app ID and is different from the ID that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="5c9c2-146">**2.**  如果你的应用已在个人范围内为用户上载或旁加载，可以按 `teamsAppId` 如下方式检索：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-146">**2.**  If your app has already been uploaded or sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="5c9c2-147">**Microsoft Graph页面参考：**[列出为用户安装的应用](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="5c9c2-147">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="5c9c2-148">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-148">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="5c9c2-149">**3.** 如果你的应用已针对团队作用域中的频道上载或旁加载，可以按 `teamsAppId` 如下方式检索：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-149">**3.** If your app has been uploaded or sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="5c9c2-150">**Microsoft Graph页面参考：**[列出团队中的应用](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="5c9c2-150">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="5c9c2-151">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-151">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="5c9c2-152">若要缩小结果列表，可以筛选 [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) 对象的任何字段。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-152">To narrow the list of results, you can filter on any of the fields of [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="5c9c2-153">✔确定当前是否已为邮件收件人安装自动程序</span><span class="sxs-lookup"><span data-stu-id="5c9c2-153">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="5c9c2-154">**Microsoft Graph页面参考：**[列出为用户安装的应用](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="5c9c2-154">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="5c9c2-155">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-155">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="5c9c2-156">如果未安装应用，此请求将返回空数组;如果已安装应用，则返回包含单个 [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) 对象的数组。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-156">This request returns an empty array if the app is not installed and an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if the app is installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="5c9c2-157">✔安装应用</span><span class="sxs-lookup"><span data-stu-id="5c9c2-157">✔ Install your app</span></span>

<span data-ttu-id="5c9c2-158">**Microsoft Graph页面参考：**[为用户安装应用](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="5c9c2-158">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="5c9c2-159">**HTTP POST** 请求：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-159">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="5c9c2-160">如果用户已运行Microsoft Teams，将立即看到应用安装。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-160">If the user has Microsoft Teams running, app installation is seen immediately.</span></span> <span data-ttu-id="5c9c2-161">若要查看已安装的应用，可能需要重新启动。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-161">A restart may be required to view the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="5c9c2-162">✔检索对话 **chatId**</span><span class="sxs-lookup"><span data-stu-id="5c9c2-162">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="5c9c2-163">为用户安装应用时，机器人将收到一个事件通知，其中包含发送主动消息 `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)的必要信息。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-163">When your app is installed for the user, the bot receives a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that contains the necessary information to send the proactive message.</span></span>

<span data-ttu-id="5c9c2-164">`chatId`也可以按如下方式检索：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-164">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="5c9c2-165">**Microsoft Graph页面参考：**[获取聊天](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="5c9c2-165">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="5c9c2-166">**1。** 你必须需要你的应用 `{teamsAppInstallationId}` 的 。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-166">**1.** You must need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="5c9c2-167">如果没有，请使用以下内容：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-167">If you don't have it, use the following:</span></span>

<span data-ttu-id="5c9c2-168">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-168">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="5c9c2-169">响应 **的 id** 属性为 `teamsAppInstallationId` 。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-169">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="5c9c2-170">**2.** 提出以下请求来获取 `chatId` ：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-170">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="5c9c2-171">**HTTP GET** 请求 (权限 — `TeamsAppInstallation.ReadWriteSelfForUser.All`) ：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-171">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="5c9c2-172">响应 **的 id** 属性为 `chatId` 。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-172">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="5c9c2-173">还可以检索具有以下 `chatId` 请求的 ，但需要更广泛的 `Chat.Read.All` 权限：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-173">You can also retrieve the `chatId` with the following request but it requires the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="5c9c2-174">**HTTP GET** 请求 (权限 — `Chat.Read.All`) ：</span><span class="sxs-lookup"><span data-stu-id="5c9c2-174">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="5c9c2-175">✔发送主动邮件</span><span class="sxs-lookup"><span data-stu-id="5c9c2-175">✔ Send proactive messages</span></span>

<span data-ttu-id="5c9c2-176">自动程序 [可以在为用户或](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) 团队添加自动程序并接收所有用户信息后发送主动消息。</span><span class="sxs-lookup"><span data-stu-id="5c9c2-176">Your bot can [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) after the bot has been added for a user or a team and has received all the user information.</span></span>

## <a name="see-also"></a><span data-ttu-id="5c9c2-177">另请参阅</span><span class="sxs-lookup"><span data-stu-id="5c9c2-177">See also</span></span>

* [<span data-ttu-id="5c9c2-178">**在应用中管理应用Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="5c9c2-178">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [<span data-ttu-id="5c9c2-179">向用户发送主动通知 SDK v4</span><span class="sxs-lookup"><span data-stu-id="5c9c2-179">Send proactive notifications to users SDK v4</span></span>](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="view-additional-code-samples"></a><span data-ttu-id="5c9c2-180">查看其他代码示例</span><span class="sxs-lookup"><span data-stu-id="5c9c2-180">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5c9c2-181">**Teams主动邮件代码示例**</span><span class="sxs-lookup"><span data-stu-id="5c9c2-181">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
