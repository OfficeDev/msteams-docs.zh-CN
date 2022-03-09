---
title: 集成 web 应用
author: Rajeshwari-v
description: 将 Web 应用程序和设备功能与应用集成Microsoft Teams概述。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
keywords: Power Platform Power Apps 人员选取器深层链接虚拟代理助理共享到Teams
ms.openlocfilehash: 0b19e5ae5a8427a77df0f4ec5fd3ea85a9abd682
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355956"
---
# <a name="integrate-web-apps"></a>集成 web 应用

通过将现有 Web 应用程序的功能集成到新平台，可以提供丰富的Microsoft Teams体验。 确保遵循[Teams准则](~/concepts/design/understand-use-cases.md)，使应用成为本机应用Teams。
本文档概述了将 Web 应用程序与 Teams、Power 平台集成以创建 Power 应用、Power Virtual Agents、虚拟助理、应用模板、Shift 连接器、一键 LMS、为网站创建"共享到 Teams"按钮、在 中添加 Microsoft Teams 选项卡的先决条件SharePoint、创建深层链接和集成设备功能。

## <a name="prerequisites"></a>先决条件

为了进行有效的集成，请确保更好地了解以下先决条件：

* Teams功能。
* SharePoint文件和数据存储的要求。
* API 要求。
* 身份验证。
* 将应用与应用进行深层Teams。
* 将应用的用例映射到Teams功能。
* 确定应用的入口点，例如个人使用和/或协作。

## <a name="low-code-platforms"></a>低代码平台

低代码平台提供了一种直观的软件开发方法，并且几乎不需要编码即可构建应用程序和流程。 可以使用低代码平台轻松创建自定义应用。 这些平台包括可视界面、后端服务的连接器以及用于构建、调试、部署和维护应用程序的内置应用生命周期管理系统。 Microsoft 提供以下创新网关，以使用Teams代码属性快速构建兼容应用程序：

* Microsoft Power 平台
* Microsoft Teams应用模板

## <a name="microsoft-power-platform"></a>Microsoft Power 平台

Microsoft Power 平台将四种强大的 Microsoft 技术（如 Power BI、Power Apps、Power Automate 和 Power Virtual Agents）组合在一个功能强大的应用程序平台中。 这些技术使您可以在统一集成的环境中生成解决方案、自动处理、分析数据以及创建虚拟代理。

### <a name="power-apps"></a>Power Apps

通过Power Apps，你可以构建连接到业务数据并针对组织需求定制的业务应用。 Power Apps支持多种应用方案，以通过画布应用解决业务挑战。 生成应用后，你可以将其从 Power Apps 制造商门户导出并嵌入Microsoft Teams。

### <a name="power-virtual-agents"></a>Power Virtual Agents

Power Virtual Agent 是无代码、引导的图形界面解决方案。 它基于 Microsoft Power Platform 和 Bot Framework 构建。 它使团队的每位成员能够创建和维护丰富的对话聊天机器人，这些聊天机器人可轻松与Teams集成。 你可以设计、开发和发布智能虚拟代理Teams而无需设置开发环境、创建 Web 服务或直接在 Bot Framework 中注册。

### <a name="create-virtual-assistant"></a>创建虚拟助手

虚拟助理是一个 Microsoft 开源模板，它使您能够创建可靠的对话解决方案，同时保持对用户体验、组织品牌和必要数据的完全控制。

## <a name="app-templates"></a>应用模板

可以使用应用模板创建自定义应用以满足组织需求。 这些是生产就绪型应用，Microsoft Teams社区驱动的开放源代码，并且可在 GitHub。 每个模板都包含为组织部署和安装应用的详细说明。 它提供了一个现成的应用程序，您可以立即安装并开始使用该应用程序。

## <a name="teams-shifts-work-force-management-connectors"></a>Teams班次工作组管理连接器

Teams班次工作组管理连接器是生产就绪型、开放源代码和社区驱动的集成。 它们通过 Shift 为一线员工的数字转换提供了无缝体验Teams流程。

## <a name="install-moodle-lms"></a>安装 Moodle LMS

