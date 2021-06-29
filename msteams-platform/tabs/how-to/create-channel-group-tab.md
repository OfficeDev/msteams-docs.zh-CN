---
title: 创建频道或组选项卡
author: laujan
description: 使用 Yeoman 生成器为用户创建频道和组选项卡的快速Microsoft Teams。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: fedaf3ec639917110e16c666734fa3eedbcda18e
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179974"
---
# <a name="create-a-channel-or-group-tab"></a><span data-ttu-id="d92dc-103">创建频道或组选项卡</span><span class="sxs-lookup"><span data-stu-id="d92dc-103">Create a channel or group tab</span></span>

## <a name="create-a-custom-channel-or-group-tab"></a><span data-ttu-id="d92dc-104">创建自定义频道或组选项卡</span><span class="sxs-lookup"><span data-stu-id="d92dc-104">Create a custom channel or group tab</span></span>

<span data-ttu-id="d92dc-105">可以使用 Yeoman 生成器、ASP.NETCore Node.js ASP.NETCore MVC 创建频道或组选项卡。</span><span class="sxs-lookup"><span data-stu-id="d92dc-105">You can create a channel or group tab using Node.js and the Yeoman Generator, ASP.NETCore, or ASP.NETCore MVC.</span></span>

# <a name="nodejs"></a>[<span data-ttu-id="d92dc-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="d92dc-106">Node.js</span></span>](#tab/nodejs)

### <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator"></a><span data-ttu-id="d92dc-107">使用 Yeoman 生成器和 Node.js创建自定义频道和组选项卡</span><span class="sxs-lookup"><span data-stu-id="d92dc-107">Create a custom channel and group tab using Node.js and the Yeoman Generator</span></span>

