---
title: 配置 OAuth 2.0 标识提供程序
description: 介绍如何在 Azure AD 上配置标识提供程序和焦点
keywords: 团队身份验证 AAD oauth 标识提供程序
ms.openlocfilehash: 799b0c20cda64456a4610acbdbedf758989bee55
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673377"
---
# <a name="configuring-identity-providers"></a>配置标识提供程序

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a>将应用程序配置为使用 Azure Active Directory 作为标识提供程序

支持 OAuth 2.0 的标识提供程序将不会对来自未知应用程序的请求进行身份验证;必须提前注册应用程序。 若要在 Azure AD 中执行此操作，请按照以下步骤操作：

1. 打开 "[应用程序注册门户](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)"。

2. 选择您的应用程序以查看其属性，或单击 "新建注册" 按钮。 查找应用程序的 "**重定向 URI** " 部分。

3. 在下拉菜单中，确保选择 " **Web** "。 更新身份验证终结点的 URL。 对于 GitHub 上的 TypeScript/node.js 和 c # 示例应用程序，重定向 Url 将类似于以下内容：

    重定向 Url：`https://<hostname>/bot-auth/simple-start`

将`<hostname>`替换为实际主机。 这可能是一个专用的承载网站，如 Azure、问题或与开发计算机上的 localhost （如） `abcd1234.ngrok.io`的 ngrok 隧道。 如果尚未完成或托管您的应用程序（或上面提到的示例应用程序），则可能还没有这些信息，但在已知该信息时，您始终可以返回此页面。

## <a name="other-authentication-providers"></a>其他身份验证提供程序

* **LinkedIn**按照[配置 LinkedIn 应用程序](https://developer.linkedin.com/docs/oauth2)中的说明操作

* **Google**从[GOOGLE API 控制台](https://console.developers.google.com/)获取 OAuth 2.0 客户端凭据
