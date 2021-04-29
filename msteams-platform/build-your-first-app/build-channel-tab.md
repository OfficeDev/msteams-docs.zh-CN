---
title: 入门 - 生成频道和组选项卡
author: girliemac
description: 使用 Microsoft Teams 频道和组选项卡快速创建 microsoft Teams Toolkit。
ms.author: timura
ms.date: 03/22/2020
ms.topic: tutorial
ms.openlocfilehash: 868a471499bf2015196b7b741e340d070d0ed458
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068740"
---
# <a name="build-your-first-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="712a4-103">为 Microsoft Teams 生成你的第一个频道和组选项卡</span><span class="sxs-lookup"><span data-stu-id="712a4-103">Build your first channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="712a4-104">本教程指导你生成基本频道 *选项卡，也称为* 组选项卡，它是团队频道或聊天的全屏页面。</span><span class="sxs-lookup"><span data-stu-id="712a4-104">This tutorial teaches you to build a basic *channel tab* also known as a *group tab*, which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="712a4-105">还可以配置此类选项卡的某些方面，例如，重命名选项卡，以便对通道有意义，而您无法在个人选项卡中这样做。</span><span class="sxs-lookup"><span data-stu-id="712a4-105">You can also configure some aspects of this kind of tab, for example, rename the tab so it's meaningful to their channel, which you cannot do in a Personal Tab.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="712a4-106">您将了解哪些功能</span><span class="sxs-lookup"><span data-stu-id="712a4-106">What you'll learn</span></span>

* <span data-ttu-id="712a4-107">使用适用于 Microsoft Teams 代码的 Microsoft Teams Toolkit创建Visual Studio项目。</span><span class="sxs-lookup"><span data-stu-id="712a4-107">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="712a4-108">了解与通道选项卡相关的应用配置和基架。</span><span class="sxs-lookup"><span data-stu-id="712a4-108">Understand the app configurations and scaffolding relevant to channel tabs.</span></span>
* <span data-ttu-id="712a4-109">创建选项卡内容和选项卡配置。</span><span class="sxs-lookup"><span data-stu-id="712a4-109">Create tab content and tab configuration.</span></span>
* <span data-ttu-id="712a4-110">在团队中生成并运行应用进行测试。</span><span class="sxs-lookup"><span data-stu-id="712a4-110">Build and run your app in teams for testing.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="712a4-111">先决条件</span><span class="sxs-lookup"><span data-stu-id="712a4-111">Prerequisites</span></span>

<span data-ttu-id="712a4-112">确保你了解如何设置和构建简单的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="712a4-112">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="712a4-113">有关详细信息，请参阅创建 [你的第一个 Microsoft Teams"Hello， World！"应用](../build-your-first-app/build-and-run.md)。</span><span class="sxs-lookup"><span data-stu-id="712a4-113">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="712a4-114">1. 创建应用项目</span><span class="sxs-lookup"><span data-stu-id="712a4-114">1. Create your app project</span></span>

<span data-ttu-id="712a4-115">Microsoft Teams Toolkit可帮助你配置应用并设置与频道和组选项卡相关的基架。</span><span class="sxs-lookup"><span data-stu-id="712a4-115">The Microsoft Teams Toolkit helps you to configure your app and set up the scaffolding relevant to channel and group tabs.</span></span> <span data-ttu-id="712a4-116">它还包含显示"Hello， World！"的基本配置页和内容页。</span><span class="sxs-lookup"><span data-stu-id="712a4-116">It also contains a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="712a4-117">消息。</span><span class="sxs-lookup"><span data-stu-id="712a4-117">message.</span></span>

<span data-ttu-id="712a4-118">**创建应用项目**</span><span class="sxs-lookup"><span data-stu-id="712a4-118">**To create your app project**</span></span>

1. 转到"Visual Studio代码"，然后选择 **左侧活动栏上的"Microsoft** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: Teams"。
1. <span data-ttu-id="712a4-120">当系统提示你登录时，使用 Microsoft 365 开发帐户登录。</span><span class="sxs-lookup"><span data-stu-id="712a4-120">Sign in with your Microsoft 365 development account when prompted to do so.</span></span>
1. <span data-ttu-id="712a4-121">在"**选择项目"** 屏幕上，选择"频道和组 (下的 **"JS**) **JavaScript 应用"。**</span><span class="sxs-lookup"><span data-stu-id="712a4-121">On the **Select project** screen, select **JS** (JavaScript) under **Channel and group app**.</span></span>
1. <span data-ttu-id="712a4-122">输入 Teams 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="712a4-122">Enter a name for your Teams app.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="712a4-123">这是应用的默认名称，也是本地计算机上应用项目目录的名称。</span><span class="sxs-lookup"><span data-stu-id="712a4-123">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>

