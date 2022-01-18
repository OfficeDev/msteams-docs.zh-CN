---
title: 浏览器的设备权限
keywords: teams 应用功能权限
description: 安全地返回对 Web 客户端中应用的设备权限支持
localization_priority: medium
ms.topic: how-to
ms.openlocfilehash: fbdca08c813d341c12fcfc824d21a6ff96d02749
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059784"
---
# <a name="device-permissions-for-the-browser"></a>浏览器的设备权限

> [!NOTE]
> 有关如何在浏览器中处理设备权限的最新更新当前仅适用于公共开发人员 [预览](../../resources/dev-preview/developer-preview-intro.md) 版。 此更新将于 2022 年 2 (通用) 正式发布。


Teams需要设备权限（如相机或麦克风访问）的应用现在要求用户在 Web 浏览器中按应用级别手动授予权限。 以前，浏览器已处理如何授予访问权限，但现在这些权限在Microsoft Teams。 这对设计应用程序以及是否需要在浏览器中具有这些权限有一些影响。

## <a name="enable-apps-device-permissions"></a>启用应用的设备权限
如果你Teams应用程序在应用程序清单中声明它需要设备权限[](native-device-permissions.md#specify-permissions)，则将显示"应用权限"选项，以便用户启用该应用的设备权限。 " **应用程序权限"** 选项具有以下功能： 

* **个人应用和任务模块对话框**： **页面** 右上角提供"应用权限"选项。
<img src="../../assets/images/tabs/apppermissions.png" alt="App permissions button" width="800"/>

* **聊天、频道或会议选项卡**：选项卡的下拉列表中提供了"应用权限"选项。 ![应用程序权限下拉列表](../../assets/images/tabs/drop-downapppermissions.png)

选择 **"应用程序权限"** 选项后，将出现一个弹出窗口，用户可以在弹出窗口中启用权限按钮。

用户需要在浏览器中启用这些权限，这些权限才能生效。 在用户更改浏览器中应用的设备权限后，系统会提示他们在浏览器中重新加载Teams。

> [!IMPORTANT]
> 必须让用户知道在何处启用这些应用程序Microsoft Teams。 

## <a name="recommendation"></a>建议
Teams浏览器中需要设备权限的应用必须向用户显示有关在浏览器中查找和启用这些权限Teams说明。 根据应用程序运行的上下文，你需要确保你的说明将用户指向访问这些权限的正确位置，因为它们对于个人应用、任务模块对话框、聊天中的选项卡以及频道或会议有所不同。

</br>
<img src="../../assets/images/tabs/enable-access.png" alt="Enable camera access" width="800"/>

## <a name="code-sample"></a>代码示例

|示例名称 | Description | Node.js |
|----------------|-----------------|--------------|
| 浏览器的 Tab 设备权限 | 示例代码演示如何显示浏览器的设备权限。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="step-by-step-guide"></a>分步指南

按照[分步指南在"页面](../../sbs-tab-device-permissions.yml)"中授予选项卡设备Microsoft Teams。

## <a name="see-also"></a>另请参阅

* [设备功能概述](device-capabilities-overview.md)
* [请求设备权限](native-device-permissions.md)
