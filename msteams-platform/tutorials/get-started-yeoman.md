---
title: 教程 - 使用 Yeoman 生成器创建第一个应用
description: 了解如何开始使用 Yeoman Microsoft Teams生成应用。
keywords: nodejs yeoman node.js入门
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: 96a4f64d487e1d16bf25abd978759fedeac1061c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566822"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="e8598-104">使用 Yeoman Microsoft Teams创建你的第一个应用</span><span class="sxs-lookup"><span data-stu-id="e8598-104">Create your first Microsoft Teams app using the Yeoman generator</span></span>

> [!Note]
> <span data-ttu-id="e8598-105">本教程来自适用于 wiki[的 Yeoman Teams生成器](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。</span><span class="sxs-lookup"><span data-stu-id="e8598-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="e8598-106">本教程介绍如何使用 Yeoman Microsoft Teams创建首个Microsoft Teams应用。</span><span class="sxs-lookup"><span data-stu-id="e8598-106">In this tutorial, we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="e8598-107">它还指导你完成使用 Yeoman 生成器Teams升级应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="e8598-107">It also walks you through the process of upgrading your Teams using the Yeoman generator.</span></span> <span data-ttu-id="e8598-108">从本教程开始的先决条件是，你拥有一个Teams允许[应用旁加载的帐户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="e8598-108">The prerequisite to start with this tutorial is that you have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![yeoman 生成器 git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="e8598-110">设置和准备计算机</span><span class="sxs-lookup"><span data-stu-id="e8598-110">Setup and prepare your machine</span></span>

<span data-ttu-id="e8598-111">在开始使用 Yeoman 生成器之前，你需要在计算机上安装以下组件。</span><span class="sxs-lookup"><span data-stu-id="e8598-111">You need to install the following on your machine before starting to use the Yeoman generator.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="e8598-112">安装 Node.js</span><span class="sxs-lookup"><span data-stu-id="e8598-112">Install Node.js</span></span>

<span data-ttu-id="e8598-113">你需要将Node.js计算机上安装。</span><span class="sxs-lookup"><span data-stu-id="e8598-113">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="e8598-114">你应该使用最新的 [LTS 版本](https://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="e8598-114">You should use the latest [LTS version](https://nodejs.org).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="e8598-115">安装代码编辑器</span><span class="sxs-lookup"><span data-stu-id="e8598-115">Install a code editor</span></span>

<span data-ttu-id="e8598-116">你需要一个代码编辑器。</span><span class="sxs-lookup"><span data-stu-id="e8598-116">You need a code editor.</span></span> <span data-ttu-id="e8598-117">本文档和图像中的大多数内容都指使用[Visual Studio Code。](https://code.visualstudio.com)</span><span class="sxs-lookup"><span data-stu-id="e8598-117">Most of this documentation and images refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span> <span data-ttu-id="e8598-118">但是，您可以随意使用您喜欢的任何文本编辑器。</span><span class="sxs-lookup"><span data-stu-id="e8598-118">However, feel free to use whatever text editor you prefer.</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="e8598-119">安装 Yeoman 和 Gulp CLI</span><span class="sxs-lookup"><span data-stu-id="e8598-119">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="e8598-120">若要使用生成器搭建项目基架，必须安装 Yeoman 工具和 Gulp CLI 任务管理器。</span><span class="sxs-lookup"><span data-stu-id="e8598-120">To scaffold projects using the generator, you must install the Yeoman tool and Gulp CLI task manager.</span></span>

<span data-ttu-id="e8598-121">打开命令提示符并键入以下内容：</span><span class="sxs-lookup"><span data-stu-id="e8598-121">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a><span data-ttu-id="e8598-122">安装生成器</span><span class="sxs-lookup"><span data-stu-id="e8598-122">Install the generator</span></span>

<span data-ttu-id="e8598-123">使用Teams安装 Yeoman 生成器：</span><span class="sxs-lookup"><span data-stu-id="e8598-123">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm install generator-teams --global
```

<span data-ttu-id="e8598-124">使用下列命令安装生成器的预览版本：</span><span class="sxs-lookup"><span data-stu-id="e8598-124">Install the preview version of the generator with the following command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="e8598-125">生成项目</span><span class="sxs-lookup"><span data-stu-id="e8598-125">Generate your project</span></span>

<span data-ttu-id="e8598-126">本节将指导你完成生成项目的步骤。</span><span class="sxs-lookup"><span data-stu-id="e8598-126">This section walks you through the steps for generating your project.</span></span>

<span data-ttu-id="e8598-127">**生成项目**</span><span class="sxs-lookup"><span data-stu-id="e8598-127">**To generate your project**</span></span>

1. <span data-ttu-id="e8598-128">打开命令提示符并创建要创建项目的新目录，并运行命令 `yo teams` 。</span><span class="sxs-lookup"><span data-stu-id="e8598-128">Open up a command prompt and create a new directory where you want to create your project, and in that directory run the command `yo teams`.</span></span> <span data-ttu-id="e8598-129">生成器启动。</span><span class="sxs-lookup"><span data-stu-id="e8598-129">The generator starts.</span></span>
1. <span data-ttu-id="e8598-130">响应生成器提示的一组问题：</span><span class="sxs-lookup"><span data-stu-id="e8598-130">Respond to the set of questions prompted by the generator:</span></span>

   ![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

   1. <span data-ttu-id="e8598-132">第一个问题是有关您的项目名称，您可以通过按 Enter 来保留它。</span><span class="sxs-lookup"><span data-stu-id="e8598-132">The first question is about your project name, you can leave it as is by pressing enter.</span></span>
   1. <span data-ttu-id="e8598-133">下一个问题询问您是否要创建新目录或使用当前目录。</span><span class="sxs-lookup"><span data-stu-id="e8598-133">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="e8598-134">由于你已进入你需要的目录中，只需按 Enter。</span><span class="sxs-lookup"><span data-stu-id="e8598-134">As you are already in the directory you want, just press enter.</span></span>
   1. <span data-ttu-id="e8598-135">在下一个问题中，键入项目的标题。</span><span class="sxs-lookup"><span data-stu-id="e8598-135">In the next question, type the title of your project.</span></span> <span data-ttu-id="e8598-136">此标题将在应用的清单和说明中使用。</span><span class="sxs-lookup"><span data-stu-id="e8598-136">This title will be used in the manifest and description of your app.</span></span> 
   1. <span data-ttu-id="e8598-137">接下来，将要求您输入公司名称，该名称也将在清单中使用。</span><span class="sxs-lookup"><span data-stu-id="e8598-137">Next, you will be asked for a company name, which also will be used in the manifest.</span></span>
   1. <span data-ttu-id="e8598-138">第五个问题询问您想要使用的清单版本。</span><span class="sxs-lookup"><span data-stu-id="e8598-138">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="e8598-139">对于本教程，请选择 `v1.5` ，这是当前可用的常规架构。</span><span class="sxs-lookup"><span data-stu-id="e8598-139">For this tutorial select `v1.5`, which is the current general available schema.</span></span>
   1. <span data-ttu-id="e8598-140">接下来，生成器将询问要添加到项目中的项目。</span><span class="sxs-lookup"><span data-stu-id="e8598-140">Next, the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="e8598-141">可以选择单个项目或任意项目组合。</span><span class="sxs-lookup"><span data-stu-id="e8598-141">You can select a single one or any combination of items.</span></span> <span data-ttu-id="e8598-142">对于本教程，只需选择 *一个选项卡*：</span><span class="sxs-lookup"><span data-stu-id="e8598-142">For this tutorials, just select *a Tab*:</span></span>

    ![项目选择](~/assets/yeoman-images/teams-first-app-2.png)

1. <span data-ttu-id="e8598-144">响应下一组基于在步骤 2 中选定的项目出现的后续问题。</span><span class="sxs-lookup"><span data-stu-id="e8598-144">Respond to the next set of follow-up questions that appear based on the items you selected in step 2.</span></span>
1. <span data-ttu-id="e8598-145">输入解决方案的托管位置的 URL。</span><span class="sxs-lookup"><span data-stu-id="e8598-145">Enter a URL of where you will host your solution.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="e8598-146">该 URL 可以是任何 URL，但默认情况下，生成器建议 Azure 网站 URL。</span><span class="sxs-lookup"><span data-stu-id="e8598-146">The URL can be any URL, but by default the generator suggests an Azure web site URL.</span></span>

1. <span data-ttu-id="e8598-147">在下一个问题中，确认是否要包含解决方案的单元测试。</span><span class="sxs-lookup"><span data-stu-id="e8598-147">In the next question, confirm if you want to include unit-testing for your solution.</span></span> <span data-ttu-id="e8598-148">默认 *响应是*。</span><span class="sxs-lookup"><span data-stu-id="e8598-148">The default response is *yes*.</span></span> <span data-ttu-id="e8598-149">如果选择包括单元测试，则生成的项目将具有一个单元测试框架和一些用于搭建基架的不同项目的默认单元测试。</span><span class="sxs-lookup"><span data-stu-id="e8598-149">If you choose to include unit-testing, the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> 
   > [!NOTE]
   > * <span data-ttu-id="e8598-150">对于本教程，选择不包括测试框架。</span><span class="sxs-lookup"><span data-stu-id="e8598-150">For this tutorial choose not to include a test framework.</span></span>
   > * <span data-ttu-id="e8598-151">生成器具有许多内置高级功能，你可以选择加入或选择退出。</span><span class="sxs-lookup"><span data-stu-id="e8598-151">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span>

1. <span data-ttu-id="e8598-152">为了便于你登录，还将询问你是否要使用 Azure Application Insights 进行登录。</span><span class="sxs-lookup"><span data-stu-id="e8598-152">In order to make signing-in easy for you, you will also be asked if you want to use Azure Application Insights for signing-in.</span></span> <span data-ttu-id="e8598-153">如果选择" *是"，* 则需要提供 Azure Application Insights 密钥。</span><span class="sxs-lookup"><span data-stu-id="e8598-153">If you choose *Yes*, you will need to provide an Azure Application Insights key.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="e8598-154">对于本教程，选择退出使用 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="e8598-154">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="e8598-155">下一组问题将基于之前选定的项目。</span><span class="sxs-lookup"><span data-stu-id="e8598-155">The next set of questions will be based on the previously selected items.</span></span> <span data-ttu-id="e8598-156">对于选项卡，你只需提供一个名称，并可以选择是否希望能够使用此应用作为 SharePoint Online Web 部件。</span><span class="sxs-lookup"><span data-stu-id="e8598-156">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="e8598-157">提供名称后，生成器将生成项目并安装所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="e8598-157">After you provide the name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="e8598-158">这可能需要一两分钟的时间。</span><span class="sxs-lookup"><span data-stu-id="e8598-158">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="e8598-159">向选项卡添加一些代码</span><span class="sxs-lookup"><span data-stu-id="e8598-159">Add some code to your tab</span></span>

<span data-ttu-id="e8598-160">生成器完成后，可以在最喜爱的代码编辑器中打开解决方案。</span><span class="sxs-lookup"><span data-stu-id="e8598-160">After the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="e8598-161">请花一两分钟的时间，熟悉代码的整理方式。</span><span class="sxs-lookup"><span data-stu-id="e8598-161">Take a minute or two and familiarize yourself with how the code is organized.</span></span> <span data-ttu-id="e8598-162">有关详细信息，请参阅Project[结构](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)文档。</span><span class="sxs-lookup"><span data-stu-id="e8598-162">For more information, see [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="e8598-163">您的选项卡位于 `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` 文件中。</span><span class="sxs-lookup"><span data-stu-id="e8598-163">Your tab is in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="e8598-164">这是选项卡React TypeScript 类。找到 `render()` 方法，在控件中添加一 `<PanelBody>` 行代码，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e8598-164">This is the TypeScript React-based class for your tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="e8598-165">保存文件并返回到命令提示符。</span><span class="sxs-lookup"><span data-stu-id="e8598-165">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="e8598-166">生成应用程序</span><span class="sxs-lookup"><span data-stu-id="e8598-166">Build your app</span></span>

<span data-ttu-id="e8598-167">现在可以生成项目。</span><span class="sxs-lookup"><span data-stu-id="e8598-167">You can now build your project.</span></span> <span data-ttu-id="e8598-168">此操作分两个步骤完成， (一个步骤，请参阅下面的) 。</span><span class="sxs-lookup"><span data-stu-id="e8598-168">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="e8598-169">首先，你需要创建Teams清单文件，将该文件上载/旁加载到Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="e8598-169">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="e8598-170">这由 Gulp 任务完成 `gulp manifest` 。</span><span class="sxs-lookup"><span data-stu-id="e8598-170">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="e8598-171">这将验证清单，并创建目录中的 zip `./package` 文件。</span><span class="sxs-lookup"><span data-stu-id="e8598-171">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="e8598-172">若要生成解决方案，请使用 `gulp build` 命令。</span><span class="sxs-lookup"><span data-stu-id="e8598-172">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="e8598-173">这会将解决方案转换为 `./dist` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e8598-173">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="e8598-174">运行应用</span><span class="sxs-lookup"><span data-stu-id="e8598-174">Run your app</span></span>

<span data-ttu-id="e8598-175">若要运行应用，请使用 `gulp serve` 命令。</span><span class="sxs-lookup"><span data-stu-id="e8598-175">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="e8598-176">这将生成并启动本地 Web 服务器，以测试你的应用。</span><span class="sxs-lookup"><span data-stu-id="e8598-176">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="e8598-177">每次在项目中保存文件时，该命令也将重新生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="e8598-177">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="e8598-178">现在，你应该能够浏览以确保 `http://localhost:3007/myFirstAppTab/` 选项卡正在呈现。</span><span class="sxs-lookup"><span data-stu-id="e8598-178">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="e8598-179">但是，尚不Microsoft Teams：</span><span class="sxs-lookup"><span data-stu-id="e8598-179">However, not in Microsoft Teams yet:</span></span>

![在浏览器中查看网站](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="e8598-181">在应用商店中Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e8598-181">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="e8598-182">Microsoft Teams不允许将应用托管在 localhost 上，因此你需要将其发布到公用 URL 或使用代理（如 ngrok）。</span><span class="sxs-lookup"><span data-stu-id="e8598-182">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="e8598-183">好消息是，搭建的项目具有此内置功能。</span><span class="sxs-lookup"><span data-stu-id="e8598-183">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="e8598-184">运行 ngrok 服务时，将在后台启动具有唯一的公用 DNS 条目，并且它还将清单打包为此唯一 URL，然后执行与 完全相同 `gulp ngrok-serve` 的操作 `gulp serve` 。</span><span class="sxs-lookup"><span data-stu-id="e8598-184">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="e8598-185">运行 `gulp ngrok-serve` 后，创建新的Microsoft Teams团队，创建团队时单击团队名称，转到团队设置，然后选择应用。 </span><span class="sxs-lookup"><span data-stu-id="e8598-185">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="e8598-186">在右下角，你应该会看到自定义Upload *的链接，* 选择它，然后浏览到项目文件夹和名为 的子文件夹 `package` 。</span><span class="sxs-lookup"><span data-stu-id="e8598-186">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="e8598-187">选择该文件夹中的 zip 文件，然后选择"打开"。</span><span class="sxs-lookup"><span data-stu-id="e8598-187">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="e8598-188">你的应用现在旁加载到Microsoft Teams：</span><span class="sxs-lookup"><span data-stu-id="e8598-188">Your App is now sideloaded into Microsoft Teams:</span></span>

![旁加载的应用](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="e8598-190">返回到 *常规频道，* 然后选择 *+* 添加新的选项卡。你应该在选项卡列表中看到您的选项卡：</span><span class="sxs-lookup"><span data-stu-id="e8598-190">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs:</span></span>

![配置选项卡](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="e8598-192">选择您的选项卡，然后按照说明添加它。</span><span class="sxs-lookup"><span data-stu-id="e8598-192">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="e8598-193">请注意，有一个自定义配置对话框，您可以编辑其源。</span><span class="sxs-lookup"><span data-stu-id="e8598-193">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="e8598-194">选择 *"保存* "将选项卡添加到频道。</span><span class="sxs-lookup"><span data-stu-id="e8598-194">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="e8598-195">完成后，您的选项卡应加载到 Microsoft Teams！</span><span class="sxs-lookup"><span data-stu-id="e8598-195">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![teams 中的"运行"选项卡](~/assets/yeoman-images/teams-first-app-6.png)

## <a name="upgrade-microsoft-teams"></a><span data-ttu-id="e8598-197">升级Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e8598-197">Upgrade Microsoft Teams</span></span>

<span data-ttu-id="e8598-198">还可使用 Yeoman Microsoft Teams将当前 Microsoft Teams 版本升级到最新版本。</span><span class="sxs-lookup"><span data-stu-id="e8598-198">You can also upgrade your current Microsoft Teams version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

<span data-ttu-id="e8598-199">**升级Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="e8598-199">**To upgrade Microsoft Teams**</span></span>

1. <span data-ttu-id="e8598-200">通过以下命令Teams获取当前版本的版本：</span><span class="sxs-lookup"><span data-stu-id="e8598-200">Get current version of Teams with the following command:</span></span>

   ```PowerShell
    yo teams --version
   ```
2. <span data-ttu-id="e8598-201">使用以下命令选择更新生成器：</span><span class="sxs-lookup"><span data-stu-id="e8598-201">Use the following command to select update your generator:</span></span>

   ```PowerShell
    yo
   ```
3. <span data-ttu-id="e8598-202">使用箭头键选择更新 **生成器**：</span><span class="sxs-lookup"><span data-stu-id="e8598-202">Use the  arrow keys to choose **Update your Generators**:</span></span>

   ![YoSelectUpdatGen 的图像](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. <span data-ttu-id="e8598-204">从生成器列表中选择你需要的生成器：</span><span class="sxs-lookup"><span data-stu-id="e8598-204">Select the generator you want from the list of generators:</span></span>
   > [!NOTE]
   > <span data-ttu-id="e8598-205">使用空格键从可用选项Teams或清除所选版本。</span><span class="sxs-lookup"><span data-stu-id="e8598-205">Use the space bar to select or clear a selected Teams version from the available options.</span></span>

    ![UseSpaceToSelectGenerators 的图像](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > <span data-ttu-id="e8598-207">完成安装需要几秒钟到Teams分钟。</span><span class="sxs-lookup"><span data-stu-id="e8598-207">It takes few seconds to minutes for Teams installation to complete.</span></span>

5. <span data-ttu-id="e8598-208">安装完成后，使用以下命令检查安装的版本：</span><span class="sxs-lookup"><span data-stu-id="e8598-208">After the installation is complete, use the following command to check the installed version:</span></span>

   ```PowerShell
    yo teams --version
   ```
   
<span data-ttu-id="e8598-209">**恭喜！生成并部署了第一个Microsoft Teams应用。你还升级了Microsoft Teams。**</span><span class="sxs-lookup"><span data-stu-id="e8598-209">**Congrats! You built and deployed your first Microsoft Teams app. You also upgraded Microsoft Teams.**</span></span>
