---
title: 提示和频繁失败的情况
description: 描述提交和大多数失败策略的提示
author: laujan
ms.author: lajanuar
ms.topic: how to
ms.openlocfilehash: 75ac2a01f1ccd8e38977e1cd099544e7dd160733
ms.sourcegitcommit: 67c021fa20eb5ea70c059fcc35be1c19c6c97c95
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2020
ms.locfileid: "42279786"
---
# <a name="tips-for-a-successful-app-submission"></a>成功提交应用程序的提示

本文解决了提交的应用程序验证失败的常见原因。 尽管它并不是您的应用程序的所有潜在问题的详尽列表，但遵循本指南将增加您的应用程序提交第一次的可能性。 有关验证策略的详细列表，*请参阅*[商业市场认证策略](/legal/marketplace/certification-policies)。

>[!NOTE]
>**[1140 节](/legal/marketplace/certification-policies#1140-teams)** 是专门针对团队应用程序的 Microsoft 团队和**[子节 1140.4](https://docs.microsoft.com/legal/marketplace/certification-policies#11404-functionality)** 解决功能要求的。

## <a name="validation-guidelines"></a>验证准则

### <a name="9989-general-considerations"></a>&#9989; 常规注意事项

另*请参阅* [Section 100 —常规](/legal/marketplace/certification-policies#100-general)

* 确保使用的是版本1.4.1 或更高版本的[Microsoft 团队 SDK](https://www.npmjs.com/package/@microsoft/teams-js)。
* 在验证过程正在进行时，请勿对应用进行更改。 执行此操作将需要对应用进行完全重新验证。
* 您的应用程序不得停止响应、意外终止或包含编程错误。 如果遇到问题，您的应用程序应正常失败，并向用户提供有效的单向转发邮件。
* 您的应用程序不得在用户环境中自动下载、安装或启动任何可执行代码。 所有下载都应从用户处寻求显式权限。
* 与您的体验相关联的任何材料（如说明和支持文档）都必须是准确的。 在您的说明和材料中，使用正确的拼写、大小写、标点符号和语法。
* 提供帮助和支持信息。 强烈建议您的应用程序包括首次运行的用户体验的帮助/常见问题解答链接。 对于所有个人应用程序，我们建议将 "帮助" 页作为 "个人" 选项卡提供，以获得更好的用户体验。

### <a name="9989--provide-a-clear-and-simple-sign-insign-out-and-sign-up-experience"></a>&#9989; 提供清晰且简单的登录/注销和注册体验

另*请参阅* [Section 1100.5-客户控制](/legal/marketplace/certification-policies#11005-customer-control)

* 如果您的应用程序或外接程序依赖于外部帐户或服务，则登录/注销和注册体验必须在应用程序中的所有功能上都显而易见且可访问。
* 如果向用户提供了显式登录选项，则必须有对应的注销选项（即使该应用程序使用的是 SSO/[缄默身份验证](~/tabs/how-to/authentication/auth-silent-aad.md)）也是如此。
* 注销选项必须仅将用户从应用程序功能中注销，而不能从团队客户端注销。
* 注销选项至少必须使用与登录选项相同的功能对用户进行签名即可。 例如，如果登录选项同时包含邮件扩展和选项卡，则注销选项必须包括邮件扩展和选项卡。

* 确保始终有一种方法来撤消以下（或类似）行为：
  * 登录 => 注销。
  * 链接帐户/服务 => 取消链接帐户/服务。
  * 连接帐户/服务 => 断开帐户/服务的连接。
  * 授权帐户/服务 => deauthorize/拒绝帐户/服务。
  * 注册帐户/服务 => 取消注册/取消订阅帐户/服务。
* 如果您的应用程序需要帐户或服务，则必须为用户提供注册或创建注册请求的方法。 如果您的应用程序是企业应用程序，则可以授予异常。
* 登录/注销功能必须在移动客户端上工作。 确保使用的是[Microsoft 团队 SDK](https://www.npmjs.com/package/@microsoft/teams-js)版本1.4.1 或更高版本。

有关身份验证的其他信息，请参阅：

* [身份验证文档](/concepts/authentication/authentication.md)
* [节点中的 Bot 身份验证示例](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
* [节点中的 Tab 身份验证示例](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [C #/.NET 中的选项卡/机器人身份验证](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

### <a name="9989-response-times-must-be-reasonable"></a>&#9989; 响应时间必须合理

* **选项卡**。 如果对操作的响应需要的时间超过三秒，则必须提供加载消息或警告。
* **Bot**。 对用户命令的响应必须在两秒内发生。 如果需要更长的处理，应用程序必须显示键入指示器。
* **撰写扩展**。 对用户命令的响应必须在5秒内发生。

> [!TIP]
> 确保您的应用程序在您的应用程序需要响应的时间过长时显示加载指示器或某种形式的警告。

### <a name="9989-tab-content-should-not-have-excessive-chrome-or-layered-navigation"></a>&#9989; 选项卡内容不应具有过多的 chrome 或分层导航

* 选项卡应提供重点内容并避免不必要的 UI 元素。 通常，这通常是指不必要的嵌套/分层导航，内容旁边的无关或不相关的 UI，或任何使用户不相关内容的链接。 例如，下面是一个选项卡视图，它省略了导航菜单，仅展示了主要内容：

![Sharepoint web 视图](~/assets/images/faq/web-sp.png)
![SharePoint 选项卡视图](~/assets/images/faq/tab-sp.png)

* 如果有多个视图选项，请考虑具有一个选项卡配置菜单供用户选择。 例如，将菜单放在 "配置" 页中，以使实际的选项卡视图干净且具有焦点，而不是在选项卡中嵌入菜单。

!["广域观点配置" 页](~/assets/images/faq/wideidea.png)

### <a name="9989-tab-configuration-must-happen-in-the-configuration-screen"></a>"&#9989;" 选项卡配置必须出现在 "配置" 屏幕中

* 配置屏幕应清楚地说明体验的价值以及如何配置选项卡。
* 配置过程不应终止用户体验，并始终为用户提供一种继续操作的方法。
* 即使用户无法立即找到要查找的内容，用户也应始终能够完成配置体验。
* 配置体验应为用户提供用于查找其内容、固定 URL 或创建新内容（如果不存在）的选项。
* 用户不必保留配置体验即可创建内容，然后再返回到团队进行固定。

![OneNote 允许用户在无法找到案例备注时粘贴 OneNote 链接](~/assets/images/faq/tab-onenote-config.png)

![用户始终可以在规划器上创建新计划，以防不存在现有计划](~/assets/images/faq/tab-planner-config.png)

![SharePoint 还允许用户直接粘贴 SharePoint 链接](~/assets/images/faq/tab-sp-config.png)

### <a name="9989-bots-must-always-be-responsive-and-fail-gracefully"></a>&#9989; Bot 必须始终响应并正常进行故障切换

你的 bot 应响应任何命令，而不是用户的终止。 下面的一些提示可帮助你的机器人智能地对用户做出响应：

* **使用命令列表**。 分析用户输入或预测用户意图非常困难。 而不是让用户猜出你的 bot 可以执行的操作，而是提供你的 bot 理解的命令列表。

![流命令列表](~/assets/images/faq/flow-bot.png)

* **包含 "帮助" 命令**。 用户在丢失时或者在你的 bot 未按预期响应时，可能会键入 "帮助"。 包含一个帮助命令，该命令描述应用程序的值将如何与所有有效命令一起使用。

![流帮助命令](~/assets/images/faq/flow-help.png)

* **在你的 bot 丢失时包括帮助内容或指南**。 当你的 bot 无法识别用户输入时，它应建议另一个操作。 例如， *"我很抱歉，我不理解。有关详细信息，请键入 "help"。* 不要使用错误消息进行响应，也不要简单说出 *"我不知道"*。 使用此机会讲授你的用户。

* 请**考虑所有作用域**。 在频道和个人对话中提到（`@*botname*`）时，请确保你的 bot 提供了适当的响应。 如果你的 bot 未在个人或团队作用域内提供有意义的上下文，请通过清单禁用该作用域。 （请参阅`bots` [Microsoft 团队清单架构参考](~/resources/schema/manifest-schema.md#bots)中的 "阻止"。）

### <a name="9989-bots-must-send-a-welcome-message-on-first-launch"></a>&#9989; Bot 必须在首次启动时发送欢迎消息

欢迎邮件是设置你的 bot 语气的最佳方式。 这是用户与 bot 的第一个交互操作。 最好的欢迎消息可以鼓励用户继续浏览应用。 如果欢迎或介绍性邮件令人困惑或不清楚，用户将不会立即看到应用程序的价值，也不会失去兴趣。 欢迎消息必须包含以下内容：

* 帮助命令。
* 价值主张
* 所有有效命令。

在设计欢迎消息时，需要注意以下几点：

#### <a name="personal-scope"></a>个人作用域

* **使您的邮件简洁和提供信息**。 大多数情况下，用户对你的应用的体验和了解可能会有所不同。 他们可能在其他平台上使用过您的应用程序，或者对您的应用程序一无所知。 您想要将您的邮件量身定制给所有访问群体，并在几个句子中说明你的 bot 的功能和与之交互的方法。 此外，还应说明应用程序的价值，以及用户将如何使用它。
![Cafe 和 Dinning bot](~/assets/images/faq/cafe-bot.png)

* **使您的邮件可操作**。 请考虑安装您的应用程序后，您希望用户做的第一件事。 是否有要尝试的酷命令？ 是否有其他应知道的启动体验？ 他们是否需要登录？ 可以在自适应卡片上添加操作，也可以提供具体示例，如 *"请尝试 ..."*， *"这是我可以执行的操作 ..."*。

#### <a name="team-scope"></a>团队作用域

当 bot 第一次添加到频道时，有些不同。 通常情况下，不应向团队中的每个人发送1:1 邮件，但机器人可以在频道中发送欢迎消息。

> [!div class="nextstepaction"]
> [了解有关团队应用程序审批策略的详细信息](/legal/marketplace/certification-policies#1140-teams) 