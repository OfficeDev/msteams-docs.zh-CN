---
title: 浏览器的设备权限
keywords: Teams 应用功能权限
description: 安全地恢复 Web 客户端中应用的设备权限支持
localization_priority: medium
ms.topic: how-to
ms.openlocfilehash: 0789715aebfd1db0c9d0100ccffb2ff213a10d1d
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756742"
---
# <a name="device-permissions-for-the-browser"></a>浏览器的设备权限

Teams需要设备权限（如相机或麦克风访问）的应用现在要求用户在 Web 浏览器中手动授予每个应用级别的权限。 以前，浏览器处理了如何授予访问权限的问题，但现在这些权限在 Microsoft Teams 中处理。 这会影响应用程序的设计方式，以及它们在浏览器中是否需要这些权限。

## <a name="enable-apps-device-permissions"></a>启用应用的设备权限

如果 Teams 应用已在 [应用程序清单](native-device-permissions.md#specify-permissions)中声明它需要设备权限，则将为用户显示“**应用权限**”选项用于启用应用的设备权限。 “**应用权限**”选项在以下功能中可用：

* **个人应用和任务模块对话框**：页面右上角提供“**应用权限**”选项。
<img src="../../assets/images/tabs/apppermissions.png" alt="App permissions button" width="800"/>

* **聊天、频道或会议选项卡**：选项卡下拉列表中提供“**应用权限**”选项。![应用权限下拉列表](../../assets/images/tabs/drop-downapppermissions.png)

选择“**应用权限**”选项后，将显示一个弹出窗口，用户可以在其中启用权限按钮。

用户需要在浏览器中启用这些权限才能使这些权限生效。 用户在浏览器中更改应用的设备权限后，系统会提示他们在 Teams 中重新加载应用程序。

> [!IMPORTANT]
> 必须让用户了解在 Microsoft Teams 中启用这些 **应用权限** 的位置。

## <a name="recommendation"></a>建议

在浏览器中需要设备权限的Teams应用必须向用户显示有关在Teams UI 中查找和启用这些权限的说明。 根据运行应用程序的上下文，需要确保说明指向用户访问这些权限的正确位置。 个人应用、任务模块对话框、聊天中的选项卡以及频道或会议的权限不同。

</br>
<img src="../../assets/images/tabs/enable-access.png" alt="Enable camera access" width="800"/>

## <a name="code-sample"></a>代码示例

|示例名称 | Description | Node.js |
|----------------|-----------------|--------------|
| 浏览器的选项卡设备权限 | 示例代码演示如何显示浏览器的设备权限。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="step-by-step-guide"></a>分步指南

按照[分步指南](../../sbs-tab-device-permissions.yml)在 Microsoft Teams 中授予选项卡设备权限。

## <a name="see-also"></a>另请参阅

* [设备功能概述](device-capabilities-overview.md)
* [请求设备权限](native-device-permissions.md)
