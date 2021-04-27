---
title: 入门 - 生成频道和组选项卡
author: heath-hamilton
description: 使用 Microsoft Teams 频道和组选项卡快速创建 microsoft Teams Toolkit。
ms.author: lajanuar
localization_priority: Normal
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: aadab4b6826b026eadd5ed564b6e5de5c29b4b1d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020875"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="0dd36-103">为 Microsoft Teams 生成频道和组选项卡</span><span class="sxs-lookup"><span data-stu-id="0dd36-103">Build a channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="0dd36-104">在本教程中，你将生成基本频道 *选项卡 (也称为* 组选项卡 *) ，* 它是团队频道或聊天的全屏页面。</span><span class="sxs-lookup"><span data-stu-id="0dd36-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab*), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="0dd36-105">与个人选项卡不同，用户可以配置此类选项卡的某些方面 (例如，重命名该选项卡，以便其频道) 。</span><span class="sxs-lookup"><span data-stu-id="0dd36-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="0dd36-106">您的工作分配</span><span class="sxs-lookup"><span data-stu-id="0dd36-106">Your assignment</span></span>

<span data-ttu-id="0dd36-107">在不久之前，你的组织创建了一个 Teams 应用，该应用使用选项卡在技术支持 (HR 等部门显示重要的) 。</span><span class="sxs-lookup"><span data-stu-id="0dd36-107">Not long ago, your organization created a Teams app that uses a tab to display important contact information (help desk, HR, etc.).</span></span> <span data-ttu-id="0dd36-108">但是，由于它是个人选项卡，每个用户都必须安装该选项卡，以查看它，并且采用低于预期。</span><span class="sxs-lookup"><span data-stu-id="0dd36-108">However, since it's a personal tab, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="0dd36-109">换句话说，太多工作人员仍不知道如何联系技术支持。</span><span class="sxs-lookup"><span data-stu-id="0dd36-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="0dd36-110">通过生成频道选项卡，可以使此信息更易于查找，这将消除要求所有人安装应用的负担。</span><span class="sxs-lookup"><span data-stu-id="0dd36-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="0dd36-111">相反，一个用户可以在频道中添加选项卡或聊天，以有利于整个组。</span><span class="sxs-lookup"><span data-stu-id="0dd36-111">Instead, one user can add the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="0dd36-112">您将了解哪些功能</span><span class="sxs-lookup"><span data-stu-id="0dd36-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="0dd36-113">使用 Microsoft Teams Toolkit for Visual Studio Code 创建应用项目</span><span class="sxs-lookup"><span data-stu-id="0dd36-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="0dd36-114">确定一些与通道选项卡相关的应用配置和基架</span><span class="sxs-lookup"><span data-stu-id="0dd36-114">Identify some of the app configurations and scaffolding relevant to channel tabs</span></span>
> * <span data-ttu-id="0dd36-115">创建选项卡内容</span><span class="sxs-lookup"><span data-stu-id="0dd36-115">Create tab content</span></span>
> * <span data-ttu-id="0dd36-116">为选项卡的配置页创建内容</span><span class="sxs-lookup"><span data-stu-id="0dd36-116">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="0dd36-117">提供建议的选项卡名称</span><span class="sxs-lookup"><span data-stu-id="0dd36-117">Provide a suggested tab name</span></span>
> * <span data-ttu-id="0dd36-118">在本地生成并运行应用</span><span class="sxs-lookup"><span data-stu-id="0dd36-118">Build and run your app locally</span></span>
> * <span data-ttu-id="0dd36-119">在 Teams 中旁加载应用进行测试</span><span class="sxs-lookup"><span data-stu-id="0dd36-119">Sideload your app in Teams for testing</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0dd36-120">开始之前</span><span class="sxs-lookup"><span data-stu-id="0dd36-120">Before you begin</span></span>

