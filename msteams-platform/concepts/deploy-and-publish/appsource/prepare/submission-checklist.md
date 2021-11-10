---
title: 准备应用商店提交
description: 介绍提交要列在应用商店Microsoft Teams应用之前的最后步骤。 了解如何验证应用包、编译测试说明以及创建应用商店一览详细信息。
ms.topic: how-to
ms.localizationpriority: medium
author: heath-hamilton
ms.author: surbhigupta
keywords: 提交应用商店分发验证应用包指南本地化
ms.openlocfilehash: 08155408e68869b76f814788afcb408afd1a72a9
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889165"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a>准备Microsoft Teams应用商店提交

你已设计、生成和测试Microsoft Teams应用。 现在，你已准备好列出它，以便用户可以发现并开始使用你的应用。

在将应用提交到 [合作伙伴中心](/office/dev/store/use-partner-center-to-submit-to-appsource)之前，请确保你已完成以下操作。

## <a name="validate-your-app-package"></a>验证应用包

当你的应用可能在测试环境中运行时，你应该检查你的应用包，以避免在提交过程中出现问题。

> [!NOTE]
>  App Studio 即将被弃用。 使用新的开发人员门户配置Teams分发[和管理应用](https://dev.teams.microsoft.com/)

应用Microsoft Teams工具可帮助你在提交到合作伙伴中心之前识别和修复问题。 该工具根据应用商店验证期间使用的相同测试用例自动检查应用的配置。

1. 转到应用[Microsoft Teams工具](https://dev.teams.microsoft.com/appvalidation.html)。  (注意：该工具在 [App Studio](../../../build-and-test/app-studio-overview.md).) 
1. Upload应用包运行自动测试。
1. 转到" **初步检查表** "并查看难以自动化的测试用例。
1. [一般情况下修复配置](~/resources/schema/manifest-schema.md) 或应用的问题。 如果自动测试为您提供错误，或者您未满足检查表中的所有条件，将会出现这些问题。

## <a name="compile-testing-instructions"></a>编译测试说明

提供说明和资源来帮助审阅者测试你的应用，包括：
* 测试帐户
* 凭据
* 许可证密钥

可以在合作伙伴中心中添加说明，或将其上载到 SharePoint 上公开提供的位置。

### <a name="feature-list"></a>功能列表

提供有关应用功能的详细信息，Teams测试每个功能的步骤。

### <a name="accounts"></a>帐户

如果你的应用需要许可证或后端安全列表，则提供测试帐户。 你提供的所有帐户都必须包含预填充的数据，以帮助测试。

根据应用的功能，可能需要提供以下所有帐户：

* 管理员帐户 (必需) 
* 非管理员帐户 (必需) 
* 未预配置为正确测试首次运行登录体验的帐户 (要求) 
* 有权访问高级或升级功能的帐户 (（如果适用) 
* 同一租户中的两个帐户，用于测试在共享上下文中工作的应用的 (体验（如果适用) 

### <a name="tenant-configurations"></a>租户配置

如果必须配置Teams租户才能使用应用，请包含这些说明以及管理员和非管理员帐户进行验证。

### <a name="video-optional"></a>视频 (可选) 

提供你的应用的录制，以便 Microsoft 可以完全了解其功能。

## <a name="create-your-store-listing-details"></a>创建应用商店一览详细信息

你提交到合作伙伴[中心&#8212;包括](https://partner.microsoft.com)你的姓名、说明、图标和图像&#8212;成为应用的 Teams 应用商店和 Microsoft AppSource 一览。

应用商店一览可能是某人对你的应用的第一印象。 通过可有效传达应用优势、功能和品牌一览增加安装量。

### <a name="specify-a-short-name"></a>指定短名称

特别是，你的应用的名称 (，它的短) 在用户如何在[](~/resources/schema/manifest-schema.md#name)应用商店中发现它中扮演重要角色。

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="示例屏幕截图突出显示了在应用商店一览中显示应用的短名称的位置。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

确保你的短名称符合应用商店 [验证准则](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#app-name)。

### <a name="write-descriptions"></a>编写说明

必须对应用有一个简短而长的介绍。

#### <a name="short-description"></a>简短说明

应用简洁摘要，应原始、具有吸引力，并面向目标受众。 将简短说明保留为一句话。

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="示例屏幕截图突出显示了在应用商店一览中显示应用的简短说明的位置。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

请确保简短说明符合应用商店 [验证准则](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#short-description)。

#### <a name="long-description"></a>较长说明

长描述可以提供一个强调你的应用的叙述性内容：

* 主要功能
* 它所解决的问题
* 目标受众

虽然此说明可以长达 4，000 个字符，但大多数用户仅会阅读 300-500 个字。

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="示例屏幕截图突出显示了在应用商店一览中显示应用长说明的位置。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

请确保你的详细说明符合应用商店 [验证准则](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#long-description)。

### <a name="adhere-to-icon-design-guidelines"></a>遵守图标设计指南

图标是用户在浏览应用商店时看到的主要元素之一。 图标应传达应用的品牌和用途，同时遵循Teams要求。

有关详细信息，请参阅[有关创建应用图标Teams指南](~/concepts/build-and-test/apps-package.md#app-icons)。

### <a name="capture-screenshots"></a>捕获屏幕截图

屏幕截图提供了应用的突出视觉预览，以补充应用名称、图标和说明。

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="示例屏幕截图突出显示了应用屏幕截图在应用商店一览中的显示位置。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

请记住以下有关屏幕截图的最佳实践：

* 每个列表最多可以有五个屏幕截图。
* 支持的文件类型包括 PNG、JPEG 和 GIF。
* 尺寸应为 1366x768 像素。
* 最大尺寸为 1，024 KB。

有关最佳做法，请参阅以下资源：

* [Teams应用商店验证指南](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#screenshots)
* [为 Microsoft 应用商店精心制作有效图像](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a>创建视频

一览中的视频可能是传达人们为什么应该使用你的应用的最有效方式。 在视频中回答以下问题：

* Who应用是否适用于？
* 你的应用可以解决哪些问题？
* 你的应用如何工作？
* 使用你的应用还有其他哪些好处？

您可以为 YouTube 或 Vimeo 视频添加 URL。

#### <a name="best-practices-for-videos"></a>视频最佳做法

* 将视频保留 60-90 秒。
* 以质量为目标。 在列表中，用户将在屏幕截图前看到视频。
* 以叙述性形式传达产品的价值。
* 演示产品的工作原理。

### <a name="select-a-category-for-your-app"></a>为应用选择类别

在提交过程中，将要求你对应用进行分类。 下表将应用商店Teams映射到合作伙伴中心中列出的[类别](https://aka.ms/PartnerCenterHomePage)。

| Teams类别       | 合作伙伴中心类别  |
|:---------------------|:---------------|
| 分析和 BI | 分析、数据可视化和 BI |
| 开发人员和 IT | 开发人员工具、IT 管理员 |
| 教育 | 教育 |
| 人力资源 | 人力资源和招聘 |
| 工作效率 | 内容管理、文件和文档、生产力、培训和教程以及实用程序 |
| 项目管理 | 通信、Project、工作流和业务管理 |
| 销售和支持 | 客户和联系人管理、客户支持、数据管理以及销售和市场营销 |
| 社交和有趣 | 图像和视频库、生活方式、新闻和天气、社交、旅行和导航 |

### <a name="localize-your-store-listing"></a>本地化应用商店一览

合作伙伴中心 [支持本地化的应用商店一览](/office/dev/store/prepare-localized-solutions)。 有关详细信息，请参阅[如何本地化你的Teams应用一览](../../../../concepts/build-and-test/apps-localization.md)。

## <a name="complete-publisher-verification"></a>完成Publisher验证

[Publisher应用商店](/azure/active-directory/develop/publisher-verification-overview)中列出的Teams应用需要验证。 有关详细信息，请参阅 [常见问题解答](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)，[如何将应用标记为发布者验证](/azure/active-directory/develop/mark-app-as-publisher-verified)，以及 [排除发布者验证的故障](/azure/active-directory/develop/troubleshoot-publisher-verification)。

## <a name="complete-publisher-attestation"></a>完成Publisher证明

[Publisher应用商店](/microsoft-365-app-certification/docs/attestation)中列出的应用Teams证明也是必需的。 此过程包括完成对应用的安全性、数据处理和合规性做法的自我评估。 此过程可帮助潜在客户做出有关使用你的应用的明智决定。

> [!NOTE]
> 如果你要提交新应用，则你无法正式完成Publisher证明，直到你的应用在应用商店Teams列出。 如果要更新列出的应用，请完成Publisher证明，然后再提交应用的最新版本进行验证。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [提交你的应用](/office/dev/store/add-in-submission-guide)

## <a name="see-also"></a>另请参阅

[解决应用商店提交Microsoft Teams时的问题](~/concepts/deploy-and-publish/appsource/resolve-submission-issues.md)
