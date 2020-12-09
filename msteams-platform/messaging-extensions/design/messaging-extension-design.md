---
title: 设计邮件扩展
description: 了解如何设计团队消息扩展并获取 Microsoft 团队 UI 工具包。
keywords: 团队设计准则参考邮件扩展提示最佳实践
author: heath-hamilton
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: ad628bdaa46058aed4acdcea1a224c7ebfe40f89
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604805"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a>正在设计你的 Microsoft 团队消息扩展

邮件扩展是用于插入应用程序内容或在不离开对话的情况下对邮件进行操作的快捷方式。

若要指导您的应用程序设计，以下信息介绍并说明了用户如何在团队中添加、使用和管理邮件扩展。

## <a name="microsoft-teams-ui-kit"></a>Microsoft 团队 UI 工具包

您可以在 Microsoft 团队 UI 工具包中找到全面的邮件扩展设计准则，包括您可以根据需要获取和修改的元素。

> [!div class="nextstepaction"]
> [ (Figma) 获取 Microsoft 团队 UI 工具包 ](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a>添加消息扩展

您可以在以下团队上下文中添加消息扩展：

* 从团队存储 (AppSource) 。
* 在频道、聊天或会议 (之前、在 "撰写" 框附近) 的前后。 值得注意的是，如果在其中一个位置添加了邮件扩展插件，则只有您可以在该上下文中使用它。

下面的示例展示了如何在频道中添加邮件扩展。

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="示例演示如何在频道中的撰写框附近添加消息扩展。" border="false":::

## <a name="set-up-a-messaging-extension"></a>设置邮件扩展

身份验证不是强制性的，但是，如果您的应用程序类似于票证跟踪工具，则可能需要用户登录才能使用邮件扩展。

为了实现跨团队应用的一致性，无法自定义登录屏幕。 如果使用单一登录 (SSO) 身份验证，则会自动登录用户。

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="示例显示带有登录按钮的邮件扩展安装程序屏幕。" border="false":::

## <a name="types-of-messaging-extensions"></a>邮件扩展类型

邮件扩展可以包含搜索命令、操作命令或同时具有这两者。 您的命令取决于您的应用程序的功能以及这些功能在团队使用案例中的工作方式。

### <a name="search-commands"></a>搜索命令

使用搜索命令，用户可以使用您的邮件扩展来快速查找外部内容并将其插入到邮件中。 搜索命令通常在 "撰写" 框中可用。 例如，您可以通过共享一小部分内容来启动或添加讨论，而无需离开团队。

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="示例显示从 &quot;撰写&quot; 框启动的基于搜索的邮件扩展插件。" border="false":::

#### <a name="compose-box-layout-options"></a>组合框版式选项

您可以使用一些选项来显示邮件扩展搜索结果，包括 [列表和网格视图](../../messaging-Ask about extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)。

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="显示邮件扩展搜索结果的布局选项的插图。" border="false":::

### <a name="action-commands"></a>操作命令

操作命令使用户能够触发操作并处理团队内的外部服务中的请求。 例如，如果您的应用程序跟踪订单，则用户可以使用同事的邮件中的内容直接在聊天中创建新的订单。

基于操作的邮件扩展通常要求用户在模式中填写表单或某些其他类型的配置。 您可以使用 [任务模块](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)创建这些体验。

## <a name="open-a-messaging-extension"></a>打开消息扩展

"撰写" 框和 "邮件/公告" 是人们使用邮件扩展的主要上下文。

### <a name="from-the-compose-box"></a>从 "撰写" 框

添加后，用户可以通过选择 "撰写" 框下的应用图标打开您的邮件扩展。 在此示例中，扩展包含搜索和操作命令。

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="示例说明如何从 &quot;撰写&quot; 框中打开消息扩展。" border="false":::

### <a name="from-a-chat-message-or-channel-post"></a>从聊天消息或频道帖子

添加后，用户可以选择 **More** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: 聊天消息或频道帖子上的更多图标以查找您的扩展的操作命令。 您的扩展可能会列在 "基于使用情况的 **更多操作** " 下。

#### <a name="chat-message"></a>聊天消息

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="示例说明如何从聊天消息中打开消息扩展。" border="false":::

#### <a name="channel-post"></a>频道帖子

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="示例说明如何从频道公告中打开邮件扩展插件。" border="false":::

## <a name="use-a-messaging-extension"></a>使用消息扩展

以下方案展示了人们使用邮件扩展的主要方式。

### <a name="insert-content-into-a-message"></a>将内容插入邮件

**1. 选择邮件扩展**。 用户可以从 "撰写" 框中搜索要共享的内容。

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="示例显示用户从 &quot;撰写&quot; 框中搜索要插入的内容。" border="false":::

**2. 插入内容**。 发布后，其他人可以答复或选择内容以查看您的应用程序中的详细信息。

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="示例演示了用户将内容发布到频道对话中。" border="false":::

### <a name="take-action-on-a-message"></a>对邮件执行操作

**1. 选择邮件扩展**。 您的应用程序可以包含一个或多个操作命令。

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="示例显示用户选择邮件扩展操作命令。" border="false":::

**2. 完成操作**。 您的应用程序可以接收和处理由邮件操作发送的任何内容或数据。 这样，用户就可以继续在对话中，以下示例不会考虑直接在应用程序中输入信息。

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="示例显示用户从 &quot;撰写&quot; 框中搜索要插入的内容。" border="false":::

### <a name="preview-links"></a>预览链接

邮件扩展还允许您将格式可识别的 URL 中的格式链接插入邮件 (此功能称为 [link unfurling](../../messaging-extensions/how-to/link-unfurling.md)。 ) 

1. 在 "撰写" 框中 **粘贴可识别的链接**。

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="示例显示用户在 &quot;compost&quot; 框中粘贴链接。" border="false":::

**2. 插入内容**。 如果您的应用程序识别了 "撰写" 框中的 URL，则会将该链接呈现为可提供 web 内容的内容丰富预览的卡片。  (有关详细信息，请参阅 [自适应卡片设计指南](../../task-modules-and-cards/cards/design-effective-cards.md) 。 ) 

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="示例显示了由于应用程序识别的 URL，在撰写框中包含一些丰富的内容。" border="false":::

## <a name="manage-a-messaging-extension"></a>管理邮件扩展

通过右键单击您的图标，用户可以固定、删除或配置您的邮件扩展。

## <a name="anatomy"></a>解析

### <a name="messaging-extension-in-the-compose-box"></a>撰写框中的邮件扩展

下面的示例是一个通过撰写框打开的邮件扩展插件。

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="该图显示了撰写框中的邮件扩展的 UI 解析。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**应用徽标**：应用徽标的颜色图标。|
|2 |**应用程序名称**：应用程序的完整名称。|
|3 |**操作命令菜单图标 (可选)**：如果指定任何) ，则打开邮件扩展 (的操作命令列表。
|4 |**搜索框**：允许用户查找他们想要插入的应用内容。|
|5 |**选项卡菜单 (可选)**：提供多个内容类别。|
|6 |**操作命令菜单 (可选)**：如果指定任何) ，则显示操作命令的列表 (。|
|7 |**应用内容**：主要用于显示搜索结果。 下面的示例使用的是列表布局 (网格布局是另一个选项) 。|
|8 |**应用徽标**：应用徽标的大纲图标。|

### <a name="messaging-extension-management-menu"></a>邮件扩展管理菜单

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="显示邮件扩展管理菜单的 UI 解析的图示。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**取消固定**：如果用户已固定你的应用程序，则为可用。|
|2 |**Remove**：从频道、聊天或会议中删除邮件分机号码。|

## <a name="best-practices"></a>最佳做法

### <a name="setup-and-general-usage"></a>设置和常规用法

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="显示邮件扩展最佳实践的示例。" border="false":::

#### <a name="do-integrate-with-single-sign-on"></a>操作：与单一登录集成

SSO 使登录过程更简单、更快速且安全。 此外，如果用户已登录到您的个人应用程序，他们也无需再次登录以访问邮件扩展。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="显示邮件扩展最佳实践的示例。" border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a>请勿：使用户离开对话

邮件扩展是指应减少上下文切换的快捷方式。 例如，您的扩展不应将用户定向到团队外部的网页。

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a>Do：突出显示你的消息扩展

邮件扩展功能并不总是很容易找到。 包括如何在应用程序详细信息页中使用它的屏幕截图。 如果您的应用程序还包含一个 bot，则可以在 "机器人欢迎" 教程中包括邮件扩展帮助文档。

### <a name="templating"></a>模板

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="显示邮件扩展最佳实践的示例。" border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a>操作：让团队能够处理一些设计工作（如果可能）

如果对用例有意义，请考虑创建基于搜索的邮件扩展。 团队使用内置主题和可访问性呈现这些类型的扩展。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="显示邮件扩展最佳实践的示例。" border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a>请勿：在任务模块中嵌入整个应用程序

如果邮件扩展需要操作命令，请保持任务模块简单并仅显示完成该操作所需的组件。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>主题

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="显示邮件扩展最佳实践的示例。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Do：利用团队颜色令牌

每个团队主题都有自己的配色方案。 若要自动处理主题更改，请在设计中使用 <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank"> (熟知的 UI) 的颜色标记 </a> 。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="显示邮件扩展最佳实践的示例。" border="false":::

#### <a name="dont-hard-code-color-values"></a>不：硬编码颜色值

如果您不使用团队颜色令牌，则设计的可伸缩性较小并需要更多时间来管理。

   :::column-end:::
:::row-end:::

### <a name="actions"></a>操作

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="显示邮件扩展最佳实践的示例。" border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a>操作：包括在上下文中有意义的操作命令

邮件操作应与用户所关注的内容相关。 例如，向用户提供用于使用某人的帖子中的文本创建问题或工作项的快捷方式。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="显示邮件扩展最佳实践的示例。" border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a>请勿：包含不是上下文的操作命令

**查看你的仪表板** 的消息操作可能似乎与大多数对话断开连接。

   :::column-end:::
:::row-end:::

### <a name="searches"></a>搜寻

#### <a name="do-show-search-results-while-typing"></a>操作：键入时显示搜索结果

在用户键入时提供建议的搜索结果。 他们可能会以最少的字符数更快地找到所需内容。

#### <a name="dont-require-users-to-submit-a-query"></a>不：要求用户提交查询

您可以让用户按下某个键或选择一个按钮以将查询发送到您的应用程序。 虽然您的应用服务服务可能更简单，但用户可能会感到困惑，他们在键入时不会看到实时搜索结果。

#### <a name="do-consider-zero-term-queries"></a>操作：考虑零期限的查询

例如，用户在搜索框中写入任何内容之前，将显示上次在您的应用程序上查看的内容。 他们可能希望将该内容插入到其对话中。

## <a name="validate-your-design"></a>验证设计

如果计划将应用程序发布到 AppSource，则应了解通常会在提交期间导致应用程序失败的设计问题。

> [!div class="nextstepaction"]
> [检查设计验证准则](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
