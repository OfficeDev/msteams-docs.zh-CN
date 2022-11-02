---
title: 移动设备上的选项卡
description: 了解选项卡在 Android 和 iOS Microsoft Teams 客户端上如何 (移动) 、身份验证、低带宽连接、测试或分发。
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 8dac56cd609466c116f39baf5dc9d9a7970645ec
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820078"
---
# <a name="tabs-on-mobile"></a>移动设备上的选项卡

构建包含选项卡的 Microsoft Teams 应用时，必须测试选项卡在 Android 和 iOS Microsoft Teams 客户端上的功能。 本文概述了必须考虑的一些关键方案。

如果选择在 Teams 移动客户端上显示频道或组选项卡，则 [`setSettings()`](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-settings-setsettings&preserve-view=true) 配置必须具有 属性的值 `websiteUrl` 。 为确保最佳用户体验，创建选项卡时，必须遵循本文中有关移动设备上的选项卡的指南。

[通过 Teams 应用商店分发](~/concepts/deploy-and-publish/appsource/publish.md)的应用对移动客户端具有单独的审批流程。 此类应用的默认行为如下所示：

| **应用功能** | **应用获得批准时的行为** | **应用未获批准时的行为** |
| --- | --- | --- |
| **个人选项卡** | 应用显示在移动客户端的底部栏中。 在 Teams 客户端中打开选项卡。 | 应用不会显示在移动客户端的底部栏中。 |
| **频道和组选项卡** | 选项卡使用 `contentUrl`在 Teams 客户端中打开。 | 使用 在 Teams 客户端 `websiteUrl`外部的浏览器中打开选项卡。 |

> [!NOTE]
>
> * 提交到 [AppSource](https://appsource.microsoft.com) 以在 Teams 上发布的应用会自动评估移动响应能力。 对于任何查询，请联系 teamsubm@microsoft.com。
> * 对于未通过 AppSource 分发的所有应用，默认情况下，选项卡在 Teams 客户端中的应用内 Web 视图中打开，不需要单独的审批过程。
> * 仅当通过 Teams 应用商店分发时，应用的默认行为才适用。 默认情况下，所有选项卡都会在 Teams 客户端中打开。
> * 若要启动对应用的移动友好性评估，请联系 teamsubm@microsoft.com 应用详细信息。

## <a name="authentication"></a>身份验证

若要在移动客户端上运行身份验证，必须将 Teams JavaScript SDK 升级到至少版本 1.4.1。

## <a name="low-bandwidth-and-intermittent-connections"></a>低带宽和间歇性连接

移动客户端以低带宽和间歇性连接运行。 应用必须通过向用户提供上下文消息来适当地处理任何超时。 还必须使用进度指示器向用户提供任何长时间运行的进程的反馈。

## <a name="testing-on-mobile-clients"></a>在移动客户端上进行测试

必须验证选项卡在各种大小和质量的移动设备上是否正常运行。 对于 Android 设备，可以在选项卡运行时使用 [DevTools](~/tabs/how-to/developer-tools.md) 调试选项卡。 建议在高性能和低性能设备（包括平板电脑）上进行测试。

## <a name="distribution"></a>分布

Teams 应用商店中列出的应用必须获得移动许可才能在 Teams 移动客户端中正常运行。 选项卡可用性和行为取决于你的应用是否获得批准。

### <a name="apps-on-teams-store-approved-for-mobile"></a>Teams 应用商店中的应用已批准用于移动版

下表描述了当应用在 Teams 应用商店中列出并批准用于移动时选项卡可用性和行为：

|功能   |移动可用性？   |移动行为|
|----------|-----------|------------|
|频道 <br /> “和组”选项卡|是|使用应用的 `contentUrl` 配置在 Teams 移动客户端中打开选项卡。|
|个人应用|是|个人应用选项卡中的每个选项卡使用各自的 `contentUrl` 配置在 Teams 移动客户端中打开。|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Teams 应用商店中的应用未获得移动版批准

下表描述了当应用在 Teams 应用商店中列出但未批准移动使用时选项卡可用性和行为：

| 功能 | 移动可用性？ | 移动行为 |
|----------|-----------|------------|
|“通道和组”选项卡|是|选项卡将在设备的默认浏览器中打开，而不是使用应用的`websiteUrl`配置在 Teams 移动客户端中打开，该配置也必须包含在源代码[的](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk#settings-namespace)`setSettings()` 函数中。 但是，用户可以在 Teams 移动客户端中查看选项卡，方法是选择应用旁边的“ **更多** ”，然后选择“ **打开**”，这会触发应用的 `contentUrl` 配置。|
|个人应用|否|不适用|

> [!NOTE]
> 如果移动应用同时具有机器人和选项卡功能，机器人消息会显示在聊天部分中。
>
> 选择“ **聊天** 机器人应用”并选择“ **更多 (...)**”时，无法在列表中看到该应用的选项卡功能。 但是，如果你从 **“聊天**”部分的右下角选择“**更多 (...)**”，则可以查看选项卡应用，其中包含指向该应用的机器人应用功能的链接。

### <a name="apps-not-on-teams-store"></a>不在 Teams 应用商店中的应用

如果要旁加载应用或发布到组织的应用目录，选项卡行为与 Microsoft 批准的移动版 Teams 应用商店应用相同。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [获取选项卡的上下文](~/tabs/how-to/access-teams-context.md)

## <a name="see-also"></a>另请参阅

* [Teams 的生成选项卡](../what-are-tabs.md)
* [具有自适应卡片的生成选项卡](../how-to/build-adaptive-card-tabs.md)
* [创建个人选项卡](../how-to/create-personal-tab.md)
* [规划 Teams 移动版的响应式选项卡](../../concepts/design/plan-responsive-tabs-for-teams-mobile.md)
* [为 Microsoft Teams 设计选项卡](tabs.md)
* [适用于 Microsoft Teams 选项卡的 DevTools](../how-to/developer-tools.md)
* [测试应用](../../concepts/build-and-test/test-app-overview.md)
* [分发 Microsoft Teams 应用](../../concepts/deploy-and-publish/apps-publish-overview.md)
* [创建 Teams 应用包](../../concepts/build-and-test/apps-package.md)
