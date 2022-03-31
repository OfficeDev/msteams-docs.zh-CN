---
title: 先决条件
author: surbhigupta
description: 每个选项卡Microsoft Teams都必须遵守这些要求。
keywords: teams 选项卡组频道可配置
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: fe72691465ca785cefb6a96c8eb4005a64601a17
ms.sourcegitcommit: 3dc9b539c6f7fbfb844c47a78e3b4d2200dabdad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2022
ms.locfileid: "64571514"
---
# <a name="prerequisites"></a>先决条件

确保在生成个人选项卡和频道或组选项卡Teams满足以下先决条件：

* 允许使用 X-Frame-Options 和 Content-Security-Policy HTTP 响应标头在 iFrame 中发现选项卡页。
  * 设置标头： `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * 对于Internet Explorer 11 兼容性，请设置 `X-Content-Security-Policy`。
  * 或者，设置标头 `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`。 此标头已弃用，但仍被大多数浏览器接受。

* 登录页不会呈现在 iFrame 中，这是防止点击劫持的一项安全措施。 身份验证逻辑需使用重定向方法。 例如，使用基于令牌或基于 Cookie 的身份验证。

    > [!NOTE]
    > 建议您设置 Cookie 的预定用途，而不是依赖默认浏览器行为。 有关详细信息，请参阅 [SameSite cookie 属性](../../resources/samesite-cookie-update.md)。

* 浏览器同源策略限制阻止网页向与所提供网页不同的域提出请求。 因此，您可以将配置或内容页重定向到另一个域或子域。 当加载或与选项卡通信时`validDomains`，跨域导航逻辑需要允许 Teams 客户端针对应用清单中的静态列表验证源。

* 根据客户端的主题Teams设计及意图设置选项卡的样式。 当构建选项卡以解决特定需求并专注于一小组任务或与选项卡的通道位置相关的数据子集时，选项卡效果最佳。

* 在内容页中，添加对使用Microsoft Teams[标记的 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 的引用。 加载页面后，调用 `microsoftTeams.initialize()`，否则不显示页面。

* 若要在移动客户端上进行身份验证，必须升级到 Teams JavaScript SDK 1.4.1 及更高版本。

* 如果选择让频道或组选项卡显示在Teams客户端上`setSettings()``websiteUrl`，则配置必须具有 属性的值。

* Microsoft Teams选项卡不支持加载使用自签名证书的 Intranet 网站。

## <a name="tools-to-build-tabs"></a>用于生成选项卡的工具

| &nbsp; | 安装 | 对于使用... |
| --- | --- | --- |
| **Required** | &nbsp; | &nbsp; |
| &nbsp; | [Node.js](https://nodejs.org/en/download/) | 后端 JavaScript 运行时环境。 使用最新的 v14 LTS 版本。|
| &nbsp; | [Microsoft Edge (](https://www.microsoft.com/edge)推荐) [Google Chrome](https://www.google.com/chrome/) | 具有开发人员工具的浏览器。 |
| &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | JavaScript、TypeScript 或 SharePoint 框架 (SPFx) 生成环境。 |
| &nbsp; | [Visual Studio 2019、](https://visualstudio.com/download)**ASP.NET 和 Web 开发** 或 **.NET Core 跨平台开发** 工作负载 | .NET。 您可以安装 2019 年 Visual Studio免费社区版。 |
| &nbsp; | [Git](https://git-scm.com/downloads) | Git 使用来自应用商店的示例GitHub。 |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/download-app) | Microsoft Teams通过聊天、会议、呼叫等应用与协作的每个人进行协作- 全部在一处。 |
| &nbsp; | [ngrok](https://ngrok.com/download) | Ngrok 是反向代理软件工具。 Ngrok 为本地运行的 Web 服务器的公开可用 HTTPS 终结点创建一个隧道。 您计算机的当前会话期间提供了您的服务器的 Web 终结点。 当计算机关闭或进入睡眠状态时，服务将不再可用。 |
| &nbsp; | [Teams 开发人员门户](https://dev.teams.microsoft.com/) | 基于 Web 的门户，用于配置、管理和分发你的 Teams 应用，包括你的组织或 Teams 商店。 |

### <a name="build-your-teams-tab"></a>生成Teams选项卡

现在，让我们生成选项卡。但首先选择要构建的选项卡：

> [!div class="nextstepaction"]
> [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
> [!div class="nextstepaction"]
> [生成频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>另请参阅

* [Teams选项卡](~/tabs/what-are-tabs.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)