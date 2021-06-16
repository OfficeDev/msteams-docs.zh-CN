---
title: 使用 Teams Toolkit 和 Visual Studio
description: 开始使用自定义工具直接在Visual Studio生成出色的自定义Microsoft Teams Toolkit
keywords: teams visual studio 工具包
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 996037f5bb1caaa2493e1eebe51039724822fef9
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949697"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="bfac2-104">使用 Teams Toolkit 和 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bfac2-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="bfac2-105">借助 Microsoft Teams 工具包，可以直接在 Visual Studio 集成开发环境（IDE）中创建自定义 Teams 应用程序。</span><span class="sxs-lookup"><span data-stu-id="bfac2-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="bfac2-106">Microsoft Teams 工具包将引导你完成整个过程，并提供构建、调试和启动 Teams 应用所需的一切资源。</span><span class="sxs-lookup"><span data-stu-id="bfac2-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfac2-107">先决条件</span><span class="sxs-lookup"><span data-stu-id="bfac2-107">Prerequisites</span></span>

1. <span data-ttu-id="bfac2-108">[启用开发人员预览](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)。</span><span class="sxs-lookup"><span data-stu-id="bfac2-108">[Enable developer preview](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span></span>

1. <span data-ttu-id="bfac2-109">确保已 ASP.NE **<span></span>T** 和 Web 开发模块添加到Visual Studio实例。</span><span class="sxs-lookup"><span data-stu-id="bfac2-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="bfac2-110">通过添加或删除工作负载和组件文档，可以按照Visual Studio中的[步骤进行](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)检查。</span><span class="sxs-lookup"><span data-stu-id="bfac2-110">You can check by following the steps in the [modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![Visual studio asp.net 模块](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="bfac2-112">如果要通过从应用程序部署应用来测试Visual Studio，则必须在Internet Information Services (环境中) ) IIS 应用程序。</span><span class="sxs-lookup"><span data-stu-id="bfac2-112">If you want to test your app by deploying it from Visual Studio, you must have Internet Information Services (IIS)) installed in your development environment.</span></span> <span data-ttu-id="bfac2-113">Visual Studio IIS，并且它不包含在默认 Windows 10、Windows 8 或 Windows 7 配置中;但是，你可以从 Microsoft 下载中心[下载最新版本](https://www.microsoft.com/download/details.aspx?id=48264)。</span><span class="sxs-lookup"><span data-stu-id="bfac2-113">Visual Studio does not include IIS and it is not included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![IIS 下载页面视图](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="bfac2-115">安装Teams Toolkit</span><span class="sxs-lookup"><span data-stu-id="bfac2-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="bfac2-116">可以从 Microsoft Teams Toolkit Visual Studio 应用商店或直接从 Visual Studio[内的](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate)"扩展"菜单中下载Visual Studio。 </span><span class="sxs-lookup"><span data-stu-id="bfac2-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span> <span data-ttu-id="bfac2-117">从 Visual Studio Marketplace 下载[Teams Toolkit for Visual Studio 2019。](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit)</span><span class="sxs-lookup"><span data-stu-id="bfac2-117">From the Visual Studio Marketplace also download [Teams Toolkit for Visual Studio 2019](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit).</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="bfac2-118">使用工具包</span><span class="sxs-lookup"><span data-stu-id="bfac2-118">Using the toolkit</span></span>

- [<span data-ttu-id="bfac2-119">设置新项目</span><span class="sxs-lookup"><span data-stu-id="bfac2-119">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="bfac2-120">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="bfac2-120">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="bfac2-121">打包应用</span><span class="sxs-lookup"><span data-stu-id="bfac2-121">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="bfac2-122">在客户端安装并运行Teams</span><span class="sxs-lookup"><span data-stu-id="bfac2-122">Install and run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="bfac2-123">验证你的应用</span><span class="sxs-lookup"><span data-stu-id="bfac2-123">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="bfac2-124">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="bfac2-124">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="bfac2-125">设置新的Teams项目</span><span class="sxs-lookup"><span data-stu-id="bfac2-125">Set up a new Teams project</span></span>

![Teams工具包](../assets/images/teamstoolkiticon.png)

1. <span data-ttu-id="bfac2-127">选择 **创建新项目**。</span><span class="sxs-lookup"><span data-stu-id="bfac2-127">Select **Create New Project**.</span></span>

    ![新建项目](../assets/images/createnewproject.png)

1. <span data-ttu-id="bfac2-129">选择适用于应用的快速 **入门工具Microsoft Teams下** 一 **步"。**</span><span class="sxs-lookup"><span data-stu-id="bfac2-129">Choose the quickstart tool for **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="bfac2-130">在"**配置新项目"** 页中，Project **名称、\*\*\*\*位置** 和 **解决方案名称**。</span><span class="sxs-lookup"><span data-stu-id="bfac2-130">In the **Configure your new project** page, enter the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="bfac2-131">选中" **将解决方案和项目放置在同一目录中"** 复选框。</span><span class="sxs-lookup"><span data-stu-id="bfac2-131">Select the **Place solution and project in the same directory** checkbox.</span></span>
1. <span data-ttu-id="bfac2-132">在 **"添加功能** "弹出窗口中，为项目设置选择一个或多个功能。</span><span class="sxs-lookup"><span data-stu-id="bfac2-132">In the **Add Capabilities** pop-up window, choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="bfac2-133">选择" **下一** 步"按钮以完成配置过程。</span><span class="sxs-lookup"><span data-stu-id="bfac2-133">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="bfac2-134">在 **"添加功能** "弹出窗口中，选择每个选定功能的属性。</span><span class="sxs-lookup"><span data-stu-id="bfac2-134">In the **Add Capabilities** pop-up window, choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="bfac2-135">选择 **“完成”**。</span><span class="sxs-lookup"><span data-stu-id="bfac2-135">Select **Finish**.</span></span> <span data-ttu-id="bfac2-136">将显示 **Microsoft Teams Toolkit** 登录页面。</span><span class="sxs-lookup"><span data-stu-id="bfac2-136">The **Microsoft Teams Toolkit** landing page is shown.</span></span>

    ![Teams工具包登录页面](../assets/images/Teamstoolkitpage.png)

## <a name="configure-your-app"></a><span data-ttu-id="bfac2-138">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="bfac2-138">Configure your app</span></span>

<span data-ttu-id="bfac2-139">应用程序的核心是Teams三个组件：</span><span class="sxs-lookup"><span data-stu-id="bfac2-139">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="bfac2-140">用户Microsoft Teams应用的客户端（包括 Web、桌面或移动）。</span><span class="sxs-lookup"><span data-stu-id="bfac2-140">The Microsoft Teams client including web, desktop, or mobile, where users interact with your app.</span></span>
  1. <span data-ttu-id="bfac2-141">响应对内容请求的服务器，Teams HTML 选项卡内容或自动程序自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="bfac2-141">A server that responds to requests for content that is displayed in Teams, for example, HTML tab content or a bot adaptive card.</span></span>
  1. <span data-ttu-id="bfac2-142">应用Teams包包含三个文件：</span><span class="sxs-lookup"><span data-stu-id="bfac2-142">A Teams app package consists of three files:</span></span>

      - <span data-ttu-id="bfac2-143">打开manifest.js</span><span class="sxs-lookup"><span data-stu-id="bfac2-143">The manifest.json</span></span>
      - <span data-ttu-id="bfac2-144">要 [显示在](../resources/schema/manifest-schema.md#icons) 公共或组织应用程序目录中的应用的颜色图标。</span><span class="sxs-lookup"><span data-stu-id="bfac2-144">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
      - <span data-ttu-id="bfac2-145">显示在[活动](../resources/schema/manifest-schema.md#icons)栏上的Teams图标。</span><span class="sxs-lookup"><span data-stu-id="bfac2-145">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="bfac2-146">安装应用后，Teams客户端将分析清单文件以确定所需信息，如应用名称和服务所在的 URL。</span><span class="sxs-lookup"><span data-stu-id="bfac2-146">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="bfac2-147">如果尚未登录，则必须登录到 Microsoft 365 帐户，以继续进行开发过程。</span><span class="sxs-lookup"><span data-stu-id="bfac2-147">If you have not done so already, you must sign in to your Microsoft 365 account to continue with the development process.</span></span>
>
> <span data-ttu-id="bfac2-148">如果你没有帐户，Microsoft 365注册开发人员计划[Microsoft 365订阅。](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="bfac2-148">If you do not have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="bfac2-149">它是免费的 90 天，只要你使用它进行开发活动，它将续订。</span><span class="sxs-lookup"><span data-stu-id="bfac2-149">It's free for 90 days and renews as long as you are using it for development activity.</span></span> <span data-ttu-id="bfac2-150">如果你有一个 Visual Studio Enterprise 或 Professional 订阅，这两个计划均Microsoft 365[免费](https://aka.ms/MyVisualStudioBenefits)开发人员订阅，在订阅生命周期内Visual Studio有效。</span><span class="sxs-lookup"><span data-stu-id="bfac2-150">If you have a Visual Studio Enterprise or Professional subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="bfac2-151">有关详细信息，请参阅[设置开发人员Microsoft 365订阅](/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="bfac2-151">For more information, see [set up a Microsoft 365 developer subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="bfac2-152">配置步骤</span><span class="sxs-lookup"><span data-stu-id="bfac2-152">Configuration steps</span></span>

1. <span data-ttu-id="bfac2-153">若要配置你的应用，请在 **登录Microsoft Teams Toolkit，** 选择"编辑 **应用包"。**</span><span class="sxs-lookup"><span data-stu-id="bfac2-153">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package**.</span></span>
1. <span data-ttu-id="bfac2-154">从"**我的环境"** 下拉菜单中，选择"开发 **"。**</span><span class="sxs-lookup"><span data-stu-id="bfac2-154">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="bfac2-155">在 **"应用详细信息** "页中，编辑应用的属性字段。</span><span class="sxs-lookup"><span data-stu-id="bfac2-155">In the **App details** page, edit your app's property fields.</span></span>
    
    <span data-ttu-id="bfac2-156">编辑"应用详细信息"页中的字段将更新应用程序manifest.js中将作为应用包的一部分提供的文件上的内容。</span><span class="sxs-lookup"><span data-stu-id="bfac2-156">Editing the fields in the App details page updates the contents of the manifest.json file that will ship as part of the app package.</span></span> <span data-ttu-id="bfac2-157">有关详细信息，请参阅Teams Toolkit[清单](https://aka.ms/teams-toolkit-manifest)。</span><span class="sxs-lookup"><span data-stu-id="bfac2-157">For more information, see [Teams Toolkit manifest](https://aka.ms/teams-toolkit-manifest).</span></span>

## <a name="package-your-app"></a><span data-ttu-id="bfac2-158">打包应用</span><span class="sxs-lookup"><span data-stu-id="bfac2-158">Package your app</span></span>

<span data-ttu-id="bfac2-159">修改 **应用程序详细信息** 页面或更新清单或应用的.publish 文件夹中的 **.env** 文件 **将** 自动生成Development.zip文件。</span><span class="sxs-lookup"><span data-stu-id="bfac2-159">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="bfac2-160">the Development.zip file includes three required files， the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="bfac2-160">The Development.zip file includes three required files, the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="bfac2-161">在本地安装和运行应用</span><span class="sxs-lookup"><span data-stu-id="bfac2-161">Install and run your app locally</span></span>

1. <span data-ttu-id="bfac2-162">从" **解决方案配置"** 下拉菜单中 **，选择"** 部署"，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="bfac2-162">From the **Solution Configurations** dropdown menu, select **Deploy** as shown in the following image:</span></span>

    !["解决方案配置"菜单](../assets/images/solution-configurations.png)

1. <span data-ttu-id="bfac2-164">选择 **"IIS Express + Teams"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="bfac2-164">Select the **IIS Express + Teams** button.</span></span>

    <span data-ttu-id="bfac2-165">应用程序安装对话框将显示在客户端Teams中。</span><span class="sxs-lookup"><span data-stu-id="bfac2-165">The app installation dialog box appears in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="bfac2-166">验证你的应用</span><span class="sxs-lookup"><span data-stu-id="bfac2-166">Validate your app</span></span>

<span data-ttu-id="bfac2-167">" **验证** "页允许你在将应用提交到 AppSource 之前检查应用包。</span><span class="sxs-lookup"><span data-stu-id="bfac2-167">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="bfac2-168">只需上传清单包，验证工具将针对所有与清单相关的测试用例检查你的应用。</span><span class="sxs-lookup"><span data-stu-id="bfac2-168">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="bfac2-169">对于每个失败的测试，该说明都提供了一个文档链接，帮助您修复错误。</span><span class="sxs-lookup"><span data-stu-id="bfac2-169">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="bfac2-170">对于难以自动执行的测试，"初步检查表"详细介绍了最常见的失败测试用例 7，并链接到完整的提交清单。</span><span class="sxs-lookup"><span data-stu-id="bfac2-170">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="bfac2-171">将应用发布到 Teams</span><span class="sxs-lookup"><span data-stu-id="bfac2-171">Publish your app to Teams</span></span>

* <span data-ttu-id="bfac2-172">在项目主页上，你可以将应用上载到团队、将应用提交到公司自定义应用商店供你组织的用户使用，或将应用提交到所有 Teams 用户的应用源。</span><span class="sxs-lookup"><span data-stu-id="bfac2-172">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

* <span data-ttu-id="bfac2-173">IT 管理员将审阅这些提交。</span><span class="sxs-lookup"><span data-stu-id="bfac2-173">Your IT admin will review these submissions.</span></span>

* <span data-ttu-id="bfac2-174">你可以返回到发布 **页面** ，检查你的提交状态，并了解你的应用是否已被 IT 管理员批准或拒绝。这同样也是你可以向应用提交更新或取消任何当前处于活动状态的提交的地方。</span><span class="sxs-lookup"><span data-stu-id="bfac2-174">You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you can submit updates to your app or cancel any currently active submissions.</span></span>

## <a name="next-step"></a><span data-ttu-id="bfac2-175">后续步骤</span><span class="sxs-lookup"><span data-stu-id="bfac2-175">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bfac2-176">维护和支持已发布的应用</span><span class="sxs-lookup"><span data-stu-id="bfac2-176">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
