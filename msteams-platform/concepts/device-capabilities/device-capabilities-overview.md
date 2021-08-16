---
title: 设备功能 - 概述
author: Rajeshwari-v
description: 本机设备功能概述。
ms.author: surbhigupta
keywords: 相机图像媒体麦克风麦克风 qr 代码 qrcode 条形码条形码扫描扫描仪位置映射功能本机设备权限
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: 4b09d4d81301aa8fc125da98a3633dc79e05d3d1
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345723"
---
# <a name="device-capabilities"></a>设备功能

Microsoft Teams平台持续增强开发人员功能，以与内置第一方体验保持一致。 借助增强Teams平台，合作伙伴可以将设备功能（如相机、QR 或条形码扫描仪、照片库、麦克风和位置）与 Web 应用集成。 此集成减少了应用开发障碍，加快了开发周期，并创建了开发人员社区的新方案或用例。

## <a name="native-device-capabilities"></a>本机设备功能

移动或桌面设备具有内置的设备，如相机和麦克风，称为功能。 可以通过 JavaScript 客户端 SDK 中提供的专用 API 在移动或桌面上访问[Microsoft Teams功能](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)：
* 媒体功能，例如
    * 相机
    * 麦克风
    * 库
    * QR 或条形码扫描仪
* 位置

获取设备功能的访问权限后，你可以将其与 Teams 平台集成，以增强协作体验。 

## <a name="request-device-permissions"></a>请求设备权限

使用[JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) Microsoft Teams SDK 中提供的工具请求访问本机设备[](native-device-permissions.md)功能所需的权限。 虽然新式 Web 浏览器中对这些功能的访问是标准操作，但你必须Teams更新应用清单来通知用户有关你使用的功能的信息。 此更新允许你在移动或桌面客户端上运行应用Teams请求权限。
 
 ## <a name="integrate-device-capabilities"></a>集成设备功能

访问设备功能后，Teams媒体功能 API 将[媒体](mobile-camera-image-permissions.md)功能与 Teams 平台集成，以增强用户体验。 这些集成功能使你的应用能够：

* 捕获和共享图像。
* 使用扫描仪控件扫描 QR [或条形码](qr-barcode-scanner-capability.md)。
* 通过麦克风录制音频。
* 使用位置选取 [器共享位置](location-capability.md)。

此外，你可以集成本机Teams选取器控件，以[](people-picker-capability.md)允许用户在 Web 应用体验中搜索和选择人员。


