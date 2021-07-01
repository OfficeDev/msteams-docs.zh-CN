---
title: 集成位置功能
author: Rajeshwari-v
description: 如何使用 JavaScript Teams SDK 利用位置功能
keywords: 位置地图功能本机设备权限
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 3e6c4bda9a1a0024380cb295cd280db1d630f019
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211609"
---
# <a name="integrate-location-capabilities"></a><span data-ttu-id="c9d6f-104">集成位置功能</span><span class="sxs-lookup"><span data-stu-id="c9d6f-104">Integrate location capabilities</span></span> 

<span data-ttu-id="c9d6f-105">你可以将本机设备的位置功能与你的应用Teams集成。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-105">You can integrate the location capabilities of native device with your Teams app.</span></span>  

<span data-ttu-id="c9d6f-106">可以使用[JavaScript Microsoft Teams SDK，](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)它提供应用访问用户的本机设备功能[所需的工具](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-106">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="c9d6f-107">使用位置 API（如 [getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) 和 [showLocation）](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) 将功能集成到你的应用中。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-107">Use the location APIs, such as [getLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) and [showLocation](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) to integrate the capabilities within your app.</span></span> 

## <a name="advantages-of-integrating-location-capabilities"></a><span data-ttu-id="c9d6f-108">集成位置功能的优点</span><span class="sxs-lookup"><span data-stu-id="c9d6f-108">Advantages of integrating location capabilities</span></span>

<span data-ttu-id="c9d6f-109">在 Teams 应用中集成位置功能的主要优点是，它允许 Teams 平台上的 Web 应用开发人员利用 Microsoft Teams JavaScript 客户端 SDK 的位置功能。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-109">The main advantage of integrating location capabilities in your Teams apps is that it allows web app developers on Teams platform to leverage location functionality with Microsoft Teams JavaScript client SDK.</span></span> 

<span data-ttu-id="c9d6f-110">以下示例显示如何在不同方案中使用位置功能的集成：</span><span class="sxs-lookup"><span data-stu-id="c9d6f-110">Following examples show how the integration of location capabilities is used in different scenarios:</span></span>
* <span data-ttu-id="c9d6f-111">在工厂中，主管可以跟踪工作者的出席情况，让他们在工厂附近自家，并通过指定的应用共享它。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-111">In a factory, the supervisor can track the attendance of workers by asking them to take a selfie in the vicinity of the factory and share it through the specified app.</span></span> <span data-ttu-id="c9d6f-112">位置数据也会与图像一起捕获和发送。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-112">The location data also gets captured and sent along with the image.</span></span>
* <span data-ttu-id="c9d6f-113">位置功能使服务提供商的维护人员能够与管理层共享手机网络的真实运行状况数据。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-113">The location capabilities enables the maintenance staff of a service provider to share authentic health data of cellular towers with the management.</span></span> <span data-ttu-id="c9d6f-114">管理层可以比较捕获的位置信息与维护人员提交的数据之间的任何不匹配情况。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-114">The management can compare any mismatch between captured location information and the data submitted by maintenance staff.</span></span>

<span data-ttu-id="c9d6f-115">若要集成位置功能，必须更新应用清单文件并调用 API。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-115">To integrate location capabilities, you must update the app manifest file and call the APIs.</span></span> <span data-ttu-id="c9d6f-116">为了进行有效的集成，您必须深入了解用于调用位置[](#code-snippets)API 的代码段。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-116">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the location APIs.</span></span> <span data-ttu-id="c9d6f-117">熟悉 API 响应错误以处理应用[](#error-handling)内的错误Teams很重要。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-117">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="c9d6f-118">目前Microsoft Teams对位置功能的支持仅适用于移动客户端。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-118">Currently, Microsoft Teams support for location capabilities is available for mobile clients only.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="c9d6f-119">更新清单</span><span class="sxs-lookup"><span data-stu-id="c9d6f-119">Update manifest</span></span>

<span data-ttu-id="c9d6f-120">通过添加 Teams 并[manifest.js](../../resources/schema/manifest-schema.md#devicepermissions) ，更新应用在 `devicePermissions` 文件上的应用 `geolocation` 。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `geolocation`.</span></span> <span data-ttu-id="c9d6f-121">它允许你的应用在开始使用位置功能之前向用户请求必要的权限。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-121">It allows your app to ask for requisite permissions from users before they start using the location capabilities.</span></span> <span data-ttu-id="c9d6f-122">应用清单的更新如下所示：</span><span class="sxs-lookup"><span data-stu-id="c9d6f-122">The update for app manifest is as follows:</span></span>

``` json
"devicePermissions": [
    "geolocation",
],
```

> [!NOTE]
> <span data-ttu-id="c9d6f-123">启动 **相关应用程序** API 时，将自动显示Teams权限提示。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-123">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="c9d6f-124">有关详细信息，请参阅请求 [设备权限](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-124">For more information, see [request device permissions](native-device-permissions.md).</span></span>

## <a name="location-apis"></a><span data-ttu-id="c9d6f-125">位置 API</span><span class="sxs-lookup"><span data-stu-id="c9d6f-125">Location APIs</span></span>

<span data-ttu-id="c9d6f-126">你必须使用以下一组 API 来启用设备的位置功能：</span><span class="sxs-lookup"><span data-stu-id="c9d6f-126">You must use the following set of APIs to enable your device's location capabilities:</span></span>

| <span data-ttu-id="c9d6f-127">API</span><span class="sxs-lookup"><span data-stu-id="c9d6f-127">API</span></span>      | <span data-ttu-id="c9d6f-128">说明</span><span class="sxs-lookup"><span data-stu-id="c9d6f-128">Description</span></span>   |
| --- | --- |
|[<span data-ttu-id="c9d6f-129">getLocation</span><span class="sxs-lookup"><span data-stu-id="c9d6f-129">getLocation</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) | <span data-ttu-id="c9d6f-130">提供用户的当前设备位置或打开本机位置选取器并返回用户选择的位置。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-130">Gives user’s current device location or opens native location picker and returns the location chosen by the user.</span></span> |
|[<span data-ttu-id="c9d6f-131">showLocation</span><span class="sxs-lookup"><span data-stu-id="c9d6f-131">showLocation</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#showLocation_Location___error__SdkError__status__boolean_____void_&preserve-view=true) | <span data-ttu-id="c9d6f-132">在地图上显示位置。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-132">Shows location on map.</span></span> |

> [!NOTE]
> <span data-ttu-id="c9d6f-133">API `getLocation()` 附带以下 [输入配置](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true)和 `allowChooseLocation` `showMap` 。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-133">The `getLocation()` API comes along with following [input configurations](/javascript/api/@microsoft/teams-js/locationprops?view=msteams-client-js-latest&preserve-view=true), `allowChooseLocation` and `showMap`.</span></span> <br/> <span data-ttu-id="c9d6f-134">如果 的 `allowChooseLocation` 值为 *true，* 则用户可以选择他们选择的任何位置。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-134">If the value of `allowChooseLocation` is *true*, then the users can choose any location of their choice.</span></span><br/>  <span data-ttu-id="c9d6f-135">如果值为 *false，* 则用户无法更改其当前位置。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-135">If the value is *false*, then the users cannot change their current location.</span></span><br/> <span data-ttu-id="c9d6f-136">如果 的 `showMap` 值为 *false，* 则提取当前位置而不显示地图。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-136">If the value of `showMap` is *false*, the current location is fetched without displaying the map.</span></span> <span data-ttu-id="c9d6f-137">`showMap` 如果 设置为 true ， `allowChooseLocation` 则 *忽略*。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-137">`showMap` is ignored if `allowChooseLocation` is set to *true*.</span></span>

<span data-ttu-id="c9d6f-138">下图描述了位置功能的 Web 应用体验：</span><span class="sxs-lookup"><span data-stu-id="c9d6f-138">The following image depicts web app experience of location capabilities:</span></span>

![位置功能的 Web 应用体验](../../assets/images/tabs/location-capability.png)

### <a name="code-snippets"></a><span data-ttu-id="c9d6f-140">代码段</span><span class="sxs-lookup"><span data-stu-id="c9d6f-140">Code snippets</span></span>

<span data-ttu-id="c9d6f-141">**调用 `getLocation` API 以检索位置：**</span><span class="sxs-lookup"><span data-stu-id="c9d6f-141">**Calling `getLocation` API to retrieve the location:**</span></span>

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

<span data-ttu-id="c9d6f-142">**调用 `showLocation` API 以显示位置：**</span><span class="sxs-lookup"><span data-stu-id="c9d6f-142">**Calling `showLocation` API to display the location:**</span></span>

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

## <a name="error-handling"></a><span data-ttu-id="c9d6f-143">错误处理</span><span class="sxs-lookup"><span data-stu-id="c9d6f-143">Error handling</span></span>

<span data-ttu-id="c9d6f-144">必须确保在你的应用内正确处理这些Teams错误。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-144">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="c9d6f-145">下表列出了错误代码以及生成错误的条件：</span><span class="sxs-lookup"><span data-stu-id="c9d6f-145">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="c9d6f-146">错误代码</span><span class="sxs-lookup"><span data-stu-id="c9d6f-146">Error code</span></span> |  <span data-ttu-id="c9d6f-147">错误名称</span><span class="sxs-lookup"><span data-stu-id="c9d6f-147">Error name</span></span>     | <span data-ttu-id="c9d6f-148">Condition</span><span class="sxs-lookup"><span data-stu-id="c9d6f-148">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="c9d6f-149">**100**</span><span class="sxs-lookup"><span data-stu-id="c9d6f-149">**100**</span></span> | <span data-ttu-id="c9d6f-150">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="c9d6f-150">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="c9d6f-151">API 在当前平台上不受支持。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-151">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="c9d6f-152">**500**</span><span class="sxs-lookup"><span data-stu-id="c9d6f-152">**500**</span></span> | <span data-ttu-id="c9d6f-153">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="c9d6f-153">INTERNAL_ERROR</span></span> | <span data-ttu-id="c9d6f-154">执行所需操作时遇到内部错误。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-154">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="c9d6f-155">**1000**</span><span class="sxs-lookup"><span data-stu-id="c9d6f-155">**1000**</span></span> | <span data-ttu-id="c9d6f-156">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="c9d6f-156">PERMISSION_DENIED</span></span> |<span data-ttu-id="c9d6f-157">用户拒绝对 Teams 应用或 Web 应用的位置权限。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-157">User denied location permissions to the Teams App or the web-app .</span></span>|
| <span data-ttu-id="c9d6f-158">**4000**</span><span class="sxs-lookup"><span data-stu-id="c9d6f-158">**4000**</span></span> | <span data-ttu-id="c9d6f-159">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="c9d6f-159">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="c9d6f-160">使用错误或不足的强制参数调用 API。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-160">API is invoked with wrong or insufficient mandatory arguments.</span></span>|
| <span data-ttu-id="c9d6f-161">**8000**</span><span class="sxs-lookup"><span data-stu-id="c9d6f-161">**8000**</span></span> | <span data-ttu-id="c9d6f-162">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="c9d6f-162">USER_ABORT</span></span> |<span data-ttu-id="c9d6f-163">用户已取消操作。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-163">User cancelled the operation.</span></span>|
| <span data-ttu-id="c9d6f-164">**9000**</span><span class="sxs-lookup"><span data-stu-id="c9d6f-164">**9000**</span></span> | <span data-ttu-id="c9d6f-165">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="c9d6f-165">OLD_PLATFORM</span></span> | <span data-ttu-id="c9d6f-166">用户位于不存在 API 实现的旧平台版本上。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-166">User is on old platform build where implementation of the API is not present.</span></span> <span data-ttu-id="c9d6f-167">升级版本应该可以解决此问题。</span><span class="sxs-lookup"><span data-stu-id="c9d6f-167">Upgrading the build should resolve the issue.</span></span>|

## <a name="see-also"></a><span data-ttu-id="c9d6f-168">另请参阅</span><span class="sxs-lookup"><span data-stu-id="c9d6f-168">See also</span></span>

* [<span data-ttu-id="c9d6f-169">将媒体功能集成到Teams</span><span class="sxs-lookup"><span data-stu-id="c9d6f-169">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="c9d6f-170">将 QR 代码或条形码扫描仪功能集成到 Teams</span><span class="sxs-lookup"><span data-stu-id="c9d6f-170">Integrate QR code or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
* [<span data-ttu-id="c9d6f-171">将人员选取器功能集成到Teams</span><span class="sxs-lookup"><span data-stu-id="c9d6f-171">Integrate People Picker capability in Teams</span></span>](people-picker-capability.md)
