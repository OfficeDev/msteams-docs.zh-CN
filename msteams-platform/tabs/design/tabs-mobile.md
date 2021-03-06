---
title: 移动设备上的选项卡
description: 介绍在移动设备上实现选项卡的开发人员Microsoft Teams注意事项。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 5053160f2456a5d1c5f68cb74ea3ccc5c5eabca5
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179718"
---
# <a name="tabs-on-mobile"></a>移动设备上的选项卡

生成包含选项卡Microsoft Teams应用时，必须测试选项卡在 Android 和 iOS 客户端上Microsoft Teams运行。 本文概述了必须考虑的一些关键方案。

如果您选择让频道或组选项卡显示在Teams客户端上，则配置必须具有 `setSettings()` `websiteUrl` 属性的值。 为了确保最佳的用户体验，在创建选项卡时，必须遵循本文中针对移动选项卡的指南。

通过[应用商店分发Teams](~/concepts/deploy-and-publish/appsource/publish.md)对移动客户端具有单独的审批流程。 此类应用的默认行为如下所示：

| **应用功能** | **应用获得批准时的行为** | **应用未获得批准时的行为** |
| --- | --- | --- |
| **个人选项卡** | 应用显示在移动客户端的底部栏中。 选项卡在 Teams 中打开。 | 应用不显示在移动客户端的底部栏中。 |
| **频道和组选项卡** | 选项卡使用 在 Teams 客户端中打开 `contentUrl` 。 | 选项卡使用 在 Teams 客户端外部的浏览器中打开 `websiteUrl` 。 |

> [!NOTE]
> * 提交到[AppSource](https://appsource.microsoft.com)以在应用上Teams将自动评估移动响应能力。 对于任何查询，请通过联系 teamsubm@microsoft.com。
> * 对于未通过 AppSource 分发的所有应用，默认情况下，选项卡在 Teams 客户端的应用内 Webview 中打开，并且不需要单独的审批流程。
> * 应用的默认行为仅在通过应用商店分发时Teams适用。 默认情况下，所有选项卡在 Teams 中打开。
> * 若要开始对应用进行移动友好评估，请通过 teamsubm@microsoft.com 与应用详细信息联系。

## <a name="authentication"></a>身份验证

若要在移动客户端上进行身份验证，必须将 JavaScript SDK Teams至少升级到版本 1.4.1。

## <a name="low-bandwidth-and-intermittent-connections"></a>低带宽和间歇性连接

移动客户端在低带宽和间歇性连接下工作。 应用必须通过向用户提供上下文消息来适当地处理任何超时。 还必须使用进度指示器为用户提供任何长时间运行的过程的反馈。

## <a name="testing-on-mobile-clients"></a>在移动客户端上测试

必须验证选项卡在各种大小和质量的移动设备上是否正常工作。 对于 Android 设备，可以在选项卡运行时使用 [DevTools](~/tabs/how-to/developer-tools.md) 调试选项卡。 建议在高性能和低性能设备（包括平板电脑）上进行测试。

## <a name="distribution"></a>分发

应用商店中列出的Teams必须经过批准，供移动使用，以在移动Teams正常运行。 选项卡可用性和行为取决于你的应用是否已获得批准。

### <a name="apps-on-teams-store-approved-for-mobile"></a>经批准Teams移动的应用商店上的应用

下表介绍了当应用在应用商店中列出并批准Teams时选项卡可用性和行为：

|功能   |移动可用性？   |移动行为|
|----------|-----------|------------|
|频道 <br /> 和组选项卡|是|选项卡使用Teams在移动客户端中 `contentUrl` 打开。|
|个人应用|是|"个人应用"选项卡中的每个选项卡使用各自的Teams在移动客户端中 `contentUrl` 打开。|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a>未批准Teams移动的应用商店上的应用

下表介绍了当应用在应用商店中列出但Teams未批准的移动用途时选项卡可用性和行为：

| 功能 | 移动可用性？ | 移动行为 |
|----------|-----------|------------|
|"频道和组"选项卡|是|选项卡在设备的默认浏览器中打开，而不是Teams应用的配置打开，这还必须包含在源代码 `websiteUrl` 的 `setSettings()` [函数中](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true)。 但是，用户可以在移动Teams中查看选项卡，方法为选择应用旁边的"更多"并选择"打开"，这将触发应用的 `contentUrl` 配置。|
|个人应用|不支持|不适用|

### <a name="apps-not-on-teams-store"></a>不在应用商店Teams应用

如果要将应用旁加载或发布到组织的应用程序目录，选项卡行为Teams Microsoft 批准的移动应用商店应用的行为相同。

## <a name="see-also"></a>另请参阅

* [选项卡设计指南](~/tabs/design/tabs.md)
* [Teams选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [获取选项卡的上下文](~/tabs/how-to/access-teams-context.md)
