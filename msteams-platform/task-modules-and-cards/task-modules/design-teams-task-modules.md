---
title: 设计任务模块
author: heath-hamilton
description: 了解如何设计 Teams 应用的任务模块并获取 Microsoft Teams UI 工具包。
ms.localizationpriority: high
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 1514ed8e3101065efd482ced45de98b8b0f58ab8
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104131"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a>为 Microsoft Teams 应用设计任务模块

可以使用任务模块在 Teams 应用中创建模式弹出式体验。 使用此功能可显示丰富的媒体和信息，或完成复杂的任务。

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="示例显示任务模块。" border="false":::

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

可在 Microsoft Teams UI Kit 中查看更全面的任务模块设计指南，包括可根据需要获取和修改的元素。

> [!div class="nextstepaction"]
> [获取 Microsoft Teams UI Kit (用户)](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a>打开任务模块

任务模块几乎可以从应用中的任意位置启动。

* **选项卡**: 任务模块可以从选项卡内的任意链接启动。情在希望用户专注于互动的情况下使用。
* **机器人**: 任务模块可以从机器人消息中的链接启动。
* **自适应卡片**: 当用户选择按钮时，可以从自适应卡片 (使用消息扩展或机器人发送) 启动任务模块。
* **消息扩展（操作命令）**：消息扩展允许你对消息内容执行特定操作。选择操作将打开任务模块。
* **消息扩展（撰写框上下文）**：在撰写框中，可以设计消息扩展来打开任务模块，而不是典型的浮出控件。保留任务模块以进行复杂交互，例如完成表单。

## <a name="anatomy"></a>解剖

任务模块为托管应用体验提供了灵活的图面。它们是使用 iframe（桌面）或 Web 视图（移动设备）生成的，因此你可以使用我们的 UI 模板（推荐）或从头开始设计任务模块。

它们也可以使用[自适应卡片](../../task-modules-and-cards/cards/design-effective-cards.md)框架生成，这可以是更简单、更快地促进常见的方案(如表单)。

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/task-module/mobile-task-module-anatomy.png" alt-text="插图显示了移动端任务模块的 UI 解剖。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**标题**: 让标题清晰简洁。 描述希望用户完成的任务。
|2|**应用名称**：应用的全名。|
|3|**关闭按钮**: 关闭任务模块。 不应应用内容中未保存的更改。|
|4|**webview**: 托管应用内容的响应空间。|
|5|**操作(可选)**: 与应用内容相关的按钮。|

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="插图显示了任务模块的 UI 解剖。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**应用图标**|
|2|**应用名称**：应用的全名。|
|3|**标题**: 让标题清晰简洁。 描述希望用户完成的任务。
|4|**关闭按钮**: 关闭任务模块。 不应应用内容中未保存的更改。|
|5|**iframe**: 托管应用内容的响应空间。|
|6 |**操作(可选)**: 与应用内容相关的按钮。|

## <a name="designing-with-ui-templates"></a>使用 UI 模板进行设计

请考虑对任务模块中的常见布局使用模板。每个组件都由较小的组件组成，可创建一个精致的响应式设计，该设计可以现成地使用或针对你的方案或品牌外观进行自定义。

* [列表](../../concepts/design/design-teams-app-ui-templates.md#list): 列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目执行操作。
* [表单](../../concepts/design/design-teams-app-ui-templates.md#form): 表单是用于收集、验证和提交用户输入的结构化方式。
* [空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空状态模板可用于许多方案，包括登录、首次运行体验、错误消息等。

## <a name="examples"></a>示例

### <a name="list"></a>列出

列表在任务模块中运行良好，因为它们易于扫描。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/task-module/mobile-list.png" alt-text="移动设备上任务模块中的示例列表。" border="false":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="任务模块中的示例列表。" border="false":::

### <a name="form"></a>表单

任务模块是显示具有顺序用户输入和内联验证表单的好地方。 可以利用自适应卡片作为嵌入表单元素的方法。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/task-module/mobile-form.png" alt-text="移动设备上任务模块中的示例表单。" border="false":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/form.png" alt-text="任务模块中的示例表单。" border="false":::

### <a name="sign-in"></a>登录

使用一系列任务模块创建重点登录或注册流程，使用户能够轻松完成顺序步骤。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/task-module/mobile-sign-in.png" alt-text="移动设备上任务模块中的登录体验示例。" border="false":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="任务模块中的登录体验示例。" border="false":::

### <a name="media"></a>媒体

在任务模块中嵌入媒体内容，以获得重点查看体验。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/task-module/mobile-media.png" alt-text="移动设备上任务模块中的示例媒体内容。" border="false":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="任务模块中的示例媒体内容。" border="false":::

### <a name="empty-state"></a>空状态

用于欢迎、错误和成功消息。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/task-module/mobile-empty-state.png" alt-text="移动设备上任务模块中的示例空状态。" border="false":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="任务模块中的示例空状态。" border="false":::

### <a name="image-gallery"></a>图像库

在 iframe(桌面)或 Webview(移动版)中嵌入库轮播。

##### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/task-module/mobile-image-gallery.png" alt-text="移动设备上任务模块中的示例图像库。" border="false":::

##### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="任务模块中的示例图像库。" border="false":::

### <a name="poll"></a>投票

此示例显示从自适应卡启动的投票结果。 投票也可以放置在任务模块中。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/task-module/mobile-poll.png" alt-text="移动设备上任务模块中的示例投票。" border="false":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="任务模块中的示例投票。" border="false":::

## <a name="best-practices"></a>最佳实践

使用上述建议打造优质应用体验。

### <a name="usability"></a>可用性

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="显示任务模块最佳做法(一次一个任务模块)的示例。" border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a>请执行: 一次使用一个任务模块

目标是让用户专注于完成一项任务！

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="显示任务模块最佳做法(在任务模块的顶部弹出对话框)的示例。" border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a>请勿执行: 在任务模块顶部弹出对话框

这会创造一种无重点且混乱的用户体验。

   :::column-end:::
:::row-end:::

### <a name="responsive"></a>快速响应

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="显示任务模块最佳做法(请确保内容快速响应)的示例。" border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a>请执行: 确保内容快速响应

尽管任务模块中托管的自适应卡片在移动设备上呈现良好，但如果选择使用 iframe 来托管应用内容，请确保 UI 响应迅速且跨设备运行良好。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="显示任务模块最佳做法(不使用水平滚动条)的示例。" border="false":::

#### <a name="dont-use-horizontal-scroll-bars"></a>请勿执行: 使用水平滚动条

最佳做法是使内容保持专注，且不会过长。 如果需要滚动，请垂直滚动，而不是水平滚动。

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a>简单

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="显示任务模块最佳做法(保持简短)的示例。" border="false":::

#### <a name="do-keep-it-short"></a>请执行: 保持简短。

可以轻松创建多步骤向导，但这并不一定意味着应该这么做！ 多屏任务模块可能会出现问题，因为传入的消息会分散注意力并诱使用户退出。 如果任务确实有涉及到，请弹出完整的网页，而不是任务模块。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="显示任务模块最佳做法(请勿有长交互)的示例。" border="false":::

#### <a name="dont-have-long-interactions"></a>请勿执行: 具有长交互

尽量使交互简短而有针对性。

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a>错误消息

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="显示任务模块最佳做法(使用内联错误信息)的示例。" border="false":::

#### <a name="do-use-inline-error-messages"></a>执行: 使用内联错误信息

有关内联错误处理的指南，请参阅表单 UI 模板。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="显示任务模块最佳做法(将错误信息放在对话框中)的示例。" border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a>请勿执行: 将错误信息放在对话框中

不要在任务模块顶部的对话框中弹出错误消息。这会造成令人困惑的用户体验。

   :::column-end:::
:::row-end:::
