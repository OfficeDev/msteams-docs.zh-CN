---
title: 入门 - 生成首个应用概述和先决条件
author: girliemac
description: 了解如何开始使用 Microsoft Teams 应用开发和设置环境。
ms.author: timura
ms.date: 03/18/2021
ms.topic: quickstart
ms.openlocfilehash: 3bc99c535ea659f046b65dc26d9a60de0dd49cab
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068563"
---
# <a name="get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="b050f-103">Microsoft Teams 应用开发入门</span><span class="sxs-lookup"><span data-stu-id="b050f-103">Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="b050f-104">生成一个简单的应用，了解 Teams 应用开发的基本知识。</span><span class="sxs-lookup"><span data-stu-id="b050f-104">Build a simple app to learn the basics of Teams app development.</span></span> <span data-ttu-id="b050f-105">一旦看到"Hello， World！"，请尝试阅读任何其他入门文章，详细了解常见工具、基本概念和高级功能。</span><span class="sxs-lookup"><span data-stu-id="b050f-105">Once you see "Hello, World!", try any of the other get started articles for more information on common tools, fundamental concepts, and advanced features.</span></span>



## <a name="what-youll-learn"></a><span data-ttu-id="b050f-106">您将了解哪些功能</span><span class="sxs-lookup"><span data-stu-id="b050f-106">What you'll learn</span></span>

* <span data-ttu-id="b050f-107">快速启动并运行 Teams Toolkit（Visual Studio代码扩展）</span><span class="sxs-lookup"><span data-stu-id="b050f-107">Get up and running quickly with the Teams Toolkit, a Visual Studio Code extension</span></span> 
* <span data-ttu-id="b050f-108">使用 App Studio 配置应用</span><span class="sxs-lookup"><span data-stu-id="b050f-108">Configure your app with App Studio</span></span> 
* <span data-ttu-id="b050f-109">熟悉 Teams 开发人员工具和 SDK</span><span class="sxs-lookup"><span data-stu-id="b050f-109">Get familiar with Teams developer tools and SDKs</span></span>
* <span data-ttu-id="b050f-110">考虑重要的 Teams 应用概念，例如身份验证和设计最佳做法</span><span class="sxs-lookup"><span data-stu-id="b050f-110">Consider important Teams app concepts, such as authentication and design best practices</span></span>

<span data-ttu-id="b050f-111">可以使用你选择的任何技术生成 Teams 应用，例如，使用 CLI (命令行) 。</span><span class="sxs-lookup"><span data-stu-id="b050f-111">You can build Teams app using any technology of your choice, for example, command-line interface (CLI).</span></span> <span data-ttu-id="b050f-112">但是，这些文章可帮助你开始使用以下推荐的工具和技术：</span><span class="sxs-lookup"><span data-stu-id="b050f-112">But, these articles help you get started with the following recommended tools and technologies:</span></span>

* <span data-ttu-id="b050f-113">Teams Toolkit，Visual Studio代码扩展</span><span class="sxs-lookup"><span data-stu-id="b050f-113">Teams Toolkit, a Visual Studio Code extension</span></span>
* <span data-ttu-id="b050f-114">React.js选项卡</span><span class="sxs-lookup"><span data-stu-id="b050f-114">React.js for tabs</span></span>
* <span data-ttu-id="b050f-115">Node.js聊天机器人和消息扩展的扩展</span><span class="sxs-lookup"><span data-stu-id="b050f-115">Node.js for bots and messaging extensions</span></span>


## <a name="teams-app-fundamentals"></a><span data-ttu-id="b050f-116">Teams 应用基础</span><span class="sxs-lookup"><span data-stu-id="b050f-116">Teams app fundamentals</span></span>

<span data-ttu-id="b050f-117">你可以为自己、组织中的人员或世界各地用户生成自定义 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="b050f-117">You can build custom Teams apps for yourself, people in your org, or people all over the world.</span></span> <span data-ttu-id="b050f-118">在开始之前，你应该了解以下有关 Teams 应用开发的基本概念：</span><span class="sxs-lookup"><span data-stu-id="b050f-118">Before you begin, you should understand the following fundamental concepts about Teams app development:</span></span>

### <a name="common-app-use-cases"></a><span data-ttu-id="b050f-119">常见应用用例</span><span class="sxs-lookup"><span data-stu-id="b050f-119">Common app use cases</span></span>

<span data-ttu-id="b050f-120">自定义 Teams 应用可帮助的一些典型方案包括：</span><span class="sxs-lookup"><span data-stu-id="b050f-120">Some typical scenarios that a custom Teams app can help with are:</span></span>

* <span data-ttu-id="b050f-121">在 Teams 客户端中嵌入基于 Web 的内容，如 Web 应用或网站的一部分</span><span class="sxs-lookup"><span data-stu-id="b050f-121">Embed web-based content, such as a web app or part of a website, in the Teams client</span></span>
* <span data-ttu-id="b050f-122">在另一个系统中快速查找信息并添加到 Teams 对话</span><span class="sxs-lookup"><span data-stu-id="b050f-122">Look up information quickly in another system and adding it to a Teams conversation</span></span> 
* <span data-ttu-id="b050f-123">直接从对话中的内容触发工作流和进程</span><span class="sxs-lookup"><span data-stu-id="b050f-123">Trigger workflows and processes directly from what's said in a conversation</span></span> 

### <a name="app-capabilities-and-tools"></a><span data-ttu-id="b050f-124">应用功能和工具</span><span class="sxs-lookup"><span data-stu-id="b050f-124">App capabilities and tools</span></span>

