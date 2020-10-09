---
title: 开始构建第一个团队应用
author: heath-hamilton
description: 构建首个 Microsoft 团队应用程序的概述和先决条件
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: quickstart
ms.openlocfilehash: 14776b147309877212f710677ae5941238cf5c0d
ms.sourcegitcommit: 560bf433129c16888135879e2703dbdeb38ec99f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "48397692"
---
# <a name="build-your-first-teams-app-overview"></a><span data-ttu-id="d90b0-103">构建你的第一个团队应用概述</span><span class="sxs-lookup"><span data-stu-id="d90b0-103">Build your first Teams app overview</span></span>

<span data-ttu-id="d90b0-104">在 " **构建您的首个应用** 课程" 中，您将创建基本的团队应用程序。</span><span class="sxs-lookup"><span data-stu-id="d90b0-104">In the **build your first app** lessons, you create basic Teams apps.</span></span> <span data-ttu-id="d90b0-105">每个教程演示如何构建一个简单的真实团队应用程序，同时向您介绍了常见工具、基本概念以及更高级的功能。</span><span class="sxs-lookup"><span data-stu-id="d90b0-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="d90b0-106">你将了解的内容</span><span class="sxs-lookup"><span data-stu-id="d90b0-106">What you'll learn</span></span>

<span data-ttu-id="d90b0-107">下面介绍了学习课程后您知道的内容。</span><span class="sxs-lookup"><span data-stu-id="d90b0-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="d90b0-108">**使用团队工具包快速启动和运行**： Visual Studio 代码的 Microsoft 团队工具包负责创建您的应用程序项目和基架，以便您可以在几分钟内运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="d90b0-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="d90b0-109">**使用清单定义您的应用**程序：应用程序清单是指您在其中指定团队应用程序使用的功能和服务的位置。</span><span class="sxs-lookup"><span data-stu-id="d90b0-109">**Define your app with the manifest**: The app manifest is where you specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="d90b0-110">**确定您的应用程序访问群体的范围**：构建一个工作组应用程序以供个人使用、协作或同时使用这两者。</span><span class="sxs-lookup"><span data-stu-id="d90b0-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
  > * <span data-ttu-id="d90b0-111">**获取团队框架的经验**：自定义应用 (例如，将其配色方案更改为与 "团队" 主题) 与团队 JavaScript SDK 中的 "帮助" 相匹配。</span><span class="sxs-lookup"><span data-stu-id="d90b0-111">**Get experience with Teams frameworks**: Customize your app (for example, change its color scheme to match the Teams theme) with help from the Teams JavaScript SDK.</span></span> <span data-ttu-id="d90b0-112">此外，了解用于创建和管理 bot 的常用工具。</span><span class="sxs-lookup"><span data-stu-id="d90b0-112">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="d90b0-113">**在您的应用程序上展开**：在整个课程中，您将找到可能对 (（如身份验证和设计指南) ）感兴趣的相关主题。</span><span class="sxs-lookup"><span data-stu-id="d90b0-113">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="d90b0-114">团队应用程序基础</span><span class="sxs-lookup"><span data-stu-id="d90b0-114">Teams app fundamentals</span></span>

<span data-ttu-id="d90b0-115">在开始教程之前，您应该了解以下有关为团队生成应用程序的信息。</span><span class="sxs-lookup"><span data-stu-id="d90b0-115">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a><span data-ttu-id="d90b0-116">应用可以具有多个功能和入口点</span><span class="sxs-lookup"><span data-stu-id="d90b0-116">Apps can have multiple capabilities and entry points</span></span>

