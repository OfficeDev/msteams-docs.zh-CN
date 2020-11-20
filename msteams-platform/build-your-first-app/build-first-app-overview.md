---
title: 入门-构建您的首个应用程序概述和先决条件
author: heath-hamilton
description: 了解如何开始使用 Microsoft 团队应用程序开发和设置你的环境。
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: e2e73e755c45fa3bff3b6320dfbf0999a575fe99
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346810"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a><span data-ttu-id="35a7d-103">构建你的首个 Microsoft 团队应用概述</span><span class="sxs-lookup"><span data-stu-id="35a7d-103">Build your first Microsoft Teams app overview</span></span>

<span data-ttu-id="35a7d-104">在 " **构建您的首个应用** 课程" 中，您将创建基本的团队应用程序。</span><span class="sxs-lookup"><span data-stu-id="35a7d-104">In the **build your first app** lessons, you create basic Teams apps.</span></span> <span data-ttu-id="35a7d-105">每个教程演示如何构建一个简单的真实团队应用程序，同时向您介绍了常见工具、基本概念以及更高级的功能。</span><span class="sxs-lookup"><span data-stu-id="35a7d-105">Each tutorial walks through how to build a simple, real-world Teams app while introducing you to common tools, fundamental concepts, and more advanced features.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="35a7d-106">你将了解的内容</span><span class="sxs-lookup"><span data-stu-id="35a7d-106">What you'll learn</span></span>

<span data-ttu-id="35a7d-107">下面介绍了学习课程后您知道的内容。</span><span class="sxs-lookup"><span data-stu-id="35a7d-107">Here's an idea of what you'll know after going through the lessons.</span></span>

