---
title: 入门 - 生成频道和组选项卡
author: heath-hamilton
description: 使用 Microsoft Teams Toolkit 快速创建 Microsoft Teams 频道和Toolkit。
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: 2ad0474859118f302a39e823f7669dc54061d525
ms.sourcegitcommit: 5687a901d48bcf2f5a3a086e0f703f854e8b9c21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2021
ms.locfileid: "49795452"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="5f1ee-103">为 Microsoft Teams 生成频道和组选项卡</span><span class="sxs-lookup"><span data-stu-id="5f1ee-103">Build a channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="5f1ee-104">在本教程中，你将生成基本频道 *选项卡 (也称为* 组选项卡 *) ，* 它是团队频道或聊天的全屏页面。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab*), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="5f1ee-105">与个人选项卡不同，用户可以配置此类选项卡的一些 (例如，重命名该选项卡，以便其通道) 。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="5f1ee-106">你的作业</span><span class="sxs-lookup"><span data-stu-id="5f1ee-106">Your assignment</span></span>

<span data-ttu-id="5f1ee-107">前不久，你的组织创建了一个 Teams 应用，该应用使用选项卡在技术支持、人力资源等 (显示重要的) 。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-107">Not long ago, your organization created a Teams app that uses a tab to display important contact information (help desk, HR, etc.).</span></span> <span data-ttu-id="5f1ee-108">但是，由于它是个人选项卡，因此每个用户必须安装该选项卡以查看它，并且采用率低于预期。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-108">However, since it's a personal tab, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="5f1ee-109">换句话说，太多工作人员仍不知道如何联系技术支持人员。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="5f1ee-110">通过生成频道选项卡，可以使此信息更易于查找，这将消除要求所有人安装应用的负担。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="5f1ee-111">相反，一个用户可以在频道中添加选项卡或聊天，以有利于整个组。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-111">Instead, one user can add the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="5f1ee-112">您将了解哪些知识</span><span class="sxs-lookup"><span data-stu-id="5f1ee-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="5f1ee-113">使用 Microsoft Teams Toolkit for Visual Studio Code 创建应用项目</span><span class="sxs-lookup"><span data-stu-id="5f1ee-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="5f1ee-114">确定一些与通道选项卡相关的应用配置和基架</span><span class="sxs-lookup"><span data-stu-id="5f1ee-114">Identify some of the app configurations and scaffolding relevant to channel tabs</span></span>
> * <span data-ttu-id="5f1ee-115">创建选项卡内容</span><span class="sxs-lookup"><span data-stu-id="5f1ee-115">Create tab content</span></span>
> * <span data-ttu-id="5f1ee-116">为选项卡的配置页创建内容</span><span class="sxs-lookup"><span data-stu-id="5f1ee-116">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="5f1ee-117">提供建议的选项卡名称</span><span class="sxs-lookup"><span data-stu-id="5f1ee-117">Provide a suggested tab name</span></span>
> * <span data-ttu-id="5f1ee-118">在本地生成和运行应用</span><span class="sxs-lookup"><span data-stu-id="5f1ee-118">Build and run your app locally</span></span>
> * <span data-ttu-id="5f1ee-119">在 Teams 中旁加载应用进行测试</span><span class="sxs-lookup"><span data-stu-id="5f1ee-119">Sideload your app in Teams for testing</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5f1ee-120">准备工作</span><span class="sxs-lookup"><span data-stu-id="5f1ee-120">Before you begin</span></span>

