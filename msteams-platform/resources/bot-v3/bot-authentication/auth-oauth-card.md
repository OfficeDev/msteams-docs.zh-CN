---
title: 将 Azure Bot 服务用于 Teams
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
# <a name="using-azure-bot-service-for-authentication-in-teams"></a>将 Azure Bot 服务用于 Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

如果没有 Azure Bot Service 的 OAuthCard，在自动程序中实现身份验证会很复杂。 这是一个全堆栈挑战，涉及构建 Web 体验、与外部 OAuth 提供程序集成、令牌管理，以及处理正确的服务器到服务器 API 调用以安全完成身份验证流。 这可能会导致需要输入"神奇数字"的奇怪体验。

借助 Azure Bot Service 的 OAuthCard，Teams自动程序可以更轻松地登录用户和访问外部数据提供程序。 无论你是否已实现身份验证并且想要切换到更简单的方法，或者如果你希望首次向自动程序服务添加身份验证，OAuthCard 都可以简化操作。

身份验证[中的](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)其他主题介绍不使用 OAuthCard 的身份验证，因此如果您想要更深入地了解 Teams 中的身份验证，或者有一个无法使用 OAuthCard 的情况，您仍可以参考这些主题。

## <a name="support-for-the-oauthcard"></a>对 OAuthCard 的支持

目前，对 OAuthCard 的使用位置存在一些限制。 其中包括：

* 该卡不能与来宾 [访问一起使用](/MicrosoftTeams/guest-access)
* 它不能与免费Microsoft Teams[一起](https://products.office.com/microsoft-teams/free)
* 它只能用于自动程序身份验证
* 它仅适用于在 Azure Bot 服务 [中注册的机器人](https://azure.microsoft.com/services/bot-service/)

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a>Azure 自动程序服务如何协助我进行身份验证？

有关使用 OAuthCard 的完整文档，请参阅主题：通过 Azure Bot 服务向自动 [程序添加身份验证](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true)。 请注意，本主题位于 Azure Bot Framework 文档集，并非特定于 Teams。

以下各节将告知如何在 Teams 中使用 OAuthCard。

## <a name="main-benefits-for-teams-developers"></a>开发人员的主要Teams

OAuthCard 通过以下方式帮助进行身份验证：

* 提供基于 Web 的开箱即用身份验证流：无需再编写和托管网页来定向外部登录体验或提供重定向。
* 对于最终用户是无缝的：在完全登录体验中Teams。
* 包括简单的令牌管理：无需再实现令牌存储系统，而是自动程序服务负责令牌缓存并提供用于提取这些令牌的安全机制。
* 受完整 SDK 支持：易于集成和使用自动程序服务。
* 具有对许多热门 OAuth 提供程序（如 Azure AD/MSA、Facebook 和 Google）的现成支持。

## <a name="when-should-i-implement-my-own-solution"></a>我应在何时实施自己的解决方案？

由于访问令牌是敏感信息，因此你可能不希望将它们存储在外部服务中。 在这种情况下，你可以选择仍在 Teams 中实现自己的令牌管理系统和登录体验，如 Teams[身份验证](~/resources/bot-v3/bot-authentication/auth-flow-bot.md)主题的其余部分所述。

## <a name="getting-started-with-oauthcard-in-teams"></a>在 Teams 中开始使用 OAuthCard

> [!NOTE]
> 本指南使用 Bot Framework v3 SDK。 你可以在此处找到 v4 [实现](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)。 你仍然需要创建清单，并包括 token.botframework.com，否则"登录"按钮 `validDomains` 将不能打开身份验证窗口。 使用 [App Studio](~/concepts/build-and-test/app-studio-overview.md) 生成清单。

首先需要配置 Azure 自动程序服务以设置外部身份验证提供程序。 有关 [详细步骤，请参阅配置](~/concepts/authentication/configure-identity-provider.md) 标识提供程序。

若要启用使用 Azure Bot 服务的身份验证，你需要对代码进行以下添加：

1. 在 token.botframework.com 清单的 部分中包括 `validDomains` Teams，因为系统将会嵌入自动程序服务的登录页。
2. 每当机器人需要访问经过身份验证的资源时，从自动程序服务获取令牌。 如果没有可用的令牌，则向用户发送包含 OAuthCard 的消息，请求他们登录到外部服务。
3. 处理登录完成活动。 这将确保身份验证请求和令牌与当前与自动程序交互的用户相关联。
4. 每当机器人需要执行已验证的操作（如调用外部 REST API）时检索令牌。

在对话框代码中，你需要将此代码段添加到 (C#) ，以检查现有访问令牌：

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

如果访问令牌不存在，代码随后会向用户发送包含 OAuthCard 的邮件：

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

若要处理登录完成活动，需要处理此 Invoke：

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

在对话框代码中，然后可以从 Bot 身份验证服务检索令牌：

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

## <a name="using-oauthcard-with-messaging-extensions"></a>将 OAuthCard 与邮件扩展一同使用

您还可以使用 Azure Bot 服务将第三方提供程序连接到邮件扩展。 该流与自动程序相同，除了不返回 OAuthCard，服务将返回登录提示。

下面的代码 (C#) 演示如何创建登录响应：

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

请注意，在以上示例中，您需要直接对 属性 `GetSignInLinkAsync` `client.OAuthApi` 进行调用。

当用户成功完成登录序列时，你的服务将收到另一个 Invoke 请求，其中包含原始用户查询以及包含"神奇代码"的状态参数字符串。 现在，可以使用此字符串以及用户 ID 和连接名称获取令牌。

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
