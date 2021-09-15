---
title: 设计自定义应用
author: heath-hamilton
description: 了解如何设计Microsoft Teams应用。 资源包括Microsoft Teams UI 工具包、最佳做法、示例等。
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: f2e0043162081ba85e328182257d79161fb7875d
ms.sourcegitcommit: 72de146d11e81fd9777374dd3915ad290fd07d82
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2021
ms.locfileid: "59360466"
---
# <a name="designing-your-microsoft-teams-app"></a>设计Microsoft Teams应用

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="概念性图像，Microsoft Teams设计指南。":::

无论你是使用低代码工具的设计人员、产品经理、开发人员还是制造商，这些指南都可以帮助你快速做出正确的设计决策，Microsoft Teams应用。

## <a name="creating-a-cohesive-experience"></a>创建统一体验

设计Teams与设计传统的 Web 应用类似，但有些不同。 有效的设计突出显示了应用的独特属性，同时自然地适应Teams和上下文。

这些指南和资源可以帮助您实现此平衡。 你将了解在设计应用模型时要Teams应避免 (如选项卡导航中的多级) 。

## <a name="teams-app-design-principles"></a>Teams应用设计原则

Teams应用可帮助用户共同实现更多目标。 使用这些原则来指导你的设计。

:::row:::
   :::column span="":::

### <a name="collaborative"></a>协作

Teams应用通过用户之间的协调与共享活动促进协作。

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a>可信赖性

应用安全且合规。 用户可以轻松查找有关隐私的信息。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a>全局包含

具有所有背景、技能集和专业的人都可以使用该应用。 它在文化、种族和社会上是感知的。

   :::column-end:::
   :::column span="":::

### <a name="light"></a>轻负载

应用程序侧重于与工作流混合的核心Teams方案。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a>本机或不同

该应用使用本机Teams设计组件或你自己的组件。 配色方案、控件等不会混合使用。

   :::column-end:::
   :::column span="":::

### <a name="useful"></a>有用

该应用基于用户需要在应用中Teams。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a>易于使用

UI 易于理解、外观和声调舒适，并且使用户工作效率更高。

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a>快速响应

应用与设备和屏幕无关。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a>辅助功能

应用在Teams对比度、导航替代项等方面满足辅助功能要求。

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a>描述良好

文本、图标和图像可明确应用用途及其使用方法。

   :::column-end:::
:::row-end:::

## <a name="teams-design-system"></a>Teams设计系统

了解[应用设计Teams基础](design-teams-app-fundamentals.md)，包括布局、配色方案等。

## <a name="app-capabilities"></a>应用功能

了解用户如何添加、使用和管理Teams应用程序，以充分利用设计中每个功能。

* [个人应用](../../concepts/design/personal-apps.md)
* [选项卡](../../tabs/design/tabs.md)
* [消息扩展](../../messaging-extensions/design/messaging-extension-design.md)
* [机器人](../../bots/design/bots.md)
* [会议扩展](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="ui-templates"></a>UI 模板

使用常见用例和工作流的模板快速Teams[高保真设计](design-teams-app-ui-templates.md)。

## <a name="basic-ui-components"></a>基本 UI 组件

根据Fluent UI，这些是你可以从头开始创建Teams[](design-teams-app-basic-ui-components.md)体验的核心元素。

## <a name="tools-and-samples"></a>工具和示例

以下工具可帮助设计人员和开发人员入门：

### <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

设计Teams UI 组件、模板以及可根据需要拖放和修改的示例来设计应用。 UI 工具包还包括有关应用在不同的应用场景中的外观和行为Teams信息。

> [!div class="nextstepaction"]
> [获取图 (Ui) ](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft TeamsUI 库

在浏览器中查看和测试Teams UI 模板和相关组件。

> [!div class="nextstepaction"]
> [尝试 UI 库 (场) ](https://dev-int.teams.microsoft.com/storybook/main/index.html)

直接将这些模板和相关组件导入到Teams应用程序项目中。

> [!div class="nextstepaction"]
> [获取 UI 库 (GitHub) ](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>示例应用

你可以上载示例应用，以查看应用在客户端中的外观Teams行为。

> [!div class="nextstepaction"]
> [获取示例应用 (GitHub) ](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a>其他资源

若要了解更多信息，请尝试以下资源之一：

### <a name="fluent-ui-documentation"></a>FluentUI 文档

获取用于生成用户体验的基本 Fluent UI 组件的代码示例Teams详细信息。

> [!div class="nextstepaction"]
> [尝试Teams UI (Fluent UI) ](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a>自适应卡设计器

在基于 Web 的工具中设计自适应卡片。

> [!div class="nextstepaction"]
> [适用自适应卡设计器](https://adaptivecards.io/designer/)
