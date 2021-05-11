---
title: 使用证书的自动程序Azure Active Directory
description: 介绍 azure AD 身份验证Teams以及如何在机器人中使用它
keywords: teams 身份验证机器人 AAD
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: c3f2f7fe3eb6b10faef2b24b3212081a881d6f8f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020686"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a><span data-ttu-id="d04cc-104">在自动程序Microsoft Teams用户</span><span class="sxs-lookup"><span data-stu-id="d04cc-104">Authenticate a user in a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="d04cc-105">你可能希望在你的 Teams 应用中使用许多服务，其中大多数服务都需要进行身份验证和授权才能访问该服务。</span><span class="sxs-lookup"><span data-stu-id="d04cc-105">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="d04cc-106">服务包括 Facebook、Twitter 以及当然Teams。</span><span class="sxs-lookup"><span data-stu-id="d04cc-106">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="d04cc-107">用户Teams Microsoft Azure Active Directory (Azure AD) 中存储Graph。</span><span class="sxs-lookup"><span data-stu-id="d04cc-107">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph.</span></span> <span data-ttu-id="d04cc-108">本文将重点介绍使用 Azure AD 进行身份验证，以访问此信息。</span><span class="sxs-lookup"><span data-stu-id="d04cc-108">This article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="d04cc-109">OAuth 2.0 是 Azure AD 和许多其他服务提供商使用的身份验证的开放式标准。</span><span class="sxs-lookup"><span data-stu-id="d04cc-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="d04cc-110">了解 OAuth 2.0 是使用 Teams 和 Azure AD 中的身份验证的先决条件。</span><span class="sxs-lookup"><span data-stu-id="d04cc-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="d04cc-111">以下示例使用 OAuth 2.0 隐式授予流，目的是最终从 Azure AD 和 Microsoft Graph 中读取用户配置文件信息。</span><span class="sxs-lookup"><span data-stu-id="d04cc-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="d04cc-112">本文中介绍的身份验证流与选项卡的身份验证流非常相似，只是选项卡可以使用基于 Web 的身份验证流，而自动程序要求从代码驱动身份验证。</span><span class="sxs-lookup"><span data-stu-id="d04cc-112">The authentication flow described in this article is very similar to that of tabs except that tabs can use web based authentication flow, and bots require authentication to be driven from code.</span></span> <span data-ttu-id="d04cc-113">从移动平台实现身份验证时，本文中的概念也很有用。</span><span class="sxs-lookup"><span data-stu-id="d04cc-113">The concepts in this article will also be useful when implementing authentication from the mobile platform.</span></span>

<span data-ttu-id="d04cc-114">有关自动程序身份验证流的一般概述，请参阅主题 [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="d04cc-114">For a general overview of authentication flow for bots see the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="d04cc-115">配置标识提供程序</span><span class="sxs-lookup"><span data-stu-id="d04cc-115">Configuring identity providers</span></span>

<span data-ttu-id="d04cc-116">有关[将](~/concepts/authentication/configure-identity-provider.md)OAuth 2.0 回调重定向 URL 配置为标识提供程序 () 配置 OAuth 2.0 Azure Active Directory的详细信息，请参阅主题。</span><span class="sxs-lookup"><span data-stu-id="d04cc-116">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="d04cc-117">启动身份验证流</span><span class="sxs-lookup"><span data-stu-id="d04cc-117">Initiate authentication flow</span></span>

<span data-ttu-id="d04cc-118">身份验证流应该由用户操作触发。</span><span class="sxs-lookup"><span data-stu-id="d04cc-118">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="d04cc-119">不应自动打开身份验证弹出窗口，因为这可能会触发浏览器的弹出窗口阻止程序，并让用户混淆。</span><span class="sxs-lookup"><span data-stu-id="d04cc-119">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

## <a name="add-ui-to-start-authentication"></a><span data-ttu-id="d04cc-120">添加 UI 以开始身份验证</span><span class="sxs-lookup"><span data-stu-id="d04cc-120">Add UI to start authentication</span></span>

<span data-ttu-id="d04cc-121">将 UI 添加到自动程序，以便用户能够根据需要登录。</span><span class="sxs-lookup"><span data-stu-id="d04cc-121">Add UI to the bot to enable the user to sign in when needed.</span></span> <span data-ttu-id="d04cc-122">在此处，它通过"缩略图"卡片在 TypeScript 中完成：</span><span class="sxs-lookup"><span data-stu-id="d04cc-122">Here it is done from a Thumbnail card, in TypeScript:</span></span>

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

<span data-ttu-id="d04cc-123">三个按钮已添加到 Hero Card：登录、显示配置文件和注销。</span><span class="sxs-lookup"><span data-stu-id="d04cc-123">Three buttons have been added to the Hero Card: Sign in, Show Profile, and Sign out.</span></span>

## <a name="sign-the-user-in"></a><span data-ttu-id="d04cc-124">让用户登录</span><span class="sxs-lookup"><span data-stu-id="d04cc-124">Sign the user in</span></span>

<span data-ttu-id="d04cc-125">由于出于安全原因必须执行的验证和支持 Teams 的移动版本，代码未在此处显示，但下面是在用户按下"登录"按钮时启动该过程的代码示例[。](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195)</span><span class="sxs-lookup"><span data-stu-id="d04cc-125">Because of the validation that must be performed for security reasons and the support for the mobile versions of Teams, the code isn't shown here, but [here's an example of the code that kicks off the process when the user presses the Sign in button.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195).</span></span>

