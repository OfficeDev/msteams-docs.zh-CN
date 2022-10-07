---
title: 将 Teams 选项卡添加到 SharePoint
author: surbhigupta
description: 了解如何使用代码示例将现有 Teams 选项卡作为 SharePoint 框架 Web 部件部署到 SharePoint。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 076cf027e2696848319fc0beb7ae69c3633b8dc4
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499193"
---
# <a name="add-teams-tab-to-sharepoint"></a>将 Teams 选项卡添加到 SharePoint

通过在 SharePoint 中将 Microsoft Teams 选项卡添加为 SPFx Web 部件，可以在 Microsoft Teams 和 SharePoint 之间获得丰富的集成体验。 本文档介绍如何从 Microsoft Teams 示例应用获取选项卡并在 SharePoint 中使用它。

## <a name="rich-integration-between-teams-and-sharepoint"></a>Teams 和 SharePoint 之间的丰富集成

随着 11 月 Teams 和 SharePoint Framework v.1.7 的发布，开发人员具有两种强大的功能：

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
                        <p>通过将 Teams 应用引入 SharePoint，在 SharePoint 中创建丰富的应用体验（本文）。</p>
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
                        <h3>Teams 中的 SharePoint 框架</h3>
                        <p>将 SharePoint Web 部件引入 Teams，并让 SharePoint 管理托管。</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>SharePoint 中的 Teams 选项卡

使用 SharePoint 框架 v.1.7，可以在 SharePoint 中托管 Teams 选项卡。 当 SharePoint 中托管的选项卡获得类似的 **完整页面** 体验时，公开 Teams 选项卡的所有功能，同时保留 SharePoint 网站的上下文和熟悉性。

### <a name="sharepoint-framework-in-teams"></a>Teams 中的 SharePoint 框架

还可以使用SharePoint 框架实现 Teams 选项卡。 SharePoint 框架 Web 部件托管在 SharePoint 中，无需任何外部服务（如 Azure）。 对于 SharePoint 开发人员来说，这大大简化了 Teams 选项卡的开发过程。 有关 Teams 中的 SharePoint 框架的详细信息，请参阅[如何在 Teams 中使用 SharePoint 框架](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)。

## <a name="introduction"></a>简介

此处使用的选项卡已托管在 Azure 上，用于专注于所需的集成工作。

所使用的示例应用是人才管理应用程序。 它管理团队中空缺职位候选人的招聘过程。 请构建示例 Teams 应用并将其加载到 Teams 中。 不要创建真正的人才管理应用程序。

### <a name="benefits-of-this-approach"></a>此方法的好处

* 使用现有 Teams 选项卡访问 SharePoint 用户。
* 将应用清单直接上传到 SharePoint 应用程序目录。 SharePoint 现在支持 [Teams 应用程序包](~/concepts/build-and-test/apps-package.md)。
* 用户在页面上配置选项卡，就像配置任何其他 SharePoint Web 部件一样。
* 在 Teams 中运行时，选项卡可以访问其[上下文](~/tabs/how-to/access-teams-context.md)。

若要将 Teams 选项卡添加到 SharePoint，请执行以下步骤将 Teams 选项卡添加到 SharePoint：

## <a name="1-test-the-sample-app"></a>1. 测试示例应用

下载[示例应用清单](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)。

1. 打开 Microsoft Teams。
1. 选择侧栏选项卡左下角的“**应用商店**”图标。
1. 选择左下角的“**上传自定义应用**”。 下图显示了相应的屏幕：  

    ![上传自定义应用](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. 要上传的文件位于“**下载**”文件夹中。 它称为TalentMgmt-Azure.zip。 下图显示了相应的屏幕：

    ![Azure 中的 TalentMgmt](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. 可以看到人才管理应用的安装或许可屏幕。 选择要安装的团队。
1. 选择“**安装**”并开始试验应用。

## <a name="2-use-teams-tab-in-sharepoint"></a>2. 在 SharePoint 中使用 Teams 选项卡

1. 访问 `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`，将 Teams 应用包上传并部署到 SharePoint 应用程序目录。 例如，`https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`。

1. 出现提示时，启用“**使此解决方案对组织中的所有站点可用**”复选框。
下图显示了相应的屏幕：

   ![Sharepoint 视图中的选项卡](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. 在网站中，通过选择右上角的齿轮按钮，然后选择“**添加页面**”来创建新页面。
下图显示了相应的屏幕：

   ![Sharepoint 视图](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. 可以看到 SharePoint 页面创作体验。 将页面命名为“**我的 Teams 选项卡**”。

1. 选择 `+` 按钮打开 Web 部件工具箱，然后选择名为“**Contoso HR**”的 Teams 选项卡。 Web 部件按字母顺序排序。 如果是长列表，则可以使用搜索栏来查找它。 这会在画布中创建包含 Teams 选项卡的 Web 部件。下图显示了选项卡视图：

   ![选项卡视图](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. 完成编辑后，选择“**发布**”按钮。

1. 选择“**将页面添加到导航**”以在左侧导航栏中快速引用页面。
下图显示 SharePoint 中的选项卡：

   ![Sharepoint 图像中的选项卡](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a>3. 在 SharePoint 中浏览应用页面

发布页面后，可以探索[将 Teams 应用转变为 SharePoint 中更完整的体验](/sharepoint/dev/spfx/web-parts/single-part-app-pages)。 这会将当前页面转换为应用页面，显示正常的 SharePoint 页面布局，其中包含 Teams 选项卡的完整页面体验。

下图显示了 SharePoint 中 Teams 应用的完整体验：![Sharepoint 中选项卡的图像](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **SPFx** |
|-----------------|-----------------|----------|
| SPFx Web 部件 | 选项卡、频道和群组的 SPFx Web 部件示例。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a>另请参阅

* [使用 SharePoint 框架生成 Microsoft Teams 选项卡 - 教程](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
* [在 SharePoint Online 中使用单个部件应用程序页面](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
* [集成 web 应用](~/samples/integrate-web-apps-overview.md)
