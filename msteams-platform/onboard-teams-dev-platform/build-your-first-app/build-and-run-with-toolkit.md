---
title: 构建并运行您的第一个团队应用程序
author: heath-hamilton
description: 运行你的首个 Microsoft 团队应用。
ms.openlocfilehash: 98af8d8d6d89007e36c24bd34661ec21b33cbdf1
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651923"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="cc801-103">生成并运行你的首个 Microsoft 团队应用</span><span class="sxs-lookup"><span data-stu-id="cc801-103">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="cc801-104">您可以通过快速构建和运行基本应用程序直接在 Microsoft 团队平台上进行开发。</span><span class="sxs-lookup"><span data-stu-id="cc801-104">You can jump right into developing on the Microsoft Teams platform by quickly building and running a basic app.</span></span>

> [!NOTE]
> <span data-ttu-id="cc801-105">在遵循这些教程时， (特别对) 做出响应，有助于了解 JavaScript 的工作知识。</span><span class="sxs-lookup"><span data-stu-id="cc801-105">It's helpful to have working knowledge of JavaScript (specifically React) when following these tutorials.</span></span>

## <a name="set-up-your-development-account"></a><span data-ttu-id="cc801-106">设置你的开发帐户</span><span class="sxs-lookup"><span data-stu-id="cc801-106">Set up your development account</span></span>

<span data-ttu-id="cc801-107">若要为团队构建应用程序，您需要一个允许旁加载 (的团队帐户。您的帐户可能已提供此) 。</span><span class="sxs-lookup"><span data-stu-id="cc801-107">To build apps for Teams, you need a Teams account that allows sideloading (your account may already provide this).</span></span> <span data-ttu-id="cc801-108">如果不是，请注册 Microsoft 365 开发人员订阅，以便您可以获取测试租户。</span><span class="sxs-lookup"><span data-stu-id="cc801-108">If it doesn't, register for a Microsoft 365 developer subscription so you can get a test tenant.</span></span>

1. <span data-ttu-id="cc801-109">验证是否可以在团队中旁加载应用程序：</span><span class="sxs-lookup"><span data-stu-id="cc801-109">Verify if you can sideload apps in Teams:</span></span>
    1. <span data-ttu-id="cc801-110">在 "团队客户端" 中，选择 "**应用**"。</span><span class="sxs-lookup"><span data-stu-id="cc801-110">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="cc801-111">查找用于**上传自定义应用程序**的选项。</span><span class="sxs-lookup"><span data-stu-id="cc801-111">Look for an option to **Upload a custom app**.</span></span>
