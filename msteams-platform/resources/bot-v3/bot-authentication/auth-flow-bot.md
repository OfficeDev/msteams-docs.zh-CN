---
title: 机器人的身份验证流
description: 介绍机器人中的身份验证流
keywords: Teams, 身份验证流程, 机器人
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: 4930edcef81fca60f45ecdfd9bab863eb4524753
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757204"
---
# <a name="microsoft-teams-authentication-flow-for-bots"></a>Microsoft Teams机器人的身份验证流

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

OAuth 2.0 是 Azure AD 和许多其他标识提供者用于身份验证和授权的开放标准。 基本了解 OAuth 2.0 是在 Teams 中使用身份验证的先决条件；[下面是一个很好的概述](https://aaronparecki.com/oauth-2-simplified/)，它比[正式规范](https://oauth.net/2/)更易于遵循。 选项卡和机器人的身份验证流不同，因为选项卡类似于网站，因此它们可以直接使用 OAuth 2.0，机器人不是而且必须以不同的方式执行一些操作，但核心概念是相同的。

有关使用 [OAuth 2.0 授权代码授予类型的](https://oauth.net/2/grant-types/authorization-code/)节点演示机器人身份验证流的示例，请参阅GitHub存储库[Microsoft Teams身份验证示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)例。

![机器人身份验证序列图](~/assets/images/authentication/bot_auth_sequence_diagram.png)

1. 用户向机器人发送消息。
2. 机器人确定用户是否需要登录。
    * 在此示例中，机器人将访问令牌存储在其用户数据存储中。 它要求用户登录，如果它没有所选标识提供者的已验证令牌。 （[查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76)）
3. 机器人将 URL 构造到身份验证流程的起始页，并使用 `signin` 操作将卡片发送给用户。 （[查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190)）
    * 与Teams中的其他应用程序身份验证流一样，起始页必须位于列表中的`validDomains`域和与帖子登录重定向页相同的域上。
    * **重要** 提示：OAuth 2.0 授权代码授予流在身份验证请求中调 `state` 用参数，该参数包含唯一会话令牌以防止 [跨站点请求伪造攻击](https://en.wikipedia.org/wiki/Cross-site_request_forgery)。 该示例使用随机生成的 GUID。
4. 当用户选择 *登录* 按钮时，Teams打开一个弹出窗口并将其导航到起始页。
5. 起始页将用户重定向到标识提供者的 `authorize` 终结点。 （[查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56)）
6. 在提供者的网站上，用户登录并授予对机器人的访问权限。
7. 提供程序使用授权代码将用户带到机器人的 OAuth 重定向页面。
8. 机器人兑换访问令牌的授权代码，并 **临时** 将令牌与启动登录流程的用户关联。 下面，我们将其称为“*临时令牌*”。
    * 在该示例中，机器人将参数的 `state` 值与启动登录过程的用户的 ID 相关联，以便以后可以将其与 `state` 标识提供者返回的值匹配。 （[查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99)）
    * **重要** 提示：机器人存储它从标识提供者接收的令牌，并将其与特定用户关联，但标记为“挂起的验证”。 暂时令牌尚不能使用：必须进一步验证：
      1. **验证从标识提供者收到的内容。** 必须根据之前保存的内容来确认 `state` 参数的值。
      1. **验证从 Teams 收到的内容。** 执行[双重身份验证](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)，以确保使用标识提供者授权机器人的用户是与机器人聊天的同一用户。 这可以防止[中间人](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)和[网络钓鱼](https://en.wikipedia.org/wiki/Phishing)攻击。 机器人生成验证码并存储与用户关联的验证码。 验证码由以下步骤 9 和 10 中所述的Teams自动发送。 （[查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113)）
9. OAuth 回调呈现调用 `notifySuccess("<verification code>")` 的页面。 （[查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs)）
10. Teams关闭弹出窗口并将`<verification code>`发送回`notifySuccess()`机器人。 机器人收到带有 `name = signin/verifyState` 的 [invoke](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) 消息。
11. 机器人根据使用用户的临时令牌存储的验证码检查传入的验证码。 （[查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140)）
12. 如果匹配，机器人会将令牌标记为已验证并可供使用。 否则，身份验证流程失败，机器人会删除临时令牌。

> [!Note]
> 如果在移动设备上遇到身份验证问题，请确保 Javascript SDK 已更新到版本 1.4.1 或更高版本。

## <a name="samples"></a>示例

有关显示机器人身份验证过程的示例代码，请参阅：

* [Microsoft Teams节点)  (机器人身份验证示例](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)

## <a name="more-details"></a>更多详细信息

有关针对Azure Active Directory的机器人身份验证的详细实现演练，请参阅：

* [在 Microsoft Teams 机器人中对用户进行身份验证](~/resources/bot-v3/bot-authentication/auth-bot-AAD.md)
