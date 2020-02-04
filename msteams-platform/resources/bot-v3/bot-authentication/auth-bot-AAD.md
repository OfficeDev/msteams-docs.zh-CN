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
# <a name="authenticate-a-user-in-a-microsoft-teams-bot"></a><span data-ttu-id="e18cb-104">在 Microsoft 团队 bot 中对用户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="e18cb-104">Authenticate a user in a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="e18cb-105">您可能需要在团队应用程序中使用许多服务，这些服务中的大多数都需要身份验证和授权才能获取对服务的访问权限。</span><span class="sxs-lookup"><span data-stu-id="e18cb-105">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="e18cb-106">服务包括 Facebook、Twitter 和课程团队。</span><span class="sxs-lookup"><span data-stu-id="e18cb-106">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="e18cb-107">使用 Microsoft Graph，工作组用户拥有存储在 Azure Active Directory （Azure AD）中的用户配置文件信息。</span><span class="sxs-lookup"><span data-stu-id="e18cb-107">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph.</span></span> <span data-ttu-id="e18cb-108">本文重点介绍了如何使用 Azure AD 进行身份验证，以获取对此信息的访问权限。</span><span class="sxs-lookup"><span data-stu-id="e18cb-108">This article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="e18cb-109">OAuth 2.0 是一种开放的标准，用于 Azure AD 和许多其他服务提供商使用的身份验证。</span><span class="sxs-lookup"><span data-stu-id="e18cb-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="e18cb-110">了解 OAuth 2.0 是在团队和 Azure AD 中使用身份验证的先决条件。</span><span class="sxs-lookup"><span data-stu-id="e18cb-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="e18cb-111">下面的示例使用 OAuth 2.0 隐式授予流，其目标是最终从 Azure AD 和 Microsoft Graph 读取用户的配置文件信息。</span><span class="sxs-lookup"><span data-stu-id="e18cb-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="e18cb-112">本文中所述的身份验证流与选项卡的身份验证流非常相似，不同之处在于，选项卡可以使用基于 web 的身份验证流，并且 bot 需要通过代码驱动的身份验证。</span><span class="sxs-lookup"><span data-stu-id="e18cb-112">The authentication flow described in this article is very similar to that of tabs except that tabs can use web based authentication flow, and bots require authentication to be driven from code.</span></span> <span data-ttu-id="e18cb-113">在从移动平台实施身份验证时，本文中的概念也很有用。</span><span class="sxs-lookup"><span data-stu-id="e18cb-113">The concepts in this article will also be useful when implementing authentication from the mobile platform.</span></span>

