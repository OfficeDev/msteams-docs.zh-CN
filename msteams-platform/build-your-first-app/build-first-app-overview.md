---
title: 入门 - 生成首个应用概述和先决条件
author: heath-hamilton
description: 了解如何开始使用 Microsoft Teams 应用开发和设置环境。
ms.author: lajanuar
localization_priority: Normal
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: d975383022089579a04317de73595106e7920c56
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019991"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a><span data-ttu-id="06f01-103">生成首个 Microsoft Teams 应用概述</span><span class="sxs-lookup"><span data-stu-id="06f01-103">Build your first Microsoft Teams app overview</span></span>

<span data-ttu-id="06f01-104">在 **入门课程** 中，你将了解如何创建基本的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="06f01-104">In the **get started** lessons, you learn how to create basic Teams apps.</span></span> <span data-ttu-id="06f01-105">每个教程将介绍如何生成简单的实际 Teams 应用，同时向用户介绍通用工具、基本概念和更高级的功能。</span><span class="sxs-lookup"><span data-stu-id="06f01-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="06f01-106">您将了解哪些功能</span><span class="sxs-lookup"><span data-stu-id="06f01-106">What you'll learn</span></span>

<span data-ttu-id="06f01-107">以下是在学习课程后你将了解的一些信息。</span><span class="sxs-lookup"><span data-stu-id="06f01-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="06f01-108">使用 **Teams Toolkit** 快速启动并运行：Microsoft Teams Toolkit for Visual Studio Code 负责创建应用项目和基架，以便你可以数分钟内拥有正在运行的应用。</span><span class="sxs-lookup"><span data-stu-id="06f01-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="06f01-109">**使用 App Studio 配置应用**：指定 Teams 应用使用的功能和服务。</span><span class="sxs-lookup"><span data-stu-id="06f01-109">**Configure your app with App Studio**: Specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="06f01-110">**确定应用受众的范围**：生成适用于个人使用和/或协作的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="06f01-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
> * <span data-ttu-id="06f01-111">**获取 Teams 工具和 SDK** 体验：使用 Teams JavaScript 客户端 SDK 帮助自定义应用。</span><span class="sxs-lookup"><span data-stu-id="06f01-111">**Get experience with Teams tools and SDKs**: Customize your app with help from the Teams JavaScript client SDK.</span></span> <span data-ttu-id="06f01-112">例如，更改应用的配色方案以匹配 Teams 主题。</span><span class="sxs-lookup"><span data-stu-id="06f01-112">For example, change your app's color scheme to match the Teams theme.</span></span> <span data-ttu-id="06f01-113">此外，了解用于创建和管理机器人的常用工具。</span><span class="sxs-lookup"><span data-stu-id="06f01-113">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="06f01-114">**在应用中展开**：在整个课程过程中，你将找到你可能感兴趣的相关主题 (如身份验证和设计指南) 。</span><span class="sxs-lookup"><span data-stu-id="06f01-114">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="06f01-115">Teams 应用基础</span><span class="sxs-lookup"><span data-stu-id="06f01-115">Teams app fundamentals</span></span>

<span data-ttu-id="06f01-116">在开始教程之前，你应了解以下有关构建 Teams 应用的信息。</span><span class="sxs-lookup"><span data-stu-id="06f01-116">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a><span data-ttu-id="06f01-117">应用可以有多个功能和入口点</span><span class="sxs-lookup"><span data-stu-id="06f01-117">Apps can have multiple capabilities and entry points</span></span>

