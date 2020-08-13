---
title: 为团队创建通道选项卡
author: heath-hamilton
description: 了解如何在您的首个 Microsoft 团队应用程序中构建 "频道" 选项卡。
ms.topic: tutorial
ms.openlocfilehash: f0c59328219b5611efc02c9eb04db6fdc517ca08
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651925"
---
# <a name="create-a-channel-tab-for-teams"></a><span data-ttu-id="0f390-103">为团队创建通道选项卡</span><span class="sxs-lookup"><span data-stu-id="0f390-103">Create a channel tab for Teams</span></span>

<span data-ttu-id="0f390-104">在本教程中，你将构建一个基本的*频道选项卡*，一个用于团队频道或聊天的全屏内容页面。</span><span class="sxs-lookup"><span data-stu-id="0f390-104">In this tutorial, you'll build a basic *channel tab*, a full-screen content page for a team channel or chat.</span></span> <span data-ttu-id="0f390-105">与 "个人" 选项卡不同，用户可以配置频道选项卡的某些方面 (例如，重命名选项卡，使其通道) 有意义。</span><span class="sxs-lookup"><span data-stu-id="0f390-105">Unlike a personal tab, users can configure some aspects of a channel tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0f390-106">准备工作</span><span class="sxs-lookup"><span data-stu-id="0f390-106">Before you begin</span></span>

<span data-ttu-id="0f390-107">您需要一个基本运行的应用程序才能开始使用。</span><span class="sxs-lookup"><span data-stu-id="0f390-107">You need a basic running app to get started.</span></span> <span data-ttu-id="0f390-108">如果没有，请按照生成中的说明操作[，并运行你的团队首个应用](build-and-run-with-toolkit.md)。</span><span class="sxs-lookup"><span data-stu-id="0f390-108">If you don't have one, follow the instructions at [build and run your Teams first app](build-and-run-with-toolkit.md).</span></span> <span data-ttu-id="0f390-109">在创建应用程序项目时，请仅选择 "**组" 或 "团队通道" 选项卡**选项。</span><span class="sxs-lookup"><span data-stu-id="0f390-109">When you create your app project, choose only the **Group or Teams channel tab** option.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="0f390-110">您的分配</span><span class="sxs-lookup"><span data-stu-id="0f390-110">Your assignment</span></span>

<span data-ttu-id="0f390-111">以前，你的组织创建了一个 "团队" 选项卡，其中包含有关如何联系重要功能 (技术支持、人力资源等 ) 的信息。</span><span class="sxs-lookup"><span data-stu-id="0f390-111">Not long ago, your organization created a Teams tab with information on how to contact important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="0f390-112">但是，由于该选项卡的作用范围仅供个人使用，因此每个用户都必须安装该选项卡，才能看到它，并且采用低于预期。</span><span class="sxs-lookup"><span data-stu-id="0f390-112">However, since the tab was scoped only for personal use, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="0f390-113">换句话说，工作线程太多仍不知道如何联系技术支持人员。</span><span class="sxs-lookup"><span data-stu-id="0f390-113">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="0f390-114">您可以通过构建通道选项卡使此信息更易于查找，这将消除要求每个人安装应用程序的负担。</span><span class="sxs-lookup"><span data-stu-id="0f390-114">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="0f390-115">相反，一个用户可以在频道或聊天中安装该选项卡，以了解整个组的好处。</span><span class="sxs-lookup"><span data-stu-id="0f390-115">Instead, one user can install the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="0f390-116">你将了解的内容</span><span class="sxs-lookup"><span data-stu-id="0f390-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="0f390-117">标识与通道选项卡相关的应用程序清单和基架组件</span><span class="sxs-lookup"><span data-stu-id="0f390-117">Identify the app manifest and scaffolding components relevant to channel tabs</span></span>
> * <span data-ttu-id="0f390-118">创建选项卡的内容</span><span class="sxs-lookup"><span data-stu-id="0f390-118">Create content for your tab</span></span>
> * <span data-ttu-id="0f390-119">创建选项卡的配置页的内容</span><span class="sxs-lookup"><span data-stu-id="0f390-119">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="0f390-120">允许配置和安装该选项卡</span><span class="sxs-lookup"><span data-stu-id="0f390-120">Allow the tab to be configured and installed</span></span>
> * <span data-ttu-id="0f390-121">提供建议的选项卡名称</span><span class="sxs-lookup"><span data-stu-id="0f390-121">Provide a suggested tab name</span></span>

## <a name="identify-relevant-app-manifest-and-scaffolding-components"></a><span data-ttu-id="0f390-122">确定相关的应用程序清单和基架组件</span><span class="sxs-lookup"><span data-stu-id="0f390-122">Identify relevant app manifest and scaffolding components</span></span>

