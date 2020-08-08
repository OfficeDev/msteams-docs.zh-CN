---
title: 使用 Microsoft Graph 在团队中启用主动备机器人安装和邮件功能
description: 介绍了如何在团队中进行主动消息传递以及如何实现。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: 团队前瞻性消息聊天安装图
ms.openlocfilehash: f1d2c51957eefbc548918210b843e408eb1107c8
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587739"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a><span data-ttu-id="fa8a0-104">使用 Microsoft Graph (公共预览版在团队中启用主动备机器人安装和主动消息) </span><span class="sxs-lookup"><span data-stu-id="fa8a0-104">Enable proactive bot installation and proactive messaging in Teams with Microsoft Graph (Public Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="fa8a0-105">Microsoft Graph 公共预览版适用于早期访问和反馈。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-105">Microsoft Graph public previews are available for early-access and feedback.</span></span> <span data-ttu-id="fa8a0-106">尽管此版本已经历大量测试，但不适合在生产中使用。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="fa8a0-107">团队中的主动消息</span><span class="sxs-lookup"><span data-stu-id="fa8a0-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="fa8a0-108">启动由 bot 启动与用户的对话的主动消息。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="fa8a0-109">它们可用于多种用途，包括发送欢迎邮件、执行调查或投票以及广播组织范围内的通知。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span>  <span data-ttu-id="fa8a0-110">可以将团队**中的主动**消息作为临时或**基于对话框的**对话进行传递：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="fa8a0-111">消息类型</span><span class="sxs-lookup"><span data-stu-id="fa8a0-111">Message Type</span></span> | <span data-ttu-id="fa8a0-112">说明</span><span class="sxs-lookup"><span data-stu-id="fa8a0-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="fa8a0-113">临时的主动消息</span><span class="sxs-lookup"><span data-stu-id="fa8a0-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="fa8a0-114">Bot 在不中断对话流的情况下 interjects 邮件。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="fa8a0-115">基于对话框的主动消息</span><span class="sxs-lookup"><span data-stu-id="fa8a0-115">Dialog-based proactive message</span></span> | <span data-ttu-id="fa8a0-116">Bot 将创建一个新的对话线程，控制对话，传递主动消息，关闭并将控制返回到上一个对话框。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

<span data-ttu-id="fa8a0-117">*请参阅*[向用户 SDK v4 发送主动通知](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)</span><span class="sxs-lookup"><span data-stu-id="fa8a0-117">*See*, [Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)</span></span>

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="fa8a0-118">团队中的主动应用安装</span><span class="sxs-lookup"><span data-stu-id="fa8a0-118">Proactive app installation in Teams</span></span>

<span data-ttu-id="fa8a0-119">在你的 bot 可以主动向用户发送邮件之前，它需要安装为个人应用程序，或者安装在用户所属的团队中。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-119">Before your bot can proactively message a user, it needs to be installed either as a personal app, or in a team where the user is a member.</span></span> <span data-ttu-id="fa8a0-120">有时，您可能需要主动向_尚未_安装或之前与您的应用程序交互的用户发送邮件。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-120">At times,  you may need to proactively message users that have _not_ installed or previously interacted with your app.</span></span> <span data-ttu-id="fa8a0-121">例如，需要向组织中的每个人发送重要信息。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-121">For instance, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="fa8a0-122">在这种情况下，您可以使用 Microsoft Graph API 为用户主动安装机器人。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-122">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="fa8a0-123">权限</span><span class="sxs-lookup"><span data-stu-id="fa8a0-123">Permissions</span></span>

<span data-ttu-id="fa8a0-124">Microsoft Graph [teamsAppInstallation 资源类型](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0)权限允许您在 Microsoft 团队平台中管理所有用户 (个人) 或团队 (频道) 范围的应用程序安装生命周期：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-124">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) permissions allow you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="fa8a0-125">应用权限</span><span class="sxs-lookup"><span data-stu-id="fa8a0-125">Application permission</span></span> | <span data-ttu-id="fa8a0-126">说明</span><span class="sxs-lookup"><span data-stu-id="fa8a0-126">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="fa8a0-127">允许工作组应用在未登录或使用之前为任何**用户**读取、安装、升级和卸载自己。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-127">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="fa8a0-128">允许团队应用在未登录或使用之前，在任何**团队**中读取、安装、升级和卸载自己。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-128">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="fa8a0-129">若要使用这些权限，您必须将[webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo)密钥添加到您的应用程序清单中，其中包含以下值：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-129">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="fa8a0-130">**id** —您的 Azure AD 应用程序 id。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-130">**id**  — your Azure AD app id.</span></span>
> * <span data-ttu-id="fa8a0-131">**资源**—应用程序的资源 URL。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-131">**resource** — the resource URL for the app.</span></span>
>

