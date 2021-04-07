---
title: 获取选项卡的上下文
description: 介绍如何将用户上下文获取有关选项卡的用户上下文
keywords: Teams 选项卡用户上下文
ms.openlocfilehash: 18c8541e948f206fcdddc3a942325e2f5d6e3e5c
ms.sourcegitcommit: 309823e6911b4e8e307493cbd59880fe69a4dca3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2020
ms.locfileid: "49727161"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a>获取 Microsoft Teams 选项卡的上下文

你的选项卡可能需要上下文信息以显示相关内容。

* 你的选项卡可能需要有关用户、团队或公司的基本信息。
* 选项卡可能需要区域设置和主题信息。
* 你的选项卡可能需要阅读`entityId``subEntityId`此选项卡中内容的内容的选项卡。

## <a name="user-context"></a>用户上下文

用户、团队或公司的上下文在

* 需要将应用中的资源创建或与指定的用户或团队关联。
* 想要针对 Azure Active Directory 或其他标识提供程序启动身份验证流程，并且不希望用户再次输入其用户名。 （有关在 Microsoft Teams 选项卡中进行身份验证详细信息，请参阅 [Microsoft Teams 选项卡中的用户身份验证](~/concepts/authentication/authentication.md)。）

> [!IMPORTANT]
> 虽然此用户信息可帮助提供流畅的用户体验，但 *不应* 使用它作为身份证明。 例如，攻击者可能会将你的页面加载在"错误的浏览器"中，并呈现有害信息或请求。

## <a name="accessing-context"></a>访问上下文

可以通过两种方式访问上下文信息：

* 插入 URL 占位符值
* 使用 Microsoft Teams JavaScript [SDK](/javascript/api/overview/msteams-client)

### <a name="getting-context-by-inserting-url-placeholder-values"></a>通过插入 URL 占位符值获取上下文

在配置或内容 URL 中使用占位符。 确定实际配置或内容 URL 时，Microsoft Teams 会使用相关值替换占位符。 可用的占位符包含上下文对象 [上](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 字段。 常用占位符包括以下内容：

* {entityId}：首次配置选项卡列表时， [此选项卡中提供的](~/tabs/how-to/create-tab-pages/configuration-page.md)。
* {subEntityId}：此选项卡内为特定项目 [深链接](~/concepts/build-and-test/deep-links.md) 提供 _ID_。这应用于还原到实体中的特定状态;例如，滚动到特定部分的内容或激活特定部分的内容。
* {loginHint}：适用于 Azure AD 登录提示的值。这通常是当前用户的家庭租户中的登录名。
* {userPrincipalName}：当前租户中当前用户的用户主体名称。
* {userObjectId}：当前租户中的当前用户的 Azure AD 对象 ID。
* {主题}：当前 UI 主题，如 `default`、 `dark`或 `contrast`。
* {groupId}：选项卡所在的 Office 365 组的 ID。
* {tid}：当前用户的 Azure AD 租户 ID。
* {locale}：用户格式设置为 languageId-countryId 的当前区域设置（例如 en-us）。

>[!NOTE]
>上一 `{upn}` 占位符现已弃用。 出于向后兼容性，它目前是 `{loginHint}`的同义词。

例如，假设在选项卡清单中，将 `configURL` 属性设置为

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

已登录的用户具有以下属性：

* 他们的用户名是"user@example.com"
* 其公司租户 ID 为"e2653c 等"
* 他们是 ID 为 "00209384-etc" 的 Office 365 组的成员。
* 用户将 Teams 主题设置为"深色"

当他们配置你的选项卡时，Teams 将调用此 URL：

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a>使用 Microsoft Teams JavaScript 库获取上下文

还可通过调用 `microsoftTeams.getContext(function(context) { /* ... */ })` 使用[ Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 检索前面列出的信息。

上下文变量将类似以下示例。

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
    "tenantSKU": "The license type for the current user tenant",
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

## <a name="retrieving-context-in-private-channels"></a>在专用频道中检索上下文

> [!Note]
> 专用频道目前为私人开发人员预览版。

当你的内容页面加载在专用频道中时，从免费呼叫 `getContext` 接收的数据将被模糊显示，以保护频道的隐私。 当你的内容页面位于专用频道中时，会更改以下字段。 如果页面使用任意以下值，需检查 `channelType` 字段以确定页面是否加载在专用频道中，并作出相应响应。

* `groupId` - 未定义专用频道
* `teamId` - 设置为专用频道的会话 Id
* `teamName` - 设置为专用频道的名称
* `teamSiteUrl` - 设置为专用频道的独特 SharePoint 网站的 URL
* `teamSitePath` - 设置为专用频道的独特 SharePoint 网站路径
* `teamSiteDomain` - 设置为专用频道的独特 SharePoint 网站域的域

> [!Note]
>  teamSiteUrl 也适用于标准频道。

## <a name="theme-change-handling"></a>主题更改处理

可致电组织，注册应用，告知主题是否 `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`。

函数 `theme` 参数将为一个字符串，其值为 `default`、 `dark`或 `contrast`。
