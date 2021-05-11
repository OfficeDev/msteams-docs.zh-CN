---
title: 入门 - 生成首个应用概述和先决条件
author: girliemac
description: 了解如何开始使用应用Microsoft Teams和设置环境。
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
# <a name="get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="28e26-103">开始Microsoft Teams开发</span><span class="sxs-lookup"><span data-stu-id="28e26-103">Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="28e26-104">生成一个简单的应用，了解Teams应用的基础知识。</span><span class="sxs-lookup"><span data-stu-id="28e26-104">Build a simple app to learn the basics of Teams app development.</span></span> <span data-ttu-id="28e26-105">一旦看到"Hello， World！"，请尝试阅读任何其他入门文章，详细了解常见工具、基本概念和高级功能。</span><span class="sxs-lookup"><span data-stu-id="28e26-105">Once you see "Hello, World!", try any of the other get started articles for more information on common tools, fundamental concepts, and advanced features.</span></span>



## <a name="what-youll-learn"></a><span data-ttu-id="28e26-106">您将了解哪些功能</span><span class="sxs-lookup"><span data-stu-id="28e26-106">What you'll learn</span></span>

* <span data-ttu-id="28e26-107">快速启动并运行 Teams Toolkit 扩展Visual Studio Code扩展</span><span class="sxs-lookup"><span data-stu-id="28e26-107">Get up and running quickly with the Teams Toolkit, a Visual Studio Code extension</span></span> 
* <span data-ttu-id="28e26-108">使用 App Studio 配置应用</span><span class="sxs-lookup"><span data-stu-id="28e26-108">Configure your app with App Studio</span></span> 
* <span data-ttu-id="28e26-109">熟悉开发人员Teams SDK</span><span class="sxs-lookup"><span data-stu-id="28e26-109">Get familiar with Teams developer tools and SDKs</span></span>
* <span data-ttu-id="28e26-110">考虑Teams概念，如身份验证和设计最佳做法</span><span class="sxs-lookup"><span data-stu-id="28e26-110">Consider important Teams app concepts, such as authentication and design best practices</span></span>

<span data-ttu-id="28e26-111">可以使用你Teams的任何技术来构建应用，例如，使用 CLI (命令行) 。</span><span class="sxs-lookup"><span data-stu-id="28e26-111">You can build Teams app using any technology of your choice, for example, command-line interface (CLI).</span></span> <span data-ttu-id="28e26-112">但是，这些文章可帮助你开始使用以下推荐的工具和技术：</span><span class="sxs-lookup"><span data-stu-id="28e26-112">But, these articles help you get started with the following recommended tools and technologies:</span></span>

* <span data-ttu-id="28e26-113">Teams Toolkit，Visual Studio Code扩展</span><span class="sxs-lookup"><span data-stu-id="28e26-113">Teams Toolkit, a Visual Studio Code extension</span></span>
* <span data-ttu-id="28e26-114">React.js选项卡</span><span class="sxs-lookup"><span data-stu-id="28e26-114">React.js for tabs</span></span>
* <span data-ttu-id="28e26-115">Node.js聊天机器人和消息扩展的扩展</span><span class="sxs-lookup"><span data-stu-id="28e26-115">Node.js for bots and messaging extensions</span></span>


## <a name="teams-app-fundamentals"></a><span data-ttu-id="28e26-116">Teams应用基础</span><span class="sxs-lookup"><span data-stu-id="28e26-116">Teams app fundamentals</span></span>

<span data-ttu-id="28e26-117">你可以为你自己Teams组织中的人员或世界各地人构建自定义应用。</span><span class="sxs-lookup"><span data-stu-id="28e26-117">You can build custom Teams apps for yourself, people in your org, or people all over the world.</span></span> <span data-ttu-id="28e26-118">在开始之前，你应该了解以下有关应用开发Teams概念：</span><span class="sxs-lookup"><span data-stu-id="28e26-118">Before you begin, you should understand the following fundamental concepts about Teams app development:</span></span>

### <a name="common-app-use-cases"></a><span data-ttu-id="28e26-119">常见应用用例</span><span class="sxs-lookup"><span data-stu-id="28e26-119">Common app use cases</span></span>

<span data-ttu-id="28e26-120">自定义应用可以使用的Teams一些典型方案包括：</span><span class="sxs-lookup"><span data-stu-id="28e26-120">Some typical scenarios that a custom Teams app can help with are:</span></span>

* <span data-ttu-id="28e26-121">在客户端中嵌入基于 Web 的内容，如 Web 应用或Teams部分</span><span class="sxs-lookup"><span data-stu-id="28e26-121">Embed web-based content, such as a web app or part of a website, in the Teams client</span></span>
* <span data-ttu-id="28e26-122">在另一个系统中快速查找信息并添加到Teams对话</span><span class="sxs-lookup"><span data-stu-id="28e26-122">Look up information quickly in another system and adding it to a Teams conversation</span></span> 
* <span data-ttu-id="28e26-123">直接从对话中的内容触发工作流和进程</span><span class="sxs-lookup"><span data-stu-id="28e26-123">Trigger workflows and processes directly from what's said in a conversation</span></span> 

### <a name="app-capabilities-and-tools"></a><span data-ttu-id="28e26-124">应用功能和工具</span><span class="sxs-lookup"><span data-stu-id="28e26-124">App capabilities and tools</span></span>

