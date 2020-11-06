---
title: 入门-构建并运行您的首个应用程序
author: heath-hamilton
description: 快速创建显示 "Hello，World！" 的 Microsoft 团队应用程序 使用 Microsoft 团队工具包的邮件。
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 62c4bd950183ceb64fb30b528661cf84e9210d89
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931772"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="5522b-104">生成并运行你的首个 Microsoft 团队应用</span><span class="sxs-lookup"><span data-stu-id="5522b-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="5522b-105">您可以通过构建显示为 "Hello，World！" 的个人选项卡，直接跳转到 Microsoft 团队开发。</span><span class="sxs-lookup"><span data-stu-id="5522b-105">You can jump right into Microsoft Teams development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="5522b-106">1. 创建您的应用程序项目</span><span class="sxs-lookup"><span data-stu-id="5522b-106">1. Create your app project</span></span>

<span data-ttu-id="5522b-107">使用 Visual Studio Code 中的 Microsoft 团队工具包设置您的首个应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="5522b-107">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队** "， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **创建新的团队应用** "。
1. <span data-ttu-id="5522b-109">出现提示时，使用 Microsoft 365 开发帐户登录。</span><span class="sxs-lookup"><span data-stu-id="5522b-109">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="5522b-110">在 " **添加功能** " 屏幕上，依次选择 **"** **下一步** "。</span><span class="sxs-lookup"><span data-stu-id="5522b-110">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="显示如何使用 Visual Studio Code 团队工具包配置应用程序项目的屏幕截图。":::
1. <span data-ttu-id="5522b-112">为你的团队应用输入名称。</span><span class="sxs-lookup"><span data-stu-id="5522b-112">Enter a name for your Teams app.</span></span> <span data-ttu-id="5522b-113"> (这是您的应用程序的默认名称，也是本地计算机上的应用程序项目目录的名称。 ) </span><span class="sxs-lookup"><span data-stu-id="5522b-113">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="5522b-114">仅检查 " **个人" 选项卡** 选项，然后选择屏幕底部的 " **完成** " 以配置项目。</span><span class="sxs-lookup"><span data-stu-id="5522b-114">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="5522b-115">2. 了解重要的应用程序项目组件</span><span class="sxs-lookup"><span data-stu-id="5522b-115">2. Understand important app project components</span></span>

<span data-ttu-id="5522b-116">工具包配置项目后，您就可以使用组件为团队构建基本的个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="5522b-116">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="5522b-117">项目目录和文件显示在 Visual Studio Code 的 "资源管理器" 区域中。</span><span class="sxs-lookup"><span data-stu-id="5522b-117">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="显示 Visual Studio Code 中的 _OL_QUOTE_PLACEHOLDER_个人_OL_QUOTE_PLACEHOLDER_ 选项卡的应用程序项目文件的屏幕截图。":::

### <a name="app-scaffolding"></a><span data-ttu-id="5522b-119">应用程序基架</span><span class="sxs-lookup"><span data-stu-id="5522b-119">App scaffolding</span></span>

