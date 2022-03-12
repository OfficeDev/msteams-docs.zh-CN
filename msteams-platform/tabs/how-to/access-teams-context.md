---
title: 获取选项卡的上下文
description: 介绍如何将用户上下文获取有关选项卡的用户上下文
ms.localizationpriority: medium
ms.topic: how-to
keywords: Teams 选项卡用户上下文
ms.openlocfilehash: b991a9703faedd3b849287abd5aef2d42e1baf9e
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453682"
---
# <a name="get-context-for-your-tab"></a>获取选项卡的上下文

您的选项卡需要上下文信息来显示相关内容：

* 有关用户、团队或公司的基本信息。
* 区域设置和主题信息。
* 读取 标识 `entityId` 此选项卡中的内容的 或 `subEntityId` 。

## <a name="user-context"></a>用户上下文

在以下情况下，有关用户、团队或公司的上下文可能特别有用：

* 在应用中创建资源或将资源与指定的用户或团队关联。
* 您从用户或其他Microsoft Azure Active Directory (Azure AD) 启动身份验证流，并且不需要用户再次输入其用户名。

有关详细信息，请参阅验证[用户Microsoft Teams](~/concepts/authentication/authentication.md)。

> [!IMPORTANT]
> 虽然此用户信息可帮助提供流畅的用户体验，但不得使用它作为标识证明。  例如，攻击者可以在浏览器中加载页面并呈现有害的信息或请求。

## <a name="access-context-information"></a>访问上下文信息

可以通过两种方式访问上下文信息：

* 插入 URL 占位符值。
* 使用 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)。

### <a name="get-context-by-inserting-url-placeholder-values"></a>通过插入 URL 占位符值获取上下文

在配置或内容 URL 中使用占位符。 确定实际配置或内容 URL 时，Microsoft Teams 会使用相关值替换占位符。 可用占位符包括上下文对象上 [的所有](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 字段。 常用占位符包括以下内容：

* {entityId}：首次配置选项卡列表时， [此选项卡中提供的](~/tabs/how-to/create-tab-pages/configuration-page.md)。
* {subEntityId}：为此选项卡内的特定项生成深层链接时[](~/concepts/build-and-test/deep-links.md)提供的 ID。这必须用于还原到实体中的特定状态;例如，滚动到或激活特定内容部分。
* {loginHint}：适合用作登录提示的值Azure AD。 这通常是其主租户中当前用户的登录名。
* {userPrincipalName}：当前租户中当前用户的用户主体名称。
* {userObjectId}：Azure AD租户中当前用户的对象 ID。
* {theme}：当前用户界面 (UI) 主题，`default``dark`如 、 或 `contrast`。
* {groupId}：选项卡Office 365组 ID。
* {tid}：当前用户的 Azure AD 租户 ID。
* {locale}：设置为 languageId-countryId 的用户的当前区域设置 (en-us) 。

> [!NOTE]
> 上一 `{upn}` 占位符现已弃用。 出于向后兼容性，它目前是 `{loginHint}`的同义词。

例如，在选项卡清单中，将 属性`configURL``"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`设置为 ，登录用户具有以下属性：

* 其 **用户名 user@example.com。**
* 其公司租户 ID 为 **e2653c 等**。
* 他们是 id 为 **00209384** Office 365组的成员。
* 用户已设置其Teams主题 **为深色**。

在配置选项卡时，Teams调用以下 URL：

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>使用 JavaScript Microsoft Teams获取上下文

还可通过调用 `microsoftTeams.getContext(function(context) { /* ... */ })` 使用[ Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 检索前面列出的信息。

以下代码提供了上下文变量的示例：

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
    "groupId": "Guid identifying the current Office 365 Group ID",
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
    "hostClientType": "The type of host client. Possible values are android, ios, web, desktop, surfaceHub, teamsRoomsAndroid, teamsPhones, teamsDisplays rigel (deprecated, use teamsRoomsWindows instead)",
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
    "defaultOneNoteSectionId": "The OneNote section ID that is linked to the channel",
    "isMultiWindow": "The indication whether the tab is in a pop out window"
}
```

## <a name="retrieve-context-in-private-channels"></a>检索私人频道中的上下文

当你的内容页面加载到私人频道中 `getContext` 时，你通过调用收到的数据会混淆以保护通道的隐私。

当内容页位于私人频道中时，将更改以下字段：

* `groupId`：未为私人频道定义
* `teamId`：设置为私人频道的 threadId
* `teamName`：设置为私人频道的名称
* `teamSiteUrl`：设置为专用频道的唯一SharePoint网站 URL
* `teamSitePath`：设置为专用频道的独特SharePoint网站的路径
* `teamSiteDomain`：设置为专用频道的独特、唯SharePoint网站域的域

如果页面使用了这些值 `channelType` 中的任意值，则 field `Private` 的值必须确定页面是否加载到私人频道中，并可以做出相应的响应。

## <a name="retrieve-context-in-microsoft-teams-connect-shared-channels"></a>检索共享Microsoft Teams 连接中的上下文

> [!NOTE]
> 目前，Microsoft Teams 连接频道仅在开发人员[预览版](../../resources/dev-preview/developer-preview-intro.md)中。

在共享频道中加载内容Microsoft Teams 连接，`getContext`由于共享频道中用户的唯一名单，从呼叫接收的数据会发生变化。

当内容页位于共享通道中时，将更改以下字段：

* `groupId`：未为共享频道定义。
* `teamId`：设置为团队 `threadId` 的 ，频道为当前用户共享。 如果用户有权访问多个团队 `teamId` ，则 设置为托管共享频道 (创建) 团队。
* `teamName`：设置为团队的名称，为当前用户共享频道。 如果用户有权访问多个团队 `teamName` ，则 设置为托管共享频道 (创建) 团队。
* `teamSiteUrl`：设置为共享频道的唯一SharePoint网站 URL。
* `teamSitePath`：设置为共享频道的唯一SharePoint网站的路径。
* `teamSiteDomain`：设置为共享通道的唯一SharePoint网站域的域。

除了这些字段更改之外，还有两个新字段可用于共享频道：

* `hostTeamGroupId`：设置为与 `groupId` 托管团队或创建共享频道的团队关联的 。 属性可以使 Microsoft Graph API 调用检索共享通道的成员身份。
* `hostTeamTenantId`：设置为与 `tenantId` 托管团队或创建共享频道的团队关联的 。 属性可以与在 字段中找到的当前用户的租户 ID `tid` `getContext` 交叉引用，以确定用户是托管团队租户的内部用户还是外部用户。

如果页面使用了这些值 `channelType` 中的任意值，则 field `Shared` 的值必须确定页面是否加载到共享通道中，并可以做出相应的响应。

## <a name="handle-theme-change"></a>处理主题更改

你可以注册应用，以在主题发生更改时通过调用 通知 `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`。

函数 `theme` 中的参数是值为 `default`、 或 的 `dark`字符串 `contrast`。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [具有自适应卡片的生成选项卡](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="see-also"></a>另请参阅

* [选项卡设计指南](../../tabs/design/tabs.md)
* [Teams选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [在选项卡中使用任务模块](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