>[!NOTE]
>
> * <span data-ttu-id="fa8a0-132">你的 bot 需要_应用程序_不是_用户委派_的权限，因为安装不是你自己的，而是供其他人访问。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-132">Your bot requires _application_ not _user delegated_ permissions because the installation is not for yourself but for others.</span></span>
>
> * <span data-ttu-id="fa8a0-133">Azure AD 租户管理员必须[显式授予对应用程序的权限](/graph/security-authorization#grant-permissions-to-an-application)。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-133">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="fa8a0-134">在向应用程序授予权限后，Azure AD 租户的_所有_成员都将获得已授予的权限。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-134">After an application is granted permissions, _all_ members of the Azure AD tenant will gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="fa8a0-135">启用主动应用安装和邮件传递</span><span class="sxs-lookup"><span data-stu-id="fa8a0-135">Enable proactive app installation and messaging</span></span>

 > [!IMPORTANT]
><span data-ttu-id="fa8a0-136">Microsoft Graph 将仅安装在组织的[应用程序目录](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)或[AppSource](https://appsource.microsoft.com/)中发布的应用程序。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-136">Microsoft Graph will only install apps published within your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="fa8a0-137">✔为团队创建和发布主动消息机器人</span><span class="sxs-lookup"><span data-stu-id="fa8a0-137">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="fa8a0-138">若要开始，你将需要具有[主动消息](../../concepts/bots/bot-conversations/bots-conv-proactive.md)功能且在组织的[应用程序目录](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)或[AppSource](https://appsource.microsoft.com/)中[发布](../../concepts/deploy-and-publish/overview.md)的[团队的 bot](../../bots/how-to/create-a-bot-for-teams.md) 。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-138">To get started, you will need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities and  [published](../../concepts/deploy-and-publish/overview.md) in your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

>[!TIP]
> <span data-ttu-id="fa8a0-139">生产就绪的[**公司 Communicator**](../..//samples/app-templates.md#company-communicator)应用模板支持广播消息传递，是构建主动机器人应用程序的良好基础。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-139">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template enables broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="fa8a0-140">`teamsAppId`为您的应用程序✔获取</span><span class="sxs-lookup"><span data-stu-id="fa8a0-140">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="fa8a0-141">**1.** 你将需要 `teamsAppId` 执行后续步骤。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-141">**1.** You will need the `teamsAppId`  for the next steps.</span></span>

<span data-ttu-id="fa8a0-142">`teamsAppId`可以从组织的应用程序目录中检索：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-142">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="fa8a0-143">**Microsoft Graph 页面参考：** [teamsApp 资源类型](/graph/api/resources/teamsapp?view=graph-rest-1.0)</span><span class="sxs-lookup"><span data-stu-id="fa8a0-143">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0)</span></span>

<span data-ttu-id="fa8a0-144">**HTTP GET**请求：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-144">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="fa8a0-145">请求将返回一个 `teamsApp` 对象。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-145">The request will return a `teamsApp`  object.</span></span> <span data-ttu-id="fa8a0-146">返回的对象 `id` 是应用程序的目录生成的应用程序 id，与您在团队应用程序清单中提供的 "id：" 不同：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-146">The returned object's `id`  is the app's catalog generated app id and is different from the "id:" that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="fa8a0-147">**2.** 如果您的应用程序已为个人范围内的用户上载/旁加载，则可以按如下所示检索 `teamsAppId` ：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-147">**2.**  If your app has already been uploaded/sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="fa8a0-148">**Microsoft Graph 页面参考：** [列出为用户安装的应用程序](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="fa8a0-148">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="fa8a0-149">**HTTP GET**请求：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-149">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="fa8a0-150">**3.** 如果您的应用程序已在团队作用域中的某个频道上传/旁加载，则可以 `teamsAppId` 按如下所示检索：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-150">**3.** If your app has already been uploaded/sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="fa8a0-151">**Microsoft Graph 页面参考：** [列出团队中的应用程序](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="fa8a0-151">**Microsoft Graph page reference:** [List apps in team](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="fa8a0-152">**HTTP GET**请求：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-152">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{manifestId}'
```

>[!TIP]
> <span data-ttu-id="fa8a0-153">您可以对[**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0)对象的任何字段进行筛选以缩小结果列表的范围。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-153">You can filter on any of the fields of the [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0) object to narrow the list of results.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="fa8a0-154">✔确定当前是否为邮件收件人安装了你的 bot</span><span class="sxs-lookup"><span data-stu-id="fa8a0-154">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="fa8a0-155">**Microsoft Graph 页面参考：** [列出为用户安装的应用程序](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="fa8a0-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="fa8a0-156">**HTTP GET**请求：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="fa8a0-157">如果未安装应用程序，则此请求将返回一个空数组; 如果已安装，则返回一个包含一个[teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta)对象的数组。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-157">This request will return an empty array if the app is not installed, or an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) object if it has been installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="fa8a0-158">✔安装您的应用程序</span><span class="sxs-lookup"><span data-stu-id="fa8a0-158">✔ Install your app</span></span>

<span data-ttu-id="fa8a0-159">**Microsoft Graph 参考：** [为用户安装应用程序](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="fa8a0-159">**Microsoft Graph reference:** [Install app for user](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="fa8a0-160">**HTTP POST**请求：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-160">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="fa8a0-161">如果用户运行的是 Microsoft 团队，他们可能会立即看到应用安装。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-161">If the user has Microsoft Teams running, they may see the app install immediately.</span></span> <span data-ttu-id="fa8a0-162">或者，可能需要重新启动才能查看已安装的应用程序。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-162">Alternatively,  a  restart may be necessary to see the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="fa8a0-163">✔检索对话**chatId**</span><span class="sxs-lookup"><span data-stu-id="fa8a0-163">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="fa8a0-164">为用户安装您的应用程序时，bot 将收到 `conversationUpdate` [事件通知](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)，其中包含发送主动消息所需的信息。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-164">When your app is installed for the user, the bot will receive a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that will contain the necessary information to send the proactive message.</span></span>

<span data-ttu-id="fa8a0-165">`chatId`也可以按如下所示检索：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-165">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="fa8a0-166">**Microsoft Graph 参考：** [获取聊天](/graph/api/chat-get?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="fa8a0-166">**Microsoft Graph reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="fa8a0-167">**1.** 你将需要你的应用程序 `{teamsAppInstallationId}` 。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-167">**1.** You will need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="fa8a0-168">如果你没有此项，请使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-168">If you don't have it, use the following:</span></span>

<span data-ttu-id="fa8a0-169">**HTTP GET**请求：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-169">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="fa8a0-170">响应的**id**属性是 `teamsAppInstallationId` 。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-170">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="fa8a0-171">**2.** 发出以下请求以获取 `chatId` ：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-171">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="fa8a0-172">**HTTP GET**请求 (权限— `TeamsAppInstallation.ReadWriteSelfForUser.All`) ：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="fa8a0-173">响应的**id**属性是 `chatId` 。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-173">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="fa8a0-174">或者，您可以 `chatId` 使用下面的请求检索，但它将需要更广泛的 `Chat.Read.All` 权限：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-174">Alternately, you can retrieve the `chatId`  with the request below, but it will require the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="fa8a0-175">**HTTP GET**请求 (权限— `Chat.Read.All`) ：</span><span class="sxs-lookup"><span data-stu-id="fa8a0-175">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="fa8a0-176">✔发送主动消息</span><span class="sxs-lookup"><span data-stu-id="fa8a0-176">✔ Send proactive messages</span></span>

<span data-ttu-id="fa8a0-177">为用户或团队添加了你的 bot 并获取了必要的用户信息后，即可开始[发送主动消息](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-177">Once your bot has been added for a user or team and has acquired the necessary user  information, it can begin to [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp).</span></span>

# <a name="c--net"></a>[<span data-ttu-id="fa8a0-178">C #/.NET</span><span class="sxs-lookup"><span data-stu-id="fa8a0-178">C# / .NET</span></span>](#tab/csharp)

<span data-ttu-id="fa8a0-179">下面的代码片段来自[c # 的 Microsoft Bot 框架示例。](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span><span class="sxs-lookup"><span data-stu-id="fa8a0-179">The following code snippet is from the [Microsoft Bot Framework Samples for C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="fa8a0-180">JavaScript</span><span class="sxs-lookup"><span data-stu-id="fa8a0-180">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="fa8a0-181">下面的代码片段来自适用于[JavaScript 的 Microsoft Bot 框架示例](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages)。</span><span class="sxs-lookup"><span data-stu-id="fa8a0-181">The following code snippet is from the [Microsoft Bot Framework Samples for JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).</span></span>

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

## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="fa8a0-182">团队管理员的相关主题</span><span class="sxs-lookup"><span data-stu-id="fa8a0-182">Related topic for Teams administrators</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="fa8a0-183">**在 Microsoft 团队中管理应用程序安装策略**</span><span class="sxs-lookup"><span data-stu-id="fa8a0-183">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a><span data-ttu-id="fa8a0-184">查看其他代码示例</span><span class="sxs-lookup"><span data-stu-id="fa8a0-184">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="fa8a0-185">**团队主动消息代码示例**</span><span class="sxs-lookup"><span data-stu-id="fa8a0-185">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
