---
title: 集成 QR 或条码扫描仪功能
author: Rajeshwari-v
description: 如何使用 JavaScript Teams SDK 利用 QR 或条形码扫描仪功能
keywords: 相机媒体 qr 代码 qrcode 条形码条形码扫描仪扫描功能本机设备权限
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 02332ad1f0805bfc4972333086e48552761a48a8
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345253"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a>集成 QR 或条码扫描仪功能 

条形码是一种以可视和机器可读的形式表示数据的方法。 条码包含有关产品的信息，如条形图和空格形式的类型、大小、制造商和来源国家/地区。 该代码使用本机设备相机上的光学扫描仪进行读取。 为了获得更丰富的协作体验，可以将 Teams 平台中提供的 QR 或条形码扫描仪功能与 Teams 应用集成。   

可以使用[JavaScript Microsoft Teams SDK，](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)它提供应用访问用户的本机设备功能[所需的工具](native-device-permissions.md)。 使用 [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API 将扫描程序功能集成到你的应用中。 

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a>集成 QR 或条形码扫描仪功能的优势

以下是 QR 或条形码扫描仪功能集成的优势： 

* 集成使 Web 应用开发人员Teams JavaScript 客户端 SDK 利用 QR 或条形码Teams功能。
* 使用此功能，用户只需在扫描仪 UI 中心的框架内对齐 QR 或条形码，代码将自动扫描。 存储的数据将重新与调用 Web 应用共享。 这样可以避免手动输入冗长的产品代码或其他相关信息带来的不便和人为错误。

若要集成 QR 或条形码扫描仪功能，必须更新应用清单文件并调用 [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API。 为了进行有效的集成，你必须深入了解用于调用[scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API 的代码段，这允许你使用本机 QR 或条形码扫描仪功能。 [](#code-snippet) API 为不支持的条形码标准提供错误。
熟悉 API 响应错误以处理应用[](#error-handling)内的错误Teams很重要。

> [!NOTE] 
> 目前，Microsoft Teams QR 或条形码扫描仪功能的支持仅适用于移动客户端。

## <a name="update-manifest"></a>更新清单

通过添加 Teams 并[manifest.js](../../resources/schema/manifest-schema.md#devicepermissions) ，更新文件 `devicePermissions` 上的应用。 `media` 它允许你的应用在用户开始使用 QR 或条形码扫描仪功能之前向用户请求必要的权限。 应用清单的更新如下所示：

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> 启动 **相关 API** 时，将自动显示Teams权限提示。 有关详细信息，请参阅请求 [设备权限](native-device-permissions.md)。

## <a name="scanbarcode-api"></a>ScanBarCode API

[scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API 调用扫描程序控件，使用户可以扫描不同类型的条形码，并返回字符串形式的结果。

若要自定义条形码扫描体验，可选 [条形码配置](/javascript/api/@microsoft/teams-js/microsoftteams.media.barcodeconfig?view=msteams-client-js-latest&preserve-view=true) 作为输入传递到 [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API。 可以使用 指定扫描的退出间隔（以秒为单位 `timeOutIntervalInSec` ）。 其默认值为 30 秒，最大值为 60 秒。

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
| QR 码 | 是 | 是 |
| RSS 展开 | 是 | 否 |
| RSS-14 | 是 | 否 |
| UPC-A | 是 | 是 |
| UPC-E | 是 | 是 |

下图描述了 QR 或条形码扫描仪功能 Web 应用体验：

![qr 或条形码扫描仪功能 Web 应用体验](../../assets/images/tabs/qr-barcode-scanner-capability.png)

## <a name="error-handling"></a>错误处理

必须确保在应用应用中正确处理这些Teams错误。 下表列出了错误代码以及生成错误的条件： 

|错误代码 |  错误名称     | 条件|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API 在当前平台上不受支持。|
| **500** | INTERNAL_ERROR | 执行所需操作时遇到内部错误。|
| **1000** | PERMISSION_DENIED |用户拒绝权限。|
| **3000** | NO_HW_SUPPORT | 基础硬件不支持该功能。|
| **4000** | INVALID_ARGUMENTS | 一个或多个参数无效。|
| **8000** | USER_ABORT |用户中止操作。|
| **8001** | OPERATION_TIMED_OUT | 无法检测给定时间间隔的条形码。|
| **9000** | OLD_PLATFORM | 平台代码已过时，不实现此 API。|

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

* [集成媒体中的媒体Teams](mobile-camera-image-permissions.md)
* [在 Teams 中集成位置Teams](location-capability.md)
* [将人员选取器集成到Teams](people-picker-capability.md)

