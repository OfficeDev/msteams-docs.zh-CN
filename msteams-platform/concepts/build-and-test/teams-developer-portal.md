---
title: 使用开发人员门户管理应用
description: 了解如何使用开发人员门户管理Microsoft Teams。
keywords: 开发人员门户团队入门
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 6dca8723248441c3cf672931295b4b68e02cc24c
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949684"
---
# <a name="manage-your-apps-with-the-developer-portal-for-microsoft-teams"></a><span data-ttu-id="96c9b-104">使用开发人员门户管理应用Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="96c9b-104">Manage your apps with the Developer Portal for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="96c9b-105">适用于开发人员的开发人员Teams目前处于[公共开发人员预览版中](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="96c9b-105">The Developer Portal for Teams is currently in [public developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

<span data-ttu-id="96c9b-106">开发人员<a href="https://dev.teams.microsoft.com" target="_blank">门户Teams</a>是配置、分发和管理应用程序的主要Microsoft Teams工具。</span><span class="sxs-lookup"><span data-stu-id="96c9b-106">The <a href="https://dev.teams.microsoft.com" target="_blank">Developer Portal for Teams</a> is the primary tool for configuring, distributing, and managing your Microsoft Teams apps.</span></span> <span data-ttu-id="96c9b-107">通过开发人员门户，你可以与应用上的同事协作、设置运行时环境等。</span><span class="sxs-lookup"><span data-stu-id="96c9b-107">With the Developer Portal, you can collaborate with colleagues on your app, set up runtime environments, and much more.</span></span>

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="显示开发人员门户主页的屏幕截图Teams。":::

## <a name="register-an-app"></a><span data-ttu-id="96c9b-109">注册应用</span><span class="sxs-lookup"><span data-stu-id="96c9b-109">Register an app</span></span>

<span data-ttu-id="96c9b-110">开发人员门户提供了几种注册应用Teams方法：</span><span class="sxs-lookup"><span data-stu-id="96c9b-110">The Developer Portal provides a couple ways to register a Teams app:</span></span>

* <span data-ttu-id="96c9b-111">注册全新的应用</span><span class="sxs-lookup"><span data-stu-id="96c9b-111">Register a brand new app</span></span>
* <span data-ttu-id="96c9b-112">导入现有应用包</span><span class="sxs-lookup"><span data-stu-id="96c9b-112">Import an existing app package</span></span>

> [!NOTE]
> <span data-ttu-id="96c9b-113">如果使用 Microsoft Teams Toolkit [for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)创建应用，可以在开发人员门户中管理该应用。</span><span class="sxs-lookup"><span data-stu-id="96c9b-113">If you create an app using the [Microsoft Teams Toolkit for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension), you can manage that app in the Developer Portal.</span></span>

## <a name="set-up-an-environment"></a><span data-ttu-id="96c9b-114">设置环境</span><span class="sxs-lookup"><span data-stu-id="96c9b-114">Set up an environment</span></span>

<span data-ttu-id="96c9b-115">你可以配置环境和全局变量，以帮助将应用从本地运行时转换到生产环境。</span><span class="sxs-lookup"><span data-stu-id="96c9b-115">You can configure environments and global variables to help transition your app from your local runtime to production.</span></span> <span data-ttu-id="96c9b-116">全局变量在所有环境中使用。</span><span class="sxs-lookup"><span data-stu-id="96c9b-116">Global variables are used across all environments.</span></span>

<span data-ttu-id="96c9b-117">**设置环境**</span><span class="sxs-lookup"><span data-stu-id="96c9b-117">**To set up an environment**</span></span>

1. <span data-ttu-id="96c9b-118">在开发人员门户中，选择你正在处理的应用。</span><span class="sxs-lookup"><span data-stu-id="96c9b-118">In the Developer Portal, select the app you're working on.</span></span>
2. <span data-ttu-id="96c9b-119">转到"**环境"** 页，然后选择 **"+ 添加环境"。**</span><span class="sxs-lookup"><span data-stu-id="96c9b-119">Go to the **Environments** page and select **+ Add an environment**.</span></span>
3. <span data-ttu-id="96c9b-120">选择 **" + 添加变量** "，为环境创建配置变量。</span><span class="sxs-lookup"><span data-stu-id="96c9b-120">Select **+ Add a variable** to create configuration variables for your environment.</span></span>

<span data-ttu-id="96c9b-121">**使用变量**</span><span class="sxs-lookup"><span data-stu-id="96c9b-121">**To use variables**</span></span>

<span data-ttu-id="96c9b-122">使用变量名称而不是硬编码值来设置应用配置。</span><span class="sxs-lookup"><span data-stu-id="96c9b-122">Use the variable names instead of hard-coded values to set your app configurations.</span></span>

