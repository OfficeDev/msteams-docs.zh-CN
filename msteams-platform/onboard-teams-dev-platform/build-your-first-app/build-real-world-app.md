---
title: 构建你的第一个团队应用
author: heath-hamilton
description: 构建真实 Microsoft 团队应用程序的教程
ms.openlocfilehash: 4915dde4ef5a852f4fc5d1e4c83e3349db2eaf6b
ms.sourcegitcommit: 80bf79a952bb14cbc38c0bd1e3cf8a346158e28e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2020
ms.locfileid: "46655672"
---
# <a name="learn-how-to-build-your-first-teams-app"></a><span data-ttu-id="550f7-103">了解如何构建你的第一个团队应用</span><span class="sxs-lookup"><span data-stu-id="550f7-103">Learn how to build your first Teams app</span></span>

<span data-ttu-id="550f7-104">在 "**构建您的第一个应用程序**" 中，您将了解如何通过教程创建基本的团队应用程序。</span><span class="sxs-lookup"><span data-stu-id="550f7-104">In **Build your first app**, you learn how to create a basic Teams app through tutorials.</span></span> <span data-ttu-id="550f7-105">本课将相互构建，指导您完成创建简单的实际团队应用程序的每个步骤。</span><span class="sxs-lookup"><span data-stu-id="550f7-105">The lessons build on each other, walking you through each step of creating a simple, real-world Teams app.</span></span> <span data-ttu-id="550f7-106">我们将向你介绍常见工具、基本概念以及相关方法的有用链接。</span><span class="sxs-lookup"><span data-stu-id="550f7-106">We introduce you to common tools, fundamental concepts, and useful links along the way.</span></span>

<span data-ttu-id="550f7-107">首先，创建并运行 "Hello，World！"。</span><span class="sxs-lookup"><span data-stu-id="550f7-107">You'll start with creating and running a "Hello, World!"</span></span> <span data-ttu-id="550f7-108">选项卡应用。</span><span class="sxs-lookup"><span data-stu-id="550f7-108">tab app.</span></span> <span data-ttu-id="550f7-109">然后，你将创建一些简单的 UI，并了解如何使用 Microsoft 团队 Javascript SDK 获取有用的上下文。</span><span class="sxs-lookup"><span data-stu-id="550f7-109">You'll then create some simple UI and learn how to get useful context with the Microsoft Teams Javascript SDK.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="550f7-110">你将了解的内容</span><span class="sxs-lookup"><span data-stu-id="550f7-110">What you'll learn</span></span>

> [!div class="checklist"]
  >
  > - <span data-ttu-id="550f7-111">**使用团队工具包快速启动和运行**： Visual Studio 代码的 Microsoft 团队工具包负责创建您的应用程序项目和基架，以便您可以在几分钟内运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="550f7-111">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > - <span data-ttu-id="550f7-112">**使用清单定义您的应用程序**：清单是一个蓝图，可在其中指定团队应用使用的功能和服务。</span><span class="sxs-lookup"><span data-stu-id="550f7-112">**Define your app with the manifest**: The manifest is a blueprint where you specify the capabilities and services your Teams app uses.</span></span>
  > - <span data-ttu-id="550f7-113">**确定访问群体的范围**：您可以构建一个工作组应用程序以供个人使用或协作。</span><span class="sxs-lookup"><span data-stu-id="550f7-113">**Scope your audience**: You can build a Teams app for personal use or collaboration.</span></span> <span data-ttu-id="550f7-114">在教程中，你将了解如何为单个用户或频道或聊天中的一组人员构建一个选项卡。</span><span class="sxs-lookup"><span data-stu-id="550f7-114">In the tutorials, you'll learn how build a tab for individual users or a group of people in a channel or chat.</span></span>
  > - <span data-ttu-id="550f7-115">**利用团队 SDK 获取上下文**：了解如何使用 Microsoft 团队 JavaScript SDK 执行主题更改或设置配置体验</span><span class="sxs-lookup"><span data-stu-id="550f7-115">**Utilize Teams SDK to get context**: Learn how to use the Microsoft Teams JavaScript SDK to perform theme change or set up configuration experience</span></span>  
  > - <span data-ttu-id="550f7-116">**在您的应用程序上展开**：在整个教程中，我们将链接到您可能感兴趣的相关主题 (其中包括身份验证和设计准则) 。</span><span class="sxs-lookup"><span data-stu-id="550f7-116">**Expand on your app**: Throughout the tutorials, we link to related topics you're probably interested in (some of which include authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="550f7-117">团队应用程序基础</span><span class="sxs-lookup"><span data-stu-id="550f7-117">Teams app fundamentals</span></span>

