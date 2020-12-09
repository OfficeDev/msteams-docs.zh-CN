---
title: 正在设计你的 bot
description: 了解如何设计团队 bot 并获取 Microsoft 团队 UI 工具包。
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d1a7470f4986de22ecca7071823b620cb0234abb
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605390"
---
# <a name="designing-your-microsoft-teams-bot"></a>正在设计你的 Microsoft 团队 bot

Bot 是执行一组特定任务的会话中应用程序。 根据 <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot 框架</a>，bot 与用户进行通信，响应他们的问题，并主动通知他们发生更改和其他事件。 这是一种很好的方法。

若要指导您的应用程序设计，以下信息介绍并说明了用户如何在团队中添加、使用和管理 bot。

## <a name="microsoft-teams-ui-kit"></a>Microsoft 团队 UI 工具包

您可以在 Microsoft 团队 UI 工具包中找到更全面的 bot 设计指南，包括您可以根据需要获取和修改的元素。

> [!div class="nextstepaction"]
> [ (Figma) 获取 Microsoft 团队 UI 工具包 ](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a>添加 bot

聊天、频道和个人应用中提供了 bot。 您可以通过以下方式之一添加机器人：

* 从团队存储 (AppSource) 。
* 通过在工作组左侧选择 " **更多** " 图标来使用应用浮出控件。
* 在 "新聊天" 或 "撰写" 框中使用 @mention (下面的示例演示如何在组聊天) 中执行此操作。

:::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="示例演示如何使用 @mention 在组中添加机器人。" border="false":::

## <a name="introduce-a-bot"></a>引入机器人

你的 bot 会自行引入并描述它可以执行的操作，这一点非常重要。 此初始 exchange 可帮助用户了解如何使用 bot，找出它的局限性，最重要的是，让他们能够轻松地与之进行交互。

### <a name="welcome-message-in-a-one-on-one-chat"></a>一对一聊天中的欢迎消息

在个人上下文中，欢迎邮件设置你的 bot 的语气。 该邮件包含问候语、bot 可以执行的操作以及有关如何在 (进行交互的一些建议（例如，"请尝试询问我 ..."） ) 。 如果可能，这些建议应返回存储的响应，而无需登录。

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="示例显示了个人应用程序中的 bot 简介。" border="false":::

### <a name="introductions-in-group-chats-and-channels"></a>群研讨和频道中的简介

你的 bot 的简介与个人上下文 (（如个人应用) ）相比，在组聊天和频道中略有不同。 在实际生活中，如果你输入的会议室完全为人，则为你将自行引入，而不是欢迎大家已经在那里的人。 将这种想法引入到你的 bot 设计中。

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="示例显示了协作上下文中的 bot 简介。" border="false":::

### <a name="bot-authentication-with-single-sign-on"></a>单一登录的 Bot 身份验证

当某个人将邮件发送到 bot 时，可能需要登录才能使用其所有功能。 您可以使用单一登录 (SSO) 简化身份验证过程。

别忘了：在机器人命令菜单中 (**我可以执行哪些操作？**) ，还必须提供命令来注销。

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="示例显示了带有登录按钮的 bot。" border="false":::

### <a name="tours"></a>漫游

您可以包含欢迎邮件的教程，如果 bot 响应的是 "帮助" 命令之类的内容。 教程是描述你的 bot 可以执行的操作的最有效方式。 如果适用，它们也很适合描述应用程序的其他功能 (例如，包括邮件扩展) 的屏幕截图。

> [!IMPORTANT]
> 无需登录即可访问教程。

#### <a name="one-on-one-chats"></a>一对一聊天

在个人应用程序中，轮播可提供对你的 bot 和你的应用程序的任何其他功能的有效概述。 包含按钮鼓励用户尝试使用 bot 命令 (例如， **创建任务**) 。

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="示例显示了一次一对一聊天中的 bot 教程。" border="false":::

#### <a name="channels-and-group-chats"></a>频道和组聊天

在频道和群研讨中，应在模式 (（也称为 [任务模块](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) ）中打开一个教程，使其不会中断正在进行的对话。 这还为您提供了为您的演示实现基于角色的视图的选项。

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="示例显示频道中的 bot 教程。" border="false":::

## <a name="chat-with-a-bot"></a>与 bot 聊天

Bot 直接集成到团队的消息传递框架中。 用户可以与机器人聊天以获取其问题，或键入命令让 bot 执行一组或一组特定的任务。 Bot 可以通过聊天主动通知用户对你的应用所做的更改或更新。

### <a name="chat-with-a-bot-in-different-contexts"></a>与不同上下文中的 bot 聊天

您可以在以下上下文中使用 bot：

* **个人应用程序**：在个人应用程序中，bot 具有专用的聊天选项卡。
* **一对一聊天**：用户可以启动与 bot 的专用对话。 这与在个人应用程序中使用 bot 的体验相同。
* **分组聊天**：用户可以通过 @mentioning bot 与组聊天中的 bot 进行交互。
* **频道**：用户可以与频道中的 bot 进行交互。 通过 @mentioning "撰写" 框中的 bot 名称。 请记住，在此上下文中，bot 可用于整个团队，而不仅仅是通道。

### <a name="anatomy"></a>解析

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="示例显示 bot 的结构剖析。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**应用程序名称和图标**|
|2 |**"聊天" 选项卡**：打开与你的 bot 对话的空间 (仅适用于个人应用) 。|
|3 |**自定义选项卡**：打开与您的应用程序相关的其他内容。|
|4 |**"关于" 选项卡**：显示有关您的应用程序的基本信息。|
|5 |**聊天气泡**： Bot 对话使用团队消息传递框架。|
|6 |**自适应卡片**：如果你的 bot 的响应包含自适应卡片，卡片将占用完整的聊天气泡宽度。|
|7 |**命令菜单**：显示你)  (定义的你的 bot 的标准命令。

### <a name="command-menu"></a>命令菜单

命令菜单提供您希望机器人始终响应的单词或短语的列表。 当有人正在使用 bot 时，"命令" 菜单将显示在 "撰写" 框的上方。 当选中某个命令时，它会插入到邮件中。

命令列表应简短。 此菜单仅用于突出显示你的 bot 的主要功能。 也将命令保持简洁。 例如，创建一个名为 " **帮助** " 的命令，而不 **能帮助我** 吗？
无论会话的状态如何，命令菜单都必须始终可用。

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="示例显示 bot 的命令菜单。" border="false":::

## <a name="understand-what-people-are-saying"></a>了解人们的评价

使用同义词库并从尽可能多的不同背景中获取人员，以帮助您生成标准查询的不同解释。

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="显示机器人可能如何解释 &quot;Hello&quot; 的插图。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="图示：机器人如何解释 &quot;帮助&quot;。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="显示机器人可能解释 &quot;感谢&quot; 的说明。" border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a>从邮件中提取意图和数据

将你的 bot 设计为识别意图，这将从你的人员那里获取某人想要响应邮件或查询的内容。 意向将邮件或查询分类为单个操作，其中包含一个或多个受操作影响的数据对象。 

下面的示例概述了发送到 bot 的邮件中的用户意图和数据。

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="示例中所示的 &quot;将航班预订给西雅图&quot; 这一句，用户意图是 &quot;书籍 a 航班&quot;，数据是 &quot;西雅图&quot;。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="示例显示在句子 &quot;何时打开存储&quot;，用户意图是 &quot;when&quot;，且数据为 &quot;开放&quot;。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="示例中显示了句子 &quot;安排会议时，在通讯组中使用王俊元&quot;、用户意向为 &quot;安排会议&quot; 和 &quot;分发中的 Bob&quot; 等数据。" border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a>分析和改进

了解用户在与你的 bot 聊天时应说出的内容。 随着用户群在不同位置和 emc 的增长，这将是一个持续的反复发生的过程。 您可以使用 (Microsoft LUIS) 调整您的 bot 的语言识别和意图映射。

* [了解 LUIS](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence)：了解 LUIS 如何使用 AI 提供对应用数据的自然语言理解 (NLU) 。
* [与 LUIS 集成](https://www.luis.ai/)：将自然语言功能添加到你的机器人中，而不是创建机器学习模型的复杂过程。

## <a name="use-cases"></a>用例

### <a name="simple-queries"></a>简单查询

Bot 可以提供与查询或一组相关匹配项完全匹配的项，以帮助消除歧义。 对于相关的匹配项，请使用列表卡片对内容进行分组。

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="示例显示与 bot 的简单查询交互。" border="false":::

### <a name="multi-turn-interactions"></a>多转换交互

虽然你的 bot 可以支持完整的请求和问题，但它还应能够处理多项交互。 预测可能的后续步骤使用户可以更轻松地执行完整的任务流 (而不是期望他们手工创建一个全面的请求) 。

在下面的示例中，bot 将使用有关下一步操作的选项来响应每个邮件。

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="示例显示与 bot 之间的多路交互交互。" border="false":::

### <a name="reach-out-to-users"></a>与用户联系

通过主动消息传递，你的 bot 可以像摘要那样操作，以特定频率发送与个人、组聊天或频道相关的通知。 当文档中的内容发生了更改或工作项关闭时，bot 可能会发送一封邮件。

在以下示例中，用户将收到 toast 通知，即 bot 在另一个频道中将其推广。

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="示例展示了自动将用户从另一个频道传递给用户的 toast。" border="false":::

现在，该频道中的用户可以从 bot 读取其邮件。

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="示例显示了用户查看 bot 的主动消息。" border="false":::

### <a name="use-tabs-with-bots"></a>使用带 bot 的选项卡

选项卡可使你的 bot 更易于使用。 例如，如果你的 bot 可以创建工作项，则在选项卡中的一个中心位置显示所有这些项会非常好。有关 [设计选项卡](../../tabs/design/tabs.md)的详细信息，请参阅。

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="示例显示选项卡如何帮助组织 bot 内容。" border="false":::

## <a name="manage-a-bot"></a>管理 bot

用户应该能够更改机器人的设置。 您可以使用 bot 命令提供此功能，但在 [任务模块](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) 中包含所有设置通常效率更高 (如以下示例中所示) 。

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="示例显示了用于配置 bot 设置的任务模块。" border="false":::

## <a name="best-practices"></a>最佳做法

### <a name="content"></a>内容

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="do-establish-a-clear-persona"></a>操作：建立明确角色

你的 bot 的语气是否友好和轻型、"只是真实" 还是超级 quirky？ 它应如何在不同的方案中做出响应？ 规划和记录你的 bot 角色可以更轻松地编写看似自然和内聚的响应。

有关在<a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft 团队 UI 工具包 (Figma) </a>中写入 bot 的详细信息，请参阅。

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a>操作：清楚地传达机器人可以执行的操作

欢迎消息和教程帮助用户了解使用你的 bot 可以执行的操作。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="dont-obscure-your-bots-features"></a>不：遮盖你的 bot 的功能

第一事是印象。 在使用 nondescript 登录邮件时，用户可能会感到困惑或有疑问。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="do-recognize-non-questions"></a>操作：识别非问题

你的 bot 应能够响应类似于 "Hi"、"帮助" 和 "感谢" 的邮件，同时还可以对常见的拼写错误和俗语进行评估。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a>请勿：错过对欣喜的机会

有些人希望对话以流的方式自然，就像真正的人一样。 尽量避免对简单邮件的 clumsy 响应。

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a>疑难解答

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="do-provide-help"></a>Do：提供帮助

如果你的 bot 无法满足请求，请为用户提供用于教育自己与你的 bot 进行交互的方法。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="dont-leave-users-stranded"></a>请勿：让用户处于进退两难

如果用户无法解决问题，他们将很快放弃你的机器人。

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a>复杂的交互

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="do-use-task-modules-or-tabs"></a>操作：使用任务模块或选项卡

如果你的 bot 提供了需要更多步骤的答案，则可以链接到任务模块或选项卡以完成任务或流。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a>请勿：使多项交互变单调乏味

完成单个任务的一个广泛的对话速度缓慢且过于复杂。 它还要求开发人员考虑状态更改 (例如，会话超时或发送 "取消" 邮件) 。

   :::column-end:::
:::row-end:::

### <a name="privacy"></a>隐私

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a>操作：仅在个人上下文中显示敏感信息

如果你的 bot 位于组聊天或频道中，我们建议将用户定向到专用位置 (如任务模块、选项卡或浏览器) 查看敏感信息。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a>请勿：某些内容并非每个人都能看到

你的 bot 不应将敏感信息泄露给一组用户。

   :::column-end:::
:::row-end:::

## <a name="learn-more"></a>了解更多

这些其他指南可帮助你使用你的 bot 设计：

* [正在设计你的个人应用](../../concepts/design/personal-apps.md)
* [设计自适应卡片](../../task-modules-and-cards/cards/design-effective-cards.md)
* [正在设计任务模块](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)

## <a name="validate-your-design"></a>验证设计

如果计划将应用程序发布到 AppSource，则应了解通常会在提交期间导致应用程序失败的设计问题。

> [!div class="nextstepaction"]
> [检查设计验证准则](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
