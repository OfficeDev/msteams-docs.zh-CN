---
title: 移动设备上的选项卡
description: 了解 Android 和 iOS Microsoft Teams 客户端上的 Tab 功能如何 (移动) 、身份验证、低带宽连接、测试或分发。
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 0dbb74d5c2854897f82708aa83a0c49df4f28890
ms.sourcegitcommit: bd96080c78f25eb0a67ce176df5e255be348f7b1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2022
ms.locfileid: "68575766"
---
# <a name="tabs-on-mobile"></a>移动设备上的选项卡

生成包含选项卡的 Microsoft Teams 应用时，必须测试选项卡在 Android 和 iOS Microsoft Teams 客户端上的功能。 本文概述了必须考虑的一些关键方案。

如果选择在 Teams 移动客户端上显示频道或组选项卡，则 [`setSettings()`](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-settings-setsettings&preserve-view=true) 配置必须具有属性值 `websiteUrl` 。 为了确保最佳用户体验，在创建选项卡时，必须遵循本文中有关移动选项卡的指南。

[通过 Teams 应用商店分发的](~/concepts/deploy-and-publish/appsource/publish.md)应用对移动客户端有单独的审批过程。 此类应用的默认行为如下所示：

| **应用功能** | **应用获得批准时的行为** | **如果应用未获得批准，则为行为** |
| --- | --- | --- |
| **个人选项卡** | 应用显示在移动客户端的底部栏中。 在 Teams 客户端中打开选项卡。 | 应用不会显示在移动客户端的底部栏中。 |
| **频道和组选项卡** | 使用 `contentUrl`>a0>在 Teams 客户端中打开该选项卡。 | 该选项卡在 Teams 客户端外部的浏览器中打开 `websiteUrl`。 |

> [!NOTE]
>
> * 提交到 [AppSource](https://appsource.microsoft.com) 以便在 Teams 上发布的应用会自动评估移动响应能力。 对于任何查询，请联系 teamsubm@microsoft.com。
> * 对于未通过 AppSource 分发的所有应用，默认情况下，该选项卡会在 Teams 客户端的应用内 Web 视图中打开，并且不需要单独的审批过程。
> * 应用的默认行为仅在通过 Teams 应用商店分发时适用。 默认情况下，所有选项卡都会在 Teams 客户端中打开。
> * 若要针对移动友好度启动应用评估，请联系 teamsubm@microsoft.com 应用详细信息。

## <a name="authentication"></a>身份验证

若要在移动客户端上进行身份验证，必须将 Teams JavaScript SDK 升级到至少版本 1.4.1。

## <a name="low-bandwidth-and-intermittent-connections"></a>低带宽和间歇性连接

移动客户端具有低带宽和间歇性连接的功能。 应用必须通过向用户提供上下文消息来适当地处理任何超时。 还必须使用进度指示器向用户提供任何长时间运行的进程的反馈。

## <a name="testing-on-mobile-clients"></a>在移动客户端上测试

必须验证选项卡是否在各种大小和质量的移动设备上正常运行。 对于 Android 设备，可以在选项卡运行时使用 [DevTools](~/tabs/how-to/developer-tools.md) 调试选项卡。 建议在高性能和低性能设备（包括平板电脑）上进行测试。

## <a name="distribution"></a>分布

必须批准 Teams 应用商店中列出的应用才能在 Teams 移动客户端中正常使用移动应用。 选项卡可用性和行为取决于应用是否获得批准。

### <a name="apps-on-teams-store-approved-for-mobile"></a>已批准用于移动的 Teams 应用商店上的应用

下表描述了当应用在 Teams 应用商店中列出并批准用于移动时选项卡可用性和行为：

|功能   |移动可用性？   |移动行为|
|----------|-----------|------------|
|频道 <br /> 和组选项卡|是|使用应用 `contentUrl` 的配置在 Teams 移动客户端中打开选项卡。|
|个人应用|是|个人应用选项卡中的每个选项卡都使用各自 `contentUrl` 的配置在 Teams 移动客户端中打开。|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Teams 应用商店上的应用未获得移动应用批准

下表描述了在 Teams 应用商店中列出但未批准用于移动用途的应用时选项卡可用性和行为：

| 功能 | 移动可用性？ | 移动行为 |
|----------|-----------|------------|
|“频道和组”选项卡|是|选项卡在设备的默认浏览器中打开，而不是使用应用配置的 `websiteUrl` Teams 移动客户端，该配置也必须包含在源代码的`setSettings()`[函数](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk#settings-namespace)中。 但是，用户可以通过选择应用旁边的 **“更多”** 并选择 **“打开**”来查看 Teams 移动客户端中的选项卡，这会触发应用的 `contentUrl` 配置。|
|个人应用|否|不适用|

> [!NOTE]
> 如果移动应用同时具有机器人和选项卡功能，则会在聊天部分中显示机器人消息。
>
> 选择“ **机器人聊天** ”应用并选择 **“更多 (...)**”时，无法在列表中看到该应用的选项卡功能。 但是，如果从 **“聊天**”部分右下角选择“**更多 (...)**”，则可以使用指向该应用的机器人应用功能的链接来查看选项卡应用。

### <a name="apps-not-on-teams-store"></a>不适用于 Teams 应用商店的应用

如果旁加载应用或发布到组织的应用目录，选项卡行为与 Microsoft 批准的适用于移动的 Teams 应用商店应用相同。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [获取选项卡的上下文](~/tabs/how-to/access-teams-context.md)

## <a name="see-also"></a>另请参阅

* [选项卡设计指南](~/tabs/design/tabs.md)
* [Teams 选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [规划 Teams 移动版 - Teams](~/concepts/design/plan-responsive-tabs-for-teams-mobile.md)
