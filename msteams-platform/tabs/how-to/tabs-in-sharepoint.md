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
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a>在 SharePoint 中添加 Microsoft Teams 选项卡作为 SPFx Web 部件

## <a name="rich-integration-between-teams-and-sharepoint"></a>Teams 和 SharePoint 之间的丰富集成

在 11 月发布的 Teams 和 SharePoint 框架 v 中。 1.7，开发人员具有两个强大的功能：

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
                        <h3>SharePoint 中的 Teams 选项卡</h3>
                        <p>通过将 Teams 应用引入 Sharepoint，在 SharePoint 中 (丰富的应用) 。</p>
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
                        <h3>Teams 中的 SharePoint 框架</h3>
                        <p>将 SharePoint Web 部件引入 Teams，让 SharePoint 管理托管服务。</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>SharePoint 中的 Teams 选项卡

借助 SharePoint Framework v.1.7，我们现在支持开发人员使用 Teams 选项卡，在 SharePoint 中托管它。 由于 SharePoint 中托管的选项卡获得类似的"完整页面"体验，公开 Teams 选项卡的所有功能，同时保留 SharePoint 网站的上下文和熟悉度。

### <a name="sharepoint-framework-in-teams"></a>Teams 中的 SharePoint 框架

您还可以使用 SharePoint 框架实现 Microsoft Teams 选项卡。 对于 SharePoint 开发人员，这大大简化了 Teams 选项卡的开发过程，因为 SharePoint 框架 Web 部件托管在 SharePoint 中，无需任何外部服务（如 Azure）。 [了解有关在 Teams 中使用 SharePoint 框架有关详细信息。](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>简介

这些说明将介绍如何从 Microsoft Teams 示例应用程序中使用选项卡，以及如何在 SharePoint 中使用它。 我们将使用已托管在 Azure 上的选项卡，以便专注于所需的集成工作。

我们使用的示例应用是一个"人才管理"应用程序。 它管理团队中打开职位的应聘者的招聘流程。  (应用本身虽然看起来不错，但实际上并没有执行任何操作。 我们希望专注于生成 Teams 应用并加载到 Teams 中，而不是创建真正的人才管理应用程序。) 

### <a name="benefits-of-this-approach"></a>此方法的好处

- 使用现有的 Teams 选项卡联系 SharePoint 用户
- 将应用程序清单直接上载到 SharePoint 应用程序目录。 [SharePoint](~/concepts/build-and-test/apps-package.md) 现在支持 Teams 应用程序包
- 最终用户在页面上配置选项卡，就像任何其他 SharePoint Web 部件一样
- 选项卡可以访问其 [上下文，](~/tabs/how-to/access-teams-context.md) 就像在 Teams 内运行时一样

## <a name="step-1-testing-the-sample-app"></a>步骤 1：测试示例应用

从此处下载示例应用 [**清单**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)。

在 Microsoft Teams 中，单击左下角的应用商店图标，然后在左下角单击"上载自定义应用"。 要上载的文件将位于"下载"文件夹中;它称为TalentMgmt-Azure.zip。 如果一切顺利，你将看到人才管理应用的安装/同意屏幕。 选择要安装到的团队，然后单击"安装"按钮。 你现在可以随意试用该应用。

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a>步骤 2：在 SharePoint 中使用 Teams 选项卡

通过访问（例如）将 Teams 应用包上载并部署到 SharePoint 应用程序 `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 目录 `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 。

当系统提示时，启用"使此解决方案对组织内的所有网站可用"：

![Sharepoint 视图中的选项卡](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

在网站中，单击右上角的齿轮按钮，然后"添加页面"，创建新页面：

![Sharepoint 视图](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

你将看到 SharePoint 页面创作体验。 将你的页面命名为"我的 Teams 选项卡"。

通过按 + 按钮打开 Web 部件工具箱，然后选择名为"Contoso HR" (Teams 选项卡) 。 Web 部件按字母顺序排序;如果是长列表，可以使用搜索栏查找它。 这将在包含 Teams 选项卡的画布上创建 Web 部件：

![选项卡视图](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

完成编辑后，按"发布"按钮。

您可能需要单击"向导航添加页面"，以在左侧导航栏中快速引用页面：

![Sharepoint 图像中的选项卡](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a>步骤 3：在 SharePoint 中浏览应用程序页面

发布页面后，你可以探索在 SharePoint 内将 Teams 应用转变为 [更完整的体验](/sharepoint/dev/spfx/web-parts/single-part-app-pages)。 这会将当前页面转换为应用程序页，显示具有 Teams 选项卡完整页面体验的正常 SharePoint 页面布局：

![Sharepoint 中选项卡的图像](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>代码示例
| **示例名称** | **说明** | **SPFx** |
|-----------------|-----------------|----------|
| SPFx Web 部件 | 选项卡、通道和组的 SPFx Web 部件示例。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="more-information"></a>更多信息

- [使用 SharePoint 框架生成 Microsoft Teams 选项卡 - 教程](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [在 SharePoint Online 中使用单个部件应用程序页面](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
