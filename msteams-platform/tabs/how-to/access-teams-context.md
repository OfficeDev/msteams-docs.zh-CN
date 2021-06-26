---
title: 获取选项卡的上下文
description: 介绍如何将用户上下文获取有关选项卡的用户上下文
localization_priority: Normal
ms.topic: how-to
keywords: Teams 选项卡用户上下文
ms.openlocfilehash: 29f574ae924ddde52b63590aba3fcc06a3d446af
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140276"
---
# <a name="get-context-for-your-tab"></a><span data-ttu-id="a41ef-104">获取选项卡的上下文</span><span class="sxs-lookup"><span data-stu-id="a41ef-104">Get context for your tab</span></span>

<span data-ttu-id="a41ef-105">您的选项卡需要上下文信息来显示相关内容：</span><span class="sxs-lookup"><span data-stu-id="a41ef-105">Your tab requires contextual information to display relevant content:</span></span>

* <span data-ttu-id="a41ef-106">有关用户、团队或公司的基本信息。</span><span class="sxs-lookup"><span data-stu-id="a41ef-106">Basic information about the user, team, or company.</span></span>
* <span data-ttu-id="a41ef-107">区域设置和主题信息。</span><span class="sxs-lookup"><span data-stu-id="a41ef-107">Locale and theme information.</span></span>
* <span data-ttu-id="a41ef-108">读取 `entityId` 标识 `subEntityId` 此选项卡中的内容的 或。</span><span class="sxs-lookup"><span data-stu-id="a41ef-108">Read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="a41ef-109">用户上下文</span><span class="sxs-lookup"><span data-stu-id="a41ef-109">User context</span></span>

<span data-ttu-id="a41ef-110">在以下情况下，有关用户、团队或公司的上下文可能特别有用：</span><span class="sxs-lookup"><span data-stu-id="a41ef-110">Context about the user, team, or company can be especially useful when:</span></span>

