---
title: 最近更新
description: 介绍 Microsoft Teams 中所有新的开发人员功能
ms.topic: reference
keywords: teams 新增功能
ms.openlocfilehash: d1a6a0532a857d02e7188c42282f1d0727d6f309
ms.sourcegitcommit: 23ed7edf145df10dcfba15c43978eae9e0d451a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2021
ms.locfileid: "50753544"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>Microsoft Teams 中针对开发人员的新增功能

>[!TIP]
> 查看 Teams 应用模板目录中常见团队 [**方案的示例解决方案**](samples/app-templates.md)！ 目录按字母顺序排序，并且最新添加内容用星形 标记。

## <a name="change-log"></a>更改日志

更改日志列出了对 Microsoft Teams 平台和此文档集的更改。 有时，条目可用于引起对 Teams 开发人员感兴趣的新功能的注意。

| "日期" | **备注** | **已更改的主题** |
| -------- | --------- | ------------------ |
|03/05/2021|注意：选项卡将不再具有围绕其体验的边距。 选项卡开发人员应查看和更新其应用。 | [删除制表位边距](resources/removing-tab-margins.md) |
|03/05/2021 | 默认安装范围和组功能在开发人员预览版中。| [默认安装范围和组功能](concepts/deploy-and-publish/apps-upload.md#add-a-default-install-scope-and-group-capability) |
|03/05/2021|对个人应用选项卡重新排序|[对个人应用中的聊天选项卡重新排序](tabs/how-to/create-tab-pages/content-page.md#reorder-static-personal-tabs)|
|03/04/2021|自适应卡片中的信息屏蔽在开发人员预览版中。| [自适应卡片中的信息屏蔽](task-modules-and-cards/cards/cards-format.md#information-masking-in-adaptive-cards) |
|02/19/2021|新增：添加了位置功能。 <br/> 更新：位置功能信息将添加到设备功能概述、本机设备权限、集成媒体功能和 QR 或条形码扫描仪功能文件中。|[概述](concepts/device-capabilities/device-capabilities-overview.md)、 [请求设备权限](concepts/device-capabilities/native-device-permissions.md)、 [集成媒体功能](concepts/device-capabilities/mobile-camera-image-permissions.md)、 [集成 QR 或条形码](concepts/device-capabilities/qr-barcode-scanner-capability.md)扫描仪功能 、 [集成位置功能](concepts/device-capabilities/location-capability.md) |
|02/18/2021|新增：添加了 QR 或条形码扫描仪功能。 <br/> 更新：QR 或条形码扫描仪功能信息已添加到设备功能概述、本机设备权限和集成媒体功能文件中。|[概述](concepts/device-capabilities/device-capabilities-overview.md)、 [请求设备权限](concepts/device-capabilities/native-device-permissions.md)、 [集成媒体功能](concepts/device-capabilities/mobile-camera-image-permissions.md)、 [集成 QR 或条形码扫描仪功能](concepts/device-capabilities/qr-barcode-scanner-capability.md) |
|02/09/2021|新增：添加了设备功能概述。 <br/> 更新：麦克风功能信息将添加到本机设备权限中，并集成媒体功能文件。|[概述](concepts/device-capabilities/device-capabilities-overview.md)、 [请求设备权限](concepts/device-capabilities/native-device-permissions.md) [、集成媒体功能](concepts/device-capabilities/mobile-camera-image-permissions.md)|
|11/30/2020|新增：标识平台与 Teams Toolkit 集成Visual Studio选项卡的代码|[使用 Teams 身份验证和选项卡Toolkit Visual Studio单一登录身份验证](toolkit/visual-studio-code-tab-sso.md)|
|11/16/2020|Teams 应用清单已更新到版本 1.8|[参考：Microsoft Teams 的清单架构](resources/schema/manifest-schema.md)|
|11/10/2020|Teams 机器人设计指南|[机器人设计指南](bots/design/bots.md)|
|9/30/2020|现在支持在移动设备上向机器人发送和接收文件。|[通过自动程序发送和接收文件](resources/bot-v3/bots-files.md)|
|09/22/2020|新的"Teams 入门"指南|[生成首个 Teams 应用概述](build-your-first-app/build-first-app-overview.md)|
|9/18/2020|支持会议中的 Teams 应用 (版本预览) |[在 Teams 会议中创建 Teams](apps-in-teams-meetings/create-apps-for-teams-meetings.md) [会议和应用的应用](apps-in-teams-meetings/teams-apps-in-meetings.md)|
|8/19/2020|使用 Microsoft Graph 导入 Teams 消息|[使用 Microsoft Graph 将第三方平台消息导入 Teams](graph-api/import-messages/import-external-messages-to-teams.md)
| 08/12/2020 |已移动到 GA 的传入 Webhook 中的自适应卡片支持。|[使用传入 webhook 发送自适应卡](~/webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook) |
|08/10/2020|开始构建 Teams 应用及Visual Studio Toolkit。|[使用 Microsoft Teams Toolkit 和 Visual Studio 代码生成应用](toolkit/visual-studio-overview.md) |
|08/06/2020|支持选项卡 SSO 身份验证|[开发 SSO Microsoft Teams 选项卡](tabs/how-to/authentication/auth-aad-sso.md#develop-an-sso-microsoft-teams-tab) |
|07/27/2020 | Graph 公共预览版中的 (自动程序) |[使用 Microsoft Graph 在 Teams 中启用主动机器人安装和主动消息传递](graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)|
| 07/22/2020 |移动设备功能更新。|[请求 Microsoft Teams 选项卡的设备权限](concepts/device-capabilities/native-device-permissions.md) |
|07/20/2020|适用于 AppSource 提交的 Teams 应用验证工具。|[Teams 应用验证工具](concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)
|07/15/2020|为 Teams 创建虚拟助手|[Microsoft Teams 虚拟助手](samples/virtual-assistant.md)|
|07/14/2020|显示本机加载指示器文档|[显示本机加载指示器](tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)
|07/01/2020|开始使用应用代码Visual Studio Teams Toolkit。|[使用 Microsoft Teams Toolkit 和 Visual Studio 代码生成应用](toolkit/visual-studio-code-overview.md) |
|07/01/2020|适用于 Teams Web 和桌面客户端的选项卡 GA 的单一登录|[单Sign-On (SSO) ](tabs/how-to/authentication/auth-aad-sso.md)|
|06/05/2020| 清单架构已更新到版本 1.7| [参考：Microsoft Teams 的清单架构](resources/schema/manifest-schema.md)|
| 05/20/2020 | 使用 Microsoft Graph API 的资源特定许可权限在开发人员预览版中。 |[RSC (特定资源) — 开发者预览版](graph-api/rsc/resource-specific-consent.md) |
|5/18/2020|将 Power Virtual Agents 与 Teams 集成|[将 Power Virtual Agents 聊天机器人与 Microsoft Teams 集成](bots/how-to/add-power-virtual-agents-bot-to-teams.md)|
|04/01/2020|将 WFM 系统与适用于 Teams 的 Shifts 连接器集成|[Microsoft Teams Shifts WFM 连接器](samples/shifts-wfm-connectors.md)
| 03/24/2020 | 添加了对检索对话中单个成员的支持，并添加了对检索分页成员的额外支持。 | [为机器人获取 Teams 上下文](~/bots/how-to/get-teams-context.md)
| 12/26/2019 | 发送到自动程序的有效负载中的参数不再加密，从而允许您使用此值构造到这些消息 `replyToId` 的深层链接。 邮件有效负载包括 参数中的加密值。 `legacy.replyToId`.  |
| 11/5/2019 | 在 Web 内容页面中使用 Teams JavaScript SDK 进行单一登录是开发人员预览版。 | [单一登录](tabs/how-to/authentication/auth-aad-sso.md) |
| 10/31/2019 | 更新了对话机器人和消息传递扩展文档以反映 4.6 Bot Framework SDK。 "资源"部分提供了 v3 SDK 文档。 | 所有机器人和消息传递扩展文档。 |
| 10/31/2019 | 新的文档结构和主要文章重构。 请通过创建 GitHub 问题报告任何死链接或 404。 | 全部都一样！ |
| 9/13/2019 | 从基于操作的消息扩展安装请求自动程序。 | [使用消息传递扩展启动操作](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 8/28/2019 | 支持选项卡和连接器中的私人频道。 | [获取选项卡的上下文](tabs/how-to/access-teams-context.md#retrieving-context-in-private-channels) |
| 06/20/2019 | 从外部网站将外部网站共享到 Teams 频道。 | [共享到 Teams](~/share-to-teams.md) |
| 05/25/2019 | 使用来自任务模块的自动程序消息进行响应。 | [使用来自任务模块的自动程序消息进行响应](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | 群聊中的聊天机器人。 | [在群聊或频道中与机器人交互](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | 应用清单本地化。 | [应用本地化](~/publishing/apps-localization.md) |
| 05/20/2019 | 邮件操作。 | [邮件操作](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | 链接取消 (自定义 URL 预览) 。 | [链接展开](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | 适用于应用商店应用的应用程序认证计划。 | [应用程序认证](~/publishing/application-certification.md) |
| 05/06/2019 | 应用模板现已可用。 | [应用模板](~/samples/app-templates.md) |
| 04/23/2019 | 基于操作的消息扩展现已可用。 | [基于操作的邮件扩展](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | 创建到私人聊天的深层链接已退出开发人员预览，并且不可用。 | [到聊天的深层链接](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 01/23/2019 | 在选项卡上下文中显示 SKU 和 licenceType 信息。 | [选项卡上下文](~/concepts/tabs/tabs-context.md) |
| 11/12/2018 | 群聊中的选项卡现在在 Teams 的已发布版本中可用，并且已退出开发人员预览版。 作为此工作的一部分，为了清楚起见，选项卡部分已进行了重新修改。| [可配置的选项卡](~/concepts/tabs/tabs-configurable.md) |
| 11/11/2018 | 节点 JS 和 .NET/C# 入门已更新为在 Teams 中使用 App Studio，并且添加了关于在 Azure 中托管基于节点的 Teams 应用的新部分。 | [使用 C#/.NET](~/get-started/get-started-dotnet-app-studio.md)和 App Studio 开始在 Microsoft Teams 平台上开始使用 Node JS 和  [App Studio，](~/get-started/get-started-nodejs-app-studio.md)在 Azure 中托管 [Node Teams 应用](~/get-started/get-started-nodejs-in-azure.md)|
| 11/09/2018 | 现在，您可以创建指向用户之间的私人聊天的深层链接。 | [到聊天的深层链接](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 11/08/2018 | SharePoint Framework 1.7 附带了将 Microsoft Teams 选项卡用作 SharePoint 框架 Web 部件的新功能。 | [SharePoint 中的选项卡](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | "任务模块"功能已发布。 任务模块允许你在 Teams 应用程序中从机器人和选项卡创建模式弹出体验。 在弹出窗口中，可以运行自己的自定义 HTML/JavaScript 代码、显示基于小部件（如 YouTube 或 Microsoft Stream 视频）或 `<iframe>` 显示自适应 [卡片](https://docs.microsoft.com/adaptive-cards/)。 | [任务模块概述](~/concepts/task-modules/task-modules-overview.md)， [选项卡中的任务模块](~/concepts/task-modules/task-modules-tabs.md)，  [机器人中的任务模块](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | 卡片的格式设置信息已更新，并且已在适用于 Teams 的桌面版、iOS 和 Android 客户端中进行测试。 | [卡片](~/concepts/cards/cards.md)[、卡片格式](~/concepts/cards/cards-format.md) |
| 09/24/2018 | Microsoft Graph 的通话和联机会议 API 已发布到 beta 版本，Teams 应用现在可以通过多种使用语音和视频的方式与用户进行交互。 | [通话和联机会议](~/concepts/calls-and-meetings/registering-calling-bot.md)机器人、[实时媒体](~/concepts/calls-and-meetings/real-time-media-concepts.md)概念、注册呼叫[](~/concepts/calls-and-meetings/registering-calling-bot.md)机器人、[调试和](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)本地测试、应用程序托管的[媒体](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)、[处理传入呼叫通知](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | 选项卡配置页现在高度明显高。 | [选项卡设计](tabs/design/tabs.md) |
| 08/15/2018 | Teams 现在支持自适应卡片。|[Teams 中的自适应卡片操作](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | 已记录开发人员对 DevTools 的客户端开发者预览版。| [适用于 Microsoft Teams 桌面客户端的 DevTools](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | 邮件扩展现在支持多个命令。 此功能已开发者预览版，现在发布给所有用户。| [composeExtensions.commands](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | 连接器现在支持内联配置。 为了清楚起见，连接器文档也进行了修订和扩展。| [连接器](~/concepts/connectors/connectors.md)|
| 08/06/2018 | 自动程序现在可以发送和接收文件。| [通过自动程序发送和接收文件](~/concepts/bots/bots-files.md)|
| 07/27/2018 | 开发人员预览版现在支持邮件扩展中的多个命令。 | [邮件扩展已扩展](~/resources/dev-preview/developer-preview-features.md)|
| 07/23/2018 | 有关应用重新认证的信息已添加到发布部分。 |[清单权限](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | 在开发人员预览版中，为选项卡配置页面分配了更多空间。 | [选项卡配置页高度明显高于](tabs/design/tabs.md)|
| 07/12/2018 | 有关来宾访问的信息。 | [Microsoft Teams 中的来宾访问](https://docs.microsoft.com/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | 已添加 Microsoft Teams 租户应用程序目录的预发布信息。 | [发布 Microsoft Teams 应用](~/publishing/apps-publish.md)|
| 05/31/2018 | Teams 开发人员预览 (3.6) 更新为包括向群聊添加聊天机器人和选项卡的功能。 | [开发人员预览版中的功能](~/resources/dev-preview/developer-preview-features.md)， [开发人员预览架构](~/resources/schema/manifest-schema-dev-preview.md)|
| 05/29/2018 | Teams 中的自适应卡片操作现在支持自适应 [卡片](task-modules-and-cards/cards/cards-reference.md)。 |
| 05/29/2018 | 如果你使用的是开发人员预览 [版](~/resources/dev-preview/developer-preview-intro.md)，则自动程序现在可以发送和接收文件。| [通过自动程序发送和接收文件](~/concepts/bots/bots-files.md)，Microsoft Teams 公共开发者预览版 [中的功能](~/resources/dev-preview/developer-preview-features.md)|
| 04/17/2018 | replyToID 已添加到 和 card `Invoke` 操作 `MessageBack` 的有效负载中。 如果需要更新卡片操作所来自的邮件，这尤其有用。 | [卡片操作](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | 添加了本主题以跟踪对 Teams 编程接口和此文档集的更改。 | [新增功能](~/whats-new.md)|
| 04/10/2018 | 更改了身份验证 URL，以在路径中统一使用租户 ID。 | [选项卡的身份验证流](~/concepts/authentication/auth-flow-tab.md)[，AAD 选项卡身份验证](~/concepts/authentication/auth-tab-AAD.md)|
| 04/06/2018 | 添加了有关使用命令框的设计准则。 |[命令框](~/resources/design/framework/command-box.md)|
| 04/02/2018 | 使用机器人为应用发送通知。 |[仅限通知的机器人](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | 主动邮件的扩展文档。 |[开始对话](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | 卡片的重构文档。 |[卡片](~/concepts/cards/cards.md)、[卡片操作](~/concepts/cards/cards-actions.md)[、卡片格式、](~/concepts/cards/cards-format.md)[卡片参考](~/concepts/cards/cards-reference.md)|
| 03/03/2018 | 添加了 Teams App Studio 文档。 |[使用 Teams App Studio 快速开发应用](~/get-started/get-started-app-studio.md) [，使用 App Studio 中的控件库](~/get-started/app-studio-component-library.md)|
| 02/27/2018 | 添加了示例代码以演示 AsTeamsChannelAccounts () 方法。 |[获取机器人的背景资料](~/concepts/bots/bots-context.md)|
| 02/05/2018 | 添加了有关开始使用 C#。 |[开始在 Microsoft Teams 平台上使用 C#/.NET ](./get-started/get-started-dotnet-app-studio.md)|

## <a name="submit-your-questions-bugs-feature-requests-and-contributions"></a>提交问题、Bug、功能请求和贡献

我们通过多个渠道听取 [开发人员社区的意见](feedback.md)。
