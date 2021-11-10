---
title: 使用高级 UI 组件设计应用
author: heath-hamilton
description: 了解 ui Teams，如痕迹导航、通知栏、阶段视图以及相关用例。
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: reference
ms.openlocfilehash: d42205ff7d62d1c65956baed4f7841c8fe70b2e5
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889256"
---
# <a name="designing-your-microsoft-teams-app-with-advanced-ui-components"></a>使用高级 UI Microsoft Teams设计应用

以下组件是基本[UI](~/concepts/design/design-teams-app-basic-ui-components.md)组件的组合，可用于常见Teams设计情况，如导航。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

基于<a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent UI，Microsoft Teams</a>UI 工具包包括专为生成 Teams 应用而设计的组件和模式。 在 UI 工具包中，你可以将此处列出的组件直接获取并插入设计中，并查看如何使用每个组件的更多示例。

> [!div class="nextstepaction"]
> [获取 Microsoft Teams UI Kit（用户）](https://www.figma.com/community/file/916836509871353159)

## <a name="breadcrumb"></a>痕迹导航栏

痕迹导航是一种导航帮助，可传达应用的层次结构。 它们可帮助用户了解他们查看的页面如何适应整体体验，并提供了对层次结构中较高级别的一键访问。

### <a name="top-use-cases"></a>热门用例

* 通信层次结构
* 导航

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/ui-templates/mobile-breadcrumb.png" alt-text="示例演示移动版痕迹导航模板。" border="false":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="示例在桌面上显示痕迹导航模板。" border="false":::

## <a name="left-nav"></a>左导航

使用左侧导航键浏览"页面"选项卡Teams页面。在下面的示例中，左侧导航位于通道列表和选项卡内容之间。

### <a name="top-use-cases"></a>热门用例

* 浏览"页面"选项卡Teams页面。
* 将复杂应用分解为多个页面。

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/ui-templates/mobile-left-nav.png" alt-text="示例显示移动版上的左侧导航模板。" border="false":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="示例在桌面上显示左侧导航模板。" border="false":::

## <a name="notification-bar"></a>通知栏

通知栏是一个专用区域，用于显示无需用户立即采取措施的简短重要消息。 特定背景颜色和图标与特定类型的消息相关联， (请参阅下面的) 。

### <a name="top-use-cases"></a>热门用例

* 关键消息、错误和警告
* 成功消息
* 信息性或促销性消息

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/ui-templates/mobile-notification-bar.png" alt-text="示例显示移动设备上的通知栏 UI 模板。" border="false":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="示例显示桌面上的通知栏 UI 模板。" border="false":::

## <a name="stage-view"></a>阶段视图

阶段视图允许用户在大型图面上查看内容（如图像、文件或网站Teams而无需切换上下文。 此组件主要用于查看内容。 不要用于复杂的交互。

请参阅如何实现 [阶段视图](~/tabs/tabs-link-unfurling.md)。

### <a name="top-use-cases"></a>热门用例

* 在浏览器内的较大图面Teams而不是其他应用或浏览器
* 聚焦媒体或其他丰富内容

### <a name="mobile"></a>移动设备

你的应用可以从自适应卡片、共享链接或视觉组件启动阶段 (如图表) 。

:::image type="content" source="../../assets/images/ui-templates/mobile-stage.png" alt-text="示例演示移动设备上的阶段模板。" border="false":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="示例在桌面上显示阶段模板。" border="false":::

## <a name="toolbar"></a>工具栏

工具栏是一个容器，用于对一组控件进行分组。

### <a name="top-use-cases"></a>热门用例

* 应用内容的上下文操作
* 上下文筛选器和查找
* 导航和痕迹导航

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/ui-templates/mobile-toolbar.png" alt-text="示例显示移动设备上的工具栏模板。" border="false":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="示例在桌面上显示工具栏模板。" border="false":::
