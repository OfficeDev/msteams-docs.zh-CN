---
title: 设计自定义应用
author: heath-hamilton
description: 了解如何设计 Microsoft Teams 应用。 资源包括 Microsoft Teams UI 工具包、最佳做法、示例等。
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 0c791b1e4733cd2a015e443ca5c4d0c433dd4d31
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911903"
---
# <a name="designing-your-microsoft-teams-app"></a>设计 Microsoft Teams 应用

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="介绍 Microsoft Teams 设计准则的概念图像。":::

无论你是使用低代码工具的设计人员、产品经理、开发人员还是制造商，这些指南都可以帮助您为 Microsoft Teams 应用快速做出正确的设计决策。

## <a name="teams-app-design-principles"></a>Teams 应用设计原则

Teams 应用可帮助用户共同实现更多目标。 使用这些原则指导你的设计。

:::row:::
   :::column span="":::

### <a name="collaborative"></a>协作

Teams 应用可帮助用户共同实现更多目标。 使用这些原则指导你的设计。

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a>可信赖

应用安全且合规。 用户可以轻松地查找有关隐私的信息。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a>全局包含

具有所有背景、技能集和专业的人都可以使用该应用。 它在文化、种族和社交方面是感知的。

   :::column-end:::
   :::column span="":::

### <a name="light"></a>轻负载

该应用侧重于与 Teams 工作流混合的核心方案。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a>本机或不同

该应用使用本机 Teams 设计组件或你自己的组件。 配色方案、控件等不混合。

   :::column-end:::
   :::column span="":::

### <a name="useful"></a>有用

该应用基于用户需要在 Teams 中执行的方案。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a>易于使用

UI 易于理解、外观和语气都令人愉悦，并且使用户工作效率更高。

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a>快速响应

应用与设备和屏幕无关。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a>辅助功能

该应用在颜色对比度、导航替代项等方面满足 Teams 辅助功能要求。

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a>良好描述

文本、图标和图像可明确应用用途及其使用方法。

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a>创建统一体验

设计 Teams 应用与设计传统的 Web 应用类似，但有些不同。 有效的设计将突出显示应用的独特属性，同时自然地适应 Teams 功能和上下文。

这些指南和资源可以帮助您实现此平衡。 你将了解在设计 Teams 应用模型时要 (哪些操作，例如选项卡导航中的多级) 。

## <a name="planning-your-app"></a>规划应用

若要设计高质量的 Teams 应用，你必须先了解希望你的应用执行哪些操作，以及你认为用户将如何使用它。 如果还没有，请花一些时间正确 [规划你的应用](../../concepts/extensibility-points.md)。

## <a name="design-fundamentals"></a>设计基础知识

了解 [Teams 应用设计的基础，](design-teams-app-fundamentals.md)包括布局、配色方案等。

## <a name="basic-fluent-ui-components-for-teams"></a>Teams 的基本 Fluent UI 组件

基于 Fluent UI，这些是创建 [熟悉的 Teams 界面的核心元素](design-teams-app-basic-ui-components.md)。

## <a name="ui-templates"></a>UI 模板

使用常见 Teams 用例和工作流的模板快速创建复杂的高保真 [设计](design-teams-app-ui-templates.md)。

## <a name="app-capabilities"></a>应用功能

了解用户如何添加、使用和管理 Teams 应用，以充分利用设计中每个功能。

* [个人应用](../../concepts/design/personal-apps.md)
* [选项卡](../../tabs/design/tabs.md)
* [消息扩展](../../messaging-extensions/design/messaging-extension-design.md)
* [机器人](../../bots/design/bots.md)
* [会议扩展](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [任务模块](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [自适应卡](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="tools-and-samples"></a>工具和示例

以下工具可帮助设计人员和开发人员入门。

### <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI 工具包

使用 UI 组件、模板和示例设计 Teams 应用，你可以根据需要进行拖放和修改。 UI 工具包还包括有关应用在不同的 Teams 方案中的外观和行为的综合信息。

> [!div class="nextstepaction"]
> [获取图 (Ui) ](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft Teams UI 库

在浏览器中查看和测试单个 Teams UI 模板和相关组件。

> [!div class="nextstepaction"]
> [尝试 UI 库和 () ](https://dev-int.teams.microsoft.com/storybook/main/index.html)

直接将这些模板和相关组件导入 Teams 应用项目中。

> [!div class="nextstepaction"]
> [使用 GitHub (获取 UI) ](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>示例应用

安装示例应用以查看 UI 模板在 Teams 上下文中的外观和行为。

> [!div class="nextstepaction"]
> [从 GitHub (获取) ](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a>其他资源

若要了解更多信息，请尝试以下资源之一。

### <a name="fluent-ui-documentation"></a>Fluent UI 文档

获取用于构建 Teams 体验的基于 Fluent UI 的组件的代码示例和实现详细信息。

> [!div class="nextstepaction"]
> [尝试使用 Fluent UI (Teams UI) ](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a>自适应卡片设计器

在基于 Web 的工具中设计自适应卡片。

> [!div class="nextstepaction"]
> [试用自适应卡片设计器](https://adaptivecards.io/designer/)
