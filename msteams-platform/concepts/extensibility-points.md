---
title: 团队客户端中的可扩展点
author: clearab
description: 了解 Microsoft 团队客户端中适用于你的应用的扩展点。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f65a5111bf59b08347291caa15c557dc0a48e886
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673065"
---
# <a name="extensible-points-in-the-teams-client"></a>团队客户端中的可扩展点

在 Microsoft 团队平台上构建的应用程序使用托管的 web 服务扩展 Microsoft 团队客户端（web、移动和桌面）。 团队平台提供了一组丰富且灵活的可扩展性点、UI 构造和 Api，以便您在构建应用程序时充分利用这些功能。 您的应用程序可以像将现有网站嵌入到团队的选项卡中一样简单，也可以在全功能的多面应用程序在团队客户端的整个范围内吸引用户。 您可以选择集成现有应用，或创建完全为工作组构建的新体验。

可以在多个位置扩展 Microsoft 团队客户端，以允许用户与您的应用程序进行交互。 根据您的方案，您可以选择将重点放在单个扩展点（如个人对话机器人），也可以将多个扩展点组合在一起。

## <a name="teams-channels-and-group-chats"></a>团队、频道和组聊天

团队、频道和组聊天允许多人进行协作。 此上下文中的应用使自己可供组或对话的所有成员使用，通常重点是启用其他协作工作流或解锁新的社会交互。 您的应用程序将有权访问 Api，使其能够获取有关会话中成员、团队中的渠道以及有关团队或对话的元数据的信息。

可通过以下方式扩展它们：

* **[会话 bot](~/bots/what-are-bots.md)** 通过聊天与对话成员交互，并响应事件（如正在添加的新成员或正在重命名的通道）。 与此上下文中的 bot 的所有对话对频道或组的所有成员都是可见的，因此您需要确保对话与每个人都相关。

* **[可配置的选项卡](~/tabs/what-are-tabs.md)**，提供为安装在的频道或组聊天中配置的全屏嵌入式 web 体验。 所有成员都将在相同的共享 web 应用上进行交互，因此无状态的单页面应用体验是典型的。

* **[Webhook 和连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)**，使外部服务能够将邮件发布到对话，以及向您的用户发送邮件到您的服务。 您可以利用卡片和卡片操作来创建丰富的可操作邮件。

### <a name="personal-apps"></a>个人应用程序

[个人应用](~/concepts/design/personal-apps.md)是团队应用中重点关注与单个用户的交互的部分。 每个用户的体验各不相同。 你的应用程序的此部分可以固定到左导航滑轨，为你的用户启用一次单击访问。

它们可以包含：

* 与用户之间有一对一对话的**[对话 bot](~/bots/what-are-bots.md)** 。 由于这是私人对话，如果你的应用需要进行多项对话，或者提供仅与单个用户相关的通知，则通常最好在个人应用中进行此交互。

* 提供全屏嵌入式 web 体验的**[个人选项卡](~/tabs/what-are-tabs.md)**。

## <a name="messages"></a>邮件

邮件是团队中的协作的核心。 使用**[邮件扩展操作命令](~/messaging-extensions/what-are-messaging-extensions.md)**，应用可以允许用户从邮件中调用您的应用程序的 API，将邮件内容发送到您的应用程序以进行处理或操作。 您的应用程序可以通过向用户呈现表单（任务模块）来做出响应，以收集详细信息、向原始邮件发送回复或将邮件直接发送给用户。

## <a name="writing-messages"></a>写入邮件

您的应用程序可以通过使用户能够在外部系统中搜索或执行操作，并使用可操作按钮以丰富的结构化格式来插入结果，从而帮助用户创建更有效的邮件。

您的应用程序可以通过三种方法来帮助用户创建更好的邮件：

* **[邮件扩展-搜索命令](~/messaging-extensions/what-are-messaging-extensions.md)**，允许他们快速搜索外部系统、预览搜索结果，然后将结果作为富卡片插入聊天。

* **[消息扩展-link unfurling](~/messaging-extensions/what-are-messaging-extensions.md)** 允许你的应用监视你感兴趣的 web 域。 将包含该域的 URL 粘贴到 "撰写" 消息框中时，将会调用应用程序的 API，从而使您能够向邮件添加丰富的卡片，其中包含有关要链接到的项目的其他信息。

* **[邮件扩展-操作命令](~/messaging-extensions/what-are-messaging-extensions.md)** 向用户呈现模式窗体（任务模块），将窗体的结果提交到您的应用程序，然后直接在对话中插入邮件，或创建用户在发送到对话之前可以编辑的部分邮件。

## <a name="user-interface-ui-elements"></a>用户界面（UI）元素

除了扩展点之外，Microsoft 团队平台还提供灵活的 UI 元素，以便应用充分利用这些元素。 通过这些元素，您可以创建丰富的体验，使其成为团队客户端的本机外观。

### <a name="cards--card-actions"></a>卡片 & 卡片操作

[卡片](~/task-modules-and-cards/what-are-cards.md)是由架构化 JSON 定义的用户界面容器，可包含多个属性和附件。 它们可以包含经过格式化的文本、媒体、控件（如下拉框和单选按钮）以及触发卡片操作的按钮。 卡片操作可向应用程序的 API 发送有效负载、打开链接、启动身份验证流或向对话发送邮件。 Microsoft 团队平台支持多种类型的卡片，包括自适应卡片、英雄卡片、缩略图卡片等。 它们可以组合到卡片集合中，并显示在列表或轮播中。

### <a name="task-modules"></a>任务模块

[任务模块](~/task-modules-and-cards/what-are-task-modules.md)使您能够在团队应用程序中创建模式弹出窗口体验。 在弹出式菜单中，您可以运行自己的自定义 HTML/JavaScript 代码`<iframe>` ，显示小部件（如 YouTube 或 Microsoft Stream 视频）或显示自适应卡片。 它们在启动和完成任务或显示丰富的信息（如视频或 Power BI 仪表板）时尤其有用。 与选项卡或基于对话的 bot 体验相比，启动和完成任务的用户的弹出体验通常更为自然。

### <a name="deep-links"></a>Deep links

您的应用程序可以创建[URL 深层链接](~/concepts/build-and-test/deep-links.md)，以帮助您通过您的应用程序和团队客户端导航您的用户。 您可以为团队中的大多数实体创建 deeplink，某些（如新的会议请求）允许您使用 URL 中的查询字符串预填充信息。 例如，您的会话自动程序可以向任务模块发送一封邮件，其中包含一个 deeplink，以将一个卡片作为一对一的邮件发送给一个用户，而这又包含一个 deeplink，以便在特定的日期/时间使用特定用户新建会议。 使用深层链接可在应用程序可用的各种扩展点之间进行连接，始终保持用户在正确的上下文中的持续时间。

### <a name="web-content-pages"></a>Web 内容页

[Web 内容页](~/tabs/how-to/create-tab-pages/content-page.md)是可嵌入到选项卡或任务模块中的承载的网页。 若要使您的网页嵌入 Microsoft 团队客户端，必须执行以下操作：

* 在 HTTPS 上托管。
* 能够`<iframe>`由团队客户端嵌入。
* 包括 Microsoft 团队 JavaScript 客户端 SDK，并在页面加载时`initialize()`调用 SDK 的方法。
