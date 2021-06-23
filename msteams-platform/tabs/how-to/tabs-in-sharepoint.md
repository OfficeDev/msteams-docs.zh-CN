---
title: 将 Teams 选项卡添加到 SharePoint
author: surbhigupta
description: 如何将现有"Teams"选项卡SharePoint Web SharePoint 框架部件。
keywords: teams 选项卡 sharepoint 框架开发
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 6720cf3fdc8a02d325bf775f4bf319b9d07ec17c
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068648"
---
# <a name="add-teams-tab-to-sharepoint"></a>将 Teams 选项卡添加到 SharePoint 

通过将 Microsoft Teams 中的 Microsoft Teams 选项卡添加为 SharePoint Web 部件，Microsoft Teams和 SharePoint 之间SPFx丰富的集成体验。 本文档指导您如何从示例应用中Microsoft Teams选项卡，以及如何在 SharePoint。 

## <a name="rich-integration-between-teams-and-sharepoint"></a>Teams 和 SharePoint

在 11 月发布的 Teams 和 SharePoint 框架 v.1.7 版中，开发人员具有两项强大的功能：

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
                        <h3>Teams选项卡在SharePoint</h3>
                        <p>本文将介绍的SharePoint sharepoint Teams，在 sharepoint (丰富的) 。</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li>
    <a href="/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/SharePoint-web-part-exposed-as-a-Tab-in-Microsoft-Teams.png" alt="web-part-exposed-as-a-tab" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>SharePoint 框架Teams</h3>
                        <p>将 SharePoint Web 部件Teams，SharePoint管理托管。</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>Teams选项卡SharePoint

使用 SharePoint 框架 v.1.7，可以在 SharePoint 中托管Teams选项卡。 作为托管在 SharePoint的选项卡获得类似的完整页面体验，公开 Teams 选项卡的所有功能，同时保留 SharePoint 网站的上下文和熟悉度。

### <a name="sharepoint-framework-in-teams"></a>SharePoint 框架Teams

您还可以使用 Microsoft Teams 实现SharePoint 框架。 SharePoint 框架 Web 部件托管在 SharePoint中，无需任何外部服务，如 Azure。 对于SharePoint开发人员来说，这大大简化了选项卡Teams过程。 有关 SharePoint 框架 中Teams，请参阅如何使用 SharePoint 框架 中的[Teams。](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>简介

此处使用的选项卡已托管在 Azure 上，侧重于所需的集成工作。

使用的示例应用是一个"人才管理"应用程序。 它管理团队中职位候选人的招聘流程。 生成一个Teams应用，并加载到Teams。 不要创建真实的人才管理应用程序。

### <a name="benefits-of-this-approach"></a>此方法的好处

* 使用SharePoint选项卡联系Teams用户。
* Upload将应用程序清单直接SharePoint应用程序目录。 [Teams应用程序包](~/concepts/build-and-test/apps-package.md)现在受 SharePoint。
* 用户配置页面上的选项卡，就像任何其他 web SharePoint一样。
* 当在页面内[运行时](~/tabs/how-to/access-teams-context.md)，选项卡可以访问其Teams。

**将Teams选项卡添加到SharePoint**

执行以下步骤以将"Teams"选项卡SharePoint：

## <a name="1-test-the-sample-app"></a>1. 测试示例应用程序

下载 [示例应用清单](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)。

1. 打开 Microsoft Teams。
1. 选择 **"旁** "选项卡左下角的"应用商店"图标。
1. 选择 **Upload左侧选择** 自定义应用。 下图显示了相应的屏幕：  

    ![上传自定义应用](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. 要上载的文件位于"下载 **"** 文件夹中。 它称为TalentMgmt-Azure.zip。 下图显示了相应的屏幕：
 
    ![Azure 中的 TalentMgmt](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. 你可以看到人才管理应用的安装或许可屏幕。 选择要安装的团队。 
1. 选择 **安装** 并开始对应用进行试验。

## <a name="2-use-teams-tab-in-sharepoint"></a>2. 使用Teams中的"SharePoint

1. Upload 访问 ，Teams应用程序包SharePoint应用程序目录 `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 。 例如，`https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`。

1. 当系统提示时，启用 **"使此解决方案对组织的所有网站都可用"。**
下图显示了相应的屏幕：

   ![Sharepoint 视图中的选项卡](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. 在网站中，选择右上角的齿轮按钮，然后选择"添加页面"，以 **创建新页面**。
下图显示了相应的屏幕：

   ![Sharepoint 视图](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. You can see the SharePoint pages authoring experience. 将页面名称为 **"我的Teams选项卡"。**

1. 通过按按钮打开 Web 部件工具箱，然后选择Teams `+` 选项卡，名为 **Contoso HR**。 Web 部件按字母顺序排序。 如果是长列表，可以使用搜索栏来查找它。 这将在画布上创建一个 Web 部件，其中包含Teams选项卡。下图显示了选项卡视图：

   ![选项卡视图](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. 编辑 **完成后，** 按"发布"按钮。

1. 选择 **"将页面添加到导航** "，在左侧导航栏中快速引用页面。 下图显示了 Sharepoint 中的选项卡： 

   ![Sharepoint 图像中的选项卡](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a>3. 在应用程序中浏览SharePoint

发布页面后，你可以探索将Teams[应用转换为更完整的](/sharepoint/dev/spfx/web-parts/single-part-app-pages)SharePoint。 这会将当前页面转换为"应用页面"，以"SharePoint"选项卡的完整页面体验显示正常页面Teams布局。 

下图显示了 Sharepoint 中选项卡Teams的完整 ![ 体验：Sharepoint 中的选项卡图像](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>代码示例
| **示例名称** | **说明** | **SPFx** |
|-----------------|-----------------|----------|
| SPFx Web 部件 | SPFx、通道和组的 Web 部件示例。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a>另请参阅

* [使用 SharePoint 框架生成 Microsoft Teams 选项卡 - 教程](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
* [在 SharePoint Online 中使用单个部件应用程序页面](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
* [集成 web 应用](~/samples/integrate-web-apps-overview.md)
