---
title: 应用验证失败的常见原因
description: 了解应用无法通过应用验证的最常见原因。 链接断开、描述中的错误、无效的策略链接、有效的域准则冲突、无效的支持链接等。
ms.topic: overview
author: v-ypalikila
ms.author: v-ypalikila
ms.localizationpriority: high
ms.openlocfilehash: 1743bfc861afbbad851d2bfa6ff4236dca680ecf
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100908"
---
# <a name="common-reasons-for-app-validation-failure"></a>应用验证失败的常见原因

由于应用开发过程中出现问题，大多数应用不会通过应用商店提交过程。 本文中解决了最常见的问题或原因，以帮助你更好地准备应用，然后 [提交以供审阅](/office/dev/store/add-in-submission-guide?toc=/microsoftteams/platform/toc.json&bc=/microsoftteams/platform/breadcrumb/toc.json)。 避免这些常见故障，并遵循 [Microsoft Teams 应用商店验证准则](prepare/teams-store-validation-guidelines.md) 和 [商业市场认证策略](/legal/marketplace/certification-policies) 提高应用通过 Microsoft Teams 应用商店提交过程的可能性。

以下是应用被拒绝的最常见原因：

:::row:::
   :::column:::
      :::image type="icon" source="../../../assets/icons/broken-links-errors-icon-1.png" link="#broken-links-functional-bugs-app-crashes-and-unexpected-errors":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../assets/icons/app-description-icon.png" link="#app-description":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/trademark-icon.png" link="#violation-of-microsoft-trademark-and-brand-guidelines":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/testability-icon.png" link="#testability":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/compliance-icon.png" link="#microsoft-365-app-compliance-program":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column:::
      :::image type="icon" source="../../../assets/icons/app-guideline-icon.png" link="#violation-of-app-icon-guidelines":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../assets/icons/app-name-icon.png" link="#app-name":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/support-link-icon.png" link="#support-link":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/schema-icon.png" link="#manifest-schema":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/app-ui-icon.png" link="#app-ui":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column:::
      :::image type="icon" source="../../../assets/icons/domain-icon.png" link="#valid-domains":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/localization-icon.png" link="#localization-information":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../assets/icons/developer-name-icon.png" link="#provider-or-developer-name-mismatch":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/privacy-policy-icon.png" link="#privacy-policy":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/terms-of-use-icon.png" link="#terms-of-use":::
   :::column-end:::
:::row-end:::

## <a name="broken-links-functional-bugs-app-crashes-and-unexpected-errors"></a>断开链接、功能 bug、应用崩溃和意外错误

测试应用以验证应用的正确性、功能和使用情况。 确保全面测试应用，检查应用支持的所有端到端工作流，根据  [商业市场认证策略](/legal/marketplace/certification-policies)在操作系统和浏览器上测试应用兼容性，并修复所有 bug。 提交审阅之前，必须在应用中避免以下错误：

* 应用中的链接断开。

* 阻止应用使用的功能 bug。

* 应用崩溃。

* 持续加载阻止应用支持的已声明工作流完成的应用图面。

* 应用使用、登录和注册体验期间以及应用功能无法按预期工作的情况出现意外错误消息。

* 在提交以供审阅之前，请确保应用已完成并可供发布。

## <a name="app-description"></a>应用说明

一个很好的描述可以使你的应用在 Microsoft Teams 商店中脱颖而出，并帮助鼓励客户下载它。 必须在应用说明中避免以下错误：

* 清单和 AppSource 完整说明中不包含新用户的前进方式信息，如“注册”或“入门”或“帮助”和“联系我们”链接。

* 特定于区域的应用名称或功能不会在清单和合作伙伴中心应用说明中标注。

* 应用清单和长说明中不会指出外部帐户或服务对完成登录、注销和注册体验的限制或帐户依赖关系。

* 应用清单中的简短和完整说明不会突出显示应用的价值主张。

* 支持的应用功能不会更新。

* 应用与其他应用的比较。

* 对集成的引用，这些集成不是应用功能的一部分。

* 语法错误。

* 应用简短和完整说明相同。

## <a name="violation-of-microsoft-trademark-and-brand-guidelines"></a>违反 Microsoft 商标和品牌准则

Microsoft 的品牌资产，包括徽标、图标、设计、商业外观、字体、产品名称、服务、声音、表情符号以及任何其他品牌特征和元素，无论是否已注册，都是 Microsoft 及其公司集团拥有的专有资产。

