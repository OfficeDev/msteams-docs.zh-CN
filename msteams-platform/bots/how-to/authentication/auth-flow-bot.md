---
title: 适用于 bot 的 Microsoft 团队身份验证流
description: 介绍了 bot 中的 Microsoft 团队身份验证流
keywords: 团队身份验证流 bot
ms.topic: overview
ms.openlocfilehash: b9e72a0e1064779d9a2e49deda24e5e2eaed5962
ms.sourcegitcommit: aca9990e1f84b07b9e77c08bfeca4440eb4e64f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "49409083"
---
# <a name="authentication-flow-for-bots-in-microsoft-teams"></a>Microsoft 团队中的 bot 的身份验证流

OAuth 2.0 是一种开放标准，用于 Azure Active Directory (Azure AD) 和许多其他标识提供程序使用的身份验证和授权。 对 OAuth 2.0 的基本了解是在团队中使用身份验证的先决条件; [下面是一个很好的概述](https://aaronparecki.com/oauth-2-simplified/) ，比 [正式规范](https://oauth.net/2/)更易于遵循。 选项卡和 bot 的身份验证流略有不同，选项卡非常类似于网站，因此它们可以直接使用 OAuth 2.0，而 bot 不是，并且必须以不同的方式执行几项操作，但核心概念是相同的。

请参阅 GitHub 存储库 [Microsoft 团队身份验证示例](https://github.com/OfficeDev/microsoft-teams-sample-auth-node) ，该示例演示如何使用 Node.js 和 [OAuth 2.0 授权代码授予类型](https://oauth.net/2/grant-types/authorization-code/)演示 bot 的身份验证流。

![Bot 身份验证序列图](../../../assets/images/authentication/bot_auth_sequence_diagram.png)

1. 用户向 bot 发送一封邮件。
2. 机器人确定用户是否需要登录。
    * 在此示例中，机器人将访问令牌存储在其用户数据存储中。 如果没有为选定的标识提供程序验证令牌，则它要求用户登录。  ([查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76)) 
3. 机器人将 URL 构造到身份验证流的起始页，并将卡片发送给具有操作的用户 `signin` 。  ([查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190)) 
    * 与团队中的其他应用程序身份验证流一样，起始页必须位于列表中的域中 `validDomains` ，并且在与登录后重定向页面相同的域中。
    * **重要说明**： OAuth 2.0 授权代码授予对 `state` 身份验证请求中的参数的流调用，其中包含唯一会话令牌，以防止 [跨站点请求伪造攻击](https://en.wikipedia.org/wiki/Cross-site_request_forgery)。 该示例使用随机生成的 GUID。
4. 当用户选择 *登录* 按钮时，团队打开一个弹出窗口并导航到起始页。
> [!NOTE]
> 可以通过 URL 中的宽度和高度查询字符串参数控制弹出窗口的大小。 例如，如果您添加宽度 = 500 和 height = 500，则会看到一个500x500 像素的弹出窗口。 团队将显示具有给定像素大小的弹出窗口，最大值为主窗口大小的百分比。
5. 起始页将用户重定向到标识提供程序的 `authorize` 终结点。  ([查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56)) 
6. 在提供程序的网站上，用户登录并授予对机器人的访问权限。
7. 提供程序使用授权代码将用户带到 bot 的 OAuth 重定向页面。
8. Bot 兑现访问令牌的授权代码，并且 **临时** 会将令牌与启动登录流的用户相关联。 在下面，我们称之为 *临时令牌*。
    * 在此示例中，机器人将 `state` 参数值与启动登录进程的用户的 ID 关联，以便以后能够将其与 `state` 标识提供程序返回的值相匹配。  ([查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99)) 
    * **重要说明**：机器人存储从标识提供程序接收的令牌，并将其与特定用户相关联，但它被标记为 "挂起验证"。 临时令牌尚不能使用;必须进一步对其进行验证：
      1. **验证从标识提供程序收到的内容。** `state`必须根据先前保存的内容确认参数的值。 
      1. **验证从团队收到的内容。** 执行 [两步身份验证](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) 验证，以确保通过标识提供程序向 bot 授权的用户是与 bot 聊天的用户。 这将抵御 [中间人](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) 攻击和 [网络钓鱼](https://en.wikipedia.org/wiki/Phishing) 攻击。 机器人生成验证代码并存储它，与用户相关联。 由团队自动发送验证代码，如下所述。  ([查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113)) 
9. OAuth 回调将呈现一个调用的页面 `notifySuccess("<verification code>")` 。  ([查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs)) 
10. 团队关闭弹出窗口并将发送到的自动程序发送 `<verification code>` `notifySuccess()` 回机器人。 Bot 接收带有的 [调用](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) 邮件 `name = signin/verifyState` 。
11. Bot 将检查传入验证代码，以防止使用用户的临时令牌存储的验证代码。  ([查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140)) 
12. 如果匹配，则机器人标记令牌为已验证，可供使用。 否则，身份验证流将失败，并且 bot 会删除临时令牌。

> [!NOTE]
> 如果您在移动设备上进行身份验证时遇到问题，请确保您的 JavaScript SDK 已更新到版本1.4.1 或更高版本。

## <a name="samples"></a>示例

有关显示 bot 身份验证过程的示例代码，请参阅：

* [Microsoft 团队 bot 身份验证示例 ( # A0) ](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)

## <a name="more-details"></a>更多详细信息

有关针对 Azure AD 的 bot 身份验证的详细实施演练，请参阅：

* [向你的团队 bot 添加身份验证](add-authentication.md)
