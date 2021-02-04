---
title: 入门 - 生成并运行你的第一个应用
author: heath-hamilton
description: 快速创建显示"Hello， World！" 的 Microsoft Teams 应用 消息 Toolkit。
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 46a92f54cdbf68e28510c0bd4cc0b7018cfaae3c
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093948"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="ec7ed-104">生成并运行你的第一个 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="ec7ed-104">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="ec7ed-105">通过生成显示"Hello， World！"的个人选项卡开始 Microsoft Teams 开发。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-105">Start Microsoft Teams development by building a personal tab that displays "Hello, World!".</span></span>
<span data-ttu-id="ec7ed-106">按照以下步骤生成并运行你的第一个 Teams 应用：</span><span class="sxs-lookup"><span data-stu-id="ec7ed-106">Build and run your first Teams app using the following steps:</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="ec7ed-107">1. 创建应用项目</span><span class="sxs-lookup"><span data-stu-id="ec7ed-107">1. Create your app project</span></span>

<span data-ttu-id="ec7ed-108">使用 Microsoft Teams Toolkit代码Visual Studio设置你的第一个应用项目。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-108">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span> <span data-ttu-id="ec7ed-109">使用以下步骤创建应用项目：</span><span class="sxs-lookup"><span data-stu-id="ec7ed-109">Create your app project using the following steps:</span></span>

1. 在Visual Studio代码中，选择左侧活动栏上的 **Microsoft Teams，** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 **"创建新的 Teams 应用"。**
1. <span data-ttu-id="ec7ed-111">当系统提示时，使用 Microsoft 365 开发帐户登录。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-111">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="ec7ed-112">在"**添加功能"屏幕上**，选择 **"Tab"，** 然后选择"**下一步"。**</span><span class="sxs-lookup"><span data-stu-id="ec7ed-112">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="Screenshot showing how to configure your app project with the Visual Studio Code Teams Toolkit.":::
1. <span data-ttu-id="ec7ed-114">输入 Teams 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-114">Enter a name for your Teams app.</span></span> <span data-ttu-id="ec7ed-115"> (这是应用的默认名称，也是本地计算机上应用项目目录的名称。) </span><span class="sxs-lookup"><span data-stu-id="ec7ed-115">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="ec7ed-116">仅选中 **"个人"选项卡\*\*\*\*选项，然后选择** 屏幕底部的"完成"以配置项目。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-116">Check only the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-understand-important-app-project-components"></a><span data-ttu-id="ec7ed-117">2. 了解重要的应用项目组件</span><span class="sxs-lookup"><span data-stu-id="ec7ed-117">2. Understand important app project components</span></span>

<span data-ttu-id="ec7ed-118">工具包配置项目后，你即拥有为 Teams 生成基本个人选项卡的组件。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-118">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="ec7ed-119">项目目录和文件显示在代码的资源管理器Visual Studio区域中。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-119">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="Screenshot showing app project files for a personal tab in Visual Studio Code.":::

### <a name="app-scaffolding"></a><span data-ttu-id="ec7ed-121">应用基架</span><span class="sxs-lookup"><span data-stu-id="ec7ed-121">App scaffolding</span></span>

<span data-ttu-id="ec7ed-122">该工具包会基于你在设置过程中添加的功能在目录中自动 `src` 创建基架。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-122">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="ec7ed-123">例如，如果在设置期间创建选项卡，则目录中的文件非常重要，因为它处理应用的初始化 `App.js` `src/components` 和路由。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-123">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="ec7ed-124">它调用 [Microsoft Teams JavaScript 客户端 SDK](../tabs/how-to/using-teams-client-sdk.md) 以在应用和 Teams 之间建立通信。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-124">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-id"></a><span data-ttu-id="ec7ed-125">应用程序 ID</span><span class="sxs-lookup"><span data-stu-id="ec7ed-125">App ID</span></span>

<span data-ttu-id="ec7ed-126">使用 Teams 应用 ID 使用 App Studio 配置应用。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-126">Configure your app with App Studio using the Teams app ID.</span></span> <span data-ttu-id="ec7ed-127">在位于项目文件中的对象中查找 `teamsAppId` `package.json` ID。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-127">Find the ID in the `teamsAppId` object, which is located in your project's `package.json` file.</span></span>

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="ec7ed-128">3. 生成并运行应用</span><span class="sxs-lookup"><span data-stu-id="ec7ed-128">3. Build and run your app</span></span>

