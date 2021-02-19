---
title: 集成 QR 或条形码扫描仪功能
description: 如何使用 Teams JavaScript 客户端 SDK 利用 QR 或条形码扫描仪功能
keywords: 相机媒体 qr 代码 qrcode 条码条形码扫描仪扫描功能本机设备权限
ms.author: lajanuar
ms.openlocfilehash: 048c6b58fc126d1dd08867605784b6a150737195
ms.sourcegitcommit: 0bb6efb3003a1949288e4601e3301b69e67d4c26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2021
ms.locfileid: "50295087"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a>集成 QR 或条形码扫描仪功能 

条形码是一种以可视和机器可读的形式表示数据的方法。 条码包含有关产品的信息，如条形图和空格形式的类型、大小、制造商和来源国家/地区。 使用本机设备相机上的光学扫描仪读取代码。 为了获得更丰富的协作体验，你可以将 Teams 平台中提供的 QR 或条形码扫描仪功能与 Teams 应用集成。 本文档指导您了解如何集成该功能。  

可以使用 [Microsoft Teams JavaScript 客户端 SDK，](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)它提供应用访问用户的本机设备功能 [所需的工具](native-device-permissions.md)。 使用 `scanBarCode` API 将扫描程序功能集成到你的应用中。 

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a>集成 QR 或条形码扫描仪功能的优势

* 集成使 Teams 平台上的 Web 应用开发人员能够利用 Teams JavaScript 客户端 SDK 的 QR 或条形码扫描功能。
* 使用此功能，用户只需在扫描仪 UI 中心的框架内对齐 QR 或条形码，代码将自动扫描。 存储的数据将重新与调用 Web 应用共享。 这可以避免手动输入长产品代码或其他相关信息的不便和人为错误。

若要集成 QR 或条形码扫描仪功能，必须更新应用清单文件并调用 `scanBarCode` API。 为了进行有效集成，你必须对调用 API[](#code-snippet)的代码段有一个很好的了解，这允许你使用本机 `scanBarCode` QR 或条形码扫描仪功能。 API 为不支持的条形码标准提供错误。
熟悉 API 响应错误以处理[](#error-handling)Teams 应用中的错误非常重要。

> [!NOTE] 
> 目前，Microsoft Teams 对 QR 或条形码扫描仪功能的支持仅适用于移动客户端。

## <a name="update-manifest"></a>更新清单

通过 [ 添加manifest.js并](../../resources/schema/manifest-schema.md#devicepermissions) 指定来更新 Teams 应用文件 `devicePermissions` `media` 。 它允许你的应用在开始使用 QR 或条形码扫描仪功能之前向用户请求必要的权限。

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> 启动 **相关** Teams API 时，将自动显示请求权限提示。 有关详细信息，请参阅"[请求设备权限"。](native-device-permissions.md)

## <a name="scanbarcode-api"></a>ScanBarCode API

API 调用扫描程序控件，使用户可以扫描不同类型的条形码，并返回 `ScanBarCode` 字符串形式的结果。

若要自定义条形码扫描体验，可选条形码配置作为输入传递到 `ScanBarCode` API。 可以使用 .指定扫描的间隔（以秒为单位 `timeOutIntervalInSec` ）。 其默认值为 30 秒，最大值为 60 秒。

**scanBarCode ()** API 支持以下条形码类型：

| 条形码类型 | 在 Android 上受支持 | 在 iOS 上受支持 |
| ---------- | ---------- | ------------ |
| 代码栏 | 是 | 否 |
| 代码 39 | 是 | 是 | 
| 代码 93 | 是 | 是 |
| 代码 128 | 是 | 是 |
| EAN-13 | 是 | 是 |
| EAN-8 | 是 | 是 |
| ITF | 否 | 是 |
| QR 代码 | 是 | 是 |
| RSS 扩展 | 是 | 否 |
| RSS-14 | 是 | 否 |
| UPC-A | 是 | 是 |
| UPC-E | 是 | 是 |

**Web 应用体验 `ScanBarCode`QR 或条形码扫描仪功能** 
 ![ Web 应用体验的 API（qr 或条形码扫描仪功能）](../../assets/images/tabs/qr-barcode-scanner-capability.png)

## <a name="error-handling"></a>错误处理

必须确保在 Teams 应用中正确处理这些错误。 下表列出了错误代码以及生成错误的条件： 

|错误代码 |  错误名称     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API 在当前平台上不受支持。|
| **500** | INTERNAL_ERROR | 执行所需操作时遇到内部错误。|
| **1000** | PERMISSION_DENIED |用户拒绝权限。|
| **3000** | NO_HW_SUPPORT | 基础硬件不支持该功能。|
| **4000** | INVALID_ARGUMENTS | 一个或多个参数无效。|
| **8000** | USER_ABORT |用户中止操作。|
| **8001** | OPERATION_TIMED_OUT | 无法检测给定时间间隔中的条码。|
| **9000** | OLD_PLATFORM | 平台代码已过时，未实现此 API。|

## <a name="code-snippet"></a>代码段

**呼叫 `ScanBarCode()` 用于** 使用相机扫描 QR 或条形码的 API：

```javascript
const config: microsoftTeams.media.BarCodeConfig = {
  timeOutIntervalInSec: 30};
microsoftTeams.media.scanBarCode((error: microsoftTeams.SdkError, decodedText: string) => {
  if (error) {
    if (error.message) {
      output(" ErrorCode: " + error.errorCode + error.message);
    } else {
      output(" ErrorCode: " + error.errorCode);
    }
  } else if (decodedText) {
    output(decodedText);
  }
}, config);
```

## <a name="see-also"></a>另请参阅

> [!div class="nextstepaction"]
> [在 Teams 中集成媒体功能](mobile-camera-image-permissions.md)
