---
title: 了解选项卡要求
author: laujan
description: 每个选项卡Microsoft Teams都必须遵守这些要求。
keywords: teams 选项卡组频道可配置
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: f45bfc8831eb6dca660df3307bf875b7ad9fbf1e
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630402"
---
# <a name="tab-requirements"></a>选项卡要求

Teams选项卡必须遵守以下要求：

* 必须允许通过 X-Frame-Options 和/或 Content-Security-Policy HTTP 响应标头在 iFrame 中提供选项卡页。
  * 设置标头： `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * 对于Internet Explorer 11 兼容性，也 `X-Content-Security-Policy` 进行设置。
  * 或者，设置标头 `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。 此标头已弃用，但仍受大多数浏览器支持。
* 通常，作为防止点击攻击的一种安全措施，登录页不会呈现在 iFrame 中。 因此，身份验证逻辑需使用重定向方法。 例如，使用基于令牌或基于 Cookie 的身份验证。

> [!NOTE]
> Chrome 80 计划于 2020 年初发布，引入了新的 Cookie 值，并默认实施 Cookie 策略。 建议设置 Cookie 的预定用途，而不是依赖默认浏览器行为。 有关详细信息，请参阅 [SameSite cookie attribute (2020 update) ](../../resources/samesite-cookie-update.md)。

* 浏览器遵守同源策略限制，该限制阻止网页向与提供网页的域不同的域提出请求。 但是，您可能需要将配置或内容页面重定向到另一个域或子域。 当加载或与选项卡通信时，跨域导航逻辑应允许 Teams 客户端针对应用程序清单中的静态 validDomains 列表验证源。

* 若要创建无缝体验，应基于客户端的主题、设计和意图Teams设置选项卡样式。 通常，当构建选项卡以解决特定需求并专注于一小组任务或与选项卡的通道位置相关的数据子集时，选项卡效果最佳。

* 在内容页中，添加对使用脚本标记[Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)的引用。 加载页面后，调用 `microsoftTeams.initialize()` 。 如果未显示，则不显示您的页面。

* 若要在移动客户端上进行身份验证，必须将 JavaScript SDK Teams至少升级到版本 1.4.1。

* 如果您选择让频道或组选项卡显示在Teams客户端上，则配置必须具有 `setSettings()` `websiteUrl` 属性的值。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 Yeoman 生成器和 Node.js 的 Yeoman 生成器创建自定义个人Microsoft Teams](~/tabs/quickstarts/create-personal-tab-node-yeoman.md)
