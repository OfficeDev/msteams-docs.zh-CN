---
title: 设计自定义应用
author: heath-hamilton
description: 了解如何设计 Microsoft Teams 应用和资源，包括 Microsoft Teams UI 工具包、最佳做法、示例等。
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 341c64b2afda7574b6d230257290220e2c97d325
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615308"
---
# <a name="designing-your-microsoft-teams-app"></a>设计 Microsoft Teams 应用

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="介绍 Microsoft Teams 设计指南的概念图。":::

无论你是使用低代码工具的设计者、产品经理、开发人员还是制造商，这些指南都可以帮助你快速为 Microsoft Teams 应用做出正确的设计决策。

## <a name="creating-a-cohesive-experience"></a>创建有凝聚力的体验

设计 Teams 应用就像设计传统的 Web 应用一样，但也略有不同。 有效的设计突出显示了应用的独特特性，同时自然地适合 Teams 功能和上下文。

这些准则和资源可帮助你实现这种平衡。 你将了解在设计 Teams 应用时应执行的操作以及应避免的操作（例如选项卡中的多级导航）。

## <a name="teams-app-design-principles"></a>Teams 应用设计原则

Teams 应用可帮助人们共同实现更多目标。 使用这些原则指导你的设计。

:::row:::
   :::column span="":::

### <a name="collaborative"></a>协同

Teams 应用通过用户之间的协调和共享活动促进协作。

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a>可信

应用安全且合规。 用户可以轻松找到有关隐私的信息。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a>全局包容性

所有背景、技能组和学科的人员都可以使用该应用。 它反映了文化、种族和社会意识。

   :::column-end:::
   :::column span="":::

### <a name="light"></a>轻负载

该应用侧重于融合 Teams 工作流的核心场景。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a>本机或非独有

应用使用本机 Teams 设计组件或你自己的组件。 没有配色方案、控件等混合。

   :::column-end:::
   :::column span="":::

### <a name="useful"></a>有用

该应用基于用户在 Teams 中需要执行的方案。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a>易于使用

UI 易于理解，外观和语气令人愉快，使人们更有效率。

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a>快速响应

该应用与设备和屏幕无关。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a>辅助功能

应用在颜色对比度、导航替代项等方面满足 Teams 辅助功能要求。

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a>很好描述

文本、图标和图像可明确应用的用途以及如何使用它。

   :::column-end:::
:::row-end:::

## <a name="teams-design-system"></a>Teams 设计系统

了解 [Teams 应用设计的基础知识](design-teams-app-fundamentals.md)，包括布局、配色方案等。

## <a name="app-capabilities"></a>应用功能

了解用户如何添加、使用和管理 Teams 应用，以充分利用设计中的每个功能。

* [个人应用](../../concepts/design/personal-apps.md)
* [选项卡](../../tabs/design/tabs.md)
* [消息扩展](../../messaging-extensions/design/messaging-extension-design.md)
* [机器人](../../bots/design/bots.md)
* [会议扩展](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="ui-templates"></a>UI 模板

使用[常用 Teams 用例和工作流的模板](design-teams-app-ui-templates.md)快速创建复杂、高保真度设计。

## <a name="basic-ui-components"></a>基本 UI 组件

根据 Fluent UI，可以使用这些 [核心元素](design-teams-app-basic-ui-components.md) 从头开始创建 Teams 体验。

## <a name="tools-and-samples"></a>工具和示例

以下工具可帮助设计人员和开发人员入门：

### <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

使用 UI 组件、模板和示例设计 Teams 应用，你可以根据需要进行拖放和修改。 UI 工具包还包括有关应用在不同 Teams 场景中外观和行为的详细信息。

> [!div class="nextstepaction"]
> [获取 UI 工具包 (Figma) ](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft Teams UI 库

Microsoft Teams UI 库可帮助你在浏览器中查看和测试单个 Teams UI 模板和相关组件。

> [!div class="nextstepaction"]
> [试用 UI 库（操场）](https://dev-int.teams.microsoft.com/storybook/main/index.html)

将这些模板和相关组件直接导入 Teams 应用项目。

> [!div class="nextstepaction"]
> [获取 UI 库 (GitHub) ](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>示例应用

可以上传示例应用，了解应用在 Teams 客户端中的外观和行为。

> [!div class="nextstepaction"]
> [获取示例应用 (GitHub) ](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a>其他资源

若要了解详细信息，请尝试以下资源之一：

### <a name="fluent-ui-documentation"></a>Fluent UI 文档

获取用于生成 Teams 体验的基本 Fluent UI 组件代码示例和操作详细信息。

> [!div class="nextstepaction"]
> [尝试 Teams UI 组件 (Fluent UI) ](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a>自适应卡设计器

在基于 Web 的工具中设计自适应卡片。

> [!div class="nextstepaction"]
> [适用自适应卡设计器](https://adaptivecards.io/designer/)

## <a name="see-also"></a>另请参阅

* [为会议阶段启用和配置应用](../../apps-in-teams-meetings/build-tabs-for-meeting.md)
* [设计 Microsoft Teams 自动程序](~/bots/design/bots.md)
* [创建虚拟助手](~/samples/virtual-assistant.md)
* [为 Microsoft Teams 应用设计任务模块](~/task-modules-and-cards/task-modules/design-teams-task-modules.md)
