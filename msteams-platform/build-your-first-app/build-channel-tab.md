---
author: heath-hamilton
description: 了解如何为你的首个 Microsoft 团队应用构建通道和组选项卡。
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
title: 生成团队频道和组选项卡
ms.openlocfilehash: d97d8c13404077bff999db48b24b773aa4bc04ca
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237809"
---
# <a name="build-a-teams-channel-and-group-tab"></a><span data-ttu-id="f833c-103">生成团队频道和组选项卡</span><span class="sxs-lookup"><span data-stu-id="f833c-103">Build a Teams channel and group tab</span></span>

<span data-ttu-id="f833c-104">在本教程中，你将构建基本的 *频道选项卡* (也称为 " *组" 选项* 卡) （它是团队频道或聊天的全屏页面）。</span><span class="sxs-lookup"><span data-stu-id="f833c-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab*), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="f833c-105">与 "个人" 选项卡不同，用户可以配置此类选项卡的某些方面 (例如，重命名选项卡，使其对频道) 有意义。</span><span class="sxs-lookup"><span data-stu-id="f833c-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="f833c-106">您的分配</span><span class="sxs-lookup"><span data-stu-id="f833c-106">Your assignment</span></span>

<span data-ttu-id="f833c-107">以前，你的组织创建了一个 "团队" 选项卡，其中包含有关如何联系重要功能 (技术支持、人力资源等 ) 的信息。</span><span class="sxs-lookup"><span data-stu-id="f833c-107">Not long ago, your organization created a Teams tab with information on how to contact important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="f833c-108">但是，由于该选项卡的作用范围仅供个人使用，因此每个用户都必须安装该选项卡，才能看到它，并且采用低于预期。</span><span class="sxs-lookup"><span data-stu-id="f833c-108">However, since the tab was scoped only for personal use, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="f833c-109">换句话说，工作线程太多仍不知道如何联系技术支持人员。</span><span class="sxs-lookup"><span data-stu-id="f833c-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="f833c-110">您可以通过构建通道选项卡使此信息更易于查找，这将消除要求每个人安装应用程序的负担。</span><span class="sxs-lookup"><span data-stu-id="f833c-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="f833c-111">相反，一个用户可以在频道或聊天中安装该选项卡，以了解整个组的好处。</span><span class="sxs-lookup"><span data-stu-id="f833c-111">Instead, one user can install the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="f833c-112">你将了解的内容</span><span class="sxs-lookup"><span data-stu-id="f833c-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="f833c-113">使用 Microsoft 团队工具包创建适用于 Visual Studio Code 的应用程序项目</span><span class="sxs-lookup"><span data-stu-id="f833c-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="f833c-114">确定与通道和组选项卡相关的一些应用程序清单属性和基架</span><span class="sxs-lookup"><span data-stu-id="f833c-114">Identify some of the app manifest properties and scaffolding relevant to channel and group tabs</span></span>
> * <span data-ttu-id="f833c-115">在本地托管应用程序</span><span class="sxs-lookup"><span data-stu-id="f833c-115">Host an app locally</span></span>
> * <span data-ttu-id="f833c-116">创建选项卡内容</span><span class="sxs-lookup"><span data-stu-id="f833c-116">Create tab content</span></span>
> * <span data-ttu-id="f833c-117">创建选项卡的配置页的内容</span><span class="sxs-lookup"><span data-stu-id="f833c-117">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="f833c-118">允许配置和安装选项卡</span><span class="sxs-lookup"><span data-stu-id="f833c-118">Allow a tab to be configured and installed</span></span>
> * <span data-ttu-id="f833c-119">提供建议的选项卡名称</span><span class="sxs-lookup"><span data-stu-id="f833c-119">Provide a suggested tab name</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="f833c-120">1. 创建您的应用程序项目</span><span class="sxs-lookup"><span data-stu-id="f833c-120">1. Create your app project</span></span>

<span data-ttu-id="f833c-121">Microsoft 团队工具包可帮助您设置与通道和组选项卡相关的应用程序清单和基架，包括显示 "Hello，World！" 的基本配置页和内容页。</span><span class="sxs-lookup"><span data-stu-id="f833c-121">The Microsoft Teams Toolkit helps you set up the app manifest and scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="f833c-122">消息。</span><span class="sxs-lookup"><span data-stu-id="f833c-122">message.</span></span>

