---
title: 针对盈利应用的测试预览
author: v-ypalikila
description: 在实时推送 SaaS 预览Teams应用创建和测试 SaaS 预览产品/服务。
ms.topic: conceptual
ms.author: v-ypalikila
ms.localizationpriority: medium
keywords: teams 应用 SaaS 提供预览产品/服务测试预览盈利 saas
ms.openlocfilehash: 849dd2ecd79a4b43d6feb6ceaca599f371df1de1
ms.sourcegitcommit: 54f6690b559beedc330b971618e574d33d69e8a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2022
ms.locfileid: "62363417"
---
# <a name="test-preview-for-monetized-apps"></a>针对盈利应用的测试预览

> [!NOTE]
> 盈利应用的测试预览当前仅适用于开发人员 [**预览**](/microsoftteams/platform/resources/dev-preview/developer-preview-intro)版。

你可以为 SaaS (软件即服务) ，并测试在 Teams 中盈利应用的端到端购买Teams。 添加为应用预览受众的用户可以Teams发布之前查看 SaaS 产品。

## <a name="create-a-preview-offer-id"></a>创建预览产品/服务 ID

你可以从合作伙伴中心的 **AppSource** 预览链接生成预览产品/服务 ID。 确保 SaaS 产品位于预览创建阶段。 若要生成预览产品/服务 ID，

1. 转到 [合作伙伴中心](https://go.microsoft.com/fwlink/?linkid=2166002) ，然后使用你的开发人员凭据登录。
1. 选择 **"市场产品/服务"**。
1. 选择要预览的 SaaS 产品/服务。
1. 为 [SaaS 产品](/azure/marketplace/create-new-saas-offer-preview) 添加预览受众。
1. 选择 **"上线"下的 AppSource** 预览链接，在采用 *publisherId.offerId-preview* 格式的浏览器地址栏中查找预览产品/服务 ID。

    :::image type="content" source="../../../../assets/images/apps-in-meetings/publish-status-publisher-signoff.png" alt-text="预览产品/服务 ID" border="true" :::

1. 从浏览器地址栏复制预览产品/服务 ID。

      :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-monetized-apps-preview-offer-id.png" alt-text="预览产品/服务 ID" border="true" :::

    > [!NOTE]
    > 与公共产品/服务 ID 不同，可以使用 *-preview* 后缀识别预览产品/服务 ID。 例如， **publisherId.offerId-preview**。

## <a name="configure-your-app-with-the-preview-offer-id"></a>使用预览产品/服务 ID 配置应用

在开始之前，使用具有预览受众的开发人员帐户登录开发人员门户，以便用户在应用商店中Teams计划。

生成预览产品/服务 ID 后，将产品/服务 ID 链接到Teams应用。 若要链接产品/服务 ID：

1. 转到 [开发人员门户](https://dev.teams.microsoft.com/) ，然后使用开发人员凭据登录。
1. 从 **左窗格中** 选择"应用"。
1. 选择要将 SaaS 产品/服务链接到的应用。
1. 选择 **计划和定价**，然后输入Publisher **ID** 和 **产品/服务 ID**。  
  确保产品/服务 ID 包含 *-preview* 后缀。
1. 选择 **"查看** "预览订阅计划。
1. 查看应用订阅下 **列出的计划，****然后选择保存。**

    :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-add-offer-id.png" alt-text="添加产品/服务 ID" :::

subscriptionOffer 属性已添加到应用清单。

```json
"subscriptionOffer": {
     "offerId": "publisherId.offerId-preview"  
     }
```

>[!NOTE]
> 检查应用订阅 *旁边的* 标签预览 **产品/** 服务以确认该优惠是否为预览产品/服务。

## <a name="sideload-the-app-to-teams"></a>将应用旁加载Teams

使用预览产品/服务 ID 配置应用后，创建更新的应用包并将其上传到Teams以测试端到端购买体验。 有关详细信息，请参阅Upload[应用Microsoft Teams](../../apps-upload.md)。 还可以在开发人员门户 **的 Teams** 中选择"预览Teams，以在 Teams 客户端中快速启动你的应用。

如果在应用清单中指定了预览产品/服务，并且预览受众是在产品/服务的合作伙伴中心中定义的，则用户可以看到"购买 **订阅"** 按钮。

:::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-buy-subscription.png" alt-text="购买订阅" border="true":::

### <a name="error-scenarios"></a>错误方案

* 如果指定了产品/服务 ID，但用户不是合作伙伴中心中定义的预览受众的一部分，则"购买订阅"按钮不会启用，并且应用会向用户显示以下警告消息：

  未找到具有 **-preview 的计划**。 请确保你在预览受众中。

  :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-no-preview-audience.png" alt-text="没有准备访问群体" border="true" :::

* 如果应用清单中指定的产品/服务 ID 不是预览版产品/服务，应用会向用户显示以下警告消息，并禁用旁加载：
  
  这不是预览产品/服务。 请务必将 **-preview** 附加到产品/服务 ID。

  :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-no-preview-offer-id.png" alt-text="no -preview" border="true" :::

## <a name="see-also"></a>另请参阅

* [将 SaaS 产品/服务与Microsoft Teams一起](include-saas-offer.md)
* [创建 SaaS 服务 (软件) 服务](include-saas-offer.md#create-your-saas-offer)
* [为 SaaS 产品添加预览受众](/azure/marketplace/create-new-saas-offer-preview)
* [预览创建阶段](/azure/marketplace/review-publish-offer)
* [查看产品/服务并发布到商业市场](/azure/marketplace/review-publish-offer#validation-and-publishing-steps)
