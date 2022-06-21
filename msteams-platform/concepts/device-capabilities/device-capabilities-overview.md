---
title: 设备功能 - 概述
author: Rajeshwari-v
description: 了解如何将本机设备功能（如相机、图像、媒体、麦克风、QR 代码等）与Microsoft Teams应用集成。
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: 26ca39aea4d759edbce62f43e9c832632d267cf6
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189449"
---
# <a name="device-capabilities"></a>设备功能

Microsoft Teams 平台一直在不断增强与内置第一方体验相匹配的开发人员功能。 增强的 Teams 平台允许合作伙伴将设备功能（如相机、QR 码或条形码扫描程序、照片库、麦克风和位置）与其 Web 应用集成。 此集成可减少应用开发障碍，缩短开发周期，并为开发人员社区创建新方案或用例。

浏览器中的设备权限有所变化。 以前，浏览器处理了如何授予访问权限，现在这些权限在Teams中处理。 有关详细信息，请参阅[浏览器设备权限](browser-device-permissions.md)。

## <a name="native-device-capabilities"></a>原生设备功能

移动设备或桌面设备具有内置设备，如相机和麦克风，称为功能。 可以通过 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) 中提供的专用 API 在移动设备或桌面设备上访问以下设备功能：

* 媒体功能，如
  * 照相机
  * 麦克风
  * 库
  * QR 码或条形码扫描程序。
* 位置

获取设备功能的访问权限后，可以将其与 Teams 平台集成，以增强协作体验。

## <a name="request-device-permissions"></a>请求设备权限

使用 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) 中的工具请求访问原生设备功能所需的[权限](native-device-permissions.md)。 虽然在现代 Web 浏览器中一般都能访问这些功能，但你必须通过更新应用列表来告知 Teams 你正在使用的功能。 此更新允许在应用在 Teams 移动客户端或桌面客户端上运行时请求权限。

## <a name="integrate-device-capabilities"></a>集成设备功能

获取设备功能的访问权限后，使用 Teams 媒体功能 API 将[媒体功能](media-capabilities.md)与 Teams 平台集成，以增强用户体验。 这些集成功能允许应用：

* 捕获和共享图像。
* 使用[扫描程序控件](qr-barcode-scanner-capability.md)扫描 QR 码或条形码。
* 通过麦克风录制音频。
* 使用[位置选取器共享位置](location-capability.md)。

此外，还可以集成 Teams 原生[人员选取器控件](people-picker-capability.md)，使用户能够在 Web 应用体验中搜索和选择人员。

## <a name="code-sample"></a>代码示例

| 示例名称           | 说明 | Node.js    |
|:---------------------|:--------------|:---------|
|设备权限 | 介绍如何演示Teams选项卡示例应用的设备权限。 |[View](<https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs>)|
