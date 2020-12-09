---
title: 正在设计任务模块
author: heath-hamilton
description: 了解如何为团队应用程序设计任务模块，并获取 Microsoft 团队 UI 工具包。
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 41584ecf58ca7718290e58e5845549e4579dac64
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605964"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a>为 Microsoft 团队应用程序设计任务模块

您可以使用任务模块在团队应用程序中创建模式弹出窗口体验。 使用此功能可以显示富媒体和信息或完成复杂的任务。

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="示例显示了任务模块。" border="false":::

## <a name="microsoft-teams-ui-kit"></a>Microsoft 团队 UI 工具包

您可以在 Microsoft 团队 UI 工具包中找到更全面的任务模块设计指南，包括可在需要时获取和修改的元素。

> [!div class="nextstepaction"]
> [ (Figma) 获取 Microsoft 团队 UI 工具包 ](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a>打开任务模块

可以从应用程序中的几乎任意位置启动任务模块。

* **选项卡**：可以从选项卡或 iframe 中的任何链接启动任务模块。 在希望用户关注交互的情况下使用。
* **Bot**：任务模块可从 Bot 邮件中的链接启动。
* **自适应卡片**：任务模块可以从自适应卡片启动， (随邮件扩展或由 bot 一起发送，) 当用户选择按钮时。
* **邮件扩展 (操作命令)**：邮件扩展允许您对邮件内容执行特定操作。 选择操作将打开任务模块。
* **邮件扩展 ("撰写框" 上下文)**：在 "撰写" 框中，您可以设计邮件扩展以打开任务模块，而不是典型的浮出控件。 为复杂的交互（如完成表单）保留任务模块。

## <a name="anatomy"></a>解析

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="显示任务模块的 UI 解析的插图。" border="false":::

任务模块是非常灵活的曲面。 可以使用 iframe （用于提取其他 UI 模板）来构建合作伙伴构建体验。 这是为了获得最精美的体验的首选。

还可以使用 [自适应卡片](../../task-modules-and-cards/cards/design-effective-cards.md) 框架生成，这是一种更简单、更快的方法来执行常见方案 (如表单) 。

|计数器|说明|
|----------|-----------|
|1|**应用程序图标**|
|2 |**应用程序名称**：应用程序的完整名称。|
|3 |**标头**：使标头清晰明了。 描述您希望用户完成的任务。
|4 |"**关闭" 按钮**：允许用户查找他们想要插入的应用内容。|
|5 |**iframe**：承载应用内容的响应空间。|
|6 |**操作 (可选)**：与应用程序内容相关的按钮。|

## <a name="designing-with-ui-templates"></a>使用 UI 模板进行设计

请考虑在任务模块中使用常用布局模板。 每个组件都由较小的组件组成，以创建可供使用或自定义的现成、适合您的方案或品牌外观的小型的快速响应设计。

* [列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可浏览的格式显示相关项目，并允许用户对整个列表或单个项目执行操作。
* [表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单以结构化方式收集、验证和提交用户输入。
* [空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。

## <a name="examples"></a>示例

### <a name="list"></a>列表

由于易于扫描，列表在任务模块中工作良好。

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="任务模块中的示例列表。" border="false":::

### <a name="form"></a>表单

任务模块是具有顺序用户输入和内联验证的表面外观。 可以使用自适应卡片作为嵌入表单元素的一种方式。

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="任务模块中的示例表单。" border="false":::

### <a name="sign-in"></a>登录

创建具有一系列任务模块的重点登录或注册流，从而让用户可以通过连续步骤轻松移动。

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="示例在任务模块中登录体验。" border="false":::

### <a name="media"></a>媒体

在任务模块中嵌入媒体内容以获得重点查看体验。

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="任务模块中的示例媒体内容。" border="false":::

### <a name="empty-state"></a>空状态

用于 "欢迎"、"错误" 和 "成功" 消息。

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="任务模块中的空状态示例。" border="false":::

### <a name="image-gallery"></a>图像库

在 iframe 中嵌入库轮播。

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="任务模块中的示例图像库。" border="false":::

### <a name="poll"></a>轮询

本示例显示从自适应卡片启动的轮询结果。

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="在任务模块中轮询的示例。" border="false":::

## <a name="best-practices"></a>最佳做法

### <a name="usability"></a>可用性

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="显示任务模块最佳实践的示例。" border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a>操作：一次使用一个任务模块

目标是将用户重点放在所有工作之后完成一项任务！

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="显示任务模块最佳实践的示例。" border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a>不：在任务模块顶部弹出对话框

这将创建一个 unfocused、令人困惑的用户体验。

   :::column-end:::
:::row-end:::

### <a name="responsive"></a>快速响应

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="显示任务模块最佳实践的示例。" border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a>执行以下操作：确保内容响应

虽然任务模块中托管的自适应卡在移动设备上的呈现效果很好，但如果您选择使用 iframe 来承载应用程序内容，请确保 UI 的响应速度良好且在设备之间能够正常工作。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="显示任务模块最佳实践的示例。" border="false":::

#### <a name="dont-use-horizontal-scrollbars"></a>不：使用水平滚动条

最佳做法是保持内容的重点和不太长。 如果需要滚动，请垂直或不水平滚动。

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a>简洁性

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="显示任务模块最佳实践的示例。" border="false":::

#### <a name="do-keep-it-short"></a>Do：将其缩短

您可以轻松地创建一个多步骤向导，但这并不一定意味着您应该！ 由于传入的邮件会分散注意力并 tempt 用户退出，因此多屏幕任务模块可能会出现问题。 如果你的任务真正涉及，请弹出到完整的网页而不是任务模块。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="显示任务模块最佳实践的示例。" border="false":::

#### <a name="dont-do-long-interactions"></a>不：执行长时间交互

尝试保持交互的简短和点。

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a>错误消息

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="显示任务模块最佳实践的示例。" border="false":::

#### <a name="do-use-inline-error-messages"></a>Do： Use inline error messages

有关内联错误处理的准则，请参阅窗体 UI 模板。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="显示任务模块最佳实践的示例。" border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a>请勿：在对话框中放置错误消息

不要在任务模块顶部的对话框中弹出错误消息。 它将创建令人费解的用户体验。

   :::column-end:::
:::row-end:::
