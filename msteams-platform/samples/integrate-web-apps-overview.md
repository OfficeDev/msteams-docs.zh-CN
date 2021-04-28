---
title: 集成 web 应用
author: Rajeshwari-v
description: 将 Web 应用程序和设备功能与 Microsoft Teams 应用集成概述。
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 01977e22d79f7e39986367e647a2d48ea9b2905c
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058654"
---
# <a name="integrate-web-apps"></a>集成 web 应用

通过将现有 Web 应用程序的功能集成到 Microsoft Teams 平台，可以提供丰富的用户体验。 确保遵循 [Teams 设计指南](~/concepts/design/understand-use-cases.md) ，使你的应用成为 Teams 本机应用。
本文档概述了将 Web 应用程序与 Teams 集成的先决条件、用于创建 Power Apps 的 Power 平台、Power 虚拟代理、虚拟助理、应用模板、Shift 连接器、在 LmS 中集成、为网站创建"共享到 Teams"按钮、在 SharePoint 中添加 Microsoft Teams 选项卡、创建深层链接以及集成设备功能。

## <a name="prerequisites"></a>先决条件   

为了进行有效的集成，请确保更好地了解以下先决条件：
* Teams 功能。 
* 文件和数据存储的 SharePoint 要求。
* API 要求。
* 身份验证。
* 将应用与 Teams 深度链接。
* 将应用的用例映射到 Teams 平台功能。
* 确定应用的入口点，例如个人使用和/或协作。

## <a name="low-code-platforms"></a>低代码平台

低代码平台提供了一种直观的软件开发方法，并且几乎不需要编码即可构建应用程序和流程。 可以使用低代码平台轻松创建自定义应用。 这些平台包括可视界面、后端服务的连接器以及用于构建、调试、部署和维护应用程序的内置应用生命周期管理系统。 Microsoft 提供以下创新网关，以使用低代码属性快速构建与 Teams 兼容的应用：
* Microsoft Power 平台
* Microsoft Teams 应用模板

## <a name="microsoft-power-platform"></a>Microsoft Power 平台

Microsoft Power 平台在一个强大的应用程序平台中结合了四项强大的 Microsoft 技术，如 Power BI、Power Apps、Power Automate 和 Power Virtual Agents。 这些技术使您可以在统一集成的环境中生成解决方案、自动处理、分析数据以及创建虚拟代理。

### <a name="power-apps"></a>Power Apps

借助 Power Apps，你可以构建连接到业务数据并满足组织需求的业务应用。 Power Apps 支持多种应用方案，通过画布应用解决业务挑战。 生成应用后，你可以将其从 Power Apps 制造商门户导出并嵌入到 Microsoft Teams 中。

### <a name="power-virtual-agents"></a>Power Virtual Agents

Power Virtual Agent 是无代码、引导的图形界面解决方案。 它基于 Microsoft Power Platform 和 Bot Framework 构建。 它使团队的每位成员能够创建和维护丰富的对话聊天机器人，这些聊天机器人可轻松与 Teams 平台集成。 你可以为 Teams 设计、开发和发布智能虚拟代理，而无需设置开发环境、创建 Web 服务或直接在 Bot Framework 中注册。

### <a name="create-virtual-assistant"></a>创建虚拟助理

虚拟助理是一个 Microsoft 开放源代码模板，它使您能够创建可靠的对话解决方案，同时保持对用户体验、组织品牌和必要数据的完全控制。 

## <a name="app-templates"></a>应用模板

可以使用应用模板创建自定义应用以满足组织需求。 这些是适用于 Microsoft Teams 的生产就绪应用，由社区驱动、开放源代码，可在 GitHub 上获取。 每个模板都包含为组织部署和安装应用的详细说明。 它提供了一个现成的应用程序，您可以立即安装并开始使用该应用程序。 

## <a name="teams-shifts-work-force-management-connectors"></a>Teams Shifts Work Force Management 连接器

Teams Shifts Work Force Management 连接器是生产就绪型、开放源代码和社区驱动的集成。 它们通过 Teams 班次为一线员工的数字转换提供了无缝体验和快速流程。

## <a name="install-moodle-lms"></a>安装 Moodle LMS

在 LMS 中，一个受欢迎的开放源代码 (系统) 。 它现在已与 Microsoft Teams 集成。 此集成可帮助教师和教师围绕 Teams 课程展开协作，提出有关成绩和作业的问题，并直接在 Teams 中通过通知保持更新。

## <a name="create-a-share-to-teams-button-for-your-website"></a>为网站创建“共享到 Teams”按钮

第三方网站可以使用启动器脚本在其网页上嵌入"共享到 Teams"按钮。 当你选择该按钮时，它将在弹出窗口中启动"共享到 Teams"体验。 这允许你直接将链接共享给任何人或 Microsoft Teams 频道，而无需切换上下文。

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a>在 SharePoint 中添加 Microsoft Teams 选项卡

通过将 SharePoint 中的"Microsoft Teams"选项卡添加为 SPFx Web 部件，可以在 Microsoft Teams 和 SharePoint 之间获得丰富的集成体验。 

## <a name="create-deep-link"></a>创建深层链接

你可以创建指向 Teams 中实体的深层链接。 可以在 Teams 内创建指向信息和功能的链接。 这些深层链接可导航到选项卡中的内容和信息。可以使用深层链接将你的应用与 Teams 链接，因为它们将应用的多个部分关联在一起，获得更本机的 Teams 体验。

## <a name="integrate-device-capabilities"></a>集成设备功能

Microsoft Teams 平台持续增强开发人员功能，以与内置第一方体验保持一致。 借助增强的 Teams 平台，合作伙伴可以使用 Microsoft Teams JavaScript 客户端 SDK 中提供的专用 API 访问和集成本机设备功能，例如相机、QR 或条形码扫描仪、照片库、麦克风和位置。 

## <a name="see-also"></a>另请参阅

- [将应用的用例映射到 Teams 平台功能](~/concepts/design/map-use-cases.md)

- [确定应用的入口点](~/concepts/extensibility-points.md)

- [集成 web 应用](~/samples/integrating-web-apps.md)

- [为 Microsoft Teams 创建低代码自定义应用](~/samples/teams-low-code-solutions.md)

- [添加强大的虚拟代理聊天机器人](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)

- [创建虚拟助理](~/samples/virtual-assistant.md)

- [Microsoft Teams 的应用模板](~/samples/app-templates.md)

- [生产就绪 Shift 连接器](~/samples/shifts-wfm-connectors.md)

- [安装 Moodle LMS](~/resources/moodleinstructions.md)

- [创建“共享到Teams”按钮](~/concepts/build-and-test/share-to-teams.md)

- [向 SharePoint 添加Teams选项卡](~/tabs/how-to/tabs-in-sharepoint.md)

- [创建深层链接](~/concepts/build-and-test/deep-links.md)

- [设备功能](~/concepts/device-capabilities/device-capabilities-overview.md)
