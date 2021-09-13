---
title: 选项卡的身份验证流
description: 描述选项卡中的身份验证流
ms.topic: conceptual
ms.localizationpriority: medium
keywords: teams 身份验证流选项卡
ms.openlocfilehash: f95a9c89fd8d40078de064da0ca7c33d929dc0a1
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155283"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>Microsoft Teams选项卡的身份验证流

> [!NOTE]
> 若要在移动客户端上对选项卡进行身份验证，必须确保使用的是至少 1.4.1 版本的 Microsoft Teams JavaScript SDK。
> TeamsSDK 为身份验证流启动单独的窗口。 将 `SameSite` 属性设置为 **Lax**。 Teams版桌面客户端或较旧版本的 Chrome 或 Safari 不支持 `SameSite` =None。

OAuth 2.0 是一个开放标准，供 AAD Azure Active Directory (和许多其他) 使用的身份验证和授权。 对 OAuth 2.0 有基本的了解是在 Teams 中进行身份验证的先决条件。 有关详细信息，请参阅 [OAuth 2 简化](https://aaronparecki.com/oauth-2-simplified/) ，比正式规范 [更易于遵循](https://oauth.net/2/)。 选项卡和聊天机器人的身份验证流不同，因为选项卡类似于网站，因此可以直接使用 OAuth 2.0。 机器人执行一些不同操作，但核心概念是相同的。

有关使用 Node 和 [OAuth 2.0](https://oauth.net/2/grant-types/implicit/)隐式授予类型的选项卡和聊天机器人的身份验证流示例，请参阅 [启动选项卡的身份验证流](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow)。

> [!NOTE]
> 在向 **用户显示登录** 按钮并调用 API 以响应选择该按钮之前，必须等待 `microsoftTeams.authentication.authenticate` SDK 初始化完成。 你可以将回调传递到 `microsoftTeams.initialize` 初始化完成时调用的 API。

![选项卡身份验证序列图](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. 用户与选项卡配置或内容页上的内容交互，通常为" **登录** "或" **登录"** 按钮。
2. 选项卡将构造其身份验证起始页的 URL。 （可选）它使用 URL 占位符的信息或Teams `microsoftTeams.getContext()` 客户端 SDK 方法，以简化用户的身份验证体验。 例如，使用 AAD 进行身份验证时，如果参数设置为用户的电子邮件地址，则如果用户最近已登录，则无需 `login_hint` 登录。 这是因为 AAD 使用用户的缓存凭据。 弹出窗口短暂显示，然后消失。
3. 然后选项卡调用 `microsoftTeams.authentication.authenticate()` 方法，并注册 `successCallback` 和 `failureCallback` 函数。
4. Teams弹出窗口中的 iframe 中打开起始页。 起始页将生成随机数据、保存数据供将来验证，并重定向到标识提供程序的终结点，如 `state` `/authorize` Azure `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` AD。 将 `<tenant id>` 替换为你自己的租户 ID，即 context.tid。
与应用程序中的Teams身份验证流类似，起始页必须位于其列表中的域上，并且必须与登录后重定向页位于同一 `validDomains` 域中。

    > [!NOTE]
    > OAuth 2.0 隐式授权流调用身份验证请求中的参数，其中包含唯一的会话数据以防止 `state` 跨站点请求 [伪造攻击](https://en.wikipedia.org/wiki/Cross-site_request_forgery)。 这些示例对数据使用随机生成的 `state` GUID。

5. 在提供商网站上，用户登录并授予对选项卡的访问权限。
6. 提供程序将用户定向到具有访问令牌的选项卡的 OAuth 2.0 重定向页面。
7. 该选项卡检查返回的值是否与之前保存的值匹配，并调用 ，这反过来调用在步骤 3 中注册 `state` `microsoftTeams.authentication.notifySuccess()` `successCallback` 的函数。
8. Teams关闭弹出窗口。
9. 选项卡显示配置 UI、刷新或重新加载选项卡内容，具体取决于用户从何处开始。

## <a name="treat-tab-context-as-hints"></a>将选项卡上下文视为提示

尽管选项卡上下文提供了有关用户的有用信息，但请勿使用此信息对用户进行身份验证。 即使您将信息作为 URL 参数获取至您的选项卡内容 URL，或者通过调用 Microsoft Teams SDK 中的 函数，也可以 `microsoftTeams.getContext()` 对用户进行身份验证。 恶意参与者可以使用自己的参数调用您的选项卡内容 URL。 主角还可以调用模拟 web 页面Microsoft Teams在 iframe 中加载选项卡内容 URL，然后向 函数返回自己的 `getContext()` 数据。 你必须将选项卡上下文中的标识相关信息视为提示，并使用前进行验证。 请参阅从弹出式页面导航到 [授权页中的注释](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)。

## <a name="code-sample"></a>代码示例

显示选项卡身份验证过程的示例代码：

| **示例名称** | **说明** | **C#** | **Node.js** |
|-----------------|-----------------|-------------|------------|
| Teams选项卡身份验证 | 使用 AAD 的选项卡的身份验证过程。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/nodejs) |

## <a name="more-details"></a>更多详细信息

有关使用 AAD 进行选项卡身份验证的详细实现，请参阅：

* [在"用户"选项卡中Teams用户](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [无提示的身份验证](~/tabs/how-to/authentication/auth-silent-AAD.md)
