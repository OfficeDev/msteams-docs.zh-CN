---
title: 使用 Teams Toolkit 和 Visual Studio
description: 开始使用自定义工具直接在Visual Studio生成出色的自定义Microsoft Teams Toolkit
keywords: teams visual studio 工具包
localization_priority: Normal
ms.topic: overview
ms.author: johmil
ms.openlocfilehash: 6a0f466ba0d95312695be8b5460fc949e3f70811
ms.sourcegitcommit: 4ac93d69927791a8ccf678ca5ee83e63b51566b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2021
ms.locfileid: "53095512"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a><span data-ttu-id="6a701-104">使用 Teams Toolkit 和 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6a701-104">Build apps with the Teams Toolkit and Visual Studio</span></span>

<span data-ttu-id="6a701-105">借助 Microsoft Teams 工具包，可以直接在 Visual Studio 集成开发环境（IDE）中创建自定义 Teams 应用程序。</span><span class="sxs-lookup"><span data-stu-id="6a701-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio integrated development environment (IDE).</span></span> <span data-ttu-id="6a701-106">Microsoft Teams 工具包将引导你完成整个过程，并提供构建、调试和启动 Teams 应用所需的一切资源。</span><span class="sxs-lookup"><span data-stu-id="6a701-106">The Microsoft Teams toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a701-107">先决条件</span><span class="sxs-lookup"><span data-stu-id="6a701-107">Prerequisites</span></span>

1. <span data-ttu-id="6a701-108">[启用开发人员预览](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)。</span><span class="sxs-lookup"><span data-stu-id="6a701-108">[Enable developer preview](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).</span></span>

2. <span data-ttu-id="6a701-109">确保已 ASP.NET **<span></span>和 Web** 开发模块添加到Visual Studio实例。</span><span class="sxs-lookup"><span data-stu-id="6a701-109">Make sure that the **<span>ASP.NET</span> and web development module** has been added to your Visual Studio instance.</span></span> <span data-ttu-id="6a701-110">有关详细信息，请参阅通过Visual Studio[或删除工作负载](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)和组件来修改服务。</span><span class="sxs-lookup"><span data-stu-id="6a701-110">For more information, see [Modify Visual Studio by adding or removing workloads and components](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true).</span></span>

![Visual studio asp.net 模块](../assets/images/visual-studio-web-dev-module.png)

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="6a701-112">安装Teams Toolkit</span><span class="sxs-lookup"><span data-stu-id="6a701-112">Install the Teams Toolkit</span></span>

<span data-ttu-id="6a701-113">可以从 Microsoft Teams Toolkit Visual Studio 应用商店或直接从 Visual Studio[内的](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit)"扩展"菜单中下载Visual Studio。 </span><span class="sxs-lookup"><span data-stu-id="6a701-113">The Microsoft Teams Toolkit for Visual Studio is available for download from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit) or directly from the **Extensions** menu within Visual Studio.</span></span>

## <a name="use-the-toolkit"></a><span data-ttu-id="6a701-114">使用工具包</span><span class="sxs-lookup"><span data-stu-id="6a701-114">Use the toolkit</span></span>

