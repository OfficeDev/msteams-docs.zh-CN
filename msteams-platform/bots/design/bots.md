---
title: Bot 设计指南
description: 介绍创建 bot 的指南
keywords: 团队设计指南参考框架 bot 对话
ms.openlocfilehash: 0691c483d12e537772b74abc015d71e1704f88c8
ms.sourcegitcommit: fdb53284a20285f7e8a7daf25e85cb5d06c52b95
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2020
ms.locfileid: "48992636"
---
# <a name="start-talking-with-bots"></a>开始与 bot 对话

Bot 是执行一组较窄或特定任务的会话式应用程序。 它们为您提供了与用户进行通信的机会，回答了他们的问题，并主动通知他们发生了哪些更改。 这是一种很好的方法。

---

## <a name="guidelines"></a>准则

### <a name="bot-design-guidelines"></a>Bot 设计指南

* 当有活动时，bot 应提供相关通知。
* 自动程序不能向不应查看该数据的访问群体向团队、组聊天或1:1 对话中推送敏感数据。
* Bot 通知应包含有意义的数据，以向用户通知通知的相关性。
* Bot 的语气应按指南中定义的方式反映团队语音。
* Bot 应提供首次运行体验欢迎消息，以突出显示 bot 的价值以及它的主要功能，这可能是 "获取教程"、带有轮播卡片的交互式教程或 "试用" 按钮的形式。
* Bot 文本不能包含任何拼写错误或语法错误。
* Bot 必须提供一组可操作的预定义的 bot 命令。
* Bot 邮件应易于理解和操作。
* 当不理解邮件时，bot 必须提供后备帮助命令。
* 由自动程序发送的卡片中嵌入的窗体应提供不需要顺序更新的确定性输入。
* 应将 Bot 通知的范围限定为团队、组聊天或1:1 对话，其中包含访问群体的相关内容。

### <a name="avatars"></a>虚拟形象

在团队中，Bot 虚拟形象的形状类似于六边形，因此人们可以快速判断他们正在与某个 bot 而不是某人交谈。 你将头像作为方块提交，我们将为你进行裁剪。 当遇到虚拟形象时，我们建议您让您能够在2英尺和使用较高的对比度的情况下清晰地消失。

[!include[Avatar image](~/includes/design/bot-avatar-image.html)]

### <a name="buttons"></a>按钮

我们每张卡片最长支持六个按钮。 编写按钮文本时请务必简明扼要，并且请注意，大多数按钮应仅处理手头的任务。

### <a name="graphics"></a>图形

图形是一种很不错的说明，但并不是所有机器人对话都需要图形，因此使用它们来获得最大影响。

### <a name="onboarding-users"></a>载入用户

关键是，bot 会自我介绍并传达他们可以为用户执行的操作。 此 *值 exchange* 可帮助用户了解如何使用 bot，这些限制可能位于何处，并且最重要的是，帮助用户容许与不像真实人员那样直观的计算机进行交互。 此外，它还向 exchange 中的用户数据授予对该服务提供的真正价值的权限。

#### <a name="welcome-messages"></a>欢迎邮件

欢迎邮件是设置你的 bot 语气并应在个人和团队或组方案中使用的最佳方式。 该消息指出了 bot 的功能以及与之进行交互的一些常见方法。 使用类似 " *请尝试询问*..." 的特定功能示例 在项目符号列表中。 只要有可能，这些建议应返回存储的响应。 此功能示例非常关键，无需用户登录即可正常工作。
有关其他指导，请 *参阅*[欢迎消息要求](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-personal-bots-must-always-send-a-welcome-message-on-first-launch)。

#### <a name="tours"></a>漫游

包括使用欢迎邮件的 *教程* 属性和对与 " *帮助* " 等效的用户输入的响应。 这是让用户了解机器人可以执行的操作的最有效方法。 在一对一体验中，Carousels 是一种很好的方法，可告知这一情景，包括 " *Try it* " 按钮。鼓励可能的响应示例。 漫游也是谈论应用程序的其他功能的很好的地方。 例如，可以包括邮件扩展和工作组选项卡的屏幕截图。  用户无需登录即可访问和使用教程。

在团队或组方案中使用演示时，他们应在任务模块中打开，以便不向用户之间的正在进行的会话添加更多的卡噪音。

### <a name="responding-to-users-and-failing-gracefully"></a>响应用户并顺利进行故障转移

你的 bot 还应能够在考虑常见的拼写错误和俗语时，对诸如 " *Hi* "、" *帮助* " 和 " *感谢* " 这样的内容做出响应。 例如：

#### <a name="x2713-hello"></a>&#x2713; Hello

`"Hi"`  `"How are you"`  `"Howdy"`

#### <a name="x2713-help"></a>&#x2713; 帮助

`"What do you do?"`  `"How does this work?"`  `"What the heck?"`

#### <a name="x2713-thanks"></a>&#x2713; 感谢

`"Thank you"`  `"Thankyou"`  `"Thx"`

你的 bot 应能够处理以下类型的查询和输入：

> [!div class="checklist"]
>
> * **识别的问题** 。 这些是用户预期的 "最佳方案情况" 问题。
> * **识别的无问题** 。 有关不受支持的功能和/或随机、无关或 profane 条目的查询。
> * **无法识别的问题** ：输入或无法识别、无意义或无意义的项。

Bot 的个性和响应类型的示例：

[!include[Bot responses](~/includes/design/bot-responses-table.html)]