<span data-ttu-id="5f1ee-121">如果尚未安装，请确保了解并 [安装 Teams 开发先决条件](build-first-app-overview.md#get-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-121">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="5f1ee-122">1. 创建应用项目</span><span class="sxs-lookup"><span data-stu-id="5f1ee-122">1. Create your app project</span></span>

<span data-ttu-id="5f1ee-123">Microsoft Teams Toolkit帮助配置你的应用和设置与频道和组选项卡相关的基架，包括显示"Hello， World！" 的基本配置页面和内容页。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-123">The Microsoft Teams Toolkit helps configure your app and set up scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="5f1ee-124">消息。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-124">message.</span></span>

> [!TIP]
> <span data-ttu-id="5f1ee-125">如果你之前尚未创建 Teams 应用项目，你可能会发现按照这些说明更详细地解释项目非常有用[](../build-your-first-app/build-and-run.md)。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-125">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. 在Visual Studio代码中，选择左侧活动栏上的 **Microsoft Teams，** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 **"创建新的 Teams 应用"。**
1. <span data-ttu-id="5f1ee-127">当系统提示时，使用 Microsoft 365 开发帐户登录。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-127">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="5f1ee-128">在"**添加功能"屏幕上**，选择 **"Tab"，** 然后选择"**下一步"。**</span><span class="sxs-lookup"><span data-stu-id="5f1ee-128">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="5f1ee-129">输入 Teams 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-129">Enter a name for your Teams app.</span></span> <span data-ttu-id="5f1ee-130"> (这是应用的默认名称，也是本地计算机上应用项目目录的名称。) 选择组或 **Teams 频道选项卡**。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-130">(This is the default name for your app and also the name of the app project directory on your local machine.) Select **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="5f1ee-131">选择 **屏幕** 底部的"完成"以配置项目。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-131">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="5f1ee-132">2. 确定相关应用程序项目组件</span><span class="sxs-lookup"><span data-stu-id="5f1ee-132">2. Identify relevant app project components</span></span>

<span data-ttu-id="5f1ee-133">使用工具包创建项目时，会自动设置大部分应用配置和基架。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-133">Much of the app configurations and scaffolding are set up automatically when you create your project with the toolkit.</span></span> <span data-ttu-id="5f1ee-134">让我们看一下用于生成频道选项卡的主要组件。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-134">Let's look at the main components for building a channel tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="5f1ee-135">应用配置</span><span class="sxs-lookup"><span data-stu-id="5f1ee-135">App configurations</span></span>

<span data-ttu-id="5f1ee-136">在工具包中，转到 **App Studio** 以查看和更新应用配置。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-136">In the toolkit, go to **App Studio** to view and update your app configurations.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="5f1ee-137">应用基架</span><span class="sxs-lookup"><span data-stu-id="5f1ee-137">App scaffolding</span></span>

<span data-ttu-id="5f1ee-138">应用基架提供在 Teams 中呈现频道选项卡的组件。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-138">The app scaffolding provides the components for rendering your channel tab in Teams.</span></span> <span data-ttu-id="5f1ee-139">可以使用许多方法，但目前只需关注以下内容：</span><span class="sxs-lookup"><span data-stu-id="5f1ee-139">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="5f1ee-140">位于项目目录中的两 `src/components` 个文件：</span><span class="sxs-lookup"><span data-stu-id="5f1ee-140">Two files located in the `src/components` directory of your project:</span></span>
  * <span data-ttu-id="5f1ee-141">`Tab.js` 用于呈现选项卡的内容页。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-141">`Tab.js` for rendering your tab's content page.</span></span>
  * <span data-ttu-id="5f1ee-142">`TabConfig.js` 用于呈现选项卡的配置页。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-142">`TabConfig.js` for rendering your tab's configuration page.</span></span>
* <span data-ttu-id="5f1ee-143">Microsoft Teams JavaScript 客户端 SDK，预加载到项目的前端组件中。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-143">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="5f1ee-144">3. 自定义选项卡内容页</span><span class="sxs-lookup"><span data-stu-id="5f1ee-144">3. Customize your tab content page</span></span>

<span data-ttu-id="5f1ee-145">复制并更新以下代码段，并包含与您的组织有关的信息，或者出于时间考虑，按如下所示使用代码。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-145">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

```JSX
<div>
  <h1>Important Contacts</h1>
    <ul>
      <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
      <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
      <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
    </ul>
</div>
```

<span data-ttu-id="5f1ee-146">转到 `src/components` 目录并打开 `Tab.js` 。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-146">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="5f1ee-147">找到 `render()` 该函数，然后将内容粘贴到 `return()` (，如下所示) 。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-147">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

```JavaScript
render() {

    let userName = Object.keys(this.state.context).length > 0 ? this.state.context['upn'] : "";

    return (
    <div>
      <h1>Important Contacts</h1>
        <ul>
          <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
          <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
          <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
        </ul>
    </div>
    );
}
```

<span data-ttu-id="5f1ee-148">将以下规则 (也位于) 中，以便无论使用哪个主题，电子邮件链接都更易于 `App.css` `src/components` 阅读。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-148">Add the following rule to `App.css` (also located in `src/components`) so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="5f1ee-149">4. 自定义选项卡配置页</span><span class="sxs-lookup"><span data-stu-id="5f1ee-149">4. Customize your tab configuration page</span></span>

<span data-ttu-id="5f1ee-150">频道或聊天中的每个选项卡都有一个配置页，这是一个模式，具有至少一个设置选项，在用户添加你的应用时显示。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-150">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="5f1ee-151">默认情况下，配置页询问用户是否要在安装选项卡时通知频道或聊天。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-151">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="5f1ee-152">向配置页面添加一些自定义内容。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-152">Add some custom content to your configuration page.</span></span> <span data-ttu-id="5f1ee-153">转到项目的目录，打开并更新 (中的占位符内容，如下面的示例 `src/components` `TabConfig.js` `return()`) 。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-153">Go to your project's `src/components` directory, open `TabConfig.js`, and update the placeholder content inside `return()` (as shown in the following example).</span></span>

```JavaScript
return (
    <div>
      <h1>Add My Contoso Contacts</h1>
      <div>
        Select <b>Save</b> to add our organization's important contacts to this workspace.
      </div>
    </div>
);
```
 
> [!TIP]
> <span data-ttu-id="5f1ee-154">至少应在此页面上提供有关你的应用的一些简短信息，因为这可能是用户第一次了解它。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-154">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="5f1ee-155">还可以包括自定义配置选项或身份验证 [工作流](../tabs/how-to/authentication/auth-aad-sso.md)（在选项卡配置页面上很常见）。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-155">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-provide-a-suggested-tab-name"></a><span data-ttu-id="5f1ee-156">5. 提供建议的选项卡名称</span><span class="sxs-lookup"><span data-stu-id="5f1ee-156">5. Provide a suggested tab name</span></span>

<span data-ttu-id="5f1ee-157">添加通道选项卡时，默认情况下应用名称 (例如，第一 **个应用) 。**</span><span class="sxs-lookup"><span data-stu-id="5f1ee-157">When you add a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="5f1ee-158">这可能适合你调用你的应用，但你可能希望提供一个在组协作上下文中更有意义的名称 (例如，团队联系人) 。 </span><span class="sxs-lookup"><span data-stu-id="5f1ee-158">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

1. <span data-ttu-id="5f1ee-159">在 `TabConfig.js` 中，转到 `microsoftTeams.settings.setSettings` 。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-159">In `TabConfig.js`, go to `microsoftTeams.settings.setSettings`.</span></span>
2. <span data-ttu-id="5f1ee-160">使用 `suggestedDisplayName` 要默认显示的选项卡名称添加属性。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-160">Add the `suggestedDisplayName` property with the tab name you want to display by default.</span></span> 
3. <span data-ttu-id="5f1ee-161">使用以下示例中提供的名称或键入您的名称。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-161">Use the name provided in the following example or type your name.</span></span> <span data-ttu-id="5f1ee-162"> (默认情况下，用户可以更改 name.) </span><span class="sxs-lookup"><span data-stu-id="5f1ee-162">(By default, users can change the name.)</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="5f1ee-163">6. 生成并运行应用</span><span class="sxs-lookup"><span data-stu-id="5f1ee-163">6. Build and run your app</span></span>

<span data-ttu-id="5f1ee-164">为符合时间需要，你将在本地生成和运行应用。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-164">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="5f1ee-165"> (工具包 .) 中也提供了 `README` 此信息。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-165">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="5f1ee-166">在终端中，转到应用项目的根目录并运行 `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-166">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="5f1ee-167">运行 `npm start`。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-167">Run `npm start`.</span></span>

<span data-ttu-id="5f1ee-168">完成后，将成功 **进行编译！**</span><span class="sxs-lookup"><span data-stu-id="5f1ee-168">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="5f1ee-169">消息。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-169">message in the terminal.</span></span> <span data-ttu-id="5f1ee-170">你的应用正在运行 `https://localhost:3000` 。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-170">Your app is running on `https://localhost:3000`.</span></span>

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="5f1ee-171">7. 在 Teams 中旁加载应用</span><span class="sxs-lookup"><span data-stu-id="5f1ee-171">7. Sideload your app in Teams</span></span>

<span data-ttu-id="5f1ee-172">你的应用已准备好在 Teams 中进行测试。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-172">Your app is ready to test in Teams.</span></span> <span data-ttu-id="5f1ee-173">为此，你必须具有允许应用旁加载的帐户。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-173">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="5f1ee-174"> (如果不确定是否拥有，请了解如何获取 Teams 开发 [帐户](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).) </span><span class="sxs-lookup"><span data-stu-id="5f1ee-174">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

1. <span data-ttu-id="5f1ee-175">在Visual Studio中，按 **F5** 键启动 Teams Web 客户端。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-175">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="5f1ee-176">若要在 Teams 中显示你的应用内容，请指定你的应用在哪些 () `localhost` 可信赖：</span><span class="sxs-lookup"><span data-stu-id="5f1ee-176">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="5f1ee-177">默认情况下，在 Google Chrome 的相同浏览器窗口中打开 (新选项卡) 按 **F5** 后打开。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-177">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="5f1ee-178">转到 `https://localhost:3000/tab` 并转到页面。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-178">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="5f1ee-179">返回到 Teams。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-179">Go back to Teams.</span></span> <span data-ttu-id="5f1ee-180">在模式中，选择"添加到 **团队** "或"添加到 **聊天** "，并找到可用于测试的频道或聊天。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-180">In the modal, select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="5f1ee-181">选择 **"设置"选项卡**。配置页以模式显示。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-181">Select **Set up a tab**. The configuration page displays in a modal.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="频道选项卡配置页面的屏幕截图。":::
1. <span data-ttu-id="5f1ee-183">选择 **"保存** "以配置选项卡。显示内容页。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-183">Select **Save** to configure the tab. The content page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="具有静态内容视图的频道选项卡的屏幕截图。":::

## <a name="well-done"></a><span data-ttu-id="5f1ee-185">干的好</span><span class="sxs-lookup"><span data-stu-id="5f1ee-185">Well done</span></span>

<span data-ttu-id="5f1ee-186">恭喜！</span><span class="sxs-lookup"><span data-stu-id="5f1ee-186">Congratulations!</span></span> <span data-ttu-id="5f1ee-187">你有一个 Teams 应用，该应用具有一个选项卡，用于显示频道和聊天中的有用内容。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-187">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="5f1ee-188">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="5f1ee-188">Learn more</span></span>

* <span data-ttu-id="5f1ee-189">使用[SSO](../tabs/how-to/authentication/auth-aad-sso.md)对选项卡用户进行身份验证：如果仅希望授权用户查看您的选项卡，请通过 Azure Active Directory) AD (设置单一登录 (SSO) 。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-189">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="5f1ee-190">[嵌入现有 Web](../tabs/how-to/add-tab.md#tab-requirements)应用或网页中的内容：我们展示了如何为选项卡创建新内容，但您也可以从外部 URL 加载内容。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-190">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="5f1ee-191">[创建无缝选项卡体验](../tabs/design/tabs.md)：请参阅设计 Teams 选项卡的建议准则。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-191">[Create a seamless tab experience](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="5f1ee-192">[构建适用于移动设备的选项卡](../tabs/design/tabs-mobile.md)：了解如何开发适用于手机和平板电脑的选项卡。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-192">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="5f1ee-193">使用 Microsoft Graph API 利用 Teams 数据</span><span class="sxs-lookup"><span data-stu-id="5f1ee-193">Utilize Teams data with the Microsoft Graph API</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="5f1ee-194">创建不带工具包的选项卡</span><span class="sxs-lookup"><span data-stu-id="5f1ee-194">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="5f1ee-195">下一课程</span><span class="sxs-lookup"><span data-stu-id="5f1ee-195">Next lesson</span></span>

<span data-ttu-id="5f1ee-196">你知道如何生成用于协作的选项卡。</span><span class="sxs-lookup"><span data-stu-id="5f1ee-196">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="5f1ee-197">想要尝试生成不同类型的 Teams 应用？</span><span class="sxs-lookup"><span data-stu-id="5f1ee-197">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5f1ee-198">创建机器人</span><span class="sxs-lookup"><span data-stu-id="5f1ee-198">Build a bot</span></span>](../build-your-first-app/build-bot.md)
