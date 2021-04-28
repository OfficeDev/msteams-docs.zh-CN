---
title: 将 Teams 选项卡添加到 SharePoint
author: laujan
description: 如何将现有 Teams 选项卡作为 SharePoint 框架 Web 部件部署到 SharePoint。
keywords: teams 选项卡 sharepoint 框架开发
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: a2ea6c470f094a9d7b8617a210559e911f5f81c9
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058479"
---
# <a name="add-teams-tab-to-sharepoint"></a>将 Teams 选项卡添加到 SharePoint 

通过将 SharePoint 中的"Microsoft Teams"选项卡添加为 SPFx Web 部件，可以在 Microsoft Teams 和 SharePoint 之间获得丰富的集成体验。 本文档将指导你了解如何从 Microsoft Teams 示例应用中使用选项卡，以及如何在 SharePoint 中使用它。 

## <a name="rich-integration-between-teams-and-sharepoint"></a>Teams 和 SharePoint 之间的丰富集成

在 11 月发布的 Teams 和 SharePoint 框架 v.1.7 中，开发人员具有两项强大的功能：

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
                        <p>将 SharePoint Web 部件引入 Teams，让 SharePoint 管理托管。</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>SharePoint 中的 Teams 选项卡

借助 SharePoint 框架 v.1.7，可以在 SharePoint 中托管 Teams 选项卡。 由于 SharePoint 中托管的选项卡获得类似的完整页面体验，因此在保留 SharePoint 网站的上下文和熟悉度的同时公开 Teams 选项卡的所有功能。

### <a name="sharepoint-framework-in-teams"></a>Teams 中的 SharePoint 框架

还可使用 SharePoint 框架实现 Microsoft Teams 选项卡。 SharePoint 框架 Web 部件托管在 SharePoint 中，无需任何外部服务，如 Azure。 对于 SharePoint 开发人员，这大大简化了 Teams 选项卡的开发过程。 有关 Teams 中的 SharePoint 框架详细信息，请参阅如何在 Teams 中使用 [SharePoint 框架。](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>简介

此处使用的选项卡已托管在 Azure 上，侧重于所需的集成工作。

使用的示例应用是一个"人才管理"应用程序。 它管理团队中职位候选人的招聘流程。 生成示例 Teams 应用，并加载到 Teams 中。 不要创建真实的人才管理应用程序。

### <a name="benefits-of-this-approach"></a>此方法的好处

* 使用现有的"Teams"选项卡联系 SharePoint 用户。
* 将应用程序清单直接上载到 SharePoint 应用程序目录。 [SharePoint](~/concepts/build-and-test/apps-package.md) 现在支持 Teams 应用程序包。
* 用户像配置任何其他 SharePoint Web 部件一样在页面上配置选项卡。
* 在 Teams 内 [运行时，](~/tabs/how-to/access-teams-context.md) 你的选项卡可以访问其上下文，也可以。

**将 Teams 选项卡添加到 SharePoint**

执行以下步骤以将 Teams 选项卡添加到 SharePoint：

## <a name="1-test-the-sample-app"></a>1. 测试示例应用程序

下载 [示例应用清单](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)。

1. 打开 Microsoft Teams。
1. 选择 **"旁** "选项卡左下角的"应用商店"图标。
1. 选择 **左下角的** "上载自定义应用"。 下图显示了相应的屏幕：  

    ![上传自定义应用](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. 要上载的文件位于"下载 **"** 文件夹中。 它称为TalentMgmt-Azure.zip。 下图显示了相应的屏幕：
 
    ![Azure 中的 TalentMgmt](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. 你可以看到人才管理应用的安装或许可屏幕。 选择要安装的团队。 
1. 选择 **安装** 并开始对应用进行试验。

## <a name="2-use-teams-tab-in-sharepoint"></a>2. 在 SharePoint 中使用"Teams"选项卡

1. 通过访问 将 Teams 应用程序包上载并部署到 SharePoint 应用程序目录 `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` 。 例如，`https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`。

1. 当系统提示时，启用 **"使此解决方案对组织的所有网站都可用"。**
下图显示了相应的屏幕：

   ![Sharepoint 视图中的选项卡](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. 在网站中，选择右上角的齿轮按钮，然后选择"添加页面"，以 **创建新页面**。
下图显示了相应的屏幕：

   ![Sharepoint 视图](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. 你可以看到 SharePoint 页面创作体验。 将页面名称为 **"我的团队"选项卡**。

1. 按按钮打开 Web 部件工具箱 `+` ，然后选择名为 **Contoso HR** 的 Teams 选项卡。 Web 部件按字母顺序排序。 如果是长列表，可以使用搜索栏来查找它。 这将在画布上创建一个包含 Teams 选项卡的 Web 部件。下图显示了选项卡视图：

   ![选项卡视图](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. 编辑 **完成后，** 按"发布"按钮。

1. 选择 **"将页面添加到导航** "，在左侧导航栏中快速引用页面。 下图显示了 Sharepoint 中的选项卡： 

   ![Sharepoint 图像中的选项卡](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a>3. 浏览 SharePoint 中的应用程序页面

发布页面后，你可以探索在 SharePoint 内将 Teams 应用转变为 [更完整的体验](/sharepoint/dev/spfx/web-parts/single-part-app-pages)。 这会将当前页面转换为应用程序页，显示具有 Teams 选项卡完整页面体验的正常 SharePoint 页面布局。 

下图显示了 Sharepoint 中 Teams 应用的完整体验 ![ ：Sharepoint 中的选项卡图像](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>代码示例
| **示例名称** | **说明** | **SPFx** |
|-----------------|-----------------|----------|
| SPFx Web 部件 | 选项卡、通道和组的 SPFx Web 部件示例。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a>另请参阅

- [使用 SharePoint 框架生成 Microsoft Teams 选项卡 - 教程](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

- [在 SharePoint Online 中使用单个部件应用程序页面](/sharepoint/dev/spfx/web-parts/single-part-app-pages)

- [集成 web 应用](~/samples/integrate-web-apps-overview.md)
