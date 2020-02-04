---
title: Microsoft 团队和 SameSite cookie 属性（2020更新）
author: laujan
description: ''
keywords: cookie 属性 samesite
ms.topic: reference
ms.author: lomeybur
ms.openlocfilehash: 167266ba0b5af1c8233cffe1fef496dd94c27ae4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673020"
---
# <a name="microsoft-teams-and-the-samesite-cookie-attribute-2020-update"></a>Microsoft 团队和 SameSite cookie 属性（2020更新）

## <a name="cookies-in-brief"></a>简单小甜饼

 Cookie 是通过 web 浏览器从网站发送并存储在计算机上的文本字符串。 它们通常用于身份验证和个性化设置，例如，撤回有状态的信息、保留用户设置、录制浏览活动以及显示相关广告。 Cookie 始终链接到特定域，并且可以由各方安装。 它们的分类方式如下所示：

 |Cookie|范围|
 | ------ | ------ |
 |**第一方 cookie**|第一方 cookie 由用户访问并用于保存数据（如购物车项目、登录凭据（如身份验证 cookie）和其他分析）的网站创建。|
 |**第二方 cookie**|第二方 cookie 在技术上与第一方 cookie 相同。 区别在于，数据是通过数据合作协议（例如[Microsoft 团队分析和报告](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference)）与第二方共享的。 |
 |**第三方 cookie**|第三方 cookie 由用户显式访问的域而不是安装，主要用于跟踪（例如 "赞" 按钮）、广告服务和 live 聊天。|

### <a name="cookies-and-http-requests"></a>Cookie 和 HTTP 请求

