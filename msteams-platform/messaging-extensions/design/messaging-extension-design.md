---
title: 邮件扩展的设计准则
description: 介绍创建邮件扩展的准则
keywords: 团队设计准则参考邮件扩展提示最佳实践
author: EmilyyC
ms.author: qinch
ms.openlocfilehash: 5d62646c5757f93cc4f6ae6e089ef3a0918f9eea
ms.sourcegitcommit: 81ac2a1070d16e20ae0e4cb6137dce09b31914af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "45152684"
---
# <a name="start-sharing-with-powerful-messaging-extensions"></a><span data-ttu-id="23c93-104">开始与强大的邮件扩展进行共享</span><span class="sxs-lookup"><span data-stu-id="23c93-104">Start sharing with powerful messaging extensions</span></span>

<span data-ttu-id="23c93-105">邮件扩展用于共享可操作内容。</span><span class="sxs-lookup"><span data-stu-id="23c93-105">Messaging extensions are designed for sharing actionable content.</span></span> <span data-ttu-id="23c93-106">此功能表示在我们的堆栈中投资回报率最高（ROI）。</span><span class="sxs-lookup"><span data-stu-id="23c93-106">This feature represents the highest return on investment (ROI) in our stack.</span></span> <span data-ttu-id="23c93-107">邮件扩展在聊天和频道中工作、支持多个查询终结点、启用新实体的创建以及使用链接 unfurling 创建自定义链接预览。</span><span class="sxs-lookup"><span data-stu-id="23c93-107">Messaging extensions work in chat and channels, support multiple query endpoints, enable the creation of new entities, and work with link unfurling to create custom link previews.</span></span> <span data-ttu-id="23c93-108">困难在于，虽然功能强大且非常有用，但它并不容易被发现。</span><span class="sxs-lookup"><span data-stu-id="23c93-108">The challenge is that while the feature is powerful and incredibly useful, it's not easily discoverable.</span></span> <span data-ttu-id="23c93-109">本指南将帮助您创建可供多个用户使用的、易于使用的邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="23c93-109">This guide will help you create messaging extensions that are readily found and utilized by more users.</span></span>

## <a name="design-guidelines"></a><span data-ttu-id="23c93-110">设计准则</span><span class="sxs-lookup"><span data-stu-id="23c93-110">Design guidelines</span></span>

### <a name="show-content-as-a-user-type"></a><span data-ttu-id="23c93-111">将内容显示为用户类型</span><span class="sxs-lookup"><span data-stu-id="23c93-111">Show content as a user type</span></span>

<span data-ttu-id="23c93-112">邮件扩展提供了使用关键字搜索查找可与一个或多个用户共享的可操作内容的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="23c93-112">Messaging extensions present a unique way to use keyword searches to find actionable content that can be shared with one or more users.</span></span> <span data-ttu-id="23c93-113">此首选交互允许用户输入具有延迟自动查询的搜索词作为用户类型。</span><span class="sxs-lookup"><span data-stu-id="23c93-113">This preferred interaction allows users to enter search terms with a delayed auto query as the user type.</span></span> <span data-ttu-id="23c93-114">此模型为模拟建议结果和要求用户键入最少字符做了很好的工作。</span><span class="sxs-lookup"><span data-stu-id="23c93-114">This model does a good job of simulating suggested results and requires users to type minimal characters.</span></span>

> [!TIP]
><span data-ttu-id="23c93-115">可能，但不适合要求用户 `enter` `search` 在发送查询时选择或之前。</span><span class="sxs-lookup"><span data-stu-id="23c93-115">It's possible, but not desirable, to require users to select `enter` or `search` before sending queries.</span></span> <span data-ttu-id="23c93-116">当后端服务的压力较少时，此模型不是标准模型，可能会混淆用户。</span><span class="sxs-lookup"><span data-stu-id="23c93-116">While there is less stress on the backend service, this model is not the norm and may confuse users.</span></span>

### <a name="consider-zero-term-queries"></a><span data-ttu-id="23c93-117">考虑零术语查询</span><span class="sxs-lookup"><span data-stu-id="23c93-117">Consider zero-term queries</span></span>

<span data-ttu-id="23c93-118">零术语查询直接由用户操作触发，而不是由用户在搜索框中写入术语。</span><span class="sxs-lookup"><span data-stu-id="23c93-118">Zero-term queries are directly triggered by user action, rather than by the user writing terms in a search box.</span></span> <span data-ttu-id="23c93-119">所有邮件扩展都受益于零期限查询，通常基于用户上次在服务中看到的内容。</span><span class="sxs-lookup"><span data-stu-id="23c93-119">All messaging extensions benefit from zero-term queries, usually based on what the user last saw on the service.</span></span> <span data-ttu-id="23c93-120">优势在于，希望共享用户上次看到的内容相当高的可能性。</span><span class="sxs-lookup"><span data-stu-id="23c93-120">The advantage is that the likelihood of wanting to share something the user last saw is quite high.</span></span> <span data-ttu-id="23c93-121">其他零术语查询可能基于该服务。</span><span class="sxs-lookup"><span data-stu-id="23c93-121">Other zero-term queries might be based on the service.</span></span> <span data-ttu-id="23c93-122">例如， `news` 可能显示最近发布的最近事件和即将到来的新闻扩展。</span><span class="sxs-lookup"><span data-stu-id="23c93-122">For instance, `news`  might show recently posted news extensions from recent and upcoming events.</span></span>