> [!div class="checklist"]
  >
  > * <span data-ttu-id="35a7d-108">**使用团队工具包快速启动和运行**： Visual Studio 代码的 Microsoft 团队工具包负责创建您的应用程序项目和基架，以便您可以在几分钟内运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="35a7d-108">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > * <span data-ttu-id="35a7d-109">**使用应用程序 Studio 配置应用**：指定你的团队应用使用的功能和服务。</span><span class="sxs-lookup"><span data-stu-id="35a7d-109">**Configure your app with App Studio**: Specify the capabilities and services your Teams app uses.</span></span>
  > * <span data-ttu-id="35a7d-110">**确定您的应用程序访问群体的范围**：构建一个工作组应用程序以供个人使用、协作或同时使用这两者。</span><span class="sxs-lookup"><span data-stu-id="35a7d-110">**Scope your app's audience**: Build a Teams app for personal use, collaboration, or both.</span></span>
  > * <span data-ttu-id="35a7d-111">**获取团队工具和 sdk 的经验**：自定义应用 (例如，将其配色方案更改为与 "团队" 主题) 与团队 JavaScript SDK 中的 "帮助" 相匹配。</span><span class="sxs-lookup"><span data-stu-id="35a7d-111">**Get experience with Teams tools and SDKs**: Customize your app (for example, change its color scheme to match the Teams theme) with help from the Teams JavaScript SDK.</span></span> <span data-ttu-id="35a7d-112">此外，了解用于创建和管理 bot 的常用工具。</span><span class="sxs-lookup"><span data-stu-id="35a7d-112">Also, learn about common tools for creating and managing bots.</span></span>
  > * <span data-ttu-id="35a7d-113">**在您的应用程序上展开**：在整个课程中，您将找到可能对 (（如身份验证和设计指南) ）感兴趣的相关主题。</span><span class="sxs-lookup"><span data-stu-id="35a7d-113">**Expand on your app**: Throughout the lessons, you'll find related topics you're probably interested in (such as authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="35a7d-114">团队应用程序基础</span><span class="sxs-lookup"><span data-stu-id="35a7d-114">Teams app fundamentals</span></span>

<span data-ttu-id="35a7d-115">在开始教程之前，您应该了解以下有关为团队生成应用程序的信息。</span><span class="sxs-lookup"><span data-stu-id="35a7d-115">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a><span data-ttu-id="35a7d-116">应用可以具有多个功能和入口点</span><span class="sxs-lookup"><span data-stu-id="35a7d-116">Apps can have multiple capabilities and entry points</span></span>

<span data-ttu-id="35a7d-117">团队应用程序由一个或多个 [平台功能](../concepts/capabilities-overview.md) 组成 (用户如何使用应用程序) 和 [入口点](../concepts/extensibility-points.md) (用户发现应用程序) 。</span><span class="sxs-lookup"><span data-stu-id="35a7d-117">A Teams app is made up of one or more [platform capabilities](../concepts/capabilities-overview.md) (how people use the app) and [entry points](../concepts/extensibility-points.md) (where people discover the app).</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="35a7d-118">团队不会托管您的应用程序</span><span class="sxs-lookup"><span data-stu-id="35a7d-118">Teams doesn't host your app</span></span>

<span data-ttu-id="35a7d-119">团队应用程序包括以下重要部分：</span><span class="sxs-lookup"><span data-stu-id="35a7d-119">A Teams app includes the following important pieces:</span></span>

* <span data-ttu-id="35a7d-120">对应用程序加电的逻辑、数据存储和 API 调用。</span><span class="sxs-lookup"><span data-stu-id="35a7d-120">The logic, data storage, and API calls that power your app.</span></span> <span data-ttu-id="35a7d-121">这些服务不是由团队托管的，并且必须可通过 HTTPS 访问。</span><span class="sxs-lookup"><span data-stu-id="35a7d-121">These services are not hosted by Teams and must be accessible via HTTPS.</span></span>
* <span data-ttu-id="35a7d-122">团队客户端 (web、桌面或移动) 上的用户使用您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="35a7d-122">The Teams client (web, desktop, or mobile) where people use your app.</span></span>
* <span data-ttu-id="35a7d-123">您的应用程序 ID，可让您使用应用程序 Studio 配置应用程序。</span><span class="sxs-lookup"><span data-stu-id="35a7d-123">Your app ID, which lets you configure your app with App Studio.</span></span>

## <a name="get-prerequisites"></a><span data-ttu-id="35a7d-124">获取先决条件</span><span class="sxs-lookup"><span data-stu-id="35a7d-124">Get prerequisites</span></span>

<span data-ttu-id="35a7d-125">验证您是否具有用于生成团队应用程序的正确帐户，并安装一些建议的开发工具。</span><span class="sxs-lookup"><span data-stu-id="35a7d-125">Verify you have the right account for building Teams apps and install some recommended development tools.</span></span>

### <a name="set-up-your-development-account"></a><span data-ttu-id="35a7d-126">设置你的开发帐户</span><span class="sxs-lookup"><span data-stu-id="35a7d-126">Set up your development account</span></span>

<span data-ttu-id="35a7d-127">您需要一个允许自定义应用程序旁加载的团队帐户。</span><span class="sxs-lookup"><span data-stu-id="35a7d-127">You need a Teams account that allows custom app sideloading.</span></span> <span data-ttu-id="35a7d-128"> (你的帐户可能已提供此。 ) </span><span class="sxs-lookup"><span data-stu-id="35a7d-128">(Your account may already provide this.)</span></span>

1. <span data-ttu-id="35a7d-129">如果您有团队帐户，请验证您是否可以在团队中旁加载应用程序：</span><span class="sxs-lookup"><span data-stu-id="35a7d-129">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="35a7d-130">在 "团队客户端" 中，选择 " **应用**"。</span><span class="sxs-lookup"><span data-stu-id="35a7d-130">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="35a7d-131">查找用于 **上传自定义应用程序** 的选项。</span><span class="sxs-lookup"><span data-stu-id="35a7d-131">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="图显示了在团队中可以上载自定义应用程序的位置。":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><span data-ttu-id="35a7d-133">如果您看不到旁加载选项或没有团队帐户，<b>请选择此处</b>。</span><span class="sxs-lookup"><span data-stu-id="35a7d-133"><b>Select here</b> if you can't see the sideload option or don't have a Teams account.</span></span></summary>

<span data-ttu-id="35a7d-134">你可以通过加入 Microsoft 365 开发人员计划获取免费的团队测试帐户，以允许应用旁加载。</span><span class="sxs-lookup"><span data-stu-id="35a7d-134">You can get a free Teams test account that allows app sideloading by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="35a7d-135"> (注册过程大约需要两分钟时间。 ) </span><span class="sxs-lookup"><span data-stu-id="35a7d-135">(The registration process takes approximately two minutes.)</span></span>

1. <span data-ttu-id="35a7d-136">转到 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="35a7d-136">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="35a7d-137">选择 " **立即加入** "，然后按照屏幕上的说明操作。</span><span class="sxs-lookup"><span data-stu-id="35a7d-137">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="35a7d-138">进入 "欢迎" 屏幕时，选择 " **设置 E5 订阅**"。</span><span class="sxs-lookup"><span data-stu-id="35a7d-138">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="35a7d-139">设置管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="35a7d-139">Set up your administrator account.</span></span> <span data-ttu-id="35a7d-140">完成后，您应该会看到类似这样的屏幕。</span><span class="sxs-lookup"><span data-stu-id="35a7d-140">Once you finish, you should see a screen like this.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="注册 Microsoft 365 开发人员计划后，您会看到的示例。":::
1. <span data-ttu-id="35a7d-142">使用刚刚设置的管理员帐户登录到团队。</span><span class="sxs-lookup"><span data-stu-id="35a7d-142">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="35a7d-143">验证您是否现在已 **上载自定义应用程序** 选项。</span><span class="sxs-lookup"><span data-stu-id="35a7d-143">Verify if you now have the **Upload a custom app** option.</span></span>

</details>

> [!Note]
> <span data-ttu-id="35a7d-144">如果仍然无法旁加载应用，请参阅 [启用自定义团队应用并打开自定义应用上载](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。</span><span class="sxs-lookup"><span data-stu-id="35a7d-144">If you still can't sideload apps, refer to [Enable custom Teams apps and turn on custom app uploading](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

### <a name="install-your-development-tools"></a><span data-ttu-id="35a7d-145">安装开发工具</span><span class="sxs-lookup"><span data-stu-id="35a7d-145">Install your development tools</span></span>

<span data-ttu-id="35a7d-146">您可以使用您的首选工具构建团队应用程序，但这些课程展示了如何快速开始使用 Microsoft 团队工具包获取 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="35a7d-146">You can build Teams apps with your preferred tools, but these lessons show how you can get started quickly with the Microsoft Teams Toolkit for Visual Studio Code.</span></span>

<span data-ttu-id="35a7d-147">团队仅通过 HTTPS 连接显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="35a7d-147">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="35a7d-148">若要在本地（如 bot）调试某些类型的应用程序，您将了解如何使用 ngrok 在团队和应用之间 [设置安全隧道](../concepts/build-and-test/debug.md#locally-hosted) 。</span><span class="sxs-lookup"><span data-stu-id="35a7d-148">To debug certain types of apps locally, such as a bot, you'll learn how to use [ngrok to set up a secure tunnel](../concepts/build-and-test/debug.md#locally-hosted) between Teams and your app.</span></span> <span data-ttu-id="35a7d-149"> (生产团队应用程序托管在云中。 ) </span><span class="sxs-lookup"><span data-stu-id="35a7d-149">(Production Teams apps are hosted in the cloud.)</span></span>

1. <span data-ttu-id="35a7d-150">安装 [Node.js](https://nodejs.org/en/)。</span><span class="sxs-lookup"><span data-stu-id="35a7d-150">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="35a7d-151">如果您计划生成机器人或邮件扩展，请安装 [ngrok](https://ngrok.com/download) 。</span><span class="sxs-lookup"><span data-stu-id="35a7d-151">Install [ngrok](https://ngrok.com/download) if you plan to build a bot or messaging extension.</span></span>
1. <span data-ttu-id="35a7d-152">安装最新版本的 [Visual Studio Code](https://code.visualstudio.com/download)。</span><span class="sxs-lookup"><span data-stu-id="35a7d-152">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> <span data-ttu-id="35a7d-153"> (早期版本可能在工具包中不起作用。 ) </span><span class="sxs-lookup"><span data-stu-id="35a7d-153">(Earlier versions might not work with the toolkit.)</span></span>
1. 在 Visual Studio Code 中， **Extensions** 选择 :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: 左侧活动栏上的 "扩展"，然后安装 **Microsoft 团队工具包**。

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="图显示了在 Visual Studio Code 中可以安装 Microsoft 团队工具包扩展的位置。":::

## <a name="about-the-tutorials"></a><span data-ttu-id="35a7d-156">关于教程</span><span class="sxs-lookup"><span data-stu-id="35a7d-156">About the tutorials</span></span>

<span data-ttu-id="35a7d-157">你可以从任意团队开始 **构建你的第一个应用** 课程。</span><span class="sxs-lookup"><span data-stu-id="35a7d-157">You can start with any of the Teams **build your first app** lessons.</span></span> <span data-ttu-id="35a7d-158">如果你不确定首先要转到的位置，请遵循初级友好路径，并构建一个 "Hello，World！"</span><span class="sxs-lookup"><span data-stu-id="35a7d-158">If you're not sure where to go first, follow our beginner friendly path and build a "Hello, World!"</span></span> <span data-ttu-id="35a7d-159">应用程序.</span><span class="sxs-lookup"><span data-stu-id="35a7d-159">app.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="显示团队 &quot;构建您的首个应用&quot; 教程的学习途径的技能树。" border="false":::

## <a name="next-step"></a><span data-ttu-id="35a7d-161">后续步骤</span><span class="sxs-lookup"><span data-stu-id="35a7d-161">Next step</span></span>

<span data-ttu-id="35a7d-162">设置帐户和环境后，即可开始构建。</span><span class="sxs-lookup"><span data-stu-id="35a7d-162">Once you set up your account and environment, you can start building.</span></span>

### <a name="beginner-friendly-tutorial"></a><span data-ttu-id="35a7d-163">初级友好教程</span><span class="sxs-lookup"><span data-stu-id="35a7d-163">Beginner friendly tutorial</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="35a7d-164">构建 "Hello，World！" 应用程序</span><span class="sxs-lookup"><span data-stu-id="35a7d-164">Build a "Hello, World!" app</span></span>](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a><span data-ttu-id="35a7d-165">其他教程</span><span class="sxs-lookup"><span data-stu-id="35a7d-165">Other tutorials</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="35a7d-166">创建机器人</span><span class="sxs-lookup"><span data-stu-id="35a7d-166">Build a bot</span></span>](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="35a7d-167">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="35a7d-167">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
