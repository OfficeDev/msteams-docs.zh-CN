---
title: 获取选项卡的上下文
description: 在本模块中，了解如何将用户上下文获取到选项卡、用户上下文和 Access 上下文信息
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: d6723c4733bd127dd32970e3d1059a75771c8bee
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142309"
---
# <a name="get-context-for-your-tab"></a>获取选项卡的上下文

选项卡需要上下文信息才能显示相关内容：

* 有关用户、团队或公司的基本信息。
* 区域设置和主题信息。
* 读取 `entityId` 或 `subEntityId` 标识此选项卡中的内容。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="user-context"></a>用户上下文

在以下情况下，有关用户、团队或公司的上下文可能特别有用：

* 在应用中创建资源或将资源与指定的用户或团队相关联。
* 从Microsoft Azure Active Directory (Azure AD) 或其他标识提供者启动身份验证流，并且无需用户再次输入其用户名。

有关详细信息，请参阅[Microsoft Teams中对用户进行身份验证](~/concepts/authentication/authentication.md)。

> [!IMPORTANT]
> 尽管此用户信息有助于提供流畅的用户体验，但不得将其用作标识证明。  例如，攻击者可以在浏览器中加载页面并呈现有害信息或请求。

## <a name="access-context-information"></a>访问上下文信息

可以通过两种方式访问上下文信息：

* 插入 URL 占位符值。
* 使用 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)。

### <a name="get-context-by-inserting-url-placeholder-values"></a>通过插入 URL 占位符值获取上下文

在配置或内容 URL 中使用占位符。 确定实际配置或内容 URL 时，Microsoft Teams 会使用相关值替换占位符。 可用占位符包括 [上下文](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-1.12.1&preserve-view=true) 对象上的所有字段。 常用占位符包括以下内容：

* {entityId}：首次配置选项卡列表时， [此选项卡中提供的](~/tabs/how-to/create-tab-pages/configuration-page.md)。
* {subEntityId}：在此选项卡中为特定项生成 [深层链接](~/concepts/build-and-test/deep-links.md) 时提供的 ID。这必须用于还原到实体中的特定状态;例如，滚动到特定内容或激活特定内容。
* {loginHint}：一个适合作为 Azure AD 登录提示的值。 这通常是其主租户中当前用户的登录名。
* {userPrincipalName}：当前租户中当前用户的用户主体名称。
* {userObjectId}：当前租户中当前用户的 Azure AD 对象 ID。
* {theme}：当前用户界面 (UI) 主题，例如 `default`， `dark`或 `contrast`。
* {groupId}：选项卡所在的Office 365组的 ID。
* {tid}：当前用户的 Azure AD 租户 ID。
* {locale}：格式为 languageId-countryId (en-us) 的用户的当前区域设置。

> [!NOTE]
> 上一 `{upn}` 占位符现已弃用。 出于向后兼容性，它目前是 `{loginHint}`的同义词。

例如，在将属性设置 `configURL` 为 `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`的选项卡清单中，已登录用户具有以下属性：

* 他们的用户名 **user@example.com**。
* 其公司租户 ID 为 **e2653c-etc**。
* 他们是 ID 为 **00209384 等** 的Office 365组的成员。
* 用户已将其Teams主题设置为 **深色**。

配置选项卡时，Teams调用以下 URL：

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>使用 Microsoft Teams JavaScript 库获取上下文

git-issue-clear-the-full-set-of-values-any-context-object-property-can-take 你也可以通过调用`microsoftTeams.getContext(function(context) { /* ... */ })`使用 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 检索上面列出的信息。

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
    "userLicenseType": "The license type for the current user. Possible values are E1, E3, and E5 enterprise plans",
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

还可以通过调`app.getContext()`用函数，使用 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 检索上面列出的信息。 有关其他信息，请参阅 [上下文接口](/javascript/api/@microsoft/teams-js/app.context?view=msteams-client-js-latest&preserve-view=true)的属性。


## <a name="retrieve-context-in-private-channels"></a>在专用通道中检索上下文

在专用通道中加载内容页面时，从 `getContext` 呼叫中收到的数据会混淆，以保护通道的隐私。

当内容页面位于专用频道中时，将更改以下字段：

* `groupId`：未定义专用频道
* `teamId`：设置为专用通道的 threadId
* `teamName`：设置为专用通道的名称
* `teamSiteUrl`：设置为专用通道的非重复、唯一SharePoint网站的 URL
* `teamSitePath`：设置为专用通道的非重复、唯一SharePoint网站的路径
* `teamSiteDomain`：设置为专用通道的非重复唯一SharePoint站点域的域

如果页面使用这些值中的任何一个，则字段的 `channelType` 值必须 `Private` 是确定页面是否加载在专用通道中，并且可以相应地响应。

## <a name="retrieve-context-in-microsoft-teams-connect-shared-channels"></a>检索Microsoft Teams Connect共享通道中的上下文

> [!NOTE]
> 目前，Microsoft Teams Connect共享频道仅在[开发人员预览版](../../resources/dev-preview/developer-preview-intro.md)中。

当内容页面加载到Microsoft Teams Connect共享通道中时，由于共享频道中用户的唯一名册，从`getContext`呼叫中收到的数据将会更改。

当内容页面位于共享频道中时，将更改以下字段：

* `groupId`：未定义共享通道。
* `teamId`：设置为 `threadId` 团队，为当前用户共享频道。 如果用户有权访问多个团队， `teamId` 则设置为托管 (创建) 共享通道的团队。
* `teamName`：设置为团队的名称，为当前用户共享频道。 如果用户有权访问多个团队， `teamName` 则设置为托管 (创建) 共享通道的团队。
* `teamSiteUrl`：设置为共享通道的非重复、唯一SharePoint站点的 URL。
* `teamSitePath`：设置为共享通道的非重复唯一SharePoint站点的路径。
* `teamSiteDomain`：设置为共享通道的非重复唯一SharePoint站点域的域。

除了这些字段更改之外，还有两个新字段可用于共享频道：

* `hostTeamGroupId`：设置为 `groupId` 与托管团队或创建共享频道的团队关联。 该属性可以使 Microsoft 图形 API调用检索共享通道的成员身份。
* `hostTeamTenantId`：设置为 `tenantId` 与托管团队或创建共享频道的团队关联。 可以使用当前用户的租户 ID `tid` `getContext` 交叉引用该属性，以便确定该用户是托管团队租户的内部还是外部。

如果页面使用这些值中的任何一个，则字段的 `channelType` 值必须 `Shared` 确定页面是否已加载到共享通道中，并且可以做出适当的响应。

> [!NOTE]
> 每次用户重启或重新加载Teams桌面或 Web 客户端时，都会创建一个新的 sessionID，由Teams会话跟踪，而当用户退出Teams应用并在Teams平台中重新加载它时，会创建一个新的应用会话ID，由应用会话跟踪。

## <a name="handle-theme-change"></a>处理主题更改

如果主题通过调用 `app.registerOnThemeChangeHandler(function(theme) { /* ... */ })`更改，可以注册要通知的应用。

函`theme`数中的参数是值为`default``dark``contrast`或 . 的字符串。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [具有自适应卡片的生成选项卡](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="see-also"></a>另请参阅

* [选项卡设计指南](../../tabs/design/tabs.md)
* [Teams 选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或群组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [在选项卡中使用任务模块](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
