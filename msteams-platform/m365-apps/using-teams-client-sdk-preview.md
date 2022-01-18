---
title: Microsoft Teams JavaScript 客户端 SDK v2 预览版
description: 了解 JavaScript 客户端 SDK v2 预览版Microsoft Teams更改
ms.date: 11/15/2021
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 7a8b5ed919cac07b1d0710a1f23c0ade0cca2ffb
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059819"
---
# <a name="microsoft-teams-javascript-client-sdk-v2-preview"></a>Microsoft Teams JavaScript 客户端 SDK v2 预览版

借助[Microsoft Teams JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true)客户端 SDK v2 预览版，已重构现有的 Teams SDK (或简单的 `@microsoft/teams-js`) ，以使 Teams 开发人员能够扩展 Teams 应用以在 Outlook 和 Office 中 `TeamsJS` [运行](overview.md)。 从功能角度来看，TeamsJS SDK v2 Preview () 是当前 TeamsJS SDK 的超集，它支持现有 Teams 应用功能，同时添加在 Outlook 和 Office 中托管 Teams 应用 `@microsoft/teams-js@next` 的功能。

TeamsJS SDK v2 预览版有两项重大更改，代码将需要考虑这些更改才能在其他 Microsoft 365应用程序中运行：

* [**回调函数现在返回 Promise 对象。**](#callbacks-converted-to-promises) 具有 callback 参数的所有现有函数都进行了现代化，以返回 JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对象，以改进异步操作处理和代码可读性。

 - [**API 现已组织到 *功能 中*。**](#apis-organized-into-capabilities) 你可以将功能视为提供类似功能的 API 的逻辑分组，如 、 `authentication` `calendar` 和 `mail` `monetization` `meeting` `sharing` 。

 可以使用 Teams Toolkit[扩展](https://aka.ms/teams-toolkit)Visual Studio Code简化 Teams 应用的更新过程，如下一节中所述。

> [!NOTE]
> 启用现有 Teams 应用在 Outlook 和 Office需要：
> 1. 依赖 或 `@microsoft/teams-js@2.0.0-beta.1` 更高版本，
> 2. 根据本文档中所述的所需更改修改现有应用程序代码。
>
>  如果你引用 (现有) 应用的 Teams 或更高版本，则如果你的代码调用已更改的 API，你将看到弃用 `@microsoft/teams-js@2.0.0-beta.1` 警告。 提供了 API 转换层 (映射当前 SDK 以预览 SDK API 调用) ，以使现有 Teams 应用在 Teams 中继续工作，直到它们能够更新代码以使用 TeamsJS SDK v2 预览版。 使用本文中概述的更改更新代码后，你的个人选项卡也将在 Outlook 中Office。

## <a name="updating-to-the-teams-client-sdk-v2-preview"></a>更新到 Teams 客户端 SDK v2 预览版

将你的 Teams 应用更新为使用 TeamsJS SDK v2 Preview 的最简单方法是使用 Teams Toolkit[扩展](https://aka.ms/teams-toolkit)Visual Studio Code。 本部分将介绍执行这些步骤的步骤。 如果你想要手动更新代码，请参阅转换为承诺的回调和组织[](#callbacks-converted-to-promises)为功能的[API](#apis-organized-into-capabilities)部分，了解有关所需 API 更改的更多详细信息。

### <a name="1-install-the-latest-teams-toolkit-vs-code-extension"></a>1. 安装最新的 Teams Toolkit VS Code 扩展

在 *Visual Studio Code Extensions Marketplace* 中，搜索 **Teams Toolkit安装版本** `2.10.0` 或更高版本。 工具包提供了两个命令来帮助此过程：

1. 更新清单架构的命令
1. 用于更新 SDK 引用和调用网站的命令

下面是在其他应用程序中运行个人选项卡应用Teams两个关键Microsoft 365：""

### <a name="2-updating-the-manifest"></a>2. 更新清单

# <a name="teams-toolkit"></a>[Teams Toolkit](#tab/manifest-teams-toolkit)

1. 打开命令 *调色板*： `Ctrl+Shift+P`
1. 运行 **Teams：Teams清单以支持** Outlook 和 Office 应用命令并选择应用清单文件。 将就地进行更改。

# <a name="manual-steps"></a>[手动步骤](#tab/manifest-manual)

打开Teams应用清单，然后使用 `$schema` `manifestVersion` 下列值更新 和 ：

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```
---

如果你使用Teams Toolkit创建个人应用，则还可以使用它来验证对清单文件所做的更改并识别任何错误。 打开命令调色板并找到"Teams：验证清单文件"，或者从 Teams Toolkit (的"部署"菜单中选择选项，查找 Teams 图标位于 Visual Studio Code) 左侧 `Ctrl+Shift+P` 。 

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Toolkit&quot;部署&quot;菜单下的&quot;验证清单文件&quot;选项":::

### <a name="2-update-sdk-references"></a>2. 更新 SDK 引用

若要在 Outlook 和 Office 中运行，你的应用将需要依赖[npm](https://www.npmjs.com/package/@microsoft/teams-js/v/2.0.0-beta.1)程序包 (或更高版本的 `@microsoft/teams-js@2.0.0-beta.1`) 。  若要手动执行这些步骤，以及 API 更改详细信息，请参阅以下有关转换为承诺的回调和组织[](#callbacks-converted-to-promises)为功能的[API 的部分](#apis-organized-into-capabilities)。

1. 确保[已Teams Toolkit](https://aka.ms/teams-toolkit) `v2.10.0` 或更高版本
1. 打开命令 *调色板*： `Ctrl+Shift+P`
1. 运行命令 `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

完成后，该实用工具会使用 TeamsJS SDK v2 Preview (或更高版本的) 依赖项更新你的文件，并且你的 和 `package.json` `@microsoft/teams-js@2.0.0-beta.1` `*.js/.ts` `*.jsx/.tsx` 文件将更新为：

> [!div class="checklist"]
> * `package.json` 对 TeamsJS SDK v2 Preview 的引用
> * TeamsJS SDK v2 Preview 的导入语句
> * [对](#apis-organized-into-capabilities) TeamsJS SDK v2 Preview 的函数、枚举和接口调用
> * `TODO` 注释提醒，用于查看可能受 [上下文接口更改](#updates-to-the-context-interface) 影响的区域
> * `TODO` 注释提醒以确保 [从回调](#callbacks-converted-to-promises) 样式函数转换到承诺函数在工具找到的所有调用网站中都运行良好

> [!IMPORTANT]
> html 文件内的代码不受升级工具支持，需要手动更改。

## <a name="callbacks-converted-to-promises"></a>转换为承诺的回调

Teams接收回调参数的 API 已更新为返回 JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)对象。 其中包括以下 API：

```js
app.getContext, app.initialize, appInstallDialog.openAppInstallDialog, authentication.authenticate, authentication.getAuthToken, authentication.getUser, authentication.registerAuthenticationHandlers was removed to support using Promises, calendar.openCalendarItem, calendar.composeMeeting, call.startCall, core.executeDeepLink, location.getLocation, location.showLocation, mail.openMailItem, mail.composeMail, media.captureImage, media.getMedia, media.selectMedia, media.viewImages, media.scanBarCode, meeting.getAppContentStageSharingCapabilities, meeting.getAuthenticationTokenForAnonymousUser, meeting.getIncomingClientAudioState, meeting.getLiveStreamState, meeting.getMeetingDetails, meeting.requestStartLiveStreaming, meeting.requestStopLiveStreaming, meeting.shareAppContentToStage, meeting.stopSharingAppContentToStage, meeting.toggleIncomingClientAudio, meeting.getAppContentStageSharingState, pages.backStack.navigateBack, pages.navigateCrossDomain, pages.navigateToTab, pages.tabs.getMruTabInstances, pages.tabs.getTabInstances, pages.config.setConfig, pages.config.getConfig, people.selectPeople, ChildAppWindow.postMessage, ParentAppWindow.postMessage
```

你需要更新代码调用其中任何 API 以使用 Promises 的方式。 例如，如果你的代码调用 Teams API，如下所示：

# <a name="javascript"></a>[JavaScript](#tab/javascript)

此代码：

```js
import microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context) => { /* ... */ });
```

需要更新为：

```js
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context: Context) => {
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
> 使用 Teams Toolkit 更新 TeamsJS SDK v2[](#updating-to-the-teams-client-sdk-v2-preview)预览版的代码时，会用客户端代码中的注释标记 `TODO` 所需的更新。

## <a name="apis-organized-into-capabilities"></a>组织到功能的 API

*功能* 是提供类似功能的 API 的逻辑分组。 你可以将 Microsoft Teams、Outlook 和 Office 视为主机。 主机支持给定功能（如果它支持该功能中定义的所有 API）。 主机无法部分实现功能。  功能可以是基于功能或内容的，例如 *对话框或**身份验证*。 还有一些应用程序类型（如选项卡 */**页面或机器人*）的功能以及其他分组。

在 TeamsJS SDK v2 预览版中，API 定义为 JavaScript 命名空间中名称与所需功能匹配的函数。 如果应用在支持对话框功能的主机中运行，则应用可以安全地调用 API（如 (）以及命名空间命名空间中定义的其他与对话框相关的 `dialog.open` API) 。 同时，如果应用尝试调用该主机不支持的 API，API 将引发异常。

### <a name="differentiate-your-app-experience"></a>区分你的应用体验

你可以在运行时通过调用给定功能上的 函数来检查主机是否支持 (`isSupported()` 命名空间) 。 如果受 `true` 支持，它将返回，如果不支持， `false` 并且你可以根据需要调整应用行为。 这允许你的应用在支持它的主机中打开 UI 和功能，同时继续为不支持它的主机运行。

在 Context 接口 () 上，运行你的应用的主机名称作为 *hostName* 属性公开，可通过调用 在运行时 `app.Context.app.host.name` 查询 `getContext` 。 它还作为 URL 占位符 `{hostName}` [值 提供](../tabs/how-to/access-teams-context.md#get-context-by-inserting-url-placeholder-values)。 最佳做法是谨慎使用 *hostName* 机制：

* **请勿根据** *hostName* 属性值假定主机中的某些功能可用或不可用。 相反，检查功能支持 `isSupported` () 。
* **请勿使用** *hostName 对* API 调用进行网关调用。 相反，检查功能支持 `isSupported` () 。
* **使用** *hostName* 根据应用程序运行的主机来区分其主题。 例如，在 Microsoft Teams 中运行时，可以使用紫色作为主要主题色Teams，在Outlook中运行时Outlook蓝色Outlook。
* **使用** *hostName* 根据用户运行的主机来区分向用户显示的消息。 例如，显示"在 Office 中运行时在 Office web 版 中管理任务Teams在Microsoft Teams 中运行时。

### <a name="namespaces"></a>命名空间

TeamsJS SDK v2 Preview 通过命名空间将 API *组织到* 功能中。 一些特别重要的新命名空间是 *应用*、*页面**、对话框* 和 *teamsCore。*

#### <a name="app-namespace"></a>*应用* 命名空间

命名空间 `app` 包含整个应用使用情况所需的顶级 API，包括Microsoft Teams、Office和Outlook。 来自各种其他 TeamsJS 命名空间的所有 API 已移动到 `app` TeamsJS SDK v2 Preview 中的命名空间：

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

#### <a name="core-namespace"></a>*核心* 命名空间

命名空间 `core` 包括深层链接的功能。

| 原始命名空间 `publicAPIs` | 新命名空间 `core` |
| - | - |
| `shareDeepLink` | `core.shareDeepLink` |
| `executeDeepLink` | `core.executeDeepLink` |

#### <a name="pages-namespace"></a>*pages* 命名空间

命名空间包括用于在各种客户端（包括 Microsoft 365、Teams、Office 和 Outlook）中运行和导航 `pages` 网页Outlook。 它还包括多个子功能，作为子命名空间实现。

| 原始命名空间 `global (window)` | 新命名空间 `pages` |
| - | - |
| `setFrameContext` | `pages.setCurrentFrame` (重命名)  |
| `initializeWithFrameContext` | `pages.initializeWithFrameContext` |
| `registerFullScreenHandler` | `pages.registerFullScreenHandler` |
| `navigateCrossDomain` | `pages.navigateCrossDomain` |
| `returnFocus` | `pages.returnFocus` |

##### <a name="pagestabs"></a>*pages.tabs*

| 原始命名空间 `global (window)` | 新命名空间 `pages.tabs` |
| - | - |
| `getTabInstances` |  `pages.tabs.getTabInstances` |
| `getMruTabInstances` | `pages.tabs.getMruTabInstances` |
| ` navigateToTab` | `pages.tabs.navigateToTab` |

| 原始命名空间 `navigation` | 新命名空间 `pages.tabs` |
| - | - |
| `navigation.navigateToTab` | `pages.tabs.navigateToTab` |

##### <a name="pagesconfig"></a>*pages.config*

| 原始命名空间 `settings` | 新命名空间 `pages.config`  |
| - | - |
| `settings.setSettings` | `pages.config.setConfig` (重命名) 
| `settings.getSettings` | `pages.config.getConfig` (重命名) 
| `settings.setValidityState`| `pages.config.setValidityState`
| `settings.initialize` | `pages.config.initialize`
| `settings.registerOnSaveHandler`| `pages.config.registerOnSaveHandler`
| `settings.registerOnRemoveHandler` | `pages.config.registerOnRemoveHandler`
| `settings.Settings` interface | `pages.config.Config` (重命名) 
| `settings.SaveEvent` interface | `pages.config.SaveEvent` (重命名) 
| `settings.RemoveEvent` interface | `pages.config.RemoveEvent` (重命名) 
| `settings.SaveParameters` interface | `pages.config.SaveParameters` (重命名) 
| `settings.SaveEventImpl` interface | `pages.config.SaveEventImpl` (重命名) 

| 原始命名空间 `global (window)` | 新命名空间 `pages.config` |
| - | - |
| `registerEnterSettingsHandler` | `pages.config.registerChangeConfigHandler` (重命名) 

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
| `registerAppButtonClickHandler` | `pages.appButton.onClick` (重命名) 
| `registerAppButtonHoverEnterHandler` | `pages.appButton.onHoverEnter` (重命名) 
| `registerAppButtonHoverLeaveEnter` | `pages.appButton.onHoverLeave` (重命名) 
| `FrameContext` interface | `pages.appButton.FrameInfo` (重命名) )  |

#### <a name="dialog-namespace"></a>*对话框* 命名空间

TeamsJS *任务* 命名空间已重命名为 *对话框*，并且以下 API 已重命名：

| 原始命名空间 `tasks` | 新命名空间 `dialog`  |
| - | - |
| `tasks.startTask` | `dialog.open` (重命名)  |
| `tasks.submitTasks` | `dialog.submit` (重命名)  |
| `tasks.updateTasks` | `dialog.resize` (重命名)  |
| `tasks.TaskModuleDimension` 枚举 | `dialog.DialogDimension` (重命名)  |
| `tasks.TaskInfo` interface | `dialog.DialogInfo` (重命名)  |

#### <a name="teamscore-namespace"></a>*teamsCore* 命名空间

为了通用化 TeamsJS SDK 以运行其他 Microsoft 365 主机（如 Office 和 Outlook）Teams，最初在全局命名空间) 中特定于 (的功能已移动到 *teamsCore* 命名空间：

| 原始命名空间 `global (window)` | 新命名空间 `teamsCore`  |
| - | - |
| `enablePrintCapability` | `teamsCore.enablePrintCapability`
| `print` | `teamsCore.print`
| `registerOnLoadHandler` | `teamsCore.registerOnLoadHandler`
| `registerBeforeUnloadHandler` | `teamsCore.registerBeforeUnloadHandler`
| `registerFocusEnterHandler` | `teamsCore.registerFocusEnterHandler`

### <a name="updates-to-the-context-interface"></a>对 *Context 接口* 的更新

该接口已移动到命名空间并进行了更新，以对类似的属性进行分组，以提供更好的可伸缩性，因为它在 Outlook 和 Office 中运行 `Context` `app` ，Teams。

添加了一 `app.Context.app.host.name` 个新属性，使个人选项卡能够根据主机应用程序区分用户体验。

还可以查看 TeamsJS SDK v2 预览源中的 函数，  [`transformLegacyContextToAppContext`](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/packages/teams-js/src/public/app.ts) 直观呈现更改。

| 接口中的原始 `Context` 名称 | 中的新位置 `app.Context` |
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
|` userClickTime`| `app.Context.app.userClickTime`|
| `userFileOpenPreference` | `app.Context.app.userFileOpenPreference` |
| `userLicenseType`| `app.Context.user.licenseType` |
| `userObjectId` | `app.Context.user.id`|
| ` userTeamRole` | `app.Context.team.userRole`|
| `userDisplayName` | `app.Context.user.displayName` |
| 不适用 | `app.Context.app.host.name`|

## <a name="next-steps"></a>后续步骤

还可以了解有关 [TeamsJS SDK v2 Preview](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/CHANGELOG.md) 更改日志和 [TeamsJS SDK v2 预览 API](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true)参考中的更改的详细信息。

当你准备好测试在 Teams 和 Office 中运行的 Outlook 应用时，请参阅：

> [!div class="nextstepaction"]
> [跨Teams扩展你的Microsoft 365](overview.md)
