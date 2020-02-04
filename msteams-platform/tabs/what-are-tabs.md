---
title: Microsoft 团队中的自定义选项卡是什么？
author: laujan
description: Microsoft 团队平台上的自定义选项卡概述
ms.topic: overview
ms.author: v-laujan
ms.openlocfilehash: 7560a9a7d19ca0182b2f5f45b304a96a0f2dddd4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673442"
---
# <a name="what-are-microsoft-teams-custom-tabs"></a>什么是 Microsoft 团队自定义选项卡？

选项卡是嵌入在 Microsoft 团队中的团队感知网页。 可以将它们添加为团队内的频道的一部分、组聊天或单个用户的个人应用程序。 作为应用程序的一部分，您可以添加自定义选项卡以在团队中嵌入自己的 web 内容，使用[团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)向您的 web 内容添加特定于团队的功能。

> [!NOTE]
> Chrome 80，安排在早期2020中发布，默认引入新的 cookie 值并强加 cookie 策略。 建议您为 cookie 设置预期用途，而不是依赖于默认浏览器行为。 *请参阅* [SameSite cookie 属性（2020更新）](../resources/samesite-cookie-update.md)。

团队中提供了两种类型的选项卡-通道/组和个人。 频道/组选项卡可将内容传递到频道和组聊天，这是在专门的基于 web 的内容周围创建协作空间的绝佳方式。 个人选项卡和个人范围的 bot 是个人应用程序的一部分，且范围限定为单个用户。 可以将它们固定到左侧导航栏以方便访问。

## <a name="tabs-user-scenarios"></a>选项卡用户方案

**方案：** 将现有的基于 web 的资源引入团队中。 \
**示例：** 您在团队应用程序中创建了一个个人选项卡，用于向用户提供信息性企业网站。

**方案：** 将支持页面添加到团队 bot 或邮件扩展。 \
**示例：** 您可以为用户创建向用户提供 "帮助" 和 "帮助" 网页内容的个人选项卡。

**方案：** 提供对用户定期与协作对话和协作进行交互的项目的访问。 \
**示例：** 您可以创建一个通道/组选项卡，其中包含对各个项目的深层链接。

## <a name="how-do-tabs-work"></a>选项卡如何工作？

自定义选项卡在应用程序包的应用部件清单（manifest）中声明。 对于您要在应用程序中包含为选项卡的每个网页，定义一个 URL 和一个作用域。 此外，还需要将[团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)添加到页面，并在加载`microsoftTeams.initialize()`页面后调用。 这样做将告知团队显示您的页面，使您可以访问特定于团队的信息（例如，如果团队客户端运行的是深色主题），并允许您根据结果执行操作。

无论您是否选择在频道/组或个人作用域中公开您的选项卡，您都需要在选项卡中提供一个 IFramed HTML[内容页](~/tabs/how-to/create-tab-pages/content-page.md)。对于 "个人" 选项卡，将通过`contentUrl` `staticTabs`数组中的属性直接在清单中设置内容 URL。 您的选项卡的内容将对所有用户都相同。

对于频道/组选项卡，还需要创建一个额外的配置页，使用户可以配置内容页面 URL，通常是使用 URL 查询字符串参数为该上下文加载相应的内容。 这是因为您的频道/组选项卡可以添加到多个不同的团队或组聊天。 在每次后续安装中，您的用户将能够配置选项卡，以便根据需要定制体验。 例如，在添加 "Azure DevOps 板" 选项卡时，"配置" 页允许您选择选项卡将加载的板。 配置页面 URL 由应用程序清单中`configurationUrl`的`configurableTabs`数组中的属性指定。

最多可以有一个（1）通道/组选项卡，每个应用最多可以有十六个（16）个个人选项卡。

## <a name="mobile-clients"></a>移动客户端

如果选择在工作组移动客户端上显示频道/组选项卡，则`setSettings()`配置必须具有`websiteUrl`属性值（请参阅下文）。 个人选项卡当前可在[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中使用。 将很快发布对移动客户端上的选项卡的完全支持。 若要准备更新，应按照移动选项卡[上的选项卡指南中](~/tabs/design/tabs-mobile.md)的步骤创建选项卡。
