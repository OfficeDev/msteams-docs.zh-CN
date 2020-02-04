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
# <a name="using-azure-bot-service-for-authentication-in-teams"></a>在团队中使用 Azure Bot 服务进行身份验证

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

如果没有 Azure Bot 服务的 OAuthCard，则在 Bot 中实施身份验证非常复杂。 它是一项全面的挑战，涉及构建 web 体验、与外部 OAuth 提供程序集成、令牌管理和处理正确的服务器到服务器 API 调用，以安全地完成身份验证流。 这可能会导致需要输入 "幻数" 的 clunky 体验。

借助 Azure Bot 服务的 OAuthCard，团队 Bot 可以更轻松地登录用户并访问外部数据提供程序。 无论您是否已实施身份验证，还是要切换到更简单的功能，或者如果您希望首次将身份验证添加到你的 bot 服务中，则 OAuthCard 可以更轻松地执行操作。

[身份验证](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)中的其他主题在不使用 OAuthCard 的情况下描述身份验证。因此，如果您想要更深入地了解团队中的身份验证，或在不能使用 OAuthCard 的情况下，您仍可以参考这些主题。

## <a name="support-for-the-oauthcard"></a>对 OAuthCard 的支持

目前，您可以对 OAuthCard 使用某些限制。 具体包括：

* 该卡片将不能与[来宾访问](/MicrosoftTeams/guest-access)一起使用
* 它将不会在[Microsoft 团队中免费](https://products.office.com/microsoft-teams/free)使用
* 它仅可用于 bot 身份验证
* 它仅适用于在[Azure Bot 服务](https://azure.microsoft.com/services/bot-service/)中注册的 bot

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a>Azure Bot 服务如何帮助我进行身份验证？

主题中提供了使用 OAuthCard 的完整文档，主题：[通过 Azure Bot 服务向你的 Bot 添加身份验证](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0)。 请注意，此主题位于 Azure Bot 框架文档集，而不是特定于团队。

以下各节介绍如何在团队中使用 OAuthCard。

## <a name="main-benefits-for-teams-developers"></a>团队开发人员的主要好处

OAuthCard 通过以下方式帮助进行身份验证：

* 提供现成的基于 web 的身份验证流：无需再编写和托管网页即可直接访问外部登录体验或提供重定向。
* 对于最终用户是无缝的：在团队中完全填写完整的登录体验。
* 包括轻松令牌管理：您不必再实现令牌存储系统–即 Bot 服务负责令牌缓存，并提供用于提取这些令牌的安全机制。
* 由完整的 Sdk 支持：易于集成和使用你的 bot 服务。
* 提供了对许多常用 OAuth 提供程序的现成支持，如 Azure AD/MSA、Facebook 和 Google。

## <a name="when-should-i-implement-my-own-solution"></a>我应该何时实施自己的解决方案？

由于访问令牌是敏感信息，因此您可能不希望将它们存储在外部服务中。 在这种情况下，您可以选择仍实现您自己的令牌管理系统和团队中的登录体验，如其余的团队[身份验证](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)主题中所述。

## <a name="getting-started-with-oauthcard-in-teams"></a>团队中的 OAuthCard 入门

> [!NOTE]
> 本指南使用的是 Bot 框架 v3 SDK。 你可以在[此处](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp)找到 v4 实现。 您仍需要创建一个清单并将 token.botframework.com 包括在`validDomains`部分中，因为否则 "登录" 按钮不会打开 "身份验证" 窗口。 使用[应用程序 Studio](~/concepts/build-and-test/app-studio-overview.md)生成清单。

首先需要配置 Azure bot 服务以设置外部身份验证提供程序。 有关详细步骤，请阅读[配置标识提供程序](~/concepts/authentication/configure-identity-provider.md)。

若要使用 Azure Bot 服务启用身份验证，需要对代码进行以下添加：

1. 在应用程序清单`validDomains`的部分中添加 token.botframework.com，因为团队将嵌入 Bot 服务的登录页。
2. 只要你的 bot 需要访问已通过身份验证的资源，即可从 Bot 服务中提取令牌。 如果没有可用的令牌，请将包含 OAuthCard 的邮件发送给请求他们登录外部服务的用户。
3. 处理登录完成活动。 这将确保身份验证请求和令牌与当前与你的 bot 交互的用户相关联。
4. 只要你的 bot 需要执行经过身份验证的操作（如调用外部 REST Api），即可检索令牌。

在对话框代码中，您需要添加此代码段（c #），它将检查现有的访问令牌：

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

如果访问令牌不存在，则代码将向用户发送包含 OAuthCard 的邮件：

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

若要处理 "登录完成" 活动，您需要处理此调用：

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

在对话框代码中，您可以从 Bot 身份验证服务中检索令牌：

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

## <a name="using-oauthcard-with-messaging-extensions"></a>结合使用 OAuthCard 和邮件扩展

您还可以使用 Azure Bot 服务将第三方提供程序连接到您的邮件扩展。 流与 bot 相同，不同之处在于，服务将返回登录提示，而不是返回 OAuthCard。

下面的代码段（c #）说明了如何创建登录响应：

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

请注意，在上面的示例中，您需要对`GetSignInLinkAsync` `client.OAuthApi`属性直接调用。

当用户成功完成登录序列时，服务将接收另一个包含原始用户查询的调用请求，以及包含 "幻码" 的状态参数字符串。 现在，您可以使用此字符串以及用户 ID 和连接名称提取令牌。

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
