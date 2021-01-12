---
title: 入门 - 生成并运行你的第一个应用
author: heath-hamilton
description: 快速创建显示"Hello， World！" 的 Microsoft Teams 应用 消息 Toolkit。
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: bc5d18dd887cbdbf56b8d6d013f53c21d1540370
ms.sourcegitcommit: 5687a901d48bcf2f5a3a086e0f703f854e8b9c21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2021
ms.locfileid: "49795466"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="9bb32-104">生成并运行你的第一个 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="9bb32-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="9bb32-105">通过生成显示"Hello， World！"的个人选项卡，你可以直接跳转到 Microsoft Teams 开发中。</span><span class="sxs-lookup"><span data-stu-id="9bb32-105">You can jump right into Microsoft Teams development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="9bb32-106">1. 创建应用项目</span><span class="sxs-lookup"><span data-stu-id="9bb32-106">1. Create your app project</span></span>

<span data-ttu-id="9bb32-107">使用 Microsoft Teams Toolkit代码Visual Studio设置你的第一个应用项目。</span><span class="sxs-lookup"><span data-stu-id="9bb32-107">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. 在Visual Studio代码中，选择左侧活动栏上的 **Microsoft Teams，** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 **"创建新的 Teams 应用"。**
1. <span data-ttu-id="9bb32-109">当系统提示时，使用 Microsoft 365 开发帐户登录。</span><span class="sxs-lookup"><span data-stu-id="9bb32-109">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="9bb32-110">在"**添加功能"屏幕上**，选择 **"Tab"，** 然后选择"**下一步"。**</span><span class="sxs-lookup"><span data-stu-id="9bb32-110">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Screenshot showing how to configure your app project with the Visual Studio Code Teams Toolkit.":::
1. <span data-ttu-id="9bb32-112">输入 Teams 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="9bb32-112">Enter a name for your Teams app.</span></span> <span data-ttu-id="9bb32-113"> (这是应用的默认名称，也是本地计算机上应用项目目录的名称。) </span><span class="sxs-lookup"><span data-stu-id="9bb32-113">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="9bb32-114">仅选中 **"个人"选项卡\*\*\*\*选项，然后选择** 屏幕底部的"完成"以配置项目。</span><span class="sxs-lookup"><span data-stu-id="9bb32-114">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="9bb32-115">2. 了解重要的应用项目组件</span><span class="sxs-lookup"><span data-stu-id="9bb32-115">2. Understand important app project components</span></span>

<span data-ttu-id="9bb32-116">在工具包配置项目后，你具有为 Teams 生成基本个人选项卡的组件。</span><span class="sxs-lookup"><span data-stu-id="9bb32-116">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="9bb32-117">项目目录和文件显示在代码的资源管理器Visual Studio区域中。</span><span class="sxs-lookup"><span data-stu-id="9bb32-117">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Screenshot showing app project files for a personal tab in Visual Studio Code.":::

### <a name="app-scaffolding"></a><span data-ttu-id="9bb32-119">应用基架</span><span class="sxs-lookup"><span data-stu-id="9bb32-119">App scaffolding</span></span>

<span data-ttu-id="9bb32-120">该工具包会基于你在设置过程中添加的功能在目录中 `src` 自动创建基架。</span><span class="sxs-lookup"><span data-stu-id="9bb32-120">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="9bb32-121">例如，如果在设置期间创建选项卡，则目录中的文件非常重要，因为它处理应用的 `App.js` `src/components` 初始化和路由。</span><span class="sxs-lookup"><span data-stu-id="9bb32-121">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="9bb32-122">它调用 [Microsoft Teams JavaScript 客户端 SDK，](../tabs/how-to/using-teams-client-sdk.md) 以在应用和 Teams 之间建立通信。</span><span class="sxs-lookup"><span data-stu-id="9bb32-122">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="9bb32-123">应用程序 ID</span><span class="sxs-lookup"><span data-stu-id="9bb32-123">App ID</span></span>

<span data-ttu-id="9bb32-124">使用 App Studio 配置应用需要 Teams 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="9bb32-124">Your Teams app ID is needed to configure your app with App Studio.</span></span> <span data-ttu-id="9bb32-125">您可以在位于项目文件中的对象中查找 `teamsAppId` `package.json` ID。</span><span class="sxs-lookup"><span data-stu-id="9bb32-125">You can find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="9bb32-126">3. 生成并运行应用</span><span class="sxs-lookup"><span data-stu-id="9bb32-126">3. Build and run your app</span></span>

