---
title: 将 Teams 选项卡添加到 SharePoint
author: laujan
description: 如何将现有 Teams 选项卡作为 SharePoint 框架 Web 部件部署到 SharePoint。
keywords: teams 选项卡 sharepoint 框架开发
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 08a4aef329d0e5e1d063f05959f0a589581c9c03
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020319"
---
# <a name="add-teams-tab-to-sharepoint"></a><span data-ttu-id="94bda-104">将 Teams 选项卡添加到 SharePoint</span><span class="sxs-lookup"><span data-stu-id="94bda-104">Add Teams tab to SharePoint</span></span> 

<span data-ttu-id="94bda-105">通过将 SharePoint 中的"Microsoft Teams"选项卡添加为 SPFx Web 部件，可以在 Microsoft Teams 和 SharePoint 之间获得丰富的集成体验。</span><span class="sxs-lookup"><span data-stu-id="94bda-105">You can get a rich integration experience between Microsoft Teams and SharePoint by adding a Microsoft Teams tab in SharePoint as an SPFx web part.</span></span> <span data-ttu-id="94bda-106">本文档将指导你了解如何从 Microsoft Teams 示例应用中使用选项卡，以及如何在 SharePoint 中使用它。</span><span class="sxs-lookup"><span data-stu-id="94bda-106">This document guides you on how you to take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> 

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="94bda-107">Teams 和 SharePoint 之间的丰富集成</span><span class="sxs-lookup"><span data-stu-id="94bda-107">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="94bda-108">在 11 月发布的 Teams 和 SharePoint 框架 v.1.7 中，开发人员具有两项强大的功能：</span><span class="sxs-lookup"><span data-stu-id="94bda-108">With the November release of Teams and SharePoint Framework v.1.7, developers have two powerful capabilities:</span></span>

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
                        <h3><span data-ttu-id="94bda-109">SharePoint 中的 Teams 选项卡</span><span class="sxs-lookup"><span data-stu-id="94bda-109">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="94bda-110">通过将 Teams 应用引入 Sharepoint，在 SharePoint 中 (丰富的应用) 。</span><span class="sxs-lookup"><span data-stu-id="94bda-110">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
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
                        <h3><span data-ttu-id="94bda-111">Teams 中的 SharePoint 框架</span><span class="sxs-lookup"><span data-stu-id="94bda-111">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="94bda-112">将 SharePoint Web 部件引入 Teams，让 SharePoint 管理托管。</span><span class="sxs-lookup"><span data-stu-id="94bda-112">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="94bda-113">SharePoint 中的 Teams 选项卡</span><span class="sxs-lookup"><span data-stu-id="94bda-113">Teams tabs in SharePoint</span></span>

<span data-ttu-id="94bda-114">借助 SharePoint 框架 v.1.7，可以在 SharePoint 中托管 Teams 选项卡。</span><span class="sxs-lookup"><span data-stu-id="94bda-114">With SharePoint Framework v.1.7, you can host your Teams tabs in SharePoint.</span></span> <span data-ttu-id="94bda-115">由于 SharePoint 中托管的选项卡获得类似的完整页面体验，因此在保留 SharePoint 网站的上下文和熟悉度的同时公开 Teams 选项卡的所有功能。</span><span class="sxs-lookup"><span data-stu-id="94bda-115">As tabs hosted in SharePoint get a similar **full page** experience, exposing all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="94bda-116">Teams 中的 SharePoint 框架</span><span class="sxs-lookup"><span data-stu-id="94bda-116">SharePoint Framework in Teams</span></span>

<span data-ttu-id="94bda-117">还可使用 SharePoint 框架实现 Microsoft Teams 选项卡。</span><span class="sxs-lookup"><span data-stu-id="94bda-117">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="94bda-118">SharePoint 框架 Web 部件托管在 SharePoint 中，无需任何外部服务，如 Azure。</span><span class="sxs-lookup"><span data-stu-id="94bda-118">SharePoint Framework web parts are hosted within SharePoint without any need for external services, such as Azure.</span></span> <span data-ttu-id="94bda-119">对于 SharePoint 开发人员，这大大简化了 Teams 选项卡的开发过程。</span><span class="sxs-lookup"><span data-stu-id="94bda-119">For SharePoint developers, this significantly simplifies the development process for Teams tabs.</span></span> <span data-ttu-id="94bda-120">有关 Teams 中的 SharePoint 框架详细信息，请参阅如何在 Teams 中使用 [SharePoint 框架。](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)</span><span class="sxs-lookup"><span data-stu-id="94bda-120">For more information on SharePoint Framework in Teams, see [how to use the SharePoint Framework in Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)</span></span>

