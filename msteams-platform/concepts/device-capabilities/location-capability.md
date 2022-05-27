---
title: 集成位置功能
author: Rajeshwari-v
description: 通过代码片段和示例了解如何使用 Teams JavaScript 客户端 SDK 来利用位置功能
keywords: 位置映射功能, 本机设备权限
ms.topic: conceptual
ms.localizationpriority: high
ms.author: surbhigupta
ms.openlocfilehash: d143cdd0e94664d916bd5eefa7523d92e2af183a
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757169"
---
# <a name="integrate-location-capabilities"></a>集成位置功能

可以将本机设备的位置功能与 Teams 应用集成。  

可以使用 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)，它为应用访问用户的[本机设备功能](native-device-permissions.md)提供了所需的工具。 使用位置 API（例如 [getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) 和 [showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true)）来集成应用中的功能。

## <a name="advantages-of-integrating-location-capabilities"></a>集成位置功能的优势

在 Teams 应用中集成位置功能的主要优势是，它允许 Teams 平台上的 Web 应用开发人员利用 Microsoft Teams JavaScript 客户端 SDK 的位置功能。

以下示例演示如何在不同方案中使用位置功能集成：

* 在工厂，主管可以通过要求工人在工厂附近自拍并通过指定的应用共享它来跟踪他们的出勤情况。 也可捕获位置数据并与图像一起发送。
* 位置功能使服务提供商的维护人员能够与管理层共享基站的真实运行状况数据。 管理层可以比较捕获的位置信息与维护人员提交的数据之间的任何不匹配。

若要集成位置功能，必须更新应用清单文件并调用 API。 若要进行有效的集成，必须充分了解用于调用位置 API 的[代码片段](#code-snippets)。
请务必熟悉 [API 响应错误](#error-handling)，以处理 Teams 应用中的错误。

> [!NOTE]
> 目前，Microsoft Teams 对位置功能的支持仅适用于移动客户端。

## <a name="update-manifest"></a>更新清单

通过添加 `devicePermissions` 属性并指定 `geolocation` 来更新 Teams 应用 [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) 文件。 它允许应用在用户开始使用位置功能之前向他们请求必要的权限。 应用清单的更新如下所示：

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> * 启动相关 Teams API 时，将自动显示“**请求权限**”提示。 有关详细信息，请参阅[请求设备权限](native-device-permissions.md)。
> * 在浏览器中，设备权限有所不同。 有关详细信息，请参阅[浏览器设备权限](browser-device-permissions.md)。

## <a name="location-apis"></a>位置 API

必须使用以下一组 API 来启用设备的位置功能：

| API      | 说明   |
| --- | --- |
|[getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | 提供用户的当前设备位置或打开本机位置选取器并返回用户选择的位置。 |
|[showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) | 在地图上显示位置。 |

> [!NOTE]
> `getLocation()` API 附带以下[输入配置](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true)、`allowChooseLocation` 和 `showMap`。<br/> 如果 `allowChooseLocation` 的值为 *true*，则用户可以选择所选的任何位置。<br/>  如果该值为 *false*，则用户无法更改其当前位置。<br/> 如果 `showMap` 的值为 *false*，则会提取当前位置而不显示地图。 如果 `allowChooseLocation` 设置为 *true*，则会忽略 `showMap`。

下图描述了位置功能的 Web 应用体验：

![位置功能的 Web 应用体验](../../assets/images/tabs/location-capability.png)

### <a name="code-snippets"></a>代码段

**调用 `getLocation` API 以检索位置：**

```javascript
let locationProps = {"allowChooseLocation":true,"showMap":true};
microsoftTeams.location.getLocation(locationProps, (err: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
          if (err) {
            output(err);
            return;
          }
          output(JSON.stringify(location));
});
```

**调用 `showLocation` API 以显示位置：**

```javascript
let location = {"latitude":17,"longitude":17};
microsoftTeams.location.showLocation(location, (err: microsoftTeams.SdkError, result: boolean) => {
          if (err) {
            output(err);
            return;
          }
     output(result);
});
```

## <a name="error-handling"></a>错误处理

必须确保在 Teams 应用中正确处理这些错误。 下表列出了错误代码和产生错误的条件：

|错误代码 |  错误名称     | 条件|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | 当前平台不支持 API。|
| **500** | INTERNAL_ERROR | 执行所需的操作时遇到内部错误。|
| **1000** | PERMISSION_DENIED |用户拒绝了对 Teams 应用或 Web 应用的位置权限。|
| **4000** | INVALID_ARGUMENTS | 调用 API 时的强制性参数错误或不足。|
| **8000** | USER_ABORT |用户取消了该操作。|
| **9000** | OLD_PLATFORM | 用户位于无法实现 API 的旧平台版本上。 升级版本应该可以解决此问题。|

### <a name="code-sample"></a>代码示例

|示例名称 | Description | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| 应用签入当前位置 | 用户可以签入当前位置并查看所有以前的位置签入。| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-checkin-location/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-checkin-location/nodejs) |

## <a name="see-also"></a>另请参阅

* [在 Teams 中集成媒体功能](mobile-camera-image-permissions.md)
* [在 Teams 中集成 QR 代码或条形码扫描程序功能](qr-barcode-scanner-capability.md)
* [在 Teams 中集成人员选取器](people-picker-capability.md)