1. <span data-ttu-id="712a4-124">选择 **"组"或"Teams 频道"选项卡**。</span><span class="sxs-lookup"><span data-stu-id="712a4-124">Select **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="712a4-125">选择 **屏幕** 底部的"完成"以配置项目，并在本地计算机上保存项目。</span><span class="sxs-lookup"><span data-stu-id="712a4-125">Select **Finish** at the bottom of the screen to configure your project and save your project on your local machine.</span></span>  

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="712a4-126">2. 了解应用项目组件</span><span class="sxs-lookup"><span data-stu-id="712a4-126">2. Understand your app project components</span></span>

<span data-ttu-id="712a4-127">使用工具包创建项目时，将自动设置大部分应用配置和基架。</span><span class="sxs-lookup"><span data-stu-id="712a4-127">Much of the app configurations and scaffolding are set up automatically when you create your project with the toolkit.</span></span> <span data-ttu-id="712a4-128">让我们看一下生成频道选项卡的主要组件。</span><span class="sxs-lookup"><span data-stu-id="712a4-128">Let's look at the main components for building a channel tab.</span></span>

* <span data-ttu-id="712a4-129">**应用配置**：在 **工具包** 中打开 App Studio 以查看和更新应用配置。</span><span class="sxs-lookup"><span data-stu-id="712a4-129">**App configurations**: Open **App Studio** in the toolkit to view and update your app configurations.</span></span>
* <span data-ttu-id="712a4-130">**应用基架**：应用基架提供在 Teams 中呈现频道选项卡所需的组件。</span><span class="sxs-lookup"><span data-stu-id="712a4-130">**App scaffolding**: The app scaffolding provides the components needed for rendering your channel tab in Teams.</span></span> <span data-ttu-id="712a4-131">不过，你可以处理很多项目，但现在让我们关注以下内容：</span><span class="sxs-lookup"><span data-stu-id="712a4-131">There's a lot you can work with, however, for now let's focus on the following:</span></span>
  * <span data-ttu-id="712a4-132">位于项目目录中 `src/components` 的文件：</span><span class="sxs-lookup"><span data-stu-id="712a4-132">The files located in the `src/components` directory of your project:</span></span>
    * <span data-ttu-id="712a4-133">`Tab.js` 用于呈现选项卡的内容页。</span><span class="sxs-lookup"><span data-stu-id="712a4-133">`Tab.js` for rendering your tab's content page.</span></span>
    * <span data-ttu-id="712a4-134">`TabConfig.js` 用于呈现选项卡的配置页面。</span><span class="sxs-lookup"><span data-stu-id="712a4-134">`TabConfig.js` for rendering your tab's configuration page.</span></span>
  * <span data-ttu-id="712a4-135">Microsoft Teams JavaScript 客户端 SDK，预加载到项目的前端组件中。</span><span class="sxs-lookup"><span data-stu-id="712a4-135">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="712a4-136">3. 自定义选项卡内容页</span><span class="sxs-lookup"><span data-stu-id="712a4-136">3. Customize your tab content page</span></span>

1. <span data-ttu-id="712a4-137">复制并修改以下代码示例，并包含与组织有关的信息。</span><span class="sxs-lookup"><span data-stu-id="712a4-137">Copy and modify the following code sample with information that's relevant to your organization.</span></span> <span data-ttu-id="712a4-138">也可以按以下代码段使用代码段：</span><span class="sxs-lookup"><span data-stu-id="712a4-138">You can also use the snippet as it is:</span></span>
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
1. <span data-ttu-id="712a4-139">转到 `src/components` 目录并打开 `Tab.js` 文件。</span><span class="sxs-lookup"><span data-stu-id="712a4-139">Go to the `src/components` directory and open the `Tab.js` file.</span></span> <span data-ttu-id="712a4-140">找到 `render()` 函数，然后将代码粘贴到 内 `return()` ，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="712a4-140">Locate the `render()` function and paste your code inside `return()` as shown in the following example:</span></span>
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
1. <span data-ttu-id="712a4-141">转到 目录，然后用以下代码更新文件，使电子邮件链接更易于在任何使用的主题 `src/components` `App.css` 中阅读：</span><span class="sxs-lookup"><span data-stu-id="712a4-141">Go to the `src/components` directory and update the `App.css` file with the following code to make the email links easier to read in any theme that is used:</span></span>
    ```CSS
    a {
      color: inherit;
    }
    ```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="712a4-142">4. 自定义选项卡配置页</span><span class="sxs-lookup"><span data-stu-id="712a4-142">4. Customize your tab configuration page</span></span>

