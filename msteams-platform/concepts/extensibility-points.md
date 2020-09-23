---
title: 团队应用程序的入口点
author: heath-hamilton
description: 介绍用户在团队中使用应用程序的方式和位置。
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 1c68467177fc440993f059133f049f18785374b7
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "48209779"
---
# <a name="entry-points-for-teams-apps"></a><span data-ttu-id="f31d3-103">团队应用程序的入口点</span><span class="sxs-lookup"><span data-stu-id="f31d3-103">Entry points for Teams apps</span></span>

<span data-ttu-id="f31d3-104">团队平台提供了一组灵活的入口点，用户可在其中发现和使用您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="f31d3-104">The Teams platform provides a flexible set of entry points where people can discover and use your app.</span></span> <span data-ttu-id="f31d3-105">您的应用程序可以像将现有网站嵌入个人选项卡或多面应用程序（用户在多个入口点之间进行交互）一样简单。</span><span class="sxs-lookup"><span data-stu-id="f31d3-105">Your app can be as simple as embedding an existing website in a personal tab or a multi-faceted app that users interact with across several entry points.</span></span>

<span data-ttu-id="f31d3-106">最成功的应用程序会让团队成为本地用户，因此务必仔细规划应用程序的入口点。</span><span class="sxs-lookup"><span data-stu-id="f31d3-106">The most successful apps feel native to Teams, so it's important to carefully plan your app's entry points.</span></span>

## <a name="teams-channels-and-group-chats"></a><span data-ttu-id="f31d3-107">团队、频道和组聊天</span><span class="sxs-lookup"><span data-stu-id="f31d3-107">Teams, channels, and group chats</span></span>

<span data-ttu-id="f31d3-108">团队、频道和组聊天是协作空间。</span><span class="sxs-lookup"><span data-stu-id="f31d3-108">Teams, channels, and group chats are collaboration spaces.</span></span> <span data-ttu-id="f31d3-109">使用这些入口点的应用程序可供所有成员使用，并且通常侧重于其他工作流或解除新的社会交互。</span><span class="sxs-lookup"><span data-stu-id="f31d3-109">Apps that use these entry points are available to all members and typically focus on additional workflows or unlocking new social interactions.</span></span>

<span data-ttu-id="f31d3-110">下面介绍了团队应用程序功能在协作上下文中的常见使用方法：</span><span class="sxs-lookup"><span data-stu-id="f31d3-110">Here's how Teams app capabilities are commonly used in collaborative contexts:</span></span>

* <span data-ttu-id="f31d3-111">[**选项卡**](~/tabs/what-are-tabs.md) 提供为团队、频道或组聊天配置的全屏嵌入式 web 体验。</span><span class="sxs-lookup"><span data-stu-id="f31d3-111">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience configured for the team, channel, or group chat.</span></span> <span data-ttu-id="f31d3-112">所有成员都与基于 web 的内容进行交互，因此无状态的单页面应用体验是典型的。</span><span class="sxs-lookup"><span data-stu-id="f31d3-112">All members interact with the same web-based content, so a stateless single page app experience is typical.</span></span>

* <span data-ttu-id="f31d3-113">[**邮件扩展**](~/messaging-extensions/what-are-messaging-extensions.md) 是将外部内容插入到对话中或对邮件执行操作而不离开团队的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="f31d3-113">[**Messaging extensions**](~/messaging-extensions/what-are-messaging-extensions.md) are shortcuts for inserting external content into a conversation or taking action on messages without leaving Teams.</span></span> <span data-ttu-id="f31d3-114">链接 unfurling 在共享公共 URL 中的内容时提供丰富的内容。</span><span class="sxs-lookup"><span data-stu-id="f31d3-114">Link unfurling provides rich content when sharing content from a common URL.</span></span>

* <span data-ttu-id="f31d3-115">[**Bot**](~/bots/what-are-bots.md) 通过聊天与对话的成员进行交互，并响应事件 (如添加新成员或重命名频道) 。</span><span class="sxs-lookup"><span data-stu-id="f31d3-115">[**Bots**](~/bots/what-are-bots.md) interact with members of the conversation through chat and responding to events (like adding a new member or renaming a channel).</span></span> <span data-ttu-id="f31d3-116">与这些上下文中的 bot 的对话对团队、频道或组的所有成员都可见，因此应与所有人相关的 bot 对话。</span><span class="sxs-lookup"><span data-stu-id="f31d3-116">Conversations with a bot in these contexts are visible to all members of the team, channel, or group, so bot conversations should be relevant to everyone.</span></span>