> [!TIP]
> <span data-ttu-id="f833c-123">如果之前尚未创建团队应用程序项目，您可能会发现，请按照 [以下说明](../build-your-first-app/build-and-run.md) 更详细地说明项目。</span><span class="sxs-lookup"><span data-stu-id="f833c-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队**"， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **创建新的团队应用**"。
1. <span data-ttu-id="f833c-125">为你的团队应用输入名称。</span><span class="sxs-lookup"><span data-stu-id="f833c-125">Enter a name for your Teams app.</span></span> <span data-ttu-id="f833c-126"> (这是您的应用程序的默认名称，也是本地计算机上的应用程序项目目录的名称。 ) </span><span class="sxs-lookup"><span data-stu-id="f833c-126">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="f833c-127">在 " **添加功能** " 屏幕上，依次选择 **"选项卡" 和 "** **团队通道" 选项卡**。</span><span class="sxs-lookup"><span data-stu-id="f833c-127">On the **Add capabilities** screen, select **Tab** then **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="f833c-128">选择屏幕底部的 " **完成** " 以配置项目。</span><span class="sxs-lookup"><span data-stu-id="f833c-128">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="f833c-129">2. 确定相关的应用程序项目组件</span><span class="sxs-lookup"><span data-stu-id="f833c-129">2. Identify relevant app project components</span></span>

<span data-ttu-id="f833c-130">大多数应用程序清单和基架是在使用团队工具包创建项目时自动设置的。</span><span class="sxs-lookup"><span data-stu-id="f833c-130">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="f833c-131">我们来看看构建通道和组选项卡的主要组件。</span><span class="sxs-lookup"><span data-stu-id="f833c-131">Let's look at the main components for building a channel and group tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="f833c-132">应用程序清单</span><span class="sxs-lookup"><span data-stu-id="f833c-132">App manifest</span></span>

<span data-ttu-id="f833c-133">应用程序清单中的以下代码段显示了 [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs) ，其中包括与通道和组选项卡相关的属性和默认值。</span><span class="sxs-lookup"><span data-stu-id="f833c-133">The following snippet from the app manifest shows [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs), which includes the properties and default values relevant to channel and group tabs.</span></span>

```JSON
"configurableTabs": [
    {
        "configurationUrl": "{baseUrl0}/config",
        "canUpdateConfiguration": true,
        "scopes": [
            "team",
            "groupchat"
        ]
    }
],
```

* <span data-ttu-id="f833c-134">`configurationUrl`：您的选项卡配置页的主机 URL (必须是 HTTPS) 。</span><span class="sxs-lookup"><span data-stu-id="f833c-134">`configurationUrl`: The host URL for your tab configuration page (must be HTTPS).</span></span>
* <span data-ttu-id="f833c-135">`canUpdateConfiguration`：如果设置为 `true` ，则用户可以更改选项卡设置、重命名选项卡或将其从频道或聊天中删除。</span><span class="sxs-lookup"><span data-stu-id="f833c-135">`canUpdateConfiguration`: If set to `true`, users can change tab settings, rename the tab, or remove it from a channel or chat.</span></span>
* <span data-ttu-id="f833c-136">`scopes`：指定用户是否可以在频道中安装应用程序 (`team`) 和聊天 (`groupchat`) 。</span><span class="sxs-lookup"><span data-stu-id="f833c-136">`scopes`: Specifies if users can install the app in channels (`team`) and chats (`groupchat`).</span></span> <span data-ttu-id="f833c-137">至少需要一个值。</span><span class="sxs-lookup"><span data-stu-id="f833c-137">At least one value is required.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="f833c-138">应用程序基架</span><span class="sxs-lookup"><span data-stu-id="f833c-138">App scaffolding</span></span>