引用 Microsoft 商标、产品名称和服务时，必须遵循 [Microsoft 商标和品牌准则](https://www.microsoft.com/legal/intellectualproperty/trademarks)。 必须避免导致应用拒绝的以下常见冲突：

* 在产品/服务一览中将 Microsoft 缩写为 MS 或 MSFT，将产品/服务列表中的第一个 Microsoft Teams 实例引用为 **Teams** ，而不是 **Microsoft Teams**。

* 在产品/服务内容中使用 Microsoft 品牌资产，而无需 Microsoft 的快速许可。

* 创建一个产品/服务列表（包括产品/服务说明、标题、图标、屏幕截图和视频），以模拟或展示它是 Microsoft Teams 应用商店的官方 Microsoft 应用。

## <a name="testability"></a>测试  

 [详细测试说明](prepare/teams-store-validation-guidelines.md#app-package-and-store-listing) 和凭据可帮助你成功查看应用。

确保在合作伙伴中心的“认证信息说明”部分提供查看应用所需的所有详细信息、需要登录的功能的有效演示凭据以及设置任何特殊配置的说明、需要难以复制和完成的环境的功能的演示视频或硬件。 此外，请确保提供最新的联系信息。

必须避免在应用评审期间 20% 的应用中出现以下问题：

* 没有测试说明或凭据来测试应用。

* 当有两个测试帐户的依赖项用于测试协作方案时，仅提供一个测试帐户。

* 提供的测试说明和凭据不足以完成应用功能测试。

## <a name="microsoft-365-app-compliance-program"></a>Microsoft 365 应用合规性  

Microsoft 365应用合规性计划通过评估有关应用的安全性和合规性信息，帮助组织评估和管理风险。 **必须先完成**[发布者验证](/azure/active-directory/develop/mark-app-as-publisher-verified)，然后才能提交应用以供审核才能在 Microsoft Teams 应用商店中发布。

## <a name="violation-of-app-icon-guidelines"></a>违反应用图标准则

图标是用户在浏览 Teams 应用商店时看到的主要元素之一。 图标必须传达应用的品牌和用途，同时遵守应用图标[准则](../../build-and-test/apps-package.md#app-icons)。 必须避免导致应用拒绝的以下冲突：

* 包含具有不同颜色和轮廓图标或非白色和非透明轮廓图标的应用包的应用提交。

* 合作伙伴中心中具有不同徽标的应用提交和提交供审阅的应用包。

## <a name="app-name"></a>应用名称

应用名称对于用户在 Microsoft Teams 应用商店中发现应用起着至关重要的作用。 确保应用名称符合[应用名称准则](prepare/teams-store-validation-guidelines.md#app-name)，并且不违反 [Microsoft 商标和品牌准则](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks)。 必须避免导致应用拒绝的以下冲突：

* 应用名称在整个应用功能中的使用不一致。
* 作为应用包的一部分提交的应用清单中提到的应用名称与合作伙伴中心不匹配。
* 追加了 *Beta 版*、 *开发* 和 *Prod* 的应用名称，以指示应用尚未准备好生产。
* 应用提交，其中开发人员更改了应用名称，但旧应用名称在应用中使用。

## <a name="support-link"></a>支持链接

 支持链接不得要求用户进行身份验证，并且必须直接获得适当的支持信息。 必须确保应用包含有效的支持链接，以便用户联系。

## <a name="manifest-schema"></a>清单架构

Teams 应用清单介绍了应用如何集成到 Microsoft Teams 产品中。 应用清单必须符合公开发布的 [清单架构](../../../resources/schema/manifest-schema.md)。 如果应用支持本地化，请确保使用本地化清单架构版本 1.5 或更高版本。 包含预览架构（未公开发布）的应用包无法进行应用评审。

如果要提交应用更新，则必须更新清单中声明的应用版本。 建议在提交新应用或应用更新时始终使用最新公开发布的清单架构，并确保 Microsoft Teams 应用商店和Microsoft AppSource中的清单架构版本相同。

应用包只能包含应用的清单、颜色图标和大纲图标。 包含任何其他文件或文件夹的应用包无法通过应用评审。

## <a name="app-ui"></a>应用 UI

应用的 UI 不能看起来不完整，并且应该很直观。 在应用的 UI 上执行操作时，请确保不会向用户显示空白屏幕。 截断或重叠内容的应用以及显示损坏图像的应用无法通过应用评审。

## <a name="valid-domains"></a>有效域

应用提交必须遵守 microsoft 商业市场认证策略下的[外部域](/legal/marketplace/certification-policies)准则。 若要使应用通过评审，请确保应用清单中列出的有效域受组织的直接控制。

## <a name="localization-information"></a>本地化信息

如果应用支持本地化，则必须在应用包中包含本地化语言文件。 本地化文件必须符合 [Teams 本地化架构](../../build-and-test/apps-localization.md)。 支持本地化但应用清单中缺少本地化信息的应用无法通过应用评审。

## <a name="provider-or-developer-name-mismatch"></a>提供程序或开发人员名称不匹配

你必须确保在两个店面的产品/服务一览中提供相同的开发人员名称，以避免在从 Microsoft Teams 应用商店或Microsoft AppSource获取应用期间最终用户混淆。 开发人员名称不匹配的产品/服务经常无法通过应用评审。

## <a name="privacy-policy"></a>隐私策略

产品/服务列表必须包含有效的隐私策略链接。 具有无效、不安全和损坏的隐私策略链接的产品/服务无法通过应用评审。 你的隐私策略必须遵循[特权策略准则](prepare/teams-store-validation-guidelines.md#privacy-policy)。

## <a name="terms-of-use"></a>使用条款

产品/服务列表必须包含有效的使用条款链接。 具有无效、不安全和损坏使用条款链接的产品/服务无法通过应用评审。 必须遵循[使用条款准则](prepare/teams-store-validation-guidelines.md#terms-of-use)。

## <a name="see-also"></a>另请参阅

* [Microsoft Teams 商店验证指南](prepare/teams-store-validation-guidelines.md)
* [商业市场认证策略](/legal/marketplace/certification-policies)
* [Microsoft 商标和品牌准则](https://www.microsoft.com/legal/intellectualproperty/trademarks)
