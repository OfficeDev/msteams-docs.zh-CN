---
title: 在 Teams 中将 Azure Bot 服务用于身份验证
description: 介绍 Azure Bot Service OAuthCard 及其用于身份验证方式
ms.topic: conceptual
localization_priority: Normal
keywords: teams 身份验证 OAuthCard OAuth 卡 Azure Bot 服务
ms.openlocfilehash: 3d0df4f04625c5be3468d12319b54096ae06de90
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020679"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a><span data-ttu-id="f383f-104">在 Teams 中将 Azure Bot 服务用于身份验证</span><span class="sxs-lookup"><span data-stu-id="f383f-104">Using Azure Bot Service for Authentication in Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="f383f-105">如果没有 Azure Bot Service 的 OAuthCard，在自动程序中实现身份验证会很复杂。</span><span class="sxs-lookup"><span data-stu-id="f383f-105">Without the Azure Bot Service’s OAuthCard it is complicated to implement authentication in a bot.</span></span> <span data-ttu-id="f383f-106">这是一个全堆栈挑战，涉及构建 Web 体验、与外部 OAuth 提供程序集成、令牌管理，以及处理正确的服务器到服务器 API 调用以安全完成身份验证流。</span><span class="sxs-lookup"><span data-stu-id="f383f-106">It is a full-stack challenge that involving building a web experience, integrating with external OAuth providers, token management, and handling the right server-to-server API calls to complete authentication flow securely.</span></span> <span data-ttu-id="f383f-107">这可能会导致需要输入"神奇数字"的奇怪体验。</span><span class="sxs-lookup"><span data-stu-id="f383f-107">This can result in clunky experiences requiring the entry of “magic numbers”.</span></span>

<span data-ttu-id="f383f-108">借助 Azure Bot Service 的 OAuthCard，Teams 自动程序可以更轻松地登录用户和访问外部数据提供程序。</span><span class="sxs-lookup"><span data-stu-id="f383f-108">With Azure Bot Service’s OAuthCard, it is easier for your Teams bot to sign in your users and access external data providers.</span></span> <span data-ttu-id="f383f-109">无论你是否已实现身份验证并且想要切换到更简单的方法，或者如果你希望首次向自动程序服务添加身份验证，OAuthCard 都可以简化操作。</span><span class="sxs-lookup"><span data-stu-id="f383f-109">Whether you’ve already implemented auth and you want to switch over to something simpler, or if you are looking to add authentication to your bot service for the first time, the OAuthCard can make it easier.</span></span>

<span data-ttu-id="f383f-110">身份验证中的其他[](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)主题介绍不使用 OAuthCard 的身份验证，因此如果你想要更加深入地了解 Teams 中的身份验证，或者你无法使用 OAuthCard，你仍然可以参考这些主题。</span><span class="sxs-lookup"><span data-stu-id="f383f-110">Other topics in [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) describe authentication without using the OAuthCard, so if you want to understand authentication in Teams more deeply, or have a situation where you can not use the OAuthCard, you can still refer to those topics.</span></span>

## <a name="support-for-the-oauthcard"></a><span data-ttu-id="f383f-111">对 OAuthCard 的支持</span><span class="sxs-lookup"><span data-stu-id="f383f-111">Support for the OAuthCard</span></span>

<span data-ttu-id="f383f-112">目前，对 OAuthCard 的使用位置存在一些限制。</span><span class="sxs-lookup"><span data-stu-id="f383f-112">There are currently some restrictions to where you can use the OAuthCard.</span></span> <span data-ttu-id="f383f-113">具体包括：</span><span class="sxs-lookup"><span data-stu-id="f383f-113">These include:</span></span>

