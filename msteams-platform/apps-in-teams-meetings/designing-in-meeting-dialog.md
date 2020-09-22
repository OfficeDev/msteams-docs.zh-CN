---
title: 设计 Microsoft 团队会议对话
author: heath-hamilton
description: 为 Microsoft 团队设计会议内对话的指南和最佳实践。
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 8e9671d8d284311d3d0a299573d3f0e08b195e97
ms.sourcegitcommit: b01986739a05c65094618fbe76aeb53d038b1c74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "48178328"
---
# <a name="design-an-in-meeting-dialog"></a>设计会议内对话

会议中的对话框显示在团队会议阶段。 他们需要用户注意、确认或交互，但这并不会中断会议。

## <a name="use-cases"></a>用例

会议组织者 (（如会议组织者) 可能希望参与者执行以下操作触发会议组织者：

* 提供简短反馈
* 进行简短调查或轮询
* 提交批准
* 获取提醒

## <a name="example"></a>示例

下面的示例显示会议参与者的角度看，会议中的对话框可能是什么样子的。 正如您所看到的，内容和任务是轻型的。

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-participant-view.png" alt-text="示例显示会议参与者的视角中会议对话框的外观。":::

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">请参阅完整的方案 (Figma) </a>

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">请参阅其他示例用例 (Figma) </a>

## <a name="anatomy"></a>解析

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-anatomy.png" alt-text="会议中的对话框视图的 UI 剖析。" border="false":::

1. **应用程序图标**
1. **应用名称**
1. **操作字符串**
1. **消除图标：** 关闭单个对话框。 始终使用右上关闭图标而不是页脚中的操作。
1. **Web 视图**：显示所有第三方应用程序内容和按钮 (标准团队按钮的建议) 。

### <a name="sizing"></a>调整

会议中的对话框的大小可能因不同的用例而异，但您必须始终保留填充和组件大小。