<span data-ttu-id="d90b0-117">团队应用程序由一个或多个 [平台功能](../concepts/capabilities-overview.md) 和 [入口点](../concepts/extensibility-points.md)组成。</span><span class="sxs-lookup"><span data-stu-id="d90b0-117">Teams apps are made up of one or more [platform capabilities](../concepts/capabilities-overview.md) and [entry points](../concepts/extensibility-points.md).</span></span> <span data-ttu-id="d90b0-118">您可以使用大量的团队特定 [UI 组件和约定](../concepts/extensibility-points.md#ui-components)（如卡片和任务模块）呈现应用程序。</span><span class="sxs-lookup"><span data-stu-id="d90b0-118">You can present your app using a number of Teams-specific [UI components and conventions](../concepts/extensibility-points.md#ui-components), such as cards and task modules.</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="d90b0-119">团队不会托管您的应用程序</span><span class="sxs-lookup"><span data-stu-id="d90b0-119">Teams doesn't host your app</span></span>

<span data-ttu-id="d90b0-120">团队应用程序包含三个重要部分：</span><span class="sxs-lookup"><span data-stu-id="d90b0-120">A Teams app includes three important pieces:</span></span>

* <span data-ttu-id="d90b0-121">对应用程序加电的逻辑、数据存储和 API 调用。</span><span class="sxs-lookup"><span data-stu-id="d90b0-121">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="d90b0-122">这些服务不是由团队托管的，并且必须可通过 HTTPS 访问。</span><span class="sxs-lookup"><span data-stu-id="d90b0-122">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="d90b0-123">团队客户端 (web、桌面或移动) 上的用户使用您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="d90b0-123">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="d90b0-124">您的应用程序包，可用于在团队中安装应用程序。</span><span class="sxs-lookup"><span data-stu-id="d90b0-124">Your app package, which you use to install the app in Teams.</span></span> <span data-ttu-id="d90b0-125">它包含应用程序元数据以及指向托管服务的指针。</span><span class="sxs-lookup"><span data-stu-id="d90b0-125">It contains app metadata and pointers to your hosted services.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="d90b0-126">获取先决条件</span><span class="sxs-lookup"><span data-stu-id="d90b0-126">Get prerequisites</span></span>

<span data-ttu-id="d90b0-127">验证您是否具有用于生成团队应用程序的正确帐户，并安装一些建议的开发工具。</span><span class="sxs-lookup"><span data-stu-id="d90b0-127">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="d90b0-128">设置你的开发帐户</span><span class="sxs-lookup"><span data-stu-id="d90b0-128">Set up your development account</span></span>

<span data-ttu-id="d90b0-129">您需要一个允许自定义应用程序旁加载的团队帐户。</span><span class="sxs-lookup"><span data-stu-id="d90b0-129">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="d90b0-130"> (你的帐户可能已提供此。 ) </span><span class="sxs-lookup"><span data-stu-id="d90b0-130">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="d90b0-131">如果您有团队帐户，请验证您是否可以在团队中旁加载应用程序：</span><span class="sxs-lookup"><span data-stu-id="d90b0-131">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="d90b0-132">在 "团队客户端" 中，选择 " **应用**"。</span><span class="sxs-lookup"><span data-stu-id="d90b0-132">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="d90b0-133">查找用于 **上传自定义应用程序**的选项。</span><span class="sxs-lookup"><span data-stu-id="d90b0-133">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="图显示了在团队中可以上载自定义应用程序的位置。":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="d90b0-135">如果您看不到旁加载选项或没有团队帐户，<b>请选择此处</b>。</span><span class="sxs-lookup"><span data-stu-id="d90b0-135"><b>Select here</b> if you can't see the sideload option or don't have a Teams account.</span></span></summary>

<span data-ttu-id="d90b0-136">你可以通过加入 Microsoft 365 开发人员计划获取免费的团队测试帐户，以允许应用旁加载。</span><span class="sxs-lookup"><span data-stu-id="d90b0-136">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="d90b0-137"> (注册过程大约需要两分钟时间。 ) </span><span class="sxs-lookup"><span data-stu-id="d90b0-137">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="d90b0-138">转到 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="d90b0-138">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="d90b0-139">选择 " **立即加入** "，然后按照屏幕上的说明操作。</span><span class="sxs-lookup"><span data-stu-id="d90b0-139">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="d90b0-140">进入 "欢迎" 屏幕时，选择 " **设置 E5 订阅**"。</span><span class="sxs-lookup"><span data-stu-id="d90b0-140">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="d90b0-141">设置管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="d90b0-141">Set up your administrator account.</span></span> <span data-ttu-id="d90b0-142">完成后，您应该会看到类似这样的屏幕。</span><span class="sxs-lookup"><span data-stu-id="d90b0-142">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="图显示了在团队中可以上载自定义应用程序的位置。":::
1. <span data-ttu-id="d90b0-144">使用刚刚设置的管理员帐户登录到团队。</span><span class="sxs-lookup"><span data-stu-id="d90b0-144">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="d90b0-145">验证您是否现在已 **上载自定义应用程序** 选项。</span><span class="sxs-lookup"><span data-stu-id="d90b0-145">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

### <a name="install-your-development-tools"></a><span data-ttu-id="d90b0-146">安装开发工具</span><span class="sxs-lookup"><span data-stu-id="d90b0-146">Install your development tools</span></span>

<span data-ttu-id="d90b0-147">您可以使用您的首选工具构建团队应用程序，但这些课程展示了如何快速开始使用 Microsoft 团队工具包获取 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="d90b0-147">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="d90b0-148">团队仅通过 HTTPS 连接显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="d90b0-148">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="d90b0-149">由于您将在本地托管您的第一个应用程序以节省时间，因此您将了解如何使用 ngrok 在团队和您的应用程序之间 [设置安全隧道](../concepts/build-and-test/debug.md#locally-hosted) 。</span><span class="sxs-lookup"><span data-stu-id="d90b0-149">Since you'll host your first app locally to save time, you'll learn how to use [ngrok to set up a secure tunnel](../concepts/build-and-test/debug.md#locally-hosted) between Teams and your app.</span></span> <span data-ttu-id="d90b0-150"> (生产级团队应用程序托管在云中。 ) </span><span class="sxs-lookup"><span data-stu-id="d90b0-150">(Production-level Teams apps are hosted in the cloud.)</span></span>

1. <span data-ttu-id="d90b0-151">安装 [Node.js](https://nodejs.org/en/)。</span><span class="sxs-lookup"><span data-stu-id="d90b0-151">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="d90b0-152">安装 [ngrok](https://ngrok.com/download)。</span><span class="sxs-lookup"><span data-stu-id="d90b0-152">Install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="d90b0-153">安装最新版本的 [Visual Studio Code](https://code.visualstudio.com/download)。</span><span class="sxs-lookup"><span data-stu-id="d90b0-153">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="d90b0-154"> (早期版本可能在工具包中不起作用。 ) </span><span class="sxs-lookup"><span data-stu-id="d90b0-154">(Earlier versions might not work with the toolkit.)</span></span>
1. 在 Visual Studio Code 中， **Extensions**选择 :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: 左侧活动栏上的 "扩展"，然后安装**Microsoft 团队工具包**。

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="图显示了在团队中可以上载自定义应用程序的位置。":::

## <a name="about-the-tutorials"></a><span data-ttu-id="d90b0-157">关于教程</span><span class="sxs-lookup"><span data-stu-id="d90b0-157">About the tutorials</span></span>

<span data-ttu-id="d90b0-158">你可以从任意团队开始 **构建你的第一个应用** 课程。</span><span class="sxs-lookup"><span data-stu-id="d90b0-158">You can start with any of the Teams **build your first app** lessons.</span></span> <span data-ttu-id="d90b0-159">如果你不确定首先要转到的位置，请遵循初级友好路径，并构建一个 "Hello，World！"</span><span class="sxs-lookup"><span data-stu-id="d90b0-159">If you're not sure where to go first, follow our beginner friendly path and build a "Hello, World!"</span></span> <span data-ttu-id="d90b0-160">应用程序.</span><span class="sxs-lookup"><span data-stu-id="d90b0-160">app.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="图显示了在团队中可以上载自定义应用程序的位置。" border="false":::

## <a name="next-step"></a><span data-ttu-id="d90b0-162">后续步骤</span><span class="sxs-lookup"><span data-stu-id="d90b0-162">Next step</span></span>

<span data-ttu-id="d90b0-163">设置帐户和环境后，即可开始构建。</span><span class="sxs-lookup"><span data-stu-id="d90b0-163">Once you set up your account and environment, you can start building.</span></span>

### <a name="beginner-friendly-tutorial"></a><span data-ttu-id="d90b0-164">初级友好教程</span><span class="sxs-lookup"><span data-stu-id="d90b0-164">Beginner friendly tutorial</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d90b0-165">构建 "Hello，World！" 应用程序</span><span class="sxs-lookup"><span data-stu-id="d90b0-165">Build a "Hello, World!" app</span></span>](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a><span data-ttu-id="d90b0-166">其他教程</span><span class="sxs-lookup"><span data-stu-id="d90b0-166">Other tutorials</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d90b0-167">创建机器人</span><span class="sxs-lookup"><span data-stu-id="d90b0-167">Build a bot</span></span>](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="d90b0-168">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="d90b0-168">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
