---
title: 正在设计会议分机
author: heath-hamilton
description: 了解如何在团队会议中设计应用并获取 Microsoft 团队 UI 工具包。
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 3d18895626d5f2846d10e7145a622834d82b2e98
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605941"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>正在设计 Microsoft 团队会议扩展

您可以创建应用程序以提高会议的生产率。 例如，要求人员在呼叫过程中完成调查或发送不会中断会议流的快速提醒。

## <a name="microsoft-teams-ui-kit"></a>Microsoft 团队 UI 工具包

您可以在 Microsoft 团队 UI 工具包中找到更全面的设计准则，包括可在需要时获取和修改的元素。

> [!div class="nextstepaction"]
> [ (Figma) 获取 Microsoft 团队 UI 工具包 ](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>添加会议分机

您可以在会议前后添加会议分机号。 您还可以直接从团队存储 (AppSource) 中的特定会议的应用程序。

### <a name="add-before-a-meeting"></a>在会议之前添加

在会议之前，会议详细信息选择 " **添加选项卡 +** " 以打开 "应用程序" 飞出并查找针对会议优化的应用程序。

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="示例演示如何在会议之前添加会议分机号。" border="false":::

### <a name="add-during-a-meeting"></a>在会议过程中添加

在会议中，选择 "**更多** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **添加应用程序**"，然后选择所需的应用程序。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="示例演示如何在会议过程中添加会议分机号。" border="false":::

## <a name="before-a-meeting"></a>会议前

在会议之前，您可以在选项卡中添加内容。下面的示例展示了用户在呼叫过程中将应答的草案调查问题。

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="示例演示如何在呼叫之前在会议详细信息中应用内容。" border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>剖析：会议选项卡 (之前和之后的会议) 

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="示例显示会议前后会议选项卡的结构解析。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**选项卡名称**：选项卡的导航标签。|
|2 |**选项卡溢出**：打开选项卡操作，例如 "重命名" 和 "删除"。|
|3 |**iframe**：显示应用内容。|

### <a name="designing-with-ui-templates"></a>使用 UI 模板进行设计

使用以下团队 UI 模板之一来帮助设计 "会议" 选项卡：

* [列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可浏览的格式显示相关项目，并允许用户对整个列表或单个项目执行操作。
* [任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board)：任务板（有时称为 "看板母板" 或 "泳道"）是用于跟踪工作项或票证状态的卡片的集合。
* [仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard)：仪表板是一个包含多个卡片的画布，可提供数据或内容的概述。
* [表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单以结构化方式收集、验证和提交用户输入。
* [空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。
* [左侧](../../concepts/design/design-teams-app-ui-templates.md#left-nav)导航：如果您的选项卡需要一些导航，则左侧导航模板可有所帮助。 通常情况下，应保持最小的选项卡导航。

## <a name="use-an-in-meeting-tab"></a>使用会议中的选项卡

"会议" 选项卡是在会议过程中充实协作的画布。 与会者可以通过共享或基于角色的视图在会议阶段外的专用空间中查看应用程序内容并与之交互。

### <a name="use-cases"></a>用例

用户可能会使用 "会议" 选项卡执行以下操作：

* 提供详细反馈 (例如，评估求职候选人) 
* 为会议参与者快速创建轮询、调查或任务项
* 显示与会议相关的注释 (例如，有关销售线索的信息) 

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="示例演示如何在 &quot;会议&quot; 选项卡中显示轮询内容。" border="false":::

### <a name="anatomy-in-meeting-tab"></a>剖析：会议中的选项卡

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="示例显示了 &quot;会议&quot; 选项卡的结构解析。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**选定)  (的应用程序图标**：16像素透明应用程序徽标。|
|2 |**应用名称**|
|3 |**标头**：包括您的应用程序名称。|
|4 |"**关闭" 按钮**：关闭选项卡。始终使用右上关闭图标而不是页脚中的操作。|
|5 |**通知栏**：错误警报显示在标头正下方，并将 iframe 内容向下推送20个像素。|
|6 |**iframe**：显示应用内容。|

### <a name="spacing"></a>Spacing

优化 "会议" 选项卡，使其适合在280像素宽 iframe 区域中的边缘到边缘。 Iframe 左侧和右侧的填充量为20像素，在选项卡标题之间。 Iframe 是选项卡底部的完全出血。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="示例显示了会议制表符间距尺寸。" border="false":::

### <a name="scrolling"></a>上下

Iframe 内容应垂直滚动。 您只能看到您已滚动的内容 (不在) 以上或之下的任何内容。 滚动条是 iframe 内容的一部分。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="示例显示 &quot;会议&quot; 选项卡如何滚动。" border="false":::

### <a name="navigation"></a>导航

对于具有导航层或较大内容的方案，建议允许用户导航到辅助层。 用户必须能够返回到上一层。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="示例显示了会议内导航。" border="false":::

## <a name="use-an-in-meeting-dialog"></a>使用会议中的对话框

会议中的对话框显示在团队会议阶段。 他们需要用户注意、确认或交互，但这并不会中断会议。 您应谨慎使用这些方案，并针对较亮和面向任务的方案。

### <a name="use-cases"></a>用例

会议组织者 (（如会议组织者) 可能希望参与者执行以下操作触发会议组织者：

* 提供简短反馈
* 进行简短调查或轮询
* 提交批准
* 获取提醒

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="示例演示如何使用会议内对话框。" border="false":::

### <a name="anatomy-in-meeting-dialog"></a>剖析：会议对话

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="示例显示了会议对话框的结构解析。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**标头**：包括应用程序图标、名称、操作字符串和关闭图标。|
|2 |**iframe**：显示应用内容。|

### <a name="anatomy-in-meeting-dialog-header"></a>剖析：会议对话头

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="示例显示了会议对话标题的结构解析。" border="false":::

有两个标头变量。 如果可能，请使用头像和头像，以强调对话框是否来自某个人。

|计数器|说明|
|----------|-----------|
|1|**虚拟形象**：启动 "会议" 对话框的人员。|
|2 |**应用程序图标**|
|3 |**应用名称**|
|4 |"**关闭" 按钮**：关闭对话框。|
|5 |**操作字符串**：通常说明启动对话框的是谁。|

### <a name="responsive-behavior"></a>响应行为

会议中的对话框的大小可能因不同的方案而异。 请务必保持填充和组件大小。

* **Width**： iframe 宽度是指定范围内的绝对值。
* **Height**：对话框的高度由 iframe 中的内容决定。 垂直滚动将接管超出最大高度的内容。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="示例显示 &quot;会议中&quot; 对话框。宽： Min--280 像素 (248 像素 iframe) 。最大值为460像素 (428 像素 iframe) 。高度：300像素 (iframe) 。" border="false":::

## <a name="after-a-meeting"></a>会议后

你可以在会议结束后返回到会议并查看应用内容。 在此示例中，会议组织者可以在 " **Contoso** " 选项卡中查看轮询结果。 (注意：从设计的角度看，会议前后选项卡体验之间没有任何区别。 ) 

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="示例显示 &quot;会议后&quot; 选项卡。" border="false":::

## <a name="best-practices"></a>最佳做法

### <a name="interactions"></a>相互作用

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>操作：限制交互的数量

对于 "会议中" 对话框，删除不会帮助用户快速完成某些不必要的内容。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>请勿：引入不必要的元素

具有多个交互组件的单个会议对话可以分散呼叫。

   :::column-end:::
:::row-end:::

### <a name="layout"></a>布局

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="do-use-single-column-layouts"></a>Do： Use 单列版式

由于对话位于会议阶段的中心，因此任务完成应快速而简单，以避免用户不满。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="dont-clutter-the-space"></a>不：打乱空间

密集或过于复杂的内容可能会分散注意力，尤其是在会议过程中。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="do-use-single-columns"></a>操作：使用单个列

在给定会议的选项卡的范围内，强烈建议在一列中显示内容。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="dont-use-multiple-columns"></a>请勿：使用多个列

由于 "会议" 选项卡的空间有限，不建议使用多列布局。

   :::column-end:::
:::row-end:::

### <a name="controls"></a>控件

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="do-right-align-the-primary-action"></a>操作：将主要操作右对齐

我们建议 positioining 对最右侧位置的最大视觉上的操作。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a>不：左对齐或居中对齐操作

这与对话框中的控件放置的标准团队模式不同，可能与顶部的对话框冲突。

   :::column-end:::
:::row-end:::

### <a name="scroll"></a>Scroll

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="do-scroll-vertically"></a>Do：垂直滚动

建议将最具视觉的繁重操作定位到最右侧的位置。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="dont-scroll-horizontally"></a>不：水平滚动

水平滚动不是团队中的预期行为。 会议环境中的其他画布将垂直滚动。

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>工作流

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>操作：会议中选项卡中的表面复杂方案

如果您的应用程序包含多个任务，强烈建议在 "会议" 选项卡中使用单列版式。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="dont-package-complex-scenarios-in-the-in-meeting-dialog"></a>不：在会议对话中打包复杂方案

会议中的对话框用于进行简要交互。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>主题

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="do-use-teams-color-tokens"></a>任务：使用团队颜色标记

团队会议针对深色模式进行了优化，以帮助减少视觉和认知干扰，以便用户可以将注意力集中在讨论和共享内容上。 了解如何使用 <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">颜色令牌 (熟知的 UI) </a>。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a>请勿：包含另一个消除按钮

提供用于关闭 "会议" 选项卡内容的选项可能会导致出现问题，因为标头中已有一个按钮可消除 "会议" 选项卡本身。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>导航

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="do-have-a-back-button"></a>操作：有一个 "后退" 按钮

如果在 "会议" 选项卡中有多个导航层，则用户必须能够返回到其以前的视图。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a>请勿：包含另一个消除按钮

提供用于关闭 "会议" 选项卡内容的选项可能会导致出现问题，因为标头中已有一个按钮可消除 "会议" 选项卡本身。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>警告：避免在会议中选项卡中模式

在 "已过窄的会议" 选项卡中) 的模式 (也称为 "任务模块" 可能会自动换行并掩盖内容。

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a>验证设计

如果计划将应用程序发布到 AppSource，则应了解通常会在提交期间导致应用程序失败的设计问题。

> [!div class="nextstepaction"]
> [检查设计验证准则](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
