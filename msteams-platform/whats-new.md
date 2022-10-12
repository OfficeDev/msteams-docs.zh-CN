---
title: Teams 中面向开发人员的新增功能和更新
description: 了解新的 Microsoft Teams 开发人员功能以及对现有功能的更新、弃用说明和更改。 订阅 RSS 源以获取最新更新。
ms.topic: reference
ms.localizationpriority: high
zone_pivot_groups: What-new-features
ms.openlocfilehash: 07a4edf8751707a9ae0268b05b0314c85f471209
ms.sourcegitcommit: 20070f1708422d800d7b1d84b85cbce264616ead
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2022
ms.locfileid: "68537575"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>Microsoft Teams 中面向开发人员的新增功能

::: zone pivot="ga-feature"

发现正式发布 (正式版) 的 Microsoft Teams 平台功能。 现在可以通过订阅 RSS 源[![下载源](~/assets/images/RSSfeeds.png)](https://aka.ms/TeamsPlatformUpdates)来获取最新的 Teams 平台更新。 有关详细信息，请参阅[配置 RSS 源](#get-latest-updates)。

## <a name="generally-available"></a>正式发布

:::row:::
:::column:::

:::image type="icon" source="~/assets/images/general-availabe.png":::

:::column-end:::
:::column span="2":::

适用于所有应用开发人员的 Microsoft Teams 平台功能。

**2022 年 9 月**

* ***2022 年 9 月 30*** 日： [管理 Teams 中第三方应用的 SaaS 许可证](concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md#manage-license-for-third-party-apps-in-teams)
* ***2022 年 9 月 29*** 日： [Teams 移动应用现在支持将文件下载到本地设备。](concepts/device-capabilities/media-capabilities.md#file-download-on-teams-mobile)
* ***2022 年 9 月 16*** 日： [基于搜索的消息扩展插件中的自适应卡片现在支持通用操作。](messaging-extensions/how-to/search-commands/universal-actions-for-search-based-message-extensions.md)
* ***2022 年 9 月 6*** 日： [引入了用于通过 `selectMedia` API 使用相机捕获视频的代码片段。](concepts/device-capabilities/media-capabilities.md#code-snippets)

:::column-end:::
:::row-end:::

<br>
<details>
<summary><b>2022</b></summary>

| **Date** | **更新** | **在此处查找** |
| -------- | --------- | ----------------|
| 08/09/2022 | 为 Visual Studio 2022 引入了 Teams 工具包 | 工具和 SDK > 适用于 Visual Studio 的 Teams 工具包 > [适用于 Visual Studio 的 Teams 工具包概述](toolkit/teams-toolkit-overview-visual-studio.md) |
| 2022/08/03 | 从个人应用或选项卡共享到 Teams | 与 Teams 集成 > 共享到 Teams > [从个人应用或选项卡共享到 Teams](concepts/build-and-test/share-to-teams-from-personal-app-or-tab.md) |
| 2022/08/03 | 添加了在会议后场景中检索会议脚本的功能。 | 为 Teams 会议和通话构建应用 > 使用 Graph API 获取会议脚本 > [概述](graph-api/meeting-transcripts/overview-transcripts.md) |
| 2022/08/03 | 将展开共享链接到 Web 应用中的团队 | 与 Teams >“共享到 Teams”集成> [从 Web 应用共享到 Teams](concepts/build-and-test/share-to-teams-from-web-apps.md) |
| 08/01/2022| 注意：开发人员门户现已正式发布，App Studio 自 2022 年 8 月 1 日开始弃用。 | 工具和 SDK >[Teams 开发人员门户](concepts/build-and-test/teams-developer-portal.md) |
| 07/28/2022 | 为会议内通知添加 Teams 显示图片和人员卡片| 为 Teams 会议和通话构建应用>为会议启用和配置应用>[会议内通知](apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md#in-meeting-notification) |
| 07/28/2022 | 在 Teams 中构建共享频道 | 为 Teams 会议和通话构建应用>[共享频道](concepts/build-and-test/Shared-channels.md) |
| 07/28/2022|引入的应用清单 v1.14| 应用部件清单> [Teams 的应用部件清单架构](resources/schema/manifest-schema.md)|
| 2022/07/26|建议的机器人操作| “生成机器人”>“机器人对话”>“[机器人对话中的消息](bots/how-to/conversations/conversation-messages.md#send-suggested-actions)”|
| 07/21/2022 | 引入了发送活动源通知的分步指南 | 设计应用> UI 组件>活动源通知> [发送活动源通知](sbs-graphactivity-feedbroadcast.yml) |
| 2022/07/08| 用于通过对话和安装更新事件将用户在应用安装期间选择的通道 ID 发送到机器人的更新 |  生成机器人>机器人对话> Teams 机器人中的对话事件> [Teams 机器人中的对话事件](bots/how-to/conversations/subscribe-to-conversation-events.md) |
| 06/16/2022 | 更新了支持桌面和移动设备的媒体功能| 集成设备功能 > [集成媒体功能](concepts/device-capabilities/media-capabilities.md)|
| 06/08/2022 | 成功消息的可选卡片反馈| “生成机器人”>“机器人对话”>“[机器人对话中的消息](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)”|
| 06/03/2022 | 更新了添加身份验证模块，用于使用新的结构和过程为选项卡应用启用 SSO | 添加身份验证 > 选项卡 > [在选项卡应用中启用单一登录](tabs/how-to/authentication/tab-sso-overview.md) |
| 2022 年 5 月 24 日 | 快速批准发布链接到 SaaS 产品/服务的应用的其他提示 | 发布到 Teams 应用商店>概述>[快速批准发布链接到 SaaS 产品/服务的应用的其他提示](~/concepts/deploy-and-publish/appsource/publish.md#additional-tips-for-rapid-approval-to-publish-your-app-linked-to-a-saas-offer) |
| 2022 年 5 月 24 日 | 将已启用 Outlook 和 Office 的应用提交到 Teams 应用商店 | 在 Microsoft 365 中扩展应用>[概述](m365-apps/overview.md) |
| 2022 年 5 月 24 日 | TeamsJS 版本 2.0.0 中的应用指南和新增功能| 工具和 SDK > [Teams JavaScript 客户端 SDK](tabs/how-to/using-teams-client-sdk.md)  |
| 2022 年 5 月 24 日 | 适用于 Visual Studio Code 的 Teams 工具包版本 4.0.0 现已正式发布 | 工具和 SDK > 适用于 Visual Studio Code 的 Teams 工具包 > <br> •  [Teams 工具包概述](toolkit/teams-toolkit-fundamentals.md) <br> • [使用 JavaScript 生成命令机器人](toolkit/add-capability.md) <br> • [使用 JavaScript 生成通知机器人](toolkit/add-capability.md) <br> • [预览并自定义 Teams 应用清单](toolkit/TeamsFx-preview-and-customize-app-manifest.md) <br> • [连接到现有 API](toolkit/add-API-connection.md) <br> • [将功能添加到 Teams 应用](toolkit/add-capability.md) <br> • [添加单一登录体验](toolkit/add-single-sign-on.md) <br> • [将云资源添加到 Teams 应用](toolkit/add-resource.md) |
| 2022 年 5 月 24 日 | 已引入应用清单版本 1.13 | 应用清单> [Microsoft Teams 的清单架构](resources/schema/manifest-schema.md) |
| 5/24/2022|GCC 和 GCCH 中的机器人和消息扩展| • 规划应用 > [概述](concepts/app-fundamentals-overview.md#government-community-cloud) </br> • 生成机器人 > [概述](bots/what-are-bots.md) </br> • 生成邮件扩展 > [概述](messaging-extensions/what-are-messaging-extensions.md) |
|2022/04/26|使用机器人卸载个人应用的行为 | 生成机器人>机器人对话>[使用机器人在个个人应用程序中卸载行为更新](bots/how-to/conversations/subscribe-to-conversation-events.md#uninstall-behavior-for-personal-app-with-bot)|
| 2022/04/22 | 针对盈利应用的测试预览 | 使应用盈利 > [盈利应用的测试预览](concepts/deploy-and-publish/appsource/prepare/test-preview-for-monetized-apps.md)
| 2022/04/22 | 应用内购买流，用于盈利应用 | 使应用盈利 > [应用内购买](concepts/deploy-and-publish/appsource/prepare/in-app-purchase-flow.md)
| 04/28/2022 | 应用验证失败的常见原因 | 将应用>发布到 Teams 应用商店> [应用验证失败的常见原因](concepts/deploy-and-publish/appsource/common-reasons-for-app-validation-failure.md)|
| 2022/04/20 |  设置 CI/CD 管道 | 工具和 SDK >用于 Visual Studio Code 的 Teams 工具包>[设置 CI/CD 管道](toolkit/use-CICD-template.md)|
| 2022 年 4 月 19 日 | 在 Microsoft Teams 中上传应用 | 分发应用 > [上传应用](concepts/deploy-and-publish/apps-upload.md)|
| 2022 年 4 月 1 日 | 引入了创建 Teams 对话机器人的分步指南| “声称机器人”>“机器人对话”>“频道和组对话”>“[创建 Teams 对话机器人的分步指南](sbs-teams-conversation-bot.yml)” |
| 2022 年 3 月 30 日 | 已使用选项卡和机器人更新 Blazor 应用入门模块|  开始 > [使用 Blazor 生成第一个应用](sbs-gs-blazorupdate.yml)|
| 2022 年 3 月 30 日 | 浏览器的设备权限 | “集成设备功能”>“[浏览器的设备权限](concepts/device-capabilities/browser-device-permissions.md)” |
| 2022 年 3 月 29 日 |集成人员选取器 | “与 Teams 集成”>“[与人员选取器集成](concepts/device-capabilities/people-picker-capability.md)”
| 2022 年 3 月 23 日 | 介绍了在 Teams 中使用机器人展开链接的分步指南 | 生成邮件扩展>添加链接展开功能>[在 Teams 中使用机器人展开链接](sbs-botbuilder-linkunfurling.yml)|  
| 2022 年 3 月 22 日 | 添加了有关调试过程的信息| • 工具和 SDK > Teams Toolkit Visual Studio Code > [在本地调试 Teams 应用](toolkit/debug-local.md) </br> • 工具和 SDK > Teams Toolkit Visual Studio Code > [调试后台进程](toolkit/debug-background-process.md)|
| 2022 年 3 月 14 日 | 介绍了在 Microsoft Teams 中生成和测试连接器的分步指南 | 生成 Webhook 和连接器 > 创建 Office 365 连接器 > [生成 Teams 连接器](sbs-teams-connectors.yml)|
| 03/10/2022 | 添加了有关 Moodle LMS 和 Microsoft 365 插件的信息 | 与 Teams 集成> Moodle LMS >[Moodle 学习管理系统](resources/moodle-overview.md)|  
| 2022/03/03 | 如何使用外部 OAuth 提供程序添加身份验证| 添加身份验证 > 选项卡 > [使用外部 OAuth 提供程序](tabs/how-to/authentication/auth-oauth-provider.md) |
| 2022/02/25 | 引入了在 Teams 中调用任务模块的分步指南| 生成卡片和任务模块 > 生成任务模块 > 使用机器人中的任务模块 > [从 Teams 中调用任务模块](sbs-botbuilder-taskmodule.yml)|
| 2022/02/24| 引入了生成基于操作的邮件扩展的分步指南 | 生成邮件扩展>操作命令>定义操作命令>[生成基于操作的邮件扩展](sbs-meetingextension-action.yml)|
| 2022/02/24 | 引入了生成基于搜索的邮件扩展的分步指南 | 生成邮件扩展>搜索命令>定义搜索命令>[生成基于搜索的邮件扩展](sbs-messagingextension-searchcommand.yml)|
| 2022/02/24 | 引入了创建传出 Webhook 的分步指南 | 生成 Webhook 和连接器 > 创建传出 Webhook > [创建传出 Webhook](sbs-outgoing-webhooks.yml)|
| 2022/02/23 | Microsoft Teams 应用商店排名参数| 分发应用 > 发布到 Teams 应用商店 > [Microsoft Teams 应用商店排名参数](concepts/deploy-and-publish/appsource/post-publish/teams-store-ranking-parameters.md)|
| 2022/02/18 | 为 Microsoft Teams 开发人员文档引入了广泛的术语表，可帮助你快速找到有关术语的定义 | [术语表](~/get-started/glossary.md) |
| 2022/02/18 | 更新了概述模块，用于将 Teams 应用映射到组织目标、用户情景和探索 Teams 应用功能 | [概述 > 适合的 Teams 应用](overview.md) |
| 2022/02/18 | 更新了应用基础知识模块以规划应用，以包括将用例映射到 Teams 功能和应用规划清单 | [规划应用 > 概述](~/concepts/app-fundamentals-overview.md) |
| 02/17/2022 | 提交应用后会发生什么？| 分发应用>发布到 Teams 应用商店>[概述](concepts/deploy-and-publish/appsource/publish.md) |
| 02/15/2022 | 介绍了如何将文件从机器人上传到 Teams 的分步指南 | 生成机器人>发送和接收文件>[如何将文件从机器人上传到 Teams 的分步指南](sbs-file-handling-in-bot.yml) |
| 2022 年 2 月 11 日 | 共享会议演示区域| • 为 Teams 会议生成应用 >[共享会议阶段](apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md#shared-meeting-stage) </br> • 为 Teams 会议生成应用 > [会议应用 API 参考](apps-in-teams-meetings/API-references.md) </br> • 应用清单 > 公共开发人员预览 > [开发人员预览清单架构](resources/schema/manifest-schema-dev-preview.md)|
| 02/08/2022 | 引入创建通话和会议机器人的分步指南。| 生成机器人 >通话和会议机器人 >注册通话和会议机器人 >[创建通话和会议机器人的分步指南](sbs-calling-and-meeting.yml) |
| 02/02/2022 | 引入了应用清单版本 1.12 | 应用清单> [应用程序清单架构](resources/schema/manifest-schema.md) |
| 2022/01/25 | 发送实时字幕 API | 生成 Teams 会议应用 > 会议应用 API 参考 > [会议应用 API 引用](apps-in-teams-meetings/API-references.md#send-real-time-captions-api)|
| 01/19/2022 | 自适应卡片表单完成反馈 | 生成机器人 >机器人对话 >机器人对话中的消息 >[Form 完成反馈](bots/how-to/conversations/conversation-messages.md#form-completion-feedback)|
| 01/17/2022 | 适用于桌面的自适应卡片中的人员选取器 | 生成卡片和任务模块>生成卡片> [自适应卡片中的人员选取器](task-modules-and-cards/cards/people-picker.md)|

</details>
</br>
<details>
<summary><b>较旧的更新</b></summary>

浏览此处列出的以前 GA 版本的更新。

</br>
<details>
<summary><b>2021</b></summary>

| **Date** | **更新** | **在此处查找** |
| -------- | --------- | ----------------|
|12/24/2021| 引入了授予 Tab 设备权限的分步指南 | 应用基础>设备功能>[授予 Tab 设备权限的分步指南](sbs-tab-device-permissions.yml) |
|12/23/2021| 引入使用自适应卡片创建选项卡的分步指南。| 添加身份验证>选项卡>使用 SSO 身份验证> [分步指南创建具有自适应卡片的选项卡](sbs-tab-with-adaptive-cards.yml) |
|12/21/2021 | 已更新 Teams 工具包 3.0.0 的 JavaScript、C# 和 Node.js 模块入门。 | • 开始>[使用 JavaScript 生成第一个应用](sbs-gs-javascript.yml) <br> • 入门>使用[ C# 或 .NET 生成第一个应用](sbs-gs-csharp.yml) <br> • 入门>[使用 Node.js 生成第一个应用](sbs-gs-nodejs.yml) |
|12/20/2021| 引入了使用单一登录 (SSO) 的选项卡和邮件扩展的分步指南 | 添加身份验证>选项卡>使用 SSO 身份验证>[选项卡和邮件扩展的 SSO 分步指南](sbs-tabs-and-messaging-extensions-with-SSO.yml)|
|12/20/2021| 引入了创建会议内容气泡的分步指南 | 生成 Teams 会议应用>为会议启用和配置应用> [创建会议内容气泡的分步指南](sbs-meeting-content-bubble.yml) |
|12/09/2021| 引入了会议演示区域视图的分步指南 | 生成会议 Teams 应用>为会议启用和配置应用>[创建会议阶段视图的分步指南](sbs-meetings-stage-view.yml)|
|12/13/2021 | 针对链接到 SaaS 产品/服务的应用引入了指南 | 发布应用>发布到 Teams 应用商店>查看应用商店验证指南>[链接到 SaaS 产品/服务的应用指南](concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#apps-linked-to-saas-offer)|
|12/09/2021| 引入了创建会议侧窗格的分步指南 | 生成用于 Teams 会议的应用>启用和配置会议应用>[在 Teams 中创建会议侧窗格的分步指南](sbs-meetings-sidepanel.yml)|
|12/01/2021 | 引入了新应用商店图标 | • 设计应用>应用功能>[为 Microsoft Teams 设计个人应用](concepts/design/personal-apps.md)</br> • 设计应用> UI 组件>[使用高级 UI 组件设计 Microsoft Teams 应用](concepts/design/design-teams-app-advanced-ui-components.md) |
|11/24/2021| 引入了生成会议令牌的分步指南 | 生成用于 Teams 会议>启用和配置会议应用>[在 Teams 中创建会议令牌的分步指南](sbs-meeting-token-generator.yml)|
|11/17/2021| 更新 Microsoft Teams 应用商店验证指南|[应用商店验证指南](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)|
|11/17/2021| 桌面和移动用户的静态和动态键入式搜索 | • 生成卡片和任务模块>生成卡片> [自适应卡片内的提前输入搜索](task-modules-and-cards/cards/dynamic-search.md) </br> • 生成卡片和任务模块>生成卡片>概述>[自适应卡片内的提前输入搜索](task-modules-and-cards/what-are-cards.md#type-ahead-search-in-adaptive-cards) </br> • 生成卡片和任务模块>概述>[卡片和任务模块概述](task-modules-and-cards/cards-and-task-modules.md)|
|11/13/2021| 可以启用机器人以使用特定于资源的许可 （RSC） 接收所有通道消息 | • 生成机器人>机器人对话>机器人对话消息>[使用 RSC 接收所有通道消息](~/bots/how-to/conversations/channel-messages-with-rsc.md) </br> • 生成机器人>机器人对话> [机器人对话概述](~/bots/how-to/conversations/conversation-basics.md) </br> • 生成机器人>机器人对话> [频道和组对话](~/bots/how-to/conversations/channel-and-group-conversations.md) |
|10/28/2021| 使用可交易的 SaaS 产品/服务使 Teams 应用盈利 | 发布应用>发布到 Teams 应用商店>[在 Teams 应用程序中包含 SaaS 产品/服务](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md) |
|10/25/2021| 通过分步指南中的新结构和过程更新了 Microsoft Teams 开发人员文档的入门模块 | 入门>[你的第一个 Teams 应用入门](get-started/get-started-overview.md) |
|10/20/2021| 会议演示区域现已在 GA 中提供 | 生成用于 Teams 会议的应用>[启用和配置 Teams 会议应用](apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md) |
|10/20/2021| 会议详细信息 API 和实时 Teams 会议事件 | 为 Teams 会议生成应用 > [获取会议详细信息 API](apps-in-teams-meetings/API-references.md#get-meeting-details-api) |
|10/18/2021| 选项卡链接展开和演示区域视图 | 生成选项卡>[选项卡链接展开和阶段视图](tabs/tabs-link-unfurling.md) |
|10/08/2021| 设计自适应卡片的新最佳做法 | 设计应用> UI 组件>[为 Teams 应用设计自适应卡片](task-modules-and-cards/cards/design-effective-cards.md) |
|10/05/2021| 隐藏 Teams 应用，直到管理员允许取消隐藏应用 | 默认情况下，设计应用> [阻止用户的应用，直到管理员批准](concepts/design/enable-app-customization.md#block-apps-by-default-for-users-until-an-admin-approves) |
|10/05/2021| 规划适用于 Teams 移动设备的应用 | 应用基础知识>[规划 Teams 移动的响应式选项卡](concepts/design/plan-responsive-tabs-for-teams-mobile.md) |
|10/04/2021| 引入了用于管理 Teams 应用的新 Teams 开发人员门户 | 工具和 SDK >[Teams 开发人员门户](concepts/build-and-test/teams-developer-portal.md) |
|09/21/2021|对于机器人和传入 Webhook，Teams 在用户提及中支持 Azure AD 对象 ID 和 UPN | • 生成卡片和任务模块>生成卡片>[用户提及的 Azure AD 对象 ID 和 UPN](task-modules-and-cards/what-are-cards.md#support-for-azure-ad-object-id-and-upn-in-user-mention) </br> • 生成卡片和任务模块>生成卡片> [卡片- 概述](task-modules-and-cards/cards/cards-format.md#format-cards-with-markdown) |
|08/16/2021| 支持在自适应卡片上进行输入验证（适用于所有功能的 v1.3）和通用操作（适用于机器人发送卡的 v1.4） | • 自适应卡>创作卡> [输入验证](/adaptive-cards/authoring-cards/input-validation)</br> • 生成卡片和任务模块>生成卡>自适应卡的通用操作>[适用于自适应卡片 v1.4 的通用操作](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md) |
|08/30/2021| "自定义在一起模式"场景功能将参与者合并到单个虚拟场景中，并将其视频流置于预先确定的席位中 | 为 Teams 会议生成应用> [“自定义在一起模式”场景](~/apps-in-teams-meetings/teams-together-mode.md) |
|08/25/2021| 引入了创建具有单一登录 (SSO) 的 Teams 机器人的分步指南。 | 添加身份验证>机器人> [使用 SSO 创建 Teams 机器人的分步指南](sbs-bots-with-sso.yml) |
|08/19/2021| 将机器人安装到对话线程时，收到安装更新事件。 | 生成机器人>机器人对话> [安装更新事件](bots/how-to/conversations/subscribe-to-conversation-events.md#installation-update-event) |
|08/12/2021|具有自适应卡片的生成选项卡| 生成选项卡> [具有自适应卡片生成选项卡](tabs/how-to/build-adaptive-card-tabs.md) |
|08/04/2021|选项卡的体验周围将不再有边距 | 生成选项卡> [删除选项卡边距](resources/removing-tab-margins.md) |
|07/08/2021|Teams 移动版在会议中添加对应用的支持 | 为 Teams 会议生成应用>[会议应用扩展性](apps-in-teams-meetings/meeting-app-extensibility.md) |
|06/28/2021|集成人员选取器功能 | 与 Teams 集成>[与人员选取器功能集成](concepts/device-capabilities/people-picker-capability.md) |  
|06/25/2021| 引入了发送主动消息的分步指南 | 生成机器人>机器人对话>主动消息>[发送主动消息的分步指南](sbs-send-proactive.yml) |
|06/09/2021| 自适应卡片中具有 `allowExpand` 属性的图像的演示区域视图 | 生成卡片和任务模块>自适应卡片>[自适应卡片内的图像阶段视图](task-modules-and-cards/cards/cards-format.md#stage-view-for-images-in-adaptive-cards) |
|05/31/2021| 对话选项卡 | 生成选项卡> [开始和继续有关选项卡中内容的对话](~/tabs/how-to/conversational-tabs.md) |
|05/24/2021| 使用移动模式更新了 Teams 应用设计准则 | 设计应用>[设计 Teams 应用](~/concepts/design/design-teams-app-overview.md) |
|05/13/2021| 已添加有关 mConnect 和 Skooler 的信息 | 与 Teams 集成> Moodle LMS >[Moodle 学习管理系统](resources/moodle-overview.md)|
|05/10/2021| 应用清单 v1.10 已发布 | 应用清单> [清单架构](resources/schema/manifest-schema.md) |
|05/10/2021| 新应用自定义功能 | 设计应用> [启用组织以自定义应用](concepts/design/enable-app-customization.md) |
|05/07/2021| 聊天中的音频和视频通话的深层链接 | 与 Teams 集成>[深度链接](concepts/build-and-test/deep-links.md#navigate-to-an-audio-or-audio-video-call) |
|04/30/2021|有关如何将应用发布到 Teams 应用商店的新指南 | • 发布到 Teams 应用商店>[将应用发布到 Teams 应用商店](concepts/deploy-and-publish/appsource/publish.md)</br> • 发布到 Teams 应用商店>[ Teams 应用商店验证指南](concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) |
|04/29/2021 | 对自适应卡片 v1.4 的通用操作的支持 | 生成卡片和任务模块>生成卡片>自适应卡片的通用操作> [自适应卡片的通用操作](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md) |
|04/29/2021 | 用户特定视图 | 生成卡片和任务模块>生成卡片>自适应卡片的通用操作> [用户特别视图](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/User-Specific-Views.md) |
|04/29/2021 | 顺序工作流 | 生成卡片和任务模块>生成卡片>自适应卡片的通用操作> [顺序工作流](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/Sequential-Workflows.md) |
|04/29/2021 | 最新卡片 | 生成卡片和任务模块>生成卡片>自适应卡片的通用操作> [最新卡片](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/Up-To-Date-Views.md) |
|04/08/2021| 应用自定义功能 | • 设计应用> [设计团队应用概述](concepts/design/enable-app-customization.md)</br>  • 工具和 SDK > [开发人员门户](concepts/build-and-test/teams-developer-portal.md) </br> • 应用清单>公共开发人员预览> [清单架构](resources/schema/manifest-schema-dev-preview.md) |
|03/18/2021| 注意：更新到 Bot Framework SDK 版本 4.10 或以上版本，因为我们已开始弃用 `TeamsInfo.getMembers`和`TeamsInfo.GetMembersAsync`。 | 生成机器人> [团队/聊天成员的机器人 API 更改](resources/team-chat-member-api-changes.md) |
|03/05/2021|默认安装范围和组功能 | 分配应用> [默认安装范围和组功能](concepts/deploy-and-publish/add-default-install-scope.md) |
|03/05/2021|对个人应用选项卡重新排序 | 生成选项卡> [个人应用中的聊天选项卡重新排序](tabs/how-to/create-personal-tab.md#reorder-static-personal-tabs) |
|03/04/2021|自适应卡片中的信息屏蔽 | 生成卡片和任务模块>生成卡片> [自适应卡片中的信息屏蔽](task-modules-and-cards/cards/cards-format.md#information-masking-in-adaptive-cards) |
|02/19/2021|添加了位置功能。 <br/> 在设备功能概述、本机设备权限、集成媒体功能以及 QR 或条形码扫描仪功能文件中添加位置功能信息 | • 应用基础>设备功能> [概述](concepts/device-capabilities/device-capabilities-overview.md) </br> • 应用基础>设备功能> [请求设备权限](concepts/device-capabilities/native-device-permissions.md) </br> • 应用基础>设备功能> [与媒体功能集成](concepts/device-capabilities/media-capabilities.md) </br> • 应用基础>设备功能>[将 QR 或条形码扫描程序功能集成](concepts/device-capabilities/qr-barcode-scanner-capability.md) </br> • 应用基础>设备功能>[与位置功能集成](concepts/device-capabilities/location-capability.md) |
|02/18/2021|添加了 QR 或条形码扫描仪功能。 <br/> QR 或条形码扫描仪功能信息已添加到设备功能概述、本机设备权限和集成媒体功能文件中 | • 应用基础>设备功能> [概述](concepts/device-capabilities/device-capabilities-overview.md) </br> • 应用基础>设备功能> [请求设备权限](concepts/device-capabilities/native-device-permissions.md) </br> • 应用基础>设备功能> [与媒体功能集成](concepts/device-capabilities/media-capabilities.md) </br> • 应用基础>设备功能>[将 QR 或条形码扫描程序功能集成](concepts/device-capabilities/qr-barcode-scanner-capability.md) |
|02/09/2021|添加了设备功能概述。 <br/> 已将麦克风功能信息添加到本机设备权限和集成媒体功能文件中 |• 应用基础>设备功能> [概述](concepts/device-capabilities/device-capabilities-overview.md) </br> 应用基础> • 设备功能> [请求设备权限](concepts/device-capabilities/native-device-permissions.md) </br> • 应用基础>设备功能> [与媒体功能集成](concepts/device-capabilities/media-capabilities.md)|

<br>

</details>

<br>

<details>
<summary><b>2020</b></summary>

| **Date** | **更新** | **在此处查找** |
| -------- | --------- | ------------------ |
|11/30/2020|标识平台与 Teams 工具包和 Visual Studio Code 选项卡集成 |[使用选项卡的 Teams 工具包和 Visual Studio Code 单一登录身份验证](toolkit/add-single-sign-on.md)|
|11/16/2020|Teams 应用清单更新到版本 1.8。|[参考：Microsoft Teams 的清单架构](resources/schema/manifest-schema.md)|
|11/10/2020|Teams 机器人设计准则 |[机器人设计指南](bots/design/bots.md)|
|09/30/2020|现在支持在移动设备上向机器人发送和接收文件 |[通过机器人发送和接收文件](resources/bot-v3/bots-files.md)|
|09/22/2020|Teams 开发入门的新信息 |[生成首个 Teams 应用概述](build-your-first-app/build-first-app-overview.md)|
|09/18/2020|支持会议内 Teams 应用 (发布预览版) |[Teams 会议中的应用](apps-in-teams-meetings/teams-apps-in-meetings.md)|
|08/19/2020|使用 Microsoft Graph 导入 Teams 消息 |[使用 Microsoft Graph 将第三方平台消息导入 Teams](graph-api/import-messages/import-external-messages-to-teams.md)
|08/12/2020 |自适应卡片传入 Webhook 中的支持已移至 GA |[使用传入 webhook 发送自适应卡](~/webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook) |
|08/10/2020|开始使用 Visual Studio 工具包构建 Teams 应用 |[使用 Microsoft Teams 工具包和Visual Studio Code 生成应用](toolkit/visual-studio-overview.md) |
|08/06/2020|支持选项卡 SSO 身份验证 |[开发 SSO Microsoft Teams 选项卡](tabs/how-to/authentication/tab-sso-overview.md) |
|07/27/2020 | 图形主动机器人和消息 (公共预览版) |[使用 Microsoft Graph 在 Teams 中启用主动机器人安装和主动消息传送](graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)|
|07/22/2020 |移动设备功能更新 |[Microsoft Teams 选项卡请求设备权限](concepts/device-capabilities/native-device-permissions.md) |
|07/20/2020|适用于 AppSource 提交的 Teams 应用验证工具 |[Teams 应用验证工具](concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
|07/15/2020|为 Teams 创建虚拟助理 |[Microsoft Teams 虚拟助理](samples/virtual-assistant.md)|
|07/14/2020|显示本机加载指示器文档 |[显示本机加载指示器](tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)
|07/01/2020|开始使用 Visual Studio Code 工具包构建 Teams 应用 |[使用 Microsoft Teams 工具包和Visual Studio Code 生成应用](sbs-gs-javascript.yml) |
|07/01/2020|适用于 Teams Web 和桌面客户端的选项卡 GA 的单一登录 |[单一登录 (SSO)](tabs/how-to/authentication/tab-sso-overview.md)|
|06/05/2020| 清单架构已更新到版本 1.7。| [参考：Microsoft Teams 的清单架构](resources/schema/manifest-schema.md)|
|05/18/2020|将 Power Virtual Agents 与 Teams 集成 |[将 Power Virtual Agents 聊天机器人与 Microsoft Teams 集成](bots/how-to/add-power-virtual-agents-bot-to-teams.md)|
|04/01/2020|将 WFM 系统与适用于 Teams 的排班连接器集成 |[Microsoft Teams Shifts WFM 连接器](samples/shifts-wfm-connectors.md)
|03/24/2020 | 已添加对检索会话单个成员的支持，以及对检索分页成员的其他支持 | [为机器人获取 Teams 上下文](~/bots/how-to/get-teams-context.md) |

<br>

</details>

<br>

<details>
  
<summary><b>2019</b></summary>

| **Date** | **更新** | **在此处查找** |
| -------- | --------- | ------------------ |
| 12/26/2019 | The `replyToId` parameter in payloads sent to a bot is no longer encrypted, allowing you to use this value to construct deeplinks to these messages. Message payloads include the encrypted values in the parameter `legacy.replyToId`.  |
| 11/05/2019 | 使用 Teams JavaScript SDK 的单一登录。 | [单一登录](tabs/how-to/authentication/tab-sso-overview.md) |
| 10/31/2019 | 已更新对话机器人和邮件扩展文档，以反映 4.6 Bot Framework SDK。 有关 v3 SDK 的文档，请参阅"资源"部分。 | 所有机器人和邮件扩展文档 |
| 10/31/2019 | 新的文档结构和主要文章重构。 请通过创建 GitHub 问题来报告任何死链接或 404。 | 全部都一样！ |
| 09/13/2019 | 请求机器人是从基于操作的邮件扩展安装的。 | [使用邮件扩展启动操作](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 08/28/2019 | 支持选项卡和连接器中的私人频道。 | [获取选项卡的上下文](tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels) |
| 06/20/2019 | 将外部网站（从外部网站）共享到 Teams 频道。 | [共享到 Teams](concepts/build-and-test/share-to-teams-overview.md)。 |
| 05/25/2019 | 使用来自任务模块的机器人消息进行响应。 | [使用来自任务模块的机器人消息进行响应。](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | 群聊中的机器人。 | [在群组聊天或频道中与机器人交互](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | 应用清单本地化。 | [应用本地化](~/publishing/apps-localization.md) |
| 05/20/2019 | 邮件操作。 | [邮件操作](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | 链接取消 (自定义 URL 预览) 。 | [链接展开](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | 适用于应用商店应用的应用程序认证计划。 | [应用程序认证](~/concepts/deploy-and-publish/appsource/post-publish/overview.md#complete-microsoft-365-certification) |
| 05/06/2019 | 应用模板现已可用 | [应用模板](~/samples/app-templates.md) |
| 04/23/2019 | 基于操作的邮件扩展现已可用。 | [基于操作的邮件扩展](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | 创建到私人聊天的深层链接。 | [到聊天的深层链接](concepts/build-and-test/deep-links.md#navigate-to-a-chat) |
| 01/23/2019 | 在选项卡上下文中显示 SKU 和 licenceType 信息。 | [选项卡上下文](~/concepts/tabs/tabs-context.md) |
|
</details>

<br>

<details>
<summary><b>2018</b></summary>

| **Date** | **更新** | **在此处查找** |
| -------- | --------- | ------------------ |
| 11/12/2018 | 群聊中的选项卡现已在发布的 Teams 版本中提供。 作为此工作的一部分，为了清楚起见，选项卡部分已重新工作。| [可配置的选项卡](~/concepts/tabs/tabs-configurable.md) |
| 11/09/2018 | 现在，可以创建指向用户之间的私人聊天的深层链接。 | [到聊天的深层链接](concepts/build-and-test/deep-links.md#navigate-to-a-chat) |
| 11/08/2018 | SharePoint Framework 1.7 随附了一项新功能，可将 Microsoft Teams 选项卡用作 SharePoint 框架 Web 部件。 | [SharePoint 中的选项卡](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | 已发布 **任务模块** 功能。 任务模块允许在 Teams 应用程序中从机器人和选项卡创建模式弹出体验。 在弹出窗口中，你可以运行自己自定义的 HTML/JavaScript 代码，显示基于 `<iframe>`的小组件，如 YouTube 或 Microsoft Stream 视频，或显示[自适应卡片](/adaptive-cards/)。 | [任务模块概述](~/concepts/task-modules/task-modules-overview.md)，[选项卡中的任务模块](~/concepts/task-modules/task-modules-tabs.md)，[机器人中的任务模块](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | 卡片的格式设置信息已在适用于 Teams 的桌面、iOS 和 Android 客户端中进行了更新和测试。 | [卡片](~/concepts/cards/cards.md)、[卡片格式](~/concepts/cards/cards-format.md) |
| 09/24/2018 | 适用于 Microsoft Graph 的通话和联机会议 API 已发布到 beta 版本，Teams 应用现在可以通过多种使用语音和视频的方式与用户进行交互。 | [通话和联机会议机器人](~/concepts/calls-and-meetings/registering-calling-bot.md)、[实时媒体概念](~/concepts/calls-and-meetings/real-time-media-concepts.md)、[注册呼叫机器人](~/concepts/calls-and-meetings/registering-calling-bot.md)、[调试和本地测试](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)、[应用程序托管的媒体](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)、[处理传入呼叫通知](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | 选项卡配置页面现在明显增高。 | [选项卡设计](tabs/design/tabs.md) |
| 08/15/2018 | Teams 现在支持自适应卡片。|[在 Teams 中自适应卡操作](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | 对 DevTools 的客户端支持。| [ Microsoft Teams 桌面客户端的 DevTools](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | 邮件扩展现在支持多个命令。 | [composeExtensions.commands](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | 连接器现在支持内联配置。 为了清楚起见，还修改和扩展了连接器文档。| [连接器](~/concepts/connectors/connectors.md)|
| 08/06/2018 | 机器人现在可以发送和接收文件。 | [通过机器人发送和接收文件](~/bots/how-to/bots-filesv4.md)|
| 07/23/2018 | 有关应用重新认证的信息已添加到“发布”部分。 |[清单权限](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | 为选项卡配置页面分配更多空间。 | [选项卡配置页高度明显增高](tabs/design/tabs.md)|
| 07/12/2018 | 有关来宾访问的信息。 | [Microsoft Teams 中的来宾访问](/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | 已添加 Microsoft Teams 租户应用程序目录的信息。 | [发布 Microsoft Teams 应用](~/publishing/apps-publish.md)|
| 05/29/2018 | Teams 现在支持自适应卡片。 | [在 Teams 中自适应卡操作](task-modules-and-cards/cards/cards-reference.md) |
| 04/17/2018 | replyToID 已添加到 `Invoke` 和 `MessageBack` 卡操作的有效负载中。 如果需要更新卡片邮件发出操作，这尤其有用。 | [卡片操作](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | 添加了本主题以跟踪对 Teams 编程界面和此文档集的更改。 | [新增功能](~/whats-new.md)|
| 04/10/2018 | 更改了身份验证 URL，以在路径中统一使用租户 ID。 | [选项卡身份验证流](~/concepts/authentication/auth-flow-tab.md)、[Azure AD 选项卡身份验证](~/concepts/authentication/auth-tab-AAD.md)|
| 04/06/2018 | 添加了有关使用命令框的设计准则。 |[命令框](~/resources/design/framework/command-box.md)|
| 04/02/2018 | 使用机器人为应用发送通知。 |[仅限通知的机器人](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | 主动邮件传送的扩展文档。 |[开始对话](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | 卡片的重构文档。 |[卡片](~/concepts/cards/cards.md)、[卡片操作](~/concepts/cards/cards-actions.md)、[卡片格式](~/concepts/cards/cards-format.md)、[卡片参考](~/concepts/cards/cards-reference.md)|
| 02/27/2018 | 添加了示例代码以演示 AsTeamsChannelAccounts () 方法。 |[获取机器人的背景资料](~/concepts/bots/bots-context.md)|
| 02/05/2018 | 添加了有关开始使用 C# 的主题。 |[开始在 Microsoft Teams 平台上使用 C#/.NET ](./get-started/get-started-dotnet-app-studio.md)|
|
</details>
</details>
</details>

::: zone-end

::: zone pivot="dev-preview"

发现开发人员预览版中的 Microsoft Teams 平台功能。 现在可以通过订阅 RSS 源[![下载源](~/assets/images/RSSfeeds.png)](https://aka.ms/TeamsPlatformUpdates)来获取最新的 Teams 平台更新。 有关详细信息，请参阅[配置 RSS 源](#get-latest-updates)。

## <a name="developer-preview"></a>开发者预览版

:::row:::
:::column:::

:::image type="icon" source="~/assets/images/developer-preview.png":::

:::column-end:::
:::column span="2":::

开发人员预览是一个公共计划，可提前访问未发布 Teams 功能。

**2022 年 10 月**

***2022 年 10 月 11*** 日： [生成一个深度链接以共享内容以在会议中登台。](apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md#generate-a-deep-link-to-share-content-to-stage-in-meetings)

:::column-end:::
:::row-end:::

| **Date** | **更新** | **在此处查找** |
| -------- | --------- | ------------------ |
| 09/23/2022 | 引入了对计划频道会议的会议应用支持。 | 为 Teams 会议和呼叫构建应用> [统一会议应用](apps-in-teams-meetings/meeting-app-extensibility.md) |
| 08/23/2022 | 在移动设备中将应用共享到 Teams 会议阶段 | 为 Teams 会议和呼叫构建应用> [为会议启用和配置应用](/microsoftteams/platform/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings) |
| 08/10/2022 | 计划公共频道会议的应用 | 为 Teams 会议和通话构建应用 > [概述](apps-in-teams-meetings/teams-apps-in-meetings.md) |
| 2022/08/03 | 在 Teams 会议阶段将应用的 API 静音和取消静音 | 为 Teams 会议和通话生成应用 > [会议应用 API 参考](/microsoftteams/platform/apps-in-teams-meetings/api-references?tabs=dotnet) |
| 08/02/2022| Teams 协作控制| 与 Teams > [协作控件集成](samples/collaboration-control.md) |
| 2022/06/30 | 用于即时会议、一对一和群组通话的应用| 为 Teams 会议和通话构建应用 > [概述](apps-in-teams-meetings/teams-apps-in-meetings.md)|
|2022 年 5 月 24 日| 通过 Live Share SDK 增强协作 | 构建 Teams 会议应用>通过 Live Share 增强协作>[概述](apps-in-teams-meetings/teams-live-share-overview.md) |
| 02/03/2022 | 已引入应用清单版本 1.13 | 应用清单 > 公共开发人员预览 > [清单架构](resources/schema/manifest-schema-dev-preview.md) |
| 01/17/2022 | 适用于移动的自适应卡片中的人员选取器 | 生成卡片和任务模块>生成卡片> [自适应卡片中的人员选取器](task-modules-and-cards/cards/people-picker.md)|
| 10/28/2021 |可以启用机器人以使用特定于资源的许可 （RSC） 接收所有通道消息 | • 生成机器人>机器人对话> [机器人对话概述](~/bots/how-to/conversations/conversation-basics.md) </br> • 生成机器人>机器人对话> [频道和组对话](~/bots/how-to/conversations/channel-and-group-conversations.md) |
| 06/16/2021 | 聊天的特定资源许可 | • 利用 Microsoft Graph 的 Teams 数据>[特定资源许可](graph-api/rsc/resource-specific-consent.md) </br> • 测试你的应用> Microsoft Graph >[测试 Teams 中资源特定许可权限](graph-api/rsc/test-resource-specific-consent.md)|

有关详细信息，请参阅[ Teams 公共开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)。

::: zone-end

::: zone pivot="dep-feature"

发现已弃用的 Microsoft Teams 平台功能。 现在可以通过订阅 RSS 源[![下载源](~/assets/images/RSSfeeds.png)](https://aka.ms/TeamsPlatformUpdates)来获取最新的 Teams 平台更新。 有关详细信息，请参阅[配置 RSS 源](#get-latest-updates)。

## <a name="deprecated"></a>不推荐使用

:::row:::
:::column:::

:::image type="icon" source="~/assets/images/deprecated.png":::

:::column-end:::
:::column span="2":::

Microsoft Teams 平台功能不可用。

**2022 年 8 月**

***2022 年 8 月 1*** 日：已弃用 App Studio，使用 Teams [开发人员门户](concepts/build-and-test/teams-developer-portal.md) 。

:::column-end:::
:::row-end:::

::: zone-end

## <a name="teams-app-template-catalog"></a>Teams 应用程序模板目录

Along with new features, we also provide [production-ready Teams app templates](samples/app-templates.md) that you can deploy right away or modify to your needs. Newly added templates are indicated with a star ☆.

## <a name="submit-your-feedback"></a>提交反馈

我们鼓励 Teams 开发人员提问、提交 Bug、提交功能请求和做出贡献。 可以通过任何可用渠道 [提交反馈](feedback.md)。

## <a name="get-latest-updates"></a>获取最新更新

可以通过配置到 [RSS 源](https://aka.ms/TeamsPlatformUpdates)来获取最新的 Teams 平台更新。

### <a name="to-configure-rss-feed"></a>配置 RSS 源

1. 打开 Microsoft Teams。
1. 从左窗格中选择“**Teams**”。
1. 选择团队中的频道。
1. 选择省略号 &#x25CF;&#x25CF;&#x25CF; ，然后从下拉列表中选择 **“连接器**”。
1. 在出现的 “**连接器**” 对话框中搜索 **RSS**。
1. 选择“**配置**”。
1. 在“**输入RSS 连接器的名称”中输入名称。**
1. 在 RSS 源的 **地址中输入 **<https://aka.ms/TeamsPlatformUpdates>****。
1. 从“**摘要频率**”下拉列表中选择源 的频率。
1. 选择“保存”。
