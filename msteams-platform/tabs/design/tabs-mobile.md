---
title: 移动设备上的选项卡
description: 在本模块中，了解如何在Microsoft Teams移动设备上实现选项卡、身份验证、低带宽连接、在移动客户端上进行测试、分发等等。
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: da9757ee0153b3f2fe80e576e156f45bc90a15cd
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144263"
---
# <a name="tabs-on-mobile"></a>移动设备上的选项卡

生成包含选项卡的Microsoft Teams应用时，必须测试选项卡在Android和iOS Microsoft Teams客户端上的功能。 本文概述了必须考虑的一些关键方案。

如果选择在Teams移动客户端上显示频道或组选项卡，则[`setSettings()`](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-settings-setsettings&preserve-view=true)配置必须具有属性的`websiteUrl`值。 为了确保最佳用户体验，在创建选项卡时，必须遵循本文中有关移动选项卡的指南。

[通过Teams存储分发的](~/concepts/deploy-and-publish/appsource/publish.md)应用对移动客户端具有单独的审批流程。 此类应用的默认行为如下所示：

| **应用功能** | **应用获得批准时的行为** | **如果应用未获得批准，则为行为** |
| --- | --- | --- |
| **个人选项卡** | 应用显示在移动客户端的底部栏中。 在Teams客户端中打开选项卡。 | 应用不会显示在移动客户端的底部栏中。 |
| **频道和组选项卡** | 该选项卡在使用`contentUrl`Teams客户端中打开。 | 该选项卡在使用`websiteUrl`Teams客户端外部的浏览器中打开。 |

> [!NOTE]
>
> * 提交到 [AppSource](https://appsource.microsoft.com) 以在Teams上发布的应用会自动评估移动响应能力。 对于任何查询，请联系 teamsubm@microsoft.com。
> * 对于未通过 AppSource 分发的所有应用，默认情况下，选项卡会在Teams客户端的应用内 Web 视图中打开，并且无需单独的审批过程。
> * 仅当通过 Teams 存储分布时，应用的默认行为才适用。 默认情况下，所有选项卡在Teams客户端中打开。
> * 若要针对移动友好度启动应用评估，请联系 teamsubm@microsoft.com 应用详细信息。

## <a name="authentication"></a>身份验证

若要在移动客户端上进行身份验证，必须将 JavaScript SDK Teams升级到至少版本 1.4.1。

## <a name="low-bandwidth-and-intermittent-connections"></a>低带宽和间歇性连接

移动客户端具有低带宽和间歇性连接的功能。 应用必须通过向用户提供上下文消息来适当地处理任何超时。 还必须使用进度指示器向用户提供任何长时间运行的进程的反馈。

## <a name="testing-on-mobile-clients"></a>在移动客户端上测试

必须验证选项卡是否在各种大小和质量的移动设备上正常运行。 对于Android设备，可以在选项卡运行时使用 [DevTools](~/tabs/how-to/developer-tools.md) 调试选项卡。 建议在高性能和低性能设备（包括平板电脑）上进行测试。

## <a name="distribution"></a>分布

必须批准Teams存储中列出的应用，以便移动应用在Teams移动客户端中正常运行。 选项卡可用性和行为取决于应用是否获得批准。

### <a name="apps-on-teams-store-approved-for-mobile"></a>已批准用于移动Teams应用商店上的应用

下表描述了应用在Teams存储中列出并批准用于移动时选项卡的可用性和行为：

|功能   |移动可用性？   |移动行为|
|----------|-----------|------------|
|频道 <br /> 和组选项卡|是|使用应用`contentUrl`的配置在Teams移动客户端中打开选项卡。|
|个人应用|是|个人应用选项卡中的每个选项卡都使用其各自`contentUrl`的配置在Teams移动客户端中打开。|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Teams应用商店上的应用未获得移动应用批准

下表描述了当应用在Teams存储中列出但未批准用于移动时选项卡的可用性和行为：

| 功能 | 移动可用性？ | 移动行为 |
|----------|-----------|------------|
|“频道和组”选项卡|是|选项卡在设备的默认浏览器中打开，而不是使用应用的`websiteUrl`配置Teams移动客户端，该配置也必须包含在源代码的`setSettings()`[函数](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk#settings-namespace)中。 但是，用户可以通过选择应用旁边的 **“更多”** 并选择 **“打开**”来查看Teams移动客户端中的选项卡，这会触发应用的`contentUrl`配置。|
|个人应用|不支持|不适用|

### <a name="apps-not-on-teams-store"></a>应用不在Teams应用商店

如果旁加载应用或发布到组织的应用目录，选项卡行为与 Microsoft 批准的移动应用Teams应用商店行为相同。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [获取选项卡的上下文](~/tabs/how-to/access-teams-context.md)

## <a name="see-also"></a>另请参阅

* [选项卡设计指南](~/tabs/design/tabs.md)
* [Teams 选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或群组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [规划Teams移动版 - Teams](~/concepts/design/plan-responsive-tabs-for-teams-mobile.md)
