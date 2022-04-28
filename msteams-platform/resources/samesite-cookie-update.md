---
title: SameSite cookie 属性
author: laujan
description: 了解 Cookie 类型，包括 SameSite Cookie、其特性、它们在Teams选项卡、任务模块和消息扩展中的影响，以及它们在Teams中的身份验证
keywords: cookie 属性 samesite
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: 1fbaf46da93a0d7c253f1f5d2ad6c9ae1764565a
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104488"
---
# <a name="samesite-cookie-attribute"></a>SameSite cookie 属性

Cookie 是从网站发送的文本字符串，由 Web 浏览器存储在计算机上。 它们用于身份验证和个性化设置。 例如，Cookie 用于召回有状态信息、保留用户设置、记录浏览活动以及显示相关广告。 Cookie 始终链接到特定域，由各方安装。

## <a name="types-of-cookies"></a>Cookie 类型

Cookie 类型及其相应的范围如下所示：

|Cookie|范围|
| ------ | ------ |
|第一方 Cookie|第一方 Cookie 由用户访问的网站创建。 它用于保存数据，如购物车物品，登录凭据。 例如，身份验证 Cookie 和其他分析。|
|第二方 Cookie|第二方 Cookie 在技术上与第一方 Cookie 相同。 不同的是，数据通过数据合作关系协议与第二方共享。 例如，[Microsoft Teams分析和报告](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference)。 |
|第三方 Cookie|第三方 Cookie 由用户显式访问的域以外的域安装，主要用于跟踪。 例如， **Like** 按钮、广告服务和实时聊天。|

## <a name="cookies-and-http-requests"></a>Cookie 和 HTTP 请求

在引入 SameSite 限制之前，Cookie 存储在浏览器上。 它们附加到每个 HTTP Web 请求，并由 `Set Cookie` HTTP 响应标头发送到服务器。 此方法引入了安全漏洞，例如跨站点请求伪造（称为 CSRF 攻击）。 SameSite 组件通过在 SetCookie 标头中的实现和管理来减少公开。

## <a name="samesite-cookie-attribute-initial-release"></a>SameSite Cookie 属性：初始版本

Google Chrome 版本 51 将规范作为可选属性引入 `SetCookie SameSite` 。 从 Build 17672 开始，Windows 10引入了 [MicrosoftEdge 浏览器的&nbsp;](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/) SameSite Cookie 支持。

可以选择不将 SameSite Cookie 属性添加到 `SetCookie` 标头，也可以使用两个设置之一（ **Lax** 和 **Strict**）添加它。 未实现的 SameSite 属性被视为默认状态。

## <a name="samesite-cookie-attribute-2020-release"></a>SameSite Cookie 属性：2020 版本

Chrome 80 于 2020 年 2 月发布，引入了新的 Cookie 值，并默认实施 Cookie 策略。 三个值将传递到更新后的 SameSite 属性： **Strict**、 **Lax** 或 **None**。 如果未指定，Cookie SameSite 属性默认采用该值 `SameSite=Lax` 。

SameSite Cookie 属性如下所示：

|设置 | 执法 | 值 |属性规范 |
| -------- | ----------- | --------|--------|
| **宽松**  | Cookie 仅在第一 **方** 上下文和 HTTP GET 请求中自动发送。 在跨站点子请求（例如对加载图像或 iframe 的调用）上，将保留 SameSite Cookie。 当用户从外部站点导航到 URL 时发送，例如，通过关注链接发送。| **Default** |`Set-Cookie: key=value; SameSite=Lax`|
| **严格** |浏览器仅发送第一方上下文请求的 Cookie。 这些请求源自设置 Cookie 的站点。 如果请求源自与当前位置不同的 URL，则不会发送带有 `Strict` 该属性标记的 Cookie。| 可选 |`Set-Cookie: key=value; SameSite=Strict`|
| **无** | Cookie 在第一方上下文和跨源请求中发送;但是，必须显式设置 **`None`** 该值，并且所有浏览器请求 **都必须遵循 HTTPS 协议** ，并包含 **`Secure`** 需要加密连接的属性。 不符合该要求的 Cookie 将被 **拒绝**。 <br/>**这两个属性一起是必需的**。 如果  **`None`** 未 **`Secure`**  指定或未使用 HTTPS 协议，则拒绝第三方 Cookie。| 可选，但如果设置，则需要 HTTPS 协议。 |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="teams-implications-and-adjustments"></a>Teams影响和调整

1. 为 Cookie 启用相关的 SameSite 设置，并验证应用和扩展是否继续在Teams中工作。
1. 如果应用或扩展失败，请在 Chrome 80 发布之前进行必要的修复。
1. Microsoft 内部合作伙伴可以加入以下团队以获取有关此问题的详细信息或帮助： <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47>

> [!NOTE]
> 必须设置 SameSite 属性以反映对 Cookie 的预期用途。 不要依赖默认浏览器行为。 有关详细信息，请参阅[开发人员：为新的 SameSite=None 做好准备;保护 Cookie 设置](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)。

### <a name="tabs-task-modules-and-message-extensions"></a>选项卡、任务模块和消息扩展

* Teams选项卡用于`<iframes>`嵌入在顶级或第一方上下文中查看的内容。
* 任务模块允许你在 Teams 应用程序中创建模式弹出体验。 与选项卡类似，模式窗口将在当前页面内打开。
* 消息扩展允许你从外部资源将扩充的内容插入聊天消息中。

当网站显示在 `<iframe>`其中时，嵌入内容使用的任何 Cookie 都被视为第三方。 此外，如果页面上的任何远程资源依赖于发送包含请求 `<img>` 和 `<script>` 标记、外部字体和个性化内容的 Cookie，则必须确保这些资源标记为跨站点使用情况，例如 `SameSite=None; Secure` ，或确保有回退。

### <a name="authentication"></a>身份验证

必须使用基于 Web 的身份验证流进行以下操作：

* 选项卡中的嵌入内容页。
* 配置页、任务模块和消息扩展。
* 具有任务模块的对话机器人。

根据更新后的 SameSite 限制，如果链接派生自外部网站，浏览器不会将 Cookie 添加到已过身份验证的网站。 必须确保针对跨站点使用 `SameSite=None; Secure` 情况标记身份验证 Cookie，或确保有回退。

## <a name="android-system-webview"></a>Android System WebView

Android WebView 是一个 Chrome 系统组件，允许 Android 应用显示 Web 内容。 虽然新限制是默认的，但从 Chrome 80 开始，不会立即在 WebView 上强制实施这些限制。 将来将应用它们。 为了准备，Android 允许本机应用通过 [CookieManager API 直接设置 CookieManager API](https://developer.android.com/reference/android/webkit/CookieManager)。

> [!NOTE]
>
> * 必须根据需要声明第一方 Cookie `SameSite=Lax` `SameSite=Strict`。
> * 必须将第三方 Cookie 声明为 `SameSite=None; Secure`.

## <a name="see-also"></a>另请参阅

* [SameSite 示例](https://github.com/GoogleChromeLabs/samesite-examples)
* [SameSite Cookie 食谱](https://web.dev/samesite-cookie-recipes/)
* [已知的不兼容客户端]( https://www.chromium.org/updates/same-site/incompatible-clients)
* [开发人员：为新的 SameSite=None 做准备；安全 Cookie 设置](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [ASP.NET 和 ASP.NET Core 中即将发生的 SameSite Cookie 更改](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [HTTP Cookie](https://developer.mozilla.org/docs/Web/HTTP/Cookies)
