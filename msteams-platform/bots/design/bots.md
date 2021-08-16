---
title: 设计机器人
description: 了解如何设计 Teams 自动程序并获取 Microsoft Teams UI Kit。
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: ea0392868b06653657beff60b157070eaef7f4ba
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345646"
---
# <a name="designing-your-microsoft-teams-bot"></a>设计 Microsoft Teams 自动程序

自动程序是执行一组特定任务的对话应用。 根据 Microsoft <a href="https://dev.botframework.com/" target="_blank">框架</a>，自动程序会与用户进行通信、回复其问题，并主动通知他们更改和其他事件。 这是一个很好的方法。

> [!IMPORTANT]
> 目前，自动程序政府社区云 (GCC) DOD GCC-High和国防部 (中) 。

为指导应用设计，以下信息描述并说明用户可以如何在 Teams 中添加、使用和管理机器人。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

可在 Microsoft Teams UI Kit 中查看更全面的机器人设计指南，包括可根据需要获取和修改的元素。

> [!div class="nextstepaction"]
> [获取 Microsoft Teams UI Kit （用户）](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a>添加机器人

自动程序可用于聊天、频道和个人应用。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

用户可以添加自动程序，方法如下：

* 从 Teams 应用商店。
* 通过使用应用飞出，选择 teams **"更多应用"** 图标。
* 当有@mention聊天或撰写框时（以下示例显示了如何在群组聊天中执行这一操作）。

    :::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="示例演示了如何使用智能机器人在群组聊天中添加@mention。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

用户可以访问使用自动程序在桌面上添加的@mention。

:::image type="content" source="../../assets/images/bots/mobile-access-bot-chat-at-mention.png" alt-text="示例演示如何使用移动设备访问群聊中的@mention。" border="false":::

---

## <a name="introduce-a-bot"></a>介绍机器人

自动程序要自行介绍并描述其功能，这一点至关重要。 此初始交换可帮助用户了解与智能机器人有关的方式，了解其限制，最重要的是，熟悉与智能机器人的交互。

### <a name="welcome-message-in-a-one-on-one-chat"></a>一对一聊天中的欢迎消息

在个人环境中，欢迎消息可设置机器人的风格。 消息包括问候语、机器人可以做什么，以及一些如何交互的建议。 例如，"尝试询问我..."。 如果可能，建议应返回存储的响应，无需登录。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="例如，显示了个人应用中的机器人简介。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-personal-welcome.png" alt-text="示例显示了移动版个人应用中的机器人简介。" border="false":::

---

### <a name="welcome-message-in-channels-and-group-chats"></a>频道和群聊中的欢迎消息

与个人空间（如个人应用聊天）相比，机器人在频道和群组聊天中的 () 略有不同。 在现实中，如果进入一个人员完整的房间;你可自我介绍，而不是每个已存在的人。 将这一思路融入你的机器人设计中。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="在协作上下文中显示自动介绍的示例。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-group-welcome.png" alt-text="示例演示了在移动版协作上下文中的机器人简介。" border="false":::

---

### <a name="bot-authentication-with-single-sign-on"></a>使用单一登录的自动身份验证

当用户向机器人发送消息时，可能需要登录才能使用其所有功能。 可以使用单一登录 （SSO） 简化身份验证过程。

请不要忘记：在自动程序命令菜单（**我该怎么办？**）中，还必须提供一个命令以注销。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="示例显示具有登录按钮的自动程序。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-sso-example.png" alt-text="示例显示移动版上具有登录按钮的自动程序。" border="false":::

---

### <a name="tours"></a>导览

可在包含欢迎消息的教程以及自动程序响应类似"帮助"命令时包括教程。 教程是介绍机器人功能最有效的方法。 如果适用，它们还非常适用于描述应用的其他功能。 例如，包括邮件扩展的屏幕截图。

> [!IMPORTANT]
> 无需登录即可访问教程。

#### <a name="one-on-one-chats"></a>一对一聊天

在个人应用中，变盘可提供自动程序的有效概述以及应用的其他任意功能。 建议包括允许用户试用自动程序命令的按钮。 例如， **创建任务**。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="一对一聊天中的自动浏览示例。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-tour-personal.png" alt-text="示例演示了机器人在移动版一对一聊天中的教程。" border="false":::

---

#### <a name="channels-and-group-chats"></a>频道和群组聊天

在频道和群组聊天中，应在模式（也称为 [任务模块](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) 中打开浏览，这样不会中断持续对话。 还可选择为教程实施基于角色的视图。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="示例显示频道中的自动浏览。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-tour-channel.png" alt-text="示例演示移动频道中的自动程序教程。" border="false":::

---

## <a name="chat-with-a-bot"></a>与聊天机器人聊天

自动程序可直接集成到团队的消息框架。 用户可以与智能机器人聊天，以获得其问题的解答或键入命令，让智能机器人执行一组窄或特定的任务。 自动程序可主动通过聊天通知用户应用更改或更新。

### <a name="chat-with-a-bot-in-different-contexts"></a>在不同上下文中与机器人聊天

可在下列上下文中使用自动程序：

* **个人应用**：在个人应用中，机器人具有专用的聊天选项卡。
* **一对一聊天**：用户可以启动与机器人的私密对话。 体验与在个人应用中使用机器人相同。
* **群组聊天**：通过智能机器人，用户可以在群组聊天中@mentioning机器人。
* **频道**：用户可以与频道中的机器人交互。 选择@mentioning组合框中的机器人姓名。 请记住，在此上下文中，自动程序可供整个团队使用，而不只是频道。

### <a name="anatomy"></a>解剖

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="示例显示了机器人的结构分析。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**应用名称和图标**|
|2|**"聊天** 选项卡"中：打开与机器人对话的空白（仅适用于个人应用）。|
|3 |**自定义选项卡**：打开与应用相关的其他内容。|
|4 |**关于选项卡**：显示有关应用的基本信息。|
|5 |**聊天气泡**：自动对话使用 Teams 消息框架。|
|6 |**自适应卡片**：如果你的机器人响应包含自适应卡片，该卡片将占用聊天气泡的全部宽度。|
|7 |**命令菜单**：显示自动程序的标准命令（由你定义）。|

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-anatomy.png" alt-text="示例演示移动机器人的结构结构分析。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**应用名称和图标**|
|2|**"聊天** 选项卡"中：打开与机器人对话的空白（仅适用于个人应用）。|
|3 |**自定义选项卡**：打开与应用相关的其他内容。|
|4 |**聊天气泡**：自动对话使用 Teams 消息框架。|
|5 |**自适应卡片**：如果你的机器人响应包含自适应卡片，该卡片将占用聊天气泡的全部宽度。|

---

### <a name="command-menu"></a>命令菜单

命令菜单提供希望自动程序始终响应的字词或短语的列表。 当某人与机器人进行聊天时，命令菜单显示在组合框上方。 当选择命令时，它将插入到邮件中。

命令列表应简短。 此菜单旨在突出显示机器人的主要功能。 命令保持简明性。 例如，创建名为"帮助 **命令** 而不是 **"命令，请帮我**？
无论对话状态如何，命令菜单必须始终可用。

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="示例显示自动程序的命令菜单。" border="false":::

## <a name="understand-what-people-are-saying"></a>了解人们所说的

使用同义词库，尽可能从不同的背景请人员，帮助你生成不同的标准查询理解。

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="显示自动程序如何解读&quot;Hello&quot;的示意图。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="显示自动程序如何解读&quot;帮助&quot;的示意图。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="显示自动程序如何解读&quot;谢谢&quot;的插图。" border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a>从邮件中提取意图和数据

设计智能机器人以识别意图，该意图可捕获智能机器人在响应邮件或查询时所捕获的信息。 意图将邮件或查询分为单个操作，包括受该操作影响的一个或多个数据对象。 

以下示例概述了发送到自动程序的消息中的用户意图和数据：

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="显示在句子&quot;预订到西雅图的航班&quot;中的示例，用户意图是&quot;预定航班&quot;，数据为&quot;西雅图&quot;。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="显示在句子&quot;存储何时打开&quot;中的示例，用户意图是&quot;何时打开&quot;且数据为&quot;打开&quot;。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="示例显示在句子&quot;下午 1 点与 Bob 在分发中安排会议&quot;中，用户意图是&quot;安排会议&quot;，数据为&quot;下午 1 点&quot;和&quot;Bob 正在分发&quot;。" border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a>分析和改进

了解用户与机器人聊天时所说的内容。 随着你的用户群在不同位置和组织之间增长，这一过程将持续迭代。 可以使用 Microsoft 语言理解 （TUNE） 优化自动程序的语言识别和意图映射。

* [了解组织](/azure/cognitive-services/luis/artificial-intelligence)：了解用户如何使用 AI 为应用数据提供自然语言理解 （NLU）。
* [与 COMPLEX](https://www.luis.ai/)集成：向机器人添加自然语言功能，而无需创建机器学习模型这个复杂流程。

## <a name="use-cases"></a>用例

### <a name="simple-queries"></a>简单查询

自动程序可提供查询或一组相关匹配项的精确匹配，有助于进行语言不匹配。 相关匹配项，使用列表卡对内容进行分组。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="示例显示与自动程序的简单查询交互。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-simple-query.png" alt-text="示例显示与移动机器人的简单查询交互。" border="false":::

---

### <a name="multi-turn-interactions"></a>多位交互

虽然自动程序可支持完整的请求和问题，但也应能够处理多位交互。 如果想了解可能的下一步操作，用户就更轻松完成整个任务流（而不是期望他们精心制作一个全面的请求）。

在下面的示例中，自动程序使用可能想要执行下一步操作的选项来响应每条消息。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="示例显示与自动程序之间的多元交互。" border="false":::


# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-multi-turn.png" alt-text="示例显示与移动设备上的机器人的多向交互。" border="false":::


---

### <a name="reach-out-to-users"></a>联系用户

通过主动消息传递，机器人可以充当摘要，以特定频率发送与个人、群组聊天或频道相关的通知。 文档更改了某些内容或关闭工作项目时，自动程序可能会发送邮件。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

在下面的示例中，用户收到一条 Toast 通知，提示机器人在另一个频道中向用户发送消息。

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="示例显示了自动程序主动向另一个频道中的用户消息传递消息的祝念。" border="false":::

现在，用户可以从自动程序阅读其邮件。

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="示例显示用户查看自动程序主动的消息。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

在下面的示例中，用户收到一条通知，提示机器人在另一个频道中向用户发送消息。

:::image type="content" source="../../assets/images/bots/mobile-bot-proactive-message-toast.png" alt-text="示例显示自动程序从移动版上另一个频道主动传送用户的 Toast。" border="false":::

现在，用户可以从自动程序阅读其邮件。

:::image type="content" source="../../assets/images/bots/mobile-bot-proactive-message.png" alt-text="示例显示用户正在移动设备上查看机器人的主动消息。" border="false":::

---

### <a name="use-tabs-with-bots"></a>将标签用于机器人

在个人应用中，选项卡可以补充机器人可以执行哪些操作。 例如，如果你的机器人可以创建工作项目，就太棒了在选项卡内的一个中心位置显示所有这些项。详细了解如何 [选项卡](../../tabs/design/tabs.md)。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="示例显示选项卡可如何帮助整理自动程序内容。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/bots/mobile-bot-with-tab.png" alt-text="示例显示选项卡如何有助于在移动设备上组织聊天机器人内容。" border="false":::

---

## <a name="manage-a-bot"></a>管理自动程序

用户应能够更改自动程序的设置。 可通过自动程序命令提供此功能，但将 [任务模块](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) （如下例所示）中所有设置通常更高效。

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="示例显示一个任务模块，用于配置机器人的设置。" border="false":::

## <a name="best-practices"></a>最佳实践

使用上述建议打造优质应用体验。

### <a name="content"></a>内容

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="显示建立清晰人物的自动程序最佳做法的示例。" border="false":::

#### <a name="do-establish-a-clear-persona"></a>执行：建立一个清晰的人

你的机器人的口风格是否友好且浅，"仅事实"或超可人？ 如何在不同的情况下进行响应？ 通过规划和记录机器人用户的内容，可以更轻松地编写自然且有凝聚力的答复。

在 Microsoft Teams UI Kit （Kitma） 中 <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">机器人编写功能。</a>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="显示以清楚地传达机器人可以执行哪些功能的示例。" border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a>工作：清楚传达你的机器人可以做什么

欢迎消息和导览可帮助用户了解他们可以使用智能机器人执行什么操作。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="显示不遮盖机器人功能的示例。" border="false":::

#### <a name="dont-obscure-your-bots-features"></a>不要：遮住了机器人的功能

第一印象很重要。 当显示非描述登录邮件时，用户可能会困惑或可疑。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="显示自动程序应识别非问题的示例。" border="false":::

#### <a name="do-recognize-non-questions"></a>注意：识别非问题

你的自动程序应能够回复"你好"、"帮助"和"谢谢"等消息，同时还调查常见的拼写错误和拼错的信息。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="显示应避免对简单自动程序消息的不一致响应的示例。" border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a>不要：错过一些可喜欢的机会

一些人希望对话可以像与真实人员一样自然流式交流。 尽量避免对简单邮件的字体显示错误。

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a>疑难解答

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="显示自动程序的示例应帮助用户了解如何使用机器人。" border="false":::

#### <a name="do-provide-help"></a>执行：提供帮助

如果机器人不满足请求，提供用户指导用户与机器人交互的方法。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="显示自动程序不应将用户设置成这样一个示例。" border="false":::

#### <a name="dont-leave-users-stranded"></a>请勿参与：将用户困

用户如果无法解决问题，会迅速离开机器人。

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a>复杂交互

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="显示你可以将任务模块或选项卡与自动程序一起用于复杂交互的示例。" border="false":::

#### <a name="do-use-task-modules-or-tabs"></a>Do：使用任务模块或选项卡

如果您的自动程序提供了需要执行更多步骤的答案，您可以链接到任务模块或选项卡以完成任务或流程。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="显示自动程序应避免多向交互的示例。" border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a>不要：进行多元交互，件非常乏味

完成单个任务的丰富对话速度缓慢且过于复杂。 这还需要开发人员考虑状态更改（例如对话超时或发送"取消"消息）。

   :::column-end:::
:::row-end:::

### <a name="privacy"></a>隐私

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="显示自动程序应如何在个人上下文中显示私人信息的示例。" border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a>Do：仅在个人上下文中显示敏感信息

如果自动程序位于群组聊天或频道中，建议将用户引导至专用位置（例如任务模块、选项卡或浏览器）以查看敏感信息。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="显示机器人不应向组或人员显示敏感信息的示例。" border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a>不要：某些内容并非由每个人看到

你的自动程序不得向一组人员泄露敏感信息。

   :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅

以下其他准则可帮助你进行机器人设计：

* [设计个人应用](../../concepts/design/personal-apps.md)
* [设计自适应卡片](../../task-modules-and-cards/cards/design-effective-cards.md)
* [设计任务模块](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