> [!NOTE]
> <span data-ttu-id="d92dc-108">本文遵循 Microsoft OfficeDev Microsoft Teams存储库中构建您的第一个 GitHub [App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki 中概述的步骤。</span><span class="sxs-lookup"><span data-stu-id="d92dc-108">This article follows the steps outlined in the [build Your first Microsoft Teams app](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="d92dc-109">You can create a custom channel or group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span><span class="sxs-lookup"><span data-stu-id="d92dc-109">You can create a custom channel or group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span></span>

### <a name="prerequisites-for-apps"></a><span data-ttu-id="d92dc-110">应用的先决条件</span><span class="sxs-lookup"><span data-stu-id="d92dc-110">Prerequisites for apps</span></span>

<span data-ttu-id="d92dc-111">您必须了解以下先决条件：</span><span class="sxs-lookup"><span data-stu-id="d92dc-111">You must have an understanding of the following prerequisites:</span></span>

- <span data-ttu-id="d92dc-112">你必须拥有一个Office 365租户和一个已启用"允许上载 **自定义应用"的团队**。</span><span class="sxs-lookup"><span data-stu-id="d92dc-112">You must have an Office 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="d92dc-113">有关详细信息，请参阅[准备你的Office 365租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="d92dc-113">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="d92dc-114">如果当前没有 Office 365 帐户，可以通过开发人员计划注册Office 365订阅。</span><span class="sxs-lookup"><span data-stu-id="d92dc-114">If you do not currently have an Office 365 account, you can sign up for a free subscription through the Office 365 Developer Program.</span></span> <span data-ttu-id="d92dc-115">只要将订阅用于正在进行的开发，订阅就保持活动状态。</span><span class="sxs-lookup"><span data-stu-id="d92dc-115">The subscription remains active as long as you are using it for ongoing development.</span></span> <span data-ttu-id="d92dc-116">请参阅[欢迎使用 Office 365 开发人员计划](/office/developer-program/microsoft-365-developer-program)。</span><span class="sxs-lookup"><span data-stu-id="d92dc-116">See [welcome to the Office 365 Developer Program](/office/developer-program/microsoft-365-developer-program).</span></span>

<span data-ttu-id="d92dc-117">此外，此项目要求在开发环境中安装以下内容：</span><span class="sxs-lookup"><span data-stu-id="d92dc-117">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="d92dc-118">任何文本编辑器或 IDE。</span><span class="sxs-lookup"><span data-stu-id="d92dc-118">Any text editor or IDE.</span></span> <span data-ttu-id="d92dc-119">你可以免费安装和[Visual Studio Code](https://code.visualstudio.com/download)应用程序。</span><span class="sxs-lookup"><span data-stu-id="d92dc-119">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

- <span data-ttu-id="d92dc-120">[Node.js/npm](https://nodejs.org/en/)。</span><span class="sxs-lookup"><span data-stu-id="d92dc-120">[Node.js/npm](https://nodejs.org/en/).</span></span> <span data-ttu-id="d92dc-121">使用最新的 LTS 版本。</span><span class="sxs-lookup"><span data-stu-id="d92dc-121">Use the latest LTS version.</span></span> <span data-ttu-id="d92dc-122">Node 程序包管理器 (npm) 在系统中安装 Node.js。</span><span class="sxs-lookup"><span data-stu-id="d92dc-122">The Node Package Manager (npm) installs in your system with the installation of Node.js.</span></span>

- <span data-ttu-id="d92dc-123">在成功安装 Node.js，在命令提示符中输入以下内容来安装 [Yeoman](https://yeoman.io/) 和 [gulp-cli](https://www.npmjs.com/package/gulp-cli) 程序包：</span><span class="sxs-lookup"><span data-stu-id="d92dc-123">After you have successfully installed Node.js, install the [Yeoman](https://yeoman.io/) and [gulp-cli](https://www.npmjs.com/package/gulp-cli) packages by entering the following in your command prompt:</span></span>

    ```bash
    npm install yo gulp-cli --global
    ```

- <span data-ttu-id="d92dc-124">在命令Microsoft Teams输入以下内容，安装应用生成器：</span><span class="sxs-lookup"><span data-stu-id="d92dc-124">Install the Microsoft Teams Apps generator by entering the following in your command prompt:</span></span>

    ```bash
    npm install generator-teams --global
    ```

### <a name="generate-your-project"></a><span data-ttu-id="d92dc-125">生成项目</span><span class="sxs-lookup"><span data-stu-id="d92dc-125">Generate your project</span></span>

<span data-ttu-id="d92dc-126">**生成项目**</span><span class="sxs-lookup"><span data-stu-id="d92dc-126">**To generate your project**</span></span>

1. <span data-ttu-id="d92dc-127">在命令提示符下，为选项卡项目创建新目录。</span><span class="sxs-lookup"><span data-stu-id="d92dc-127">At a command prompt, create a new directory for your tab project.</span></span>

1. <span data-ttu-id="d92dc-128">若要启动生成器，请转到新目录并键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="d92dc-128">To start the generator, go to your new directory and type the following command:</span></span>

    ```bash
    yo teams
    ```

1. <span data-ttu-id="d92dc-129">接下来，提供一系列用于应用程序文件上的 **manifest.js值：**</span><span class="sxs-lookup"><span data-stu-id="d92dc-129">Next, provide a series of values that are used in your application's **manifest.json** file:</span></span>

    ![生成器打开屏幕截图](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    <span data-ttu-id="d92dc-131">**你的解决方案名称是什么？**</span><span class="sxs-lookup"><span data-stu-id="d92dc-131">**What is your solution name?**</span></span>

    <span data-ttu-id="d92dc-132">这是项目名称。</span><span class="sxs-lookup"><span data-stu-id="d92dc-132">This is your project name.</span></span> <span data-ttu-id="d92dc-133">可以通过选择 Enter 键来 **接受建议的名称** 。</span><span class="sxs-lookup"><span data-stu-id="d92dc-133">You can accept the suggested name by selecting the **Enter** key.</span></span>

    <span data-ttu-id="d92dc-134">**要将文件存放在哪里?**</span><span class="sxs-lookup"><span data-stu-id="d92dc-134">**Where do you want to place the files?**</span></span>

    <span data-ttu-id="d92dc-135">您当前在项目目录中。</span><span class="sxs-lookup"><span data-stu-id="d92dc-135">You are currently in your project directory.</span></span> <span data-ttu-id="d92dc-136">选择 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="d92dc-136">Select **Enter**.</span></span>

    <span data-ttu-id="d92dc-137">**你的应用Microsoft Teams标题？**</span><span class="sxs-lookup"><span data-stu-id="d92dc-137">**Title of your Microsoft Teams app project?**</span></span>

    <span data-ttu-id="d92dc-138">这是你的应用包名称，将在应用清单和说明中使用。</span><span class="sxs-lookup"><span data-stu-id="d92dc-138">This is your app package name and will be used in the app manifest and description.</span></span> <span data-ttu-id="d92dc-139">输入标题或按 **Enter** 接受默认名称。</span><span class="sxs-lookup"><span data-stu-id="d92dc-139">Enter a title or select **Enter** to accept the default name.</span></span>

    <span data-ttu-id="d92dc-140">**你的 (公司) 名称？ (最多 32 个字符)**</span><span class="sxs-lookup"><span data-stu-id="d92dc-140">**Your (company) name? (max 32 characters)**</span></span>

    <span data-ttu-id="d92dc-141">你的公司名称将在应用清单中使用。</span><span class="sxs-lookup"><span data-stu-id="d92dc-141">Your company name will be used in the app manifest.</span></span> <span data-ttu-id="d92dc-142">输入公司名称或选择 **Enter** 接受默认名称。</span><span class="sxs-lookup"><span data-stu-id="d92dc-142">Enter a company name or select **Enter** to accept the default name.</span></span>

    <span data-ttu-id="d92dc-143">**要使用哪个清单版本？**</span><span class="sxs-lookup"><span data-stu-id="d92dc-143">**Which manifest version would you like to use?**</span></span>

    <span data-ttu-id="d92dc-144">选择默认架构。</span><span class="sxs-lookup"><span data-stu-id="d92dc-144">Select the default schema.</span></span>

    <span data-ttu-id="d92dc-145">**快速基架？ (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="d92dc-145">**Quick scaffolding? (Y/n)**</span></span>

    <span data-ttu-id="d92dc-146">默认值为 yes;输入 **n** 以输入你的 Microsoft 合作伙伴 ID。</span><span class="sxs-lookup"><span data-stu-id="d92dc-146">The default is yes; enter **n** to enter your Microsoft Partner Id.</span></span>

    <span data-ttu-id="d92dc-147">**输入你的 Microsoft 合作伙伴 ID（如果有） (留空可跳过)**</span><span class="sxs-lookup"><span data-stu-id="d92dc-147">**Enter your Microsoft Partner Id, if you have one? (Leave blank to skip)**</span></span>

    <span data-ttu-id="d92dc-148">此字段不是必需的，并且应该仅在你已是 Microsoft 合作伙伴网络的一 [部分时使用](https://partner.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="d92dc-148">This field is not required and should only be used if you are already part of the [Microsoft Partner Network](https://partner.microsoft.com).</span></span>

    <span data-ttu-id="d92dc-149">**要向项目添加哪些内容？**</span><span class="sxs-lookup"><span data-stu-id="d92dc-149">**What do you want to add to your project?**</span></span>

    <span data-ttu-id="d92dc-150">选择 **&ast; () 选项卡"。**</span><span class="sxs-lookup"><span data-stu-id="d92dc-150">Select **( &ast; ) A Tab**.</span></span>

    <span data-ttu-id="d92dc-151">**将在其中托管此解决方案的 URL？**</span><span class="sxs-lookup"><span data-stu-id="d92dc-151">**The URL where you will host this solution?**</span></span>

    <span data-ttu-id="d92dc-152">默认情况下，生成器建议 Azure 网站 URL。</span><span class="sxs-lookup"><span data-stu-id="d92dc-152">By default the generator suggests an Azure Web Sites URL.</span></span> <span data-ttu-id="d92dc-153">由于你仅在本地测试应用，因此不需要有效的 URL。</span><span class="sxs-lookup"><span data-stu-id="d92dc-153">You are only testing your app locally, therefore, a valid URL is not necessary.</span></span>

    <span data-ttu-id="d92dc-154">**在应用/选项卡加载时是否显示加载指示器？**</span><span class="sxs-lookup"><span data-stu-id="d92dc-154">**Would you like show a loading indicator when your app/tab loads?**</span></span>

    <span data-ttu-id="d92dc-155">选择 **在** 应用或选项卡加载时不包括加载指示器。</span><span class="sxs-lookup"><span data-stu-id="d92dc-155">Choose **not** to include a loading indicator when your app or tab loads.</span></span> <span data-ttu-id="d92dc-156">默认值为"否"，输入 **n**。</span><span class="sxs-lookup"><span data-stu-id="d92dc-156">The default is no, enter **n**.</span></span>

   <span data-ttu-id="d92dc-157">**是否希望在无选项卡标题栏的情况下呈现个人应用?**</span><span class="sxs-lookup"><span data-stu-id="d92dc-157">**Would you like personal apps to be rendered without a tab header-bar?**</span></span>

    <span data-ttu-id="d92dc-158">选择 **不包括** 在没有选项卡标题栏的情况下呈现的个人应用。</span><span class="sxs-lookup"><span data-stu-id="d92dc-158">Choose **not** to include personal apps to be rendered without a tab header-bar.</span></span> <span data-ttu-id="d92dc-159">默认值为否，输入 **n**。</span><span class="sxs-lookup"><span data-stu-id="d92dc-159">Default is no, enter **n**.</span></span>

    <span data-ttu-id="d92dc-160">**是否包含测试框架和初始测试？ (y/N)**</span><span class="sxs-lookup"><span data-stu-id="d92dc-160">**Would you like to include Test framework and initial tests? (y/N)**</span></span>

    <span data-ttu-id="d92dc-161">选择 **不包括** 此项目的测试框架。</span><span class="sxs-lookup"><span data-stu-id="d92dc-161">Choose **not** to include a test framework for this project.</span></span> <span data-ttu-id="d92dc-162">默认值为 yes;输入 **n**。</span><span class="sxs-lookup"><span data-stu-id="d92dc-162">The default is yes; enter **n**.</span></span>

    <span data-ttu-id="d92dc-163">**是否将 Azure 应用程序Insights遥测？ (y/N)**</span><span class="sxs-lookup"><span data-stu-id="d92dc-163">**Would you like to use Azure Applications Insights for telemetry? (y/N)**</span></span>

    <span data-ttu-id="d92dc-164">选择 **不包括** [Azure 应用程序Insights。](/azure/azure-monitor/app/app-insights-overview)</span><span class="sxs-lookup"><span data-stu-id="d92dc-164">Choose **not** to include [Azure Application Insights](/azure/azure-monitor/app/app-insights-overview).</span></span> <span data-ttu-id="d92dc-165">默认值为"否";输入 **n**。</span><span class="sxs-lookup"><span data-stu-id="d92dc-165">The default is no; enter **n**.</span></span>

    <span data-ttu-id="d92dc-166">**默认选项卡名称 (最多为 16 个字符) ？**</span><span class="sxs-lookup"><span data-stu-id="d92dc-166">**Default Tab Name (max 16 characters)?**</span></span>

    <span data-ttu-id="d92dc-167">命名选项卡。此选项卡名称将在整个项目中用作文件或 URL 路径组件。</span><span class="sxs-lookup"><span data-stu-id="d92dc-167">Name your tab. This tab name will be used throughout your project as a file or URL path component.</span></span>

    <span data-ttu-id="d92dc-168">**要创建哪种类型的选项卡？**</span><span class="sxs-lookup"><span data-stu-id="d92dc-168">**What kind of Tab would you like to create?**</span></span>

    <span data-ttu-id="d92dc-169">使用箭头键选择"可 **配置"** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="d92dc-169">Use the arrow keys to select **Configurable** tab.</span></span>

    <span data-ttu-id="d92dc-170">**您打算对 Tab 使用哪些范围？**</span><span class="sxs-lookup"><span data-stu-id="d92dc-170">**What scopes do you intend to use for your Tab?**</span></span>

    <span data-ttu-id="d92dc-171">可以选择团队或群聊。</span><span class="sxs-lookup"><span data-stu-id="d92dc-171">You can select a team or a group chat.</span></span>

    <span data-ttu-id="d92dc-172">**是否需对选项卡提供 Azure AD 单一登录支持？**</span><span class="sxs-lookup"><span data-stu-id="d92dc-172">**Do you require Azure AD Single-Sign-On support for the tab?**</span></span>

    <span data-ttu-id="d92dc-173">选择 **不包括** 选项卡的 Azure AD 单一登录支持。默认值为"是"，输入 **n**。</span><span class="sxs-lookup"><span data-stu-id="d92dc-173">Choose **not** to include Azure AD Single-Sign-On support for the tab. The default is yes, enter **n**.</span></span>

    <span data-ttu-id="d92dc-174">**是否希望此选项卡在 SharePoint Online 中可用？ (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="d92dc-174">**Do you want this tab to be available in SharePoint Online? (Y/n)**</span></span>

    <span data-ttu-id="d92dc-175">输入 **n**。</span><span class="sxs-lookup"><span data-stu-id="d92dc-175">Enter **n**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d92dc-176">path component **yourDefaultTabNameTab**， is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span><span class="sxs-lookup"><span data-stu-id="d92dc-176">The path component **yourDefaultTabNameTab**, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
    >
    > <span data-ttu-id="d92dc-177">例如：DefaultTabName：MyTab   >  **/MyTabTab/**</span><span class="sxs-lookup"><span data-stu-id="d92dc-177">For example: DefaultTabName: **MyTab** > **/MyTabTab/**</span></span>

1. <span data-ttu-id="d92dc-178">在Visual Studio Code或任何代码编辑器中，转到项目目录并打开以下文件：</span><span class="sxs-lookup"><span data-stu-id="d92dc-178">In Visual Studio Code or any code editor, go to your project directory and open the following file:</span></span>

    ```bash
    ./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
    ```

1. <span data-ttu-id="d92dc-179">找到 `render()` 方法，将以下 `<div>` 标记和内容添加到容器 `<PanelBody>` 代码的顶部：</span><span class="sxs-lookup"><span data-stu-id="d92dc-179">Locate the `render()` method and add the following `<div>` tag and content to the top of the `<PanelBody>` container code:</span></span>

    ```html
        <PanelBody>
            <div style={styles.section}>
                Hello World! Yo Teams rocks!
            </div>
        </PanelBody>
    ```

1. <span data-ttu-id="d92dc-180">确保保存更新后的文件。</span><span class="sxs-lookup"><span data-stu-id="d92dc-180">Make sure to save the updated file.</span></span>

### <a name="build-and-run-your-application"></a><span data-ttu-id="d92dc-181">生成并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="d92dc-181">Build and run your application</span></span>

<span data-ttu-id="d92dc-182">在命令提示符下，打开项目目录以完成下一个任务。</span><span class="sxs-lookup"><span data-stu-id="d92dc-182">At a command prompt, open your project directory to complete the next tasks.</span></span>

#### <a name="create-the-app-package"></a><span data-ttu-id="d92dc-183">创建应用包</span><span class="sxs-lookup"><span data-stu-id="d92dc-183">Create the app package</span></span>

<span data-ttu-id="d92dc-184">你必须有一个应用包来测试应用中的Teams。</span><span class="sxs-lookup"><span data-stu-id="d92dc-184">You must have an app package to test your tab in Teams.</span></span> <span data-ttu-id="d92dc-185">它是包含以下所需文件的 zip 文件夹：</span><span class="sxs-lookup"><span data-stu-id="d92dc-185">It is a zip folder that contains the following required files:</span></span>

- <span data-ttu-id="d92dc-186">全 **色图标** ，大小为 192 x 192 像素。</span><span class="sxs-lookup"><span data-stu-id="d92dc-186">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="d92dc-187">一 **个 32** x 32 像素的透明边框图标。</span><span class="sxs-lookup"><span data-stu-id="d92dc-187">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="d92dc-188">指定 **manifest.js** 属性的 on 文件。</span><span class="sxs-lookup"><span data-stu-id="d92dc-188">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="d92dc-189">程序包通过 gulp 任务创建，该任务验证文件上的manifest.js，并生成 **./package** 目录中的 zip 文件夹。</span><span class="sxs-lookup"><span data-stu-id="d92dc-189">The package is created through a gulp task that validates the manifest.json file and generates the zip folder in the **./package directory**.</span></span> <span data-ttu-id="d92dc-190">在命令提示符中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="d92dc-190">In the command prompt, enter the following command:</span></span>

```bash
gulp manifest
```

#### <a name="build-your-application"></a><span data-ttu-id="d92dc-191">生成应用程序</span><span class="sxs-lookup"><span data-stu-id="d92dc-191">Build your application</span></span>

<span data-ttu-id="d92dc-192">生成命令将解决方案转换为 **./dist** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="d92dc-192">The build command transpiles your solution into the **./dist** folder.</span></span> <span data-ttu-id="d92dc-193">在命令提示符中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="d92dc-193">Enter the following command in the command prompt:</span></span>

```bash
gulp build
```

#### <a name="run-your-application-in-localhost"></a><span data-ttu-id="d92dc-194">在 localhost 中运行应用程序</span><span class="sxs-lookup"><span data-stu-id="d92dc-194">Run your application in localhost</span></span>

1. <span data-ttu-id="d92dc-195">在命令提示符中输入以下内容，以启动本地 Web 服务器：</span><span class="sxs-lookup"><span data-stu-id="d92dc-195">Start a local web server by entering the following in the command prompt:</span></span>

    ```bash
    gulp serve
    ```

1. <span data-ttu-id="d92dc-196">`http://localhost:3007/<yourDefaultAppNameTab>/`在浏览器中输入 ，将 替换为选项卡名称，然后查看应用程序的主页 **<yourDefaultAppNameTab>** ，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="d92dc-196">Enter `http://localhost:3007/<yourDefaultAppNameTab>/` in your browser, replace **<yourDefaultAppNameTab>** with your tab name, and view your application's home page as shown in the following image:</span></span>

    ![主页屏幕截图](~/assets/images/tab-images/homePage.png)

1. <span data-ttu-id="d92dc-198">若要查看选项卡配置页面，请转到 `https://localhost:3007/<yourDefaultAppNameTab>/config.html` 。</span><span class="sxs-lookup"><span data-stu-id="d92dc-198">To view your tab configuration page, go to `https://localhost:3007/<yourDefaultAppNameTab>/config.html`.</span></span> <span data-ttu-id="d92dc-199">如下所示：</span><span class="sxs-lookup"><span data-stu-id="d92dc-199">The following is shown:</span></span>

    ![配置页面屏幕截图](~/assets/images/tab-images/configurationPage.png)

### <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="d92dc-201">建立到选项卡的安全隧道</span><span class="sxs-lookup"><span data-stu-id="d92dc-201">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="d92dc-202">Microsoft Teams是一种基于云的产品，要求使用 HTTPS 终结点从云中提供选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="d92dc-202">Microsoft Teams is a cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="d92dc-203">Teams不允许本地托管。</span><span class="sxs-lookup"><span data-stu-id="d92dc-203">Teams does not allow local hosting.</span></span> <span data-ttu-id="d92dc-204">必须将选项卡发布到公用 URL，或使用将本地端口公开到面向 Internet 的 URL 的代理。</span><span class="sxs-lookup"><span data-stu-id="d92dc-204">You must either publish your tab to a public URL or use a proxy that exposes your local port to an internet-facing URL.</span></span>

<span data-ttu-id="d92dc-205">若要测试选项卡扩展，请使用内置于此应用程序中的[ngrok。](https://ngrok.com/docs)</span><span class="sxs-lookup"><span data-stu-id="d92dc-205">To test your tab extension, use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="d92dc-206">Ngrok 是反向代理软件工具，可创建到本地运行的 Web 服务器的公共 HTTPS 终结点的隧道。</span><span class="sxs-lookup"><span data-stu-id="d92dc-206">Ngrok is a reverse proxy software tool that creates a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="d92dc-207">在计算机的当前会话期间，您的服务器的 Web 终结点可用。</span><span class="sxs-lookup"><span data-stu-id="d92dc-207">Your server's web endpoints are available during the current session on your computer.</span></span> <span data-ttu-id="d92dc-208">当计算机关闭或进入睡眠状态时，服务不再可用。</span><span class="sxs-lookup"><span data-stu-id="d92dc-208">When the computer is shut down or goes to sleep the service is no longer available.</span></span>

<span data-ttu-id="d92dc-209">在命令提示符中，退出 localhost 并输入以下内容：</span><span class="sxs-lookup"><span data-stu-id="d92dc-209">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="d92dc-210">将选项卡上载到 Microsoft Teams 并成功保存后，可以在选项卡库中查看它、将其添加到选项卡栏并与其交互，直到 ngrok 隧道会话结束。</span><span class="sxs-lookup"><span data-stu-id="d92dc-210">After your tab has been uploaded to Microsoft Teams and successfully saved, you can view it in the tabs gallery, add it to the tabs bar, and interact with it until your ngrok tunnel session ends.</span></span> <span data-ttu-id="d92dc-211">如果重新启动 ngrok 会话，则必须使用新 URL 更新应用。</span><span class="sxs-lookup"><span data-stu-id="d92dc-211">If you restart your ngrok session, you must update your app with the new URL.</span></span>

### <a name="upload-your-application-to-teams"></a><span data-ttu-id="d92dc-212">Upload应用程序以Teams</span><span class="sxs-lookup"><span data-stu-id="d92dc-212">Upload your application to Teams</span></span>

<span data-ttu-id="d92dc-213">**将应用程序上载到Teams**</span><span class="sxs-lookup"><span data-stu-id="d92dc-213">**To upload your application to Teams**</span></span>

1. <span data-ttu-id="d92dc-214">转到Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="d92dc-214">Go to Microsoft Teams.</span></span> <span data-ttu-id="d92dc-215">如果使用基于 [Web 的版本，](https://teams.microsoft.com) 可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="d92dc-215">If you use the [web-based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
1. <span data-ttu-id="d92dc-216">在左窗格中的团队中，选择 &#x25CF;&#x25CF;&#x25CF; 测试选项卡的团队旁边的省略号，然后选择"**管理团队"。**</span><span class="sxs-lookup"><span data-stu-id="d92dc-216">From your teams on the left pane, select the ellipses &#x25CF;&#x25CF;&#x25CF; next to the team that you are using to test your tab and choose **Manage team**.</span></span>
1. <span data-ttu-id="d92dc-217">在主窗格中，从选项卡栏中选择"应用"，Upload位于页面右下角的自定义应用。</span><span class="sxs-lookup"><span data-stu-id="d92dc-217">In the main pane, select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right corner of the page.</span></span>
1. <span data-ttu-id="d92dc-218">转到项目目录，浏览到 **./package** 文件夹，选择应用包 zip 文件夹，然后选择"打开 **"。**</span><span class="sxs-lookup"><span data-stu-id="d92dc-218">Go your project directory, browse to the **./package** folder, select the app package zip folder, and choose **Open**.</span></span>

    ![添加的"频道"选项卡](../../assets/images/tab-images/channeltabadded.png)

1. <span data-ttu-id="d92dc-220">在 **弹出** 对话框中选择"添加"。</span><span class="sxs-lookup"><span data-stu-id="d92dc-220">Select **Add** in the pop-up dialog box.</span></span> <span data-ttu-id="d92dc-221">您的选项卡将上载到Teams。</span><span class="sxs-lookup"><span data-stu-id="d92dc-221">Your tab uploads into Teams.</span></span>
1. <span data-ttu-id="d92dc-222">返回到团队，选择要显示选项卡的频道，从选项卡➕选择选项卡，然后从库中选择您的选项卡。</span><span class="sxs-lookup"><span data-stu-id="d92dc-222">Return to your team, choose the channel where you want to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
1. <span data-ttu-id="d92dc-223">按照添加选项卡的说明操作。频道或组选项卡有一个自定义配置对话框。</span><span class="sxs-lookup"><span data-stu-id="d92dc-223">Follow the directions for adding a tab. There is a custom configuration dialog box for your channel or group tab.</span></span>
1. <span data-ttu-id="d92dc-224">选择 **"** 保存"，您的选项卡将添加到频道的选项卡栏中。</span><span class="sxs-lookup"><span data-stu-id="d92dc-224">Select **Save** and your tab is added to the channel's tab bar.</span></span>

    ![已上载"频道"选项卡](../../assets/images/tab-images/channeltabuploaded.png)

# <a name="aspnet-core"></a>[<span data-ttu-id="d92dc-226">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="d92dc-226">ASP.NET Core</span></span>](#tab/aspnetcore)

### <a name="create-a-custom-channel-or-group-tab-with-aspnet-core"></a><span data-ttu-id="d92dc-227">使用自定义频道或组选项卡 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="d92dc-227">Create a custom channel or group tab with ASP.NET Core</span></span>

<span data-ttu-id="d92dc-228">可以使用"Core 用户"页面C#自定义频道 ASP.Net 组选项卡。</span><span class="sxs-lookup"><span data-stu-id="d92dc-228">You can create a custom channel or group tab using C# and ASP.Net Core Razor page.</span></span> <span data-ttu-id="d92dc-229">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md)还用于完成应用清单，并部署选项卡以Teams。</span><span class="sxs-lookup"><span data-stu-id="d92dc-229">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) is also used to finalize your app manifest and deploy your tab to Teams.</span></span>

### <a name="prerequisites-for-teams-apps"></a><span data-ttu-id="d92dc-230">应用Teams的先决条件</span><span class="sxs-lookup"><span data-stu-id="d92dc-230">Prerequisites for Teams apps</span></span>

<span data-ttu-id="d92dc-231">您必须了解以下先决条件：</span><span class="sxs-lookup"><span data-stu-id="d92dc-231">You must have an understanding of the following prerequisites:</span></span>

- <span data-ttu-id="d92dc-232">你必须拥有一个Office 365租户和一个已启用"允许上载 **自定义应用"的团队**。</span><span class="sxs-lookup"><span data-stu-id="d92dc-232">You must have an Office 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="d92dc-233">有关详细信息，请参阅[准备你的Office 365租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="d92dc-233">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="d92dc-234">如果你当前没有Microsoft 365帐户，可以通过 Microsoft 开发人员计划注册免费[订阅](https://developer.microsoft.com/en-us/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="d92dc-234">If you do not currently have a Microsoft 365 account, you can sign up for a free subscription through the [Microsoft Developer Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program).</span></span> <span data-ttu-id="d92dc-235">只要将订阅用于正在进行的开发，订阅就保持活动状态。</span><span class="sxs-lookup"><span data-stu-id="d92dc-235">The subscription remains active as long as you are using it for ongoing development.</span></span>

- <span data-ttu-id="d92dc-236">使用 App Studio 将应用程序导入Teams。</span><span class="sxs-lookup"><span data-stu-id="d92dc-236">Use App Studio to import your application to Teams.</span></span> <span data-ttu-id="d92dc-237">若要安装 App Studio，**请选择应用** 左下角的 Teams ![ ](~/assets/images/tab-images/storeApp.png) 应用，然后搜索 **App Studio**。</span><span class="sxs-lookup"><span data-stu-id="d92dc-237">To install App Studio, select **Apps** ![Store App](~/assets/images/tab-images/storeApp.png) at the lower left corner of the Teams app, and search for **App Studio**.</span></span> <span data-ttu-id="d92dc-238">找到磁贴后，选择它 **，然后选择弹出** 对话框中的"添加"以安装它。</span><span class="sxs-lookup"><span data-stu-id="d92dc-238">After you find the tile, select it and choose **Add** in the pop-up dialog box to install it.</span></span>

<span data-ttu-id="d92dc-239">此外，此项目要求在开发环境中安装以下内容：</span><span class="sxs-lookup"><span data-stu-id="d92dc-239">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="d92dc-240">当前版本的 IDE Visual Studio **安装了 .NET CORE 跨平台开发** 工作负载。</span><span class="sxs-lookup"><span data-stu-id="d92dc-240">The current version of the Visual Studio IDE with the **.NET CORE cross-platform development** workload installed.</span></span> <span data-ttu-id="d92dc-241">如果尚未安装Visual Studio，可以免费下载和安装[Microsoft Visual Studio Community版本。](https://visualstudio.microsoft.com/downloads)</span><span class="sxs-lookup"><span data-stu-id="d92dc-241">If you do not already have Visual Studio, you can download and install the latest [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) version for free.</span></span>

- <span data-ttu-id="d92dc-242">[ngrok](https://ngrok.com)反向代理工具。</span><span class="sxs-lookup"><span data-stu-id="d92dc-242">The [ngrok](https://ngrok.com) reverse proxy tool.</span></span> <span data-ttu-id="d92dc-243">使用 ngrok 创建到本地运行的 Web 服务器的公开可用的 HTTPS 终结点的隧道。</span><span class="sxs-lookup"><span data-stu-id="d92dc-243">Use ngrok to create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="d92dc-244">您可以 [下载 ngrok](https://ngrok.com/download)。</span><span class="sxs-lookup"><span data-stu-id="d92dc-244">You can [download ngrok](https://ngrok.com/download).</span></span>

### <a name="get-the-source-code"></a><span data-ttu-id="d92dc-245">获取源代码</span><span class="sxs-lookup"><span data-stu-id="d92dc-245">Get the source code</span></span>

<span data-ttu-id="d92dc-246">在命令提示符下，为选项卡项目创建新目录。</span><span class="sxs-lookup"><span data-stu-id="d92dc-246">At a command prompt, create a new directory for your tab project.</span></span> <span data-ttu-id="d92dc-247">提供了一个简单的项目来开始操作。</span><span class="sxs-lookup"><span data-stu-id="d92dc-247">A simple project is provided to get you started.</span></span> <span data-ttu-id="d92dc-248">使用下面的命令将示例存储库克隆到新目录中：</span><span class="sxs-lookup"><span data-stu-id="d92dc-248">Clone the sample repository into your new directory using the following command:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="d92dc-249">或者，您可以通过下载 zip 文件夹并提取文件来检索源代码。</span><span class="sxs-lookup"><span data-stu-id="d92dc-249">Alternately, you can retrieve the source code by downloading the zip folder and extracting the files.</span></span>

<span data-ttu-id="d92dc-250">**生成并运行选项卡项目**</span><span class="sxs-lookup"><span data-stu-id="d92dc-250">**To build and run the tab project**</span></span>

1. <span data-ttu-id="d92dc-251">获得源代码后，转到"打开Visual Studio并选择"打开 **项目或解决方案"。**</span><span class="sxs-lookup"><span data-stu-id="d92dc-251">After you have the source code, go to Visual Studio and select **Open a project or solution**.</span></span>
1. <span data-ttu-id="d92dc-252">转到选项卡应用程序目录，然后打开 **ChannelGroupTab.sln**。</span><span class="sxs-lookup"><span data-stu-id="d92dc-252">Go to the tab application directory and open **ChannelGroupTab.sln**.</span></span>
1. <span data-ttu-id="d92dc-253">若要生成并运行应用程序，请按 **F5** 或从"调试 **"** 菜单中选择"开始 **调试** "。</span><span class="sxs-lookup"><span data-stu-id="d92dc-253">To build and run your application, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span>
1. <span data-ttu-id="d92dc-254">在浏览器中，转到以下 URL 并验证应用程序是否加载正确：</span><span class="sxs-lookup"><span data-stu-id="d92dc-254">In a browser, go to the following URLs and verify the application loaded properly:</span></span>

    - `http://localhost:44355`
    - `http://localhost:44355/privacy`
    - `http://localhost:44355/tou`

### <a name="review-the-source-code"></a><span data-ttu-id="d92dc-255">查看源代码</span><span class="sxs-lookup"><span data-stu-id="d92dc-255">Review the source code</span></span>

#### <a name="startupcs"></a><span data-ttu-id="d92dc-256">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="d92dc-256">Startup.cs</span></span>

<span data-ttu-id="d92dc-257">此项目从 2.2 web 应用程序 ASP.NET Core模板创建，在设置时选中了"高级 **- 为 HTTPS** 配置"复选框。</span><span class="sxs-lookup"><span data-stu-id="d92dc-257">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="d92dc-258">MVC 服务由依赖关系注入框架的方法 `ConfigureServices()` 注册。</span><span class="sxs-lookup"><span data-stu-id="d92dc-258">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="d92dc-259">此外，空模板默认情况下不支持为静态内容提供服务，因此，将静态文件中间件添加到 以下 `Configure()` 代码的方法中：</span><span class="sxs-lookup"><span data-stu-id="d92dc-259">Additionally, the empty template does not enable serving static content by default, so the static files middleware is added to the `Configure()` method using the following code:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
  {
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
  }
public void Configure(IApplicationBuilder app)
  {
    app.UseStaticFiles();
    app.UseMvc();
  }
```

#### <a name="wwwroot-folder"></a><span data-ttu-id="d92dc-260">wwwroot 文件夹</span><span class="sxs-lookup"><span data-stu-id="d92dc-260">wwwroot folder</span></span>

<span data-ttu-id="d92dc-261">在 ASP.NET Core中，Web 根文件夹是应用程序查找静态文件的位置。</span><span class="sxs-lookup"><span data-stu-id="d92dc-261">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

#### <a name="indexcshtml"></a><span data-ttu-id="d92dc-262">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="d92dc-262">Index.cshtml</span></span>

<span data-ttu-id="d92dc-263">ASP.NET Core将名为 **Index** 的文件视为网站的默认页面或主页。</span><span class="sxs-lookup"><span data-stu-id="d92dc-263">ASP.NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="d92dc-264">当浏览器 URL 指向网站的根目录时 **，Index.cshtml** 将显示为应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="d92dc-264">When your browser URL points to the root of the site, **Index.cshtml** is displayed as the home page for your application.</span></span>

#### <a name="tabcs"></a><span data-ttu-id="d92dc-265">Tab.cs</span><span class="sxs-lookup"><span data-stu-id="d92dc-265">Tab.cs</span></span>

<span data-ttu-id="d92dc-266">此C#文件包含在配置过程中从 **Tab.cshtml** 调用的方法。</span><span class="sxs-lookup"><span data-stu-id="d92dc-266">This C# file contains a method that is called from **Tab.cshtml** during configuration.</span></span>

#### <a name="appmanifest-folder"></a><span data-ttu-id="d92dc-267">AppManifest 文件夹</span><span class="sxs-lookup"><span data-stu-id="d92dc-267">AppManifest folder</span></span>

<span data-ttu-id="d92dc-268">此文件夹包含以下所需的应用包文件：</span><span class="sxs-lookup"><span data-stu-id="d92dc-268">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="d92dc-269">全 **色图标** ，大小为 192 x 192 像素。</span><span class="sxs-lookup"><span data-stu-id="d92dc-269">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="d92dc-270">一 **个 32** x 32 像素的透明边框图标。</span><span class="sxs-lookup"><span data-stu-id="d92dc-270">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="d92dc-271">指定 **manifest.js** 属性的 on 文件。</span><span class="sxs-lookup"><span data-stu-id="d92dc-271">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="d92dc-272">这些文件需要在应用包中压缩，以用于将选项卡上载到Teams。</span><span class="sxs-lookup"><span data-stu-id="d92dc-272">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span> <span data-ttu-id="d92dc-273">当用户选择添加或更新选项卡时，Microsoft Teams清单中指定的内容，将其嵌入 IFrame 中，并将其呈现在 `configurationUrl` 选项卡中。</span><span class="sxs-lookup"><span data-stu-id="d92dc-273">When a user chooses to add or update your tab, Microsoft Teams loads the `configurationUrl` specified in your manifest, embeds it in an IFrame, and renders it in your tab.</span></span>

#### <a name="csproj"></a><span data-ttu-id="d92dc-274">.csproj</span><span class="sxs-lookup"><span data-stu-id="d92dc-274">.csproj</span></span>

<span data-ttu-id="d92dc-275">在"Visual Studio资源管理器"窗口中，右键单击项目并选择"编辑Project **文件"。**</span><span class="sxs-lookup"><span data-stu-id="d92dc-275">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="d92dc-276">在文件末尾，你将看到以下代码，该代码在应用程序生成时创建和更新 zip 文件夹：</span><span class="sxs-lookup"><span data-stu-id="d92dc-276">At the end of the file, you see the following code that creates and updates your zip folder when the application builds:</span></span>

```xml
<PropertyGroup>
    <PostBuildEvent>powershell.exe Compress-Archive -Path \"$(ProjectDir)AppManifest\*\" -DestinationPath \"$(TargetDir)tab.zip\" -Force</PostBuildEvent>
  </PropertyGroup>

  <ItemGroup>
    <EmbeddedResource Include="AppManifest\icon-outline.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\icon-color.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\manifest.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
  </ItemGroup>
```

### <a name="establish-a-secure-tunnel-to-your-tab-for-teams"></a><span data-ttu-id="d92dc-277">为选项卡建立安全隧道，以Teams</span><span class="sxs-lookup"><span data-stu-id="d92dc-277">Establish a secure tunnel to your tab for Teams</span></span>

<span data-ttu-id="d92dc-278">Microsoft Teams是一种基于云的产品，要求使用 HTTPS 终结点从云中提供选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="d92dc-278">Microsoft Teams is a cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="d92dc-279">Teams不允许本地托管。</span><span class="sxs-lookup"><span data-stu-id="d92dc-279">Teams does not allow local hosting.</span></span> <span data-ttu-id="d92dc-280">必须将选项卡发布到公用 URL，或使用向面向 Internet 的 URL 公开本地端口的代理。</span><span class="sxs-lookup"><span data-stu-id="d92dc-280">You must either publish your tab to a public URL, or use a proxy that exposes your local port to an internet-facing URL.</span></span>

<span data-ttu-id="d92dc-281">若要测试您的选项卡，请使用 [ngrok](https://ngrok.com/docs)。</span><span class="sxs-lookup"><span data-stu-id="d92dc-281">To test your tab, use [ngrok](https://ngrok.com/docs).</span></span> <span data-ttu-id="d92dc-282">当 ngrok 正在您的计算机上运行时，您的服务器的 Web 终结点可用。</span><span class="sxs-lookup"><span data-stu-id="d92dc-282">Your server's web endpoints are available while ngrok is running on your computer.</span></span> <span data-ttu-id="d92dc-283">在 ngrok 的免费版本中，如果您关闭 ngrok，则下次启动 URL 时 URL 会有所不同。</span><span class="sxs-lookup"><span data-stu-id="d92dc-283">In the free version of ngrok, if you close ngrok, the URLs are different the next time you start it.</span></span>

- <span data-ttu-id="d92dc-284">在项目目录根目录的命令提示符下，运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="d92dc-284">At a command prompt in the root of your project directory, run the following command:</span></span>

    ```bash
    ngrok http https://localhost:44355 -host-header="localhost:44355"
    ```

- <span data-ttu-id="d92dc-285">Ngrok 侦听来自 Internet 的请求，当应用程序在端口 44355 上运行时，它会将它们路由到您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="d92dc-285">Ngrok listens to requests from the internet and routes them to your application when it is running on port 44355.</span></span> <span data-ttu-id="d92dc-286">它应 `https://y8rCgT2b.ngrok.io/` 类似于 **y8rCgT2b** 替换为 ngrok 字母数字 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="d92dc-286">It should resemble `https://y8rCgT2b.ngrok.io/` where **y8rCgT2b** is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

- <span data-ttu-id="d92dc-287">确保使命令提示符保持运行 ngrok，并记下 URL。</span><span class="sxs-lookup"><span data-stu-id="d92dc-287">Ensure that you keep the command prompt with ngrok running and make a note of the URL.</span></span>

### <a name="update-your-application"></a><span data-ttu-id="d92dc-288">更新应用程序</span><span class="sxs-lookup"><span data-stu-id="d92dc-288">Update your application</span></span>

<span data-ttu-id="d92dc-289">在 **Tab.cshtml** 中，应用程序向用户显示两个选项按钮，用于显示带红色或灰色图标的选项卡。</span><span class="sxs-lookup"><span data-stu-id="d92dc-289">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="d92dc-290">分别选择 **"选择灰色\*\*\*\*"或**"选择红色"按钮触发器或 ，设置 并启用配置页上的" `saveGray()` `saveRed()` `settings.setValidityState(true)` 保存"按钮。 </span><span class="sxs-lookup"><span data-stu-id="d92dc-290">Choosing the **Select Gray** or **Select Red** button triggers `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="d92dc-291">此代码Teams您已完成配置要求，并且可以继续安装。</span><span class="sxs-lookup"><span data-stu-id="d92dc-291">This code lets Teams know that you have completed the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="d92dc-292">设置 `settings.setSettings` 的参数。</span><span class="sxs-lookup"><span data-stu-id="d92dc-292">The parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="d92dc-293">最后 `saveEvent.notifySuccess()` ，调用 以指示已成功解析内容 URL。</span><span class="sxs-lookup"><span data-stu-id="d92dc-293">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has been successfully resolved.</span></span>

#### <a name="_layoutcshtml"></a><span data-ttu-id="d92dc-294">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="d92dc-294">_Layout.cshtml</span></span>

<span data-ttu-id="d92dc-295">若要在页面中显示选项卡Teams，必须包含 **Microsoft Teams JavaScript** 客户端 SDK，并包括页面加载 `microsoftTeams.initialize()` 后对 的调用。</span><span class="sxs-lookup"><span data-stu-id="d92dc-295">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="d92dc-296">这是选项卡和客户端Teams的方式：</span><span class="sxs-lookup"><span data-stu-id="d92dc-296">This is how your tab and the Teams client communicate:</span></span>

<span data-ttu-id="d92dc-297">转到" **共享"** 文件夹，打开 **_Layout.cshtml，** 然后向 标记中添加 `<head>` 以下内容：</span><span class="sxs-lookup"><span data-stu-id="d92dc-297">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

> [!IMPORTANT]
> <span data-ttu-id="d92dc-298">不要复制并粘贴此页 `<script src="...">` 中的 URL，因为它们不表示最新版本。</span><span class="sxs-lookup"><span data-stu-id="d92dc-298">Do not copy and paste the `<script src="...">` URLs from this page, as they do not represent the latest version.</span></span> <span data-ttu-id="d92dc-299">若要获取最新版本的 SDK，请始终转到[Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js)。</span><span class="sxs-lookup"><span data-stu-id="d92dc-299">To get the latest version of the SDK, always go to [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js).</span></span>

#### <a name="tabcshtml"></a><span data-ttu-id="d92dc-300">Tab.cshtml</span><span class="sxs-lookup"><span data-stu-id="d92dc-300">Tab.cshtml</span></span>

<span data-ttu-id="d92dc-301">**更新 Tab.cshtml**</span><span class="sxs-lookup"><span data-stu-id="d92dc-301">**To update Tab.cshtml**</span></span>

1. <span data-ttu-id="d92dc-302">在 **"文件"中Visual Studio Tab.cshtml** 并更新嵌入的 `<script>` 。</span><span class="sxs-lookup"><span data-stu-id="d92dc-302">Open **Tab.cshtml** in Visual Studio and update the embedded `<script>`.</span></span>

1. <span data-ttu-id="d92dc-303">在脚本顶部，调用 `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="d92dc-303">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

1. <span data-ttu-id="d92dc-304">将每个 `websiteUrl` 函数 `contentUrl` 中的 和 值更新为选项卡的 HTTPS ngrok URL。</span><span class="sxs-lookup"><span data-stu-id="d92dc-304">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

    <span data-ttu-id="d92dc-305">现在，您的代码应包含以下内容， **其中 y8rCgT2b** 替换为您的 ngrok URL：</span><span class="sxs-lookup"><span data-stu-id="d92dc-305">Your code should now include the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

    ```javascript
        microsoftTeams.initialize();

        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
        });
        }
    ```

1. <span data-ttu-id="d92dc-306">保存更新的 **Tab.cshtml**。</span><span class="sxs-lookup"><span data-stu-id="d92dc-306">Save the updated **Tab.cshtml**.</span></span>

### <a name="build-and-run-your-application-for-teams"></a><span data-ttu-id="d92dc-307">生成并运行应用程序Teams</span><span class="sxs-lookup"><span data-stu-id="d92dc-307">Build and run your application for Teams</span></span>

<span data-ttu-id="d92dc-308">**构建和运行应用程序**</span><span class="sxs-lookup"><span data-stu-id="d92dc-308">**To build and run your application**</span></span>

1. <span data-ttu-id="d92dc-309">In Visual Studio， press **F5** or choose **Start Debugging** from the **Debug** menu.</span><span class="sxs-lookup"><span data-stu-id="d92dc-309">In Visual Studio, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span>
1. <span data-ttu-id="d92dc-310">通过打开浏览器，然后通过命令提示符窗口中提供的 ngrok HTTPS URL 进入内容页面，验证 **ngrok** 是否正常运行。</span><span class="sxs-lookup"><span data-stu-id="d92dc-310">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="d92dc-311">你需要让应用程序在 Visual Studio 和 ngrok 中运行才能完成本文中提供的步骤。</span><span class="sxs-lookup"><span data-stu-id="d92dc-311">You need to have both your application in Visual Studio and ngrok running to complete the steps provided in this article.</span></span> <span data-ttu-id="d92dc-312">如果需要停止运行应用程序，Visual Studio运行应用程序，请 **保持 ngrok 运行**。</span><span class="sxs-lookup"><span data-stu-id="d92dc-312">If you need to stop running your application in Visual Studio to work on it, **keep ngrok running**.</span></span> <span data-ttu-id="d92dc-313">当应用程序在应用程序中重新启动时，它会侦听并恢复Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d92dc-313">It listens and resumes routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="d92dc-314">如果您必须重新启动 ngrok 服务，它将返回一个新 URL，并且您必须使用新 URL 更新您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="d92dc-314">If you have to restart the ngrok service it returns a new URL and you have to update your application with the new URL.</span></span>

### <a name="upload-your-tab-for-teams"></a><span data-ttu-id="d92dc-315">Upload选项卡进行Teams</span><span class="sxs-lookup"><span data-stu-id="d92dc-315">Upload your tab for Teams</span></span>

> [!NOTE]
> <span data-ttu-id="d92dc-316">App Studio 可用于编辑 **文件上的** manifest.js，以及将已完成的程序包上传到Teams。</span><span class="sxs-lookup"><span data-stu-id="d92dc-316">App Studio can be used to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="d92dc-317">还可以手动编辑 on **manifest.js** 文件。</span><span class="sxs-lookup"><span data-stu-id="d92dc-317">You can also manually edit the **manifest.json** file.</span></span> <span data-ttu-id="d92dc-318">如果这样做，请确保再次生成解决方案以创建要 **tab.zip文件。**</span><span class="sxs-lookup"><span data-stu-id="d92dc-318">If you do, ensure that you build the solution again to create the **tab.zip** file to upload.</span></span>

<span data-ttu-id="d92dc-319">**使用 App Studio 上传选项卡**</span><span class="sxs-lookup"><span data-stu-id="d92dc-319">**To upload your tab with App Studio**</span></span>

1. <span data-ttu-id="d92dc-320">转到Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="d92dc-320">Go to Microsoft Teams.</span></span> <span data-ttu-id="d92dc-321">如果使用基于 [Web 的版本，](https://teams.microsoft.com)可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="d92dc-321">If you use the [web-based version](https://teams.microsoft.com), you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

1. <span data-ttu-id="d92dc-322">转到 **App Studio，** 然后选择清单 **编辑器** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="d92dc-322">Go to **App Studio** and select the **Manifest editor** tab.</span></span>

1. <span data-ttu-id="d92dc-323">选择 **"在清单编辑器** 中导入现有 **应用"** 开始为选项卡更新应用包。源代码附带其自己的部分完整清单。</span><span class="sxs-lookup"><span data-stu-id="d92dc-323">Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="d92dc-324">应用包的名称 **tab.zip。**</span><span class="sxs-lookup"><span data-stu-id="d92dc-324">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="d92dc-325">可从以下路径获得：</span><span class="sxs-lookup"><span data-stu-id="d92dc-325">It is available from the following path:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. <span data-ttu-id="d92dc-326">Uploadtab.zipApp  Studio。</span><span class="sxs-lookup"><span data-stu-id="d92dc-326">Upload **tab.zip** to App Studio.</span></span>

#### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="d92dc-327">使用清单编辑器更新应用包</span><span class="sxs-lookup"><span data-stu-id="d92dc-327">Update your app package with Manifest editor</span></span>

<span data-ttu-id="d92dc-328">将应用包上传到 App Studio 后，必须对其进行配置。</span><span class="sxs-lookup"><span data-stu-id="d92dc-328">After you have uploaded your app package into App Studio, you must configure it.</span></span>

<span data-ttu-id="d92dc-329">在清单编辑器欢迎页面的右侧面板中选择新导入选项卡的磁贴。</span><span class="sxs-lookup"><span data-stu-id="d92dc-329">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="d92dc-330">清单编辑器左侧有一个步骤列表，右侧是一个属性列表，其中每个步骤都必须具有值。</span><span class="sxs-lookup"><span data-stu-id="d92dc-330">There is a list of steps on the left side of the Manifest editor, and on the right, a list of properties that must have values for each of those steps.</span></span> <span data-ttu-id="d92dc-331">大部分信息已由你的用户 **manifest.js，但** 有些字段必须更新。</span><span class="sxs-lookup"><span data-stu-id="d92dc-331">Much of the information has been provided by your **manifest.json** but there are fields that you must update.</span></span>

##### <a name="details-app-details"></a><span data-ttu-id="d92dc-332">详细信息：应用详细信息</span><span class="sxs-lookup"><span data-stu-id="d92dc-332">Details: App details</span></span>

<span data-ttu-id="d92dc-333">在" **应用详细信息"** 部分中：</span><span class="sxs-lookup"><span data-stu-id="d92dc-333">In the **App details** section:</span></span>

1. <span data-ttu-id="d92dc-334">在 **"标识\*\*\*\*"下**，选择"生成"以将占位符 ID 替换为选项卡所需的 GUID。</span><span class="sxs-lookup"><span data-stu-id="d92dc-334">Under **Identification**, select **Generate** to replace the placeholder ID with the required GUID for your tab.</span></span>

1. <span data-ttu-id="d92dc-335">在 **"开发人员信息**" **下，使用** **ngrok** HTTPS URL 更新网站。</span><span class="sxs-lookup"><span data-stu-id="d92dc-335">Under **Developer information**, update **Website** with your **ngrok** HTTPS URL.</span></span>

1. <span data-ttu-id="d92dc-336">在 **"应用程序 URL"** 下，将隐私声明更新为 和 `https://<yourngrokurl>/privacy` **使用条款** 以 `https://<yourngrokurl>/tou`>。</span><span class="sxs-lookup"><span data-stu-id="d92dc-336">Under **App URLs**, update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

##### <a name="capabilities-tabs"></a><span data-ttu-id="d92dc-337">功能：选项卡</span><span class="sxs-lookup"><span data-stu-id="d92dc-337">Capabilities: Tabs</span></span>

<span data-ttu-id="d92dc-338">在" **选项卡"** 部分：</span><span class="sxs-lookup"><span data-stu-id="d92dc-338">In the **Tabs** section:</span></span>

1. <span data-ttu-id="d92dc-339">在"**团队"选项卡** 下，选择"**添加"。**</span><span class="sxs-lookup"><span data-stu-id="d92dc-339">Under **Team tab**, select **Add**.</span></span>

1. <span data-ttu-id="d92dc-340">在" **团队"选项卡** 弹出窗口中，将" **配置 URL"更新** 为 `https://<yourngrokurl>/tab` 。</span><span class="sxs-lookup"><span data-stu-id="d92dc-340">In the **Team tab** pop-up window, update the **Configuration URL** to `https://<yourngrokurl>/tab`.</span></span>

1. <span data-ttu-id="d92dc-341">确保选中 **了"可以更新配置\*\*\*\*？"、"团队**"和"**群聊**"复选框，然后选择"保存 **"。**</span><span class="sxs-lookup"><span data-stu-id="d92dc-341">Ensure the **Can update configuration?**, **Team**, and **Group chat** checkboxes are selected and select **Save**.</span></span>

##### <a name="finish-domains-and-permissions"></a><span data-ttu-id="d92dc-342">完成时间：域和权限</span><span class="sxs-lookup"><span data-stu-id="d92dc-342">Finish: Domains and permissions</span></span>

<span data-ttu-id="d92dc-343">在" **域和权限"** 部分， **选项卡** 中的"域"必须包含不带 HTTPS 前缀的 ngrok `<yourngrokurl>.ngrok.io/` URL。</span><span class="sxs-lookup"><span data-stu-id="d92dc-343">In the **Domains and permissions** section, **Domains from your tabs** must contain your ngrok URL without the HTTPS prefix `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="d92dc-344">完成：测试和分发</span><span class="sxs-lookup"><span data-stu-id="d92dc-344">Finish: Test and distribute</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d92dc-345">在右侧，在 **"说明"** 中，你将看到以下警告：</span><span class="sxs-lookup"><span data-stu-id="d92dc-345">On the right, in **Description**, you see the following warning:</span></span>
>
> <span data-ttu-id="d92dc-346">&#9888; "**'validDomains' array cannot contain a tunneling site..."**</span><span class="sxs-lookup"><span data-stu-id="d92dc-346">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
> <span data-ttu-id="d92dc-347">在测试选项卡时，可以忽略此警告。</span><span class="sxs-lookup"><span data-stu-id="d92dc-347">This warning can be ignored while testing your tab.</span></span>

1. <span data-ttu-id="d92dc-348">在"**测试和分发"部分**，选择"安装 **"。**</span><span class="sxs-lookup"><span data-stu-id="d92dc-348">In the **Test and Distribute** section, select **Install**.</span></span>

1. <span data-ttu-id="d92dc-349">在弹出对话框中，选择"添加到团队 **"** 或从下拉列表中选择"**添加到聊天"。**</span><span class="sxs-lookup"><span data-stu-id="d92dc-349">In the pop-up dialog box, select **Add to a team** or from the drop-down, select **Add to a chat**.</span></span>

1. <span data-ttu-id="d92dc-350">选择要显示选项卡的团队或聊天，然后选择"**设置选项卡"。**</span><span class="sxs-lookup"><span data-stu-id="d92dc-350">Choose the team or chat where you want the tab to be displayed and select **Set up a tab**.</span></span>

1. <span data-ttu-id="d92dc-351">在下一个弹出对话框中，**选择"选择** 灰色"或"**选择红色**"，然后选择"保存 **"。**</span><span class="sxs-lookup"><span data-stu-id="d92dc-351">In the next pop-up dialog box, choose either **Select Gray** or **Select Red**, and select **Save**.</span></span>

1. <span data-ttu-id="d92dc-352">若要查看您的选项卡，请转到安装选项卡的团队或聊天，然后从选项卡栏中选择它。</span><span class="sxs-lookup"><span data-stu-id="d92dc-352">To view your tab, go to the team or chat where you installed the tab, and select it from the tab bar.</span></span> <span data-ttu-id="d92dc-353">将显示在配置过程中选择的页面。</span><span class="sxs-lookup"><span data-stu-id="d92dc-353">The page that you chose during configuration is displayed.</span></span>

    ![频道选项卡 ASPNET 已上载](../../assets/images/tab-images/channeltabaspnetuploaded.png)

# <a name="aspnet-core-mvc"></a>[<span data-ttu-id="d92dc-355">ASP.NET CoreMVC</span><span class="sxs-lookup"><span data-stu-id="d92dc-355">ASP.NET Core MVC</span></span>](#tab/aspnetcoremvc)

### <a name="create-a-custom-channel-or-group-tab-with-aspnet-core-mvc"></a><span data-ttu-id="d92dc-356">使用 MVC 创建自定义频道或 ASP.NET Core选项卡</span><span class="sxs-lookup"><span data-stu-id="d92dc-356">Create a custom channel or group tab with ASP.NET Core MVC</span></span>

<span data-ttu-id="d92dc-357">可以使用自定义频道或组选项卡，C#和 ASP.Net 核心 MVC。</span><span class="sxs-lookup"><span data-stu-id="d92dc-357">You can create a custom channel or group tab using C# and ASP.Net Core MVC.</span></span> <span data-ttu-id="d92dc-358">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md)还用于完成应用清单，并部署选项卡以Teams。</span><span class="sxs-lookup"><span data-stu-id="d92dc-358">[App Studio for Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md) is also used to finalize your app manifest and deploy your tab to Teams.</span></span>

### <a name="prerequisites-for-custom-channel-or-group-tab"></a><span data-ttu-id="d92dc-359">自定义频道或组选项卡的先决条件</span><span class="sxs-lookup"><span data-stu-id="d92dc-359">Prerequisites for custom channel or group tab</span></span>

- <span data-ttu-id="d92dc-360">你必须拥有一个Microsoft 365租户和一个已启用"允许上载自定义 **应用"的团队**。</span><span class="sxs-lookup"><span data-stu-id="d92dc-360">You must have a Microsoft 365 tenant and a team configured with **Allow uploading custom apps** enabled.</span></span> <span data-ttu-id="d92dc-361">有关详细信息，请参阅[准备你的Office 365租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="d92dc-361">For more information, see [prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="d92dc-362">如果你当前没有Microsoft 365帐户，可以通过 Microsoft 开发人员计划注册免费[订阅](https://developer.microsoft.com/en-us/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="d92dc-362">If you do not currently have a Microsoft 365 account, you can sign up for a free subscription through the [Microsoft Developer Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program).</span></span> <span data-ttu-id="d92dc-363">只要将订阅用于正在进行的开发，订阅就保持活动状态。</span><span class="sxs-lookup"><span data-stu-id="d92dc-363">The subscription remains active as long as you are using it for ongoing development.</span></span>

- <span data-ttu-id="d92dc-364">使用 App Studio 将应用程序导入Teams。</span><span class="sxs-lookup"><span data-stu-id="d92dc-364">Use App Studio to import your application to Teams.</span></span> <span data-ttu-id="d92dc-365">若要安装 App Studio，**请选择应用** 左下角的 Teams ![ ](~/assets/images/tab-images/storeApp.png) 应用，然后搜索 **App Studio**。</span><span class="sxs-lookup"><span data-stu-id="d92dc-365">To install App Studio, select **Apps** ![Store App](~/assets/images/tab-images/storeApp.png) at the lower left corner of the Teams app, and search for **App Studio**.</span></span> <span data-ttu-id="d92dc-366">找到磁贴后，选择它 **，然后选择弹出** 对话框中的"添加"以安装它。</span><span class="sxs-lookup"><span data-stu-id="d92dc-366">After you find the tile, select it and choose **Add** in the pop-up dialog box to install it.</span></span>

<span data-ttu-id="d92dc-367">此外，此项目要求在开发环境中安装以下内容：</span><span class="sxs-lookup"><span data-stu-id="d92dc-367">In addition, this project requires that you have the following installed in your development environment:</span></span>

- <span data-ttu-id="d92dc-368">当前版本的 IDE Visual Studio **安装了 .NET CORE 跨平台开发** 工作负载。</span><span class="sxs-lookup"><span data-stu-id="d92dc-368">The current version of the Visual Studio IDE with the **.NET CORE cross-platform development** workload installed.</span></span> <span data-ttu-id="d92dc-369">如果尚未安装Visual Studio，可以免费下载和安装[Microsoft Visual Studio Community版本。](https://visualstudio.microsoft.com/downloads)</span><span class="sxs-lookup"><span data-stu-id="d92dc-369">If you do not already have Visual Studio, you can download and install the latest [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) version for free.</span></span>

- <span data-ttu-id="d92dc-370">[ngrok](https://ngrok.com)反向代理工具。</span><span class="sxs-lookup"><span data-stu-id="d92dc-370">The [ngrok](https://ngrok.com) reverse proxy tool.</span></span> <span data-ttu-id="d92dc-371">使用 ngrok 创建到本地运行的 Web 服务器的公开可用的 HTTPS 终结点的隧道。</span><span class="sxs-lookup"><span data-stu-id="d92dc-371">Use ngrok to create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="d92dc-372">您可以 [下载 ngrok](https://ngrok.com/download)。</span><span class="sxs-lookup"><span data-stu-id="d92dc-372">You can [download ngrok](https://ngrok.com/download).</span></span>

### <a name="get-the-source-code"></a><span data-ttu-id="d92dc-373">获取源代码</span><span class="sxs-lookup"><span data-stu-id="d92dc-373">Get the source code</span></span>

<span data-ttu-id="d92dc-374">在命令提示符下，为选项卡项目创建新目录。</span><span class="sxs-lookup"><span data-stu-id="d92dc-374">At a command prompt, create a new directory for your tab project.</span></span> <span data-ttu-id="d92dc-375">提供了一 [个简单的"频道组](https://github.com/OfficeDev/microsoft-teams-sample-tabs/tree/master/ChannelGroupTabMVC) 选项卡"项目，方便你入门。</span><span class="sxs-lookup"><span data-stu-id="d92dc-375">A simple [Channel Group Tab](https://github.com/OfficeDev/microsoft-teams-sample-tabs/tree/master/ChannelGroupTabMVC) project is provided to get you started.</span></span> <span data-ttu-id="d92dc-376">使用下面的命令将示例存储库克隆到新目录中：</span><span class="sxs-lookup"><span data-stu-id="d92dc-376">Clone the sample repository into your new directory using the following command:</span></span>

```bash
git clone https://github.com/OfficeDev/microsoft-teams-sample-tabs.git
```

<span data-ttu-id="d92dc-377">或者，您可以通过下载 zip 文件夹并提取文件来检索源代码。</span><span class="sxs-lookup"><span data-stu-id="d92dc-377">Alternately, you can retrieve the source code by downloading the zip folder and extracting the files.</span></span>

<span data-ttu-id="d92dc-378">**生成并运行选项卡项目**</span><span class="sxs-lookup"><span data-stu-id="d92dc-378">**To build and run the tab project**</span></span>

1. <span data-ttu-id="d92dc-379">获得源代码后，转到"打开Visual Studio并选择"打开 **项目或解决方案"。**</span><span class="sxs-lookup"><span data-stu-id="d92dc-379">After you have the source code, go to Visual Studio and select **Open a project or solution**.</span></span>
1. <span data-ttu-id="d92dc-380">转到选项卡应用程序目录，然后打开 **ChannelGroupTabMVC.sln**。</span><span class="sxs-lookup"><span data-stu-id="d92dc-380">Go to the tab application directory and open **ChannelGroupTabMVC.sln**.</span></span>
1. <span data-ttu-id="d92dc-381">若要生成并运行应用程序，请按 **F5** 或从"调试 **"** 菜单中选择"开始 **调试** "。</span><span class="sxs-lookup"><span data-stu-id="d92dc-381">To build and run your application, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span>
1. <span data-ttu-id="d92dc-382">在浏览器中，导航到以下 URL 并验证应用程序是否加载正确：</span><span class="sxs-lookup"><span data-stu-id="d92dc-382">In a browser, navigate to the following URLs and verify that the application loaded properly:</span></span>

    - `http://localhost:44360`
    - `http://localhost:44360/privacy`
    - `http://localhost:44360/tou`

### <a name="review-the-source-code"></a><span data-ttu-id="d92dc-383">查看源代码</span><span class="sxs-lookup"><span data-stu-id="d92dc-383">Review the source code</span></span>

#### <a name="startupcs"></a><span data-ttu-id="d92dc-384">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="d92dc-384">Startup.cs</span></span>

<span data-ttu-id="d92dc-385">此项目从 2.2 web 应用程序 ASP.NET Core模板创建，在设置时选中了"高级 **- 为 HTTPS** 配置"复选框。</span><span class="sxs-lookup"><span data-stu-id="d92dc-385">This project was created from an ASP.NET Core 2.2 Web Application empty template with the **Advanced - Configure for HTTPS** check box selected at setup.</span></span> <span data-ttu-id="d92dc-386">MVC 服务由依赖关系注入框架的方法 `ConfigureServices()` 注册。</span><span class="sxs-lookup"><span data-stu-id="d92dc-386">The MVC services are registered by the dependency injection framework's `ConfigureServices()` method.</span></span> <span data-ttu-id="d92dc-387">此外，空模板默认情况下不支持为静态内容提供服务，因此，将静态文件中间件添加到 以下 `Configure()` 代码的方法中：</span><span class="sxs-lookup"><span data-stu-id="d92dc-387">Additionally, the empty template does not enable serving static content by default, so the static files middleware is added to the `Configure()` method using the following code:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
  {
    services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
  }
public void Configure(IApplicationBuilder app)
  {
    app.UseStaticFiles();
    app.UseMvc();
  }
```

#### <a name="wwwroot-folder"></a><span data-ttu-id="d92dc-388">wwwroot 文件夹</span><span class="sxs-lookup"><span data-stu-id="d92dc-388">wwwroot folder</span></span>

<span data-ttu-id="d92dc-389">在 ASP.NET Core中，Web 根文件夹是应用程序查找静态文件的位置。</span><span class="sxs-lookup"><span data-stu-id="d92dc-389">In ASP.NET Core, the web root folder is where the application looks for static files.</span></span>

#### <a name="appmanifest-folder"></a><span data-ttu-id="d92dc-390">AppManifest 文件夹</span><span class="sxs-lookup"><span data-stu-id="d92dc-390">AppManifest folder</span></span>

<span data-ttu-id="d92dc-391">此文件夹包含以下所需的应用包文件：</span><span class="sxs-lookup"><span data-stu-id="d92dc-391">This folder contains the following required app package files:</span></span>

- <span data-ttu-id="d92dc-392">全 **色图标** ，大小为 192 x 192 像素。</span><span class="sxs-lookup"><span data-stu-id="d92dc-392">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="d92dc-393">一 **个 32** x 32 像素的透明边框图标。</span><span class="sxs-lookup"><span data-stu-id="d92dc-393">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="d92dc-394">指定 **manifest.js** 属性的 on 文件。</span><span class="sxs-lookup"><span data-stu-id="d92dc-394">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="d92dc-395">这些文件需要在应用包中压缩，以用于将选项卡上载到Teams。</span><span class="sxs-lookup"><span data-stu-id="d92dc-395">These files need to be zipped in an app package for use in uploading your tab to Teams.</span></span>

#### <a name="csproj"></a><span data-ttu-id="d92dc-396">.csproj</span><span class="sxs-lookup"><span data-stu-id="d92dc-396">.csproj</span></span>

<span data-ttu-id="d92dc-397">在"Visual Studio资源管理器"窗口中，右键单击项目并选择"编辑Project **文件"。**</span><span class="sxs-lookup"><span data-stu-id="d92dc-397">In the Visual Studio Solution Explorer window, right-click on the project and select **Edit Project File**.</span></span> <span data-ttu-id="d92dc-398">在文件末尾，你将看到以下代码，该代码在应用程序生成时创建和更新 zip 文件夹：</span><span class="sxs-lookup"><span data-stu-id="d92dc-398">At the end of the file you see the following code that creates and updates your zip folder when the application builds:</span></span>

```xml
<PropertyGroup>
    <PostBuildEvent>powershell.exe Compress-Archive -Path \"$(ProjectDir)AppManifest\*\" -DestinationPath \"$(TargetDir)tab.zip\" -Force</PostBuildEvent>
  </PropertyGroup>

  <ItemGroup>
    <EmbeddedResource Include="AppManifest\icon-outline.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\icon-color.png">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
    <EmbeddedResource Include="AppManifest\manifest.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </EmbeddedResource>
  </ItemGroup>
```

#### <a name="models"></a><span data-ttu-id="d92dc-399">模型</span><span class="sxs-lookup"><span data-stu-id="d92dc-399">Models</span></span>

<span data-ttu-id="d92dc-400">**ChannelGroup.cs** 提供 Message 对象和方法，将在配置过程中从控制器调用该对象和方法。</span><span class="sxs-lookup"><span data-stu-id="d92dc-400">**ChannelGroup.cs** presents a Message object and methods that will be called from the controllers during configuration.</span></span>

#### <a name="views"></a><span data-ttu-id="d92dc-401">视图</span><span class="sxs-lookup"><span data-stu-id="d92dc-401">Views</span></span>

<span data-ttu-id="d92dc-402">这些是 MVC 中 ASP.NET Core视图：</span><span class="sxs-lookup"><span data-stu-id="d92dc-402">These are the different views in ASP.NET Core MVC:</span></span>

* <span data-ttu-id="d92dc-403">主页：ASP.NET Core将名为 **Index** 的文件视为网站的默认页面或主页。</span><span class="sxs-lookup"><span data-stu-id="d92dc-403">Home: ASP.NET Core treats files called **Index** as the default or home page for the site.</span></span> <span data-ttu-id="d92dc-404">当浏览器 URL 指向网站的根目录时 **，Index.cshtml** 将显示为应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="d92dc-404">When your browser URL points to the root of the site, **Index.cshtml** will be displayed as the home page for your application.</span></span>

* <span data-ttu-id="d92dc-405">Shared：部分视图标记 **_Layout.cshtml** 包含应用程序的整体页面结构和共享的可视元素。</span><span class="sxs-lookup"><span data-stu-id="d92dc-405">Shared: The partial view markup **_Layout.cshtml** contains the application's overall page structure and shared visual elements.</span></span> <span data-ttu-id="d92dc-406">它还将引用Teams库。</span><span class="sxs-lookup"><span data-stu-id="d92dc-406">It will also reference the Teams Library.</span></span>

#### <a name="controllers"></a><span data-ttu-id="d92dc-407">控制器</span><span class="sxs-lookup"><span data-stu-id="d92dc-407">Controllers</span></span>

<span data-ttu-id="d92dc-408">控制器使用 `ViewBag` 属性将值动态传输给视图。</span><span class="sxs-lookup"><span data-stu-id="d92dc-408">The controllers use the `ViewBag` property to transfer values dynamically to the views.</span></span>

[!INCLUDE [dotnet-ngrok-intro](~/includes/tabs/dotnet-ngrok-intro.md)]

* <span data-ttu-id="d92dc-409">打开项目目录根目录中的命令提示符并运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="d92dc-409">Open a command prompt in the root of your project directory and run the following command:</span></span>

    ```bash
    ngrok http https://localhost:443560 -host-header="localhost:44360"
    ```

* <span data-ttu-id="d92dc-410">Ngrok 将侦听来自 Internet 的请求，并且将在应用程序在端口 44355 上运行时将它们路由到您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="d92dc-410">Ngrok will listen to requests from the internet and will route them to your application when it is running on port 44355.</span></span> <span data-ttu-id="d92dc-411">它应 `https://y8rCgT2b.ngrok.io/` 类似于 **y8rCgT2b** 替换为 ngrok 字母数字 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="d92dc-411">It should resemble `https://y8rCgT2b.ngrok.io/` where **y8rCgT2b** is replaced by your ngrok alpha-numeric HTTPS URL.</span></span>

* <span data-ttu-id="d92dc-412">确保使命令提示符保持运行 ngrok，并记下 URL。</span><span class="sxs-lookup"><span data-stu-id="d92dc-412">Ensure that you keep the command prompt with ngrok running and make a note of the URL.</span></span>

### <a name="update-your-application"></a><span data-ttu-id="d92dc-413">更新应用程序</span><span class="sxs-lookup"><span data-stu-id="d92dc-413">Update your application</span></span>

<span data-ttu-id="d92dc-414">在 **Tab.cshtml** 中，应用程序向用户显示两个选项按钮，用于显示带红色或灰色图标的选项卡。</span><span class="sxs-lookup"><span data-stu-id="d92dc-414">Within **Tab.cshtml** the application presents the user with two option buttons for displaying the tab with either a red or gray icon.</span></span> <span data-ttu-id="d92dc-415">选择"**选择灰色**"或"**选择红色**"按钮，分别触发或 ，设置 并启用配置页上的" `saveGray()` `saveRed()` `settings.setValidityState(true)` 保存"按钮。 </span><span class="sxs-lookup"><span data-stu-id="d92dc-415">Choosing the **Select Gray** or **Select Red** button, triggers `saveGray()` or `saveRed()`, respectively, sets `settings.setValidityState(true)`, and enables the **Save** button on the configuration page.</span></span> <span data-ttu-id="d92dc-416">此代码Teams您已完成配置要求，并且可以继续安装。</span><span class="sxs-lookup"><span data-stu-id="d92dc-416">This code lets Teams know that you have completed the configuration requirements and the installation can proceed.</span></span> <span data-ttu-id="d92dc-417">保存时，将设置 `settings.setSettings` 的参数。</span><span class="sxs-lookup"><span data-stu-id="d92dc-417">On save, the parameters of `settings.setSettings` are set.</span></span> <span data-ttu-id="d92dc-418">最后 `saveEvent.notifySuccess()` ，调用 以指示已成功解析内容 URL。</span><span class="sxs-lookup"><span data-stu-id="d92dc-418">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has been successfully resolved.</span></span>

[!INCLUDE [dotnet-update-app](~/includes/tabs/dotnet-update-chan-grp-app.md)]

---

## <a name="see-also"></a><span data-ttu-id="d92dc-419">另请参阅</span><span class="sxs-lookup"><span data-stu-id="d92dc-419">See also</span></span>

* [<span data-ttu-id="d92dc-420">Teams选项卡</span><span class="sxs-lookup"><span data-stu-id="d92dc-420">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="d92dc-421">创建个人选项卡</span><span class="sxs-lookup"><span data-stu-id="d92dc-421">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="d92dc-422">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="d92dc-422">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="d92dc-423">具有自适应卡片的生成选项卡</span><span class="sxs-lookup"><span data-stu-id="d92dc-423">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="next-step"></a><span data-ttu-id="d92dc-424">后续步骤</span><span class="sxs-lookup"><span data-stu-id="d92dc-424">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d92dc-425">创建内容页</span><span class="sxs-lookup"><span data-stu-id="d92dc-425">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
