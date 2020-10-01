---
title: 在 SharePoint 中将 Microsoft 团队选项卡添加为 SPFx web 部件
author: laujan
description: 如何将现有团队选项卡作为 SharePoint 框架 web 部件部署到 SharePoint。
keywords: sharepoint 框架开发的团队选项卡
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d7f617f0967743eab84423cd31f78d4700db1c1c
ms.sourcegitcommit: e92408e751a8f51028908ab7e2415a8051a536c0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2020
ms.locfileid: "48326345"
---
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a><span data-ttu-id="ede3e-104">在 SharePoint 中将 Microsoft 团队选项卡添加为 SPFx web 部件</span><span class="sxs-lookup"><span data-stu-id="ede3e-104">Adding a Microsoft Teams tab in SharePoint as an SPFx web part</span></span>

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="ede3e-105">团队和 SharePoint 之间的丰富集成</span><span class="sxs-lookup"><span data-stu-id="ede3e-105">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="ede3e-106">在11月发布的团队和 SharePoint Framework 2007 中。</span><span class="sxs-lookup"><span data-stu-id="ede3e-106">With the November release of Teams and SharePoint Framework v.</span></span> <span data-ttu-id="ede3e-107">1.7，开发人员具有两项强大的功能：</span><span class="sxs-lookup"><span data-stu-id="ede3e-107">1.7, developers have two powerful capabilities:</span></span>

<ul  class="panelContent cardsC">
<li>
    <a href="#introduction">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/image084.png" alt="tab-in-sharepoint view"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3><span data-ttu-id="ede3e-108">SharePoint 中的团队选项卡</span><span class="sxs-lookup"><span data-stu-id="ede3e-108">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="ede3e-109">通过将团队应用引入 Sharepoint (本文) ，在 SharePoint 中创建丰富的应用程序体验。</span><span class="sxs-lookup"><span data-stu-id="ede3e-109">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li>
    <a href="https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/SharePoint-web-part-exposed-as-a-Tab-in-Microsoft-Teams.png" alt="web-part-exposed-as-a-tab" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3><span data-ttu-id="ede3e-110">团队中的 SharePoint 框架</span><span class="sxs-lookup"><span data-stu-id="ede3e-110">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="ede3e-111">将 SharePoint web 部件引入团队，让 SharePoint 为您管理托管。</span><span class="sxs-lookup"><span data-stu-id="ede3e-111">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="ede3e-112">SharePoint 中的团队选项卡</span><span class="sxs-lookup"><span data-stu-id="ede3e-112">Teams tabs in SharePoint</span></span>

<span data-ttu-id="ede3e-113">通过 SharePoint Framework 1.7 版，我们现在支持开发人员将其团队选项卡和托管在 SharePoint 中。</span><span class="sxs-lookup"><span data-stu-id="ede3e-113">With SharePoint Framework v.1.7, we’re now supporting the ability for developers to take their Teams tabs and host it in SharePoint.</span></span> <span data-ttu-id="ede3e-114">作为 SharePoint 中托管的选项卡获取类似的 "整页" 体验，从而公开了 "团队" 选项卡的所有功能，同时保留了 SharePoint 网站的上下文和熟悉程度。</span><span class="sxs-lookup"><span data-stu-id="ede3e-114">As Tabs hosted in SharePoint get a similar "full page" experience, exposing the all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="ede3e-115">团队中的 SharePoint 框架</span><span class="sxs-lookup"><span data-stu-id="ede3e-115">SharePoint Framework in Teams</span></span>