在 LMS 中，一Learning是一 (开源) 。 现在，它与 Microsoft Teams。 此集成可帮助教师和教师协作处理与开发方案课程有关的问题，提出有关成绩和作业的问题，并直接在 Teams。

## <a name="create-a-share-to-teams-button-for-your-website"></a>为网站创建“共享到 Teams”按钮

第三方网站可以使用启动器脚本将"共享"嵌入Teams网页上的"共享"按钮。 当你选择该按钮时，它将在弹出窗口中Teams共享"体验。 这允许你直接将链接共享给任何人员或Microsoft Teams频道，而无需切换上下文。

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a>在Microsoft Teams中添加SharePoint

通过将 Microsoft Teams 中的 Microsoft Teams 选项卡添加为 SharePoint SharePoint Web 部件，Microsoft Teams和 SPFx 丰富的集成体验。

## <a name="create-deep-link"></a>创建深层链接

可以创建指向网站中的实体的深层Teams。 你可以创建 Teams 中的信息和功能的链接。 这些深层链接可导航到选项卡中的内容和信息。可以使用深层链接将你的应用与Teams，因为它们将应用的多个部分关联在一起，获得更本机的Teams体验。

## <a name="integrate-device-capabilities"></a>集成设备功能

Microsoft Teams平台持续增强开发人员功能，以与内置第一方体验保持一致。 借助增强的 Teams 平台，合作伙伴可以使用 Microsoft Teams JavaScript 客户端 SDK 中提供的专用 API 访问和集成本机设备功能，例如相机、QR 或条形码扫描仪、照片库、麦克风和位置。

## <a name="integrate-people-picker"></a>集成人员选取器

你可以集成本机Teams选取器控件，以允许用户在 Web 应用体验中搜索和选择人员。

## <a name="integrate-teams-in-your-external-app"></a>将Teams集成到外部应用中

通过构建应用，Microsoft Teams自己的Teams嵌入体验。 如果你想要反向此模型，并将Teams或其他通信功能集成到你自己的外部应用体验中，请参阅 [Azure Communication Services](/azure/communication-services/overview)。 Azure Communication Services 是基于云的服务，具有 REST API 和客户端库 SDK，可帮助你将通信集成到你自己的自定义应用程序中。 借助 UI 库，Teams嵌入常规React样式的 Web 组件，以调用[和聊天](https://azure.github.io/communication-ui-library/)。

Azure Communication Services 应用程序可以使用公共预览功能与 [Teams，并](/azure/communication-services/concepts/teams-interop)启用自定义应用程序以匿名Teams会议。 例如，您可以将视频通话集成到移动银行应用程序中，并允许最终用户使用 Microsoft Teams 与银行员工进行虚拟Microsoft Teams。

还可以集成Microsoft 365标识，以构建代表用户嵌入视频和 PSTN 呼叫Teams应用程序。 如果你过去使用过[Skype for Business](/skype-sdk/appsdk/skypeappsdk) SDK，建议将这些功能作为 Azure Communication Services 的一部分作为替代。

## <a name="see-also"></a>另请参阅

* [将应用的用例映射到Teams功能](~/concepts/design/map-use-cases.md)
* [确定应用的入口点](~/concepts/extensibility-points.md)
* [Teams 集成注意事项](~/samples/integrating-web-apps.md)
* [为用户创建低代码自定义Microsoft Teams](~/samples/teams-low-code-solutions.md)
* [添加强大的虚拟代理聊天机器人](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
* [创建虚拟助理](~/samples/virtual-assistant.md)
* [Microsoft Teams 的应用模板](~/samples/app-templates.md)
* [生产就绪 Shift 连接器](~/samples/shifts-wfm-connectors.md)
* [安装 Moodle LMS](~/resources/moodleinstructions.md)
* [创建“共享到Teams”按钮](~/concepts/build-and-test/share-to-teams.md)
* [向 SharePoint 添加Teams选项卡](~/tabs/how-to/tabs-in-sharepoint.md)
* [创建深层链接](~/concepts/build-and-test/deep-links.md)
* [设备功能](~/concepts/device-capabilities/device-capabilities-overview.md)
* [人员选取器控件](~/concepts/device-capabilities/people-picker-capability.md)
