---
title: 先决条件
author: surbhigupta
description: 每个选项卡Microsoft Teams都必须遵守这些要求。
keywords: teams 选项卡组频道可配置
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 72fd6e291d282787ad406e2677c2e3ef58a4fe47
ms.sourcegitcommit: 781f34af2a95952bf437d0b7236ae995f4e14a08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2021
ms.locfileid: "60948605"
---
# <a name="prerequisites"></a>先决条件

Teams选项卡必须遵循以下先决条件：

* 必须允许选项卡页使用 X-Frame-Options 和 Content-Security-Policy HTTP 响应标头显示在 iFrame 中。
  * 设置标头： `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * 对于Internet Explorer 11 兼容性，请设置 `X-Content-Security-Policy` 。
  * 或者，设置标头 `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。 此标头已弃用，但仍被大多数浏览器接受。

* 通常，作为防止点击劫持的安全措施，登录页不会呈现在 iFrame 中。 身份验证逻辑需使用重定向方法。 例如，使用基于令牌或基于 Cookie 的身份验证。

    > [!NOTE]
    > Chrome 80 计划于 2020 年初发布，引入了新的 Cookie 值，并默认实施 Cookie 策略。 建议您设置 Cookie 的预定用途，而不是依赖默认浏览器行为。 有关详细信息，请参阅 [SameSite cookie 属性](../../resources/samesite-cookie-update.md)。

* 浏览器遵守同源策略限制。 它会阻止网页向与所提供网页不同的域提出请求。 但是，您可以将配置或内容页重定向到另一个域或子域。 当加载或与选项卡通信时，跨域导航逻辑必须允许Teams客户端针对应用清单中的静态列表 `validDomains` 验证源。

* 您必须基于客户端的主题、Teams设计及意图设置选项卡的样式。 通常，当选项卡专为满足特定需求而构建，并且侧重于一小组任务或与选项卡的通道位置相关的数据子集时，选项卡运行效果最佳。

* 在内容页中，添加对使用脚本标记[Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)的引用。 加载页面后，调用 `microsoftTeams.initialize()` ，否则不显示页面。

* 若要在移动客户端上进行身份验证，必须将 Teams JavaScript SDK 升级到至少版本 1.4.1。

* 如果您选择让频道或组选项卡显示在Teams客户端上，则配置必须具有 `setSettings()` `websiteUrl` 属性的值。

* MS Teams 选项卡不支持加载使用自签名证书的 Intranet 网站。

## <a name="tools-you-can-use-to-build-tabs"></a>可用于生成选项卡的工具
* [Visual Studio Code 的Teams工具包](../../toolkit/visual-studio-code-overview.md)
* [Visual Studio 的Teams工具包](../../toolkit/visual-studio-overview.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)

## <a name="see-also"></a>另请参阅

* [Teams选项卡](~/tabs/what-are-tabs.md)
* [使用 JavaScript 生成第一个应用](../../get-started/first-app-react.md)
* [使用 Blazor 生成第一个应用](../../get-started/first-app-blazor.md)
* [使用 SPFx 生成第一个应用](../../get-started/first-app-spfx.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)
