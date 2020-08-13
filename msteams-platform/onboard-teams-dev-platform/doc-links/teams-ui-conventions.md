---
title: 确定团队应用程序上下文
author: heath-hamilton
description: 在规划团队应用程序时，您必须确定是否将在协作空间、个人空间或两者中使用应用程序。
ms.openlocfilehash: 05c92aa8b199cbdb58e477fb4a64467c150edbfd
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651892"
---
# <a name="getting-to-know-teams-ui-conventions"></a><span data-ttu-id="d399e-103">获取已知团队 UI 约定</span><span class="sxs-lookup"><span data-stu-id="d399e-103">Getting to know Teams UI conventions</span></span>

<span data-ttu-id="d399e-104">应用程序通常表现出一个或多个标准团队 UI 约定。</span><span class="sxs-lookup"><span data-stu-id="d399e-104">Apps typically exhibit one or more standard Teams UI conventions.</span></span> <span data-ttu-id="d399e-105">使用这些约定构建应用程序的功能会导致丰富的体验，让团队用户的本地体验感到不上。</span><span class="sxs-lookup"><span data-stu-id="d399e-105">Building out your app's capabilities using these conventions leads to rich experiences that feel native to Teams users.</span></span>

## <a name="cards"></a><span data-ttu-id="d399e-106">卡</span><span class="sxs-lookup"><span data-stu-id="d399e-106">Cards</span></span>

<span data-ttu-id="d399e-107">[卡片](~/task-modules-and-cards/what-are-cards.md) 是由架构化 JSON 定义的 UI 容器，可包含多个属性和附件。</span><span class="sxs-lookup"><span data-stu-id="d399e-107">[Cards](~/task-modules-and-cards/what-are-cards.md) are UI containers defined by schematized JSON that can contain multiple properties and attachments.</span></span> <span data-ttu-id="d399e-108">它们可以包含带格式的文本、媒体、控件 (如下拉框和单选按钮) 和用于触发卡片操作的按钮。</span><span class="sxs-lookup"><span data-stu-id="d399e-108">They can contain formatted text, media, controls (like dropdown boxes and radio buttons) and buttons that trigger card actions.</span></span>

<span data-ttu-id="d399e-109">卡片操作可向应用程序的 API 发送有效负载、打开链接、启动身份验证流或向对话发送邮件。</span><span class="sxs-lookup"><span data-stu-id="d399e-109">Card actions can send payloads to your app's API, open a link, initiate authentication flows, or send messages to conversations.</span></span> <span data-ttu-id="d399e-110">团队平台支持多种类型的卡片，包括自适应卡片、英雄卡片、缩略图卡片等。</span><span class="sxs-lookup"><span data-stu-id="d399e-110">The Teams platform supports multiple types of cards, including Adaptive Cards, hero cards, thumbnail cards, and more.</span></span> <span data-ttu-id="d399e-111">您可以组合卡片集合并显示在列表或轮播中。</span><span class="sxs-lookup"><span data-stu-id="d399e-111">You can combine card collections and displayed in a list or carousel.</span></span>

## <a name="task-modules"></a><span data-ttu-id="d399e-112">任务模块</span><span class="sxs-lookup"><span data-stu-id="d399e-112">Task modules</span></span>

<span data-ttu-id="d399e-113">[任务模块](~/task-modules-and-cards/what-are-task-modules.md) 提供了团队中的模式弹出窗口体验。</span><span class="sxs-lookup"><span data-stu-id="d399e-113">[Task modules](~/task-modules-and-cards/what-are-task-modules.md) provide modal popup experiences in Teams.</span></span> <span data-ttu-id="d399e-114">它们对于启动工作流、收集用户输入或显示丰富的信息（如视频或 Power BI 仪表板）尤其有用。</span><span class="sxs-lookup"><span data-stu-id="d399e-114">They are especially useful for initiating workflows, collecting user input, or displaying rich information such as videos or Power BI dashboards.</span></span> <span data-ttu-id="d399e-115">在任务模块中，可以运行自定义前端代码、显示 `<iframe>` 小部件或显示自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="d399e-115">In task modules, you can run custom front-end code, display an `<iframe>` widget, or show an Adaptive Card.</span></span>

