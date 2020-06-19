---
title: 获取您的选项卡的上下文
description: 介绍如何获取选项卡的用户上下文
keywords: 团队选项卡用户上下文
ms.openlocfilehash: 01919999e38d6b659f014b0f05b76d3f332db9ab
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801012"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a><span data-ttu-id="7df18-104">获取 Microsoft 团队选项卡的上下文</span><span class="sxs-lookup"><span data-stu-id="7df18-104">Get context for your Microsoft Teams tab</span></span>

<span data-ttu-id="7df18-105">您的选项卡可能需要上下文信息才能显示相关内容。</span><span class="sxs-lookup"><span data-stu-id="7df18-105">Your tab might require contextual information to display relevant content.</span></span>

* <span data-ttu-id="7df18-106">您的选项卡可能需要有关用户、团队或公司的基本信息。</span><span class="sxs-lookup"><span data-stu-id="7df18-106">Your tab might need basic information about the user, team, or company.</span></span>
* <span data-ttu-id="7df18-107">您的选项卡可能需要区域设置和主题信息。</span><span class="sxs-lookup"><span data-stu-id="7df18-107">Your tab might need locale and theme information.</span></span>
* <span data-ttu-id="7df18-108">您的选项卡可能需要读取 `entityId` 或 `subEntityId` 标识此选项卡中的内容。</span><span class="sxs-lookup"><span data-stu-id="7df18-108">Your tab might need to read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="7df18-109">用户上下文</span><span class="sxs-lookup"><span data-stu-id="7df18-109">User context</span></span>

<span data-ttu-id="7df18-110">有关用户、团队或公司的上下文尤其有用</span><span class="sxs-lookup"><span data-stu-id="7df18-110">Context about the user, team or company can be especially useful when</span></span>

* <span data-ttu-id="7df18-111">您需要使用指定的用户或团队创建或关联应用程序中的资源。</span><span class="sxs-lookup"><span data-stu-id="7df18-111">You need to create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="7df18-112">您想要针对 Azure Active Directory 或其他标识提供程序启动身份验证流，并且不希望要求用户再次输入其用户名。</span><span class="sxs-lookup"><span data-stu-id="7df18-112">You want to initiate an authentication flow against Azure Active Directory or other identity provider, and you don't want to require the user to enter their username again.</span></span> <span data-ttu-id="7df18-113">（有关在 Microsoft 团队选项卡中进行身份验证的详细信息，请参阅在[Microsoft 团队中对用户进行身份验证选项卡](~/concepts/authentication/authentication.md)。）</span><span class="sxs-lookup"><span data-stu-id="7df18-113">(For more information on authenticating within your Microsoft Teams tab, see [Authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7df18-114">尽管此用户信息可以帮助提供平稳的用户体验，但*不*应将其用作身份证明。</span><span class="sxs-lookup"><span data-stu-id="7df18-114">Although this user information can help provide a smooth user experience, you should *not* use it as proof of identity.</span></span> <span data-ttu-id="7df18-115">例如，攻击者可以在 "错误浏览器" 中加载页面，并向其提供所需的任何信息。</span><span class="sxs-lookup"><span data-stu-id="7df18-115">For example, an attacker could you load your page in a "bad browser" and provide it with any information they want.</span></span>

## <a name="accessing-context"></a><span data-ttu-id="7df18-116">访问上下文</span><span class="sxs-lookup"><span data-stu-id="7df18-116">Accessing context</span></span>

