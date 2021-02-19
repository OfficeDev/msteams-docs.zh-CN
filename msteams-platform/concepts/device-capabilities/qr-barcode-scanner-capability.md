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
# <a name="integrate-qr-or-barcode-scanner-capability"></a><span data-ttu-id="7c864-104">集成 QR 或条形码扫描仪功能</span><span class="sxs-lookup"><span data-stu-id="7c864-104">Integrate QR or barcode scanner capability</span></span> 

<span data-ttu-id="7c864-105">条形码是一种以可视和机器可读的形式表示数据的方法。</span><span class="sxs-lookup"><span data-stu-id="7c864-105">Barcode is a method of representing data in a visual and machine-readable form.</span></span> <span data-ttu-id="7c864-106">条码包含有关产品的信息，如条形图和空格形式的类型、大小、制造商和来源国家/地区。</span><span class="sxs-lookup"><span data-stu-id="7c864-106">The barcode contains information about a product, such as a type, size, manufacturer, and Country of origin in the form of bars and spaces.</span></span> <span data-ttu-id="7c864-107">使用本机设备相机上的光学扫描仪读取代码。</span><span class="sxs-lookup"><span data-stu-id="7c864-107">The code is read using the optical scanner on your native device camera.</span></span> <span data-ttu-id="7c864-108">为了获得更丰富的协作体验，你可以将 Teams 平台中提供的 QR 或条形码扫描仪功能与 Teams 应用集成。</span><span class="sxs-lookup"><span data-stu-id="7c864-108">For a richer collaborative experience, you can integrate the QR or barcode scanner capability provided in the Teams platform with your Teams app.</span></span> <span data-ttu-id="7c864-109">本文档指导您了解如何集成该功能。</span><span class="sxs-lookup"><span data-stu-id="7c864-109">This document guides you on how to integrate the capability.</span></span>  