<span data-ttu-id="712a4-143">频道或聊天中的每个选项卡都有一个配置页面，即至少具有一个设置选项的模式，在用户添加应用时显示此选项。</span><span class="sxs-lookup"><span data-stu-id="712a4-143">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="712a4-144">默认情况下，配置页会询问用户是否要在安装选项卡时通知频道或聊天。</span><span class="sxs-lookup"><span data-stu-id="712a4-144">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span> <span data-ttu-id="712a4-145">您可以通过添加自定义内容来自定义配置页。</span><span class="sxs-lookup"><span data-stu-id="712a4-145">You can customize the configuration page by adding custom content.</span></span>

<span data-ttu-id="712a4-146">若要添加自定义内容，请从 目录中打开 `TabConfig.js` `src/components` 文件并更新内的占位符内容 `return()` ，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="712a4-146">To add custom content, open `TabConfig.js` file from the `src/components` directory and update the placeholder content inside `return()` as shown in the following example:</span></span>

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
> <span data-ttu-id="712a4-147">在此页面上提供有关你的应用的简短信息，因为这将是用户第一次阅读它。</span><span class="sxs-lookup"><span data-stu-id="712a4-147">Give a brief information about your app on this page since this would be the first time users are reading about it.</span></span> <span data-ttu-id="712a4-148">还可以包括自定义配置选项或身份验证 [工作流](../tabs/how-to/authentication/auth-aad-sso.md)，这是在选项卡配置页面上很常见的。</span><span class="sxs-lookup"><span data-stu-id="712a4-148">You can also include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-customize-your-tab-name"></a><span data-ttu-id="712a4-149">5. 自定义选项卡名称</span><span class="sxs-lookup"><span data-stu-id="712a4-149">5. Customize your tab name</span></span>

<span data-ttu-id="712a4-150">添加通道选项卡时，应用程序名称默认显示，例如，第 **一个应用**。</span><span class="sxs-lookup"><span data-stu-id="712a4-150">When you add a channel tab, the app name displays by default, for example, **first-app**.</span></span> <span data-ttu-id="712a4-151">还可以提供在组协作上下文中更有意义的名称，例如，"**团队联系人"：**</span><span class="sxs-lookup"><span data-stu-id="712a4-151">You can also provide a name that makes more sense in the context of group collaboration, for example, **Team Contacts**:</span></span>

1. <span data-ttu-id="712a4-152">转到 `src/components` 目录并打开 `TabConfig.js` 文件。</span><span class="sxs-lookup"><span data-stu-id="712a4-152">Go to the `src/components` directory and open the `TabConfig.js` file.</span></span>
1. <span data-ttu-id="712a4-153">在 `suggestedDisplayName` 下面添加包含要默认显示的选项卡名称的属性 `microsoftTeams.settings.setSettings` ，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="712a4-153">Add the `suggestedDisplayName` property with the tab name you want to display by default under `microsoftTeams.settings.setSettings` as shown in the following example:</span></span>

  ```JavaScript
    microsoftTeams.settings.setSettings({
    "contentUrl": "https://localhost:3000/tab",
    "suggestedDisplayName": "Team Contacts"
  });
  ```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="712a4-154">6. 生成并运行应用</span><span class="sxs-lookup"><span data-stu-id="712a4-154">6. Build and run your app</span></span>

<span data-ttu-id="712a4-155">本教程指导你在本地生成和运行应用。</span><span class="sxs-lookup"><span data-stu-id="712a4-155">This tutorial teaches you to build and run your app locally.</span></span> 

1. <span data-ttu-id="712a4-156">转到终端中应用项目的根目录。</span><span class="sxs-lookup"><span data-stu-id="712a4-156">Go to the root directory of your app project in Terminal.</span></span>
1. <span data-ttu-id="712a4-157">运行 `npm install`。</span><span class="sxs-lookup"><span data-stu-id="712a4-157">Run `npm install`.</span></span>
1. <span data-ttu-id="712a4-158">运行 `npm start`。</span><span class="sxs-lookup"><span data-stu-id="712a4-158">Run `npm start`.</span></span>

<span data-ttu-id="712a4-159">此信息也存在于工具包 `README` 的 部分中。</span><span class="sxs-lookup"><span data-stu-id="712a4-159">This information is also present in the `README` section of the toolkit.</span></span>
<span data-ttu-id="712a4-160">你的应用在编译 `https://localhost:3000` 成功后 **运行！**</span><span class="sxs-lookup"><span data-stu-id="712a4-160">Your app is running on `https://localhost:3000` after the **Compiled successfully!**</span></span> <span data-ttu-id="712a4-161">消息显示在终端中。</span><span class="sxs-lookup"><span data-stu-id="712a4-161">message appears in the terminal.</span></span> 

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="712a4-162">7. 在 Teams 中旁加载应用</span><span class="sxs-lookup"><span data-stu-id="712a4-162">7. Sideload your app in Teams</span></span>