<span data-ttu-id="b050f-125">应用由一个或多个 Teams 功能和用户交互点决定。</span><span class="sxs-lookup"><span data-stu-id="b050f-125">An app is made up of one or more Teams capabilities and user interaction points.</span></span> <span data-ttu-id="b050f-126">你的开发工具集将因所需的功能而异。</span><span class="sxs-lookup"><span data-stu-id="b050f-126">Your development toolset will vary depending on the capabilities you want.</span></span>

| <span data-ttu-id="b050f-127">**应用功能**</span><span class="sxs-lookup"><span data-stu-id="b050f-127">**App capabilities**</span></span>| <span data-ttu-id="b050f-128">**交互点**</span><span class="sxs-lookup"><span data-stu-id="b050f-128">**Interaction points**</span></span> | <span data-ttu-id="b050f-129">**推荐的工具**</span><span class="sxs-lookup"><span data-stu-id="b050f-129">**Recommended tools**</span></span> | <span data-ttu-id="b050f-130">**SDK**</span><span class="sxs-lookup"><span data-stu-id="b050f-130">**SDKs**</span></span> | <span data-ttu-id="b050f-131">**技术堆栈**</span><span class="sxs-lookup"><span data-stu-id="b050f-131">**Technology stacks**</span></span> |
|--------|--------|--------|--------|--------|
| <span data-ttu-id="b050f-132">选项卡</span><span class="sxs-lookup"><span data-stu-id="b050f-132">Tabs</span></span> | <span data-ttu-id="b050f-133">用户可在个人上下文和共享上下文中与嵌入的 Web 内容交互的空间</span><span class="sxs-lookup"><span data-stu-id="b050f-133">Spaces where users can interact with embedded web content in personal and shared contexts</span></span> | <span data-ttu-id="b050f-134">使用 Teams 扩展或 Yeoman Toolkit VS 代码</span><span class="sxs-lookup"><span data-stu-id="b050f-134">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="b050f-135">团队 JavaScript 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="b050f-135">Teams JavaScript client SDK</span></span> | <span data-ttu-id="b050f-136">常规 Web 技术 (HTML、CSS 和 JavaScript) 或 React.js</span><span class="sxs-lookup"><span data-stu-id="b050f-136">General web technologies (HTML, CSS, and JavaScript) or React.js</span></span> |
| <span data-ttu-id="b050f-137">机器人</span><span class="sxs-lookup"><span data-stu-id="b050f-137">Bots</span></span> | <span data-ttu-id="b050f-138">在个人上下文和共享上下文中与用户交互的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="b050f-138">Chatbots that interact with users in personal and shared contexts</span></span> | <span data-ttu-id="b050f-139">使用 Teams 扩展或 Yeoman Toolkit VS 代码</span><span class="sxs-lookup"><span data-stu-id="b050f-139">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="b050f-140">Bot Franework SDK</span><span class="sxs-lookup"><span data-stu-id="b050f-140">Bot Franework SDK</span></span> | <span data-ttu-id="b050f-141">Node.js、C# 或 Python</span><span class="sxs-lookup"><span data-stu-id="b050f-141">Node.js, C#, or Python</span></span> | 
| <span data-ttu-id="b050f-142">消息扩展</span><span class="sxs-lookup"><span data-stu-id="b050f-142">Messaging extensions</span></span> | <span data-ttu-id="b050f-143">插入应用内容或处理邮件而不离开对话的快捷方式</span><span class="sxs-lookup"><span data-stu-id="b050f-143">Shortcuts for inserting app content or acting on a message without navigating away from the conversation</span></span> | <span data-ttu-id="b050f-144">使用 Teams 扩展或 Yeoman Toolkit VS 代码</span><span class="sxs-lookup"><span data-stu-id="b050f-144">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="b050f-145">Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="b050f-145">Bot Framework SDK</span></span> | <span data-ttu-id="b050f-146">Node.js、C# 或 Python</span><span class="sxs-lookup"><span data-stu-id="b050f-146">Node.js, C#, or Python</span></span> |

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="b050f-147">Teams 不托管你的应用</span><span class="sxs-lookup"><span data-stu-id="b050f-147">Teams doesn't host your app</span></span>

<span data-ttu-id="b050f-148">当用户在 Teams 中安装你的应用时，他们仅安装包含配置文件 (也称为应用清单) 应用图标的应用包。</span><span class="sxs-lookup"><span data-stu-id="b050f-148">When a user installs your app in Teams, they only install an app package that contains a configuration file (also known as an app manifest) and your app’s icons.</span></span> <span data-ttu-id="b050f-149">应用的逻辑和数据存储托管在其他地方，如开发期间 Azure Web 服务或 localhost。</span><span class="sxs-lookup"><span data-stu-id="b050f-149">Your app’s logic and data storage are hosted elsewhere, such as Azure Web Services or localhost during development.</span></span> <span data-ttu-id="b050f-150">Teams 通过 HTTPS 访问这些资源。</span><span class="sxs-lookup"><span data-stu-id="b050f-150">Teams accesses these resources via HTTPS.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="插图显示 Teams 上的应用指向云服务器中的应用逻辑。":::

## <a name="next-step"></a><span data-ttu-id="b050f-152">后续步骤</span><span class="sxs-lookup"><span data-stu-id="b050f-152">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b050f-153">生成并运行你的第一个 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="b050f-153">Build and run your first Teams app</span></span>](../build-your-first-app/build-and-run.md)
