---
title: 什么是自定义选项卡Teams？
author: laujan
description: 自定义选项卡在 Teams 概述
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 21499a4e18acee369b4b1bda6184e4b14b6262ec
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52629968"
---
# <a name="microsoft-teams-tabs"></a>Microsoft Teams 选项卡

选项卡是Teams网页中嵌入的可感知Microsoft Teams。 它们是简单的 HTML <iframe 标记，这些标记指向在应用程序清单中声明的域，并可以添加为单个用户的团队、群聊或个人应用中的频道的一 \> 部分。 可以将自定义选项卡与你的应用一起，以将自己的 Web 内容嵌入Teams或Teams Web 内容添加特定于 Web 的功能。 有关详细信息，请参阅[javaScript Teams SDK。](/javascript/api/overview/msteams-client)

有两种类型的选项卡可用于Teams频道/组和个人。 频道/组选项卡将内容传送给频道和群聊，是围绕基于 Web 的专用内容创建协作空间的一种很好的方法。 个人选项卡和个人范围的自动程序是个人应用的一部分，范围为单个用户。 它们可固定到左侧导航栏，便于访问。

## <a name="tab-features"></a>选项卡功能

> [!div class="checklist"]
>
> * 如果将选项卡添加到同样具有自动程序的应用，则自动程序也会添加到团队。
> * 了解Azure Active Directory (Azure AD) 当前用户的 ID。
> * 用户用于指示语言（即 ）区域设置感知 `en-us` 。 
> * 单一登录 (SSO) 功能（如果受支持）。
> * 能够使用机器人或应用通知深层链接到选项卡或服务中的子实体，例如单个工作项。
> * 从选项卡内的链接打开任务模块的能力。
> * 在选项卡SharePoint Web 部件重用。

## <a name="tabs-user-scenarios"></a>选项卡用户方案

**应用场景：** 将基于 Web 的现有资源引入Teams。 \
**示例：** 在向用户显示信息Teams个人选项卡的应用中创建个人选项卡。

**应用场景：** 向自动程序或消息传递Teams添加支持页面。 \
**示例：** 创建个人选项卡，为用户提供 *关于* 网页的内容和帮助网页内容。

**应用场景：** 提供对用户定期与之交互的项目的访问权限，以便进行协作对话与协作。 \
**示例：** 创建一个通道/组选项卡，该选项卡具有到各个项目的深层链接。

## <a name="understand-how-tabs-work"></a>了解选项卡如何工作

自定义选项卡在应用包的应用清单中声明。 对于希望作为选项卡包含在应用中的每个网页，可定义 URL 和范围。 此外，你需要将 Teams [JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)添加到页面，并加载 `microsoftTeams.initialize()` 页面后调用。 这样做将Teams显示你的页面，让你能够访问 Teams 特定信息 (例如，如果 Teams 客户端正在运行深色主题 *) ，* 并允许你根据结果采取措施。

无论你选择在频道/组还是个人范围内公开选项卡，都需要在选项卡<iframe \> HTML 内容页面。 [](~/tabs/how-to/create-tab-pages/content-page.md)对于个人选项卡，内容 URL 直接在Teams清单中通过 `contentUrl` 数组中的 属性 `staticTabs` 进行设置。 对于所有用户，选项卡的内容都相同。

对于频道/组选项卡，您还需要创建一个附加配置页面，以便用户能够配置内容页 URL，通常使用 URL 查询字符串参数加载该上下文的适当内容。 这是因为频道/组选项卡可以添加到多个不同的团队或群组聊天中。 每次后续安装时，用户将能够配置选项卡，从而允许您根据需要定制体验。 当用户添加或配置选项卡时，URL 与用户界面中呈现的选项卡Teams关联。 配置选项卡只是向该 URL 添加其他参数。 例如，当您添加"Azure Boards"选项卡时，配置页允许您选择将加载该选项卡的板。 配置页面 URL 由应用清单  `configurationUrl` 的 `configurableTabs` 数组中的 属性指定。

你可以有多个频道或组选项卡，每个应用最多有 16 个个人选项卡。

## <a name="mobile-considerations"></a>移动注意事项

如果您选择让频道或组选项卡显示在Teams客户端上，则配置必须具有 `setSettings()` `websiteUrl` 属性的值。 为了确保最佳的用户体验，在创建选项卡时，必须遵循针对[](~/tabs/design/tabs-mobile.md)移动选项卡的指南。 通过[应用商店分发Teams](~/concepts/deploy-and-publish/appsource/publish.md)对移动客户端具有单独的审批流程。 此类应用的默认行为如下所示：

| **应用功能** | **应用获得批准时的行为** | **应用未获得批准时的行为** |
| --- | --- | --- |
| **个人选项卡** | 应用显示在移动客户端的底部栏中。 选项卡在 Teams 中打开。 | 应用不显示在移动客户端的底部栏中。 |
| **频道和组选项卡** | 选项卡使用 在 Teams 客户端中打开 `contentUrl` 。 | 选项卡使用 在 Teams 客户端外部的浏览器中打开 `websiteUrl` 。 |

> [!NOTE]
>
> 应用的默认行为仅在通过应用商店分发时Teams适用。 默认情况下，所有选项卡在 Teams 中打开。
> 若要开始对应用进行移动友好评估，请通过 teamsubm@microsoft.com 与应用详细信息联系。

## <a name="see-also"></a>另请参阅

* [请求设备权限](../concepts/device-capabilities/native-device-permissions.md)
* [集成媒体功能](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [集成 QR 或条形码扫描仪](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [集成位置功能](../concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [选项卡要求](~/tabs/how-to/tab-requirements.md)
