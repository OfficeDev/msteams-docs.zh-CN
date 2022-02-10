---
title: SameSite cookie 属性
author: laujan
description: 了解 Cookie 类型，包括 SameSite Cookie、其属性、Teams 选项卡、任务模块和消息传递扩展中的含义，以及 cookie 在 Teams
keywords: cookie 属性 samesite
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: 3c587056821eff3c24358a1dfbf6ecc63351a3c3
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518476"
---
# <a name="samesite-cookie-attribute"></a>SameSite cookie 属性

Cookie 是由网站发送的文本字符串，由 Web 浏览器存储在计算机上。 它们用于身份验证和个性化。 例如，Cookie 用于调用状态信息、保留用户设置、记录浏览活动以及显示相关广告。 Cookie 始终链接到特定域，并且由各方安装。

## <a name="types-of-cookies"></a>Cookie 的类型

Cookie 类型及其相应的范围如下所示：

|Cookie|范围|
| ------ | ------ |
|第一方 Cookie|第一方 Cookie 由用户访问的网站创建。 它用于保存数据（如购物车项目）和登录凭据。 例如，身份验证 Cookie 和其他分析。|
|第二方 Cookie|从技术上说，第二方 Cookie 和第一方 Cookie 相同。 区别在于，通过数据合作关系协议与第二方共享数据。 例如，[Microsoft Teams分析和报告](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference)。 |
|第三方 Cookie|第三方 Cookie 由用户显式访问的域外的其他域安装，主要用于跟踪。 例如， **"喜欢** "按钮、广告服务以及实时聊天。|

## <a name="cookies-and-http-requests"></a>Cookie 和 HTTP 请求

在引入 SameSite 限制之前，Cookie 存储在浏览器中。 它们附加到每个 HTTP Web 请求，并 `Set Cookie` 按 HTTP 响应标头发送到服务器。 此方法引入了安全漏洞，如跨站点请求伪造（称为 CSRF 攻击）。 SameSite 组件通过 SetCookie 标头中的实现和管理减少了曝光。

## <a name="samesite-cookie-attribute-initial-release"></a>SameSite Cookie 属性：初始版本

Google Chrome 版本 51 引入了 `SetCookie SameSite` 规范作为可选属性。 从内部版本 17672 开始，Windows 10 [MicrosoftEdge&nbsp;](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/) 浏览器引入了 SameSite Cookie 支持。

你可以选择不向标头添加 SameSite Cookie `SetCookie` 属性，或者使用 **Lax** 和 Strict 这两个设置之 **一添加它**。 未启用的 SameSite 属性被视为默认状态。

## <a name="samesite-cookie-attribute-2020-release"></a>SameSite Cookie 属性：2020 版本

Chrome 80 于 2020 年 2 月发布，引入了新的 Cookie 值，并默认实施 Cookie 策略。 将三个值传递到更新的 SameSite 属性： **Strict**、 **Lax** 或 **None**。 如果未指定，则 Cookie SameSite 属性默认采用 `SameSite=Lax` 值。
 
SameSite Cookie 属性如下所示：

|设置 | 强制 | 值 |属性规范 |
| -------- | ----------- | --------|--------|
| **Lax**  | Cookie 仅在第一 **方上下文中和** HTTP GET 请求中自动发送。 SameSite Cookie 在跨站点子请求（例如，对加载图像或 iframe 的调用）上被预扣。 当用户从外部网站导航到 URL 时发送，例如，通过以下链接发送。| **默认** |`Set-Cookie: key=value; SameSite=Lax`|
| **Strict** |浏览器仅发送第一方上下文请求的 Cookie。 这些是来自设置 Cookie 的网站的请求。 如果请求的 URL 与当前位置的 URL 不同，则不发送任何用 属性标记 `Strict` 的 Cookie。| 可选 |`Set-Cookie: key=value; SameSite=Strict`|
| **无** | Cookie 在第一方上下文和跨源请求中发送;但是，该值必须显式设置为 **`None`** ，并且所有浏览器请求都必须遵循 **HTTPS** **`Secure`** 协议并包括需要加密连接的属性。 不满足该要求的 Cookie 将 **被拒绝**。 <br/>**这两个属性是必需项**。 如果  **`None`** 未指定 HTTPS **`Secure`**  协议或未指定 HTTPS 协议，则拒绝第三方 Cookie。| 可选，但如果已设置，则 HTTPS 协议是必需的。 |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="teams-implications-and-adjustments"></a>Teams含义和调整

1. 为 Cookie 启用相关的 SameSite 设置，并验证您的应用程序和扩展是否继续在 Teams。
1. 如果你的应用或扩展失败，在 Chrome 80 版本之前进行必要的修复。
1. Microsoft 内部合作伙伴可以加入以下团队，获取此问题详细信息或帮助： <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47>。

> [!NOTE]
> 必须设置 SameSite 属性以反映 Cookie 的预定用途。 不要依赖于默认浏览器行为。 有关详细信息，请参阅开发人员[：为新的 SameSite=None 做好准备;安全 Cookie 设置](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)。

### <a name="tabs-task-modules-and-messaging-extensions"></a>选项卡、任务模块和消息传递扩展

* Teams选项卡用于`<iframes>`嵌入在顶级或第一方上下文中查看的内容。
* 任务模块允许你在 Teams 应用程序中创建模式弹出体验。 与选项卡类似，模式窗口在当前页面内打开。
* 消息扩展允许您将扩充的内容插入到来自外部资源的聊天消息中。

当网站显示在 中时，嵌入内容使用的任何 Cookie 都将被视为第三方 `<iframe>`。 `<img>` `<script>` `SameSite=None; Secure`此外，如果页面上的任何远程资源依赖于随请求和标记、外部字体和个性化内容一起发送的 Cookie，则必须确保它们标记为跨网站使用，例如或确保已进行回退。

### <a name="authentication"></a>身份验证

您必须对以下内容使用基于 Web 的身份验证流：

* 选项卡中的嵌入内容页。
* 配置页面、任务模块和消息扩展。
* 包含任务模块的对话机器人。

根据更新的 SameSite 限制，如果链接派生自外部网站，则浏览器不会将 Cookie 添加到已经过身份验证的网站。 必须确保你的身份验证 Cookie 标记为跨网站 `SameSite=None; Secure` 使用，或确保已进行回退。

## <a name="android-system-webview"></a>Android System WebView

Android WebView 是允许 Android 应用显示 Web 内容的 Chrome 系统组件。 虽然新限制是默认限制，但从 Chrome 80 开始，不会立即在 WebView 上强制执行这些限制。 将来将应用这些策略。 为了做好准备，Android 允许本机应用直接通过 [CookieManager API 设置 Cookie](https://developer.android.com/reference/android/webkit/CookieManager)。

> [!NOTE]
> * 必须在适当时将第一方 Cookie 声明为 `SameSite=Lax` 或 `SameSite=Strict`。
> * 必须将第三方 Cookie 声明为 `SameSite=None; Secure`。

## <a name="see-also"></a>另请参阅

* [SameSite 示例](https://github.com/GoogleChromeLabs/samesite-examples)
* [SameSite Cookie 食谱](https://web.dev/samesite-cookie-recipes/)
* [已知不兼容的客户端]( https://www.chromium.org/updates/same-site/incompatible-clients)
* [开发人员：为新的 SameSite=None 做准备；安全 Cookie 设置](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [ASP.NET 和 ASP.NET Core 中即将发生的 SameSite Cookie 更改](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [HTTP Cookie](https://developer.mozilla.org/docs/Web/HTTP/Cookies)