<span data-ttu-id="d399e-116">考虑您想要如何构建应用程序时，请记住，模式是用户输入信息或完成任务（与选项卡或基于对话的 bot 体验相比）的自然。</span><span class="sxs-lookup"><span data-stu-id="d399e-116">When considering how you want to build your app, remember that modals are natural for users to enter information or complete tasks compared to a tab or a conversation-based bot experience.</span></span>

## <a name="deep-links"></a><span data-ttu-id="d399e-117">深度链接</span><span class="sxs-lookup"><span data-stu-id="d399e-117">Deep links</span></span>

<span data-ttu-id="d399e-118">您的应用程序可以创建 [URL 深层链接](~/concepts/build-and-test/deep-links.md) ，以帮助您通过您的应用程序和团队客户端导航您的用户。</span><span class="sxs-lookup"><span data-stu-id="d399e-118">Your app can create [URL deep links](~/concepts/build-and-test/deep-links.md) to help navigate your user through your app, and the Teams client.</span></span> <span data-ttu-id="d399e-119">您可以为团队中的大多数实体创建 deeplink，有些 (如新的会议请求) 允许您使用 URL 中的查询字符串预填充信息。</span><span class="sxs-lookup"><span data-stu-id="d399e-119">You can create a deeplink for most entities within Teams, and some (like a new meeting request) allow you to pre-populate information using query strings in the URL.</span></span> 

<span data-ttu-id="d399e-120">例如，您的会话自动程序可以向任务模块发送一封邮件，其中包含一个 deeplink，以将一个卡片作为一对一的邮件发送给一个用户，而这又包含一个 deeplink，以便在特定的日期/时间使用特定用户新建会议。</span><span class="sxs-lookup"><span data-stu-id="d399e-120">For example, your conversational bot could send a message to a channel with a deeplink to a task module that results in a card being sent as a one-to-one message to a user, that in turn contains a deeplink to create a new meeting with a specific user at a certain date/time.</span></span> <span data-ttu-id="d399e-121">使用深层链接可在应用程序可用的各种扩展点之间进行连接，始终保持用户在正确的上下文中的持续时间。</span><span class="sxs-lookup"><span data-stu-id="d399e-121">Use deep links to connect across the various extension points available to your app, keeping your user in the correct context at all times.</span></span>

## <a name="web-based-content"></a><span data-ttu-id="d399e-122">基于 Web 的内容</span><span class="sxs-lookup"><span data-stu-id="d399e-122">Web-based content</span></span>

<span data-ttu-id="d399e-123">[基于 Web 的内容](~/tabs/how-to/create-tab-pages/content-page.md) 是您承载的可嵌入到选项卡或任务模块中的网页。</span><span class="sxs-lookup"><span data-stu-id="d399e-123">[Web-based content](~/tabs/how-to/create-tab-pages/content-page.md) is a webpage you host that can be embedded in a tab or task module.</span></span> <span data-ttu-id="d399e-124">若要在团队客户端中嵌入您的网页，必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="d399e-124">To embed your webpage in the Teams client, it must:</span></span>

* <span data-ttu-id="d399e-125">包含 `HTTPS` 在 URL 中。</span><span class="sxs-lookup"><span data-stu-id="d399e-125">Include `HTTPS` in the URL.</span></span>
* <span data-ttu-id="d399e-126">嵌入在中 `<iframe>` 。</span><span class="sxs-lookup"><span data-stu-id="d399e-126">Be embedded in an `<iframe>`.</span></span>
* <span data-ttu-id="d399e-127">包括 Microsoft 团队 JavaScript 客户端 SDK，并 `initialize()` 在页面加载时调用 SDK 的方法。</span><span class="sxs-lookup"><span data-stu-id="d399e-127">Include the Microsoft Teams JavaScript client SDK and invoke the SDK's `initialize()` method on page load.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d399e-128">后续步骤</span><span class="sxs-lookup"><span data-stu-id="d399e-128">Next steps</span></span>

* [<span data-ttu-id="d399e-129">设计应用程序</span><span class="sxs-lookup"><span data-stu-id="d399e-129">Designing your app</span></span>](../../tabs/design/tabs.md)
