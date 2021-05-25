---
title: 移动设备上的选项卡
description: 介绍在移动设备上实现选项卡的开发人员Microsoft Teams注意事项。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 41ba96b64bd31f3b226aeba72969bc44c1ae8955
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630654"
---
# <a name="tabs-on-mobile"></a>移动设备上的选项卡

生成包含选项卡的 Microsoft Teams 应用时，必须考虑 (并测试) 选项卡在 Android 和 iOS Microsoft Teams 上的运行方式。 以下各节概述了需要考虑的一些关键方案。

## <a name="authentication"></a>身份验证

若要在移动客户端上进行身份验证，必须将 JavaScript SDK Teams至少升级到版本 1.4.1。

## <a name="low-bandwidth-and-intermittent-connections"></a>低带宽和间歇性连接

移动客户端经常需要在低带宽和间歇性连接下运行。 应用应该通过向用户提供上下文消息来适当地处理任何超时。 您还应使用用户进度指示器，以针对任何长时间运行的过程向用户提供反馈。

## <a name="testing-on-mobile-clients"></a>在移动客户端上测试

需要验证选项卡在各种大小和质量的移动设备上是否正常工作。 对于 Android 设备，可以在选项卡运行时使用 [DevTools](~/tabs/how-to/developer-tools.md) 调试选项卡。 建议在高性能和低性能设备（包括平板电脑）上进行测试。

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
|"频道和组"选项卡|是|选项卡将在设备的默认浏览器中打开，而不是Teams应用的配置（还必须包含在源代码的 函数中）中的移动 `websiteUrl` `setSettings()` [客户端](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true)。 但是，用户仍可在移动客户端Teams选项卡，方法为选择应用旁边的"更多"并选择"打开"，这将触发应用的 `contentUrl` 配置。|
|个人应用|不支持|不适用|

### <a name="apps-not-on-teams-store"></a>不在应用商店Teams应用

如果要将应用旁加载或发布到组织的应用程序目录，选项卡行为将Teams Microsoft 批准的移动应用商店应用的行为相同。

## <a name="see-also"></a>另请参阅

* [选项卡设计指南](~/tabs/design/tabs.md)
