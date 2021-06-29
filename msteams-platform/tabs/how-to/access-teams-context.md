---
title: 获取选项卡的上下文
description: 介绍如何将用户上下文获取有关选项卡的用户上下文
localization_priority: Normal
ms.topic: how-to
keywords: Teams 选项卡用户上下文
ms.openlocfilehash: 8c91cf5a65f13d9f58f6ae8aa2678266c37338c8
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179725"
---
# <a name="get-context-for-your-tab"></a>获取选项卡的上下文

您的选项卡需要上下文信息来显示相关内容：

* 有关用户、团队或公司的基本信息。
* 区域设置和主题信息。
* 读取 `entityId` 标识 `subEntityId` 此选项卡中的内容的 或。

## <a name="user-context"></a>用户上下文

在以下情况下，有关用户、团队或公司的上下文可能特别有用：

* 在应用中创建资源或将资源与指定的用户或团队关联。
* 从 AAD Azure Active Directory (或其他) 启动身份验证流，并且不需要用户再次输入其用户名。 有关详细信息，请参阅"验证[用户身份Microsoft Teams选项卡。](~/concepts/authentication/authentication.md)

> [!IMPORTANT]
> 虽然此用户信息可帮助提供流畅的用户体验，但不得使用它作为标识证明。 例如，攻击者可以在浏览器中加载页面并呈现有害的信息或请求。

## <a name="access-context-information"></a>访问上下文信息

可以通过两种方式访问上下文信息：

* 插入 URL 占位符值。
* 使用[Microsoft Teams JavaScript 客户端 SDK。](/javascript/api/overview/msteams-client)

### <a name="get-context-by-inserting-url-placeholder-values"></a>通过插入 URL 占位符值获取上下文

在配置或内容 URL 中使用占位符。 确定实际配置或内容 URL 时，Microsoft Teams 会使用相关值替换占位符。 可用占位符包括上下文对象上 [的所有](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 字段。 常用占位符包括以下内容：

* {entityId}：首次配置选项卡列表时， [此选项卡中提供的](~/tabs/how-to/create-tab-pages/configuration-page.md)。
* {subEntityId}：为此选项卡内的特定项生成深层链接时[](~/concepts/build-and-test/deep-links.md)提供的 ID。这必须用于还原到实体中的特定状态;例如，滚动到或激活特定内容部分。
* {loginHint}：适合用作 AAD 登录提示的值。 这通常是其主租户中当前用户的登录名。
* {userPrincipalName}：当前租户中当前用户的用户主体名称。
* {userObjectId}：当前租户中当前用户的 AAD 对象 ID。
* {theme}：当前用户界面 (UI) 主题，如 、 `default` `dark` 或 `contrast` 。
* {groupId}：选项卡Office 365组 ID。
* {tid}：当前用户的 AAD 租户 ID。
* {locale}：格式化为 languageId-countryId 的用户的当前区域设置。 例如，en-us。

> [!NOTE]
> 上一 `{upn}` 占位符现已弃用。 出于向后兼容性，它目前是 `{loginHint}`的同义词。

例如，在选项卡清单中，将 `configURL` 属性设置为 `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"` ，登录用户具有以下属性：

* 其用户名为 **user@example.com**。
* 他们的公司租户 ID 是 **e2653c-etc。**
* 他们是 id 为 **00209384 Office 365组的成员。**
* 用户已设置其Teams主题为 **深色**。

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

## <a name="retrieve-context-in-private-channels"></a>检索私人频道中的上下文

> [!Note]
> 专用频道目前为私人开发人员预览版。

当你的内容页面加载到私人频道中时，你通过调用收到的数据会混淆以保护 `getContext` 通道的隐私。 当内容页位于私人频道中时，将更改以下字段：

* `groupId`：未为私人频道定义
* `teamId`：设置为私人频道的 threadId
* `teamName`：设置为私人频道的名称
* `teamSiteUrl`：设置为专用频道的独特SharePoint网站的 URL
* `teamSitePath`：设置为专用频道的独特SharePoint网站的路径
* `teamSiteDomain`：设置为专用频道的唯一SharePoint网站域的域

如果页面使用了这些值中的任意值，则必须检查字段以确定页面是否加载到私人频道中并 `channelType` 做出相应的响应。

> [!Note]
> `teamSiteUrl` 还适用于标准频道。

## <a name="handle-theme-change"></a>处理主题更改

你可以注册应用，以在主题发生更改时通过调用 通知 `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` 。

函数 `theme` 中的参数是值为 、 `default` 或 的 `dark` 字符串 `contrast` 。

## <a name="see-also"></a>另请参阅

* [选项卡设计指南](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Teams选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [具有自适应卡片的生成选项卡](~/tabs/how-to/build-adaptive-card-tabs.md)