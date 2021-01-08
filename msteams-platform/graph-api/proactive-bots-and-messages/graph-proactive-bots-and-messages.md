---
title: 使用 Microsoft Graph 在 Teams 中启用主动机器人安装和消息传递
description: 介绍 Teams 中的主动消息传递以及如何实现。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams 主动消息聊天安装图
ms.openlocfilehash: ee1620c8fdcaeeecf0e8b0992017bf6f2fbacbf9
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731970"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a><span data-ttu-id="2d45e-104">使用 Microsoft Graph 公共预览版在 Teams 中启用主动自动 (和主动) </span><span class="sxs-lookup"><span data-stu-id="2d45e-104">Enable proactive bot installation and proactive messaging in Teams with Microsoft Graph (Public Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="2d45e-105">Microsoft Graph 和 Microsoft Teams 公共预览版可用于早期访问和反馈。</span><span class="sxs-lookup"><span data-stu-id="2d45e-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="2d45e-106">尽管此版本已经过大量测试，但不适合在生产中使用。</span><span class="sxs-lookup"><span data-stu-id="2d45e-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="2d45e-107">Teams 中的主动消息传递</span><span class="sxs-lookup"><span data-stu-id="2d45e-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="2d45e-108">主动消息由机器人启动，以开始与用户的对话。</span><span class="sxs-lookup"><span data-stu-id="2d45e-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="2d45e-109">它们用于多种用途，包括发送欢迎消息、开展调查或投票以及广播组织范围内的通知。</span><span class="sxs-lookup"><span data-stu-id="2d45e-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span>  <span data-ttu-id="2d45e-110">Teams 中的主动消息可以作为临时对话 **或** 基于对话 **的对话** 传递：</span><span class="sxs-lookup"><span data-stu-id="2d45e-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="2d45e-111">消息类型</span><span class="sxs-lookup"><span data-stu-id="2d45e-111">Message Type</span></span> | <span data-ttu-id="2d45e-112">说明</span><span class="sxs-lookup"><span data-stu-id="2d45e-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="2d45e-113">临时主动消息</span><span class="sxs-lookup"><span data-stu-id="2d45e-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="2d45e-114">自动程序在未中断对话流的情况下干扰消息。</span><span class="sxs-lookup"><span data-stu-id="2d45e-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="2d45e-115">基于对话框的主动消息</span><span class="sxs-lookup"><span data-stu-id="2d45e-115">Dialog-based proactive message</span></span> | <span data-ttu-id="2d45e-116">机器人创建新的对话框线程、控制对话、传递主动消息、关闭并返回对上一对话框的控制。</span><span class="sxs-lookup"><span data-stu-id="2d45e-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

