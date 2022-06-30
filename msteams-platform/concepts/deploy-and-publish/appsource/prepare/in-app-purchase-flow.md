---
title: 用于应用盈利的应用内购买流
description: 了解在 Teams 应用中实现应用内购买和试用功能所需的基本任务和概念。
author: v-npaladugu
ms.author: surbhigupta
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 8bbfac3f72fb9ddbfb21d36f4a1ad2516af52b83
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558056"
---
# <a name="in-app-purchases"></a>应用内购买

Microsoft Teams 提供可用于实现应用内购买的 API，以从免费升级到付费 Teams 应用。 通过应用内购买，可以直接从应用内将用户从免费计划转换为付费计划。

## <a name="implement-in-app-purchases"></a>实现应用内购买

如果要向应用的用户提供应用内购买体验，请确保满足以下要求：

* 应用是基于 [Teams 客户端 SDK 库](https://github.com/OfficeDev/microsoft-teams-library-js) 构建的。

* 应用是使用可交易的 [SaaS 产品/服务](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md) 启用的。

* 应用是通过 [RSC 权限](#update-manifest) 启用的。

* 应用是通过 [`openPurchaseExperience`API](#purchase-experience-api) 调用的。

可以通过更新 `manifest.json` 文件或通过从 **开发人员门户** 的 **权限** 部分启用 **显示应用内购买产品/服务** 来启用应用内购买体验。

### <a name="update-manifest"></a>更新清单

要启用应用内购买体验，请通过添加 RSC 权限来更新 Teams 应用 `manifest.json` 文件。 通过此操作，应用的用户可以升级到应用的付费版本并开始使用新功能。 应用清单的更新如下所示：

```json

"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "InAppPurchase.Allow.User",
                "type": "Delegated"
            }
        ]
    }
}
```

### <a name="purchase-experience-api"></a>购买体验 API

如果要触发应用的应用内购买，请从 Web 应用调用 `openPurchaseExperience` API。

以下是从应用调用 API 的示例：

```json
<body> 
<div> 
<div class="sectionTitle">openPurchaseExperience</div> 
<button onclick="openPurchaseExperience()">openPurchaseExperience</button> 
</div> 
</body> 
<script> 
   function openPurchaseExperience() {
      microsoftTeams.initialize();
      let callbackcalled = false;
      microsoftTeams.monetization.openPurchaseExperience((e) => {
      console.log("callback is being called");
      callbackcalled = true;  
      if (!!e && typeof e !== "string") {
            e = JSON.stringify(e);
            alert(e);
        }
        return;
      });
      console.log("after callback: ",callbackcalled);
    } 
</script> 
```

## <a name="end-user-in-app-purchasing-experience"></a>最终用户应用内购买体验

以下示例向用户展示了如何购买名为 *Contoso Tasks for Teams* 的虚构 Teams 应用订阅计划：

1. 在 Teams **应用商店** 中，找到并选择该应用。

1. 在应用详细信息对话框中，选择“**购买订阅**”或“**为我添加**”。

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplancontoso.png" alt-text="购买所选应用的订阅。":::

1. “**为我添加**”提供应用的免费试用版，稍后可以将其“**升级**”为付费版本。

    :::image type="content" source="~/assets/images/saas-offer/upgradeapp.png" alt-text="升级到所选应用的订阅。" lightbox="../../../../assets/images/saas-offer/upgradeapp.png":::

1. 在“**选择订阅计划**”对话框中，选择计划，然后选择“**结账**”。

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplancontoso.png" alt-text="选择相应的订阅计划。" lightbox="../../../../assets/images/saas-offer/choosingsubscriptionplancontoso.png":::

1. 完成交易并选择“**立即配置**”以设置订阅。

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-configure-now.png" alt-text="设置订阅。" lightbox="../../../../assets/images/saas-offer/saas-offer-configure-now.png":::

    :::image type="content" source="~/assets/images/saas-offer/getstarted.png" alt-text="订阅的登陆页面。" lightbox="../../../../assets/images/saas-offer/getstarted.png":::

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [针对盈利应用的测试预览](~/concepts/deploy-and-publish/appsource/prepare/Test-preview-for-monetized-apps.md)

## <a name="see-also"></a>另请参阅

* [Microsoft Teams 应用随附 SaaS 产品/服务](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
* [创建软件即服务 (SaaS) 产品/服务](include-saas-offer.md#create-your-saas-offer)