1. <span data-ttu-id="96c9b-123">在 `{{` 开发人员门户的任何字段中输入。</span><span class="sxs-lookup"><span data-stu-id="96c9b-123">Enter `{{` in any field in the Developer Portal.</span></span> <span data-ttu-id="96c9b-124">将显示一个下拉列表，包含为所选环境创建的所有变量以及全局变量。</span><span class="sxs-lookup"><span data-stu-id="96c9b-124">A dropdown with all the variables you've created for the chosen environment along with the global variables appears.</span></span>  
1. <span data-ttu-id="96c9b-125">在下载应用包 (例如，准备好发布到 Teams 应用商店) 时，请选择想要使用的环境。</span><span class="sxs-lookup"><span data-stu-id="96c9b-125">Before downloading your app package (for example, when getting ready to publish to the Teams store), select the environment you want to use.</span></span> <span data-ttu-id="96c9b-126">应用配置根据环境自动更新。</span><span class="sxs-lookup"><span data-stu-id="96c9b-126">Your app configurations update automatically based on the environment.</span></span> 

## <a name="identify-app-owners"></a><span data-ttu-id="96c9b-127">确定应用所有者</span><span class="sxs-lookup"><span data-stu-id="96c9b-127">Identify app owners</span></span>

<span data-ttu-id="96c9b-128">每个应用都包括 **一个所有者** 页面，可在其中与组织中的同事共享应用注册。 **参与者** 角色具有与所有者 **角色相同的权限** ，但删除应用的能力除外。</span><span class="sxs-lookup"><span data-stu-id="96c9b-128">Each app includes an **Owners** page, where you can share your app registration with colleagues in your org. The **Contributor** role has the same permissions as the **Owner** role except the ability to delete an app.</span></span>

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a><span data-ttu-id="96c9b-129">配置应用的功能和其他重要元数据</span><span class="sxs-lookup"><span data-stu-id="96c9b-129">Configure your app's capabilities and other important metadata</span></span>

<span data-ttu-id="96c9b-130">一Teams应用是 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="96c9b-130">A Teams app is a web app.</span></span> <span data-ttu-id="96c9b-131">像所有 Web 应用一样，其源代码通常在 IDE 或代码编辑器中开发，并托管在云中的 (Azure) 。</span><span class="sxs-lookup"><span data-stu-id="96c9b-131">Like all web apps, its source code is typically developed in an IDE or code editor and hosted somewhere in the cloud (like Azure).</span></span>

<span data-ttu-id="96c9b-132">若要在应用程序中安装和呈现Teams，必须包含一组可识别Teams配置。</span><span class="sxs-lookup"><span data-stu-id="96c9b-132">To install and render your app in Teams, you must include a set of configurations that Teams recognizes.</span></span> <span data-ttu-id="96c9b-133">这通常通过创建应用清单（包含显示应用内容Teams元数据的 JSON 文件）完成。</span><span class="sxs-lookup"><span data-stu-id="96c9b-133">This has traditionally been done by crafting an app manifest, a JSON file that contains all the metadata Teams needs to display your app content.</span></span> <span data-ttu-id="96c9b-134">开发人员门户将此过程抽象化，并包括新功能和工具，以帮助你取得更多成功。</span><span class="sxs-lookup"><span data-stu-id="96c9b-134">The Developer Portal abstracts this process and includes new features and tooling to help you be more successful.</span></span>

## <a name="test-your-app-directly-in-teams"></a><span data-ttu-id="96c9b-135">直接在应用中测试Teams</span><span class="sxs-lookup"><span data-stu-id="96c9b-135">Test your app directly in Teams</span></span>

<span data-ttu-id="96c9b-136">开发人员门户提供用于测试和调试应用的选项：</span><span class="sxs-lookup"><span data-stu-id="96c9b-136">The Developer Portal provides options for testing and debugging your app:</span></span>

* <span data-ttu-id="96c9b-137">在 **"概述**"页上，你可以查看应用配置是否针对应用商店Teams验证的快照。</span><span class="sxs-lookup"><span data-stu-id="96c9b-137">On the **Overview** page, you can see a snapshot of whether your app's configurations validate against Teams store test cases.</span></span>
* <span data-ttu-id="96c9b-138">通过 **"Teams** 预览"按钮，你可以快速在 Teams 客户端中启动应用进行调试。</span><span class="sxs-lookup"><span data-stu-id="96c9b-138">The **Preview in Teams** button lets you launch your app quickly in the Teams client for debugging.</span></span>

## <a name="distribute-your-app"></a><span data-ttu-id="96c9b-139">分发应用</span><span class="sxs-lookup"><span data-stu-id="96c9b-139">Distribute your app</span></span>

<span data-ttu-id="96c9b-140">从开发人员门户中，使用"分发"按钮下载应用包、发布到组织或发布到 Teams 应用商店。</span><span class="sxs-lookup"><span data-stu-id="96c9b-140">From the Developer Portal, use the **Distribute** button to download an app package, publish to your org, or publish to the Teams store.</span></span>