<span data-ttu-id="9bb32-127">为符合时间需要，你将在本地生成和运行应用。</span><span class="sxs-lookup"><span data-stu-id="9bb32-127">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="9bb32-128"> (工具包 .) 中也提供了 `README` 此信息。</span><span class="sxs-lookup"><span data-stu-id="9bb32-128">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="9bb32-129">在终端中，转到应用项目的根目录并运行 `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="9bb32-129">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="9bb32-130">运行 `npm start`。</span><span class="sxs-lookup"><span data-stu-id="9bb32-130">Run `npm start`.</span></span>

<span data-ttu-id="9bb32-131">完成后，将成功 **进行编译！**</span><span class="sxs-lookup"><span data-stu-id="9bb32-131">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="9bb32-132">消息。</span><span class="sxs-lookup"><span data-stu-id="9bb32-132">message in the terminal.</span></span> <span data-ttu-id="9bb32-133">你的应用正在运行 `https://localhost:3000` 。</span><span class="sxs-lookup"><span data-stu-id="9bb32-133">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="9bb32-134">4. 在 Teams 中旁加载应用</span><span class="sxs-lookup"><span data-stu-id="9bb32-134">4. Sideload your app in Teams</span></span>

<span data-ttu-id="9bb32-135">你的应用已准备好在 Teams 中进行测试。</span><span class="sxs-lookup"><span data-stu-id="9bb32-135">Your app is ready to test in Teams.</span></span> <span data-ttu-id="9bb32-136">为此，你必须具有允许应用旁加载的帐户。</span><span class="sxs-lookup"><span data-stu-id="9bb32-136">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="9bb32-137"> (如果不确定是否拥有，请了解如何获取 Teams 开发 [帐户](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).) </span><span class="sxs-lookup"><span data-stu-id="9bb32-137">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

> [!TIP]
> <span data-ttu-id="9bb32-138">在旁加载应用之前，使用工具包中包含的 App [Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)中的验证功能检查问题。</span><span class="sxs-lookup"><span data-stu-id="9bb32-138">Before sideloading your app, check for issues using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="9bb32-139">必须修复错误，以成功旁加载应用。</span><span class="sxs-lookup"><span data-stu-id="9bb32-139">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="9bb32-140">在Visual Studio中，按 **F5** 键启动 Teams Web 客户端。</span><span class="sxs-lookup"><span data-stu-id="9bb32-140">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="9bb32-141">若要在 Teams 中显示你的应用内容，请指定你的应用在哪些 () `localhost` 可信赖：</span><span class="sxs-lookup"><span data-stu-id="9bb32-141">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="9bb32-142">默认情况下，在 Google Chrome 的相同浏览器窗口中打开 (新选项卡) 按 **F5** 后打开。</span><span class="sxs-lookup"><span data-stu-id="9bb32-142">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="9bb32-143">转到 `https://localhost:3000/tab` 并转到页面。</span><span class="sxs-lookup"><span data-stu-id="9bb32-143">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="9bb32-144">返回到 Teams。</span><span class="sxs-lookup"><span data-stu-id="9bb32-144">Go back to Teams.</span></span> <span data-ttu-id="9bb32-145">在对话框中，选择 **"为我添加** "以安装应用。</span><span class="sxs-lookup"><span data-stu-id="9bb32-145">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="显示 Teams 中运行的个人选项卡应用示例&quot;Hello， World！&quot;的屏幕截图。":::

<span data-ttu-id="9bb32-147">🎉恭喜！</span><span class="sxs-lookup"><span data-stu-id="9bb32-147">🎉 Congratulations!</span></span> <span data-ttu-id="9bb32-148">你的应用在 Teams 中运行。</span><span class="sxs-lookup"><span data-stu-id="9bb32-148">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="9bb32-149">后续步骤</span><span class="sxs-lookup"><span data-stu-id="9bb32-149">Next step</span></span>

<span data-ttu-id="9bb32-150">在刚创建的个人选项卡上展开，或生成另一种类型的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="9bb32-150">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9bb32-151">添加到个人选项卡</span><span class="sxs-lookup"><span data-stu-id="9bb32-151">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="9bb32-152">创建频道选项卡</span><span class="sxs-lookup"><span data-stu-id="9bb32-152">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="9bb32-153">创建机器人</span><span class="sxs-lookup"><span data-stu-id="9bb32-153">Build a bot</span></span>](../build-your-first-app/build-bot.md)
