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
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a>在 SharePoint 中将 Microsoft 团队选项卡添加为 SPFx web 部件

## <a name="rich-integration-between-teams-and-sharepoint"></a>团队和 SharePoint 之间的丰富集成

在11月发布的团队和 SharePoint Framework 2007 中。 1.7，开发人员具有两项强大的功能：

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
                        <h3>SharePoint 中的团队选项卡</h3>
                        <p>通过将团队应用引入 Sharepoint (本文) ，在 SharePoint 中创建丰富的应用程序体验。</p>
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
                        <h3>团队中的 SharePoint 框架</h3>
                        <p>将 SharePoint web 部件引入团队，让 SharePoint 为您管理托管。</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>SharePoint 中的团队选项卡

通过 SharePoint Framework 1.7 版，我们现在支持开发人员将其团队选项卡和托管在 SharePoint 中。 作为 SharePoint 中托管的选项卡获取类似的 "整页" 体验，从而公开了 "团队" 选项卡的所有功能，同时保留了 SharePoint 网站的上下文和熟悉程度。

### <a name="sharepoint-framework-in-teams"></a>团队中的 SharePoint 框架

您还可以使用 SharePoint 框架实施 Microsoft 团队选项卡。 对于 SharePoint 开发人员，这极大地简化了团队选项卡的开发过程，因为 SharePoint 框架 web 部件托管在 SharePoint 中，无需任何外部服务（如 Azure）。 [了解有关在团队中使用 SharePoint 框架的详细信息。](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>简介

这些说明将介绍如何从 Microsoft 团队示例应用中获取一个选项卡，并在 SharePoint 中使用它。 我们将使用 Azure 上已托管的选项卡，以将重点放在所需的集成工作上。

我们正在使用的示例应用是一个人才管理应用程序。 它管理团队中打开职位的候选人的聘用过程。  (应用程序本身，尽管它看起来不错，但实际上并不会执行任何操作。 我们希望将重点放在团队应用程序上，并将其加载到团队中，而不是创建真实的人才管理应用程序。 ) 

### <a name="benefits-of-this-approach"></a>此方法的优点

- 使用现有团队选项卡访问 SharePoint 用户
- 将您的应用程序清单直接上传到 SharePoint 应用程序目录。 [团队应用程序包](~/concepts/build-and-test/apps-package.md) 现已由 SharePoint 支持
- 最终用户在页面上配置选项卡的方式与任何其他 SharePoint web 部件一样
- 您的选项卡可以像在团队中运行一样访问其[上下文](~/tabs/how-to/access-teams-context.md)

## <a name="step-1-testing-the-sample-app"></a>步骤1：测试示例应用程序

从 [**此处**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)下载示例应用程序清单。

在 Microsoft 团队中，单击左下角的 "存储" 图标，然后在左下角 "上载自定义应用"。 要上载的文件将位于您的 "下载" 文件夹中。它被称为 TalentMgmt-Azure.zip。 如果一切正常，你将看到 "人才管理" 应用程序的 "安装/同意" 屏幕。 选择要安装到的团队，然后单击 "安装" 按钮。 现在，你可以免费试用该应用。

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a>步骤2：使用 SharePoint 中的 "团队" 选项卡

通过访问将团队应用程序包上载并部署到 SharePoint 应用程序目录 `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 中，例如 `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 。

出现提示时，启用 "使此解决方案可用于组织中的所有站点"：

![Sharepoint 视图中的选项卡](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

在网站中，单击右上角的 "齿轮" 按钮以创建新页面，然后单击 "添加页面"：

![Sharepoint 视图](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

你将看到 SharePoint 页面创作体验。 将页面命名为 "我的团队选项卡"。

按 "+" 按钮打开 "web 部件工具箱"，然后选择名为 "Contoso HR" 的 "团队" 选项卡 () 。 Web 部件按字母顺序排序;如果是较长的列表，则可以使用搜索栏查找它。 这将在包含 "团队" 选项卡的画布中创建 web 部件：

![选项卡视图](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

完成编辑后，请按 "发布" 按钮。

您可能需要单击 "将页面添加到导航" 以快速引用左侧导航栏中的页面：

![Sharepoint 图像中的选项卡](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a>步骤3：浏览 SharePoint 中的应用程序页

发布页面后，您可以浏览在 [SharePoint 中将团队应用程序转变成更全面的体验](/sharepoint/dev/spfx/web-parts/single-part-app-pages)。 此操作会将当前页面转换为应用程序页面，显示常规 SharePoint 页面布局，并为 "团队" 选项卡提供完整页面体验：

![Sharepoint 中选项卡的图像](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="more-information"></a>详细信息

- [使用 SharePoint 框架生成 Microsoft Teams 选项卡 - 教程](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [在 SharePoint Online 中使用单个部件应用程序页面](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
