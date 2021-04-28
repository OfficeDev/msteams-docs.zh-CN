---
title: 为 Microsoft Teams 创建低代码自定义应用
author: laujan
description: 详细说明 Teams 的可用 Microsoft 低和无代码解决方案
localization_priority: Normal
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 78386c310ee4a82e5fdc6832f0cd288181674dbb
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058682"
---
# <a name="create-low-code-custom-apps-for-microsoft-teams"></a>为 Microsoft Teams 创建低代码自定义应用

Microsoft Teams 具有可扩展性和自适应性。 这意味着你可以为 Teams 构建自定义应用程序，以满足用户不同的需求。 低代码自定义应用比从头开始创建的应用节省时间、提供快速的解决方案并满足需求。 本文档概述了 Microsoft Power Platform、Power Virtual Agents chatbot 和 Virtual Assistant。

低代码平台提供了一种直观的软件开发方法，并且几乎不需要编码即可构建应用程序和流程。 它们允许没有经验的开发人员轻松生成自定义应用，几乎无需编码，专业开发人员可以快速开发和部署应用。 这些平台包括可视接口、后端服务的连接器以及内置应用生命周期管理系统，用于构建、调试、部署和维护应用程序。 Microsoft Power Platform 是使用低代码属性快速构建 Teams 兼容应用的创新网关。

## <a name="teams-and-microsoft-power-platform"></a>Teams 和 Microsoft Power Platform

Microsoft Power Platform 在一个强大的应用程序平台中结合了四种强大的 Microsoft 技术，如 Power BI、Power Apps、Power Automate、以前是 Microsoft Flow 和 Power Virtual Agents。 这些技术让你能够构建解决方案、自动化流程、分析数据，以及创建统一集成的环境中的虚拟代理：

:::image type="content" source="../assets/images/power-platform-and-teams/ms-power-platform.png" alt-text="Power 平台服务":::

> [!NOTE]
> 不得使用 Microsoft Power Platform 创建要发布到 Teams 应用商店的应用。 Microsoft Power Platform 应用只能发布到组织的应用商店。

### <a name="-teams-and-power-bi"></a>✔ Teams 和 Power BI

