---
title: 获取选项卡的上下文
description: 介绍如何将用户上下文获取有关选项卡的用户上下文
localization_priority: Normal
ms.topic: how-to
keywords: Teams 选项卡用户上下文
ms.openlocfilehash: 0d9224a941ae4f6a5ad125c93d5877ec49b6df28
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566864"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a><span data-ttu-id="738e9-104">获取 Microsoft Teams 选项卡的上下文</span><span class="sxs-lookup"><span data-stu-id="738e9-104">Get context for your Microsoft Teams tab</span></span>

<span data-ttu-id="738e9-105">您的选项卡必须要求上下文信息以显示相关内容：</span><span class="sxs-lookup"><span data-stu-id="738e9-105">Your tab must require contextual information to display relevant content:</span></span>

* <span data-ttu-id="738e9-106">有关用户、团队或公司的基本信息。</span><span class="sxs-lookup"><span data-stu-id="738e9-106">Basic information about the user, team, or company.</span></span>
* <span data-ttu-id="738e9-107">区域设置和主题信息。</span><span class="sxs-lookup"><span data-stu-id="738e9-107">Locale and theme information.</span></span>
* <span data-ttu-id="738e9-108">读取 `entityId` 标识 `subEntityId` 此选项卡中的内容的 或。</span><span class="sxs-lookup"><span data-stu-id="738e9-108">Read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="738e9-109">用户上下文</span><span class="sxs-lookup"><span data-stu-id="738e9-109">User context</span></span>

<span data-ttu-id="738e9-110">在以下情况下，有关用户、团队或公司的上下文可能特别有用：</span><span class="sxs-lookup"><span data-stu-id="738e9-110">Context about the user, team or company can be especially useful when:</span></span>

* <span data-ttu-id="738e9-111">在应用中创建资源或将资源与指定的用户或团队关联。</span><span class="sxs-lookup"><span data-stu-id="738e9-111">You create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="738e9-112">您针对用户或其他Azure Active Directory启动身份验证流，并且不希望要求用户再次输入其用户名。</span><span class="sxs-lookup"><span data-stu-id="738e9-112">You initiate an authentication flow against Azure Active Directory or other identity provider, and you don't want to require the user to enter their username again.</span></span> <span data-ttu-id="738e9-113">有关在用户标签页中进行身份验证Microsoft Teams，请参阅"验证用户Microsoft Teams[选项卡。](~/concepts/authentication/authentication.md)</span><span class="sxs-lookup"><span data-stu-id="738e9-113">For more information on authenticating within your Microsoft Teams tab, see [Authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="738e9-114">虽然此用户信息可帮助提供流畅的用户体验，但 *不应* 使用它作为身份证明。</span><span class="sxs-lookup"><span data-stu-id="738e9-114">Although this user information can help provide a smooth user experience, you should *not* use it as proof of identity.</span></span> <span data-ttu-id="738e9-115">例如，攻击者可能会将你的页面加载在"错误的浏览器"中，并呈现有害信息或请求。</span><span class="sxs-lookup"><span data-stu-id="738e9-115">For example, an attacker could load your page in a "bad browser" and render harmful information or requests.</span></span>

## <a name="accessing-context"></a><span data-ttu-id="738e9-116">访问上下文</span><span class="sxs-lookup"><span data-stu-id="738e9-116">Accessing context</span></span>

