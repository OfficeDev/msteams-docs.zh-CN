---
title: 使用 JavaScript 客户端 SDK 生成选项卡和其他托管体验
author: heath-hamilton
ms.author: surbhigupta
description: JavaScript Microsoft Teams SDK 概述，它可以帮助你构建Teams托管在 <iframe>.
localization_priority: Normal
keywords: teams 选项卡组通道可配置的静态 SDK JavaScript 个人
ms.topic: conceptual
ms.openlocfilehash: d1bcf9fd853d1b0e93c99ae62ad32f462fc98ed4eee1796e7ae5510ad02a8909
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2021
ms.locfileid: "57704933"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>使用 JavaScript 客户端 SDK 生成选项卡Microsoft Teams托管体验

JavaScript Microsoft Teams SDK 可以帮助你在 Teams 创建托管体验，这意味着在 iframe 中显示应用内容。

SDK 有助于开发具有以下任一功能Teams应用：

* [选项卡](../../tabs/what-are-tabs.md)
* [任务模块](../../task-modules-and-cards/what-are-task-modules.md)

例如，SDK 可以使选项卡[响应](../../build-your-first-app/build-personal-tab.md#3-update-your-tab-theme)用户在客户端中Teams更改。

## <a name="getting-started"></a>入门

根据您的开发首选项执行下列操作之一：

* [使用 npm 或更新安装 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)
* [克隆 SDK (GitHub) ](https://github.com/OfficeDev/microsoft-teams-library-js)

## <a name="common-sdk-functions"></a>通用 SDK 函数

请参阅下表以了解常用的 SDK 函数。 [SDK 参考文档提供了](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)更全面的信息。

### <a name="basic-functions"></a>基本函数

| 功能  | 说明          | 文档|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | 初始化 SDK。 必须先调用此函数，然后才能调用任何其他 SDK。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| 获取正在运行页面的当前状态。 回调检索 **Context** 对象。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-&preserve-view=true)<br/>[context obj](/javascript/api/@microsoft/teams-js/@microsoft.teams-js?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | 初始化Teams库，并设置选项卡的框架[上下文，具体取决于](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)contentUrl 和 websiteUrl。 这可确保在正确的 URL 上运行"转到网站/重新加载"功能。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initializewithframecontext-framecontext--------void--string---&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | 根据 contentUrl [和](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) websiteUrl 设置选项卡的框架上下文。 这可确保在正确的 URL 上运行"转到网站/重新加载"功能。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#setframecontext-framecontext-&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |当用户切换选项卡的全屏/窗口视图时注册的处理程序。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-&preserve-view=true)<br/>[boolean](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerFullScreenHandler__isFullScreen__boolean_____void_&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |在用户选择启用的选项卡按钮以重新配置选项卡 **设置** 注册的处理程序。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |获取应用拥有的选项卡。 回调检索 **TabInformation** 对象。 **TabInstanceParameters** 对象是可选参数。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|获取用户最近使用的选项卡。 回调检索 **TabInformation** 对象。 **TabInstanceParameters** 对象是可选参数。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|将 **DeepLinkParameters** 对象作为输入，并共享一个深层链接对话框，用户可以使用该对话框导航到选项卡 *中的内容*。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-&preserve-view=true)<br/>[deepLink obj](/javascript/api/@microsoft/teams-js/microsoftteams.deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|将所需的 **deepLink** 作为输入，将用户导航到 URL 或触发客户端操作（如打开 *或* 安装）Teams。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|将 **TabInstance** 对象作为输入并导航到指定的选项卡实例。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstance?view=msteams-client-js-latest&preserve-view=true)|

### <a name="authentication-namespace"></a>身份验证命名空间

| 功能  | 说明          | 文档|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|启动身份验证请求，该请求使用调用方提供的参数打开新窗口。 可选输入值由 **AuthenticateParameters 对象** 定义。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[auth obj](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|通知启动身份验证请求的框架请求已成功并关闭身份验证窗口|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|通知启动身份验证请求的帧请求失败并关闭身份验证窗口。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.getAuthToken(authTokenRequest: AuthTokenRequest)`|发送代表应用颁发 Azure AD 令牌的请求。 如果令牌尚未过期，可以从缓存获取。 否则，会向 Azure AD 发送请求以获取新令牌。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#getAuthToken_AuthTokenRequest_&preserve-view=true)|

### <a name="settings-namespace"></a>设置命名空间

| 功能  | 说明          | 文档|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|初始值为 false。 在有效性 **状态****为** true 时激活"保存或删除"按钮。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|获取当前实例的设置。 回调检索 **设置** 对象。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|配置当前实例的设置。 有效设置由 设置 **对象定义**。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|在用户选择"保存"按钮时注册 **的** 处理程序。 此处理程序应该用于创建或更新支持内容的基础资源。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|在用户选择"删除"按钮时注册 **的** 处理程序。 此处理程序应该用于删除支持内容的基础资源。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|

### <a name="task-modules-namespace"></a>任务模块命名空间

| 功能  | 说明          | 文档|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|将 **TaskInfo** 对象作为输入，并允许应用打开任务模块。 可选 **submitHandler** 在任务模块完成时注册。 |[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[taskInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|提交任务模块。 可选 **结果** 字符串参数是发送到自动程序或应用的结果，通常是 JSON 对象或序列化;可选的 **appIds** 字符串或字符串数组参数有助于验证调用是否来自与调用任务模块的 appId 相同的 appId。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)|
