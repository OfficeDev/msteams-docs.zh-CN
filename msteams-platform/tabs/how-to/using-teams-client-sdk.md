---
title: 使用 Microsoft Teams JavaScript 客户端 SDK 生成选项卡和其他托管体验
author: heath-hamilton
ms.author: surbhigupta
description: Microsoft Teams JavaScript 客户端 SDK 概述，它可帮助你构建托管 <iframe> 在 Teams、Office 和 Outlook 中的应用体验。
ms.localizationpriority: high
keywords: teams 选项卡, 组频道, 可配置静态 SDK, JavaScript, 个人版 m365
ms.topic: conceptual
ms.openlocfilehash: 3b607056e2e3e10ff6817acdea4425573f99c170
ms.sourcegitcommit: 12510f34b00bfdd0b0e92d35c8dbe6ea1f6f0be2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2022
ms.locfileid: "66033041"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>使用 Microsoft Teams JavaScript 客户端 SDK 生成选项卡和其他托管体验

Microsoft Teams JavaScript 客户端 SDK 可帮助你在 Teams、Office 和 Outlook 中创建托管体验，其中应用内容托管在 [iframe](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) 中。 SDK 有助于开发具有以下 Teams 功能的应用：

* [选项卡](../../tabs/what-are-tabs.md)
* [对话（任务模块）](../../task-modules-and-cards/what-are-task-modules.md)

从版本 `2.0.0` 开始，除了 Microsoft Teams 之外，还重构了现有的 Teams 客户端 SDK（`@microsoft/teams-js` 或简称 `TeamsJS`），以使 [Teams 应用能够在 Outlook 和 Office 中运行](/microsoftteams/platform/m365-apps/overview)。 从功能角度来看，最新版本的 TeamsJS 支持所有现有的 (v.1.x.x) Teams 应用功能，同时添加在 Outlook 和 Office 中托管 Teams 应用的可选功能。

下面是各种应用方案的当前版本控制指南：

[!INCLUDE [pre-release-label](~/includes/teamjs-version-details.md)]

本文的其余部分将引导你了解 Teams JavaScript 客户端 SDK 的结构和最新更新。

### <a name="microsoft-365-support-running-teams-apps-in-office-and-outlook"></a>Microsoft 365 支持（在 Office 和 Outlook 中运行 Teams 应用）

TeamsJS v.2.0 为某些类型的 Teams 应用引入了在 Microsoft 365 生态系统中运行的能力。 目前，适用于 Teams 应用的其他 Microsoft 365 应用程序主机（包括 Office 和 Outlook）支持一部分可为 Teams 平台构建的应用程序类型和功能。 此支持将随时间推移而扩展。 有关 Teams 应用的主机支持摘要，请参阅[跨 Microsoft 365 扩展 Teams 应用](../../m365-apps/overview.md)。

下表列出了 Teams 选项卡和对话框（任务模块）功能（公共命名空间），以及对在其他 Microsoft 365 主机中运行的扩展支持。

> [!TIP]
> 可通过对给定功能（命名空间）调用 `isSupported()` 函数，来在运行时检查主机是否支持该功能。

