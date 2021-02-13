---
title: 设备功能概述
description: 本机设备功能概述。
keywords: 相机图像媒体麦克风功能本机设备权限
ms.topic: overview
ms.openlocfilehash: 8b2f92cb4586d646bde02742883122bb009847ea
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2021
ms.locfileid: "50232845"
---
# <a name="device-capabilities"></a><span data-ttu-id="dac87-104">设备功能</span><span class="sxs-lookup"><span data-stu-id="dac87-104">Device capabilities</span></span> 

<span data-ttu-id="dac87-105">Microsoft Teams 平台不断增强开发人员功能，以与内置的第一方体验保持一致。</span><span class="sxs-lookup"><span data-stu-id="dac87-105">Microsoft Teams platform is continuously enhancing developer capabilities aligning with built-in first-party experiences.</span></span> <span data-ttu-id="dac87-106">借助增强的 Teams 平台，合作伙伴可以将设备功能（如相机、照片库、麦克风和位置）与 Web 应用集成。</span><span class="sxs-lookup"><span data-stu-id="dac87-106">The enhanced Teams platform allows partners to integrate device capabilities, such as camera, photo gallery, microphone, and location, with their web apps.</span></span> <span data-ttu-id="dac87-107">此集成减少了应用开发障碍，加快了开发周期，并创建了开发人员社区的新方案或用例。</span><span class="sxs-lookup"><span data-stu-id="dac87-107">This integration reduces the barrier to app development, speeds-up development-cycle, and creates new scenarios or use-cases for the developer community.</span></span>

## <a name="native-device-capabilities"></a><span data-ttu-id="dac87-108">本机设备功能</span><span class="sxs-lookup"><span data-stu-id="dac87-108">Native device capabilities</span></span>

<span data-ttu-id="dac87-109">移动或桌面设备具有内置的设备，如相机和麦克风，称为功能。</span><span class="sxs-lookup"><span data-stu-id="dac87-109">A mobile or desktop device has built-in devices, such as a camera and microphone, called capabilities.</span></span> <span data-ttu-id="dac87-110">可以通过 Microsoft Teams JavaScript 客户端 SDK 中提供的专用 API 访问移动或 [桌面上的以下设备功能](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)：</span><span class="sxs-lookup"><span data-stu-id="dac87-110">You can access the following device capabilities on mobile or desktop through dedicated APIs available in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true):</span></span>
* <span data-ttu-id="dac87-111">媒体功能，例如</span><span class="sxs-lookup"><span data-stu-id="dac87-111">Media capabilities, such as</span></span>
    * <span data-ttu-id="dac87-112">相机</span><span class="sxs-lookup"><span data-stu-id="dac87-112">Camera</span></span>
    * <span data-ttu-id="dac87-113">麦克风</span><span class="sxs-lookup"><span data-stu-id="dac87-113">Microphone</span></span>
    * <span data-ttu-id="dac87-114">库</span><span class="sxs-lookup"><span data-stu-id="dac87-114">Gallery</span></span>
* <span data-ttu-id="dac87-115">位置</span><span class="sxs-lookup"><span data-stu-id="dac87-115">Location</span></span>

<span data-ttu-id="dac87-116">获取设备功能的访问权限后，你可以将其与 Teams 平台集成，以增强协作体验。</span><span class="sxs-lookup"><span data-stu-id="dac87-116">After getting access to the device capabilities, you can integrate them with Teams platform to enhance the collaborative experience.</span></span> 

## <a name="request-device-permissions"></a><span data-ttu-id="dac87-117">请求设备权限</span><span class="sxs-lookup"><span data-stu-id="dac87-117">Request device permissions</span></span>

<span data-ttu-id="dac87-118">使用[Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)中提供[](native-device-permissions.md)的工具请求访问本机设备功能所需的权限。</span><span class="sxs-lookup"><span data-stu-id="dac87-118">Use the tools present in [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) to  request the required  [permissions](native-device-permissions.md) for  accessing the native device capabilities.</span></span> <span data-ttu-id="dac87-119">虽然新式 Web 浏览器中对这些功能的访问是标准功能，但你必须通过更新应用清单来通知 Teams 你使用的功能。</span><span class="sxs-lookup"><span data-stu-id="dac87-119">While access to these capabilities is standard in modern web browsers, you must inform Teams about the capabilities that you are using by updating your app manifest.</span></span> <span data-ttu-id="dac87-120">此更新允许你在应用在 Teams 移动客户端或桌面客户端上运行时请求权限。</span><span class="sxs-lookup"><span data-stu-id="dac87-120">This update allows you to request permissions while your app runs on Teams mobile or desktop clients.</span></span>
 
 ## <a name="integrate-device-capabilities"></a><span data-ttu-id="dac87-121">集成设备功能</span><span class="sxs-lookup"><span data-stu-id="dac87-121">Integrate device capabilities</span></span>

<span data-ttu-id="dac87-122">获取设备功能的访问权限后，使用 **Teams 媒体** 功能 API [](mobile-camera-image-permissions.md)将功能与 Teams 平台集成，以增强用户体验。</span><span class="sxs-lookup"><span data-stu-id="dac87-122">After getting access to device capabilities,use **Teams media capability APIs** to [integrate the capabilities](mobile-camera-image-permissions.md) with Teams platform to enhance the user experience.</span></span> <span data-ttu-id="dac87-123">这些集成功能允许应用：</span><span class="sxs-lookup"><span data-stu-id="dac87-123">These integrated capabilities allow your app to:</span></span>

* <span data-ttu-id="dac87-124">捕获和共享图像</span><span class="sxs-lookup"><span data-stu-id="dac87-124">Capture and share images</span></span>
* <span data-ttu-id="dac87-125">通过麦克风录制音频</span><span class="sxs-lookup"><span data-stu-id="dac87-125">Record audio through microphone</span></span>
* <span data-ttu-id="dac87-126">共享位置信息</span><span class="sxs-lookup"><span data-stu-id="dac87-126">Share the location information</span></span>