<span data-ttu-id="2d45e-117">*请参阅*， [向用户 SDK v4 发送主动通知](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2d45e-117">*See*, [Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)</span></span>

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="2d45e-118">Teams 中的主动应用安装</span><span class="sxs-lookup"><span data-stu-id="2d45e-118">Proactive app installation in Teams</span></span>

<span data-ttu-id="2d45e-119">在自动程序可以主动向用户发送消息之前，需要以个人应用或用户为成员的团队进行安装。</span><span class="sxs-lookup"><span data-stu-id="2d45e-119">Before your bot can proactively message a user, it needs to be installed either as a personal app, or in a team where the user is a member.</span></span> <span data-ttu-id="2d45e-120">有时，你可能需要主动向尚未安装或之前与你的应用交互的用户发送消息。</span><span class="sxs-lookup"><span data-stu-id="2d45e-120">At times,  you may need to proactively message users that have _not_ installed or previously interacted with your app.</span></span> <span data-ttu-id="2d45e-121">例如，需要向组织中的每个人发送重要信息。</span><span class="sxs-lookup"><span data-stu-id="2d45e-121">For instance, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="2d45e-122">对于此类方案，可以使用 Microsoft Graph API 主动为用户安装自动程序。</span><span class="sxs-lookup"><span data-stu-id="2d45e-122">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="2d45e-123">权限</span><span class="sxs-lookup"><span data-stu-id="2d45e-123">Permissions</span></span>

<span data-ttu-id="2d45e-124">Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) 资源类型权限允许你在 Microsoft Teams 平台内管理用户 (个人) 或团队 (频道) 范围的应用的安装生命周期：</span><span class="sxs-lookup"><span data-stu-id="2d45e-124">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions allow you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="2d45e-125">应用权限</span><span class="sxs-lookup"><span data-stu-id="2d45e-125">Application permission</span></span> | <span data-ttu-id="2d45e-126">说明</span><span class="sxs-lookup"><span data-stu-id="2d45e-126">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="2d45e-127">允许 Teams 应用为任何用户读取、安装、升级和卸载自身，而无需事先登录或使用。</span><span class="sxs-lookup"><span data-stu-id="2d45e-127">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="2d45e-128">允许 Teams 应用在任何团队中读取、安装、升级和卸载自身，而无需事先登录或使用。</span><span class="sxs-lookup"><span data-stu-id="2d45e-128">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="2d45e-129">若要使用这些权限，必须将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：</span><span class="sxs-lookup"><span data-stu-id="2d45e-129">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="2d45e-130">**id**  — Azure AD 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="2d45e-130">**id**  — your Azure AD app id.</span></span>
> * <span data-ttu-id="2d45e-131">**资源** — 应用的资源 URL。</span><span class="sxs-lookup"><span data-stu-id="2d45e-131">**resource** — the resource URL for the app.</span></span>
>

