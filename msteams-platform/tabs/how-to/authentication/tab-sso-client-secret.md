---
title: 创建客户端机密
description: 描述如何创建客户端机密
ms.topic: how-to
ms.localizationpriority: medium
keywords: teams 身份验证选项卡 Microsoft Azure Active Directory (Azure AD) 图形 API
ms.openlocfilehash: 79116a0da845cd143de695424a904cf5b5968a15
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2022
ms.locfileid: "65887992"
---
# <a name="create-client-secret"></a>创建客户端机密

客户端机密是应用程序在请求令牌时用来证明其标识的字符串。

1. 选择 **“管理** > **证书&机密**。

2. 选择 **+新建客户端机密**。

    :::image type="content" source="../../../assets/images/adaptive-cards/client-secret.png" alt-text="客户端机密页":::

   将显示 **“添加客户端机密** ”页。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-secret.png" alt-text="添加客户端机密页" border="true":::

3. 输入说明。
4. 选择机密的有效期。
5. 选择“**添加**”。

   浏览器上弹出一条消息，指出客户端机密已更新，客户端机密显示在页面上。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-secret-added.png" alt-text="添加了客户端机密":::

6. 选择客户端机密 **值** 旁边的复制按钮。
7. 保存复制的值以供以后使用。

   > [!NOTE]
   > 请确保在创建客户端机密后立即复制该值。 该值仅在创建客户端机密时可见，之后无法查看。
