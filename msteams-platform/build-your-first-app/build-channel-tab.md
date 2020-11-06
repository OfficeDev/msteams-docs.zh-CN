---
title: 入门-构建通道和组选项卡
author: heath-hamilton
description: 使用 Microsoft 团队工具包快速创建 Microsoft 团队频道和分组选项卡。
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: 46b5410a1ae7c866f8998362765dfe5462df94cb
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931762"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="c927b-103">为 Microsoft 团队构建通道和组选项卡</span><span class="sxs-lookup"><span data-stu-id="c927b-103">Build a channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="c927b-104">在本教程中，你将构建基本的 *频道选项卡* (也称为 " *组" 选项* 卡) （它是团队频道或聊天的全屏页面）。</span><span class="sxs-lookup"><span data-stu-id="c927b-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab* ), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="c927b-105">与 "个人" 选项卡不同，用户可以配置此类选项卡的某些方面 (例如，重命名选项卡，使其对频道) 有意义。</span><span class="sxs-lookup"><span data-stu-id="c927b-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="c927b-106">您的分配</span><span class="sxs-lookup"><span data-stu-id="c927b-106">Your assignment</span></span>

<span data-ttu-id="c927b-107">以前，您的组织创建了一个团队应用程序，该应用程序使用选项卡来显示重要的联系人信息， (技术支持、人力资源等 ) 。</span><span class="sxs-lookup"><span data-stu-id="c927b-107">Not long ago, your organization created a Teams app that uses a tab to display important contact information (help desk, HR, etc.).</span></span> <span data-ttu-id="c927b-108">但是，由于它是一个 "个人" 选项卡，因此每个用户都必须安装该选项卡，才能看到它，并且采用情况低于预期。</span><span class="sxs-lookup"><span data-stu-id="c927b-108">However, since it's a personal tab, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="c927b-109">换句话说，工作线程太多仍不知道如何联系技术支持人员。</span><span class="sxs-lookup"><span data-stu-id="c927b-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="c927b-110">您可以通过构建通道选项卡使此信息更易于查找，这将消除要求每个人安装应用程序的负担。</span><span class="sxs-lookup"><span data-stu-id="c927b-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="c927b-111">相反，一个用户可以在频道或聊天中添加该选项卡，以了解整个组的好处。</span><span class="sxs-lookup"><span data-stu-id="c927b-111">Instead, one user can add the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="c927b-112">你将了解的内容</span><span class="sxs-lookup"><span data-stu-id="c927b-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="c927b-113">使用 Microsoft 团队工具包创建适用于 Visual Studio Code 的应用程序项目</span><span class="sxs-lookup"><span data-stu-id="c927b-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="c927b-114">确定与频道和组选项卡相关的一些应用配置和基架</span><span class="sxs-lookup"><span data-stu-id="c927b-114">Identify some of the app configurations and scaffolding relevant to channel and group tabs</span></span>
> * <span data-ttu-id="c927b-115">创建选项卡内容</span><span class="sxs-lookup"><span data-stu-id="c927b-115">Create tab content</span></span>
> * <span data-ttu-id="c927b-116">创建选项卡的配置页的内容</span><span class="sxs-lookup"><span data-stu-id="c927b-116">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="c927b-117">提供建议的选项卡名称</span><span class="sxs-lookup"><span data-stu-id="c927b-117">Provide a suggested tab name</span></span>
> * <span data-ttu-id="c927b-118">在本地生成和运行应用程序</span><span class="sxs-lookup"><span data-stu-id="c927b-118">Build and run your app locally</span></span>
> * <span data-ttu-id="c927b-119">在团队中旁加载您的应用程序以供测试</span><span class="sxs-lookup"><span data-stu-id="c927b-119">Sideload your app in Teams for testing</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c927b-120">准备工作</span><span class="sxs-lookup"><span data-stu-id="c927b-120">Before you begin</span></span>

