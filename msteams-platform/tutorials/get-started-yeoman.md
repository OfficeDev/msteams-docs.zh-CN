---
title: 教程 - 使用 Yeoman 生成器创建第一个应用
description: 了解如何开始使用 Yeoman 生成器生成 Microsoft Teams 应用。
keywords: nodejs yeoman node.js入门
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: f7f0fb3ba1be28dfa7d343be3af9d122b4ad090d
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037002"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="4222c-104">使用 Yeoman 生成器创建你的第一个 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="4222c-104">Create your first Microsoft Teams app using the Yeoman generator</span></span>

>[!Note]
><span data-ttu-id="4222c-105">本教程来自 Teams [Wiki 的 Yeoman 生成器](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。</span><span class="sxs-lookup"><span data-stu-id="4222c-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="4222c-106">本教程介绍如何使用 Microsoft Teams Yeoman 生成器创建首个 Microsoft Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="4222c-106">In this tutorial we will walk through creating your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="4222c-107">它假定你有一个允许应用旁 [加载的](~/concepts/build-and-test/prepare-your-o365-tenant.md)Teams 帐户。</span><span class="sxs-lookup"><span data-stu-id="4222c-107">It assumes that you have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![yeoman 生成器 git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a><span data-ttu-id="4222c-109">设置和准备计算机</span><span class="sxs-lookup"><span data-stu-id="4222c-109">Setup and prepare your machine</span></span>

<span data-ttu-id="4222c-110">在开始使用 Yeoman 生成器之前，你需要在计算机上安装以下组件。</span><span class="sxs-lookup"><span data-stu-id="4222c-110">You need to install the following on your machine before starting to use the Yeoman generator.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="4222c-111">安装 Node.js</span><span class="sxs-lookup"><span data-stu-id="4222c-111">Install Node.js</span></span>

<span data-ttu-id="4222c-112">你需要将Node.js安装在计算机上。</span><span class="sxs-lookup"><span data-stu-id="4222c-112">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="4222c-113">你应该使用最新的 [LTS 版本](https://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="4222c-113">You should use the latest [LTS version](https://nodejs.org).</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="4222c-114">安装代码编辑器</span><span class="sxs-lookup"><span data-stu-id="4222c-114">Install a code editor</span></span>

<span data-ttu-id="4222c-115">你还需要一个代码编辑器，可以随意使用你喜欢的任何文本编辑器。</span><span class="sxs-lookup"><span data-stu-id="4222c-115">You also need a code editor, feel free to use whatever text editor you prefer.</span></span> <span data-ttu-id="4222c-116">但是，本文档和屏幕截图中的大多数内容都指使用Visual Studio [代码](https://code.visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="4222c-116">However most of this documentation and screenshots refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span>

### <a name="install-yeoman-and-gulp-cli"></a><span data-ttu-id="4222c-117">安装 Yeoman 和 Gulp CLI</span><span class="sxs-lookup"><span data-stu-id="4222c-117">Install Yeoman and Gulp CLI</span></span>

<span data-ttu-id="4222c-118">若要能够使用 Teams 生成器搭建项目，需要安装 Yeoman 工具以及 Gulp CLI 任务管理器。</span><span class="sxs-lookup"><span data-stu-id="4222c-118">To be able to scaffold projects using the Teams generator you need to install the Yeoman tool as well as the Gulp CLI task manager.</span></span>

<span data-ttu-id="4222c-119">打开命令提示符并键入以下内容：</span><span class="sxs-lookup"><span data-stu-id="4222c-119">Open up a command prompt and type the following:</span></span>

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a><span data-ttu-id="4222c-120">安装生成器</span><span class="sxs-lookup"><span data-stu-id="4222c-120">Install the generator</span></span>

<span data-ttu-id="4222c-121">使用以下命令安装 Teams Yeoman 生成器：</span><span class="sxs-lookup"><span data-stu-id="4222c-121">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm install generator-teams --global
```

<span data-ttu-id="4222c-122">若要安装生成器的预览版本，请运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="4222c-122">To install preview versions of the generator, run this command:</span></span>

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a><span data-ttu-id="4222c-123">生成项目</span><span class="sxs-lookup"><span data-stu-id="4222c-123">Generate your project</span></span>

<span data-ttu-id="4222c-124">打开命令提示符并创建要创建项目的新目录，并运行命令 `yo teams` 。</span><span class="sxs-lookup"><span data-stu-id="4222c-124">Open up a command prompt and create a new directory where you want to create your project and in that directory run the command `yo teams`.</span></span>

<span data-ttu-id="4222c-125">这会启动生成器，这会提示您一组问题。</span><span class="sxs-lookup"><span data-stu-id="4222c-125">This starts the generator, which prompts you with a set of questions.</span></span>

![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

<span data-ttu-id="4222c-127">第一个问题与项目名称有关，可以通过按 Enter 来保留它。</span><span class="sxs-lookup"><span data-stu-id="4222c-127">The first question is about your project name, you can leave it as is by pressing enter.</span></span> <span data-ttu-id="4222c-128">下一个问题询问您是否要创建新目录或使用当前目录。</span><span class="sxs-lookup"><span data-stu-id="4222c-128">Next question asks you if you want to create a new directory or use the current one.</span></span> <span data-ttu-id="4222c-129">由于我们已在我们需要的目录中，只需按 Enter 键。</span><span class="sxs-lookup"><span data-stu-id="4222c-129">As we already are in the directory we want, we just press enter.</span></span>

<span data-ttu-id="4222c-130">下一步需要项目的标题，此标题将在应用的清单和说明中使用。</span><span class="sxs-lookup"><span data-stu-id="4222c-130">The following step asks for a title of your project, this title will be used in the manifest and description of your app.</span></span> <span data-ttu-id="4222c-131">然后，将要求您输入公司名称，该名称也将在清单中使用。</span><span class="sxs-lookup"><span data-stu-id="4222c-131">And then you will be asked for a company name, which also will be used in the manifest.</span></span>

<span data-ttu-id="4222c-132">第五个问题询问您有关想要使用的清单版本。</span><span class="sxs-lookup"><span data-stu-id="4222c-132">The fifth question asks you about what version of the manifest you want to use.</span></span> <span data-ttu-id="4222c-133">对于本教程， `v1.5` 请选择当前可用的常规架构。</span><span class="sxs-lookup"><span data-stu-id="4222c-133">For this tutorial select `v1.5`, which is the current general available schema.</span></span>

<span data-ttu-id="4222c-134">在此之后，生成器将询问要添加到项目中的项目。</span><span class="sxs-lookup"><span data-stu-id="4222c-134">After this the generator will ask you for what items you want to add to your project.</span></span> <span data-ttu-id="4222c-135">可以选择单个项目或任意项目组合。</span><span class="sxs-lookup"><span data-stu-id="4222c-135">You can select a single one or any combination of items.</span></span> <span data-ttu-id="4222c-136">现在，只需选择 *一个选项卡*。</span><span class="sxs-lookup"><span data-stu-id="4222c-136">For now, just select *a Tab*.</span></span>

![项目选择](~/assets/yeoman-images/teams-first-app-2.png)

<span data-ttu-id="4222c-138">根据选择的项目，将询问一组后续问题。</span><span class="sxs-lookup"><span data-stu-id="4222c-138">Based on what items you select, you will be asked a set of follow-up questions.</span></span>

<span data-ttu-id="4222c-139">现在您需要输入解决方案的托管位置的 URL。</span><span class="sxs-lookup"><span data-stu-id="4222c-139">Now you need to enter a URL of where you will host your solution.</span></span> <span data-ttu-id="4222c-140">这可以是任何 URL，但默认情况下，生成器建议使用 Azure 网站 URL。</span><span class="sxs-lookup"><span data-stu-id="4222c-140">This can be any URL, but by default the generator suggests an Azure Web Sites URL.</span></span>

<span data-ttu-id="4222c-141">生成器具有许多内置高级功能，你可以选择加入或选择退出。</span><span class="sxs-lookup"><span data-stu-id="4222c-141">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span> <span data-ttu-id="4222c-142">在 URL 问题后，将询问您是否要包含解决方案的单元测试，默认值为"是"。</span><span class="sxs-lookup"><span data-stu-id="4222c-142">Following the URL question you will be asked if you want to include unit-testing for your solution, default is yes.</span></span> <span data-ttu-id="4222c-143">如果选择此选项，生成的项目将具有单元测试框架和一些用于搭建基架的不同项的默认单元测试。</span><span class="sxs-lookup"><span data-stu-id="4222c-143">If you choose this the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> <span data-ttu-id="4222c-144">对于本教程，选择不包括测试框架。</span><span class="sxs-lookup"><span data-stu-id="4222c-144">For this tutorial choose not to include a test framework.</span></span>

<span data-ttu-id="4222c-145">为了便于进行日志记录，还会询问您是否要使用 Azure 应用程序见解进行日志记录。</span><span class="sxs-lookup"><span data-stu-id="4222c-145">In order to make logging easy for you, you will also be asked if you want to use Azure Application Insights for logging.</span></span> <span data-ttu-id="4222c-146">如果选择"是"，则需要提供 Azure 应用程序见解密钥。</span><span class="sxs-lookup"><span data-stu-id="4222c-146">If you choose Yes, you will need to provide a Azure Application Insights key.</span></span> <span data-ttu-id="4222c-147">对于本教程，选择退出使用 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="4222c-147">For this tutorial opt-out of using Application Insights.</span></span>

<span data-ttu-id="4222c-148">下一组问题将基于你之前选择的项目。</span><span class="sxs-lookup"><span data-stu-id="4222c-148">The next set of questions will be based on your selection of items previously.</span></span> <span data-ttu-id="4222c-149">对于选项卡，你只需提供一个名称，并且可以选择是否希望将此应用程序用作 SharePoint Online Web 部件。</span><span class="sxs-lookup"><span data-stu-id="4222c-149">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="4222c-150">提供此名称后，生成器将生成项目并安装所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="4222c-150">Once you have provided this name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="4222c-151">这将需要一两分钟。</span><span class="sxs-lookup"><span data-stu-id="4222c-151">This will take a minute or two.</span></span>

## <a name="add-some-code-to-your-tab"></a><span data-ttu-id="4222c-152">向选项卡添加一些代码</span><span class="sxs-lookup"><span data-stu-id="4222c-152">Add some code to your tab</span></span>

<span data-ttu-id="4222c-153">生成器完成后，可以在你最喜爱的代码编辑器中打开解决方案。</span><span class="sxs-lookup"><span data-stu-id="4222c-153">Once the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="4222c-154">请花一两分钟，熟悉代码的组织结构，您可以在项目结构文档中阅读 [有关该代码](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) 的更多内容。</span><span class="sxs-lookup"><span data-stu-id="4222c-154">Take a minute or two and familiarize yourself with how the code is organized - you can read more about that in the [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="4222c-155">您的选项卡将位于 `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` 文件中。</span><span class="sxs-lookup"><span data-stu-id="4222c-155">Your Tab will be located in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="4222c-156">这是 Tab 的基于 TypeScript React 的类。找到该方法，在控件内添加一行代码，如下所示 `render()` `<PanelBody>` ：</span><span class="sxs-lookup"><span data-stu-id="4222c-156">This is the TypeScript React based class for your Tab. Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

<span data-ttu-id="4222c-157">保存文件并返回到命令提示符。</span><span class="sxs-lookup"><span data-stu-id="4222c-157">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="4222c-158">生成应用程序</span><span class="sxs-lookup"><span data-stu-id="4222c-158">Build your app</span></span>

<span data-ttu-id="4222c-159">现在可以生成项目。</span><span class="sxs-lookup"><span data-stu-id="4222c-159">You can now build your project.</span></span> <span data-ttu-id="4222c-160">此操作分两步完成， (一个步骤，请参阅下面的) 。</span><span class="sxs-lookup"><span data-stu-id="4222c-160">This is done in two steps (or one step, see below).</span></span>

<span data-ttu-id="4222c-161">首先，你需要创建 Teams 应用清单文件，将其上载/旁加载到 Microsoft Teams 中。</span><span class="sxs-lookup"><span data-stu-id="4222c-161">First you need to create the Teams App manifest file, that you upload/sideload into Microsoft Teams.</span></span> <span data-ttu-id="4222c-162">这由 Gulp 任务完成 `gulp manifest` 。</span><span class="sxs-lookup"><span data-stu-id="4222c-162">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="4222c-163">这将验证清单，并创建目录中的 zip `./package` 文件。</span><span class="sxs-lookup"><span data-stu-id="4222c-163">This will validate the manifest and create a zip file in the `./package` directory.</span></span>

<span data-ttu-id="4222c-164">若要生成解决方案，请使用 `gulp build` 该命令。</span><span class="sxs-lookup"><span data-stu-id="4222c-164">To build your solution you use the `gulp build` command.</span></span> <span data-ttu-id="4222c-165">这会将解决方案转换为 `./dist` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="4222c-165">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="4222c-166">运行应用</span><span class="sxs-lookup"><span data-stu-id="4222c-166">Run your app</span></span>

<span data-ttu-id="4222c-167">若要运行应用，请使用 `gulp serve` 该命令。</span><span class="sxs-lookup"><span data-stu-id="4222c-167">To run your app you use the `gulp serve` command.</span></span> <span data-ttu-id="4222c-168">这将生成并启动本地 Web 服务器，供你测试你的应用。</span><span class="sxs-lookup"><span data-stu-id="4222c-168">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="4222c-169">每次在项目中保存文件时，该命令也将重新生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="4222c-169">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="4222c-170">现在应该可以浏览以确保 `http://localhost:3007/myFirstAppTab/` 选项卡正在呈现。</span><span class="sxs-lookup"><span data-stu-id="4222c-170">You should now be able to browse to `http://localhost:3007/myFirstAppTab/` to ensure that your tab is rendering.</span></span> <span data-ttu-id="4222c-171">但是，尚未在 Microsoft Teams 中。</span><span class="sxs-lookup"><span data-stu-id="4222c-171">However, not in Microsoft Teams yet.</span></span>

![在浏览器中查看网站](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="4222c-173">在 Microsoft Teams 中运行应用</span><span class="sxs-lookup"><span data-stu-id="4222c-173">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="4222c-174">Microsoft Teams 不允许你将应用托管在 localhost 上，因此你需要将其发布到公用 URL 或使用代理（如 ngrok）。</span><span class="sxs-lookup"><span data-stu-id="4222c-174">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span>

<span data-ttu-id="4222c-175">好消息是，基架项目具有此内置功能。</span><span class="sxs-lookup"><span data-stu-id="4222c-175">Good news is that the scaffolded project has this built-in.</span></span> <span data-ttu-id="4222c-176">运行 ngrok 服务时，将在后台启动具有唯一的公用 DNS 条目，并且它还会使用该唯一 URL 打包清单，然后执行与相同 `gulp ngrok-serve` 操作 `gulp serve` 。</span><span class="sxs-lookup"><span data-stu-id="4222c-176">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>

<span data-ttu-id="4222c-177">运行后，创建一个新的 Microsoft Teams 团队，当它创建时，单击团队名称，转到团队设置， `gulp ngrok-serve` 然后选择 *应用*。</span><span class="sxs-lookup"><span data-stu-id="4222c-177">After running `gulp ngrok-serve`, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*.</span></span> <span data-ttu-id="4222c-178">在右下角，你应该会看到一个链接"上传自定义应用"，选择它，然后浏览到项目文件夹和名为的子文件夹 `package` 。</span><span class="sxs-lookup"><span data-stu-id="4222c-178">In the lower right corner you should see a link *Upload a custom app*, select it and then browse to your project folder and the subfolder called `package`.</span></span> <span data-ttu-id="4222c-179">选择该文件夹中的 zip 文件，然后选择"打开"。</span><span class="sxs-lookup"><span data-stu-id="4222c-179">Select the zip file in that folder and choose open.</span></span> <span data-ttu-id="4222c-180">你的应用现在旁加载到 Microsoft Teams 中。</span><span class="sxs-lookup"><span data-stu-id="4222c-180">Your App is now sideloaded into Microsoft Teams.</span></span>

![旁加载的应用](~/assets/yeoman-images/teams-first-app-4.png)

<span data-ttu-id="4222c-182">返回到 *"常规"* 频道并选择 *+* 添加新的选项卡。你应该在选项卡列表中看到您的选项卡。</span><span class="sxs-lookup"><span data-stu-id="4222c-182">Go back to the *General* channel and select *+* to add a new Tab. You should see your tab in the list of tabs.</span></span>

![配置选项卡](~/assets/yeoman-images/teams-first-app-5.png)

<span data-ttu-id="4222c-184">选择您的选项卡并按照说明添加它。</span><span class="sxs-lookup"><span data-stu-id="4222c-184">Choose your tab and follow the instructions to add it.</span></span> <span data-ttu-id="4222c-185">请注意，有一个自定义配置对话框，您可以编辑源。</span><span class="sxs-lookup"><span data-stu-id="4222c-185">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="4222c-186">选择 *"* 保存"将选项卡添加到频道。</span><span class="sxs-lookup"><span data-stu-id="4222c-186">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="4222c-187">完成后，你的选项卡应在 Microsoft Teams 中加载！</span><span class="sxs-lookup"><span data-stu-id="4222c-187">Once done your tab should be loaded inside Microsoft Teams!</span></span>

![在团队中运行选项卡](~/assets/yeoman-images/teams-first-app-6.png)

<span data-ttu-id="4222c-189">**恭喜！你生成并部署了你的第一个 Microsoft Teams 应用**</span><span class="sxs-lookup"><span data-stu-id="4222c-189">**Congrats! You built and deployed your first Microsoft Teams app**</span></span>