<span data-ttu-id="5522b-120">该工具包将根据您在安装过程中添加的功能，在目录中自动为您创建基架 `src` 。</span><span class="sxs-lookup"><span data-stu-id="5522b-120">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="5522b-121">例如，如果在安装过程中创建选项卡，则该 `App.js` 目录中的文件 `src/components` 很重要，因为它会处理您的应用程序的初始化和路由。</span><span class="sxs-lookup"><span data-stu-id="5522b-121">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="5522b-122">它调用 [Microsoft 团队 SDK](../tabs/how-to/using-teams-client-sdk.md) 以在您的应用程序和团队之间建立通信。</span><span class="sxs-lookup"><span data-stu-id="5522b-122">It calls the [Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="5522b-123">应用程序 ID</span><span class="sxs-lookup"><span data-stu-id="5522b-123">App ID</span></span>

<span data-ttu-id="5522b-124">您的团队应用程序 ID 是使用应用程序 Studio 配置应用程序所必需的。</span><span class="sxs-lookup"><span data-stu-id="5522b-124">Your Teams app ID is needed to configure your app with App Studio.</span></span> <span data-ttu-id="5522b-125">您可以在 `teamsAppId` 项目文件中找到该对象的 ID `package.json` 。</span><span class="sxs-lookup"><span data-stu-id="5522b-125">You can find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="5522b-126">3. 生成并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="5522b-126">3. Build and run your app</span></span>

<span data-ttu-id="5522b-127">在时间方面，你将在本地构建和运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="5522b-127">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="5522b-128"> (工具包中也提供了此信息 `README` 。 ) </span><span class="sxs-lookup"><span data-stu-id="5522b-128">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="5522b-129">在终端中，转到您的应用程序项目的根目录并运行该目录 `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="5522b-129">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="5522b-130">运行 `npm start` 。</span><span class="sxs-lookup"><span data-stu-id="5522b-130">Run `npm start`.</span></span>

<span data-ttu-id="5522b-131">完成后，已 **成功编译了！**</span><span class="sxs-lookup"><span data-stu-id="5522b-131">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="5522b-132">终端中的邮件。</span><span class="sxs-lookup"><span data-stu-id="5522b-132">message in the terminal.</span></span> <span data-ttu-id="5522b-133">您的应用程序正在运行 `https://localhost:3000` 。</span><span class="sxs-lookup"><span data-stu-id="5522b-133">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="5522b-134">4. 在团队中旁加载您的应用程序</span><span class="sxs-lookup"><span data-stu-id="5522b-134">4. Sideload your app in Teams</span></span>

<span data-ttu-id="5522b-135">您的应用程序已准备好在团队中进行测试。</span><span class="sxs-lookup"><span data-stu-id="5522b-135">Your app is ready to test in Teams.</span></span> <span data-ttu-id="5522b-136">若要执行此操作，您必须具有允许应用旁加载的帐户。</span><span class="sxs-lookup"><span data-stu-id="5522b-136">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="5522b-137"> (如果您不能确定，请了解如何获取 [团队开发帐户](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)。 ) </span><span class="sxs-lookup"><span data-stu-id="5522b-137">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

> [!TIP]
> <span data-ttu-id="5522b-138">在添加您的应用程序之前，请使用 [应用程序中的验证功能](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)检查是否存在问题，该功能包含在工具包中。</span><span class="sxs-lookup"><span data-stu-id="5522b-138">Before sideloading your app, check for issues using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="5522b-139">必须修复错误才能成功旁加载应用。</span><span class="sxs-lookup"><span data-stu-id="5522b-139">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="5522b-140">在 Visual Studio Code 中，按 **F5** 键以启动团队 web 客户端。</span><span class="sxs-lookup"><span data-stu-id="5522b-140">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="5522b-141">若要在团队中显示应用内容，请指定您的应用程序的运行位置 (`localhost`) 是可信的：</span><span class="sxs-lookup"><span data-stu-id="5522b-141">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="5522b-142">默认情况下，在同一浏览器窗口中打开一个新选项卡 () 按 **F5** 后打开的。</span><span class="sxs-lookup"><span data-stu-id="5522b-142">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="5522b-143">转到 `https://localhost:3000/tab` ""，然后继续转到 "" 页。</span><span class="sxs-lookup"><span data-stu-id="5522b-143">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="5522b-144">返回到 "团队"。</span><span class="sxs-lookup"><span data-stu-id="5522b-144">Go back to Teams.</span></span> <span data-ttu-id="5522b-145">在对话框中，选择 "添加"，以安装您 **的** 应用程序。</span><span class="sxs-lookup"><span data-stu-id="5522b-145">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="显示在团队中运行的示例 _OL_QUOTE_PLACEHOLDER_Hello，World！_OL_QUOTE_PLACEHOLDER_ 个人选项卡应用程序的屏幕截图。":::

<span data-ttu-id="5522b-147">🎉祝贺！</span><span class="sxs-lookup"><span data-stu-id="5522b-147">🎉 Congratulations!</span></span> <span data-ttu-id="5522b-148">你的应用程序正在团队中运行。</span><span class="sxs-lookup"><span data-stu-id="5522b-148">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="5522b-149">后续步骤</span><span class="sxs-lookup"><span data-stu-id="5522b-149">Next step</span></span>

<span data-ttu-id="5522b-150">展开刚创建的 "个人" 选项卡或生成另一种类型的 "团队" 应用。</span><span class="sxs-lookup"><span data-stu-id="5522b-150">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5522b-151">添加到你的个人选项卡</span><span class="sxs-lookup"><span data-stu-id="5522b-151">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="5522b-152">创建频道选项卡</span><span class="sxs-lookup"><span data-stu-id="5522b-152">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="5522b-153">创建机器人</span><span class="sxs-lookup"><span data-stu-id="5522b-153">Build a bot</span></span>](../build-your-first-app/build-bot.md)
