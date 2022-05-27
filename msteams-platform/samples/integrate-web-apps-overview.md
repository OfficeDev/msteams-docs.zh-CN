---
title: 集成 web 应用
author: Rajeshwari-v
description: 将 Web 应用程序和设备功能与 Microsoft Teams 应用集成的概述。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
keywords: Power Platform, Power Apps, 人员选取器, 深层链接, 虚拟代理助理, 共享到 Teams
ms.openlocfilehash: dc31644fca25aeca12b7e5f3095ebae53a3c02ac
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757666"
---
# <a name="integrate-web-apps"></a>集成 web 应用

可以通过将现有 Web 应用程序的功能集成到 Microsoft Teams Platform 来提供丰富的用户体验。 请确保遵循 [Teams 设计准则](~/concepts/design/understand-use-cases.md)，以便应用原生支持 Teams。
本文档概述了将 Web 应用程序与 Teams 集成的先决条件、用于创建 Power 应用的 Power Platform、Power Virtual Agents、虚拟助理、应用模板、排班连接器、Moodle LMS、为网站创建“共享到 Teams”按钮、在 SharePoint 中添加 Microsoft Teams 选项卡、创建深层链接以及集成设备功能。

## <a name="prerequisites"></a>先决条件

为了有效集成，请确保更好地了解以下先决条件：

* Teams 功能。
* 文件和数据存储的 SharePoint 要求。
* API 要求。
* 身份验证。
* 应用与 Teams 的深层链接。
* 将应用的用例映射到 Teams 平台功能。
* 确定应用的入口点，例如个人使用、协作或两者。

## <a name="low-code-platforms"></a>低代码平台

低代码平台提供了一种直观的软件开发方法，并且只需少量编码或无需编码即可构建应用程序和进程。 可以使用低代码平台轻松创建自定义应用。 这些平台包括可视界面、后端服务的连接器，以及用于构建、调试、部署和维护应用程序的内置应用生命周期管理系统。 Microsoft 提供以下创新网关，以使用低代码属性快速构建与 Teams 兼容的应用：

* Microsoft Power Platform
* Microsoft Teams 应用模板

## <a name="microsoft-power-platform"></a>Microsoft Power Platform

Microsoft Power Platform 将四种强大的 Microsoft 技术（如 Power BI、Power Apps、Power Automate 和 Power Virtual Agents）结合在一个功能强大的应用程序平台中。 借助这些技术，可以在统一且集成的环境中构建解决方案、自动化进程、分析数据和创建虚拟代理。

>[!NOTE]
>不得使用 Microsoft Power Platform 创建要发布到 Teams 应用商店的应用。 Microsoft Power Platform 应用只能发布到组织的应用商店。

### <a name="power-apps"></a>Power Apps

使用 Power Apps，可以构建连接到业务数据并根据组织需求量身定制的业务应用。 Power Apps 支持各种应用方案，可通过画布应用解决业务难题。 构建应用后，可以从 Power Apps 创建者门户导出该应用并将其嵌入 Microsoft Teams 中。

### <a name="power-virtual-agents"></a>Power Virtual Agents

Power Virtual Agent 是一种无代码引导式图形界面解决方案。 它基于 Microsoft Power Platform 和 Bot Framework 构建。 它使团队的每个成员能够创建和维护与 Teams 平台轻松集成的丰富对话聊天机器人。 可以为 Teams 设计、开发和发布智能虚拟代理，而无需设置开发环境、创建 Web 服务或直接向 Bot Framework 注册。

### <a name="create-virtual-assistant"></a>创建虚拟助手

虚拟助理是一个 Microsoft 开源模板，可用于创建可靠的对话解决方案，同时保持对用户体验、组织品牌和必要数据的完全控制。

## <a name="app-templates"></a>应用模板

可以使用应用模板创建自定义的应用以满足组织需求。 这些是适用于 Microsoft Teams 的生产就绪型应用，它们由社区驱动、开源且可在 GitHub 上获取。 每个模板都包含有关为组织部署和安装应用的详细说明。 它提供了一个现成的应用程序，可以立即安装并开始使用。

## <a name="install-moodle-lms"></a>安装 Moodle LMS