<span data-ttu-id="06f01-118">Teams 应用由一个或多个平台功能 (用户[](../concepts/capabilities-overview.md)如何使用应用) 以及 (使用应用的入口点) 。 [](../concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="06f01-118">A Teams app is made up of one or more [platform capabilities](../concepts/capabilities-overview.md) (how people use the app) and [entry points](../concepts/extensibility-points.md) (where people use the app).</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="06f01-119">Teams 不托管你的应用</span><span class="sxs-lookup"><span data-stu-id="06f01-119">Teams doesn't host your app</span></span>

<span data-ttu-id="06f01-120">Teams 应用包括以下重要部分：</span><span class="sxs-lookup"><span data-stu-id="06f01-120">A Teams app includes the following important pieces:</span></span>

* <span data-ttu-id="06f01-121">支持你的应用的逻辑、数据存储和 API 调用。</span><span class="sxs-lookup"><span data-stu-id="06f01-121">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="06f01-122">这些服务不是由 Teams 托管的，必须通过 HTTPS 访问。</span><span class="sxs-lookup"><span data-stu-id="06f01-122">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="06f01-123">Teams 客户端 (Web、桌面或移动) ，用户可使用你的应用。</span><span class="sxs-lookup"><span data-stu-id="06f01-123">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="06f01-124">应用 ID，允许你使用 App Studio 配置应用。</span><span class="sxs-lookup"><span data-stu-id="06f01-124">Your app ID, which lets you configure your app with App Studio.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="06f01-125">获取先决条件</span><span class="sxs-lookup"><span data-stu-id="06f01-125">Get prerequisites</span></span>

<span data-ttu-id="06f01-126">验证你拥有用于生成 Teams 应用所需的正确帐户，并安装一些推荐的开发工具。</span><span class="sxs-lookup"><span data-stu-id="06f01-126">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="06f01-127">设置开发帐户</span><span class="sxs-lookup"><span data-stu-id="06f01-127">Set up your development account</span></span>

<span data-ttu-id="06f01-128">你需要一个允许自定义应用旁加载的 Teams 帐户。</span><span class="sxs-lookup"><span data-stu-id="06f01-128">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="06f01-129"> (你的帐户可能已经提供此功能) </span><span class="sxs-lookup"><span data-stu-id="06f01-129">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="06f01-130">如果你有 Teams 帐户，请验证你能否在 Teams 中旁加载应用：</span><span class="sxs-lookup"><span data-stu-id="06f01-130">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="06f01-131">在 Teams 客户端中，选择"**应用"。**</span><span class="sxs-lookup"><span data-stu-id="06f01-131">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="06f01-132">查找"上载自定义 **应用"选项**。</span><span class="sxs-lookup"><span data-stu-id="06f01-132">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="显示可以在 Teams 中上传自定义应用位置的图示。":::
    
    <span data-ttu-id="06f01-134">如果看不到该按钮，则没有在组织中的上载自定义应用的权限。可以通过注册免费的 Microsoft 365 开发人员订阅获取此功能。</span><span class="sxs-lookup"><span data-stu-id="06f01-134">If you don't see the button, you don't have permission to upload custom apps in your org. You can get this feature by signing up for a free Microsoft 365 developer subscription.</span></span>

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="06f01-135"><b>获取免费的 Microsoft 365 开发人员订阅</b></span><span class="sxs-lookup"><span data-stu-id="06f01-135"><b>Get your free Microsoft 365 developer subscription</b></span></span></summary>

<span data-ttu-id="06f01-136">可以通过加入 Microsoft 365 开发人员计划获取允许应用旁加载的免费 Teams 测试帐户。</span><span class="sxs-lookup"><span data-stu-id="06f01-136">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="06f01-137"> (注册过程大约需要两分钟) </span><span class="sxs-lookup"><span data-stu-id="06f01-137">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="06f01-138">转到 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="06f01-138">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="06f01-139">选择 **立即加入** 并按照屏幕上的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="06f01-139">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="06f01-140">当你进入欢迎屏幕时，选择 **"设置 E5 订阅"。**</span><span class="sxs-lookup"><span data-stu-id="06f01-140">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="06f01-141">设置管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="06f01-141">Set up your administrator account.</span></span> <span data-ttu-id="06f01-142">完成后，你应该会看到如下所示的屏幕。</span><span class="sxs-lookup"><span data-stu-id="06f01-142">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="注册 Microsoft 365 开发人员计划后看到的示例。":::
1. <span data-ttu-id="06f01-144">使用刚设置的管理员帐户登录 Teams。</span><span class="sxs-lookup"><span data-stu-id="06f01-144">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="06f01-145">验证你现在是否具有" **上载自定义应用"** 选项。</span><span class="sxs-lookup"><span data-stu-id="06f01-145">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

> [!Note]
> <span data-ttu-id="06f01-146">如果仍无法旁加载应用，请参阅 [启用自定义 Teams 应用并启用自定义应用上传](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。</span><span class="sxs-lookup"><span data-stu-id="06f01-146">If you still can't sideload apps, see [enable custom Teams apps and turn on custom app uploading](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

### <a name="install-your-development-tools"></a><span data-ttu-id="06f01-147">安装开发工具</span><span class="sxs-lookup"><span data-stu-id="06f01-147">Install your development tools</span></span>

<span data-ttu-id="06f01-148">可以使用首选工具生成 Teams 应用，但以下课程显示了如何快速开始使用 Microsoft Teams Toolkit for Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="06f01-148">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="06f01-149">Teams 仅通过 HTTPS 连接显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="06f01-149">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="06f01-150">若要在本地调试某些类型的应用（如机器人），你将了解如何使用 [ngrok](../concepts/build-and-test/debug.md#locally-hosted) 在 Teams 和你的应用之间设置安全隧道。</span><span class="sxs-lookup"><span data-stu-id="06f01-150">To debug certain types of apps locally, such as a bot, you'll learn how to use [ngrok to set up a secure tunnel](../concepts/build-and-test/debug.md#locally-hosted) between Teams and your app.</span></span> <span data-ttu-id="06f01-151"> (生产 Teams 应用托管在云中。) </span><span class="sxs-lookup"><span data-stu-id="06f01-151">(Production Teams apps are hosted in the cloud.)</span></span>

1. <span data-ttu-id="06f01-152">安装 [Node.js](https://nodejs.org/en/)。</span><span class="sxs-lookup"><span data-stu-id="06f01-152">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="06f01-153">如果要构建机器人或消息传递扩展，请安装 [ngrok，](https://ngrok.com/download) 然后使用 [ngrok 创建隧道](https://docs.microsoft.com/microsoftteams/platform/tutorials/get-started-dotnet-app-studio#tunnel-using-ngrok)。</span><span class="sxs-lookup"><span data-stu-id="06f01-153">Install [ngrok](https://ngrok.com/download) if you are building a bot or messaging extension and [create a tunnel using ngrok](https://docs.microsoft.com/microsoftteams/platform/tutorials/get-started-dotnet-app-studio#tunnel-using-ngrok).</span></span>
1. <span data-ttu-id="06f01-154">安装最新版本的 [Visual Studio Code](https://code.visualstudio.com/download)。</span><span class="sxs-lookup"><span data-stu-id="06f01-154">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="06f01-155"> (早期版本可能无法与工具包一) </span><span class="sxs-lookup"><span data-stu-id="06f01-155">(Earlier versions might not work with the toolkit.)</span></span>
1. 在Visual Studio代码"中，选择左侧活动栏上的"扩展 :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: "，然后安装 **Microsoft Teams Toolkit。**

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="此插图显示Visual Studio代码可以安装 Microsoft Teams Toolkit扩展。":::

## <a name="about-the-tutorials"></a><span data-ttu-id="06f01-158">关于教程</span><span class="sxs-lookup"><span data-stu-id="06f01-158">About the tutorials</span></span>

<span data-ttu-id="06f01-159">你可以从任何 Teams 入门 **课程** 开始。</span><span class="sxs-lookup"><span data-stu-id="06f01-159">You can start with any of the Teams **get started** lessons.</span></span> <span data-ttu-id="06f01-160">如果你不确定首先从何处开始，请按照初学者友好路径，生成"Hello， World！"</span><span class="sxs-lookup"><span data-stu-id="06f01-160">If you're not sure where to go first, follow our beginner friendly path and build a "Hello, World!"</span></span> <span data-ttu-id="06f01-161">应用。</span><span class="sxs-lookup"><span data-stu-id="06f01-161">app.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="显示 Teams&quot;入门&quot;课程的学习路径的技能树。" border="false":::

## <a name="next-step"></a><span data-ttu-id="06f01-163">后续步骤</span><span class="sxs-lookup"><span data-stu-id="06f01-163">Next step</span></span>

<span data-ttu-id="06f01-164">设置帐户和环境后，就可以开始构建了。</span><span class="sxs-lookup"><span data-stu-id="06f01-164">Once you set up your account and environment, you can start building.</span></span>

### <a name="beginner-friendly-tutorial"></a><span data-ttu-id="06f01-165">初学者友好教程</span><span class="sxs-lookup"><span data-stu-id="06f01-165">Beginner friendly tutorial</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="06f01-166">生成"Hello， World！"应用</span><span class="sxs-lookup"><span data-stu-id="06f01-166">Build a "Hello, World!" app</span></span>](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a><span data-ttu-id="06f01-167">其他教程</span><span class="sxs-lookup"><span data-stu-id="06f01-167">Other tutorials</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="06f01-168">创建机器人</span><span class="sxs-lookup"><span data-stu-id="06f01-168">Build a bot</span></span>](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="06f01-169">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="06f01-169">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
