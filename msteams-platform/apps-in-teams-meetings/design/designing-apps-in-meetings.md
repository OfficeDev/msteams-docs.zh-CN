---
title: 设计会议扩展
author: heath-hamilton
description: 了解如何在会议Teams设计应用并获取 Microsoft Teams UI 工具包。
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 621fbb1e3da7ef9083229acf93b05c72cc528bf2ec813529d93025e1a54d79c6
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2021
ms.locfileid: "57702385"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>设计会议Microsoft Teams扩展

你可以创建应用来使会议更加高效。 例如，要求用户在呼叫过程中完成调查或发送不会中断会议流的快速提醒。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

你可以找到更全面的设计指南，包括你可以根据需要获取和修改的元素，Microsoft Teams UI 工具包。

> [!div class="nextstepaction"]
> [获取 Microsoft Teams UI Kit（用户）](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>添加会议扩展

用户可以在会议之前和会议期间添加会议扩展名。 他们还可以直接从应用商店添加特定会议Teams应用。

### <a name="add-before-a-meeting"></a>在会议前添加

在会议详细信息中，用户可以选择"添加选项卡 **+"** 以打开应用飞出控件并查找针对会议优化的应用。

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="示例演示如何在会议之前添加会议扩展名。" border="false":::

### <a name="add-during-a-meeting"></a>会议期间添加

# <a name="desktop"></a>[桌面设备](#tab/desktop)

在会议中，**用户可以选择"** 更多 :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **添加应用**"，然后选择他们需要的应用。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="示例演示如何在会议期间添加会议扩展名。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

在桌面上添加应用后，可以选择该应用，并且可以通过选择"更多"在会议使用 **该应用** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: 。

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="示例演示如何在移动会议期间添加会议扩展。" border="false":::

---

## <a name="before-a-meeting"></a>会议前

在会议之前，用户可以在选项卡中添加内容。以下示例显示了一个草稿调查问题，人员将在呼叫过程中回答该问题。

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="示例演示如何在呼叫之前应用会议详细信息中的内容。" border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>结构：会议 (会议之前和之后) 

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="示例显示会议之前和之后的会议选项卡的结构结构分析。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**选项卡名称**：选项卡的导航标签。|
|2|**Tab 溢出**：打开选项卡操作，如重命名和删除。|
|3|**iframe：** 显示应用内容。|

### <a name="designing-with-ui-templates"></a>使用 UI 模板进行设计

使用以下 UI 模板Teams之一来帮助设计会议选项卡：

* [列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目采取操作。
* [任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board)：任务板（有时称为看板或街道）是一组卡片，通常用于跟踪工作项或票证的状态。
* [仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard)：仪表板是包含多个卡片的画布，可提供数据或内容的概述。
* [表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单用于以结构化方式收集、验证和提交用户输入。
* [空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。
* [左侧导航](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav)：如果你的选项卡需要一些导航，左侧导航组件会有所帮助。 通常，应该将导航保持在最低程度。

## <a name="use-an-in-meeting-tab"></a>使用会议内选项卡

"会议内"选项卡是一块画布，用于增强会议期间的协作。 与会者可以通过共享视图或基于角色的视图在会议阶段外的专用空间中查看应用内容并与之交互。

### <a name="use-cases"></a>用例

人们可能会使用"会议内"选项卡：

* 提供详细反馈。 例如，评估一个职位候选人。
* 为会议参与者创建投票、调查或任务项。
* 显示与会议相关的备注。 例如，有关销售线索的信息。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="示例演示如何在会议中的选项卡中显示投票内容。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="示例演示如何在移动设备上的&quot;会议&quot;选项卡中显示投票内容。" border="false":::

---

### <a name="anatomy-in-meeting-tab"></a>结构：会议内选项卡

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="示例显示会议内选项卡的结构结构分析。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**应用图标 (选择**) ：16 像素透明应用徽标。|
|2|**应用名称**|
|3|**标头**：包括你的应用名称。|
|4 |**关闭按钮**：关闭选项卡。始终使用右上方的关闭图标，而不是页脚中的操作。|
|5 |**通知栏**：错误警报显示在标题正下方，将 iframe 内容向下推送 20 像素。|
|6 |**iframe：** 显示应用内容。|

### <a name="spacing"></a>Spacing

优化会议选项卡以适合 280 像素宽的 iframe 区域中的边缘到边缘。 在 iframe 的左侧和右侧以及选项卡标题之间有 20 个像素的填充。 iframe 完全出血到选项卡底部。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="示例显示会议中的选项卡间距尺寸。" border="false":::

### <a name="scrolling"></a>滚动

如果允许滚动，请记住以下几点：

* iframe 内容中的内容只应垂直滚动。
* 用户只能看到他们滚动到的内容， (上方或) 。 
* 滚动条是 iframe 内容的一部分。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="示例显示如何滚动会议中的选项卡。" border="false":::

### <a name="navigation"></a>导航

对于具有导航层或大量内容的方案，我们建议允许用户导航到辅助层。 用户必须能够返回到上一层。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="示例显示会议内导航。" border="false":::

## <a name="use-an-in-meeting-dialog"></a>使用会议内对话框

会议中的对话框显示在会议Teams上。 它们需要用户的注意、确认或交互，但很细微，不会中断会议。 应谨慎使用这些模式，并针对轻型和面向任务的场景。

### <a name="use-cases"></a>用例

会议内对话框由以下用户触发 (例如会议组织者) 可能希望参与者：

* 提供简短反馈
* 参加简短调查或投票
* 提交审批
* 获取提醒

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="示例演示如何使用会议内对话框。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="示例演示如何在移动设备上使用会议内对话框。" border="false":::

---

### <a name="anatomy-in-meeting-dialog"></a>结构：会议内对话框

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="示例显示会议对话的结构结构分析。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**标头**：包括应用图标、名称、操作字符串和关闭图标。|
|2|**iframe：** 显示应用内容。|

### <a name="anatomy-in-meeting-dialog-header"></a>结构：会议内对话框标头

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="示例显示会议内对话框标题的结构结构分析。" border="false":::

有两个标头变量。 如果可能，将变体与头像一同使用，以强调对话框来自某人。

|计数器|说明|
|----------|-----------|
|1|**头** 像：启动会议对话的人。|
|2|**应用程序图标**|
|3|**应用名称**|
|4 |**关闭按钮**：关闭对话框。|
|5 |**操作字符串**：通常描述启动对话框的人。|

### <a name="responsive-behavior-in-meeting-dialogs"></a>响应行为：会议内对话框

根据不同的方案，会议内对话框的大小可能会有所不同。 确保保持填充和组件大小。

* **Width：** 可以指定对话框的 iframe 的宽度（在支持的大小范围内的任何位置）。
* **高度**：可以在支持的大小范围内的任何位置指定对话框的 iframe 的高度。 如果应用内容超出最大高度，还可以允许用户垂直滚动。

若要实现，使用 键指定宽度和 [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) 高度。

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="示例显示会议内对话框。宽度：最小为 280 像素 (248 像素的 iframe) 。最大为 460 像素 (428 像素的 iframe) 。高度：300 像素 (iframe) 。" border="false":::

## <a name="use-the-shared-meeting-stage"></a>使用共享会议阶段

共享会议阶段可帮助会议参与者实时地与应用内容进行交互和协作。 例如，用户可以专注于编辑文档、使用白板进行集体讨论或查看仪表板。

共享到会议阶段的应用占用的空间与共享屏幕相同。 该阶段将针对所有会议参与者进行重定向。

### <a name="use-cases"></a>用例

共享会议阶段与协作和参与有关。 下面是帮助您入门的一些示例方案。

:::row:::
   :::column span="1":::

**编辑和查看**：深入了解仪表板，与通话中的每个人一起规划。

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review.png" alt-text="示例显示共享会议阶段正在审阅的仪表板。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

**白板：** 在共享画布上一起绘制和创意。

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-whiteboard.png" alt-text="示例显示共享会议阶段上的白板。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

**测验**：使用交互式材料测试知识和获取见解。

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-quiz.png" alt-text="示例在共享会议阶段显示测验。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="anatomy-shared-meeting-stage"></a>结构：共享会议阶段

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy.png" alt-text="图像显示共享会议阶段的设计结构。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**应用图标**：突出显示的图标表示应用的"会议中"选项卡已打开。|
|2|**共享到会议阶段按钮**：将应用共享到会议阶段的入口点。 显示是否将应用配置为使用共享会议阶段。|
|3|**iframe：** 显示应用内容。|
|4 |**"停止共享"** 按钮：停止将应用共享到会议阶段。 仅显示启动共享的参与者。|
|5 |**演示者属性**：显示共享应用的参与者的姓名。|

### <a name="responsive-behavior-shared-meeting-stage"></a>响应行为：共享会议阶段

共享到会议阶段的应用的大小因会议状态和用户调整窗口大小而异。 保持填充和导航和控件的响应式布局，就像在浏览器中一样。

* 侧 **面板**：会议期间，用户随时都可以打开侧面板，以聊天、查看名单或使用应用 (即会议中的选项卡) 。 面板打开时，阶段动态重新排列。
* **视频和音频网格**：视频和音频网格始终可见，以显示会议参与者。 当用户聚焦或固定会议中的某人时，这将增加参与者网格的高度或宽度，具体取决于方向。

#### <a name="meeting-stage-without-side-panel"></a>没有侧 (面板的) 

当侧面板未打开时，默认情况下，会议阶段为 994x678 像素，并且至少为 792x382 像素。

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-no-side-panel.png" alt-text="显示关闭侧面板时共享会议阶段响应的图像。" border="false":::

#### <a name="meeting-stage-with-side-panel"></a>带侧 (面板的) 

侧面板打开时，默认情况下，会议阶段为 918x540 像素，并且至少为 472x382 像素。

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-with-side-panel.png" alt-text="显示侧面板打开时共享会议阶段响应的图像。" border="false":::

## <a name="after-a-meeting"></a>会议后

可以在会议结束后返回到会议并查看应用内容。 本示例中，会议组织者可以在 **Contoso** 选项卡中查看投票结果。 (注意：从设计的角度来看，会议前和会议后选项卡体验之间没有区别。) 

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="示例插图显示会议后选项卡。" border="false":::

## <a name="best-practices"></a>最佳实践

使用上述建议打造优质应用体验。

### <a name="interactions"></a>交互

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="显示如何限制交互数的示例。" border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>操作：限制交互数

对于会议内对话框，删除不帮助用户快速完成某些内容的不必要内容。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="显示如何不引入不必要的元素的示例。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>请勿：引入不必要的元素

具有多个交互的单个会议对话可能会干扰呼叫。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-do.png" alt-text="显示如何创建聚焦环境的示例。" border="false":::

#### <a name="do-create-a-focused-environment"></a>要执行：创建重点环境

我们建议将应用体验的范围仅保留为会议阶段。 你可以将侧面板中的"会议内"选项卡用作某些方案的辅助专用视图。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-dont.png" alt-text="显示会议期间如何不包括竞争图面的示例。" border="false":::

#### <a name="dont-include-competing-surfaces"></a>不要：包括竞争面

你的应用应仅要求用户一次专注于一个图面，无论它是在阶段进行协作还是响应会议内对话框。  (注意：当你的应用处于阶段时，你无法保留由其他应用触发的)  

   :::column-end:::
:::row-end:::

### <a name="layout"></a>布局

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="显示如何使用单列对话框布局的示例。" border="false":::

#### <a name="do-use-a-one-column-dialog"></a>操作：使用单列对话框

由于对话框位于会议阶段的中心，任务完成应快速而简单，以避免用户感到沮丧。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="显示不应使会议扩展空间混乱的示例。" border="false":::

#### <a name="dont-clutter-the-space"></a>Don't： Clutter the space

密集或结构过度的内容可能会让人分心和不知所措，尤其是在会议期间。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="显示单列选项卡布局的示例。" border="false":::

#### <a name="do-use-a-one-column-tab"></a>操作：使用单列选项卡

鉴于"会议"选项卡的窄性质，我们强烈建议在单个列中显示内容。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="显示具有多个列的选项卡的示例。" border="false":::

#### <a name="dont-use-multiple-columns"></a>请勿：使用多个列

由于"会议内"选项卡的空间有限，因此不建议使用具有多个列的布局。

   :::column-end:::
:::row-end:::

### <a name="controls"></a>控件

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="显示如何右对齐主要控件的示例。" border="false":::

#### <a name="do-right-align-the-primary-action"></a>应做：右对齐主要操作

我们建议将视觉最重的操作定位到最右边的位置。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="显示不应左对齐主要控件的示例。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a>不：左对齐或居中对齐操作

这偏离了用于Teams控件放置的标准模式，并且可能会与顶部对话框后面的对话框冲突。

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a>滚动

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="在会议中的选项卡中显示垂直滚动的示例。" border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-do.png" alt-text="显示共享会议阶段中的垂直滚动的示例。" border="false":::

#### <a name="do-scroll-vertically"></a>操作：垂直滚动

用户预期垂直滚动Teams (和任何其他位置) 。 如果你具有创意画布（如白板，用户可以在 x 和 y 轴上平移）。这可能不适用。

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="显示会议内选项卡中水平滚动的示例。" border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-dont.png" alt-text="显示共享会议阶段中的水平滚动的示例。" border="false":::

#### <a name="dont-scroll-horizontally"></a>不：水平滚动

在包括会议环境或会议Teams (，水平滚动不是预期) 。

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>工作流

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="在会议选项卡中显示复杂方案的示例。" border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>Do： Surface complex scenarios in the in-meeting tab

如果你的应用包含多个任务，我们强烈建议将会议中的选项卡与单列布局一同使用。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="在会议对话中显示复杂方案的示例。" border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a>请勿：使会议对话变得复杂

会议内对话框用于简短交互。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>主题

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="显示具有深色主题的会议扩展名的示例。" border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-do.png" alt-text="另一个示例显示具有深色主题的会议扩展。" border="false":::

#### <a name="do-focus-on-dark-theme"></a>应做：专注于深色主题

Teams会议针对深色主题进行了优化，以帮助减少视觉和认知噪音，以便用户可以专注于讨论和共享内容。 请记住特定类型的应用 (如白板和文档编辑) 不需要深色画布。

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="显示颜色与会议主题不匹配的会议扩展的示例。" border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-dont.png" alt-text="另一个示例显示具有与会议主题不匹配的颜色的会议扩展。" border="false":::

#### <a name="dont-use-unfamiliar-colors"></a>请勿：使用不熟悉的颜色

与会议环境发生冲突的颜色可能会分散注意力，对会议环境Teams。 了解颜色渐变[Teams，](https://developer.microsoft.com/fluentui#/styles/web/colors/products)包括调用主题中性色。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>导航

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="显示具有后退按钮的会议扩展名的示例。" border="false":::

#### <a name="do-have-a-back-button"></a>操作：具有"后退"按钮

如果在会议选项卡中具有多个导航层，用户必须能够返回到其以前的视图。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="显示具有两个消除按钮的会议扩展的示例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a>请勿：包含其他消除按钮

提供关闭会议内选项卡内容的选项可能会导致问题，因为标题中已有一个按钮可以关闭会议中的选项卡本身。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="显示会议选项卡 (模式或) 模块的示例。" border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>警告：避免会议内选项卡中的模式

模式 (也称为任务模块) 在已经较窄的会议内选项卡中可能会封装和遮盖内容。

   :::column-end:::
:::row-end:::

### <a name="responsive-behavior"></a>响应行为

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-do.png" alt-text="显示如何正确调整会议扩展大小的示例。" border="false":::

#### <a name="do-resize-and-scale-your-app-responsively"></a>应做：响应式调整应用大小和缩放应用

应用内容应在较小的窗口中动态调整大小和缩小。 使应用的主导航和任何浮动控件可见。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-dont.png" alt-text="显示如何正确调整会议扩展大小的示例。" border="false":::

#### <a name="dont-crop-or-clip-primary-ui-components"></a>不：裁剪或剪裁主要 UI 组件

浮动导航和屏幕外控件和需要滚动查找可能会让用户感到困惑。 当应用内容无法容纳在 iframe 中时，不应水平滚动。

   :::column-end:::
:::row-end:::

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [为会议配置应用](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
