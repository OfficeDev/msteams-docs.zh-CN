---
title: 使用 Microsoft Teams Toolkit 和 Visual Studio
description: 开始使用 Microsoft Teams Visual Studio直接生成出色的自定义Toolkit
keywords: teams visual studio 工具包
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 08df1d3907a1a3683eb42222e247cd7fd6c0177b
ms.sourcegitcommit: 5e1300d6f4f2ea23beb3cdbbf4bd46999eef4e87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/15/2021
ms.locfileid: "49875005"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="fe92f-104">使用 Teams Toolkit 和 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fe92f-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="fe92f-105">Microsoft Teams Toolkit使你可以直接在 IDE Visual Studio集成开发 (创建自定义 Teams) 。</span><span class="sxs-lookup"><span data-stu-id="fe92f-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="fe92f-106">Microsoft Teams 工具包将指导你完成此过程，并提供生成、调试和启动 Teams 应用所需的一切。</span><span class="sxs-lookup"><span data-stu-id="fe92f-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe92f-107">先决条件</span><span class="sxs-lookup"><span data-stu-id="fe92f-107">Prerequisites</span></span>

1. [<span data-ttu-id="fe92f-108">启用开发人员预览</span><span class="sxs-lookup"><span data-stu-id="fe92f-108">Enable developer preview</span></span>](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. <span data-ttu-id="fe92f-109">确保已ASP.NE **<span></span>T** 和 Web 开发模块添加到Visual Studio实例。</span><span class="sxs-lookup"><span data-stu-id="fe92f-109">Make sure that the **<span>ASP.NE</span>T and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="fe92f-110">可以通过添加或删除工作负载和组件文档，按照"修改Visual Studio中的 [步骤进行](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) 检查。</span><span class="sxs-lookup"><span data-stu-id="fe92f-110">You can check by following the steps in the [Modify Visual Studio by adding or removing workloads and component](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true) documentation.</span></span>

![visual studio asp.net 模块](../assets/images/visual-studio-web-dev-module.png)

3. <span data-ttu-id="fe92f-112">如果你想要通过从应用程序部署应用来测试Visual Studio，则需要在开发环境中 (Internet Information Services) IIS 应用程序。</span><span class="sxs-lookup"><span data-stu-id="fe92f-112">If you would like test your app by deploying it from Visual Studio, you'll need to have IIS (Internet Information Services) installed in your development environment.</span></span> <span data-ttu-id="fe92f-113">Visual Studio不包括 IIS，并且未包含在默认 Windows 10、Windows 8 或 Windows 7 配置中;但是，可以从 Microsoft 下载中心下载 [最新版本](https://www.microsoft.com/download/details.aspx?id=48264)。</span><span class="sxs-lookup"><span data-stu-id="fe92f-113">Visual Studio does not include IIS and it isn't included in the default Windows 10, Windows 8, or Windows 7 configuration; however, you can download the latest version from the [Microsoft download center](https://www.microsoft.com/download/details.aspx?id=48264).</span></span>

![IIS 下载页面视图](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="fe92f-115">安装 Teams Toolkit</span><span class="sxs-lookup"><span data-stu-id="fe92f-115">Install the Teams Toolkit</span></span>

<span data-ttu-id="fe92f-116">Microsoft Teams Toolkit for Visual Studio 可从 Visual Studio [Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate)下载，也可以直接从 Visual Studio 中的"扩展"菜单中下载。</span><span class="sxs-lookup"><span data-stu-id="fe92f-116">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="fe92f-117">使用工具包</span><span class="sxs-lookup"><span data-stu-id="fe92f-117">Using the toolkit</span></span>

- [<span data-ttu-id="fe92f-118">设置新项目</span><span class="sxs-lookup"><span data-stu-id="fe92f-118">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="fe92f-119">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="fe92f-119">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="fe92f-120">打包应用</span><span class="sxs-lookup"><span data-stu-id="fe92f-120">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="fe92f-121">在 Teams 中运行应用</span><span class="sxs-lookup"><span data-stu-id="fe92f-121">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="fe92f-122">验证你的应用</span><span class="sxs-lookup"><span data-stu-id="fe92f-122">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="fe92f-123">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="fe92f-123">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="fe92f-124">设置新的 Teams 项目</span><span class="sxs-lookup"><span data-stu-id="fe92f-124">Set up a new Teams project</span></span>

1. <span data-ttu-id="fe92f-125">选择 **"新建项目"。**</span><span class="sxs-lookup"><span data-stu-id="fe92f-125">Select **Create a new project**.</span></span>
1. <span data-ttu-id="fe92f-126">选择 **Microsoft Teams 应用**，然后选择"下 **一步"。**</span><span class="sxs-lookup"><span data-stu-id="fe92f-126">Choose **Microsoft Teams App** and select **Next**.</span></span>
1. <span data-ttu-id="fe92f-127">您将到达"配置 **新项目**"屏幕，您可以在其中选择项目名称、**位置** 和 **解决方案名称**。 </span><span class="sxs-lookup"><span data-stu-id="fe92f-127">You will arrive at the **Configure your new project** screen where you can choose the **Project name**, **Location**, and **Solution name**.</span></span>
1. <span data-ttu-id="fe92f-128">选中标记为"将解决方案和项目 **放在同一目录中"的框**。</span><span class="sxs-lookup"><span data-stu-id="fe92f-128">Check the box labeled **Place solution and project in the same directory**.</span></span>
1. <span data-ttu-id="fe92f-129">标记为"添加功能"的弹出窗口将允许你为项目设置选择一个或多个功能。</span><span class="sxs-lookup"><span data-stu-id="fe92f-129">A pop-up window labeled **Add Capabilities** will allow you to choose one or more capabilities for your project setup.</span></span>
1. <span data-ttu-id="fe92f-130">选择 **"下一** 步"按钮以完成配置过程。</span><span class="sxs-lookup"><span data-stu-id="fe92f-130">Select the **Next** button to complete the configuration process.</span></span>
1. <span data-ttu-id="fe92f-131">标记为"添加功能"的弹出窗口将允许你选择每个选定功能的属性。</span><span class="sxs-lookup"><span data-stu-id="fe92f-131">A pop-up window labeled **Add Capabilities** will allow you to choose the properties for each selected capability.</span></span>
1. <span data-ttu-id="fe92f-132">选择 **"完成** "，你将登录 **Microsoft Teams Toolkit** 登录页。</span><span class="sxs-lookup"><span data-stu-id="fe92f-132">Select **Finish** and you will  land on the **Microsoft Teams Toolkit** landing page.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="fe92f-133">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="fe92f-133">Configure your app</span></span>

<span data-ttu-id="fe92f-134">Teams 应用的核心包括三个组件：</span><span class="sxs-lookup"><span data-stu-id="fe92f-134">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="fe92f-135">Microsoft Teams 客户端 (Web、桌面或移动) 用户与你的应用交互。</span><span class="sxs-lookup"><span data-stu-id="fe92f-135">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="fe92f-136">响应对将在 Teams 中显示的内容（例如，HTML 选项卡内容或自动程序自适应卡片）的请求的服务器。</span><span class="sxs-lookup"><span data-stu-id="fe92f-136">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="fe92f-137">包含 [三个文件的](/concepts/build-and-test/apps-package.md) Teams 应用包：</span><span class="sxs-lookup"><span data-stu-id="fe92f-137">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="fe92f-138">打开manifest.js</span><span class="sxs-lookup"><span data-stu-id="fe92f-138">The manifest.json</span></span>
  > - <span data-ttu-id="fe92f-139">[要显示在](../resources/schema/manifest-schema.md#icons)公共或组织应用程序目录中的应用的颜色图标</span><span class="sxs-lookup"><span data-stu-id="fe92f-139">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="fe92f-140">[用于显示在](../resources/schema/manifest-schema.md#icons)Teams 活动栏上的大纲图标。</span><span class="sxs-lookup"><span data-stu-id="fe92f-140">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="fe92f-141">安装应用后，Teams 客户端将分析清单文件以确定所需信息，如应用名称和服务所在的 URL。</span><span class="sxs-lookup"><span data-stu-id="fe92f-141">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="fe92f-142">如果尚未登录，则需要登录到 Microsoft 365 或帐户，以继续开发过程。</span><span class="sxs-lookup"><span data-stu-id="fe92f-142">If you haven't done so already, you will need to sign in to your Microsoft 365  or account to continue with the development process.</span></span>
>
> <span data-ttu-id="fe92f-143">如果你没有 Microsoft 365 帐户，可以注册 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program) 订阅。</span><span class="sxs-lookup"><span data-stu-id="fe92f-143">If you don't have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="fe92f-144">它 *90* 天免费，并且将持续续订，只要使用它进行开发活动。</span><span class="sxs-lookup"><span data-stu-id="fe92f-144">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="fe92f-145">如果你有企业Visual Studio专业版订阅，这两个计划都包括免费的 Microsoft 365 开发人员[](https://aka.ms/MyVisualStudioBenefits)订阅，在订阅的生命周期内Visual Studio订阅。</span><span class="sxs-lookup"><span data-stu-id="fe92f-145">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="fe92f-146">*请参阅*[设置 Microsoft 365 开发人员订阅](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="fe92f-146">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>
>

### <a name="configuration-steps"></a><span data-ttu-id="fe92f-147">配置步骤</span><span class="sxs-lookup"><span data-stu-id="fe92f-147">Configuration steps</span></span>

1. <span data-ttu-id="fe92f-148">若要配置你的应用，请在 **Microsoft Teams Toolkit** 登录页上，选择"编辑 **应用包"。**</span><span class="sxs-lookup"><span data-stu-id="fe92f-148">To configure your app, on the **Microsoft Teams Toolkit** landing page, select **Edit app package** .</span></span>
1. <span data-ttu-id="fe92f-149">从 **"我的环境**"下拉菜单中，选择 **"开发"。**</span><span class="sxs-lookup"><span data-stu-id="fe92f-149">From the **My Environments** drop-down menu, select **development**.</span></span>
1. <span data-ttu-id="fe92f-150">你将登录" **应用详细信息** "页，可在其中编辑应用的属性字段。</span><span class="sxs-lookup"><span data-stu-id="fe92f-150">You will land on the **App details** page where you can edit your app's property fields.</span></span>
1. <span data-ttu-id="fe92f-151">编辑"应用详细信息"页中的字段将更新manifest.js最终作为应用包的一部分提供的文件上的内容。</span><span class="sxs-lookup"><span data-stu-id="fe92f-151">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="fe92f-152">了解更多</span><span class="sxs-lookup"><span data-stu-id="fe92f-152">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="fe92f-153">打包应用</span><span class="sxs-lookup"><span data-stu-id="fe92f-153">Package your app</span></span>

<span data-ttu-id="fe92f-154">修改 **应用详细信息** 页面或更新清单或应用的.publish 文件夹中的 **.env** 文件 **将** 自动生成Development.zip文件。</span><span class="sxs-lookup"><span data-stu-id="fe92f-154">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="fe92f-155">the Development.zip file includes three required files — the **manifest.json** and [two icons.](../concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="fe92f-155">The Development.zip file includes three required files — the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="fe92f-156">在本地安装和运行应用</span><span class="sxs-lookup"><span data-stu-id="fe92f-156">Install and run your app locally</span></span>

1. <span data-ttu-id="fe92f-157">从"**解决方案配置**"下拉菜单中，选择"部署 **"。**</span><span class="sxs-lookup"><span data-stu-id="fe92f-157">From the **Solution Configurations** dropdown menu, select **Deploy**.</span></span>

![解决方案配置菜单](../assets/images/solution-configurations.png)

2. <span data-ttu-id="fe92f-159">选择 **IIS Express + Teams** 按钮。</span><span class="sxs-lookup"><span data-stu-id="fe92f-159">Select the **IIS Express + Teams** button.</span></span>

1. <span data-ttu-id="fe92f-160">Teams 将启动，应用安装对话应显示在 Teams 客户端中。</span><span class="sxs-lookup"><span data-stu-id="fe92f-160">Teams will launch and the app installation dialogue should appear in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="fe92f-161">验证你的应用</span><span class="sxs-lookup"><span data-stu-id="fe92f-161">Validate your app</span></span>

<span data-ttu-id="fe92f-162">" **验证** "页允许你在将应用提交到 AppSource 之前检查应用包。</span><span class="sxs-lookup"><span data-stu-id="fe92f-162">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="fe92f-163">只需上传清单包，验证工具将针对所有清单相关的测试用例检查你的应用。</span><span class="sxs-lookup"><span data-stu-id="fe92f-163">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="fe92f-164">对于每个失败的测试，该说明都提供了一个文档链接，以帮助您修复错误。</span><span class="sxs-lookup"><span data-stu-id="fe92f-164">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="fe92f-165">对于难以自动执行的测试，"初步清单"会详细介绍 7 个最常见的失败测试用例，以及指向完整提交清单的链接。</span><span class="sxs-lookup"><span data-stu-id="fe92f-165">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="fe92f-166">将应用发布到 Teams</span><span class="sxs-lookup"><span data-stu-id="fe92f-166">Publish your app to Teams</span></span>

<span data-ttu-id="fe92f-167">✔在项目主页上，可以将应用上传到团队，将应用提交到组织中用户的公司自定义应用商店，或将应用提交到所有 Teams 用户的应用源。</span><span class="sxs-lookup"><span data-stu-id="fe92f-167">✔ On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

<span data-ttu-id="fe92f-168">✔ IT 管理员将查看这些提交。</span><span class="sxs-lookup"><span data-stu-id="fe92f-168">✔ Your IT admin will review these submissions.</span></span>

<span data-ttu-id="fe92f-169">✔你可以返回到"发布"页面以检查提交状态，并了解你的应用是否由 IT 管理员批准或拒绝。这也是你向应用提交更新或取消任何当前处于活动状态的提交的地方。</span><span class="sxs-lookup"><span data-stu-id="fe92f-169">✔  You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fe92f-170">下一步：维护和支持已发布的应用</span><span class="sxs-lookup"><span data-stu-id="fe92f-170">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