[Microsoft Teams 的 Power BI](https://powerbi.microsoft.com/blog/announcing-new-power-bi-tab-for-microsoft-teams/)选项卡增加了对 Teams 工作区中报告的支持，并允许用户共享交互式 Power [BI](/power-bi/collaborate-share/service-embed-report-microsoft-teams)内容，并与[Teams](/power-bi/collaborate-share/service-collaborate-microsoft-teams)频道和聊天中的其他人协作。 你可以从头开始创建打包 [的 Power BI 应用](/power-bi/collaborate-share/service-create-distribute-apps) 内容，并将其作为应用分发，或在 [Power BI 中创建模板应用](/connect-data/service-template-apps-create)。 此外，使用 Teams 中的 [新 Power BI](https://go.microsoft.com/fwlink/?linkid=2143643) 应用将整个基本 Power BI 服务体验引入 Teams。

### <a name="-teams-and-power-apps"></a>✔ Teams 和 Power Apps

借助 [Power Apps，](/powerapps/powerapps-overview)你可以构建连接到业务数据并满足组织需求的业务应用。  Power Apps 支持多种应用方案，以通过画布应用解决 [业务挑战](/powerapps/maker/#canvas-apps)。 生成后，你可以从 Power Apps 制造商门户导出应用， [并嵌入到 Microsoft Teams 中](/power-platform/admin/embed-app-teams)。

Teams 中的 [新 Power Apps](https://go.microsoft.com/fwlink/?linkid=2143374) 应用为应用制造商提供了在 Teams 内创建和编辑应用和工作流的集成体验。 他们可以快速发布应用并共享给团队成员。 成员可以使用这些应用，而无需在多个应用和服务之间切换。

### <a name="-teams-and-power-automate"></a>✔ Teams 和 Power Automate

可以使用 Teams [中的](https://flow.microsoft.com/connectors/shared_teams/microsoft-teams/) Power Automate 应用创建流程，以直接在 Teams 环境中 [自动执行重复工作任务](/power-automate/flows-teams)。 你可以触发 [来自 Microsoft Teams](/power-automate/trigger-flow-teams-message) 中任何消息的流， [并使用 Power Automate 中的自适应卡片](/power-automate/create-adaptive-cards)。 此外，你可以构建流来自定义 Microsoft Teams，并添加从 Teams 中新的 [Power Apps](https://go.microsoft.com/fwlink/?linkid=2143539) 应用中进一步的价值。

### <a name="-teams-and-power-virtual-agents"></a>✔ Teams 和 Power Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) is a no code， guided graphical interface solution， built on the Microsoft Power Platform and the Bot Framework. 它使团队的每位成员能够创建和维护丰富的对话聊天机器人，这些聊天机器人可轻松与 Teams 平台集成。 在 Power Virtual Agents 中创作的所有内容自然呈现在 Teams 中，Power Virtual Agents 机器人与 Teams 本机聊天画布中的用户互动。 可以通过 Power Virtual Agents 门户将[Power Virtual Agents 聊天机器人](/power-virtual-agents/publication-add-bot-to-microsoft-teams)集成到[Teams。](https://powervirtualagents.microsoft.com)

使用 Teams 中的新 [Power Virtual Agents](https://aka.ms/pva-teams-docs) 应用，轻松从 Teams 内创建、管理和发布对话聊天机器人。 你可以与组织的其他人员共享聊天机器人，并获取他们问题的答案。

### <a name="-virtual-assistant-for-teams"></a>✔ Teams 虚拟助理

虚拟助理是一个 Microsoft 开放源代码模板，它使您能够创建可靠的对话解决方案，同时保持对用户体验、组织品牌和必要数据的完全控制。 你可以将虚拟助理配置为集成到 [Teams 环境中](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro)。 

### <a name="-power-platform-learn-modules"></a>✔ Power Platform Learn 模块

|  主题  |  链接  |
|:---------|:----------------------|
|Power BI|[Power BI for App Makers](/learn/browse/?expanded=power-platform&products=power-bi&roles=maker)</br>[Power BI for Developers](/learn/browse/?expanded=power-platform&products=power-bi&roles=developer)|
|Power Apps|[Power Apps for App Makers](/learn/browse/?products=power-apps&roles=maker)</br>[适用于开发人员的 Power Apps](/learn/browse/?products=power-apps)|
|Power Automate|[适用于应用制造商的 Power Automate](/learn/browse/?expanded=power-platform&products=power-automate&roles=maker)</br>[适用于开发人员的 Power Automate](/learn/browse/?expanded=power-platform&products=power-automate&roles=developer)|
|Power Virtual Agents|[适用于应用制造商和开发人员的 Power Virtual Agents](/learn/browse/?products=power-virtual-agents&expanded=power-platform&roles=maker)|

### <a name="-project-oakdale-preview"></a>✔ Project Oak一 (预览) 

> [!NOTE]
> Project **Oak一** 起重命名为 Teams **的 Dataverse 项目**。

[Project Oak oak](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180
) 是即将在 Microsoft Teams 中推出的新低代码数据平台。 它允许开发人员直接在 Teams 内创建 Teams Power Platform 解决方案。 有关 Project Oak用户详细信息，请参阅 [Teams 博客 Microsoft Project Oak一文](https://powerapps.microsoft.com/blog/introducing-project-oakdale-a-new-low-code-data-platform-for-microsoft-teams)。

### <a name="-microsoft-blog-insights"></a>✔ Microsoft 博客见解

[进一步了解 Project Oak在数据平台的功能](https://powerapps.microsoft.com/blog/a-closer-look-at-data-platform-capabilities-in-project-oakdale/)

[宣布推出 Power Platform 和 Teams 更新，帮助客户适应远程工作](https://cloudblogs.microsoft.com/powerplatform/2020/05/19/announcing-power-platform-and-teams-updates-to-help-customers-adapt-to-remote-work/)

[Teams 正在塑造使用低代码功能增强数字工作区的未来](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180)

### <a name="-managing-power-platform-apps"></a>✔ Power Platform 应用

> [!div class="nextstepaction"]
> [在 Microsoft Teams 管理中心管理 Microsoft Power Platform 应用](/microsoftteams/manage-power-platform-apps)

## <a name="see-also"></a>另请参阅

- [集成 web 应用](~/samples/integrate-web-apps-overview.md)