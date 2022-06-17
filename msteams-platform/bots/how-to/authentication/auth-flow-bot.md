---
title: 机器人的 Microsoft Teams 身份验证流程
description: 在本模块中，了解如何在Microsoft Teams及其代码示例中为机器人执行身份验证流。
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: de263a75b7b8077570dca2f94bf6937d9d339bbe
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143233"
---
# <a name="authentication-flow-for-bots-in-microsoft-teams"></a>Microsoft Teams 中的机器人身份验证流程

OAuth 2.0 是 Azure Active Directory 和许多其他标识提供者用于身份验证和授权的开放标准。 基本了解 OAuth 2.0 是在 Teams 中使用身份验证的先决条件；[下面是一个很好的概述](https://aaronparecki.com/oauth-2-simplified/)，它比[正式规范](https://oauth.net/2/)更易于遵循。 选项卡和机器人的身份验证流略有不同 - 选项卡类似于网站，因此可以直接使用 OAuth 2.0，而机器人不是，必须以不同的方式执行一些操作，但核心概念是相同的。

有关使用 Node.js 和 [OAuth 2.0 授权代码授权类型](https://oauth.net/2/grant-types/authorization-code/)演示机器人身份验证流程的示例，请参阅 GitHub 存储库 [Microsoft Teams 身份验证示例](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs)。

![机器人身份验证序列图](../../../assets/images/authentication/bot_auth_sequence_diagram.png)

1. 用户向机器人发送消息。
2. 机器人确定用户是否需要登录。
   在此示例中，机器人将访问令牌存储在其用户数据存储中。 如果用户没有所选标识提供者的已验证令牌，它会要求用户登录。 （[查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76)）
3. 机器人将 URL 构造到身份验证流程的起始页，并使用 `signin` 操作将卡片发送给用户。 （[查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190)）</br>
    与 Teams 中的其他应用程序身份验证流程一样，起始页必须位于 `validDomains` 列表上的域中，并且与登录后重定向页面位于同一域中。
    > [!IMPORTANT]
    > OAuth 2.0 授权代码授予流程在身份验证请求中调用 `state` 参数，其包含唯一会话令牌，以防止[跨网站请求伪造攻击](https://en.wikipedia.org/wiki/Cross-site_request_forgery)。 该示例使用随机生成的 GUID。
4. 当用户选择“*登录*”按钮时，Teams 将打开一个弹出窗口并导航到起始页。
   > [!NOTE]
   > 可以通过 URL 中的宽度和高度查询字符串参数控制弹出窗口的大小。 例如，如果添加宽度 600 和宽度 600，则弹出窗口的大小为 600x600 像素。 弹出窗口的实际大小上限为 Teams 主窗口大小的百分比。 如果 Teams 窗口较小，则弹出窗口小于指定的尺寸。

5. 起始页将用户重定向到标识提供者的 `authorize` 终结点。 （[查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56)）
6. 在提供者的网站上，用户登录并授予对机器人的访问权限。
7. 提供者使用授权代码将用户转到机器人的 OAuth 重定向页面。
8. 机器人兑换访问令牌的授权代码，并 **临时** 将令牌与启动登录流程的用户关联。 下面，我们将其称为“*临时令牌*”。
    * 在该示例中，机器人将 `state` 参数的值与启动登录过程的用户的 ID 相关联，以便以后可以将其与标识提供者返回的 `state` 值匹配。 （[查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99)）
      > [!IMPORTANT]
      > 机器人存储它从标识提供者收到的令牌，并将其与特定用户关联，但令牌被标记为“等待验证”。
    * 如果不进一步验证，便无法使用临时令牌。
      1. **验证从标识提供者收到的内容。** 必须根据之前保存的内容来确认 `state` 参数的值。
      1. **验证从 Teams 收到的内容。** 执行[双重身份验证](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)，以确保使用标识提供者授权机器人的用户是与机器人聊天的同一用户。 这可以防止[中间人](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)和[网络钓鱼](https://en.wikipedia.org/wiki/Phishing)攻击。 机器人生成验证码并存储与用户关联的验证码。 验证码由 Teams 自动发送，如下所述。 （[查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113)）
9. OAuth 回调呈现调用 `notifySuccess("<verification code>")` 的页面。 （[查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs)）
10. Teams 关闭弹出窗口并将发送到 `notifySuccess()` 的 `<verification code>` 发送回机器人。 机器人收到带有 `name = signin/verifyState` 的 [invoke](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) 消息。
11. 机器人根据使用用户的临时令牌存储的验证码检查传入的验证码。 （[查看代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140)）
12. 如果匹配，机器人会将令牌标记为已验证并可供使用。 否则，身份验证流程失败，机器人会删除临时令牌。

    > [!NOTE]
    > 如果在移动设备上遇到身份验证问题，请确保 JavaScript SDK 已更新到版本 1.4.1 或更高版本。

## <a name="code-sample"></a>代码示例

显示机器人身份验证过程的示例代码：

| **示例名称** | **说明** | **Node.js** | **.NET** | **Python** |
|-----------------|----------------|--------------|----------|-----------|
| Teams 身份验证 | 此示例演示了 Microsoft Teams 应用中的身份验证。 | [View](https://github.com/OfficeDev/microsoft-teams-sample-auth-node) | | |
| 机器人身份验证 | 此示例演示如何对在 Microsoft Teams 中运行的机器人使用身份验证 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth)

## <a name="see-also"></a>另请参阅

[向 Teams 机器人添加身份验证](add-authentication.md)