* <span data-ttu-id="f383f-114">该卡不能与来宾 [访问一起使用](/MicrosoftTeams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="f383f-114">The card will not work with [guest access](/MicrosoftTeams/guest-access)</span></span>
* <span data-ttu-id="f383f-115">它不能免费与 [Microsoft Teams 一起使用](https://products.office.com/microsoft-teams/free)</span><span class="sxs-lookup"><span data-stu-id="f383f-115">It will not work with [Microsoft Teams free](https://products.office.com/microsoft-teams/free)</span></span>
* <span data-ttu-id="f383f-116">它只能用于自动程序身份验证</span><span class="sxs-lookup"><span data-stu-id="f383f-116">It can only be used for bot authentication</span></span>
* <span data-ttu-id="f383f-117">它仅适用于在 Azure Bot 服务 [中注册的机器人](https://azure.microsoft.com/services/bot-service/)</span><span class="sxs-lookup"><span data-stu-id="f383f-117">It only works for bots registered in the [Azure Bot Service](https://azure.microsoft.com/services/bot-service/)</span></span>

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a><span data-ttu-id="f383f-118">Azure 自动程序服务如何协助我进行身份验证？</span><span class="sxs-lookup"><span data-stu-id="f383f-118">How does the Azure Bot Service help me do authentication?</span></span>

<span data-ttu-id="f383f-119">有关使用 OAuthCard 的完整文档，请参阅主题：通过 Azure Bot 服务向自动 [程序添加身份验证](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="f383f-119">Full documentation using the OAuthCard is available in the topic: [Add authentication to your bot via Azure Bot Service](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true).</span></span> <span data-ttu-id="f383f-120">请注意，本主题位于 Azure Bot Framework 文档集内，并不特定于 Teams。</span><span class="sxs-lookup"><span data-stu-id="f383f-120">Note that this topic is in the Azure Bot Framework documentation set, and is not specific to Teams.</span></span>

<span data-ttu-id="f383f-121">以下各节将告知如何在 Teams 中使用 OAuthCard。</span><span class="sxs-lookup"><span data-stu-id="f383f-121">The following sections tell how to use the OAuthCard in Teams.</span></span>

## <a name="main-benefits-for-teams-developers"></a><span data-ttu-id="f383f-122">Teams 开发人员的主要好处</span><span class="sxs-lookup"><span data-stu-id="f383f-122">Main benefits for Teams developers</span></span>

<span data-ttu-id="f383f-123">OAuthCard 通过以下方式帮助进行身份验证：</span><span class="sxs-lookup"><span data-stu-id="f383f-123">The OAuthCard helps with authentication in the following ways:</span></span>

* <span data-ttu-id="f383f-124">提供基于 Web 的开箱即用身份验证流：无需再编写和托管网页来定向外部登录体验或提供重定向。</span><span class="sxs-lookup"><span data-stu-id="f383f-124">Provides an out-of-box web-based authentication flow: you no longer have to write and host a web page to direct to external login experiences or provide a redirect.</span></span>
* <span data-ttu-id="f383f-125">对于最终用户是无缝的：在 Teams 中完成完全登录体验。</span><span class="sxs-lookup"><span data-stu-id="f383f-125">Is seamless for end users: complete the full sign in experience right within Teams.</span></span>
* <span data-ttu-id="f383f-126">包括简单的令牌管理：无需再实现令牌存储系统，而是自动程序服务负责令牌缓存并提供用于提取这些令牌的安全机制。</span><span class="sxs-lookup"><span data-stu-id="f383f-126">Includes easy token management: you no longer have to implement a token storage system – instead, the Bot Service takes care of token caching and provides a secure mechanism for fetching those tokens.</span></span>
* <span data-ttu-id="f383f-127">受完整 SDK 支持：易于集成和使用自动程序服务。</span><span class="sxs-lookup"><span data-stu-id="f383f-127">Is supported by complete SDKs: easy to integrate and consume from your bot service.</span></span>
* <span data-ttu-id="f383f-128">具有对许多热门 OAuth 提供程序（如 Azure AD/MSA、Facebook 和 Google）的现成支持。</span><span class="sxs-lookup"><span data-stu-id="f383f-128">Has out-of-box support for many popular OAuth providers, such as Azure AD/MSA, Facebook, and Google.</span></span>

## <a name="when-should-i-implement-my-own-solution"></a><span data-ttu-id="f383f-129">我应在何时实施自己的解决方案？</span><span class="sxs-lookup"><span data-stu-id="f383f-129">When should I implement my own solution?</span></span>

<span data-ttu-id="f383f-130">由于访问令牌是敏感信息，因此你可能不希望将它们存储在外部服务中。</span><span class="sxs-lookup"><span data-stu-id="f383f-130">Because access tokens are sensitive information, you may not wish to have them stored in an external service.</span></span> <span data-ttu-id="f383f-131">在这种情况下，你可以选择在 Teams 中仍实现自己的令牌管理系统和登录体验，如 [Teams](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) 身份验证主题的其余部分所述。</span><span class="sxs-lookup"><span data-stu-id="f383f-131">In this case, you may choose to still implement your own token management system and login experience within Teams, as described in the rest of the Teams [Authentication](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) topics.</span></span>

## <a name="getting-started-with-oauthcard-in-teams"></a><span data-ttu-id="f383f-132">Teams 中的 OAuthCard 入门</span><span class="sxs-lookup"><span data-stu-id="f383f-132">Getting started with OAuthCard in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="f383f-133">本指南使用 Bot Framework v3 SDK。</span><span class="sxs-lookup"><span data-stu-id="f383f-133">This guide is using the Bot Framework v3 SDK.</span></span> <span data-ttu-id="f383f-134">你可以在此处找到 v4 [实现](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="f383f-134">You can find the v4 implementation [here](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span></span> <span data-ttu-id="f383f-135">你仍然需要创建清单，并包括 token.botframework.com，否则"登录"按钮 `validDomains` 将不能打开身份验证窗口。</span><span class="sxs-lookup"><span data-stu-id="f383f-135">You will still need to create a manifest and include token.botframework.com in the `validDomains` section, because otherwise the Sign in button will not open the authentication window.</span></span> <span data-ttu-id="f383f-136">使用 [App Studio](~/concepts/build-and-test/app-studio-overview.md) 生成清单。</span><span class="sxs-lookup"><span data-stu-id="f383f-136">Use the [App Studio](~/concepts/build-and-test/app-studio-overview.md) to generate your manifest.</span></span>

<span data-ttu-id="f383f-137">首先需要配置 Azure 自动程序服务以设置外部身份验证提供程序。</span><span class="sxs-lookup"><span data-stu-id="f383f-137">You’ll first need to configure your Azure bot service to set up external authentication providers.</span></span> <span data-ttu-id="f383f-138">有关 [详细步骤，请参阅配置](~/concepts/authentication/configure-identity-provider.md) 标识提供程序。</span><span class="sxs-lookup"><span data-stu-id="f383f-138">Read [Configuring identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps.</span></span>

<span data-ttu-id="f383f-139">若要启用使用 Azure Bot 服务的身份验证，你需要对代码进行以下添加：</span><span class="sxs-lookup"><span data-stu-id="f383f-139">To enable authentication using the Azure Bot Service, you need to make these additions to your code:</span></span>

1. <span data-ttu-id="f383f-140">将 token.botframework.com 包括在应用清单的 部分中，因为 `validDomains` Teams 将嵌入自动程序服务的登录页。</span><span class="sxs-lookup"><span data-stu-id="f383f-140">Include token.botframework.com in the `validDomains` section of your app manifest because Teams will embed the Bot Service’s login page.</span></span>
2. <span data-ttu-id="f383f-141">每当机器人需要访问经过身份验证的资源时，从自动程序服务获取令牌。</span><span class="sxs-lookup"><span data-stu-id="f383f-141">Fetch the token from the Bot Service whenever your bot needs to access authenticated resources.</span></span> <span data-ttu-id="f383f-142">如果没有可用的令牌，则向用户发送包含 OAuthCard 的消息，请求他们登录到外部服务。</span><span class="sxs-lookup"><span data-stu-id="f383f-142">If no token is available, send a message with an OAuthCard to the user requesting them to log into the external service.</span></span>
3. <span data-ttu-id="f383f-143">处理登录完成活动。</span><span class="sxs-lookup"><span data-stu-id="f383f-143">Handle the login completion activity.</span></span> <span data-ttu-id="f383f-144">这将确保身份验证请求和令牌与当前与自动程序交互的用户相关联。</span><span class="sxs-lookup"><span data-stu-id="f383f-144">This ensures that the authentication request and the token are associated with the user currently interacting with your bot.</span></span>
4. <span data-ttu-id="f383f-145">每当机器人需要执行已验证的操作（如调用外部 REST API）时检索令牌。</span><span class="sxs-lookup"><span data-stu-id="f383f-145">Retrieve the token whenever your bot needs to perform authenticated actions, such as calling external REST APIs.</span></span>

<span data-ttu-id="f383f-146">在对话框代码中，你需要将此代码段添加到 (C#) ，以检查现有访问令牌：</span><span class="sxs-lookup"><span data-stu-id="f383f-146">In your dialog code, you’ll need to add this snippet (C#), which checks for an existing access token:</span></span>

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

<span data-ttu-id="f383f-147">如果访问令牌不存在，代码随后会向用户发送包含 OAuthCard 的邮件：</span><span class="sxs-lookup"><span data-stu-id="f383f-147">If an access token doesn’t exist, your code will then send a message with an OAuthCard to the user:</span></span>

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

<span data-ttu-id="f383f-148">若要处理登录完成活动，需要处理此 Invoke：</span><span class="sxs-lookup"><span data-stu-id="f383f-148">To handle the login complete activity, you’ll need to process this Invoke:</span></span>

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

<span data-ttu-id="f383f-149">在对话框代码中，然后可以从 Bot 身份验证服务检索令牌：</span><span class="sxs-lookup"><span data-stu-id="f383f-149">In your dialog code, you can then retrieve the token from the Bot authentication service:</span></span>

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

## <a name="using-oauthcard-with-messaging-extensions"></a><span data-ttu-id="f383f-150">将 OAuthCard 与邮件扩展一同使用</span><span class="sxs-lookup"><span data-stu-id="f383f-150">Using OAuthCard with messaging extensions</span></span>

<span data-ttu-id="f383f-151">您还可以使用 Azure Bot 服务将第三方提供程序连接到邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="f383f-151">You can also use Azure Bot Service to connect third-party providers to your messaging extension.</span></span> <span data-ttu-id="f383f-152">该流与自动程序相同，除了不返回 OAuthCard，服务将返回登录提示。</span><span class="sxs-lookup"><span data-stu-id="f383f-152">The flow is the same as with a bot, except instead of returning an OAuthCard, your service will return a login prompt.</span></span>

<span data-ttu-id="f383f-153">下面的代码 (C#) 演示如何创建登录响应：</span><span class="sxs-lookup"><span data-stu-id="f383f-153">The following snippet (C#) illustrates how to craft the login response:</span></span>

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

<span data-ttu-id="f383f-154">请注意，在以上示例中，您需要直接对 属性 `GetSignInLinkAsync` `client.OAuthApi` 进行调用。</span><span class="sxs-lookup"><span data-stu-id="f383f-154">Note that in the example above you need to make the call to `GetSignInLinkAsync` directly against the `client.OAuthApi` property.</span></span>

<span data-ttu-id="f383f-155">当用户成功完成登录序列时，你的服务将收到另一个 Invoke 请求，其中包含原始用户查询以及包含"神奇代码"的状态参数字符串。</span><span class="sxs-lookup"><span data-stu-id="f383f-155">When the user successfully completes the login sequence, your service will receive another Invoke request containing the original user query, along with a state parameter string containing the “magic code”.</span></span> <span data-ttu-id="f383f-156">现在，可以使用此字符串以及用户 ID 和连接名称获取令牌。</span><span class="sxs-lookup"><span data-stu-id="f383f-156">You can now fetch the token using this string, along with the user ID and connection name.</span></span>

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