<span data-ttu-id="550f7-118">在开始教程之前，您应该了解以下有关为团队生成应用程序的信息。</span><span class="sxs-lookup"><span data-stu-id="550f7-118">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities"></a><span data-ttu-id="550f7-119">应用可以有多种功能</span><span class="sxs-lookup"><span data-stu-id="550f7-119">Apps can have multiple capabilities</span></span>

<span data-ttu-id="550f7-120">团队应用程序由一个或多个[平台功能](../capabilities-overview.md)组成，包括[选项卡](../doc-links/what-are-tabs.md)、 [bot](../doc-links/what-are-bots.md )、[邮件扩展](../doc-links/what-are-messaging-extensions.md)和[webhook 和连接器](../doc-links/what-are-webhooks-and-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="550f7-120">Teams apps are made up of one or more [platform capabilities](../capabilities-overview.md), including [tabs](../doc-links/what-are-tabs.md), [bots](../doc-links/what-are-bots.md ), [messaging extensions](../doc-links/what-are-messaging-extensions.md), and [webhooks and connectors](../doc-links/what-are-webhooks-and-connectors.md).</span></span> <span data-ttu-id="550f7-121">团队应用程序还具有许多[UI 约定和元素](../doc-links/teams-ui-conventions.md)（如卡片、任务模块和深层链接），您可以使用它们生成最佳的用户体验。</span><span class="sxs-lookup"><span data-stu-id="550f7-121">Teams apps also have many [UI conventions and elements](../doc-links/teams-ui-conventions.md), such as cards, task modules, and deep linking, you can use to build the best possible user experience.</span></span>

<span data-ttu-id="550f7-122">对于这些教程，你将仅构建选项卡，但可以根据需要将机器人或其他功能添加到你的应用。</span><span class="sxs-lookup"><span data-stu-id="550f7-122">For these tutorials, you'll build only tabs but can add a bot or other capability to your app as you like.</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="550f7-123">团队不会托管您的应用程序</span><span class="sxs-lookup"><span data-stu-id="550f7-123">Teams doesn't host your app</span></span>  

<span data-ttu-id="550f7-124">团队应用程序包含三个主要部分：</span><span class="sxs-lookup"><span data-stu-id="550f7-124">A Teams app consists of three major pieces:</span></span>

1. <span data-ttu-id="550f7-125">Microsoft 团队客户端 (web、桌面或移动) ，用户与您的应用程序进行交互。</span><span class="sxs-lookup"><span data-stu-id="550f7-125">The Microsoft Teams client (web, desktop, or mobile) where users interact with your app.</span></span>
1. <span data-ttu-id="550f7-126">执行必要的逻辑、数据存储和 API 调用以对应用程序供电的应用程序、服务、工作流或网站。</span><span class="sxs-lookup"><span data-stu-id="550f7-126">Your app, service, workflow, or website that performs the necessary logic, data storage, and API calls to power your app.</span></span>
1. <span data-ttu-id="550f7-127">您的应用程序包，可用于在团队中安装应用程序。</span><span class="sxs-lookup"><span data-stu-id="550f7-127">Your app package, which you use to install the app in Teams.</span></span> <span data-ttu-id="550f7-128">它包含应用程序元数据 (名称、图标等，以及指向服务的 ) 和指针。</span><span class="sxs-lookup"><span data-stu-id="550f7-128">It contains app metadata (name, icons, etc.) and pointers to your services.</span></span>

## <a name="next-step"></a><span data-ttu-id="550f7-129">后续步骤</span><span class="sxs-lookup"><span data-stu-id="550f7-129">Next step</span></span>

<span data-ttu-id="550f7-130">这就是我们现在开始的一切吧！</span><span class="sxs-lookup"><span data-stu-id="550f7-130">That's all for now, let's get started!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="550f7-131">生成并运行您的第一个应用程序</span><span class="sxs-lookup"><span data-stu-id="550f7-131">Build and run your first app</span></span>](build-and-run-with-toolkit.md)
