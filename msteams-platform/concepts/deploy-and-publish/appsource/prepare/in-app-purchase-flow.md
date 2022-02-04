---
title: 应用内购买流，用于盈利应用
description: 了解在 Teams 应用中实现应用内购买和试用功能所需的基本任务和概念。
author: v-npaladugu
ms.author: surbhigupta
ms.topic: how-to
localization_priority: Normal
ms.openlocfilehash: 455809e64a934384d28e00bdf721ae8c66cb7d19
ms.sourcegitcommit: 54f6690b559beedc330b971618e574d33d69e8a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2022
ms.locfileid: "62363414"
---
# <a name="in-app-purchases"></a>应用内购买

Microsoft Teams API，可用于实现应用内购买，以从免费升级到付费Teams应用。 应用内购买允许你直接从应用内将用户从免费计划转换为付费计划。

> [!NOTE]
> 当前仅在开发人员预览Teams应用的应用内 [**购买**](/microsoftteams/platform/resources/dev-preview/developer-preview-intro)。

## <a name="implement-in-app-purchases"></a>实现应用内购买

若要向应用用户提供应用内购买体验，请确保以下各项：

* 应用基于客户端 [SDK Teams构建](https://github.com/OfficeDev/microsoft-teams-library-js)。

* 应用通过可交易 [SaaS 产品/服务启用](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)。

* 使用 [RSC 权限启用应用](#update-manifest)。

* 使用 API 调用 [`openPurchaseExperience` 应用](#purchase-experience-api)。

可通过更新 **manifest.json** 文件或从开发人员门户的权限部分启用显示应用内购买产品/服务来启用应用内 **购买体验**。

### <a name="update-manifest"></a>更新清单

若要启用应用内购买体验，请Teams RSC 权限更新你的 Teams app **manifest.json** 文件。 它允许你的应用用户升级到应用的付费版本并开始使用新功能。 应用清单的更新如下所示：

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
```

### <a name="purchase-experience-api"></a>购买体验 API

若要触发应用内购买，请从 `openPurchaseExperience` Web 应用调用 API。

下面是从应用调用 API 的示例：

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

以下示例显示用户为名为 *Contoso Tasks* for Teams 虚拟应用程序购买订阅Teams：

1. 在 Teams **应用商店中**，查找并选择该应用。

1. 在应用详细信息对话框中，选择 **"购买订阅"或** " **为我添加"**。 

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplancontoso.png" alt-text="购买所选应用的订阅。" border="true":::

    
1. **"为我添加** "提供应用的免费试用版，稍后 **将其** 升级到付费版本。

    :::image type="content" source="~/assets/images/saas-offer/upgradeapp.png" alt-text="升级到所选应用的订阅。" border="true":::

1. 在" **选择订阅计划** "对话框中，选择该计划并选择"签出 **"**。

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplancontoso.png" alt-text="选择适当的订阅计划。" border="true":::

1. 完成交易，然后选择"现在 **配置** "以设置订阅。

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-configure-now.png" alt-text="设置订阅。" border="true":::

    :::image type="content" source="~/assets/images/saas-offer/getstarted.png" alt-text="订阅的登陆页面。" border="true":::


## <a name="see-also"></a>另请参阅

* [将 SaaS 产品/服务与Microsoft Teams一起](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
* [创建 SaaS 服务 (软件) 服务](include-saas-offer.md#create-your-saas-offer)