---
title: 最近更新
description: 介绍 Microsoft 团队中的所有新开发人员功能
keywords: 团队新增功能最新
ms.openlocfilehash: f8550070ed010d99c0c33202ada95b64c05cdc4f
ms.sourcegitcommit: 68aeac34a2e585b985eabfae5d160b6b26d43b1a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/26/2020
ms.locfileid: "42982142"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>Microsoft 团队中面向开发人员的新增功能

## <a name="change-log"></a>更改日志

更改日志将列出 Microsoft 团队平台和此文档集的更改。 有时，条目可用于吸引团队开发人员感兴趣的新功能。

| **Date** | **备注** | **更改的主题** |
| -------- | --------- | ------------------ |
| 03/24/2020 | 添加了对检索会话的单个成员和其他支持检索分页成员的支持。 | [获取你的 bot 的团队上下文](~/bots/how-to/get-teams-context.md)
| 12/26/2019 | 发送`replyToId`到 bot 的负载中的参数不再加密，这样您就可以使用此值来构造 deeplinks 给这些邮件。 邮件负载在参数`legacy.replyToId`中包含加密的值。  |
| 11/5/2019 | 使用 web 内容页中的团队 JavaScript SDK 进行单一登录是在开发人员预览版中 | [单一登录](~/tabs/how-to/authentication/auth-aad-sso.md) |
| 10/31/2019 | 已更新会话 bot 和邮件扩展文档，以反映 4.6 Bot 框架 SDK。 有关 v3 SDK 的文档在 "资源" 部分提供。 | 所有机器人和邮件扩展文档。 |
| 10/31/2019 | 新的文档结构和主要文章重构。 请通过创建 GitHub 问题报告任何死链接或404 | 全部！ |
| 9/13/2019 | 从基于操作的消息扩展安装请求 bot | [使用邮件扩展启动操作](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 8/28/2019 | 在选项卡和连接器中支持专用通道 | [获取您的选项卡的上下文](tabs/how-to/access-teams-context.md#retrieving-context-in-private-channels) |
| 06/20/2019 | 将外部网站从外部网站共享到团队频道 | [与团队共享](~/share-to-teams.md) |
| 05/25/2019 | 使用来自任务模块的 bot 消息进行响应 | [使用来自任务模块的 bot 消息进行响应](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | 组聊天中的 bot | [与组聊天或频道中的 bot 进行交互](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | 应用程序清单本地化 | [应用本地化](~/publishing/apps-localization.md) |
| 05/20/2019 | 邮件操作 | [邮件操作](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | 链接 unfurling （自定义 URL 预览） | [链接 unfurling](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | 适用于 store 应用的应用程序认证计划 | [应用程序证书](~/publishing/application-certification.md) |
| 05/06/2019 | 应用模板现已推出。 | [应用模板](~/samples/app-templates.md) |
| 04/23/2019 | 基于操作的邮件扩展现已提供 | [基于操作的邮件扩展](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | 创建到专用聊天的深层链接不适用于开发人员预览和可用 | [深层链接到聊天](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 01/23/2019 | 在选项卡上下文中呈现 SKU 和 licenceType 信息 | [选项卡上下文](~/concepts/tabs/tabs-context.md) |
| 11/12/2018 | 组聊天中的选项卡现在在团队的已发布版本中可用，已从开发人员预览版中移出。 作为此工作的一部分，"选项卡" 部分已进行了改编以实现清晰度。| [可配置选项卡](~/concepts/tabs/tabs-configurable.md) |
| 11/11/2018 | 对 Node JS 和 for .NET/c # 的入门已更新为使用团队中的应用程序 Studio，并在 Azure 中基于托管节点的团队应用程序添加了一个新的部分。 | [Microsoft team platform With c #/.NET 和应用程序 studio 入门](~/get-started/get-started-dotnet-app-studio.md)， [microsoft Team PLATFORM with Node JS and app studio](~/get-started/get-started-nodejs-app-studio.md)入门，在[Azure 中托管你的节点团队应用程序](~/get-started/get-started-nodejs-in-azure.md)|
| 11/09/2018 | 现在，您可以创建到用户之间的私人聊天的深层链接。 | [深层链接到聊天](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 11/08/2018 | SharePoint Framework 1.7 附带了一项新功能，可将 Microsoft 团队选项卡用作 SharePoint 框架 web 部件。 | [SharePoint 中的选项卡](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | 已发布 "任务模块" 功能。 任务模块使您能够在团队应用程序中从 bot 和选项卡中创建模式弹出窗口体验。 在弹出菜单中，您可以运行自己的自定义 HTML/JavaScript 代码， `<iframe>`显示基于一个小部件（如 YouTube 或 Microsoft Stream 视频），或显示一个[自适应卡片](https://docs.microsoft.com/adaptive-cards/)。 | [任务模块概述](~/concepts/task-modules/task-modules-overview.md)、[选项卡中的任务模块](~/concepts/task-modules/task-modules-tabs.md)、 [bot 中的任务模块](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | 更新了智能卡的格式信息，并在桌面、iOS 和 Android 客户端中对团队进行了测试。 | [卡片](~/concepts/cards/cards.md)，[卡片格式](~/concepts/cards/cards-format.md) |
| 09/24/2018 | Microsoft Graph 的呼叫和联机会议 Api 已发布到 beta，团队应用现在可以使用语音和视频以丰富的方式与用户进行交互。 | [呼叫和联机会议 bot](~/concepts/calls-and-meetings/registering-calling-bot.md)、[实时媒体概念](~/concepts/calls-and-meetings/real-time-media-concepts.md)、[注册呼叫机器人](~/concepts/calls-and-meetings/registering-calling-bot.md)、[调试和本地测试](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)、[应用程序托管媒体](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)、[处理传入呼叫通知](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | 选项卡配置页面现在高度增加。 | [选项卡设计](tabs/design/tabs.md) |
| 08/15/2018 | 团队中现支持自适应卡片。|[团队中的自适应卡片操作](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | 对 DevTools 的客户端支持已经过记录，以供开发人员预览。| [Microsoft 团队桌面客户端的 DevTools](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | 邮件扩展现在支持多个命令。 此功能已在开发人员预览版中，现已发布给所有用户。| [composeExtensions](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | 串联配置现在在连接器中受支持。 为了清楚起见，连接器文档也进行了修订和扩展| [连接器](~/concepts/connectors/connectors.md)|
| 08/06/2018 | 你的 bot 现在可以发送和接收文件。| [通过你的 bot 发送和接收文件](~/concepts/bots/bots-files.md)|
| 07/27/2018 | 现在，开发人员预览版支持邮件扩展中的多个命令。 | [邮件扩展已扩展](~/resources/dev-preview/developer-preview-features.md)|
| 07/23/2018 | 有关应用程序重新认证的信息已添加到 "发布" 部分。 |[清单权限](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | 在开发人员预览版中，已向选项卡配置页分配更多空间。 | [选项卡配置页面高度增加](tabs/design/tabs.md#configuration-page-height)|
| 07/12/2018 | 有关来宾访问的信息。 | [Microsoft Teams 中的来宾访问](https://docs.microsoft.com/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | 已添加 Microsoft 团队租户应用程序目录的预发布信息。 | [发布 Microsoft 团队应用程序](~/publishing/apps-publish.md)|
| 05/31/2018 | 团队开发人员预览版（ring 3.6）已更新，以包括将 bot 和选项卡添加到分组聊天的功能。 | [开发人员预览版中的功能](~/resources/dev-preview/developer-preview-features.md)（[开发人员预览版架构](~/resources/schema/manifest-schema-dev-preview.md)）|
| 05/29/2018 | 自适应卡片现在在团队中的[自适应卡片操作中](task-modules-and-cards/cards/cards-reference.md)受支持 |
| 05/29/2018 | 如果使用的是[开发人员预览](~/resources/dev-preview/developer-preview-intro.md)，你的 bot 现在可以发送和接收文件。| [通过你的 Bot 发送和接收文件](~/concepts/bots/bots-files.md)，[适用于 Microsoft 团队的公共开发人员预览版中的功能](~/resources/dev-preview/developer-preview-features.md)|
| 04/17/2018 | 已将 replyToID 添加到`Invoke`和`MessageBack`卡片操作的有效负载中。 如果需要更新卡片操作来自的邮件，这将非常有用。 | [卡片操作](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | 添加了本主题，以跟踪对团队编程接口和此文档集所做的更改。 | [新增功能](~/whats-new.md)|
| 04/10/2018 | 更改了身份验证 Url，以便在路径中始终使用租户 ID。 | [选项卡的身份验证流](~/concepts/authentication/auth-flow-tab.md)（ [AAD 选项卡身份验证](~/concepts/authentication/auth-tab-AAD.md)）|
| 04/06/2018 | 添加了有关使用命令框的设计准则。 |[命令框](~/resources/design/framework/command-box.md)|
| 04/02/2018 | 使用 bot 向您的应用程序发送通知。 |[仅通知 bot](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | 用于主动消息的扩展文档。 |[启动对话](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | 卡片的重构文档。 |[卡片](~/concepts/cards/cards.md)、[卡片操作](~/concepts/cards/cards-actions.md)、[卡片格式](~/concepts/cards/cards-format.md)、[卡片参考](~/concepts/cards/cards-reference.md)|
| 03/03/2018 | 添加了团队应用程序 Studio 的文档。 |[使用应用程序 studio 中的控件库在](~/get-started/app-studio-component-library.md)[团队应用程序 studio 中快速开发应用](~/get-started/get-started-app-studio.md)程序|
| 02/27/2018 | 添加了示例代码以演示 AsTeamsChannelAccounts （）方法。 |[获取你的 bot 的上下文](~/concepts/bots/bots-context.md)|
| 02/05/2018 | 新增了使用 c # 入门主题。 |[开始在 Microsoft Teams 平台上使用 C#/.NET ](./get-started/get-started-dotnet-app-studio.md)|

## <a name="submit-your-questions-bugs-feature-requests-and-contributions"></a>提交您的问题、bug、功能请求和发布内容

我们会在[多个频道](~/feedback.md)中侦听开发人员社区。
