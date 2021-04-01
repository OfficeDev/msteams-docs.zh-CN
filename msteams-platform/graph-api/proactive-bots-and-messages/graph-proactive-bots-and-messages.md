---
title: 使用 Microsoft Graph 在 Teams 中授权主动安装机器人和消息传递
description: 介绍 Teams 中的主动消息传递以及如何实现。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams 主动消息聊天安装图
ms.openlocfilehash: 4f9c1c2e73fc89d37792e59153affc398bb87044
ms.sourcegitcommit: 3bd2627b7a334568f61ccc606395e3d89aa521d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "51475933"
---
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a><span data-ttu-id="44ba6-104">使用 Graph API 以及发送邮件主动安装应用</span><span class="sxs-lookup"><span data-stu-id="44ba6-104">Proactive installation of apps using Graph API and send messages</span></span>

>[!IMPORTANT]
> <span data-ttu-id="44ba6-105">Microsoft Graph 和 Microsoft Teams 公共预览版可用于早期访问和反馈。</span><span class="sxs-lookup"><span data-stu-id="44ba6-105">Microsoft Graph and Microsoft Teams public previews are available for early access and feedback.</span></span> <span data-ttu-id="44ba6-106">尽管此版本已经过大量测试，但不适合在生产中使用。</span><span class="sxs-lookup"><span data-stu-id="44ba6-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="44ba6-107">Teams 中的主动消息传递</span><span class="sxs-lookup"><span data-stu-id="44ba6-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="44ba6-108">主动消息由机器人启动，以开始与用户的对话。</span><span class="sxs-lookup"><span data-stu-id="44ba6-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="44ba6-109">它们用于多种用途，包括发送欢迎消息、开展调查或投票以及广播组织范围内的通知。</span><span class="sxs-lookup"><span data-stu-id="44ba6-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span> <span data-ttu-id="44ba6-110">Teams 中的主动消息 **可以作为临时** 对话或基于 **对话的对话** 传递：</span><span class="sxs-lookup"><span data-stu-id="44ba6-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="44ba6-111">消息类型</span><span class="sxs-lookup"><span data-stu-id="44ba6-111">Message Type</span></span> | <span data-ttu-id="44ba6-112">说明</span><span class="sxs-lookup"><span data-stu-id="44ba6-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="44ba6-113">临时主动邮件</span><span class="sxs-lookup"><span data-stu-id="44ba6-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="44ba6-114">机器人在不中断对话流的情况下与消息进行交互。</span><span class="sxs-lookup"><span data-stu-id="44ba6-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="44ba6-115">基于对话框的主动消息</span><span class="sxs-lookup"><span data-stu-id="44ba6-115">Dialog-based proactive message</span></span> | <span data-ttu-id="44ba6-116">机器人创建新的对话线程、控制对话、传递主动消息、关闭并返回对上一对话框的控制。</span><span class="sxs-lookup"><span data-stu-id="44ba6-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