- [<span data-ttu-id="6a701-115">设置新项目</span><span class="sxs-lookup"><span data-stu-id="6a701-115">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="6a701-116">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="6a701-116">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="6a701-117">在应用商店中Teams</span><span class="sxs-lookup"><span data-stu-id="6a701-117">Run your app in Teams</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="6a701-118">验证你的应用</span><span class="sxs-lookup"><span data-stu-id="6a701-118">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="6a701-119">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="6a701-119">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="6a701-120">设置新的Teams项目</span><span class="sxs-lookup"><span data-stu-id="6a701-120">Set up a new Teams project</span></span>

1. <span data-ttu-id="6a701-121">启动 Visual Studio 2019。</span><span class="sxs-lookup"><span data-stu-id="6a701-121">Launch Visual Studio 2019.</span></span>
2. <span data-ttu-id="6a701-122">选择 **创建新项目**。</span><span class="sxs-lookup"><span data-stu-id="6a701-122">Select **Create a new project**.</span></span>
3. <span data-ttu-id="6a701-123">搜索 **"Microsoft Teams应用"，** 然后选择"下一 **步"。**</span><span class="sxs-lookup"><span data-stu-id="6a701-123">Search for **Microsoft Teams App** and select **Next**.</span></span>
4. <span data-ttu-id="6a701-124">在"**配置新项目"中**，输入Project **名称、\*\*\*\*位置** 和 **解决方案名称**。</span><span class="sxs-lookup"><span data-stu-id="6a701-124">In the **Configure your new project**, enter the **Project name**, **Location**, and **Solution name**.</span></span>
5. <span data-ttu-id="6a701-125">选择 **"** 下一步"输入应用的名称。</span><span class="sxs-lookup"><span data-stu-id="6a701-125">Select **Next** to enter a name for the app.</span></span>
6. <span data-ttu-id="6a701-126">在"其他信息"屏幕中，输入应用程序名称和开发人员 **或公司名称**，Teams应用。</span><span class="sxs-lookup"><span data-stu-id="6a701-126">In the Additional Information screen, enter an **Application Name** and **Developer or Company name** for your Teams app.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="6a701-127">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="6a701-127">Configure your app</span></span>

<span data-ttu-id="6a701-128">应用程序的核心是Teams三个组件：</span><span class="sxs-lookup"><span data-stu-id="6a701-128">At its core, the Teams app embraces three components:</span></span>

- <span data-ttu-id="6a701-129">The Microsoft Teams client (web， desktop or mobile) where users interact with your app.</span><span class="sxs-lookup"><span data-stu-id="6a701-129">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
- <span data-ttu-id="6a701-130">响应对网站中显示的内容的请求的服务器Teams。</span><span class="sxs-lookup"><span data-stu-id="6a701-130">A server that responds to requests for content displayed in Teams.</span></span> <span data-ttu-id="6a701-131">例如，HTML 选项卡内容或自动程序自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="6a701-131">For example, HTML tab content or a bot adaptive card.</span></span>
- <span data-ttu-id="6a701-132">应用Teams包包含三个文件：</span><span class="sxs-lookup"><span data-stu-id="6a701-132">A Teams app package consists of three files:</span></span>

    > [!div class="checklist"]
    >
    > - <span data-ttu-id="6a701-133">打开manifest.js</span><span class="sxs-lookup"><span data-stu-id="6a701-133">The manifest.json</span></span>
    > - <span data-ttu-id="6a701-134">要 [显示在](../resources/schema/manifest-schema.md#icons) 公共或组织应用程序目录中的应用的颜色图标。</span><span class="sxs-lookup"><span data-stu-id="6a701-134">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
    > - <span data-ttu-id="6a701-135">显示在[活动](../resources/schema/manifest-schema.md#icons)栏上的Teams图标。</span><span class="sxs-lookup"><span data-stu-id="6a701-135">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="6a701-136">安装应用后，Teams客户端将分析清单文件以确定所需信息，如应用名称和服务所在的 URL。</span><span class="sxs-lookup"><span data-stu-id="6a701-136">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

> [!NOTE]
><span data-ttu-id="6a701-137">如果尚未登录，则必须登录到 Microsoft 365 帐户，以继续进行开发过程。</span><span class="sxs-lookup"><span data-stu-id="6a701-137">If you have not done so already, you must sign in to your Microsoft 365 account to continue with the development process.</span></span>
>
> <span data-ttu-id="6a701-138">如果你没有帐户，Microsoft 365注册开发人员计划[Microsoft 365订阅。](https://developer.microsoft.com/microsoft-365/dev-program)</span><span class="sxs-lookup"><span data-stu-id="6a701-138">If you do not have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="6a701-139">它是免费的 90 天，只要你使用它进行开发活动，它将续订。</span><span class="sxs-lookup"><span data-stu-id="6a701-139">It's free for 90 days and renews as long as you are using it for development activity.</span></span> <span data-ttu-id="6a701-140">如果你有一个 Visual Studio Enterprise 或 Professional 订阅，这两个计划均Microsoft 365[免费](https://aka.ms/MyVisualStudioBenefits)开发人员订阅，在订阅生命周期内Visual Studio有效。</span><span class="sxs-lookup"><span data-stu-id="6a701-140">If you have a Visual Studio Enterprise or Professional subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="6a701-141">有关详细信息，请参阅[设置开发人员Microsoft 365订阅](/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="6a701-141">For more information, see [set up a Microsoft 365 developer subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="6a701-142">配置步骤</span><span class="sxs-lookup"><span data-stu-id="6a701-142">Configuration steps</span></span>

1. <span data-ttu-id="6a701-143">若要配置应用，请选择"Project > **TeamsFx >配置 SSO..."** 菜单。</span><span class="sxs-lookup"><span data-stu-id="6a701-143">To configure your app, select the **Project > TeamsFx > Configure for SSO...** menu.</span></span>

<span data-ttu-id="6a701-144">当系统提示时，登录到具有 M365 租户的 Microsoft 帐户。</span><span class="sxs-lookup"><span data-stu-id="6a701-144">When prompted, sign in to your Microsoft account that has an M365 tenant.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="6a701-145">在本地安装和运行应用</span><span class="sxs-lookup"><span data-stu-id="6a701-145">Install and run your app locally</span></span>

<span data-ttu-id="6a701-146">按 F5 开始调试。</span><span class="sxs-lookup"><span data-stu-id="6a701-146">Press F5 to start debugging.</span></span> <span data-ttu-id="6a701-147">应用程序安装对话框将显示在客户端Teams中。</span><span class="sxs-lookup"><span data-stu-id="6a701-147">The app installation dialog box appears in the Teams client.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="6a701-148">验证你的应用</span><span class="sxs-lookup"><span data-stu-id="6a701-148">Validate your app</span></span>

<span data-ttu-id="6a701-149">通过 **Project > TeamsFx 验证> Teams清单**"菜单，你可以检查应用包是否有效。</span><span class="sxs-lookup"><span data-stu-id="6a701-149">The **Project > TeamsFx Validate > Teams Manifest** menu allows you to check that your app package is valid.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="6a701-150">将应用发布到 Teams</span><span class="sxs-lookup"><span data-stu-id="6a701-150">Publish your app to Teams</span></span>

<span data-ttu-id="6a701-151">在[](https://dev.teams.microsoft.com/home)Teams 开发人员门户中，你可以将应用上载到团队、将应用提交到组织中用户的公司自定义应用商店，或将应用提交到所有 Teams 用户的应用源。</span><span class="sxs-lookup"><span data-stu-id="6a701-151">In the [Teams Developer Portal](https://dev.teams.microsoft.com/home), you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span>

- <span data-ttu-id="6a701-152">IT 管理员将审阅这些提交。</span><span class="sxs-lookup"><span data-stu-id="6a701-152">Your IT admin will review these submissions.</span></span>
- <span data-ttu-id="6a701-153">你可以返回到发布 **页面** ，检查你的提交状态，并了解你的应用是否已被 IT 管理员批准或拒绝。这同样也是你可以向应用提交更新或取消任何当前处于活动状态的提交的地方。</span><span class="sxs-lookup"><span data-stu-id="6a701-153">You can return to the **Publish** page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you can submit updates to your app or cancel any currently active submissions.</span></span>

## <a name="next-step"></a><span data-ttu-id="6a701-154">后续步骤</span><span class="sxs-lookup"><span data-stu-id="6a701-154">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6a701-155">使用 Blazor 生成Microsoft Teams应用程序</span><span class="sxs-lookup"><span data-stu-id="6a701-155">Build and run your first Microsoft Teams app with Blazor</span></span>](../get-started/first-app-blazor.md)
