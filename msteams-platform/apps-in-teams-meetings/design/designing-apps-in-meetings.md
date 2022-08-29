---
title: 设计会议扩展插件
author: heath-hamilton
description: 了解如何实现设计指南并使用 UI 模板为 Teams 设计会议扩展。
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 04/07/2022
ms.openlocfilehash: d0d994a7966f3ee172b29e6f9a6f1d4d4a2edff0
ms.sourcegitcommit: 2d2a08f671c3d19381403ba1af5dff1f06bb4dd6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2022
ms.locfileid: "67338849"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>设计 Microsoft Teams 会议扩展

你可以创建应用来提高会议效率。 例如，要求用户在会议期间完成调查，或发送一个不会中断会议流程的快速提醒。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

可以在 Microsoft Teams UI 工具包中找到更全面的设计准则，包括可以根据需要获取和修改的元素。

> [!div class="nextstepaction"]
> [获取 Microsoft Teams UI Kit（用户）](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>添加会议扩展插件

用户可以在会议前和会议期间添加会议扩展插件。 他们还可以直接从 Teams 商店添加特定会议的应用。

### <a name="add-before-a-meeting"></a>在会议前添加

在会议详细信息中，用户可以选择 **“添加选项卡 +** ”以打开应用浮出控件并查找针对会议优化的应用。

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="示例演示如何在会议前添加会议扩展名。":::

### <a name="add-during-a-meeting"></a>在会议期间添加

#### <a name="mobile"></a>移动设备

添加应用 (例如，在桌面) 上，用户可以通过选择 **“更多**:::image type="icon" source="../../assets/icons/teams-client-more.png":::”来访问会议中的应用。

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="示例演示如何在移动设备上的会议期间添加会议扩展。":::

#### <a name="desktop"></a>桌面

在会议中，用户可以选择 **“更多**:::image type="icon" source="../../assets/icons/teams-client-more.png"::: > **添加应用**”并选择所需的应用。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="示例演示如何在会议期间添加会议扩展名。":::

## <a name="before-a-meeting"></a>会议前

在会议之前，你的应用可供选项卡中的用户使用。下面的示例演示了人们将在会议期间回答的调查问题草稿。

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="示例演示如何在通话前在会议详细信息中应用内容。":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>解剖：会议前后 (“会议”选项卡) 

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="示例演示会议前后会议选项卡的结构解剖。":::

|计数器|说明|
|----------|-----------|
|1|**选项卡名称**: 选项卡的导航标签。|
|2|**选项卡溢出**: 打开选项卡操作，如重命名和删除。|
|3|**iframe**: 显示应用内容。|

### <a name="design-with-ui-templates"></a>使用 UI 模板进行设计

使用以下 Teams UI 模板之一来帮助设计会议选项卡：

* [列表](../../concepts/design/design-teams-app-ui-templates.md#list): 列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目执行操作。
* [任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board): 任务板 (有时称为看板或泳道) 是通常用于跟踪工作项或票证状态的卡片集合。
* [仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard): 仪表板是包含多个卡片的画布，可提供数据或内容的概述。
* [表单](../../concepts/design/design-teams-app-ui-templates.md#form): 表单是用于收集、验证和提交用户输入的结构化方式。
* [空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空状态模板可用于许多方案，包括登录、首次运行体验、错误消息等。
* [左侧导航](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): 如果选项卡需要导航，左侧导航组件可提供帮助。 通常，应将导航保持在最低限度。

## <a name="use-an-in-meeting-tab"></a>使用会议内选项卡

会议内选项卡是用于在会议期间增强协作的画布。 与会者可以通过共享视图或基于角色的视图在会议阶段外的专用空间中查看应用内容并与之交互。

### <a name="use-cases"></a>用例

人员可以使用会议中选项卡执行以下操作：

* 提供详细的反馈。 例如，评估应聘者。
* 为会议参与者创建轮询、调查或任务项。
* 显示与会议相关的笔记。 例如，有关销售潜在顾客的信息。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="示例演示如何在移动设备上的会议内选项卡中显示投票内容。":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="示例演示如何在会议内选项卡中显示轮询内容。":::

### <a name="anatomy-in-meeting-tab"></a>解剖：会议内选项卡

:::image type="content" source="../../assets/in-meeting-tab-anatomy.png" alt-text="示例显示会议内选项卡的结构解剖。":::

|计数器|说明|
|----------|-----------|
|1|**所选)  (应用图标**：16 像素透明应用徽标。|
|2|**应用名称**|
|3|**标头**：包括应用名称。|
|4|**关闭按钮**：关闭选项卡。始终使用右上角的关闭图标，而不是页脚中的操作。|
|5|**通知栏**：错误警报直接显示在标头下方，并将 iframe 内容的其余部分向下推送到 20 像素。|
|6|**iframe**: 显示应用内容。|

### <a name="spacing"></a>Spacing

优化会议内选项卡，以在 280 像素宽的 iframe 区域内调整边缘到边缘。 iframe 的左侧和右侧以及选项卡标头之间有 20 像素的填充。 iframe 已完全出血到选项卡底部。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="示例显示会议内选项卡间距维度。":::

### <a name="scrolling"></a>滚动

如果允许滚动，请记住以下内容：

* iframe 内容中的内容应仅垂直滚动。
* 用户只能看到已滚动到 (的内容，) 或更低。
* 滚动条是 iframe 内容的一部分。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="示例演示会议中选项卡的滚动方式。":::

### <a name="navigation"></a>导航

对于具有导航层或大量内容的方案，建议允许用户导航到辅助层。 用户必须能够返回到上一层。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="示例显示会议内导航。":::

## <a name="use-an-in-meeting-dialog"></a>使用会议内对话框

Teams 会议阶段显示的会议内对话框。 它们需要用户的注意、确认或交互，但很微妙，不会中断会议。 应谨慎使用这些功能，并针对轻型和面向任务的方案使用这些方案。

### <a name="use-cases"></a>用例

会议内对话框由用户 (触发，例如会议组织者) 可能希望参与者：

* 提供简短的反馈。
* 进行简短的调查或轮询。
* 提交审批。
* 获取提醒。

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="示例演示如何在移动设备上使用会议内对话框。":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text=" 示例演示如何使用会议内对话框。":::

### <a name="anatomy-in-meeting-dialog"></a>解剖：会议内对话框

:::image type="content" source="../../assets/in-meeting-dialog-anatomy.png" alt-text="示例演示会议内对话框的结构解剖。":::

|计数器|说明|
|----------|-----------|
|1|**标头**：包括应用图标、名称、操作字符串和关闭图标。|
|2|**iframe**: 显示应用内容。|

### <a name="anatomy-in-meeting-dialog-header"></a>解剖：会议内对话框标头

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="示例显示会议内对话标题的结构解剖。":::

有两个标头变体。 如果可能，请将变体与头像配合使用，以增强对话框来自一个人。

|计数器|说明|
|----------|-----------|
|1|**头像**：启动会议内对话框的人员。|
|2|**应用图标**|
|3|**应用名称**|
|4|**关闭按钮**：关闭对话框。|
|5|**操作字符串**：通常描述谁启动了对话框。|

### <a name="responsive-behavior-in-meeting-dialogs"></a>响应行为：会议内对话框

会议内对话可能因大小而异，以考虑不同的方案。 请确保保持填充和组件大小。

* **宽度**：可以在受支持的大小范围内的任何位置指定对话框 iframe 的宽度。
* **高度**：可以在受支持大小范围内的任何位置指定对话框 iframe 的高度。 如果应用内容超过最大高度，还可以允许用户垂直滚动。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="示例显示会议内对话框。宽度：最小 280 像素 (248 像素的 iframe) 。最大 460 像素 (428 像素的 iframe) 。高度：300 像素 (iframe) 。":::

## <a name="use-the-shared-meeting-stage"></a>使用共享会议阶段

你可以允许用户在会议阶段共享你的某些或所有应用内容并与之交互。 下面是用户在会议期间如何使用此功能的示例：

* 编辑文档。
* 白板化
* 查看仪表板。
* 观看视频。
* 玩游戏。

共享到会议阶段的应用占用的空间与共享屏幕相同。 舞台也会以同样的方式为所有会议参与者重新定向。

> [!NOTE]
> 目前，移动用户无法将应用内容共享到会议阶段。 不过，他们可以看到从桌面共享的内容。

### <a name="use-cases"></a>用例

共享会议阶段是关于协作和参与的。 下面是一些帮助你入门的示例方案。

:::row:::
   :::column span="1":::

**编辑和评审**：深入了解仪表板，并与会议中的每个人一起进行规划。

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review.png" alt-text="示例显示在共享会议阶段查看的仪表板。":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review-component.png" alt-text="示例显示正在共享会议阶段查看的仪表板组件。":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

**白板**：在共享画布上一起绘制和构想。

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-whiteboard.png" alt-text="示例显示共享会议阶段上的白板。":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

**测验**：使用交互式材料测试知识并获取见解。

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-quiz.png" alt-text="示例显示共享会议阶段的测验。":::

   :::column-end:::
:::row-end:::

### <a name="anatomy-share-all-app-content-to-a-meeting"></a>解剖：将所有应用内容共享到会议

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy.png" alt-text="图像显示共享会议阶段在共享所有应用内容时的设计解剖。":::

|计数器|说明|
|----------|-----------|
|1|**应用图标**：突出显示的图标指示应用的会议内选项卡处于打开状态。|
|2|**“共享到会议”按钮**：将应用共享到会议的入口点。 如果将应用配置为使用共享会议阶段，则显示。|
|3|**演示者归因**：显示共享应用的参与者的名称。|
|4|**iframe**: 显示应用内容。|
|5|**停止共享按钮**：停止将应用共享到会议阶段。 仅显示启动共享的参与者。|

### <a name="anatomy-share-specific-app-content-to-a-meeting"></a>解剖：将特定应用内容共享到会议

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy-component.png" alt-text="图像显示仅共享特定应用内容时共享的共享会议阶段的设计解剖。":::

|计数器|说明|
|----------|-----------|
|1|**应用图标**：突出显示的图标指示应用的会议内选项卡处于打开状态。|
|2|**“共享到会议”按钮**：将应用共享到会议的入口点。 若要获得一致的体验，请始终使用标准 Teams 共享图标。 **“共享到会议** ”是建议的默认文本，但也可以为用例自定义它。 例如， **一起玩** 游戏应用或 **一起观看** 视频应用。 无论哪种方式，请明确操作将创建与会议中的每个人共享的交互式体验。|
|3|**演示者归因**：显示共享应用的参与者的名称。|
|4|**iframe**: 显示应用内容。|
|5|**停止共享按钮**：停止将应用共享到会议阶段。 仅显示启动共享的参与者。|

### <a name="responsive-behavior-shared-meeting-stage"></a>响应行为：共享会议阶段

共享到会议阶段的应用根据会议状态和用户调整窗口大小的大小而有所不同。 保持填充以及导航和控件的响应式布局，就像在浏览器中一样。

* **侧面板**：用户可以在会议期间随时打开侧面板以聊天、查看名册或使用应用 (即会议中选项卡) 。 该阶段在面板打开时动态重新排列。
* **视频和音频网格**：视频和音频网格始终可见以显示会议参与者。 当用户在会议中聚焦或固定某人时，这会根据方向增加参与者网格的高度或宽度。

#### <a name="meeting-stage-without-side-panel"></a>没有侧面板的会议阶段 () 

当侧面板未打开时，默认情况下会议阶段为 994x678 像素，可以是至少 792x382 像素。

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-no-side-panel.png" alt-text="显示已关闭侧面板的共享会议阶段响应能力的图像。":::

#### <a name="meeting-stage-with-side-panel"></a>使用侧面板) 的会议阶段 (

当侧面板打开时，默认情况下会议阶段为 918x540 像素，并且可以是至少 472x382 像素。

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-with-side-panel.png" alt-text="显示共享会议阶段响应的图像，侧面板已打开。":::

## <a name="after-a-meeting"></a>会议后

可以在会议结束后返回会议并查看应用内容。 在此示例中，会议组织者可以在 **Contoso** 选项卡中查看投票结果。 (注意：从设计角度来看，会前和会后选项卡体验之间没有区别。) 

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="示例插图显示会后选项卡。":::

## <a name="best-practices"></a>最佳做法

使用上述建议打造优质应用体验。

### <a name="interactions"></a>相互 作用

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="演示如何限制交互数的示例。":::

#### <a name="do-limit-the-number-of-interactions"></a>请执行以下操作：限制交互数

对于会议内对话框，删除不帮助用户快速完成操作的不必要的内容。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="演示如何不引入不必要的元素的示例。":::

#### <a name="dont-introduce-unnecessary-elements"></a>不要：引入不必要的元素

具有多个交互的单个会议内对话框可能会分散会议的注意力。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-do.png" alt-text="演示如何创建重点环境的示例。":::

#### <a name="do-create-a-focused-environment"></a>请执行以下操作：创建重点环境

建议将应用的体验范围保留为仅限会议阶段。 可以使用侧面板中的会议内选项卡作为特定方案的辅助专用视图。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-dont.png" alt-text="演示如何在会议期间不包含相互竞争的图面的示例。":::

#### <a name="dont-include-competing-surfaces"></a>不要：包括相互竞争的表面

你的应用应该只要求用户一次专注于单个图面，无论是在舞台上协作还是响应会议内对话框。  (注意：在应用处于阶段时，不能让其他应用触发对话框。) 

   :::column-end:::
:::row-end:::

### <a name="layout"></a>布局

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="演示应如何使用单列对话布局的示例。":::

#### <a name="do-use-a-one-column-dialog"></a>请执行以下操作：使用单列对话框

由于对话位于会议阶段的中心，因此任务完成速度快且简单，以避免用户的挫折感。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="显示不应混乱会议扩展空间的示例。":::

#### <a name="dont-clutter-the-space"></a>不要：杂乱无章的空间

密集或过度结构化的内容可能会分散注意力和难以忍受，尤其是在会议期间。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="显示单列选项卡布局的示例。":::

#### <a name="do-use-a-one-column-tab"></a>请执行以下操作：使用单列选项卡

鉴于会议内选项卡的窄性质，我们强烈建议在单列中显示内容。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="显示包含多个列的选项卡的示例。":::

#### <a name="dont-use-multiple-columns"></a>不要：使用多个列

由于会议中选项卡的空间有限，因此不建议使用多个列的布局。

   :::column-end:::
:::row-end:::

### <a name="controls"></a>控件

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="演示如何右对齐主控件的示例。":::

#### <a name="do-right-align-the-primary-action"></a>请执行以下操作：右对齐主要操作

建议将视觉上最重的操作定位到最正确的位置。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="示例显示不应如何使主控件保持对齐。":::

#### <a name="dont-left-or-center-align-actions"></a>不要：左对齐或居中对齐操作

这偏离了控制放置在对话框中的标准 Teams 模式，并且可能与顶部对话框的对话相冲突。

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a>滚动

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="显示会议内选项卡中的垂直滚动的示例。":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-do.png" alt-text="显示共享会议阶段中的垂直滚动的示例。":::

#### <a name="do-scroll-vertically"></a>请执行以下操作：垂直滚动

用户期望在 Teams (和) 的其他位置进行垂直滚动。 如果你有一个创造性的画布（如白板），用户可以在 x 轴和 y 轴上平移，则这可能不适用。

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="显示会议内选项卡中水平滚动的示例。":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-dont.png" alt-text="显示共享会议阶段的水平滚动的示例。":::

#### <a name="dont-scroll-horizontally"></a>不要：水平滚动

水平滚动不是 Teams (（包括会议环境) ）中的预期行为。

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>工作流

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="显示会议内选项卡中的复杂方案的示例。":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>Do：会议内选项卡中的 Surface 复杂方案

如果应用包含多个任务，强烈建议将会议内选项卡与单列布局配合使用。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="显示会议内对话框中的复杂方案的示例。":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a>不要：使会议内对话变得复杂

会议内对话用于简短交互。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>主题

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="显示带有深色主题的会议扩展的示例。":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-do.png" alt-text="另一个示例显示具有深色主题的会议扩展。":::

#### <a name="do-focus-on-dark-theme"></a>请执行以下操作：关注深色主题

Teams 会议针对深色主题进行了优化，有助于减少视觉和认知噪音，以便用户可以专注于讨论和共享内容。 请记住某些类型的应用 (如白板化和文档编辑) 不需要深色画布。

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="显示与会议主题不匹配的颜色的会议扩展的示例。":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-dont.png" alt-text="另一个示例显示与会议主题不匹配的颜色的会议扩展插件。":::

#### <a name="dont-use-unfamiliar-colors"></a>不要：使用不熟悉的颜色

与会议环境冲突的颜色可能会分散注意力，并且对于 Teams 则显得不那么本机。 了解 Teams [颜色渐变](https://developer.microsoft.com/fluentui#/styles/web/colors/products)，包括调用主题中性。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>导航

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="显示带有后退按钮的会议扩展的示例。":::

#### <a name="do-have-a-back-button"></a>做：有一个后退按钮

如果会议内选项卡中有多个导航层，则用户必须能够返回到其以前的视图。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="显示具有两个消除按钮的会议扩展的示例。":::

#### <a name="dont-include-another-dismiss-button"></a>不要：包括另一个“关闭”按钮

提供用于关闭会议中选项卡内容的选项可能会导致问题，因为标头中已有一个按钮来关闭会议内选项卡本身。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="显示在会议中选项卡内) 模式 (或任务模块的示例。":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>注意：避免会议内选项卡中的模式

模式 (也称为任务模块) 在已经狭窄的会议内选项卡可能会包装和掩盖内容。

   :::column-end:::
:::row-end:::

### <a name="responsive-behavior"></a>响应行为

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-do.png" alt-text="演示如何正确调整会议扩展大小的示例。":::

#### <a name="do-resize-and-scale-your-app-responsively"></a>执行以下操作：快速调整应用大小和缩放应用

应用内容应在较小的窗口中动态调整大小和凝结。 使应用的主导航和任何浮动控件保持可见。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-dont.png" alt-text="演示如何不正确调整会议扩展大小的示例。":::

#### <a name="dont-crop-or-clip-primary-ui-components"></a>不要：裁剪或剪辑主 UI 组件

屏幕外浮动导航和控件以及需要滚动查找可能会让用户感到困惑。 当应用内容不能容纳在 iframe 中时，它不应水平滚动。

   :::column-end:::
:::row-end:::

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [为会议配置应用](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
