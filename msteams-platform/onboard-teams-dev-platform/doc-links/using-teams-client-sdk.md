---
title: 使用 Teams 客户端 SDK
author: laujan
description: 如何使用团队客户端 SDK 向自定义选项卡添加团队感知功能
keywords: 团队选项卡组频道可配置静态 SDK JavaScript 个人
ms.topic: conceptual
ms.openlocfilehash: 66d44617b897e44268ae2cee53f7ea64743ad821
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651893"
---
# <a name="using-the-teams-client-sdk"></a>使用 Teams 客户端 SDK

**团队 javascript 客户端 SDK**和**团队 Javascript 库**是[Microsoft 团队开发人员平台](https://msdn.microsoft.com/microsoft-teams)的一部分，提供了用于简化团队应用程序创建的工具和过程。 团队客户端 SDK 作为 npm 包进行分发。 可在以下位置找到最新版本： <https://www.npmjs.com/package/@microsoft/teams-js> 。 团队库位于 <https://github.com/OfficeDev/microsoft-teams-library-js> 。

下表概述了在选项卡开发中通常使用的团队库函数：

## <a name="teams-sdk-public-api"></a>团队 SDK 公共 API 

| 功能  | 说明          | 文档|
| -----     | -----     | -----    | -----        |
| `microsoftTeams.initialize()` | 初始化团队库。 此函数必须在任何其他 SDK 调用之前调用。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-)|
|`microsoftTeams.getContext(callback: (context: Context)`| 获取运行页面的当前状态。 回调将检索 **Context** 对象。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-)<br/>[上下文 obj](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | 初始化团队库，并根据 contentUrl 和 websiteUrl 设置选项卡的 [帧上下文](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest) 。 这可确保 "转到网站/重新加载" 功能在正确的 URL 上运行。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initializewithframecontext-framecontext--------void--string---)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | 根据 contentUrl 和 websiteUrl 设置选项卡的 [帧上下文](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest) 。 这可确保 "转到网站/重新加载" 功能在正确的 URL 上运行。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#setframecontext-framecontext-)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |当用户切换选项卡的全屏/窗口视图时注册的处理程序。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-)<br/>[boolean](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest#isfullscreen)|
|`microsoftTeams.registerChangeSettingsHandler()` |当用户选择 "已启用的 **设置** " 按钮以重新配置选项卡时注册的处理程序。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |获取应用程序拥有的选项卡。 该回调检索 **TabInformation** 对象。 **TabInstanceParameters**对象是可选参数。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|获取用户最近使用过的选项卡。 该回调检索 **TabInformation** 对象。 **TabInstanceParameters**对象是可选参数。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.teaminformation?view=msteams-client-js-latest)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstanceparameters?view=msteams-client-js-latest)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|将 **DeepLinkParameters** 对象作为输入，并共享一个 deep link 对话框，用户可使用该对话框导航到 *选项卡中的*内容。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-)<br/>[deepLink obj](/javascript/api/@microsoft/teams-js/microsoftteams.deeplinkparameters?view=msteams-client-js-latest)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|采用必需的 **deepLink** 作为输入，并将用户导航到 URL 或触发客户端操作（如打开或安装） *团队中*的应用程序。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|采用 **TabInstance** 对象作为输入并导航到指定的选项卡实例。|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstance?view=msteams-client-js-latest)|

## <a name="authentication-namespace"></a>身份验证命名空间

| 功能  | 说明          | 文档|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|启动身份验证请求，以使用呼叫者提供的参数打开新窗口。 可选输入值由 **AuthenticateParameters** 对象定义。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#authenticate-authenticateparameters-)<br/>[auth obj](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|通知启动了请求成功的身份验证请求的帧，并关闭了身份验证窗口|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#notifysuccess-string--string-)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|通知启动了请求失败的身份验证请求的帧，并关闭了身份验证窗口。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#notifyfailure-string--string-)|

## <a name="settings-namespace"></a>设置命名空间

| 功能  | 说明          | 文档|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|初始值为 false。 当有效性状态为 true 时，激活 " **保存** " 或 " **删除** " 按钮。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#setvaliditystate-boolean-)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|获取当前实例的设置。 回调将检索 **Settings** 对象。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#getsettings--instancesettings--settings-----void-)<br/>[设置 obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|配置当前实例的设置。 有效设置由 **settings** 对象定义。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#setsettings-settings-)<br/>[设置 obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|当用户选择 " **保存** " 按钮时注册的处理程序。 此处理程序应用于创建或更新用于为内容加电的基础资源。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#registeronsavehandler--evt--saveevent-----void-)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|当用户选择 " **删除** " 按钮时注册的处理程序。 此处理程序应用于删除为内容加电的基础资源。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#registeronremovehandler--evt--removeevent-----void-)|

## <a name="tasks-namespace"></a>任务命名空间

| 功能  | 说明          | 文档|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|采用 **TaskInfo** 对象作为输入，并允许应用打开任务模块。 在任务模块完成时，将注册可选 **submitHandler** 。 |[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#starttask-taskinfo---err--string--result--string-----void-)<br/>[taskInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.taskinfo?view=msteams-client-js-latest)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|提交任务模块。 可选的 **result** string 参数是发送到 bot 或应用程序的结果，通常为 JSON 对象或序列化;可选的 **appIds** 字符串或字符串数组参数可帮助验证调用是否源于调用任务模块的相同 appId。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---)|