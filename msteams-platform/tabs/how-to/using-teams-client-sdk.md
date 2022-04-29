---
title: 使用 JavaScript 客户端 SDK 生成选项卡和其他托管体验
author: heath-hamilton
ms.author: surbhigupta
description: Microsoft Teams JavaScript 客户端 SDK 概述可帮助你构建 Teams 应用体验，托管在 <iframe>. 它包括基本函数、身份验证命名空间和设置命名空间。
ms.localizationpriority: high
keywords: teams 选项卡组频道可配置静态 SDK JavaScript 个人版
ms.topic: conceptual
ms.openlocfilehash: f4204555e57c270ad03a7a01d5b231d63b72296a
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111890"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>使用 Microsoft Teams JavaScript 客户端 SDK 生成选项卡和其他托管体验

Microsoft Teams JavaScript 客户端 SDK 可帮助你在 Teams 中创建托管体验，这意味着在 iframe 中显示应用内容。

SDK 有助于开发具有以下任何 Teams 功能的应用：

* [选项卡](../../tabs/what-are-tabs.md)
* [任务模块](../../task-modules-and-cards/what-are-task-modules.md)

例如，SDK 可以使[选项卡对用户在 Teams 客户端中进行的主题更改](../../build-your-first-app/build-personal-tab.md#3-update-your-tab-theme)做出反应。

## <a name="getting-started"></a>入门

根据开发首选项执行以下操作之一：

* [使用 npm 或 Yarn 安装 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)
* [克隆 SDK (GitHub)](https://github.com/OfficeDev/microsoft-teams-library-js)

## <a name="common-sdk-functions"></a>常用 SDK 函数

请参阅下表，了解常用的 SDK 函数。 [SDK 参考文档](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)提供了更全面的信息。

### <a name="basic-functions"></a>基本函数

| 功能  | 说明          | 文档|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | 初始化 SDK。 必须在调用任何其他 SDK 之前调用此函数。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-initialize&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| 获取页面正在运行的当前状态。 回调将检索 **Context** 对象。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest&preserve-view=true)<br/>[context obj](/javascript/api/@microsoft/teams-js/@microsoft.teams-js?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | 初始化 Teams 库，并根据 contentUrl 和 websiteUrl 设置选项卡的 [frame context](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)。 这可确保转到网站/重新加载功能在正确的 URL 上运行。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-initializewithframecontext&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | 根据 contentUrl 和 websiteUrl 设置选项卡的 [frame context](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)。 这可确保转到网站/重新加载功能在正确的 URL 上运行。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-setframecontext&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: Boolean)` |用户切换选项卡的全屏/窗口视图时注册的处理程序。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-registerfullscreenhandler&preserve-view=true)<br/>[Boolean](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-registerfullscreenhandler&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |用户选择启用 **设置** 按钮重新配置选项卡时注册的处理程序。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |获取应用的选项卡。 回调将检索 **TabInformation** 对象。 **TabInstanceParameters** 对象是可选参数。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-gettabinstances&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|获取用户最近使用的选项卡。 回调将检索 **TabInformation** 对象。 **TabInstanceParameters** 对象是可选参数。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-getmrutabinstances&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|将 **DeepLinkParameters** 对象作为输入和共享一个深度链接对话框，用户可以使用该对话框导航到 *选项卡中* 的内容。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-sharedeeplink&preserve-view=true)<br/>[deepLink obj](/javascript/api/@microsoft/teams-js/microsoftteams.deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: Boolean, reason?: string))`|将所需的 **deepLink** 作为输入并将用户导航到 URL 或触发客户端操作（例如打开或安装 *Teams 中* 的应用程序）。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-executedeeplink&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: Boolean, reason?: string))`|将 **TabInstance** 对象作为输入并导航到指定的选项卡实例。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-navigatetotab&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstance?view=msteams-client-js-latest&preserve-view=true)|

### <a name="authentication-namespace"></a>身份验证命名空间

| 功能  | 说明          | 文档|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|启动身份验证请求，该请求使用调用方提供的参数打开新窗口。 可选输入值由 **AuthenticateParameters** 对象定义。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[auth obj](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|通知启动身份验证请求的帧请求已成功并关闭身份验证窗口|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|通知启动身份验证请求的帧请求失败并关闭身份验证窗口。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.getAuthToken(authTokenRequest: AuthTokenRequest)`|发送请求以代表应用颁发 Azure AD 令牌。 如果令牌尚未过期，则可以从缓存中获取该令牌。 否则，将向 Azure AD 发送请求以获取新令牌。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-authentication-getauthtoken&preserve-view=true)|

### <a name="settings-namespace"></a>设置命名空间

| 功能  | 说明          | 文档|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: Boolean)`|初始值为 false。 当有效性状态为 true 时，激活 **保存** 或 **删除** 按钮。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|获取当前实例的设置。 回调将检索 **Settings** 对象。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: Boolean, reason?: string)`|配置当前实例的设置。 有效设置由 **Settings** 对象定义。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|用户选择 **保存** 按钮时注册的处理程序。 此处理程序应用于创建或更新为内容提供动力的基础资源。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|用户选择 **删除** 按钮时注册的处理程序。 此处理程序应用于删除为内容提供动力的基础资源。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|

### <a name="task-modules-namespace"></a>任务模块命名空间

| 功能  | 说明          | 文档|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|将 **TaskInfo** 对象作为输入，并允许应用打开任务模块。 任务模块完成后，将注册可选 **submitHandler**。 |[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[taskInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|提交任务模块。 可选 **result** 字符串参数是发送到机器人或应用的结果，通常是 JSON 对象或序列化，可选 **appIds** 字符串或字符串数组参数有助于验证调用是否源自调用任务模块的 appId。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-tasks-submittask&preserve-view=true)|
