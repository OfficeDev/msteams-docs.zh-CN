---
title: 教程 - 使用 Yeoman 生成器创建第一个应用
description: 了解如何开始使用 Yeoman Microsoft Teams生成应用。
keywords: nodejs yeoman node.js入门
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: a3519da1495dc51a811f4e95bc4ada9b11aa8292
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254332"
---
# <a name="build-your-first-microsoft-teams-app-using-the-yeoman-generator"></a><span data-ttu-id="e9d61-104">使用 Yeoman Microsoft Teams生成首个应用</span><span class="sxs-lookup"><span data-stu-id="e9d61-104">Build your first Microsoft Teams app using the Yeoman generator</span></span>

> [!Note]
> <span data-ttu-id="e9d61-105">本教程来自适用于 wiki[的 Yeoman Teams生成器](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。</span><span class="sxs-lookup"><span data-stu-id="e9d61-105">This tutorial comes from the [Yeoman generator for Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span>

<span data-ttu-id="e9d61-106">本教程介绍如何使用 Yeoman Microsoft Teams生成首个Microsoft Teams应用。</span><span class="sxs-lookup"><span data-stu-id="e9d61-106">In this tutorial, you will learn how to build your very first Microsoft Teams app using the Microsoft Teams Yeoman generator.</span></span> <span data-ttu-id="e9d61-107">它还指导你完成使用 Yeoman 生成器Teams升级应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="e9d61-107">It also walks you through the process of upgrading your Teams using the Yeoman generator.</span></span> <span data-ttu-id="e9d61-108">在开始之前，你必须拥有一个Teams[允许应用旁加载的帐户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="e9d61-108">Before you begin, you must have a Teams account that allows [app sideloading](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

![yeoman 生成器 git](~/assets/yeoman-demo.gif)

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="e9d61-110">获取先决条件</span><span class="sxs-lookup"><span data-stu-id="e9d61-110">Get Prerequisites</span></span>

<span data-ttu-id="e9d61-111">在开始使用 Yeoman 生成器之前，你需要在计算机上安装以下组件：</span><span class="sxs-lookup"><span data-stu-id="e9d61-111">You need to install the following on your machine before starting to use the Yeoman generator:</span></span>

* <span data-ttu-id="e9d61-112">Node.js</span><span class="sxs-lookup"><span data-stu-id="e9d61-112">Node.js</span></span>

   <span data-ttu-id="e9d61-113">你需要将Node.js计算机上安装。</span><span class="sxs-lookup"><span data-stu-id="e9d61-113">You need to have Node.js installed on your machine.</span></span> <span data-ttu-id="e9d61-114">你应该使用最新的 [LTS 版本](https://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="e9d61-114">You should use the latest [LTS version](https://nodejs.org).</span></span>

* <span data-ttu-id="e9d61-115">代码编辑器</span><span class="sxs-lookup"><span data-stu-id="e9d61-115">A code editor</span></span>

   <span data-ttu-id="e9d61-116">你需要一个代码编辑器。</span><span class="sxs-lookup"><span data-stu-id="e9d61-116">You need a code editor.</span></span> <span data-ttu-id="e9d61-117">本文档和图像中的大多数内容都指使用[Visual Studio Code。](https://code.visualstudio.com)</span><span class="sxs-lookup"><span data-stu-id="e9d61-117">Most of this documentation and images refer to using [Visual Studio Code](https://code.visualstudio.com).</span></span> <span data-ttu-id="e9d61-118">但是，您可以随意使用您喜欢的任何文本编辑器。</span><span class="sxs-lookup"><span data-stu-id="e9d61-118">However, feel free to use whatever text editor you prefer.</span></span>

* <span data-ttu-id="e9d61-119">Yeoman 和 Gulp CLI</span><span class="sxs-lookup"><span data-stu-id="e9d61-119">Yeoman and Gulp CLI</span></span>

   <span data-ttu-id="e9d61-120">若要使用生成器搭建项目基架，必须安装 Yeoman 工具和 Gulp CLI 任务管理器。</span><span class="sxs-lookup"><span data-stu-id="e9d61-120">To scaffold projects using the generator, you must install the Yeoman tool and Gulp CLI task manager.</span></span>

   <span data-ttu-id="e9d61-121">打开命令提示符并键入以下内容：</span><span class="sxs-lookup"><span data-stu-id="e9d61-121">Open up a command prompt and type the following:</span></span>

   ```bash
   npm install yo gulp-cli --global
   ```

## <a name="install-the-generator"></a><span data-ttu-id="e9d61-122">安装生成器</span><span class="sxs-lookup"><span data-stu-id="e9d61-122">Install the generator</span></span>

<span data-ttu-id="e9d61-123">使用Teams安装 Yeoman 生成器：</span><span class="sxs-lookup"><span data-stu-id="e9d61-123">Install the Teams Yeoman generator with the following command:</span></span>

```bash
npm init yo teams
```

<span data-ttu-id="e9d61-124">使用下列命令安装生成器的预览版本：</span><span class="sxs-lookup"><span data-stu-id="e9d61-124">Install the preview version of the generator with the following command:</span></span>

```bash
npm init yo teams@preview
```

## <a name="generate-your-project"></a><span data-ttu-id="e9d61-125">生成项目</span><span class="sxs-lookup"><span data-stu-id="e9d61-125">Generate your project</span></span>

<span data-ttu-id="e9d61-126">本节将指导你完成生成项目的步骤。</span><span class="sxs-lookup"><span data-stu-id="e9d61-126">This section walks you through the steps to generate your project.</span></span>

<span data-ttu-id="e9d61-127">**生成项目**</span><span class="sxs-lookup"><span data-stu-id="e9d61-127">**To generate your project**</span></span>

1. <span data-ttu-id="e9d61-128">打开命令提示符并创建要创建项目的新目录。</span><span class="sxs-lookup"><span data-stu-id="e9d61-128">Open a command prompt and create a new directory where you want to create your project.</span></span>
1. <span data-ttu-id="e9d61-129">转到 目录，然后运行命令 `yo teams` 。</span><span class="sxs-lookup"><span data-stu-id="e9d61-129">Go to the directory, and run the command `yo teams`.</span></span> <span data-ttu-id="e9d61-130">生成器启动。</span><span class="sxs-lookup"><span data-stu-id="e9d61-130">The generator starts.</span></span>
1. <span data-ttu-id="e9d61-131">响应生成器提示的一组问题：</span><span class="sxs-lookup"><span data-stu-id="e9d61-131">Respond to the set of questions prompted by the generator:</span></span>

   ![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

   1. <span data-ttu-id="e9d61-133">输入项目的名称。</span><span class="sxs-lookup"><span data-stu-id="e9d61-133">Enter a name for your project.</span></span> <span data-ttu-id="e9d61-134">按 Enter 可保持其为 。</span><span class="sxs-lookup"><span data-stu-id="e9d61-134">You can leave it as is by pressing Enter.</span></span>
   1. <span data-ttu-id="e9d61-135">如果要创建新目录，请输入新目录的路径。</span><span class="sxs-lookup"><span data-stu-id="e9d61-135">Enter a path for the new directory if you want to create a new directory.</span></span> <span data-ttu-id="e9d61-136">由于你已进入你需要的目录中，只需按 Enter。</span><span class="sxs-lookup"><span data-stu-id="e9d61-136">As you are already in the directory you want, just press Enter.</span></span>
   1. <span data-ttu-id="e9d61-137">输入项目的标题。</span><span class="sxs-lookup"><span data-stu-id="e9d61-137">Enter the title of your project.</span></span> <span data-ttu-id="e9d61-138">此标题将在应用的清单和说明中使用。</span><span class="sxs-lookup"><span data-stu-id="e9d61-138">This title will be used in the manifest and description of your app.</span></span> 
   1. <span data-ttu-id="e9d61-139">输入还将在清单中使用的公司名称。</span><span class="sxs-lookup"><span data-stu-id="e9d61-139">Enter a company name which also will be used in the manifest.</span></span>
   1. <span data-ttu-id="e9d61-140">输入想要使用的清单版本。</span><span class="sxs-lookup"><span data-stu-id="e9d61-140">Enter the version of the manifest you want to use.</span></span> <span data-ttu-id="e9d61-141">对于本教程，请选择 `v1.5` ，这是当前可用的常规架构。</span><span class="sxs-lookup"><span data-stu-id="e9d61-141">For this tutorial select `v1.5`, which is the current general available schema.</span></span>
   1. <span data-ttu-id="e9d61-142">选择要添加到项目中的项目。</span><span class="sxs-lookup"><span data-stu-id="e9d61-142">Select the items you want to add to your project.</span></span> <span data-ttu-id="e9d61-143">可以选择单个项目或任意项目组合。</span><span class="sxs-lookup"><span data-stu-id="e9d61-143">You can select a single one or any combination of items.</span></span> <span data-ttu-id="e9d61-144">对于本教程，只需选择 *一个选项卡*：</span><span class="sxs-lookup"><span data-stu-id="e9d61-144">For this tutorials, just select *a Tab*:</span></span>

    ![项目选择](~/assets/yeoman-images/teams-first-app-2.png)

1. <span data-ttu-id="e9d61-146">响应根据在步骤 2 中选定的项目出现的下一组后续问题。</span><span class="sxs-lookup"><span data-stu-id="e9d61-146">Respond to the next set of follow-up questions that appear based on the items you selected in Step 2.</span></span>
1. <span data-ttu-id="e9d61-147">输入解决方案的托管位置的 URL。</span><span class="sxs-lookup"><span data-stu-id="e9d61-147">Enter a URL for the location where you will host your solution.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="e9d61-148">该 URL 可以是任何 URL，但默认情况下，生成器建议 Azure 网站 URL。</span><span class="sxs-lookup"><span data-stu-id="e9d61-148">The URL can be any URL, but by default the generator suggests an Azure web site URL.</span></span>

1. <span data-ttu-id="e9d61-149">确认是否要包含解决方案的单元测试。</span><span class="sxs-lookup"><span data-stu-id="e9d61-149">Confirm if you want to include unit-testing for your solution.</span></span> <span data-ttu-id="e9d61-150">默认响应为 **"是"。**</span><span class="sxs-lookup"><span data-stu-id="e9d61-150">The default response is **Yes**.</span></span> <span data-ttu-id="e9d61-151">如果选择包括单元测试，则生成的项目将具有单元测试框架和一些针对基架的不同项目的默认单元测试。</span><span class="sxs-lookup"><span data-stu-id="e9d61-151">If you opt to include unit-testing, the generated project will have a unit testing framework and some default unit tests for the different items being scaffolded.</span></span> 
   > [!NOTE]
   > * <span data-ttu-id="e9d61-152">对于本教程，选择不包括测试框架。</span><span class="sxs-lookup"><span data-stu-id="e9d61-152">For this tutorial choose not to include a test framework.</span></span>
   > * <span data-ttu-id="e9d61-153">生成器具有许多内置高级功能，你可以选择加入或选择退出。</span><span class="sxs-lookup"><span data-stu-id="e9d61-153">The generator has a lot of built-in advanced features that you can opt-in or opt-out of.</span></span>

1. <span data-ttu-id="e9d61-154">为了便于你登录，还将询问你是否要使用 Azure 应用程序Insights登录。</span><span class="sxs-lookup"><span data-stu-id="e9d61-154">In order to make signing-in easy for you, you will also be asked if you want to use Azure Application Insights for signing-in.</span></span> <span data-ttu-id="e9d61-155">如果选择"**是"，** 则需要提供 Azure 应用程序Insights密钥。</span><span class="sxs-lookup"><span data-stu-id="e9d61-155">If you select **Yes**, you will need to provide an Azure Application Insights key.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="e9d61-156">对于本教程，选择退出使用应用程序Insights。</span><span class="sxs-lookup"><span data-stu-id="e9d61-156">For this tutorial opt-out of using Application Insights.</span></span>

   <span data-ttu-id="e9d61-157">下一组问题将基于之前选定的项目。</span><span class="sxs-lookup"><span data-stu-id="e9d61-157">The next set of questions will be based on the previously selected items.</span></span> <span data-ttu-id="e9d61-158">对于选项卡，你只需提供一个名称，并可以选择是否希望能够使用此应用作为 SharePoint Online Web 部件。</span><span class="sxs-lookup"><span data-stu-id="e9d61-158">For a tab you only need to provide a name and optionally choose if you want to be able to use this app as a SharePoint Online web part.</span></span> <span data-ttu-id="e9d61-159">提供名称后，生成器将生成项目并安装所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="e9d61-159">After you provide the name the generator will generate the project and install all dependencies.</span></span> <span data-ttu-id="e9d61-160">这可能需要一两分钟的时间。</span><span class="sxs-lookup"><span data-stu-id="e9d61-160">This will take a minute or two.</span></span>

## <a name="add-code-to-your-tab"></a><span data-ttu-id="e9d61-161">将代码添加到选项卡</span><span class="sxs-lookup"><span data-stu-id="e9d61-161">Add code to your tab</span></span>

<span data-ttu-id="e9d61-162">生成器完成后，可以在最喜爱的代码编辑器中打开解决方案。</span><span class="sxs-lookup"><span data-stu-id="e9d61-162">After the generator is done you can open up the solution in your favorite code editor.</span></span> <span data-ttu-id="e9d61-163">请花一两分钟的时间，熟悉代码的整理方式。</span><span class="sxs-lookup"><span data-stu-id="e9d61-163">Take a minute or two and familiarize yourself with how the code is organized.</span></span> <span data-ttu-id="e9d61-164">有关详细信息，请参阅Project[结构](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)文档。</span><span class="sxs-lookup"><span data-stu-id="e9d61-164">For more information, see [Project Structure](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) documentation.</span></span>

<span data-ttu-id="e9d61-165">您的选项卡位于 `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` 文件中。</span><span class="sxs-lookup"><span data-stu-id="e9d61-165">Your tab is in the `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` file.</span></span> <span data-ttu-id="e9d61-166">这是选项卡React TypeScript 类。</span><span class="sxs-lookup"><span data-stu-id="e9d61-166">This is the TypeScript React-based class for your tab.</span></span> 

1. <span data-ttu-id="e9d61-167">找到 `render()` 方法，在控件中添加一 `<PanelBody>` 行代码，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e9d61-167">Locate the `render()` method and add a line of code inside the `<PanelBody>` control so it looks like this:</span></span>

   ``` TypeScript
   <PanelBody>
      <div style={styles.section}>
      Hello World! Yo Teams rocks!
      </div>
   </PanelBody>
   ```
1. <span data-ttu-id="e9d61-168">保存文件并返回到命令提示符。</span><span class="sxs-lookup"><span data-stu-id="e9d61-168">Save the file and return to the command prompt.</span></span>

## <a name="build-your-app"></a><span data-ttu-id="e9d61-169">生成应用程序</span><span class="sxs-lookup"><span data-stu-id="e9d61-169">Build your app</span></span>

<span data-ttu-id="e9d61-170">现在可以生成项目。</span><span class="sxs-lookup"><span data-stu-id="e9d61-170">You can now build your project.</span></span> <span data-ttu-id="e9d61-171">此操作分两步完成。</span><span class="sxs-lookup"><span data-stu-id="e9d61-171">This is done in two steps.</span></span>

1. <span data-ttu-id="e9d61-172">为Teams应用创建应用清单Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="e9d61-172">Create the Teams App manifest file for the app that you uploaded into Microsoft Teams.</span></span> <span data-ttu-id="e9d61-173">这由 Gulp 任务完成 `gulp manifest` 。</span><span class="sxs-lookup"><span data-stu-id="e9d61-173">This is done by the Gulp task `gulp manifest`.</span></span> <span data-ttu-id="e9d61-174">这将验证清单，并创建目录中的 zip `./package` 文件。</span><span class="sxs-lookup"><span data-stu-id="e9d61-174">This will validate the manifest and create a zip file in the `./package` directory.</span></span>
1. <span data-ttu-id="e9d61-175">运行 `gulp build` 命令以生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="e9d61-175">Run the `gulp build` command to build the solution.</span></span> <span data-ttu-id="e9d61-176">这会将解决方案转换为 `./dist` 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e9d61-176">This will transpile your solution into the `./dist` folder.</span></span> 

## <a name="run-your-app"></a><span data-ttu-id="e9d61-177">运行应用</span><span class="sxs-lookup"><span data-stu-id="e9d61-177">Run your app</span></span>

<span data-ttu-id="e9d61-178">若要运行应用，请使用 `gulp serve` 命令。</span><span class="sxs-lookup"><span data-stu-id="e9d61-178">To run your app, use the `gulp serve` command.</span></span> <span data-ttu-id="e9d61-179">这将生成并启动本地 Web 服务器，以测试你的应用。</span><span class="sxs-lookup"><span data-stu-id="e9d61-179">This will build and start a local web server for you to test your app.</span></span> <span data-ttu-id="e9d61-180">每次在项目中保存文件时，该命令也将重新生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="e9d61-180">The command will also rebuild the application whenever you save a file in your project.</span></span> 

<span data-ttu-id="e9d61-181">现在应转到 ， `http://localhost:3007/myFirstAppTab/` 并确保选项卡正在呈现。</span><span class="sxs-lookup"><span data-stu-id="e9d61-181">You should now be go to `http://localhost:3007/myFirstAppTab/` and ensure that your tab is rendering.</span></span> <span data-ttu-id="e9d61-182">但是，它尚未Microsoft Teams中。</span><span class="sxs-lookup"><span data-stu-id="e9d61-182">However, it is not in Microsoft Teams yet.</span></span> 

<span data-ttu-id="e9d61-183">**在页面呈现选项卡Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="e9d61-183">**To render your tab in Microsoft Teams**</span></span>

![在浏览器中查看网站](~/assets/yeoman-images/teams-first-app-3.png)

### <a name="run-your-app-in-microsoft-teams"></a><span data-ttu-id="e9d61-185">在应用商店中Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e9d61-185">Run your app in Microsoft Teams</span></span>

<span data-ttu-id="e9d61-186">Microsoft Teams不允许将应用托管在 localhost 上，因此你需要将其发布到公用 URL 或使用代理（如 ngrok）。</span><span class="sxs-lookup"><span data-stu-id="e9d61-186">Microsoft Teams does not allow you to have your app hosted on localhost, so you need to either publish it to a public URL or use a proxy such as ngrok.</span></span> <span data-ttu-id="e9d61-187">好消息是，搭建的项目具有此内置功能。</span><span class="sxs-lookup"><span data-stu-id="e9d61-187">Good news is that the scaffolded project has this built-in.</span></span> 

<span data-ttu-id="e9d61-188">**若要在应用商店中运行Teams**</span><span class="sxs-lookup"><span data-stu-id="e9d61-188">**To run your app in Teams**</span></span>

1. <span data-ttu-id="e9d61-189">在 `gulp ngrok-serve` 终端中运行。</span><span class="sxs-lookup"><span data-stu-id="e9d61-189">Run `gulp ngrok-serve` in Terminal.</span></span> <span data-ttu-id="e9d61-190">运行 ngrok 服务时，将在后台启动具有唯一的公用 DNS 条目，并且它还将清单打包为此唯一 URL，然后执行与 完全相同 `gulp ngrok-serve` 的操作 `gulp serve` 。</span><span class="sxs-lookup"><span data-stu-id="e9d61-190">When you run `gulp ngrok-serve` the ngrok service will be started in the background, with a unique and public DNS entry and it will also package the manifest with that unique URL and then do the exact same thing as `gulp serve`.</span></span>
1. <span data-ttu-id="e9d61-191">创建新的团队Microsoft Teams团队。</span><span class="sxs-lookup"><span data-stu-id="e9d61-191">Create a new Microsoft Teams team.</span></span>
1. <span data-ttu-id="e9d61-192">Select the Team name > Teams 设置 > Apps.</span><span class="sxs-lookup"><span data-stu-id="e9d61-192">Select the Team name > Teams Settings > Apps.</span></span>
1. <span data-ttu-id="e9d61-193">从右下角，选择 **"Upload应用"。**</span><span class="sxs-lookup"><span data-stu-id="e9d61-193">From the lower right corner, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="e9d61-194">转到项目 `package` 文件夹下的文件夹。</span><span class="sxs-lookup"><span data-stu-id="e9d61-194">Go to the `package` folder under your project folder.</span></span> 
1. <span data-ttu-id="e9d61-195">选择该文件夹中的 zip 文件，然后选择"打开"。</span><span class="sxs-lookup"><span data-stu-id="e9d61-195">Select the zip file in that folder and select open.</span></span> 
   <span data-ttu-id="e9d61-196">你的应用现在旁加载到Microsoft Teams：</span><span class="sxs-lookup"><span data-stu-id="e9d61-196">Your App is now sideloaded into Microsoft Teams:</span></span>

   ![旁加载的应用](~/assets/yeoman-images/teams-first-app-4.png)
1. <span data-ttu-id="e9d61-198">返回到 **常规频道，** 然后选择 **+** 添加新的选项卡。你应该在选项卡列表中看到您的选项卡： ![ 配置选项卡](~/assets/yeoman-images/teams-first-app-5.png)</span><span class="sxs-lookup"><span data-stu-id="e9d61-198">Go back to the **General** channel and select **+** to add a new Tab. You should see your tab in the list of tabs: ![configure tab](~/assets/yeoman-images/teams-first-app-5.png)</span></span>
1. <span data-ttu-id="e9d61-199">选择您的选项卡，然后按照说明添加它。</span><span class="sxs-lookup"><span data-stu-id="e9d61-199">Select your tab and follow the instructions to add it.</span></span> <span data-ttu-id="e9d61-200">请注意，有一个自定义配置对话框，您可以编辑其源。</span><span class="sxs-lookup"><span data-stu-id="e9d61-200">Notice that you have a custom configuration dialog, for which you can edit the source.</span></span> <span data-ttu-id="e9d61-201">选择 *"保存* "将选项卡添加到频道。</span><span class="sxs-lookup"><span data-stu-id="e9d61-201">Select *Save* to add your tab to the channel.</span></span> <span data-ttu-id="e9d61-202">现在选项卡已加载到 Microsoft Teams！</span><span class="sxs-lookup"><span data-stu-id="e9d61-202">Your tab is now loaded inside Microsoft Teams!</span></span>

   ![teams 中的"运行"选项卡](~/assets/yeoman-images/teams-first-app-6.png)

### <a name="upgrade-microsoft-teams"></a><span data-ttu-id="e9d61-204">升级Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e9d61-204">Upgrade Microsoft Teams</span></span>

<span data-ttu-id="e9d61-205">还可使用 Yeoman Microsoft Teams将当前 Microsoft Teams 版本升级到最新版本。</span><span class="sxs-lookup"><span data-stu-id="e9d61-205">You can also upgrade your current Microsoft Teams version to the latest version using the Microsoft Teams Yeoman generator.</span></span>

<span data-ttu-id="e9d61-206">**升级Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="e9d61-206">**To upgrade Microsoft Teams**</span></span>

1. <span data-ttu-id="e9d61-207">通过以下命令Teams获取当前版本的版本：</span><span class="sxs-lookup"><span data-stu-id="e9d61-207">Get current version of Teams with the following command:</span></span>

   ```PowerShell
    yo teams --version
   ```
2. <span data-ttu-id="e9d61-208">使用以下命令选择和更新生成器：</span><span class="sxs-lookup"><span data-stu-id="e9d61-208">Use the following command to select and update your generator:</span></span>

   ```PowerShell
    yo
   ```
3. <span data-ttu-id="e9d61-209">使用箭头键选择更新 **生成器**：</span><span class="sxs-lookup"><span data-stu-id="e9d61-209">Use the  arrow keys to select **Update your Generators**:</span></span>

   ![YoSelectUpdatGen 的图像](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. <span data-ttu-id="e9d61-211">从生成器列表中选择你需要的生成器：</span><span class="sxs-lookup"><span data-stu-id="e9d61-211">Select the generator you want from the list of generators:</span></span>
   > [!NOTE]
   > <span data-ttu-id="e9d61-212">使用空格键从可用选项Teams或清除所选版本。</span><span class="sxs-lookup"><span data-stu-id="e9d61-212">Use the space bar to select or clear a selected Teams version from the available options.</span></span>

    ![UseSpaceToSelectGenerators 的图像](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > <span data-ttu-id="e9d61-214">完成安装需要几秒钟到Teams分钟。</span><span class="sxs-lookup"><span data-stu-id="e9d61-214">It takes few seconds to minutes for Teams installation to complete.</span></span>

5. <span data-ttu-id="e9d61-215">安装完成后，使用以下命令检查安装的版本：</span><span class="sxs-lookup"><span data-stu-id="e9d61-215">After the installation is complete, use the following command to check the installed version:</span></span>

   ```PowerShell
    yo teams --version
   ```
   <span data-ttu-id="e9d61-216">恭喜！</span><span class="sxs-lookup"><span data-stu-id="e9d61-216">Congrats!</span></span> <span data-ttu-id="e9d61-217">生成并部署了第一个Microsoft Teams应用。</span><span class="sxs-lookup"><span data-stu-id="e9d61-217">You built and deployed your first Microsoft Teams app.</span></span> <span data-ttu-id="e9d61-218">你还升级了Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="e9d61-218">You also upgraded Microsoft Teams.</span></span>

 ## <a name="see-also"></a><span data-ttu-id="e9d61-219">另请参阅</span><span class="sxs-lookup"><span data-stu-id="e9d61-219">See also</span></span>

* [<span data-ttu-id="e9d61-220">教程概述</span><span class="sxs-lookup"><span data-stu-id="e9d61-220">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="e9d61-221">创建对话机器人应用</span><span class="sxs-lookup"><span data-stu-id="e9d61-221">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="e9d61-222">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="e9d61-222">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="e9d61-223">代码示例</span><span class="sxs-lookup"><span data-stu-id="e9d61-223">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)