---
title: 使用 Microsoft 团队工具包和 Visual Studio 生成应用程序
description: 开始在 Visual Studio 中使用 Microsoft 团队工具包直接构建强大的自定义应用程序
keywords: 团队 visual studio 工具包
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 5ba3cd8b5714876a96595aec295ff6d0066e115f
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2020
ms.locfileid: "49476984"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="49518-104">使用团队工具包和 Visual Studio 生成应用程序</span><span class="sxs-lookup"><span data-stu-id="49518-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="49518-105">Microsoft 团队工具包使您能够在 Visual Studio 集成开发环境 (IDE) 中直接创建自定义团队应用。</span><span class="sxs-lookup"><span data-stu-id="49518-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="49518-106">Microsoft 团队工具包将引导您完成此过程，并提供生成、调试和启动团队应用所需的所有内容。</span><span class="sxs-lookup"><span data-stu-id="49518-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49518-107">先决条件</span><span class="sxs-lookup"><span data-stu-id="49518-107">Prerequisites</span></span>

1. [<span data-ttu-id="49518-108">启用开发人员预览</span><span class="sxs-lookup"><span data-stu-id="49518-108">Enable developer preview</span></span>](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. <span data-ttu-id="49518-109">请确保已将 **<span>ASP.NE</span>T 和 web 开发模块** 添加到 Visual Studio 实例中。</span><span class="sxs-lookup"><span data-stu-id="49518-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="49518-110">您可以通过 [添加或删除工作负荷和组件文档，按照 Modify Visual Studio](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) 中的步骤进行检查。</span><span class="sxs-lookup"><span data-stu-id="49518-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![visual studio asp.net 模块](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="49518-112">如果您想要通过从 Visual Studio 部署应用程序来测试您的应用程序，您需要在开发环境中安装 IIS (Internet 信息服务) 。</span><span class="sxs-lookup"><span data-stu-id="49518-112">If you would like test your app by deploy it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="49518-113">Visual Studio 不包含 IIS，它不包含在默认的 Windows 10、Windows 8 或 Windows 7 配置中;但是，可以从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=48264)下载最新版本。</span><span class="sxs-lookup"><span data-stu-id="49518-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![IIS 下载页面视图](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="49518-115">安装团队工具包</span><span class="sxs-lookup"><span data-stu-id="49518-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="49518-116">Visual studio 的 Microsoft 团队工具包可从 [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) 下载，也可直接从 visual studio 中的 " **扩展** " 菜单下载。</span><span class="sxs-lookup"><span data-stu-id="49518-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="49518-117">使用工具包</span><span class="sxs-lookup"><span data-stu-id="49518-117">Using the toolkit</span></span>

- [<span data-ttu-id="49518-118">设置新项目</span><span class="sxs-lookup"><span data-stu-id="49518-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="49518-119">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="49518-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="49518-120">打包应用程序</span><span class="sxs-lookup"><span data-stu-id="49518-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="49518-121">在团队中运行应用程序</span><span class="sxs-lookup"><span data-stu-id="49518-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="49518-122">验证您的应用程序</span><span class="sxs-lookup"><span data-stu-id="49518-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="49518-123">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="49518-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="49518-124">设置新的团队项目</span><span class="sxs-lookup"><span data-stu-id="49518-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="49518-125">选择 " **新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="49518-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="49518-126">选择 " **Microsoft 团队应用** "，然后选择 " **下一步**"。</span><span class="sxs-lookup"><span data-stu-id="49518-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="49518-127">您将收到 " **配置新项目** " 屏幕，您可在其中选择 **项目名称**、 **位置** 和 **解决方案名称**。</span><span class="sxs-lookup"><span data-stu-id="49518-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="49518-128">选中标记 " **将解决方案和项目放在同一目录中**" 的框。</span><span class="sxs-lookup"><span data-stu-id="49518-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="49518-129">标有 " **添加功能** " 的弹出窗口将允许您为项目设置选择一个或多个功能。</span><span class="sxs-lookup"><span data-stu-id="49518-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="49518-130">选择 " **下一步** " 按钮完成配置过程。</span><span class="sxs-lookup"><span data-stu-id="49518-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="49518-131">标有 " **添加功能** " 的弹出窗口将允许您为每个选定的功能选择属性。</span><span class="sxs-lookup"><span data-stu-id="49518-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="49518-132">选择 " **完成** "，你将在 **Microsoft 团队工具包** 登录页上进行土地。</span><span class="sxs-lookup"><span data-stu-id="49518-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="49518-133">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="49518-133">Configure your app</span></span>

<span data-ttu-id="49518-134">在其核心中，团队应用程序包含三个组件：</span><span class="sxs-lookup"><span data-stu-id="49518-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="49518-135">Microsoft 团队客户端 (web、桌面或移动) ，用户与您的应用程序进行交互。</span><span class="sxs-lookup"><span data-stu-id="49518-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="49518-136">对将在团队中显示的内容请求做出响应的服务器，例如，HTML 选项卡内容或 bot 自适应卡。</span><span class="sxs-lookup"><span data-stu-id="49518-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="49518-137">由三个文件组成的团队 [应用程序包](/concepts/build-and-test/apps-package.md) ：</span><span class="sxs-lookup"><span data-stu-id="49518-137">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="49518-138">上的 manifest.js</span><span class="sxs-lookup"><span data-stu-id="49518-138">The manifest.json</span></span>
  > - <span data-ttu-id="49518-139">显示在公用或组织应用程序目录中的应用程序的[彩色图标](../resources/schema/manifest-schema.md#icons)</span><span class="sxs-lookup"><span data-stu-id="49518-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="49518-140">"团队" 活动栏中显示的 [大纲图标](../resources/schema/manifest-schema.md#icons) 。</span><span class="sxs-lookup"><span data-stu-id="49518-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="49518-141">在安装应用程序时，团队客户端会分析清单文件以确定所需的信息，如应用程序的名称和服务所在的 URL。</span><span class="sxs-lookup"><span data-stu-id="49518-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="49518-142">如果尚未执行此操作，则需要登录到 Microsoft 365 或帐户，才能继续执行开发过程。</span><span class="sxs-lookup"><span data-stu-id="49518-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="49518-143">如果你没有 Microsoft 365 帐户，你可以注册 [microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program) 订阅。</span><span class="sxs-lookup"><span data-stu-id="49518-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="49518-144">它在90天内 *免费* 使用，并且将持续更新，只要你将其用于开发活动即可。</span><span class="sxs-lookup"><span data-stu-id="49518-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="49518-145">如果你有 Visual Studio *Enterprise* 或 *专业版* 订阅，这两个程序都包括一个免费的 Microsoft 365 [开发人员订阅](https://aka.ms/MyVisualStudioBenefits)，在 Visual Studio 订阅的生命周期内处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="49518-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="49518-146">*请参阅*[设置 Microsoft 365 开发人员订阅](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="49518-146">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="49518-147">配置步骤</span><span class="sxs-lookup"><span data-stu-id="49518-147">Configuration steps</span></span>

1. <span data-ttu-id="49518-148">若要配置应用程序，请在 " **Microsoft 团队工具包** " 登录页上，选择 " **编辑应用程序包** "。</span><span class="sxs-lookup"><span data-stu-id="49518-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package** .</span></span>
1. <span data-ttu-id="49518-149">从 " **我的环境** " 下拉菜单中，选择 " **开发**"。</span><span class="sxs-lookup"><span data-stu-id="49518-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="49518-150">您将在 " **应用程序详细信息** " 页上放置，您可以在其中编辑应用程序的属性字段。</span><span class="sxs-lookup"><span data-stu-id="49518-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="49518-151">编辑应用程序详细信息页中的字段将更新作为应用程序包一部分最终交付的文件上的 manifest.js的内容。</span><span class="sxs-lookup"><span data-stu-id="49518-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="49518-152">了解更多</span><span class="sxs-lookup"><span data-stu-id="49518-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="49518-153">打包应用程序</span><span class="sxs-lookup"><span data-stu-id="49518-153">Package your app</span></span>

<span data-ttu-id="49518-154">修改 **应用程序详细信息** 页或更新 **清单**，或应用程序的 **. publish** 文件夹中的 **env** 文件将自动生成 **Development.zip** 文件。</span><span class="sxs-lookup"><span data-stu-id="49518-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="49518-155">Development.zip 文件包括三个所需的文件，即 **manifest.js打开** 和 [两个图标文件](../concepts/build-and-test/apps-package.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="49518-155">The Development.zip file includes three required files — the **manifest.json** and [two icon files](../concepts/build-and-test/apps-package.md#icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="49518-156">在本地安装和运行应用程序</span><span class="sxs-lookup"><span data-stu-id="49518-156">Install and run your app locally</span></span>

1. <span data-ttu-id="49518-157">从 " **解决方案配置** " 下拉菜单中选择 " **部署**"。</span><span class="sxs-lookup"><span data-stu-id="49518-157">From the **Solution Configurations** dropdown menu, select **Deploy**.</span></span>

![解决方案配置菜单](../assets/images/solution-configurations.png)

2. <span data-ttu-id="49518-159">选择 " **ISS Express + 团队** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="49518-159">Select the **ISS Express + Teams** button.</span></span>

1. <span data-ttu-id="49518-160">团队将启动，并且应用程序安装对话框应显示在团队客户端中。</span><span class="sxs-lookup"><span data-stu-id="49518-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="49518-161">验证您的应用程序</span><span class="sxs-lookup"><span data-stu-id="49518-161">Validate your app</span></span>

<span data-ttu-id="49518-162">通过 " **验证** " 页面，您可以在将应用程序提交到 AppSource 之前检查应用程序包。</span><span class="sxs-lookup"><span data-stu-id="49518-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="49518-163">只需上传清单包，验证工具就会检查应用程序是否符合所有与清单相关的测试用例。</span><span class="sxs-lookup"><span data-stu-id="49518-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="49518-164">对于每个失败的测试，说明提供的文档链接可帮助您修复错误。</span><span class="sxs-lookup"><span data-stu-id="49518-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="49518-165">对于难以自动化的测试， **初步清单** 详细说明了最常见的失败测试事例的7，以及指向完整提交核对清单的链接。</span><span class="sxs-lookup"><span data-stu-id="49518-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="49518-166">将您的应用程序发布到团队</span><span class="sxs-lookup"><span data-stu-id="49518-166">Publish your app to Teams</span></span>

<span data-ttu-id="49518-167">✔在项目主页上，您可以将应用程序上载到团队，将您的应用程序提交到贵组织中用户的公司自定义应用商店，或将应用程序提交到所有团队用户的应用程序源。</span><span class="sxs-lookup"><span data-stu-id="49518-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="49518-168">✔你的 IT 管理员将查看这些提交。</span><span class="sxs-lookup"><span data-stu-id="49518-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="49518-169">✔您可以返回到 " **发布** " 页面以检查提交状态，并了解您的应用程序是否已由 IT 管理员批准或拒绝。此外，您还可以将更新提交到您的应用程序或取消任何当前活动的提交。</span><span class="sxs-lookup"><span data-stu-id="49518-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="49518-170">下一步：维护和支持发布的应用程序</span><span class="sxs-lookup"><span data-stu-id="49518-170">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