<span data-ttu-id="e18cb-114">有关 bot 身份验证流的一般概述，请参阅[bot 中的主题身份验证流](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="e18cb-114">For a general overview of authentication flow for bots see the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="e18cb-115">配置标识提供程序</span><span class="sxs-lookup"><span data-stu-id="e18cb-115">Configuring identity providers</span></span>

<span data-ttu-id="e18cb-116">有关在使用 Azure Active Directory 作为标识提供程序时配置 OAuth 2.0 回调重定向 URL 的详细步骤，请参阅主题[配置标识提供程序](~/concepts/authentication/configure-identity-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="e18cb-116">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="e18cb-117">启动身份验证流</span><span class="sxs-lookup"><span data-stu-id="e18cb-117">Initiate authentication flow</span></span>

<span data-ttu-id="e18cb-118">应由用户操作触发身份验证流。</span><span class="sxs-lookup"><span data-stu-id="e18cb-118">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="e18cb-119">您不应自动打开身份验证弹出窗口，因为这可能会触发浏览器的弹出窗口阻止器，并将用户搞糊涂。</span><span class="sxs-lookup"><span data-stu-id="e18cb-119">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

## <a name="add-ui-to-start-authentication"></a><span data-ttu-id="e18cb-120">添加 UI 以启动身份验证</span><span class="sxs-lookup"><span data-stu-id="e18cb-120">Add UI to start authentication</span></span>

<span data-ttu-id="e18cb-121">向 bot 添加 UI 以使用户能够在需要时登录。</span><span class="sxs-lookup"><span data-stu-id="e18cb-121">Add UI to the bot to enable the user to sign in when needed.</span></span> <span data-ttu-id="e18cb-122">以下是在 TypeScript 中通过缩略图执行的操作：</span><span class="sxs-lookup"><span data-stu-id="e18cb-122">Here it is done from a Thumbnail card, in TypeScript:</span></span>

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

<span data-ttu-id="e18cb-123">已向 "英雄卡片" 中添加了三个按钮：登录、显示配置文件和注销。</span><span class="sxs-lookup"><span data-stu-id="e18cb-123">Three buttons have been added to the Hero Card: Sign in, Show Profile, and Sign out.</span></span>

## <a name="sign-the-user-in"></a><span data-ttu-id="e18cb-124">在中为用户签名</span><span class="sxs-lookup"><span data-stu-id="e18cb-124">Sign the user in</span></span>

<span data-ttu-id="e18cb-125">由于出于安全原因和支持团队的移动版本而必须执行的验证，此处不显示代码，但[下面的示例展示了当用户按下 "登录" 按钮时](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195)，将启动进程的代码。。</span><span class="sxs-lookup"><span data-stu-id="e18cb-125">Because of the validation that must be performed for security reasons and the support for the mobile versions of Teams, the code isn't shown here, but [here's an example of the code that kicks off the process when the user presses the Sign in button.](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/e84020562d7c8b83f4a357a4a4d91298c5d2989d/src/dialogs/BaseIdentityDialog.ts#L154-L195).</span></span>

<span data-ttu-id="e18cb-126">在 bot 的主题[身份验证流](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)中对验证和移动支持进行了说明。</span><span class="sxs-lookup"><span data-stu-id="e18cb-126">The validation and mobile support are explained in the topic [Authentication flow in bots](~/resources/bot-v3/bot-authentication/auth-flow-bot.md).</span></span>

<span data-ttu-id="e18cb-127">请务必将身份验证重定向 URL 的域添加到清单[`validDomains`](~/resources/schema/manifest-schema.md#validdomains)部分。</span><span class="sxs-lookup"><span data-stu-id="e18cb-127">Be sure to add the domain of your authentication redirect URL to the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="e18cb-128">如果不这样做，则不会显示登录弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="e18cb-128">If you don't, the login popup will not appear.</span></span>

## <a name="showing-user-profile-information"></a><span data-ttu-id="e18cb-129">显示用户配置文件信息</span><span class="sxs-lookup"><span data-stu-id="e18cb-129">Showing user profile information</span></span>

<span data-ttu-id="e18cb-130">尽管获取访问令牌很困难，因为在不同的网站之间来回切换以及必须解决的安全问题，一旦您拥有令牌，从 Azure Active Directory 获取信息非常简单。</span><span class="sxs-lookup"><span data-stu-id="e18cb-130">Although getting an access token is difficult because of all the transitions back and forth across different websites and the security issues that must be addressed, once you have a token, obtaining information from Azure Active Directory is straightforward.</span></span> <span data-ttu-id="e18cb-131">Bot 使用访问令牌调用`me` Graph 终结点。</span><span class="sxs-lookup"><span data-stu-id="e18cb-131">The bot makes a call to the `me` Graph endpoint with the access token.</span></span> <span data-ttu-id="e18cb-132">Graph 将响应登录用户的用户信息。</span><span class="sxs-lookup"><span data-stu-id="e18cb-132">Graph responds with the user information for the person who logged in.</span></span> <span data-ttu-id="e18cb-133">响应中的信息用于构造 bot 卡并发送。</span><span class="sxs-lookup"><span data-stu-id="e18cb-133">Information from the response is used to construct a bot card and sent.</span></span>

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

<span data-ttu-id="e18cb-134">如果用户未登录，则系统会提示他们执行此操作。</span><span class="sxs-lookup"><span data-stu-id="e18cb-134">If the user is not signed in they are prompted to do so.</span></span>

## <a name="sign-the-user-out"></a><span data-ttu-id="e18cb-135">注销用户</span><span class="sxs-lookup"><span data-stu-id="e18cb-135">Sign the user out</span></span>

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

## <a name="other-samples"></a><span data-ttu-id="e18cb-136">其他示例</span><span class="sxs-lookup"><span data-stu-id="e18cb-136">Other samples</span></span>

<span data-ttu-id="e18cb-137">有关显示 bot 身份验证过程的示例代码，请参阅：</span><span class="sxs-lookup"><span data-stu-id="e18cb-137">For sample code showing the bot authentication process see:</span></span>

* [<span data-ttu-id="e18cb-138">Microsoft 团队 bot 身份验证示例</span><span class="sxs-lookup"><span data-stu-id="e18cb-138">Microsoft Teams bot authentication sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
