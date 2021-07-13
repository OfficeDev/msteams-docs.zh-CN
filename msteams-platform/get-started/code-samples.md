---
title: 应用代码示例
description: 适用于开发人员平台的示例应用程序Microsoft Teams和说明
localization_priority: Normal
ms.topic: reference
keywords: Microsoft Teams开发人员示例
ms.openlocfilehash: 09369123f23fc76b5e8c9fe3d5e89df56763d21f
ms.sourcegitcommit: 10380fc80d7f281d2892b3514f87d1bd05180496
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2021
ms.locfileid: "53373912"
---
# <a name="overview"></a><span data-ttu-id="8787d-104">概述</span><span class="sxs-lookup"><span data-stu-id="8787d-104">Overview</span></span>

<span data-ttu-id="8787d-105">本教程介绍如何使用 React、Blazor、SPFx、C# 或 .NET、Node.js 和 Yeoman 生成器创建应用。</span><span class="sxs-lookup"><span data-stu-id="8787d-105">In this tutorial, you will learn how to create an app using React, Blazor, SPFx, C# or .NET, Node.js, and Yeoman Generator.</span></span> <span data-ttu-id="8787d-106">你还将了解如何创建你的第一个机器人和消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="8787d-106">You will also learn to create your first bot and messaging extension.</span></span> <span data-ttu-id="8787d-107">本教程将指导你完成选项卡、聊天机器人、消息传递扩展、Webhook 和连接器以及 Graph API 的多个代码示例，帮助你自定义和配置应用。</span><span class="sxs-lookup"><span data-stu-id="8787d-107">This tutorial will take you through multiple Code Samples for Tabs, Bots, Messaging Extensions, Webhooks and Connectors, and Graph APIs that will help you to customize and configure your apps.</span></span> <span data-ttu-id="8787d-108">此外，还可以参阅 Microsoft Learn 部分，通过创建自定义应用Teams开发人员平台功能。</span><span class="sxs-lookup"><span data-stu-id="8787d-108">In addition, you can also refer to the Microsoft Learn sections where you can extend the Teams developer platform capabilities by creating custom apps.</span></span>  

## <a name="getting-started-with-microsoft-learn"></a><span data-ttu-id="8787d-109">Microsoft Learn 入门</span><span class="sxs-lookup"><span data-stu-id="8787d-109">Getting started with Microsoft Learn</span></span>

