---
title: 使用高级 UI 组件设计应用
author: heath-hamilton
description: 了解 Teams UI 组件，如痕迹、通知栏、阶段视图以及相关用例。
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: reference
ms.openlocfilehash: 055ee4440982add222b76454f1ff4382f129ff21
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558840"
---
# <a name="designing-your-microsoft-teams-app-with-advanced-ui-components"></a>使用高级 UI 组件设计 Microsoft Teams 应用

以下组件是可用于常见 Teams 设计情况（如导航） [的基本 UI 组件](~/concepts/design/design-teams-app-basic-ui-components.md) 的组合。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI 工具包基于 <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI</a>，包括专为构建 Teams 应用而设计的组件和模式。 在 UI 工具包中，可以直接将此处列出的组件抓取并插入到设计中，并查看有关如何使用每个组件的更多示例。

> [!div class="nextstepaction"]
> [获取 Microsoft Teams UI Kit （用户）](https://www.figma.com/community/file/916836509871353159)

## <a name="breadcrumb"></a>痕迹导航栏

痕迹擦洗是一种导航辅助工具，可传达应用的层次结构。 它们可帮助用户了解他们查看的页面如何适应整体体验，并提供对该层次结构中更高级别的单击访问权限。

### <a name="top-use-cases"></a>最主要用例

* 通信层次结构
* 导航

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/ui-templates/mobile-breadcrumb.png" alt-text="示例显示移动设备上的痕迹清理模板。":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="示例演示桌面上的痕迹清理模板。":::

## <a name="left-nav"></a>左导航

使用左侧导航在 Teams 选项卡中浏览多个页面。在以下示例中，左侧导航位于通道列表和选项卡内容之间。

### <a name="top-use-cases"></a>最主要用例

* 在 Teams 选项卡中浏览多个页面。
* 将复杂应用分解为多个页面。

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/ui-templates/mobile-left-nav.png" alt-text="示例显示移动版上的左导航模板。":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="示例显示桌面上的左导航模板。":::

## <a name="notification-bar"></a>通知栏

通知栏是用于显示简短的重要消息的专用区域，不需要用户立即执行操作。 特定背景颜色和图标与特定类型的消息相关联， (请参阅下) 。

可以使用 Fluent UI [警报](https://fluentsite.z22.web.core.windows.net/0.59.0/components/alert/definition) 组件实现通知栏。

### <a name="top-use-cases"></a>最主要用例

* 关键消息、错误和警告
* 成功消息
* 信息性或促销性消息

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/ui-templates/mobile-notification-bar.png" alt-text="示例显示移动设备上的通知栏 UI 模板。":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="示例显示桌面上的通知栏 UI 模板。":::

## <a name="stage-view"></a>阶段视图

阶段视图允许用户在 Teams 中的大型图面上查看内容（如图像、文件或网站），而无需切换上下文。 此组件主要用于查看内容。 不要将其用于复杂的交互。

了解如何实现 [阶段视图](~/tabs/tabs-link-unfurling.md)。

### <a name="top-use-cases"></a>最主要用例

* 在 Teams 内部的大型图面中显示内容，而不是其他应用或浏览器
* 聚焦媒体或其他丰富内容

### <a name="mobile"></a>移动设备

应用可以从自适应卡片、共享链接或视觉组件（例如图表) ） (启动阶段。

:::image type="content" source="../../assets/images/ui-templates/mobile-stage.png" alt-text="示例显示移动设备上的阶段模板。":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="示例显示桌面上的阶段模板。":::

## <a name="toolbar"></a>工具栏

工具栏是用于对一组控件进行分组的容器。

### <a name="top-use-cases"></a>最主要用例

* 应用内容的上下文操作。
* 上下文筛选和查找。
* 导航和痕迹。

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/ui-templates/mobile-toolbar.png" alt-text="示例显示移动设备上的工具栏模板。":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="示例显示桌面上的工具栏模板。":::
