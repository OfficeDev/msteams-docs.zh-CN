---
title: 使用 Microsoft Teams 安全和Toolkit生成Visual Studio
description: 使用 Microsoft Teams 服务器直接在 Visual Studio内构建出色的自定义Toolkit
keywords: Teams Visual Studio 工具包
ms.topic: overview
ms.openlocfilehash: 79ea22cfd154313247132c22684d444c0813c66f
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819201"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a><span data-ttu-id="446ca-104">使用 Microsoft Teams 安全和 Toolkit构建Visual Studio</span><span class="sxs-lookup"><span data-stu-id="446ca-104">Build apps with the Microsoft Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="446ca-105">Microsoft Teams Toolkit允许你在开发人员的集成开发环境内直接 Visual Studio创建自定义 Teams 应用， (IDE) 。</span><span class="sxs-lookup"><span data-stu-id="446ca-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="446ca-106">Microsoft Teams 工具包将指导你完成该过程，并提供生成、调试和启动 Teams 应用所需的一切。</span><span class="sxs-lookup"><span data-stu-id="446ca-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="446ca-107">先决条件</span><span class="sxs-lookup"><span data-stu-id="446ca-107">Prerequisites</span></span>

1. [<span data-ttu-id="446ca-108">启用开发人员预览版</span><span class="sxs-lookup"><span data-stu-id="446ca-108">Enable developer preview</span></span>](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. <span data-ttu-id="446ca-109">确保已 **<span>ASP.NE</span>您的 Web 开发模块** 添加到您的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="446ca-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="446ca-110">您可以通过添加或删除工作负载和 [组件文档来按照"修改Visual Studio中的步骤进行检查](/visualstudio/install/modify-visual-studio?view=vs-2019) 。</span><span class="sxs-lookup"><span data-stu-id="446ca-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019) documentation.</span></span>

