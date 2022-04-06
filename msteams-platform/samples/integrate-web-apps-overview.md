---
title: 集成 web 应用
author: Rajeshwari-v
description: 将 Web 应用程序和设备功能与Microsoft Teams应用集成的概述。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
keywords: power platform power apps people picker deep link virtual agent assistant share-to-Teams
ms.openlocfilehash: 8fe6b41f129497d439d9cf5ef391c800d6ddea0e
ms.sourcegitcommit: f892125106adb6731a20127f15d6e92f279127c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2022
ms.locfileid: "64685588"
---
# <a name="integrate-web-apps"></a>集成 web 应用

可以通过将现有 Web 应用程序的功能集成到Microsoft Teams平台来提供丰富的用户体验。 请确保遵循[Teams设计准则](~/concepts/design/understand-use-cases.md)，使应用能够原生地Teams。
本文档概述了将 Web 应用程序与Teams集成的先决条件、用于创建 Power 应用的 Power 平台、Power Virtual Agents、虚拟助理、应用模板、Shift 连接器、Moodle LMS、为网站创建"共享到Teams"按钮、在其中添加Microsoft Teams选项卡SharePoint、创建深层链接和集成设备功能。

## <a name="prerequisites"></a>先决条件

若要进行有效的集成，请确保更好地了解以下先决条件：

* Teams功能。
* SharePoint文件和数据存储的要求。
* API 要求。
* 认证。
* 应用与Teams的深度链接。
* 将应用的用例映射到Teams平台功能。
* 确定应用的入口点，例如个人使用、协作或两者。

## <a name="low-code-platforms"></a>低代码平台

低代码平台提供一种直观的软件开发方法，并且只需很少或根本不需要编码即可生成应用程序和流程。 可以使用低代码平台轻松创建自定义应用。 这些平台包括视觉界面、连接器到后端服务，以及内置的应用生命周期管理系统，用于生成、调试、部署和维护应用程序。 Microsoft 提供以下创新网关，以使用低代码属性快速构建Teams兼容的应用：

* Microsoft Power platform
* Microsoft Teams应用模板

## <a name="microsoft-power-platform"></a>Microsoft Power platform

Microsoft Power 平台将四种强大的 Microsoft 技术（如Power BI、Power Apps、Power Automate和Power Virtual Agents）结合在一个强大的应用程序平台中。 借助这些技术，你可以在统一且集成的环境中生成解决方案、自动化进程、分析数据和创建虚拟代理。

>[!NOTE]
>不得使用 Microsoft Power Platform 创建要发布到Teams应用商店的应用。 Microsoft Power Platform 应用只能发布到组织的应用商店。

### <a name="power-apps"></a>Power Apps

使用Power Apps，可以生成连接到业务数据并根据组织需求量身定制的业务应用。 Power Apps支持各种应用方案，通过画布应用解决业务难题。 生成应用后，可以从Power Apps创建者门户导出应用并嵌入Microsoft Teams。

### <a name="power-virtual-agents"></a>Power Virtual Agents

Power Virtual Agent 是一种无代码引导式图形接口解决方案。 它基于 Microsoft Power Platform 和 Bot Framework 构建。 它使团队的每个成员能够创建和维护与Teams平台轻松集成的丰富聊天机器人。 可以为Teams设计、开发和发布智能虚拟代理，而无需设置开发环境、创建 Web 服务或直接注册到 Bot Framework。

### <a name="create-virtual-assistant"></a>创建虚拟助手

虚拟助理是一个 Microsoft 开源模板，可用于创建可靠的对话解决方案，同时保持对用户体验、组织品牌和必要数据的完全控制。

## <a name="app-templates"></a>应用模板

可以使用应用模板创建自定义的应用以满足组织需求。 这些是面向Microsoft Teams的生产就绪应用，由社区驱动、开源提供，可在GitHub上使用。 每个模板都包含有关为组织部署和安装应用的详细说明。 它提供了一个现成的应用程序，你可以立即安装并开始使用。

## <a name="teams-shifts-work-force-management-connectors"></a>Teams班工作队管理连接器

Teams Shifts Work Force Management 连接器是生产就绪、开源和社区驱动的集成。 它们为具有Teams班次的第一线工人的数字化转型提供了无缝的体验和快速过程。

