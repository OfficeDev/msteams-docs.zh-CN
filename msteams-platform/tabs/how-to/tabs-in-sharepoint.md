---
title: 在 SharePoint 中添加 Microsoft Teams 选项卡作为 SPFx Web 部件
author: laujan
description: 如何将现有 Teams 选项卡作为 SharePoint 框架 Web 部件部署到 SharePoint。
keywords: teams 选项卡 sharepoint 框架开发
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2e5d1b01aa5f7566e25c7720d6a0539386226576
ms.sourcegitcommit: 6caf503de5544fb8b9c8c6bef8eff4ff5a46068c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/17/2021
ms.locfileid: "50270789"
---
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a><span data-ttu-id="6de12-104">在 SharePoint 中添加 Microsoft Teams 选项卡作为 SPFx Web 部件</span><span class="sxs-lookup"><span data-stu-id="6de12-104">Adding a Microsoft Teams tab in SharePoint as an SPFx web part</span></span>

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="6de12-105">Teams 和 SharePoint 之间的丰富集成</span><span class="sxs-lookup"><span data-stu-id="6de12-105">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="6de12-106">在 11 月发布的 Teams 和 SharePoint 框架 v 中。</span><span class="sxs-lookup"><span data-stu-id="6de12-106">With the November release of Teams and SharePoint Framework v.</span></span> <span data-ttu-id="6de12-107">1.7，开发人员具有两个强大的功能：</span><span class="sxs-lookup"><span data-stu-id="6de12-107">1.7, developers have two powerful capabilities:</span></span>

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
                        <h3><span data-ttu-id="6de12-108">SharePoint 中的 Teams 选项卡</span><span class="sxs-lookup"><span data-stu-id="6de12-108">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="6de12-109">通过将 Teams 应用引入 Sharepoint，在 SharePoint 中 (丰富的应用) 。</span><span class="sxs-lookup"><span data-stu-id="6de12-109">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
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
                        <h3><span data-ttu-id="6de12-110">Teams 中的 SharePoint 框架</span><span class="sxs-lookup"><span data-stu-id="6de12-110">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="6de12-111">将 SharePoint Web 部件引入 Teams，让 SharePoint 管理托管服务。</span><span class="sxs-lookup"><span data-stu-id="6de12-111">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="6de12-112">SharePoint 中的 Teams 选项卡</span><span class="sxs-lookup"><span data-stu-id="6de12-112">Teams tabs in SharePoint</span></span>

<span data-ttu-id="6de12-113">借助 SharePoint Framework v.1.7，我们现在支持开发人员使用 Teams 选项卡，在 SharePoint 中托管它。</span><span class="sxs-lookup"><span data-stu-id="6de12-113">With SharePoint Framework v.1.7, we’re now supporting the ability for developers to take their Teams tabs and host it in SharePoint.</span></span> <span data-ttu-id="6de12-114">由于 SharePoint 中托管的选项卡获得类似的"完整页面"体验，公开 Teams 选项卡的所有功能，同时保留 SharePoint 网站的上下文和熟悉度。</span><span class="sxs-lookup"><span data-stu-id="6de12-114">As Tabs hosted in SharePoint get a similar "full page" experience, exposing the all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="6de12-115">Teams 中的 SharePoint 框架</span><span class="sxs-lookup"><span data-stu-id="6de12-115">SharePoint Framework in Teams</span></span>

<span data-ttu-id="6de12-116">您还可以使用 SharePoint 框架实现 Microsoft Teams 选项卡。</span><span class="sxs-lookup"><span data-stu-id="6de12-116">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="6de12-117">对于 SharePoint 开发人员，这大大简化了 Teams 选项卡的开发过程，因为 SharePoint 框架 Web 部件托管在 SharePoint 中，无需任何外部服务（如 Azure）。</span><span class="sxs-lookup"><span data-stu-id="6de12-117">For SharePoint developers, this significantly simplifies the development process for Teams tabs because SharePoint Framework web parts are hosted within SharePoint without any need for external services such as Azure.</span></span> [<span data-ttu-id="6de12-118">了解有关在 Teams 中使用 SharePoint 框架有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="6de12-118">Learn more about using the SharePoint Framework in Teams.</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a><span data-ttu-id="6de12-119">简介</span><span class="sxs-lookup"><span data-stu-id="6de12-119">Introduction</span></span>

<span data-ttu-id="6de12-120">这些说明将介绍如何从 Microsoft Teams 示例应用程序中使用选项卡，以及如何在 SharePoint 中使用它。</span><span class="sxs-lookup"><span data-stu-id="6de12-120">These instructions will explain how you can take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> <span data-ttu-id="6de12-121">我们将使用已托管在 Azure 上的选项卡，以便专注于所需的集成工作。</span><span class="sxs-lookup"><span data-stu-id="6de12-121">We will be using a tab that's already hosted on Azure in order to focus on the required integration work.</span></span>

<span data-ttu-id="6de12-122">我们使用的示例应用是一个"人才管理"应用程序。</span><span class="sxs-lookup"><span data-stu-id="6de12-122">The sample app we're using is a Talent Management application.</span></span> <span data-ttu-id="6de12-123">它管理团队中打开职位的应聘者的招聘流程。</span><span class="sxs-lookup"><span data-stu-id="6de12-123">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="6de12-124"> (应用本身虽然看起来不错，但实际上并没有执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="6de12-124">(The app itself, while it looks nice, doesn't actually do anything.</span></span> <span data-ttu-id="6de12-125">我们希望专注于生成 Teams 应用并加载到 Teams 中，而不是创建真正的人才管理应用程序。) </span><span class="sxs-lookup"><span data-stu-id="6de12-125">We want to focus on building a Teams app and loading it into Teams, not create a real talent management application.)</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="6de12-126">此方法的好处</span><span class="sxs-lookup"><span data-stu-id="6de12-126">Benefits of this approach</span></span>

