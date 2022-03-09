---
title: 使用外部 OAuth 提供程序
description: 描述使用外部 OAuth 提供程序的身份验证
ms.topic: how-to
ms.localizationpriority: high
keywords: 使用外部 OAuth 提供程序进行团队身份验证
ms.openlocfilehash: c9327eb731d537d0f4eff04cc381a883bde5d98e
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "63360521"
---
# <a name="use-external-oauth-providers"></a>使用外部 OAuth 提供程序

可以使用更新的 `authenticate()` API 支持外部或第三方 (3P) OAuth 提供程序，例如 Google、GitHub、LinkedIn 和 Facebook：

```JavaScript
function authenticate(authenticateParameters?: AuthenticateParameters)
``` 

以下内容添加到 `authenticate()` API 以支持外部 OAuth 提供程序：

* `isExternal` 参数
* 现有 `url` 参数中的两个占位符值

下表提供了 `authenticate()` API 参数和函数的列表及其说明：

| 参数| 说明|
| --- | --- |
|`isExternal` | 参数的类型为布尔值，指示身份验证窗口在外部浏览器中打开。|
|`failureCallback`| 如果身份验证失败，并且身份验证弹出窗口说明了失败的原因，则调用该函数。|
|`height` |弹出窗口的首选高度。 如果值超出可接受的边界，则可以忽略该值。|
|`successCallback`| 如果身份验证成功，则调用该函数，并从身份验证弹出窗口返回结果。 身份验证是结果。|
|`url`  <br>|身份验证弹出的 3P 应用服务器 URL，具有以下两个参数占位符：</br> <br> - `oauthRedirectMethod`：在 `{}` 中传递占位符。 此占位符被 Teams 平台替换为 deeplink 或网页，这会通知应用服务器呼叫是否来自移动平台。</br> <br> - `authId`：此占位符被 UUID 替换。 应用服务器使用它来维护会话。| 
|`width`|弹出窗口的首选宽度。 如果值超出可接受的边界，则可以忽略该值。|

有关参数的详细信息，请参阅[身份验证参数接口](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest&preserve-view=true)。

## <a name="add-authentication-to-external-browsers"></a>向外部浏览器添加身份验证

> [!NOTE]
> * 目前，只能向外部浏览器添加对移动版选项卡的身份验证。 
> * 使用 JS SDK 的 beta 版本来利用此功能。 beta 版本通过 [NPM](https://www.npmjs.com/package/@microsoft/teams-js/v/1.12.0-beta.2) 提供。

下图提供了向外部浏览器添加身份验证的流：

 :::image type="content" source="../../../assets/images/tabs/tabs-authenticate-OAuth.PNG" alt-text="authenticate-OAuth" border="true":::

### <a name="steps-to-perform-authentication-to-external-browsers"></a>对外部浏览器执行身份验证的步骤

<!-- #### 1. Pass `isExternal` and placeholders in `url` -->
**1. 启动外部身份验证登录过程**

3P 应用调用 SDK 函数 `microsoftTeams.authentication.authenticate`，`isExternal` 设置为 true 以启动外部身份验证登录过程。 

传递的 `url` 包含 `{authId}` 的占位符，以及 `{oauthRedirectMethod}`。  


```JavaScript
microsoftTeams.authentication.authenticate({
   url: 'https://3p.app.server/auth?oauthRedirectMethod={oauthRedirectMethod}&authId={authId}',
   isExternal: true,
   successCallback: function (result) {
   //sucess 
   } failureCallback: function (reason) {
   //failure 
    }
});
```

**2. 外部浏览器中的 Teams 链接**

Teams 客户端在将 `oauthRedirectMethod` 和 `authId` 的占位符替换为合适的值后，在外部浏览器中打开 URL。 

#### <a name="example"></a>示例

```http
 https://3p.app.server/auth?oauthRedirectMethod=deeplink&authId=1234567890 
```

**3. 3P 应用服务器响应**

3P 应用服务器使用以下两个查询参数接收并保存 `url`：

| 参数 | 说明|
| --- | --- |
| `oauthRedirectMethod` |指示 3P 应用必须如何使用以下两个值之一将身份验证请求的响应发送回 Teams：deeplink 或 page。|
|`authId` | 为此特定身份验证请求创建的请求 ID Teams，需要通过 deeplink 发送回 Teams。|

> [!TIP]
> 3P 应用可以封送 OAuth `state` 查询参数中的 `authId`、`oauthRedirectMethod`，同时生成 OAuthProvider 的登录 URL。 `state` 包含传递的 `authId` 和 `oauthRedirectMethod`，当 OAuthProvider 重定向回 3P 服务器时，3P 应用使用值将身份验证响应发送回 Teams，如 **6. 3P 应用服务器对 Teams 的响应** 中所述。 

**4. 3P 应用服务器重定向到指定的 `url`**

3P 应用服务器在外部浏览器中重定向到 OAuth 提供程序身份验证页。 `redirect_uri` 是 3P 应用服务器上的专用路由。 可以在 OAuth 提供程序的开发控制台中将 `redirect_uri` 注册为静态，需要通过状态对象发送参数。 

#### <a name="example"></a>示例

```http
https://accounts.google.com/o/oauth2/v2/auth?redirect_uri=https://3p.app.server/authredirect&state={"authId":"…","oauthRedirectMethod":"…"}&client_id=…&response_type=code&access_type=offline&scope= … 
```

**5. 登录到外部浏览器**

用户登录到外部浏览器。 OAuth 提供程序使用身份验证代码和状态对象重定向回 `redirect_uri`。

**6. 3P 应用服务器对 Teams 的响应** 

3P 应用服务器处理响应并检查 `oauthRedirectMethod`，它将从状态对象中的外部 OAuth 提供程序返回，以确定是否需要通过身份验证回调深层链接或通过调用 `notifySuccess()` 的网页返回响应。

```JavaScript
const state = JSON.parse(req.query.state)
if (state.oauthRedirectMethod === 'deeplink') {
   return res.redirect('msteams://teams.microsoft.com/l/auth-callback?authId=${state.authId}&code=${req.query.code}')
}
else {
// continue redirecting to a web-page that will call notifySuccsss() – usually this method is used in Teams-Web
…
```

**7. 3P 应用生成深层链接**

3P 应用以以下格式为 Teams 移动版生成深层链接，并将会话 ID 的身份验证代码发送回 Teams。
 
```JavaScript
return res.redirect(`msteams://teams.microsoft.com/l/auth-callback?authId=${state.authId}&code=${req.query.code}`)
```

 **8. Teams 成功回调结果**

Teams 调用成功回调，并将结果（身份验证代码）发送到 3P 应用。 3P 应用接收成功回调中的代码，并使用代码检索令牌、用户信息、更新用户界面。

```JavaScript
successCallback: function (result) { 
… 
} 
```

## <a name="see-also"></a>另请参阅

* [配置标识提供程序](../../../concepts/authentication/configure-identity-provider.md)
* [选项卡的 Microsoft Teams 身份验证流](auth-flow-tab.md)