<span data-ttu-id="7df18-117">您可以通过两种方式访问上下文信息：</span><span class="sxs-lookup"><span data-stu-id="7df18-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="7df18-118">插入 URL 占位符值</span><span class="sxs-lookup"><span data-stu-id="7df18-118">Insert URL placeholder values</span></span>
* <span data-ttu-id="7df18-119">使用[Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="7df18-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client)</span></span>

### <a name="getting-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="7df18-120">通过插入 URL 占位符值获取上下文</span><span class="sxs-lookup"><span data-stu-id="7df18-120">Getting context by inserting URL placeholder values</span></span>

<span data-ttu-id="7df18-121">在配置或内容 Url 中使用占位符。</span><span class="sxs-lookup"><span data-stu-id="7df18-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="7df18-122">Microsoft 团队会在确定要导航到的实际配置或内容 URL 时，将占位符替换为相关值。</span><span class="sxs-lookup"><span data-stu-id="7df18-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL to navigate to.</span></span> <span data-ttu-id="7df18-123">可用的占位符包括[Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest)对象上的所有字段。</span><span class="sxs-lookup"><span data-stu-id="7df18-123">The available placeholders include all fields on the [Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) object.</span></span> <span data-ttu-id="7df18-124">常见占位符包括以下内容：</span><span class="sxs-lookup"><span data-stu-id="7df18-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="7df18-125">{entityId}：首次[配置选项卡](~/tabs/how-to/create-tab-pages/configuration-page.md)时为此选项卡中的项提供的 ID。</span><span class="sxs-lookup"><span data-stu-id="7df18-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="7df18-126">{subEntityId}：在此选项卡_中_为特定项生成[深层链接](~/concepts/build-and-test/deep-links.md)时提供的 ID。应使用此设置还原到实体中的特定状态;例如，滚动到或激活特定的内容片段。</span><span class="sxs-lookup"><span data-stu-id="7df18-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item _within_ this tab. This should be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="7df18-127">{loginHint}：一个适用于 Azure AD 的登录提示的值。这通常是当前用户的登录名，位于其主租户中。</span><span class="sxs-lookup"><span data-stu-id="7df18-127">{loginHint}: A value suitable as a login hint for Azure AD.This is usually the login name of the current user, in their home tenant.</span></span>
* <span data-ttu-id="7df18-128">{userPrincipalName}：当前租户中当前用户的用户主体名称。</span><span class="sxs-lookup"><span data-stu-id="7df18-128">{userPrincipalName}: The User Principal Name of the current user, in the current tenant.</span></span>
* <span data-ttu-id="7df18-129">{userObjectId}：当前租户中当前用户的 Azure AD 对象 ID。</span><span class="sxs-lookup"><span data-stu-id="7df18-129">{userObjectId}: The Azure AD object ID of the current user, in the current tenant.</span></span>
* <span data-ttu-id="7df18-130">{主题}：当前的 UI 主题，如 `default` 、 `dark` 或 `contrast` 。</span><span class="sxs-lookup"><span data-stu-id="7df18-130">{theme}: The current UI theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="7df18-131">{groupId}：选项卡所在的 Office 365 组的 ID。</span><span class="sxs-lookup"><span data-stu-id="7df18-131">{groupId}: The ID of the Office 365 Group in which the tab resides.</span></span>
* <span data-ttu-id="7df18-132">{tid}：当前用户的 Azure AD 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="7df18-132">{tid}: The Azure AD tenant ID of the current user.</span></span>
* <span data-ttu-id="7df18-133">{locale}：用户的当前区域设置格式为 languageId-countryId （例如，en-us）。</span><span class="sxs-lookup"><span data-stu-id="7df18-133">{locale}: The current locale of the user formatted as languageId-countryId (for example, en-us).</span></span>

>[!NOTE]
><span data-ttu-id="7df18-134">以前的 `{upn}` 占位符现在已被弃用。</span><span class="sxs-lookup"><span data-stu-id="7df18-134">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="7df18-135">为了向后兼容，它当前是的同义词 `{loginHint}` 。</span><span class="sxs-lookup"><span data-stu-id="7df18-135">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="7df18-136">例如，假设在您的选项卡清单中，您将 `configURL` 属性设置为</span><span class="sxs-lookup"><span data-stu-id="7df18-136">For example, suppose in your tab manifest you set the `configURL` attribute to</span></span>

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

<span data-ttu-id="7df18-137">登录用户具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="7df18-137">And the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="7df18-138">其用户名为 "user@example.com"</span><span class="sxs-lookup"><span data-stu-id="7df18-138">Their username is 'user@example.com'</span></span>
* <span data-ttu-id="7df18-139">他们的公司租户 ID 为 "e2653c-etc"</span><span class="sxs-lookup"><span data-stu-id="7df18-139">Their company tenant ID is 'e2653c-etc'</span></span>
* <span data-ttu-id="7df18-140">它们是 id 为 "00209384-etc" 的 Office 365 组的成员</span><span class="sxs-lookup"><span data-stu-id="7df18-140">They are a member of the Office 365 group with id '00209384-etc'</span></span>
* <span data-ttu-id="7df18-141">用户已将其 "团队" 主题设置为 "深色"</span><span class="sxs-lookup"><span data-stu-id="7df18-141">The user has set their Teams theme to 'dark'</span></span>

<span data-ttu-id="7df18-142">在配置您的选项卡时，团队会调用此 URL：</span><span class="sxs-lookup"><span data-stu-id="7df18-142">When they configure your tab, Teams calls this URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="7df18-143">使用 Microsoft 团队 JavaScript 库获取上下文</span><span class="sxs-lookup"><span data-stu-id="7df18-143">Getting context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="7df18-144">您还可以通过调用来使用[Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)检索上面列出的信息 `microsoftTeams.getContext(function(context) { /* ... */ })` 。</span><span class="sxs-lookup"><span data-stu-id="7df18-144">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="7df18-145">上下文变量将如以下示例所示。</span><span class="sxs-lookup"><span data-stu-id="7df18-145">The context variable will look like the following example.</span></span>

```json
{
    "teamId": "The Microsoft Teams ID in the format 19:[id]@thread.skype",
    "teamName": "The name of the current team",
    "channelId": "The channel ID in the format 19:[id]@thread.skype",
    "channelName": "The name of the current channel",
    "chatId": "The chat ID in the in the format 19:[id]@thread.skype",
    "locale": "The current locale of the user formatted as languageId-countryId (for example, en-us)",
    "entityId": "The developer-defined unique ID for the entity this content points to",
    "subEntityId": "The developer-defined unique ID for the sub-entity this content points to",
    "loginHint": "A value suitable as a login hint for Azure AD. This is usually the login name of the current user, in their home tenant",
    "userPrincipalName": "The User Principal Name of the current user, in the current tenant",
    "userObjectId": "The Azure AD object id of the current user, in the current tenant",
    "tid": "The Azure AD tenant ID of the current user",
    "groupId": "Guid identifying the current O365 Group ID",
    "theme": "The current UI theme: default | dark | contrast",
    "isFullScreen": "Indicates whether the tab is in full-screen mode",
    "userLicenseType": "Indicates the user licence type in the given SKU (for example, student or teacher)",
    "tenantSKU": "Indicates the SKU category of the tenant (for example, EDU)",
    "channelType": "microsoftTeams.ChannelType.Private | microsoftTeams.ChannelType.Regular"
}
```

## <a name="retrieving-context-in-private-channels"></a><span data-ttu-id="7df18-146">检索专用通道中的上下文</span><span class="sxs-lookup"><span data-stu-id="7df18-146">Retrieving context in private channels</span></span>

> [!Note]
> <span data-ttu-id="7df18-147">专用通道目前位于私有开发人员预览版中。</span><span class="sxs-lookup"><span data-stu-id="7df18-147">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="7df18-148">当您的内容页加载到专用通道中时，将对从该调用中接收的数据 `getContext` 进行模糊处理，以保护通道的隐私。</span><span class="sxs-lookup"><span data-stu-id="7df18-148">When your content page is loaded in a private channel, the data you receive from the `getContext` call will be obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="7df18-149">当内容页位于专用通道中时，会更改以下字段。</span><span class="sxs-lookup"><span data-stu-id="7df18-149">The following fields are changed when your content page is in a private channel.</span></span> <span data-ttu-id="7df18-150">如果您的页面使用以下任何值，则需要检查该 `channelType` 字段以确定页面是否已加载到专用通道中，并进行相应的响应。</span><span class="sxs-lookup"><span data-stu-id="7df18-150">If your page makes use of any of the values below, you'll need to check the `channelType` field to determine if your page is loaded in a private channel, and respond appropriately.</span></span>

* <span data-ttu-id="7df18-151">`groupId`-专用通道未定义</span><span class="sxs-lookup"><span data-stu-id="7df18-151">`groupId` - Undefined for private channels</span></span>
* <span data-ttu-id="7df18-152">`teamId`-设置为专用通道的 threadId</span><span class="sxs-lookup"><span data-stu-id="7df18-152">`teamId` - Set to the threadId of the private channel</span></span>
* <span data-ttu-id="7df18-153">`teamName`-设置为专用通道的名称</span><span class="sxs-lookup"><span data-stu-id="7df18-153">`teamName` - Set to the name of the private channel</span></span>
* <span data-ttu-id="7df18-154">`teamSiteUrl`-设置为专用通道的独特的唯一 SharePoint 网站的 URL</span><span class="sxs-lookup"><span data-stu-id="7df18-154">`teamSiteUrl` - Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="7df18-155">`teamSitePath`-设置为专用通道的独特的唯一 SharePoint 网站的路径</span><span class="sxs-lookup"><span data-stu-id="7df18-155">`teamSitePath` - Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="7df18-156">`teamSiteDomain`-设置为专用通道的独特的唯一 SharePoint 网站域的域</span><span class="sxs-lookup"><span data-stu-id="7df18-156">`teamSiteDomain` - Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

## <a name="theme-change-handling"></a><span data-ttu-id="7df18-157">主题更改处理</span><span class="sxs-lookup"><span data-stu-id="7df18-157">Theme change handling</span></span>

<span data-ttu-id="7df18-158">您可以注册您的应用程序，以通过调用的主题更改来进行通知 `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` 。</span><span class="sxs-lookup"><span data-stu-id="7df18-158">You can register your app to be told if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="7df18-159">`theme`函数中的参数将是值为 `default` 、或的字符串 `dark` `contrast` 。</span><span class="sxs-lookup"><span data-stu-id="7df18-159">The `theme` argument in the function will be a string with a value of `default`, `dark`, or `contrast`.</span></span>