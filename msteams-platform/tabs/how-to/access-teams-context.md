---
title: 获取选项卡的上下文
description: 了解选项卡的上下文、用户、团队或公司的上下文、访问信息、在专用频道或共享频道中检索上下文以及处理主题更改。
ms.localizationpriority: high
ms.topic: how-to
ms.openlocfilehash: 2048f46e6cbe181a755df12b61c5153aacc21186
ms.sourcegitcommit: bd30d33af59dd870a309ae72b4c4496c9c1f920d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2022
ms.locfileid: "67635306"
---
# <a name="get-context-for-your-tab"></a>获取选项卡的上下文

选项卡需要上下文信息才能显示相关内容：

* 有关用户、团队或公司的基本信息。
* 区域设置和主题信息。
* `page.subPageId`标`page.id`识此选项卡中的内容， (称为 `entityId` TeamsJS v.2.0.0) 之前`subEntityId`。

## <a name="user-context"></a>用户上下文

在以下情况下，有关用户、团队或公司的上下文可能特别有用：

* 在应用中创建资源或将资源与指定的用户或团队相关联。
* 从Microsoft Azure Active Directory (Azure AD) 或其他标识提供者启动身份验证流，并且无需用户再次输入其用户名。

有关详细信息，请参阅 [Microsoft Teams 中的用户身份验证](~/concepts/authentication/authentication.md)。

> [!IMPORTANT]
> 尽管此用户信息有助于提供流畅的用户体验，但不得将其用作标识证明。  例如，攻击者可以在浏览器中加载页面并呈现有害信息或请求。

## <a name="access-context-information"></a>访问上下文信息

可以通过两种方式访问上下文信息：

