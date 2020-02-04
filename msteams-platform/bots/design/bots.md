---
title: Bot 设计指南
description: 介绍创建 bot 的指南
keywords: 团队设计指南参考框架 bot 对话
ms.openlocfilehash: f59a1e9c280f27567692b4d10341db79d05c3464
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673411"
---
# <a name="start-talking-with-bots"></a>开始与 bot 对话

Bot 是执行一组较窄或特定任务的会话式应用程序。 它们为您提供了与用户进行通信的机会，回答了他们的问题，并主动通知他们发生了哪些更改。 这是一种很好的方法。

---

## <a name="guidelines"></a>准则

### <a name="avatars"></a>虚拟形象

在团队中，Bot 虚拟形象的形状类似于六边形，因此人们可以快速判断他们正在与某个 bot 而不是某人交谈。 你将头像作为方块提交，我们将为你进行裁剪。 当遇到虚拟形象时，我们建议您让您能够在2英尺和使用较高的对比度的情况下清晰地消失。

[!include[Avatar image](~/includes/design/bot-avatar-image.html)]

### <a name="buttons"></a>按钮

我们每张卡片最长支持六个按钮。 编写按钮文本时请务必简明扼要，并且请注意，大多数按钮应仅处理手头的任务。

### <a name="graphics"></a>图形

图形是一种很不错的说明，但并不是所有机器人对话都需要图形，因此使用它们来获得最大影响。

### <a name="responding-to-users-and-failing-gracefully"></a>响应用户并顺利进行故障转移

你的 bot 还应能够在考虑常见的拼写错误和俗语时，对诸如 "Hi"、"帮助" 和 "谢谢" 这样的事情做出响应。 例如：

#### <a name="x2713-hello"></a>&#x2713; Hello

`Hi` `how are you` `howdy`

#### <a name="x2713-help"></a>&#x2713; 帮助

`What do you do?` `How does this work?` `What the heck?`

#### <a name="x2713-thanks"></a>&#x2713; 感谢

`Thank you` `thankyou` `thx`

你的 bot 应能够处理以下类型的查询和输入：

* **识别的问题**：这些是用户预计会遇到的 "最佳方案" 问题。
* **可识别的无问题**：查询不受支持的功能、随机的信息，或当有人想在你的 bot 咒骂时。
* **无法识别的问题：无法**识别的输入（例如，杂乱）。

Bot 的个性和响应类型的示例：

[!include[Bot responses](~/includes/design/bot-responses-table.html)]

> [!TIP]
> 编写机器人脚本时，请询问自己： "我的公司是否为 embarrassed 如果响应是通过屏幕捕获并共享吗？"

### <a name="understanding-what-users-are-trying-to-say"></a>了解用户试图说出的内容

#### <a name="use-a-thesaurus-for-synonyms"></a>对同义词使用同义词库

当灵感触发变体时，请使用同义词库并从尽可能多的不同背景中获取人员，以帮助您生成每个查询的不同解释。

#### <a name="make-use-of-telemetry-and-interviews"></a>使用遥测和访谈

了解用户在查询你的 bot 时所说的含义以及它们的意图。 当你在不同位置和公司类型中获取用户时，这将是一个持续的过程。 您可以使用语言理解智能服务（[LUIS](/azure/cognitive-services/luis/what-is-luis)）微调语言识别和意图映射。

### <a name="how-often-should-you-use-your-bot-to-reach-out-to-a-user"></a>应多长时间使用你的 bot 与用户联系？

#### <a name="x2713-when-a-state-has-changed"></a>状态更改时 &#x2713;

例如，如果工作分配标记为 "已完成"、"bug 更改时"、"新社交媒体可用" 或 "已完成轮询"。

#### <a name="x2713-when-the-timing-is-right"></a>当计时正确时 &#x2713;

你的 bot 可以像每日摘要那样操作，以特定频率向用户或频道发送通知。

将用户保持在控制之下。 提供包括频率和优先级的通知设置。

[!include[Bot notification](~/includes/design/bot-notification-image.html)]

---

## <a name="using-tabs"></a>使用选项卡

选项卡使你的 bot 功能更强大。 通过选项卡，您可以创建以下内容：

### <a name="x2713-a-place-to-host-standing-queries"></a>&#x2713; 承载驻留查询的位置

在 bot 和单个用户之间的个人对话中，选项卡可以容纳用户特定的信息和列表。 它们也是维护对常见问题（Faq）的 bot 响应的理想位置，因此用户无需继续提问。

### <a name="x2713-a-place-to-finish-a-conversation"></a>&#x2713; 完成对话的位置

您可以从卡片链接到选项卡。 如果你的 bot 提供了需要更多步骤的答案，则它可以链接到选项卡以完成任务或流。

### <a name="x2713-a-place-to-provide-some-help"></a>&#x2713; 提供一些帮助的位置

添加一个选项卡，educates 用户如何与你的 bot 进行通信。 您可以为其所做的操作或 Faq 提供一些上下文。

![提供帮助](~/assets/images/framework/framework_bots_tbot-help.png)

> [!TIP]
> 在选项卡中嵌入网站的各个部分可帮助某人在使用您的服务时维护对话的上下文。 它消除了在浏览器中启动服务的需求，并在应用程序之间来回切换。

---

## <a name="best-practices"></a>最佳做法

### <a name="x2713-bots-arent-assistants"></a>&#x2713; Bot 不助手

与代理不同，例如 Cortana、bot 充当专家。

### <a name="x2713-discourage-chitchat"></a>&#x2713; 阻止 chitchat

除非为对话构建了你的 bot，否则会发现将 chitchat 重定向到任务完成的方法。

### <a name="x2713-introduce-some-personality"></a>&#x2713; 引入了一些个性

保持你的 bot 个人与你的产品的语音一致。 将你的 bot 想象为你的公司说话。

### <a name="x2713-maintain-tone"></a>&#x2713; 保持音调

确定您是否希望您的语气是友好和浅、"只是真实" 还是超级 quirky。

### <a name="x2713-encourage-easy-task-flow"></a>&#x2713; 鼓励轻松的任务流

支持多项交互，同时仍允许完整构建的问题。 预测下一步将帮助用户更轻松地完成任务流。

如果用户需要几个步骤来完成某项任务，则允许你的 bot 在每个步骤中执行这些步骤，但通过让其建议更快速的途径来完成。 例如，如果用户已进行了多个会话设置，则会设置一个会议（通过先指定一个会议，然后确定要通知的时间，然后指出一天），使用以下建议完成对话：下一次，请尝试询问您是否可以 "安排在明天1:00 的 Bob 开会"。