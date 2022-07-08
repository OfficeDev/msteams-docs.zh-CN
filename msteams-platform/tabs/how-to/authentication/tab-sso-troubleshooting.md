---
title: 在 Teams 中使用 SSO 对选项卡的身份验证进行故障排除
description: 排查 Teams 中的 SSO 身份验证问题以及如何在选项卡中使用它
ms.topic: how-to
ms.localizationpriority: high
keywords: 团队身份验证选项卡 Microsoft Azure Active Directory (Azure AD) SSO 错误问题
ms.openlocfilehash: fa17ffef08f85124a230f76419158f4216f55416
ms.sourcegitcommit: 07f41abbeb1572a306a789485953c5588d65051e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2022
ms.locfileid: "66658952"
---
# <a name="troubleshoot-sso-authentication-in-teams"></a>在 Teams 中的 SSO 身份验证故障排除

下面是有关 SSO 的问题和问题列表，以及如何解决这些问题。
<br>

## <a name="support-for-microsoft-graph"></a>支持 Microsoft Graph

<br>
<details>
<summary>1. 图形 API 是否适用于 Postman？</summary>
<br>
可以将 Microsoft Graph Postman 集合与 Microsoft Graph API 配合使用。

有关详细信息，请参阅[结合使用 Postman 和 Microsoft Graph API](/graph/use-postman)。
</details>
<br>
<details>
<summary>2. 图形 API 是否适用于 Microsoft Graph 资源管理器？</summary>
<br>
是的，图形 API 在 Microsoft Graph 资源管理器中工作。

有关详细信息，请参阅 [Graph 浏览器](https://developer.microsoft.com/graph/graph-explorer)。

</details>
<br>

## <a name="error-messages-and-how-to-handle-them"></a>错误消息及其处理方式

<br>
<details>
<summary>1. 错误：缺少同意。</summary>
<br>
当 Azure AD 收到访问 Microsoft Graph 资源的请求时，它会检查用户（或租户管理员）是否同意此资源。 如果用户或管理员没有同意记录，Azure AD 向 Web 服务发送错误消息。

代码必须告知客户端（例如，在 403 禁止访问响应的正文中）如何处理错误：

- 如果选项卡应用需要 Microsoft Graph 仅管理员可以为其授予同意的范围，则代码应生成错误。
- 如果用户只能许可所需的范围，则代码应回退到用户身份验证备用系统。

</details>
<br>
<details>
<summary>2. 错误：缺少作用域（权限）。</summary>
<br>
此错误仅在开发过程中出现。

若要处理此错误，服务器端代码应向客户端发送 403 禁止响应。 它应将错误记录到控制台或将其记录在日志中。
</details>
<br>
<details>
<summary>3. 错误：Microsoft Graph 的访问令牌中的受众无效。</summary>
<br>
服务器端代码应向客户端发送 403 禁止访问响应，以向用户显示消息。 建议还应将错误记录到控制台，或将其记录在日志中。
</details>
<br>
<details>
<summary>4. 错误：主机名不能基于已拥有的域。</summary>
<br>
可以在以下两种方案之一中收到此错误：

1. 不会将自定义域添加到 Azure AD。 若要将自定义域添加到 Azure AD并注册它，请按照 [添加自定义域名Azure AD](/azure/active-directory/fundamentals/add-custom-domain) 过程，然后按照步骤再次 [配置访问令牌的范围](tab-sso-register-aad.md#configure-scope-for-access-token)。
1. 你未在 Microsoft 365 租赁中使用管理员凭据登录。 以管理员身份登录 Microsoft 365。

</details>
<br>
<details>
<summary>5. 错误：在返回的访问令牌中未收到用户主体名称 (UPN)。</summary>
<br>
可以在 Azure AD 中将 UPN 添加为可选声明。

有关详细信息，请参阅 [向应用提供可选声明](/azure/active-directory/develop/active-directory-optional-claims) 和 [访问令牌](/azure/active-directory/develop/access-tokens)。
</details>
<br>
<details>
<summary>6. 错误：Teams SDK 错误：resourceDisabled。</summary>
<br>
若要避免此错误，请确保在 Azure AD 应用注册和 Teams 客户端中正确配置应用程序 ID URI。

有关应用程序 ID URI 的详细信息，请参阅“[公开 API](tab-sso-register-aad.md#to-expose-an-api)”。

</details>
<br>

<details>
<summary>7. 错误：运行选项卡应用时出现常规错误。</summary>
<br>
当在 Azure AD 中进行的一个或多个应用配置不正确时，可能会显示一般性错误。 若要解决此错误，请检查在代码和 Teams 清单中配置的应用详细信息是否与 Azure AD 中的值匹配。

下图显示了在 Azure AD 中配置的应用详细信息的示例。

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-app-details.png" alt-text="Azure AD 中的应用配置值":::

检查以下值是否在 Azure AD、客户端代码和 Teams 应用清单之间匹配：

- **应用 ID**：在 Azure AD 中生成的应用 ID 在代码和 Teams 清单文件中应相同。 检查 Teams 清单中的应用 ID 是否与 Azure AD 中的应用程序 **（客户端）ID** 匹配。

- **应用机密**：在应用后端配置的应用机密应与Azure AD中 **的客户端凭据** 匹配。
    还应检查客户端密码是否已过期。

- **应用程序 ID URI**：代码和 Teams 应用清单文件中的应用 ID URI 应与 Azure AD 中的应用程序 **ID URI** 匹配。

- **应用权限**：检查你在作用域中定义的权限是否与应用要求一样。 如果是这样，请检查是否在访问令牌中向用户授予了访问令牌。

- **管理员同意**：如果任何范围都需要管理员同意，请检查是否已向用户授予特定作用域的同意。

此外，检查发送到选项卡应用的访问令牌，以验证以下值是否正确：

- **受众 (aud)**：检查令牌中的应用 ID 是否正确，如 Azure AD 中所述。
- **租户 ID (tid)**：检查令牌中提到的租户是否正确。
- **用户标识 (preferred_username)**：检查用户标识是否与当前用户要访问的范围的访问令牌请求中的用户名匹配。
- **作用域 (scp)**：检查请求访问令牌的作用域是否正确，以及 Azure AD 中定义的范围。
- **Azure AD 版本 1.0 或 2.0 (ver)**：检查 Azure AD 版本是否正确。

可以使用 [JWT](https://jwt.ms) 检查令牌。

</details>
