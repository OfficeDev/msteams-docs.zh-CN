---
title: 使用第三方 OAuth 提供程序启用身份验证
description: 本文介绍选项卡、第三方 OAuth 提供程序、OAuth by Azure AD 和身份验证代码示例中的 Teams 身份验证流。
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 33300461e16f5a8ab5e1e69f5fea775adb2359aa
ms.sourcegitcommit: d5628e0d50c3f471abd91c3a3c2f99783b087502
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2022
ms.locfileid: "67435054"
---
# <a name="enable-authentication-using-third-party-oauth-provider"></a>使用第三方 OAuth 提供程序启用身份验证

可以使用第三方 OAuth 标识提供程序 (IdP) 在选项卡应用中启用身份验证。 在此方法中，应用用户标识由 OAuth IdP（例如 Azure AD、Google、Facebook、GitHub 或任何其他提供程序）验证并授予访问权限。 需要配置与 IdP 的信任关系，并且应用用户也应向其注册。

> [!NOTE]
> 要使身份验证适用于移动客户端上的选项卡，需要确保至少使用 Microsoft Teams JavaScript SDK 版本 1.4.1。  
> Teams SDK 会为身份验证流启动单独的窗口。 将 `SameSite` 属性设置为 **Lax**。 Teams 桌面客户端或旧版 Chrome 或 Safari 不支持 `SameSite`=None。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="use-oauth-idp-to-enable-authentication"></a>使用 OAuth IdP 启用身份验证

OAuth 2.0 是 Microsoft Azure Active Directory (Azure AD) 和许多其他身份提供程序用于身份验证和授权的开放标准。 对 OAuth 2.0 的基本理解是在 Teams 选项卡中使用身份验证的先决条件。 有关详细信息，请参阅[简化 OAuth 2](https://aaronparecki.com/oauth-2-simplified/)，这比[正式规范](https://oauth.net/2/)更容易遵循。 选项卡的身份验证流和机器人不同，因为选项卡类似于网站，因此可以直接使用 OAuth 2.0。 机器人以不同方式执行一些操作，但核心概念是相同的。

例如，使用 Node 和“[OAuth 2.0 隐式授权类型](https://oauth.net/2/grant-types/implicit/)”的选项卡和机器人的身份验证流，请参阅[启动选项卡的身份验证流](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow)。

本部分使用 Azure AD 作为第三方 OAuth 提供程序的示例，以便在选项卡应用中启用身份验证。

> [!NOTE]
> 在向用户显示“**登录**”按钮并调用 `authentication.authenticate` API 以对选择按钮做出响应之前，必须等待 SDK 初始化完成。 可以链接 `.then()` 处理程序或 `await` 使函 `app.initialize()` 数完成。

![选项卡身份验证序列图](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. 用户与选项卡配置或内容页面上的内容交互，通常使用“**登入**”或“**登录**”按钮。
2. 该选项卡可构造其身份验证起始页的 URL。 或者，它使用 URL 占位符或调用 `app.getContext()` Teams 客户端 SDK 方法的信息来简化用户的身份验证体验。 例如，使用 Azure AD 进行身份验证时，如果 `login_hint` 参数设置为用户的电子邮件地址，则用户无需登录（如果他们最近这样做）。 这是因为 Azure AD 使用用户的已缓存凭据。 弹出窗口会短暂显示，然后消失。
3. 然后，该选项卡调用该 `authentication.authenticate()` 方法。
4. Teams 将在弹出窗口中的 iframe 打开起始页。 起始页生成随机 `state` 数据，将其保存以供将来验证，并重定向到身份提供程序的 `/authorize` 端点，例如 Azure AD 的 `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize`。 将 `<tenant id>` 替换为自己的租户 ID（即 context.tid）。
与 Teams 中的其他应用授权流类似，起始页必须在其 `validDomains` 列表中的域上，并且与签到后的重定向页面在同一个域上。

    > [!NOTE]
    > OAuth 2.0 隐式授权流在认证请求中调用包含唯一的会话数据的 `state` 参数，以防止[跨站请求伪造 (CSRF) 攻击](https://en.wikipedia.org/wiki/Cross-site_request_forgery)。下面的示例使用随机生成的 GUID 作为 `state` 数据。

5. 在提供程序网站上，用户签到并授予对该选项卡的访问权限。
6. 提供程序通过访问令牌将用户带到选项卡的 OAuth 2.0 重定向页面。
7. 该选项卡检查返回 `state` 的值是否与之前保存的值匹配，并调用调用，而调 `authentication.notifySuccess()`用成功处理程序 (`.then()`) 步骤 3 中基于 `authenticate()` 承诺的方法。
8. Teams 关闭弹出窗口。
9. 选项卡根据用户开始的位置，要么显示配置 UI，要么刷新或重新加载选项卡内容。

> [!NOTE]
> 如果应用程序支持 SAML SSO，则无法使用选项卡 SSO 生成的 JWT 令牌，因为它不受支持。

## <a name="treat-tab-context-as-hints"></a>将选项卡上下文视为提示

尽管选项卡上下文提供了有关用户的有用信息，但不要使用此信息对用户进行身份验证。 即使将信息作为 URL 参数获取到选项卡内容 URL 或通过调用 Microsoft Teams 客户端 SDK 中的 `app.getContext()` 函数，也要对用户进行身份验证。 恶意操作者可以使用自己的参数调用选项卡内容 URL。 操作者还可以调用模拟 Microsoft Teams 的网页，在 iframe 中加载选项卡内容 URL，并将其本身数据返回到 `getContext()` 函数。 必须将选项卡上下文中与身份相关的信息视为提示，并在使用前对其进行验证。 请参阅[从弹出页导航到授权页](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page)中的备注。

## <a name="code-sample"></a>代码示例

显示选项卡身份验证流程的示例代码：

| **示例名称** | **说明** | **C#** | **Node.js** |
|-----------------|-----------------|-------------|------------|
| Teams 选项卡身份验证 | 使用 Azure AD 的选项卡身份验证流程。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/nodejs) |

## <a name="see-also"></a>另请参阅

有关使用 Azure AD 实施选项卡身份验证的详情，请参阅：

* [在 Teams 选项卡中对用户进行身份验证](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [无提示的身份验证](~/tabs/how-to/authentication/auth-silent-AAD.md)
