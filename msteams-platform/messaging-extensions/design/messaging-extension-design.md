---
title: 设计邮件扩展
description: 了解如何设计 Teams 邮件扩展并获取 Microsoft Teams UI Kit。 描述 Teams 设计指南参考邮件扩展提示最佳实践
author: heath-hamilton
ms.localizationpriority: high
ms.author: surbhigupta
ms.topic: conceptual
ms.openlocfilehash: 2d3d31a0e59be22eb4f84bbdeb70897f4d584b83
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558749"
---
# <a name="designing-your-microsoft-teams-message-extension"></a>设计 Microsoft Teams 邮件扩展

邮件扩展是是插入应用内容或处理邮件而不离开对话的快捷方式。
为指导应用设计，以下信息描述并说明用户可以如何在 Teams 中添加、使用和管理邮件扩展。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

可在 Microsoft Teams UI Kit 中查看全面的邮件扩展设计指南，包括可根据需要获取和修改的元素。

> [!div class="nextstepaction"]
> [获取 Microsoft Teams UI Kit (用户)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-message-extension"></a>添加邮件扩展

可以在以下 Teams 上下文中添加邮件扩展：

* 从 Teams 应用商店。
* 在频道、聊天或会议（会议之前、期间和之后）中的撰写框旁边。 值得注意的是，如果在这些位置之一添加邮件扩展，则只能在该上下文中使用。

以下示例演示如何在频道中添加邮件扩展。

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/messaging-extension/mobile-add-in-channel.png" alt-text="示例演示了如何在移动设备的频道的撰写框附近添加邮件扩展。":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="示例演示了如何在频道的撰写框附近添加邮件扩展。":::

## <a name="set-up-a-message-extension"></a>设置邮件扩展

身份验证不是强制性的，但如果应用类似于票证跟踪工具，则需要用户登录才能使用邮件扩展。

为确保 Teams 应用的一致性，你无法自定义登录屏幕。 如果使用单一登录 (SSO) 身份验证，则用户会自动登录。

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/messaging-extension/mobile-set-up.png" alt-text="示例显示了移动设备上带有登录按钮的邮件扩展设置屏幕。":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="示例显示了带有登录按钮的邮件扩展设置屏幕。":::

## <a name="types-of-message-extensions"></a>邮件扩展类型

邮件扩展可以包含搜索命令、操作命令或两者兼有。 你的命令取决于应用的功能以及这些功能在 Teams 用例中的适用性。

### <a name="search-commands"></a>搜索命令

借助搜索命令，用户可以使用邮件扩展来快速查找外部内容并插入到邮件中。 搜索命令通常在撰写框中可用。 例如，你可以通过共享一段内容来开始讨论或添加到讨论中，而无需离开 Teams。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/messaging-extension/mobile-search-command-type.png" alt-text="示例展示了在移动设备上从撰写框启动的基于搜索的邮件扩展。":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="示例展示了从撰写框启动的基于搜索的邮件扩展。":::

#### <a name="compose-box-layout-options"></a>撰写框布局选项

有多种选项显示邮件扩展搜索结果，包括[列表和网格视图](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)。

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="图例：邮件扩展搜索结果的布局选项":::

### <a name="action-commands"></a>操作命令

操作命令允许用户在 Teams 中触发外部服务的操作和流程请求。 例如，如果应用跟踪订单，则用户可以直接从聊天中，使用同事的消息内容新建订单。

基于操作的邮件扩展通常要求用户填写某个模式中的一个表单或一些其他类型的配置。 你可以使用[任务模块](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)创建这些体验。

## <a name="open-a-message-extension"></a>打开邮件扩展

撰写框和邮件或帖子是用户使用邮件扩展的主要上下文。

### <a name="from-the-compose-box"></a>从撰写框

添加后，用户可以选择撰写框下方的应用图标来打开邮件扩展。 在这些示例中，扩展同时拥有搜索和操作命令。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-compose-box.png" alt-text="示例演示了如何在移动设备上从撰写框打开邮件扩展。":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="示例演示了如何从撰写框打开邮件扩展。":::

### <a name="from-a-chat-message-or-channel-post"></a>从聊天消息或频道帖子

添加后，用户可以选择聊天消息或频道帖子上的“**更多**:::image type="icon" source="../../assets/icons/teams-client-more.png":::”图标来查找扩展的操作命令。 根据使用情况，扩展可能列在 **更多操作** 的下方。

#### <a name="chat-message"></a>聊天消息

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="示例演示了如何从聊天消息打开邮件扩展。":::

#### <a name="channel-post"></a>频道帖子

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="示例演示了如何在移动设备上从频道帖子打开邮件扩展。":::

## <a name="use-a-message-extension"></a>使用邮件扩展

以下场景介绍了用户使用邮件扩展的主要方式。

### <a name="insert-content-into-a-message"></a>在消息中插入内容

**1.选择邮件扩展**。用户可以从撰写框中搜索要共享的内容。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-search.png" alt-text="示例展示了用户在移动设备上从撰写框搜索要插入的内容。":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="示例展示了用户从撰写框搜索要插入的内容。":::

**2.插入内容**。发布内容后，其他人可以回复或选择内容，以查看应用中的详细信息。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-posted.png" alt-text="示例展示了用户在移动设备的频道对话中发布内容。":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="示例展示了用户在频道对话中发布的内容。":::

### <a name="take-action-on-a-message"></a>对消息执行操作

**1.选择邮件扩展**。 应用可以包含一个或多个操作命令。

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="示例演示了用户选择邮件扩展操作命令。":::

**2. 完成操作**。 应用可以接收和处理消息操作发送的任何内容或数据。 用户在继续对话时完成应用中的操作。

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="对消息执行操作的示例。":::

### <a name="preview-links"></a>预览链接

邮件扩展还允许将识别到的 URL 中极具特色的链接插入到邮件中（此功能称为“[链接展开](../../messaging-extensions/how-to/link-unfurling.md)”。）

**1. 在撰写框中粘贴识别到的链接**。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/messaging-extension/mobile-paste-preview-link.png" alt-text="示例演示了用户如何在移动设备上的撰写框中粘贴链接。":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="示例演示了用户如何在撰写框中粘贴链接。":::

**2.插入内容**。如果应用识别出撰写框中的 URL，它会将链接呈现为提供 Web 内容的内容丰富的预览的卡片。（有关详细信息，请参阅 [自适应卡片设计指南](../../task-modules-and-cards/cards/design-effective-cards.md)。）

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-preview-link.png" alt-text="示例演示了在移动设备上 URL 被应用识别后如何在撰写框中包含一些丰富内容。":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="示例演示了在被应用识别后，URL 如何在撰写框中包含一些丰富内容。":::

## <a name="manage-a-message-extension"></a>管理邮件扩展

用户可以通过右键单击图标来固定、删除或配置邮件扩展。

## <a name="anatomy"></a>解剖

### <a name="message-extension-in-the-compose-box"></a>撰写框中的邮件扩展

以下示例展示了从撰写框打开的邮件扩展。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/messaging-extension/mobile-anatomy-compose.png" alt-text="图例：移动设备的撰写框中的邮件扩展的 UI 解剖。":::

|计数器|说明|
|----------|-----------|
|1|**应用名称**：应用的全名。|
|2|**操作命令菜单图标（可选）**：打开邮件扩展的操作命令列表（如果指定）。
|3|**搜索框**：允许用户查找要插入的应用内容。|
|4|**选项卡菜单（可选）**：提供多个内容类别。|
|5|**操作命令菜单（可选）**：显示操作命令列表（如果指定）。|
|6 |**应用内容**：主要用于显示搜索结果。|

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="图例：撰写框中邮件扩展的 UI 解剖。":::

|计数器|说明|
|----------|-----------|
|1|**应用徽标**：应用徽标的彩色图标。|
|2|**应用名称**：应用的全名。|
|3|**操作命令菜单图标（可选）**：打开邮件扩展的操作命令列表（如果指定）。
|4|**搜索框**：允许用户查找要插入的应用内容。|
|5|**选项卡菜单（可选）**：提供多个内容类别。|
|6 |**操作命令菜单（可选）**：显示操作命令列表（如果指定）。|
|7 |**应用内容**：主要用于显示搜索结果。 此处的示例使用的是列表布局（另一个选项是网格布局）。|
|8 |**应用徽标**：应用徽标的大纲图标。|

### <a name="message-extension-management-menu"></a>邮件扩展管理菜单

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="图例：邮件扩展管理菜单的 UI 解剖。":::

|计数器|说明|
|----------|-----------|
|1|**取消固定**：如果用户已固定应用，则可用。|
|2|**删除**：从频道、聊天或会议中删除邮件扩展。|

## <a name="best-practices"></a>最佳做法

使用上述建议打造优质应用体验。

### <a name="setup-and-general-usage"></a>设置和一般用途

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="示例：设置和一般用途。":::

#### <a name="do-integrate-with-single-sign-on"></a>建议：与单一登录集成

S单一登录可使登录过程更轻松、更快速、更安全。此外，如果用户已登录到你的个人应用，则不必重新登录即可访问邮件扩展。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="示例：与单一登录集成。":::

#### <a name="dont-take-users-away-from-the-conversation"></a>不建议：让用户离开对话

邮件扩展是旨在减少上下文切换的快捷方式。 例如，你的扩展不应将用户定向到 Teams 外部的网页。

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-message-extension"></a>建议：突出显示邮件扩展

若要查找邮件扩展通常并不容易。 在应用详细信息页面中包含如何使用教程屏幕截图。 如果应用还包括机器人，则可以在机器人欢迎教程中包含邮件扩展帮助文档。

### <a name="templating"></a>模板化

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="示例：模板化。":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a>建议：如果可能，让 Teams 处理一些设计工作

如果对用例有意义，请考虑创建基于搜索的邮件扩展。 Teams 使用内置主题和辅助功能来呈现这一类型的扩展。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="示例：处理设计工作。":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a>不建议：在任务模块中嵌入整个应用

如果邮件扩展需要操作命令，请保持任务模块的简洁性，并仅显示完成操作所需的组件。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>主题

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="示例：主题。":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>建议：充分利用 Teams 颜色令牌

每个 Teams 主题都有自己的配色方案。 若要自动处理主题更改，请在设计中使用<a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">颜色令牌 (Fluent UI)</a>。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="示例：颜色令牌。":::

#### <a name="dont-hard-code-color-values"></a>不建议：硬编码颜色值

如果不使用 Teams 颜色令牌，则设计将无法缩放，并需要更多时间进行管理。

   :::column-end:::
:::row-end:::

### <a name="actions"></a>操作

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="示例：操作。":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a>建议：包含上下文中有意义的操作命令

消息操作应与用户正在查看的内容相关。 例如，为用户提供使用某人帖子中的文本创建问题或工作项的快捷方式。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="示例：操作命令。":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a>不建议：包含与上下文无关的操作命令

用于 **查看仪表板** 的消息操作，可能似乎与绝大多数对话都没有关联。

   :::column-end:::
:::row-end:::

### <a name="searches"></a>搜索

#### <a name="do-show-search-results-while-typing"></a>建议：键入时显示搜索结果

当用户键入时，提供建议的搜索结果。 用户可以用最少的字符数量，更快地查找到所需内容。

#### <a name="dont-require-users-to-submit-a-query"></a>不建议：要求用户提交查询

可以让用户按一个键或选择一个按钮将查询发送到应用。 虽然从应用服务来看，这样做可能更容易，但用户可能会感到困惑，因为他们在键入时并不能看到实时搜索结果。

#### <a name="do-consider-zero-term-queries"></a>建议：考虑零关键词查询

例如，当用户在搜索框中写入任何内容之前，显示他们上次在应用中查看的内容。 这些可能正是他们希望插入到对话中的内容。
