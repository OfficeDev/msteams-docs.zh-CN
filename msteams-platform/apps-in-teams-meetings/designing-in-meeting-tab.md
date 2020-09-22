---
title: 设计 Microsoft 团队会议选项卡
author: heath-hamilton
description: 为 Microsoft 团队设计 "会议" 选项卡的指南和最佳实践。
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 91981ab79c8e50483568dd0dc750b4e9b3fdef24
ms.sourcegitcommit: b01986739a05c65094618fbe76aeb53d038b1c74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "48178321"
---
# <a name="design-an-in-meeting-tab"></a>设计会议中的选项卡

"会议" 选项卡是在会议过程中充实协作的画布。 根据 "团队" 选项卡功能，与会者可以通过共享或基于角色的视图在会议阶段外的专用空间中查看应用程序内容并与之交互。

## <a name="use-cases"></a>用例

用户可能会使用 "会议" 选项卡执行以下操作：

* 提供详细反馈 (例如，评估求职候选人) 
* 为会议参与者快速创建轮询、调查或任务项
* 显示与会议相关的注释 (例如，有关销售线索的信息) 

## <a name="example"></a>示例

以下示例显示了显示调查应用程序内容的 "会议" 选项卡。

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-organizer-view.png" alt-text="示例显示会议组织者的视角中会议 "会议" 选项卡的外观。":::

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">请参阅完整的方案 (Figma) </a>

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">请参阅其他示例用例 (Figma) </a>

## <a name="anatomy"></a>解析

"会议" 选项卡将使用以下维度显示您的应用程序内容：

* **宽度**：280像素用于 web 视图区域。 在 web 视图的左侧和右侧有20像素的填充。
* **高度**：完全出血到选项卡的底部。在 web 视图区域和选项卡头之间有20像素的填充。

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-anatomy.png" alt-text="显示会议扩展 "会议" 选项卡的 UI 剖析的插图。" border="false":::

1. **应用图标**： "会议中" 选项卡的入口点。
1. **标头**：包含选项卡名称。
1. **名称**：选项卡实例的名称。
1. **消除**：关闭选项卡。始终使用右上关闭图标而不是页脚中的操作。
1. **Web 视图**：显示所有第三方应用程序内容。

## <a name="behavior"></a>行为

### <a name="scale"></a>Scale

目前，"会议中" 选项卡的宽度是固定的。

### <a name="scrolling"></a>上下

以下是有关在 "会议" 选项卡中滚动的内容：

* 应仅能够垂直滚动。
* 您只能看到您已滚动的内容 (不在) 以上或之下的任何内容。
* 滚动条是 web 视图内容的一部分。

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-scroll.png" alt-text="显示如何在 "会议" 选项卡中滚动 web 视图内容的工作方式的图示。" border="false":::

### <a name="navigation"></a>导航

对于具有导航层或较大内容的方案，建议允许用户导航到辅助层。 用户必须能够返回到上一层。

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-nav.png" alt-text="显示如何在 "会议" 选项卡中导航到辅助图层的图示工作方式。" border="false":::

## <a name="components"></a>组件

"在会议中" 选项卡主要是基于以下 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI 组件（ (Figma) </a>）生成的，这是基于 " <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">流畅设计" 系统</a>的。

组件 | 准则 | 示例
 - | - | -
按钮 | 主要和次要按钮可以是中型或小型 | 发送响应
Input | 用于简短用户输入的字段。 标签文本可以包含图标  | 输入反馈
下拉列表 | 从列表中选择一个或多个选项。 可以包括搜索和多选功能 | 选择语言
选择控件 | 将 checkbox 用于多个选项或单选按钮，然后切换选择单个选项。 有关更详细的选择，请使用滑块 | 投票中的投票
警报 | 无论是显示紧急邮件、错误状态还是警告，邮件都应短，并且不会中断用户的当前任务 | 提交响应时显示问题

## <a name="theming"></a>主题

### <a name="colors"></a>颜色

将 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">推荐的配色方案 (Figma) </a> 用于背景、foregrounds 和传达状态。

### <a name="typography"></a>版式

对标题、正文文本和元数据文本使用 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">建议的字体大小和权重 (Figma) </a> 。

## <a name="best-practices"></a>最佳做法

### <a name="responsiveness"></a>性