Moodle 是一种常用的 Learning Management System (LMS)。 它现在已与 Microsoft Teams 集成。 此集成可帮助教师围绕 Moodle 课程进行协作，提出有关成绩和作业的问题，并直接在 Teams 中随时关注通知。

## <a name="create-a-share-to-teams-button-for-your-website"></a>为网站创建“共享到 Teams”按钮

第三方网站可以使用启动器脚本在其网页上嵌入“共享到 Teams”按钮。 选择该按钮时，它会在弹出窗口中启动“共享到 Teams”体验。 这样你无需切换上下文，即可将链接直接共享给任何人或 Microsoft Teams 频道。

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a>在 SharePoint 中添加 Microsoft Teams 选项卡

通过在 SharePoint 中将 Microsoft Teams 选项卡添加为 SPFx Web 部件，可以在 Microsoft Teams 和 SharePoint 之间获得丰富的集成体验。

## <a name="create-deep-link"></a>创建深层链接

可以在 Teams 中创建指向实体的深层链接。 你可以创建 Teams 中的信息和功能的链接。 这些深层链接导航到选项卡中的内容和信息。可以使用深层链接将应用与 Teams 链接，因为它们将应用的多个部分绑定在一起，以获得更加原生的 Teams 体验。

## <a name="integrate-device-capabilities"></a>集成设备功能

Microsoft Teams 平台不断增强开发人员功能，与内置的第一方体验保持一致。增强的 Teams 平台允许合作伙伴使用 Microsoft Teams JavaScript 客户端 SDK 中提供的专用 API 访问和集成原生设备功能，例如相机、QR 或条形码扫描仪、照片库、麦克风、位置。

## <a name="integrate-people-picker"></a>集成人员选取器

可以集成 Teams 本机人员选取器控件，使用户能够在 Web 应用体验中搜索和选择人员。

## <a name="integrate-teams-in-your-external-app"></a>在外部应用中集成 Teams

可以通过构建 Teams 应用，将自己的体验嵌入到 Microsoft Teams 中。 若要 *反转* 此模型并将 Teams 或其他通信功能集成到自己的外部应用体验中，请参阅 [Azure 通信服务](/azure/communication-services/overview)。 Azure 通信服务是具有 REST API 和客户端库 SDK 的基于云的服务，可帮助你将通信集成到自己的自定义应用程序中。 可以借助 [UI 库](https://azure.github.io/communication-ui-library/)嵌入通用或 Teams 样式的 React Web 组件以进行呼叫和聊天。

Azure 通信服务应用程序可以使用公共预览功能[与 Teams 进行互操作](/azure/communication-services/concepts/teams-interop)，并使自定义应用程序能够匿名加入 Teams 会议。 例如，可以将视频通话集成到移动银行应用程序中，并允许最终用户使用 Microsoft Teams 与银行员工进行虚拟会面。

你还可以集成 Microsoft 365 标识，以构建代表 Teams 用户嵌入视频和 PSTN 呼叫的外部应用程序。 如果过去使用过 [Skype for Business SDK](/skype-sdk/appsdk/skypeappsdk)，则建议将这些功能作为Azure 通信服务的一部分进行替换。

## <a name="see-also"></a>另请参阅

* [将应用的用例映射到 Teams 平台功能](~/concepts/design/map-use-cases.md)
* [确定应用的入口点](~/concepts/extensibility-points.md)
* [Teams 集成注意事项](~/samples/integrating-web-apps.md)
* [为 Microsoft Teams 创建低代码自定义应用](~/samples/teams-low-code-solutions.md)
* [添加强大的虚拟代理聊天机器人](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
* [创建虚拟助理](~/samples/virtual-assistant.md)
* [Microsoft Teams 的应用模板](~/samples/app-templates.md)
* [生产就绪型 Shift 连接器](~/samples/shifts-wfm-connectors.md)
* [安装 Moodle LMS](~/resources/moodleinstructions.md)
* [从 Web 应用共享到 Teams](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [向 SharePoint 添加Teams选项卡](~/tabs/how-to/tabs-in-sharepoint.md)
* [创建深层链接](~/concepts/build-and-test/deep-links.md)
* [设备功能](~/concepts/device-capabilities/device-capabilities-overview.md)
* [人员选取器控件](~/concepts/device-capabilities/people-picker-capability.md)