<span data-ttu-id="ec7ed-129">在本地生成并运行应用以节省时间。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-129">Build and run your app locally to save time.</span></span> <span data-ttu-id="ec7ed-130">This information is also available in the toolkit `README` .</span><span class="sxs-lookup"><span data-stu-id="ec7ed-130">This information is also available in the toolkit `README`.</span></span> <span data-ttu-id="ec7ed-131">使用以下步骤生成并运行应用：</span><span class="sxs-lookup"><span data-stu-id="ec7ed-131">Build and run your app using the following steps:</span></span>

1. <span data-ttu-id="ec7ed-132">在终端中，转到应用项目的根目录并运行 `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-132">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="ec7ed-133">运行 `npm start`。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-133">Run `npm start`.</span></span>

<span data-ttu-id="ec7ed-134">完成后，将成功 **进行编译！**</span><span class="sxs-lookup"><span data-stu-id="ec7ed-134">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="ec7ed-135">消息。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-135">message in the terminal.</span></span> <span data-ttu-id="ec7ed-136">你的应用正在运行 `https://localhost:3000` 。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-136">Your app is running on `https://localhost:3000`.</span></span>

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="ec7ed-137">4. 在 Teams 中旁加载应用</span><span class="sxs-lookup"><span data-stu-id="ec7ed-137">4. Sideload your app in Teams</span></span>

<span data-ttu-id="ec7ed-138">你的应用已准备好在 Teams 中进行测试。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-138">Your app is ready to test in Teams.</span></span> <span data-ttu-id="ec7ed-139">为此，你必须拥有允许应用旁加载的 Microsoft 365 开发帐户。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-139">To do this, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="ec7ed-140">有关帐户打开详细信息，请参阅 [Teams 开发帐户](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-140">For more information on account opening, see [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).</span></span> 

> [!TIP]
> <span data-ttu-id="ec7ed-141">使用 App [Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)中的验证功能（包含在工具包中）旁加载应用之前检查问题。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-141">Check for issues before sideloading your app, using the [validation feature in App Studio](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool), which is included in the toolkit.</span></span> <span data-ttu-id="ec7ed-142">修复错误以成功旁加载应用。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-142">Fix the errors to successfully sideload the app.</span></span>

<span data-ttu-id="ec7ed-143">使用以下步骤在 Teams 中旁加载应用：</span><span class="sxs-lookup"><span data-stu-id="ec7ed-143">Sideload your app in Teams using the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="ec7ed-144">若要在 Teams 中旁加载应用之前启用旁加载，请按照"打开 [应用旁加载"中的步骤操作](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-144">To enable sideloading before you sideload your app in Teams, follow the steps in [Turn on app sideloading](../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading).</span></span>

1. <span data-ttu-id="ec7ed-145">选择 **F5** 键以在 Visual Studio 代码中启动 Teams Web 客户端。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-145">Select the **F5** key to launch a Teams web client in Visual Studio Code.</span></span>
1. <span data-ttu-id="ec7ed-146">若要在 Teams 中显示你的应用内容，请指定你的应用在哪些 () `localhost` 可信：</span><span class="sxs-lookup"><span data-stu-id="ec7ed-146">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="ec7ed-147">默认情况下，在 Google Chrome 的相同浏览器窗口中打开 (选项卡，) **按 F5 后打开**。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-147">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="ec7ed-148">转到 `https://localhost:3000/tab` 并转到页面。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-148">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="ec7ed-149">返回到 Teams。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-149">Go back to Teams.</span></span> <span data-ttu-id="ec7ed-150">在对话框中，选择 **"为我添加** "以安装应用。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-150">In the dialog, select **Add for me** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="显示 Teams 中运行的个人选项卡应用示例&quot;Hello， World！&quot;的屏幕截图。":::

<span data-ttu-id="ec7ed-152">🎉恭喜！</span><span class="sxs-lookup"><span data-stu-id="ec7ed-152">🎉 Congratulations!</span></span> <span data-ttu-id="ec7ed-153">你的应用在 Teams 中运行。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-153">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="ec7ed-154">后续步骤</span><span class="sxs-lookup"><span data-stu-id="ec7ed-154">Next step</span></span>

<span data-ttu-id="ec7ed-155">在刚创建的个人选项卡上展开，或生成另一种类型的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="ec7ed-155">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ec7ed-156">添加到个人选项卡</span><span class="sxs-lookup"><span data-stu-id="ec7ed-156">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="ec7ed-157">创建频道选项卡</span><span class="sxs-lookup"><span data-stu-id="ec7ed-157">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="ec7ed-158">创建机器人</span><span class="sxs-lookup"><span data-stu-id="ec7ed-158">Build a bot</span></span>](../build-your-first-app/build-bot.md)
