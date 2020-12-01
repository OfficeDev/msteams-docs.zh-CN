---
title: 单一登录身份验证与团队工具包和 Visual Studio Code for 选项卡
description: 使用 Microsoft 团队工具包生成支持在 Visual Studio Code 中直接进行单一登录和 Microsoft Graph 调用的选项卡
keywords: 团队 visual studio code 工具包选项卡 sso 图形身份验证 Azure 标识平台
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: fe734143975688cd35c510cd68cd0779a2200a18
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2020
ms.locfileid: "49477732"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a><span data-ttu-id="690f8-104">单一登录身份验证与团队工具包和 Visual Studio Code for 选项卡</span><span class="sxs-lookup"><span data-stu-id="690f8-104">Single sign-on authentication with Teams Toolkit and Visual Studio Code for tabs</span></span>

<span data-ttu-id="690f8-105">Microsoft 团队工具包使您能够在 Visual Studio Code 中直接为选项卡应用程序创建单一登录 (SSO) 身份验证。</span><span class="sxs-lookup"><span data-stu-id="690f8-105">The Microsoft Teams Toolkit enables you to create single sign-on (SSO) authentication  for tab apps directly within Visual Studio Code.</span></span> <span data-ttu-id="690f8-106">该工具包将引导您完成整个过程，并提供所需的所有内容，包括在 Azure 门户中预配 Microsoft identity platform 注册。</span><span class="sxs-lookup"><span data-stu-id="690f8-106">The toolkit guides you through the process and provides everything you need including provisioning your Microsoft identity platform registration in the Azure portal.</span></span>

## <a name="get-started--create-a-project"></a><span data-ttu-id="690f8-107">入门-创建项目</span><span class="sxs-lookup"><span data-stu-id="690f8-107">Get started — create a project</span></span>

1. <span data-ttu-id="690f8-108">在工具包中创建一个新项目。</span><span class="sxs-lookup"><span data-stu-id="690f8-108">Create a new project in the toolkit.</span></span>
1. <span data-ttu-id="690f8-109">选择 "tab" 作为要创建的扩展类型。</span><span class="sxs-lookup"><span data-stu-id="690f8-109">Select tab as the type of extension you'd like to create.</span></span>
1. <span data-ttu-id="690f8-110">选择支持 SSO 的选项。</span><span class="sxs-lookup"><span data-stu-id="690f8-110">Select the option to support SSO.</span></span>

> [!TIP]
> <span data-ttu-id="690f8-111">安装完成后，应在 Visual Studio Code 活动栏中看到 "团队" 工具包。</span><span class="sxs-lookup"><span data-stu-id="690f8-111">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="690f8-112">如果不是，请在活动栏中右键单击，然后选择 " **Microsoft 团队** " 以固定该工具包以方便访问。</span><span class="sxs-lookup"><span data-stu-id="690f8-112">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="configure-your-project"></a><span data-ttu-id="690f8-113">配置项目</span><span class="sxs-lookup"><span data-stu-id="690f8-113">Configure your project</span></span>

1. <span data-ttu-id="690f8-114">若要在团队中启用 SSO，应用必须具有 Azure 应用注册资源。</span><span class="sxs-lookup"><span data-stu-id="690f8-114">To enable SSO within Teams, your app must have an Azure app registration resource.</span></span> <span data-ttu-id="690f8-115">团队工具包将代表你预配应用注册。</span><span class="sxs-lookup"><span data-stu-id="690f8-115">The Teams Toolkit will provision the app registration on your behalf.</span></span>
1. <span data-ttu-id="690f8-116">输入将托管您的应用程序的 URL，然后选择 " **下一步**"。</span><span class="sxs-lookup"><span data-stu-id="690f8-116">Enter the URL where your app will be hosted and select **next**.</span></span> <span data-ttu-id="690f8-117">您的应用程序注册将使用提供的 URL 进行配置。</span><span class="sxs-lookup"><span data-stu-id="690f8-117">Your app registration will be configured using the provided URL.</span></span>
1. <span data-ttu-id="690f8-118">应用注册的配置详细信息将存储在 `.env` 项目源代码的文件中。</span><span class="sxs-lookup"><span data-stu-id="690f8-118">The app registration's configuration details will be stored in the `.env` files in your project's source code.</span></span>

