---
title: 先决条件
author: surbhigupta
description: 本文介绍生成 Microsoft Teams 个人选项卡、频道选项卡或组选项卡的先决条件。了解生成选项卡所需的工具。
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: e1160566f73a63a7de87653900cdc64ba7cb0e52
ms.sourcegitcommit: 87bba925d005eb331d876a0b9b75154f8100e911
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2022
ms.locfileid: "67450413"
---
# <a name="prerequisites"></a>先决条件

在构建 Teams 个人和频道或组选项卡时，请确保遵守以下先决条件：

* 允许使用 X-Frame-Options 和 Content-Security-Policy HTTP 响应标头在 iFrame 中发现选项卡页。
  * 设置标头：`Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * 为实现 Internet Explorer 11 兼容性，请设置 `X-Content-Security-Policy`。
  * 或设置标头 `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`。 此标头已弃用，但仍被大多数浏览器接受。

* 作为防止点击劫持的安全措施，登录页不会在 iFrame 中呈现。 身份验证逻辑需要使用重定向以外的方法。 例如，使用基于令牌或基于 Cookie 的身份验证。

    > [!NOTE]
    > 建议为 Cookie 设置预期用途，而不是依赖默认浏览器行为。 有关详细信息，请参阅 [SameSite cookie 属性](../../resources/samesite-cookie-update.md)。

* 浏览器同源策略限制可防止网页向所服务网页以外的不同域发出请求。 因此，可以将配置或内容页重定向到另一个域或子域。 加载或与选项卡通信时，跨域导航逻辑需要允许 Teams 客户端根据应用清单中的静态 `validDomains` 列表验证原点。

* 根据 Teams 客户端的主题、设计和意向设置选项卡样式。 在构建选项卡以满足特定需求并专注于一小组任务或与选项卡频道位置相关的数据子集时，选项卡效果最佳。

* 在内容页中，使用脚本标记添加对 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 的引用。 加载页面后，调用 `app.initialize()`，否则不会显示页面。

* 要在移动客户端上使用身份验证，必须升级到 Teams JavaScript SDK 1.4.1 及更高版本。

* 如果选择让频道或组选项卡显示在 Teams 移动客户端上，则 `setConfig()` 配置必须具有 `websiteUrl` 属性的值。

* Microsoft Teams 选项卡不支持加载使用自签名证书的 Intranet 网站的功能。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="tools-to-build-tabs"></a>用于生成选项卡的工具

| &nbsp; | 安装 | 用于使用... |
| --- | --- | --- |
| **Required** | &nbsp; | &nbsp; |
| &nbsp; | [Node.js](https://nodejs.org/en/download/) | 后端 JavaScript 运行时环境。 使用最新的 v16 LTS 版本。|
| &nbsp; | [Microsoft Edge](https://www.microsoft.com/edge)（推荐）或 [Google Chrome](https://www.google.com/chrome/) | 包含开发人员工具的浏览器。 |
| &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | JavaScript、TypeScript 或 SharePoint 框架 (SPFx) 生成环境。 |
| &nbsp; | [Visual Studio 2019](https://visualstudio.com/download)、**ASP.NET 和 web 开发** 或 **.NET Core 跨平台开发** 工作负载 | .NET。 你可以安装 2019 Visual Studio 的免费社区版。 |
| &nbsp; | [Git](https://git-scm.com/downloads) | 使用 GitHub 中示例应用存储库的 Git。 |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/download-app) | 通过聊天、会议、通话等应用与每一位同事进行协作的 Microsoft Teams - 一个地方完成所有操作。 |
| &nbsp; | [ngrok](https://ngrok.com/download) | Ngrok 是反向代理软件工具。 Ngrok 创建通向本地运行 Web 服务器的公开可用 HTTPS 终结点的隧道。 在计算机上当前会话期间，服务器的 Web 终结点可用。 当计算机关机或进入睡眠状态时，服务将不再可用。 |
| &nbsp; | [Teams 开发人员门户](https://dev.teams.microsoft.com/) | 基于 Web 的门户，用于配置、管理和分发 Teams 应用，包括组织或 Teams 应用商店。 |

### <a name="build-your-teams-tab"></a>生成 Teams 选项卡

现在，让我们生成选项卡。但首先请选择要生成的选项卡：

> [!div class="nextstepaction"]
> [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
> [!div class="nextstepaction"]
> [生成频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>另请参阅

* [Teams 选项卡](~/tabs/what-are-tabs.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)