>[!NOTE]
>
> * <span data-ttu-id="2d45e-132">您的自动 _程序需要_ 应用程序而不是用户 _委派_ 的权限，因为安装并非针对自己，而对于其他人。</span><span class="sxs-lookup"><span data-stu-id="2d45e-132">Your bot requires _application_ not _user delegated_ permissions because the installation is not for yourself but for others.</span></span>
>
> * <span data-ttu-id="2d45e-133">Azure AD 租户管理员必须 [明确授予对应用程序的权限](/graph/security-authorization#grant-permissions-to-an-application)。</span><span class="sxs-lookup"><span data-stu-id="2d45e-133">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="2d45e-134">向应用程序授予权限后，Azure AD 租户的所有成员都将获得授予的权限。 </span><span class="sxs-lookup"><span data-stu-id="2d45e-134">After an application is granted permissions, _all_ members of the Azure AD tenant will gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="2d45e-135">启用主动应用安装和消息传递</span><span class="sxs-lookup"><span data-stu-id="2d45e-135">Enable proactive app installation and messaging</span></span>

 > [!IMPORTANT]
><span data-ttu-id="2d45e-136">Microsoft Graph 将仅安装在组织的应用目录或[](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) [AppSource 中发布的应用](https://appsource.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="2d45e-136">Microsoft Graph will only install apps published within your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="2d45e-137">✔为 Teams 创建和发布主动消息自动程序</span><span class="sxs-lookup"><span data-stu-id="2d45e-137">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="2d45e-138">若要开始，你需要一个具有主动消息传递功能的[Teams](../../bots/how-to/create-a-bot-for-teams.md)自动程序，并发布到[](../../concepts/deploy-and-publish/overview.md)组织的应用目录或[AppSource 中](https://appsource.microsoft.com/)。 [](../../concepts/bots/bot-conversations/bots-conv-proactive.md) [](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)</span><span class="sxs-lookup"><span data-stu-id="2d45e-138">To get started, you will need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities and  [published](../../concepts/deploy-and-publish/overview.md) in your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

>[!TIP]
> <span data-ttu-id="2d45e-139">生产就绪型 [**公司Communicator**](../..//samples/app-templates.md#company-communicator) 模板支持广播消息，是构建主动式机器人应用程序的良好基础。</span><span class="sxs-lookup"><span data-stu-id="2d45e-139">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template enables broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="2d45e-140">✔获取 `teamsAppId` 应用</span><span class="sxs-lookup"><span data-stu-id="2d45e-140">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="2d45e-141">**1.** 需要执行 `teamsAppId`  以下步骤。</span><span class="sxs-lookup"><span data-stu-id="2d45e-141">**1.** You will need the `teamsAppId`  for the next steps.</span></span>

<span data-ttu-id="2d45e-142">`teamsAppId`可以从组织的应用程序目录中检索：</span><span class="sxs-lookup"><span data-stu-id="2d45e-142">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="2d45e-143">**Microsoft Graph 页面参考**[：teamsApp 资源类型](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2d45e-143">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

<span data-ttu-id="2d45e-144">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="2d45e-144">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="2d45e-145">请求将返回一 `teamsApp`  个对象。</span><span class="sxs-lookup"><span data-stu-id="2d45e-145">The request will return a `teamsApp`  object.</span></span> <span data-ttu-id="2d45e-146">返回的对象是应用的目录生成的应用 ID，不同于你在 Teams 应用清单中提供的 `id`  "id："：</span><span class="sxs-lookup"><span data-stu-id="2d45e-146">The returned object's `id`  is the app's catalog generated app id and is different from the "id:" that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="2d45e-147">**2.**  如果你的应用已在个人范围内为用户上载/旁加载，你可以按 `teamsAppId` 如下方式检索：</span><span class="sxs-lookup"><span data-stu-id="2d45e-147">**2.**  If your app has already been uploaded/sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="2d45e-148">**Microsoft Graph 页面参考：**[列出为用户安装的应用](/graph/api/userteamwork-list-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2d45e-148">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="2d45e-149">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="2d45e-149">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="2d45e-150">**3.** 如果你的应用已在团队范围内为频道上载/旁加载，你可以按 `teamsAppId` 如下方式检索：</span><span class="sxs-lookup"><span data-stu-id="2d45e-150">**3.** If your app has already been uploaded/sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="2d45e-151">**Microsoft Graph 页面参考：**[列出团队中的应用](/graph/api/team-list-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2d45e-151">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="2d45e-152">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="2d45e-152">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="2d45e-153">可以筛选 [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) 对象的任何字段以缩小结果列表。</span><span class="sxs-lookup"><span data-stu-id="2d45e-153">You can filter on any of the fields of the [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object to narrow the list of results.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="2d45e-154">✔确定当前是否已为邮件收件人安装自动程序</span><span class="sxs-lookup"><span data-stu-id="2d45e-154">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="2d45e-155">**Microsoft Graph 页面参考：**[列出为用户安装的应用](/graph/api/userteamwork-list-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2d45e-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="2d45e-156">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="2d45e-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="2d45e-157">如果未安装应用，此请求将返回空数组;如果已安装，则返回包含单个 [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta&preserve-view=true) 对象的数组。</span><span class="sxs-lookup"><span data-stu-id="2d45e-157">This request will return an empty array if the app is not installed, or an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta&preserve-view=true) object if it has been installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="2d45e-158">✔安装应用</span><span class="sxs-lookup"><span data-stu-id="2d45e-158">✔ Install your app</span></span>

<span data-ttu-id="2d45e-159">**Microsoft Graph 页面参考：**[为用户安装应用](/graph/api/userteamwork-post-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2d45e-159">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="2d45e-160">**HTTP POST** 请求：</span><span class="sxs-lookup"><span data-stu-id="2d45e-160">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="2d45e-161">如果用户正在运行 Microsoft Teams，他们可能会立即看到应用安装。</span><span class="sxs-lookup"><span data-stu-id="2d45e-161">If the user has Microsoft Teams running, they may see the app install immediately.</span></span> <span data-ttu-id="2d45e-162">或者，可能需要重新启动才能看到已安装的应用。</span><span class="sxs-lookup"><span data-stu-id="2d45e-162">Alternatively,  a  restart may be necessary to see the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="2d45e-163">✔检索 **对话 chatId**</span><span class="sxs-lookup"><span data-stu-id="2d45e-163">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="2d45e-164">为用户安装应用时，自动程序将收到一个事件通知，其中包含发送主动消息 `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)的必要信息。</span><span class="sxs-lookup"><span data-stu-id="2d45e-164">When your app is installed for the user, the bot will receive a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that will contain the necessary information to send the proactive message.</span></span>

<span data-ttu-id="2d45e-165">`chatId`也可以按如下方式检索：</span><span class="sxs-lookup"><span data-stu-id="2d45e-165">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="2d45e-166">**Microsoft Graph 页面参考：**[获取聊天](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2d45e-166">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="2d45e-167">**1.** 你将需要你的应用 `{teamsAppInstallationId}` 。</span><span class="sxs-lookup"><span data-stu-id="2d45e-167">**1.** You will need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="2d45e-168">如果没有，请使用以下内容：</span><span class="sxs-lookup"><span data-stu-id="2d45e-168">If you don't have it, use the following:</span></span>

<span data-ttu-id="2d45e-169">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="2d45e-169">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="2d45e-170">响应 **的 id** 属性是 `teamsAppInstallationId` 。</span><span class="sxs-lookup"><span data-stu-id="2d45e-170">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="2d45e-171">**2.** 提出以下请求以提取 `chatId` ：</span><span class="sxs-lookup"><span data-stu-id="2d45e-171">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="2d45e-172">**HTTP GET** 请求 (权限 — `TeamsAppInstallation.ReadWriteSelfForUser.All`) ：</span><span class="sxs-lookup"><span data-stu-id="2d45e-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="2d45e-173">响应 **的 id** 属性是 `chatId` 。</span><span class="sxs-lookup"><span data-stu-id="2d45e-173">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="2d45e-174">或者，您可以使用下面的请求检索， `chatId`  但需要更广泛的 `Chat.Read.All` 权限：</span><span class="sxs-lookup"><span data-stu-id="2d45e-174">Alternately, you can retrieve the `chatId`  with the request below, but it will require the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="2d45e-175">**HTTP GET** 请求 (权限 — `Chat.Read.All`) ：</span><span class="sxs-lookup"><span data-stu-id="2d45e-175">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="2d45e-176">✔发送主动邮件</span><span class="sxs-lookup"><span data-stu-id="2d45e-176">✔ Send proactive messages</span></span>

<span data-ttu-id="2d45e-177">为用户或团队添加自动程序并获取必要的用户信息后，它就可以开始发送 [主动消息](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="2d45e-177">Once your bot has been added for a user or team and has acquired the necessary user  information, it can begin to [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span></span>

# <a name="c--net"></a>[<span data-ttu-id="2d45e-178">C# / .NET</span><span class="sxs-lookup"><span data-stu-id="2d45e-178">C# / .NET</span></span>](#tab/csharp)

<span data-ttu-id="2d45e-179">以下代码段来自适用于 C# 的 [Microsoft Bot Framework 示例。](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span><span class="sxs-lookup"><span data-stu-id="2d45e-179">The following code snippet is from the [Microsoft Bot Framework Samples for C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="2d45e-180">JavaScript</span><span class="sxs-lookup"><span data-stu-id="2d45e-180">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="2d45e-181">以下代码段来自 [适用于 JavaScript 的 Microsoft Bot Framework 示例](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages)。</span><span class="sxs-lookup"><span data-stu-id="2d45e-181">The following code snippet is from the [Microsoft Bot Framework Samples for JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).</span></span>

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

## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="2d45e-182">适用于 Teams 管理员的相关主题</span><span class="sxs-lookup"><span data-stu-id="2d45e-182">Related topic for Teams administrators</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2d45e-183">**在 Teams 中管理应用设置策略**</span><span class="sxs-lookup"><span data-stu-id="2d45e-183">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a><span data-ttu-id="2d45e-184">查看其他代码示例</span><span class="sxs-lookup"><span data-stu-id="2d45e-184">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2d45e-185">**Teams 主动邮件代码示例**</span><span class="sxs-lookup"><span data-stu-id="2d45e-185">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