<span data-ttu-id="28e26-125">应用由一个或多个Teams和用户交互点。</span><span class="sxs-lookup"><span data-stu-id="28e26-125">An app is made up of one or more Teams capabilities and user interaction points.</span></span> <span data-ttu-id="28e26-126">你的开发工具集将因所需的功能而异。</span><span class="sxs-lookup"><span data-stu-id="28e26-126">Your development toolset will vary depending on the capabilities you want.</span></span>

| <span data-ttu-id="28e26-127">**应用功能**</span><span class="sxs-lookup"><span data-stu-id="28e26-127">**App capabilities**</span></span>| <span data-ttu-id="28e26-128">**交互点**</span><span class="sxs-lookup"><span data-stu-id="28e26-128">**Interaction points**</span></span> | <span data-ttu-id="28e26-129">**推荐的工具**</span><span class="sxs-lookup"><span data-stu-id="28e26-129">**Recommended tools**</span></span> | <span data-ttu-id="28e26-130">**SDK**</span><span class="sxs-lookup"><span data-stu-id="28e26-130">**SDKs**</span></span> | <span data-ttu-id="28e26-131">**技术堆栈**</span><span class="sxs-lookup"><span data-stu-id="28e26-131">**Technology stacks**</span></span> |
|--------|--------|--------|--------|--------|
| <span data-ttu-id="28e26-132">选项卡</span><span class="sxs-lookup"><span data-stu-id="28e26-132">Tabs</span></span> | <span data-ttu-id="28e26-133">用户可在个人上下文和共享上下文中与嵌入的 Web 内容交互的空间</span><span class="sxs-lookup"><span data-stu-id="28e26-133">Spaces where users can interact with embedded web content in personal and shared contexts</span></span> | <span data-ttu-id="28e26-134">VS Code扩展Teams Toolkit Yeoman 生成器</span><span class="sxs-lookup"><span data-stu-id="28e26-134">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="28e26-135">团队 JavaScript 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="28e26-135">Teams JavaScript client SDK</span></span> | <span data-ttu-id="28e26-136">常规 Web 技术 (HTML、CSS 和 JavaScript) 或 React.js</span><span class="sxs-lookup"><span data-stu-id="28e26-136">General web technologies (HTML, CSS, and JavaScript) or React.js</span></span> |
| <span data-ttu-id="28e26-137">机器人</span><span class="sxs-lookup"><span data-stu-id="28e26-137">Bots</span></span> | <span data-ttu-id="28e26-138">在个人上下文和共享上下文中与用户交互的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="28e26-138">Chatbots that interact with users in personal and shared contexts</span></span> | <span data-ttu-id="28e26-139">VS Code扩展Teams Toolkit Yeoman 生成器</span><span class="sxs-lookup"><span data-stu-id="28e26-139">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="28e26-140">Bot Franework SDK</span><span class="sxs-lookup"><span data-stu-id="28e26-140">Bot Franework SDK</span></span> | <span data-ttu-id="28e26-141">Node.js、C# 或 Python</span><span class="sxs-lookup"><span data-stu-id="28e26-141">Node.js, C#, or Python</span></span> | 
| <span data-ttu-id="28e26-142">消息扩展</span><span class="sxs-lookup"><span data-stu-id="28e26-142">Messaging extensions</span></span> | <span data-ttu-id="28e26-143">插入应用内容或处理邮件而不离开对话的快捷方式</span><span class="sxs-lookup"><span data-stu-id="28e26-143">Shortcuts for inserting app content or acting on a message without navigating away from the conversation</span></span> | <span data-ttu-id="28e26-144">VS Code扩展Teams Toolkit Yeoman 生成器</span><span class="sxs-lookup"><span data-stu-id="28e26-144">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="28e26-145">Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="28e26-145">Bot Framework SDK</span></span> | <span data-ttu-id="28e26-146">Node.js、C# 或 Python</span><span class="sxs-lookup"><span data-stu-id="28e26-146">Node.js, C#, or Python</span></span> |

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="28e26-147">Teams不托管应用</span><span class="sxs-lookup"><span data-stu-id="28e26-147">Teams doesn't host your app</span></span>

<span data-ttu-id="28e26-148">当用户在 Teams 中安装你的应用时，他们只会安装一个包含配置文件 (也称为应用清单) 和应用的图标的应用包。</span><span class="sxs-lookup"><span data-stu-id="28e26-148">When a user installs your app in Teams, they only install an app package that contains a configuration file (also known as an app manifest) and your app’s icons.</span></span> <span data-ttu-id="28e26-149">应用的逻辑和数据存储托管在其他地方，如开发期间 Azure Web 服务或 localhost。</span><span class="sxs-lookup"><span data-stu-id="28e26-149">Your app’s logic and data storage are hosted elsewhere, such as Azure Web Services or localhost during development.</span></span> <span data-ttu-id="28e26-150">Teams HTTPS 访问这些资源。</span><span class="sxs-lookup"><span data-stu-id="28e26-150">Teams accesses these resources via HTTPS.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="插图显示应用Teams指向云服务器中的应用逻辑。":::

## <a name="next-step"></a><span data-ttu-id="28e26-152">后续步骤</span><span class="sxs-lookup"><span data-stu-id="28e26-152">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="28e26-153">生成并运行你的第一个Teams应用</span><span class="sxs-lookup"><span data-stu-id="28e26-153">Build and run your first Teams app</span></span>](../build-your-first-app/build-and-run.md)