<span data-ttu-id="ede3e-116">您还可以使用 SharePoint 框架实施 Microsoft 团队选项卡。</span><span class="sxs-lookup"><span data-stu-id="ede3e-116">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="ede3e-117">对于 SharePoint 开发人员，这极大地简化了团队选项卡的开发过程，因为 SharePoint 框架 web 部件托管在 SharePoint 中，无需任何外部服务（如 Azure）。</span><span class="sxs-lookup"><span data-stu-id="ede3e-117">For SharePoint developers, this significantly simplifies the development process for Teams tabs because SharePoint Framework web parts are hosted within SharePoint without any need for external services such as Azure.</span></span> [<span data-ttu-id="ede3e-118">了解有关在团队中使用 SharePoint 框架的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ede3e-118">Learn more about using the SharePoint Framework in Teams.</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a><span data-ttu-id="ede3e-119">简介</span><span class="sxs-lookup"><span data-stu-id="ede3e-119">Introduction</span></span>

<span data-ttu-id="ede3e-120">这些说明将介绍如何从 Microsoft 团队示例应用中获取一个选项卡，并在 SharePoint 中使用它。</span><span class="sxs-lookup"><span data-stu-id="ede3e-120">These instructions will explain how you can take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> <span data-ttu-id="ede3e-121">我们将使用 Azure 上已托管的选项卡，以将重点放在所需的集成工作上。</span><span class="sxs-lookup"><span data-stu-id="ede3e-121">We will be using a tab that's already hosted on Azure in order to focus on the required integration work.</span></span>

<span data-ttu-id="ede3e-122">我们正在使用的示例应用是一个人才管理应用程序。</span><span class="sxs-lookup"><span data-stu-id="ede3e-122">The sample app we're using is a Talent Management application.</span></span> <span data-ttu-id="ede3e-123">它管理团队中打开职位的候选人的聘用过程。</span><span class="sxs-lookup"><span data-stu-id="ede3e-123">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="ede3e-124"> (应用程序本身，尽管它看起来不错，但实际上并不会执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="ede3e-124">(The app itself, while it looks nice, doesn't actually do anything.</span></span> <span data-ttu-id="ede3e-125">我们希望将重点放在团队应用程序上，并将其加载到团队中，而不是创建真实的人才管理应用程序。 ) </span><span class="sxs-lookup"><span data-stu-id="ede3e-125">We want to focus on building a Teams app and loading it into Teams, not create a real talent management application.)</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="ede3e-126">此方法的优点</span><span class="sxs-lookup"><span data-stu-id="ede3e-126">Benefits of this approach</span></span>

- <span data-ttu-id="ede3e-127">使用现有团队选项卡访问 SharePoint 用户</span><span class="sxs-lookup"><span data-stu-id="ede3e-127">Reach SharePoint users with your existing Teams tab</span></span>
- <span data-ttu-id="ede3e-128">将您的应用程序清单直接上传到 SharePoint 应用程序目录。</span><span class="sxs-lookup"><span data-stu-id="ede3e-128">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="ede3e-129">[团队应用程序包](~/concepts/build-and-test/apps-package.md) 现已由 SharePoint 支持</span><span class="sxs-lookup"><span data-stu-id="ede3e-129">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint</span></span>
- <span data-ttu-id="ede3e-130">最终用户在页面上配置选项卡的方式与任何其他 SharePoint web 部件一样</span><span class="sxs-lookup"><span data-stu-id="ede3e-130">End users configure the tab on a page just like any other SharePoint web part</span></span>
- <span data-ttu-id="ede3e-131">您的选项卡可以像在团队中运行一样访问其[上下文](~/tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="ede3e-131">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) just as it can when running inside Teams</span></span>

## <a name="step-1-testing-the-sample-app"></a><span data-ttu-id="ede3e-132">步骤1：测试示例应用程序</span><span class="sxs-lookup"><span data-stu-id="ede3e-132">Step 1: Testing the sample app</span></span>

