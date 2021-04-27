---
title: 了解选项卡要求
author: laujan
description: Microsoft Teams 中的每个选项卡都必须遵守这些要求。
keywords: teams 选项卡组频道可配置
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8013c10050ae81ada0f2a27576cd43077eafe1e0
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019578"
---
# <a name="tab-requirements"></a>选项卡要求

Teams 选项卡必须遵循以下要求：

* 必须允许通过 X-Frame-Options 和/或 Content-Security-Policy HTTP 响应标头在 iFrame 中提供选项卡页。
  * 设置标头： `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * 对于Internet Explorer 11 兼容性，也 `X-Content-Security-Policy` 进行设置。
  * 或者，设置标头 `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。 此标头已弃用，但仍受大多数浏览器支持。
* 通常，作为防止点击攻击的一种安全措施，登录页不会呈现在 iFrame 中。 因此，身份验证逻辑需要使用重定向策略 (，例如，使用基于令牌或基于 Cookie 的身份验证) 。

> [!NOTE]
> Chrome 80 计划于 2020 年初发布，引入了新的 Cookie 值，并默认实施 Cookie 策略。 建议设置 Cookie 的预定用途，而不是依赖默认浏览器行为。 *请参阅* [SameSite cookie attribute (2020 update)](../../resources/samesite-cookie-update.md)。

* 浏览器遵守同源策略限制，该限制阻止网页向与提供网页的域不同的域提出请求。 但是，您可能需要将配置或内容页面重定向到另一个域或子域。 当加载或与选项卡通信时，跨域导航逻辑应允许 Teams 客户端针对应用清单中的静态 validDomains 列表验证源。

* 若要创建无缝体验，你应基于 Teams 客户端的主题、设计和意图设置选项卡的样式。 通常，当构建选项卡以解决特定需求并专注于一小组任务或与选项卡的通道位置相关的数据子集时，选项卡效果最佳。

* 在内容页中，使用脚本标记添加 [对 Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 的引用。 加载页面后，调用 `microsoftTeams.initialize()` 。 如果未显示，则不显示您的页面。

* 若要在移动客户端上进行身份验证，必须将 Teams JavaScript SDK 至少升级到版本 1.4.1。

* 如果选择让频道或组选项卡显示在 Teams 移动客户端上，则配置 `setSettings()` 必须具有 `websiteUrl` 属性的值。