## <a name="install-moodle-lms"></a>安装 Moodle LMS

Moodle 是一种常用的开源Learning管理系统 (LMS) 。 它现在已与Microsoft Teams集成。 此集成可帮助教师和教师围绕 Moodle 课程进行协作，提出有关成绩和作业的问题，并直接在Teams中随时更新通知。

## <a name="create-a-share-to-teams-button-for-your-website"></a>为网站创建“共享到 Teams”按钮

第三方网站可以使用启动器脚本将"共享"嵌入到其网页上Teams按钮。 选择该按钮时，它会在弹出窗口中启动"共享"以Teams体验。 这样便可以直接共享指向任何人或Microsoft Teams通道的链接，而无需切换上下文。

## <a name="add-a-microsoft-teams-tab-in-sharepoint"></a>在SharePoint中添加Microsoft Teams选项卡

通过将SharePoint中的Microsoft Teams选项卡添加为SPFx Web 部件，可以在Microsoft Teams和SharePoint之间获得丰富的集成体验。

## <a name="create-deep-link"></a>创建深层链接

可以在Teams中创建指向实体的深层链接。 你可以创建 Teams 中的信息和功能的链接。 这些深层链接导航到选项卡中的内容和信息。你可以使用深层链接将应用与Teams链接在一起，因为它们将应用的多个部分链接在一起，以获得更本机Teams体验。

## <a name="integrate-device-capabilities"></a>集成设备功能

Microsoft Teams平台不断增强开发人员功能，与内置的第一方体验保持一致。 增强的Teams平台允许合作伙伴使用 Microsoft Teams JavaScript 客户端 SDK 中提供的专用 API 访问和集成本机设备功能，例如相机、QR 或条形码扫描程序、照片库、麦克风和位置。

## <a name="integrate-people-picker"></a>集成人员选取器

可以集成Teams本机人员选取器控件，使用户能够在 Web 应用体验中搜索和选择人员。

## <a name="integrate-teams-in-your-external-app"></a>在外部应用中集成Teams

可以通过构建Teams应用，将自己的体验嵌入到Microsoft Teams中。 若要 *反转* 此模型并将Teams或其他通信功能集成到自己的外部应用体验中，请参阅 [Azure 通信服务](/azure/communication-services/overview)。 Azure 通信服务是具有 REST API 和客户端库 SDK 的基于云的服务，可帮助你将通信集成到自己的自定义应用程序中。 可以在 [UI 库](https://azure.github.io/communication-ui-library/)的帮助下嵌入泛型或Teams样式React Web 组件进行通话和聊天。

Azure 通信服务应用程序可以使用公共预览功能[与Teams进行互操作](/azure/communication-services/concepts/teams-interop)，并使自定义应用程序能够匿名加入Teams会议。 例如，可以将视频通话集成到移动银行应用程序中，并允许最终用户使用Microsoft Teams与银行员工进行虚拟会面。

还可以集成Microsoft 365标识，以生成代表Teams用户嵌入视频和 PSTN 调用的外部应用程序。 如果过去使用[过Skype for Business SDK](/skype-sdk/appsdk/skypeappsdk)，则建议将这些功能作为Azure 通信服务的一部分作为替代。

## <a name="see-also"></a>另请参阅

* [将应用的用例映射到Teams平台功能](~/concepts/design/map-use-cases.md)
* [确定应用的入口点](~/concepts/extensibility-points.md)
* [Teams 集成注意事项](~/samples/integrating-web-apps.md)
* [为Microsoft Teams创建低代码自定义应用](~/samples/teams-low-code-solutions.md)
* [添加强大的虚拟代理聊天机器人](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
* [创建虚拟助手](~/samples/virtual-assistant.md)
* [Microsoft Teams 的应用模板](~/samples/app-templates.md)
* [生产就绪的 Shift 连接器](~/samples/shifts-wfm-connectors.md)
* [安装 Moodle LMS](~/resources/moodleinstructions.md)
* [从 Web 应用共享到Teams](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [向 SharePoint 添加Teams选项卡](~/tabs/how-to/tabs-in-sharepoint.md)
* [创建深层链接](~/concepts/build-and-test/deep-links.md)
* [设备功能](~/concepts/device-capabilities/device-capabilities-overview.md)
* [人员选取器控件](~/concepts/device-capabilities/people-picker-capability.md)