## <a name="introduction"></a><span data-ttu-id="94bda-121">简介</span><span class="sxs-lookup"><span data-stu-id="94bda-121">Introduction</span></span>

<span data-ttu-id="94bda-122">此处使用的选项卡已托管在 Azure 上，侧重于所需的集成工作。</span><span class="sxs-lookup"><span data-stu-id="94bda-122">The tab used here is already hosted on Azure, to focus on the required integration work.</span></span>

<span data-ttu-id="94bda-123">使用的示例应用是一个"人才管理"应用程序。</span><span class="sxs-lookup"><span data-stu-id="94bda-123">The sample app that is being used is a Talent Management application.</span></span> <span data-ttu-id="94bda-124">它管理团队中职位候选人的招聘流程。</span><span class="sxs-lookup"><span data-stu-id="94bda-124">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="94bda-125">生成示例 Teams 应用，并加载到 Teams 中。</span><span class="sxs-lookup"><span data-stu-id="94bda-125">Build a sample Teams app and load it into Teams.</span></span> <span data-ttu-id="94bda-126">不要创建真实的人才管理应用程序。</span><span class="sxs-lookup"><span data-stu-id="94bda-126">Do not create a real talent management application.</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="94bda-127">此方法的好处</span><span class="sxs-lookup"><span data-stu-id="94bda-127">Benefits of this approach</span></span>

* <span data-ttu-id="94bda-128">使用现有的"Teams"选项卡联系 SharePoint 用户。</span><span class="sxs-lookup"><span data-stu-id="94bda-128">Reach SharePoint users with your existing Teams tab.</span></span>
* <span data-ttu-id="94bda-129">将应用程序清单直接上载到 SharePoint 应用程序目录。</span><span class="sxs-lookup"><span data-stu-id="94bda-129">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="94bda-130">[SharePoint](~/concepts/build-and-test/apps-package.md) 现在支持 Teams 应用程序包。</span><span class="sxs-lookup"><span data-stu-id="94bda-130">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint.</span></span>
* <span data-ttu-id="94bda-131">用户像配置任何其他 SharePoint Web 部件一样在页面上配置选项卡。</span><span class="sxs-lookup"><span data-stu-id="94bda-131">The users configure the tab on a page just like any other SharePoint web part.</span></span>
* <span data-ttu-id="94bda-132">在 Teams 内 [运行时，](~/tabs/how-to/access-teams-context.md) 你的选项卡可以访问其上下文，也可以。</span><span class="sxs-lookup"><span data-stu-id="94bda-132">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) sameas it can, when running inside Teams.</span></span>

<span data-ttu-id="94bda-133">**将 Teams 选项卡添加到 SharePoint**</span><span class="sxs-lookup"><span data-stu-id="94bda-133">**To add Teams tab to SharePoint**</span></span>

<span data-ttu-id="94bda-134">执行以下步骤以将 Teams 选项卡添加到 SharePoint：</span><span class="sxs-lookup"><span data-stu-id="94bda-134">Perform the following steps to add Teams tab to SharePoint:</span></span>

## <a name="1-test-the-sample-app"></a><span data-ttu-id="94bda-135">1. 测试示例应用程序</span><span class="sxs-lookup"><span data-stu-id="94bda-135">1. Test the sample app</span></span>