<span data-ttu-id="f833c-139">应用程序基架提供一个 `TabConfig.js` 文件，该文件位于 `src/components` 项目目录中，用于呈现您的选项卡的配置页面即将在此) 中 (详细信息。</span><span class="sxs-lookup"><span data-stu-id="f833c-139">The app scaffolding provides a `TabConfig.js` file, located in the `src/components` directory of your project, for rendering your tab's configuration page (more on this soon).</span></span>

## <a name="3-run-your-app"></a><span data-ttu-id="f833c-140">3. 运行您的应用程序</span><span class="sxs-lookup"><span data-stu-id="f833c-140">3. Run your app</span></span>

<span data-ttu-id="f833c-141">在时间方面，你将在本地构建和运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="f833c-141">In the interest of time, you'll build and run your app locally.</span></span>

1. <span data-ttu-id="f833c-142">在终端中，转到您的应用程序项目的根目录并运行该目录 `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="f833c-142">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="f833c-143">运行 `npm start` 。</span><span class="sxs-lookup"><span data-stu-id="f833c-143">Run `npm start`.</span></span>

<span data-ttu-id="f833c-144">完成后，已 **成功编译了！**</span><span class="sxs-lookup"><span data-stu-id="f833c-144">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="f833c-145">终端中的邮件。</span><span class="sxs-lookup"><span data-stu-id="f833c-145">message in the terminal.</span></span>

## <a name="4-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="f833c-146">4. 设置应用程序的安全隧道</span><span class="sxs-lookup"><span data-stu-id="f833c-146">4. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="f833c-147">出于测试目的，让我们将您的选项卡托管在本地 web 服务器上 (端口 3000) 。</span><span class="sxs-lookup"><span data-stu-id="f833c-147">For testing purposes, let's host your tab on a local web server (port 3000).</span></span>

1. <span data-ttu-id="f833c-148">在终端中，运行 `ngrok http 3000` 。</span><span class="sxs-lookup"><span data-stu-id="f833c-148">In a terminal, run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="f833c-149">复制你提供的 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="f833c-149">Copy the HTTPS URL you're provided.</span></span>
1. <span data-ttu-id="f833c-150">在 `.publish` 目录中，打开 `Development.env` 。</span><span class="sxs-lookup"><span data-stu-id="f833c-150">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="f833c-151">将 `baseUrl0` 值替换为复制的 URL。</span><span class="sxs-lookup"><span data-stu-id="f833c-151">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="f833c-152"> (例如，改 `baseUrl0=http://localhost:3000` 为 `baseUrl0=https://85528b2b3ca5.ngrok.io` 。 ) </span><span class="sxs-lookup"><span data-stu-id="f833c-152">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="f833c-153">你的应用程序清单指向你承载该选项卡的位置。</span><span class="sxs-lookup"><span data-stu-id="f833c-153">Your app manifest is pointing to where you're hosting the tab.</span></span>

## <a name="5-customize-your-tab-content-page"></a><span data-ttu-id="f833c-154">5. 自定义 "选项卡内容" 页</span><span class="sxs-lookup"><span data-stu-id="f833c-154">5. Customize your tab content page</span></span>

<span data-ttu-id="f833c-155">在目录中打开应用程序清单 (`manifest.json`) ， `.publish` 并在中设置以下属性 [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) 来定义您的选项卡的内容页面。</span><span class="sxs-lookup"><span data-stu-id="f833c-155">Open the app manifest (`manifest.json`) in the `.publish` directory and set the following properties in [`staticTabs`](../resources/schema/manifest-schema.md#statictabs), which defines your tab's content page.</span></span>

```JSON
"staticTabs": [
    {
        "entityId": "index",
        "name": "My Contacts",
        "contentUrl": "{baseUrl0}/tab",
        "scopes": [ "personal" ]
    }
],
```

<span data-ttu-id="f833c-156">使用与您的组织相关的信息复制和更新以下代码段，如果有时间，请使用代码。</span><span class="sxs-lookup"><span data-stu-id="f833c-156">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="f833c-157">转到 `src/components` 目录并打开 `Tab.js` 。</span><span class="sxs-lookup"><span data-stu-id="f833c-157">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="f833c-158">找到 `render()` 函数并将内容粘贴 (中， `return()` 如) 所示。</span><span class="sxs-lookup"><span data-stu-id="f833c-158">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="f833c-159">将以下规则添加到 `App.css` ，无论使用哪个主题，电子邮件链接更易于阅读。</span><span class="sxs-lookup"><span data-stu-id="f833c-159">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="6-create-your-tab-configuration-page"></a><span data-ttu-id="f833c-160">6. 创建选项卡配置页</span><span class="sxs-lookup"><span data-stu-id="f833c-160">6. Create your tab configuration page</span></span>

<span data-ttu-id="f833c-161">频道或聊天中的每个选项卡都有一个配置页面，其中包含至少一个安装选项的模式，在用户安装您的应用程序时显示。</span><span class="sxs-lookup"><span data-stu-id="f833c-161">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users install your app.</span></span> <span data-ttu-id="f833c-162">默认情况下，配置页面会询问用户是否要在安装该选项卡时通知频道或聊天。</span><span class="sxs-lookup"><span data-stu-id="f833c-162">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="f833c-163">将一些内容添加到您的配置页面。</span><span class="sxs-lookup"><span data-stu-id="f833c-163">Add some content to your configuration page.</span></span> <span data-ttu-id="f833c-164">转到项目的 `src/components` 目录，打开 `TabConfig.js` ，并在 (中插入一些内容， `return()` 如) 所示。</span><span class="sxs-lookup"><span data-stu-id="f833c-164">Go to your project's `src/components` directory, open `TabConfig.js`, and insert some content inside `return()` (as shown).</span></span>

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
> <span data-ttu-id="f833c-165">至少，在此页面上提供有关您的应用程序的一些简要信息，因为这可能是用户首次了解它。</span><span class="sxs-lookup"><span data-stu-id="f833c-165">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="f833c-166">您还可以包括自定义配置选项或 [身份验证工作流](../tabs/how-to/authentication/auth-aad-sso.md)，这在选项卡配置页上很常见。</span><span class="sxs-lookup"><span data-stu-id="f833c-166">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="7-allow-the-tab-to-be-configured-and-installed"></a><span data-ttu-id="f833c-167">7. 允许配置和安装该选项卡</span><span class="sxs-lookup"><span data-stu-id="f833c-167">7. Allow the tab to be configured and installed</span></span>

<span data-ttu-id="f833c-168">若要使用户能够成功配置和安装该选项卡，您必须将 [设置的安全主机 URL](#4-set-up-a-secure-tunnel-to-your-app) 添加到配置页面组件。</span><span class="sxs-lookup"><span data-stu-id="f833c-168">For users to successfully configure and install the tab, you must add the [secure host URL you set up](#4-set-up-a-secure-tunnel-to-your-app) to the configuration page component.</span></span>

<span data-ttu-id="f833c-169">转到 `TabConfig.js` 并找到 `microsoftTeams.settings.setSettings` 。</span><span class="sxs-lookup"><span data-stu-id="f833c-169">Go to `TabConfig.js` and locate `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="f833c-170">对于 `"contentUrl"` ，将 URL 的一部分替换为 `localhost:3000` 您在其中承载选项卡内容的域 (如) 所示。</span><span class="sxs-lookup"><span data-stu-id="f833c-170">For `"contentUrl"`, replace the `localhost:3000` part of the URL with the domain where you're hosting the tab content (as shown).</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
});
```

<span data-ttu-id="f833c-171">此外，请确保 `microsoftTeams.settings.setValidityState(true);` 。</span><span class="sxs-lookup"><span data-stu-id="f833c-171">Also, make sure that `microsoftTeams.settings.setValidityState(true);`.</span></span> <span data-ttu-id="f833c-172">默认情况下，它是默认设置，但如果设置为 `false` ，将禁用 "配置" 页上的 " **保存** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="f833c-172">It is by default, but if set to `false`, the **Save** button is disabled on the configuration page.</span></span>

## <a name="8-provide-a-suggested-tab-name"></a><span data-ttu-id="f833c-173">8. 提供建议的选项卡名称</span><span class="sxs-lookup"><span data-stu-id="f833c-173">8. Provide a suggested tab name</span></span>

<span data-ttu-id="f833c-174">在安装用于个人用途的选项卡时，显示名称是 `name` `staticTabs` 应用部件清单的部分中的属性 (例如，我的 **联系人**) 。</span><span class="sxs-lookup"><span data-stu-id="f833c-174">When you install a tab for personal use, the display name is the `name` property in the `staticTabs` portion of the app manifest (for example, **My Contacts**).</span></span> <span data-ttu-id="f833c-175">安装通道选项卡时，默认情况下，应用名称会显示 (例如， **第一个应用程序**) 。</span><span class="sxs-lookup"><span data-stu-id="f833c-175">When you install a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="f833c-176">这可能会很好，具体取决于您调用应用程序的内容，但您可能希望提供一个名称，以便在组协作的上下文中更有意义 (例如， **工作组联系人**) 。</span><span class="sxs-lookup"><span data-stu-id="f833c-176">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

<span data-ttu-id="f833c-177">在中 `TabConfig.js` ，返回到 `microsoftTeams.settings.setSettings` 。</span><span class="sxs-lookup"><span data-stu-id="f833c-177">In `TabConfig.js`, go back to `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="f833c-178">添加 `suggestedDisplayName` 默认情况下要显示的选项卡名称的属性 (如) 所示。</span><span class="sxs-lookup"><span data-stu-id="f833c-178">Add the `suggestedDisplayName` property with the tab name you want to display by default (as shown).</span></span> <span data-ttu-id="f833c-179">使用提供的名称或创建自己的名称。</span><span class="sxs-lookup"><span data-stu-id="f833c-179">Use the provided name or create your own.</span></span> <span data-ttu-id="f833c-180">请记住，在清单中，如果您允许用户根据需要更改名称。</span><span class="sxs-lookup"><span data-stu-id="f833c-180">Remember, in the manifest you're allowing users to change the name if they want.</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="9-view-the-tab"></a><span data-ttu-id="f833c-181">9. 查看选项卡</span><span class="sxs-lookup"><span data-stu-id="f833c-181">9. View the tab</span></span>

<span data-ttu-id="f833c-182">若要查看您的选项卡的配置和内容页，必须在频道或聊天中安装它。</span><span class="sxs-lookup"><span data-stu-id="f833c-182">To see your tab's configuration and content pages, you must install it in a channel or chat.</span></span>

1. <span data-ttu-id="f833c-183">在 "团队客户端" 中，选择 " **应用**"。</span><span class="sxs-lookup"><span data-stu-id="f833c-183">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="f833c-184">选择 " **上载自定义应用程序** "，然后选择您的应用程序 `Development.zip` 。</span><span class="sxs-lookup"><span data-stu-id="f833c-184">Select **Upload a custom app** and choose your app's `Development.zip`.</span></span>
1. <span data-ttu-id="f833c-185">选择 " **添加到团队** " 或 " **添加到聊天** "，找到可用于测试的频道或聊天。</span><span class="sxs-lookup"><span data-stu-id="f833c-185">Choose **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="f833c-186">选择 **"设置选项卡"**。将显示 "配置" 页。</span><span class="sxs-lookup"><span data-stu-id="f833c-186">Select **Set up a tab**. The configuration page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="频道选项卡配置页的屏幕截图。":::
1. <span data-ttu-id="f833c-188">选择 " **保存** " 以配置选项卡。将显示内容。</span><span class="sxs-lookup"><span data-stu-id="f833c-188">Select **Save** to configure the tab. The content displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="包含静态内容视图的频道选项卡的屏幕截图。":::

## <a name="well-done"></a><span data-ttu-id="f833c-190">干的好</span><span class="sxs-lookup"><span data-stu-id="f833c-190">Well done</span></span>

<span data-ttu-id="f833c-191">恭喜你！</span><span class="sxs-lookup"><span data-stu-id="f833c-191">Congratulations!</span></span> <span data-ttu-id="f833c-192">您有一个包含选项卡的团队应用程序，用于在频道和聊天中显示有用的内容。</span><span class="sxs-lookup"><span data-stu-id="f833c-192">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="f833c-193">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="f833c-193">Learn more</span></span>

* <span data-ttu-id="f833c-194">[使用 Sso 对选项卡用户进行身份验证](../tabs/how-to/authentication/auth-aad-sso.md)：如果您仅希望授权用户查看您的选项卡，请通过 Azure Active DIRECTORY (AD) 设置单一登录 (SSO) 。</span><span class="sxs-lookup"><span data-stu-id="f833c-194">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="f833c-195">[从现有 web 应用或网页嵌入内容](../tabs/how-to/add-tab.md#tab-requirements)：我们向您介绍了如何为个人选项卡创建新内容，但您也可以从外部 URL 加载内容。</span><span class="sxs-lookup"><span data-stu-id="f833c-195">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="f833c-196">[为您的选项卡创建无缝体验](../tabs/design/tabs.md)：有关设计团队选项卡的建议指南，请参阅。</span><span class="sxs-lookup"><span data-stu-id="f833c-196">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="f833c-197">[为移动设备构建选项卡](../tabs/design/tabs-mobile.md)：了解如何为电话和平板电脑开发选项卡。</span><span class="sxs-lookup"><span data-stu-id="f833c-197">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="f833c-198">创建不带工具箱的选项卡</span><span class="sxs-lookup"><span data-stu-id="f833c-198">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="f833c-199">下一课</span><span class="sxs-lookup"><span data-stu-id="f833c-199">Next lesson</span></span>

<span data-ttu-id="f833c-200">您知道如何构建协作选项卡。</span><span class="sxs-lookup"><span data-stu-id="f833c-200">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="f833c-201">想要尝试构建不同种类的团队应用吗？</span><span class="sxs-lookup"><span data-stu-id="f833c-201">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f833c-202">构建 bot</span><span class="sxs-lookup"><span data-stu-id="f833c-202">Build a bot</span></span>](../build-your-first-app/build-bot.md)
