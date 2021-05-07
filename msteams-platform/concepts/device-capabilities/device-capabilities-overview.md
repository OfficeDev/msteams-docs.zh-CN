---
title: 设备功能 - 概述
author: Rajeshwari-v
description: 本机设备功能概述。
ms.author: surbhigupta
keywords: 相机图像媒体麦克风麦克风 qr 代码 qrcode 条形码条形码扫描扫描仪位置映射功能本机设备权限
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: d67b343e3e07d7aea79282ce02ef8247fcf77159
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230895"
---
# <a name="device-capabilities"></a><span data-ttu-id="2f17e-104">设备功能</span><span class="sxs-lookup"><span data-stu-id="2f17e-104">Device capabilities</span></span>

<span data-ttu-id="2f17e-105">Microsoft Teams平台持续增强开发人员功能，以与内置第一方体验保持一致。</span><span class="sxs-lookup"><span data-stu-id="2f17e-105">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="2f17e-106">借助增强Teams平台，合作伙伴可以将设备功能（如相机、QR 或条形码扫描仪、照片库、麦克风和位置）与 Web 应用集成。</span><span class="sxs-lookup"><span data-stu-id="2f17e-106">The enhanced Teams platform allows partners to integrate device capabilities, such as camera, QR or barcode scanner, photo gallery, microphone, and location with their web apps.</span></span> <span data-ttu-id="2f17e-107">此集成减少了应用开发障碍，加快了开发周期，并创建了开发人员社区的新方案或用例。</span><span class="sxs-lookup"><span data-stu-id="2f17e-107">This integration reduces the barrier to app development, speeds-up development-cycle, and creates new scenarios or use-cases for the developer community.</span></span>

## <a name="native-device-capabilities"></a><span data-ttu-id="2f17e-108">本机设备功能</span><span class="sxs-lookup"><span data-stu-id="2f17e-108">Native device capabilities</span></span>

<span data-ttu-id="2f17e-109">移动或桌面设备具有内置的设备，如相机和麦克风，称为功能。</span><span class="sxs-lookup"><span data-stu-id="2f17e-109">A mobile or desktop device has built-in devices, such as a camera and microphone, called capabilities.</span></span> <span data-ttu-id="2f17e-110">可以通过 JavaScript 客户端 SDK 中提供的专用 API 在移动或桌面上Microsoft Teams[以下设备功能](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)：</span><span class="sxs-lookup"><span data-stu-id="2f17e-110">You can access the following device capabilities on mobile or desktop through dedicated APIs available in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span></span>
* <span data-ttu-id="2f17e-111">媒体功能，例如</span><span class="sxs-lookup"><span data-stu-id="2f17e-111">Media capabilities, such as</span></span>
    * <span data-ttu-id="2f17e-112">相机</span><span class="sxs-lookup"><span data-stu-id="2f17e-112">Camera</span></span>
    * <span data-ttu-id="2f17e-113">麦克风</span><span class="sxs-lookup"><span data-stu-id="2f17e-113">Microphone</span></span>
    * <span data-ttu-id="2f17e-114">库</span><span class="sxs-lookup"><span data-stu-id="2f17e-114">Gallery</span></span>
    * <span data-ttu-id="2f17e-115">QR 或条形码扫描仪</span><span class="sxs-lookup"><span data-stu-id="2f17e-115">QR or barcode scanner</span></span>
* <span data-ttu-id="2f17e-116">位置</span><span class="sxs-lookup"><span data-stu-id="2f17e-116">Location</span></span>

<span data-ttu-id="2f17e-117">获取设备功能的访问权限后，你可以将其与 Teams 平台集成，以增强协作体验。</span><span class="sxs-lookup"><span data-stu-id="2f17e-117">After getting access to the device capabilities, you can integrate them with Teams platform to enhance the collaborative experience.</span></span> 

## <a name="request-device-permissions"></a><span data-ttu-id="2f17e-118">请求设备权限</span><span class="sxs-lookup"><span data-stu-id="2f17e-118">Request device permissions</span></span>

<span data-ttu-id="2f17e-119">使用[JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)客户端 SDK Microsoft Teams中的工具请求访问本机设备功能[](native-device-permissions.md)所需的权限。</span><span class="sxs-lookup"><span data-stu-id="2f17e-119">Use the tools present in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) to request the required  [permissions](native-device-permissions.md) for accessing the native device capabilities.</span></span> <span data-ttu-id="2f17e-120">虽然新式 Web 浏览器中对这些功能的访问是标准操作，但你必须Teams更新应用清单来通知用户有关你使用的功能的信息。</span><span class="sxs-lookup"><span data-stu-id="2f17e-120">While access to these capabilities is standard in modern web browsers, you must inform Teams about the capabilities that you are using by updating your app manifest.</span></span> <span data-ttu-id="2f17e-121">此更新允许你在移动或桌面客户端上运行应用Teams请求权限。</span><span class="sxs-lookup"><span data-stu-id="2f17e-121">This update allows you to request permissions while your app runs on Teams mobile or desktop clients.</span></span>
 
 ## <a name="integrate-device-capabilities"></a><span data-ttu-id="2f17e-122">集成设备功能</span><span class="sxs-lookup"><span data-stu-id="2f17e-122">Integrate device capabilities</span></span>

<span data-ttu-id="2f17e-123">获取设备功能的访问权限后，Teams媒体功能 API 将[媒体](mobile-camera-image-permissions.md)功能与 Teams 平台集成，以增强用户体验。</span><span class="sxs-lookup"><span data-stu-id="2f17e-123">After getting access to device capabilities, use Teams media capability APIs to [integrate media capabilities](mobile-camera-image-permissions.md) with Teams platform to enhance the user experience.</span></span> <span data-ttu-id="2f17e-124">这些集成功能使你的应用能够：</span><span class="sxs-lookup"><span data-stu-id="2f17e-124">These integrated capabilities allow your app to:</span></span>

* <span data-ttu-id="2f17e-125">捕获和共享图像</span><span class="sxs-lookup"><span data-stu-id="2f17e-125">Capture and share images</span></span>
* <span data-ttu-id="2f17e-126">使用扫描仪控件扫描 QR [或条形码](qr-barcode-scanner-capability.md)</span><span class="sxs-lookup"><span data-stu-id="2f17e-126">Scan QR or barcode using [scanner control](qr-barcode-scanner-capability.md)</span></span>
* <span data-ttu-id="2f17e-127">通过麦克风录制音频</span><span class="sxs-lookup"><span data-stu-id="2f17e-127">Record audio through microphone</span></span>
* <span data-ttu-id="2f17e-128">使用位置选取 [器共享位置](location-capability.md)。</span><span class="sxs-lookup"><span data-stu-id="2f17e-128">Share location using [location picker](location-capability.md).</span></span>
