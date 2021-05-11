---
title: 'Microsoft Teams 2020 更新 (和 SameSite cookie) '
author: laujan
description: 描述 SameSite Cookie 的属性
keywords: cookie 属性 samesite
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: 1841e349f3da61c6f8077e5a56874989aa6212ca
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101812"
---
# <a name="microsoft-teams-and-the-samesite-cookie-attribute-2020-update"></a>Microsoft Teams 2020 更新 (和 SameSite cookie) 

## <a name="cookies-in-brief"></a>简短 Cookie

 Cookie 是文本字符串，从网站发送，并且由 Web 浏览器存储在计算机上。 它们通常用于身份验证和个性化设置，例如，重新调用有状态的信息、保留用户设置、记录浏览活动以及显示相关广告。 Cookie 始终链接到特定域，并且可能由各方安装。 它们按以下方式分类：

 |Cookie|范围|
 | ------ | ------ |
 |**第一方 Cookie**|第一方 Cookie 由用户访问的网站创建，用于保存数据，如购物车项目、登录凭据 (例如身份验证 cookie) 和其他分析。|
 |**第二方 Cookie**|从技术上说，第二方 Cookie 和第一方 Cookie 相同。 区别在于，数据通过数据合作关系协议（例如， (分析和报告协议Microsoft Teams[第](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference)二方) 。 |
 |**第三方 Cookie**|第三方 Cookie 由用户显式访问的域外的其他域安装，主要用于跟踪 (例如"喜欢"按钮) 、广告服务以及实时聊天。|

### <a name="cookies-and-http-requests"></a>Cookie 和 HTTP 请求

在引入 SameSite 限制之前，当 Cookie 存储在浏览器中时，它们附加到每个 *HTTP* Web 请求，然后由 Set-Cookie HTTP 响应标头发送到服务器。 可以预测，该性能可能会引入安全漏洞，如跨站点请求伪造和 CSRF (攻击) 攻击。 *请参阅* [HTTP Cookie。](https://developer.mozilla.org/docs/Web/HTTP/Cookies) SameSite 组件通过 SetCookie 标头中的实现和管理缓解了曝光。

### <a name="samesite-attribute-initial-release"></a>SameSite 属性：初始版本

Google Chrome 版本 51 引入了 SetCookie SameSite 规范作为 *可选* 属性。 从内部版本 17672 开始，Windows 10为浏览器引入了 SameSite [cookie Microsoft Edge支持](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/)。

开发人员可以选择不将 SameSite Cookie 属性添加到 SetCookie 标头，或者他们可以通过以下两个设置之一添加该属性 *：Lax* 和 *Strict*。 未启用的 SameSite 属性被视为默认状态。

## <a name="samesite-cookie-attribute-2020-release"></a>SameSite Cookie 属性：2020 版本

Chrome 80 计划于 2020 年 2 月发布，引入了新的 Cookie 值，并默认实施 Cookie 策略。 可以将三个值传递到更新的 SameSite 属性 *：Strict、Lax* 或 *None*。  未指定 SameSite 属性的 Cookie 将默认为 `SameSite=Lax` 。

|设置 | 强制 | 值 |属性规范 |
| -------- | ----------- | --------|--------|
| **Lax**  | Cookie 仅在第一方上下文中和HTTP GET 请求中自动发送。 SameSite Cookie 将在跨站点子请求（如调用加载图像或 iframe）上被保留，但在用户从外部网站导航到 URL 时（例如，通过以下链接）发送。| **默认** |`Set-Cookie: key=value; SameSite=Lax`|
| **Strict** |浏览器仅发送来自将 cookie 设置为 (的网站的第一方上下文请求的) 。 如果请求来自与当前位置不同的 URL，则不发送任何用 属性标记 `Strict` 的 Cookie。| 可选 |`Set-Cookie: key=value; SameSite=Strict`|
| **无** | Cookie 将在第一方上下文和跨源请求中发送;但是，该值必须显式设置为 ，并且所有浏览器请求都必须遵循 HTTPS 协议并包括需要加密连接 **`None`**  **`Secure`** 的属性。 不满足该要求的 Cookie 将 **被拒绝**。 <br/>**这两个属性是必需项**。 如果 **`None`** 未指定 HTTPS 协议或未指定 HTTPS 协议，将拒绝第 **`Secure`**  三方 Cookie。| 可选，但如果已设置，则 HTTPS 协议是必需的。 |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="teams-implications-and-adjustments"></a>Teams含义和调整

1. 为 Cookie 启用相关的 SameSite 设置，并验证应用和扩展是否继续在 Teams。
1. 如果你的应用或扩展失败，在 Chrome 80 版本之前进行必要的修复。
1. 如果 Microsoft 内部合作伙伴需要此问题详细信息或帮助，可以加入以下团队 <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47> ：。

> [!NOTE]
> 为获得最佳方案，建议您始终设置 SameSite 属性以反映 Cookie 的预定用途。 不要依赖于默认浏览器行为。 有关详细信息，请参阅开发人员[：为新的 SameSite=None 做好准备;安全 Cookie 设置](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)。

### <a name="tabs-task-modules-and-message-extensions"></a>选项卡、任务模块和邮件扩展

* Teams选项卡用于嵌入在顶级或第一方上下文中 `<iframes>` 查看的内容。
* 任务模块允许你在 Teams 应用程序中创建模式弹出体验。 与选项卡类似，模式窗口在当前页面内打开。
* 消息扩展允许您将扩充的内容插入到来自外部资源的聊天消息中。

当网站显示在 中时，嵌入内容使用的任何 Cookie 都将被视为第三方 `<iframe>` 。 此外，如果页面上的任何远程资源依赖于通过请求和标记、外部字体和个性化内容发送的 Cookie，则必须确保这些已标记为跨网站使用，例如或确保已进行回退。 `<img>` `<script>` `SameSite=None; Secure`

### <a name="authentication"></a>身份验证

* 如果需要对选项卡中的嵌入内容页进行身份验证，则需要使用基于 Web 的身份验证流。
* 基于 Web 的身份验证流还可用于配置页面、任务模块或邮件扩展。
* 你可以将基于 Web 的身份验证流用于需要使用任务模块的对话机器人。

根据更新的 SameSite 限制，如果链接派生自外部网站，则浏览器不会将 Cookie 添加到已经过身份验证的网站。 你将需要确保你的身份验证 Cookie 标记为跨站点使用，或者确保 `SameSite=None; Secure` 回退已到位。

### <a name="android-system-webview"></a>Android System WebView

Android WebView 是允许 Android 应用显示 Web 内容的 Chrome 系统组件。 尽管新限制将成为默认限制，但从 Chrome 80 开始，不会立即在 WebView 上强制执行这些限制。 将来将应用这些策略。 为进行准备，Android 允许本机应用直接通过[CookeManager API 设置 Cookie：](https://developer.android.com/reference/android/webkit/CookieManager)

* 对于仅在第一方上下文中需要的 Cookie，应根据需要将其声明为 `SameSite=Lax` 或 `SameSite=Strict` 。
* 对于第三方上下文中所需的 Cookie，应确保它们声明为 `SameSite=None; Secure` 。

## <a name="learn-more"></a>了解详细信息

* [SameSite 示例](https://github.com/GoogleChromeLabs/samesite-examples)

* [SameSite Cookie 食谱](https://web.dev/samesite-cookie-recipes/)

* [已知不兼容的客户端]( https://www.chromium.org/updates/same-site/incompatible-clients)

* [开发人员：为新的 SameSite=None 做好准备;安全 Cookie 设置](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)

**OpenId 连接影响**<br>
[即将在网站和网站 ASP.NET ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
