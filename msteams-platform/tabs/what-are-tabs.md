---
title: 什么是 Teams 中的自定义选项卡？
author: laujan
description: Teams 平台上的自定义选项卡概述
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: af6d0a87fbbb87ae4abf09a2ff53319299f452df
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449218"
---
# <a name="what-are-microsoft-teams-tabs"></a>什么是 Microsoft Teams 选项卡？

选项卡是嵌入在 Microsoft Teams 中的 Teams 感知网页。 它们是简单的 HTML <iframe 标记，指向在应用程序清单中声明的域，并可以添加为单个用户团队、群聊或个人应用中频道的一 \> 部分。 你可以将自定义选项卡与你的应用一起，以在 Teams 中嵌入自己的 Web 内容或向 Web 内容添加特定于 Teams 的功能。 *请参阅* [Teams JavaScript 客户端 SDK。](/javascript/api/overview/msteams-client)

> [!NOTE]
> Chrome 80 计划于 2020 年初发布，引入了新的 Cookie 值，并默认实施 Cookie 策略。 建议为 Cookie 设置预期用途，而不是依赖默认浏览器行为。 *请参阅* [SameSite cookie 属性 (2020 update) 。](../resources/samesite-cookie-update.md)

Teams 中提供了两种类型的选项卡： 频道/组和个人。 频道/组选项卡向频道和群聊提供内容，是围绕基于 Web 的专用内容创建协作空间的一种很好方法。 个人选项卡和个人范围的自动程序是个人应用的一部分，范围为单个用户。 可以固定到左侧导航栏，便于访问。

## <a name="lesser-known-tab-features"></a>不太已知的选项卡功能

> [!div class="checklist"]
>
> * 如果将选项卡添加到同样具有自动程序的应用，则自动程序也会添加到团队。
> * 了解 Azure Active Directory (Azure AD) 当前用户的 ID。
> * 用户区域设置感知以指示语言，例如 `en-us` 。 
> * 单一登录 (SSO) （如果支持）。
> * 能够使用自动程序或应用通知深入链接到选项卡或服务中的子实体，例如单个工作项。
> * 从选项卡内的链接打开任务模块的能力。
> * 在选项卡中重用 SharePoint Web 部件。

## <a name="tabs-user-scenarios"></a>选项卡用户方案

**方案：** 将基于 Web 的现有资源引入 Teams 中。 \
**示例：** 你在 Teams 应用中创建一个向用户显示信息性公司网站的个人选项卡。

**方案：** 将支持页面添加到 Teams 自动程序或消息传递扩展。 \
**示例：** 创建个人选项卡，向用户 *提供有关* 网页 *内容* 并提供帮助。

**方案：** 提供对用户定期与之交互的项目的访问权限，以便进行协作对话和协作。 \
**示例：** 创建一个通道/组选项卡，该选项卡具有指向单个项目的深层链接。

## <a name="how-do-tabs-work"></a>选项卡如何工作？

自定义选项卡在应用包的应用清单中声明。 对于要作为选项卡包含在应用中的每个网页，定义一个 URL 和一个范围。 此外，你需要将 Teams [JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 添加到页面，在页面加载 `microsoftTeams.initialize()` 后调用。 这样做将告诉 Teams 显示你的页面，让你访问特定于 Teams 的信息 (例如，如果 Teams 客户端运行的是深色主题 *) ，* 并允许你根据结果采取措施。

无论你选择在频道/组或个人范围内公开选项卡，都需要在选项卡<iframe HTML 内容 \> 页。 [](~/tabs/how-to/create-tab-pages/content-page.md)对于个人选项卡，内容 URL 由数组中的属性直接在 Teams `contentUrl` 应用清单 `staticTabs` 中设置。 对于所有用户，选项卡的内容将相同。

对于通道/组选项卡，您还需要创建一个附加配置页，允许用户配置内容页 URL，通常使用 URL 查询字符串参数加载该上下文的适当内容。 这是因为你的频道/组选项卡可以添加到多个不同的团队或群聊中。 每次后续安装时，用户将能够配置选项卡，从而根据需要定制体验。 当用户添加或配置选项卡时，URL 与 Teams UI 中呈现的选项卡相关联。 配置选项卡只是向该 URL 添加其他参数。 例如，添加 Azure 板选项卡时，配置页允许你选择该选项卡将加载的板。 配置页面 URL 由应用清单  `configurationUrl` `configurableTabs` 中的数组中的属性指定。

每个应用最多可以有 1 (1) 1 个频道/组选项卡 (16) 16 个个人选项卡。

## <a name="mobile-clients"></a>移动客户端

如果你选择让频道或组选项卡显示在 Teams 移动客户端上，则 `setSettings()` 配置必须具有属性的值 `websiteUrl` 。 为了确保最佳的用户体验，在创建选项卡时，必须遵循移动[](~/tabs/design/tabs-mobile.md)选项卡指南。 通过 [Appsource 分发的应用](~/concepts/deploy-and-publish/appsource/publish.md) 具有单独的移动客户端审批流程。 此类应用的默认行为如下所示：

| **应用功能** | **应用通过审批时的行为** | **应用未获得批准时的行为** |
| --- | --- | --- |
| **静态选项卡** | 应用显示在移动客户端的底部栏中。 选项卡在 Teams 客户端中打开。 | 应用程序不显示在移动客户端的底部栏中。 |
| **可配置选项卡** | 选项卡使用 在 Teams 客户端中打开 `contentUrl` 。 | 该选项卡将在 Teams 客户端外部的浏览器中使用 `websiteUrl` 打开。 |


>[!NOTE]
>
>- 应用的默认行为仅适用于通过 AppSource (Teams 应用商店) 。 对于通过其他分发方法分发的应用，没有 [审批流程](~/concepts/deploy-and-publish/overview.md)。 默认情况下，所有选项卡在 Teams 客户端中打开。
>- 若要启动针对移动友好型应用的评估，请teamsubm@microsoft.com应用详细信息。

> [!div class="nextstepaction"]
> [了解更多信息：请求设备权限](../concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
> [了解更多信息：集成媒体功能](../concepts/device-capabilities/mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [了解更多信息：在 Teams 中集成 QR 或条形码扫描仪功能](../concepts/device-capabilities/qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [了解更多信息：在 Teams 中集成位置功能](../concepts/device-capabilities/location-capability.md)
