---
title: Microsoft Teams自动程序身份验证流
description: 介绍Microsoft Teams代码示例的自动程序中的身份验证流。
keywords: teams 身份验证流自动程序
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: 30e7817ba72dbca50852b91b4c5791f8ece1a36a
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453024"
---
# <a name="authentication-flow-for-bots-in-microsoft-teams"></a>聊天机器人的身份验证Microsoft Teams

OAuth 2.0 是一种开放标准，用于身份验证和授权，Azure Active Directory提供程序使用。 对 OAuth 2.0 有基本的了解是在身份验证中Teams;[下面是比正式](https://aaronparecki.com/oauth-2-simplified/)规范更易于遵循的一个很好的[概述](https://oauth.net/2/)。 选项卡和聊天机器人的身份验证流有一点不同 ：选项卡与网站非常相似，因此可以直接使用 OAuth 2.0，而机器人不会并且必须执行一些不同操作，但核心概念是相同的。

有关演示GitHub [Microsoft Teams](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs)和 [OAuth 2.0](https://oauth.net/2/grant-types/authorization-code/) 授权代码授予类型的Node.js自动程序身份验证流的示例，请参阅 GitHub 存储库和身份验证示例。

![自动程序身份验证序列图](../../../assets/images/authentication/bot_auth_sequence_diagram.png)

1. 用户向自动程序发送消息。
2. 自动程序确定用户是否需要登录。
   本示例中，自动程序将访问令牌存储在其用户数据存储中。 如果所选标识提供程序没有经过验证的令牌，它会要求用户登录。  ([视图代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76)) 
3. 机器人构建身份验证流起始页的 URL，然后通过操作向用户发送卡片 `signin` 。  ([视图代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190)) </br>
    与应用程序中的Teams`validDomains`一样，起始页必须位于列表上的域中，并且与登录后重定向页位于同一域中。
    > [!IMPORTANT]
    > OAuth 2.0 `state` 授权代码授予对身份验证请求中参数的流调用，其中包含用于防止跨站点请求伪造攻击的唯一会话 [令牌](https://en.wikipedia.org/wiki/Cross-site_request_forgery)。 此示例使用随机生成的 GUID。
4. 当用户选择登录按钮时，Teams打开一个弹出窗口并导航到起始页。
   > [!NOTE]
   > 弹出窗口的大小可以通过 URL 中的 width 和 height 查询字符串参数进行控制。 例如，如果添加 width=600 和 height=600，则弹出窗口的大小为 600x600 像素。 弹出窗口的实际大小以主窗口大小的百Teams百分比表示。 如果Teams窗口较小，则弹出窗口小于指定的尺寸。

5. 起始页将用户重定向到标识提供程序的终结点 `authorize` 。  ([视图代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56)) 
6. 在提供商的网站上，用户登录并授予对机器人的访问权限。
7. 提供程序会使用授权代码将用户定向到机器人的 OAuth 重定向页面。
8. 自动程序兑换授权代码获取访问令牌，并临时将令牌与启动登录流程的用户关联。 下面我们将此令牌称为 *临时令牌*。
    * 在示例中 `state` ，自动程序将参数值与启动登录过程的用户的 ID `state` 关联，以便以后可以与标识提供程序返回的值匹配。  ([视图代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99)) 
      > [!IMPORTANT]
      > 自动程序存储从标识提供程序收到的令牌，并关联到特定用户，但标记为"待验证"。
    * 临时令牌如果不进一步验证，则不能使用。
      1. **验证从标识提供程序接收的信息。** 必须针对 `state` 之前保存的值确认参数的值。
      1. **验证接收自Teams。** 执行 [两步](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) 身份验证验证以确保通过标识提供程序授权自动程序的用户是正在与机器人聊天的同一用户。 这可[抵御中间人和网络钓鱼](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)[攻击。](https://en.wikipedia.org/wiki/Phishing) 机器人生成验证码，并存储与用户关联的验证码。 验证码由用户自动发送Teams如下所述。  ([视图代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113)) 
9. OAuth 回调呈现调用 的页面 `notifySuccess("<verification code>")`。  ([视图代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs)) 
10. Teams关闭弹出窗口，并将 发送`<verification code>``notifySuccess()`回自动程序。 机器人通过 接收 [调用](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) 消息 `name = signin/verifyState`。
11. 自动程序根据使用用户临时令牌存储的验证码检查传入验证码。  ([视图代码](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140)) 
12. 如果匹配，则自动程序将令牌标记为已验证并可供使用。 否则，身份验证流将失败，自动程序会删除临时令牌。

    > [!NOTE]
    > 如果你在移动设备上遇到身份验证问题，请确保 JavaScript SDK 已更新到版本 1.4.1 或更高版本。

## <a name="code-sample"></a>代码示例

显示自动程序身份验证过程的示例代码：

| **示例名称** | **说明** | **Node.js** | **.NET** | **Python** |
|-----------------|----------------|--------------|----------|-----------|
| Teams身份验证 | 此示例演示了Microsoft Teams身份验证。 | [View](https://github.com/OfficeDev/microsoft-teams-sample-auth-node) | | |
| 自动程序身份验证 | 此示例演示如何对在 Microsoft Teams 中运行的自动程序使用身份验证 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth)

## <a name="see-also"></a>另请参阅

[向 Teams 机器人添加身份验证](add-authentication.md)
