---
title: Microsoft 团队中的自定义选项卡是什么？
author: laujan
description: Microsoft 团队平台上的自定义选项卡概述
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: f338387e658733981c16b36ed2a05c15132fc87c
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651879"
---
# <a name="what-are-tabs"></a>什么是选项卡？

通过选项卡，您可以在团队中嵌入基于 web 的内容。 它们是指向应用程序清单中声明的域的简单 iframe，可以是团队频道、组聊天或个人应用程序的一部分。 *请参阅*[团队 JAVASCRIPT 客户端 SDK](/javascript/api/overview/msteams-client)。

> [!NOTE]
> Chrome 80 引入了新的 cookie 值，并默认实施了 cookie 策略。 建议您为 cookie 设置预期用途，而不是依赖于默认浏览器行为。 *请参阅* [SameSite cookie 属性 (2020 update) ](../../resources/samesite-cookie-update.md)。

"团队：频道/组" 和 "个人" 选项卡中有两种类型的选项卡。 频道/组选项卡可将内容传递到频道和组聊天，这是在专门的基于 web 的内容周围创建协作空间的绝佳方式。 个人选项卡以及个人范围内的 bot 是个人应用程序的一部分，用于与单个用户的交互。 可以将它们固定到左侧导航栏以方便访问。

## <a name="user-scenarios"></a>用户方案

**方案：** 将现有的基于 web 的资源引入团队中。 \
**示例：** 您在团队应用程序中创建了一个个人选项卡，用于向用户提供信息性企业网站。

**方案：** 将支持页面添加到团队 bot 或邮件扩展。 \
**示例：** 您可以为用户创建向用户提供 "帮助" 和 "帮助" 网页内容的个人选项卡。

**方案：** 提供对用户定期与协作对话和协作进行交互的项目的访问。 \
**示例：** 您可以创建一个通道/组选项卡，其中包含对各个项目的深层链接。

## <a name="how-do-tabs-work"></a>选项卡如何工作？

自定义选项卡在应用程序包的应用部件清单（manifest）中声明。 对于您要在应用程序中包含为选项卡的每个网页，定义一个 URL 和一个作用域。 此外，还需要将 [团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 添加到页面，并在 `microsoftTeams.initialize()` 加载页面后调用。 如果这样做，将告知团队显示您的页面，使您可以访问特定于团队的信息 (例如，如果团队客户端运行的是深色主题) ，并允许您根据结果执行操作。

无论您是否选择在频道/组或个人作用域中公开您的选项卡，您都需要在选项卡中提供一个 IFramed HTML [内容页](~/tabs/how-to/create-tab-pages/content-page.md) 。对于 "个人" 选项卡，将通过数组中的属性直接在清单中设置内容 URL `contentUrl` `staticTabs` 。 您的选项卡的内容将对所有用户都相同。

对于频道/组选项卡，还需要创建一个额外的配置页，使用户可以配置内容页面 URL，通常是使用 URL 查询字符串参数为该上下文加载相应的内容。 这是因为您的频道/组选项卡可以添加到多个不同的团队或组聊天。 在每次后续安装中，您的用户将能够配置选项卡，以便根据需要定制体验。 当用户添加选项卡或配置选项卡时，会将 URL 与团队 UI 中显示的选项卡相关联。 配置选项卡只是将其他参数添加到该 URL。 例如，在添加 "Azure DevOps 板" 选项卡时，"配置" 页允许您选择选项卡将加载的板。 配置页面 URL 由  `configurationUrl` `configurableTabs` 应用程序清单中的数组中的属性指定。

每个应用最多可以有一个通道/组选项卡和最多16个个人选项卡。

## <a name="lesser-known-tab-features"></a>较少的已知选项卡功能

* 如果将选项卡添加到也具有 bot 的应用程序中，则也会将 bot 添加到团队中。
* 对当前用户的 Azure Active Directory ID 的感知。
* 用户的区域设置感知以指示语言 (例如， `en-us`) 。
* SSO 功能（如果支持）。
* 可以使用 bot 或应用程序通知深入链接到选项卡或服务 (中的子实体，例如，单个工作项) 。
* 通过选项卡中的链接打开任务模块的功能。
* 在选项卡中重用 SharePoint web 部件。

## <a name="tabs-on-mobile"></a>移动设备上的选项卡

如果选择在工作组移动客户端上显示 "频道/组" 选项卡，则该 `setSettings()` 配置必须具有该属性的值 `websiteUrl` (请参阅下) 。 个人选项卡当前可在 [开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中使用。 将很快发布对移动客户端上的选项卡的完全支持。 若要准备更新，应按照移动选项卡 [上的选项卡指南中](~/tabs/design/tabs-mobile.md) 的步骤创建选项卡。

## <a name="learn-more"></a>了解详细信息

* [规划应用程序](../../concepts/extensibility-points.md)
* [生成应用程序](../../concepts/building-an-app.md)
* [部署应用程序](../../concepts/deploy-and-publish/overview.md)
