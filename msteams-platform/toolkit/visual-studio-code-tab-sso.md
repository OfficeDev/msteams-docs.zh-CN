---
title: 使用选项卡的身份验证Teams Toolkit Visual Studio Code单一登录身份验证
description: 生成一个支持单一登录和 Microsoft Graph直接在Visual Studio Code内调用的Microsoft Teams Toolkit
keywords: teams visual studio code toolkit tabs sso graph authentication Azure identity platform
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: daf9a1b0bb64fee9584d0f58d749cf2b1ccaa4ef
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018423"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a><span data-ttu-id="6426e-104">使用选项卡的身份验证Teams Toolkit Visual Studio Code单一登录身份验证</span><span class="sxs-lookup"><span data-stu-id="6426e-104">Single sign-on authentication with Teams Toolkit and Visual Studio Code for tabs</span></span>

<span data-ttu-id="6426e-105">利用Microsoft Teams Toolkit，你可以直接在 (内为选项卡) 创建单一登录 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="6426e-105">The Microsoft Teams Toolkit enables you to create single sign-on (SSO) authentication  for tab apps directly within Visual Studio Code.</span></span> <span data-ttu-id="6426e-106">该工具包将指导你完成该过程，并提供你所需的一切，包括在 Azure 门户Microsoft 标识平台你的应用注册。</span><span class="sxs-lookup"><span data-stu-id="6426e-106">The toolkit guides you through the process and provides everything you need including provisioning your Microsoft identity platform registration in the Azure portal.</span></span>

## <a name="get-started--create-a-project"></a><span data-ttu-id="6426e-107">入门 — 创建项目</span><span class="sxs-lookup"><span data-stu-id="6426e-107">Get started — create a project</span></span>

1. <span data-ttu-id="6426e-108">在工具包中创建新项目。</span><span class="sxs-lookup"><span data-stu-id="6426e-108">Create a new project in the toolkit.</span></span>
1. <span data-ttu-id="6426e-109">选择选项卡作为你要创建的扩展类型。</span><span class="sxs-lookup"><span data-stu-id="6426e-109">Select tab as the type of extension you'd like to create.</span></span>
1. <span data-ttu-id="6426e-110">选择支持 SSO 的选项。</span><span class="sxs-lookup"><span data-stu-id="6426e-110">Select the option to support SSO.</span></span>

> [!TIP]
> <span data-ttu-id="6426e-111">安装后，您应在活动Teams Toolkit看到Visual Studio Code栏。</span><span class="sxs-lookup"><span data-stu-id="6426e-111">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="6426e-112">如果没有，请在活动栏中右键单击并选择"Microsoft Teams固定工具包以轻松访问。</span><span class="sxs-lookup"><span data-stu-id="6426e-112">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="configure-your-project"></a><span data-ttu-id="6426e-113">配置项目</span><span class="sxs-lookup"><span data-stu-id="6426e-113">Configure your project</span></span>

1. <span data-ttu-id="6426e-114">若要在应用内Teams SSO，应用必须具有 Azure 应用注册资源。</span><span class="sxs-lookup"><span data-stu-id="6426e-114">To enable SSO within Teams, your app must have an Azure app registration resource.</span></span> <span data-ttu-id="6426e-115">应用Teams Toolkit将代表你预配应用注册。</span><span class="sxs-lookup"><span data-stu-id="6426e-115">The Teams Toolkit will provision the app registration on your behalf.</span></span>
1. <span data-ttu-id="6426e-116">输入你的应用将托管的 URL，然后选择下一 **步**。</span><span class="sxs-lookup"><span data-stu-id="6426e-116">Enter the URL where your app will be hosted and select **next**.</span></span> <span data-ttu-id="6426e-117">你的应用注册将使用提供的 URL 进行配置。</span><span class="sxs-lookup"><span data-stu-id="6426e-117">Your app registration will be configured using the provided URL.</span></span>
1. <span data-ttu-id="6426e-118">应用注册的配置详细信息将存储在项目的源代码 `.env` 中的文件中。</span><span class="sxs-lookup"><span data-stu-id="6426e-118">The app registration's configuration details will be stored in the `.env` files in your project's source code.</span></span>

