---
title: Microsoft Teams 开发人员平台
author: clearab
description: 介绍 Microsoft 团队开发人员平台的概述页面，以及如何开始为 Microsoft 团队构建应用程序。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: cb9d91f2de29bac00f4cdcd9672adf9d7d4ee734
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673491"
---
# <a name="what-are-microsoft-teams-apps"></a><span data-ttu-id="4f5bd-103">什么是 Microsoft 团队应用？</span><span class="sxs-lookup"><span data-stu-id="4f5bd-103">What are Microsoft Teams apps?</span></span>

<span data-ttu-id="4f5bd-104">Microsoft 团队是 Office 365 中的协作工作区，它与用户使用的应用程序和服务集成，以实现共同完成的工作。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-104">Microsoft Teams is a collaboration workspace in Office 365 that integrates with apps and services people use to get work done together.</span></span> <span data-ttu-id="4f5bd-105">Microsoft 团队开发人员平台使开发人员可以轻松地集成自己的应用程序和服务，以提高工作效率、更快地做出决策、提供焦点（通过减少上下文切换），并围绕现有内容创建协作并流会.</span><span class="sxs-lookup"><span data-stu-id="4f5bd-105">The Microsoft Teams developer platform makes it easy for developers to integrate their own apps and services to improve productivity, make decisions faster, provide focus (by reducing context switching), and create collaboration around existing content and workflows.</span></span> <span data-ttu-id="4f5bd-106">在 Microsoft 团队平台上构建的应用程序是团队客户端和您的服务和工作流之间的桥梁;将它们直接引入协作平台的上下文中。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-106">Apps built on the Microsoft Teams platform are bridges between the Teams client and your services and workflows; bringing them directly into the context of your collaboration platform.</span></span>

## <a name="what-can-teams-apps-do"></a><span data-ttu-id="4f5bd-107">团队应用程序可以做什么？</span><span class="sxs-lookup"><span data-stu-id="4f5bd-107">What can Teams apps do?</span></span>

<span data-ttu-id="4f5bd-108">基于 Microsoft 团队平台构建的应用主要侧重于提高协作能力和提高生产率。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-108">Apps built on the Microsoft Teams platform primarily focus on increasing collaboration and improving productivity.</span></span> <span data-ttu-id="4f5bd-109">您的应用程序可能很简单，如从其他系统发布通知或复杂的多面应用程序。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-109">Your app can be something simple, like posting notifications from other systems, or complex multi-faceted applications.</span></span> <span data-ttu-id="4f5bd-110">只需记住，团队就是社会协作平台;最佳应用重点是帮助人员自己快速学习并更好地协同工作。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-110">Just keep in mind that Teams is a social collaboration platform; the best apps focus on helping people express themselves and work better together.</span></span>

* <span data-ttu-id="4f5bd-111">**对外部系统中的项目进行协作。**</span><span class="sxs-lookup"><span data-stu-id="4f5bd-111">**Collaborate on items in external systems.**</span></span> <span data-ttu-id="4f5bd-112">自定义团队应用程序的一个核心方案是，将信息或项目从某个其他地方引入到团队中，并围绕它进行对话。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-112">One of the core scenarios for a custom Teams app is to bring information or items into Teams from some other place, and have a conversation around it.</span></span> <span data-ttu-id="4f5bd-113">您可以将信息推送到团队中，使用户能够按需搜索和请求，或使其在嵌入的 web 视图中可用。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-113">You can push information into Teams, enable your users to search for and pull it on demand, or make it available in an embedded web view.</span></span>

* <span data-ttu-id="4f5bd-114">**触发对话中的工作流。**</span><span class="sxs-lookup"><span data-stu-id="4f5bd-114">**Trigger workflows from conversations.**</span></span> <span data-ttu-id="4f5bd-115">通常，对话会导致需要启动一些工作流或完成某些操作;请记下有关这一点的说明，查看我的拉取请求，将其转换为销售线索等。您的团队应用可以在团队内部将访问工作流。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-115">Often conversations result in the need to kick off some workflow or complete some action; take a note about that, review my pull request, convert that to a sales lead, etc. Your Teams app can put access to that workflow right inside of Teams.</span></span>

