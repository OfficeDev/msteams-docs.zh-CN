---
title: 为 Microsoft Teams 创建低代码自定义应用
author: surbhigupta
description: 了解 Teams 和 Microsoft Power Platform 提供的 Microsoft 低代码和无代码解决方案。
ms.localizationpriority: medium
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 59730f586ff90a6f0de9061c41ccc6c2e24385ef
ms.sourcegitcommit: 68bf3adb8aaae07caf684f7d9efb5cb7c84598b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2022
ms.locfileid: "67382935"
---
# <a name="create-low-code-custom-apps-for-teams"></a>为 Teams 创建低代码自定义应用

Microsoft Teams 具有可扩展性和适应性。 这意味着你可以为 Teams 构建自定义应用程序，以满足用户的不同需求。 低代码自定义应用可节省时间，提供快速的解决方案，并满足与从头开始创建的应用相同的需求。 本文档概述了 Microsoft Power Platform、Power Virtual Agents 聊天机器人和虚拟助理。

低代码平台提供了一种直观的软件开发方法，并且只需很少编码或无需编码即可构建应用程序和进程。 它们允许没有经验的开发人员轻松构建自定义应用，只需很少或无需编码，专业开发人员可以快速开发和部署应用。 这些平台包括可视界面、后端服务的连接器，以及用于构建、调试、部署和维护应用程序的内置应用生命周期管理系统。 Microsoft Power Platform 是一种创新型网关，可使用低代码属性快速构建与 Teams 兼容的应用。

## <a name="teams-and-microsoft-power-platform"></a>Teams 和 Microsoft Power Platform

Microsoft Power Platform 将四种强大的 Microsoft 技术（如 Power BI、Power Apps、Power Automate（以前称为 Microsoft Flow）和 Power Virtual Agents）结合在一个功能强大的应用程序平台中。 借助这些技术，可以在统一且集成的环境中构建解决方案、自动化进程、分析数据和创建虚拟代理：

:::image type="content" source="../assets/images/power-platform-and-teams/ms-power-platform.png" alt-text="Power Platform 服务":::