<span data-ttu-id="7c864-110">可以使用 [Microsoft Teams JavaScript 客户端 SDK，](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)它提供应用访问用户的本机设备功能 [所需的工具](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="7c864-110">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="7c864-111">使用 `scanBarCode` API 将扫描程序功能集成到你的应用中。</span><span class="sxs-lookup"><span data-stu-id="7c864-111">Use the `scanBarCode` API to integrate the scanner capability within your app.</span></span> 

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a><span data-ttu-id="7c864-112">集成 QR 或条形码扫描仪功能的优势</span><span class="sxs-lookup"><span data-stu-id="7c864-112">Advantage of integrating QR or barcode scanner capability</span></span>

* <span data-ttu-id="7c864-113">集成使 Teams 平台上的 Web 应用开发人员能够利用 Teams JavaScript 客户端 SDK 的 QR 或条形码扫描功能。</span><span class="sxs-lookup"><span data-stu-id="7c864-113">The integration allows web app developers on Teams platform to leverage QR or barcode scanning functionality with Teams JavaScript client SDK.</span></span>
* <span data-ttu-id="7c864-114">使用此功能，用户只需在扫描仪 UI 中心的框架内对齐 QR 或条形码，代码将自动扫描。</span><span class="sxs-lookup"><span data-stu-id="7c864-114">With this feature, the user only needs to align a QR or barcode within a frame at the center of the scanner UI and the code gets scanned automatically.</span></span> <span data-ttu-id="7c864-115">存储的数据将重新与调用 Web 应用共享。</span><span class="sxs-lookup"><span data-stu-id="7c864-115">The stored data is shared back with the calling web app.</span></span> <span data-ttu-id="7c864-116">这可以避免手动输入长产品代码或其他相关信息的不便和人为错误。</span><span class="sxs-lookup"><span data-stu-id="7c864-116">This avoids the inconvenience and human-errors of entering lengthy product codes or other relevant information manually.</span></span>

<span data-ttu-id="7c864-117">若要集成 QR 或条形码扫描仪功能，必须更新应用清单文件并调用 `scanBarCode` API。</span><span class="sxs-lookup"><span data-stu-id="7c864-117">To integrate QR or barcode scanner capability, you must update the app manifest file and call the `scanBarCode` API.</span></span> <span data-ttu-id="7c864-118">为了进行有效集成，你必须对调用 API[](#code-snippet)的代码段有一个很好的了解，这允许你使用本机 `scanBarCode` QR 或条形码扫描仪功能。</span><span class="sxs-lookup"><span data-stu-id="7c864-118">For effective integration, you must have a good understanding of [code snippet](#code-snippet) for calling the `scanBarCode` API, which allows you to use native QR or barcode scanner capability.</span></span> <span data-ttu-id="7c864-119">API 为不支持的条形码标准提供错误。</span><span class="sxs-lookup"><span data-stu-id="7c864-119">The API gives an error for an unsupported barcode standard.</span></span>
<span data-ttu-id="7c864-120">熟悉 API 响应错误以处理[](#error-handling)Teams 应用中的错误非常重要。</span><span class="sxs-lookup"><span data-stu-id="7c864-120">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="7c864-121">目前，Microsoft Teams 对 QR 或条形码扫描仪功能的支持仅适用于移动客户端。</span><span class="sxs-lookup"><span data-stu-id="7c864-121">Currently, Microsoft Teams support for QR or barcode scanner capability is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="7c864-122">更新清单</span><span class="sxs-lookup"><span data-stu-id="7c864-122">Update manifest</span></span>

<span data-ttu-id="7c864-123">通过 [ 添加manifest.js并](../../resources/schema/manifest-schema.md#devicepermissions) 指定来更新 Teams 应用文件 `devicePermissions` `media` 。</span><span class="sxs-lookup"><span data-stu-id="7c864-123">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="7c864-124">它允许你的应用在开始使用 QR 或条形码扫描仪功能之前向用户请求必要的权限。</span><span class="sxs-lookup"><span data-stu-id="7c864-124">It allows your app to ask for requisite permissions from users before they start using  the QR or barcode scanner capability.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="7c864-125">启动 **相关** Teams API 时，将自动显示请求权限提示。</span><span class="sxs-lookup"><span data-stu-id="7c864-125">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="7c864-126">有关详细信息，请参阅"[请求设备权限"。](native-device-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="7c864-126">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="scanbarcode-api"></a><span data-ttu-id="7c864-127">ScanBarCode API</span><span class="sxs-lookup"><span data-stu-id="7c864-127">ScanBarCode API</span></span>

<span data-ttu-id="7c864-128">API 调用扫描程序控件，使用户可以扫描不同类型的条形码，并返回 `ScanBarCode` 字符串形式的结果。</span><span class="sxs-lookup"><span data-stu-id="7c864-128">The `ScanBarCode` API invokes scanner control that enables the user to scan different types of barcode, and returns the result as a string.</span></span>

<span data-ttu-id="7c864-129">若要自定义条形码扫描体验，可选条形码配置作为输入传递到 `ScanBarCode` API。</span><span class="sxs-lookup"><span data-stu-id="7c864-129">To customize the barcode scanning experience, optional barcode configuration is passed as input to `ScanBarCode` API.</span></span> <span data-ttu-id="7c864-130">可以使用 .指定扫描的间隔（以秒为单位 `timeOutIntervalInSec` ）。</span><span class="sxs-lookup"><span data-stu-id="7c864-130">You can specify the scan time-out interval in seconds using `timeOutIntervalInSec`.</span></span> <span data-ttu-id="7c864-131">其默认值为 30 秒，最大值为 60 秒。</span><span class="sxs-lookup"><span data-stu-id="7c864-131">Its default value is 30 seconds and the maximum value is 60 seconds.</span></span>

<span data-ttu-id="7c864-132">**scanBarCode ()** API 支持以下条形码类型：</span><span class="sxs-lookup"><span data-stu-id="7c864-132">The **scanBarCode()** API supports the following barcode types:</span></span>

| <span data-ttu-id="7c864-133">条形码类型</span><span class="sxs-lookup"><span data-stu-id="7c864-133">Barcode Type</span></span> | <span data-ttu-id="7c864-134">在 Android 上受支持</span><span class="sxs-lookup"><span data-stu-id="7c864-134">Supported on Android</span></span> | <span data-ttu-id="7c864-135">在 iOS 上受支持</span><span class="sxs-lookup"><span data-stu-id="7c864-135">Supported on iOS</span></span> |
| ---------- | ---------- | ------------ |
| <span data-ttu-id="7c864-136">代码栏</span><span class="sxs-lookup"><span data-stu-id="7c864-136">Codebar</span></span> | <span data-ttu-id="7c864-137">是</span><span class="sxs-lookup"><span data-stu-id="7c864-137">Yes</span></span> | <span data-ttu-id="7c864-138">否</span><span class="sxs-lookup"><span data-stu-id="7c864-138">No</span></span> |
| <span data-ttu-id="7c864-139">代码 39</span><span class="sxs-lookup"><span data-stu-id="7c864-139">Code 39</span></span> | <span data-ttu-id="7c864-140">是</span><span class="sxs-lookup"><span data-stu-id="7c864-140">Yes</span></span> | <span data-ttu-id="7c864-141">是</span><span class="sxs-lookup"><span data-stu-id="7c864-141">Yes</span></span> | 
| <span data-ttu-id="7c864-142">代码 93</span><span class="sxs-lookup"><span data-stu-id="7c864-142">Code 93</span></span> | <span data-ttu-id="7c864-143">是</span><span class="sxs-lookup"><span data-stu-id="7c864-143">Yes</span></span> | <span data-ttu-id="7c864-144">是</span><span class="sxs-lookup"><span data-stu-id="7c864-144">Yes</span></span> |
| <span data-ttu-id="7c864-145">代码 128</span><span class="sxs-lookup"><span data-stu-id="7c864-145">Code 128</span></span> | <span data-ttu-id="7c864-146">是</span><span class="sxs-lookup"><span data-stu-id="7c864-146">Yes</span></span> | <span data-ttu-id="7c864-147">是</span><span class="sxs-lookup"><span data-stu-id="7c864-147">Yes</span></span> |
| <span data-ttu-id="7c864-148">EAN-13</span><span class="sxs-lookup"><span data-stu-id="7c864-148">EAN-13</span></span> | <span data-ttu-id="7c864-149">是</span><span class="sxs-lookup"><span data-stu-id="7c864-149">Yes</span></span> | <span data-ttu-id="7c864-150">是</span><span class="sxs-lookup"><span data-stu-id="7c864-150">Yes</span></span> |
| <span data-ttu-id="7c864-151">EAN-8</span><span class="sxs-lookup"><span data-stu-id="7c864-151">EAN-8</span></span> | <span data-ttu-id="7c864-152">是</span><span class="sxs-lookup"><span data-stu-id="7c864-152">Yes</span></span> | <span data-ttu-id="7c864-153">是</span><span class="sxs-lookup"><span data-stu-id="7c864-153">Yes</span></span> |
| <span data-ttu-id="7c864-154">ITF</span><span class="sxs-lookup"><span data-stu-id="7c864-154">ITF</span></span> | <span data-ttu-id="7c864-155">否</span><span class="sxs-lookup"><span data-stu-id="7c864-155">No</span></span> | <span data-ttu-id="7c864-156">是</span><span class="sxs-lookup"><span data-stu-id="7c864-156">Yes</span></span> |
| <span data-ttu-id="7c864-157">QR 代码</span><span class="sxs-lookup"><span data-stu-id="7c864-157">QR Code</span></span> | <span data-ttu-id="7c864-158">是</span><span class="sxs-lookup"><span data-stu-id="7c864-158">Yes</span></span> | <span data-ttu-id="7c864-159">是</span><span class="sxs-lookup"><span data-stu-id="7c864-159">Yes</span></span> |
| <span data-ttu-id="7c864-160">RSS 扩展</span><span class="sxs-lookup"><span data-stu-id="7c864-160">RSS Expanded</span></span> | <span data-ttu-id="7c864-161">是</span><span class="sxs-lookup"><span data-stu-id="7c864-161">Yes</span></span> | <span data-ttu-id="7c864-162">否</span><span class="sxs-lookup"><span data-stu-id="7c864-162">No</span></span> |
| <span data-ttu-id="7c864-163">RSS-14</span><span class="sxs-lookup"><span data-stu-id="7c864-163">RSS-14</span></span> | <span data-ttu-id="7c864-164">是</span><span class="sxs-lookup"><span data-stu-id="7c864-164">Yes</span></span> | <span data-ttu-id="7c864-165">否</span><span class="sxs-lookup"><span data-stu-id="7c864-165">No</span></span> |
| <span data-ttu-id="7c864-166">UPC-A</span><span class="sxs-lookup"><span data-stu-id="7c864-166">UPC-A</span></span> | <span data-ttu-id="7c864-167">是</span><span class="sxs-lookup"><span data-stu-id="7c864-167">Yes</span></span> | <span data-ttu-id="7c864-168">是</span><span class="sxs-lookup"><span data-stu-id="7c864-168">Yes</span></span> |
| <span data-ttu-id="7c864-169">UPC-E</span><span class="sxs-lookup"><span data-stu-id="7c864-169">UPC-E</span></span> | <span data-ttu-id="7c864-170">是</span><span class="sxs-lookup"><span data-stu-id="7c864-170">Yes</span></span> | <span data-ttu-id="7c864-171">是</span><span class="sxs-lookup"><span data-stu-id="7c864-171">Yes</span></span> |

<span data-ttu-id="7c864-172">**Web 应用体验 `ScanBarCode`QR 或条形码扫描仪功能** 
 ![ Web 应用体验的 API（qr 或条形码扫描仪功能）](../../assets/images/tabs/qr-barcode-scanner-capability.png)</span><span class="sxs-lookup"><span data-stu-id="7c864-172">**Web app experience for `ScanBarCode` API for QR or barcode scanner capability**
![web app experience for qr or barcode scanner capability](../../assets/images/tabs/qr-barcode-scanner-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="7c864-173">错误处理</span><span class="sxs-lookup"><span data-stu-id="7c864-173">Error handling</span></span>

<span data-ttu-id="7c864-174">必须确保在 Teams 应用中正确处理这些错误。</span><span class="sxs-lookup"><span data-stu-id="7c864-174">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="7c864-175">下表列出了错误代码以及生成错误的条件：</span><span class="sxs-lookup"><span data-stu-id="7c864-175">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="7c864-176">错误代码</span><span class="sxs-lookup"><span data-stu-id="7c864-176">Error code</span></span> |  <span data-ttu-id="7c864-177">错误名称</span><span class="sxs-lookup"><span data-stu-id="7c864-177">Error name</span></span>     | <span data-ttu-id="7c864-178">Condition</span><span class="sxs-lookup"><span data-stu-id="7c864-178">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="7c864-179">**100**</span><span class="sxs-lookup"><span data-stu-id="7c864-179">**100**</span></span> | <span data-ttu-id="7c864-180">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="7c864-180">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="7c864-181">API 在当前平台上不受支持。</span><span class="sxs-lookup"><span data-stu-id="7c864-181">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="7c864-182">**500**</span><span class="sxs-lookup"><span data-stu-id="7c864-182">**500**</span></span> | <span data-ttu-id="7c864-183">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="7c864-183">INTERNAL_ERROR</span></span> | <span data-ttu-id="7c864-184">执行所需操作时遇到内部错误。</span><span class="sxs-lookup"><span data-stu-id="7c864-184">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="7c864-185">**1000**</span><span class="sxs-lookup"><span data-stu-id="7c864-185">**1000**</span></span> | <span data-ttu-id="7c864-186">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="7c864-186">PERMISSION_DENIED</span></span> |<span data-ttu-id="7c864-187">用户拒绝权限。</span><span class="sxs-lookup"><span data-stu-id="7c864-187">Permission is denied by the user.</span></span>|
| <span data-ttu-id="7c864-188">**3000**</span><span class="sxs-lookup"><span data-stu-id="7c864-188">**3000**</span></span> | <span data-ttu-id="7c864-189">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="7c864-189">NO_HW_SUPPORT</span></span> | <span data-ttu-id="7c864-190">基础硬件不支持该功能。</span><span class="sxs-lookup"><span data-stu-id="7c864-190">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="7c864-191">**4000**</span><span class="sxs-lookup"><span data-stu-id="7c864-191">**4000**</span></span> | <span data-ttu-id="7c864-192">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="7c864-192">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="7c864-193">一个或多个参数无效。</span><span class="sxs-lookup"><span data-stu-id="7c864-193">One or more arguments are invalid.</span></span>|
| <span data-ttu-id="7c864-194">**8000**</span><span class="sxs-lookup"><span data-stu-id="7c864-194">**8000**</span></span> | <span data-ttu-id="7c864-195">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="7c864-195">USER_ABORT</span></span> |<span data-ttu-id="7c864-196">用户中止操作。</span><span class="sxs-lookup"><span data-stu-id="7c864-196">User aborts the operation.</span></span>|
| <span data-ttu-id="7c864-197">**8001**</span><span class="sxs-lookup"><span data-stu-id="7c864-197">**8001**</span></span> | <span data-ttu-id="7c864-198">OPERATION_TIMED_OUT</span><span class="sxs-lookup"><span data-stu-id="7c864-198">OPERATION_TIMED_OUT</span></span> | <span data-ttu-id="7c864-199">无法检测给定时间间隔中的条码。</span><span class="sxs-lookup"><span data-stu-id="7c864-199">Could not detect the barcode in the given time interval.</span></span>|
| <span data-ttu-id="7c864-200">**9000**</span><span class="sxs-lookup"><span data-stu-id="7c864-200">**9000**</span></span> | <span data-ttu-id="7c864-201">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="7c864-201">OLD_PLATFORM</span></span> | <span data-ttu-id="7c864-202">平台代码已过时，未实现此 API。</span><span class="sxs-lookup"><span data-stu-id="7c864-202">Platform code is outdated and does not implement this API.</span></span>|

## <a name="code-snippet"></a><span data-ttu-id="7c864-203">代码段</span><span class="sxs-lookup"><span data-stu-id="7c864-203">Code snippet</span></span>

<span data-ttu-id="7c864-204">**呼叫 `ScanBarCode()` 用于** 使用相机扫描 QR 或条形码的 API：</span><span class="sxs-lookup"><span data-stu-id="7c864-204">**Calling `ScanBarCode()` API** for scanning QR or barcode using camera:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="7c864-205">另请参阅</span><span class="sxs-lookup"><span data-stu-id="7c864-205">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7c864-206">在 Teams 中集成媒体功能</span><span class="sxs-lookup"><span data-stu-id="7c864-206">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