1. <span data-ttu-id="cc801-112">如果您有此选项，则可以开始构建。</span><span class="sxs-lookup"><span data-stu-id="cc801-112">If you have this option, you can start building.</span></span> <span data-ttu-id="cc801-113">如果不是，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="cc801-113">If not, do the following:</span></span>
    1. <span data-ttu-id="cc801-114">注册[Microsoft 365 开发人员订阅](../doc-links/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="cc801-114">Register for a [Microsoft 365 developer subscription](../doc-links/prepare-your-o365-tenant.md).</span></span>
    1. <span data-ttu-id="cc801-115">为您的测试帐户[启用自定义应用程序旁加载](../doc-links/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。</span><span class="sxs-lookup"><span data-stu-id="cc801-115">[Enable custom app sideloading](../doc-links/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) for your test account.</span></span>

## <a name="get-your-development-tools"></a><span data-ttu-id="cc801-116">获取你的开发工具</span><span class="sxs-lookup"><span data-stu-id="cc801-116">Get your development tools</span></span>

<span data-ttu-id="cc801-117">您可以使用您的首选工具生成团队应用程序，但您需要使用 Visual Studio Code 和 Microsoft 团队工具包快速入门。</span><span class="sxs-lookup"><span data-stu-id="cc801-117">You can build Teams apps with your preferred tools, but here's what you need to get started quickly with Visual Studio Code and the Microsoft Teams Toolkit.</span></span>

1. <span data-ttu-id="cc801-118">安装最新版本的[Visual Studio Code](https://code.visualstudio.com/download)。</span><span class="sxs-lookup"><span data-stu-id="cc801-118">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span>
1. <span data-ttu-id="cc801-119">在 Visual Studio Code 中， **Extensions**选择 ![ 左侧活动栏上的 "扩展 Visual Studio 工具包视图"， ](../doc-links/images/vs-code-extensions.png) 然后安装**Microsoft 团队工具包**。</span><span class="sxs-lookup"><span data-stu-id="cc801-119">In Visual Studio Code, select **Extensions** ![visual studio toolkit view](../doc-links/images/vs-code-extensions.png) on the left Activity Bar and install the **Microsoft Teams Toolkit**.</span></span>
1. <span data-ttu-id="cc801-120">安装 [Node.js](https://nodejs.org/en/)。</span><span class="sxs-lookup"><span data-stu-id="cc801-120">Install [Node.js](https://nodejs.org/en/).</span></span>

## <a name="create-an-app-project"></a><span data-ttu-id="cc801-121">创建应用程序项目</span><span class="sxs-lookup"><span data-stu-id="cc801-121">Create an app project</span></span>

<span data-ttu-id="cc801-122">Microsoft 团队工具包可帮助您设置第一个应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="cc801-122">The Microsoft Teams Toolkit can help you set up your first app project.</span></span>

1. <span data-ttu-id="cc801-123">在 Visual Studio Code 中，通过选择 "团队" 图标打开工具包</span><span class="sxs-lookup"><span data-stu-id="cc801-123">In Visual Studio Code, open the toolkit by selecting the Teams icon</span></span> ![团队图标](../doc-links/images/favicon-16x16.png) <span data-ttu-id="cc801-125">在左侧的活动栏上。</span><span class="sxs-lookup"><span data-stu-id="cc801-125">on the left Activity Bar.</span></span>
1. <span data-ttu-id="cc801-126">选择 "**创建新的团队应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="cc801-126">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="cc801-127">出现提示时，请输入您的应用程序的名称。</span><span class="sxs-lookup"><span data-stu-id="cc801-127">When prompted, enter a name for your app.</span></span> <span data-ttu-id="cc801-128">这是您的应用程序的默认名称，也是本地计算机上的项目目录的名称。</span><span class="sxs-lookup"><span data-stu-id="cc801-128">This is the default name for your app and also the name of the project directory on your local machine.</span></span>
1. <span data-ttu-id="cc801-129">在 "**添加功能**" 屏幕上，依次选择 **"** **下一步**"。</span><span class="sxs-lookup"><span data-stu-id="cc801-129">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="cc801-130">检查 "**个人" 选项卡**选项，然后选择 "**完成**" 来配置项目。</span><span class="sxs-lookup"><span data-stu-id="cc801-130">Check the **Personal tab** option and select **Finish** to configure your project.</span></span>

![工具箱添加选项卡视图](../doc-links/images/toolkit-add-tabs.PNG)

<span data-ttu-id="cc801-132">完成后，您便拥有了用于构建个人选项卡的应用程序基架组件。</span><span class="sxs-lookup"><span data-stu-id="cc801-132">Once complete, you have the app scaffolding components for building a personal tab.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="cc801-133">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="cc801-133">Run your app</span></span>

<span data-ttu-id="cc801-134">按照 `README.md` 项目中的说明生成、运行应用程序并将其部署到团队。</span><span class="sxs-lookup"><span data-stu-id="cc801-134">Follow the `README.md` in your project to build, run, and deploy your app to Teams.</span></span> <span data-ttu-id="cc801-135">通常情况下，这些说明可帮助您执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="cc801-135">In general, these instructions help you do the following:</span></span>

* <span data-ttu-id="cc801-136">将您的应用程序托管在上 `localhost` 。</span><span class="sxs-lookup"><span data-stu-id="cc801-136">Host your app on `localhost`.</span></span>
* <span data-ttu-id="cc801-137">[设置具有 ngrok 的安全隧道](../doc-links/debug.md#locally-hosted)，以便团队可以访问您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="cc801-137">[Set up a secure tunnel with ngrok](../doc-links/debug.md#locally-hosted) so that Teams can access your app.</span></span> <span data-ttu-id="cc801-138"> (安装[ngrok](https://ngrok.com/download)。 ) </span><span class="sxs-lookup"><span data-stu-id="cc801-138">(Install [ngrok](https://ngrok.com/download).)</span></span>
* <span data-ttu-id="cc801-139">在使用文件夹中的团队客户端中[旁加载您的应用程序](../doc-links/apps-upload.md) `Development.zip` `.publish` 。</span><span class="sxs-lookup"><span data-stu-id="cc801-139">[Sideload your app](../doc-links/apps-upload.md) in the Teams client using the `Development.zip` in the `.publish` folder.</span></span>

<span data-ttu-id="cc801-140">旁加载您的应用程序后，它应在团队客户端中如下所示。</span><span class="sxs-lookup"><span data-stu-id="cc801-140">Once you sideload your app, it should look like this in the Teams client.</span></span>

![Hello world 示例选项卡](../doc-links/images/tab-running.png)

## <a name="important-app-project-files"></a><span data-ttu-id="cc801-142">重要的应用程序项目文件</span><span class="sxs-lookup"><span data-stu-id="cc801-142">Important app project files</span></span>

<span data-ttu-id="cc801-143">设置应用程序项目和基架后，请花些时间了解一些主要文件团队应用程序开发人员使用的文件。</span><span class="sxs-lookup"><span data-stu-id="cc801-143">With your app project and scaffolding set up, take some time to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="cc801-144">应用程序清单 (`manifest.json`) </span><span class="sxs-lookup"><span data-stu-id="cc801-144">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="cc801-145">在目录中 `.publish` ，应用程序清单是任何应用程序项目的起始点。</span><span class="sxs-lookup"><span data-stu-id="cc801-145">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="cc801-146">清单定义您的应用程序的基本属性并指向所需的资源。</span><span class="sxs-lookup"><span data-stu-id="cc801-146">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="cc801-147">在安装应用程序时，团队会对清单进行分析，以了解如何在客户端中呈现您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="cc801-147">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

<span data-ttu-id="cc801-148">在下面的教程中，你将重点介绍用于构建个人和频道选项卡的应用程序清单的各个部分。</span><span class="sxs-lookup"><span data-stu-id="cc801-148">In the following tutorials, you'll focus on the sections of the app manifest for building personal and channel tabs.</span></span>

### <a name="package-developmentzip"></a><span data-ttu-id="cc801-149">包 (`Development.zip`) </span><span class="sxs-lookup"><span data-stu-id="cc801-149">Package (`Development.zip`)</span></span>

<span data-ttu-id="cc801-150">也位于目录中 `.publish` ，您需要应用程序包才能在团队中[旁加载您的应用程序](../../overview.md#how-can-you-share-your-teams-app)。</span><span class="sxs-lookup"><span data-stu-id="cc801-150">Also located in the `.publish` directory, you need the app package to [sideload your app](../../overview.md#how-can-you-share-your-teams-app) in Teams.</span></span> <span data-ttu-id="cc801-151">在[发布到组织的应用程序目录](../../overview.md#how-can-you-share-your-teams-app)或[AppSource](../../concepts/deploy-and-publish/appsource/publish.md)时也使用它。</span><span class="sxs-lookup"><span data-stu-id="cc801-151">It's also used when [publishing to your organization's app catalog](../../overview.md#how-can-you-share-your-teams-app) or [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="cc801-152">以下是有关应用程序包文件的一些详细信息：</span><span class="sxs-lookup"><span data-stu-id="cc801-152">Here are some details about the app package files:</span></span>

|<span data-ttu-id="cc801-153">名称</span><span class="sxs-lookup"><span data-stu-id="cc801-153">Name</span></span>|<span data-ttu-id="cc801-154">类型</span><span class="sxs-lookup"><span data-stu-id="cc801-154">Type</span></span>|<span data-ttu-id="cc801-155">Size</span><span class="sxs-lookup"><span data-stu-id="cc801-155">Size</span></span>|<span data-ttu-id="cc801-156">清单位置</span><span class="sxs-lookup"><span data-stu-id="cc801-156">Manifest location</span></span>|<span data-ttu-id="cc801-157">工具包文件名</span><span class="sxs-lookup"><span data-stu-id="cc801-157">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="cc801-158">**应用程序清单**</span><span class="sxs-lookup"><span data-stu-id="cc801-158">**App manifest**</span></span>|`.json`| <span data-ttu-id="cc801-159">—</span><span class="sxs-lookup"><span data-stu-id="cc801-159">—</span></span> | <span data-ttu-id="cc801-160">—</span><span class="sxs-lookup"><span data-stu-id="cc801-160">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="cc801-161">**颜色徽标**</span><span class="sxs-lookup"><span data-stu-id="cc801-161">**Color logo**</span></span>|`.png`|<span data-ttu-id="cc801-162">192 &times; 192 像素</span><span class="sxs-lookup"><span data-stu-id="cc801-162">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="cc801-163">**大纲徽标**</span><span class="sxs-lookup"><span data-stu-id="cc801-163">**Outline logo**</span></span>|`.png`|<span data-ttu-id="cc801-164">32 &times; 32 像素</span><span class="sxs-lookup"><span data-stu-id="cc801-164">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

### <a name="scaffolding-src"></a><span data-ttu-id="cc801-165">基架 (`src`) </span><span class="sxs-lookup"><span data-stu-id="cc801-165">Scaffolding (`src`)</span></span>

<span data-ttu-id="cc801-166">该工具包将根据您在安装过程中添加的功能，在目录中自动为您创建基架 `src` 。</span><span class="sxs-lookup"><span data-stu-id="cc801-166">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="cc801-167">但无论您拥有哪种类型的应用程序，都会创建一些文件。</span><span class="sxs-lookup"><span data-stu-id="cc801-167">Some files are created no matter what kind of app you have, though.</span></span> <span data-ttu-id="cc801-168">例如， `App.js` 目录中的文件 `src/components` 很重要，因为它处理您的应用程序的初始化和路由。</span><span class="sxs-lookup"><span data-stu-id="cc801-168">For example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="cc801-169">最重要的是，它调用[Microsoft 团队 SDK](../doc-links/using-teams-client-sdk.md)以在您的应用程序和团队之间建立通信。</span><span class="sxs-lookup"><span data-stu-id="cc801-169">Most importantly, it calls the [Microsoft Teams SDK](../doc-links/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

<span data-ttu-id="cc801-170">您可以在教程中了解有关用于创建个人和频道选项卡的更多有关基架的信息。</span><span class="sxs-lookup"><span data-stu-id="cc801-170">You can learn more about scaffolding in the tutorials for creating personal and channel tabs.</span></span>

## <a name="next-step"></a><span data-ttu-id="cc801-171">后续步骤</span><span class="sxs-lookup"><span data-stu-id="cc801-171">Next step</span></span>

<span data-ttu-id="cc801-172">🎉祝贺！</span><span class="sxs-lookup"><span data-stu-id="cc801-172">🎉 Congratulations!</span></span> <span data-ttu-id="cc801-173">您有一个正在运行的团队应用程序。</span><span class="sxs-lookup"><span data-stu-id="cc801-173">You have a running Teams app.</span></span> <span data-ttu-id="cc801-174">选择以下按钮以了解如何向其添加实际功能。</span><span class="sxs-lookup"><span data-stu-id="cc801-174">Select the following button to learn how to add a real-world feature to it.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cc801-175">生成个人选项卡</span><span class="sxs-lookup"><span data-stu-id="cc801-175">Build a personal tab</span></span>](add-personal-tab.md)