在引入 SameSite 限制之前，cookie 存储在浏览器中时，它们被附加到*每个*HTTP web 请求，并通过设置 Cookie HTTP 响应头发送到服务器。 是可预测的，这种性能可能会引入安全漏洞，如跨站点请求伪造（CSRF）攻击。 *请参阅* [HTTP cookie](https://developer.mozilla.org/docs/Web/HTTP/Cookies)。 SameSite 组件通过其在 SetCookie 标头中的实现和管理减轻了暴露。

### <a name="samesite-attribute-initial-release"></a>SameSite 属性：初始版本

Google Chrome 版本51引入了 SetCookie SameSite 规范作为*可选*属性。 从版本17672开始，Windows 10 为[Microsoft Edge 浏览器](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/)引入了 SameSite cookie 支持。

开发者可以选择不将 SameSite cookie 属性添加到 SetCookie 标头，也可以使用以下两个设置之一（不*严格*和*严格*）添加它。 未实现的 SameSite 属性被视为默认状态。

## <a name="samesite-cookie-attribute-2020-release"></a>SameSite cookie 属性：2020版本

Chrome 80，计划在二月2020中发布，引入了新的 cookie 值，并默认强加了 cookie 策略。 三个值可以传递到更新的 SameSite 属性： *Strict*、*宽松*或*无*。 未指定 SameSite 属性的 cookie 将默认为`SameSite=Lax`。

|Setting | 强行 | 值 |属性规范 |
| -------- | ----------- | --------|--------|
| **严格**  | Cookie 只会在*第一方*上下文和 HTTP GET 请求中自动发送。 将在跨站点子请求（例如，调用加载图像或 iframe）上预扣 SameSite cookie，但当用户导航到来自外部网站的 URL （例如，通过使用链接）时，将会发送这些 cookie。| **默认** |`Set-Cookie: key=value; SameSite=Lax`|
| **全** |浏览器将仅发送第一方上下文请求的 cookie （源自设置 cookie 的站点的请求）。 如果请求源自于当前位置不同的 URL，则不会发送使用该`Strict`属性标记的任何 cookie。| 可选 |`Set-Cookie: key=value; SameSite=Strict`|
| **无** | Cookie 将同时在第一方上下文和跨源请求中发送;但是，必须将该值显式设置为**`None`** ，并且所有浏览器请求**必须遵循 HTTPS 协议**，并包括**`Secure`** 需要加密连接的属性。 不符合该要求的 cookie 将被**拒绝**。 <br/>**这两个属性同时需要**。 如果仅**`None`** 在未指定**`Secure`** 的情况下指定，或者未使用 HTTPS 协议，则将拒绝第三方 cookie。| 可选，但如果设置，则需要 HTTPS 协议。 |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="handling-incompatible-clients"></a>处理不兼容客户端

> [!IMPORTANT]
> 目前， `SameSite=None` [**团队桌面客户端**](/aspnet/core/security/samesite?view=aspnetcore-3.1#test-with-electron)或更早版本的 Chrome 或 Safari 不支持此方法。 *请参阅*[已知不兼容的客户端]( https://www.chromium.org/updates/same-site/incompatible-clients)。
>但是，有两种**解决方法**：
>
>1. 检查用户代理以便提供正确的 SameSite 属性。 您可以在[**c #**](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)和[**node.js**](https://web.dev/samesite-cookie-recipes/)中实现用户代理检查。
>2. 使用新旧模型和旧模型设置 cookie 属性。 *请参阅*[处理不兼容客户端](https://web.dev/samesite-cookie-recipes/#handling-incompatible-clients)<br><br>
>**如果您的应用程序在团队桌面客户端中运行，并且您将 SameSite 属性`SameSite=None`设置为，则您的应用程序将无法按预期工作。**

使用这两种方法均可确保在团队桌面客户端升级到`SameSite=None`兼容版本的 Chromium 时，您的应用程序能够继续正常工作。

## <a name="teams-implications-and-adjustments"></a>团队的含义和调整

>[!WARNING]
>**在团队桌面客户端中运行的应用程序与`SameSite=None`属性不兼容，它们不会按预期工作。** 请参阅上面的**解决方法解决方案**。

1. 为 cookie 启用相关的 SameSite 设置，并验证您的应用程序和扩展是否继续在团队中工作。
1. 如果您的应用程序或扩展出现故障，请在 Chrome 80 版本之前进行必要的修复。
1. 如果 Microsoft 内部合作伙伴需要详细信息或帮助解决此问题，则可以加入以下团队： <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47>。

> [!NOTE]
> 为获得最佳实践，建议您始终设置 SameSite 属性以反映您的 cookie 的预期用途，而不依赖于默认浏览器行为。 *请参阅*[开发人员：为新 SameSite 准备就绪 = 无;安全的 Cookie 设置](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)。

### <a name="tabs-task-modules-and-message-extensions"></a>选项卡、任务模块和邮件扩展名

* 工作组选项卡`<iframes>`用于嵌入在顶级或第一方上下文中查看的内容。
* 任务模块使您能够在团队应用程序中创建模式弹出窗口体验。 与选项卡类似，模式窗口在当前页中打开。
* 邮件扩展允许你将丰富的内容从外部资源插入聊天消息。

当网站显示在中时，嵌入内容使用的任何 cookie 都将被视为第三`<iframe>`方。 此外，如果页面上的任何远程资源依赖于通过请求（例如， `<img>` `<script>`标记、外部字体和个性化内容）发送的 cookie，则需要确保将其标记为跨网站使用— `SameSite=None; Secure`或确保回退已准备就绪。

### <a name="authentication"></a>身份验证

* 如果需要在选项卡中对嵌入的内容页进行身份验证，则需要使用基于 web 的身份验证流。
* 基于 web 的身份验证流还可用于配置页面、任务模块或邮件扩展。
* 您可以对对话机器人使用基于 web 的身份验证流，您需要使用任务模块。

根据更新的 SameSite 限制，如果链接派生自外部网站，浏览器将不会向已经过身份验证的网站添加 cookie。 您需要确保您的身份验证 cookie 已标记为跨网站使用— `SameSite=None; Secure`或者确保回退已准备就绪。

### <a name="android-system-webview"></a>Android 系统 Web 视图

Android Web 视图是一个 Chrome 系统组件，它允许 Android 应用显示 web 内容。 虽然新的限制将成为默认值，但从 Chrome 80 开始，它们不会立即在 WebViews 上强制实施。 以后将对其应用。 为准备好，Android 允许本机应用通过[COOKEMANAGER API](https://developer.android.com/reference/android/webkit/CookieManager)直接设置 cookie：

* 对于仅在第一方上下文中需要的 cookie，应根据需要将其声明`SameSite=Lax`为`SameSite=Strict`或。
* 对于第三方上下文中所需的 cookie，应确保将它们声明为`SameSite=None; Secure`。

## <a name="learn-more"></a>了解更多

[SameSite 示例](https://github.com/GoogleChromeLabs/samesite-examples)

[SameSite cookie 食谱](https://web.dev/samesite-cookie-recipes/)

[已知不兼容客户端]( https://www.chromium.org/updates/same-site/incompatible-clients)

[开发人员：为新 SameSite 准备就绪 = 无;安全 Cookie 设置](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)

**OpenId Connect 影响**<br>
[ASP.NET 和 ASP.NET Core 中即将推出的 SameSite Cookie 更改](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
