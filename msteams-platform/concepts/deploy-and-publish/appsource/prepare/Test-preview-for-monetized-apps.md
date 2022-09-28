---
title: 针对盈利应用的测试预览
author: v-ypalikila
description: 在实时推送产品/服务之前，为 Teams 应用创建和测试 SaaS 预览版产品/服务。 创建预览产品/服务 ID，使用预览产品/服务 ID 配置应用，并旁加载。
ms.topic: conceptual
ms.author: v-ypalikila
ms.localizationpriority: high
ms.openlocfilehash: 98b9876a93fe6040cf66a16475fe7fdacf98a520
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100789"
---
# <a name="test-preview-for-monetized-apps"></a>针对盈利应用的测试预览

你可以创建软件即服务 (SaaS) 产品/服务，并在 Teams 中测试盈利应用的端到端购买体验。 作为 Teams 应用的预览版受众添加的用户可以在发布之前查看你的 SaaS 产品/服务。

## <a name="create-a-preview-offer-id"></a>创建预览版产品/服务 ID

可以从合作伙伴中心中的 **AppSource 预览** 链接生成预览版产品/服务 ID。 确保 SaaS 产品/服务处于预览版创建阶段。 要生成预览版产品/服务 ID，请执行以下操作：

1. 转到 [合作伙伴中心](https://go.microsoft.com/fwlink/?linkid=2166002) 并使用开发人员凭据登录。
1. 选择“**市场产品/服务**”。
1. 选择要预览的 SaaS 产品/服务。
1. 为 SaaS 产品/服务添加 [预览版受众](/azure/marketplace/create-new-saas-offer-preview)。
1. 选择“**上线发布**”下面的“**AppSource 预览**”链接，以在浏览器地址栏中查找采用 *publisherId.offerId-preview* 格式的预览版产品/服务 ID。

    :::image type="content" source="../../../../assets/images/apps-in-meetings/publish-status-publisher-signoff.png" alt-text="预览版产品/服务 ID" :::

1. 从浏览器地址栏复制预览版产品/服务 ID。

      :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-monetized-apps-preview-offer-id.png" alt-text="预览版产品/服务" :::

    > [!NOTE]
    > Unlike a public offer ID, the Preview offer ID can be recognized with the *-preview* suffix. For example, **publisherId.offerId-preview**.

## <a name="configure-your-app-with-the-preview-offer-id"></a>使用预览版产品/服务 ID 配置应用

开始之前，请使用带 **预览版受众** 的开发人员账户登录到 **开发人员门户**，以便用户在 Teams 应用商店中查看订阅计划。

After you've generated your Preview offer ID, link the offer ID to your Teams app. To link the offer ID:

1. 转到 [开发人员门户](https://dev.teams.microsoft.com/) 并使用开发人员凭据登录。
1. 从左窗格中选择“**应用**”。
1. 选择要将 SaaS 产品/服务链接到的应用。
1. 选择“**计划和定价**”，然后输入 **发布者 ID** 和 **产品/服务 ID**。  
  确保产品/服务 ID 包含 *-preview* 后缀。
1. 选择“**查看**”以预览订阅计划。
1. 查看“**应用订阅**”下列出的计划，然后选择“**保存**”。

    :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-add-offer-id.png" alt-text="添加产品/服务 id" :::

将 subscriptionOffer 属性添加到应用清单。

```json
"subscriptionOffer": {
     "offerId": "publisherId.offerId-preview"  
     }
```

>[!NOTE]
> 检查“**应用订阅**”旁边的标签“*预览版产品/服务*”，以确认产品/服务是否为预览版产品/服务。

## <a name="sideload-the-app-to-teams"></a>将应用旁加载到 Teams

使用预览版产品/服务 ID 配置应用后，创建更新的应用包并将其上传到 Teams 以测试端到端购买体验。 有关详细信息，请参阅 [在 Microsoft Teams 中上传应用](../../apps-upload.md)。 还可以在 Teams 开发人员门户中选择“**在 Teams 中预览**”，以便在 Teams 客户端中快速启动应用。

如果在应用清单中指定了预览版产品/服务，并且预览版受众是在产品/服务的合作伙伴中心内定义的，则用户可以看到“**购买订阅**”按钮。

:::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-buy-subscription.png" alt-text="购买订阅":::

### <a name="error-scenarios"></a>错误方案

* 如果指定了产品/服务 ID，但用户不属于合作伙伴中心中定义的 **预览版受众**，则将不启用“**购买订阅**”按钮，并且应用将向用户显示以下警告消息：

  找不到带有 **-preview** 的计划。 请确保你属于预览版受众。

  :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-no-preview-audience.png" alt-text="无预览版受众" :::

* 如果应用清单中指定的产品/服务 ID 不是预览版产品/服务，应用将向用户显示以下警告消息，并禁用旁加载：
  
  这不是预览版产品/服务。 请务必将 **-preview** 追加到产品/服务 ID。

  :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-no-preview-offer-id.png" alt-text="无 -preview" :::

## <a name="see-also"></a>另请参阅

* [Microsoft Teams 应用随附 SaaS 产品/服务](include-saas-offer.md)
* [创建软件即服务 (SaaS) 产品/服务](include-saas-offer.md#create-your-saas-offer)
* [为 SaaS 产品/服务添加预览版受众](/azure/marketplace/create-new-saas-offer-preview)
* [预览创建阶段](/azure/marketplace/review-publish-offer)
* [查看并向商业市场发布产品/服务](/azure/marketplace/review-publish-offer#validation-and-publishing-steps)