<span data-ttu-id="ede3e-133">从 [**此处**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)下载示例应用程序清单。</span><span class="sxs-lookup"><span data-stu-id="ede3e-133">Download the sample app manifest from [**here**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

<span data-ttu-id="ede3e-134">在 Microsoft 团队中，单击左下角的 "存储" 图标，然后在左下角 "上载自定义应用"。</span><span class="sxs-lookup"><span data-stu-id="ede3e-134">In Microsoft Teams, click on the Store icon at the lower left and then "Upload a custom app" at the lower left.</span></span> <span data-ttu-id="ede3e-135">要上载的文件将位于您的 "下载" 文件夹中。它被称为 TalentMgmt-Azure.zip。</span><span class="sxs-lookup"><span data-stu-id="ede3e-135">The file to upload will be located in your Downloads folder; it's called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="ede3e-136">如果一切正常，你将看到 "人才管理" 应用程序的 "安装/同意" 屏幕。</span><span class="sxs-lookup"><span data-stu-id="ede3e-136">If all goes well, you'll see the install/consent screen for the talent management app.</span></span> <span data-ttu-id="ede3e-137">选择要安装到的团队，然后单击 "安装" 按钮。</span><span class="sxs-lookup"><span data-stu-id="ede3e-137">Choose the team you want to install to and click the Install button.</span></span> <span data-ttu-id="ede3e-138">现在，你可以免费试用该应用。</span><span class="sxs-lookup"><span data-stu-id="ede3e-138">You're now free to experiment with the app.</span></span>

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a><span data-ttu-id="ede3e-139">步骤2：使用 SharePoint 中的 "团队" 选项卡</span><span class="sxs-lookup"><span data-stu-id="ede3e-139">Step 2: Using the Teams tab in SharePoint</span></span>

<span data-ttu-id="ede3e-140">通过访问将团队应用程序包上载并部署到 SharePoint 应用程序目录 `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 中，例如 `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 。</span><span class="sxs-lookup"><span data-stu-id="ede3e-140">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`, e.g. `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

<span data-ttu-id="ede3e-141">出现提示时，启用 "使此解决方案可用于组织中的所有站点"：</span><span class="sxs-lookup"><span data-stu-id="ede3e-141">When prompted, enable "Make this solution available to all sites in the organization":</span></span>

![Sharepoint 视图中的选项卡](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

<span data-ttu-id="ede3e-143">在网站中，单击右上角的 "齿轮" 按钮以创建新页面，然后单击 "添加页面"：</span><span class="sxs-lookup"><span data-stu-id="ede3e-143">In your site, create a new page by clicking in the gear button at the upper right and then "Add a page":</span></span>

![Sharepoint 视图](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

<span data-ttu-id="ede3e-145">你将看到 SharePoint 页面创作体验。</span><span class="sxs-lookup"><span data-stu-id="ede3e-145">You'll see the SharePoint Pages authoring experience.</span></span> <span data-ttu-id="ede3e-146">将页面命名为 "我的团队选项卡"。</span><span class="sxs-lookup"><span data-stu-id="ede3e-146">Name your page "My Teams Tab".</span></span>

<span data-ttu-id="ede3e-147">按 "+" 按钮打开 "web 部件工具箱"，然后选择名为 "Contoso HR" 的 "团队" 选项卡 () 。</span><span class="sxs-lookup"><span data-stu-id="ede3e-147">Open the web part toolbox by pressing the + button, and select your Teams Tab (named "Contoso HR").</span></span> <span data-ttu-id="ede3e-148">Web 部件按字母顺序排序;如果是较长的列表，则可以使用搜索栏查找它。</span><span class="sxs-lookup"><span data-stu-id="ede3e-148">Web parts are sorted alphabetically; if it's a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="ede3e-149">这将在包含 "团队" 选项卡的画布中创建 web 部件：</span><span class="sxs-lookup"><span data-stu-id="ede3e-149">This will create a web part in the canvas that contains your Teams tab:</span></span>

![选项卡视图](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

<span data-ttu-id="ede3e-151">完成编辑后，请按 "发布" 按钮。</span><span class="sxs-lookup"><span data-stu-id="ede3e-151">Press the "Publish" button when you are finished editing.</span></span>

<span data-ttu-id="ede3e-152">您可能需要单击 "将页面添加到导航" 以快速引用左侧导航栏中的页面：</span><span class="sxs-lookup"><span data-stu-id="ede3e-152">You may want to click "Add page to navigation" to have a quick reference to your page in the left navigation bar:</span></span>

![Sharepoint 图像中的选项卡](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="ede3e-154">步骤3：浏览 SharePoint 中的应用程序页</span><span class="sxs-lookup"><span data-stu-id="ede3e-154">Step 3: Explore App Pages in SharePoint</span></span>

<span data-ttu-id="ede3e-155">发布页面后，您可以浏览在 [SharePoint 中将团队应用程序转变成更全面的体验](/sharepoint/dev/spfx/web-parts/single-part-app-pages)。</span><span class="sxs-lookup"><span data-stu-id="ede3e-155">Once your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="ede3e-156">此操作会将当前页面转换为应用程序页面，显示常规 SharePoint 页面布局，并为 "团队" 选项卡提供完整页面体验：</span><span class="sxs-lookup"><span data-stu-id="ede3e-156">This converts the current page into an App Page, showing the normal SharePoint page layout with a full-page experience for the Teams tab:</span></span>

![Sharepoint 中选项卡的图像](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="more-information"></a><span data-ttu-id="ede3e-158">详细信息</span><span class="sxs-lookup"><span data-stu-id="ede3e-158">More information</span></span>

- [<span data-ttu-id="ede3e-159">使用 SharePoint 框架生成 Microsoft Teams 选项卡 - 教程</span><span class="sxs-lookup"><span data-stu-id="ede3e-159">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [<span data-ttu-id="ede3e-160">在 SharePoint Online 中使用单个部件应用程序页面</span><span class="sxs-lookup"><span data-stu-id="ede3e-160">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