* <span data-ttu-id="4f5bd-116">**将重要事件的团队通知给团队。**</span><span class="sxs-lookup"><span data-stu-id="4f5bd-116">**Notify your team of important events.**</span></span> <span data-ttu-id="4f5bd-117">电子邮件通知的病假？</span><span class="sxs-lookup"><span data-stu-id="4f5bd-117">Sick of email notifications?</span></span> <span data-ttu-id="4f5bd-118">改为向团队发送通知！</span><span class="sxs-lookup"><span data-stu-id="4f5bd-118">Send notifications to Teams instead!</span></span> <span data-ttu-id="4f5bd-119">将通知直接发送给用户、频道、活动源或订阅邮件的任何人。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-119">Send notifications directly to users, to a channel, to the Activity Feed, or to anyone who subscribes to them.</span></span>

* <span data-ttu-id="4f5bd-120">**从其他网站/服务嵌入功能。**</span><span class="sxs-lookup"><span data-stu-id="4f5bd-120">**Embed functionality from other sites/services.**</span></span> <span data-ttu-id="4f5bd-121">有时，您只需让您的应用程序更易于发现。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-121">Sometimes you just need to make your app easier to discover.</span></span> <span data-ttu-id="4f5bd-122">嵌入现有的单页面应用程序，或为团队从头开始构建一些内容。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-122">Embed your existing single-page app, or build something from scratch for Teams.</span></span>

## <a name="how-do-teams-apps-work"></a><span data-ttu-id="4f5bd-123">团队应用程序的工作原理是什么？</span><span class="sxs-lookup"><span data-stu-id="4f5bd-123">How do Teams apps work?</span></span>

<span data-ttu-id="4f5bd-124">有关 Microsoft 团队的自定义应用程序的第一件事（除了可以令人惊奇），团队不是托管服务。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-124">The first thing to know about custom apps for Microsoft Teams (other than how amazing they can be), is that Teams is not a hosting service.</span></span> <span data-ttu-id="4f5bd-125">您的应用程序包包含有关您的应用程序（名称、图标等）的元数据，以及指向承载该应用程序的 web 服务的指针。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-125">Your app package contains metadata about your app (name, icons, etc.), and pointers to the web services you host that power your app.</span></span> <span data-ttu-id="4f5bd-126">Microsoft 团队提供了分发机制、UI/UX 构造以供您利用，并且您可以使用 Api 来扩充可用于您的应用程序的信息和操作。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-126">Microsoft Teams provides the distribution mechanism, UI/UX constructs for you to take advantage of, and APIs you can use to augment the information and actions available to your app.</span></span>

<span data-ttu-id="4f5bd-127">团队应用程序包含三个主要部分：</span><span class="sxs-lookup"><span data-stu-id="4f5bd-127">A Teams app consists of three major pieces:</span></span>

* <span data-ttu-id="4f5bd-128">用户将与您的应用程序进行交互**的 Microsoft 团队客户端（web、桌面或移动版）** 。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-128">**The Microsoft Teams client (web, desktop or mobile)** where users will interact with your app.</span></span>
* <span data-ttu-id="4f5bd-129">**您的团队应用程序包**，用于创建用户安装的应用程序，并包含应用程序的元数据和指向服务的指针。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-129">**Your Teams app package** that creates the app installed by your users, and contains your app's metadata and pointers to your services.</span></span>
* <span data-ttu-id="4f5bd-130">执行必要逻辑的**服务、工作流或网站**对应用程序供电的数据存储和 API 调用。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-130">**Your service, workflow or website** which perform the necessary logic, data storage and API calls to power your app.</span></span>

