---
title: 设计任务模块
author: heath-hamilton
description: 了解如何为应用设计任务Teams并获取 Microsoft Teams UI 工具包。
localization_priority: Normal
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 347ce42c41706f698e2f8897a0518aae0850a275
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101728"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a>为应用程序设计Microsoft Teams模块

可以使用任务模块在 Teams应用中创建模式弹出体验。 使用此功能可显示富媒体和信息或完成复杂的任务。

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="示例显示任务模块。" border="false":::

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

可以在自定义 UI 工具包中查找更全面的任务模块设计指南，包括可根据需要获取和修改Microsoft Teams元素。

> [!div class="nextstepaction"]
> [获取 Microsoft Teams UI Kit （用户）](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a>打开任务模块

任务模块几乎可以从你的应用中的任何位置启动。

* **Tab：** 可以从选项卡内的任何链接启动任务模块。在希望用户专注于交互的方案中使用。
* **自动** 程序：可以从自动程序消息内的链接启动任务模块。
* **自适应卡片**：任务模块可以从随消息传递扩展 (发送的自适应卡片启动，也可在用户选择按钮) 自动程序启动。
* **邮件扩展 (操作命令) ：** 邮件扩展允许您对邮件内容执行特定操作。 选择操作将打开任务模块。
* **邮件扩展 (撰写**) ：在撰写框中，可以设计邮件扩展以打开任务模块，而不是典型的飞出框。 保留用于复杂交互的任务模块，例如完成表单。

## <a name="anatomy"></a>解剖

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="显示任务模块的 UI 分析的图示。" border="false":::

任务模块非常灵活。 它们可以使用 iframe 生成，并拉取其他 UI 模板，以托管合作伙伴构建的体验。 这是最完善体验的首选。

它们还可使用自适应卡片框架生成[](../../task-modules-and-cards/cards/design-effective-cards.md)，该框架可以更简单、更快速地执行窗体或 (应用场景) 。

|计数器|说明|
|----------|-----------|
|1|**应用程序图标**|
|2|**应用名称**：应用的完整名称。|
|3|**标头**：使标题简洁明了。 描述希望用户完成的任务。
|4 |**关闭按钮**：允许用户查找要插入的应用内容。|
|5 |**iframe：** 托管应用内容的响应空间。|
|6 |**操作 (可选) ：** 与应用内容相关的按钮。|

## <a name="designing-with-ui-templates"></a>使用 UI 模板进行设计

请考虑对任务模块中的常见布局使用模板。 每个组件都由较小的组件组成，以创建一个简洁、响应迅速的设计，该设计可以使用开箱即用或针对你的方案进行自定义，或者与品牌外观一起自定义。

* [列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目采取操作。
* [表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单用于以结构化方式收集、验证和提交用户输入。
* [空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。

## <a name="examples"></a>示例

### <a name="list"></a>列表

列表在任务模块中运行得非常好，因为它们易于扫描。

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="任务模块中的示例列表。" border="false":::

### <a name="form"></a>表单

任务模块是显示具有顺序用户输入和内联验证的表单的一个很好的位置。 可以利用自适应卡片作为嵌入表单元素的一种方式。

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="任务模块中的示例窗体。" border="false":::

### <a name="sign-in"></a>登录

创建具有一系列任务模块的集中登录或注册流，使用户能够在顺序步骤中轻松移动。

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="任务模块中的登录体验示例。" border="false":::

### <a name="media"></a>Media

在任务模块中嵌入媒体内容，实现集中的观看体验。

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="任务模块中的媒体内容示例。" border="false":::

### <a name="empty-state"></a>空状态

用于欢迎、错误和成功消息。

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="任务模块中的空状态示例。" border="false":::

### <a name="image-gallery"></a>图像库

在 iframe 中嵌入库的盘点。

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="任务模块中的示例图像库。" border="false":::

### <a name="poll"></a>投票

此示例显示从自适应卡片启动的投票结果。 轮询也可以放置在任务模块内。

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="任务模块中的轮询示例。" border="false":::

## <a name="best-practices"></a>最佳做法

使用这些建议创建高质量的应用体验。

### <a name="usability"></a>可用性

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="显示任务模块最佳实践的示例 (一个任务模块一) 。" border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a>应做：一次使用一个任务模块

目标是使用户专注于完成一项任务！

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="示例显示任务模块最佳实践 (在任务模块模型顶部弹出) 。" border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a>请勿：在任务模块顶部弹出对话框

这将创建一种没有焦点的、令人困惑的用户体验。

   :::column-end:::
:::row-end:::

### <a name="responsive"></a>快速响应

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="显示任务模块最佳实践的示例 (确保内容响应迅速) 。" border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a>应做：确保内容响应迅速

虽然任务模块中托管的自适应卡片在移动设备上可正常呈现，但如果选择使用 iframe 托管应用内容，请确保 UI 响应迅速且跨设备运行良好。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="显示任务模块最佳实践的示例 (不使用水平滚动条) 。" border="false":::

#### <a name="dont-use-horizontal-scroll-bars"></a>禁止：使用水平滚动条

最佳做法是使内容保持集中，不要过长。 如果需要滚动，请垂直滚动，而不是水平滚动。

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a>简单性

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="显示任务模块最佳实践的示例 (使任务模块) 。" border="false":::

#### <a name="do-keep-it-short"></a>应做：保持简短

你可以轻松创建多步骤向导，但这并不意味着你应该！ 多屏幕任务模块可能会出现问题，因为传入的消息会分散注意力并吸引用户退出。 如果确实涉及你的任务，请弹出到完整网页，而不是任务模块。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="显示任务模块最佳实践的示例 (操作没有长交互) 。" border="false":::

#### <a name="dont-have-long-interactions"></a>请勿：进行长交互

尽量使交互保持简短并达到目标。

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a>错误消息

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="显示任务模块最佳实践的示例 (内嵌错误消息) 。" border="false":::

#### <a name="do-use-inline-error-messages"></a>Do：使用内联错误消息

有关内嵌错误处理的准则，请参阅表单 UI 模板。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="显示任务模块最佳实践的示例 (将错误消息放入对话框) 。" border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a>请勿：在对话框中放入错误消息

不要在任务模块顶部的对话框中弹出错误消息。 它创建令人困惑的用户体验。

   :::column-end:::
:::row-end:::