> [!TIP]
> 编写机器人脚本时，请询问自己： "我的公司是否为 embarrassed 如果响应是通过屏幕捕获并共享吗？"

### <a name="understanding-what-users-are-trying-to-say"></a>了解用户试图说出的内容

#### <a name="use-a-thesaurus-for-synonyms"></a>对同义词使用同义词库

当灵感触发变体时，请使用同义词库并从尽可能多的不同背景中获取人员，以帮助您生成每个查询的不同解释。

#### <a name="make-use-of-telemetry-and-interviews"></a>使用遥测和访谈

了解用户在查询你的 bot 时所说的含义以及它们的意图。 当你在不同位置和公司类型中获取用户时，这将是一个持续的过程。 您可以使用语言理解智能服务 ([LUIS](/azure/cognitive-services/luis/what-is-luis)) 来微调语言识别和意图映射。

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

在 bot 和单个用户之间的个人对话中，选项卡可以包含用户特定的信息和列表。 它们也是维护对常见问题 (Faq) 的 bot 响应的好地方，因此用户无需继续提问。

### <a name="x2713-a-place-to-finish-a-conversation"></a>&#x2713; 完成对话的位置

您可以从卡片链接到选项卡。 如果你的 bot 提供了需要更多步骤的答案，则它可以链接到选项卡以完成任务或流。 例如，为了响应，"如何设置 iPhone 的格式？" 好的响应可能是一个卡片，它概括了前几个步骤，并具有一个 *显示更多* 步骤的按钮，然后将用户带到 bot 的 " *帮助* " 选项卡和指向特定说明的深层链接。

### <a name="x2713-a-place-to-host-a-settings-page"></a>&#x2713; 承载设置页面的位置

Bot 应具有一些用户控件。 对于很多机器人，通过聊天界面允许它;但是，很难记住这些设置。 "设置" 选项卡可以显示 "用户" 设置，允许用户一次更改所有设置，也可能是更复杂的 bot 自定义行为的一个良好的位置。

### <a name="x2713-a-place-to-provide-some-help"></a>&#x2713; 提供一些帮助的位置

添加一个选项卡，educates 用户如何与你的 bot 进行通信。 您可以为其所做的操作或 Faq 提供一些上下文。

![提供帮助](~/assets/images/framework/framework_bots_tbot-help.png)

> [!TIP]
> 在选项卡中嵌入网站的各个部分将有助于用户在使用您的服务时维护对话的上下文。 它消除了在浏览器中启动服务的需求，并在应用程序之间来回切换。

---

## <a name="bots-in-channels"></a>通道中的 bot

可以通过对频道中的 bot 进行调用来实现 `@mention` 。 机器人对话框在通道和组中应是唯一的，而不是一对一方案，通常最好是考虑不同的方法。 在下列情况下，尤其如此：

### <a name="sensitive-data-sent-by-a-bot"></a>Bot 发送的敏感数据

虽然团队中的用户可以在服务中知道，但实际用户角色却不能。 这意味着，在涉及威胁的教育场景中，不会在团队设置中共享父联系人信息和学生联系人信息。 而 bot 的邮件可能是： "今天发生两个威胁事件" 和一个显示详细信息的按钮。

在网页中启动详细信息，或任务模块可以提示用户凭据或查询与 AAD 帐户配对的用户角色的索引。 在这两个选项中，数据都在一个专用视图作用域中，并且不会有数据泄露。 如果在用户与 bot 之间的一对一聊天中发送相同的数据，则该数据仅对该上下文中的用户可见，因此，在 bot 邮件中完全显示该数据是安全的。 应避免将用户从频道中提取到一对一聊天，因为这会导致强制导航高度中断。

### <a name="sending-cards-as-a-response-to-interactions"></a>作为交互的响应发送卡片

发送轮播卡片以在一对一聊天中 *进行漫游* 是完全可接受的，相同的模式可能会在活动频道中向大量用户发送数十或数百个 *漫游 carousels* 。 为避免这种情况，辅助卡应托管在任务模块中。 此模式使用户在使用频道的上下文中保持用户的正常，并使频道清除过多的 bot 响应，并且可以选择在显示 *漫游* 时考虑不同的用户角色。

## <a name="useful-tips"></a>有用的提示

### <a name="x2713-remember-bots-arent-assistants"></a>&#x2713; 记住，bot 不助手

与代理不同，例如 Cortana、bot 充当专家。

### <a name="x2713-discourage-chitchat"></a>&#x2713; 阻止 chitchat

除非为对话构建了你的 bot，否则会发现将 chitchat 重定向到任务完成的方法。

### <a name="x2713-introduce-some-personality"></a>&#x2713; 引入了一些个性

保持你的 bot 个人与你的产品的语音一致。 将你的 bot 想象为你的公司说话。

### <a name="x2713-maintain-tone"></a>&#x2713; 保持音调

确定您是否希望您的语气是友好和浅、"只是真实" 还是超级 quirky。

### <a name="x2713-encourage-easy-task-flow"></a>&#x2713; 鼓励轻松的任务流

支持多项交互，同时仍允许完整构建的问题。 预测下一步将帮助用户更轻松地完成任务流。

如果用户需要几个步骤来完成某项任务，则允许你的 bot 在每个步骤中执行这些步骤，但通过让其建议更快速的途径来完成。 例如，如果用户已进行了多个会话，则先指定一个会议，然后确定该时间，然后再指出一天) 来设置会议 (，并在下面的建议下完成此对话：下一次，请尝试询问您是否可以 "在明天1:00 的时间安排与小明的会议"。