<span data-ttu-id="0f390-123">大多数频道选项卡应用程序基架和清单在您使用团队工具包创建项目时自动设置。</span><span class="sxs-lookup"><span data-stu-id="0f390-123">Much of the channel tab app scaffolding and manifest is set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="0f390-124">我们来看看构建 "频道" 选项卡的主要组件。</span><span class="sxs-lookup"><span data-stu-id="0f390-124">Let's look at the main components for building a channel tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="0f390-125">应用程序清单</span><span class="sxs-lookup"><span data-stu-id="0f390-125">App manifest</span></span>

<span data-ttu-id="0f390-126">应用程序清单中的以下代码段显示了 [`configurableTabs`](../../resources/schema/manifest-schema.md#configurabletabs) ，其中包括与频道选项卡相关的属性和默认值。</span><span class="sxs-lookup"><span data-stu-id="0f390-126">The following snippet from the app manifest shows [`configurableTabs`](../../resources/schema/manifest-schema.md#configurabletabs), which includes the properties and default values relevant to channel tabs.</span></span>

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

* <span data-ttu-id="0f390-127">`configurationUrl`：您的选项卡配置页的主机 URL (必须是 HTTPS) 。</span><span class="sxs-lookup"><span data-stu-id="0f390-127">`configurationUrl`: The host URL for your tab configuration page (must be HTTPS).</span></span>
* <span data-ttu-id="0f390-128">`canUpdateConfiguration`：如果设置为 `true` ，则用户可以更改选项卡设置、重命名选项卡或将其从频道或聊天中删除。</span><span class="sxs-lookup"><span data-stu-id="0f390-128">`canUpdateConfiguration`: If set to `true`, users can change tab settings, rename the tab, or remove it from a channel or chat.</span></span>
* <span data-ttu-id="0f390-129">`scopes`：指定用户是否可以在频道中安装应用程序 (`team`) 和聊天 (`groupchat`) 。</span><span class="sxs-lookup"><span data-stu-id="0f390-129">`scopes`: Specifies if users can install the app in channels (`team`) and chats (`groupchat`).</span></span> <span data-ttu-id="0f390-130">至少需要一个值。</span><span class="sxs-lookup"><span data-stu-id="0f390-130">At least one value is required.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="0f390-131">应用程序基架</span><span class="sxs-lookup"><span data-stu-id="0f390-131">App scaffolding</span></span>

<span data-ttu-id="0f390-132">应用程序基架提供一个 `TabConfig.js` 文件，该文件位于 `src/components` 项目目录中，用于呈现您的选项卡的配置页面即将在此) 中 (详细信息。</span><span class="sxs-lookup"><span data-stu-id="0f390-132">The app scaffolding provides a `TabConfig.js` file, located in the `src/components` directory of your project, for rendering your tab's configuration page (more on this soon).</span></span>

## <a name="create-your-tab-content"></a><span data-ttu-id="0f390-133">创建选项卡内容</span><span class="sxs-lookup"><span data-stu-id="0f390-133">Create your tab content</span></span>

<span data-ttu-id="0f390-134">打开您的应用程序清单 (`manifest.json`) 并在中设置以下属性 [`staticTabs`](../../resources/schema/manifest-schema.md#statictabs) ，其中定义了您的选项卡的内容页面。</span><span class="sxs-lookup"><span data-stu-id="0f390-134">Open your app manifest (`manifest.json`) and set the following properties in [`staticTabs`](../../resources/schema/manifest-schema.md#statictabs), which defines your tab's content page.</span></span>

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

<span data-ttu-id="0f390-135">使用与您的组织相关的信息复制和更新以下代码段，如果有时间，请使用代码。</span><span class="sxs-lookup"><span data-stu-id="0f390-135">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="0f390-136">转到 `src/components` 目录并打开 `Tab.js` 。</span><span class="sxs-lookup"><span data-stu-id="0f390-136">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="0f390-137">找到 `render()` 函数并将内容粘贴 (中， `return()` 如) 所示。</span><span class="sxs-lookup"><span data-stu-id="0f390-137">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="0f390-138">将以下规则添加到 `App.css` ，无论使用哪个主题，电子邮件链接更易于阅读。</span><span class="sxs-lookup"><span data-stu-id="0f390-138">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
  a {
    color: inherit;
  }
```

## <a name="create-your-tab-configuration-page"></a><span data-ttu-id="0f390-139">创建选项卡配置页</span><span class="sxs-lookup"><span data-stu-id="0f390-139">Create your tab configuration page</span></span>

<span data-ttu-id="0f390-140">每个频道选项卡都有一个配置页面，其中包含至少一个安装选项的模式，在安装应用程序时将显示该选项。</span><span class="sxs-lookup"><span data-stu-id="0f390-140">Every channel tab has a configuration page, a modal with at least one setup option that displays when installing the app.</span></span> <span data-ttu-id="0f390-141">默认情况下，配置页面会询问用户是否要在安装该选项卡时通知频道或聊天。</span><span class="sxs-lookup"><span data-stu-id="0f390-141">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="0f390-142">将一些内容添加到您的配置页面。</span><span class="sxs-lookup"><span data-stu-id="0f390-142">Add some content to your configuration page.</span></span> <span data-ttu-id="0f390-143">转到项目的 `src/components` 目录，打开 `TabConfig.js` ，并在 (中插入一些内容， `return()` 如) 所示。</span><span class="sxs-lookup"><span data-stu-id="0f390-143">Go to your project's `src/components` directory, open `TabConfig.js`, and insert some content inside `return()` (as shown).</span></span>

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
> <span data-ttu-id="0f390-144">至少，在此页面上提供有关您的应用程序的一些简要信息，因为这可能是用户首次了解它。</span><span class="sxs-lookup"><span data-stu-id="0f390-144">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="0f390-145">您还可以包括自定义配置选项或[身份验证工作流](../../tabs/how-to/authentication/auth-aad-sso.md)，这在选项卡配置页上很常见。</span><span class="sxs-lookup"><span data-stu-id="0f390-145">You also could include custom configuration options or an [authentication workflow](../../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="allow-the-tab-to-be-configured-and-installed"></a><span data-ttu-id="0f390-146">允许配置和安装该选项卡</span><span class="sxs-lookup"><span data-stu-id="0f390-146">Allow the tab to be configured and installed</span></span>

<span data-ttu-id="0f390-147">若要使用户能够成功配置和安装 "频道" 选项卡，您必须添加在[创建和运行第一个应用程序](build-and-run-with-toolkit.md)到 "配置" 页面组件时设置的主机 URL。</span><span class="sxs-lookup"><span data-stu-id="0f390-147">For users to successfully configure and install the channel tab, you must add the host URL you set up when [creating and running your first app](build-and-run-with-toolkit.md) to the configuration page component.</span></span>

<span data-ttu-id="0f390-148">转到 `TabConfig.js` 并找到 `microsoftTeams.settings.setSettings` 。</span><span class="sxs-lookup"><span data-stu-id="0f390-148">Go to `TabConfig.js` and locate `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="0f390-149">对于 `"contentUrl"` ，将 URL 的一部分替换为 `localhost:3000` 您在其中承载选项卡内容的域 (如) 所示。</span><span class="sxs-lookup"><span data-stu-id="0f390-149">For `"contentUrl"`, replace the `localhost:3000` part of the URL with the domain where you're hosting the tab content (as shown).</span></span>

```JavaScript
    microsoftTeams.settings.setSettings({
      "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
    });
```

<span data-ttu-id="0f390-150">此外，请确保 `microsoftTeams.settings.setValidityState(true);` 。</span><span class="sxs-lookup"><span data-stu-id="0f390-150">Also, make sure that `microsoftTeams.settings.setValidityState(true);`.</span></span> <span data-ttu-id="0f390-151">默认情况下，它是默认设置，但如果设置为 `false` ，将禁用 "配置" 页上的 "**保存**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="0f390-151">It is by default, but if set to `false`, the **Save** button is disabled on the configuration page.</span></span>

## <a name="provide-a-suggested-tab-name"></a><span data-ttu-id="0f390-152">提供建议的选项卡名称</span><span class="sxs-lookup"><span data-stu-id="0f390-152">Provide a suggested tab name</span></span>

<span data-ttu-id="0f390-153">在安装用于个人用途的选项卡时，显示名称是 `name` `staticTabs` 应用部件清单 (部分中的属性，例如，"我的**联系人**") 。</span><span class="sxs-lookup"><span data-stu-id="0f390-153">When you install a tab for personal use, the display name is the `name` property in the `staticTabs` portion of of the app manifest (for example, **My Contacts**).</span></span> <span data-ttu-id="0f390-154">安装通道选项卡时，默认情况下，应用名称会显示 (例如，**第一个应用程序**) 。</span><span class="sxs-lookup"><span data-stu-id="0f390-154">When you install a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="0f390-155">这可能会很好，具体取决于您调用应用程序的内容，但您可能希望提供一个名称，以便在组协作的上下文中更有意义 (例如，**工作组联系人**) 。</span><span class="sxs-lookup"><span data-stu-id="0f390-155">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

<span data-ttu-id="0f390-156">在中 `TabConfig.js` ，返回到 `microsoftTeams.settings.setSettings` 。</span><span class="sxs-lookup"><span data-stu-id="0f390-156">In `TabConfig.js`, go back to `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="0f390-157">添加 `suggestedDisplayName` 默认情况下要显示的选项卡名称的属性 (如) 所示。</span><span class="sxs-lookup"><span data-stu-id="0f390-157">Add the `suggestedDisplayName` property with the tab name you want to display by default (as shown).</span></span> <span data-ttu-id="0f390-158">使用提供的名称或创建自己的名称。</span><span class="sxs-lookup"><span data-stu-id="0f390-158">Use the provided name or create your own.</span></span> <span data-ttu-id="0f390-159">请记住，在清单中，如果您允许用户根据需要更改名称。</span><span class="sxs-lookup"><span data-stu-id="0f390-159">Remember, in the manifest you're allowing users to change the name if they want.</span></span>

```JavaScript
    microsoftTeams.settings.setSettings({
      "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
      "suggestedDisplayName": "Team Contacts"
    });
```

## <a name="view-the-channel-tab"></a><span data-ttu-id="0f390-160">查看通道选项卡</span><span class="sxs-lookup"><span data-stu-id="0f390-160">View the channel tab</span></span>

<span data-ttu-id="0f390-161">若要查看频道选项卡的配置和内容页，必须在频道或聊天中安装它。</span><span class="sxs-lookup"><span data-stu-id="0f390-161">To see your channel tab's configuration and content pages, you must install it in a channel or chat.</span></span>

1. <span data-ttu-id="0f390-162">在 "团队客户端" 中，选择 "**应用**"。</span><span class="sxs-lookup"><span data-stu-id="0f390-162">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="0f390-163">选择 "**上载自定义应用程序**"，然后选择您的应用程序 `Development.zip` 。</span><span class="sxs-lookup"><span data-stu-id="0f390-163">Select **Upload a custom app** and choose your app's `Development.zip`.</span></span>
1. <span data-ttu-id="0f390-164">选择 "**添加到团队**" 或 "**添加到聊天**"，找到可用于测试的频道或聊天。</span><span class="sxs-lookup"><span data-stu-id="0f390-164">Choose **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="0f390-165">选择 **"设置选项卡"**。将显示 "配置" 页。</span><span class="sxs-lookup"><span data-stu-id="0f390-165">Select **Set up a tab**. The configuration page displays.</span></span>

:::image type="content" source="../doc-links/images/channel-tab-tutorial-content.png" alt-text="频道选项卡配置页的示例屏幕截图":::

<span data-ttu-id="0f390-167">选择 "**保存**" 以配置选项卡后，将显示内容。</span><span class="sxs-lookup"><span data-stu-id="0f390-167">Once you select **Save** to configure the tab, the content displays.</span></span>

![带有静态内容的频道选项卡的示例屏幕截图](../doc-links/images/channel-tab-tutorial-content-installed.png)

## <a name="well-done"></a><span data-ttu-id="0f390-169">干的好</span><span class="sxs-lookup"><span data-stu-id="0f390-169">Well done</span></span>

<span data-ttu-id="0f390-170">恭喜你！</span><span class="sxs-lookup"><span data-stu-id="0f390-170">Congratulations!</span></span> <span data-ttu-id="0f390-171">您有一个带有通道选项卡的团队应用程序，用于在频道和聊天中显示有用的内容。</span><span class="sxs-lookup"><span data-stu-id="0f390-171">You have a Teams app with a channel tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="0f390-172">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="0f390-172">Learn more</span></span>

* <span data-ttu-id="0f390-173">[使用 Sso 对选项卡用户进行身份验证](../../tabs/how-to/authentication/auth-aad-sso.md)：如果您仅希望授权用户查看您的选项卡，请通过 Azure Active DIRECTORY (AD) 设置单一登录 (SSO) 。</span><span class="sxs-lookup"><span data-stu-id="0f390-173">[Authenticate tab users with SSO](../../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="0f390-174">[从现有 web 应用或网页嵌入内容](../../tabs/how-to/add-tab.md#tab-requirements)：我们向您介绍了如何为个人选项卡创建新内容，但您也可以从外部 URL 加载内容。</span><span class="sxs-lookup"><span data-stu-id="0f390-174">[Embed content from an existing web app or webpage](../../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="0f390-175">[为您的选项卡创建无缝体验](../../tabs/design/tabs.md)：有关设计团队选项卡的建议指南，请参阅。</span><span class="sxs-lookup"><span data-stu-id="0f390-175">[Create a seamless experience for your tab](../../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="0f390-176">[为移动设备构建选项卡](../../tabs/design/tabs-mobile.md)：了解如何为智能手机和平板电脑开发选项卡。</span><span class="sxs-lookup"><span data-stu-id="0f390-176">[Build tabs for mobile](../../tabs/design/tabs-mobile.md): Understand how to develop tabs for smartphones and tablets.</span></span>
