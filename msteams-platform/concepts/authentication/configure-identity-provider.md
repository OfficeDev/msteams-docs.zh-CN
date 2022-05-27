---
title: 配置 OAuth 2.0 标识提供程序
description: '介绍如何配置标识提供程序，重点介绍 Microsoft Azure Active Directory (Azure AD) '
ms.topic: how-to
ms.localizationpriority: medium
keywords: teams 身份验证 Azure AD oauth 标识提供程序
ms.openlocfilehash: 6ab95958c66fcf680cdab54d3307eab5dc66fa57
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757050"
---
# <a name="configure-identity-providers"></a>配置标识提供程序

## <a name="configuring-an-application-to-use-azure-ad-as-an-identity-provider"></a>配置应用程序以使用 Azure AD 作为标识提供程序

支持 OAuth 2.0 的标识提供者不会对来自未知应用程序的请求进行身份验证;应用程序必须提前注册。 若要使用 Azure AD 执行此操作，请执行以下步骤：

1. 打开“[应用程序注册门户](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)”。

2. 选择应用以查看其属性，或选择“新建注册”按钮。 查找应用的 **“重定向 URI”** 部分。

3. 从下拉菜单中选择“**Web**”。 将 URL 更新到身份验证终结点。 对于 GitHub 上的 TypeScript/Node.js 和 C# 示例应用，重定向 URL 将类似于以下内容：

    重定向 URL：`https://<hostname>/bot-auth/simple-start`

替换 `<hostname>` 为实际主机，该主机可能是专用托管站点，例如 Azure、Glitch 或到开发计算机上的 localhost 的 ngrok 隧道，例如 `abcd1234.ngrok.io`。 如果尚未完成或托管你的应用 (或上述示例应用)，则可能没有此信息，你始终可以在得知该信息时返回到此页面。

## <a name="other-authentication-providers"></a>其他身份验证提供程序

* **LinkedIn：** 按照 [配置 LinkedIn 应用程序](/linkedin/talent/apply-with-linkedin)中的说明操作

* **Google：** 从 [Google API 控制台](https://console.developers.google.com/)获取 OAuth 2.0 客户端凭据

* **选项卡中的外部 OAuth 提供程序：** 有关详细信息，请参阅 [使用外部 OAuth 提供程序](../../tabs/how-to/authentication/auth-oauth-provider.md)

## <a name="see-also"></a>另请参阅

* [在 Microsoft Teams 机器人中对用户进行身份验证](../../resources/bot-v3/bot-authentication/auth-bot-AAD.md)
* [对选项卡的单一登录 (SSO) 支持](../../tabs/how-to/authentication/auth-aad-sso.md)
* [在 Microsoft Teams 选项卡中对用户进行身份验证](../../tabs/how-to/authentication/auth-tab-aad.md)
