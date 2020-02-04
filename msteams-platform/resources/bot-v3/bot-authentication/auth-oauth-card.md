---
title: 在团队中使用 Azure Bot 服务进行身份验证
description: 介绍了 Azure Bot 服务 OAuthCard 以及如何使用它进行身份验证
keywords: 团队身份验证 OAuthCard OAuth 卡 Azure Bot 服务
ms.openlocfilehash: 0397c45b39470d97c1158b2681462038de618a39
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673302"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a><span data-ttu-id="d7fa2-104">在团队中使用 Azure Bot 服务进行身份验证</span><span class="sxs-lookup"><span data-stu-id="d7fa2-104">Using Azure Bot Service for Authentication in Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="d7fa2-105">如果没有 Azure Bot 服务的 OAuthCard，则在 Bot 中实施身份验证非常复杂。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-105">Without the Azure Bot Service’s OAuthCard it is complicated to implement authentication in a bot.</span></span> <span data-ttu-id="d7fa2-106">它是一项全面的挑战，涉及构建 web 体验、与外部 OAuth 提供程序集成、令牌管理和处理正确的服务器到服务器 API 调用，以安全地完成身份验证流。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-106">It is a full-stack challenge that involving building a web experience, integrating with external OAuth providers, token management, and handling the right server-to-server API calls to complete authentication flow securely.</span></span> <span data-ttu-id="d7fa2-107">这可能会导致需要输入 "幻数" 的 clunky 体验。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-107">This can result in clunky experiences requiring the entry of “magic numbers”.</span></span>

<span data-ttu-id="d7fa2-108">借助 Azure Bot 服务的 OAuthCard，团队 Bot 可以更轻松地登录用户并访问外部数据提供程序。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-108">With Azure Bot Service’s OAuthCard, it is easier for your Teams bot to sign in your users and access external data providers.</span></span> <span data-ttu-id="d7fa2-109">无论您是否已实施身份验证，还是要切换到更简单的功能，或者如果您希望首次将身份验证添加到你的 bot 服务中，则 OAuthCard 可以更轻松地执行操作。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-109">Whether you’ve already implemented auth and you want to switch over to something simpler, or if you are looking to add authentication to your bot service for the first time, the OAuthCard can make it easier.</span></span>

<span data-ttu-id="d7fa2-110">[身份验证](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)中的其他主题在不使用 OAuthCard 的情况下描述身份验证。因此，如果您想要更深入地了解团队中的身份验证，或在不能使用 OAuthCard 的情况下，您仍可以参考这些主题。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-110">Other topics in [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) describe authentication without using the OAuthCard, so if you want to understand authentication in Teams more deeply, or have a situation where you can not use the OAuthCard, you can still refer to those topics.</span></span>

## <a name="support-for-the-oauthcard"></a><span data-ttu-id="d7fa2-111">对 OAuthCard 的支持</span><span class="sxs-lookup"><span data-stu-id="d7fa2-111">Support for the OAuthCard</span></span>

<span data-ttu-id="d7fa2-112">目前，您可以对 OAuthCard 使用某些限制。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-112">There are currently some restrictions to where you can use the OAuthCard.</span></span> <span data-ttu-id="d7fa2-113">具体包括：</span><span class="sxs-lookup"><span data-stu-id="d7fa2-113">These include:</span></span>

