---
title: 创建客户端机密
description: 描述如何创建客户端机密
ms.topic: how-to
ms.localizationpriority: medium
keywords: Azure AD) 图形 API Microsoft Azure Active Directory (团队身份验证选项卡
ms.openlocfilehash: 77d1c4e43c9bdfb9d2cb9e3e97ee3a26b8b0fa01
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558847"
---
# <a name="create-client-secret"></a>创建客户端机密

客户端机密是应用程序在请求令牌时用来证明其标识的字符串。

1. 选择 **“管理** > **证书&机密**。

2. 选择 **+新建客户端机密**。

    :::image type="content" source="../../../assets/images/adaptive-cards/client-secret.png" alt-text="客户端机密页":::

   将显示 **“添加客户端机密** ”页。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-secret.png" alt-text="添加客户端机密页":::

3. 输入说明。
4. 选择机密的有效期。
5. 选择“**添加**”。

   浏览器上弹出一条消息，指出客户端机密已更新，客户端机密显示在页面上。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-secret-added.png" alt-text="添加了客户端机密":::

6. 选择客户端机密 **值** 旁边的复制按钮。
7. 保存复制的值以供以后使用。

   > [!NOTE]
   > 请确保在创建客户端机密后立即复制该值。 该值仅在创建客户端机密时可见，之后无法查看。
