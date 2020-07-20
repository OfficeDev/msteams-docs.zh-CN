---
title: 使用 Microsoft 团队工具包和 Visual Studio Code 生成应用程序
description: 开始在 Visual Studio Code 中使用 Microsoft 团队工具包直接构建强大的自定义应用程序
keywords: 团队 visual studio code 工具包
ms.date: 06/30/2020
ms.openlocfilehash: 17f21d1656b32074318030b9df9e643200f58f80
ms.sourcegitcommit: ecf7ca8e77e77fe3f4cad1b13e3d31a825155555
ms.translationtype: Auto
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "45054250"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="32669-104">使用 Microsoft 团队工具包和 Visual Studio Code 生成应用程序</span><span class="sxs-lookup"><span data-stu-id="32669-104">Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="32669-105">Microsoft 团队工具包使你能够在 Visual Studio Code 环境中直接创建自定义团队应用。</span><span class="sxs-lookup"><span data-stu-id="32669-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio Code environment.</span></span> <span data-ttu-id="32669-106">该工具包将引导您完成整个过程，并提供生成、调试和启动团队应用程序所需的所有内容。</span><span class="sxs-lookup"><span data-stu-id="32669-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="32669-107">安装团队工具包</span><span class="sxs-lookup"><span data-stu-id="32669-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="32669-108">Visual studio Code 的 Microsoft 团队工具包可从[Visual Studio Marketplace](https://aka.ms/teams-toolkit)下载，也可直接作为 Visual studio code 中的扩展。</span><span class="sxs-lookup"><span data-stu-id="32669-108">The Microsoft Teams Toolkit for Visual Studio Code is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio Code.</span></span>

> [!TIP]
> <span data-ttu-id="32669-109">安装完成后，应在 Visual Studio Code 活动栏中看到 "团队" 工具包。</span><span class="sxs-lookup"><span data-stu-id="32669-109">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="32669-110">如果不是，请在活动栏中右键单击，然后选择 " **Microsoft 团队**" 以固定该工具包以方便访问。</span><span class="sxs-lookup"><span data-stu-id="32669-110">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="32669-111">使用工具包</span><span class="sxs-lookup"><span data-stu-id="32669-111">Using the toolkit</span></span>