* 使用 [URL 占位符值](#get-context-by-inserting-url-placeholder-values)。
* 从 Microsoft Teams JavaScript 客户端 SDK [上下文](/javascript/api/@microsoft/teams-js/app.context) 对象。

### <a name="get-context-by-inserting-url-placeholder-values"></a>通过插入 URL 占位符值获取上下文

在配置或内容 URL 中使用占位符。 确定实际配置或内容 URL 时，Microsoft Teams 会使用相关值替换占位符。 可用占位符包括 [上下文](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 对象上的所有字段。 常见占位符包括以下属性：

* [{page.id}](/javascript/api/@microsoft/teams-js/app.pageinfo#@microsoft-teams-js-app-pageinfo-id)：首次 [配置页面](~/tabs/how-to/create-tab-pages/configuration-page.md)时定义的页面的开发人员定义的唯一 ID。  (称为 `{entityId}` TeamsJS v.2.0.0) 之前。
* [{page.subPageId}](/javascript/api/@microsoft/teams-js/app.pageinfo#@microsoft-teams-js-app-pageinfo-subpageid)：在为页面中的特定项目生成 [深层链接](~/concepts/build-and-test/deep-links.md) 时定义的此内容点的子页的开发人员定义的唯一 ID。  (称为 `{subEntityId}` TeamsJS v.2.0.0) 之前。
* [{user.loginHint}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-loginhint)：一个适合作为 Azure AD 登录提示的值。 这通常是其主租户中当前用户的登录名。  (称为 `{loginHint}` TeamsJS v.2.0.0) 之前。
* [{user.userPrincipalName}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-userprincipalname)：当前租户中当前用户的用户主体名称。  (称为 `{userPrincipalName}` TeamsJS v.2.0.0) 之前。
* [{user.id}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-id)：当前租户中当前用户的 Azure AD 对象 ID。  (称为 `{userObjectId}` TeamsJS v.2.0.0) 之前。
* [{app.theme}](/javascript/api/@microsoft/teams-js/app.appinfo#@microsoft-teams-js-app-appinfo-theme)：当前用户界面 (UI) 主题，例如 `default`， `dark`或 `contrast`。  (称为 `{theme}` TeamsJS v.2.0.0) 之前。
* [{team.groupId}](/javascript/api/@microsoft/teams-js/app.teaminfo#@microsoft-teams-js-app-teaminfo-groupid)：选项卡所在的Office 365组的 ID。  (称为 `{groupId}` TeamsJS v.2.0.0) 之前
* [{user.tenant.id}](/javascript/api/@microsoft/teams-js/app.tenantinfo#@microsoft-teams-js-app-tenantinfo-id)：当前用户的 Azure AD 租户 ID。  (称为 `{tid}` TeamsJS v.2.0.0) 之前。
* [{app.locale}](/javascript/api/@microsoft/teams-js/app.appinfo#@microsoft-teams-js-app-appinfo-locale)：例如`en-us`，格式为 *languageId-countryId* 的用户的当前区域设置。  (称为 `{locale}` TeamsJS v.2.0.0) 之前。

> [!NOTE]
> 上一 `{upn}` 占位符现已弃用。 出于向后兼容性，它目前是 `{user.loginHint}`的同义词。

例如，在应用清单中，如果将 Tab *configurationUrl* 属性设置为 `"https://www.contoso.com/config?name={user.loginHint}&tenant={user.tenant.id}&group={team.groupId}&theme={app.theme}"` 登录用户，则具有以下属性：

* 他们的用户名 **user@example.com**。
* 其公司租户 ID 为 **e2653c-etc**。
* 他们是 ID 为 **00209384 等** 的Office 365组的成员。
* 用户已将其 Teams 主题设置为 **深色**。

. . . 然后，在配置选项卡时，Teams 将调用以下 URL：

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>使用 Microsoft Teams JavaScript 库获取上下文

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

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

## <a name="typescript"></a>TypeScript

```TypeScript
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context: Context) => {
    /*...*/
});
```

等效 `async/await` 模式：

```TypeScript
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context: Context = await app.getContext();
  /*...*/
}
```

## <a name="javascript"></a>JavaScript

```js
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context) => {
    /*...*/
});
```

等效 `async/await` 模式：

```js
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context = await app.getContext();
  /*...*/
}
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

## <a name="typescript"></a>TypeScript

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context: microsoftTeams.Context) => {
  /* ... */
});
```

## <a name="javascript"></a>JavaScript

```js
import microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context) => {
  /* ... */ 
});
```

---

下表列出了上下文对象的常用 *上下文* 属性：

| TeamsJS v2 名称 | TeamsJS v1 名称 | 说明 |
|-----------------|-----------------|-------------|
| team.internalId | teamId | 与内容关联的团队的 Microsoft Teams ID。 |
| team.displayName | teamName | 与内容关联的团队的名称。 |
| channel.id | channelId | 与内容关联的通道的 Microsoft Teams ID。 |
| channel.displayName | channelName | 与内容关联的通道的名称。 |
| chat.id | chatId | 与内容关联的聊天的 Microsoft Teams ID。 |
| app.locale | 区域设置 | 用户为格式化为 languageId-countryId 的应用配置的当前区域设置 (例如，en-us) 。 |
| page.id | entityId | 此内容指向的页面的开发人员定义的唯一 ID。 |
| page.subPageId | subEntityId | 此内容指向的子页的开发人员定义的唯一 ID。 此字段应用于还原到页面中的特定状态，例如滚动到特定内容或激活特定内容。 |
| user.loginHint | loginHint | 适用于在使用 Azure AD 进行身份验证时用作login_hint的值。 由于恶意方可以在浏览器中运行内容，因此，此值仅应用作用户身份的提示，而绝不应用作标识证明。 仅当在清单中请求标识权限时，此字段才可用。 |
| user.userPrincipalName | Upn | 当前用户的 UPN。 这可能是外部身份验证的 UPN (例如来宾用户) 。 由于恶意方在浏览器中运行内容，因此此值仅应用作用户身份的提示，而绝不应用作标识证明。 仅当在清单中请求标识权限时，此字段才可用。 |
| user.id | userObjectId | 当前用户的 Azure AD 对象 ID。 由于恶意方在浏览器中运行内容，因此此值仅应用作用户身份的提示，而绝不应用作标识证明。 仅当在清单中请求标识权限时，此字段才可用。 |
| user.tenant.id | tid | 当前用户的 Azure AD 租户 ID。 由于恶意方可以在浏览器中运行内容，因此，此值仅应用作用户身份的提示，而绝不应用作标识证明。 仅当在清单中请求标识权限时，此字段才可用。 |
| team.groupId | groupId | 与内容关联的团队的Office 365组 ID。 仅当在清单中请求标识权限时，此字段才可用。 |
| app.theme  | theme | 当前 UI 主题：默认、深色、对比度 |
| page.isFullScreen | isFullScreen | 指示页面是否处于全屏模式。 |
| team.type | teamType | 团队的类型。 |
| sharepointSite.teamSiteUrl | teamSiteUrl | 与团队关联的根 SharePoint 网站。 |
| sharepointSite.teamSiteDomain | teamSiteDomain | 与团队关联的根 SharePoint 网站的域。 |
| sharepointSite.teamSitePath | teamSitePath | 与团队关联的 SharePoint 网站的相对路径。 |
| channel.relativeUrl | channelRelativeUrl | 与通道关联的 SharePoint 文件夹的相对路径。 |
| app.host.sessionId | sessionId | 当前主机会话的唯一 ID，用于关联遥测数据。 |
| team.userRole | userTeamRole | 用户在团队中的角色。 由于恶意方可以在浏览器中运行你的内容，因此此值应仅用作用户角色的提示，而不应用作其角色的证明。 |
| team.isArchived | isTeamArchived | 指示是否存档团队。 应用应将此用作信号，以防止对与存档的团队关联的内容进行任何更改。 |
| app.host.clientType | hostClientType | 主机客户端的类型。 可能的值为：android、ios、Web、桌面、rigel |
| page.frameContext | frameContext | 页面 URL 加载 (内容、任务、设置、删除、sidePanel) 的上下文 |
| sharepoint | sharepoint | SharePoint 上下文。 仅当托管在 SharePoint 中时，此功能才可用。 |
| user.tenant.teamsSku | tenantSKU | 当前用户租户的许可证类型。 可能的值为 enterprise、free、edu、unknown |
| user.licenseType | userLicenseType | 当前用户的许可证类型。 可能的值为 E1、E3 和 E5 企业计划 |
| app.parentMessageId | parentMessageId | 从中启动此任务模块的父消息的 ID。 这仅在从机器人卡启动的任务模块中可用。 |
| app.host.ringId | ringId | 当前环 ID。 |
| app.sessionId | appSessionId | 当前主机会话的唯一 ID，用于关联遥测数据。 |
| user.isCallingAllowed | isCallingAllowed | 表示是否允许当前登录用户调用。 |
| user.isPSTNCallingAllowed | isPSTNCallingAllowed | 指示当前用户是否允许 PSTN 调用 |
| meeting.id | meetingId | 选项卡在会议上下文中运行时使用的会议 ID。 |
| channel.defaultOneNoteSectionId | defaultOneNoteSectionId | 链接到通道的 OneNote 节 ID。 |
| page.isMultiWindow | isMultiWindow | 指示选项卡是否在弹出窗口中。 |

有关详细信息，请参阅 [上下文接口和 *上下文* 接口](using-teams-client-sdk.md#updates-to-the-context-interface) API 参考汇报。[](/javascript/api/@microsoft/teams-js/app.context)

## <a name="retrieve-context-in-private-channels"></a>在专用通道中检索上下文

> [!NOTE]
> 专用频道目前仅在专用开发人员预览版中。

在专用通道中加载内容页面时，从 `getContext` 呼叫中收到的数据会混淆，以保护通道的隐私。

当内容页面位于专用频道中时，将更改以下字段：

* `team.groupId`：未定义专用频道
* `team.internalId`：设置为专用通道的 threadId
* `team.displayName`：设置为专用通道的名称
* `sharepointSite.url`：设置为专用频道的非重复唯一 SharePoint 网站的 URL
* `sharepointSite.path`：设置为专用频道的非重复唯一 SharePoint 网站的路径
* `sharepointSite.domain`：设置为专用通道的非重复唯一 SharePoint 网站域的域

如果页面使用这些值中的任何一个，则字段的 `channel.membershipType` 值必须 `Private` 是确定页面是否加载在专用通道中，并且可以相应地响应。

> [!NOTE]
>`teamSiteUrl` 也适用于标准通道。 如果页面使用这些值中的任何一个，则字段的 `channelType` 值必须 `Shared` 确定页面是否已加载到共享通道中，并且可以做出适当的响应。

## <a name="get-context-in-shared-channels"></a>获取共享通道中的上下文

在共享通道中加载内容 UX 时，使用从 `getContext` 调用收到的数据进行共享通道更改。 如果 Tab 使用以下任一值，则必须填充字 `channelType` 段以确定是否在共享通道中加载该选项卡，并做出适当的响应。
对于共享频道， `groupId` 其值是 `null`，因为主机团队的 groupId 无法准确反映共享频道的真实成员身份。 若要解决此问题，新添加了`hostTeamGroupID`这些属性和`hostTenantID`属性，对于进行 Microsoft 图形 API 调用以检索成员身份非常有用。 `hostTeam` 引用创建共享通道的团队。 `currentTeam` 引用当前用户正在从中访问共享通道的团队。

有关这些概念的详细信息，请参阅 [共享频道](~/concepts/build-and-test/shared-channels.md)。

在共享通道中使用以下 `getContext` 属性：

| 属性 | 说明 |
|----------|--------------|
|`channelId`| 该属性设置为共享通道线程 ID。|
|`channelType`| 该属性设置 `sharedChannel` 为共享通道。|
|`groupId`|该属性 `null` 适用于共享通道。|
|`hostTenantId`| 该属性是新添加的，并描述了主机的租户 ID，可用于与当前用户的 `tid` 租户 ID 属性进行比较。 |
|`hostTeamGroupId`| 该属性是新添加的，并描述了主机团队的 Azure AD 组 ID，可用于进行 Microsoft 图形 API 调用以检索共享频道成员身份。 |
|`teamId`|该属性是新添加的，并设置为当前共享团队的线程 ID。 |
|`teamName`|该属性设置为当前共享团队的 `teamName`属性。 |
|`teamType`|该属性设置为当前共享团队的 `teamType`属性。|
|`teamSiteUrl`|该属性描述共享通道的 `channelSiteUrl`。|
|`teamSitePath`| 该属性描述共享通道的 `channelSitePath`。|
|`teamSiteDomain`| 该属性描述共享通道的 `channelSiteDomain`。|
|`tenantSKU`| 该属性描述主机团队的 `tenantSKU`属性。|
|`tid`|  该属性描述当前用户的租户 ID。|
|`userObjectId`|  该属性描述当前用户的 ID。|
|`userPrincipalName`| 该属性描述当前用户的 UPN。|

有关共享通道的详细信息，请参阅 [共享频道](~/concepts/build-and-test/shared-channels.md)。

## <a name="handle-theme-change"></a>处理主题更改

如果主题通过调用 `microsoftTeams.app.registerOnThemeChangeHandler(function(theme) { /* ... */ })`更改，可以注册要通知的应用。

函`theme`数中的参数是值为`default``dark``contrast`或 . 的字符串。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [具有自适应卡片的生成选项卡](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="see-also"></a>另请参阅

* [选项卡设计指南](../../tabs/design/tabs.md)
* [Teams 选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [在选项卡中使用任务模块](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