- <span data-ttu-id="6de12-127">使用现有的 Teams 选项卡联系 SharePoint 用户</span><span class="sxs-lookup"><span data-stu-id="6de12-127">Reach SharePoint users with your existing Teams tab</span></span>
- <span data-ttu-id="6de12-128">将应用程序清单直接上载到 SharePoint 应用程序目录。</span><span class="sxs-lookup"><span data-stu-id="6de12-128">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="6de12-129">[SharePoint](~/concepts/build-and-test/apps-package.md) 现在支持 Teams 应用程序包</span><span class="sxs-lookup"><span data-stu-id="6de12-129">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint</span></span>
- <span data-ttu-id="6de12-130">最终用户在页面上配置选项卡，就像任何其他 SharePoint Web 部件一样</span><span class="sxs-lookup"><span data-stu-id="6de12-130">End users configure the tab on a page just like any other SharePoint web part</span></span>
- <span data-ttu-id="6de12-131">选项卡可以访问其 [上下文，](~/tabs/how-to/access-teams-context.md) 就像在 Teams 内运行时一样</span><span class="sxs-lookup"><span data-stu-id="6de12-131">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) just as it can when running inside Teams</span></span>

## <a name="step-1-testing-the-sample-app"></a><span data-ttu-id="6de12-132">步骤 1：测试示例应用</span><span class="sxs-lookup"><span data-stu-id="6de12-132">Step 1: Testing the sample app</span></span>

