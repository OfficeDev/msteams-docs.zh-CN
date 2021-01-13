---
title: Teams 中的自定义选项卡是什么？
author: laujan
description: Teams 平台上的自定义选项卡概述
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 64c6e44177f1fb598895f748dbd0ec1c0b1e3aa1
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797888"
---
# <a name="what-are-microsoft-teams-tabs"></a>什么是 Microsoft Teams 选项卡？

选项卡是 Microsoft Teams 中嵌入的可感知 Teams 的网页。 它们是简单的 HTML <iframe 标记，指向在应用程序清单中声明的域，并可以添加为单个用户团队、群聊或个人应用中的频道的一 \> 部分。 你可以将自定义选项卡与你的应用一起，以在 Teams 中嵌入自己的 Web 内容或向 Web 内容添加特定于 Teams 的功能。 *请参阅* [Teams JavaScript 客户端 SDK。](/javascript/api/overview/msteams-client)

> [!NOTE]
> 计划于 2020 年初发布的 Chrome 80 引入了新的 Cookie 值，并默认实施 Cookie 策略。 建议您设置 Cookie 的预定用途，而不是依赖默认浏览器行为。 *请参阅* [SameSite cookie 属性 (2020 update) 。](../resources/samesite-cookie-update.md)

Teams 中提供两种类型的选项卡： 频道/组和个人。 频道/组选项卡向频道和群聊提供内容，是围绕基于 Web 的专用内容创建协作空间的一种很好的方法。 个人选项卡和个人范围的自动程序是个人应用的一部分，并且范围为单个用户。 它们可固定到左侧导航栏，便于访问。

## <a name="lesser-known-tab-features"></a>不太已知的选项卡功能

> [!div class="checklist"]
>
> * 如果将选项卡添加到同样具有自动程序的应用，则自动程序也会添加到团队中。
> * Azure Active Directory (Azure AD) 当前用户的 ID。
> * 用于指示语言（例如，）的用户区域设置感知 `en-us` 。 
> * 单一登录 (SSO) 功能（如果受支持）。
> * 能够使用机器人或应用通知深层链接到选项卡或服务中的子实体，例如单个工作项。
> * 从选项卡中的链接打开任务模块的能力。
> * 在选项卡中重用 SharePoint Web 部件。

## <a name="tabs-user-scenarios"></a>选项卡用户方案

**方案：** 将现有的基于 Web 的资源引入 Teams 中。 \
**示例：** 在 Teams 应用中创建个人选项卡，向用户显示信息性公司网站。

**方案：** 将支持页面添加到 Teams 自动程序或消息传递扩展。 \
**示例：** 创建个人选项卡，向 *用户提供有关* 网页 *内容* 并帮助用户。

**方案：** 提供对用户定期交互的项目的访问权限，以便进行协作对话和协作。 \
**示例：** 创建一个通道/组选项卡，其深层链接到各个项目。

## <a name="how-do-tabs-work"></a>选项卡如何工作？

自定义选项卡在应用包的应用清单中声明。 对于要作为选项卡包含在应用中的每个网页，定义一个 URL 和一个范围。 此外，你需要将 Teams [JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 添加到你的页面，并加载 `microsoftTeams.initialize()` 页面后调用。 这样做将告诉 Teams 显示你的页面、授予你访问特定于 Teams 的信息 (例如，如果 Teams 客户端运行的是深色主题 *) ，* 并允许你根据结果采取措施。

无论是选择在频道/组还是个人范围内公开选项卡，都需要在选项卡中<iframe \> HTML 内容页。 [](~/tabs/how-to/create-tab-pages/content-page.md)对于个人选项卡，内容 URL 直接通过数组中的属性在 Teams `contentUrl` 应用清单 `staticTabs` 中设置。 对于所有用户，选项卡的内容将相同。

对于频道/组选项卡，您还需要创建一个附加配置页面，以允许用户配置内容页 URL，通常使用 URL 查询字符串参数来加载该上下文的适当内容。 这是因为可以将频道/组选项卡添加到多个不同的团队或群组聊天中。 每次后续安装时，用户将能够配置选项卡，从而根据需要定制体验。 当用户添加或配置选项卡时，URL 与 Teams UI 中呈现的选项卡相关联。 配置选项卡只是向该 URL 添加其他参数。 例如，当你添加 Azure 板选项卡时，配置页允许你选择该选项卡将加载的板。 配置页面 URL 由应用清单  `configurationUrl` 中 `configurableTabs` 数组中的属性指定。

每个应用最多只能有一 (1) 频道/组选项卡 (16) 16 个个人选项卡。

## <a name="mobile-clients"></a>移动客户端

如果你选择让频道或组选项卡显示在 Teams 移动客户端上，则配置必须具有 `setSettings()` 属性的值 `websiteUrl` 。 为了确保最佳的用户体验，在创建选项卡时，必须遵循移动[](~/tabs/design/tabs-mobile.md)选项卡指南。 通过 [Appsource 分发的应用](~/concepts/deploy-and-publish/appsource/publish.md) 对移动客户端具有单独的审批流程。 此类应用的默认行为如下所示：

| **应用功能** | **应用通过审批时的行为** | **应用未获得批准时的行为** |
| --- | --- | --- |
| **静态选项卡** | 应用显示在移动客户端的底部栏中。 选项卡在 Teams 客户端中打开。 | 应用程序不显示在移动客户端的底部栏中。 |
| **可配置选项卡** | The tab opens in the Teams client using `contentUrl` . | 选项卡将在 Teams 客户端外部的浏览器中使用 `websiteUrl` 打开。 |


>[!NOTE]
>
>- 应用的默认行为仅在通过 AppSource 分发时适用。 对于通过其他分发方法分发的应用程序，没有 [审批流程](~/concepts/deploy-and-publish/overview.md)。 默认情况下，所有选项卡在 Teams 客户端中打开。
>- 若要启动应用评估，实现移动友好功能，teamsubm@microsoft.com应用详细信息进行联系。


> [!div class="nextstepaction"]
> [了解更多信息：请求设备权限](/concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
>[了解更多信息：相机和图像库权限](/concepts/device-capabilities/mobile-camera-image-permissions.md)
