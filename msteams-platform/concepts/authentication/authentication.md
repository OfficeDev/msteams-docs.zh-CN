---
title: 对应用用户进行身份验证
description: 介绍 Teams 中的身份验证以及如何在应用中使用它
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Teams 身份验证 OAuth SSO Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: 53f258769140a2b40bb59a1232250f74ec693bee
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757155"
---
# <a name="authenticate-users-in-microsoft-teams"></a>在 Microsoft Teams 中对用户进行身份验证

> [!Note]
> 移动客户端上基于 Web 的身份验证需要版本 1.4.1 或更高版本的 Teams JavaScript 客户端 SDK。

若要访问受 Azure AD 保护的用户信息以及从 Facebook 和 Twitter 等服务访问数据，应用需要与这些提供商建立受信任的连接。 如果应用在用户范围内使用 Microsoft Graph API，则请对用户进行身份验证，以检索相应的身份验证令牌。

Teams 中包含两种两种不同的应用身份验证流程。 在嵌入在选项卡、配置页面或任务模块中的[内容页面](~/tabs/how-to/create-tab-pages/content-page.md)中执行传统的基于 Web 的身份验证流程。 如果应用包含对话机器人，请使用 OAuthPrompt 流和 Azure Bot Framework 的令牌服务（可选），在对话中对用户进行身份验证。

## <a name="web-based-authentication-flow"></a>基于 Web 的身份验证流程

对[选项卡](~/tabs/what-are-tabs.md)使用基于 Web 的身份验证流程，并选择将其与[对话机器人](~/bots/what-are-bots.md)或[消息传递扩展](~/messaging-extensions/what-are-messaging-extensions.md)一起使用。 在 Web 内容页面中使用 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 来启用身份验证。 启用身份验证后，将内容页面嵌入到选项卡、配置页面或任务模块中。 有关基于 Web 的身份验证流程的详细信息，请参阅：

* [向 Teams 机器人添加身份验证](~/bots/how-to/authentication/add-authentication.md)介绍如何将基于 Web 的身份验证流程与聊天机器人配合使用。
* [选项卡中的身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)描述选项卡身份验证在Teams中的工作原理，其中显示了用于选项卡的典型基于 Web 的身份验证流。
* [选项卡中的 Azure AD 身份验证](~/tabs/how-to/authentication/auth-tab-AAD.md)介绍如何从Teams 应用的选项卡内连接到 Azure AD。
* [无提示身份验证 Azure AD](~/tabs/how-to/authentication/auth-silent-AAD.md)介绍如何使用Azure AD 减少应用中的登录或同意提示。
* [.Net 或 C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) 或者 [JavaScript 或 Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) 提供了基于 Web 的身份验证示例。

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>对话机器人的 OAuthPrompt 流程

Azure Bot Framework OAuth Prompt 使你可以更轻松地对使用对话机器人的应用程序进行身份验证。 使用 Azure Bot Framework 的令牌服务来协助进行令牌缓存。

有关使用 OAuthPrompt 的详细信息，请参阅：

* [机器人身份验证流概述](~/bots/how-to/authentication/auth-flow-bot.md)介绍了身份验证在Teams应用中的机器人中的工作原理，其中显示了用于Teams Web、桌面应用和移动应用上的机器人的基于 Web 的身份验证流。
* [机器人身份验证](~/bots/how-to/authentication/add-authentication.md)介绍如何将 OAuth 身份验证添加到 Teams 机器人。

## <a name="code-sample"></a>代码示例

提供机器人身份验证 v3 SDK 示例。

| **示例名称** | **说明** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| 机器人身份验证 | 此示例演示如何开始在 Microsoft Teams 机器人中进行身份验证。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| 选项卡、机器人和消息扩展 (ME) SSO | 此示例显示用于 Tab、Bot 和 ME 的 SSO - 搜索、操作、链接展开。 |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | 不可用 |

## <a name="configure-the-identity-provider"></a>配置标识提供程序

无论应用的身份验证流程如何，都可配置标识提供程序以便为与 Teams 应用通信。 大多数示例和演练主要涉及将 Azure AD 用作标识提供程序。 但是，无论标识提供程序如何，这些概念都适用。

有关详细信息，请参阅[配置标识提供程序](~/concepts/authentication/configure-identity-provider.md)。

## <a name="third-party-cookies-on-ios"></a>iOS 上的第三方 Cookie

iOS 14 更新后，Apple 默认阻止所有应用的[第三方 Cookie](https://webkit.org/blog/10218/full-third-party-cookie-blocking-and-more/) 访问。 因此，利用第三方 Cookie 在其频道或聊天选项卡和个人应用中进行身份验证的应用将无法在Teams iOS客户端上完成其身份验证工作流。 若要符合隐私和安全要求，必须转为使用基于令牌的系统，或在用户身份验证工作流程中使用第一方 Cookie。

## <a name="see-also"></a>另请参阅

* [选项卡的 Microsoft Teams 身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)
* [为机器人提供单一登录支持](~/bots/how-to/authentication/auth-aad-sso-bots.md)
* [为消息扩展添加身份验证](~/messaging-extensions/how-to/add-authentication.md)
