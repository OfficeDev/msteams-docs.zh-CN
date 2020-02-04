---
title: 使用 Azure Active Directory 对 bot 进行身份验证
description: 介绍了团队中的 Azure AD 身份验证以及如何在你的 bot 中使用它
keywords: 团队身份验证 bot AAD
ms.date: 03/01/2018
ms.openlocfilehash: 268af02c51b21b65214bce4673b54ac564a125ae
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673301"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a>在 Microsoft 团队 bot 中对用户进行身份验证

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

您可能需要在团队应用程序中使用许多服务，这些服务中的大多数都需要身份验证和授权才能获取对服务的访问权限。 服务包括 Facebook、Twitter 和课程团队。 使用 Microsoft Graph，工作组用户拥有存储在 Azure Active Directory （Azure AD）中的用户配置文件信息。 本文重点介绍了如何使用 Azure AD 进行身份验证，以获取对此信息的访问权限。

OAuth 2.0 是一种开放的标准，用于 Azure AD 和许多其他服务提供商使用的身份验证。 了解 OAuth 2.0 是在团队和 Azure AD 中使用身份验证的先决条件。 下面的示例使用 OAuth 2.0 隐式授予流，其目标是最终从 Azure AD 和 Microsoft Graph 读取用户的配置文件信息。

本文中所述的身份验证流与选项卡的身份验证流非常相似，不同之处在于，选项卡可以使用基于 web 的身份验证流，并且 bot 需要通过代码驱动的身份验证。 在从移动平台实施身份验证时，本文中的概念也很有用。

有关 bot 身份验证流的一般概述，请参阅[bot 中的主题身份验证流](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)。

## <a name="configuring-identity-providers"></a>配置标识提供程序

有关在使用 Azure Active Directory 作为标识提供程序时配置 OAuth 2.0 回调重定向 URL 的详细步骤，请参阅主题[配置标识提供程序](~/concepts/authentication/configure-identity-provider.md)。

## <a name="initiate-authentication-flow"></a>启动身份验证流

应由用户操作触发身份验证流。 您不应自动打开身份验证弹出窗口，因为这可能会触发浏览器的弹出窗口阻止器，并将用户搞糊涂。

## <a name="add-ui-to-start-authentication"></a>添加 UI 以启动身份验证

向 bot 添加 UI 以使用户能够在需要时登录。 以下是在 TypeScript 中通过缩略图执行的操作：

```typescript
// Show prompt of options
protected async promptForAction(session: builder.Session): Promise<void> {
    let msg = new builder.Message(session)
        .addAttachment(new builder.ThumbnailCard(session)
            .title(this.providerDisplayName)
            .buttons([
                 builder.CardAction.messageBack(session, "{}", "Sign in")
                     .text("SignIn")
                     .displayText("Sign in"),
                  builder.CardAction.messageBack(session, "{}", "Show profile")
                     .text("ShowProfile")
                     .displayText("Show profile"),
                  builder.CardAction.messageBack(session, "{}", "Sign out")
                     .text("SignOut")
                     .displayText("Sign out"),
            ]));
    session.send(msg);
}
```

已向 "英雄卡片" 中添加了三个按钮：登录、显示配置文件和注销。

## <a name="sign-the-user-in"></a>在中为用户签名

由于出于安全原因和支持团队的移动版本而必须执行的验证，此处不显示代码，但[下面的示例展示了当用户按下 "登录" 按钮时](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195)，将启动进程的代码。。

在 bot 的主题[身份验证流](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)中对验证和移动支持进行了说明。

请务必将身份验证重定向 URL 的域添加到清单[`validDomains`](~/resources/schema/manifest-schema.md#validdomains)部分。 如果不这样做，则不会显示登录弹出窗口。

## <a name="showing-user-profile-information"></a>显示用户配置文件信息

尽管获取访问令牌很困难，因为在不同的网站之间来回切换以及必须解决的安全问题，一旦您拥有令牌，从 Azure Active Directory 获取信息非常简单。 Bot 使用访问令牌调用`me` Graph 终结点。 Graph 将响应登录用户的用户信息。 响应中的信息用于构造 bot 卡并发送。

```typescript
// Show user profile
protected async showUserProfile(session: builder.Session): Promise<void> {
    let azureADApi = this.authProvider as AzureADv1Provider;
    let userToken = this.getUserToken(session);

    if (userToken) {
        let profile = await azureADApi.getProfileAsync(userToken.accessToken);
        let profileCard = new builder.ThumbnailCard()
            .title(profile.displayName)
            .subtitle(profile.mail)
            .text(`${profile.jobTitle}<br/> ${profile.officeLocation}`);
        session.send(new builder.Message().addAttachment(profileCard));
    } else {
        session.send("Please sign in to AzureAD so I can access your profile.");
    }

    await this.promptForAction(session);
}

// Helper function to make the Graph API call
public async getProfileAsync(accessToken: string): Promise<any> {
    let options = {
        url: "https://graph.microsoft.com/v1.0/me",
        json: true,
        headers: {
            "Authorization": `Bearer ${accessToken}`,
        },
    };
    return await request.get(options);
}
```

如果用户未登录，则系统会提示他们执行此操作。

## <a name="sign-the-user-out"></a>注销用户

```typescript
// Handle user logout request
private async handleLogout(session: builder.Session): Promise<void> {
    if (!utils.getUserToken(session, this.providerName)) {
        session.send(`You're already signed out of ${this.providerDisplayName}.`);
    } else {
        utils.setUserToken(session, this.providerName, null);
        session.send(`You're now signed out of ${this.providerDisplayName}.`);
    }

    await this.promptForAction(session);
}
```

## <a name="other-samples"></a>其他示例

有关显示 bot 身份验证过程的示例代码，请参阅：

* [Microsoft 团队 bot 身份验证示例](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