<span data-ttu-id="96c9b-141">有关详细信息，请参阅分发[你的Teams应用](~/concepts/deploy-and-publish/apps-publish-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="96c9b-141">For more information, see [distribute your Teams app](~/concepts/deploy-and-publish/apps-publish-overview.md).</span></span>

## <a name="analyze-your-apps-usage"></a><span data-ttu-id="96c9b-142">分析应用的使用情况</span><span class="sxs-lookup"><span data-stu-id="96c9b-142">Analyze your app's usage</span></span>

<span data-ttu-id="96c9b-143">在 **"概述** "页上，你可以看到应用的活动用户总数。</span><span class="sxs-lookup"><span data-stu-id="96c9b-143">On the **Overview** page, you can see the total number of active users for your app.</span></span> <span data-ttu-id="96c9b-144">这些指标可用于通过开发人员门户发布到 Teams 商店或组织的应用程序目录，并且范围为应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="96c9b-144">These metrics are available for apps published to the Teams store or an org's app catalog through Developer Portal and scoped to the app ID.</span></span>

| <span data-ttu-id="96c9b-145">跃点数</span><span class="sxs-lookup"><span data-stu-id="96c9b-145">Metric</span></span> | <span data-ttu-id="96c9b-146">定义</span><span class="sxs-lookup"><span data-stu-id="96c9b-146">Definition</span></span> |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="96c9b-147">*每月 R30*</span><span class="sxs-lookup"><span data-stu-id="96c9b-147">*Monthly R30*</span></span> | <span data-ttu-id="96c9b-148">默认使用率指标。</span><span class="sxs-lookup"><span data-stu-id="96c9b-148">The default usage metric.</span></span> <span data-ttu-id="96c9b-149">它显示了在 UTC 时间滚动 30 天窗口内使用你的应用的唯一活动用户数。</span><span class="sxs-lookup"><span data-stu-id="96c9b-149">It shows you the count of unique active users that used your app within that rolling 30-day window in UTC.</span></span> |
| <span data-ttu-id="96c9b-150">*每天*</span><span class="sxs-lookup"><span data-stu-id="96c9b-150">*Daily*</span></span> | <span data-ttu-id="96c9b-151">显示以 UTC 格式在给定日期使用应用的唯一活动用户数。</span><span class="sxs-lookup"><span data-stu-id="96c9b-151">Shows you the count of unique active users that used your app in a given day in UTC.</span></span> |

<span data-ttu-id="96c9b-152">显示过去七天、30 天和 60 天的每月使用情况和每日使用情况。</span><span class="sxs-lookup"><span data-stu-id="96c9b-152">Monthly and daily usage is shown for the past seven, 30 days, and 60 days.</span></span> <span data-ttu-id="96c9b-153">您应在 24-48 小时内看到给定一天的使用情况。</span><span class="sxs-lookup"><span data-stu-id="96c9b-153">You should see usage reflected for a given day within 24-48 hours.</span></span> <span data-ttu-id="96c9b-154">新应用的使用情况最多可能需要 3-5 天才能显示。</span><span class="sxs-lookup"><span data-stu-id="96c9b-154">Usage for new apps can take up to 3-5 days to display.</span></span>

## <a name="use-tools-to-create-app-features"></a><span data-ttu-id="96c9b-155">使用工具创建应用功能</span><span class="sxs-lookup"><span data-stu-id="96c9b-155">Use tools to create app features</span></span>

<span data-ttu-id="96c9b-156">开发人员门户还包括可帮助你构建应用或应用Teams功能的工具。</span><span class="sxs-lookup"><span data-stu-id="96c9b-156">The Developer Portal also includes tools to help you build some key features of Teams apps.</span></span> <span data-ttu-id="96c9b-157">其中一些工具包括：</span><span class="sxs-lookup"><span data-stu-id="96c9b-157">Some of these tools include:</span></span>

* <span data-ttu-id="96c9b-158">**Scene studio：** 为 [会议设计自定义](~/apps-in-teams-meetings/teams-together-mode.md)一Teams场景。</span><span class="sxs-lookup"><span data-stu-id="96c9b-158">**Scene studio**: Design [custom Together Mode scenes](~/apps-in-teams-meetings/teams-together-mode.md) for Teams meetings.</span></span>
* <span data-ttu-id="96c9b-159">**自适应卡片编辑器**：创建和预览要包括在应用的自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="96c9b-159">**Adaptive Cards editor**: Create and preview Adaptive Cards to include with your apps.</span></span>
* <span data-ttu-id="96c9b-160">**Microsoft 标识平台管理**：使用 Azure AD Azure Active Directory (注册) 以帮助用户登录并提供 API 访问权限。</span><span class="sxs-lookup"><span data-stu-id="96c9b-160">**Microsoft identity platform management**: Register your apps with Azure Active Directory (Azure AD) to help users sign in and provide access to APIs.</span></span>
