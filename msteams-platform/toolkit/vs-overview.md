---
title: 使用 Microsoft 团队工具包和 Visual Studio 生成应用程序
description: 开始在 Visual Studio 中使用 Microsoft 团队工具包直接构建强大的自定义应用程序
keywords: 团队 visual studio 工具包
ms.date: 06/30/2020
ms.openlocfilehash: e5715cf23cfd221b65afe0e6258ce06ff98770aa
ms.sourcegitcommit: 694babb79d379360a20cf928a9d2b88dd6d3bdd0
ms.translationtype: Auto
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "45051711"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a><span data-ttu-id="ff344-104">使用 Microsoft 团队工具包和 Visual Studio 生成应用程序</span><span class="sxs-lookup"><span data-stu-id="ff344-104">Build apps with the Microsoft Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="ff344-105">Microsoft 团队工具包使您能够在 Visual Studio 环境中直接创建自定义团队应用。</span><span class="sxs-lookup"><span data-stu-id="ff344-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio environment.</span></span> <span data-ttu-id="ff344-106">该工具包将引导您完成整个过程，并提供生成、调试和启动团队应用程序所需的所有内容。</span><span class="sxs-lookup"><span data-stu-id="ff344-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="ff344-107">安装团队工具包</span><span class="sxs-lookup"><span data-stu-id="ff344-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="ff344-108">Visual studio 的 Microsoft 团队工具包可从[Visual Studio Marketplace](https://aka.ms/teams-toolkit)下载或直接作为 visual studio 中的扩展。</span><span class="sxs-lookup"><span data-stu-id="ff344-108">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="ff344-109">使用工具包</span><span class="sxs-lookup"><span data-stu-id="ff344-109">Using the toolkit</span></span>