<span data-ttu-id="738e9-117">可以通过两种方式访问上下文信息：</span><span class="sxs-lookup"><span data-stu-id="738e9-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="738e9-118">插入 URL 占位符值。</span><span class="sxs-lookup"><span data-stu-id="738e9-118">Insert URL placeholder values.</span></span>
* <span data-ttu-id="738e9-119">使用[Microsoft Teams JavaScript 客户端 SDK。](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="738e9-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client).</span></span>

### <a name="getting-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="738e9-120">通过插入 URL 占位符值获取上下文</span><span class="sxs-lookup"><span data-stu-id="738e9-120">Getting context by inserting URL placeholder values</span></span>

<span data-ttu-id="738e9-121">在配置或内容 URL 中使用占位符。</span><span class="sxs-lookup"><span data-stu-id="738e9-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="738e9-122">确定实际配置或内容 URL 时，Microsoft Teams 会使用相关值替换占位符。</span><span class="sxs-lookup"><span data-stu-id="738e9-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL.</span></span> <span data-ttu-id="738e9-123">可用的占位符包含上下文对象 [上](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 字段。</span><span class="sxs-lookup"><span data-stu-id="738e9-123">The available placeholders include all fields on the [Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) object.</span></span> <span data-ttu-id="738e9-124">常用占位符包括以下内容：</span><span class="sxs-lookup"><span data-stu-id="738e9-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="738e9-125">{entityId}：首次配置选项卡列表时， [此选项卡中提供的](~/tabs/how-to/create-tab-pages/configuration-page.md)。</span><span class="sxs-lookup"><span data-stu-id="738e9-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="738e9-126">{subEntityId}：此选项卡内为特定项目 [深链接](~/concepts/build-and-test/deep-links.md) 提供 _ID_。这应用于还原到实体中的特定状态;例如，滚动到特定部分的内容或激活特定部分的内容。</span><span class="sxs-lookup"><span data-stu-id="738e9-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item _within_ this tab. This should be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="738e9-127">{loginHint}：适用于 Azure AD 登录提示的值。这通常是当前用户的家庭租户中的登录名。</span><span class="sxs-lookup"><span data-stu-id="738e9-127">{loginHint}: A value suitable as a login hint for Azure AD.This is usually the login name of the current user, in their home tenant.</span></span>
* <span data-ttu-id="738e9-128">{userPrincipalName}：当前租户中当前用户的用户主体名称。</span><span class="sxs-lookup"><span data-stu-id="738e9-128">{userPrincipalName}: The User Principal Name of the current user, in the current tenant.</span></span>
* <span data-ttu-id="738e9-129">{userObjectId}：当前租户中的当前用户的 Azure AD 对象 ID。</span><span class="sxs-lookup"><span data-stu-id="738e9-129">{userObjectId}: The Azure AD object ID of the current user, in the current tenant.</span></span>
* <span data-ttu-id="738e9-130">{主题}：当前 UI 主题，如 `default`、 `dark`或 `contrast`。</span><span class="sxs-lookup"><span data-stu-id="738e9-130">{theme}: The current UI theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="738e9-131">{groupId}：选项卡所在的 Office 365 组的 ID。</span><span class="sxs-lookup"><span data-stu-id="738e9-131">{groupId}: The ID of the Office 365 Group in which the tab resides.</span></span>
* <span data-ttu-id="738e9-132">{tid}：当前用户的 Azure AD 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="738e9-132">{tid}: The Azure AD tenant ID of the current user.</span></span>
* <span data-ttu-id="738e9-133">{locale}：格式化为 languageId-countryId 的用户的当前区域设置。</span><span class="sxs-lookup"><span data-stu-id="738e9-133">{locale}: The current locale of the user formatted as languageId-countryId.</span></span> <span data-ttu-id="738e9-134">例如，en-us。</span><span class="sxs-lookup"><span data-stu-id="738e9-134">For example, en-us.</span></span>

>[!NOTE]
><span data-ttu-id="738e9-135">上一 `{upn}` 占位符现已弃用。</span><span class="sxs-lookup"><span data-stu-id="738e9-135">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="738e9-136">出于向后兼容性，它目前是 `{loginHint}`的同义词。</span><span class="sxs-lookup"><span data-stu-id="738e9-136">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="738e9-137">例如，假设在选项卡清单中将 属性设置为 `configURL` `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"` ，登录用户具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="738e9-137">For example, suppose in your tab manifest you set the `configURL` attribute to `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`, the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="738e9-138">其用户名为"user@example.com"。</span><span class="sxs-lookup"><span data-stu-id="738e9-138">Their username is 'user@example.com'.</span></span>
* <span data-ttu-id="738e9-139">其公司租户 ID 为"e2653c-etc"。</span><span class="sxs-lookup"><span data-stu-id="738e9-139">Their company tenant ID is 'e2653c-etc'.</span></span>
* <span data-ttu-id="738e9-140">他们是 id 为"00209384-etc"Office 365组的成员。</span><span class="sxs-lookup"><span data-stu-id="738e9-140">They are a member of the Office 365 group with id '00209384-etc'.</span></span>
* <span data-ttu-id="738e9-141">用户已设置其Teams主题为"深色"。</span><span class="sxs-lookup"><span data-stu-id="738e9-141">The user has set their Teams theme to 'dark'.</span></span>

<span data-ttu-id="738e9-142">当他们配置选项卡时，Teams调用以下 URL：</span><span class="sxs-lookup"><span data-stu-id="738e9-142">When they configure your tab, Teams calls the following URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="738e9-143">使用 Microsoft Teams JavaScript 库获取上下文</span><span class="sxs-lookup"><span data-stu-id="738e9-143">Getting context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="738e9-144">还可通过调用 `microsoftTeams.getContext(function(context) { /* ... */ })` 使用[ Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 检索前面列出的信息。</span><span class="sxs-lookup"><span data-stu-id="738e9-144">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="738e9-145">上下文变量如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="738e9-145">The context variable looks like the following example:</span></span>

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

## <a name="retrieving-context-in-private-channels"></a><span data-ttu-id="738e9-146">在专用频道中检索上下文</span><span class="sxs-lookup"><span data-stu-id="738e9-146">Retrieving context in private channels</span></span>

> [!Note]
> <span data-ttu-id="738e9-147">专用频道目前为私人开发人员预览版。</span><span class="sxs-lookup"><span data-stu-id="738e9-147">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="738e9-148">当你的内容页面加载在专用频道中时，从免费呼叫 `getContext` 接收的数据将被模糊显示，以保护频道的隐私。</span><span class="sxs-lookup"><span data-stu-id="738e9-148">When your content page is loaded in a private channel, the data you receive from the `getContext` call will be obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="738e9-149">当你的内容页面位于专用频道中时，会更改以下字段。</span><span class="sxs-lookup"><span data-stu-id="738e9-149">The following fields are changed when your content page is in a private channel.</span></span> <span data-ttu-id="738e9-150">如果页面使用任意以下值，需检查 `channelType` 字段以确定页面是否加载在专用频道中，并作出相应响应。</span><span class="sxs-lookup"><span data-stu-id="738e9-150">If your page makes use of any of the values below, you'll need to check the `channelType` field to determine if your page is loaded in a private channel, and respond appropriately.</span></span>

* <span data-ttu-id="738e9-151">`groupId`：未为私人频道定义</span><span class="sxs-lookup"><span data-stu-id="738e9-151">`groupId`: Undefined for private channels</span></span>
* <span data-ttu-id="738e9-152">`teamId`：设置为私人频道的 threadId</span><span class="sxs-lookup"><span data-stu-id="738e9-152">`teamId`: Set to the threadId of the private channel</span></span>
* <span data-ttu-id="738e9-153">`teamName`：设置为私人频道的名称</span><span class="sxs-lookup"><span data-stu-id="738e9-153">`teamName`: Set to the name of the private channel</span></span>
* <span data-ttu-id="738e9-154">`teamSiteUrl`：设置为专用频道的独特SharePoint网站的 URL</span><span class="sxs-lookup"><span data-stu-id="738e9-154">`teamSiteUrl`: Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="738e9-155">`teamSitePath`：设置为专用频道的独特SharePoint网站的路径</span><span class="sxs-lookup"><span data-stu-id="738e9-155">`teamSitePath`: Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="738e9-156">`teamSiteDomain`：设置为专用频道的唯一SharePoint网站域的域</span><span class="sxs-lookup"><span data-stu-id="738e9-156">`teamSiteDomain`: Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

> [!Note]
>  <span data-ttu-id="738e9-157">teamSiteUrl 也适用于标准频道。</span><span class="sxs-lookup"><span data-stu-id="738e9-157">teamSiteUrl works well for standard channels also.</span></span>

## <a name="theme-change-handling"></a><span data-ttu-id="738e9-158">主题更改处理</span><span class="sxs-lookup"><span data-stu-id="738e9-158">Theme change handling</span></span>

<span data-ttu-id="738e9-159">可致电组织，注册应用，告知主题是否 `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`。</span><span class="sxs-lookup"><span data-stu-id="738e9-159">You can register your app to be told if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="738e9-160">函数 `theme` 参数将为一个字符串，其值为 `default`、 `dark`或 `contrast`。</span><span class="sxs-lookup"><span data-stu-id="738e9-160">The `theme` argument in the function will be a string with a value of `default`, `dark`, or `contrast`.</span></span>