> [!NOTE]
>
> - 如果有兴趣在 Teams 应用商店中为所有组织中的用户发布电源应用，请填写此 [表单](https://go.microsoft.com/fwlink/?linkid=2204468)。
> - 如果有兴趣为特定组织发布应用，请参阅以下内容：
>   - [Power Apps 和 Microsoft Teams 集成](/power-apps/teams/overview)
>   - [使用 Power Apps 在 Microsoft Teams 中创建应用](/power-apps/teams/create-apps-overview)

### <a name="-teams-and-power-bi"></a>✔ Teams 和 Power BI

[Microsoft Teams 的 Power BI 选项卡](https://powerbi.microsoft.com/blog/announcing-new-power-bi-tab-for-microsoft-teams/)增加了对 Teams 工作区中报表的支持，并且允许用户[共享交互式 Power BI 内容](/power-bi/collaborate-share/service-embed-report-microsoft-teams)，并[在 Teams 频道和聊天中与其他人协作](/power-bi/collaborate-share/service-collaborate-microsoft-teams)。 可以从头开始创建打包的 [Power BI 应用](/power-bi/collaborate-share/service-create-distribute-apps)内容，并将其作为应用分发，或者[在 Power BI 中创建模板应用](/power-bi/connect-data/service-template-apps-create)。 此外，可使用 [Teams 中的新 Power BI 应用](https://go.microsoft.com/fwlink/?linkid=2143643)将整个基本 Power BI 服务体验引入 Teams。

### <a name="-teams-and-power-apps"></a>✔ Teams 和 Power Apps

使用 [Power Apps](/powerapps/powerapps-overview)，可以构建连接到业务数据并根据组织需求量身定制的业务应用。  Power Apps 支持各种应用方案，可通过[画布应用](/powerapps/maker/#canvas-apps)解决业务难题。 构建后，可以从 Power Apps 创建者门户导出应用并将其[嵌入 Microsoft Teams 中](/power-platform/admin/embed-app-teams)。

Teams 中的新 [Power Apps 应用](https://go.microsoft.com/fwlink/?linkid=2143374)为应用创建者提供了在 Teams 中创建和编辑应用及工作流的集成体验。 他们可以快速发布应用并将其共享给团队成员。 成员可以使用这些应用，而无需在多个应用和服务之间切换。

### <a name="-teams-and-power-automate"></a>✔ Teams 和 Power Automate

可以使用 [Teams 中的 Power Automate 应用](/power-automate/flows-teams)直接在 Teams 环境中[创建流来自动执行重复性工作任务](https://flow.microsoft.com/connectors/shared_teams/microsoft-teams/)。 可以[从 Microsoft Teams 中的任何消息触发流](/power-automate/trigger-flow-teams-message)，并[在 Power Automate 中使用自适应卡片](/power-automate/create-adaptive-cards)。 此外，你还可以生成流，以便从 Teams 中的新 [Power Apps 应用](https://go.microsoft.com/fwlink/?linkid=2143539)自定义并进一步增加 Microsoft Teams 的价值。

### <a name="-teams-and-power-virtual-agents"></a>✔ Teams 和 Power Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) 是基于 Microsoft Power Platform 和 Bot Framework 构建的无代码、引导式图形界面解决方案。 它使团队的每个成员能够创建和维护与 Teams 平台轻松集成的丰富对话聊天机器人。 在 Power Virtual Agents 中创作的所有内容都会在 Teams 中自然呈现，并且 Power Virtual Agents 机器人可与用户在 Teams 本机聊天画布中进行互动。 可以通过 [Power Virtual Agents 门户](https://powervirtualagents.microsoft.com)将 [Power Virtual Agents 聊天机器人集成](/power-virtual-agents/publication-add-bot-to-microsoft-teams)到 Teams。

使用 Teams 中的新 [Power Virtual Agents 应用](https://aka.ms/pva-teams-docs)，从 Teams 中轻松创建、管理和发布对话聊天机器人。 可以与组织中的其他人共享机器人，以便聊天并获取问题的答案。

### <a name="-virtual-assistant-for-teams"></a>✔ Teams 虚拟助理

虚拟助理是一个 Microsoft 开源模板，可用于创建可靠的对话解决方案，同时保持对用户体验、组织品牌和必要数据的完全控制。 可以配置虚拟助理以[集成到 Teams 环境](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro)。

### <a name="-power-platform-learn-modules"></a>✔ Power Platform Learn 模块

|  主题  |  链接  |
|:---------|:----------------------|
|Power BI|[面向应用创建者的 Power BI](/learn/browse/?expanded=power-platform&products=power-bi&roles=maker)</br>[面向开发人员的 Power BI](/learn/browse/?expanded=power-platform&products=power-bi&roles=developer)|
|Power Apps|[面向应用创建者的 Power Apps](/learn/browse/?products=power-apps&roles=maker)</br>[面向开发人员的 Power Apps](/learn/browse/?products=power-apps)|
|Power Automate|[面向应用创建者的 Power Automate](/learn/browse/?expanded=power-platform&products=power-automate&roles=maker)</br>[面向开发人员的 Power Automate](/learn/browse/?expanded=power-platform&products=power-automate&roles=developer)|
|Power Virtual Agents|[面向应用创建者和开发人员的 Power Virtual Agents](/learn/browse/?products=power-virtual-agents&expanded=power-platform&roles=maker)|

### <a name="-project-oakdale-preview"></a>✔ Project Oakdale（预览版）

> [!NOTE]
> Project **Oakdale** 已重命名为项目 **Dataverse for Teams**。

[Project Oakdale](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180
) 是 Microsoft Teams 即将推出的新低代码数据平台。 它允许开发人员直接在 Teams 中创建 Teams Power Platform 解决方案。 有关 Project Oakdale 的详细信息，请参阅 [Teams 博客 Microsoft Project Oakdale](https://powerapps.microsoft.com/blog/introducing-project-oakdale-a-new-low-code-data-platform-for-microsoft-teams)。

### <a name="-microsoft-blog-insights"></a>✔ Microsoft 博客见解

[深入了解 Project Oakdale 中的数据平台功能](https://powerapps.microsoft.com/blog/a-closer-look-at-data-platform-capabilities-in-project-oakdale/)

[推出 Power Platform 和 Teams 更新以帮助客户适应远程工作](https://cloudblogs.microsoft.com/powerplatform/2020/05/19/announcing-power-platform-and-teams-updates-to-help-customers-adapt-to-remote-work/)

[Teams 正在通过低代码功能塑造工作的未来以增强数字工作区](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180)

### <a name="-managing-power-platform-apps"></a>✔ 管理 Power Platform 应用

> [!div class="nextstepaction"]
> [在 Microsoft Teams 管理中心管理 Microsoft Power Platform 应用](/microsoftteams/manage-power-platform-apps)

## <a name="see-also"></a>另请参阅

[集成 web 应用](~/samples/integrate-web-apps-overview.md)
