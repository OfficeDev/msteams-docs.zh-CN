---
title: 在应用中包含 SaaS 产品/服务
description: 了解如何通过订阅计划Microsoft Teams应用盈利。
author: heath-hamilton
ms.author: surbhigupta
ms.topic: how-to
ms.localizationpriority: medium
ms.openlocfilehash: b358b7bbdd780851eedb78ca2151bc062d402f99
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059614"
---
# <a name="include-a-saas-offer-with-your-microsoft-teams-app"></a>将 SaaS 产品/服务与Microsoft Teams一起

:::row:::
   :::column span="3":::

借助可交易的软件即服务 (SaaS) 产品，你可以直接从你的 Teams 应用商店一览中销售订阅计划来盈利 Teams 应用。 例如，假设你有一个任何人都可以在应用商店中获取的免费应用。 现在，你可以为需要更多功能的用户提供高级和企业计划。

下面是如何从你的应用中盈利的一般想法：

1.  [规划 SaaS 产品/](#plan-your-saas-offer)

1.  [与 SaaS 实施 API 集成](#integrate-with-the-saas-fulfillment-apis)。

1.  [构建订阅管理的登陆页面](#build-a-landing-page-for-subscription-management)。

1.  [创建 SaaS 产品/服务](#create-your-saas-offer)。

1.  [针对 SaaS 产品配置你的应用](#configure-your-app-for-the-saas-offer)。

1.  [将应用发布到Teams应用商店](#publish-your-app)。

   :::column-end:::
   :::column span="1":::
   
:::image type="content" source="~/assets/images/saas-offer/saas-offer-diagram.png" alt-text="显示如何将 SaaS 产品/服务与你的应用Teams图。" border="false":::

   :::column-end:::
:::row-end:::

## <a name="plan-your-saas-offer"></a>规划 SaaS 产品

有关全面指导， [请参阅如何为 Microsoft 商业市场规划 SaaS 产品](/azure/marketplace/plan-saas-offer)。

在规划如何利用 Teams 盈利时，需要考虑以下一些操作：

* 确定订阅模型。 可交易 SaaS 产品可以包含多个订阅计划。 可供任何人使用的公共订阅计划最为常见，但你可能还希望仅面向具有交易的特定客户。 有关详细信息，请参阅 [Microsoft 商业市场中的专用产品/服务](/azure/marketplace/private-offers)。
* 阅读 SaaS 优惠的"通过 [*Microsoft*](/azure/marketplace/plan-saas-offer#listing-options)销售"一览选项，如果你希望用户直接通过应用商店购买应用的订阅计划，Teams此选项。
* 了解[Azure Active Directory (Azure AD) SSO](/azure/marketplace/azure-ad-saas) (单一) 如何帮助客户购买和管理订阅。  (Azure AD SaaS 产品/服务Teams应用需要 SSO。) 
* 了解你负责管理和支付支持客户使用 SaaS 产品所需的基础结构。
* 规划移动。 为了避免违反第三方应用商店策略，你的应用不能包括允许用户在移动设备上购买订阅计划的链接。 但是，你仍然可以指示你的应用是否具有需要订阅计划的功能。 有关详细信息，请参阅相关的商业 [市场认证策略](/legal/marketplace/certification-policies#114048-mobile-experience)。

## <a name="integrate-with-the-saas-fulfillment-apis"></a>与 SaaS 实施 API 集成

需要与 SaaS 实施 API 集成，才能将你的Teams盈利。 这些 API 可帮助你在用户购买订阅计划后管理订阅计划的生命周期。

有关完整说明和 API 参考，请参阅 [SaaS 履行 API 文档](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-apis)。 通常，购买订阅后，你将使用 API 实现以下步骤：

1. 通过 [*登录页面的*](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-life-cycle#purchased-but-not-yet-activated-pendingfulfillmentstart) URL 接收购买标识令牌。

1. 使用令牌检索订阅详细信息。

1. 通知商业市场订阅已激活。

### <a name="best-practices-for-implementing-subscription-management"></a>实现订阅管理的最佳方案

* 借助可交易 saaS Teams应用， (订阅计划) 许可证应分配给单个用户，而不是组或整个组织。
* 为用户分配订阅计划后，请通过自动程序或Teams通知他们。 在消息传递中，包括有关如何将应用添加到Teams入门的信息。
* 支持多个管理员的想法。 换句话说，同一组织中的多个用户可以购买和管理自己的订阅。

## <a name="build-a-landing-page-for-subscription-management"></a>构建订阅管理的登录页面 

当某人在 Teams 商店中为你的应用购买完订阅计划后，商业市场将引导他们到你的登录页面，他们可以在此页面管理订阅 (例如将许可证分配给其组织) 中的特定用户。

有关完整说明，请参阅 [为 SaaS 产品生成登陆页面](/azure/marketplace/azure-ad-transactable-saas-landing-page)。

### <a name="best-practices-for-landing-pages"></a>登录页面的最佳实践

为要盈利的应用生成登录Teams请考虑以下方法。 请参阅最终用户购买体验中的 [登录页面示例](#end-user-purchasing-experience)。

* 用户必须能够使用用于购买订阅Azure AD登录页面。 有关详细信息，请参阅Azure AD市场中的可交易[SaaS 产品/服务](/azure/marketplace/azure-ad-saas)。
* 允许用户在你的登录页面上执行以下操作。 不要忘记考虑适合用户的角色和权限 (例如，你可能希望仅允许订阅管理员搜索以下) ：
  * 使用电子邮件或另一种标识形式搜索其组织中的用户。
  * 查看他们可以在列表中为其分配许可证的用户。
  * 同时向一个或多个用户分配许可证。
  * 分配和管理不同类型的许可证 (（如果) ）。
  * 验证许可证是否已被分配给其他用户。
  * 取消他们的订阅。
* 提供如何使用你的应用的简介。
* 添加获取支持的方法，例如常见问题解答、知识库或联系人电子邮件。
* 提供链接，使订阅者可以轻松返回到登陆页面。 例如，在应用的"关于"选项卡中包括 **此** 链接。

## <a name="create-your-saas-offer"></a>创建 SaaS 产品

集成 SaaS 实施 API 并构建登录页面（用户可以管理其订阅）后，就可以正式创建、测试和发布可交易 SaaS 产品了。

> [!IMPORTANT]
> Teams SaaS 产品/服务 ("按用户/月"和"用户/) "定价模型。 有关详细信息，请参阅 [SaaS 定价模型](/azure/marketplace/plan-saas-offer#saas-pricing-models)。

### <a name="create-the-offer"></a>创建产品/服务

有关如何 [在合作伙伴中心中](/azure/marketplace/create-new-saas-offer) 完成此操作的完整说明，请参阅创建 SaaS 产品。 以下步骤介绍了在高级别上要执行哪些操作。

1.  如果没有 [合作伙伴中心](https://partner.microsoft.com/) 帐户，请创建该帐户。

1.  为可交易 SaaS 产品配置订阅计划、定价详细信息等。 特别是，请确保完成以下步骤：

    * 在 **"安装** 详细信息"下 **，选择"** 是"选项以指定你通过 Microsoft 销售产品/服务。
     
    * 在 **Microsoft 365集成**"下，将 AppSource 链接添加到应用一览。 此步骤可确保用户除了可以在 AppSource 中购买订阅计划Teams。

1. 存储你的发布者并提供 ID。  (稍后需要它们，以在开发人员门户中将产品/服务链接到) 

1. 将产品/服务发布到商业市场。

### <a name="test-the-offer"></a>测试产品/服务

我们强烈建议你在发布 SaaS 产品之前验证端到端购买体验。 为此，只需创建单独的产品/服务进行测试。 有关完整信息，请参阅[测试产品/服务概述](/azure/marketplace/plan-saas-offer#test-offer)[、创建测试产品](/azure/marketplace/create-saas-dev-test-offer)/服务[并预览你的产品/服务](/azure/marketplace/test-publish-saas-offer)。

> [!IMPORTANT]
> 你必须在 AppSource 中测试可交易 SaaS 产品。 目前，在应用完成应用商店验证Teams无法测试端到端事务。

从Teams的角度来看，这些测试必须验证许可证和分配的数量是否与用户Teams中心内内容匹配：

* 在登录页面上激活和配置他们的订阅计划。
* 向自己或他人分配、删除或重新分配许可证。
* 取消或续订其订阅。

### <a name="publish-the-offer"></a>发布产品/服务

完成测试后， [实时发布产品/服务](/azure/marketplace/test-publish-saas-offer#publish-your-offer-live)。

## <a name="configure-your-app-for-the-saas-offer"></a>为应用配置 SaaS 产品

你已发布 SaaS 产品/服务，但仍必须将它链接到 Teams 应用，以便用户在应用商店中查看Teams计划。

1. 转到开发人员 [门户，然后选择](https://dev.teams.microsoft.com/)**应用。**
1. 在 **应用** 页面上，选择要将 SaaS 产品/服务链接到的应用。
1. 转到计划和 **定价** 页面，并指定你的发布者和产品/服务 ID。  (如果你还没有现成的这些 ID，可以在合作伙伴中心找到它们。) 
1. 选择 **"** 查看"预览 SaaS 产品/服务订阅计划。
1. 如果一切看起来都不错，请选择"保存 **"。**

   `subscriptionOffer`属性将添加到应用[清单](~/resources/schema/manifest-schema-dev-preview.md#subscriptionoffer)中。

   ```json
      "subscriptionOffer": {
        "offerId": "publisherId.offerId"  
        }
   ```

## <a name="publish-your-app"></a>发布应用程序

你已创建 SaaS 产品/服务，并Teams你的应用，现在应该将应用发布到 Teams 应用商店。 有关完整说明，请参阅[将应用发布到Teams应用商店](~/concepts/deploy-and-publish/appsource/publish.md)。

> [!IMPORTANT]
> 即使你的应用已列在应用商店Teams，你仍然必须再次完成应用商店验证过程，以包含你的 SaaS 产品。

发布后，当用户 **尝试向应用** 添加应用时，将在应用详细信息对话框中看到"购买订阅"Teams。

## <a name="end-user-purchasing-experience"></a>最终用户购买体验

以下示例显示用户如何购买名为 *Recloud* 的虚拟Teams订阅计划。

1. 在 Teams 应用商店中，查找并选择 *"重新云"* 应用。

1. 在应用详细信息对话框中，选择 **购买订阅**。

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplan.png" alt-text="购买所选应用的订阅。":::

1. 选择你的国家/地区以查看你位置的订阅计划。

1. 在 **"选择订阅计划**"对话框中，选择您需要的计划，然后选择"签出 **"。**  (注意：专用计划仅对提供优惠的组织中的用户可见。 这些计划用"特别优惠" **图标** :::image type="icon" source="~/assets/icons/special-icon.png"::: 指示。) 

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplan.png" alt-text="选择适当的订阅计划。":::

1. 在"**签出**"对话框中，提供任何所需信息，然后选择"**下订单"。**

    :::image type="content" source="~/assets/images/saas-offer/placesubscriptionorder.png" alt-text="下订单。":::

1. 系统提示时，选择 **"立即设置** "以设置订阅。

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-set-up.png" alt-text="设置订阅。":::

1. 通过 *Recloud* 网站管理订阅 (也称为登录 [) 。](#build-a-landing-page-for-subscription-management)

    :::image type="content" source="~/assets/images/saas-offer/subscriptionlicenses.png" alt-text="配置用户许可证。":::

## <a name="admin-purchasing-experience"></a>管理员购买体验

管理员可以在管理中心 中Teams[应用订阅计划](/MicrosoftTeams/purchase-third-party-apps)。

## <a name="remove-a-saas-offer-from-your-app"></a>从应用中删除 SaaS 产品

如果你取消链接你的应用商店一览Teams SaaS 产品，则必须重新发布你的应用，以查看应用商店中的更改。

1. 转到开发人员 [门户，然后选择](https://dev.teams.microsoft.com/)**应用。**
1. 在 **"应用** "页面上，选择要删除产品/服务的应用。
1. 转到计划和定价 **页面，****然后选择还原**。
1. 取消产品/服务链接后，执行以下操作以更新应用商店一览：
   1. 选择 **分发>发布到Teams应用商店。**
   1. 选择 **"打开** 合作伙伴中心"开始在没有优惠的情况下重新发布应用的过程。

## <a name="see-also"></a>另请参阅

[维护和支持已发布的应用](../post-publish/overview.md)
