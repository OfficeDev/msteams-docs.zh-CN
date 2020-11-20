---
title: 使用 Teams 客户端 SDK
author: laujan
description: 如何使用团队客户端 SDK 向自定义选项卡添加团队感知功能
keywords: 团队选项卡组频道可配置静态 SDK JavaScript 个人
ms.topic: conceptual
ms.openlocfilehash: 0a701e3baff08b35592288408cf32d0a2a0a2584
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346782"
---
# <a name="using-the-teams-client-sdk"></a>使用 Teams 客户端 SDK

**团队 javascript 客户端 SDK** 和 **团队 Javascript 库** 是 [Microsoft 团队开发人员平台](/microsoftteams/platform/)的一部分，提供了用于简化团队应用程序创建的工具和过程。 团队客户端 SDK 作为 npm 包进行分发。 可在以下位置找到最新版本： <https://www.npmjs.com/package/@microsoft/teams-js> 。 团队库位于 <https://github.com/OfficeDev/microsoft-teams-library-js> 。

下表概述了在选项卡开发中通常使用的团队库函数：

## <a name="teams-sdk-public-api"></a>团队 SDK 公共 API 

| 功能  | 说明          | 文档|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | 初始化团队库。 此函数必须在任何其他 SDK 调用之前调用。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| 获取运行页面的当前状态。 回调将检索 **Context** 对象。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-&preserve-view=true)<br/>[上下文 obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | 初始化团队库，并根据 contentUrl 和 websiteUrl 设置选项卡的 [帧上下文](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) 。 这可确保 "转到网站/重新加载" 功能在正确的 URL 上运行。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initializewithframecontext-framecontext--------void--string---&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | 根据 contentUrl 和 websiteUrl 设置选项卡的 [帧上下文](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) 。 这可确保 "转到网站/重新加载" 功能在正确的 URL 上运行。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#setframecontext-framecontext-&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |当用户切换选项卡的全屏/窗口视图时注册的处理程序。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-&preserve-view=true)<br/>[boolean](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerFullScreenHandler__isFullScreen__boolean_____void_&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |当用户选择 "已启用的 **设置** " 按钮以重新配置选项卡时注册的处理程序。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |获取应用程序拥有的选项卡。 该回调检索 **TabInformation** 对象。 **TabInstanceParameters** 对象是可选参数。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|获取用户最近使用过的选项卡。 该回调检索 **TabInformation** 对象。 **TabInstanceParameters** 对象是可选参数。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[tabInstance obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|将 **DeepLinkParameters** 对象作为输入，并共享一个 deep link 对话框，用户可使用该对话框导航到 *选项卡中的* 内容。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-&preserve-view=true)<br/>[deepLink obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|采用必需的 **deepLink** 作为输入，并将用户导航到 URL 或触发客户端操作（如打开或安装） *团队中* 的应用程序。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|采用 **TabInstance** 对象作为输入并导航到指定的选项卡实例。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-&preserve-view=true)<br/>[tabInstance obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tabinstance?view=msteams-client-js-latest&preserve-view=true)|

## <a name="authentication-namespace"></a>身份验证命名空间

| 功能  | 说明          | 文档|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|启动身份验证请求，以使用呼叫者提供的参数打开新窗口。 可选输入值由 **AuthenticateParameters** 对象定义。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[auth obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|通知启动了请求成功的身份验证请求的帧，并关闭了身份验证窗口|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|通知启动了请求失败的身份验证请求的帧，并关闭了身份验证窗口。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)|

## <a name="settings-namespace"></a>设置命名空间

| 功能  | 说明          | 文档|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|初始值为 false。 当有效性状态为 true 时，激活 " **保存** " 或 " **删除** " 按钮。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|获取当前实例的设置。 回调将检索 **Settings** 对象。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)<br/>[设置 obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|配置当前实例的设置。 有效设置由 **settings** 对象定义。|[function](/https://docs.microsoft.com/en-us/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest)<br/>[设置 obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|当用户选择 " **保存** " 按钮时注册的处理程序。 此处理程序应用于创建或更新用于为内容加电的基础资源。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|当用户选择 " **删除** " 按钮时注册的处理程序。 此处理程序应用于删除为内容加电的基础资源。|[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|

## <a name="tasks-namespace"></a>任务命名空间

| 功能  | 说明          | 文档|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|采用 **TaskInfo** 对象作为输入，并允许应用打开任务模块。 在任务模块完成时，将注册可选 **submitHandler** 。 |[function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[taskInfo obj](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|提交任务模块。 可选的 **result** string 参数是发送到 bot 或应用程序的结果，通常为 JSON 对象或序列化;可选的 **appIds** 字符串或字符串数组参数可帮助验证调用是否源于调用任务模块的相同 appId。|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)|
