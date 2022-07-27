---
title: 使用 Azure Active Directory 对机器人进行身份验证
description: 介绍 Teams 中的 Azure AD 身份验证以及如何在机器人中使用它
keywords: teams 身份验证机器人 Azure AD
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: 2b467f6a7b4678110dece3b54a67227df6beeaf7
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035161"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a>在 Microsoft Teams 机器人中对用户进行身份验证

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

你可能想要在 Teams 应用中使用许多服务，其中大多数服务都需要身份验证和授权才能获取访问权限。 这些服务包括 Facebook、Twitter 和 Teams。 Teams 中的用户具有使用 Microsoft Graph 存储在 Azure Active Directory 中的用户配置文件信息。 本主题重点介绍如何使用 Azure AD 进行身份验证以获取访问权限。
OAuth 2.0 是 Azure AD 和许多其他服务提供商使用的身份验证开放标准。 了解 OAuth 2.0 是在 Teams 和 Azure AD 中使用身份验证的先决条件。 以下示例使用 OAuth 2.0 隐式授予流最终从 Azure AD 和 Microsoft Graph 读取用户的个人资料信息。

本主题中描述的身份验证流类似于选项卡，但选项卡可以使用基于 Web 的身份验证流，机器人需要从代码驱动身份验证。 从移动平台实现身份验证时，本主题中的概念也很有用。

有关机器人身份验证流的一般概述，请参阅 [机器人中的身份验证流](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)主题。

## <a name="configuring-identity-providers"></a>配置身份提供程序

有关在将 Azure Active Directory 用作标 [识提供者](~/concepts/authentication/configure-identity-provider.md) 时配置 OAuth 2.0 回调重定向 URL () 的详细步骤，请参阅主题“配置标识提供者”。

## <a name="initiate-authentication-flow"></a>启动身份验证流

身份验证流应由用户操作触发。 不要自动打开身份验证弹出窗口，因为它可能会触发浏览器的弹出窗口阻止程序并混淆用户。

## <a name="add-ui-to-start-authentication"></a>添加 UI 以开始身份验证

将 UI 添加到机器人，使用户能够在需要时登录。 下面是通过缩略图卡在 TypeScript 中完成的：

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

英雄卡片中添加了三个按钮：登录、显示配置文件和注销。

## <a name="sign-the-user-in"></a>将用户登录

由于出于安全原因和对 Teams 移动版本的支持而必须执行的验证，此处未显示代码，但 [下面是用户按下“登录”按钮时启动过程的代码示例](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195)。

验证和移动支持在 [机器人中的身份验证流主题中](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)进行了说明。

请务必将身份验证的域重定向 URL 添加到 [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) 清单部分。 如果不登录，则不会显示弹出窗口。

## <a name="showing-user-profile-information"></a>显示用户配置文件信息

虽然获取访问令牌是很困难的，因为在不同的网站之间来回转换以及必须解决的安全问题，一旦有了令牌，从 Azure Active Directory 获取信息就很简单了。 机器人使用访问令牌调 `me` 用 Graph 终结点。 Graph 使用登录者的用户信息进行响应。 响应中的信息用于构造机器人卡并发送。

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

如果用户未登录，系统会提示用户登录。

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

有关显示机器人身份验证过程的示例代码，请参阅：

* [Microsoft Teams 机器人身份验证示例](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