<span data-ttu-id="6426e-119">若要详细了解如何预配 Azure 应用注册，请参阅我们的单一登录[ (SSO](../tabs/how-to/authentication/auth-aad-sso.md)) 支持选项卡文档。 </span><span class="sxs-lookup"><span data-stu-id="6426e-119">If you would like to learn more about how your Azure app registration will be provisioned, please _see_  our [single sign-on (SSO) support for tabs](../tabs/how-to/authentication/auth-aad-sso.md) documentation.</span></span>

> [!TIP]
> <span data-ttu-id="6426e-120">你将需要转到 Azure **应用注册** 并更新 API *URI，* 并重定向 *URL，只要* 更改此 URL。</span><span class="sxs-lookup"><span data-stu-id="6426e-120">You will need to go to **Azure App Registrations** and update your *API URI* and *redirect URLs* whenever you change this URL.</span></span>

## <a name="run-your-project"></a><span data-ttu-id="6426e-121">运行项目</span><span class="sxs-lookup"><span data-stu-id="6426e-121">Run your project</span></span>

1. <span data-ttu-id="6426e-122">从 **文件夹选择 npm** `api-server` 安装。</span><span class="sxs-lookup"><span data-stu-id="6426e-122">Select **npm install** from the `api-server` folder.</span></span> <span data-ttu-id="6426e-123">然后 **npm 启动**。</span><span class="sxs-lookup"><span data-stu-id="6426e-123">Then **npm start**.</span></span>
1. <span data-ttu-id="6426e-124">从 **文件夹选择 npm** `.src` 安装。</span><span class="sxs-lookup"><span data-stu-id="6426e-124">Select **npm install** from the `.src` folder.</span></span> <span data-ttu-id="6426e-125">然后 **npm 启动**。</span><span class="sxs-lookup"><span data-stu-id="6426e-125">Then **npm start**.</span></span>
1. <span data-ttu-id="6426e-126">如果你使用的是像 [ngrok](https://ngrok.com/)这样的隧道服务，请运行它并确保 URL 与你在项目创建向导中输入的内容相匹配。</span><span class="sxs-lookup"><span data-stu-id="6426e-126">If you are using a tunneling service like [ngrok](https://ngrok.com/), run it and make sure the URL matches with what you entered in the project creation wizard.</span></span> <span data-ttu-id="6426e-127">如果没有，则需要在 Azure 中创建的应用注册中更新 _API URI_ 和重定向 URL。 </span><span class="sxs-lookup"><span data-stu-id="6426e-127">If it doesn't, you will need to update your _API URI_ and _redirect URL_ in the app registration that was created in Azure.</span></span>
1. <span data-ttu-id="6426e-128">导航到"活动"窗口左侧的活动Visual Studio Code栏。</span><span class="sxs-lookup"><span data-stu-id="6426e-128">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="6426e-129">选择" **运行** "图标以显示 **"运行和调试"** 视图。</span><span class="sxs-lookup"><span data-stu-id="6426e-129">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="6426e-130">您还可以使用键盘快捷方式 **Ctrl+Shift+D**。</span><span class="sxs-lookup"><span data-stu-id="6426e-130">You can also use the keyboard shortcut **Ctrl+Shift+D**.</span></span>

> [!TIP]
> <span data-ttu-id="6426e-131">如果为浏览器禁用了弹出窗口，则你可能不会在浏览器中看到应用安装对话。</span><span class="sxs-lookup"><span data-stu-id="6426e-131">You may not see the app install dialogue in the browser if pop-up windows are disabled for your browser.</span></span> <span data-ttu-id="6426e-132">如果发生这种情况，请启用弹出窗口并刷新页面。</span><span class="sxs-lookup"><span data-stu-id="6426e-132">If this happens, enable pop-up windows and refresh the page.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6426e-133">了解更多信息：使用 Microsoft Teams Toolkit 和 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="6426e-133">Learn more: Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>](visual-studio-code-overview.md)
