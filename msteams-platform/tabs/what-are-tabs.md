---
title: 什么是团队中的自定义选项卡？
author: laujan
description: 团队平台上的自定义选项卡概述
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 67b509e7d4f71fe6b597a22bb9141f51dc8284ab
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "48209772"
---
# <a name="what-are-microsoft-teams-custom-tabs"></a>什么是 Microsoft 团队自定义选项卡？

选项卡是嵌入在 Microsoft 团队中的团队感知网页。 它们是指向应用程序清单中声明的域的简单 iframe，可以作为单个用户的团队中的频道的一部分添加，也可以添加到组聊天或作为个人应用程序。 您可以将自定义选项卡包含在您的应用程序中，以在工作组中嵌入自己的 web 内容，并向 web 内容中添加特定于团队的功能。 *请参阅*[团队 JAVASCRIPT 客户端 SDK](/javascript/api/overview/msteams-client)。

> [!NOTE]
> Chrome 80，安排在早期2020中发布，默认引入新的 cookie 值并强加 cookie 策略。 建议您为 cookie 设置预期用途，而不是依赖于默认浏览器行为。 *请参阅* [SameSite cookie 属性 (2020 update) ](../resources/samesite-cookie-update.md)。

团队中提供了两种类型的选项卡-通道/组和个人。 频道/组选项卡可将内容传递到频道和组聊天，这是在专门的基于 web 的内容周围创建协作空间的绝佳方式。 个人选项卡和个人范围的 bot 是个人应用程序的一部分，且范围限定为单个用户。 可以将它们固定到左侧导航栏以方便访问。

## <a name="lesser-known-tab-features"></a>较低的已知选项卡功能

> [!div class="checklist"]
>
> * 如果将某个选项卡添加到也具有 bot 的应用程序中，则也会将该 bot 添加到团队中。
> * 感知当前用户的 AAD ID。
> * 用户的区域设置感知以指示语言，即， `en-us` 。 
> * SSO 功能（如果支持）。
> * 能够使用 bot 或应用程序通知深入链接到选项卡或服务内的子实体（例如，单个工作项）。
> * 通过选项卡中的链接打开任务模块的功能。
> * 在选项卡中重用 SharePoint web 部件。

## <a name="tabs-user-scenarios"></a>选项卡用户方案

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

最多可以有一个 (1) 频道/组选项卡，每个应用最多可以有十六个 (16) 个人选项卡。

## <a name="mobile-clients"></a>移动客户端

如果选择在工作组移动客户端上显示 "频道/组" 选项卡，则 `setSettings()` 配置必须具有该属性的值 `websiteUrl` 。 为了确保获得最佳用户体验，在创建选项卡时，应遵循 [移动电话上的选项卡指南](~/tabs/design/tabs-mobile.md) 。
