---
title: 设备功能概述
description: 本机设备功能概述。
keywords: 相机图像媒体麦克风麦克风 qr 代码 qrcode 条码条形码扫描程序功能本机设备权限
ms.topic: overview
ms.openlocfilehash: 03ce0267f7160772e30ec88de2c29f81886b5280
ms.sourcegitcommit: 6ff8d1244ac386641ebf9401804b8df3854b02dc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2021
ms.locfileid: "50294724"
---
# <a name="device-capabilities"></a>设备功能 

Microsoft Teams 平台不断增强开发人员功能，以与内置的第一方体验保持一致。 借助增强的 Teams 平台，合作伙伴可以将设备功能（如相机、QR 或条形码扫描仪、照片库、麦克风和位置）与 Web 应用集成。 此集成减少了应用开发障碍，加快了开发周期，并创建了开发人员社区的新方案或用例。

## <a name="native-device-capabilities"></a>本机设备功能

移动或桌面设备具有内置的设备，如相机和麦克风，称为功能。 可以通过 Microsoft Teams JavaScript 客户端 SDK 中提供的专用 API 访问移动或 [桌面上的以下设备功能](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)：
* 媒体功能，例如
    * 相机
    * 麦克风
    * 库
    * QR 或条形码扫描仪
* 位置

获取设备功能的访问权限后，你可以将其与 Teams 平台集成，以增强协作体验。 

## <a name="request-device-permissions"></a>请求设备权限

使用[Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)中提供[](native-device-permissions.md)的工具请求访问本机设备功能所需的权限。 虽然新式 Web 浏览器中对这些功能的访问是标准功能，但你必须通过更新应用清单来通知 Teams 你使用的功能。 此更新允许你在应用在 Teams 移动客户端或桌面客户端上运行时请求权限。
 
 ## <a name="integrate-device-capabilities"></a>集成设备功能

获取设备功能的访问权限后，使用 Teams 媒体功能 API 将 [媒体](mobile-camera-image-permissions.md) 功能与 Teams 平台集成，以增强用户体验。 这些集成功能允许应用：

* 捕获和共享图像
* 使用扫描仪控件扫描 QR [或条形码](qr-barcode-scanner-capability.md)
* 通过麦克风录制音频
* 共享位置信息