- [<span data-ttu-id="ff344-110">设置新项目</span><span class="sxs-lookup"><span data-stu-id="ff344-110">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="ff344-111">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="ff344-111">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="ff344-112">打包应用程序</span><span class="sxs-lookup"><span data-stu-id="ff344-112">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="ff344-113">在团队中运行应用程序</span><span class="sxs-lookup"><span data-stu-id="ff344-113">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="ff344-114">验证您的应用程序</span><span class="sxs-lookup"><span data-stu-id="ff344-114">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="ff344-115">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="ff344-115">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="ff344-116">设置新的团队项目</span><span class="sxs-lookup"><span data-stu-id="ff344-116">Set up a new Teams project</span></span>

1. <span data-ttu-id="ff344-117">创建一个新项目并选择 "Microsoft Terams 工具包" 模板。</span><span class="sxs-lookup"><span data-stu-id="ff344-117">Create a new project and select the Microsoft Terams Toolkit template.</span></span>
1. <span data-ttu-id="ff344-118">你将进入 "**添加功能**" 屏幕，为新应用配置属性。</span><span class="sxs-lookup"><span data-stu-id="ff344-118">You will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="ff344-119">选择 "**完成**" 按钮完成配置过程。</span><span class="sxs-lookup"><span data-stu-id="ff344-119">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="ff344-120">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="ff344-120">Configure your app</span></span>

<span data-ttu-id="ff344-121">在其核心中，团队应用程序包含三个组件：</span><span class="sxs-lookup"><span data-stu-id="ff344-121">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="ff344-122">Microsoft 团队客户端（web、桌面或移动版），用户与您的应用程序进行交互。</span><span class="sxs-lookup"><span data-stu-id="ff344-122">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="ff344-123">对将在团队中显示的内容请求做出响应的服务器，例如，HTML 选项卡内容或 bot 自适应卡。</span><span class="sxs-lookup"><span data-stu-id="ff344-123">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="ff344-124">由三个文件组成的团队[应用程序包](/concepts/build-and-test/apps-package.md)：</span><span class="sxs-lookup"><span data-stu-id="ff344-124">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="ff344-125">上的 manifest.js</span><span class="sxs-lookup"><span data-stu-id="ff344-125">The manifest.json</span></span> 
  > - <span data-ttu-id="ff344-126">显示在公用或组织应用程序目录中的应用程序的[彩色图标](../resources/schema/manifest-schema.md#icons)</span><span class="sxs-lookup"><span data-stu-id="ff344-126">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="ff344-127">"团队" 活动栏中显示的[大纲图标](../resources/schema/manifest-schema.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="ff344-127">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="ff344-128">在安装应用程序时，团队客户端会分析清单文件以确定所需的信息，如应用程序的名称和服务所在的 URL。</span><span class="sxs-lookup"><span data-stu-id="ff344-128">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="ff344-129">若要配置您的应用程序，请导航到**Microsoft 团队工具包**扩展窗口。</span><span class="sxs-lookup"><span data-stu-id="ff344-129">To configure your app, navigate to the **Microsoft Teams Toolkit** extension window.</span></span>
1. <span data-ttu-id="ff344-130">选择 "**编辑应用程序包**" 以查看**应用程序详细信息**页。</span><span class="sxs-lookup"><span data-stu-id="ff344-130">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="ff344-131">编辑应用程序详细信息页中的字段将更新作为应用程序包一部分最终交付的文件上的 manifest.js的内容。</span><span class="sxs-lookup"><span data-stu-id="ff344-131">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="ff344-132">了解更多</span><span class="sxs-lookup"><span data-stu-id="ff344-132">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="ff344-133">打包应用程序</span><span class="sxs-lookup"><span data-stu-id="ff344-133">Package your app</span></span>

<span data-ttu-id="ff344-134">修改您的应用**程序详细信息**页面或更新**清单**，或应用程序的 **. publish**文件夹中的**env**文件将自动生成**Development.zip**文件。</span><span class="sxs-lookup"><span data-stu-id="ff344-134">Modifying your the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="ff344-135">您需要在同一文件夹中包含[两个图标](../concepts/build-and-test/apps-package.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="ff344-135">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="ff344-136">在本地安装和运行应用程序</span><span class="sxs-lookup"><span data-stu-id="ff344-136">Install and run your app locally</span></span>

<span data-ttu-id="ff344-137">从 "*解决方案配置*" 下拉菜单中，选择 "*部署*"。</span><span class="sxs-lookup"><span data-stu-id="ff344-137">From the *Solutions Configurations* dropdown menu, select *Deploy*.</span></span> <span data-ttu-id="ff344-138">按 " *ISS Express + 团队*" 按钮。</span><span class="sxs-lookup"><span data-stu-id="ff344-138">Press the *ISS Express + Teams* button.</span></span> <span data-ttu-id="ff344-139">团队将启动，并且应用程序安装对话框应显示在团队客户端中。</span><span class="sxs-lookup"><span data-stu-id="ff344-139">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="ff344-140">验证您的应用程序</span><span class="sxs-lookup"><span data-stu-id="ff344-140">Validate your app</span></span>

<span data-ttu-id="ff344-141">通过 "**验证**" 页面，您可以在将应用程序提交到 AppSource 之前检查应用程序包。</span><span class="sxs-lookup"><span data-stu-id="ff344-141">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="ff344-142">只需上传清单包，验证工具就会检查应用程序是否符合所有与清单相关的测试用例。</span><span class="sxs-lookup"><span data-stu-id="ff344-142">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="ff344-143">对于每个失败的测试，说明提供的文档链接可帮助您修复错误。</span><span class="sxs-lookup"><span data-stu-id="ff344-143">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="ff344-144">对于难以自动化的测试，**初步清单**详细说明了最常见的失败测试事例的7，以及指向完整提交核对清单的链接。</span><span class="sxs-lookup"><span data-stu-id="ff344-144">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="ff344-145">将您的应用程序发布到团队</span><span class="sxs-lookup"><span data-stu-id="ff344-145">Publish your app to Teams</span></span>

<span data-ttu-id="ff344-146">在您的项目主页上，您可以将应用程序上载到团队，将您的应用程序提交到贵组织中用户的公司自定义应用商店，或将您的应用程序提交到所有团队用户的应用程序源。</span><span class="sxs-lookup"><span data-stu-id="ff344-146">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span> <span data-ttu-id="ff344-147">你的 IT 管理员将查看这些提交。</span><span class="sxs-lookup"><span data-stu-id="ff344-147">Your IT admin will review these submissions.</span></span> <span data-ttu-id="ff344-148">您可以返回到 "*发布*" 页面以查看您的提交状态，并了解您的应用程序是否已由 IT 管理员批准或拒绝。此外，您还可以将更新提交到您的应用程序或取消任何当前活动的提交。</span><span class="sxs-lookup"><span data-stu-id="ff344-148">You can return to the *Publish* page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ff344-149">下一步：维护和支持发布的应用程序</span><span class="sxs-lookup"><span data-stu-id="ff344-149">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
