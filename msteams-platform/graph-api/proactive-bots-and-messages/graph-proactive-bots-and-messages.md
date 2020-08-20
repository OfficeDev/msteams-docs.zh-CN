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
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a><span data-ttu-id="6a71f-104">使用 Microsoft Graph 公共预览版启用 Teams 中的主动机器人安装 (主动) </span><span class="sxs-lookup"><span data-stu-id="6a71f-104">Enable proactive bot installation and proactive messaging in Teams with Microsoft Graph (Public Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="6a71f-105">Microsoft Graph 和 Microsoft Teams 公共预览版可提供快速访问权限和反馈。</span><span class="sxs-lookup"><span data-stu-id="6a71f-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="6a71f-106">虽然此版本已经进行了大的测试，但它不适合用于生产。</span><span class="sxs-lookup"><span data-stu-id="6a71f-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="6a71f-107">Teams 中的主动消息传递</span><span class="sxs-lookup"><span data-stu-id="6a71f-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="6a71f-108">主动邮件由机器人启动，以与用户开始对话。</span><span class="sxs-lookup"><span data-stu-id="6a71f-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="6a71f-109">它们用于许多目的，包括发送欢迎邮件、进行调查或投票，以及广播组织范围内的通知。</span><span class="sxs-lookup"><span data-stu-id="6a71f-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span>  <span data-ttu-id="6a71f-110">Teams 中的主动消息可以作为临**时对话或基于对话框\*\*\*\*的对话**传递：</span><span class="sxs-lookup"><span data-stu-id="6a71f-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="6a71f-111">消息类型</span><span class="sxs-lookup"><span data-stu-id="6a71f-111">Message Type</span></span> | <span data-ttu-id="6a71f-112">说明</span><span class="sxs-lookup"><span data-stu-id="6a71f-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="6a71f-113">临时主动邮件</span><span class="sxs-lookup"><span data-stu-id="6a71f-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="6a71f-114">机器人将截获一条消息，而不会中断对话流。</span><span class="sxs-lookup"><span data-stu-id="6a71f-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="6a71f-115">基于对话框的主动邮件</span><span class="sxs-lookup"><span data-stu-id="6a71f-115">Dialog-based proactive message</span></span> | <span data-ttu-id="6a71f-116">机器人会创建新的对话框线程，控制对话，传递主动消息，关闭，然后将控件返回到上一个对话。</span><span class="sxs-lookup"><span data-stu-id="6a71f-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

<span data-ttu-id="6a71f-117">*请参阅*、 [向用户 SDK v4 发送主动通知](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)</span><span class="sxs-lookup"><span data-stu-id="6a71f-117">*See*, [Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)</span></span>

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="6a71f-118">Teams 中的主动应用安装</span><span class="sxs-lookup"><span data-stu-id="6a71f-118">Proactive app installation in Teams</span></span>

<span data-ttu-id="6a71f-119">在自动程序可主动向用户传出消息之前，需要将其作为个人应用或用户所在团队进行安装。</span><span class="sxs-lookup"><span data-stu-id="6a71f-119">Before your bot can proactively message a user, it needs to be installed either as a personal app, or in a team where the user is a member.</span></span> <span data-ttu-id="6a71f-120">有时，你可能需要主动向尚未 _安装或之前_ 未与应用进行交互的消息用户。</span><span class="sxs-lookup"><span data-stu-id="6a71f-120">At times,  you may need to proactively message users that have _not_ installed or previously interacted with your app.</span></span> <span data-ttu-id="6a71f-121">例如，需要向组织中的所有人显示至其他所有人的信息。</span><span class="sxs-lookup"><span data-stu-id="6a71f-121">For instance, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="6a71f-122">对于此类应用场景，可使用 Microsoft Graph API 主动为用户安装自动程序。</span><span class="sxs-lookup"><span data-stu-id="6a71f-122">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="6a71f-123">权限</span><span class="sxs-lookup"><span data-stu-id="6a71f-123">Permissions</span></span>

<span data-ttu-id="6a71f-124">使用 Microsoft Graph [teamsAppInstallation 资源类型](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) 权限，可管理 Microsoft Teams 平台内 (个人) 或团队 (频道) 的应用安装生命周期：</span><span class="sxs-lookup"><span data-stu-id="6a71f-124">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) permissions allow you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="6a71f-125">应用权限</span><span class="sxs-lookup"><span data-stu-id="6a71f-125">Application permission</span></span> | <span data-ttu-id="6a71f-126">说明</span><span class="sxs-lookup"><span data-stu-id="6a71f-126">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="6a71f-127">允许 Teams 应用针对任何用户自己读取、安装 **、升级和**卸载其自身，而无需在登录或使用之前。</span><span class="sxs-lookup"><span data-stu-id="6a71f-127">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="6a71f-128">允许 Teams 应用在任何团队中自行读取、安装、升级和 **卸载其自**身，而无需先登录或使用。</span><span class="sxs-lookup"><span data-stu-id="6a71f-128">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="6a71f-129">若要使用这些权限，必须使用以下 [值将 webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到应用部件清单：</span><span class="sxs-lookup"><span data-stu-id="6a71f-129">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="6a71f-130">**id**  — 你的 Azure AD 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="6a71f-130">**id**  — your Azure AD app id.</span></span>
> * <span data-ttu-id="6a71f-131">**资源** — 应用程序的资源 URL。</span><span class="sxs-lookup"><span data-stu-id="6a71f-131">**resource** — the resource URL for the app.</span></span>
>

>[!NOTE]
>
> * <span data-ttu-id="6a71f-132">自动程序不需要_具有非__用户委派权限_的应用程序，因为安装对用户来来并不是用户。</span><span class="sxs-lookup"><span data-stu-id="6a71f-132">Your bot requires _application_ not _user delegated_ permissions because the installation is not for yourself but for others.</span></span>
>
> * <span data-ttu-id="6a71f-133">Azure AD 租户管理员必须 [对应用程序显式授予权限](/graph/security-authorization#grant-permissions-to-an-application)。</span><span class="sxs-lookup"><span data-stu-id="6a71f-133">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="6a71f-134">授权应用程序后 _，Azure_ AD 租户的所有成员都将获取已授予的权限。</span><span class="sxs-lookup"><span data-stu-id="6a71f-134">After an application is granted permissions, _all_ members of the Azure AD tenant will gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="6a71f-135">启用主动应用安装和消息</span><span class="sxs-lookup"><span data-stu-id="6a71f-135">Enable proactive app installation and messaging</span></span>

 > [!IMPORTANT]
><span data-ttu-id="6a71f-136">Microsoft Graph 仅将安装在组织的应用程序目录或 [AppSource](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) [中发布的应用](https://appsource.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="6a71f-136">Microsoft Graph will only install apps published within your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="6a71f-137">✔为 Teams 创建和发布主动邮件传递自动程序</span><span class="sxs-lookup"><span data-stu-id="6a71f-137">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="6a71f-138">若要开始使用，需要具有主动[邮件](../../bots/how-to/create-a-bot-for-teams.md)功能的 Teams[proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md)自动程序，并[发布](../../concepts/deploy-and-publish/overview.md)在组织的应用目录[或](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) [AppSource 中](https://appsource.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="6a71f-138">To get started, you will need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities and  [published](../../concepts/deploy-and-publish/overview.md) in your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

>[!TIP]
> <span data-ttu-id="6a71f-139">生产就绪 [**型公司Communicator**](../..//samples/app-templates.md#company-communicator) 公司模板支持广播消息，并且是构建主动机器人应用程序的很好基础。</span><span class="sxs-lookup"><span data-stu-id="6a71f-139">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template enables broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="6a71f-140">✔为 `teamsAppId` 你的应用获取</span><span class="sxs-lookup"><span data-stu-id="6a71f-140">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="6a71f-141">**1.** 后续步骤 `teamsAppId`  中将需要您。</span><span class="sxs-lookup"><span data-stu-id="6a71f-141">**1.** You will need the `teamsAppId`  for the next steps.</span></span>

<span data-ttu-id="6a71f-142">可以 `teamsAppId` 从组织的应用程序目录检索到：</span><span class="sxs-lookup"><span data-stu-id="6a71f-142">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="6a71f-143">**Microsoft Graph 页参考**[：teamsApp 资源类型](/graph/api/resources/teamsapp?view=graph-rest-1.0)</span><span class="sxs-lookup"><span data-stu-id="6a71f-143">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0)</span></span>

<span data-ttu-id="6a71f-144">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="6a71f-144">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="6a71f-145">请求将返回 `teamsApp`  对象。</span><span class="sxs-lookup"><span data-stu-id="6a71f-145">The request will return a `teamsApp`  object.</span></span> <span data-ttu-id="6a71f-146">返回的对象是 `id`  应用的目录生成的应用 ID，与在 Teams 应用清单中提供的"id："不同：</span><span class="sxs-lookup"><span data-stu-id="6a71f-146">The returned object's `id`  is the app's catalog generated app id and is different from the "id:" that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="6a71f-147">**2.**  如果已为个人范围内的用户上传/旁加载应用，你可以如下所示 `teamsAppId` 进行检索：</span><span class="sxs-lookup"><span data-stu-id="6a71f-147">**2.**  If your app has already been uploaded/sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="6a71f-148">**Microsoft Graph 页参考：**[列出为用户安装的应用](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="6a71f-148">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="6a71f-149">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="6a71f-149">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="6a71f-150">**3.** 如果已为团队范围内的频道上传/旁加载应用，可以按如下所示 `teamsAppId` 检索：</span><span class="sxs-lookup"><span data-stu-id="6a71f-150">**3.** If your app has already been uploaded/sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="6a71f-151">**Microsoft Graph 页参考：**[列出团队中的应用](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="6a71f-151">**Microsoft Graph page reference:** [List apps in team](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="6a71f-152">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="6a71f-152">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="6a71f-153">可以筛选 [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0) 对象的任何字段来缩小结果列表。</span><span class="sxs-lookup"><span data-stu-id="6a71f-153">You can filter on any of the fields of the [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0) object to narrow the list of results.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="6a71f-154">✔确定当前是否为邮件收件人安装了机器人</span><span class="sxs-lookup"><span data-stu-id="6a71f-154">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="6a71f-155">**Microsoft Graph 页参考：**[列出为用户安装的应用](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="6a71f-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="6a71f-156">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="6a71f-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="6a71f-157">如果未安装应用，则此请求将返回空数组，或者返回包含单个 [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) 对象的数组（如果已安装）。</span><span class="sxs-lookup"><span data-stu-id="6a71f-157">This request will return an empty array if the app is not installed, or an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) object if it has been installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="6a71f-158">✔安装应用</span><span class="sxs-lookup"><span data-stu-id="6a71f-158">✔ Install your app</span></span>

<span data-ttu-id="6a71f-159">**Microsoft Graph 参考：**[为用户安装应用](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="6a71f-159">**Microsoft Graph reference:** [Install app for user](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="6a71f-160">**HTTP POST** 请求：</span><span class="sxs-lookup"><span data-stu-id="6a71f-160">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="6a71f-161">如果用户运行 Microsoft Teams，可能会立即看到应用安装。</span><span class="sxs-lookup"><span data-stu-id="6a71f-161">If the user has Microsoft Teams running, they may see the app install immediately.</span></span> <span data-ttu-id="6a71f-162">或者，可能需要重新启动才能查看已安装的应用。</span><span class="sxs-lookup"><span data-stu-id="6a71f-162">Alternatively,  a  restart may be necessary to see the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="6a71f-163">✔检索对话 **chatId**</span><span class="sxs-lookup"><span data-stu-id="6a71f-163">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="6a71f-164">为用户安装应用后，机器人将收到 `conversationUpdate` [事件通知](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) ，其中包含发送主动消息所需的信息。</span><span class="sxs-lookup"><span data-stu-id="6a71f-164">When your app is installed for the user, the bot will receive a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that will contain the necessary information to send the proactive message.</span></span>

<span data-ttu-id="6a71f-165">`chatId`也可以按如下方式检索：</span><span class="sxs-lookup"><span data-stu-id="6a71f-165">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="6a71f-166">**Microsoft Graph 参考：**[获取聊天](/graph/api/chat-get?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="6a71f-166">**Microsoft Graph reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="6a71f-167">**1.** 您将需要您的应用程序 `{teamsAppInstallationId}` 。</span><span class="sxs-lookup"><span data-stu-id="6a71f-167">**1.** You will need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="6a71f-168">如果没有，请使用以下名称：</span><span class="sxs-lookup"><span data-stu-id="6a71f-168">If you don't have it, use the following:</span></span>

<span data-ttu-id="6a71f-169">**HTTP GET** 请求：</span><span class="sxs-lookup"><span data-stu-id="6a71f-169">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="6a71f-170">响应的 **id** 属性为 `teamsAppInstallationId` .</span><span class="sxs-lookup"><span data-stu-id="6a71f-170">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="6a71f-171">**2.** 发出以下请求可提取 `chatId` ：</span><span class="sxs-lookup"><span data-stu-id="6a71f-171">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="6a71f-172">**HTTP GET** 请求 (权限 — `TeamsAppInstallation.ReadWriteSelfForUser.All`) ：</span><span class="sxs-lookup"><span data-stu-id="6a71f-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="6a71f-173">响应的 **id** 属性为 `chatId` .</span><span class="sxs-lookup"><span data-stu-id="6a71f-173">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="6a71f-174">或者，你也可以根据 `chatId`  下面请求检索请求，但需要更广泛 `Chat.Read.All` 的权限：</span><span class="sxs-lookup"><span data-stu-id="6a71f-174">Alternately, you can retrieve the `chatId`  with the request below, but it will require the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="6a71f-175">**HTTP GET** 请求 (权限 — `Chat.Read.All`) ：</span><span class="sxs-lookup"><span data-stu-id="6a71f-175">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="6a71f-176">✔动发送主动邮件</span><span class="sxs-lookup"><span data-stu-id="6a71f-176">✔ Send proactive messages</span></span>

<span data-ttu-id="6a71f-177">为用户或团队添加了机器人并获取必要的用户信息后，可以开始 [发送主动邮件](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)。</span><span class="sxs-lookup"><span data-stu-id="6a71f-177">Once your bot has been added for a user or team and has acquired the necessary user  information, it can begin to [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp).</span></span>

# <a name="c--net"></a>[<span data-ttu-id="6a71f-178">C# / .NET</span><span class="sxs-lookup"><span data-stu-id="6a71f-178">C# / .NET</span></span>](#tab/csharp)

<span data-ttu-id="6a71f-179">以下代码段来自 [于 C# 的 Microsoft Bot Framework 示例。](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span><span class="sxs-lookup"><span data-stu-id="6a71f-179">The following code snippet is from the [Microsoft Bot Framework Samples for C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="6a71f-180">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6a71f-180">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="6a71f-181">以下代码段来自 [Microsoft Bot Framework JavaScript 示例](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages)。</span><span class="sxs-lookup"><span data-stu-id="6a71f-181">The following code snippet is from the [Microsoft Bot Framework Samples for JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).</span></span>

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

## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="6a71f-182">有关 Teams 管理员的相关主题</span><span class="sxs-lookup"><span data-stu-id="6a71f-182">Related topic for Teams administrators</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6a71f-183">**在 Microsoft Teams 中管理应用设置策略**</span><span class="sxs-lookup"><span data-stu-id="6a71f-183">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a><span data-ttu-id="6a71f-184">查看其他代码示例</span><span class="sxs-lookup"><span data-stu-id="6a71f-184">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6a71f-185">**Teams 主动消息传递代码示例**</span><span class="sxs-lookup"><span data-stu-id="6a71f-185">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