<img width="450px" title=""新建配置" 选项卡" src="../../assets/images/messaging-extension/zero-term-query.png" />

### <a name="include-link-unfurling"></a><span data-ttu-id="23c93-124">包含链接 unfurling</span><span class="sxs-lookup"><span data-stu-id="23c93-124">Include link unfurling</span></span>

<span data-ttu-id="23c93-125">在团队中共享内容的最常见方法之一是通过超链接，无论它是已在使用中的任务，还是您找到了有趣的视频。</span><span class="sxs-lookup"><span data-stu-id="23c93-125">One of the most common ways to share content in Teams is through a hyperlink, whether it is a task you've been working on or a  video that you found funny.</span></span> <span data-ttu-id="23c93-126">当用户在团队中共享链接时，将显示包括图像、标题或说明的预览。</span><span class="sxs-lookup"><span data-stu-id="23c93-126">When a user shares a link in Teams, a  preview including image, title or description is displayed.</span></span> <span data-ttu-id="23c93-127">通过[链接 unfurling](../how-to/link-unfurling.md) ，您现在可以自定义这些预览。</span><span class="sxs-lookup"><span data-stu-id="23c93-127">With [link unfurling](../how-to/link-unfurling.md) you can now customize these previews.</span></span> <span data-ttu-id="23c93-128">用户在决定使用您的预览后，系统也会提示您安装您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="23c93-128">Users will also be prompted to install your app after they decide to use your preview.</span></span> <span data-ttu-id="23c93-129">向您的应用程序添加链接 unfurling 功能可大大增加您的应用程序可发现性。</span><span class="sxs-lookup"><span data-stu-id="23c93-129">Adding link unfurling functionality to your app can greatly increase your app discoverability.</span></span>

### <a name="highlight-your-messaging-extension"></a><span data-ttu-id="23c93-130">突出显示您的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="23c93-130">Highlight your messaging extension</span></span>

<span data-ttu-id="23c93-131">消息传递扩展并不总是很容易找到。</span><span class="sxs-lookup"><span data-stu-id="23c93-131">Messaging extensions are not always easy to find.</span></span> <span data-ttu-id="23c93-132">在应用程序详细信息页面中添加应用屏幕截图和帮助文档，以确保邮件扩展的功能。</span><span class="sxs-lookup"><span data-stu-id="23c93-132">Include app screenshots in the app detail page and your help documentation to feature your messaging extension.</span></span> <span data-ttu-id="23c93-133">您还可以在 bot 教程中添加您的邮件扩展的操作*方法*文档，以突出显示 bot 交互之外的整个应用程序。</span><span class="sxs-lookup"><span data-stu-id="23c93-133">You can also include *how-to* documentation for your messaging extension in bot tours to highlight the entire app beyond the bot interactions.</span></span>

### <a name="add-actions-on-card"></a><span data-ttu-id="23c93-134">在卡片上添加操作</span><span class="sxs-lookup"><span data-stu-id="23c93-134">Add actions on card</span></span>

<span data-ttu-id="23c93-135">不要只向用户显示文本。</span><span class="sxs-lookup"><span data-stu-id="23c93-135">Don't just display text to users.</span></span> <span data-ttu-id="23c93-136">具有可与之交互的内容，并执行下一个操作。</span><span class="sxs-lookup"><span data-stu-id="23c93-136">Have something they can interact with and perform the next action.</span></span> <span data-ttu-id="23c93-137">例如，"位置" 应用程序不只是在卡片上插入地图，还具有一个按钮，该按钮在选中时将向该位置显示行车路线。</span><span class="sxs-lookup"><span data-stu-id="23c93-137">For example, the Places app doesn't just insert a map on the card, but also has a button that, when selected, will show directions to the location.</span></span> <span data-ttu-id="23c93-138">在获取卡片后，用户可以执行更多任务。</span><span class="sxs-lookup"><span data-stu-id="23c93-138">Users can perform more tasks after obtaining the card.</span></span>

<img width="450px" title=""新建配置" 选项卡" src="../../assets/images/messaging-extension/action-on-card.png" />

### <a name="keep-users-in-the-app-context"></a><span data-ttu-id="23c93-140">将用户保留在应用上下文中</span><span class="sxs-lookup"><span data-stu-id="23c93-140">Keep users in the app context</span></span>

<span data-ttu-id="23c93-141">如果卡片不够，并且需要提供详细信息的链接，请考虑打开一个选项卡，而不是打开浏览器以获得更好的用户体验。</span><span class="sxs-lookup"><span data-stu-id="23c93-141">If a card is not enough and you need to provide a link for more information, consider opening a tab instead of opening a browser for a better user experience.</span></span> <span data-ttu-id="23c93-142">*请参阅*[使用自定义选项卡扩展团队应用](../../tabs/how-to/add-tab.md)</span><span class="sxs-lookup"><span data-stu-id="23c93-142">*See* [Extend your Teams app with a custom tab](../../tabs/how-to/add-tab.md)</span></span>
