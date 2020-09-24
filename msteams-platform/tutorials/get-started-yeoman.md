---
title: Microsoft 团队的 Yeoman 生成器入门
description: 使用 Microsoft 团队的 Yeoman 生成器开始构建强大的应用程序
keywords: 入门 node.js nodejs yeoman
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: f9b3f165d3b5387f8e7d30563134ed4889920ca5
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237991"
---
# <a name="build-your-first-microsoft-teams-app"></a><span data-ttu-id="f711b-104">构建你的首个 Microsoft 团队应用</span><span class="sxs-lookup"><span data-stu-id="f711b-104">Build your First Microsoft Teams App</span></span>

>[!Note]
><span data-ttu-id="f711b-105">本教程来自适用于 [团队 wiki 的 yeoman 生成器](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span><span class="sxs-lookup"><span data-stu-id="f711b-105">This tutorial comes from the [yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)</span></span>

<span data-ttu-id="f711b-106">在本教程中，我们将逐步介绍如何使用 Microsoft 团队 Yeoman 生成器创建首个 Microsoft 团队应用程序。</span><span class="sxs-lookup"><span data-stu-id="f711b-106">In this tutorial we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="f711b-107">它假定您已 [启用 Microsoft 团队应用程序的侧面加载](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="f711b-107">It assumes that you have [enabled side-loading of Microsoft Teams apps](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![yeoman 生成器 git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="f711b-109">设置和准备计算机</span><span class="sxs-lookup"><span data-stu-id="f711b-109">Setup and prepare your machine</span></span>

<span data-ttu-id="f711b-110">您需要在您的计算机上安装以下程序，然后才能开始使用团队生成器。</span><span class="sxs-lookup"><span data-stu-id="f711b-110">You need to install the following on your machine before starting to use the Teams Generator.</span></span>

### <a name="install-node"></a><span data-ttu-id="f711b-111">安装节点</span><span class="sxs-lookup"><span data-stu-id="f711b-111">Install Node</span></span>

<span data-ttu-id="f711b-112">您需要在您的计算机上安装 NodeJS。</span><span class="sxs-lookup"><span data-stu-id="f711b-112">You need to have NodeJS installed on your machine.</span></span> <span data-ttu-id="f711b-113">应使用最新的 [LTS 版本](https://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="f711b-113">You should use the latest [LTS version](https://nodejs.org).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="f711b-114">安装代码编辑器</span><span class="sxs-lookup"><span data-stu-id="f711b-114">Install a code editor</span></span>

<span data-ttu-id="f711b-115">此外，您还需要代码编辑器，可以随时使用您喜欢的任何文本编辑器。</span><span class="sxs-lookup"><span data-stu-id="f711b-115">You also need a code editor, feel free to use whatever text editor you prefer.</span></span> <span data-ttu-id="f711b-116">但大部分文档和屏幕截图都是指使用 [Visual Studio Code](https://code.visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="f711b-116">However most of this documentation and screenshots refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="f711b-117">安装 Yeoman 和 Gulp CLI</span><span class="sxs-lookup"><span data-stu-id="f711b-117">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="f711b-118">若要能够使用团队生成器搭建项目，您需要安装 Yeoman 工具以及 Gulp CLI 任务管理器。</span><span class="sxs-lookup"><span data-stu-id="f711b-118">To be able to scaffold projects using the Teams generator you need to install the Yeoman tool as well as the Gulp CLI task manager.</span></span>

<span data-ttu-id="f711b-119">打开命令提示符并键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="f711b-119">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-microsoft-teams-apps-generator---yo-teams"></a><span data-ttu-id="f711b-120">安装 Microsoft 团队应用生成器-Yo 团队</span><span class="sxs-lookup"><span data-stu-id="f711b-120">Install the Microsoft Teams Apps generator - Yo Teams</span></span>

<span data-ttu-id="f711b-121">使用以下命令安装 Microsoft 团队应用的 Yeoman 生成器：</span><span class="sxs-lookup"><span data-stu-id="f711b-121">The Yeoman generator for Microsoft Teams apps are installed with the following command:</span></span>

```bash
npm install generator-teams --global
```

#### <a name="install-preview-versions"></a><span data-ttu-id="f711b-122">安装预览版本</span><span class="sxs-lookup"><span data-stu-id="f711b-122">Install preview versions</span></span>

<span data-ttu-id="f711b-123">如果要使用此命令安装团队生成器的预览版本，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="f711b-123">If you want to install preview versions of the Teams generator with this command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="f711b-124">生成项目</span><span class="sxs-lookup"><span data-stu-id="f711b-124">Generate your project</span></span>

<span data-ttu-id="f711b-125">打开命令提示符并创建要在其中创建项目的新目录，并在该目录中键入该命令 `yo teams` 。</span><span class="sxs-lookup"><span data-stu-id="f711b-125">Open up a command prompt and create a new directory where you want to create your project and in that directory type the command `yo teams`.</span></span> <span data-ttu-id="f711b-126">这将启动 "团队应用生成器"，系统将会提示您一组问题。</span><span class="sxs-lookup"><span data-stu-id="f711b-126">This will start the Teams Apps generator and you will be asked a set of questions.</span></span>

![yo 团队](~/assets/yeoman-images/teams-first-app-1.png)

<span data-ttu-id="f711b-128">第一个问题是关于您的项目名称的，您可以通过按 enter 将其保留原样。</span><span class="sxs-lookup"><span data-stu-id="f711b-128">The first question is about your project name, you can leave it as is by pressing enter.</span></span> <span data-ttu-id="f711b-129">下一个问题会询问您是否要创建新目录或使用当前目录。</span><span class="sxs-lookup"><span data-stu-id="f711b-129">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="f711b-130">正如我们所需的目录中，我们只需按下 enter 键。</span><span class="sxs-lookup"><span data-stu-id="f711b-130">As we already are in the directory we want, we just press enter.</span></span>

<span data-ttu-id="f711b-131">下面的步骤要求您提供项目的标题，此标题将用于您的应用程序的清单和说明。</span><span class="sxs-lookup"><span data-stu-id="f711b-131">The following step asks for a title of your project, this title will be used in the manifest and description of your app.</span></span> <span data-ttu-id="f711b-132">然后，系统将要求你提供一个公司名称，该名称也将在清单中使用。</span><span class="sxs-lookup"><span data-stu-id="f711b-132">And then you will be asked for a company name, which also will be used in the manifest.</span></span>

<span data-ttu-id="f711b-133">第五个问题会询问您要使用的清单版本。</span><span class="sxs-lookup"><span data-stu-id="f711b-133">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="f711b-134">对于此教程，请选择 " `v1.5` 当前常规可用架构"。</span><span class="sxs-lookup"><span data-stu-id="f711b-134">For this tutorial select `v1.5`, which is the current general available schema.</span></span>

<span data-ttu-id="f711b-135">在此之后，生成器将询问您要添加到项目中的项目。</span><span class="sxs-lookup"><span data-stu-id="f711b-135">After this the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="f711b-136">您可以选择一个或多个项目组合。</span><span class="sxs-lookup"><span data-stu-id="f711b-136">You can select a single one or any combination of items.</span></span> <span data-ttu-id="f711b-137">现在，只需选择 *一个选项卡*。</span><span class="sxs-lookup"><span data-stu-id="f711b-137">For now, just select *a Tab*.</span></span>

![项目选择](~/assets/yeoman-images/teams-first-app-2.png)

<span data-ttu-id="f711b-139">根据您选择的项目，系统会询问您一组后续问题。</span><span class="sxs-lookup"><span data-stu-id="f711b-139">Based on what items you select, you will be asked a set of follow-up questions.</span></span>

<span data-ttu-id="f711b-140">现在，您需要输入将在其中承载解决方案的 URL。</span><span class="sxs-lookup"><span data-stu-id="f711b-140">Now you need to enter a URL of where you will host your solution.</span></span> <span data-ttu-id="f711b-141">它可以是任何 URL，但默认情况下生成器会建议 Azure 网站 URL。</span><span class="sxs-lookup"><span data-stu-id="f711b-141">This can be any URL, but by default the generator suggests an Azure Web Sites URL.</span></span>

<span data-ttu-id="f711b-142">生成器具有许多内置高级功能，您可以选择或选择退出。</span><span class="sxs-lookup"><span data-stu-id="f711b-142">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span> <span data-ttu-id="f711b-143">按照 URL 提示问题，系统将提示您是否要包括解决方案的单元测试，默认值为 "是"。</span><span class="sxs-lookup"><span data-stu-id="f711b-143">Following the URL question you will be asked if you want to include unit-testing for your solution, default is yes.</span></span> <span data-ttu-id="f711b-144">如果选择此选项，则生成的项目将具有单元测试框架，并且会对要搭建的不同项目进行一些默认的单元测试。</span><span class="sxs-lookup"><span data-stu-id="f711b-144">If you choose this the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> <span data-ttu-id="f711b-145">对于本教程，请选择不包含测试框架。</span><span class="sxs-lookup"><span data-stu-id="f711b-145">For this tutorial choose not to include a test framework.</span></span>

<span data-ttu-id="f711b-146">为了使日志记录变得简单，系统也会询问您是否要使用 Azure Application Insights 进行日志记录。</span><span class="sxs-lookup"><span data-stu-id="f711b-146">In order to make logging easy for you, you will also be asked if you want to use Azure Application Insights for logging.</span></span> <span data-ttu-id="f711b-147">如果你选择 "是"，你将需要提供 Azure Application Insights 密钥。</span><span class="sxs-lookup"><span data-stu-id="f711b-147">If you choose Yes, you will need to provide a Azure Application Insights key.</span></span> <span data-ttu-id="f711b-148">有关此教程，请退出使用 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="f711b-148">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="f711b-149">接下来的一组问题将基于您以前选择的项。</span><span class="sxs-lookup"><span data-stu-id="f711b-149">The next set of questions will be based on your selection of items previously.</span></span> <span data-ttu-id="f711b-150">对于选项卡，仅需要提供一个名称，并且可以选择是否希望能够将此应用用作 SharePoint Online web 部件。</span><span class="sxs-lookup"><span data-stu-id="f711b-150">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="f711b-151">提供此名称后，生成器将生成项目并安装所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="f711b-151">Once you have provided this name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="f711b-152">这需要一分钟或两分钟。</span><span class="sxs-lookup"><span data-stu-id="f711b-152">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="f711b-153">向您的选项卡添加一些代码</span><span class="sxs-lookup"><span data-stu-id="f711b-153">Add some code to your tab</span></span>

<span data-ttu-id="f711b-154">生成器完成后，您可以在最喜爱的代码编辑器中打开该解决方案。</span><span class="sxs-lookup"><span data-stu-id="f711b-154">Once the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="f711b-155">花一分钟或两分钟，熟悉代码的组织方式-您可以在 [项目结构](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) 文档中阅读有关该信息的详细信息。</span><span class="sxs-lookup"><span data-stu-id="f711b-155">Take a minute or two and familiarize yourself with how the code is organized - you can read more about that in the [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="f711b-156">您的选项卡将位于 `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` 文件中。</span><span class="sxs-lookup"><span data-stu-id="f711b-156">Your Tab will be located in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="f711b-157">这是您的选项卡的基于 TypeScript 响应的类。找到 `render()` 方法并在控件中添加一行代码， `<PanelBody>` 使其如下所示：</span><span class="sxs-lookup"><span data-stu-id="f711b-157">This is the TypeScript React based class for your Tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="f711b-158">保存文件并返回到命令提示符。</span><span class="sxs-lookup"><span data-stu-id="f711b-158">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="f711b-159">生成应用程序</span><span class="sxs-lookup"><span data-stu-id="f711b-159">Build your app</span></span>

<span data-ttu-id="f711b-160">现在可以生成项目。</span><span class="sxs-lookup"><span data-stu-id="f711b-160">You can now build your project.</span></span> <span data-ttu-id="f711b-161">这是通过两个步骤 (或一个步骤完成的，请参阅下面的) 。</span><span class="sxs-lookup"><span data-stu-id="f711b-161">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="f711b-162">首先，您需要创建团队应用程序清单文件，并将其上传/旁加载到 Microsoft 团队。</span><span class="sxs-lookup"><span data-stu-id="f711b-162">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="f711b-163">这是由 Gulp 任务完成的 `gulp manifest` 。</span><span class="sxs-lookup"><span data-stu-id="f711b-163">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="f711b-164">这将验证清单并在目录中创建 zip 文件 `./package` 。</span><span class="sxs-lookup"><span data-stu-id="f711b-164">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="f711b-165">若要生成解决方案，请使用 `gulp build` 命令。</span><span class="sxs-lookup"><span data-stu-id="f711b-165">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="f711b-166">这会将您的解决方案转换到该 `./dist` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="f711b-166">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="f711b-167">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="f711b-167">Run your app</span></span>

<span data-ttu-id="f711b-168">若要运行您的应用程序，请使用 `gulp serve` 命令。</span><span class="sxs-lookup"><span data-stu-id="f711b-168">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="f711b-169">这将为您生成并启动一个本地 web 服务器来测试您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="f711b-169">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="f711b-170">当您在项目中保存文件时，该命令也会重新生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="f711b-170">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="f711b-171">现在，您应该能够浏览到 `http://localhost:3007/myFirstAppTab/` ，以确保您的选项卡呈现。</span><span class="sxs-lookup"><span data-stu-id="f711b-171">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="f711b-172">但在 Microsoft 团队中尚不会。</span><span class="sxs-lookup"><span data-stu-id="f711b-172">However, not in Microsoft Teams yet.</span></span>

![在浏览器中查看网站](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="f711b-174">在 Microsoft 团队中运行应用程序</span><span class="sxs-lookup"><span data-stu-id="f711b-174">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="f711b-175">Microsoft 团队不允许您在 localhost 上托管您的应用程序，因此您需要将其发布到公用 URL 或使用代理（如 ngrok）。</span><span class="sxs-lookup"><span data-stu-id="f711b-175">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="f711b-176">好消息是搭建项目具有此内置的。</span><span class="sxs-lookup"><span data-stu-id="f711b-176">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="f711b-177">在运行 `gulp ngrok-serve` ngrok 服务时，将在后台启动，并使用唯一的公共 DNS 条目，并将清单打包为该唯一的 URL，然后执行与相同的完全相同的任务 `gulp serve` 。</span><span class="sxs-lookup"><span data-stu-id="f711b-177">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="f711b-178">运行后 `gulp ngrok-serve` ，创建一个新的 Microsoft 团队团队，并在创建时单击团队名称，以转到 "团队设置"，然后选择 " *应用*"。</span><span class="sxs-lookup"><span data-stu-id="f711b-178">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="f711b-179">在右下角，您应该会看到一个链接 " *上传自定义应用程序*"，选择它，然后浏览到您的项目文件夹和名为的子文件夹 `package` 。</span><span class="sxs-lookup"><span data-stu-id="f711b-179">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="f711b-180">选择该文件夹中的 zip 文件，然后选择 "打开"。</span><span class="sxs-lookup"><span data-stu-id="f711b-180">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="f711b-181">现在，您的应用程序将旁加载到 Microsoft 团队中。</span><span class="sxs-lookup"><span data-stu-id="f711b-181">Your App is now sideloaded into Microsoft Teams.</span></span>

![旁加载应用程序](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="f711b-183">返回到 *常规* 频道并选择 *+* 添加新的选项卡。您应该会在选项卡列表中看到您的选项卡。</span><span class="sxs-lookup"><span data-stu-id="f711b-183">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs.</span></span>

![配置选项卡](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="f711b-185">选择您的选项卡，然后按照说明添加它。</span><span class="sxs-lookup"><span data-stu-id="f711b-185">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="f711b-186">请注意，您有一个自定义配置对话框，您可以在其中编辑该源。</span><span class="sxs-lookup"><span data-stu-id="f711b-186">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="f711b-187">选择 " *保存* " 将选项卡添加到频道。</span><span class="sxs-lookup"><span data-stu-id="f711b-187">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="f711b-188">完成后，应在 Microsoft 团队中加载您的选项卡！</span><span class="sxs-lookup"><span data-stu-id="f711b-188">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![在团队中运行选项卡](~/assets/yeoman-images/teams-first-app-6.png)

<span data-ttu-id="f711b-190">**Congrats!你构建并部署了你的首个 Microsoft 团队应用**</span><span class="sxs-lookup"><span data-stu-id="f711b-190">**Congrats! You built and deployed your first Microsoft Teams App**</span></span>
