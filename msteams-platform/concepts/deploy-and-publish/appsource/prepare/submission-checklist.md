---
title: 准备应用商店提交
description: 在提交要在应用商店中列出的 Microsoft Teams 应用之前，请了解最后步骤。 了解如何验证应用包等。
ms.topic: how-to
ms.localizationpriority: high
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: c71579900f910d2677ab0d48bab5a37853dfb69c
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123165"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a>准备 Microsoft Teams 应用商店提交

你已设计、生成和测试了 Microsoft Teams 应用。 现在，你已准备好将其列出，以便用户可以发现并开始使用你的应用。

请观看以下视频，以了解有关将应用发布到 Microsoft Teams 应用商店的详细信息：
<br>

> [!VIDEO <https://www.microsoft.com/videoplayer/embed/RE4WG3l>]
<br>

在将应用提交到 [合作伙伴中心](/office/dev/store/use-partner-center-to-submit-to-appsource) 之前，确保已完成以下操作。

## <a name="validate-your-app-package"></a>验证应用包

虽然应用可能在测试环境中工作，但应检查应用包以避免在提交过程中遇到问题。

> [!WARNING]
> 如果一直在使用 App Studio，我们建议你试用 [开发人员门户](https://dev.teams.microsoft.com/) 来配置、分发和管理 Teams 应用。 App Studio 将于 2022 年 6 月 30 日弃用。

Microsoft Teams 应用验证工具可帮助你在提交到合作伙伴中心之前识别和修复问题。 该工具将根据应用商店验证期间使用的相同测试用例自动检查应用的配置。

1. 转到“[Microsoft Teams 应用验证工具](https://dev.teams.microsoft.com/appvalidation.html)”。 （注意：该工具也可在 [App Studio](../../../build-and-test/app-studio-overview.md) 中使用。）
1. 上传应用包以运行自动测试。
1. 转到“**初步清单**”并查看难以自动执行的测试用例。
1. [修复配置问题](~/resources/schema/manifest-schema.md)或应用一般问题。如果自动测试提示错误或未满足清单中的所有条件，则会出现这些问题。

## <a name="compile-testing-instructions"></a>编译测试说明

提供说明和资源，以帮助审阅者测试应用，包括：

* 测试帐户
* 凭据
* 许可证密钥

可以在合作伙伴中心中添加说明，或将其上传到 SharePoint 上的公开可用位置。

### <a name="feature-list"></a>功能列表

提供有关应用在 Teams 中的功能以及每个功能的测试步骤的详细信息。

### <a name="accounts"></a>帐户

如果应用需要许可证或后端安全列表，请提供测试帐户。 所提供的全部帐户必须包含预填充的数据，以帮助进行测试。

根据应用的功能，可能需要提供以下全部帐户：

* 管理员账户（必需）
* 非管理员帐户（必需）
* 未对其进行预配置以正确测试首次运行登录体验的账户（必需）
* 有权访问高级或升级功能的帐户（如果适用）
* 同一租户中的两个帐户，用于测试应用在共享上下文中工作的协作体验（如果适用）

### <a name="tenant-configurations"></a>租户配置

如果必须将 Teams 租户配置为使用你的应用，请包括这些说明和管理员及非管理员帐户以便进行验证。

### <a name="video-optional"></a>视频（可选）

提供应用的录制内容，以便 Microsoft 能够完全了解其功能。

## <a name="create-your-store-listing-details"></a>创建应用商店一览详细信息

提交到 [合作伙伴中心](https://partner.microsoft.com) 的详细信息 - 包括你的姓名、说明、图标和图像 - 将成为你的应用的 Teams 应用商店和 Microsoft AppSource 一览。

应用商店一览可能是人们对应用的第一印象。 通过有效传达应用优势、功能和品牌的一览来可增加应用的安装。

### <a name="specify-a-short-name"></a>指定短名称

应用的名称（特别是它的 *[短名称](~/resources/schema/manifest-schema.md#name)*）对于用户如何在应用商店中发现它具有重要作用。

:::row:::

:::column span="3":::
:::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="突出显示应用短名称在应用商店一览中显示位置的示例屏幕截图。":::
:::column-end:::
:::column span="1":::
:::column-end:::

:::row-end:::

确保短名称符合 [应用商店验证准则](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#app-name)。

### <a name="write-descriptions"></a>撰写说明

必须对应用有一个简短而长的介绍。

#### <a name="short-description"></a>简短说明

应用的简洁摘要，应为原创作品、具有吸引力且针对目标受众。将简短说明保留为一句话。

:::row:::

:::column span="3":::
:::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="突出显示应用简短说明在应用商店一览中显示位置的示例屏幕截图。":::
:::column-end:::
:::column span="1":::
:::column-end:::

:::row-end:::

请确保简短说明遵循 [应用商店验证准则](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#short-description)。

#### <a name="long-description"></a>较长说明

较长说明可以提供突出显示应用以下方面的叙述：

* 主要功能
* 可解决的问题
* 目标受众

虽然此说明可以长达 4，000 个字符，但大多数用户仅会阅读 300-500 个字。

:::row:::

:::column span="3":::
:::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="突出显示应用较长说明在应用商店一览中显示位置的示例屏幕截图。":::
:::column-end:::
:::column span="1":::
:::column-end:::

:::row-end:::

请确保较长说明遵循 [应用商店验证准则](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#long-description)。

### <a name="adhere-to-icon-design-guidelines"></a>遵循图标设计准则

图标是用户在浏览应用商店时看到的主要元素之一。 图标应传达应用的品牌和用途，同时应遵循以下要求。

要了解详细信息，请参阅 [创建 Teams 应用图标指南](~/concepts/build-and-test/apps-package.md#app-icons)。

### <a name="capture-screenshots"></a>捕获屏幕截图

屏幕截图提供了应用的突出视觉预览，以补充应用名称、图标和说明。

:::row:::

:::column span="3":::
:::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="突出显示应用屏幕截图在应用商店一览中显示位置的示例屏幕截图。":::
:::column-end:::
:::column span="1":::
:::column-end:::

:::row-end:::

请记住以下有关屏幕截图的最佳做法：

* 每个列表最多可以有五个屏幕截图。
* 支持的文件类型包括 PNG、JPEG 和 GIF 图像格式。
* 尺寸应为 1366 x 768 像素。
* 最大尺寸为 1，024 KB。

有关最佳做法，请参阅以下资源：

* [Teams 应用商店验证准则](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#screenshots)
* [制作适用于 Microsoft 应用商店的有效图像](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a>创建视频

一览中的视频可能是传达为什么应使用你的应用的最有效方法。应在视频中解决以下问题：

* 应用适合谁使用？
* 应用可以解决哪些问题？
* 应用的工作原理是什么？
* 使用应用可以得到哪些其他好处？

可以为 YouTube 或 Vimeo 视频添加 URL。

#### <a name="best-practices-for-videos"></a>视频最佳做法

* 将视频长度保持在 60-90 秒之间。
* 以质量为目标。在应用一览中，用户将在看到屏幕截图之前先看到你的视频。
* 以叙述形式传达产品的价值。
* 演示产品的工作方式。

### <a name="select-a-category-for-your-app"></a>为应用选择一个类别

提交期间，系统将要求你对应用进行分类。 下表将 Teams 应用商店类别映射到 [合作伙伴中心](https://aka.ms/PartnerCenterHomePage) 中列出的类别。

| Teams 类别       | 合作伙伴中心类别  |
|:---------------------|:---------------|
| 分析和 BI | 分析、数据可视化和 BI |
| 开发人员和 IT | 开发人员工具，IT 管理员 |
| 教育 | 教育 |
| 人力资源 | 人力资源和招聘 |
| 工作效率 | 内容管理、文件和文档、生产力、培训和教程以及实用工具 |
| 项目管理 | 通信、项目管理、工作流和业务管理 |
| 销售和客户服务 | 客户和联系人管理、客户支持、财务管理，以及销售和市场营销 |
| 社交和娱乐 | 图像和视频库、生活方式、新闻和天气、社交、旅行和导航 |

### <a name="localize-your-store-listing"></a>本地化应用商店一览

合作伙伴中心支持 [本地化的应用商店一览](/office/dev/store/prepare-localized-solutions)。 有关详细信息，请参阅 [如何本地化 Teams 应用一览](../../../../concepts/build-and-test/apps-localization.md)。

## <a name="complete-publisher-verification"></a>完成发布者验证

[发布者验证](/azure/active-directory/develop/publisher-verification-overview) 对于在应用商店中列出的 Teams 应用是必需的。 有关详细信息，请参阅 [常见问题解答](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)，[如何将应用标记为发布者验证](/azure/active-directory/develop/mark-app-as-publisher-verified)，以及 [排除发布者验证的故障](/azure/active-directory/develop/troubleshoot-publisher-verification)。

## <a name="complete-publisher-attestation"></a>完成发布者证明

[发布者证明](/microsoft-365-app-certification/docs/attestation) 对于在应用商店中列出的 Teams 应用也是必需的。 此过程包括完成对应用安全性、数据处理和合规性做法的自我评估。 此过程可帮助潜在客户做出有关使用应用的明智决策。

> [!NOTE]
> 如果要提交新的应用，则在 Teams 应用商店中列出应用之前，无法正式完成发布者证明。 如果正在更新列出的应用，请在提交最新版本应用进行认证之前完成发布者证明。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [提交你的应用](/office/dev/store/add-in-submission-guide)

## <a name="see-also"></a>另请参阅

[解决 Microsoft Teams 应用商店提交失败时出现的问题](~/concepts/deploy-and-publish/appsource/resolve-submission-issues.md)