| <span data-ttu-id="8787d-110">**功能**</span><span class="sxs-lookup"><span data-stu-id="8787d-110">**Capability**</span></span>| <span data-ttu-id="8787d-111">**学习模块**</span><span class="sxs-lookup"><span data-stu-id="8787d-111">**Learn module**</span></span>|
|--------|-------------|
| <span data-ttu-id="8787d-112">选项卡 — 嵌入式 Web 体验</span><span class="sxs-lookup"><span data-stu-id="8787d-112">Tabs  — embedded web experiences</span></span>  |  [<span data-ttu-id="8787d-113">为 Microsoft Teams 创建嵌入式 Web 体验（选项卡）</span><span class="sxs-lookup"><span data-stu-id="8787d-113">Create embedded web experiences with tabs for Microsoft Teams</span></span>](/learn/modules/embedded-web-experiences/) |
| <span data-ttu-id="8787d-114">Webhook 和连接器</span><span class="sxs-lookup"><span data-stu-id="8787d-114">Webhooks and connectors</span></span>  |  [<span data-ttu-id="8787d-115">使用 Webhook 和 Office 365 连接器将 Web 服务连接到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8787d-115">Connect web services to Microsoft Teams with webhooks and Office 365 Connectors</span></span>](/learn/modules/msteams-webhooks-connectors/) |
|<span data-ttu-id="8787d-116">消息扩展</span><span class="sxs-lookup"><span data-stu-id="8787d-116">Messaging extensions</span></span>  | [<span data-ttu-id="8787d-117">通过消息传递扩展在 Microsoft Teams 中进行以任务为导向的交互</span><span class="sxs-lookup"><span data-stu-id="8787d-117">Task-oriented interactions in Microsoft Teams with messaging extensions</span></span>](/learn/modules/msteams-messaging-extensions/)  |
| <span data-ttu-id="8787d-118">任务模块</span><span class="sxs-lookup"><span data-stu-id="8787d-118">Task modules</span></span> |  [<span data-ttu-id="8787d-119">使用任务Microsoft Teams中收集输入</span><span class="sxs-lookup"><span data-stu-id="8787d-119">Collect input in Microsoft Teams with Task Modules</span></span>](/learn/modules/msteams-task-modules/) |
| <span data-ttu-id="8787d-120">对话机器人</span><span class="sxs-lookup"><span data-stu-id="8787d-120">Conversational bots</span></span>  | [<span data-ttu-id="8787d-121">为 Microsoft Teams 创建交互式对话机器人</span><span class="sxs-lookup"><span data-stu-id="8787d-121">Create interactive conversational bots for Microsoft Teams</span></span>](/learn/modules/msteams-conversation-bots/)  |

## <a name="build-your-first-microsoft-teams-app-overview"></a><span data-ttu-id="8787d-122">生成首个Microsoft Teams应用概述</span><span class="sxs-lookup"><span data-stu-id="8787d-122">Build your first Microsoft Teams app overview</span></span>

<span data-ttu-id="8787d-123">在 **入门课程** 中，你将了解如何创建基本Teams应用。</span><span class="sxs-lookup"><span data-stu-id="8787d-123">In the **get started** lessons, you learn how to create basic Teams apps.</span></span> <span data-ttu-id="8787d-124">每个教程将介绍如何生成简单的实际 Teams 应用，同时向用户介绍通用工具、基本概念和更高级的功能。</span><span class="sxs-lookup"><span data-stu-id="8787d-124">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

### <a name="teams-app-fundamentals"></a><span data-ttu-id="8787d-125">Teams应用基础</span><span class="sxs-lookup"><span data-stu-id="8787d-125">Teams app fundamentals</span></span>

<span data-ttu-id="8787d-126">开发人员[Teams允许你](../overview.md)生成自定义应用。</span><span class="sxs-lookup"><span data-stu-id="8787d-126">The [Teams developer platform](../overview.md) lets you build custom apps.</span></span> <span data-ttu-id="8787d-127">自定义 Microsoft Teams 应用可以帮助解决以下常见情况：</span><span class="sxs-lookup"><span data-stu-id="8787d-127">Some common scenarios that a custom Microsoft Teams app can help with are:</span></span>

* <span data-ttu-id="8787d-128">在 Teams 客户端中直接嵌入网站或 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="8787d-128">Embed your website or web app directly in the Teams client.</span></span>
* <span data-ttu-id="8787d-129">帮助用户快速查找另一个系统中的信息，将结果添加到 Teams。</span><span class="sxs-lookup"><span data-stu-id="8787d-129">Help users quickly look up information in another system and add the results to a conversation in Teams.</span></span>
* <span data-ttu-id="8787d-130">触发基于 Teams 中对话的工作流和流程，保留对话上下文。</span><span class="sxs-lookup"><span data-stu-id="8787d-130">Trigger workflows and processes based on a conversation in Teams, preserving the context of the conversation.</span></span>

<span data-ttu-id="8787d-131">在开始教程之前，你应了解以下内容，以生成适用于Teams。</span><span class="sxs-lookup"><span data-stu-id="8787d-131">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="app-capabilities"></a><span data-ttu-id="8787d-132">应用功能</span><span class="sxs-lookup"><span data-stu-id="8787d-132">App capabilities</span></span>

<span data-ttu-id="8787d-133">A Teams app is made up of one or more [platform capabilities](../concepts/capabilities-overview.md) and [user interaction points](../concepts/extensibility-points.md).</span><span class="sxs-lookup"><span data-stu-id="8787d-133">A Teams app is made up of one or more [platform capabilities](../concepts/capabilities-overview.md) and [user interaction points](../concepts/extensibility-points.md).</span></span>

<span data-ttu-id="8787d-134">根据应用所需的功能，你将需要相应的开发工具集。</span><span class="sxs-lookup"><span data-stu-id="8787d-134">Depending on what capabilities you want for your app, you will need an appropriate development toolset.</span></span>

<span data-ttu-id="8787d-135">|应用功能|用户交互|推荐的工具|SDK |技术堆栈| |--------|-------------||--------||--------||--------| |选项卡|全屏嵌入式 Web 体验。</span><span class="sxs-lookup"><span data-stu-id="8787d-135">| App capabilities | User interactions | Recommended tools | SDKs | Technology stacks | |--------|-------------||--------||--------||--------| | Tabs | A full-screen embedded web experience.</span></span> <span data-ttu-id="8787d-136">|VS Code扩展Teams Toolkit或 YoTeams (Yeoman Generator) |[Teams客户端 SDK](/javascript/api/overview/msteams-client) |通常，HTML、CSS 和 JavaScript | |自动程序|与成员对话的聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="8787d-136">| VS Code with Teams Toolkit extension, or YoTeams (Yeoman Generator) | [Teams client SDK](/javascript/api/overview/msteams-client) | Web technology in general, HTML, CSS, and JavaScript | | Bots | A chat bot that converses with members.</span></span> <span data-ttu-id="8787d-137">|VS Code扩展Teams Toolkit或 YoTeams (Yeoman Generator) |[Bot Framework SDK](https://dev.botframework.com/) |Node.js、C# 或 Python | |邮件扩展|用于将外部内容插入对话或对邮件采取措施的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="8787d-137">| VS Code with Teams Toolkit extension, or YoTeams (Yeoman Generator) | [Bot Framework SDK](https://dev.botframework.com/) | Node.js, C#, or Python | | Messaging extensions | Shortcuts for inserting external content into a conversation or taking action on messages.</span></span> <span data-ttu-id="8787d-138">|VS Code扩展Teams Toolkit或 YoTeams (Yeoman Generator) |[Bot Framework SDK](https://dev.botframework.com/) |Node.js、C# 或 Python |</span><span class="sxs-lookup"><span data-stu-id="8787d-138">| VS Code with Teams Toolkit extension, or YoTeams (Yeoman Generator) | [Bot Framework SDK](https://dev.botframework.com/) | Node.js, C#, or Python |</span></span>

<span data-ttu-id="8787d-139">入门部分将介绍推荐的工具集和常用技术，例如 Visual Studio Code 和 Teams 扩展、React.js（适用于选项卡）和 Node.js（适用于机器人和消息传递扩展，尽管不限于使用这些特定 *堆栈）。*</span><span class="sxs-lookup"><span data-stu-id="8787d-139">The Get started section will take you through recommended tool sets and commonly used technologies, such as Visual Studio Code with Teams extension, React.js for tabs, and Node.js for bots and messaging extensions, although *you are not limited to using these particular stacks*.</span></span>

<span data-ttu-id="8787d-140">如果你更喜欢使用命令行界面和 CLI (CLI) ，请参阅使用[Yeoman](../get-started/get-started-yeoman.md)Microsoft Teams创建你的第一个 Microsoft Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="8787d-140">If you prefer using a command-line interface (CLI), see [create your first Microsoft Teams app using the Yeoman generator](../get-started/get-started-yeoman.md).</span></span>

### <a name="teams-does-not-host-your-app"></a><span data-ttu-id="8787d-141">Teams托管你的应用</span><span class="sxs-lookup"><span data-stu-id="8787d-141">Teams does not host your app</span></span>

<span data-ttu-id="8787d-142">你将仅将包含配置文件（称为清单和应用图标）的应用包安装到Teams客户端。</span><span class="sxs-lookup"><span data-stu-id="8787d-142">You will only install an app package that contains a configuration file, called manifest and app icons to Teams client.</span></span> <span data-ttu-id="8787d-143">其余的应用逻辑和数据存储托管在其他地方，如 Azure Web 服务。</span><span class="sxs-lookup"><span data-stu-id="8787d-143">The rest of the app logics and data storage are hosted elsewhere, such as Azure Web Services.</span></span> <span data-ttu-id="8787d-144">在开发过程中，云或 localhost 中的应用通过 HTTPS Teams访问。</span><span class="sxs-lookup"><span data-stu-id="8787d-144">Your app in the cloud or localhost during your development accesses Teams via HTTPS.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="插图显示应用Teams指向云服务器中的应用逻辑。":::

## <a name="see-also"></a><span data-ttu-id="8787d-146">另请参阅</span><span class="sxs-lookup"><span data-stu-id="8787d-146">See also</span></span>

* [<span data-ttu-id="8787d-147">使用应用程序创建React</span><span class="sxs-lookup"><span data-stu-id="8787d-147">Create an app using React</span></span>](first-app-react.md)
* [<span data-ttu-id="8787d-148">使用 Blazor 创建应用</span><span class="sxs-lookup"><span data-stu-id="8787d-148">Create an app using Blazor</span></span>](first-app-blazor.md)
* [<span data-ttu-id="8787d-149">使用应用程序创建SPFx</span><span class="sxs-lookup"><span data-stu-id="8787d-149">Create an app using SPFx</span></span>](first-app-spfx.md)
* [<span data-ttu-id="8787d-150">使用或 C# .NET 创建应用</span><span class="sxs-lookup"><span data-stu-id="8787d-150">Create an app using C# or .NET</span></span>](get-started-dotnet-app-studio.md)
* [<span data-ttu-id="8787d-151">使用Node.js创建应用</span><span class="sxs-lookup"><span data-stu-id="8787d-151">Create an app using Node.js</span></span>](get-started-nodejs-app-studio.md)
* [<span data-ttu-id="8787d-152">使用 Yeoman 生成器创建应用</span><span class="sxs-lookup"><span data-stu-id="8787d-152">Create an app using Yeoman generator</span></span>](get-started-yeoman.md)
* [<span data-ttu-id="8787d-153">创建对话机器人应用</span><span class="sxs-lookup"><span data-stu-id="8787d-153">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="8787d-154">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="8787d-154">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="8787d-155">代码示例</span><span class="sxs-lookup"><span data-stu-id="8787d-155">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)