<span data-ttu-id="0dd36-121">如果尚未了解，请确保 [了解并安装 Teams 开发先决条件](build-first-app-overview.md#get-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="0dd36-121">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="0dd36-122">1. 创建应用项目</span><span class="sxs-lookup"><span data-stu-id="0dd36-122">1. Create your app project</span></span>

<span data-ttu-id="0dd36-123">Microsoft Teams Toolkit帮助配置你的应用和设置与频道和组选项卡相关的基架，包括显示"Hello， World！"的基本配置页面和内容页。</span><span class="sxs-lookup"><span data-stu-id="0dd36-123">The Microsoft Teams Toolkit helps configure your app and set up scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="0dd36-124">消息。</span><span class="sxs-lookup"><span data-stu-id="0dd36-124">message.</span></span>

> [!TIP]
> <span data-ttu-id="0dd36-125">如果你之前尚未创建 Teams 应用项目，你可能会发现按照这些说明更详细地解释项目会[](../build-your-first-app/build-and-run.md)很有帮助。</span><span class="sxs-lookup"><span data-stu-id="0dd36-125">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. 在Visual Studio代码"中，选择左侧活动栏上的 **"Microsoft Teams"，** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择"**创建新的 Teams 应用"。**
1. <span data-ttu-id="0dd36-127">系统提示时，使用 Microsoft 365 开发帐户登录。</span><span class="sxs-lookup"><span data-stu-id="0dd36-127">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="0dd36-128">在"**添加功能"屏幕上**，选择"**选项卡**"，然后选择"下一 **步"。**</span><span class="sxs-lookup"><span data-stu-id="0dd36-128">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="0dd36-129">输入 Teams 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="0dd36-129">Enter a name for your Teams app.</span></span> <span data-ttu-id="0dd36-130"> (这是应用的默认名称，也是本地计算机上应用项目目录的名称。) 选择组或 Teams 频道 **选项卡**。</span><span class="sxs-lookup"><span data-stu-id="0dd36-130">(This is the default name for your app and also the name of the app project directory on your local machine.) Select **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="0dd36-131">选择 **屏幕** 底部的"完成"以配置项目。</span><span class="sxs-lookup"><span data-stu-id="0dd36-131">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="0dd36-132">2. 确定相关的应用程序项目组件</span><span class="sxs-lookup"><span data-stu-id="0dd36-132">2. Identify relevant app project components</span></span>

<span data-ttu-id="0dd36-133">使用工具包创建项目时，将自动设置大部分应用配置和基架。</span><span class="sxs-lookup"><span data-stu-id="0dd36-133">Much of the app configurations and scaffolding are set up automatically when you create your project with the toolkit.</span></span> <span data-ttu-id="0dd36-134">让我们看一下生成频道选项卡的主要组件。</span><span class="sxs-lookup"><span data-stu-id="0dd36-134">Let's look at the main components for building a channel tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="0dd36-135">应用配置</span><span class="sxs-lookup"><span data-stu-id="0dd36-135">App configurations</span></span>

<span data-ttu-id="0dd36-136">在工具包中，转到 **App Studio** 以查看和更新应用配置。</span><span class="sxs-lookup"><span data-stu-id="0dd36-136">In the toolkit, go to **App Studio** to view and update your app configurations.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="0dd36-137">应用基架</span><span class="sxs-lookup"><span data-stu-id="0dd36-137">App scaffolding</span></span>

<span data-ttu-id="0dd36-138">应用基架提供在 Teams 中呈现频道选项卡的组件。</span><span class="sxs-lookup"><span data-stu-id="0dd36-138">The app scaffolding provides the components for rendering your channel tab in Teams.</span></span> <span data-ttu-id="0dd36-139">你可以处理很多项目，但现在你只需关注以下内容：</span><span class="sxs-lookup"><span data-stu-id="0dd36-139">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="0dd36-140">位于项目目录中 `src/components` 的两个文件：</span><span class="sxs-lookup"><span data-stu-id="0dd36-140">Two files located in the `src/components` directory of your project:</span></span>
  * <span data-ttu-id="0dd36-141">`Tab.js` 用于呈现选项卡的内容页。</span><span class="sxs-lookup"><span data-stu-id="0dd36-141">`Tab.js` for rendering your tab's content page.</span></span>
  * <span data-ttu-id="0dd36-142">`TabConfig.js` 用于呈现选项卡的配置页面。</span><span class="sxs-lookup"><span data-stu-id="0dd36-142">`TabConfig.js` for rendering your tab's configuration page.</span></span>
* <span data-ttu-id="0dd36-143">Microsoft Teams JavaScript 客户端 SDK，预加载到项目的前端组件中。</span><span class="sxs-lookup"><span data-stu-id="0dd36-143">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="0dd36-144">3. 自定义选项卡内容页</span><span class="sxs-lookup"><span data-stu-id="0dd36-144">3. Customize your tab content page</span></span>

<span data-ttu-id="0dd36-145">复制以下代码段并更新与您的组织相关的信息，或者出于时间考虑，按如下所示使用代码。</span><span class="sxs-lookup"><span data-stu-id="0dd36-145">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="0dd36-146">转到 目录 `src/components` 并打开 `Tab.js` 。</span><span class="sxs-lookup"><span data-stu-id="0dd36-146">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="0dd36-147">找到 `render()` 函数，然后将内容粘贴到 `return()` (，如) 。</span><span class="sxs-lookup"><span data-stu-id="0dd36-147">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="0dd36-148">将以下规则 (也位于) ，因此无论使用哪个主题，电子邮件链接 `App.css` `src/components` 都更易于阅读。</span><span class="sxs-lookup"><span data-stu-id="0dd36-148">Add the following rule to `App.css` (also located in `src/components`) so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="0dd36-149">4. 自定义选项卡配置页</span><span class="sxs-lookup"><span data-stu-id="0dd36-149">4. Customize your tab configuration page</span></span>

<span data-ttu-id="0dd36-150">频道或聊天中的每个选项卡都有一个配置页面，即至少具有一个设置选项的模式，在用户添加应用时显示此选项。</span><span class="sxs-lookup"><span data-stu-id="0dd36-150">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="0dd36-151">默认情况下，配置页会询问用户是否要在安装选项卡时通知频道或聊天。</span><span class="sxs-lookup"><span data-stu-id="0dd36-151">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="0dd36-152">将一些自定义内容添加到配置页面。</span><span class="sxs-lookup"><span data-stu-id="0dd36-152">Add some custom content to your configuration page.</span></span> <span data-ttu-id="0dd36-153">转到项目的目录，打开 ，并更新 (中的占位符内容，如以下示例 `src/components` `TabConfig.js` `return()`) 。</span><span class="sxs-lookup"><span data-stu-id="0dd36-153">Go to your project's `src/components` directory, open `TabConfig.js`, and update the placeholder content inside `return()` (as shown in the following example).</span></span>

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
> <span data-ttu-id="0dd36-154">至少，请在此页面上提供有关你的应用的一些简短信息，因为这可能是用户第一次了解它。</span><span class="sxs-lookup"><span data-stu-id="0dd36-154">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="0dd36-155">还可以包括自定义配置选项或身份验证 [工作流](../tabs/how-to/authentication/auth-aad-sso.md)，这在选项卡配置页面上很常见。</span><span class="sxs-lookup"><span data-stu-id="0dd36-155">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-provide-a-suggested-tab-name"></a><span data-ttu-id="0dd36-156">5. 提供建议的选项卡名称</span><span class="sxs-lookup"><span data-stu-id="0dd36-156">5. Provide a suggested tab name</span></span>

<span data-ttu-id="0dd36-157">添加通道选项卡时，默认情况下，应用名称 (，例如，第一 **个应用**) 。</span><span class="sxs-lookup"><span data-stu-id="0dd36-157">When you add a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="0dd36-158">这可能没有问题，具体取决于你调用你的应用的名称，但你可能希望提供一个在组协作上下文中更有意义的名称 (例如，团队联系人) 。 </span><span class="sxs-lookup"><span data-stu-id="0dd36-158">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

1. <span data-ttu-id="0dd36-159">在 `TabConfig.js` 中，转到 `microsoftTeams.settings.setSettings` 。</span><span class="sxs-lookup"><span data-stu-id="0dd36-159">In `TabConfig.js`, go to `microsoftTeams.settings.setSettings`.</span></span>
2. <span data-ttu-id="0dd36-160">使用 `suggestedDisplayName` 要默认显示的选项卡名称添加 属性。</span><span class="sxs-lookup"><span data-stu-id="0dd36-160">Add the `suggestedDisplayName` property with the tab name you want to display by default.</span></span> 
3. <span data-ttu-id="0dd36-161">使用以下示例中提供的名称或键入您的名称。</span><span class="sxs-lookup"><span data-stu-id="0dd36-161">Use the name provided in the following example or type your name.</span></span> <span data-ttu-id="0dd36-162"> (默认情况下，用户可以更改 name.) </span><span class="sxs-lookup"><span data-stu-id="0dd36-162">(By default, users can change the name.)</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="0dd36-163">6. 生成并运行应用</span><span class="sxs-lookup"><span data-stu-id="0dd36-163">6. Build and run your app</span></span>

<span data-ttu-id="0dd36-164">为了在时间上，你将在本地生成并运行你的应用。</span><span class="sxs-lookup"><span data-stu-id="0dd36-164">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="0dd36-165"> (此信息也可在工具包 `README` .) </span><span class="sxs-lookup"><span data-stu-id="0dd36-165">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="0dd36-166">在终端中，转到应用项目的根目录并运行 `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="0dd36-166">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="0dd36-167">运行 `npm start`。</span><span class="sxs-lookup"><span data-stu-id="0dd36-167">Run `npm start`.</span></span>

<span data-ttu-id="0dd36-168">完成后，将成功 **编译！**</span><span class="sxs-lookup"><span data-stu-id="0dd36-168">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="0dd36-169">消息。</span><span class="sxs-lookup"><span data-stu-id="0dd36-169">message in the terminal.</span></span> <span data-ttu-id="0dd36-170">你的应用在 上运行 `https://localhost:3000` 。</span><span class="sxs-lookup"><span data-stu-id="0dd36-170">Your app is running on `https://localhost:3000`.</span></span>

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="0dd36-171">7. 在 Teams 中旁加载应用</span><span class="sxs-lookup"><span data-stu-id="0dd36-171">7. Sideload your app in Teams</span></span>

<span data-ttu-id="0dd36-172">你的应用已准备好在 Teams 中进行测试。</span><span class="sxs-lookup"><span data-stu-id="0dd36-172">Your app is ready to test in Teams.</span></span> <span data-ttu-id="0dd36-173">为此，你必须具有允许应用旁加载的帐户。</span><span class="sxs-lookup"><span data-stu-id="0dd36-173">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="0dd36-174"> (如果你不确定拥有该帐户，请了解如何获取 Teams 开发 [帐户](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).) </span><span class="sxs-lookup"><span data-stu-id="0dd36-174">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

1. <span data-ttu-id="0dd36-175">在Visual Studio代码"中，按 **F5** 键以启动 Teams Web 客户端。</span><span class="sxs-lookup"><span data-stu-id="0dd36-175">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="0dd36-176">若要在 Teams 中显示你的应用内容，请指定你的应用在哪些 () `localhost` 可信：</span><span class="sxs-lookup"><span data-stu-id="0dd36-176">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="0dd36-177">默认情况下，在 Google Chrome 的相同浏览器窗口中打开 (新选项卡) 按 **F5 打开**。</span><span class="sxs-lookup"><span data-stu-id="0dd36-177">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="0dd36-178">转到 `https://localhost:3000/tab` 并转到页面。</span><span class="sxs-lookup"><span data-stu-id="0dd36-178">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="0dd36-179">返回到 Teams。</span><span class="sxs-lookup"><span data-stu-id="0dd36-179">Go back to Teams.</span></span> <span data-ttu-id="0dd36-180">在模式中，选择"**添加到团队"** 或"添加到聊天"，然后找到可用于测试的频道或聊天。</span><span class="sxs-lookup"><span data-stu-id="0dd36-180">In the modal, select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="0dd36-181">选择 **"设置选项卡"。** 配置页以模式显示。</span><span class="sxs-lookup"><span data-stu-id="0dd36-181">Select **Set up a tab**. The configuration page displays in a modal.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="频道选项卡配置页面的屏幕截图。":::
1. <span data-ttu-id="0dd36-183">选择 **"保存** "以配置选项卡。将显示内容页。</span><span class="sxs-lookup"><span data-stu-id="0dd36-183">Select **Save** to configure the tab. The content page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="具有静态内容视图的频道选项卡的屏幕截图。":::

## <a name="well-done"></a><span data-ttu-id="0dd36-185">干的好</span><span class="sxs-lookup"><span data-stu-id="0dd36-185">Well done</span></span>

<span data-ttu-id="0dd36-186">恭喜！</span><span class="sxs-lookup"><span data-stu-id="0dd36-186">Congratulations!</span></span> <span data-ttu-id="0dd36-187">你有一个 Teams 应用，该应用具有一个选项卡，用于显示频道和聊天中的有用内容。</span><span class="sxs-lookup"><span data-stu-id="0dd36-187">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="0dd36-188">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="0dd36-188">Learn more</span></span>

* <span data-ttu-id="0dd36-189">遵循 [我们的设计指南](../tabs/design/tabs.md) ，使用生产就绪 [UI](../concepts/design/design-teams-app-ui-templates.md) 模板构建，以创建无缝体验。</span><span class="sxs-lookup"><span data-stu-id="0dd36-189">Follow our [design guidelines](../tabs/design/tabs.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* <span data-ttu-id="0dd36-190">了解 [选项卡的移动](../tabs/design/tabs-mobile.md) 注意事项。</span><span class="sxs-lookup"><span data-stu-id="0dd36-190">Understand [mobile considerations](../tabs/design/tabs-mobile.md) for tabs.</span></span>
* <span data-ttu-id="0dd36-191">[将 SSO 身份验证添加到选项卡](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="0dd36-191">[Add SSO authentication to your tab](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>
* <span data-ttu-id="0dd36-192">通过 Microsoft [Graph](https://docs.microsoft.com/graph/teams-concept-overview)利用 Teams 数据。</span><span class="sxs-lookup"><span data-stu-id="0dd36-192">Utilize Teams data with [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>
* [<span data-ttu-id="0dd36-193">创建不带工具包的选项卡</span><span class="sxs-lookup"><span data-stu-id="0dd36-193">Create a tab without the toolkit</span></span>](../tabs/quickstarts/create-channel-group-tab-node-yeoman.md)

## <a name="next-lesson"></a><span data-ttu-id="0dd36-194">下一课程</span><span class="sxs-lookup"><span data-stu-id="0dd36-194">Next lesson</span></span>

<span data-ttu-id="0dd36-195">了解如何生成用于协作的选项卡。</span><span class="sxs-lookup"><span data-stu-id="0dd36-195">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="0dd36-196">想要尝试构建不同类型的 Teams 应用？</span><span class="sxs-lookup"><span data-stu-id="0dd36-196">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0dd36-197">创建机器人</span><span class="sxs-lookup"><span data-stu-id="0dd36-197">Build a bot</span></span>](../build-your-first-app/build-bot.md)