|功能 | 主机支持 | 注释 |
|-----------|--------------|-------|
| 应用 | Teams、Outlook、Office | 表示应用初始化和生命周期的命名空间。 |
| appInitialization| | 已弃用。 替换为 `app` 命名空间。 |
| appInstallDialog | Teams||
| 身份验证 | Teams、Outlook、Office | |
| 日历 | Teams、Outlook ||
| 通话 | Teams||
| 聊天 |Teams||
| 对话框 | Teams、Outlook、Office | 表示对话的命名空间（以前称为“*任务模块*”。 请参阅有关[对话](#dialogs)的说明。 |
| 位置 |Teams| 请参阅有关[应用权限](#app-permissions)的说明。|
| mail | Outlook（仅限 Windows 桌面版）||
| 媒体 |Teams| 请参阅有关[应用权限](#app-permissions)的说明。|
| pages | Teams、Outlook、Office | 表示页面导航的命名空间。 请参阅有关[深层链接](#deep-linking)的说明。 |
| people |Teams||
| settings || 已弃用。 已被 `pages.config` 取代。|
| 共享 | Teams||
| tasks | | 已弃用。 已被 `dialog` 功能取代。 请参阅有关[对话](#dialogs)的说明。|
| teamsCore | Teams | 包含 Teams 特定功能的命名空间。|
| video | Teams||

#### <a name="app-permissions"></a>应用权限

在 Teams 外部运行的应用尚不支持要求用户授予 [设备权限](../../concepts/device-capabilities/device-capabilities-overview.md)的应用功能（例如 *位置*）。 在 Outlook 或 Office 中运行时，当前无法在“设置”或应用标头中检查应用权限。 如果在 Office 或 Outlook 中运行的 Teams 应用调用触发设备权限的 TeamsJS（或 HTML5）API，则该 API 将生成错误，并且无法显示要求用户同意的系统对话框。

当前的指导是修改代码以捕获故障：

* 在使用某项功能之前检查它的 [isSupported()](#differentiate-your-app-experience)。 `media`、`meeting` 和 `files` 尚不支持 *isSupported* 调用，并且尚不能在 Teams 之外使用。
* 在调用 TeamsJS 和 HTML5 API 时捕获和处理错误。

当 API 不受支持或生成错误时，请添加逻辑以正常失败或提供解决方法。 例如：

* 将用户定向到应用的网站。
* 指示用户使用 Teams 中的应用完成流。
* 通知用户功能尚不可用。

此外，最佳做法是确保应用清单仅指定它使用的设备权限。

#### <a name="deep-linking"></a>深层链接

在 TeamsJS 版本 2.0 之前，所有深层链接方案都是使用 `shareDeepLink`（生成 *指向* 应用特定部分的链接）和 `executeDeepLink`（*从* 应用或在应用 *内* 导航到深层链接）处理的。 TeamsJS v.2.0 引入了一个新的 API `navigateToApp`，用于以一致的方式跨应用主机（Office 和 Outlook 以及 Teams）导航到应用中的页面（和子页）。 下面是深层链接方案的更新指南：

##### <a name="deep-links-into-your-app"></a>应用内的深层链接

使用 `pages.shareDeepLink`（在 TeamsJS v.2.0 之前称为 *shareDeepLink*）生成并显示可复制链接供用户共享。 单击后，如果尚未为应用程序主机安装应用（在链接路径中指定），则系统会提示用户安装该应用。

##### <a name="navigation-within-your-app"></a>在应用内导航

使用新的 `pages.navigateToApp` API 在托管应用程序中的应用内导航。

此 API 等效于导航到深层链接（类似于现已弃用的 *executeDeepLink*），而无需应用构造 URL 或管理不同应用程序主机的不同深层链接格式。

##### <a name="deep-links-out-of-your-app"></a>应用外的深层链接

对于从应用到其当前主机的各个区域的深层链接，请使用 TeamsJS SDK 提供的强类型 API。 例如，使用“*日历*”功能从应用打开计划对话框或日历项目。

对于从应用到同一主机中运行的其他应用的深层链接，请使用 `pages.navigateToApp`。

对于任何其他外部深层链接方案，可以使用 `app.openLink`，它提供与现已弃用的（从 TeamsJS v.2.0 开始）*executeDeepLink* API 类似的功能。

#### <a name="dialogs"></a>对话框

从 TeamsJS 版本 2.0 开始，“[任务模块](../../task-modules-and-cards/what-are-task-modules.md)”的 Teams 平台概念已重命名为“*对话*”，以便更好地与 Microsoft 365 开发人员生态系统中的现有概念保持一致。 因此，`tasks` 命名空间已被弃用，取而代之于新的 `dialog` 命名空间。

此新的对话功能将拆分为主要功能 (`dialog`)（用于支持基于 HTML 的对话）以及子功能 `dialog.bot`（用于基于机器人的对话开发）。

对话功能尚不支持[自适应卡片对话](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)。 仍需使用 `tasks.startTask()` 调用基于自适应卡片的对话。

`dialog.open` 函数当前仅适用于打开基于 HTMl 的对话，并返回可用于将消息 (`ChildAppWindow.postMessage`) 传递到新打开的对话的回调函数 (`PostMessageChannel`)。  `dialog.open` 会返回回调（而不是 Promise），因为它不需要应用执行来暂停等待对话关闭（从而为各种用户交互模式提供更大的灵活性）。

## <a name="whats-new-in-teamsjs-version-20"></a>TeamsJS 版本 2.0 中的新增功能

TeamsJS 1.x.x 版本和 v.2.0.0 及更高版本之间有两个重大更改：

* [**回调函数现在返回 Promise 对象。**](#callbacks-converted-to-promises) TeamsJS v.1.12 中大多数具有回调参数的函数都已现代化，可返回 JavaScript [Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对象，以便改进异步操作的处理和代码可读性。

* [**API 现在已组织成 *功能*。**](#apis-organized-into-capabilities) 可以将功能视为提供类似功能的 API 的逻辑分组，例如 `authentication`、`dialog`、`chat` 和 `calendar`。 每个命名空间都表示一个单独的功能。

> [!TIP]
> 可以使用适用于 Microsoft Visual Studio Code 的 [Teams 工具包扩展](https://aka.ms/teams-toolkit)简化现有 Teams 应用的 [TeamsJS v.2.0 更新过程](#updating-to-the-teams-client-sdk-v200)。

### <a name="backwards-compatibility"></a>向后兼容

从现有 Teams 应用开始引用 `@microsoft/teams-js@2.0.0`（或更高版本）后，你将看到已更改的任何代码调用 API 的弃用警告。

提供了 API 转换层（将 v.1 SDK 映射到 v.2 SDK API 调用），使现有 Teams 应用能够继续在 Teams 中工作，直到它们能够更新应用程序代码以使用 TeamsJS v.2 API 模式。

#### <a name="teams-only-apps"></a>仅限 Teams 的应用

即使你希望应用仅在 Teams（而不是 Office 和 Outlook）中运行，最佳做法是尽快开始引用最新的 TeamsJS（*v.2.0* 或更高版本），以便从最新改进、新功能和支持（甚至对于仅限 Teams 的应用）中获益。 将继续支持 TeamsJS v.1.12，但不会添加任何新功能或改进。

完成后，下一步是使用本文中所述的更改[更新现有应用程序代码](#2-update-sdk-references)。 在此期间，v.1 到 v.2 API 转换层提供向后兼容性，确保现有 Teams 应用继续在 TeamsJS 版本 2.0 中工作。

#### <a name="teams-apps-running-across-microsoft-365"></a>跨 Microsoft 365 运行的 Teams 应用

使现有 Teams 应用能够在 Outlook 和 Office 中运行需要满足以下所有条件：

1. 依赖于 TeamsJS 版本 2.0 (`@microsoft/teams-js@2.0`) 或更高版本；

2. 根据本文中所述的所需更改[修改现有应用程序代码](#2-update-sdk-references)，以及

3. [将应用清单更新](#3-update-the-manifest-optional)到版本 1.13 或更高版本。

有关详细信息，请参阅[跨 Microsoft 365 扩展 Teams 应用](../../m365-apps/overview.md)。

### <a name="callbacks-converted-to-promises"></a>转换为 promise 的回调

以前使用回调参数的 Teams API 已更新为返回 JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对象。其中包括以下 API：

```js
app.getContext, app.initialize, appInstallDialog.openAppInstallDialog, app.openLink, authentication.authenticate, authentication.getAuthToken, authentication.getUser, authentication.registerAuthenticationHandlers was removed to support using Promises, calendar.openCalendarItem, calendar.composeMeeting, call.startCall, chat.getChatMembers, conversations.openConversation, location.getLocation, location.showLocation, mail.openMailItem, mail.composeMail, pages.backStack.navigateBack, pages.navigateCrossDomain, pages.navigateToTab, pages.tabs.getMruTabInstances, pages.tabs.getTabInstances, pages.getConfig, pages.config.setConfig, pages.backStack.navigateBack, people.selectPeople, teams.fullTrust.getConfigSetting, teams.fullTrust.joinedTeams.getUserJoinedTeams
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
> 使用 [Teams 工具包更新到 TeamsJS v.2.0](#updating-to-the-teams-client-sdk-v200) 时，所需的更新会在客户端代码中标记 `TODO` 注释。

### <a name="apis-organized-into-capabilities"></a>组织为功能的 API

*功能* 是提供类似功能的 API 的逻辑分组（通过命名空间）。 你可以将 Microsoft Teams、Outlook 和 Office 视为选项卡应用的主机。 如果主机支持该功能中定义的所有 API，则它支持给定功能。 主机无法部分实现功能。 功能可以基于特性或内容，例如 *身份验证* 或 *对话*。 应用程序类型也有一些功能，例如 *页面* 和其他分组。

从 TeamsJS v.2.0 开始，API 定义为 JavaScript 命名空间中名称与其所需功能匹配的函数。 例如，如果应用在支持 *对话* 功能的主机中运行，则应用可以安全地调用 API，例如 `dialog.open`（以及命名空间中定义的其他对话相关 API）。 如果应用尝试调用该主机中不支持的 API，则 API 将生成异常。 若要验证运行应用的当前主机是否支持给定功能，请调用其命名空间的 [isSupported()](#differentiate-your-app-experience) 函数。

#### <a name="differentiate-your-app-experience"></a>区分应用体验

可以通过对给定功能（命名空间）调用 `isSupported()` 函数，在运行时检查主机是否支持该功能。 如果支持，则返回 `true`；如果不支持，则返回 `false`，并且可以根据需要调整应用行为。 这样，应用便能在支持它的主机中亮起 UI 和功能，同时继续为不支持的主机运行。

运行应用之主机的名称作为 Context 接口 (`app.Context.app.host.name`) 上的 *hostName* 属性公开，可在运行时通过调用 `getContext` 进行查询。 它也可用作 `{hostName}` [URL 占位符值](./access-teams-context.md#get-context-by-inserting-url-placeholder-values)。 最佳做法是谨慎使用 *hostName* 机制：

* **请勿** 根据 *hostName* 属性值假设某个功能在主机中可用或不可用。相反，请检查功能支持 (`isSupported`)。
* **请勿** 使用 *hostName* 控制 API 调用。 相反，请检查功能支持 (`isSupported`)。
* **请** 使用 *hostName* 根据运行应用程序的主机来区分应用程序的主题。 例如，在 Teams 中运行时，可以使用 Microsoft Teams 紫色作为主要主题色；在 Outlook 中运行时，可以使用 Outlook 蓝色。
* **请** 使用 *hostName* 根据运行主机来区分向用户显示的消息。 例如，例如，在 Office 网页版中运行时显示“*在 Office 中管理任务*”，在 Microsoft Teams 中运行时显示“*在 Teams 中管理任务*”。

#### <a name="namespaces"></a>命名空间

从 TeamsJS v.2.0 开始，API 通过命名空间组织成 *功能*。 一些特别重要的新命名空间包括 *app*、*pages*、*dialog* 和 *teamsCore*。

##### <a name="app-namespace"></a>*app* 命名空间

`app` 命名空间包含跨 Microsoft Teams、Office 和 Outlook 的整体应用使用所需的顶级 API。 从 TeamsJS v.2.0 开始，其他各种 TeamsJS 命名空间中的所有 API 都已移动到 `app` 命名空间：

| 原始命名空间 `global (window)` | 新命名空间 `app` |
| - | - |
| `executeDeepLink` | `app.openLink`（已重命名） |
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

##### <a name="pages-namespace"></a>*pages* 命名空间

`pages` 命名空间包括用于在各种 Microsoft 365 主机（包括 Teams、Office 和 Outlook）中运行和导航网页的功能。 它还包括多个子功能，作为子名称空间实现。

| 原始命名空间 `global (window)` | 新命名空间 `pages` |
| - | - |
| `setFrameContext` | `pages.setCurrentFrame`（已重命名） |
| `initializeWithFrameContext` | `pages.initializeWithFrameContext` |
| `registerFocusEnterHandler` | `pages.registerFocusEnterHandler`
| `registerFullScreenHandler` | `pages.registerFullScreenHandler` |
| `navigateCrossDomain` | `pages.navigateCrossDomain` |
| `returnFocus` | `pages.returnFocus` |
| `shareDeepLink` | `pages.shareDeepLink` |

| 原始命名空间 `settings` | 新命名空间 `pages`  |
| - | - |
| `settings.getSettings` | `pages.getConfig`（已重命名）

###### <a name="pagestabs"></a>*pages.tabs*

| 原始命名空间 `global (window)` | 新命名空间 `pages.tabs` |
| - | - |
| `getTabInstances` |  `pages.tabs.getTabInstances` |
| `getMruTabInstances` | `pages.tabs.getMruTabInstances` |

| 原始命名空间 `navigation` | 新命名空间 `pages.tabs` |
| - | - |
| `navigation.navigateToTab` | `pages.tabs.navigateToTab` |

###### <a name="pagesconfig"></a>*pages.config*

| 原始命名空间 `settings` | 新命名空间 `pages.config`  |
| - | - |
| `settings.setSettings` | `pages.config.setConfig`（已重命名）
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
| `registerChangeConfigHandler` | `pages.config.registerChangeConfigHandler`（已重命名）

###### <a name="pagesbackstack"></a>*pages.backStack*

| 原始命名空间 `navigation` | 新命名空间 `pages.backStack`  |
| - | - |
| `navigation.navigateBack` | `pages.backStack.navigateBack`

| 原始命名空间 `global (window)` | 新命名空间 `pages.backStack`  |
| - | - |
| `registerBackButtonHandler` | `pages.backStack.registerBackButtonHandler`

###### <a name="pagesappbutton"></a>*pages.appButton*

| 原始命名空间 `global (window)` | 新命名空间 `pages.appButton`  |
| - | - |
| `registerAppButtonClickHandler` | `pages.appButton.onClick`（已重命名）
| `registerAppButtonHoverEnterHandler` | `pages.appButton.onHoverEnter`（已重命名）
| `registerAppButtonHoverLeaveEnter` | `pages.appButton.onHoverLeave`（已重命名）
| `FrameContext` 接口 | `pages.appButton.FrameInfo`（已重命名） |

##### <a name="dialog-namespace"></a>*dialog* 命名空间

TeamsJS *tasks* 命名空间已重命名为 *dialog*，并且已重命名以下 API：

| 原始命名空间 `tasks` | 新命名空间 `dialog`  |
| - | - |
| `tasks.startTask` | `dialog.open`（已重命名） |
| `tasks.submitTasks` | `dialog.submit`（已重命名） |
| `tasks.updateTasks` | `dialog.update.resize`（已重命名） |
| `tasks.TaskModuleDimension` 枚举 | `dialog.DialogDimension`（已重命名） |
| `tasks.TaskInfo` 接口 | `dialog.DialogInfo`（已重命名） |

此外，此功能已拆分为主要功能 (`dialog`)（用于支持基于 HTML 的对话）以及子功能 `dialog.bot`（用于基于机器人的对话）。

##### <a name="teamscore-namespace"></a>*teamsCore* 命名空间

若要将 TeamsJS SDK 通用化以运行其他 Microsoft 365 主机（如 Office 和 Outlook），Teams 特定的功能（最初在 *global* 命名空间中）已移动到 *teamsCore* 命名空间：

| 原始命名空间 `global (window)` | 新命名空间 `teamsCore`  |
| - | - |
| `enablePrintCapability` | `teamsCore.enablePrintCapability`
| `print` | `teamsCore.print`
| `registerOnLoadHandler` | `teamsCore.registerOnLoadHandler`
| `registerBeforeUnloadHandler` | `teamsCore.registerBeforeUnloadHandler`

#### <a name="updates-to-the-context-interface"></a>*Context* 接口更新

`Context` 接口已移动到 `app` 命名空间并更新为对类似属性进行分组，以便在 Outlook 和 Office 以及 Teams 中运行时获得更好的可扩展性。

添加了一个新属性 `app.Context.app.host.name`，使选项卡能够根据主机应用程序区分用户体验。

还可以通过查看 [TeamsJS v.2.0 源](https://github.com/OfficeDev/microsoft-teams-library-js/blob/main/packages/teams-js/src/public/app.ts)（*app.ts* 文件）中的 `transformLegacyContextToAppContext` 函数来可视化更改。

| 接口中的 `Context` 原始名称 | `app.Context` 中的新位置 |
| - | - |
| `appIconPosition` | `app.Context.app.iconPositionVertical` |
| `appLaunchId`| *不在 TeamsJS v.2.0 中* |
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

## <a name="updating-to-the-teams-client-sdk-v200"></a>更新到 Teams 客户端 SDK v.2.0.0

更新 Teams 应用以使用 TeamsJS v.2.0 的最简单方法是使用适用于 Visual Studio Code 的 [Teams 工具包扩展](https://aka.ms/teams-toolkit)。 本部分将指导你完成执行此操作的步骤。 如果希望手动更新代码，请参阅[转换为 promise 的回调](#callbacks-converted-to-promises)和[组织为功能的 API](#apis-organized-into-capabilities) 部分，以获取有关所需 API 更改的更多详细信息。

### <a name="1-install-the-latest-teams-toolkit-visual-studio-code-extension"></a>1. 安装最新的 Teams 工具包 Visual Studio Code 扩展

在 *Visual Studio Code 扩展商城* 中，搜索“**Teams 工具包**”并安装版本 `2.10.0` 或更高版本。

### <a name="2-update-sdk-references"></a>2. 更新 SDK 引用

若要在 Outlook 和 Office 中运行，应用将需要依赖于 [npm 包](https://www.npmjs.com/package/@microsoft/teams-js/v/2.0.0) `@microsoft/teams-js@2.0.0`（或更高版本）。 若要手动执行这些步骤以及有关 API 更改的详细信息，请参阅以下部分[转换为 promise 的回调](#callbacks-converted-to-promises)和[组织为功能的 API](#apis-organized-into-capabilities)。

1. 确保拥有 [Teams 工具包](https://aka.ms/teams-toolkit) `v.2.10.0` 或更高版本
1. 打开 *命令面板*：`Ctrl+Shift+P`
1. 运行命令 `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`。

完成后，该实用工具将使用 TeamsJS v.2.0（`@microsoft/teams-js@2.0.0` 或更高版本）依赖项更新 `package.json` 文件，`*.js/.ts` 和 `*.jsx/.tsx` 文件将更新为：

> [!div class="checklist"]
>
> * 对 TeamsJS v.2.0 的 `package.json` 引用
> * TeamsJS v.2.0 的 Import 语句
> * 对 TeamsJS v.2.0 的[函数、枚举和接口调用](#apis-organized-into-capabilities)
> * `TODO` 注释提醒，查看可能受 [ 上下文 ](#updates-to-the-context-interface) 接口更改影响的区域
> * `TODO` 注释提醒，[将回调函数转换为 promise](#callbacks-converted-to-promises)

> [!IMPORTANT]
> 升级工具不支持 html 文件中的代码，需要手动更改。

### <a name="3-update-the-manifest-optional"></a>3. 更新清单（可选）

如果要更新 Teams 应用以在 Office 和 Outlook 中运行，则还需要将应用清单更新为版本 1.13 或更高版本。 可以使用 Teams 工具包轻松执行此操作，也可以手动执行此操作。

# <a name="teams-toolkit"></a>[Teams 工具包](#tab/manifest-teams-toolkit)

1. 打开 *命令面板*：`Ctrl+Shift+P`
1. 运行“**Teams：升级 Teams 清单以支持 Outlook 和 Office 应用**”命令并选择应用清单文件。将就地进行更改。

# <a name="manual-steps"></a>[ 手动步骤 ](#tab/manifest-manual)

打开 Teams 应用清单，使用以下值更新 `$schema` 和 `manifestVersion`：

```json
{
    "$schema" : "https://developer.microsoft.com/json-schemas/teams/v1.13/MicrosoftTeams.schema.json",
    "manifestVersion" : "1.13"
}
```

---

如果使用 Teams 工具包创建了个人应用，则还可以使用它来验证清单文件的更改并识别任何错误。 打开命令面板 `Ctrl+Shift+P` 并找到“**Teams：验证清单文件**”，或者从 Teams 工具包的“部署”菜单中选择选项（查找 Visual Studio Code 左侧的 Teams 图标）。

:::image type="content" source="../../m365-apps/images/toolkit-validate-manifest-file.png" alt-text=" Teams 工具包“部署”菜单下的“验证清单文件”选项":::

## <a name="next-steps"></a>后续步骤

* 使用 [TeamsJS 引用](/javascript/api/overview/msteams-client)开始使用 Microsoft Teams JavaScript 客户端 SDK。
* 查看[更改日志](https://github.com/OfficeDev/microsoft-teams-library-js/blob/main/packages/teams-js/CHANGELOG.md)以了解 TeamsJS 的最新更新。