<span data-ttu-id="4f5bd-131">请务必记住，您在 Microsoft 团队应用程序中公开的任何功能在 internet 上都是公开的，除非您采取其他步骤来保护它。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-131">It is important to keep in mind that any functionality you expose in a Microsoft Teams app is publicly available over the internet unless you take additional steps to secure it.</span></span> <span data-ttu-id="4f5bd-132">如果你要提供对机密或受保护信息的访问权限，你需要确保你的服务至少对连接到你的应用的终结点进行身份验证，或对[你的用户进行身份验证](~/concepts/authentication/authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-132">If you are providing access to confidential or protected information you'll want make sure your services are at a minimum authenticating the endpoint connecting to your app, or [authenticating your users](~/concepts/authentication/authentication.md).</span></span>

## <a name="how-can-you-share-your-teams-app"></a><span data-ttu-id="4f5bd-133">如何共享你的团队应用？</span><span class="sxs-lookup"><span data-stu-id="4f5bd-133">How can you share your Teams app?</span></span>

<span data-ttu-id="4f5bd-134">当您准备好共享 Microsoft 团队应用程序时，您有三个选项，具体取决于您的目标访问群体。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-134">When you're ready to share your Microsoft Teams apps, you have three options depending on who your target audience is.</span></span>

* <span data-ttu-id="4f5bd-135">**[直接上载您的应用程序](~/concepts/deploy-and-publish/apps-upload.md)** 如果您的应用程序只需要与您的团队或组织中的少数几个人共享您的应用程序，则可以共享您的应用程序包并直接上载它。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-135">**[Upload your app directly](~/concepts/deploy-and-publish/apps-upload.md)** If your app only needs to be shared to your team, or a few individuals in your organization, you can share your app package and upload it directly.</span></span>
* <span data-ttu-id="4f5bd-136">**[发布到你的组织应用程序目录](~/concepts/deploy-and-publish/apps-publish.md)** 您可以通过您的应用程序目录与整个组织共享您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-136">**[Publish to your organizational app catalog](~/concepts/deploy-and-publish/apps-publish.md)** You can share your app with your entire organization through your app catalog.</span></span>
* <span data-ttu-id="4f5bd-137">**[发布到公用应用商店](~/concepts/deploy-and-publish/apps-publish.md)** 如果你的应用程序适用于所有人，你可以将其发布到我们的公共应用商店。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-137">**[Publish to the public app store](~/concepts/deploy-and-publish/apps-publish.md)** If your app is for everyone, you can publish it to our public app store.</span></span> <span data-ttu-id="4f5bd-138">根据你的目标，你可能有资格获取市场营销和销售帮助。</span><span class="sxs-lookup"><span data-stu-id="4f5bd-138">Depending on your goals, you might be eligible for marketing and sales assistance.</span></span>

## <a name="get-started"></a><span data-ttu-id="4f5bd-139">入门</span><span class="sxs-lookup"><span data-stu-id="4f5bd-139">Get started</span></span>

* [<span data-ttu-id="4f5bd-140">在 C 中构建 bot 和选项卡应用#</span><span class="sxs-lookup"><span data-stu-id="4f5bd-140">Build a bot and tab app in C#</span></span>](~/tutorials/get-started-dotnet-app-studio.md)
* [<span data-ttu-id="4f5bd-141">构建 JavaScript/node.js 中的 bot 和选项卡应用程序</span><span class="sxs-lookup"><span data-stu-id="4f5bd-141">Build a bot and tab app in JavaScript/Node.js</span></span>](~/tutorials/get-started-nodejs-app-studio.md)

## <a name="learn-more"></a><span data-ttu-id="4f5bd-142">了解更多</span><span class="sxs-lookup"><span data-stu-id="4f5bd-142">Learn more</span></span>

* [<span data-ttu-id="4f5bd-143">团队客户端中的可扩展性点</span><span class="sxs-lookup"><span data-stu-id="4f5bd-143">Extensibility points in the Teams client</span></span>](~/concepts/extensibility-points.md)
* [<span data-ttu-id="4f5bd-144">构建团队相关应用程序</span><span class="sxs-lookup"><span data-stu-id="4f5bd-144">Building apps for Teams</span></span>](~/concepts/building-an-app.md)