<span data-ttu-id="44ba6-117">请参阅向[用户发送主动通知 SDK v4。](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="44ba6-117">See, [Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span></span>

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="44ba6-118">Teams 中的主动应用安装</span><span class="sxs-lookup"><span data-stu-id="44ba6-118">Proactive app installation in Teams</span></span>

<span data-ttu-id="44ba6-119">在自动程序可以主动向用户发送消息之前，它必须作为个人应用或用户是成员的团队进行安装。</span><span class="sxs-lookup"><span data-stu-id="44ba6-119">Before your bot can proactively message a user, it must be installed either as a personal app or in a team where the user is a member.</span></span> <span data-ttu-id="44ba6-120">有时，你需要主动向尚未安装或之前与你的应用交互的用户发送消息。</span><span class="sxs-lookup"><span data-stu-id="44ba6-120">At times, you need to proactively message users that have not installed or previously interacted with your app.</span></span> <span data-ttu-id="44ba6-121">例如，需要向组织中的每个人发送重要信息。</span><span class="sxs-lookup"><span data-stu-id="44ba6-121">For example, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="44ba6-122">对于此类方案，可以使用 Microsoft Graph API 主动为用户安装自动程序。</span><span class="sxs-lookup"><span data-stu-id="44ba6-122">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="44ba6-123">权限</span><span class="sxs-lookup"><span data-stu-id="44ba6-123">Permissions</span></span>

<span data-ttu-id="44ba6-124">Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) 资源类型权限可帮助你管理 Microsoft Teams 平台内所有 (个人) 或团队 () 范围的应用的安装生命周期：</span><span class="sxs-lookup"><span data-stu-id="44ba6-124">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions helps you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="44ba6-125">应用权限</span><span class="sxs-lookup"><span data-stu-id="44ba6-125">Application permission</span></span> | <span data-ttu-id="44ba6-126">说明</span><span class="sxs-lookup"><span data-stu-id="44ba6-126">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="44ba6-127">允许 Teams 应用为任何用户读取、安装、升级和卸载自身，而无需事先登录或使用。</span><span class="sxs-lookup"><span data-stu-id="44ba6-127">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="44ba6-128">允许 Teams 应用在任何团队中读取、安装、升级和卸载自身，而无需事先登录或使用。</span><span class="sxs-lookup"><span data-stu-id="44ba6-128">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="44ba6-129">若要使用这些权限，必须将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：</span><span class="sxs-lookup"><span data-stu-id="44ba6-129">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="44ba6-130">**id** — 你的 Azure AD 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="44ba6-130">**id** — your Azure AD app ID.</span></span>
> * <span data-ttu-id="44ba6-131">**resource** — 应用的资源 URL。</span><span class="sxs-lookup"><span data-stu-id="44ba6-131">**resource** — the resource URL for the app.</span></span>
>
>[!NOTE]
>
> * <span data-ttu-id="44ba6-132">自动程序需要应用程序权限，而不是用户委派权限，因为安装适用于其他人。</span><span class="sxs-lookup"><span data-stu-id="44ba6-132">Your bot requires application and not user delegated permissions because the installation is for others.</span></span>
>
> * <span data-ttu-id="44ba6-133">Azure AD 租户管理员 [必须明确授予对应用程序的权限](/graph/security-authorization#grant-permissions-to-an-application)。</span><span class="sxs-lookup"><span data-stu-id="44ba6-133">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="44ba6-134">向应用程序授予权限后，Azure AD 租户的所有成员都将获得已授予的权限。</span><span class="sxs-lookup"><span data-stu-id="44ba6-134">After an application is granted permissions, all members of the Azure AD tenant gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="44ba6-135">启用主动应用安装和消息传递</span><span class="sxs-lookup"><span data-stu-id="44ba6-135">Enable proactive app installation and messaging</span></span>

 > [!IMPORTANT]
><span data-ttu-id="44ba6-136">Microsoft Graph 只能安装在组织的应用目录或[](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)AppSource 中[发布的应用](https://appsource.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="44ba6-136">Microsoft Graph can only install apps published within your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="44ba6-137">✔为 Teams 创建和发布主动消息机器人</span><span class="sxs-lookup"><span data-stu-id="44ba6-137">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="44ba6-138">若要开始，你需要一个适用于[Teams](../../bots/how-to/create-a-bot-for-teams.md)的[](../../concepts/bots/bot-conversations/bots-conv-proactive.md)自动程序，具有在组织的应用[](../../concepts/deploy-and-publish/overview.md)目录或[AppSource](https://appsource.microsoft.com/)[](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)中发布的主动消息功能。</span><span class="sxs-lookup"><span data-stu-id="44ba6-138">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that is [published](../../concepts/deploy-and-publish/overview.md) in your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

>[!TIP]
> <span data-ttu-id="44ba6-139">生产就绪型 [**公司Communicator**](../..//samples/app-templates.md#company-communicator) 模板允许广播消息，它是构建主动自动程序应用程序的良好基础。</span><span class="sxs-lookup"><span data-stu-id="44ba6-139">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template permits broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="44ba6-140">✔获取 `teamsAppId` 应用的</span><span class="sxs-lookup"><span data-stu-id="44ba6-140">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="44ba6-141">**1。** 需要 执行 `teamsAppId` 以下步骤。</span><span class="sxs-lookup"><span data-stu-id="44ba6-141">**1.** You need the `teamsAppId` for the next steps.</span></span>

<span data-ttu-id="44ba6-142">`teamsAppId`可以从组织的应用程序目录中检索：</span><span class="sxs-lookup"><span data-stu-id="44ba6-142">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="44ba6-143">**Microsoft Graph 页面参考**[：teamsApp 资源类型](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="44ba6-143">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

<span data-ttu-id="44ba6-144">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="44ba6-144">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="44ba6-145">请求必须返回 `teamsApp` 对象。</span><span class="sxs-lookup"><span data-stu-id="44ba6-145">The request must return a `teamsApp` object.</span></span> <span data-ttu-id="44ba6-146">返回的对象是应用的目录生成的应用 ID，不同于你在 Teams 应用清单中提供的 `id` ID：</span><span class="sxs-lookup"><span data-stu-id="44ba6-146">The returned object `id` is the app's catalog generated app ID and is different from the ID that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="44ba6-147">**2.**  如果你的应用已在个人范围内为用户上载或旁加载，可以按 `teamsAppId` 如下方式检索：</span><span class="sxs-lookup"><span data-stu-id="44ba6-147">**2.**  If your app has already been uploaded or sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="44ba6-148">**Microsoft Graph 页面参考：**[列出为用户安装的应用](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="44ba6-148">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="44ba6-149">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="44ba6-149">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="44ba6-150">**3.** 如果你的应用已针对团队作用域中的频道上载或旁加载，可以按 `teamsAppId` 如下方式检索：</span><span class="sxs-lookup"><span data-stu-id="44ba6-150">**3.** If your app has been uploaded or sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="44ba6-151">**Microsoft Graph 页面参考：**[列出团队中的应用](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="44ba6-151">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="44ba6-152">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="44ba6-152">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="44ba6-153">若要缩小结果列表，可以筛选 [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) 对象的任何字段。</span><span class="sxs-lookup"><span data-stu-id="44ba6-153">To narrow the list of results, you can filter on any of the fields of [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="44ba6-154">✔确定当前是否已为邮件收件人安装自动程序</span><span class="sxs-lookup"><span data-stu-id="44ba6-154">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="44ba6-155">**Microsoft Graph 页面参考：**[列出为用户安装的应用](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="44ba6-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="44ba6-156">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="44ba6-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="44ba6-157">如果未安装应用，此请求将返回空数组;如果已安装应用，则返回包含单个 [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) 对象的数组。</span><span class="sxs-lookup"><span data-stu-id="44ba6-157">This request returns an empty array if the app is not installed and an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if the app is installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="44ba6-158">✔安装应用</span><span class="sxs-lookup"><span data-stu-id="44ba6-158">✔ Install your app</span></span>

<span data-ttu-id="44ba6-159">**Microsoft Graph 页面参考：**[为用户安装应用](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="44ba6-159">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="44ba6-160">**HTTP POST** 请求：</span><span class="sxs-lookup"><span data-stu-id="44ba6-160">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="44ba6-161">如果用户正在运行 Microsoft Teams，将立即看到应用安装。</span><span class="sxs-lookup"><span data-stu-id="44ba6-161">If the user has Microsoft Teams running, app installation is seen immediately.</span></span> <span data-ttu-id="44ba6-162">若要查看已安装的应用，可能需要重新启动。</span><span class="sxs-lookup"><span data-stu-id="44ba6-162">A restart may be required to view the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="44ba6-163">✔检索对话 **chatId**</span><span class="sxs-lookup"><span data-stu-id="44ba6-163">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="44ba6-164">为用户安装应用时，机器人将收到一个事件通知，其中包含发送主动消息 `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)的必要信息。</span><span class="sxs-lookup"><span data-stu-id="44ba6-164">When your app is installed for the user, the bot receives a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that contains the necessary information to send the proactive message.</span></span>

<span data-ttu-id="44ba6-165">`chatId`也可以按如下方式检索：</span><span class="sxs-lookup"><span data-stu-id="44ba6-165">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="44ba6-166">**Microsoft Graph 页面参考：**[获取聊天](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="44ba6-166">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="44ba6-167">**1。** 你必须需要你的应用 `{teamsAppInstallationId}` 的 。</span><span class="sxs-lookup"><span data-stu-id="44ba6-167">**1.** You must need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="44ba6-168">如果没有，请使用以下内容：</span><span class="sxs-lookup"><span data-stu-id="44ba6-168">If you don't have it, use the following:</span></span>

<span data-ttu-id="44ba6-169">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="44ba6-169">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="44ba6-170">响应 **的 id** 属性为 `teamsAppInstallationId` 。</span><span class="sxs-lookup"><span data-stu-id="44ba6-170">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="44ba6-171">**2.** 提出以下请求来获取 `chatId` ：</span><span class="sxs-lookup"><span data-stu-id="44ba6-171">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="44ba6-172">**HTTP GET** 请求 (权限 — `TeamsAppInstallation.ReadWriteSelfForUser.All`) ：</span><span class="sxs-lookup"><span data-stu-id="44ba6-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="44ba6-173">响应 **的 id** 属性为 `chatId` 。</span><span class="sxs-lookup"><span data-stu-id="44ba6-173">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="44ba6-174">还可以检索具有以下 `chatId` 请求的 ，但需要更广泛的 `Chat.Read.All` 权限：</span><span class="sxs-lookup"><span data-stu-id="44ba6-174">You can also retrieve the `chatId` with the following request but it requires the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="44ba6-175">**HTTP GET** 请求 (权限 — `Chat.Read.All`) ：</span><span class="sxs-lookup"><span data-stu-id="44ba6-175">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="44ba6-176">✔发送主动邮件</span><span class="sxs-lookup"><span data-stu-id="44ba6-176">✔ Send proactive messages</span></span>

<span data-ttu-id="44ba6-177">自动程序 [可以在为用户或](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) 团队添加自动程序并接收所有用户信息后发送主动消息。</span><span class="sxs-lookup"><span data-stu-id="44ba6-177">Your bot can [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) after the bot has been added for a user or a team and has received all the user information.</span></span>

## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="44ba6-178">Teams 管理员相关主题</span><span class="sxs-lookup"><span data-stu-id="44ba6-178">Related topic for Teams administrators</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="44ba6-179">**在 Teams 中管理应用设置策略**</span><span class="sxs-lookup"><span data-stu-id="44ba6-179">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a><span data-ttu-id="44ba6-180">查看其他代码示例</span><span class="sxs-lookup"><span data-stu-id="44ba6-180">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="44ba6-181">**Teams 主动邮件代码示例**</span><span class="sxs-lookup"><span data-stu-id="44ba6-181">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