<span data-ttu-id="94bda-136">下载 [示例应用清单](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)。</span><span class="sxs-lookup"><span data-stu-id="94bda-136">Download the [sample app manifest](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

1. <span data-ttu-id="94bda-137">打开 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="94bda-137">Open Microsoft Teams.</span></span>
1. <span data-ttu-id="94bda-138">选择 **"旁** "选项卡左下角的"应用商店"图标。</span><span class="sxs-lookup"><span data-stu-id="94bda-138">Select the **Appstore** icon at the lower left of side tab.</span></span>
1. <span data-ttu-id="94bda-139">选择 **左下角的** "上载自定义应用"。</span><span class="sxs-lookup"><span data-stu-id="94bda-139">Select **Upload a custom app** at the lower left.</span></span> <span data-ttu-id="94bda-140">下图显示了相应的屏幕：</span><span class="sxs-lookup"><span data-stu-id="94bda-140">The following image displays the corresponding screen:</span></span>  

    ![上传自定义应用](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. <span data-ttu-id="94bda-142">要上载的文件位于"下载 **"** 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="94bda-142">The file to upload is located in your **Downloads** folder.</span></span> <span data-ttu-id="94bda-143">它称为TalentMgmt-Azure.zip。</span><span class="sxs-lookup"><span data-stu-id="94bda-143">It is called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="94bda-144">下图显示了相应的屏幕：</span><span class="sxs-lookup"><span data-stu-id="94bda-144">The following image displays the corresponding screen:</span></span>
 
    ![Azure 中的 TalentMgmt](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. <span data-ttu-id="94bda-146">你可以看到人才管理应用的安装或许可屏幕。</span><span class="sxs-lookup"><span data-stu-id="94bda-146">You can see the install or consent screen for the talent management app.</span></span> <span data-ttu-id="94bda-147">选择要安装的团队。</span><span class="sxs-lookup"><span data-stu-id="94bda-147">Select the team you want to install.</span></span> 
1. <span data-ttu-id="94bda-148">选择 **安装** 并开始对应用进行试验。</span><span class="sxs-lookup"><span data-stu-id="94bda-148">Select the **Install** and start experimenting with the app.</span></span>

## <a name="2-use-teams-tab-in-sharepoint"></a><span data-ttu-id="94bda-149">2. 在 SharePoint 中使用"Teams"选项卡</span><span class="sxs-lookup"><span data-stu-id="94bda-149">2. Use Teams tab in SharePoint</span></span>

1. <span data-ttu-id="94bda-150">通过访问 将 Teams 应用程序包上载并部署到 SharePoint 应用程序目录 `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 。</span><span class="sxs-lookup"><span data-stu-id="94bda-150">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span> <span data-ttu-id="94bda-151">例如，`https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`。</span><span class="sxs-lookup"><span data-stu-id="94bda-151">For example, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

1. <span data-ttu-id="94bda-152">当系统提示时，启用 **"使此解决方案对组织的所有网站都可用"。**</span><span class="sxs-lookup"><span data-stu-id="94bda-152">When prompted, enable **Make this solution available to all sites in the organization**.</span></span>
<span data-ttu-id="94bda-153">下图显示了相应的屏幕：</span><span class="sxs-lookup"><span data-stu-id="94bda-153">The following image displays the corresponding screen:</span></span>

   ![Sharepoint 视图中的选项卡](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. <span data-ttu-id="94bda-155">在网站中，选择右上角的齿轮按钮，然后选择"添加页面"，以 **创建新页面**。</span><span class="sxs-lookup"><span data-stu-id="94bda-155">In your site, create a new page by selecting the gear button at the upper right and then  select **Add a page**.</span></span>
<span data-ttu-id="94bda-156">下图显示了相应的屏幕：</span><span class="sxs-lookup"><span data-stu-id="94bda-156">The following image displays the corresponding screen:</span></span>

   ![Sharepoint 视图](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. <span data-ttu-id="94bda-158">你可以看到 SharePoint 页面创作体验。</span><span class="sxs-lookup"><span data-stu-id="94bda-158">You can see the SharePoint pages authoring experience.</span></span> <span data-ttu-id="94bda-159">将页面名称为 **"我的团队"选项卡**。</span><span class="sxs-lookup"><span data-stu-id="94bda-159">Name your page as **My Teams Tab**.</span></span>

1. <span data-ttu-id="94bda-160">按按钮打开 Web 部件工具箱 `+` ，然后选择名为 **Contoso HR** 的 Teams 选项卡。</span><span class="sxs-lookup"><span data-stu-id="94bda-160">Open the web part toolbox by pressing the `+` button, and select your Teams Tab, named **Contoso HR**.</span></span> <span data-ttu-id="94bda-161">Web 部件按字母顺序排序。</span><span class="sxs-lookup"><span data-stu-id="94bda-161">Web parts are sorted alphabetically.</span></span> <span data-ttu-id="94bda-162">如果是长列表，可以使用搜索栏来查找它。</span><span class="sxs-lookup"><span data-stu-id="94bda-162">If it is a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="94bda-163">这将在画布上创建一个包含 Teams 选项卡的 Web 部件。下图显示了选项卡视图：</span><span class="sxs-lookup"><span data-stu-id="94bda-163">This creates a web part in the canvas that contains your Teams tab. The following image displays the tab view:</span></span>

   ![选项卡视图](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. <span data-ttu-id="94bda-165">编辑 **完成后，** 按"发布"按钮。</span><span class="sxs-lookup"><span data-stu-id="94bda-165">Press the **Publish** button after you finish  editing.</span></span>

1. <span data-ttu-id="94bda-166">选择 **"将页面添加到导航** "，在左侧导航栏中快速引用页面。</span><span class="sxs-lookup"><span data-stu-id="94bda-166">Select **Add page to navigation** to have a quick reference to your page in the left navigation bar.</span></span> <span data-ttu-id="94bda-167">下图显示了 Sharepoint 中的选项卡：</span><span class="sxs-lookup"><span data-stu-id="94bda-167">The following image displays the tab in Sharepoint:</span></span> 

   ![Sharepoint 图像中的选项卡](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="94bda-169">3. 浏览 SharePoint 中的应用程序页面</span><span class="sxs-lookup"><span data-stu-id="94bda-169">3. Explore App Pages in SharePoint</span></span>

<span data-ttu-id="94bda-170">发布页面后，你可以探索在 SharePoint 内将 Teams 应用转变为 [更完整的体验](/sharepoint/dev/spfx/web-parts/single-part-app-pages)。</span><span class="sxs-lookup"><span data-stu-id="94bda-170">After your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="94bda-171">这会将当前页面转换为应用程序页，显示具有 Teams 选项卡完整页面体验的正常 SharePoint 页面布局。</span><span class="sxs-lookup"><span data-stu-id="94bda-171">This converts the current page into an App Page, showing the normal SharePoint page layout with a full page experience for the Teams tab.</span></span> 

<span data-ttu-id="94bda-172">下图显示了 Sharepoint 中 Teams 应用的完整体验 ![ ：Sharepoint 中的选项卡图像](~/assets/images/tabs/tabs-in-sharepoint/image085.png)</span><span class="sxs-lookup"><span data-stu-id="94bda-172">The following image displays the complete experience of Teams app in Sharepoint: ![Image of Tabs in Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)</span></span>

## <a name="code-sample"></a><span data-ttu-id="94bda-173">代码示例</span><span class="sxs-lookup"><span data-stu-id="94bda-173">Code sample</span></span>
| <span data-ttu-id="94bda-174">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="94bda-174">**Sample name**</span></span> | <span data-ttu-id="94bda-175">**描述**</span><span class="sxs-lookup"><span data-stu-id="94bda-175">**Description**</span></span> | <span data-ttu-id="94bda-176">**SPFx**</span><span class="sxs-lookup"><span data-stu-id="94bda-176">**SPFx**</span></span> |
|-----------------|-----------------|----------|
| <span data-ttu-id="94bda-177">SPFx Web 部件</span><span class="sxs-lookup"><span data-stu-id="94bda-177">SPFx web part</span></span> | <span data-ttu-id="94bda-178">选项卡、通道和组的 SPFx Web 部件示例。</span><span class="sxs-lookup"><span data-stu-id="94bda-178">SPFx web part samples for tabs, channels, and groups.</span></span> | [<span data-ttu-id="94bda-179">View</span><span class="sxs-lookup"><span data-stu-id="94bda-179">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a><span data-ttu-id="94bda-180">另请参阅</span><span class="sxs-lookup"><span data-stu-id="94bda-180">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="94bda-181">使用 SharePoint 框架生成 Microsoft Teams 选项卡 - 教程</span><span class="sxs-lookup"><span data-stu-id="94bda-181">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

> [!div class="nextstepaction"]
> [<span data-ttu-id="94bda-182">在 SharePoint Online 中使用单个部件应用程序页面</span><span class="sxs-lookup"><span data-stu-id="94bda-182">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)

> [!div class="nextstepaction"]
> [<span data-ttu-id="94bda-183">集成 web 应用</span><span class="sxs-lookup"><span data-stu-id="94bda-183">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