<span data-ttu-id="c927b-121">如果还没有，请确保 [了解并安装团队开发先决条件](build-first-app-overview.md#get-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="c927b-121">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="c927b-122">1. 创建您的应用程序项目</span><span class="sxs-lookup"><span data-stu-id="c927b-122">1. Create your app project</span></span>

<span data-ttu-id="c927b-123">Microsoft 团队工具包可帮助配置您的应用程序，并设置与通道和组选项卡相关的基架，包括显示 "Hello，World！" 的基本配置页和内容页。</span><span class="sxs-lookup"><span data-stu-id="c927b-123">The Microsoft Teams Toolkit helps configure your app and set up scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="c927b-124">消息。</span><span class="sxs-lookup"><span data-stu-id="c927b-124">message.</span></span>

> [!TIP]
> <span data-ttu-id="c927b-125">如果之前尚未创建团队应用程序项目，您可能会发现，请按照 [以下说明](../build-your-first-app/build-and-run.md) 更详细地说明项目。</span><span class="sxs-lookup"><span data-stu-id="c927b-125">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队** "， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **创建新的团队应用** "。
1. <span data-ttu-id="c927b-127">出现提示时，使用 Microsoft 365 开发帐户登录。</span><span class="sxs-lookup"><span data-stu-id="c927b-127">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="c927b-128">在 " **添加功能** " 屏幕上，依次选择 **"** **下一步** "。</span><span class="sxs-lookup"><span data-stu-id="c927b-128">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="c927b-129">为你的团队应用输入名称。</span><span class="sxs-lookup"><span data-stu-id="c927b-129">Enter a name for your Teams app.</span></span> <span data-ttu-id="c927b-130"> (这是您的应用程序的默认名称，也是本地计算机上的应用程序项目目录的名称。 ) </span><span class="sxs-lookup"><span data-stu-id="c927b-130">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="c927b-131">检查 " **个人" 选项卡** 和 **"组" 或 "工作组通道" 选项卡** 选项。</span><span class="sxs-lookup"><span data-stu-id="c927b-131">Check the **Personal tab** and **Group or Teams channel tab** options.</span></span> <span data-ttu-id="c927b-132"> (你将很快了解为什么需要两种类型的选项卡。 ) </span><span class="sxs-lookup"><span data-stu-id="c927b-132">(You'll soon learn why you need both types of tabs.)</span></span>
1. <span data-ttu-id="c927b-133">选择屏幕底部的 " **完成** " 以配置项目。</span><span class="sxs-lookup"><span data-stu-id="c927b-133">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="c927b-134">2. 确定相关的应用程序项目组件</span><span class="sxs-lookup"><span data-stu-id="c927b-134">2. Identify relevant app project components</span></span>

<span data-ttu-id="c927b-135">大部分应用配置和基架是在使用团队工具包创建项目时自动设置的。</span><span class="sxs-lookup"><span data-stu-id="c927b-135">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="c927b-136">我们来看看构建通道和组选项卡的主要组件。</span><span class="sxs-lookup"><span data-stu-id="c927b-136">Let's look at the main components for building a channel and group tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="c927b-137">应用配置</span><span class="sxs-lookup"><span data-stu-id="c927b-137">App configurations</span></span>

<span data-ttu-id="c927b-138">您可以使用包含在工具包中的应用程序 Studio 查看和更新应用程序配置。</span><span class="sxs-lookup"><span data-stu-id="c927b-138">You can view and update your app configurations using App Studio, which is included in the toolkit.</span></span>

<span data-ttu-id="c927b-139">在安装过程中，该工具包最初配置了通道和组选项卡的两个基本组件：</span><span class="sxs-lookup"><span data-stu-id="c927b-139">During setup, the toolkit initially configured two essential components of channel and group tabs:</span></span>

* <span data-ttu-id="c927b-140">**配置页面** ：用于将选项卡添加到频道或聊天的对话框。</span><span class="sxs-lookup"><span data-stu-id="c927b-140">**Configuration page** : The dialog for adding a tab to a channel or chat.</span></span> <span data-ttu-id="c927b-141"> (在应用程序 Studio 中，通过转到 **"团队" 选项卡 > "团队" 选项卡** ，可以找到此页面。 ) </span><span class="sxs-lookup"><span data-stu-id="c927b-141">(In App Studio, you can find this page by going to **Tabs > Team tab**.)</span></span>
* <span data-ttu-id="c927b-142">**内容页面** ：显示主要内容的位置。</span><span class="sxs-lookup"><span data-stu-id="c927b-142">**Content page** : Where you display your primary content.</span></span> <span data-ttu-id="c927b-143"> (在应用程序 Studio 中，通过转到 " **添加个人" 选项卡 > 的选项** 卡可以找到此页面。 ) </span><span class="sxs-lookup"><span data-stu-id="c927b-143">(In App Studio, you can find this page by going to **Tabs > Add a personal tab**.)</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="c927b-144">应用程序基架</span><span class="sxs-lookup"><span data-stu-id="c927b-144">App scaffolding</span></span>

<span data-ttu-id="c927b-145">应用程序基架提供用于在团队中呈现个人选项卡的组件。</span><span class="sxs-lookup"><span data-stu-id="c927b-145">The app scaffolding provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="c927b-146">你可以使用很多，但现在你只需关注以下内容：</span><span class="sxs-lookup"><span data-stu-id="c927b-146">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="c927b-147">位于项目目录中的两个文件 `src/components` ：</span><span class="sxs-lookup"><span data-stu-id="c927b-147">Two files located in the `src/components` directory of your project:</span></span>
  * <span data-ttu-id="c927b-148">`Tab.js` 用于呈现选项卡的内容页。</span><span class="sxs-lookup"><span data-stu-id="c927b-148">`Tab.js` for rendering your tab's content page.</span></span>
  * <span data-ttu-id="c927b-149">`TabConfig.js` 用于呈现选项卡的配置页。</span><span class="sxs-lookup"><span data-stu-id="c927b-149">`TabConfig.js` for rendering your tab's configuration page.</span></span>
* <span data-ttu-id="c927b-150">Microsoft 团队 JavaScript 客户端 SDK，它在项目的前端组件中预加载。</span><span class="sxs-lookup"><span data-stu-id="c927b-150">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="c927b-151">3. 自定义 "选项卡内容" 页</span><span class="sxs-lookup"><span data-stu-id="c927b-151">3. Customize your tab content page</span></span>

<span data-ttu-id="c927b-152">使用与您的组织相关的信息复制和更新以下代码段，如果有时间，请使用代码。</span><span class="sxs-lookup"><span data-stu-id="c927b-152">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="c927b-153">转到 `src/components` 目录并打开 `Tab.js` 。</span><span class="sxs-lookup"><span data-stu-id="c927b-153">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="c927b-154">找到 `render()` 函数并将内容粘贴 (中， `return()` 如) 所示。</span><span class="sxs-lookup"><span data-stu-id="c927b-154">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="c927b-155">将以下规则添加到 `App.css` (也位于 `src/components`) 中，这样无论使用哪个主题，电子邮件链接都更易于阅读。</span><span class="sxs-lookup"><span data-stu-id="c927b-155">Add the following rule to `App.css` (also located in `src/components`) so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="c927b-156">4. 自定义您的选项卡配置页</span><span class="sxs-lookup"><span data-stu-id="c927b-156">4. Customize your tab configuration page</span></span>

<span data-ttu-id="c927b-157">频道或聊天中的每个选项卡都有一个配置页面，其中包含至少一个安装选项的对话框，在用户添加您的应用程序时显示。</span><span class="sxs-lookup"><span data-stu-id="c927b-157">Every tab in a channel or chat has a configuration page, a dialog with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="c927b-158">默认情况下，配置页面会询问用户是否要在安装该选项卡时通知频道或聊天。</span><span class="sxs-lookup"><span data-stu-id="c927b-158">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="c927b-159">将一些自定义内容添加到配置页面。</span><span class="sxs-lookup"><span data-stu-id="c927b-159">Add some custom content to your configuration page.</span></span> <span data-ttu-id="c927b-160">转到项目的 `src/components` 目录，打开 `TabConfig.js` ，并更新中的占位符内容 (中， `return()` 如下面的示例所示) 。</span><span class="sxs-lookup"><span data-stu-id="c927b-160">Go to your project's `src/components` directory, open `TabConfig.js`, and update the placeholder content inside `return()` (as shown in the following example).</span></span>

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
> <span data-ttu-id="c927b-161">至少，在此页面上提供有关您的应用程序的一些简要信息，因为这可能是用户首次了解它。</span><span class="sxs-lookup"><span data-stu-id="c927b-161">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="c927b-162">您还可以包括自定义配置选项或 [身份验证工作流](../tabs/how-to/authentication/auth-aad-sso.md)，这在选项卡配置页上很常见。</span><span class="sxs-lookup"><span data-stu-id="c927b-162">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-provide-a-suggested-tab-name"></a><span data-ttu-id="c927b-163">5. 提供建议的选项卡名称</span><span class="sxs-lookup"><span data-stu-id="c927b-163">5. Provide a suggested tab name</span></span>

<span data-ttu-id="c927b-164">在添加频道或组选项卡时，默认情况下，应用名称会显示 (例如， **第一个应用程序** ) 。</span><span class="sxs-lookup"><span data-stu-id="c927b-164">When you add a channel or group tab, by default the app name displays (for example, **first-app** ).</span></span>

<span data-ttu-id="c927b-165">这可能会很好，具体取决于您调用应用程序的内容，但您可能希望提供一个名称，以便在组协作的上下文中更有意义 (例如， **工作组联系人** ) 。</span><span class="sxs-lookup"><span data-stu-id="c927b-165">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts** ).</span></span>

<span data-ttu-id="c927b-166">在中 `TabConfig.js` ，转到 `microsoftTeams.settings.setSettings` 。</span><span class="sxs-lookup"><span data-stu-id="c927b-166">In `TabConfig.js`, go to `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="c927b-167">添加 `suggestedDisplayName` 默认情况下要显示的选项卡名称的属性 (如) 所示。</span><span class="sxs-lookup"><span data-stu-id="c927b-167">Add the `suggestedDisplayName` property with the tab name you want to display by default (as shown).</span></span> <span data-ttu-id="c927b-168">使用提供的名称或创建自己的名称。</span><span class="sxs-lookup"><span data-stu-id="c927b-168">Use the provided name or create your own.</span></span> <span data-ttu-id="c927b-169"> (默认情况下，用户可以根据需要更改名称。 ) </span><span class="sxs-lookup"><span data-stu-id="c927b-169">(By default, users to change the name if they want.)</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="c927b-170">6. 生成并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="c927b-170">6. Build and run your app</span></span>

<span data-ttu-id="c927b-171">在时间方面，你将在本地构建和运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="c927b-171">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="c927b-172"> (工具包中也提供了此信息 `README` 。 ) </span><span class="sxs-lookup"><span data-stu-id="c927b-172">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="c927b-173">在终端中，转到您的应用程序项目的根目录并运行该目录 `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="c927b-173">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="c927b-174">运行 `npm start` 。</span><span class="sxs-lookup"><span data-stu-id="c927b-174">Run `npm start`.</span></span>

<span data-ttu-id="c927b-175">完成后，已 **成功编译了！**</span><span class="sxs-lookup"><span data-stu-id="c927b-175">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="c927b-176">终端中的邮件。</span><span class="sxs-lookup"><span data-stu-id="c927b-176">message in the terminal.</span></span> <span data-ttu-id="c927b-177">您的应用程序正在运行 `https://localhost:3000` 。</span><span class="sxs-lookup"><span data-stu-id="c927b-177">Your app is running on `https://localhost:3000`.</span></span>

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="c927b-178">7. 在团队中旁加载您的应用程序</span><span class="sxs-lookup"><span data-stu-id="c927b-178">7. Sideload your app in Teams</span></span>

<span data-ttu-id="c927b-179">您的应用程序已准备好在团队中进行测试。</span><span class="sxs-lookup"><span data-stu-id="c927b-179">Your app is ready to test in Teams.</span></span> <span data-ttu-id="c927b-180">若要执行此操作，您必须具有允许应用旁加载的帐户。</span><span class="sxs-lookup"><span data-stu-id="c927b-180">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="c927b-181"> (如果您不能确定，请了解如何获取 [团队开发帐户](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)。 ) </span><span class="sxs-lookup"><span data-stu-id="c927b-181">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

1. <span data-ttu-id="c927b-182">在 Visual Studio Code 中，按 **F5** 键以启动团队 web 客户端。</span><span class="sxs-lookup"><span data-stu-id="c927b-182">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="c927b-183">若要在团队中显示应用内容，请指定您的应用程序的运行位置 (`localhost`) 是可信的：</span><span class="sxs-lookup"><span data-stu-id="c927b-183">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="c927b-184">默认情况下，在同一浏览器窗口中打开一个新选项卡 () 按 **F5** 后打开的。</span><span class="sxs-lookup"><span data-stu-id="c927b-184">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="c927b-185">转到 `https://localhost:3000/tab` ""，然后继续转到 "" 页。</span><span class="sxs-lookup"><span data-stu-id="c927b-185">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="c927b-186">返回到 "团队"。</span><span class="sxs-lookup"><span data-stu-id="c927b-186">Go back to Teams.</span></span> <span data-ttu-id="c927b-187">在对话框中，选择 " **添加到团队** " 或 " **添加到聊天** "，并找到可用于测试的频道或聊天。</span><span class="sxs-lookup"><span data-stu-id="c927b-187">In the dialog, select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="c927b-188">选择 **"设置选项卡"** 。"配置" 页将显示在对话框中。</span><span class="sxs-lookup"><span data-stu-id="c927b-188">Select **Set up a tab**. The configuration page displays in a dialog.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="频道选项卡配置页的屏幕截图。":::
1. <span data-ttu-id="c927b-190">选择 " **保存** " 以配置选项卡。将显示内容页。</span><span class="sxs-lookup"><span data-stu-id="c927b-190">Select **Save** to configure the tab. The content page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="包含静态内容视图的频道选项卡的屏幕截图。":::

## <a name="well-done"></a><span data-ttu-id="c927b-192">干的好</span><span class="sxs-lookup"><span data-stu-id="c927b-192">Well done</span></span>

<span data-ttu-id="c927b-193">祝贺你！</span><span class="sxs-lookup"><span data-stu-id="c927b-193">Congratulations!</span></span> <span data-ttu-id="c927b-194">您有一个包含选项卡的团队应用程序，用于在频道和聊天中显示有用的内容。</span><span class="sxs-lookup"><span data-stu-id="c927b-194">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="c927b-195">了解更多</span><span class="sxs-lookup"><span data-stu-id="c927b-195">Learn more</span></span>

* <span data-ttu-id="c927b-196">[使用 Sso 对选项卡用户进行身份验证](../tabs/how-to/authentication/auth-aad-sso.md)：如果您仅希望授权用户查看您的选项卡，请通过 Azure Active DIRECTORY (AD) 设置单一登录 (SSO) 。</span><span class="sxs-lookup"><span data-stu-id="c927b-196">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="c927b-197">[从现有 web 应用或网页嵌入内容](../tabs/how-to/add-tab.md#tab-requirements)：我们向您介绍了如何为个人选项卡创建新内容，但您也可以从外部 URL 加载内容。</span><span class="sxs-lookup"><span data-stu-id="c927b-197">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="c927b-198">[为您的选项卡创建无缝体验](../tabs/design/tabs.md)：有关设计团队选项卡的建议指南，请参阅。</span><span class="sxs-lookup"><span data-stu-id="c927b-198">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="c927b-199">[为移动设备构建选项卡](../tabs/design/tabs-mobile.md)：了解如何为电话和平板电脑开发选项卡。</span><span class="sxs-lookup"><span data-stu-id="c927b-199">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="c927b-200">使用 Microsoft Graph API 的团队数据</span><span class="sxs-lookup"><span data-stu-id="c927b-200">Utilize Teams data with the Microsoft Graph API</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="c927b-201">创建不带工具箱的选项卡</span><span class="sxs-lookup"><span data-stu-id="c927b-201">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="c927b-202">下一课</span><span class="sxs-lookup"><span data-stu-id="c927b-202">Next lesson</span></span>

<span data-ttu-id="c927b-203">您知道如何构建协作选项卡。</span><span class="sxs-lookup"><span data-stu-id="c927b-203">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="c927b-204">想要尝试构建不同种类的团队应用吗？</span><span class="sxs-lookup"><span data-stu-id="c927b-204">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c927b-205">创建机器人</span><span class="sxs-lookup"><span data-stu-id="c927b-205">Build a bot</span></span>](../build-your-first-app/build-bot.md)