<span data-ttu-id="d04cc-126">验证和移动支持在主题 Bot [中的身份验证流中进行了介绍](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="d04cc-126">The validation and mobile support are explained in the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

<span data-ttu-id="d04cc-127">请务必将身份验证重定向 URL 的域添加到 [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) 清单的 部分。</span><span class="sxs-lookup"><span data-stu-id="d04cc-127">Be sure to add the domain of your authentication redirect URL to the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="d04cc-128">如果不显示，将不会显示登录弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="d04cc-128">If you don't, the login popup will not appear.</span></span>

## <a name="showing-user-profile-information"></a><span data-ttu-id="d04cc-129">显示用户配置文件信息</span><span class="sxs-lookup"><span data-stu-id="d04cc-129">Showing user profile information</span></span>

<span data-ttu-id="d04cc-130">尽管由于不同网站之间的所有转换以及必须解决的安全问题，获取访问令牌非常困难，但一旦拥有令牌，从网站Azure Active Directory非常简单。</span><span class="sxs-lookup"><span data-stu-id="d04cc-130">Although getting an access token is difficult because of all the transitions back and forth across different websites and the security issues that must be addressed, once you have a token, obtaining information from Azure Active Directory is straightforward.</span></span> <span data-ttu-id="d04cc-131">机器人使用访问令牌 `me` Graph访问终结点。</span><span class="sxs-lookup"><span data-stu-id="d04cc-131">The bot makes a call to the `me` Graph endpoint with the access token.</span></span> <span data-ttu-id="d04cc-132">Graph对登录人员的用户信息做出响应。</span><span class="sxs-lookup"><span data-stu-id="d04cc-132">Graph responds with the user information for the person who logged in.</span></span> <span data-ttu-id="d04cc-133">响应中的信息用于构建并发送自动程序卡。</span><span class="sxs-lookup"><span data-stu-id="d04cc-133">Information from the response is used to construct a bot card and sent.</span></span>

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

<span data-ttu-id="d04cc-134">如果用户未登录，系统会提示用户进行登录。</span><span class="sxs-lookup"><span data-stu-id="d04cc-134">If the user is not signed in they are prompted to do so.</span></span>

## <a name="sign-the-user-out"></a><span data-ttu-id="d04cc-135">注销用户</span><span class="sxs-lookup"><span data-stu-id="d04cc-135">Sign the user out</span></span>

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

## <a name="other-samples"></a><span data-ttu-id="d04cc-136">其他示例</span><span class="sxs-lookup"><span data-stu-id="d04cc-136">Other samples</span></span>

<span data-ttu-id="d04cc-137">有关显示自动程序身份验证过程的示例代码，请参阅：</span><span class="sxs-lookup"><span data-stu-id="d04cc-137">For sample code showing the bot authentication process see:</span></span>

* [<span data-ttu-id="d04cc-138">Microsoft Teams自动程序身份验证示例</span><span class="sxs-lookup"><span data-stu-id="d04cc-138">Microsoft Teams bot authentication sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