- [<span data-ttu-id="32669-112">设置新项目</span><span class="sxs-lookup"><span data-stu-id="32669-112">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="32669-113">导入现有项目</span><span class="sxs-lookup"><span data-stu-id="32669-113">Import an existing project</span></span>](#import-an-existing-teams-app-project)
- [<span data-ttu-id="32669-114">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="32669-114">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="32669-115">打包应用程序</span><span class="sxs-lookup"><span data-stu-id="32669-115">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="32669-116">在团队中运行应用程序</span><span class="sxs-lookup"><span data-stu-id="32669-116">Run your app in Teams</span></span>](#run-your-app-in-teams)
- [<span data-ttu-id="32669-117">验证您的应用程序</span><span class="sxs-lookup"><span data-stu-id="32669-117">Validate your app</span></span>](#validate-your-app)
- [<span data-ttu-id="32669-118">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="32669-118">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="32669-119">设置新的团队项目</span><span class="sxs-lookup"><span data-stu-id="32669-119">Set up a new Teams project</span></span>

1. <span data-ttu-id="32669-120">在本地环境中为项目创建一个工作区/文件夹。</span><span class="sxs-lookup"><span data-stu-id="32669-120">Create a workspace/folder for your project in your local environment.</span></span>
1. <span data-ttu-id="32669-121">在 Visual Studio Code 中，选择 "团队" 图标</span><span class="sxs-lookup"><span data-stu-id="32669-121">In Visual Studio Code, select the Teams icon</span></span> ![Teams 图标](../assets/icons/favicon-16x16.png) <span data-ttu-id="32669-123">从窗口左侧的活动栏中进行。</span><span class="sxs-lookup"><span data-stu-id="32669-123">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="32669-124">从 "命令" 菜单中选择 **"打开 Microsoft 团队工具包"** 。</span><span class="sxs-lookup"><span data-stu-id="32669-124">Select **Open the Microsoft Teams Toolkit** from the command menu.</span></span>
1. <span data-ttu-id="32669-125">从 "命令" 菜单中选择 "**创建新的团队应用**"。</span><span class="sxs-lookup"><span data-stu-id="32669-125">Select **Create a new Teams app** from the command menu.</span></span>
1. <span data-ttu-id="32669-126">出现提示时，输入工作区的名称。</span><span class="sxs-lookup"><span data-stu-id="32669-126">When prompted, enter the name of the workspace .</span></span> <span data-ttu-id="32669-127">这将用作项目将驻留的文件夹的名称和应用程序的默认名称。</span><span class="sxs-lookup"><span data-stu-id="32669-127">This will be used as both the name of the folder where your project will reside, and the default name of your app.</span></span>
1. <span data-ttu-id="32669-128">按**enter** ，你将进入 "**添加功能**" 屏幕，为新应用配置属性。</span><span class="sxs-lookup"><span data-stu-id="32669-128">Press **Enter** and you will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="32669-129">选择 "**完成**" 按钮完成配置过程。</span><span class="sxs-lookup"><span data-stu-id="32669-129">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="import-an-existing-teams-app-project"></a><span data-ttu-id="32669-130">导入现有团队应用程序项目</span><span class="sxs-lookup"><span data-stu-id="32669-130">Import an existing Teams app project</span></span>

1. <span data-ttu-id="32669-131">在 Visual Studio Code 中，选择 "团队" 图标</span><span class="sxs-lookup"><span data-stu-id="32669-131">In Visual Studio Code, select the Teams icon</span></span> ![Teams 图标](../assets/icons/favicon-16x16.png) <span data-ttu-id="32669-133">从窗口左侧的活动栏中进行。</span><span class="sxs-lookup"><span data-stu-id="32669-133">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="32669-134">从 "命令" 菜单中选择 "**导入应用程序包**"。</span><span class="sxs-lookup"><span data-stu-id="32669-134">Select **Import app package** from the command menu.</span></span>
1. <span data-ttu-id="32669-135">选择现有[团队应用程序包](../concepts/build-and-test/apps-package.md)zip 文件。</span><span class="sxs-lookup"><span data-stu-id="32669-135">Choose your existing [Teams app package](../concepts/build-and-test/apps-package.md) zip file.</span></span>
1. <span data-ttu-id="32669-136">选择 "**选择发布包**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="32669-136">Choose the **Select publishing package** button.</span></span> <span data-ttu-id="32669-137">此时，工具包的 "配置" 选项卡应包含您的应用程序的详细信息。</span><span class="sxs-lookup"><span data-stu-id="32669-137">The configuration tab of the toolkit should now be populated with your app's details.</span></span>
1. <span data-ttu-id="32669-138">在 visual studio code 中，选择 "**文件**" "  ->  **将文件夹添加到工作区**"，将源代码目录添加到 Visual studio code Workspace。</span><span class="sxs-lookup"><span data-stu-id="32669-138">In Visual Studio Code, select **File** -> **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="32669-139">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="32669-139">Configure your app</span></span>

<span data-ttu-id="32669-140">在其核心中，团队应用程序包含三个组件：</span><span class="sxs-lookup"><span data-stu-id="32669-140">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="32669-141">Microsoft 团队客户端（web、桌面或移动版），用户与您的应用程序进行交互。</span><span class="sxs-lookup"><span data-stu-id="32669-141">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="32669-142">对将在团队中显示的内容请求做出响应的服务器，例如，HTML 选项卡内容或 bot 自适应卡。</span><span class="sxs-lookup"><span data-stu-id="32669-142">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="32669-143">由三个文件组成的团队[应用程序包](/concepts/build-and-test/apps-package.md)：</span><span class="sxs-lookup"><span data-stu-id="32669-143">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="32669-144">上的 manifest.js</span><span class="sxs-lookup"><span data-stu-id="32669-144">The manifest.json</span></span> 
  > - <span data-ttu-id="32669-145">显示在公用或组织应用程序目录中的应用程序的[彩色图标](../resources/schema/manifest-schema.md#icons)</span><span class="sxs-lookup"><span data-stu-id="32669-145">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="32669-146">"团队" 活动栏中显示的[大纲图标](../resources/schema/manifest-schema.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="32669-146">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="32669-147">在安装应用程序时，团队客户端会分析清单文件以确定所需的信息，如应用程序的名称和服务所在的 URL。</span><span class="sxs-lookup"><span data-stu-id="32669-147">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="32669-148">若要配置您的应用程序，请导航到 Visual Studio Code 中的 " **Microsoft 团队工具包**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="32669-148">To configure your app, navigate to the **Microsoft Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="32669-149">选择 "**编辑应用程序包**" 以查看**应用程序详细信息**页。</span><span class="sxs-lookup"><span data-stu-id="32669-149">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="32669-150">编辑应用程序详细信息页中的字段将更新作为应用程序包一部分最终交付的文件上的 manifest.js的内容。</span><span class="sxs-lookup"><span data-stu-id="32669-150">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> [<span data-ttu-id="32669-151">了解更多</span><span class="sxs-lookup"><span data-stu-id="32669-151">Learn more</span></span>](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a><span data-ttu-id="32669-152">打包应用程序</span><span class="sxs-lookup"><span data-stu-id="32669-152">Package your app</span></span>

<span data-ttu-id="32669-153">修改您的应用**程序详细信息**页面或更新**清单**，或应用程序的 **. publish**文件夹中的**env**文件将自动生成**Development.zip**文件。</span><span class="sxs-lookup"><span data-stu-id="32669-153">Modifying your the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="32669-154">您需要在同一文件夹中包含[两个图标](../concepts/build-and-test/apps-package.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="32669-154">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="32669-155">在本地安装和运行应用程序</span><span class="sxs-lookup"><span data-stu-id="32669-155">Install and run your app locally</span></span>

<span data-ttu-id="32669-156">有关打包和测试应用程序的详细说明，请参阅在项目主页中*构建和运行*内容。</span><span class="sxs-lookup"><span data-stu-id="32669-156">Refer to the \**Build and Run* content in your project homepage for detailed instructions for packaging and testing your app.</span></span> <span data-ttu-id="32669-157">通常情况下，您需要安装应用程序的服务器，使其运行，然后设置隧道解决方案，以便团队可以访问本地主机中运行的内容。</span><span class="sxs-lookup"><span data-stu-id="32669-157">In general, you need to install your app's server, get it running, then setup a tunneling solution so that Teams can access content running from localhost.</span></span>

## <a name="add-a-trusted-certificate-for-localhost"></a><span data-ttu-id="32669-158">为本地主机添加受信任证书</span><span class="sxs-lookup"><span data-stu-id="32669-158">Add a trusted certificate for localhost</span></span>

<span data-ttu-id="32669-159">如果您希望使用 https 在 localhost 上调试基于选项卡的应用程序，则需要将 localhost 的证书添加到 `Trusted Root Certification Authorities` 目录中。</span><span class="sxs-lookup"><span data-stu-id="32669-159">If you wish to debug your tab based app on localhost using https, you will need to add a certificate for localhost to `Trusted Root Certification Authorities` catalog.</span></span> <span data-ttu-id="32669-160">每台计算机只需完成一次此步骤。</span><span class="sxs-lookup"><span data-stu-id="32669-160">You only need to complete this step once per machine.</span></span></br></br>

<span data-ttu-id="32669-161">**创建并安装受信任的证书：**
<details>
  </span><span class="sxs-lookup"><span data-stu-id="32669-161">**Create and install a trusted certificate:**
<details>
  </span></span><summary><span data-ttu-id="32669-162">在此处展开</span><span class="sxs-lookup"><span data-stu-id="32669-162">Expand here</span></span></summary>

* <span data-ttu-id="32669-163">构建并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="32669-163">Build and run your app</span></span>
  * <span data-ttu-id="32669-164">按照项目自述文件的 "**生成和运行**" 部分中的 instuctions 操作，以便从提供服务 https://localhost:3000/tab 。通常情况下，这将涉及执行， `npm install` 然后`npm start`</span><span class="sxs-lookup"><span data-stu-id="32669-164">Follow the instuctions in the **Build and Run** section of your project Readme so that it's being served from https://localhost:3000/tab. Generally, this will involve executing `npm install` then `npm start`</span></span>
  * <span data-ttu-id="32669-165">https://localhost:3000/tab从 Google Chrome 导航到</span><span class="sxs-lookup"><span data-stu-id="32669-165">Navigate to https://localhost:3000/tab from Google Chrome</span></span>

* <span data-ttu-id="32669-166">获取 SSL 证书：</span><span class="sxs-lookup"><span data-stu-id="32669-166">Acquire the SSL certificate:</span></span>
  * <span data-ttu-id="32669-167">打开 "Chrome 开发人员工具" 窗口（ `ctrl + shift + i`  /  `cmd + option + i` ）。</span><span class="sxs-lookup"><span data-stu-id="32669-167">Open the Chrome Developer Tools window (`ctrl + shift + i` / `cmd + option + i`).</span></span>
  * <span data-ttu-id="32669-168">在 `Security` 选项卡上单击</span><span class="sxs-lookup"><span data-stu-id="32669-168">Click on the `Security` tab</span></span>
  * <span data-ttu-id="32669-169">单击 "启用"， `View certificate` 可以选择下载证书，方法是在 OS X 中将其拖放到桌面，或者单击 `Details` Windows 中的选项卡，然后单击`Copy to File…`</span><span class="sxs-lookup"><span data-stu-id="32669-169">Click on `View certificate` and you’ll have the option to download the certificate — either by dragging it to your desktop in OS X, or by clicking on the `Details` tab in Windows and clicking `Copy to File…`</span></span>
  * <span data-ttu-id="32669-170">将该文件命名为 <*任何内容*> .cer，并将其保存到不需要管理员同意执行写入操作的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="32669-170">Name the file <*anything*>.cer and save it to a folder that doesn't require admin consent to perform a write action.</span></span>
  
* <span data-ttu-id="32669-171">在**Windows**上安装证书</span><span class="sxs-lookup"><span data-stu-id="32669-171">Install the certificate on **Windows**</span></span>
  * <span data-ttu-id="32669-172">选择 `DER encoded binary X.509 (.CER)` 选项（第一个选项）并保存它。</span><span class="sxs-lookup"><span data-stu-id="32669-172">Choose the `DER encoded binary X.509 (.CER)` option (the first one) and save it.</span></span>
  * <span data-ttu-id="32669-173">双击证书并安装它。</span><span class="sxs-lookup"><span data-stu-id="32669-173">Double click on the certificate and install it.</span></span>
  * <span data-ttu-id="32669-174">选取`Local Machine`</span><span class="sxs-lookup"><span data-stu-id="32669-174">Choose `Local Machine`</span></span>
  * <span data-ttu-id="32669-175">选定`Place all certificates in the following store`</span><span class="sxs-lookup"><span data-stu-id="32669-175">Select `Place all certificates in the following store`</span></span>
  * <span data-ttu-id="32669-176">选取`Trusted Root Certification Authorities`</span><span class="sxs-lookup"><span data-stu-id="32669-176">Choose `Trusted Root Certification Authorities`</span></span>
  * <span data-ttu-id="32669-177">确认安装</span><span class="sxs-lookup"><span data-stu-id="32669-177">Confirm your installation</span></span>
  
* <span data-ttu-id="32669-178">安装证书**MAC OS X**</span><span class="sxs-lookup"><span data-stu-id="32669-178">Install the certificate **Mac OS X**</span></span>
  * <span data-ttu-id="32669-179">在 OS X 上，打开密钥链 Access 实用工具，并 `System` 从左侧的菜单中选择。</span><span class="sxs-lookup"><span data-stu-id="32669-179">On OS X, open the Keychain Access utility and select `System` from the menu on the left.</span></span> <span data-ttu-id="32669-180">单击锁定图标可启用更改。</span><span class="sxs-lookup"><span data-stu-id="32669-180">Click the lock icon to enable changes.</span></span>
  * <span data-ttu-id="32669-181">单击靠近底部的加号按钮以添加新证书，然后选择 `localhost.cer` 您拖到桌面的文件。</span><span class="sxs-lookup"><span data-stu-id="32669-181">Click the plus button near the bottom to add a new certificate, and select the `localhost.cer` file you dragged to the desktop.</span></span> <span data-ttu-id="32669-182">`Always Trust`在出现的对话框中单击。</span><span class="sxs-lookup"><span data-stu-id="32669-182">Click `Always Trust` in the dialog that appears.</span></span>
  * <span data-ttu-id="32669-183">将证书添加到系统密钥链后，双击证书并展开 `Trust` 证书详细信息部分。</span><span class="sxs-lookup"><span data-stu-id="32669-183">After adding the certificate to the system keychain, double-click the certificate and expand the `Trust` section of the certificate details.</span></span> <span data-ttu-id="32669-184">`Always Trust`为每个选项选择。</span><span class="sxs-lookup"><span data-stu-id="32669-184">Select `Always Trust` for every option.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32669-185">如果收到安全证书警告，请导航到 https://localhost:3000/tab 。如果网站仍不受信任，请重新启动您的计算机，并应接受为受信任的本地主机。</span><span class="sxs-lookup"><span data-stu-id="32669-185">If you receive a security certificate warning, navigate to https://localhost:3000/tab. If the site is still not trusted, reboot your machine and localhost should be accepted as trusted.</span></span>
</details>

## <a name="run-your-app-in-teams"></a><span data-ttu-id="32669-186">在团队中运行应用程序</span><span class="sxs-lookup"><span data-stu-id="32669-186">Run your app in Teams</span></span>
- <span data-ttu-id="32669-187">先决条件：</span><span class="sxs-lookup"><span data-stu-id="32669-187">Prerequisites:</span></span>
  - [<span data-ttu-id="32669-188">启用团队开发人员预览模式</span><span class="sxs-lookup"><span data-stu-id="32669-188">Enable Teams developer preview mode</span></span>](https://aka.ms/teams-toolkit-enable-devpreview)

1. <span data-ttu-id="32669-189">导航到 Visual Studio "代码" 窗口左侧的 "活动" 栏。</span><span class="sxs-lookup"><span data-stu-id="32669-189">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="32669-190">选择 "**运行**" 图标以显示 "**运行" 和 "调试**" 视图。</span><span class="sxs-lookup"><span data-stu-id="32669-190">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="32669-191">您还可以使用键盘快捷方式 `Ctrl+Shift+D` 。</span><span class="sxs-lookup"><span data-stu-id="32669-191">You can also use the keyboard shortcut `Ctrl+Shift+D`.</span></span>

## <a name="validate-your-app"></a><span data-ttu-id="32669-192">验证您的应用程序</span><span class="sxs-lookup"><span data-stu-id="32669-192">Validate your app</span></span>

<span data-ttu-id="32669-193">通过 "**验证**" 页面，您可以在将应用程序提交到 AppSource 之前检查应用程序包。</span><span class="sxs-lookup"><span data-stu-id="32669-193">The **Validate** page allows you to check your app package before submitting your app to AppSource.</span></span> <span data-ttu-id="32669-194">只需上传清单包，验证工具就会检查应用程序是否符合所有与清单相关的测试用例。</span><span class="sxs-lookup"><span data-stu-id="32669-194">Simply upload the manifest package and the validation tool will check your app against all manifest related test cases.</span></span> <span data-ttu-id="32669-195">对于每个失败的测试，说明提供的文档链接可帮助您修复错误。</span><span class="sxs-lookup"><span data-stu-id="32669-195">For each failed tests, the description provides a documentation link to help you fix the error.</span></span> <span data-ttu-id="32669-196">对于难以自动化的测试，**初步清单**详细说明了最常见的失败测试事例的7，以及指向完整提交核对清单的链接。</span><span class="sxs-lookup"><span data-stu-id="32669-196">For the tests that are hard to automate, the **Preliminary checklist** details 7 of the most common failed test cases as well as link to a complete submission checklist.</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="32669-197">将您的应用程序发布到团队</span><span class="sxs-lookup"><span data-stu-id="32669-197">Publish your app to Teams</span></span>

<span data-ttu-id="32669-198">在您的项目主页上，您可以将应用程序上载到团队，将您的应用程序提交到贵组织中用户的公司自定义应用商店，或将您的应用程序提交到所有团队用户的应用程序源。</span><span class="sxs-lookup"><span data-stu-id="32669-198">On your project home page, you can upload your app to a team, submit your app to your company custom app store for users in your organization, or submit your app to App Source for all Teams users.</span></span> <span data-ttu-id="32669-199">你的 IT 管理员将查看这些提交。</span><span class="sxs-lookup"><span data-stu-id="32669-199">Your IT admin will review these submissions.</span></span> <span data-ttu-id="32669-200">您可以返回到 "*发布*" 页面以查看您的提交状态，并了解您的应用程序是否已由 IT 管理员批准或拒绝。此外，您还可以将更新提交到您的应用程序或取消任何当前活动的提交。</span><span class="sxs-lookup"><span data-stu-id="32669-200">You can return to the *Publish* page to check on your submission status and learn if your app was approved or rejected by your IT admin. This is also where you'll come to submit updates to your app or cancel any currently active submissions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="32669-201">下一步：维护和支持发布的应用程序</span><span class="sxs-lookup"><span data-stu-id="32669-201">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
