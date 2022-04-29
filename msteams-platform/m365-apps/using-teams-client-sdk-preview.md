---
title: Microsoft Teams JavaScript 客户端 SDK v2 预览版
description: 了解 Microsoft Teams JavaScript 客户端 SDK v2 预览版带来的变化
ms.date: 11/15/2021
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 91f012821efacd0f0ff6032703d0520d5bd469e0
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111694"
---
# <a name="microsoft-teams-javascript-client-sdk-v2-preview"></a>Microsoft Teams JavaScript 客户端 SDK v2 预览版

借助 [Microsoft Teams JavaScript 客户端 SDK v2 预览版](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true)，现有 Teams SDK（`@microsoft/teams-js` 或简称为 `TeamsJS`）已经过重构，使 Teams 开发人员能够[扩展 Teams 应用以在 Outlook 和 Office 中运行](overview.md)。 从功能角度来看，TeamsJS SDK v2 预览版 (`@microsoft/teams-js@next`) 是当前 TeamsJS SDK 的超集，它支持现有 Teams 应用功能，同时增加了在 Outlook 和 Office 中托管 Teams 应用的能力。

TeamsJS SDK v2 预览版中有两个重大更改，代码需要考虑这些更改才能在其他 Microsoft 365 应用程序中运行：

* [**回调函数现在返回 Promise 对象。**](#callbacks-converted-to-promises) 所有具有回调参数的现有函数都已现代化，可返回 JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对象，以便改进异步操作的处理和代码可读性。

* [**API 现在已组织成 *功能*。**](#apis-organized-into-capabilities) 可以将功能视为提供类似功能的 API 的逻辑分组，例如 `authentication`、`calendar`、`mail`、`monetization`、`meeting` 和 `sharing`。

 可以使用适用于 Microsoft Visual Studio Code 的 [Teams 工具包扩展](https://aka.ms/teams-toolkit)来简化 Teams 应用的更新过程，如以下部分所述。

> [!NOTE]
> 使现有 Teams 应用在 Outlook 和 Office 中运行需要以下两者：
>
> 1. `@microsoft/teams-js@2.0.0-beta.1` 或更高版本的依赖项，以及
> 2. 根据本文档中所述的所需更改修改现有应用程序代码。
>
> 如果从现有 Teams 应用引用 `@microsoft/teams-js@2.0.0-beta.1`（或更高版本），并且代码调用已更改的 API，则将看到弃用警告。 提供了 API 转换层（将当前 SDK 映射到预览 SDK API 调用），使现有 Teams 应用能够继续在 Teams 中工作，直到它们能够更新代码以使用 TeamsJS SDK v2 预览版。 使用本文中所述的更改更新代码后，个人选项卡也将在 Outlook 和 Office 中运行。

## <a name="updating-to-the-teams-client-sdk-v2-preview"></a>更新到 Teams 客户端 SDK v2 预览版

更新 Teams 应用以使用 TeamsJS SDK v2 预览版的最简单方法是使用适用于 Visual Studio Code 的 [Teams 工具包扩展](https://aka.ms/teams-toolkit)。 本部分将指导你完成执行此操作的步骤。 如果希望手动更新代码，请参阅[转换为 promise 的回调](#callbacks-converted-to-promises)和[组织为功能的 API](#apis-organized-into-capabilities) 部分，以获取有关所需 API 更改的更多详细信息。

### <a name="1-install-the-latest-teams-toolkit-visual-studio-code-extension"></a>1. 安装最新的 Teams 工具包 Visual Studio Code 扩展

在 *Visual Studio Code 扩展商城* 中，搜索“**Teams 工具包**”并安装版本 `2.10.0` 或更高版本。 该工具包提供两个命令来协助此过程：

1. 用于更新清单架构的命令
1. 用于更新 SDK 引用和调用站点的命令

以下是在其他 Microsoft 365 应用程序中运行 Teams 个人选项卡应用所需的两个关键更新：

### <a name="2-updating-the-manifest"></a>2. 更新清单

# <a name="teams-toolkit"></a>[Teams 工具包](#tab/manifest-teams-toolkit)

1. 打开 *命令面板*：`Ctrl+Shift+P`
1. 运行“**Teams：升级 Teams 清单以支持 Outlook 和 Office 应用**”命令并选择应用清单文件。 将进行更改。

# <a name="manual-steps"></a>[手动步骤](#tab/manifest-manual)

打开 Teams 应用清单，使用以下值更新 `$schema` 和 `manifestVersion`：

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

如果使用 Teams 工具包创建了个人应用，则还可以使用它来验证清单文件的更改并识别任何错误。 打开命令面板 `Ctrl+Shift+P` 并找到“**Teams：验证清单文件**”，或者从 Teams 工具包的“部署”菜单中选择选项（查找 Visual Studio Code 左侧的 Teams 图标）。

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams 工具包“部署”菜单下的“验证清单文件”选项":::

### <a name="2-update-sdk-references"></a>2. 更新 SDK 引用

若要在 Outlook 和 Office 中运行，应用将需要依赖于 [npm 包](https://www.npmjs.com/package/@microsoft/teams-js/v/2.0.0-beta.1) `@microsoft/teams-js@2.0.0-beta.1`（或更高版本 *beta* 版本）。 若要手动执行这些步骤以及有关 API 更改的详细信息，请参阅以下部分[转换为 promise 的回调](#callbacks-converted-to-promises)和[组织为功能的 API](#apis-organized-into-capabilities)。

1. 确保拥有 [Teams 工具包](https://aka.ms/teams-toolkit) `v2.10.0` 或更高版本
1. 打开 *命令面板*：`Ctrl+Shift+P`
1. 运行命令 `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

完成后，该实用工具将使用 TeamsJS SDK v2 预览版（`@microsoft/teams-js@2.0.0-beta.1` 或更高版本）依赖项更新 `package.json` 文件，`*.js/.ts` 和 `*.jsx/.tsx` 文件将更新为：

> [!div class="checklist"]
>
> * `package.json` 对 TeamsJS SDK v2 预览版的引用
> * TeamsJS SDK v2 预览版的导入语句
> * 对 TeamsJS SDK v2 预览版的[函数、枚举和接口调用](#apis-organized-into-capabilities)
> * `TODO` 注释提醒，查看可能受 [Context](#updates-to-the-context-interface) 接口更改影响的区域
> * `TODO` 注释提醒，确保[从回调样式函数转换为 promise 函数](#callbacks-converted-to-promises)在该工具找到的每个调用站点上运行良好

> [!IMPORTANT]
> 升级工具不支持 html 文件中的代码，需要手动更改。

## <a name="callbacks-converted-to-promises"></a>转换为 promise 的回调

以前使用回调参数的 Teams API 已更新为返回 JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对象。 其中包括以下 API：

```js
app.getContext, app.initialize, appInstallDialog.openAppInstallDialog, authentication.authenticate, authentication.getAuthToken, authentication.getUser, authentication.registerAuthenticationHandlers was removed to support using Promises, calendar.openCalendarItem, calendar.composeMeeting, call.startCall, core.executeDeepLink, location.getLocation, location.showLocation, mail.openMailItem, mail.composeMail, media.captureImage, media.getMedia, media.selectMedia, media.viewImages, media.scanBarCode, meeting.getAppContentStageSharingCapabilities, meeting.getAuthenticationTokenForAnonymousUser, meeting.getIncomingClientAudioState, meeting.getLiveStreamState, meeting.getMeetingDetails, meeting.requestStartLiveStreaming, meeting.requestStopLiveStreaming, meeting.shareAppContentToStage, meeting.stopSharingAppContentToStage, meeting.toggleIncomingClientAudio, meeting.getAppContentStageSharingState, pages.backStack.navigateBack, pages.navigateCrossDomain, pages.navigateToTab, pages.tabs.getMruTabInstances, pages.tabs.getTabInstances, pages.config.setConfig, pages.config.getConfig, people.selectPeople, ChildAppWindow.postMessage, ParentAppWindow.postMessage
```

需要更新代码调用这些 API 的方式才能使用 Promise。 例如，如果代码正调用 Teams API，如下所示：

# <a name="javascript"></a>[JavaScript](#tab/javascript)

此代码：

```js
import microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context) => { /* ... */ });
```

需要更新为：

```js
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context) => {
    /*...*/
});
```

...或等效 `async/await` 模式：

```js
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context = await app.getContext();
  /*...*/
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

此代码：

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context: microsoftTeams.Context) => {
  /* ... */
});
```

需要更新为：

```TypeScript
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context: Context) => {
    /*...*/
});
```

...或等效 `async/await` 模式：

```TypeScript
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context: Context = await app.getContext();
  /*...*/
}
```

---

> [!TIP]
> 使用 [Teams 工具包](#updating-to-the-teams-client-sdk-v2-preview)更新 TeamsJS SDK v2 预览版的代码时，会在客户端代码中使用 `TODO` 注释标记所需的更新。

## <a name="apis-organized-into-capabilities"></a>组织为功能的 API

*功能* 是提供类似功能的 API 的逻辑分组。 你可以将 Microsoft Teams、Outlook 和 Office 视为主机。 如果主机支持该功能中定义的所有 API，则它支持给定功能。 主机无法部分实现功能。  功能可以基于特性或内容，例如 *dialog* 或 *authentication*。 还有一些应用程序类型的功能，例如 *选项卡/页面* 或 *机器人* 以及其他分组。

在 TeamsJS SDK v2 预览版中，API 定义为 JavaScript 命名空间中名称与其所需功能匹配的函数。 如果应用在支持 dialog 功能的主机中运行，则应用可以安全地调用 API，例如 `dialog.open`（以及命名空间中定义的其他 dialog 相关 API）。 同时，如果应用尝试调用该主机中不支持的 API，则 API 将引发异常。

### <a name="differentiate-your-app-experience"></a>区分应用体验

可以通过对给定功能（命名空间）调用 `isSupported()` 函数，在运行时检查主机是否支持该功能。 如果支持，则返回 `true`；如果不支持，则返回 `false`，并且可以根据需要调整应用行为。 这样，应用便能在支持它的主机中亮起 UI 和功能，同时继续为不支持的主机运行。

运行应用之主机的名称作为 Context 接口 (`app.Context.app.host.name`) 上的 *hostName* 属性公开，可在运行时通过调用 `getContext` 进行查询。 它也可用作 `{hostName}` [URL 占位符值](../tabs/how-to/access-teams-context.md#get-context-by-inserting-url-placeholder-values)。 最佳做法是谨慎使用 *hostName* 机制：

* **请勿** 根据 *hostName* 属性值假设某个功能在主机中可用或不可用。 相反，请检查功能支持 (`isSupported`)。
* **请勿** 使用 *hostName* 控制 API 调用。 相反，请检查功能支持 (`isSupported`)。
* **请** 使用 *hostName* 根据运行主机来区分其主题。 例如，在 Teams 中运行时，可以使用 Microsoft Teams 紫色作为主要主题色；在 Outlook 中运行时，可以使用 Outlook 蓝色。
* **请** 使用 *hostName* 根据运行主机来区分向用户显示的消息。 例如，例如，在 Office 网页版中运行时显示“*在 Office 中管理任务*”，在 Microsoft Teams 中运行时显示“*在 Teams 中管理任务*”。

### <a name="namespaces"></a>命名空间

TeamsJS SDK v2 预览版通过命名空间将 API 组织为 *功能*。 一些特别重要的新命名空间包括 *app*、*pages*、*dialog* 和 *teamsCore*。

#### <a name="app-namespace"></a>*app* 命名空间

`app` 命名空间包含跨 Microsoft Teams、Office 和 Outlook 的整体应用使用所需的顶级 API。 来自其他各种 TeamsJS 命名空间的所有 API 已移至 TeamsJS SDK v2 预览版中的 `app` 命名空间：

| 原始命名空间 `global (window)` | 新命名空间 `app` |
| - | - |
| `initialize` | `app.initialize` |
| `getContext` | `app.getContext` |
| `registerOnThemeChangeHandler` | `app.registerOnThemeChangeHandler` |

| 原始命名空间 `appInitialization` | 新命名空间 `app` |
| - | - |
| `appInitialization.notifyAppLoaded` | `app.notifyAppLoaded` |
| `appInitialization.notifySuccess` | `app.notifySuccess` |
| `appInitialization.notifyFailure` | `app.notifyFailure` |
| `appInitialization.notifyExpectedFailure` | `app.notifyExpectedFailure` |
| `appInitialization.FailedReason` 枚举 | `app.FailedReason` |
| `appInitialization.ExpectedFailureReason` 枚举 | `app.ExpectedFailureReason` |
| `appInitialization.IFailedRequest` 枚举 | `app.IFailedRequest` |
| `appInitialization.IExpectedFailureRequest` 枚举 | `app.IExpectedFailureRequest` |

#### <a name="core-namespace"></a>*core* 命名空间

`core` 命名空间包括深层链接的功能。

| 原始命名空间 `publicAPIs` | 新命名空间 `core` |
| - | - |
| `shareDeepLink` | `core.shareDeepLink` |
| `executeDeepLink` | `core.executeDeepLink` |

#### <a name="pages-namespace"></a>*pages* 命名空间

`pages` 命名空间包括用于在各种 Microsoft 365 客户端（包括 Teams、Office 和 Outlook）中运行和导航网页的功能。 它还包括几个子功能，作为子命名空间实现。

| 原始命名空间 `global (window)` | 新命名空间 `pages` |
| - | - |
| `setFrameContext` | `pages.setCurrentFrame`（已重命名） |
| `initializeWithFrameContext` | `pages.initializeWithFrameContext` |
| `registerFullScreenHandler` | `pages.registerFullScreenHandler` |
| `navigateCrossDomain` | `pages.navigateCrossDomain` |
| `returnFocus` | `pages.returnFocus` |

##### <a name="pagestabs"></a>*pages.tabs*

| 原始命名空间 `global (window)` | 新命名空间 `pages.tabs` |
| - | - |
| `getTabInstances` |  `pages.tabs.getTabInstances` |
| `getMruTabInstances` | `pages.tabs.getMruTabInstances` |
| `navigateToTab` | `pages.tabs.navigateToTab` |

| 原始命名空间 `navigation` | 新命名空间 `pages.tabs` |
| - | - |
| `navigation.navigateToTab` | `pages.tabs.navigateToTab` |

##### <a name="pagesconfig"></a>*pages.config*

| 原始命名空间 `settings` | 新命名空间 `pages.config`  |
| - | - |
| `settings.setSettings` | `pages.config.setConfig`（已重命名）
| `settings.getSettings` | `pages.config.getConfig`（已重命名）
| `settings.setValidityState`| `pages.config.setValidityState`
| `settings.initialize` | `pages.config.initialize`
| `settings.registerOnSaveHandler`| `pages.config.registerOnSaveHandler`
| `settings.registerOnRemoveHandler` | `pages.config.registerOnRemoveHandler`
| `settings.Settings` 接口 | `pages.config.Config`（已重命名）
| `settings.SaveEvent` 接口 | `pages.config.SaveEvent`（已重命名）
| `settings.RemoveEvent` 接口 | `pages.config.RemoveEvent`（已重命名）
| `settings.SaveParameters` 接口 | `pages.config.SaveParameters`（已重命名）
| `settings.SaveEventImpl` 接口 | `pages.config.SaveEventImpl`（已重命名）

| 原始命名空间 `global (window)` | 新命名空间 `pages.config` |
| - | - |
| `registerEnterSettingsHandler` | `pages.config.registerChangeConfigHandler`（已重命名）

##### <a name="pagesbackstack"></a>*pages.backStack*

| 原始命名空间 `navigation` | 新命名空间 `pages.backStack`  |
| - | - |
| `navigation.navigateBack` | `pages.backStack.navigateBack`

| 原始命名空间 `global (window)` | 新命名空间 `pages.backStack`  |
| - | - |
| `registerBackButtonHandler` | `pages.backStack.registerBackButtonHandler`

##### <a name="pagesappbutton"></a>*pages.appButton*

| 原始命名空间 `global (window)` | 新命名空间 `pages.appButton`  |
| - | - |
| `registerAppButtonClickHandler` | `pages.appButton.onClick`（已重命名）
| `registerAppButtonHoverEnterHandler` | `pages.appButton.onHoverEnter`（已重命名）
| `registerAppButtonHoverLeaveEnter` | `pages.appButton.onHoverLeave`（已重命名）
| `FrameContext` 接口 | `pages.appButton.FrameInfo`（已重命名） |

#### <a name="dialog-namespace"></a>*dialog* 命名空间

TeamsJS *tasks* 命名空间已重命名为 *dialog*，并且已重命名以下 API：

| 原始命名空间 `tasks` | 新命名空间 `dialog`  |
| - | - |
| `tasks.startTask` | `dialog.open`（已重命名） |
| `tasks.submitTasks` | `dialog.submit`（已重命名） |
| `tasks.updateTasks` | `dialog.resize`（已重命名） |
| `tasks.TaskModuleDimension` 枚举 | `dialog.DialogDimension`（已重命名） |
| `tasks.TaskInfo` 接口 | `dialog.DialogInfo`（已重命名） |

#### <a name="teamscore-namespace"></a>*teamsCore* 命名空间

若要将 TeamsJS SDK 通用化以运行其他 Microsoft 365 主机（如 Office 和 Outlook），Teams 特定的功能（最初在 *global* 命名空间中）已移动到 *teamsCore* 命名空间：

| 原始命名空间 `global (window)` | 新命名空间 `teamsCore`  |
| - | - |
| `enablePrintCapability` | `teamsCore.enablePrintCapability`
| `print` | `teamsCore.print`
| `registerOnLoadHandler` | `teamsCore.registerOnLoadHandler`
| `registerBeforeUnloadHandler` | `teamsCore.registerBeforeUnloadHandler`
| `registerFocusEnterHandler` | `teamsCore.registerFocusEnterHandler`

### <a name="updates-to-the-context-interface"></a>*Context* 接口更新

`Context` 接口已移动到 `app` 命名空间并更新为对类似属性进行分组，以便在 Outlook 和 Office 以及 Teams 中运行时获得更好的可扩展性。

添加了一个新属性 `app.Context.app.host.name`，使个人选项卡能够根据主机应用程序区分用户体验。

还可以查看 TeamsJS SDK v2 预览版源中的 [`transformLegacyContextToAppContext`](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/packages/teams-js/src/public/app.ts) 函数来可视化更改。

| 接口中的 `Context` 原始名称 | `app.Context` 中的新位置 |
| - | - |
| `appIconPosition` | `app.Context.app.iconPositionVertical` |
| `appLaunchId`| *不在 Teams 客户端 SDK v2 预览版中* |
| `appSessionId` | `app.Context.app.sessionId`|
| `channelId`| `app.Context.channel.id` |
| `channelName`| `app.Context.channel.displayName`|
| `channelRelativeUrl` | `app.Context.channel.relativeUrl`|
| `channelType`| `app.Context.channel.membershipType` |
| `chatId` | `app.Context.chat.id`|
| `defaultOneNoteSectionId`| `app.Context.channel.defaultOneNoteSectionId`|
| `entityId` | `app.Context.page.id`|
| `frameContext` | `app.Context.page.frameContext`|
| `groupId`| `app.Context.team.groupId` |
| `hostClientType` | `app.Context.app.host.clientType`|
| `hostTeamGroupId`| `app.Context.channel.ownerGroupId` |
| `hostTeamTenantId` | `app.Context.channel.ownerTenantId`|
| `isCallingAllowed` | `app.Context.user.isCallingAllowed`|
| `isFullScreen` | `app.Context.page.isFullScreen`|
| `isMultiWindow`| `app.Context.page.isMultiWindow` |
| `isPSTNCallingAllowed` | `app.Context.user.isPSTNCallingAllowed`|
| `isTeamArchived` | `app.Context.team.isArchived`|
| `locale` | `app.Context.app.locale` |
| `loginHint`| `app.Context.user.loginHint` |
| `meetingId`| `app.Context.meeting.id` |
| `osLocaleInfo` | `app.Context.app.osLocaleInfo` |
| `parentMessageId`| `app.Context.app.parentMessageId`|
| `ringId` | `app.Context.app.host.ringId`|
| `sessionId`| `app.Context.app.host.sessionId` |
| `sourceOrigin` | `app.Context.page.sourceOrigin`|
| `subEntityId`| `app.Context.page.subPageId` |
| `teamId` | `app.Context.team.internalId`|
| `teamSiteDomain` | `app.Context.sharepointSite.domain`|
| `teamSitePath` | `app.Context.sharepointSite.path`|
| `teamSiteUrl`| `app.Context.sharepointSite.url` |
| `teamTemplateId` | `app.Context.team.templateId`|
| `teamType` | `app.Context.team.type`|
| `tenantSKU`| `app.Context.user.tenant.teamsSku` |
| `tid`| `app.Context.user.tenant.id` |
| `upn` | `app.Context.user.userPrincipalName` |
|`userClickTime`| `app.Context.app.userClickTime`|
| `userFileOpenPreference` | `app.Context.app.userFileOpenPreference` |
| `userLicenseType`| `app.Context.user.licenseType` |
| `userObjectId` | `app.Context.user.id`|
| `userTeamRole` | `app.Context.team.userRole`|
| `userDisplayName` | `app.Context.user.displayName` |
| 不适用 | `app.Context.app.host.name`|

## <a name="next-steps"></a>后续步骤

还可以在 [TeamsJS SDK v2 预览版更改日志](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/packages/teams-js/CHANGELOG.md) 和 [TeamsJS SDK v2 预览版 API 参考](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true)中了解有关重大更改的详细信息。

当准备好测试在 Outlook 和 Office 中运行的 Teams 应用时，请参阅：

> [!div class="nextstepaction"]
> [跨 Microsoft 365 扩展 Teams 应用](overview.md)
