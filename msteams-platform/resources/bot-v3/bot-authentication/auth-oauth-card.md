---
title: 在 Teams 中使用 Azure 机器人服务进行身份验证
description: 介绍 Azure 机器人服务 OAuthCard 及其用于身份验证的用法
ms.topic: conceptual
localization_priority: Normal
keywords: teams 身份验证 OAuthCard OAuth 卡 Azure 机器人服务
ms.openlocfilehash: 7731e4d1148e50c748d9c5e1b55371628a78dea7
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143163"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a>在 Teams 中使用 Azure 机器人服务进行身份验证

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

如果没有 Azure 机器人服务的 OAuthCard，在机器人中实现身份验证会很复杂。 这是一个完整的堆栈挑战，涉及构建 Web 体验、与外部 OAuth 提供程序集成、令牌管理以及处理正确的服务器到服务器 API 调用，以安全地完成身份验证流。 这可能会导致需要输入“神奇数字”的笨重体验。

使用 Azure 机器人服务的 OAuthCard，Teams机器人可以更轻松地登录用户并访问外部数据提供程序。 无论你是否已实现身份验证，并且想要切换到更简单的东西，或者如果希望首次将身份验证添加到机器人服务，OAuthCard 可以简化此操作。

[身份验证](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)中的其他主题描述不使用 OAuthCard 的身份验证，因此，如果想要更深入地了解Teams的身份验证，或者遇到无法使用 OAuthCard 的情况，仍可参考这些主题。

## <a name="support-for-the-oauthcard"></a>对 OAuthCard 的支持

目前，可以使用 OAuthCard 的位置存在一些限制。 具体包括：

* 该卡不适用于 [来宾访问](/MicrosoftTeams/guest-access)。
* 它不适用于[Microsoft Teams 免费版](https://products.office.com/microsoft-teams/free)。
* 它只能用于机器人身份验证。
* 它仅适用于在 [Azure 机器人服务](https://azure.microsoft.com/services/bot-service/)中注册的机器人。

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a>Azure 机器人服务如何帮助我进行身份验证？

本主题提供了使用 OAuthCard 的完整文档：[通过 Azure 机器人服务 向机器人添加身份验证](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true)。 请注意，本主题在 Azure Bot Framework 文档集中，不特定于Teams。

以下部分介绍如何在 Teams 中使用 OAuthCard。

## <a name="main-benefits-for-teams-developers"></a>Teams开发人员的主要优势

OAuthCard 通过以下方式帮助进行身份验证：

* 提供基于 Web 的现用身份验证流：无需再编写和托管网页即可直接访问外部登录体验或提供重定向。
* 对于最终用户而言是无缝的：在Teams内完成完整登录体验。
* 包括简单的令牌管理：不再需要实现令牌存储系统 - 相反，机器人服务负责令牌缓存，并提供用于提取这些令牌的安全机制。
* 受完整 SDK 支持：易于从机器人服务集成和使用。
* 对许多受欢迎的 OAuth 提供商（如 Azure AD/MSA、Facebook 和 Google）提供现成的支持。

## <a name="when-should-i-implement-my-own-solution"></a>何时应实现自己的解决方案？

由于访问令牌是敏感信息，因此你可能不希望它们存储在外部服务中。 在这种情况下，可以选择在Teams中仍实现自己的令牌管理系统和登录体验，如其他Teams[身份验证](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)主题中所述。

## <a name="getting-started-with-oauthcard-in-teams"></a>Teams中的 OAuthCard 入门

> [!NOTE]
> 本指南使用 Bot Framework v3 SDK。 可 [在此](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)处找到 v4 实现。 仍需创建清单并在部分中 `validDomains` 包含 token.botframework.com，否则“登录”按钮将不会打开身份验证窗口。 使用 [App Studio](~/concepts/build-and-test/app-studio-overview.md) 生成清单。

首先需要将 Azure 机器人服务配置为设置外部身份验证提供程序。 有关详细步骤，请阅读 [“配置标识提供者](~/concepts/authentication/configure-identity-provider.md) ”。

若要使用 Azure 机器人服务启用身份验证，需要在代码中添加以下内容：

1. 在应用清单部分中`validDomains`包含 token.botframework.com，因为Teams将嵌入机器人服务的登录页。
2. 每当机器人需要访问经过身份验证的资源时，从机器人服务中提取令牌。 如果没有可用令牌，请向请求用户登录到外部服务的用户发送带有 OAuthCard 的消息。
3. 处理登录完成活动。 这可确保身份验证请求和令牌与当前与机器人交互的用户相关联。
4. 每当机器人需要执行经过身份验证的操作（例如调用外部 REST API）时，检索令牌。

在对话框代码中，需要添加此代码片段 (C#) ，用于检查现有访问令牌：

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

如果访问令牌不存在，则代码会向用户发送带有 OAuthCard 的消息：

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

若要处理登录完成活动，需要处理此调用：

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

然后，在对话框代码中，可以从机器人身份验证服务检索令牌：

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

## <a name="using-oauthcard-with-messaging-extensions"></a>将 OAuthCard 与消息传递扩展配合使用

还可以使用 Azure 机器人服务将第三方提供程序连接到消息传递扩展。 流与机器人相同，但服务将返回登录提示，而不是返回 OAuthCard。

以下代码片段 (C#) 演示如何创建登录响应：

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

请注意，在上面的示例中，需要直接对`client.OAuthApi`属性进行调用`GetSignInLinkAsync`。

当用户成功完成登录序列时，服务将收到另一个包含原始用户查询的 Invoke 请求，以及包含“magic code”的状态参数字符串。 现在可以使用此字符串以及用户 ID 和连接名称提取令牌。

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