* **高度**：对话框的高度由 web 视图中的内容决定。 垂直滚动将接管超出您指定的最大高度的内容。
* **宽度**： web 视图的宽度是指定范围内的绝对值。

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-sizing.png" alt-text="显示会议对话的可能尺寸的图示。高度：对话框的高度由 web 视图中的内容决定。垂直滚动将接管超出) 所定义的最大高度 (的内容。最小值：无。最大值：400像素 (320 像素 web 视图) 。宽度： web 视图的宽度是指定范围内的绝对值。最小值：288像素 (256 像素 web 视图) 。最大值：468像素 (436 像素 web 视图) 。" border="false":::

## <a name="behavior"></a>行为

请参阅 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>中的常规会议对话行为，如 rest、加载等。

### <a name="position"></a>Position

会议中的对话在会议阶段居中对齐。 无法在团队系统级通知框架中拖动和工作它们。

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-position.png" alt-text="显示会议对话的 UI 剖析的插图。" border="false":::

### <a name="aggregation"></a>聚合

一次仅显示一个对话框，从最后一次向下发送到最新的堆栈排名。 一旦对话框得以解决或消除，下一个对话框便会发生。

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">请参阅 (Figma 的示例) </a>

### <a name="scrolling"></a>上下

在会议对话中的 "web 视图" 部分发生滚动。 请记住以下有关滚动的信息：

* 应仅能够垂直滚动。
* 您只能看到您已滚动的内容 (不在) 以上或之下的任何内容。

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-scroll.png" alt-text="显示在 "会议" 对话框中滚动 web 视图内容的方式的图示。" border="false":::

### <a name="buttons"></a>按钮

"会议中" 对话框按钮是 web 视图的一部分 ([请参阅一些示例](#best-practices)) 。

与类似组件不同，在用户选择按钮后将消除会议中的对话框。

## <a name="components"></a>组件

会议中的对话框主要是基于以下 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI 组件（ (Figma) </a>）生成的，这些组件基于的是 <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">熟知的设计系统</a>。

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

虽然会议中的对话可以使呼叫更有效，但如果 obtrusive，也可以 derail 呼叫。 通常情况下，请尽量少使用对话框，并遵循这些最佳实践。

### <a name="navigation"></a>导航

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-steps-do.png" alt-text="演示如何将会议中的对话框内容限制为单个屏幕，以便用户可以将注意力集中在会议上。" border="false":::

#### <a name="do-keep-it-contained"></a>Do：将其包含

将会议中的对话框内容限制为单个屏幕，以便用户可以将注意力集中在会议上。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-steps-dont.png" alt-text="图示：会议对话框不应要求用户在内容中导航。" border="false":::

#### <a name="dont-include-multiple-steps"></a>请勿：包含多个步骤

会议中的对话框不应要求用户在内容中导航。

   :::column-end:::
:::row-end:::

### <a name="interactions"></a>相互作用

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-interactions-do.png" alt-text="图中显示为什么应删除不会帮助用户快速完成某些不必要的内容的原因。" border="false":::

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-interactions-dont.png" alt-text="另一种说明为何应删除不能帮助用户快速完成某些不必要的内容的说明。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-tab-do.png" alt-text="插图显示，如果需要复杂的交互，建议您改为在会议上使用一栏。" border="false":::

#### <a name="do-limit-number-of-interactions"></a>操作：限制交互次数

删除不会帮助用户快速完成某项不必要的内容。 如果需要复杂的交互，强烈建议您改为使用 "会议" 选项卡上的单个栏显示内容。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-tab-dont.png" alt-text="图中显示会议中的对话 distracts 中的交互过多。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>请勿：引入不必要的元素

您可以设计具有多个交互的单个会议内对话，但如果过多，可能会分散会议。

   :::column-end:::
:::row-end:::

### <a name="layout"></a>布局

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-layout-do.png" alt-text="显示会议中对话框的理想布局的插图。" border="false":::

#### <a name="do-use-single-column-layouts"></a>Do： Use 单列版式

由于对话位于会议阶段的中心，因此任务完成应快速而简单，以避免用户不满。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-layout-dont.png" alt-text="显示不建议的会议中对话框的布局的图示。" border="false":::

#### <a name="dont-clutter-the-space"></a>不：打乱空间

密集或过于复杂的内容可能会分散注意力，尤其是在会议过程中。

   :::column-end:::
:::row-end:::

### <a name="size"></a>Size

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-size-do.png" alt-text="图中显示会议对话框大小应始终是相同的。" border="false":::

#### <a name="do-keep-it-consistent"></a>Do：使其保持一致

这一点很重要，因为会议中的对话框始终显示在相同的位置。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-size-dont.png" alt-text="演示如何使用不同的对话框大小。" border="false":::

#### <a name="dont-always-fit-to-the-content"></a>不：始终填充内容

您可能试图避免水平滚动，但同一应用程序中的多个会议对话大小的体验不一致。

   :::column-end:::
:::row-end:::

### <a name="controls"></a>控件

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-controls-do.png" alt-text="显示 "在会议中放置按钮的位置" 对话框的图示。" border="false":::

#### <a name="do-right-align-the-primary-action"></a>操作：将主要操作右对齐

建议将最具视觉的繁重操作定位到最右侧的位置。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-controls-dont.png" alt-text="显示 "在会议中不放置按钮的位置" 对话框的图示。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a>不：左对齐或居中对齐操作

这与对话框中的控件放置的标准团队模式不同，可能与顶部的对话框冲突。

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a>辅助功能

有关辅助功能的信息，请参阅 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>。

## <a name="resources"></a>资源

* <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft 团队会议扩展 Figma 文件</a>

## <a name="validate-your-design"></a>验证设计

如果计划将应用程序发布到 AppSource，则应了解通常会在提交期间导致应用程序失败的设计问题。

> [!div class="nextstepaction"]
> [检查设计验证准则](../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines)