* <span data-ttu-id="f31d3-117">[**Webhook 和连接器**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) 允许外部服务将邮件发布到对话中，并允许用户向服务发送邮件。</span><span class="sxs-lookup"><span data-stu-id="f31d3-117">[**Webhooks and connectors**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) allow an external service to post messages into a conversation and users to send messages to a service.</span></span>

* <span data-ttu-id="f31d3-118">[**Microsoft GRAPH REST API**](https://docs.microsoft.com/graph/teams-concept-overview) ，用于获取有关团队、频道和组聊天的数据，以帮助自动化和管理团队流程。</span><span class="sxs-lookup"><span data-stu-id="f31d3-118">[**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview) for getting data about teams, channels, and group chats to help automate and manage Teams processes.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="f31d3-119">个人应用</span><span class="sxs-lookup"><span data-stu-id="f31d3-119">Personal apps</span></span>

<span data-ttu-id="f31d3-120">[个人应用](~/concepts/design/personal-apps.md) 重点关注与单个用户的交互。</span><span class="sxs-lookup"><span data-stu-id="f31d3-120">[Personal apps](~/concepts/design/personal-apps.md) focus on interactions with a single user.</span></span> <span data-ttu-id="f31d3-121">此上下文中的体验对每个用户都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="f31d3-121">The experience in this context is unique to each user.</span></span> <span data-ttu-id="f31d3-122">用户可以将个人应用程序固定到左侧导航轨，以便快速访问。</span><span class="sxs-lookup"><span data-stu-id="f31d3-122">Users can pin personal apps to the left navigation rail for quick access.</span></span>

<span data-ttu-id="f31d3-123">下面介绍了团队功能在个人环境中的常用功能：</span><span class="sxs-lookup"><span data-stu-id="f31d3-123">Here's how Teams capabilities are commonly used in personal contexts:</span></span>

* <span data-ttu-id="f31d3-124">[**Bot**](~/bots/what-are-bots.md) 具有与用户的一对一对话。</span><span class="sxs-lookup"><span data-stu-id="f31d3-124">[**Bots**](~/bots/what-are-bots.md) have one-on-one conversations with a user.</span></span> <span data-ttu-id="f31d3-125">需要多转对话或提供仅与特定用户相关的通知的 bot 最适用于个人上下文。</span><span class="sxs-lookup"><span data-stu-id="f31d3-125">Bots that require multi-turn conversations or provide notifications relevant only to a specific user are best suited in personal contexts.</span></span>

* <span data-ttu-id="f31d3-126">[**选项卡**](~/tabs/what-are-tabs.md) 提供了对单个用户有意义的全屏嵌入式 web 体验。</span><span class="sxs-lookup"><span data-stu-id="f31d3-126">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience that's meaningful to individual users.</span></span>

## <a name="ui-components"></a><span data-ttu-id="f31d3-127">UI 组件</span><span class="sxs-lookup"><span data-stu-id="f31d3-127">UI components</span></span>

<span data-ttu-id="f31d3-128">应用程序通常表现出一个或多个标准团队 UI 组件。</span><span class="sxs-lookup"><span data-stu-id="f31d3-128">Apps typically exhibit one or more standard Teams UI components.</span></span> <span data-ttu-id="f31d3-129">使用这些组件构建应用程序会导致丰富的体验，让团队用户的本地体验感到不在。</span><span class="sxs-lookup"><span data-stu-id="f31d3-129">Building out your app using these components leads to rich experiences that feel native to Teams users.</span></span>

### <a name="cards"></a><span data-ttu-id="f31d3-130">卡</span><span class="sxs-lookup"><span data-stu-id="f31d3-130">Cards</span></span>

<span data-ttu-id="f31d3-131">[卡片](~/task-modules-and-cards/what-are-cards.md) 是由 JSON 定义的 UI 容器，可包含带格式的文本、媒体、控件 (如下拉列表和单选按钮) 和触发操作的按钮。</span><span class="sxs-lookup"><span data-stu-id="f31d3-131">[Cards](~/task-modules-and-cards/what-are-cards.md) are UI containers defined by JSON that can contain formatted text, media, controls (like dropdowns and radio buttons) and buttons that trigger an action.</span></span>

<span data-ttu-id="f31d3-132">卡片操作可向应用程序的 API 发送有效负载、打开链接、启动身份验证流或向对话发送邮件。</span><span class="sxs-lookup"><span data-stu-id="f31d3-132">Card actions can send payloads to your app's API, open a link, initiate authentication flows, or send messages to conversations.</span></span> <span data-ttu-id="f31d3-133">团队平台支持多张卡片，包括自适应卡片、英雄卡片、缩略图卡片等。</span><span class="sxs-lookup"><span data-stu-id="f31d3-133">The Teams platform supports multiple cards, including Adaptive Cards, hero cards, thumbnail cards, and more.</span></span> <span data-ttu-id="f31d3-134">您可以组合卡片集合并显示在列表或轮播中。</span><span class="sxs-lookup"><span data-stu-id="f31d3-134">You can combine card collections and display in a list or carousel.</span></span>

### <a name="task-modules"></a><span data-ttu-id="f31d3-135">任务模块</span><span class="sxs-lookup"><span data-stu-id="f31d3-135">Task modules</span></span>

<span data-ttu-id="f31d3-136">[任务模块](~/task-modules-and-cards/what-are-task-modules.md) 在团队中提供了模式体验。</span><span class="sxs-lookup"><span data-stu-id="f31d3-136">[Task modules](~/task-modules-and-cards/what-are-task-modules.md) provide modal experiences in Teams.</span></span> <span data-ttu-id="f31d3-137">它们对于启动工作流、收集用户输入或显示丰富的信息（如视频或 Power BI 仪表板）尤其有用。</span><span class="sxs-lookup"><span data-stu-id="f31d3-137">They are especially useful for initiating workflows, collecting user input, or displaying rich information such as videos or Power BI dashboards.</span></span> <span data-ttu-id="f31d3-138">在任务模块中，可以运行自定义前端代码、显示 `<iframe>` 小部件或显示自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="f31d3-138">In task modules, you can run custom front-end code, display an `<iframe>` widget, or show an Adaptive Card.</span></span>

<span data-ttu-id="f31d3-139">考虑您想要如何构建应用程序时，请记住，模式是用户输入信息或完成任务（与选项卡或基于对话的 bot 体验相比）的自然。</span><span class="sxs-lookup"><span data-stu-id="f31d3-139">When considering how you want to build your app, remember that modals are natural for users to enter information or complete tasks compared to a tab or a conversation-based bot experience.</span></span>

### <a name="deep-links"></a><span data-ttu-id="f31d3-140">深度链接</span><span class="sxs-lookup"><span data-stu-id="f31d3-140">Deep links</span></span>

<span data-ttu-id="f31d3-141">您的应用程序可以创建 [URL 深层链接](~/concepts/build-and-test/deep-links.md) ，以帮助您通过您的应用程序和团队客户端导航您的用户。</span><span class="sxs-lookup"><span data-stu-id="f31d3-141">Your app can create [URL deep links](~/concepts/build-and-test/deep-links.md) to help navigate your user through your app, and the Teams client.</span></span> <span data-ttu-id="f31d3-142">您可以为团队中的大多数实体创建深层链接，有些 (像新的会议请求) 允许您使用 URL 中的查询字符串预填充信息。</span><span class="sxs-lookup"><span data-stu-id="f31d3-142">You can create a deep link for most entities within Teams, and some (like a new meeting request) allow you to pre-populate information using query strings in the URL.</span></span>

<span data-ttu-id="f31d3-143">例如，您的会话自动程序可以向通道发送一封邮件，其中包含指向任务模块的深层链接，从而将一个卡片作为一对一的邮件发送给用户，这又包含一个深层链接，以便在特定日期/时间使用特定用户新建会议。</span><span class="sxs-lookup"><span data-stu-id="f31d3-143">For example, your conversational bot could send a message to a channel with a deep link to a task module that results in a card being sent as a one-to-one message to a user, that in turn contains a deep link to create a new meeting with a specific user at a certain date/time.</span></span> <span data-ttu-id="f31d3-144">使用深层链接可在应用程序可用的各种扩展点之间进行连接，始终保持用户在正确的上下文中的持续时间。</span><span class="sxs-lookup"><span data-stu-id="f31d3-144">Use deep links to connect across the various extension points available to your app, keeping your user in the correct context at all times.</span></span>

### <a name="web-based-content"></a><span data-ttu-id="f31d3-145">基于 Web 的内容</span><span class="sxs-lookup"><span data-stu-id="f31d3-145">Web-based content</span></span>

<span data-ttu-id="f31d3-146">[基于 Web 的内容](~/tabs/how-to/create-tab-pages/content-page.md) 是您承载的可嵌入到选项卡或任务模块中的网页。</span><span class="sxs-lookup"><span data-stu-id="f31d3-146">[Web-based content](~/tabs/how-to/create-tab-pages/content-page.md) is a webpage you host that can be embedded in a tab or task module.</span></span>
