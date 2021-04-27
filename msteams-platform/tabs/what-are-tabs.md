---
title: Teams 中的自定义选项卡是什么？
author: laujan
description: Teams 平台上的自定义选项卡概述
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 4ce17f4d26abfd4fe21b4ac05bb7269fa39a2f7a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020287"
---
# <a name="what-are-microsoft-teams-tabs"></a>什么是 Microsoft Teams 选项卡？

选项卡是嵌入在 Microsoft Teams 中的 Teams 感知网页。 它们是简单的 HTML <iframe 标记，这些标记指向在应用程序清单中声明的域，并可以添加为单个用户的团队、群聊或个人应用中的频道的一 \> 部分。 你可以将自定义选项卡与你的应用一起，以在 Teams 中嵌入你自己的 Web 内容或将特定于 Teams 的功能添加到你的 Web 内容。 *请参阅* [Teams JavaScript 客户端 SDK。](/javascript/api/overview/msteams-client)

> [!NOTE]
> Chrome 80 计划于 2020 年初发布，引入了新的 Cookie 值，并默认实施 Cookie 策略。 建议设置 Cookie 的预定用途，而不是依赖默认浏览器行为。 *请参阅* [SameSite cookie attribute (2020 update)](../resources/samesite-cookie-update.md)。

Teams 中提供两种类型的选项卡 — 频道/组和个人。 频道/组选项卡将内容传送给频道和群聊，是围绕基于 Web 的专用内容创建协作空间的一种很好的方法。 个人选项卡和个人范围的自动程序是个人应用的一部分，范围为单个用户。 它们可固定到左侧导航栏，便于访问。

## <a name="lesser-known-tab-features"></a>不太已知的选项卡功能

> [!div class="checklist"]
>
> * 如果将选项卡添加到同样具有自动程序的应用，则自动程序也会添加到团队。
> * 了解 Azure Active Directory (Azure AD) 当前用户的 ID。
> * 用户用于指示语言（即 ）区域设置感知 `en-us` 。 
> * 单一登录 (SSO) 功能（如果受支持）。
> * 能够使用机器人或应用通知深层链接到选项卡或服务中的子实体，例如单个工作项。
> * 从选项卡内的链接打开任务模块的能力。
> * 在选项卡内重用 SharePoint Web 部件。

## <a name="tabs-user-scenarios"></a>选项卡用户方案

**应用场景：** 将现有的基于 Web 的资源引入 Teams 中。 \
**示例：** 在 Teams 应用中创建个人选项卡，向用户显示信息性公司网站。

**应用场景：** 将支持页面添加到 Teams 机器人或消息传递扩展。 \
**示例：** 创建个人选项卡，为用户提供 *关于* 网页的内容和帮助网页内容。

**应用场景：** 提供对用户定期与之交互的项目的访问权限，以便进行协作对话与协作。 \
**示例：** 创建一个通道/组选项卡，该选项卡具有到各个项目的深层链接。

## <a name="how-do-tabs-work"></a>选项卡如何工作？

自定义选项卡在应用包的应用清单中声明。 对于希望作为选项卡包含在应用中的每个网页，可定义 URL 和范围。 此外，你需要将 Teams [JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 添加到你的页面，并加载 `microsoftTeams.initialize()` 页面后调用。 这样做将告诉 Teams 显示你的页面，让你访问特定于 Teams 的信息 (例如，如果 Teams 客户端运行的是深色主题 *) ，* 并允许你根据结果采取措施。

无论你选择在频道/组还是个人范围内公开选项卡，都需要在选项卡<iframe \> HTML 内容页面。 [](~/tabs/how-to/create-tab-pages/content-page.md)对于个人选项卡，内容 URL 由 数组中的 属性直接在 Teams `contentUrl` 应用清单 `staticTabs` 中设置。 对于所有用户，选项卡的内容都相同。

对于频道/组选项卡，您还需要创建一个附加配置页面，以便用户能够配置内容页 URL，通常使用 URL 查询字符串参数加载该上下文的适当内容。 这是因为频道/组选项卡可以添加到多个不同的团队或群组聊天中。 每次后续安装时，用户将能够配置选项卡，从而允许您根据需要定制体验。 当用户添加或配置选项卡时，URL 与 Teams UI 中呈现的选项卡相关联。 配置选项卡只是向该 URL 添加其他参数。 例如，当你添加 Azure 版块选项卡时，配置页面允许你选择该选项卡将加载哪一个板。 配置页面 URL 由应用清单  `configurationUrl` 的 `configurableTabs` 数组中的 属性指定。

你可以有多个频道或组选项卡，每个应用最多有 16 个个人选项卡。

## <a name="mobile-clients"></a>移动客户端

如果选择让频道或组选项卡显示在 Teams 移动客户端上，则配置 `setSettings()` 必须具有 `websiteUrl` 属性的值。 为了确保最佳的用户体验，在创建选项卡时，必须遵循针对[](~/tabs/design/tabs-mobile.md)移动选项卡的指南。 通过 [Appsource 分发的应用](~/concepts/deploy-and-publish/appsource/publish.md) 具有单独的移动客户端审批流程。 此类应用的默认行为如下所示：

| **选项卡类型** | **应用行为（如果已针对移动客户端进行优化）** | **应用行为（如果未针对移动客户端进行优化）** |
|:-----|:-----|:-----|
| **静态选项卡** 或个人 **选项卡**|应用显示在移动客户端的底部栏中。 选项卡在 Teams 客户端的应用内 Webview 中打开。 | 应用不会显示在移动客户端中。 |
| **可配置的选项卡** | 选项卡使用 在 Teams 客户端的应用内 Webview 中打开 `contentUrl` 。 | 选择 **"** 选项卡"，使用 `websiteUrl` 设备上默认 Web 浏览器中的 打开内容。 |


> [!NOTE]
>
> * [提交到 AppSource 以在 Teams ](../concepts/deploy-and-publish/overview.md#publish-to-appsource) 上发布的应用将自动进行评估，以响应移动。 对于任何查询，请通过联系 teamsubm@microsoft.com。
> * 对于 [未通过 AppSource](../concepts/deploy-and-publish/overview.md)分发的所有应用，默认情况下，选项卡在 Teams 客户端的应用内 Webview 中打开，并且不需要单独的审批过程。

> [!div class="nextstepaction"]
> [了解更多信息：请求设备权限](../concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
> [了解更多信息：集成媒体功能](../concepts/device-capabilities/mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [了解更多信息：在 Teams 中集成 QR 或条形码扫描仪功能](../concepts/device-capabilities/qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [了解更多信息：在 Teams 中集成位置功能](../concepts/device-capabilities/location-capability.md)