会议选项卡布局应能够扩展到各种大小。 考虑选项卡在会议前后的缩放方式并拍摄形状。

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-before-meeting.png" alt-text="插图显示会议中的选项卡内容看起来像是会议前后的全屏选项卡。" border="false":::

#### <a name="before-the-meeting"></a>会议之前

确保您的选项卡布局可以适应不同语言的右侧或左侧布局，并且该控件将移动到正确的位置。  (会议前版式也可应用于会议后的版式。 ) 

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-during-meeting.png" alt-text="显示会议期间如何将会议前选项卡内容压缩到 "会议" 选项卡的插图。" border="false":::

#### <a name="during-the-meeting"></a>会议期间

将选项卡内容调整到会议选项卡布局和位置。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>主题

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-theming-do.png" alt-text="演示如何为团队会议中使用的深色主题设计 "会议" 选项卡。" border="false":::

#### <a name="do-design-for-a-dark-theme"></a>Do：深色主题的设计

团队会议针对深色模式进行了优化，以帮助减少视觉和认知干扰，以便用户可以将注意力集中在讨论和共享内容上。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-theming-dont.png" alt-text="插图显示您不应使用未 conducive 到 "团队深色" 主题的颜色。" border="false":::

#### <a name="dont-use-unfamiliar-colors"></a>不：使用不熟悉的颜色

与会议环境冲突的颜色可能会分散注意力，并使其在工作组中的显示较少。

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a>上下

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-scroll-do.png" alt-text="图中显示只允许在 "会议" 选项卡中进行垂直滚动。" border="false":::

#### <a name="do-scroll-vertically"></a>Do：垂直滚动

用户在团队中预测垂直滚动 (和其他) 。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-scroll-dont.png" alt-text="显示显示不应允许在 "会议" 选项卡中水平滚动的图示。" border="false":::

#### <a name="dont-scroll-horizontally"></a>不：水平滚动

水平滚动不是团队中的预期行为。 会议环境中的其他画布将垂直滚动。

   :::column-end:::
:::row-end:::

### <a name="layout"></a>布局

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-layout-do.png" alt-text="图示在 "会议" 选项卡中显示建议的单列版式。" border="false":::

#### <a name="do-single-columns"></a>操作：单个列

在给定会议的选项卡的范围内，强烈建议在一列中显示内容。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-layout-dont.png" alt-text="显示 "会议" 选项卡中的两列布局不理想的图示。" border="false":::

#### <a name="dont-multiple-columns"></a>不：多个列

由于 "会议" 选项卡的空间有限，不建议使用多列布局。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>导航

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-nav-do.png" alt-text="图显示如果您的会议选项卡应用程序有多个导航层，则应始终提供 "后退" 按钮。" border="false":::

#### <a name="do-have-a-back-button"></a>操作：有一个 "后退" 按钮

如果您有多个导航层，则用户必须能够回退到其以前的视图。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-nav-dont.png" alt-text="图中显示在导航的 "会议" 选项卡中添加另一个 "关闭" 按钮是多余的，可能会导致问题。" border="false":::

#### <a name="dont-include-another-close-button"></a>不：包含另一个 "关闭" 按钮

提供用于关闭 "会议" 选项卡内容的选项可能会导致出现问题，因为标头中已有 "关闭" 按钮来消除会议中的选项卡本身。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-tab-nav-caution.png" alt-text="图示在使用模式时需要谨慎 (例如，任务模块在 "会议" 选项卡中) 在给定有限的空间。" border="false":::

#### <a name="caution-using-dialogs-in-a-narrow-space"></a>警告：在窄间距中使用对话

在 "已缩小的会议" 选项卡中的对话框（如任务模块）可能会自动换行并掩盖内容。

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a>辅助功能

有关辅助功能的信息，请参阅 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>。

## <a name="resources"></a>资源

* <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft 团队会议扩展 Figma 文件</a>
* [选项卡设计指南](../tabs/design/tabs.md)
* [移动设备的选项卡设计指南](../tabs/design/tabs-mobile.md)

## <a name="validate-your-design"></a>验证设计

如果计划将应用程序发布到 AppSource，则应了解通常会在提交期间导致应用程序失败的设计问题。

> [!div class="nextstepaction"]
> [检查设计验证准则](../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines)
