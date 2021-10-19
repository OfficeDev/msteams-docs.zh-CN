---
title: 最近更新
description: 介绍开发工具中所有新的开发人员Microsoft Teams
ms.topic: reference
ms.localizationpriority: medium
keywords: teams 新增功能
ms.openlocfilehash: 3e2c7a2002192b7d752602f33865aafb12a8239f
ms.sourcegitcommit: ce956267b620f807e15e6d2df7afa022ffacc22f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2021
ms.locfileid: "60496212"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>开发人员在 Microsoft Teams

发现Microsoft Teams GA 版本和开发人员预览版 () 平台功能。

> [!IMPORTANT]
> 现在，可以通过订阅 RSS 源下载Teams获取最新更新[ ![ 。](~/assets/images/RSSfeeds.png)](https://aka.ms/TeamsPlatformUpdates) 有关详细信息，请参阅配置 [RSS 源](#get-latest-updates)。

## <a name="ga-features"></a>GA 功能

Microsoft Teams所有应用开发人员可用的平台功能。

<br>

<details>

<summary><b>2021</b></summary>

| **Date** | **备注** | **已更改的主题** |
| -------- | --------- | ------------------ |
|10/18/2021|选项卡链接取消展开和阶段视图|[选项卡链接取消展开和阶段视图](tabs/tabs-link-unfurling.md) |
|10/08/2021|设计自适应卡片的新最佳做法。|[为应用设计自适应Teams卡片](task-modules-and-cards/cards/design-effective-cards.md)|
|10/05/2021| 隐藏Teams应用程序，直到管理员允许取消隐藏该应用程序。 | [在Teams批准前隐藏应用](concepts/design/enable-app-customization.md#hide-teams-app-until-admin-approves) 
|10/05/2021|规划移动Teams应用|[规划 Teams 移动版的响应式选项卡](concepts/design/plan-responsive-tabs-for-teams-mobile.md)|
|10/04/2021| 新的开发人员门户Teams管理你的 Teams 应用。 | [Teams 开发人员门户](concepts/build-and-test/teams-developer-portal.md) |
|09/21/2021|Teams自动AAD传入 Webhook 的用户提及中支持对象 ID 和 UPN。 |[AAD提及中的对象 ID 和 UPN，](task-modules-and-cards/cards/cards-format.md#format-cards-with-markdown)[卡片 - 概述](task-modules-and-cards/what-are-cards.md#support-for-aad-object-id-and-upn-in-user-mention)|
|09/08/2021|会议阶段现已在 GA 中提供。|[为会议启用和配置Teams应用](apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)|
|08/16/2021| 支持在自适应卡片 (v1.3 上验证所有功能) 和通用操作 (v1.4 支持自动发送的) 。 |[输入验证](/adaptive-cards/authoring-cards/input-validation)， [自适应卡片的通用操作 v1.4](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md) |
|08/09/2021|会议阶段现已在 GA 中提供。|[为会议启用和配置Teams应用](apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)|
|08/30/2021| 自定义一起模式场景功能将参与者合并到单个虚拟场景，并将其视频流放在预先确定的座位中。 | [自定义一起模式场景](~/apps-in-teams-meetings/teams-together-mode.md) |
|08/25/2021| 引入了分步指南，以使用 SSO Teams单一登录 (自动) 。 | [使用 SSO 创建自动程序Teams分步指南](sbs-bots-with-sso.yml) |
|08/19/2021| 安装聊天机器人到对话线程时收到的安装更新事件。 | [安装更新事件](bots/how-to/conversations/subscribe-to-conversation-events.md#installation-update-event) |
|08/12/2021|具有自适应卡片的生成选项卡|[具有自适应卡片的生成选项卡](tabs/how-to/build-adaptive-card-tabs.md)|
|08/04/2021|选项卡将不再具有围绕其体验的边距。  | [删除制表位边距](resources/removing-tab-margins.md) |
|07/08/2021|Teams移动版增加了对会议中应用的支持。 |[会议应用可扩展性](apps-in-teams-meetings/meeting-app-extensibility.md)|
|06/28/2021|集成人员选取器功能。|[集成人员选取器功能](concepts/device-capabilities/people-picker-capability.md)|  
|06/25/2021| 引入了发送主动邮件的分步指南。 | [发送主动邮件的分步指南](sbs-send-proactive.yml) |
|06/09/2021| 自适应卡片中具有 属性的图像的阶段 `allowExpand` 视图。 | [自适应卡片中的图像阶段视图](~/task-modules-and-cards/cards/cards-format.md) |
|05/31/2021| 对话选项卡。 | [开始并继续选项卡中有关内容的对话](~/tabs/how-to/conversational-tabs.md) |
|05/24/2021| 使用Teams等更新了应用设计指南。|[设计Teams应用](~/concepts/design/design-teams-app-overview.md)
|05/13/2021| 添加了有关 mConnect 和 Skooler 的信息。|[可学习管理系统](resources/moodle-overview.md)
|05/10/2021| 应用清单 v1.10 已发布。|[清单架构](resources/schema/manifest-schema.md) |
|05/10/2021| 新的应用自定义功能。| [允许组织自定义应用](concepts/design/enable-app-customization.md) |
|05/07/2021| 聊天中的音频和视频呼叫的深层链接。 |[深度链接](concepts/build-and-test/deep-links.md#deep-linking-to-an-audio-or-audio-video-call) |
|04/30/2021|有关如何将应用发布到应用商店的新Teams指南。|[将应用发布到 Teams 应用商店](concepts/deploy-and-publish/appsource/publish.md) [，Teams应用商店验证指南](concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) |
|04/29/2021 | 对自适应卡片 v1.4 的通用操作的支持。 | [自适应卡的通用操作](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md) |
|04/29/2021 | 用户特定视图。 | [用户特定视图](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/User-Specific-Views.md) |
|04/29/2021 | 顺序工作流。 | [顺序工作流](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/Sequential-Workflows.md) |
|04/29/2021 | 最新卡片。 | [最新卡片](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/Up-To-Date-Views.md) |
|04/08/2021| 应用自定义功能。|[设计团队应用概述](concepts/design/enable-app-customization.md)[、App studio 概述](concepts/build-and-test/app-studio-overview.md#connectors)和[清单架构](resources/schema/manifest-schema-dev-preview.md) |
|03/18/2021|注意：更新到 Bot Framework SDK 版本 4.10 或以上版本，因为我们已开始弃用 `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` 和 的过程。 | [团队/聊天成员的机器人 API 更改](resources/team-chat-member-api-changes.md) |
|03/05/2021|默认安装范围和组功能。| [默认安装范围和组功能](concepts/deploy-and-publish/add-default-install-scope.md) |
|03/05/2021|对个人应用选项卡重新排序。|[对个人应用中的聊天选项卡重新排序](tabs/how-to/create-personal-tab.md#reorder-static-personal-tabs)|
|03/04/2021|自适应卡片中的信息屏蔽。| [自适应卡片中的信息屏蔽](task-modules-and-cards/cards/cards-format.md#information-masking-in-adaptive-cards) |
|02/19/2021|添加了位置功能。 <br/> 位置功能信息将添加到设备功能概述、本机设备权限、集成媒体功能以及 QR 或条形码扫描仪功能文件中。|[概述](concepts/device-capabilities/device-capabilities-overview.md)、 [请求设备权限](concepts/device-capabilities/native-device-permissions.md)、 [集成媒体功能](concepts/device-capabilities/mobile-camera-image-permissions.md)、 [集成 QR 或条形码](concepts/device-capabilities/qr-barcode-scanner-capability.md)扫描仪功能 、 [集成位置功能](concepts/device-capabilities/location-capability.md) |
|02/18/2021|添加了 QR 或条形码扫描仪功能。 <br/> QR 或条形码扫描仪功能信息已添加到设备功能概述、本机设备权限和集成媒体功能文件中。|[概述](concepts/device-capabilities/device-capabilities-overview.md)、 [请求设备权限](concepts/device-capabilities/native-device-permissions.md)、 [集成媒体功能](concepts/device-capabilities/mobile-camera-image-permissions.md)、 [集成 QR 或条形码扫描仪功能](concepts/device-capabilities/qr-barcode-scanner-capability.md) |
|02/09/2021|添加了设备功能概述。 <br/> 麦克风功能信息将添加到本机设备权限中，并集成媒体功能文件。|[概述](concepts/device-capabilities/device-capabilities-overview.md)、 [请求设备权限](concepts/device-capabilities/native-device-permissions.md) [、集成媒体功能](concepts/device-capabilities/mobile-camera-image-permissions.md)|

<br>

</details>

<br>

<details>
  
<summary><b>2020</b></summary>

| **Date** | **备注** | **已更改的主题** |
| -------- | --------- | ------------------ |
|11/30/2020|标识平台与选项卡Teams Toolkit和Visual Studio Code集成。|[使用选项卡的 Teams Toolkit 和 Visual Studio Code 单一登录身份验证](toolkit/visual-studio-code-tab-sso.md)|
|11/16/2020|Teams更新到版本 1.8 的应用清单。|[参考：Microsoft Teams](resources/schema/manifest-schema.md)|
|11/10/2020|Teams自动程序设计指南。|[机器人设计指南](bots/design/bots.md)|
|09/30/2020|现在支持在移动设备上向机器人发送和接收文件。|[通过自动程序发送和接收文件](resources/bot-v3/bots-files.md)|
|09/22/2020|开发入门的新Teams。|[生成首个Teams应用概述](build-your-first-app/build-first-app-overview.md)|
|09/18/2020|支持会议Teams应用 (发布预览) 。|[创建用于会议Teams](apps-in-teams-meetings/create-apps-for-teams-meetings.md)[应用和应用Teams会议](apps-in-teams-meetings/teams-apps-in-meetings.md)|
|08/19/2020|使用 Microsoft Teams 导入Graph。|[使用 Microsoft Graph 将第三方平台消息导入 Teams](graph-api/import-messages/import-external-messages-to-teams.md)
|08/12/2020 |已移动到 GA 的传入 Webhook 中的自适应卡片支持。|[使用传入 webhook 发送自适应卡](~/webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook) |
|08/10/2020|使用 Teams 开始构建Visual Studio Toolkit。|[使用 Microsoft Teams Toolkit 和 Visual Studio Code](toolkit/visual-studio-overview.md) |
|08/06/2020|支持选项卡 SSO 身份验证。|[开发 SSO Microsoft Teams选项卡](tabs/how-to/authentication/auth-aad-sso.md#develop-an-sso-microsoft-teams-tab) |
|07/27/2020 | Graph公共预览版中 (主动聊天机器人) 。|[在 Microsoft Teams 中启用主动自动程序安装和主动Graph](graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)|
|07/22/2020 |移动设备功能更新。|[为"用户"选项卡请求Microsoft Teams权限](concepts/device-capabilities/native-device-permissions.md) |
|07/20/2020|TeamsAppSource 提交的应用验证工具。|[Teams应用验证工具](concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
|07/15/2020|为虚拟助理创建Teams。|[虚拟助理Microsoft Teams](samples/virtual-assistant.md)|
|07/14/2020|显示本机加载指示器文档。|[显示本机加载指示器](tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)
|07/01/2020|使用 Teams 开始构建Visual Studio Code Toolkit。|[使用 Microsoft Teams Toolkit 和 Visual Studio Code](toolkit/visual-studio-code-overview.md) |
|07/01/2020|适用于 Web 和桌面客户端的选项卡 GA Teams单一登录。|[单Sign-On (SSO) ](tabs/how-to/authentication/auth-aad-sso.md)|
|06/05/2020| 清单架构已更新到版本 1.7。| [参考：Microsoft Teams](resources/schema/manifest-schema.md)|
|05/18/2020|将Power Virtual Agents与Teams。|[将聊天Power Virtual Agents聊天机器人与Microsoft Teams](bots/how-to/add-power-virtual-agents-bot-to-teams.md)|
|04/01/2020|将 WFM 系统与 Shifts Connector for Teams。|[Microsoft TeamsShifts WFM 连接器](samples/shifts-wfm-connectors.md)
|03/24/2020 | 添加了对检索对话中单个成员的支持，并添加了对检索分页成员的额外支持。 | [为机器人获取 Teams 上下文](~/bots/how-to/get-teams-context.md) |

<br>

</details>

<br>

<details>
  
<summary><b>2019</b></summary>

| **Date** | **备注** | **已更改的主题** |
| -------- | --------- | ------------------ |
| 12/26/2019 | 发送到自动程序的有效负载中的参数不再加密，从而允许您使用此值构造到这些消息 `replyToId` 的深层链接。 邮件有效负载包括参数 中的加密值 `legacy.replyToId` 。  |
| 11/05/2019 | 使用 JavaScript SDK Teams单一登录。 | [单一登录](tabs/how-to/authentication/auth-aad-sso.md) |
| 10/31/2019 | 对话机器人和消息扩展文档已更新，以反映 4.6 Bot Framework SDK。 "资源"部分提供了 v3 SDK 文档。 | 所有机器人和消息传递扩展文档。 |
| 10/31/2019 | 新的文档结构和主要文章重构。 请通过创建问题报告任何死链接或 404 GitHub问题。 | 全部都一样！ |
| 09/13/2019 | 从基于操作的消息扩展安装请求自动程序。 | [使用消息传递扩展启动操作](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 08/28/2019 | 支持选项卡和连接器中的私人频道。 | [获取选项卡的上下文](tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels) |
| 06/20/2019 | 从外部网站将外部网站共享到外部Teams通道。 | [共享到Teams](~/share-to-teams.md) |
| 05/25/2019 | 使用来自任务模块的自动程序消息进行响应。 | [使用来自任务模块的自动程序消息进行响应](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | 群聊中的聊天机器人。 | [在群聊或频道中与机器人交互](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | 应用清单本地化。 | [应用本地化](~/publishing/apps-localization.md) |
| 05/20/2019 | 邮件操作。 | [邮件操作](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | 链接取消 (自定义 URL 预览) 。 | [链接展开](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | 适用于应用商店应用的应用程序认证计划。 | [应用程序认证](~/concepts/deploy-and-publish/appsource/post-publish/overview.md#complete-microsoft-365-certification) |
| 05/06/2019 | 应用模板现已可用。 | [应用模板](~/samples/app-templates.md) |
| 04/23/2019 | 基于操作的消息扩展现已可用。 | [基于操作的邮件扩展](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | 创建到私人聊天的深层链接。 | [到聊天的深层链接](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 01/23/2019 | 在选项卡上下文中显示 SKU 和 licenceType 信息。 | [选项卡上下文](~/concepts/tabs/tabs-context.md) |

<br>

</details>

<br>

<details>

<summary><b>2018</b></summary>

| **日期** | **备注** | **已更改的主题** |
| -------- | --------- | ------------------ |
| 11/12/2018 | 群聊中的选项卡现在在 Teams 的Teams。 作为此工作的一部分，为清楚起见，选项卡部分已进行了重新修改。| [可配置的选项卡](~/concepts/tabs/tabs-configurable.md) |
| 11/11/2018 | Node JS 和 .NET/C# 入门已更新为使用 Teams 中的 App Studio，并且添加了一个新部分，以在 Azure 中托管基于 Node Teams 应用。 | [开始使用 Microsoft Teams 平台使用 C#/.NET](~/get-started/get-started-dotnet-app-studio.md)和 App Studio，开始在 Microsoft Teams 平台上使用[Node JS 和 App Studio，](~/get-started/get-started-nodejs-app-studio.md)在 Azure 中托管节点 Teams[应用](~/get-started/get-started-nodejs-in-azure.md)|
| 11/09/2018 | 现在，您可以创建指向用户之间的私人聊天的深层链接。 | [到聊天的深层链接](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 11/08/2018 | SharePoint 框架 1.7 版附带了一项新功能，Microsoft Teams选项卡作为 SharePoint 框架 Web 部件。 | [选项卡SharePoint](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | 任务 **模块功能** 已发布。 任务模块允许你从自动程序和选项卡在 Teams应用程序中创建模式弹出体验。 在弹出窗口中，可以运行自己的自定义 HTML/JavaScript 代码、显示基于小部件（如 YouTube 或 Microsoft Stream 视频）或 `<iframe>` 显示自适应 [卡片](/adaptive-cards/)。 | [任务模块概述](~/concepts/task-modules/task-modules-overview.md)， [选项卡中的任务模块](~/concepts/task-modules/task-modules-tabs.md)，  [机器人中的任务模块](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | 卡片的格式设置信息已在桌面、iOS 和 Android 客户端中进行了更新和测试，Teams。 | [卡片](~/concepts/cards/cards.md)[、卡片格式](~/concepts/cards/cards-format.md) |
| 09/24/2018 | 适用于 Microsoft Graph 的呼叫和联机会议 API 已发布到 beta 版本，Teams应用现在可以通过多种使用语音和视频的方式与用户进行交互。 | [通话和联机会议](~/concepts/calls-and-meetings/registering-calling-bot.md)机器人、[实时媒体](~/concepts/calls-and-meetings/real-time-media-concepts.md)概念、注册呼叫[](~/concepts/calls-and-meetings/registering-calling-bot.md)机器人、[调试和](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)本地测试、应用程序托管的[媒体](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)、[处理传入呼叫通知](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | 选项卡配置页面现在高度明显高。 | [选项卡设计](tabs/design/tabs.md) |
| 08/15/2018 | 自适应卡片现在受 Teams。|[自适应卡片操作Teams](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | 对 DevTools 的客户端支持。| [适用于桌面客户端Microsoft Teams DevTools](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | 邮件扩展现在支持多个命令。 | [composeExtensions.commands](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | 连接器现在支持内联配置。 为了清楚起见，连接器文档也进行了修订和扩展。| [连接器](~/concepts/connectors/connectors.md)|
| 08/06/2018 | 自动程序现在可以发送和接收文件。| [通过自动程序发送和接收文件](~/bots/how-to/bots-filesv4.md)|
| 07/23/2018 | 有关应用重新认证的信息已添加到发布部分。 |[清单权限](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | 为选项卡配置页分配了更多空间。 | [选项卡配置页高度明显高于](tabs/design/tabs.md)|
| 07/12/2018 | 有关来宾访问的信息。 | [Microsoft Teams 中的来宾访问](/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | 已添加Microsoft Teams租户应用程序目录的信息。 | [发布Microsoft Teams应用](~/publishing/apps-publish.md)|
| 05/29/2018 | 自适应卡片在 Teams。 | [自适应卡片操作Teams](task-modules-and-cards/cards/cards-reference.md) |
| 04/17/2018 | replyToID 已添加到 和 card `Invoke` 操作 `MessageBack` 的有效负载中。 如果需要更新卡片操作所来自的邮件，这尤其有用。 | [卡片操作](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | 添加了本主题以跟踪对Teams接口和本文档集的更改。 | [新增功能](~/whats-new.md)|
| 04/10/2018 | 更改了身份验证 URL，以在路径中统一使用租户 ID。 | [选项卡身份验证、选项卡](~/concepts/authentication/auth-flow-tab.md)AAD[身份验证的身份验证流](~/concepts/authentication/auth-tab-AAD.md)|
| 04/06/2018 | 添加了有关使用命令框的设计准则。 |[命令框](~/resources/design/framework/command-box.md)|
| 04/02/2018 | 使用机器人为应用发送通知。 |[仅限通知的机器人](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | 主动邮件的扩展文档。 |[开始对话](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | 卡片的重构文档。 |[卡片](~/concepts/cards/cards.md)、[卡片操作](~/concepts/cards/cards-actions.md)[、卡片格式、](~/concepts/cards/cards-format.md)[卡片参考](~/concepts/cards/cards-reference.md)|
| 03/03/2018 | 添加了 App Studio Teams文档。 |[使用 App Studio 中的Teams](~/get-started/get-started-app-studio.md)库快速开发[App Studio 应用](~/get-started/app-studio-component-library.md)|
| 02/27/2018 | 添加了示例代码以演示 AsTeamsChannelAccounts () 方法。 |[获取机器人的背景资料](~/concepts/bots/bots-context.md)|
| 02/05/2018 | 添加了有关开始使用 C#。 |[开始在 Microsoft Teams 平台上使用 C#/.NET ](./get-started/get-started-dotnet-app-studio.md)|

<br>

</details>

## <a name="developer-preview"></a>开发者预览版

开发人员预览是一个公共计划，可提前访问未发布Teams功能。  

| **日期** | **备注** | **已更改的主题** |
| -------- | --------- | ------------------ |
|10/19/2021|浏览器的设备权限。| [浏览器的设备权限](concepts/device-capabilities/browser-device-permissions.md) |
|10/14/2021 | 通过可交易Teams SaaS 产品来盈利你的应用。 | [将 SaaS 产品与你的Teams一起](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)。 |
|06/23/2021| 会议详细信息 API 和实时Teams会议事件。 | [创建适用于 Teams 会议的应用](~/apps-in-teams-meetings/API-references.md#meeting-details-api) |
|06/21/2021|使用自动程序卸载个人应用的行为 | [使用自动程序卸载个人应用中的行为更新](bots/how-to/conversations/subscribe-to-conversation-events.md#uninstall-behavior-for-personal-app-with-bot)|
|06/16/2021| 聊天的特定于资源的同意。 |[特定于资源的同意](graph-api/rsc/resource-specific-consent.md)，[测试资源特定的许可权限Teams](graph-api/rsc/test-resource-specific-consent.md)|
|05/25/2021| 针对 Teams Toolkit 和[Visual Studio](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)更新[Visual Studio Code。](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit&ssr=false#overview) | [应用开发Teams入门](~/get-started/prerequisites.md) |
|05/24/2021|自动程序可以使用 RSC (特定同意接收所有) 。|[使用 RSC、机器人](~/bots/how-to/conversations/channel-messages-with-rsc.md)对话[概述](~/bots/how-to/conversations/conversation-basics.md)、[频道和组对话](~/bots/how-to/conversations/channel-and-group-conversations.md)以及[开发人员预览](~/resources/schema/manifest-schema-dev-preview.md)清单架构接收所有消息 |

有关详细信息，请参阅[公共开发人员预览版Teams。](~/resources/dev-preview/developer-preview-intro.md)

## <a name="teams-app-template-catalog"></a>Teams应用程序模板目录

除了新功能之外，我们还提供[生产](samples/app-templates.md)就绪Teams模板，你可以立即部署这些模板或根据需要进行修改。 新添加的模板用星号表示 。

## <a name="submit-your-feedback"></a>提交反馈

我们鼓励Teams开发人员提问、提交 Bug、提交功能请求并做出贡献。 可以通过任何可用渠道 [提交反馈](feedback.md)。

## <a name="get-latest-updates"></a>获取最新更新

You can get the latest Teams platform updates by configuring to the [RSS feed](https://aka.ms/TeamsPlatformUpdates).

**配置 RSS 源**

1. 打开 Microsoft Teams。
1. Select **Teams** from the left pane.
1. 选择团队中的频道。
1. 选择省略号 &#x25CF;&#x25CF;&#x25CF; ，然后从下拉列表 **中选择连接器**。
1. 在出现的 **"** 连接器 **"** 对话框中搜索 RSS。
1. 选择"**配置"。**
1. 在"输入 **RSS 连接的名称"中输入名称。**
1. 输入 **https://aka.ms/TeamsPlatformUpdates** RSS **源的地址**。
1. 从"摘要频率"下拉列表 **中选择源** 的频率。
1. 选择“保存”。