<span data-ttu-id="6de12-133">从此处下载示例应用 [**清单**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)。</span><span class="sxs-lookup"><span data-stu-id="6de12-133">Download the sample app manifest from [**here**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

<span data-ttu-id="6de12-134">在 Microsoft Teams 中，单击左下角的应用商店图标，然后在左下角单击"上载自定义应用"。</span><span class="sxs-lookup"><span data-stu-id="6de12-134">In Microsoft Teams, click on the Store icon at the lower left and then "Upload a custom app" at the lower left.</span></span> <span data-ttu-id="6de12-135">要上载的文件将位于"下载"文件夹中;它称为TalentMgmt-Azure.zip。</span><span class="sxs-lookup"><span data-stu-id="6de12-135">The file to upload will be located in your Downloads folder; it's called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="6de12-136">如果一切顺利，你将看到人才管理应用的安装/同意屏幕。</span><span class="sxs-lookup"><span data-stu-id="6de12-136">If all goes well, you'll see the install/consent screen for the talent management app.</span></span> <span data-ttu-id="6de12-137">选择要安装到的团队，然后单击"安装"按钮。</span><span class="sxs-lookup"><span data-stu-id="6de12-137">Choose the team you want to install to and click the Install button.</span></span> <span data-ttu-id="6de12-138">你现在可以随意试用该应用。</span><span class="sxs-lookup"><span data-stu-id="6de12-138">You're now free to experiment with the app.</span></span>

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a><span data-ttu-id="6de12-139">步骤 2：在 SharePoint 中使用 Teams 选项卡</span><span class="sxs-lookup"><span data-stu-id="6de12-139">Step 2: Using the Teams tab in SharePoint</span></span>

<span data-ttu-id="6de12-140">通过访问（例如）将 Teams 应用包上载并部署到 SharePoint 应用程序 `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 目录 `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 。</span><span class="sxs-lookup"><span data-stu-id="6de12-140">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`, e.g. `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

<span data-ttu-id="6de12-141">当系统提示时，启用"使此解决方案对组织内的所有网站可用"：</span><span class="sxs-lookup"><span data-stu-id="6de12-141">When prompted, enable "Make this solution available to all sites in the organization":</span></span>

![Sharepoint 视图中的选项卡](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

<span data-ttu-id="6de12-143">在网站中，单击右上角的齿轮按钮，然后"添加页面"，创建新页面：</span><span class="sxs-lookup"><span data-stu-id="6de12-143">In your site, create a new page by clicking in the gear button at the upper right and then "Add a page":</span></span>

![Sharepoint 视图](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

<span data-ttu-id="6de12-145">你将看到 SharePoint 页面创作体验。</span><span class="sxs-lookup"><span data-stu-id="6de12-145">You'll see the SharePoint Pages authoring experience.</span></span> <span data-ttu-id="6de12-146">将你的页面命名为"我的 Teams 选项卡"。</span><span class="sxs-lookup"><span data-stu-id="6de12-146">Name your page "My Teams Tab".</span></span>

<span data-ttu-id="6de12-147">通过按 + 按钮打开 Web 部件工具箱，然后选择名为"Contoso HR" (Teams 选项卡) 。</span><span class="sxs-lookup"><span data-stu-id="6de12-147">Open the web part toolbox by pressing the + button, and select your Teams Tab (named "Contoso HR").</span></span> <span data-ttu-id="6de12-148">Web 部件按字母顺序排序;如果是长列表，可以使用搜索栏查找它。</span><span class="sxs-lookup"><span data-stu-id="6de12-148">Web parts are sorted alphabetically; if it's a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="6de12-149">这将在包含 Teams 选项卡的画布上创建 Web 部件：</span><span class="sxs-lookup"><span data-stu-id="6de12-149">This will create a web part in the canvas that contains your Teams tab:</span></span>

![选项卡视图](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

<span data-ttu-id="6de12-151">完成编辑后，按"发布"按钮。</span><span class="sxs-lookup"><span data-stu-id="6de12-151">Press the "Publish" button when you are finished editing.</span></span>

<span data-ttu-id="6de12-152">您可能需要单击"向导航添加页面"，以在左侧导航栏中快速引用页面：</span><span class="sxs-lookup"><span data-stu-id="6de12-152">You may want to click "Add page to navigation" to have a quick reference to your page in the left navigation bar:</span></span>

![Sharepoint 图像中的选项卡](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="6de12-154">步骤 3：在 SharePoint 中浏览应用程序页面</span><span class="sxs-lookup"><span data-stu-id="6de12-154">Step 3: Explore App Pages in SharePoint</span></span>

<span data-ttu-id="6de12-155">发布页面后，你可以探索在 SharePoint 内将 Teams 应用转变为 [更完整的体验](/sharepoint/dev/spfx/web-parts/single-part-app-pages)。</span><span class="sxs-lookup"><span data-stu-id="6de12-155">Once your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="6de12-156">这会将当前页面转换为应用程序页，显示具有 Teams 选项卡完整页面体验的正常 SharePoint 页面布局：</span><span class="sxs-lookup"><span data-stu-id="6de12-156">This converts the current page into an App Page, showing the normal SharePoint page layout with a full-page experience for the Teams tab:</span></span>

![Sharepoint 中选项卡的图像](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a><span data-ttu-id="6de12-158">代码示例</span><span class="sxs-lookup"><span data-stu-id="6de12-158">Code sample</span></span>
| <span data-ttu-id="6de12-159">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="6de12-159">**Sample name**</span></span> | <span data-ttu-id="6de12-160">**说明**</span><span class="sxs-lookup"><span data-stu-id="6de12-160">**Description**</span></span> | <span data-ttu-id="6de12-161">**SPFx**</span><span class="sxs-lookup"><span data-stu-id="6de12-161">**SPFx**</span></span> |
|-----------------|-----------------|----------|
| <span data-ttu-id="6de12-162">SPFx Web 部件</span><span class="sxs-lookup"><span data-stu-id="6de12-162">SPFx web part</span></span> | <span data-ttu-id="6de12-163">选项卡、通道和组的 SPFx Web 部件示例。</span><span class="sxs-lookup"><span data-stu-id="6de12-163">SPFx web part samples for tabs, channels, and groups.</span></span> | [<span data-ttu-id="6de12-164">View</span><span class="sxs-lookup"><span data-stu-id="6de12-164">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="more-information"></a><span data-ttu-id="6de12-165">更多信息</span><span class="sxs-lookup"><span data-stu-id="6de12-165">More information</span></span>

- [<span data-ttu-id="6de12-166">使用 SharePoint 框架生成 Microsoft Teams 选项卡 - 教程</span><span class="sxs-lookup"><span data-stu-id="6de12-166">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [<span data-ttu-id="6de12-167">在 SharePoint Online 中使用单个部件应用程序页面</span><span class="sxs-lookup"><span data-stu-id="6de12-167">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