<span data-ttu-id="712a4-163">你的应用已准备好在 Teams 中进行测试。</span><span class="sxs-lookup"><span data-stu-id="712a4-163">Your app is ready to test in Teams.</span></span> <span data-ttu-id="712a4-164">为此，你必须具有允许应用旁加载的帐户。</span><span class="sxs-lookup"><span data-stu-id="712a4-164">To do this, you must have an account that allows app sideloading.</span></span> 

1. <span data-ttu-id="712a4-165">使用 **F5** 键在 Visual Studio Code 中打开 Teams Web 客户端。</span><span class="sxs-lookup"><span data-stu-id="712a4-165">Open a Teams web client in Visual Studio Code with the **F5** key.</span></span>
1. <span data-ttu-id="712a4-166">通过 () 在 Teams 中显示你的应用内容，添加可信赖 `localhost` 的外接程序：</span><span class="sxs-lookup"><span data-stu-id="712a4-166">Add (`localhost`) as trustworthy by following these steps to enable your app content to display in Teams:</span></span>

   1. <span data-ttu-id="712a4-167">默认情况下，在 Google Chrome (打开一个新选项卡，) **F5** 键打开该选项卡。</span><span class="sxs-lookup"><span data-stu-id="712a4-167">Open a new tab in the same browser window (Google Chrome by default) which opened with the **F5** key.</span></span>
   1. <span data-ttu-id="712a4-168">打开 `https://localhost:3000/tab` 并继续执行页面。</span><span class="sxs-lookup"><span data-stu-id="712a4-168">Open `https://localhost:3000/tab` and proceed to the page.</span></span>

1. <span data-ttu-id="712a4-169">选择 **"添加到团队"** 或"添加到聊天"，并找到可用于从 Teams 中的模式进行测试的频道或聊天。</span><span class="sxs-lookup"><span data-stu-id="712a4-169">Select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing from the modal in Teams.</span></span>
1. <span data-ttu-id="712a4-170">选择 **"设置选项卡"。** 配置页以模式显示。</span><span class="sxs-lookup"><span data-stu-id="712a4-170">Select **Set up a tab**. The configuration page displays in a modal.</span></span>

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="频道选项卡配置页面的屏幕截图。":::

1. <span data-ttu-id="712a4-172">选择 **"保存** "以配置选项卡。将显示以下内容页：</span><span class="sxs-lookup"><span data-stu-id="712a4-172">Select **Save** to configure the tab. The following content page appears:</span></span>

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="具有静态内容视图的频道选项卡的屏幕截图。":::

## <a name="see-also"></a><span data-ttu-id="712a4-174">另请参阅</span><span class="sxs-lookup"><span data-stu-id="712a4-174">See also</span></span>

* [<span data-ttu-id="712a4-175">生成并运行你的第一个 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="712a4-175">Build and run your first Microsoft Teams app</span></span>](../build-your-first-app/build-and-run.md) 
* [<span data-ttu-id="712a4-176">团队 JavaScript 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="712a4-176">Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="712a4-177">为 Microsoft Teams 桌面和 Web 设计选项卡</span><span class="sxs-lookup"><span data-stu-id="712a4-177">Designing your tab for Microsoft Teams desktop and web</span></span>](../tabs/design/tabs.md) 
* [<span data-ttu-id="712a4-178">使用 UI 模板设计 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="712a4-178">Designing your Microsoft Teams app with UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="712a4-179">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="712a4-179">Tabs on mobile</span></span>](../tabs/design/tabs-mobile.md)
* [<span data-ttu-id="712a4-180">单一登录 (SSO) 选项卡支持</span><span class="sxs-lookup"><span data-stu-id="712a4-180">Single sign-on (SSO) support for tabs</span></span>](../tabs/how-to/authentication/auth-aad-sso.md)
* [<span data-ttu-id="712a4-181">Microsoft Teams API 概述</span><span class="sxs-lookup"><span data-stu-id="712a4-181">Microsoft Teams API overview</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="712a4-182">使用 Microsoft Teams Node.js Yeoman 生成器创建自定义个人选项卡</span><span class="sxs-lookup"><span data-stu-id="712a4-182">Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a><span data-ttu-id="712a4-183">后续步骤</span><span class="sxs-lookup"><span data-stu-id="712a4-183">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="712a4-184">创建机器人</span><span class="sxs-lookup"><span data-stu-id="712a4-184">Build a bot</span></span>](../build-your-first-app/build-bot.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="712a4-185">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="712a4-185">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)