---
title: 集成位置功能
description: 如何使用 Teams JavaScript 客户端 SDK 利用位置功能
keywords: 位置映射功能本机设备权限
ms.author: lajanuar
ms.openlocfilehash: fccf39c37c785be716bfff26907f9184c0d9beec
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449606"
---
# <a name="integrate-location-capabilities"></a>集成位置功能 

本文档指导你如何将本机设备的位置功能与 Teams 应用集成。  

可以使用 [Microsoft Teams JavaScript 客户端 SDK，](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)它提供应用访问用户的本机设备功能 [所需的工具](native-device-permissions.md)。 使用位置 API（如 [getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_) 和 [showLocation）](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_) 将功能集成到你的应用中。 

## <a name="advantages-of-integrating-location-capabilities"></a>集成位置功能的优点

在 Teams 应用中集成位置功能的主要优点是，它允许 Teams 平台上的 Web 应用开发人员通过 Microsoft Teams JavaScript 客户端 SDK 利用位置功能。 

以下示例显示了如何在不同方案中使用位置功能的集成：
* 在工厂中，主管可以通过要求员工在工厂附近自家并通过指定的应用共享来跟踪员工出席情况。 位置数据也会与图像一起捕获和发送。
* 位置功能使服务提供商的维护人员能够与管理层共享手机网络网络的真实运行状况数据。 管理层可以比较捕获的位置信息和维护人员提交的数据之间的任何不匹配情况。

若要集成位置功能，必须更新应用清单文件并调用 API。 为了有效集成，您必须对用于调用位置 API[](#code-snippets)的代码段有一个很好的了解。 熟悉 API 响应错误以处理[](#error-handling)Teams 应用中的错误非常重要。

> [!NOTE] 
> 目前，Microsoft Teams 对位置功能的支持仅适用于移动客户端。

## <a name="update-manifest"></a>更新清单

通过 [ 添加manifest.js并](../../resources/schema/manifest-schema.md#devicepermissions) 指定来更新 Teams 应用文件 `devicePermissions` `geolocation` 。 它允许你的应用在开始使用位置功能之前向用户请求必要的权限。

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> 启动 **相关** Teams API 时，将自动显示请求权限提示。 有关详细信息，请参阅请求 [设备权限](native-device-permissions.md)。

## <a name="location-apis"></a>位置 API

你必须使用以下一组 API 来启用设备的位置功能：

| API      | 说明   |
| --- | --- |
|[getLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_) | 提供用户的当前设备位置或打开本机位置选取器并返回用户选择的位置。 |
|[showLocation](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#showLocation) | 在地图上显示位置 |

> [!NOTE]

> `getLocation()`API 附带以下[输入配置](https://docs.microsoft.com/en-us/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest)和 `allowChooseLocation` `showMap` 。 <br/> 如果值为 `allowChooseLocation` *true，* 则用户可以选择其选择的任何位置。<br/>  如果值为 *false，* 则用户无法更改其当前位置。<br/> 如果值为 `showMap` *false，* 则提取当前位置而不显示地图。 `showMap` 如果设置为 `allowChooseLocation` *true，则忽略*。 

**位置功能的 Web 应用体验** 
 ![位置功能的 Web 应用体验](../../assets/images/tabs/location-capability.png)

## <a name="error-handling"></a>错误处理

必须确保在 Teams 应用中正确处理这些错误。 下表列出了错误代码以及生成错误的条件： 

|错误代码 |  错误名称     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API 在当前平台上不受支持。|
| **500** | INTERNAL_ERROR | 执行所需操作时遇到内部错误。|
| **1000** | PERMISSION_DENIED |用户拒绝对 Teams 应用或 Web 应用的位置权限。|
| **4000** | INVALID_ARGUMENTS | 使用错误的或不足的强制参数调用 API。|
| **8000** | USER_ABORT |用户已取消操作。|
| **9000** | OLD_PLATFORM | 用户位于不存在 API 实现的旧平台版本上。 升级生成应解决问题。|

## <a name="code-snippets"></a>代码段

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

## <a name="see-also"></a>另请参阅

> [!div class="nextstepaction"]
> [在 Teams 中集成媒体功能](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [在 Teams 中集成 QR 或条形码扫描仪功能](qr-barcode-scanner-capability.md)