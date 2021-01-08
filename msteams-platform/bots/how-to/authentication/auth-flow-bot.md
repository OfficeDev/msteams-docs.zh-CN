---
title: 自动程序 Microsoft Teams 身份验证流
description: 介绍自动程序中的 Microsoft Teams 身份验证流
keywords: teams 身份验证流机器人
ms.topic: overview
ms.openlocfilehash: 3d1d0055984de07b50a45015e062e6725279d1aa
ms.sourcegitcommit: b9771f8f4be9ac1ff8c85c2d7bd8d5c5408bc653
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/06/2021
ms.locfileid: "49768079"
---
# <a name="authentication-flow-for-bots-in-microsoft-teams"></a>Microsoft Teams 中机器人的身份验证流程

OAuth 2.0 是 Azure Active Directory 和 Azure AD (和许多其他标识提供程序) 身份验证和授权的开放标准。 基本了解 OAuth 2.0 是在 Teams 中处理身份验证的先决条件; [下面是比](https://aaronparecki.com/oauth-2-simplified/) 正式规范更易于遵循的一个很好的 [概述](https://oauth.net/2/)。 选项卡和聊天机器人的身份验证流有一点不同 — 选项卡与网站非常相似，因此它们可以直接使用 OAuth 2.0，而自动程序不会并且必须执行一些不同操作，但核心概念是相同的。

有关演示使用 Node.js 和[OAuth 2.0](https://oauth.net/2/grant-types/authorization-code/)授权代码授予类型的自动程序身份验证流的示例，请参阅 GitHub 存储库[Microsoft Teams](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)身份验证示例。

![自动程序身份验证序列图](../../../assets/images/authentication/bot_auth_sequence_diagram.png)

1. 用户向自动程序发送消息。
2. 自动程序确定用户是否需要登录。
   本示例中，机器人将访问令牌存储在其用户数据存储中。 如果用户没有所选标识提供程序的验证令牌，则要求用户登录。  ([查看代码) ](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76)
3. 机器人将构造身份验证流的起始页的 URL，然后通过操作向用户发送 `signin` 卡片。  ([查看代码) ](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190)</br>
    与 Teams 中的其他应用程序身份验证流一样，起始页必须位于列表上的域中，并且必须与登录后重定向页位于 `validDomains` 同一域中。
    > [!IMPORTANT] 
    > OAuth 2.0 授权代码为身份验证请求中的参数授予流调用，该参数包含唯一的会话令牌，以防止跨站点请求 `state` [伪造攻击](https://en.wikipedia.org/wiki/Cross-site_request_forgery)。 该示例使用随机生成的 GUID。
4. 当用户选择登录按钮时，Teams 将打开一个弹出窗口并导航到起始页。 
   > [!NOTE]
   > 弹出窗口的大小可以通过 URL 中的宽度和高度查询字符串参数进行控制。 例如，如果添加 width=500 且 height=500，弹出窗口的大小为 500x500 像素。 Teams 显示具有给定像素大小的弹出窗口，最大像素大小是主窗口大小的百分比。

5. 起始页将用户重定向到标识提供程序的 `authorize` 终结点。  ([查看代码) ](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56)
6. 在提供商的网站上，用户登录并授予对自动程序的访问权限。
7. 提供程序使用授权代码将用户定向到机器人的 OAuth 重定向页面。
8. 机器人兑换授权代码获取访问令牌，并临时将令牌与启动登录流程的用户关联。 下面，我们将此称为 *临时令牌*。
    * 在示例中，自动程序将参数值与启动登录过程的用户的 ID 关联，以便稍后可以与标识提供程序返回的值 `state` `state` 匹配。  ([查看代码) ](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99)
      > [!IMPORTANT] 
      > 机器人存储从标识提供程序收到的令牌，并关联到特定用户，但标记为"待验证"。 
    * 如果不进一步验证，则不能使用临时令牌。
      1. **验证从标识提供程序接收的信息。** 必须针对 `state` 之前保存的值确认参数的值。 
      1. **验证从 Teams 接收内容。** [执行两步](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)身份验证验证，以确保向标识提供程序授权自动程序的用户是正在与机器人聊天的同一用户。 这可[抵御中间人和网络钓鱼](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)[攻击](https://en.wikipedia.org/wiki/Phishing)。 自动程序生成验证码并存储它，与用户相关联。 验证码由 Teams 自动发送，如下所述。  ([查看代码) ](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113)
9. OAuth 回调呈现调用的页面 `notifySuccess("<verification code>")` 。  ([查看代码) ](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs)
10. Teams 关闭弹出窗口，并将发送的发送信息 `<verification code>` `notifySuccess()` 发送回自动程序。 自动程序接收 [与的调用](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) 消息 `name = signin/verifyState` 。
11. 自动程序根据使用用户临时令牌存储的验证码检查传入验证码。  ([查看代码) ](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140)
12. 如果匹配，机器人将令牌标记为已验证并可供使用。 否则，身份验证流将失败，自动程序会删除临时令牌。

    > [!NOTE]
    > 如果在移动设备上遇到身份验证问题，请确保 JavaScript SDK 已更新到版本 1.4.1 或更高版本。

## <a name="samples"></a>示例

有关显示自动程序身份验证过程的示例代码，请参阅：

[Microsoft Teams 自动程序身份验证示例 (Node.js) ](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)

## <a name="more-details"></a>更多详细信息

有关面向 Azure AD 的机器人身份验证的详细实现演练，请参阅：

[向 Teams 自动程序添加身份验证](add-authentication.md)
