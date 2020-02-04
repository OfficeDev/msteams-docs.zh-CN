---
title: 提示和频繁失败的情况
description: 描述提交和大多数失败策略的提示
keywords: 团队发布 faq 失败常见案例提示
ms.openlocfilehash: ffb472c918a205bdcf921b967269a80fcaa93338
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673333"
---
# <a name="tips-and-frequently-failed-cases"></a>提示和频繁失败的情况 

本文介绍了应用失败验证的一些最常见原因。 它不是您的应用程序的所有潜在问题的详尽列表。 但是，如果遵循本指南，首次传递的可能性会大大增加。 请参阅此处的详细策略列表： [AppSource 验证策略](https://dev.office.com/officestore/docs/validation-policies)。 整个 AppSource 验证策略的第14节中的策略特定于 Microsoft 团队应用。

## <a name="tips-for-successful-app-submission"></a>成功提交应用程序的提示

* 确保使用的是1.4.1 或更高版本的团队 JavaScript SDK。
* 请勿在验证过程中对应用进行更改。 这将需要对您的应用程序进行完整的重新验证。
* 您的应用程序不得停止响应、意外终止或包含编程错误。 如果遇到问题，应使用有效的方法向用户转发邮件，以使其正常失败。
* 您的应用程序不得在用户环境中自动下载、安装或启动任何可执行代码。 任何下载都应从用户处寻求显式权限。
* 与您的体验相关联的任何材料（如说明和支持文档）都必须是准确的。 在您的说明和材料中，使用正确的拼写、大小写、标点符号和语法。
* 帮助和支持：强烈建议为你的团队应用提供 "帮助/常见问题解答" 链接，并在首次运行的用户体验中提供此链接。 对于所有个人应用，我们建议您将 "帮助" 页提供为 "个人" 选项卡，以获得更好的用户体验。

## <a name="policy-112-sign-up-sign-in-and-sign-out"></a>策略11.2：注册、登录和注销

说明：应用程序必须提供清晰、简单的登录/输出和（如果适用）注册体验。 您的应用程序中的所有功能都必须能够访问体验。

* 如果向用户提供了显式登录选项，则还必须有一个注销选项（即使该应用程序使用的是 SSO/无提示身份验证）
* 注销选项必须仅注销您的应用程序的功能，而不是从团队客户端进行签名。
* 具有登录的每个作用域也必须具有注销。 注销选项至少应将用户从登录时所使用的相同功能中签出。 例如，如果登录选项将用户登录到邮件扩展和选项卡，则 "注销" 选项必须从邮件扩展名和选项卡中注销用户。

* 确保始终有一种方法来撤消以下（或类似）行为：
  * 登录 => 注销
  * 链接帐户/服务 => 取消链接帐户/服务
  * 连接帐户/服务 => 断开帐户/服务
  * 授权帐户/服务 => 取消/取消授权帐户/服务
  * 注册帐户/服务 => 取消注册帐户/服务
* 如果您的应用程序需要帐户或服务，则必须为用户提供注册或请求注册的方法。 如果您的应用程序符合 "企业" 应用程序类别，则可以查找注册过程的例外。
* 登录/注销功能必须在移动客户端上工作。 确保已将您的团队 JavaScript SDK 升级到版本1.4.1 或更高版本。

有关身份验证的其他信息，请参阅：

* [身份验证文档](~/concepts/authentication/authentication.md)
* [节点中的 Bot 身份验证示例](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
* [节点中的 Tab 身份验证示例](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [C #/.NET 中的选项卡/机器人身份验证](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

## <a name="policy-145-microsoft-teams-apps-must-respond-in-a-reasonable-timeframe"></a>策略14.5： Microsoft 团队应用必须在合理的时间段内做出响应。

* 14.5.1：对于选项卡，如果对某个操作的响应时间超过三秒，则必须提供加载消息或警告。
* 14.5.2：对于 bot，对用户命令的响应必须在两秒钟内发生。 如果需要更长的处理，则必须使用键入指示器。
* 14.5.3：对于撰写扩展，必须在5秒内发生对用户命令的响应。

> [!TIP]
> 请确保在应用程序花费的时间太长时包括加载指示器。

## <a name="policy-14153-content-in-a-tab-should-not-have-superfluousunnecessary-ui-aka-ui-chrome-or-layered-navigation"></a>Policy 14.15.3：选项卡中的内容不应具有多余/不必要的 UI （也称为： UI Chrome）或分层导航

选项卡应提供重点内容并避免与此内容无关的 UI 元素。 通常，这通常指的是不必要的嵌套/分层导航、内容旁边的不相关或不相关的 UI 或任何链接，以使用户拥有与该选项卡的内容不相关的内容。 例如，SharePoint 将从导航菜单中去除，并且仅 showcased 选项卡中的主要内容。

![Sharepoint web 视图](~/assets/images/faq/web-sp.png)
![SharePoint 选项卡视图](~/assets/images/faq/tab-sp.png)

如果有多个视图选项，请考虑具有一个选项卡配置菜单供用户选择。 例如，在选项卡中不嵌入菜单，宽创意将菜单放在 "配置" 页中，以使实际的选项卡视图干净且具有焦点。

!["广域观点配置" 页](~/assets/images/faq/wideidea.png)

## <a name="policy-14157-bots-must-respond-to-any-command-and-must-not-dead-end-the-user"></a>Policy 14.15.7： Bot 必须响应任何命令，并且不得终止用户

你的 bot 应始终响应。 下面的一些提示可帮助你的 bot 更智能地响应用户。

**使用命令列表：** 分析用户输入或预测用户的意图很困难。 为用户提供你的 bot 可以理解的命令列表，而不是让用户猜测你的机器人可以执行的操作。

![流命令列表](~/assets/images/faq/flow-bot.png)

**包含 "帮助" 命令：** 用户在丢失时或者在你的 bot 未使用其预期的响应时，最可能键入 "帮助"。 包含一个帮助命令，其中提供了你的价值主张以及所有有效命令。

![流帮助命令](~/assets/images/faq/flow-help.png)

**在你的 bot 丢失时包括帮助内容或指导：** 当您无法理解用户输入时，请为用户提供他们可以执行的操作。 例如，"我很抱歉，不理解。 有关详细信息，请键入 "help"。 不要使用错误消息进行响应，也不要简单地说出 "我不知道"。 使用此机会讲授你的用户。

**在两个作用域中进行思考：** 如果需要，请确保你的 bot 在频道和个人对话中提及（@*botname*）时提供适当的响应。 如果你的 bot 未在个人或团队作用域内提供有意义的上下文，请通过清单禁用该作用域。 （请参阅`bots` [Microsoft 团队清单架构参考](~/resources/schema/manifest-schema.md#bots)中的 "阻止"。）

## <a name="policy-14159-bot-must-send-welcome-messages-on-the-first-launch"></a>Policy 14.15.9： Bot 必须在首次启动时发送欢迎消息

欢迎邮件是设置语气的最佳方式。 这是第一个与 bot 的交互用户。 好的欢迎消息可以鼓励用户继续浏览应用程序，但如果出现错误，用户可能会在不会立即看到应用程序的值的情况下失去兴趣。

### <a name="personal-scope"></a>个人作用域

在首次启动 bot 时，用户应从自动程序中获取欢迎消息，即使在登录前也是如此。 在设计欢迎消息时需要考虑的几个提示：

**简化邮件的简要和信息性：** 您的应用程序可能具有极其不同的体验和知识。 他们可能在其他平台上使用过您的应用程序，或者可能不知道您的应用程序的任何内容。 您想要将您的邮件量身定制给所有访问群体，并通过几个句子说明你的 bot 的功能和与之交互的方法。 此外，还应说明应用程序的价值，以及用户将如何使用它。
![Cafe 和 Dinning bot](~/assets/images/faq/cafe-bot.png)

**使您的邮件可操作：** 请考虑安装您的应用程序后，您希望用户做的第一件事。 是否有任何要尝试的酷命令？ 是否有其他应知道的启动体验？ 他们是否需要登录？ 可以在自适应卡片上添加操作，也可以提供具体示例，如 "请尝试 ..."，"这是我可以执行的操作 ..."。

### <a name="team-scope"></a>团队作用域

当 bot 第一次添加到频道时，有些不同。 通常情况下，不应向团队中的每个人发送1:1 邮件，但机器人可能会在频道中发送一封欢迎消息。

## <a name="policy-141510-tab-configuration-ui-should-not-dead-end-the-experience-and-always-provide-a-way-for-a-user-to-continue"></a>策略14.15.10：选项卡配置 UI 不应终止体验，并始终为用户提供一种继续操作的方法

即使用户无法立即找到要查找的内容，用户也应始终能够完成配置体验。 配置体验应为用户提供用于查找其内容或固定 URL 的选项，如果不存在，则创建新的内容。 用户不必保留配置体验即可创建内容，然后再返回到团队进行固定。

![OneNote 允许用户在无法找到案例备注时粘贴 OneNote 链接](~/assets/images/faq/tab-onenote-config.png)

![用户始终可以在规划器上创建新计划，以防不存在现有计划](~/assets/images/faq/tab-planner-config.png)

![SharePoint 还允许用户直接粘贴 SharePoint 链接](~/assets/images/faq/tab-sp-config.png)