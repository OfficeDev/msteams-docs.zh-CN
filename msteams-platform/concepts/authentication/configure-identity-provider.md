---
title: 配置 OAuth 2.0 标识提供程序
description: '介绍如何配置标识提供程序，并重点关注Microsoft Azure Active Directory (Azure AD) '
ms.topic: how-to
ms.localizationpriority: medium
keywords: teams 身份验证Microsoft Azure Active Directory (Azure AD) oauth 标识提供程序
ms.openlocfilehash: 93622275a8bfc9007af751d8b9f6304a73450ec7
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/10/2022
ms.locfileid: "62517972"
---
# <a name="configure-identity-providers"></a>配置标识提供程序

## <a name="configuring-an-application-to-use-microsoft-azure-active-directory-azure-ad-as-an-identity-provider"></a>将应用程序配置为将Microsoft Azure Active Directory (Azure AD) 用作标识提供程序

支持 OAuth 2.0 的身份提供程序不会对来自未知应用程序的请求进行身份验证;应用程序必须提前注册。 若要使用 Microsoft Azure Active Directory (Azure AD) ，请按照以下步骤操作：

1. 打开 [应用程序注册门户](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)。

2. 选择应用以查看其属性，或选择"新建注册"按钮。 查找 **应用的重定向 URI** 部分。

3. 从 **下拉菜单** 中选择"Web"。 将 URL 更新到身份验证终结点。 对于 TypeScript/Node.js 和 C# 上的示例GitHub，重定向 URL 将类似于以下内容：

    重定向 URL： `https://<hostname>/bot-auth/simple-start`

将 `<hostname>` 替换为实际主机，该主机可能是专用托管站点，如 Azure、Glitch 或开发计算机上 localhost 的 ngrok 隧道（如 `abcd1234.ngrok.io`）。 如果你尚未完成或托管应用 (或上面提到的) 示例应用，你可能不会获得此信息，但当该信息已知时，你始终可以返回到此页面。

## <a name="other-authentication-providers"></a>其他身份验证提供程序

* **LinkedIn：** 按照配置 [LinkedIn 应用程序中的说明操作](/linkedin/talent/apply-with-linkedin)

* **Google：** 从 Google API 控制台获取 OAuth 2.0 [客户端凭据](https://console.developers.google.com/)
