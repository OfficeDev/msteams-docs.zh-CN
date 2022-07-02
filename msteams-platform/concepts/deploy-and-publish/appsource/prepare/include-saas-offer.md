---
title: 在应用中包含 SaaS 产品/服务
description: 了解如何使用订阅计划使 Microsoft Teams 应用盈利，以及如何在 Microsoft Teams 应用中包含 SaaS 产品/服务。
author: heath-hamilton
ms.author: surbhigupta
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 366902d242ece8a60e601361d4e9257defd7a836
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558189"
---
# <a name="include-a-saas-offer-with-your-teams-app"></a>在 Teams 应用中包含 SaaS 产品/服务

:::row:::
   :::column span="3":::

使用可交易的软件即服务 (SaaS) 产品/服务，可以通过直接从 Teams 应用商店一览中销售订阅计划来实现 Teams 应用盈利。 例如，假设你有一个任何人都可以在应用商店中获取的免费应用。 现在，你可以为需要更多功能的用户提供高级版和企业版计划。

下面是有关如何实现应用盈利的一般概念：

1. [规划 SaaS 产品/服务](#plan-your-saas-offer)。

1. [与 SaaS 履行 API 集成](#integrate-with-the-saas-fulfillment-apis)。

1. [生成用于订阅管理的登陆页](#build-a-landing-page-for-subscription-management)。

1. [创建 SaaS 产品/服务](#create-your-saas-offer)。

1. [为 SaaS 产品/服务配置应用](#configure-your-app-for-the-saas-offer)。

1. [将应用发布到 Teams 应用商店](#publish-your-app)。

   :::column-end:::
   :::column span="1":::

:::image type="content" source="~/assets/images/saas-offer/saas-offer-diagram.png" alt-text="关闭图，演示如何将 SaaS 产品/服务包含在 Teams 应用中的过程。":::

   :::column-end:::
:::row-end:::

## <a name="plan-your-saas-offer"></a>规划 SaaS 产品/服务

有关全面的指南，请参阅 [如何规划面向 Microsoft 商业市场的 SaaS 产品/服务](/azure/marketplace/plan-saas-offer)。

规划如何实现 Teams 应用盈利时，需要考虑以下事项：

* 针对订阅模型做出决定。 可交易的 SaaS 产品/服务可以包含多个订阅计划。 任何人都可使用的公共订阅计划最为常见，但你可能还希望通过仅面向他们的交易服务特定客户。 有关详细信息，请参阅 [Microsoft 商业市场中的专用计划](/azure/marketplace/private-plans)。
* 阅读有关 SaaS 产品/服务的 [*通过 Microsoft 销售* 列表选项](/azure/marketplace/plan-saas-offer#listing-options)，如果希望用户直接通过 Teams 应用商店购买应用的订阅计划，则需要此选项。
* 了解 [Azure Active Directory 单一登录 (SSO)](/azure/marketplace/azure-ad-saas) 如何帮助客户购买和管理订阅。 （具有 SaaS 产品/服务的 Teams 应用需要 Microsoft Azure Active Directory (Azure AD) SSO。）
* 了解你负责管理支持客户使用 SaaS 产品/服务所需的基础结构并负责支付费用。
* 规划移动设备。 为了避免违反第三方应用商店策略，你的应用不能包含允许用户在移动设备上购买订阅计划的链接。 但你仍然可以指示应用是否具有需要订阅计划的功能。 有关详细信息，请参阅相关的 [商业市场认证策略](/legal/marketplace/certification-policies#114048-mobile-experience)。
* Teams 目前不支持统一费率定价模型。 但是，可以在合作伙伴中心中创建统一费率可交易产品/服务。 有关详细信息，请参阅[销售统一费率可交易产品/服务的最新做法](#best-practices-for-selling-a-flat-rate-transactable-offer)。

## <a name="integrate-with-the-saas-fulfillment-apis"></a>与 SaaS 履行 API 集成

要实现 Teams 应用盈利，需要与 SaaS 履行 API 集成。 这些 API 可帮助你在用户购买订阅计划后管理其生命周期。

有关完整的说明和 API 参考，请参阅 [SaaS 履行 API 文档](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-apis)。 一般情况下，购买订阅后，你将使用该 API 实施以下步骤：

1. 通过指向登陆页的 URL 接收 [*购买标识令牌*](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-life-cycle#purchased-but-not-yet-activated-pendingfulfillmentstart)。

1. 使用令牌检索订阅详细信息。

1. 通知商业市场该订阅已激活。

### <a name="best-practices-for-implementing-subscription-management"></a>实现订阅管理的最佳做法

* 对于 Teams 应用的可交易 SaaS 产品/服务，应将订阅计划（许可证）分配给单个用户，而不是组或整个组织。
* 为用户分配订阅计划时，请通过 Teams 机器人或电子邮件通知他们。 在消息传递中，包括有关如何将应用添加到 Teams 并开始使用的信息。
* 支持多个管理员的想法。换句话说，同一组织中的多个用户可以购买和管理自己的订阅。

## <a name="build-a-landing-page-for-subscription-management"></a>生成用于订阅管理的登陆页面

当某人在 Teams 应用商店中购买完应用订阅计划后，商业市场会将他们定向到你的登陆页，他们可以在其中管理订阅（例如向组织中的特定用户分配许可证）。

有关完整说明，请参阅 [为 SaaS 产品/服务构建登陆页](/azure/marketplace/azure-ad-transactable-saas-landing-page)。

### <a name="best-practices-for-landing-pages"></a>登陆页的最佳做法

在为要实现盈利的 Teams 应用生成登陆页时，请考虑采用以下方法。 请参阅 [最终用户购买体验](#end-user-purchasing-experience) 中的示例登陆页。

* 用户必须能够凭借用于购买订阅的相同 Azure AD 凭据登录到登陆页。 有关详细信息，请参阅 [商业市场中的 Azure AD 和可交易 SaaS 产品/服务](/azure/marketplace/azure-ad-saas)。
* 允许用户在登陆页面上执行以下操作。不要忘记考虑适合用户的角色和权限的内容（例如，你可能只允许订阅管理员搜索用户）：
  * 使用电子邮件或其他形式的标识在其组织中搜索用户。
  * 查看他们可以在列表中向其分配许可证的用户。
  * 同时向一个或多个用户分配许可证。
  * 分配和管理不同类型的许可证（如果可用）。
  * 验证许可证是否已分配给另一个用户。
  * 取消其订阅。
* 提供有关如何使用应用的简介。
* 添加获取支持的方法，例如常见问题解答、知识库或联系人电子邮件。
* 提供一个链接，以便订阅者可以轻松地返回到登陆页面。 例如，将此链接包含在应用的“**关于**”选项卡中。

## <a name="create-your-saas-offer"></a>创建 SaaS 产品/服务

集成 SaaS 履行 API 并生成用户可在其中管理其订阅的登陆页面后，下一步是正式创建、测试和发布可交易的 SaaS 产品/服务。

> [!IMPORTANT]
> Teams 目前仅支持 SaaS 产品/服务的 **按用户**（用户/月和用户/年）定价模型。 有关详细信息，请参阅 [SaaS 定价模型](/azure/marketplace/plan-saas-offer#saas-pricing-models)。

### <a name="create-the-offer"></a>创建产品/服务

有关如何在合作伙伴中心中执行此操作的完整说明，请参阅 [创建 SaaS 产品/服务](/azure/marketplace/create-new-saas-offer)。 以下步骤介绍在高级别上要执行的操作。

1. 创建 [合作伙伴中心](https://partner.microsoft.com/) 帐户（如果没有）。

1. 为可交易的 SaaS 产品/服务配置订阅计划、定价详细信息等。 尤其要确保完成以下步骤：

    * 在“**设置详细信息**”下，选择“**是**”选项，以指定通过 Microsoft 销售产品/服务。

    * 在“**Microsoft 365 集成**”下，将 AppSource 链接添加到应用列表。 此步骤可确保除 Teams 之外，用户还可以在 AppSource 中购买订阅计划。

1. 存储发布者并提供 ID。（稍后需要它们才能将产品/服务链接到开发人员门户中的应用。）

1. 将产品/服务发布到商业市场。

### <a name="test-the-offer"></a>测试产品/服务

我们强烈建议在发布 SaaS 产品/服务之前对端到端购买体验进行验证。 为此，可以创建一个单独的产品/服务来进行测试。 有关完整信息，请参阅 [测试产品/服务概述](/azure/marketplace/plan-saas-offer#test-offer)、[创建测试产品/服务](/azure/marketplace/create-saas-dev-test-offer) 和 [预览产品/服务](/azure/marketplace/test-publish-saas-offer)。

> [!IMPORTANT]
> 可以使用 [测试盈利应用的预览版](Test-preview-for-monetized-apps.md) 在 Teams 中测试端到端事务。 对于实时产品/服务，必须完成应用商店验证过程。

从 Teams 的角度来看，在用户执行以下操作时，这些测试必须验证许可证和分配的数量是否与 Teams 管理中心中的内容匹配：

* 在登陆页面上激活并配置其订阅计划。
* 向自己或其他人分配许可证，或将其删除，或重新分配许可证。
* 取消或续订其订阅。

### <a name="publish-the-offer"></a>发布产品/服务

完成测试后，可 [在线发布产品/服务](/azure/marketplace/test-publish-saas-offer#publish-your-offer-live)。

## <a name="configure-your-app-for-the-saas-offer"></a>为 SaaS 产品/服务配置应用

你已发布 SaaS 产品/服务，但仍必须将其链接到 Teams 应用，用户才能在 Teams 应用商店中查看订阅计划。

1. 转到“[开发人员门户](https://dev.teams.microsoft.com/)”并选择“**应用**”。
1. 在“**应用**”页上，选择要将 SaaS 产品/服务链接到的应用。
1. 转到“**计划和定价**”页，并指定发布者和产品/服务 ID。 （如果没有现成可用的 ID，则可以在合作伙伴中心中找到这些 ID。）
1. 选择“**查看**”以预览 SaaS 产品/服务的订阅计划。
1. 当一切正常时，选择“**保存**”。

   将 `subscriptionOffer` 属性将添加到 [应用清单](~/resources/schema/manifest-schema-dev-preview.md#subscriptionoffer)。

   ```json
      "subscriptionOffer": {
        "offerId": "publisherId.offerId"  
        }
   ```

## <a name="publish-your-app"></a>发布应用程序

你已创建 SaaS 产品/服务并将其链接到 Teams 应用，现在可以将应用发布到 Teams 应用商店。 有关完整说明，请参阅 [将应用发布到 Teams 应用商店](~/concepts/deploy-and-publish/appsource/publish.md)。

> [!IMPORTANT]
> 即使应用已在 Teams 应用商店中列出，但仍必须再次完成应用商店验证过程才能包含 SaaS 产品/服务。

发布后，当用户尝试将应用添加到 Teams 时，将在应用详细信息对话框中看到“**购买订阅**”选项。

## <a name="end-user-purchasing-experience"></a>最终用户购买体验

以下示例演示了用户如何购买名为 *Rcloud* 的虚构 Teams 应用的订阅计划。

1. 在 Teams 应用商店中，查找并选择 *Recloud* 应用。

1. 在应用详细信息对话框中，选择“**购买订阅**”。

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplan.png" alt-text="购买所选应用的订阅。":::

1. 选择你所在的国家/地区以查看适用于所在位置的订阅计划。

1. 在“**选择订阅计划**”对话框中，选择所需计划，然后选择“**结账**”。 （注意：专用计划仅对你要向其提供产品/服务的组织中用户可见。 这些计划使用 **特别产品/服务**:::image type="icon" source="~/assets/icons/special-icon.png"::: 图标指示。）

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplan.png" alt-text="选择相应的订阅计划。":::

1. 在“**结账**”对话框中，提供任何所需信息，然后选择“**下达订单**”。

    :::image type="content" source="~/assets/images/saas-offer/placesubscriptionorder.png" alt-text="下达订阅订单。":::

1. 出现系统提示时，选择“**立即设置**”以设置订阅。

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-set-up.png" alt-text="设置订阅。":::

1. 通过 *Recloud* 网站（也称为 [登陆页](#build-a-landing-page-for-subscription-management)）管理订阅计划。

    :::image type="content" source="~/assets/images/saas-offer/subscriptionlicenses.png" alt-text="配置用户许可证。":::

## <a name="admin-purchasing-experience"></a>管理员购买体验

管理员可以在 [Teams 管理中心](/MicrosoftTeams/purchase-third-party-apps) 内购买应用订阅计划。

## <a name="remove-a-saas-offer-from-your-app"></a>从应用中删除 SaaS 产品/服务

如果取消 Teams 应用商店一览中包含的 SaaS 产品/服务链接，则必须重新发布应用才能查看应用商店中的更改。

1. 转到“[开发人员门户](https://dev.teams.microsoft.com/)”并选择“**应用**”。
1. 在“**应用**”页上，选择要从中删除产品/服务的应用。
1. 转到“**计划和定价**”页，然后选择“**还原**”。
1. 取消链接产品/服务后，执行以下操作以更新应用商店一览：
   1. 选择“**分发”>“发布到 Teams 应用商店**”。
   1. 选择“**打开合作伙伴中心**”以开始重新发布不带产品/服务的应用的过程。

## <a name="best-practices-for-selling-a-flat-rate-transactable-offer"></a>销售统一费率可交易产品/服务的最佳做法

1. 创建[统一费率可交易 SaaS 产品/服务](/azure/marketplace/plan-saas-offer)并[发布到 AppSource](/azure/marketplace/test-publish-saas-offer)。

1. 将 [SaaS 产品/服务链接到合作伙伴中心中的 Teams 应用](/azure/marketplace/create-new-saas-offer)。

    > [!CAUTION]
    > 不要将产品/服务 ID 和发布者 ID 添加到应用清单。 应用不会通过 Teams 应用商店提交过程。

1. 在 Teams 应用中生成一条应用内消息，指出需要订阅，并在 AppSource 中提供 SaaS 产品/服务的超链接，以提升你的统一费率套餐。

   > [!NOTE]
   > 确保任何市场链接不会显示在移动设备和平板电脑设备上，以遵守[第三方应用商店策略](/legal/marketplace/certification-policies)。

1. 提交应用进行验证。

1. 在 Teams 市场支持统一费率定价后，请使用产品/服务 ID 和发布者 ID 更新应用清单，并重新提交应用进行验证。

## <a name="see-also"></a>另请参阅

[维护和支持已发布的应用](../post-publish/overview.md)
