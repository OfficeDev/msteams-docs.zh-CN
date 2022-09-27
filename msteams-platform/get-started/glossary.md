---
title: Microsoft Teams 开发人员文档 - 术语表
description: 了解 Microsoft Teams 开发人员文档中使用的术语
ms.localizationpriority: high
ms.topic: reference
ms.openlocfilehash: c8a9a663244803efb113c09857e21523218108d2
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027324"
---
# <a name="glossary"></a>术语表

Teams 开发人员文档中使用的常用术语和定义。

## <a name="a"></a>A

| Term | 定义 |
| --- | --- |
| [操作命令](../messaging-extensions/how-to/action-commands/define-action-command.md) | 一种使用弹出窗口收集或显示信息的邮件扩展应用。 <br>**另请参阅**：[邮件扩展](#m)；[搜索命令](#s) |
| [自适应卡](../task-modules-and-cards/what-are-cards.md) | 由自动程序或邮件扩展添加到对话的可操作内容片段。 将文本、图形和按钮与这些卡片配合使用，以进行丰富的通信。 |
| [匿名用户](../apps-in-teams-meetings/meeting-app-extensibility.md#user-types-in-a-meeting) | A type of participant in a Teams meeting who doesn't have an Azure AD identity and isn't federated with a tenant. They are like external users in a meeting. <br>**另请参阅**：[联合用户](#f) |
| [应用程序目录](../toolkit/publish.md) | 存储 SharePoint 和 Office 应用以供组织内部使用的网站。 <br>**另请参阅**：[SPFx](#s) |
| [应用部件清单](../resources/schema/manifest-schema.md) | Teams 应用清单介绍了应用如何集成到 Microsoft Teams 产品中。 清单必须符合 [清单架构](https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json)。 |
| [应用包](../concepts/build-and-test/apps-package.md) | Teams 应用包是一个 zip 文件，其中包含应用清单文件、颜色图标和大纲图标。 |
| [应用权限](../concepts/device-capabilities/browser-device-permissions.md#enable-apps-device-permissions) | Teams 应用中用于启用设备权限的选项。 仅当应用的清单文件声明应用需要设备权限时，此选项才可用。 <br> **另请参阅**： [设备权限](#d) |
| [应用程序范围](../concepts/design/understand-use-cases.md#app-scope) | Teams 中用户可以使用你的应用的区域。 应用可以有一个或多个范围，包括个人、频道、聊天和会议。 Teams 应用可以跨范围存在。 |
| 应用托盘 | 位于 Teams 移动应用底部栏上的应用程序托盘。 它收集已打开但当前未使用或处于活动状态的所有应用。 <br>**另请参阅**：[Teams 移动](#t) |
| [Azure 资源](../toolkit/provision.md) | 通过 Azure 提供的服务，Teams 应用可将其用于 Azure 部署。 它可以是存储帐户、Web 应用、数据库等。 |
| [Azure Active Directory](../tabs/how-to/authentication/auth-tab-aad.md) | Microsoft 基于云的标识和访问管理服务。 它可帮助经过身份验证的用户访问内部和外部资源。 |
| [身份验证](../concepts/authentication/authentication.md) | 验证用户标识以访问应用的过程。 <br> **另请参阅**：[标识提供者](#i)；[SSO](#s) |
| [身份验证流](../concepts/authentication/authentication.md) | 用户对应用进行身份验证的方式。 对于 Teams 应用，我们建议使用 Azure Active Directory (AAD) 使用单一登录 (SSO) ，但另一种方法是使用第三方 OAuth 提供程序。|

## <a name="b"></a>B

| Term | 定义 |
| --- | --- |
| [Blazor](../get-started/get-started-overview.md) | A free and open-source web framework that enables developers to create web apps using C# and HTML. It's being developed by Microsoft. |
| [Bicep](../toolkit/provision.md) | 声明性语言，这意味着元素可以按任意顺序显示。 与命令性语言不同，元素的顺序不会影响部署的处理方式。 |
| [Bot](../bots/what-are-bots.md) | 机器人是执行已编程重复性任务的应用。 <br> **另请参阅**：[对话机器人](#c)；[聊天机器人](#c) |
| [机器人仿真器](../bots/how-to/debug/locally-with-an-ide.md#use-the-bot-emulator) | 一个桌面应用程序，可用于在本地或远程测试和调试机器人。 |
| [机器人框架](../bots/bot-features.md) | 一种丰富的 SDK，用于使用 C#、Java、Python 和 JavaScript 创建机器人。 如果你具有基于 Bot Framework 的机器人，则可以对其进行修改以在 Teams 中工作。 |

## <a name="c"></a>C

| Term | 定义 |
| --- | --- |
| [调用机器人](../bots/calls-and-meetings/calls-meetings-bots-overview.md) | 参与音频或视频通话和联机会议的机器人。 <br> **另请参阅**：[聊天机器人](#c)；[会议机器人](#m) |
| [功能](../toolkit/add-capability.md) | 可在应用中构建，以便与应用用户进行交互的 Teams 功能。 应用功能用于扩展 Teams 以满足应用需求。 应用可能具有一个或多个核心功能，例如选项卡、机器人和邮件扩展。 <br>**另请参阅**：[设备功能](#d)；[媒体功能](#m) |
| [聊天机器人](../bots/how-to/conversations/conversation-basics.md) | 机器人也称为聊天机器人或对话机器人。 它是一个应用，可为客户服务或支持人员等用户运行简单且重复的任务。 <br> **另请参阅**：[对话机器人](#c) |
| 频道 | 团队共享消息、工具和文件的单个位置。 可以使用频道进行团队合作和沟通。 <br>**另请参阅**：[对话](#c) |
| [客户端密码](../bots/how-to/authentication/add-authentication.md) | 应用程序在请求令牌时用来证明其标识的机密字符串。 此外，它可称为应用程序密码。|
| [云资源](../toolkit/add-resource.md) | 通过 Internet 在云上提供的服务，Teams 应用可以使用该服务。 它可以是存储帐户、Web 应用、数据库等。 |
| [协作与应用](../concepts/extensibility-points.md) | 具有可供用户在协作工作区中与其他用户一起工作的功能的应用。 <br> **另请参阅**：[独立应用](#s) |
| [撰写扩展](../resources/schema/manifest-schema.md#composeextensions) | 应用清单 (`composeExtensions`) 中引用邮件扩展功能的属性。 该属性用于当扩展需要进行身份验证或配置以继续时。 <br>**另请参阅**：[应用清单](#a)；[邮件扩展](#m) |
| [CommandBox](../resources/schema/manifest-schema.md) | 应用清单中的一种上下文类型 (`commandBox`)，可以将其配置为从 Teams 命令框中调用邮件扩展。 |
| [Connector](../webhooks-and-connectors/what-are-webhooks-and-connectors.md) | 使用连接器，用户可以订阅以接收来自 Web 服务的通知和消息。 连接器公开服务的 HTTPS 终结点，以便将消息发布到 Teams 频道，通常采用卡片形式。 <br> **另请参阅**：[Webhook](#w) |
| 对话 | Microsoft Teams 应用（选项卡或机器人）与一个或多个用户之间发送的一系列消息。 对话可以有三个范围：频道、个人聊天和群组聊天。 <br>**另请参阅**：[一对一聊天](#o)；[群组聊天](#g)；[频道](#c) |
| [对话机器人](../bots/how-to/conversations/conversation-messages.md) |  它允许用户使用文本、交互式卡片和任务模块与 Web 服务进行交互。 <br>**另请参阅** [聊天机器人](#c) |

## <a name="d"></a>D

| Term | 定义 |
| --- | --- |
| [深层链接](../concepts/build-and-test/deep-links.md) | 在 Teams 应用中，可以创建指向 Teams 中信息和功能的深层链接，或创建帮助用户导航到应用中内容的深层链接。 |
|[国防部 (DOD)](../concepts/app-fundamentals-overview.md#government-community-cloud)| DoD 环境符合国防部安全要求准则、国防联邦采购条例补充 (DFARS) 以及 ITAR)  (国际武器流量条例。|
| [Teams 开发人员门户](../concepts/build-and-test/teams-developer-portal.md) | 用于配置、分发和管理 Microsoft Teams 应用的主要工具。 借助开发人员门户，可以在应用上与同事协作、设置运行时环境等。 |
| [开发人员预览版](../resources/dev-preview/developer-preview-intro.md) | 面向开发人员的公共计划，提供对 Microsoft Teams 中未发布功能的早期访问权限。 通过此计划，可以探索和测试可能包含在 Microsoft Teams 应用中的即将推出的功能。 |
| 部署 | 用于上传应用程序后端和前端代码的过程。 在部署时，应用的代码将复制到预配期间创建的资源。 <br>**另请参阅**：[预配](#p) |
| [设备功能](../concepts/device-capabilities/device-capabilities-overview.md) | 内置设备，如移动设备或桌面设备中的相机、麦克风、条形码扫描程序、照片库。 可以通过 Microsoft Teams JavaScript 客户端 SDK 中提供的专用 API 在移动设备或桌面设备上访问以下设备功能。 <br>**另请参阅**：[功能](#c)；[媒体功能](#m)；[位置功能](#l) |
| [设备权限](../concepts/device-capabilities/browser-device-permissions.md) | 可在应用中配置的 Teams 应用设置。 可用于请求应用访问权限和利用本机设备功能的权限。 可以在 Teams 设置中管理设备权限。 <br>**另请参阅**：[应用权限](#a) |
| [开发环境](../toolkit/TeamsFx-multi-env.md#create-new-environment) | Teams 工具包默认创建的开发环境类型。 它表示远程或云环境配置。 一个项目可以有多个远程环境。 可以使用 Teams 工具包向项目添加更多开发环境。 <br>**另请参阅** [环境](#e)；[本地环境](#l) |
| [DevTools](../tabs/how-to/developer-tools.md) | 浏览器的 DevTools 用于查看控制台日志、查看或修改运行时网络请求、将断点添加到代码 (JavaScript)，以及对 Teams 应用执行交互式调试。 该功能仅在启用开发人员预览版后才适用于桌面和 Android 客户端。 |
| [动态搜索](../task-modules-and-cards/cards/dynamic-search.md#dynamic-typeahead-search) | 一种适用于自适应卡片的搜索功能，对于从大型数据集中搜索和选择数据非常有用。 它有助于在用户输入搜索字符串时筛选出选项。 <br>**另请参阅**：[静态搜索](#s) |

## <a name="e"></a>E

| Term | 定义 |
| --- | --- |
| [E5 开发人员帐户](../toolkit/tools-prerequisites.md#accounts-to-build-your-teams-app) | 用于构建应用以扩展 Microsoft 365 的 E5 开发人员订阅。 包括仅用于开发用途的 25 个用户许可证（包括管理员）。  <br>**另请参阅**：[Microsoft 365 帐户](#m) |
| [入口点](../concepts/app-fundamentals-overview.md) | Teams 应用的访问点，例如团队、频道和聊天，用户可在其中使用你的应用。 |
| [环境](../toolkit/teamsfx-multi-env.md) | Teams 工具包中的一项功能，可用于为应用项目创建和使用多个开发环境。 Teams 工具包默认创建两个开发环境：本地环境和开发环境。 <br>**另请参阅**：[本地环境](#l)；[开发环境](#d) |

## <a name="f"></a>F

| Term | 定义 |
| --- | --- |
| [联合用户](../apps-in-teams-meetings/meeting-app-extensibility.md#user-types-in-a-meeting) | Teams 应用会议中来自外部且受邀加入会议的用户类型。 此用户具有由经授权的 Teams 合作伙伴联合的有效凭据。 他们也被称为外部用户。 <br>**另请参阅**：[匿名用户](#a) |
| [首次运行体验](../concepts/design/design-teams-app-ui-templates.md)|首次运行的体验 (FRE) 是用户对产品的介绍。FRE 可帮助用户开始使用产品的功能、功能和优势，并影响用户返回并继续使用你的产品。|

## <a name="g"></a>G

| Term | 定义 |
| --- | --- |
|[政府社区云 (GCC) ](../concepts/app-fundamentals-overview.md#government-community-cloud)| GCC 环境符合联邦对云服务的要求，包括 FedRAMP High、国防联邦采购条例补充 (DFARS) ，以及 (CJI 和 FTI 数据类型) 的刑事司法和联邦税务信息系统的要求。|
|[政府社区云 (GCC) 高](../concepts/app-fundamentals-overview.md#government-community-cloud)|GCC 高环境符合国防部 (DoD) 安全要求准则、国防联邦采购条例补充 (DFARS) 以及国际武器法规 (ITAR) 。<br>**另请参阅**： [国防部 (国防部)](#d)|
| [Graph API](../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md) | 适用于 Microsoft Graph 的 REST 风格的 Web API，支持访问 Microsoft Cloud 服务资源。 <br>**另请参阅**：[Microsoft Graph 浏览器](#m) |
| [群组聊天](../resources/bot-v3/bot-conversations/bots-conversations.md) | 一种聊天功能，用户可以通过使用 @提及调用机器人，从而在组设置中与机器人聊天。 <br>**另请参阅**：[一对一聊天](#o)；[聊天机器人](#c) |

## <a name="i"></a>I

| Term | 定义 |
| --- | --- |
| [身份提供程序](../concepts/authentication/authentication.md) | 一个实体，用于存储并向用户提供凭据。 它还允许用户自行注册。  <br>**另请参阅**：[身份验证](#a) |
| [传入 Webhook](../webhooks-and-connectors/how-to/add-incoming-webhook.md) | 它允许外部应用在 Teams 频道中共享内容。 这些 Webhook 可以用作跟踪和通知工具。 <br>**另请参阅**：[Webhook](#w)；[传出 Webhook](#o) |
| [会议内应用体验](../apps-in-teams-meetings/meeting-app-extensibility.md#in-meeting-app-experience) | A stage of Teams meeting lifecycle. With the in-meeting app experience, you can engage participants during the meeting by using apps and the in-meeting dialog box. <br>**另请参阅**：[会议生命周期](#m) |

## <a name="l"></a>L

| Term | 定义 |
| --- | --- |
| [链接展开](../messaging-extensions/how-to/link-unfurling.md) | 一项和消息扩展和会议配合使用的功能，可用于展开粘贴到撰写消息区域的链接。 链接展开以在自适应卡片或会议阶段视图中显示有关链接的其他信息。 |
| [本地环境](../toolkit/TeamsFx-multi-env.md#create-new-environment) | Teams 工具包创建的默认开发环境。  <br>**另请参阅**：[环境](#e)；[开发环境](#d) |
| [本地工作台](../sbs-gs-spfx.yml) | 在使用 SPFx 创建的 Visual Studio Code 中运行和调试 Teams 应用的默认选项。 <br>**另请参阅**：[工作台](#w)；[Teams 工作台](#t) |
| [位置功能](../concepts/device-capabilities/location-capability.md) | A device capability that you can integrate with your app to know the geographical location of the app user for an enhanced collaborative experience. This feature is currently available only for Teams mobile clients only. <br>**另请参阅**：[功能](#c)；[媒体功能](#m)；[设备功能](#d)；[Teams Mobile](#t) |
| [低代码应用](../samples/teams-low-code-solutions.md) | 使用 Microsoft Power Platform 从头开始构建的自定义 Teams 应用，只需少量编码或无需编码，并且可以快速开发和部署。 |

## <a name="m"></a>M

| Term | 定义 |
| --- | --- |
| [媒体功能](../concepts/device-capabilities/media-capabilities.md) | 可以与 Teams 应用集成的本机设备功能（如相机和麦克风）。 <br>**另请参阅**：[功能](#c)；[设备功能](#d) |
| [会议机器人](../bots/calls-and-meetings/calls-meetings-bots-overview.md) | 使用实时语音、视频和屏幕共享与 Teams 通话和会议进行交互的机器人。 <br>**另请参阅**：[通话机器人](#c)；[聊天机器人](#c) |
| [会议生命周期](../apps-in-teams-meetings/meeting-app-extensibility.md#meeting-lifecycle) | 它涵盖会议前、会议内和会议后应用体验。 可以在会议生命周期的每个阶段集成选项卡、机器人和邮件扩展。 <br>**另请参阅**：[会议内体验](#i) |
| [会议阶段](../sbs-meetings-stage-view.yml) | 会议扩展应用的一项功能。 它是在会议期间所有参与者都可访问的共享空间。 可帮助参与者实时与应用内容进行交互和协作。 <br>**另请参阅**：[阶段视图](#s) |
| [邮件扩展](../messaging-extensions/what-are-messaging-extensions.md) | Message extensions are shortcuts for inserting app content or acting on a message. You can use a message extension without navigating away from the conversation. <br>**另请参阅**：[搜索命令](#s)；[操作命令](#a) |
| [会议扩展](../apps-in-teams-meetings/design/designing-apps-in-meetings.md) | 旨在用于在会议生命周期内提高工作效率的应用，例如白板、仪表板等。 |
| [Microsoft 365 账户](../toolkit/accounts.md#microsoft-365-developer-account-types) | Microsoft 365 帐户包含 25 个仅用于开发用途的用户许可证，包括管理员。 |
| [Microsoft 365 开发人员计划](../toolkit/tools-prerequisites.md)| Microsoft 365 开发人员计划可帮助你构建扩展 Microsoft 365 的应用。 |
| [Microsoft Graph 浏览器](../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md) | The gateway to data and intelligence in Microsoft 365. It provides a unified programmability model that you can use to access data in Microsoft 365, Windows 10, and Enterprise Mobility + Security. |
| [Microsoft Teams](../overview.md) | Microsoft Teams 是一种组协作软件，可用于帮助团队开展远程协作。 |
| [Microsoft Teams 平台](../concepts/app-fundamentals-overview.md) | 借助 Microsoft Teams 开发人员平台，开发人员可以轻松地将自己的应用和服务与 Teams 集成。 |
| [Microsoft Teams UI 库](../concepts/design/design-teams-app-ui-templates.md#microsoft-teams-ui-library) | Microsoft Teams UI 库可帮助你在浏览器中查看和测试单个 Teams UI 模板和相关组件。 |
| [Microsoft Teams UI 工具包](../concepts/design/design-teams-app-ui-templates.md#microsoft-teams-ui-library) | Microsoft Teams UI 工具包包括专为构建 Teams 应用而设计的组件和模式。 |

## <a name="o"></a>O

| Term | 定义 |
| --- | --- |
| [Office 365 连接器](../webhooks-and-connectors/how-to/connectors-creating.md) | 使用此连接器，可以为传入 Webhook 创建自定义配置页，并将其打包为 Teams 应用的一部分。 你可以主要使用 Office 365 连接器卡片发送邮件，并且能够向其添加一组有限的卡片操作。 |
| [传出 Webhook](../webhooks-and-connectors/how-to/add-outgoing-webhook.md) | 传出 Webhook 充当机器人并使用 @提及功能在频道中搜索消息。 它向外部 Web 服务发送通知并以丰富的消息（包括卡片和图像）进行响应。 <br>**另请参阅**：[Webhook](#w)；[传入 Webhook](#i) |
| [Outlook 通道](../m365-apps/extend-m365-teams-message-extension.md#add-an-outlook-channel-for-your-bot) | Teams 邮件扩展应用的一项功能，允许用户从 Microsoft Outlook 与其进行交互。 |
| [一对一聊天](../resources/bot-v3/bot-conversations/bots-conv-personal.md) | Teams 个人机器人应用与单个用户之间的聊天类型。 <br>**另请参阅**：[群组聊天](#g)；[聊天机器人](#c) |

## <a name="p"></a>P

| Term | 定义 |
| --- | --- |
| [人员选取器](../task-modules-and-cards/cards/people-picker.md) | Teams 平台中用于搜索和选择人员的本机控件，可将其集成在 Web 应用、自适应卡片等中。 |
| [个人应用](../concepts/design/personal-apps.md) | 个人应用是具有个人范围的 Teams 应用程序。 它侧重于与单个用户的交互。 它可以是一个对话机器人，可以与用户或提供嵌入式 Web 体验的个人选项卡进行一对一对话，或两者兼具。 <br>**另请参阅**：[共享应用](#s) |
| [Power Virtual Agents](../bots/how-to/add-power-virtual-agents-bot-to-teams.md) | 无代码引导式图形界面解决方案，可支持团队的每个成员创建可轻松与 Teams 平台集成的丰富对话聊天机器人。 |
| [主动邮件](../bots/how-to/conversations/send-proactive-messages.md) | 由机器人发送的一条消息，例如欢迎消息、通知、计划的消息，该消息不响应来自用户的请求。 |
| [预配](../toolkit/provision.md) | A process that creates resources in Azure and Microsoft 365 for your app, but no code (HTML, CSS, JavaScript, etc.) is copied to the resources. It's a prerequisite to deployment. <br>**另请参阅**：[部署](#d) |

## <a name="r"></a>R

| Term | 定义 |
| --- | --- |
| [速率限制](../bots/how-to/rate-limit.md) | 一种将邮件限制为特定最大频率的方法，可确保邮件数量足够且不会显示为垃圾邮件。 |
| [基于角色的视图](../task-modules-and-cards/cards/universal-actions-for-adaptive-cards/user-specific-views.md) | 选项卡的一项功能，其中选项卡体验可能因用户的权限级别而异。 |
| [RSC 权限](../graph-api/rsc/resource-specific-consent.md) | 团队所有者需要特定于资源的同意 (RSC) 权限功能，可允许机器人应用在未被 @提及的情况下在团队中跨频道接收消息。 |

## <a name="s"></a>S

| Term | 定义 |
| --- | --- |
| [搜索命令](../messaging-extensions/how-to/search-commands/define-search-command.md) | 一种邮件扩展应用，允许用户搜索外部系统，并使用卡片将搜索结果包含到邮件中。 <br>**另请参阅**：[邮件扩展](#m)；[操作命令](#a) |
| [顺序工作流](../task-modules-and-cards/cards/universal-actions-for-adaptive-cards/sequential-workflows.md) | 允许机器人根据用户响应与用户进行对话的工作流。 |
| [共享应用](../concepts/extensibility-points.md#shared-app-experiences) | 存在于团队、频道或聊天中的应用，用户可以在其中进行协作和交互。 <br>**另请参阅：** 个人应用 |
| [SharePoint 网站集](../sbs-gs-spfx.yml) | A collection site for SharePoint apps. You need to have an administrator account for this site before you can deploy your SPFx-based app on the SharePoint site. <br>**另请参阅**：SPFx |
| [旁加载](../toolkit/publish.md#publish-to-individual-scope-or-sideload-permission) | 将 Teams 应用加载到 Teams 客户端，以在将其分发之前在 Teams 环境中对其进行测试的过程。 |
| [SidePanel](../sbs-meetings-sidepanel.yml) | Teams 会议应用的一项功能，可用于自定义会议中的体验，并允许组织者和演示者具有不同的视图和操作集。 |
| [SPFx](../sbs-gs-spfx.yml) | SharePoint 框架 (SPFx) 是一种开发模型，用于为 Microsoft Teams 和 SharePoint 构建客户端解决方案。 |
| SSO | 单一登录的首字母缩写，这是一种身份验证方法。使用此方法，用户只需登录一次软件平台的独立服务（如 Microsoft 365）。 然后，用户无需再次进行身份验证即可访问所有服务。 <br>**另请参阅**：[身份验证](#a) |
| [阶段视图](../sbs-meetings-stage-view.yml) | A user interface component that lets you render the content that is opened in full screen in Teams and pinned as a tab. It's invoked to surface web content within Teams. Note that it is *not* the same as meeting stage. <br>**另请参阅**：[会议阶段](#m) |
| [独立应用](../samples/integrating-web-apps.md) | 单页面或大型复杂应用。 用户可以在 Teams 中使用它的某些方面。 <br>**另请参阅**：[协作 aap](#c) |
| [静态搜索](../task-modules-and-cards/cards/dynamic-search.md) | 一种 typeahead 搜索方法，允许用户从自适应卡片有效负载中的预指定值进行搜索。 <br>**另请参阅**：[动态搜索](#d) |
| [应用商店验证指南](../concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) | 一组特定于 Teams 的指南，用于在将应用提交到 Teams 应用商店之前对其进行验证。 <br>**另请参阅**：[Teams 商店](#t) |

## <a name="t"></a>T

| Term | 定义 |
| --- | --- |
| [Tab](../tabs/what-are-tabs.md) | 选项卡是 Microsoft Teams 中嵌入的 Teams 感知网页，指向在清单中声明的域。 可将其添加到团队、群组聊天或个人应用中。 |
| [选项卡聊天](../tabs/how-to/conversational-tabs.md) | 一种选项卡类型，允许用户在动态选项卡中获得重点对话体验。 |
| [任务模块](../task-modules-and-cards/what-are-task-modules.md) | Teams 应用的一项功能，可创建用于完成任务、显示视频或仪表板的模式弹出窗口。 |
| [线程讨论](../tabs/design/tabs.md#thread-discussion) | 在频道上发布的对话或用户之间的聊天。 <br>**另请参阅**：[对话](#c)；[频道](#c) |
| [Teams](../overview.md) | Microsoft Teams is the ultimate message app for your organization. It's a workspace for real-time collaboration and communication, meetings, file and app sharing. |
| [Teams 工具包](../toolkit/teams-toolkit-fundamentals.md) | 借助 Microsoft Teams 工具包，可以直接在 Visual Studio Code 环境中创建自定义 Teams 应用程序。  |
| [TeamsFx](../toolkit/teamsfx-cli.md) | TeamsFx is a text-based command line interface that accelerates Teams application development. It's also called TeamsFx CLI.|
| [TeamsFx SDK](../toolkit/teamsfx-sdk.md) | TeamsFx SDK 是使用 TeamsFx 工具包或 CLI 在基架项目中预配置的。 |
| [TeamsJS SDK](../tabs/how-to/using-teams-client-sdk.md) | TeamsJS SDK 使你能够在 Teams 中创建托管体验。 从 TeamsJS v.2.0.0 开始，可以扩展 Teams 应用以在 Outlook 和 Office 中运行。 |
| [Teams 移动](../concepts/design/plan-responsive-tabs-for-teams-mobile.md) | Microsoft Teams 作为移动应用提供。 |
| [Teams 应用商店](../concepts/deploy-and-publish/appsource/publish.md) | 一个应用商店登陆页面，可在一个位置向用户提供应用。 应用按使用情况、行业等进行分类。 应用必须遵循应用商店验证准则并获得批准，然后才能通过 Teams 应用商店向用户提供。  <br>**另请参阅**：[应用商店验证准则](#s) |
| [Teams 工作台](../sbs-gs-spfx.yml) | Visual Studio Code 中的工作台，用于使用 SPFx 和 Teams 工具包创建的 Teams 应用的编译。 <br>**另请参阅**：[工作台](#w)；[本地工作台](#l) |

## <a name="u"></a>U

| Term | 定义 |
| --- | --- |
| [UI 组件](../concepts/design/design-teams-app-basic-ui-components.md) | 对于 Teams 应用开发，可以使用 Fluent UI 组件从头开始生成应用。 |
| [UI 模板](../concepts/design/design-teams-app-ui-templates.md) | 对于 Teams 应用开发，可以使用 Teams UI 模板快速设计应用。 |
| [自适应卡的通用操作](../task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md) | 跨平台和应用程序实现自适应卡片的方法。 它使用机器人作为处理操作的常用后端。 |

## <a name="v"></a>V

| Term | 定义 |
| --- | --- |
| [虚拟助理](../samples/virtual-assistant.md) | 一个 Microsoft 开放源代码模板，支持创建可靠的对话解决方案。 |

## <a name="w"></a>W

| Term | 定义 |
| --- | --- |
| [网站 URL](../tabs/design/tabs-mobile.md) | A property in the app manifest file (`websiteUrl`) that links the app to the website of the organization or landing page of the relevant product. It's a mandatory configuration for Teams mobile client. <br>**另请参阅**：[应用清单](#a)；[Teams 移动](#t) |
| [Web 应用](../samples/integrate-web-apps-overview.md) | 在 Web 服务器上运行的应用。 它可以与 Microsoft Teams 平台集成。 |
| [Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md) | 它是 Teams 应用的一项功能，用于将其与外部应用集成。 <br>**另请参阅**：传入 webhook；传出 Webhook |
| [Web 部件](../sbs-gs-spfx.yml) | 用于在使用 Visual Studio Code 和 SharePoint 框架创建的 Teams 应用中生成页面或网站的 UI 组件。 <br>**另请参阅**：[SPFx](#s) |
| [工作台](../sbs-gs-spfx.yml) | 包含 UI 组件（如标题栏、面板等）的整体 Visual Studio Code UI。 <br>**另请参阅**：[本地工作台](#l)；[Teams 工作台](#t) |

## <a name="y"></a>Y

| Term | 定义 |
| --- | --- |
| [YoTeams](../get-started/get-started-overview.md) | 一个开发工具包，用于基于 TypeScript 和 node.js 生成 Microsoft Teams 应用程序。 |
