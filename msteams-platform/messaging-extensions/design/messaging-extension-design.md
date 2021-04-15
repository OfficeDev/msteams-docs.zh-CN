---
title: 设计邮件扩展
description: 了解如何设计 Teams 消息传递扩展和获取 Microsoft Teams UI 工具包。
keywords: 团队设计指南参考消息传递扩展提示最佳做法
author: heath-hamilton
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: c616d8e3e7c40ae124f96cb80a42873f9aaa7865
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51697009"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a>设计 Microsoft Teams 消息传递扩展

消息传递扩展是插入应用内容或在离开对话的情况下对消息操作快捷方式。
为了指导你的应用设计，以下信息介绍了并说明了用户如何在 Teams 中添加、使用和管理消息传递扩展。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

可以在 Microsoft Teams UI 工具包中查找全面的消息传递扩展设计指南，包括可根据需要获取和修改的元素。

> [!div class="nextstepaction"]
> [获取 Microsoft Teams UI Kit （用户）](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a>添加消息传递扩展

可以在以下 Teams 上下文中添加消息传递扩展：

* 从 Teams 应用商店 （AppSource）。
* 在靠近撰写框 (、在频道、聊天或会议) 、聊天或会议。 值得注意的是，如果您在这些位置之一添加邮件扩展，则仅可以在该上下文中使用它。

以下示例演示如何在频道中添加消息扩展。

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="示例演示如何在频道中的撰写框附近添加消息传递扩展。" border="false":::

## <a name="set-up-a-messaging-extension"></a>设置邮件扩展

身份验证不是强制性的，但是如果你的应用与票证跟踪工具类似，你可能需要用户登录以使用消息传递扩展。

若要跨 Teams 应用保持一致，你无法自定义登录屏幕。 如果使用单一登录 (SSO) 身份验证，用户将自动登录。

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="示例显示具有登录按钮的消息扩展设置屏幕。" border="false":::

## <a name="types-of-messaging-extensions"></a>邮件扩展类型

邮件扩展可以具有搜索命令和/或操作命令。 你的命令取决于你的应用的功能以及这些功能在 Teams 用例中的适应情况。

### <a name="search-commands"></a>搜索命令

借助搜索命令，用户可以使用邮件扩展快速查找外部内容并插入邮件。 搜索命令通常可在撰写框中使用。 例如，可以通过共享一段内容开始讨论或添加讨论，而无需离开 Teams。

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="示例显示从撰写框启动的基于搜索的邮件扩展。" border="false":::

#### <a name="compose-box-layout-options"></a>撰写框布局选项

有一些选项用于显示邮件扩展搜索结果，包括 [列表和网格视图](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)。

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="插图显示邮件扩展搜索结果的布局选项。" border="false":::

### <a name="action-commands"></a>操作命令

操作命令允许用户在 Teams 中的外部服务中触发操作并处理请求。 例如，如果您的应用程序跟踪订单，则用户可以使用同事消息的内容从聊天的右侧创建新订单。

基于操作的邮件扩展通常需要用户在模式内完成表单或某种其他种类的配置。 可以使用任务模块 创建 [这些体验](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)。

## <a name="open-a-messaging-extension"></a>打开消息传递扩展

撰写框和邮件/公告是人们使用邮件扩展的主要上下文。

### <a name="from-the-compose-box"></a>从撰写框

添加后，用户可以通过选择撰写框下方的应用图标来打开邮件扩展。 本示例中，扩展具有搜索和操作命令。

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="示例演示如何从撰写框中打开邮件扩展。" border="false":::

### <a name="from-a-chat-message-or-channel-post"></a>从聊天消息或频道帖子

添加后，用户可以选择聊天消息或频道帖子上的"更多"图标 :::image type="icon" source="../../assets/icons/teams-client-more.png"::: 来查找扩展的操作命令。 扩展名可能列在"基于 **使用情况的更多** 操作"下。

> [!NOTE]
> Microsoft Teams 移动平台上不支持聊天消息或频道帖子中的更多操作。 

#### <a name="chat-message"></a>聊天消息

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="示例演示如何从聊天消息中打开消息扩展。" border="false":::

#### <a name="channel-post"></a>频道帖子

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="示例演示如何从频道帖子打开消息传递扩展。" border="false":::

## <a name="use-a-messaging-extension"></a>使用消息传递扩展

以下方案显示了人们使用邮件扩展的主要方式。

### <a name="insert-content-into-a-message"></a>将内容插入到邮件中

**1. 选择邮件扩展**。 用户可以从撰写框中搜索要共享的内容。

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="示例显示用户搜索要从撰写框中插入的内容。" border="false":::

**2. 插入内容**。 发布后，其他人可以回复或选择内容以查看应用中的更多信息。

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="示例显示用户在频道对话中发布内容。" border="false":::

### <a name="take-action-on-a-message"></a>对邮件采取措施

**1. 选择邮件扩展**。 你的应用可以包含一个或多个操作命令。

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="示例显示用户选择消息传递扩展操作命令。" border="false":::

**2. 完成操作**。 你的应用可以接收并处理邮件操作发送的任何内容或数据。 这允许用户保持其对话，并且（以下示例）无需担心直接在应用中输入信息。

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="如何对邮件采取操作的示例。" border="false":::

### <a name="preview-links"></a>预览链接

邮件扩展还允许您将识别的 URL 中的丰富链接插入邮件 (此功能称为链接取消展开[.) ](../../messaging-extensions/how-to/link-unfurling.md)

**1. 在撰写框中** 粘贴可识别的链接。

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="示例显示用户在合成器框中粘贴链接。" border="false":::

**2. 插入内容**。 如果你的应用识别撰写框中的 URL，它将链接呈现为提供 Web 内容的内容丰富的预览的卡片。  (有关详细信息， [请参阅自适应卡片](../../task-modules-and-cards/cards/design-effective-cards.md) 设计指南) 

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="示例显示 URL 如何由你的应用识别，在撰写框中包含一些丰富的内容。" border="false":::

## <a name="manage-a-messaging-extension"></a>管理消息传递扩展

通过右键单击图标，用户可以固定、删除或配置邮件扩展。

## <a name="anatomy"></a>解剖

### <a name="messaging-extension-in-the-compose-box"></a>撰写框中的消息扩展

下面的示例是一个从撰写框打开的消息扩展。

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="插图显示撰写框中消息传递扩展的 UI 结构。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**应用徽标**：应用徽标的颜色图标。|
|2|**应用名称**：应用的完整名称。|
|3|**操作命令菜单图标 (可选**) ：如果指定任何命令， (邮件扩展策略打开操作) 。
|4 |**搜索框**：允许用户查找要插入的应用内容。|
|5 |**选项卡菜单 (可选) ：** 提供多个内容类别。|
|6 |**操作命令菜单 (可选) ：** 如果指定任何 (，将显示操作命令) 。|
|7 |**应用内容**：主要用于显示搜索结果。 此处的示例是使用列表布局 (网格布局是另一个选项) 。|
|8 |**应用徽标**：应用徽标的大纲图标。|

### <a name="messaging-extension-management-menu"></a>邮件扩展管理菜单

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="插图显示消息扩展管理菜单的 UI 结构。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**取消固定**：如果用户已固定你的应用，则可用。|
|2|**删除**：从频道、聊天或会议中删除消息扩展。|

## <a name="best-practices"></a>最佳做法

### <a name="setup-and-general-usage"></a>设置和常规用法

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="有关安装和常规用法的示例。" border="false":::

#### <a name="do-integrate-with-single-sign-on"></a>操作：与单一登录集成

SSO 使登录过程更加轻松、快速和安全。 此外，如果用户已登录到你的个人应用，他们也不必再次登录来访问邮件扩展。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="与单一登录集成的示例。" border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a>请勿：使用户离开对话

消息传递扩展是应该减少上下文切换的快捷方式。 例如，你的扩展不应将用户引导到 Teams 外部的网页。

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a>要执行：突出显示邮件扩展

邮件扩展并不总是易于查找。 在应用详细信息页面中包括如何使用它的屏幕截图。 如果你的应用还包括机器人，你可以将消息传递扩展帮助文档包括在机器人欢迎教程中。

### <a name="templating"></a>模板

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="模板示例。" border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a>完成：如果可能，让 Teams 处理一些设计工作

如果对用例有意义，请考虑创建基于搜索的邮件扩展。 Teams 通过内置 theming 和辅助功能呈现这些类型的扩展。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="有关处理设计工作的示例。" border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a>请勿：在任务模块中嵌入整个应用

如果邮件扩展需要操作命令，请保持任务模块简单，并仅显示完成该操作所需的组件。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>主题

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="有关 theming 的示例。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>应做：利用 Teams 颜色令牌

每个 Teams 主题都有自己的配色方案。 若要自动处理主题更改，请 <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank"> (Fluent UI </a>) 颜色标记。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="有关颜色令牌的示例。" border="false":::

#### <a name="dont-hard-code-color-values"></a>请勿：硬编码颜色值

如果不使用 Teams 颜色令牌，你的设计将不太可扩展，并且需要更多的时间进行管理。

   :::column-end:::
:::row-end:::

### <a name="actions"></a>操作

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="操作示例。" border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a>应做：在上下文中包括有意义的操作命令

邮件操作应该与用户正在查看的内容相关。 例如，为用户提供使用某人帖子中的文本创建问题或工作项的快捷方式。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="操作命令示例。" border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a>请勿：包括不与上下文相关的操作命令

查看仪表板 **的消息** 操作可能看起来与大多数对话断开连接。

   :::column-end:::
:::row-end:::

### <a name="searches"></a>搜索

#### <a name="do-show-search-results-while-typing"></a>Do：在键入时显示搜索结果

在用户键入时提供建议的搜索结果。 他们可以以最少的字符更快地找到所需的内容。

#### <a name="dont-require-users-to-submit-a-query"></a>请勿：要求用户提交查询

你可以让用户按某个键或选择一个按钮将查询发送到你的应用。 虽然这在你的应用服务服务上可能更容易，但人们可能会感到困惑，因为他们不会在键入时看到实时搜索结果。

#### <a name="do-consider-zero-term-queries"></a>应做：考虑零术语查询

例如，在用户向搜索框中写入任何内容之前，显示他们上次在你的应用上查看过什么内容。 他们可能会想要将这些内容插入对话中。

## <a name="validate-your-design"></a>验证你的设计

如果计划将应用发布到 AppSource，应了解提交过程中通常会导致应用出现故障的设计问题。

> [!div class="nextstepaction"]
> [检查设计验证准则](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
