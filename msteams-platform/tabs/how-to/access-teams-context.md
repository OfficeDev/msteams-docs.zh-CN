---
title: 获取您的选项卡的上下文
description: 介绍如何获取选项卡的用户上下文
keywords: 团队选项卡用户上下文
ms.openlocfilehash: 8c94c4fd895896186ddda20bfaafd1d6ccdc1e73
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346796"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a>获取 Microsoft 团队选项卡的上下文

您的选项卡可能需要上下文信息才能显示相关内容。

* 您的选项卡可能需要有关用户、团队或公司的基本信息。
* 您的选项卡可能需要区域设置和主题信息。
* 您的选项卡可能需要读取 `entityId` 或 `subEntityId` 标识此选项卡中的内容。

## <a name="user-context"></a>用户上下文

有关用户、团队或公司的上下文尤其有用

* 您需要使用指定的用户或团队创建或关联应用程序中的资源。
* 您想要针对 Azure Active Directory 或其他标识提供程序启动身份验证流，并且不希望要求用户再次输入其用户名。  (有关在 Microsoft 团队选项卡中进行身份验证的详细信息，请参阅在 [Microsoft 团队中对用户进行身份验证选项卡](~/concepts/authentication/authentication.md)。 ) 

> [!IMPORTANT]
> 尽管此用户信息可以帮助提供平稳的用户体验，但 *不* 应将其用作身份证明。 例如，攻击者可以在 "错误浏览器" 中加载页面，并向其提供所需的任何信息。

## <a name="accessing-context"></a>访问上下文

您可以通过两种方式访问上下文信息：

* 插入 URL 占位符值
* 使用 [Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)

### <a name="getting-context-by-inserting-url-placeholder-values"></a>通过插入 URL 占位符值获取上下文

在配置或内容 Url 中使用占位符。 Microsoft 团队会在确定要导航到的实际配置或内容 URL 时，将占位符替换为相关值。 可用的占位符包括 [Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) 对象上的所有字段。 常见占位符包括以下内容：

* {entityId}：首次 [配置选项卡](~/tabs/how-to/create-tab-pages/configuration-page.md)时为此选项卡中的项提供的 ID。
* {subEntityId}：在此选项卡 _中_ 为特定项生成 [深层链接](~/concepts/build-and-test/deep-links.md)时提供的 ID。应使用此设置还原到实体中的特定状态;例如，滚动到或激活特定的内容片段。
* {loginHint}：一个适用于 Azure AD 的登录提示的值。这通常是当前用户的登录名，位于其主租户中。
* {userPrincipalName}：当前租户中当前用户的用户主体名称。
* {userObjectId}：当前租户中当前用户的 Azure AD 对象 ID。
* {主题}：当前的 UI 主题，如 `default` 、 `dark` 或 `contrast` 。
* {groupId}：选项卡所在的 Office 365 组的 ID。
* {tid}：当前用户的 Azure AD 租户 ID。
* {locale}：用户的当前区域设置格式为 languageId-countryId (例如，en-us) 。
* {osLocaleInfo}：用户的操作系统中的更详细的区域设置信息（如果有）。 可与以下项一起使用：
    * @microsoft/globe NPM 程序包，以确保应用程序遵循用户的操作系统日期和
    * 时间格式配置。
* {sessionId}：要在关联遥测数据时使用的当前团队会话的唯一 ID。
* {channelId}：与内容关联的通道的 Microsoft 团队 ID。
* {channelName}：与内容关联的频道的名称。
* {chatId}：与内容相关联的聊天的 Microsoft 团队 ID。
* {url}：此选项卡的内容 URL。
* {websiteUrl}：此选项卡的网站 URL。
* {favoriteChannelsOnly}：仅允许选择最常用频道的标志。
* {favoriteTeamsOnly}：仅允许选择收藏的团队的标志。
* {userTeamRole}：团队中的当前用户的角色。
* {teamType}：团队的类型。
* {isTeamLocked}：团队的锁定状态。
* {isTeamArchived}：工作组的存档状态。
* {isFullScreen}：指示选项卡是否处于全屏模式。
* {teamSiteUrl}：与团队关联的根 SharePoint 网站。
* {teamSiteDomain}：与团队关联的根 SharePoint 网站的域。
* {teamSitePath}：与团队关联的 SharePoint 网站的相对路径。
* {channelRelativeUrl}： SharePoint 文件夹与通道关联的相对路径。
* {tenantSKU}：当前用户租户的许可证类型。
* {ringId}：当前的震铃 ID。
* {appSessionId}：用于关联遥测数据的当前会话的唯一 ID。
* {completionBotId}：指定用于发送用户与任务模块的交互结果的 bot ID。
* {conversationId}：会话的 Id。
* {hostClientType}：主机客户端的类型。 (可能的值包括： android、ios、web、desktop 和 rigel。 ) 
* {frameContext}： (内容、任务、设置、删除、sidePanel) 加载选项卡 url 的上下文。
* {sharepoint}：只有在 SharePoint 中托管时，此选项才可用。
* {meetingId}：在会议上下文中运行时，选项卡将使用它。
* {userLicenseType}当前用户的许可证类型。

>[!NOTE]
>以前的 `{upn}` 占位符现在已被弃用。 为了向后兼容，它当前是的同义词 `{loginHint}` 。

例如，假设在您的选项卡清单中，您将 `configURL` 属性设置为

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

登录用户具有以下属性：

* 其用户名为 "user@example.com"
* 他们的公司租户 ID 为 "e2653c-etc"
* 它们是 id 为 "00209384-etc" 的 Office 365 组的成员
* 用户已将其 "团队" 主题设置为 "深色"

在配置您的选项卡时，团队会调用此 URL：

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a>使用 Microsoft 团队 JavaScript 库获取上下文

您还可以通过调用来使用 [Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 检索上面列出的信息 `microsoftTeams.getContext(function(context) { /* ... */ })` 。

上下文变量将如以下示例所示。

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

## <a name="retrieving-context-in-private-channels"></a>检索专用通道中的上下文

> [!Note]
> 专用通道目前位于私有开发人员预览版中。

当您的内容页加载到专用通道中时，将对从该调用中接收的数据 `getContext` 进行模糊处理，以保护通道的隐私。 当内容页位于专用通道中时，会更改以下字段。 如果您的页面使用以下任何值，则需要检查该 `channelType` 字段以确定页面是否已加载到专用通道中，并进行相应的响应。

* `groupId` -专用通道未定义
* `teamId` -设置为专用通道的 threadId
* `teamName` -设置为专用通道的名称
* `teamSiteUrl` -设置为专用通道的独特的唯一 SharePoint 网站的 URL
* `teamSitePath` -设置为专用通道的独特的唯一 SharePoint 网站的路径
* `teamSiteDomain` -设置为专用通道的独特的唯一 SharePoint 网站域的域

## <a name="theme-change-handling"></a>主题更改处理

您可以注册您的应用程序，以通过调用的主题更改来进行通知 `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` 。

`theme`函数中的参数将是值为 `default` 、或的字符串 `dark` `contrast` 。
