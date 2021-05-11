---
title: 使用 Microsoft Teams Toolkit 和 Visual Studio
description: 开始使用自定义工具直接在Visual Studio生成出色的自定义Microsoft Teams Toolkit
keywords: teams visual studio 工具包
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: bf8250e42bdf96073d729a19e921c400f242c67a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020251"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="4be21-104">使用 Teams Toolkit 和 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4be21-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="4be21-105">借助 Microsoft Teams 工具包，可以直接在 Visual Studio 集成开发环境（IDE）中创建自定义 Teams 应用程序。</span><span class="sxs-lookup"><span data-stu-id="4be21-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="4be21-106">Microsoft Teams 工具包将引导你完成整个过程，并提供构建、调试和启动 Teams 应用所需的一切资源。</span><span class="sxs-lookup"><span data-stu-id="4be21-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4be21-107">先决条件</span><span class="sxs-lookup"><span data-stu-id="4be21-107">Prerequisites</span></span>

1. [<span data-ttu-id="4be21-108">启用开发人员预览</span><span class="sxs-lookup"><span data-stu-id="4be21-108">Enable developer preview</span></span>](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. <span data-ttu-id="4be21-109">确保已 ASP.NE **<span></span>T** 和 Web 开发模块添加到Visual Studio实例。</span><span class="sxs-lookup"><span data-stu-id="4be21-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="4be21-110">通过添加或删除工作负载和组件[文档，可以按照修改Visual Studio中的步骤进行](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)检查。</span><span class="sxs-lookup"><span data-stu-id="4be21-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![visual studio asp.net 模块](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="4be21-112">如果你想要通过从应用程序部署应用来Visual Studio，则需要在开发环境中 (Internet Information Services) IIS 应用程序。</span><span class="sxs-lookup"><span data-stu-id="4be21-112">If you would like test your app by deploying it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="4be21-113">Visual Studio不包括 IIS，并且它不包含在默认 Windows 10、Windows 8 或 Windows 7 配置中;但是，你可以从 Microsoft 下载中心[下载最新版本](https://www.microsoft.com/download/details.aspx?id=48264)。</span><span class="sxs-lookup"><span data-stu-id="4be21-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![IIS 下载页面视图](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="4be21-115">安装Teams Toolkit</span><span class="sxs-lookup"><span data-stu-id="4be21-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="4be21-116">可以从 Microsoft Teams Toolkit Visual Studio 应用商店或直接从 Visual Studio[内的](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate)"扩展"菜单中下载Visual Studio。 </span><span class="sxs-lookup"><span data-stu-id="4be21-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="4be21-117">使用工具包</span><span class="sxs-lookup"><span data-stu-id="4be21-117">Using the toolkit</span></span>

- [<span data-ttu-id="4be21-118">设置新项目</span><span class="sxs-lookup"><span data-stu-id="4be21-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="4be21-119">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="4be21-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="4be21-120">打包应用</span><span class="sxs-lookup"><span data-stu-id="4be21-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="4be21-121">在应用商店中Teams</span><span class="sxs-lookup"><span data-stu-id="4be21-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="4be21-122">验证你的应用</span><span class="sxs-lookup"><span data-stu-id="4be21-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="4be21-123">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="4be21-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="4be21-124">设置新的Teams项目</span><span class="sxs-lookup"><span data-stu-id="4be21-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="4be21-125">选择 **创建新项目**。</span><span class="sxs-lookup"><span data-stu-id="4be21-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="4be21-126">选择 **Microsoft Teams应用**"，然后选择"下一 **步"。**</span><span class="sxs-lookup"><span data-stu-id="4be21-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="4be21-127">你将到达 **配置新项目屏幕**，可在其中选择Project **名称\*\*\*\*、位置** 和 **解决方案名称**。</span><span class="sxs-lookup"><span data-stu-id="4be21-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="4be21-128">选中标记为"将解决方案 **和项目放置在同一目录中"的框**。</span><span class="sxs-lookup"><span data-stu-id="4be21-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="4be21-129">标记为"添加功能"的弹出窗口将允许你为项目设置选择一个或多个功能。</span><span class="sxs-lookup"><span data-stu-id="4be21-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="4be21-130">选择" **下一** 步"按钮以完成配置过程。</span><span class="sxs-lookup"><span data-stu-id="4be21-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="4be21-131">标记为"添加功能"的弹出窗口将允许你选择每个选定功能的属性。</span><span class="sxs-lookup"><span data-stu-id="4be21-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="4be21-132">选择 **"完成**"，你将 **登录Microsoft Teams Toolkit登录** 页面。</span><span class="sxs-lookup"><span data-stu-id="4be21-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="4be21-133">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="4be21-133">Configure your app</span></span>

<span data-ttu-id="4be21-134">应用程序的核心是Teams三个组件：</span><span class="sxs-lookup"><span data-stu-id="4be21-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="4be21-135">The Microsoft Teams client (web， desktop or mobile) where users interact with your app.</span><span class="sxs-lookup"><span data-stu-id="4be21-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="4be21-136">响应将在应用程序中显示的内容请求的服务器，Teams HTML 选项卡内容或自动程序自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="4be21-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="4be21-137">一Teams[文件](/concepts/build-and-test/apps-package.md)组成的应用包：</span><span class="sxs-lookup"><span data-stu-id="4be21-137">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="4be21-138">打开manifest.js</span><span class="sxs-lookup"><span data-stu-id="4be21-138">The manifest.json</span></span>
  > - <span data-ttu-id="4be21-139">[要显示在](../resources/schema/manifest-schema.md#icons)公共或组织应用程序目录中的应用的颜色图标</span><span class="sxs-lookup"><span data-stu-id="4be21-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="4be21-140">显示在[活动](../resources/schema/manifest-schema.md#icons)栏上的Teams图标。</span><span class="sxs-lookup"><span data-stu-id="4be21-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="4be21-141">安装应用后，Teams客户端将分析清单文件以确定所需信息，如应用名称和服务所在的 URL。</span><span class="sxs-lookup"><span data-stu-id="4be21-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="4be21-142">如果尚未登录，则需要登录帐户或帐户Microsoft 365继续开发过程。</span><span class="sxs-lookup"><span data-stu-id="4be21-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="4be21-143">如果你没有帐户，Microsoft 365注册开发人员计划[Microsoft 365订阅。](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="4be21-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="4be21-144">它 *是免费的* 90 天，并且将持续续订，只要你使用它进行开发活动。</span><span class="sxs-lookup"><span data-stu-id="4be21-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="4be21-145">如果你有一个 Visual Studio *Enterprise* 或 *Professional* 订阅，这两个计划均包括免费 Microsoft 365 [开发人员](https://aka.ms/MyVisualStudioBenefits)订阅，在订阅生命周期内Visual Studio有效。</span><span class="sxs-lookup"><span data-stu-id="4be21-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="4be21-146">*请参阅*[设置开发人员Microsoft 365订阅](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="4be21-146">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="4be21-147">配置步骤</span><span class="sxs-lookup"><span data-stu-id="4be21-147">Configuration steps</span></span>

1. <span data-ttu-id="4be21-148">若要配置你的应用，请在 **登录Microsoft Teams Toolkit，** 选择"编辑 **应用包"。**</span><span class="sxs-lookup"><span data-stu-id="4be21-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package** .</span></span>
1. <span data-ttu-id="4be21-149">从"**我的环境"** 下拉菜单中，选择"开发 **"。**</span><span class="sxs-lookup"><span data-stu-id="4be21-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="4be21-150">你将登录" **应用详细信息** "页面，可在其中编辑应用的属性字段。</span><span class="sxs-lookup"><span data-stu-id="4be21-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="4be21-151">编辑"应用详细信息"页中的字段将更新manifest.js文件（最终作为应用包的一部分提供）上的内容。</span><span class="sxs-lookup"><span data-stu-id="4be21-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="4be21-152">了解更多</span><span class="sxs-lookup"><span data-stu-id="4be21-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="4be21-153">打包应用</span><span class="sxs-lookup"><span data-stu-id="4be21-153">Package your app</span></span>

<span data-ttu-id="4be21-154">修改 **应用程序详细信息** 页面或更新清单或应用的.publish 文件夹中的 **.env** 文件 **将** 自动生成Development.zip文件。</span><span class="sxs-lookup"><span data-stu-id="4be21-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="4be21-155">The Development.zip file includes three required files — the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="4be21-155">The Development.zip file includes three required files — the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="4be21-156">在本地安装和运行应用</span><span class="sxs-lookup"><span data-stu-id="4be21-156">Install and run your app locally</span></span>

1. <span data-ttu-id="4be21-157">从"**解决方案配置"** 下拉菜单中，选择"部署 **"。**</span><span class="sxs-lookup"><span data-stu-id="4be21-157">From the **Solution Configurations** dropdown menu, select **Deploy**.</span></span>

!["解决方案配置"菜单](../assets/images/solution-configurations.png)

2. <span data-ttu-id="4be21-159">选择 **"IIS Express + Teams"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="4be21-159">Select the **IIS Express + Teams** button.</span></span>

1. <span data-ttu-id="4be21-160">Teams将启动，并且应用安装对话应显示在 Teams 客户端中。</span><span class="sxs-lookup"><span data-stu-id="4be21-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="4be21-161">验证你的应用</span><span class="sxs-lookup"><span data-stu-id="4be21-161">Validate your app</span></span>

<span data-ttu-id="4be21-162">" **验证** "页允许你在将应用提交到 AppSource 之前检查应用包。</span><span class="sxs-lookup"><span data-stu-id="4be21-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="4be21-163">只需上传清单包，验证工具将针对所有与清单相关的测试用例检查你的应用。</span><span class="sxs-lookup"><span data-stu-id="4be21-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="4be21-164">对于每个失败的测试，该说明都提供了一个文档链接，帮助您修复错误。</span><span class="sxs-lookup"><span data-stu-id="4be21-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="4be21-165">对于难以自动执行的测试，"初步检查表"详细介绍了最常见的失败测试用例 7，并链接到完整的提交清单。</span><span class="sxs-lookup"><span data-stu-id="4be21-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="4be21-166">将应用发布到 Teams</span><span class="sxs-lookup"><span data-stu-id="4be21-166">Publish your app to Teams</span></span>

<span data-ttu-id="4be21-167">✔在项目主页上，可以将应用上传到团队，将应用提交到公司自定义应用商店供组织用户使用，或将应用提交到所有 Teams 用户的应用源。</span><span class="sxs-lookup"><span data-stu-id="4be21-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="4be21-168">✔ IT 管理员将查看这些提交。</span><span class="sxs-lookup"><span data-stu-id="4be21-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="4be21-169">✔你可以返回到"发布"页面，检查提交状态并了解你的应用是否已被 IT 管理员批准或拒绝。这也是你向应用提交更新或取消任何当前处于活动状态的提交的地方。</span><span class="sxs-lookup"><span data-stu-id="4be21-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4be21-170">下一步：维护和支持已发布的应用</span><span class="sxs-lookup"><span data-stu-id="4be21-170">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
