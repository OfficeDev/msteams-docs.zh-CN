---
title: 入门 - 生成并运行你的第一个应用
author: girliemac
description: 快速创建显示Microsoft Teams Hello， World！" 的 Web 应用 message using the Microsoft Teams Toolkit.
ms.author: timura
ms.date: 03/22/2021
ms.topic: quickstart
ms.openlocfilehash: 6c3d215a3f2c1aa89a9a2bf28aad081d98c6dc33
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101721"
---
# <a name="create-your-first-microsoft-teams-app"></a><span data-ttu-id="75da9-104">创建你的第一Microsoft Teams应用</span><span class="sxs-lookup"><span data-stu-id="75da9-104">Create your first Microsoft Teams app</span></span>

<span data-ttu-id="75da9-105">本快速入门指导你构建并运行Microsoft Teams Hello， World！" 的应用。</span><span class="sxs-lookup"><span data-stu-id="75da9-105">This quickstart teaches you to build and run Microsoft Teams app that displays "Hello, World!"</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75da9-106">先决条件</span><span class="sxs-lookup"><span data-stu-id="75da9-106">Prerequisites</span></span>

<span data-ttu-id="75da9-107">在开始之前，你需要设置你的Teams[租户，](#set-up-your-teams-development-tenant)[并安装你的Teams工具](#install-your-development-tools)。</span><span class="sxs-lookup"><span data-stu-id="75da9-107">Before you begin, you need to [set up your Teams development tenant](#set-up-your-teams-development-tenant) and [install your Teams development tools](#install-your-development-tools).</span></span>

### <a name="set-up-your-teams-development-tenant"></a><span data-ttu-id="75da9-108">设置你的Teams开发租户</span><span class="sxs-lookup"><span data-stu-id="75da9-108">Set up your Teams development tenant</span></span>

<span data-ttu-id="75da9-109">**租户** 就像组织的容器。</span><span class="sxs-lookup"><span data-stu-id="75da9-109">A **tenant** is like a container for an organization.</span></span> <span data-ttu-id="75da9-110">就Teams而言，租户是组织人员聊天、共享文件和运行会议的地方。</span><span class="sxs-lookup"><span data-stu-id="75da9-110">In Teams terms, a tenant is where people from that org chat, share files, and run meetings.</span></span> <span data-ttu-id="75da9-111">作为开发人员，你需要一个租户来旁加载和测试Teams构建的应用。</span><span class="sxs-lookup"><span data-stu-id="75da9-111">As a developer, you need a tenant to sideload and test the Teams apps that you are building.</span></span>  

# <a name="do-not-have-a-tenant"></a>[<span data-ttu-id="75da9-112">没有租户</span><span class="sxs-lookup"><span data-stu-id="75da9-112">Do not have a tenant</span></span>](#tab/do-not-have-a-tenant)

<span data-ttu-id="75da9-113">通过加入开发人员计划，Teams测试帐户（包括允许应用旁加载的Microsoft 365帐户）。</span><span class="sxs-lookup"><span data-stu-id="75da9-113">You can get a free Teams test account, which includes a tenant that allows app sideloading, by joining the Microsoft 365 developer program.</span></span> <span data-ttu-id="75da9-114">注册过程大约需要两分钟。</span><span class="sxs-lookup"><span data-stu-id="75da9-114">The registration process takes approximately two minutes.</span></span>

<span data-ttu-id="75da9-115">**获取租户**</span><span class="sxs-lookup"><span data-stu-id="75da9-115">**To get a tenant**</span></span>

1. <span data-ttu-id="75da9-116">转到开发人员[Microsoft 365计划](https://developer.microsoft.com/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="75da9-116">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="75da9-117">选择 **立即加入** 并按照屏幕上的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="75da9-117">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="75da9-118">在欢迎屏幕中，选择 **"设置 E5 订阅"。**</span><span class="sxs-lookup"><span data-stu-id="75da9-118">In the Welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="75da9-119">设置你的Microsoft 365开发者帐户。</span><span class="sxs-lookup"><span data-stu-id="75da9-119">Set up your Microsoft 365 developer account.</span></span> 
   <span data-ttu-id="75da9-120">完成后，将显示以下屏幕：</span><span class="sxs-lookup"><span data-stu-id="75da9-120">After you finish, the following screen appears:</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="注册开发人员计划后看到Microsoft 365的示例。":::

1. <span data-ttu-id="75da9-122">登录以Teams新帐户登录。</span><span class="sxs-lookup"><span data-stu-id="75da9-122">Sign in to Teams with your new account.</span></span>
1. <span data-ttu-id="75da9-123">在客户端Teams，选择"应用 **"。**</span><span class="sxs-lookup"><span data-stu-id="75da9-123">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="75da9-124">验证你能否看到Upload **应用选项**。</span><span class="sxs-lookup"><span data-stu-id="75da9-124">Verify that you can see the **Upload a custom app** option.</span></span> <span data-ttu-id="75da9-125">如果你这样做，这意味着你可以旁加载应用。</span><span class="sxs-lookup"><span data-stu-id="75da9-125">If you do, this means you can sideload apps.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="插图显示可以在Teams上传自定义应用。":::

# <a name="have-a-tenant"></a>[<span data-ttu-id="75da9-127">拥有租户</span><span class="sxs-lookup"><span data-stu-id="75da9-127">Have a tenant</span></span>](#tab/have-a-tenant)

<span data-ttu-id="75da9-128">如果你已有租户，请验证你能否在租户中旁加载Teams。</span><span class="sxs-lookup"><span data-stu-id="75da9-128">If you already have a tenant, verify if you can sideload apps in Teams.</span></span>

<span data-ttu-id="75da9-129">**验证你能否旁加载应用**</span><span class="sxs-lookup"><span data-stu-id="75da9-129">**Verify that you can sideload your apps**</span></span> 

1. <span data-ttu-id="75da9-130">在"Teams客户端"中，选择"应用 **"。**</span><span class="sxs-lookup"><span data-stu-id="75da9-130">In the Teams Client, select **Apps**.</span></span> 
1.  <span data-ttu-id="75da9-131">验证你能否看到Upload **应用选项**。</span><span class="sxs-lookup"><span data-stu-id="75da9-131">Verify that you can see the **Upload a custom app** option.</span></span> <span data-ttu-id="75da9-132">如果你这样做，这意味着你可以旁加载应用。</span><span class="sxs-lookup"><span data-stu-id="75da9-132">If you do, this means you can sideload apps.</span></span> 

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="插图显示可以在Teams上传自定义应用。":::

---

### <a name="install-your-development-tools"></a><span data-ttu-id="75da9-134">安装开发工具</span><span class="sxs-lookup"><span data-stu-id="75da9-134">Install your development tools</span></span>

<span data-ttu-id="75da9-135">若要生成此应用，你将使用 Teams Toolkit for Visual Studio Code 快速入门。</span><span class="sxs-lookup"><span data-stu-id="75da9-135">To build this app, you'll use the Teams Toolkit for Visual Studio Code to quickly get started.</span></span> <span data-ttu-id="75da9-136">此外，Teams任何预先提供的工具生成应用。</span><span class="sxs-lookup"><span data-stu-id="75da9-136">You can also build Teams apps with any of your preffered tools.</span></span> 

> [!NOTE]
> <span data-ttu-id="75da9-137">Teams HTTPS 连接显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="75da9-137">Teams displays app content only through HTTPS connections.</span></span> <span data-ttu-id="75da9-138">若要在本地调试某些类型的应用（如自动程序），你将了解如何使用 ngrok 在 Teams 你的应用之间设置安全隧道。</span><span class="sxs-lookup"><span data-stu-id="75da9-138">To debug certain types of apps locally, such as a bot, you'll learn how to use ngrok to set up a secure tunnel between Teams and your app.</span></span>
> 
> <span data-ttu-id="75da9-139">生产Teams应用程序托管在云中。</span><span class="sxs-lookup"><span data-stu-id="75da9-139">Production Teams apps are hosted in the cloud.</span></span>

<span data-ttu-id="75da9-140">**安装Microsoft Teams工具**</span><span class="sxs-lookup"><span data-stu-id="75da9-140">**To install Microsoft Teams tools**</span></span>

1. <span data-ttu-id="75da9-141">安装 [Node.js](https://nodejs.org/en/)。</span><span class="sxs-lookup"><span data-stu-id="75da9-141">Install [Node.js](https://nodejs.org/en/).</span></span>
1. <span data-ttu-id="75da9-142">如果你计划构建机器人或消息传递扩展，请安装[ngrok，](https://ngrok.com/download)然后使用[ngrok 将 localhost 公开到 Internet。](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok)</span><span class="sxs-lookup"><span data-stu-id="75da9-142">If you plan to build a bot or messaging extension, install [ngrok](https://ngrok.com/download) and [expose your localhost to the Internet using ngrok](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok).</span></span>
1. <span data-ttu-id="75da9-143">安装最新版本的[Visual Studio Code](https://code.visualstudio.com/download)。</span><span class="sxs-lookup"><span data-stu-id="75da9-143">Install the latest version of [Visual Studio Code](https://code.visualstudio.com/download).</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="75da9-144">该工具包不支持早期版本的 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="75da9-144">The toolkit does not support earlier versions of Visual Studio Code.</span></span>

1. 在左侧活动栏中，选择"**扩展"。** :::image type="icon" source="../assets/icons/vs-code-extensions.png":::
1. <span data-ttu-id="75da9-146">在 **Microsoft Teams Toolkit** 中，选择"安装 **"。**</span><span class="sxs-lookup"><span data-stu-id="75da9-146">In **Microsoft Teams Toolkit**, select **Install**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="插图显示Visual Studio Code安装扩展Microsoft Teams Toolkit位置。":::

## <a name="1-create-your-app-project"></a><span data-ttu-id="75da9-148">1. 创建应用项目</span><span class="sxs-lookup"><span data-stu-id="75da9-148">1. Create your app project</span></span>

1. <span data-ttu-id="75da9-149">打开Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="75da9-149">Open Visual Studio Code.</span></span>
1. 选择 :::image type="icon" source="../assets/icons/vsc-toolkit.png":::  >  **Microsoft Teams Toolkit"新建Teams应用"。**

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-02.png" alt-text="Screenshot showing how to create your app project with the Visual Studio Code Teams Toolkit.":::
   
1. <span data-ttu-id="75da9-152">使用你的 Microsoft 365 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="75da9-152">Sign in with your Microsoft 365 development account.</span></span> <span data-ttu-id="75da9-153">可以是你刚刚创建的帐户，或者是你已经拥有允许应用旁加载的帐户。</span><span class="sxs-lookup"><span data-stu-id="75da9-153">Either the one you just created or the account you already had that allows app sideloading.</span></span>
1. <span data-ttu-id="75da9-154">在"**选择项目"屏幕上**，转到"个人应用"，然后选择 **"JS** (JavaScript) >**下一步"。**</span><span class="sxs-lookup"><span data-stu-id="75da9-154">On the **Select project** screen, go to **Personal app** and select **JS** (JavaScript) > **Next**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-03.png" alt-text="显示如何使用项目配置应用项目的Visual Studio Code Teams Toolkit。":::

1. <span data-ttu-id="75da9-156">输入你的应用Teams名称。</span><span class="sxs-lookup"><span data-stu-id="75da9-156">Enter a name for your Teams app.</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-04.png" alt-text="显示如何使用项目名称向应用项目添加名称的Visual Studio Code Teams Toolkit。":::

1. <span data-ttu-id="75da9-158">选择 **“完成”**。</span><span class="sxs-lookup"><span data-stu-id="75da9-158">Select **Finish**.</span></span> 
   <span data-ttu-id="75da9-159">现已配置项目。</span><span class="sxs-lookup"><span data-stu-id="75da9-159">Your project is now configured.</span></span> 

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="75da9-160">2. 了解应用项目组件</span><span class="sxs-lookup"><span data-stu-id="75da9-160">2. Understand your app project components</span></span>

<span data-ttu-id="75da9-161">在工具包配置应用项目后，你拥有用于生成"Hello， World！"的组件。</span><span class="sxs-lookup"><span data-stu-id="75da9-161">After the toolkit configures your app project, you have the components to build your "Hello, World!"</span></span> <span data-ttu-id="75da9-162">Teams应用。</span><span class="sxs-lookup"><span data-stu-id="75da9-162">Teams app.</span></span> <span data-ttu-id="75da9-163">项目的目录和文件位于"Visual Studio Code资源管理器"中。</span><span class="sxs-lookup"><span data-stu-id="75da9-163">The project's directories and files are located in the Visual Studio Code Explorer.</span></span> 

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-05.png" alt-text="Screenshot showing the scaffolding in your app project with the Visual Studio Code Teams Toolkit.":::

<span data-ttu-id="75da9-165">该工具包根据你在设置期间添加的功能，在目录中自动 `src` 创建应用基架。</span><span class="sxs-lookup"><span data-stu-id="75da9-165">The toolkit automatically creates app scaffolding in the `src` directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="75da9-166">由于你在设置期间创建了一个选项卡，因此目录中的文件将处理 `App.js` `src/components` 应用的初始化和路由。</span><span class="sxs-lookup"><span data-stu-id="75da9-166">Since you created a tab during setup, the `App.js` file in the `src/components` directory handles the initialization and routing of your app.</span></span> <span data-ttu-id="75da9-167">该文件还调用 Microsoft Teams JavaScript 客户端 SDK，以在应用和开发人员之间Teams。</span><span class="sxs-lookup"><span data-stu-id="75da9-167">The file also calls the Microsoft Teams JavaScript client SDK to establish communication between your app and Teams.</span></span> 

## <a name="3-build-and-run-your-app"></a><span data-ttu-id="75da9-168">3. 生成并运行应用</span><span class="sxs-lookup"><span data-stu-id="75da9-168">3. Build and run your app</span></span>

<span data-ttu-id="75da9-169">在本地生成并运行应用以节省时间。</span><span class="sxs-lookup"><span data-stu-id="75da9-169">Build and run your app locally to save time.</span></span> 

<span data-ttu-id="75da9-170">**生成和运行应用**</span><span class="sxs-lookup"><span data-stu-id="75da9-170">**To build and run your app**</span></span>

1. <span data-ttu-id="75da9-171">在Visual Studio Code中，选择"**查看终端**  >  **"。**</span><span class="sxs-lookup"><span data-stu-id="75da9-171">In Visual Studio Code, select **View** > **Terminal**.</span></span>
1. <span data-ttu-id="75da9-172">运行 `npm install`。</span><span class="sxs-lookup"><span data-stu-id="75da9-172">Run `npm install`.</span></span>
1. <span data-ttu-id="75da9-173">运行 `npm start`。</span><span class="sxs-lookup"><span data-stu-id="75da9-173">Run `npm start`.</span></span>
  
  <span data-ttu-id="75da9-174">编译 **成功！**</span><span class="sxs-lookup"><span data-stu-id="75da9-174">A **Compiled successfully!**</span></span> <span data-ttu-id="75da9-175">消息显示在终端中。</span><span class="sxs-lookup"><span data-stu-id="75da9-175">message appears in the terminal.</span></span> <span data-ttu-id="75da9-176">你的应用现在在 的 localhost 上运行 `https://localhost:3000` 。</span><span class="sxs-lookup"><span data-stu-id="75da9-176">Your app is now running on your localhost at `https://localhost:3000`.</span></span> 

## <a name="4-sideload-your-app-in-teams"></a><span data-ttu-id="75da9-177">4. 在应用程序中旁加载Teams</span><span class="sxs-lookup"><span data-stu-id="75da9-177">4. Sideload your app in Teams</span></span>

<span data-ttu-id="75da9-178">旁加载是在尚未由管理员或 Microsoft Teams安装应用的过程。</span><span class="sxs-lookup"><span data-stu-id="75da9-178">Sideloading is the process of installing an app in Teams that hasn't been approved by your admin or Microsoft.</span></span> <span data-ttu-id="75da9-179">在测试和调试应用时，旁加载Teams常见。</span><span class="sxs-lookup"><span data-stu-id="75da9-179">Sideloading is common when testing and debugging Teams apps.</span></span>

<span data-ttu-id="75da9-180">默认情况下，Teams不允许应用旁加载。</span><span class="sxs-lookup"><span data-stu-id="75da9-180">By default, Teams doesn't allow app sideloading.</span></span> <span data-ttu-id="75da9-181">可以在管理中心Teams此设置。</span><span class="sxs-lookup"><span data-stu-id="75da9-181">You can change this setting in the Teams admin center.</span></span>

<span data-ttu-id="75da9-182">**在应用程序中启用应用旁加载Teams**</span><span class="sxs-lookup"><span data-stu-id="75da9-182">**To enable app sideloading in Teams**</span></span>

1. <span data-ttu-id="75da9-183">使用[管理员Microsoft 365登录](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)管理中心。</span><span class="sxs-lookup"><span data-stu-id="75da9-183">Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credentials.</span></span>  
1. <span data-ttu-id="75da9-184">选择 **"显示所有**  >  **Teams"。**</span><span class="sxs-lookup"><span data-stu-id="75da9-184">Select **Show All** > **Teams**.</span></span> 

   ![管理中心菜单的图像](~/assets/images/prepare-test-tenant/admin-center.png)

   > [!Note] 
   > <span data-ttu-id="75da9-186">可能需要 24 小时才能显示 **Teams选项。**</span><span class="sxs-lookup"><span data-stu-id="75da9-186">It can take up to 24 hours for the **Teams** option to appear.</span></span> 

1. <span data-ttu-id="75da9-187">转到Teams **应用**  >  **设置策略**  >  全局 (组织范围内的默认) 。</span><span class="sxs-lookup"><span data-stu-id="75da9-187">Go to **Teams apps** > **Setup policies** > **Global** (Org-wide default).</span></span>

   ![打开旁加载视图](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

1. <span data-ttu-id="75da9-189">打开"上传 **自定义应用"** 切换。</span><span class="sxs-lookup"><span data-stu-id="75da9-189">Turn on the **upload custom apps** toggle.</span></span>

1. <span data-ttu-id="75da9-190">选择 **"保存** "保存更改。</span><span class="sxs-lookup"><span data-stu-id="75da9-190">Select **Save** to save the changes.</span></span>

   <span data-ttu-id="75da9-191">测试租户现在允许自定义应用旁加载。</span><span class="sxs-lookup"><span data-stu-id="75da9-191">Your test tenant now allows custom app sideloading.</span></span>

   > [!Note]
   > <span data-ttu-id="75da9-192">使用 App Studio 中的验证功能（包含在工具包中）旁加载应用之前检查问题。</span><span class="sxs-lookup"><span data-stu-id="75da9-192">Check for issues before sideloading your app using the validation feature in App Studio, which is included in the toolkit.</span></span> <span data-ttu-id="75da9-193">修复错误以成功旁加载应用。</span><span class="sxs-lookup"><span data-stu-id="75da9-193">Fix the errors to successfully sideload the app.</span></span>


### <a name="sideload-your-app"></a><span data-ttu-id="75da9-194">旁加载应用</span><span class="sxs-lookup"><span data-stu-id="75da9-194">Sideload your app</span></span>

1. <span data-ttu-id="75da9-195">在Visual Studio Code中，打开Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="75da9-195">In Visual Studio Code, open the Teams Toolkit.</span></span>
1. <span data-ttu-id="75da9-196">转到 **App Studio**。</span><span class="sxs-lookup"><span data-stu-id="75da9-196">Go to **App Studio**.</span></span>  
1. <span data-ttu-id="75da9-197">选择 **"测试和分发**  >  **安装"。**</span><span class="sxs-lookup"><span data-stu-id="75da9-197">Select **Test and Distribute** > **Install**.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-appstudio.png" alt-text="显示如何将应用旁加载至Teams客户端的屏幕截图Visual Studio Code Teams Toolkit。":::

<span data-ttu-id="75da9-199">**或者**</span><span class="sxs-lookup"><span data-stu-id="75da9-199">**Alternatively**</span></span>

1. <span data-ttu-id="75da9-200">选择 **F5** 键以打开要安装的浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="75da9-200">Select the **F5** key to open browser window to install.</span></span> <span data-ttu-id="75da9-201">这将跳过 **App Studio** 中的安装过程，Teams安装过程。</span><span class="sxs-lookup"><span data-stu-id="75da9-201">This will skip the installation process in the **App Studio** and lauch Teams in your browser.</span></span>
1. <span data-ttu-id="75da9-202">在安装对话框中，选择 **"添加**"以将应用安装到Teams。</span><span class="sxs-lookup"><span data-stu-id="75da9-202">In the installation dialog, select **Add** to install your app to Teams.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install.png" alt-text="显示如何将应用旁加载到客户端的Teams屏幕截图。":::

   > [!Note]
   > <span data-ttu-id="75da9-204">App Studio 还作为独立应用提供给 Teams 客户端。</span><span class="sxs-lookup"><span data-stu-id="75da9-204">App Studio is also available as a stand-alone app for Teams client.</span></span>

### <a name="troubleshoot-sideloading-issues"></a><span data-ttu-id="75da9-205">旁加载问题疑难解答</span><span class="sxs-lookup"><span data-stu-id="75da9-205">Troubleshoot sideloading issues</span></span>

<span data-ttu-id="75da9-206">**安装失败**</span><span class="sxs-lookup"><span data-stu-id="75da9-206">**Installation failed**</span></span>

<span data-ttu-id="75da9-207">如果在 `Manifest parsing has failed` 安装应用时显示错误消息，请验证应用信息输入是否正确。</span><span class="sxs-lookup"><span data-stu-id="75da9-207">If the `Manifest parsing has failed` error message appears while installing your app, verify that the app information is correctly entered.</span></span>

<span data-ttu-id="75da9-208">**验证应用信息**</span><span class="sxs-lookup"><span data-stu-id="75da9-208">**To verify the app information**</span></span>

* <span data-ttu-id="75da9-209">在Teams Toolkit中，转到 **App Studio**  >  **应用详细信息** 并验证是否输入了所有必需信息。</span><span class="sxs-lookup"><span data-stu-id="75da9-209">In the Teams Toolkit, go to **App Studio** > **App details** and verify that all the required information is correctly entered.</span></span>
*  <span data-ttu-id="75da9-210">如果手动编辑文件，请验证 JSON 在 App Studio 的应用清单工具 `manifest.json` 中是否定义良好。 </span><span class="sxs-lookup"><span data-stu-id="75da9-210">If you manually edited the `manifest.json` file, verify that the JSON is well-defined in the **App Manifest** tool in App Studio.</span></span>

<span data-ttu-id="75da9-211">**不显示选项卡内容**</span><span class="sxs-lookup"><span data-stu-id="75da9-211">**Tab content not displayed**</span></span>

<span data-ttu-id="75da9-212">验证你的应用是否正在运行。</span><span class="sxs-lookup"><span data-stu-id="75da9-212">Verify that your app is running.</span></span> <span data-ttu-id="75da9-213">如果不是，请转到终端并运行 `npm start` 。</span><span class="sxs-lookup"><span data-stu-id="75da9-213">If it isn't, go to the terminal and run `npm start`.</span></span>

## <a name="see-also"></a><span data-ttu-id="75da9-214">另请参阅</span><span class="sxs-lookup"><span data-stu-id="75da9-214">See also</span></span>

* [<span data-ttu-id="75da9-215">准备 Microsoft 365 租户</span><span class="sxs-lookup"><span data-stu-id="75da9-215">Prepare your Microsoft 365 tenant</span></span>](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant)
* [<span data-ttu-id="75da9-216">选择用于测试和调试应用Microsoft Teams设置</span><span class="sxs-lookup"><span data-stu-id="75da9-216">Choosing a setup to test and debug your Microsoft Teams app</span></span>](../concepts/build-and-test/debug.md)
* [<span data-ttu-id="75da9-217">使用 JavaScript 客户端 SDK 生成选项卡Microsoft Teams托管体验</span><span class="sxs-lookup"><span data-stu-id="75da9-217">Building tabs and other hosted experiences with the Microsoft Teams JavaScript client SDK</span></span>](../tabs/how-to/using-teams-client-sdk.md)
* [<span data-ttu-id="75da9-218">准备 AppSource 提交</span><span class="sxs-lookup"><span data-stu-id="75da9-218">Prepare for AppSource submission</span></span>](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [<span data-ttu-id="75da9-219">使用 App Studio for Microsoft Teams 快速开发应用</span><span class="sxs-lookup"><span data-stu-id="75da9-219">Quickly develop apps with App Studio for Microsoft Teams</span></span>](../concepts/build-and-test/app-studio-overview.md)
* [<span data-ttu-id="75da9-220">创建频道选项卡</span><span class="sxs-lookup"><span data-stu-id="75da9-220">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)

## <a name="next-step"></a><span data-ttu-id="75da9-221">后续步骤</span><span class="sxs-lookup"><span data-stu-id="75da9-221">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="75da9-222">为用户生成个人Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="75da9-222">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