* <span data-ttu-id="d7fa2-114">该卡片将不能与[来宾访问](/MicrosoftTeams/guest-access)一起使用</span><span class="sxs-lookup"><span data-stu-id="d7fa2-114">The card will not work with [guest access](/MicrosoftTeams/guest-access)</span></span>
* <span data-ttu-id="d7fa2-115">它将不会在[Microsoft 团队中免费](https://products.office.com/microsoft-teams/free)使用</span><span class="sxs-lookup"><span data-stu-id="d7fa2-115">It will not work with [Microsoft Teams free](https://products.office.com/microsoft-teams/free)</span></span>
* <span data-ttu-id="d7fa2-116">它仅可用于 bot 身份验证</span><span class="sxs-lookup"><span data-stu-id="d7fa2-116">It can only be used for bot authentication</span></span>
* <span data-ttu-id="d7fa2-117">它仅适用于在[Azure Bot 服务](https://azure.microsoft.com/services/bot-service/)中注册的 bot</span><span class="sxs-lookup"><span data-stu-id="d7fa2-117">It only works for bots registered in the [Azure Bot Service](https://azure.microsoft.com/services/bot-service/)</span></span>

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a><span data-ttu-id="d7fa2-118">Azure Bot 服务如何帮助我进行身份验证？</span><span class="sxs-lookup"><span data-stu-id="d7fa2-118">How does the Azure Bot Service help me do authentication?</span></span>

<span data-ttu-id="d7fa2-119">主题中提供了使用 OAuthCard 的完整文档，主题：[通过 Azure Bot 服务向你的 Bot 添加身份验证](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0)。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-119">Full documentation using the OAuthCard is available in the topic: [Add authentication to your bot via Azure Bot Service](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0).</span></span> <span data-ttu-id="d7fa2-120">请注意，此主题位于 Azure Bot 框架文档集，而不是特定于团队。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-120">Note that this topic is in the Azure Bot Framework documentation set, and is not specific to Teams.</span></span>

<span data-ttu-id="d7fa2-121">以下各节介绍如何在团队中使用 OAuthCard。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-121">The following sections tell how to use the OAuthCard in Teams.</span></span>

## <a name="main-benefits-for-teams-developers"></a><span data-ttu-id="d7fa2-122">团队开发人员的主要好处</span><span class="sxs-lookup"><span data-stu-id="d7fa2-122">Main benefits for Teams developers</span></span>

<span data-ttu-id="d7fa2-123">OAuthCard 通过以下方式帮助进行身份验证：</span><span class="sxs-lookup"><span data-stu-id="d7fa2-123">The OAuthCard helps with authentication in the following ways:</span></span>

* <span data-ttu-id="d7fa2-124">提供现成的基于 web 的身份验证流：无需再编写和托管网页即可直接访问外部登录体验或提供重定向。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-124">Provides an out-of-box web-based authentication flow: you no longer have to write and host a web page to direct to external login experiences or provide a redirect.</span></span>
* <span data-ttu-id="d7fa2-125">对于最终用户是无缝的：在团队中完全填写完整的登录体验。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-125">Is seamless for end users: complete the full sign in experience right within Teams.</span></span>
* <span data-ttu-id="d7fa2-126">包括轻松令牌管理：您不必再实现令牌存储系统–即 Bot 服务负责令牌缓存，并提供用于提取这些令牌的安全机制。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-126">Includes easy token management: you no longer have to implement a token storage system – instead, the Bot Service takes care of token caching and provides a secure mechanism for fetching those tokens.</span></span>
* <span data-ttu-id="d7fa2-127">由完整的 Sdk 支持：易于集成和使用你的 bot 服务。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-127">Is supported by complete SDKs: easy to integrate and consume from your bot service.</span></span>
* <span data-ttu-id="d7fa2-128">提供了对许多常用 OAuth 提供程序的现成支持，如 Azure AD/MSA、Facebook 和 Google。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-128">Has out-of-box support for many popular OAuth providers, such as Azure AD/MSA, Facebook, and Google.</span></span>

## <a name="when-should-i-implement-my-own-solution"></a><span data-ttu-id="d7fa2-129">我应该何时实施自己的解决方案？</span><span class="sxs-lookup"><span data-stu-id="d7fa2-129">When should I implement my own solution?</span></span>

<span data-ttu-id="d7fa2-130">由于访问令牌是敏感信息，因此您可能不希望将它们存储在外部服务中。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-130">Because access tokens are sensitive information, you may not wish to have them stored in an external service.</span></span> <span data-ttu-id="d7fa2-131">在这种情况下，您可以选择仍实现您自己的令牌管理系统和团队中的登录体验，如其余的团队[身份验证](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)主题中所述。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-131">In this case, you may choose to still implement your own token management system and login experience within Teams, as described in the rest of the Teams [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) topics.</span></span>

## <a name="getting-started-with-oauthcard-in-teams"></a><span data-ttu-id="d7fa2-132">团队中的 OAuthCard 入门</span><span class="sxs-lookup"><span data-stu-id="d7fa2-132">Getting started with OAuthCard in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="d7fa2-133">本指南使用的是 Bot 框架 v3 SDK。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-133">This guide is using the Bot Framework v3 SDK.</span></span> <span data-ttu-id="d7fa2-134">你可以在[此处](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp)找到 v4 实现。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-134">You can find the v4 implementation [here](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp).</span></span> <span data-ttu-id="d7fa2-135">您仍需要创建一个清单并将 token.botframework.com 包括在`validDomains`部分中，因为否则 "登录" 按钮不会打开 "身份验证" 窗口。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-135">You will still need to create a manifest and include token.botframework.com in the `validDomains` section, because otherwise the Sign in button will not open the authentication window.</span></span> <span data-ttu-id="d7fa2-136">使用[应用程序 Studio](~/concepts/build-and-test/app-studio-overview.md)生成清单。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-136">Use the [App Studio](~/concepts/build-and-test/app-studio-overview.md) to generate your manifest.</span></span>

<span data-ttu-id="d7fa2-137">首先需要配置 Azure bot 服务以设置外部身份验证提供程序。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-137">You’ll first need to configure your Azure bot service to set up external authentication providers.</span></span> <span data-ttu-id="d7fa2-138">有关详细步骤，请阅读[配置标识提供程序](~/concepts/authentication/configure-identity-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-138">Read [Configuring identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps.</span></span>

<span data-ttu-id="d7fa2-139">若要使用 Azure Bot 服务启用身份验证，需要对代码进行以下添加：</span><span class="sxs-lookup"><span data-stu-id="d7fa2-139">To enable authentication using the Azure Bot Service, you need to make these additions to your code:</span></span>

1. <span data-ttu-id="d7fa2-140">在应用程序清单`validDomains`的部分中添加 token.botframework.com，因为团队将嵌入 Bot 服务的登录页。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-140">Include token.botframework.com in the `validDomains` section of your app manifest because Teams will embed the Bot Service’s login page.</span></span>
2. <span data-ttu-id="d7fa2-141">只要你的 bot 需要访问已通过身份验证的资源，即可从 Bot 服务中提取令牌。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-141">Fetch the token from the Bot Service whenever your bot needs to access authenticated resources.</span></span> <span data-ttu-id="d7fa2-142">如果没有可用的令牌，请将包含 OAuthCard 的邮件发送给请求他们登录外部服务的用户。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-142">If no token is available, send a message with an OAuthCard to the user requesting them to log into the external service.</span></span>
3. <span data-ttu-id="d7fa2-143">处理登录完成活动。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-143">Handle the login completion activity.</span></span> <span data-ttu-id="d7fa2-144">这将确保身份验证请求和令牌与当前与你的 bot 交互的用户相关联。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-144">This ensures that the authentication request and the token are associated with the user currently interacting with your bot.</span></span>
4. <span data-ttu-id="d7fa2-145">只要你的 bot 需要执行经过身份验证的操作（如调用外部 REST Api），即可检索令牌。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-145">Retrieve the token whenever your bot needs to perform authenticated actions, such as calling external REST APIs.</span></span>

<span data-ttu-id="d7fa2-146">在对话框代码中，您需要添加此代码段（c #），它将检查现有的访问令牌：</span><span class="sxs-lookup"><span data-stu-id="d7fa2-146">In your dialog code, you’ll need to add this snippet (C#), which checks for an existing access token:</span></span>

```CSharp
// First ask Bot Service if it already has a token for this user
var token = await context.GetUserTokenAsync(ConnectionName).ConfigureAwait(false);
if (token != null)
{
    // use the token to do exciting things!
}
else
{
    // If Bot Service does not have a token, send an OAuth card to sign in 
    await SendOAuthCardAsync(context, (Activity)context.Activity);
}
```

<span data-ttu-id="d7fa2-147">如果访问令牌不存在，则代码将向用户发送包含 OAuthCard 的邮件：</span><span class="sxs-lookup"><span data-stu-id="d7fa2-147">If an access token doesn’t exist, your code will then send a message with an OAuthCard to the user:</span></span>

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

<span data-ttu-id="d7fa2-148">若要处理 "登录完成" 活动，您需要处理此调用：</span><span class="sxs-lookup"><span data-stu-id="d7fa2-148">To handle the login complete activity, you’ll need to process this Invoke:</span></span>

```CSharp
if (activity.Name == "signin/verifyState")
{
  // We do this so that we can pass handling to the right logic in the dialog. You can
  // set this to be whatever string you want.
  activity.Text = "loginComplete";
  await Conversation.SendAsync(activity, () => new Dialogs.RootDialog());

  return Request.CreateResponse(HttpStatusCode.OK);
}
```

<span data-ttu-id="d7fa2-149">在对话框代码中，您可以从 Bot 身份验证服务中检索令牌：</span><span class="sxs-lookup"><span data-stu-id="d7fa2-149">In your dialog code, you can then retrieve the token from the Bot authentication service:</span></span>

```CSharp
if (text.Contains("loginComplete"))
  {
    // Handle login completion event.
    JObject ctx = activity.Value as JObject;

    if (ctx != null)
    {
      string code = ctx["state"].ToString();

      var oauthClient = activity.GetOAuthClient();
      var token = await oauthClient.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName, magicCode: code).ConfigureAwait(false);
      if (token != null)
      {
        // Make whatever API calls here you want
        await context.PostAsync($"Success! You are now signed in.");
      }
    }
  // Need to respond to the Invoke.
  return;
}
```

## <a name="using-oauthcard-with-messaging-extensions"></a><span data-ttu-id="d7fa2-150">结合使用 OAuthCard 和邮件扩展</span><span class="sxs-lookup"><span data-stu-id="d7fa2-150">Using OAuthCard with messaging extensions</span></span>

<span data-ttu-id="d7fa2-151">您还可以使用 Azure Bot 服务将第三方提供程序连接到您的邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-151">You can also use Azure Bot Service to connect third-party providers to your messaging extension.</span></span> <span data-ttu-id="d7fa2-152">流与 bot 相同，不同之处在于，服务将返回登录提示，而不是返回 OAuthCard。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-152">The flow is the same as with a bot, except instead of returning an OAuthCard, your service will return a login prompt.</span></span>

<span data-ttu-id="d7fa2-153">下面的代码段（c #）说明了如何创建登录响应：</span><span class="sxs-lookup"><span data-stu-id="d7fa2-153">The following snippet (C#) illustrates how to craft the login response:</span></span>

```CSharp
var token = await client.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName).ConfigureAwait(false);

if (token == null)
{
  // Send the login response with the auth link.
  string link = await client.OAuthApi.GetSignInLinkAsync(activity, ConnectionName);

  response = new ComposeExtensionResponse()
  {
    ComposeExtension = new ComposeExtensionResult()
  };
  response.ComposeExtension.Type = "auth";
  response.ComposeExtension.SuggestedActions = new ComposeExtensionSuggestedAction()
  {
    Actions = new List<CardAction>()
      {
        new CardAction(ActionTypes.OpenUrl, title: "Sign into this app", value: link)
      }
    };
  return response;
}
```

<span data-ttu-id="d7fa2-154">请注意，在上面的示例中，您需要对`GetSignInLinkAsync` `client.OAuthApi`属性直接调用。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-154">Note that in the example above you need to make the call to `GetSignInLinkAsync` directly against the `client.OAuthApi` property.</span></span>

<span data-ttu-id="d7fa2-155">当用户成功完成登录序列时，服务将接收另一个包含原始用户查询的调用请求，以及包含 "幻码" 的状态参数字符串。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-155">When the user successfully completes the login sequence, your service will receive another Invoke request containing the original user query, along with a state parameter string containing the “magic code”.</span></span> <span data-ttu-id="d7fa2-156">现在，您可以使用此字符串以及用户 ID 和连接名称提取令牌。</span><span class="sxs-lookup"><span data-stu-id="d7fa2-156">You can now fetch the token using this string, along with the user ID and connection name.</span></span>

```CSharp
var query = activity.GetComposeExtensionQueryData();
JObject data = activity.Value as JObject;

var client = activity.GetOAuthClient();

// Check if the request comes with login state
if (data != null && data["state"] != null)
{
  var token = await client.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName, data["state"].ToString());

  // Do stuff with the token here.

}
```