![Visual Studio asp.net模块](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="446ca-112">如果希望通过从应用程序部署应用程序来测试 Visual Studio您的应用程序，则需要在 (Internet Information Services) 安装 IIS 应用程序。</span><span class="sxs-lookup"><span data-stu-id="446ca-112">If you would like test your app by deploy it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="446ca-113">Visual Studio不包含 IIS，并且未将其包含在默认的 Windows 10、Windows 8 或 Windows 7 配置中;但是，你可以从 Microsoft 下载中心 [下载最新版本](https://www.microsoft.com/download/details.aspx?id=48264)。</span><span class="sxs-lookup"><span data-stu-id="446ca-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![IIS 下载页面视图](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="446ca-115">安装 Teams Toolkit</span><span class="sxs-lookup"><span data-stu-id="446ca-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="446ca-116">Microsoft Teams Toolkit for Visual Studio可从 [Visual Studio Marketplace 下载或](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) 直接从 Visual Studio 中的" **扩展"** 菜单下载。</span><span class="sxs-lookup"><span data-stu-id="446ca-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="446ca-117">使用工具包</span><span class="sxs-lookup"><span data-stu-id="446ca-117">Using the toolkit</span></span>

- [<span data-ttu-id="446ca-118">设置新项目</span><span class="sxs-lookup"><span data-stu-id="446ca-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="446ca-119">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="446ca-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="446ca-120">打包应用</span><span class="sxs-lookup"><span data-stu-id="446ca-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="446ca-121">在 Teams 中运行应用</span><span class="sxs-lookup"><span data-stu-id="446ca-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="446ca-122">验证你的应用</span><span class="sxs-lookup"><span data-stu-id="446ca-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="446ca-123">发布应用</span><span class="sxs-lookup"><span data-stu-id="446ca-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="446ca-124">设置新的 Teams 项目</span><span class="sxs-lookup"><span data-stu-id="446ca-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="446ca-125">选择 **"创建新项目"。**</span><span class="sxs-lookup"><span data-stu-id="446ca-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="446ca-126">选择**Microsoft Teams 应用，然后选择**"下一**步"。**</span><span class="sxs-lookup"><span data-stu-id="446ca-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="446ca-127">你将会到达"配置**您的新建项目**"屏幕，你可以在其中选择**项目名称、\*\*\*\*位置和**解决方案**名称**。</span><span class="sxs-lookup"><span data-stu-id="446ca-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="446ca-128">选中标有文件夹 **的框，并在相同目录中标记为"放置解决方案"和项目**。</span><span class="sxs-lookup"><span data-stu-id="446ca-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="446ca-129">标记为"添加功能 **"的弹出** 窗口将允许你为项目设置选择一个或多个功能。</span><span class="sxs-lookup"><span data-stu-id="446ca-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="446ca-130">选择" **下一** 步"按钮以完成配置过程。</span><span class="sxs-lookup"><span data-stu-id="446ca-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="446ca-131">标记为"添加功能" **的弹出** 窗口将允许你为每个选定功能选择属性。</span><span class="sxs-lookup"><span data-stu-id="446ca-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="446ca-132">选择 **"** 完成"，然后登录 **Microsoft Teams Toolkit** 登录页面。</span><span class="sxs-lookup"><span data-stu-id="446ca-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="446ca-133">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="446ca-133">Configure your app</span></span>

<span data-ttu-id="446ca-134">Teams 应用从核心来托管三个组件：</span><span class="sxs-lookup"><span data-stu-id="446ca-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="446ca-135">Microsoft Teams 客户端可 (应用交互的) 应用或移动版应用程序。</span><span class="sxs-lookup"><span data-stu-id="446ca-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="446ca-136">响应将要在 Teams 中显示的内容请求的服务器，例如 HTML 选项卡内容或自动程序自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="446ca-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="446ca-137">一个 [包含三](/concepts/build-and-test/apps-package.md) 个文件的 Teams 应用包：</span><span class="sxs-lookup"><span data-stu-id="446ca-137">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="446ca-138">打开manifest.js打开</span><span class="sxs-lookup"><span data-stu-id="446ca-138">The manifest.json</span></span>
  > - <span data-ttu-id="446ca-139">要 [在公共](../resources/schema/manifest-schema.md#icons) 或组织应用程序目录中显示的应用的颜色图标</span><span class="sxs-lookup"><span data-stu-id="446ca-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="446ca-140">显示在[outline icon](../resources/schema/manifest-schema.md#icons) Teams 活动栏上的大纲图标。</span><span class="sxs-lookup"><span data-stu-id="446ca-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="446ca-141">安装应用后，Teams 客户端将分析清单文件，以确定所需的信息，如应用的名称和服务所在的 URL。</span><span class="sxs-lookup"><span data-stu-id="446ca-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="446ca-142">如果你尚未执行此操作，将需要登录 Microsoft 365 或帐户才能继续进行开发过程。</span><span class="sxs-lookup"><span data-stu-id="446ca-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="446ca-143">如果没有 Microsoft 365 帐户，可注册 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program) 订阅。</span><span class="sxs-lookup"><span data-stu-id="446ca-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="446ca-144">可以免 *费提供* 90 天，将不续续订，只要你将其用于开发活动。</span><span class="sxs-lookup"><span data-stu-id="446ca-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="446ca-145">如果你有新的Visual Studio *企业版* 或 *专业版* 订阅，这两种计划均包括免费的 Microsoft 365 [开发人员订阅](https://aka.ms/MyVisualStudioBenefits)，在生命周期订阅的Visual Studio活动。</span><span class="sxs-lookup"><span data-stu-id="446ca-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="446ca-146">*请参阅*[设置 Microsoft 365 开发人员订阅](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="446ca-146">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="446ca-147">配置步骤</span><span class="sxs-lookup"><span data-stu-id="446ca-147">Configuration steps</span></span>

1. <span data-ttu-id="446ca-148">若要配置应用，请在**Microsoft Teams 硬件硬件Toolkit，** 选择"编辑**应用包"。**</span><span class="sxs-lookup"><span data-stu-id="446ca-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package** .</span></span>
1. <span data-ttu-id="446ca-149">从"**我的环境"** 下拉菜单中，选择"**开发"。**</span><span class="sxs-lookup"><span data-stu-id="446ca-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="446ca-150">你将在"应用 **详细信息"** 页上编辑应用的属性字段。</span><span class="sxs-lookup"><span data-stu-id="446ca-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="446ca-151">编辑应用详细信息页中的字段会更新 manifest.json file 的内容，这些文件最终将作为应用包的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="446ca-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="446ca-152">了解更多</span><span class="sxs-lookup"><span data-stu-id="446ca-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="446ca-153">打包应用</span><span class="sxs-lookup"><span data-stu-id="446ca-153">Package your app</span></span>

<span data-ttu-id="446ca-154">修改应用**详细信息页面**或更新**清单，或**应用 **.publish**文件夹中的 **.env**文件将自动生成**Development.zip**文件。</span><span class="sxs-lookup"><span data-stu-id="446ca-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="446ca-155">该Development.zip文件包括三个必需的文件，**即manifest.js个**[和两个图标文件](../concepts/build-and-test/apps-package.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="446ca-155">The Development.zip file includes three required files — the **manifest.json** and [two icon files](../concepts/build-and-test/apps-package.md#icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="446ca-156">在本地安装和运行应用程序</span><span class="sxs-lookup"><span data-stu-id="446ca-156">Install and run your app locally</span></span>

1. <span data-ttu-id="446ca-157">从"**解决方案配置"下拉**菜单中，选择"**部署"。**</span><span class="sxs-lookup"><span data-stu-id="446ca-157">From the **Solution Configurations** dropdown menu, select **Deploy**.</span></span>

!["解决方案配置"菜单](../assets/images/solution-configurations.png)

2. <span data-ttu-id="446ca-159">选择 **"ISS 快速 + Teams"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="446ca-159">Select the **ISS Express + Teams** button.</span></span>

1. <span data-ttu-id="446ca-160">Teams 将启动，且应用安装对话框应出现在 Teams 客户端中。</span><span class="sxs-lookup"><span data-stu-id="446ca-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="446ca-161">验证你的应用</span><span class="sxs-lookup"><span data-stu-id="446ca-161">Validate your app</span></span>

<span data-ttu-id="446ca-162">" **验证** "页面允许你在将应用提交到 AppSource 前检查应用包。</span><span class="sxs-lookup"><span data-stu-id="446ca-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="446ca-163">只需上载清单包，验证工具即可针对所有与清单相关的测试用例检查您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="446ca-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="446ca-164">对于每个失败的测试，说明会提供一个可帮助您修复错误的文档链接。</span><span class="sxs-lookup"><span data-stu-id="446ca-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="446ca-165">对于难以自动化的测试， **最常见的失败** 测试用例的初步检查表详细信息 7 以及指向完整提交清单的链接。</span><span class="sxs-lookup"><span data-stu-id="446ca-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="446ca-166">将应用发布到 Teams</span><span class="sxs-lookup"><span data-stu-id="446ca-166">Publish your app to Teams</span></span>

<span data-ttu-id="446ca-167">✔在项目主页上，可将应用上传到团队、为公司用户将应用提交到公司自定义应用商店，也可以针对所有 Teams 用户将应用提交到 App Source。</span><span class="sxs-lookup"><span data-stu-id="446ca-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="446ca-168">✔ IT 管理员会查看这些提交。</span><span class="sxs-lookup"><span data-stu-id="446ca-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="446ca-169">✔可以返回到" **发布"** 页面检查提交状态，并了解应用是否由 IT 管理员批准或拒绝。这也是将向应用提交更新或取消任何当前活动提交的地点。</span><span class="sxs-lookup"><span data-stu-id="446ca-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="446ca-170">下一步：维护和支持已发布的应用</span><span class="sxs-lookup"><span data-stu-id="446ca-170">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