* <span data-ttu-id="a41ef-111">在应用中创建资源或将资源与指定的用户或团队关联。</span><span class="sxs-lookup"><span data-stu-id="a41ef-111">You create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="a41ef-112">从 AAD Azure Active Directory (或其他) 启动身份验证流，并且不需要用户再次输入其用户名。</span><span class="sxs-lookup"><span data-stu-id="a41ef-112">You initiate an authentication flow from Azure Active Directory (AAD) or other identity provider, and you do not require the user to enter their username again.</span></span> <span data-ttu-id="a41ef-113">有关详细信息，请参阅"验证[用户身份Microsoft Teams选项卡。](~/concepts/authentication/authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a41ef-113">For more information, see [authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a41ef-114">虽然此用户信息可帮助提供流畅的用户体验，但不得使用它作为标识证明。</span><span class="sxs-lookup"><span data-stu-id="a41ef-114">Although this user information can help provide a smooth user experience, you must not use it as proof of identity.</span></span> <span data-ttu-id="a41ef-115">例如，攻击者可以在浏览器中加载页面并呈现有害的信息或请求。</span><span class="sxs-lookup"><span data-stu-id="a41ef-115">For example, an attacker can load your page in a browser and render harmful information or requests.</span></span>

## <a name="access-context-information"></a><span data-ttu-id="a41ef-116">访问上下文信息</span><span class="sxs-lookup"><span data-stu-id="a41ef-116">Access context information</span></span>

<span data-ttu-id="a41ef-117">可以通过两种方式访问上下文信息：</span><span class="sxs-lookup"><span data-stu-id="a41ef-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="a41ef-118">插入 URL 占位符值。</span><span class="sxs-lookup"><span data-stu-id="a41ef-118">Insert URL placeholder values.</span></span>
* <span data-ttu-id="a41ef-119">使用[Microsoft Teams JavaScript 客户端 SDK。](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="a41ef-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client).</span></span>

### <a name="get-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="a41ef-120">通过插入 URL 占位符值获取上下文</span><span class="sxs-lookup"><span data-stu-id="a41ef-120">Get context by inserting URL placeholder values</span></span>

<span data-ttu-id="a41ef-121">在配置或内容 URL 中使用占位符。</span><span class="sxs-lookup"><span data-stu-id="a41ef-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="a41ef-122">确定实际配置或内容 URL 时，Microsoft Teams 会使用相关值替换占位符。</span><span class="sxs-lookup"><span data-stu-id="a41ef-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL.</span></span> <span data-ttu-id="a41ef-123">可用占位符包括上下文对象上 [的所有](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 字段。</span><span class="sxs-lookup"><span data-stu-id="a41ef-123">The available placeholders include all fields on the [context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) object.</span></span> <span data-ttu-id="a41ef-124">常用占位符包括以下内容：</span><span class="sxs-lookup"><span data-stu-id="a41ef-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="a41ef-125">{entityId}：首次配置选项卡列表时， [此选项卡中提供的](~/tabs/how-to/create-tab-pages/configuration-page.md)。</span><span class="sxs-lookup"><span data-stu-id="a41ef-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="a41ef-126">{subEntityId}：为此选项卡内的特定项生成深层链接时[](~/concepts/build-and-test/deep-links.md)提供的 ID。这必须用于还原到实体中的特定状态;例如，滚动到或激活特定内容部分。</span><span class="sxs-lookup"><span data-stu-id="a41ef-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item within this tab. This must be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="a41ef-127">{loginHint}：适合用作 AAD 登录提示的值。</span><span class="sxs-lookup"><span data-stu-id="a41ef-127">{loginHint}: A value suitable as a login hint for AAD.</span></span> <span data-ttu-id="a41ef-128">这通常是其主租户中当前用户的登录名。</span><span class="sxs-lookup"><span data-stu-id="a41ef-128">This is usually the login name of the current user in their home tenant.</span></span>
* <span data-ttu-id="a41ef-129">{userPrincipalName}：当前租户中当前用户的用户主体名称。</span><span class="sxs-lookup"><span data-stu-id="a41ef-129">{userPrincipalName}: The User Principal Name of the current user in the current tenant.</span></span>
* <span data-ttu-id="a41ef-130">{userObjectId}：当前租户中当前用户的 AAD 对象 ID。</span><span class="sxs-lookup"><span data-stu-id="a41ef-130">{userObjectId}: The AAD object ID of the current user in the current tenant.</span></span>
* <span data-ttu-id="a41ef-131">{theme}：当前用户界面 (UI) 主题，如 、 `default` `dark` 或 `contrast` 。</span><span class="sxs-lookup"><span data-stu-id="a41ef-131">{theme}: The current user interface (UI) theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="a41ef-132">{groupId}：选项卡Office 365组 ID。</span><span class="sxs-lookup"><span data-stu-id="a41ef-132">{groupId}: The ID of the Office 365 group in which the tab resides.</span></span>
* <span data-ttu-id="a41ef-133">{tid}：当前用户的 AAD 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="a41ef-133">{tid}: The AAD tenant ID of the current user.</span></span>
* <span data-ttu-id="a41ef-134">{locale}：格式化为 languageId-countryId 的用户的当前区域设置。</span><span class="sxs-lookup"><span data-stu-id="a41ef-134">{locale}: The current locale of the user formatted as languageId-countryId.</span></span> <span data-ttu-id="a41ef-135">例如，en-us。</span><span class="sxs-lookup"><span data-stu-id="a41ef-135">For example, en-us.</span></span>

> [!NOTE]
> <span data-ttu-id="a41ef-136">上一 `{upn}` 占位符现已弃用。</span><span class="sxs-lookup"><span data-stu-id="a41ef-136">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="a41ef-137">出于向后兼容性，它目前是 `{loginHint}`的同义词。</span><span class="sxs-lookup"><span data-stu-id="a41ef-137">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="a41ef-138">例如，在选项卡清单中，将 `configURL` 属性设置为 `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"` ，登录用户具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="a41ef-138">For example, in your tab manifest you set the `configURL` attribute to `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`, the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="a41ef-139">其用户名为 **user@example.com**。</span><span class="sxs-lookup"><span data-stu-id="a41ef-139">Their username is **user@example.com**.</span></span>
* <span data-ttu-id="a41ef-140">他们的公司租户 ID 是 **e2653c-etc。**</span><span class="sxs-lookup"><span data-stu-id="a41ef-140">Their company tenant ID is **e2653c-etc**.</span></span>
* <span data-ttu-id="a41ef-141">他们是 id 为 **00209384 Office 365组的成员。**</span><span class="sxs-lookup"><span data-stu-id="a41ef-141">They are a member of the Office 365 group with id **00209384-etc**.</span></span>
* <span data-ttu-id="a41ef-142">用户已设置其Teams主题为 **深色**。</span><span class="sxs-lookup"><span data-stu-id="a41ef-142">The user has set their Teams theme to **dark**.</span></span>

<span data-ttu-id="a41ef-143">在配置选项卡时，Teams调用以下 URL：</span><span class="sxs-lookup"><span data-stu-id="a41ef-143">When they configure the tab, Teams calls the following URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="a41ef-144">使用 JavaScript Microsoft Teams获取上下文</span><span class="sxs-lookup"><span data-stu-id="a41ef-144">Get context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="a41ef-145">还可通过调用 `microsoftTeams.getContext(function(context) { /* ... */ })` 使用[ Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 检索前面列出的信息。</span><span class="sxs-lookup"><span data-stu-id="a41ef-145">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="a41ef-146">以下代码提供了上下文变量的示例：</span><span class="sxs-lookup"><span data-stu-id="a41ef-146">The following code provides an example of context variable:</span></span>

```json
{
    "teamId": "The Microsoft Teams ID in the format 19:[id]@thread.skype",
    "teamName": "The name of the current team",
    "channelId": "The channel ID in the format 19:[id]@thread.skype",
    "channelName": "The name of the current channel",
    "chatId": "The chat ID in the format 19:[id]@thread.skype",
    "locale": "The current locale of the user formatted as languageId-countryId (for example, en-us)",
    "entityId": "The developer-defined unique ID for the entity this content points to",
    "subEntityId": "The developer-defined unique ID for the sub-entity this content points to",
    "loginHint": "A value suitable as a login hint for Azure AD. This is usually the login name of the current user, in their home tenant",
    "userPrincipalName": "The principal name of the current user, in the current tenant",
    "userObjectId": "The Azure AD object id of the current user, in the current tenant",
    "tid": "The Azure AD tenant ID of the current user",
    "groupId": "Guid identifying the current O365 Group ID",
    "theme": "The current UI theme: default | dark | contrast",
    "isFullScreen": "Indicates if the tab is in full-screen",
    "teamType": "The type of team",
    "teamSiteUrl": "The root SharePoint site associated with the team",
    "teamSiteDomain": "The domain of the root SharePoint site associated with the team",
    "teamSitePath": "The relative path to the SharePoint site associated with the team",
    "channelRelativeUrl": "The relative path to the SharePoint folder associated with the channel",
    "sessionId": "The unique ID for the current Teams session for use in correlating telemetry data",
    "userTeamRole": "The user's role in the team",
    "isTeamArchived": "Indicates if team is archived",
    "hostClientType": "The type of host client. Possible values are android, ios, web, desktop, rigel",
    "frameContext": "The context where tab URL is loaded (for example, content, task, setting, remove, sidePanel)",
    "sharepoint": "The SharePoint context is available only when hosted in SharePoint",
    "tenantSKU": "The license type for the current user tenant. Possible values are enterprise, free, edu, unknown",
    "userLicenseType": "The license type for the current user",
    "parentMessageId": "The parent message ID from which this task module is launched",
    "ringId": "The current ring ID",
    "appSessionId": "The unique ID for the current session used for correlating telemetry data",
    "isCallingAllowed": "Indicates if calling is allowed for the current logged in user",
    "isPSTNCallingAllowed": "Indicates if PSTN calling is allowed for the current logged in user",
    "meetingId": "The meeting ID used by tab when running in meeting context",
    "defaultOneNoteSectionId": "The OneNote section ID that is linked to the channel"
}
```

## <a name="retrieve-context-in-private-channels"></a><span data-ttu-id="a41ef-147">检索私人频道中的上下文</span><span class="sxs-lookup"><span data-stu-id="a41ef-147">Retrieve context in private channels</span></span>

> [!Note]
> <span data-ttu-id="a41ef-148">专用频道目前为私人开发人员预览版。</span><span class="sxs-lookup"><span data-stu-id="a41ef-148">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="a41ef-149">当你的内容页面加载到私人频道中时，你通过调用收到的数据会混淆以保护 `getContext` 通道的隐私。</span><span class="sxs-lookup"><span data-stu-id="a41ef-149">When your content page is loaded in a private channel, the data you receive from the `getContext` call is obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="a41ef-150">当内容页位于私人频道中时，将更改以下字段：</span><span class="sxs-lookup"><span data-stu-id="a41ef-150">The following fields are changed when your content page is in a private channel:</span></span>

* <span data-ttu-id="a41ef-151">`groupId`：未为私人频道定义</span><span class="sxs-lookup"><span data-stu-id="a41ef-151">`groupId`: Undefined for private channels</span></span>
* <span data-ttu-id="a41ef-152">`teamId`：设置为私人频道的 threadId</span><span class="sxs-lookup"><span data-stu-id="a41ef-152">`teamId`: Set to the threadId of the private channel</span></span>
* <span data-ttu-id="a41ef-153">`teamName`：设置为私人频道的名称</span><span class="sxs-lookup"><span data-stu-id="a41ef-153">`teamName`: Set to the name of the private channel</span></span>
* <span data-ttu-id="a41ef-154">`teamSiteUrl`：设置为专用频道的独特SharePoint网站的 URL</span><span class="sxs-lookup"><span data-stu-id="a41ef-154">`teamSiteUrl`: Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="a41ef-155">`teamSitePath`：设置为专用频道的独特SharePoint网站的路径</span><span class="sxs-lookup"><span data-stu-id="a41ef-155">`teamSitePath`: Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="a41ef-156">`teamSiteDomain`：设置为专用频道的唯一SharePoint网站域的域</span><span class="sxs-lookup"><span data-stu-id="a41ef-156">`teamSiteDomain`: Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

<span data-ttu-id="a41ef-157">如果页面使用了这些值中的任意值，则必须检查字段以确定页面是否加载到私人频道中并 `channelType` 做出相应的响应。</span><span class="sxs-lookup"><span data-stu-id="a41ef-157">If your page makes use of any of these values, you must check the `channelType` field to determine if your page is loaded in a private channel and respond appropriately.</span></span>

> [!Note]
> <span data-ttu-id="a41ef-158">`teamSiteUrl` 还适用于标准频道。</span><span class="sxs-lookup"><span data-stu-id="a41ef-158">`teamSiteUrl` also works well for standard channels.</span></span>

## <a name="handle-theme-change"></a><span data-ttu-id="a41ef-159">处理主题更改</span><span class="sxs-lookup"><span data-stu-id="a41ef-159">Handle theme change</span></span>

<span data-ttu-id="a41ef-160">你可以注册应用，以在主题发生更改时通过调用 通知 `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` 。</span><span class="sxs-lookup"><span data-stu-id="a41ef-160">You can register your app to be informed if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="a41ef-161">函数 `theme` 中的参数是值为 、 `default` 或 的 `dark` 字符串 `contrast` 。</span><span class="sxs-lookup"><span data-stu-id="a41ef-161">The `theme` argument in the function is a string with a value of `default`, `dark`, or `contrast`.</span></span>

## <a name="see-also"></a><span data-ttu-id="a41ef-162">另请参阅</span><span class="sxs-lookup"><span data-stu-id="a41ef-162">See also</span></span>

* [<span data-ttu-id="a41ef-163">选项卡设计指南</span><span class="sxs-lookup"><span data-stu-id="a41ef-163">Tab design guidelines</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="a41ef-164">Teams选项卡</span><span class="sxs-lookup"><span data-stu-id="a41ef-164">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="a41ef-165">先决条件</span><span class="sxs-lookup"><span data-stu-id="a41ef-165">Prerequisites</span></span>](~/tabs/how-to/tab-requirements.md)
* [<span data-ttu-id="a41ef-166">创建个人选项卡</span><span class="sxs-lookup"><span data-stu-id="a41ef-166">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="a41ef-167">创建频道或组选项卡</span><span class="sxs-lookup"><span data-stu-id="a41ef-167">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="a41ef-168">创建内容页</span><span class="sxs-lookup"><span data-stu-id="a41ef-168">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="a41ef-169">创建配置页</span><span class="sxs-lookup"><span data-stu-id="a41ef-169">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [<span data-ttu-id="a41ef-170">为选项卡创建删除页</span><span class="sxs-lookup"><span data-stu-id="a41ef-170">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
* [<span data-ttu-id="a41ef-171">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="a41ef-171">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="a41ef-172">选项卡链接展开和阶段视图</span><span class="sxs-lookup"><span data-stu-id="a41ef-172">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)
* [<span data-ttu-id="a41ef-173">创建对话选项卡</span><span class="sxs-lookup"><span data-stu-id="a41ef-173">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)
* [<span data-ttu-id="a41ef-174">选项卡边距更改</span><span class="sxs-lookup"><span data-stu-id="a41ef-174">Tab margin changes</span></span>](~/resources/removing-tab-margins.md)

## <a name="next-step"></a><span data-ttu-id="a41ef-175">后续步骤</span><span class="sxs-lookup"><span data-stu-id="a41ef-175">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a41ef-176">具有自适应卡片的生成选项卡</span><span class="sxs-lookup"><span data-stu-id="a41ef-176">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)