---
title: 用于生成应用的 Teams 解决方案
author: heath-hamilton
description: 了解用于生成应用的 Teams 解决方案概述，并提供从规划应用到分发应用的支持。
ms.topic: overview
ms.localizationpriority: high
ms.author: lajanuar
ms.date: 11/02/2021
ms.openlocfilehash: 10e35af5ec4993ea93579f70afc120ff0aa8b18a
ms.sourcegitcommit: 4eeede81a0ae8ec985c6a1ad4f608df58371402f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/14/2022
ms.locfileid: "66793059"
---
# <a name="the-teams-solution"></a>Teams 解决方案


Microsoft Teams 平台是一个功能强大、灵活的平台，用于创建适用于 Teams 的应用。 它提供了大量开发环境和工具来支持应用开发。

## <a name="the-user-story"></a>用户情景：

你已了解 Teams 产品/服务。 现在可以将它们映射到用户需求。 让我们重新回顾此方案。

旅游旅行机构的开发人员希望为他们的用户（即旅游者）构建一个应用。该应用必须：

- 检查预测信息并将其发送给在该旅游机构注册的旅行者。
- 在出发日期前一天通知用户，以便他们可以进行计划。

整理并将需求映射到 Teams 功能上：

| 用户应用需求 | 检查预测 | 旅行前的通知 | 已注册的用户 |
| --- |:---:|:---:|:---:|
| **功能** | Bot | &nbsp; | &nbsp; |
| **集成** | &nbsp; | &nbsp; | :::image type="icon" source="assets/icons/microsoft-icon.png"::: Microsoft Graph，天气 API |
| **Scope** | &nbsp; | 个人应用 | &nbsp; |
| **集成点** | &nbsp; | 聊天 | &nbsp; |

**Teams 应用解决方案**：Teams *个人聊天机器人* 应用，用于检查并在 *注册用户* 出发前向他们发送 *预测通知*。

:::image type="content" source="../msteams-platform/assets/images/overview/developer-scenario-solution.png" alt-text="一家旅游机构的开发人员构建了一个 Teams 机器人，用于向客户发送天气预报，以便他们可以提前计划出行日期":::

Teams 提供了这些功能以及许多其他功能，可为用户提供功能丰富的应用解决方案。若要开发此应用：

1. 创建个人聊天机器人应用。
1. 与外部天气预报 API 集成，连接并请求特定日期和位置的预测。
1. 与注册用户的 :::image type="icon" source="assets/icons/teams-icon.png"::: Microsoft Graph 集成。
1. 根据用户的旅行日期和旅行位置检查和发送预测详细信息。

## <a name="choose-what-suits-you"></a>选择适合你的内容

可以根据应用的要求生成 Teams 应用。 根据业务需求、开发环境、域知识等因素，选择要生成应用的环境和工具。

Teams 应用为你提供了选择生成环境的灵活性。 它包括用于应用开发的工具、框架、语言。

:::image type="content" source="../msteams-platform/assets/images/overview/tools-of-your-choice.png" alt-text="业务需求应用":::

在符合特定要求的环境中构建 Teams 应用。你甚至可以选择一个组合。

例如，可以使用 Teams 工具包和 JavaScript 生成应用，并将其托管在 SharePoint 网站上。

## <a name="teams-collaborative-platform"></a>Teams 协作平台

Teams 应用为用户带去协作工作区的优势。

作为构建应用的平台，Teams 提供了各种应用和工具包。 从规划应用到分发应用，Teams 平台在每个阶段都支持你。

:::image type="content" source="../msteams-platform/assets/images/overview/teams-dev-life-cycle.png" alt-text="说明 Teams 应用开发的生命周期。计划、设计、生成、扩展、测试、部署、分发。下面的项目符号列表中显示了详细信息。":::

从设计到构建和分发 Teams 应用，可以使用各种工具和服务。开发流的示例：

1. 规划项目并确定要求。
1. 设计应用。使用 Teams UI 工具包和 UI 库设计选项卡 UI。
1. 使用 Teams 工具包和 JavaScript 生成应用。
1. 通过 :::image type="icon" source="assets/icons/microsoft-icon.png"::: Microsoft Graph 添加更多 Teams 功能和 M365 数据来扩展功能。
1. 使用示例用户数据在开发人员租户上测试应用。
1. 将应用部署到 Azure。
1. 使用开发人员门户管理应用，并将应用发布到应用商店。 通过 SaaS 产品/服务、应用内购买等选项实现应用盈利。

## <a name="next-step"></a>后续步骤

:::row:::
    :::column span="1":::
        **开始生成**
    :::column-end:::
    :::column span="2":::
        通过设置环境并创建简单的应用，快速熟悉 Teams 的构建。

        > [!div class="nextstepaction"]
        > [构建首个应用](get-started/get-started-overview.md)
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅

:::row:::
    :::column span="1":::
        **计划应用**
    :::column-end:::
    :::column span="2":::
        了解应用用例并将其映射到 Teams 功能。

        > [!div class="nextstepaction"]
        > [计划应用](~/concepts/app-fundamentals-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **设计应用**
    :::column-end:::
    :::column span="2":::
        使用 Teams UI 工具包设计应用 UI。

        > [!div class="nextstepaction"]
        > [指定 Teams 应用](~/concepts/design/design-teams-app-process.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **生成应用程序**
    :::column-end:::
    :::column span="2":::
        正在寻找应用开发灵感？通过高保真概念模拟浏览我们的实际方案和行业解决方案列表，了解 Teams 应用可帮助用户的各种方式。

        > [!div class="nextstepaction"]
        > [查看应用方案](https://adoption.microsoft.com/en-us/extensibility-look-book-gallery/)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **跨 Microsoft 365 扩展应用**
    :::column-end:::
    :::column span="2":::
可以使用 Teams JavaScript 客户端 SDK v2 预览版来预览以其他高使用率 Microsoft 365 体验运行的 Teams 应用。

        > [!div class="nextstepaction"]
        > [扩展应用](m365-apps/overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **测试应用**
    :::column-end:::
    :::column span="2":::
        将应用与 Teams 集成后，必须在发布应用之前对其进行测试。

        > [!div class="nextstepaction"]
        > [测试应用](concepts/build-and-test/test-app-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **分发应用**
    :::column-end:::
    :::column span="2":::
        可以将 Teams 应用提供给个人、团队、组织或想要使用它的任何人。

        > [!div class="nextstepaction"]
        > [分发应用](~/concepts/deploy-and-publish/apps-publish-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **将你的应用货币化**
    :::column-end:::
    :::column span="2":::
        Teams 应用商店提供应用盈利选项，例如 SaaS 产品/服务和应用内购买。 选择适合你的 Teams 应用的最佳盈利选项。

        > [!div class="nextstepaction"]
        > [将你的应用货币化](concepts/deploy-and-publish/appsource/prepare/monetize-overview.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **与Teams整合**
    :::column-end:::
    :::column span="2":::
        将用户喜欢的现有 Web 应用、服务或系统的功能与 Teams 的协作功能混合在一起。

        > [!div class="nextstepaction"]
        > [创建现有应用](samples/integrating-web-apps.md)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
        **一些代码会大有用处**
    :::column-end:::
    :::column span="2":::
        无需成为专家程序员即可构建出色的 Teams 应用。尝试几种低代码解决方案之一。

        > [!div class="nextstepaction"]
        > [创建低代码应用](samples/teams-low-code-solutions.md)
    :::column-end:::
:::row-end:::