<span data-ttu-id="690f8-119">如果你想要了解有关如何设置 Azure 应用注册的详细信息，请 _参阅_  我们 [的单一登录 (SSO) 支持的选项卡](../tabs/how-to/authentication/auth-aad-sso.md) 文档。</span><span class="sxs-lookup"><span data-stu-id="690f8-119">If you would like to learn more about how your Azure app registration will be provisioned, please _see_  our [single sign-on (SSO) support for tabs](../tabs/how-to/authentication/auth-aad-sso.md) documentation.</span></span>

> [!TIP]
> <span data-ttu-id="690f8-120">每当您更改此 URL 时，您都需要转到 **Azure 应用注册** 并更新 *API URI* 并 *重定向 url* 。</span><span class="sxs-lookup"><span data-stu-id="690f8-120">You will need to go to **Azure App Registrations** and update your *API URI* and *redirect URLs* whenever you change this URL.</span></span>

## <a name="run-your-project"></a><span data-ttu-id="690f8-121">运行您的项目</span><span class="sxs-lookup"><span data-stu-id="690f8-121">Run your project</span></span>

1. <span data-ttu-id="690f8-122">从文件夹中选择 " **npm 安装** " `api-server` 。</span><span class="sxs-lookup"><span data-stu-id="690f8-122">Select **npm install** from the `api-server` folder.</span></span> <span data-ttu-id="690f8-123">然后 **npm 启动**。</span><span class="sxs-lookup"><span data-stu-id="690f8-123">Then **npm start**.</span></span>
1. <span data-ttu-id="690f8-124">从文件夹中选择 " **npm 安装** " `.src` 。</span><span class="sxs-lookup"><span data-stu-id="690f8-124">Select **npm install** from the `.src` folder.</span></span> <span data-ttu-id="690f8-125">然后 **npm 启动**。</span><span class="sxs-lookup"><span data-stu-id="690f8-125">Then **npm start**.</span></span>
1. <span data-ttu-id="690f8-126">如果使用的是隧道服务（如 [ngrok](https://ngrok.com/)），请运行它并确保 URL 与您在 "项目创建向导" 中输入的内容相匹配。</span><span class="sxs-lookup"><span data-stu-id="690f8-126">If you are using a tunneling service like [ngrok](https://ngrok.com/), run it and make sure the URL matches with what you entered in the project creation wizard.</span></span> <span data-ttu-id="690f8-127">如果不是这样，您将需要更新在 Azure 中创建的应用注册中的 _API URI_ 并重 _定向 URL_ 。</span><span class="sxs-lookup"><span data-stu-id="690f8-127">If it doesn't, you will need to update your _API URI_ and _redirect URL_ in the app registration that was created in Azure.</span></span>
1. <span data-ttu-id="690f8-128">导航到 Visual Studio "代码" 窗口左侧的 "活动" 栏。</span><span class="sxs-lookup"><span data-stu-id="690f8-128">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="690f8-129">选择 " **运行** " 图标以显示 " **运行" 和 "调试** " 视图。</span><span class="sxs-lookup"><span data-stu-id="690f8-129">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="690f8-130">您还可以使用键盘快捷方式 **Ctrl + Shift + D**。</span><span class="sxs-lookup"><span data-stu-id="690f8-130">You can also use the keyboard shortcut **Ctrl+Shift+D**.</span></span>

> [!TIP]
> <span data-ttu-id="690f8-131">如果浏览器禁用了弹出窗口，则在浏览器中可能不会看到 "应用程序安装" 对话框。</span><span class="sxs-lookup"><span data-stu-id="690f8-131">You may not see the app install dialogue in the browser if pop-up windows are disabled for your browser.</span></span> <span data-ttu-id="690f8-132">如果发生这种情况，请启用弹出窗口并刷新页面。</span><span class="sxs-lookup"><span data-stu-id="690f8-132">If this happens, enable pop-up windows and refresh the page.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="690f8-133">了解详细信息：使用 Microsoft 团队工具包和 Visual Studio Code 生成应用</span><span class="sxs-lookup"><span data-stu-id="690f8-133">Learn more: Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>](visual-studio-code-overview.md)
