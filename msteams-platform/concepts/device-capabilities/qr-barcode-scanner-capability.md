---
title: 集成 QR 或条码扫描仪功能
author: Rajeshwari-v
description: 如何使用 JavaScript Teams SDK 利用 QR 或条形码扫描仪功能
keywords: 相机媒体 qr 代码 qrcode 条形码条形码扫描仪扫描功能本机设备权限
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 9b85de05bea8c9f704f4d8138b041b90e159b10f
ms.sourcegitcommit: 9cabeaed9baf96c8caeb1497f0bc37abdb787d22
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646558"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a><span data-ttu-id="bb065-104">集成 QR 或条码扫描仪功能</span><span class="sxs-lookup"><span data-stu-id="bb065-104">Integrate QR or barcode scanner capability</span></span> 

<span data-ttu-id="bb065-105">本文档指导您如何集成 QR 或条形码扫描仪功能。</span><span class="sxs-lookup"><span data-stu-id="bb065-105">This document guides you on how to integrate the QR or barcode scanner capability.</span></span> 

<span data-ttu-id="bb065-106">条形码是一种以可视和机器可读的形式表示数据的方法。</span><span class="sxs-lookup"><span data-stu-id="bb065-106">Barcode is a method of representing data in a visual and machine-readable form.</span></span> <span data-ttu-id="bb065-107">条码包含有关产品的信息，如条形图和空格形式的类型、大小、制造商和来源国家/地区。</span><span class="sxs-lookup"><span data-stu-id="bb065-107">The barcode contains information about a product, such as a type, size, manufacturer, and Country of origin in the form of bars and spaces.</span></span> <span data-ttu-id="bb065-108">该代码使用本机设备相机上的光学扫描仪进行读取。</span><span class="sxs-lookup"><span data-stu-id="bb065-108">The code is read using the optical scanner on your native device camera.</span></span> <span data-ttu-id="bb065-109">为了获得更丰富的协作体验，你可以将 Teams 平台中提供的 QR 或条形码扫描仪功能与Teams集成。</span><span class="sxs-lookup"><span data-stu-id="bb065-109">For a richer collaborative experience, you can integrate the QR or barcode scanner capability provided in the Teams platform with your Teams app.</span></span>   

<span data-ttu-id="bb065-110">可以使用[JavaScript Microsoft Teams SDK，](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)它提供应用访问用户的本机设备功能[所需的工具](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="bb065-110">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="bb065-111">使用 [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API 将扫描程序功能集成到你的应用中。</span><span class="sxs-lookup"><span data-stu-id="bb065-111">Use the [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API to integrate the scanner capability within your app.</span></span> 

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a><span data-ttu-id="bb065-112">集成 QR 或条形码扫描仪功能的优势</span><span class="sxs-lookup"><span data-stu-id="bb065-112">Advantage of integrating QR or barcode scanner capability</span></span>

<span data-ttu-id="bb065-113">以下是 QR 或条形码扫描仪功能集成的优势：</span><span class="sxs-lookup"><span data-stu-id="bb065-113">Following are the advantages of integration of QR or barcode scanner capabilities:</span></span> 

* <span data-ttu-id="bb065-114">集成使 Web 应用开发者Teams JavaScript 客户端 SDK 利用 QR 或条形码Teams功能。</span><span class="sxs-lookup"><span data-stu-id="bb065-114">The integration allows web app developers on Teams platform to leverage QR or barcode scanning functionality with Teams JavaScript client SDK.</span></span>
* <span data-ttu-id="bb065-115">使用此功能，用户只需在扫描仪 UI 中心的框架内对齐 QR 或条形码，代码将自动扫描。</span><span class="sxs-lookup"><span data-stu-id="bb065-115">With this feature, the user only needs to align a QR or barcode within a frame at the center of the scanner UI and the code gets scanned automatically.</span></span> <span data-ttu-id="bb065-116">存储的数据将重新与调用 Web 应用共享。</span><span class="sxs-lookup"><span data-stu-id="bb065-116">The stored data is shared back with the calling web app.</span></span> <span data-ttu-id="bb065-117">这样可以避免手动输入冗长的产品代码或其他相关信息带来的不便和人为错误。</span><span class="sxs-lookup"><span data-stu-id="bb065-117">This avoids the inconvenience and human-errors of entering lengthy product codes or other relevant information manually.</span></span>

<span data-ttu-id="bb065-118">若要集成 QR 或条形码扫描仪功能，必须更新应用清单文件并调用 [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API。</span><span class="sxs-lookup"><span data-stu-id="bb065-118">To integrate QR or barcode scanner capability, you must update the app manifest file and call the [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API.</span></span> <span data-ttu-id="bb065-119">为了进行有效的集成，你必须深入了解用于调用[scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API 的代码段，这允许你使用本机 QR 或条形码扫描仪功能。 [](#code-snippet)</span><span class="sxs-lookup"><span data-stu-id="bb065-119">For effective integration, you must have a good understanding of [code snippet](#code-snippet) for calling the [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API, which allows you to use native QR or barcode scanner capability.</span></span> <span data-ttu-id="bb065-120">API 为不支持的条形码标准提供错误。</span><span class="sxs-lookup"><span data-stu-id="bb065-120">The API gives an error for an unsupported barcode standard.</span></span>
<span data-ttu-id="bb065-121">熟悉 API 响应错误以处理应用[](#error-handling)内的错误Teams很重要。</span><span class="sxs-lookup"><span data-stu-id="bb065-121">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="bb065-122">目前，Microsoft Teams QR 或条形码扫描仪功能的支持仅适用于移动客户端。</span><span class="sxs-lookup"><span data-stu-id="bb065-122">Currently, Microsoft Teams support for QR or barcode scanner capability is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="bb065-123">更新清单</span><span class="sxs-lookup"><span data-stu-id="bb065-123">Update manifest</span></span>

<span data-ttu-id="bb065-124">通过添加 Teams 并[manifest.js](../../resources/schema/manifest-schema.md#devicepermissions) ，更新应用在 `devicePermissions` 文件上的应用 `media` 。</span><span class="sxs-lookup"><span data-stu-id="bb065-124">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="bb065-125">它允许你的应用在用户开始使用 QR 或条形码扫描仪功能之前向用户请求必要的权限。</span><span class="sxs-lookup"><span data-stu-id="bb065-125">It allows your app to ask for requisite permissions from users before they start using  the QR or barcode scanner capability.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="bb065-126">启动 **相关应用程序** API 时，将自动显示Teams权限提示。</span><span class="sxs-lookup"><span data-stu-id="bb065-126">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="bb065-127">有关详细信息，请参阅请求 [设备权限](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="bb065-127">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="scanbarcode-api"></a><span data-ttu-id="bb065-128">ScanBarCode API</span><span class="sxs-lookup"><span data-stu-id="bb065-128">ScanBarCode API</span></span>

<span data-ttu-id="bb065-129">[scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API 调用扫描程序控件，使用户可以扫描不同类型的条形码，并返回字符串形式的结果。</span><span class="sxs-lookup"><span data-stu-id="bb065-129">The [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API invokes scanner control that enables the user to scan different types of barcode, and returns the result as a string.</span></span>

<span data-ttu-id="bb065-130">若要自定义条形码扫描体验，可选 [条形码配置](/javascript/api/@microsoft/teams-js/microsoftteams.media.barcodeconfig?view=msteams-client-js-latest&preserve-view=true) 作为输入传递到 [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API。</span><span class="sxs-lookup"><span data-stu-id="bb065-130">To customize the barcode scanning experience, optional [barcode configuration](/javascript/api/@microsoft/teams-js/microsoftteams.media.barcodeconfig?view=msteams-client-js-latest&preserve-view=true) is passed as input to [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API.</span></span> <span data-ttu-id="bb065-131">可以使用 指定扫描的退出间隔（以秒为单位 `timeOutIntervalInSec` ）。</span><span class="sxs-lookup"><span data-stu-id="bb065-131">You can specify the scan time-out interval in seconds using `timeOutIntervalInSec`.</span></span> <span data-ttu-id="bb065-132">其默认值为 30 秒，最大值为 60 秒。</span><span class="sxs-lookup"><span data-stu-id="bb065-132">Its default value is 30 seconds and the maximum value is 60 seconds.</span></span>

<span data-ttu-id="bb065-133">**scanBarCode ()** API 支持以下条形码类型：</span><span class="sxs-lookup"><span data-stu-id="bb065-133">The **scanBarCode()** API supports the following barcode types:</span></span>

| <span data-ttu-id="bb065-134">条形码类型</span><span class="sxs-lookup"><span data-stu-id="bb065-134">Barcode Type</span></span> | <span data-ttu-id="bb065-135">在 Android 上受支持</span><span class="sxs-lookup"><span data-stu-id="bb065-135">Supported on Android</span></span> | <span data-ttu-id="bb065-136">在 iOS 上受支持</span><span class="sxs-lookup"><span data-stu-id="bb065-136">Supported on iOS</span></span> |
| ---------- | ---------- | ------------ |
| <span data-ttu-id="bb065-137">代码栏</span><span class="sxs-lookup"><span data-stu-id="bb065-137">Codebar</span></span> | <span data-ttu-id="bb065-138">是</span><span class="sxs-lookup"><span data-stu-id="bb065-138">Yes</span></span> | <span data-ttu-id="bb065-139">否</span><span class="sxs-lookup"><span data-stu-id="bb065-139">No</span></span> |
| <span data-ttu-id="bb065-140">代码 39</span><span class="sxs-lookup"><span data-stu-id="bb065-140">Code 39</span></span> | <span data-ttu-id="bb065-141">是</span><span class="sxs-lookup"><span data-stu-id="bb065-141">Yes</span></span> | <span data-ttu-id="bb065-142">是</span><span class="sxs-lookup"><span data-stu-id="bb065-142">Yes</span></span> | 
| <span data-ttu-id="bb065-143">代码 93</span><span class="sxs-lookup"><span data-stu-id="bb065-143">Code 93</span></span> | <span data-ttu-id="bb065-144">是</span><span class="sxs-lookup"><span data-stu-id="bb065-144">Yes</span></span> | <span data-ttu-id="bb065-145">是</span><span class="sxs-lookup"><span data-stu-id="bb065-145">Yes</span></span> |
| <span data-ttu-id="bb065-146">代码 128</span><span class="sxs-lookup"><span data-stu-id="bb065-146">Code 128</span></span> | <span data-ttu-id="bb065-147">是</span><span class="sxs-lookup"><span data-stu-id="bb065-147">Yes</span></span> | <span data-ttu-id="bb065-148">是</span><span class="sxs-lookup"><span data-stu-id="bb065-148">Yes</span></span> |
| <span data-ttu-id="bb065-149">EAN-13</span><span class="sxs-lookup"><span data-stu-id="bb065-149">EAN-13</span></span> | <span data-ttu-id="bb065-150">是</span><span class="sxs-lookup"><span data-stu-id="bb065-150">Yes</span></span> | <span data-ttu-id="bb065-151">是</span><span class="sxs-lookup"><span data-stu-id="bb065-151">Yes</span></span> |
| <span data-ttu-id="bb065-152">EAN-8</span><span class="sxs-lookup"><span data-stu-id="bb065-152">EAN-8</span></span> | <span data-ttu-id="bb065-153">是</span><span class="sxs-lookup"><span data-stu-id="bb065-153">Yes</span></span> | <span data-ttu-id="bb065-154">是</span><span class="sxs-lookup"><span data-stu-id="bb065-154">Yes</span></span> |
| <span data-ttu-id="bb065-155">ITF</span><span class="sxs-lookup"><span data-stu-id="bb065-155">ITF</span></span> | <span data-ttu-id="bb065-156">否</span><span class="sxs-lookup"><span data-stu-id="bb065-156">No</span></span> | <span data-ttu-id="bb065-157">是</span><span class="sxs-lookup"><span data-stu-id="bb065-157">Yes</span></span> |
| <span data-ttu-id="bb065-158">QR 码</span><span class="sxs-lookup"><span data-stu-id="bb065-158">QR Code</span></span> | <span data-ttu-id="bb065-159">是</span><span class="sxs-lookup"><span data-stu-id="bb065-159">Yes</span></span> | <span data-ttu-id="bb065-160">是</span><span class="sxs-lookup"><span data-stu-id="bb065-160">Yes</span></span> |
| <span data-ttu-id="bb065-161">RSS 展开</span><span class="sxs-lookup"><span data-stu-id="bb065-161">RSS Expanded</span></span> | <span data-ttu-id="bb065-162">是</span><span class="sxs-lookup"><span data-stu-id="bb065-162">Yes</span></span> | <span data-ttu-id="bb065-163">否</span><span class="sxs-lookup"><span data-stu-id="bb065-163">No</span></span> |
| <span data-ttu-id="bb065-164">RSS-14</span><span class="sxs-lookup"><span data-stu-id="bb065-164">RSS-14</span></span> | <span data-ttu-id="bb065-165">是</span><span class="sxs-lookup"><span data-stu-id="bb065-165">Yes</span></span> | <span data-ttu-id="bb065-166">否</span><span class="sxs-lookup"><span data-stu-id="bb065-166">No</span></span> |
| <span data-ttu-id="bb065-167">UPC-A</span><span class="sxs-lookup"><span data-stu-id="bb065-167">UPC-A</span></span> | <span data-ttu-id="bb065-168">是</span><span class="sxs-lookup"><span data-stu-id="bb065-168">Yes</span></span> | <span data-ttu-id="bb065-169">是</span><span class="sxs-lookup"><span data-stu-id="bb065-169">Yes</span></span> |
| <span data-ttu-id="bb065-170">UPC-E</span><span class="sxs-lookup"><span data-stu-id="bb065-170">UPC-E</span></span> | <span data-ttu-id="bb065-171">是</span><span class="sxs-lookup"><span data-stu-id="bb065-171">Yes</span></span> | <span data-ttu-id="bb065-172">是</span><span class="sxs-lookup"><span data-stu-id="bb065-172">Yes</span></span> |

<span data-ttu-id="bb065-173">**的 Web 应用体验 `ScanBarCode`QR 或条形码扫描仪功能** 
 ![ Web 应用体验的 API，适用于 qr 或条形码扫描仪功能](../../assets/images/tabs/qr-barcode-scanner-capability.png)</span><span class="sxs-lookup"><span data-stu-id="bb065-173">**Web app experience for `ScanBarCode` API for QR or barcode scanner capability**
![web app experience for qr or barcode scanner capability](../../assets/images/tabs/qr-barcode-scanner-capability.png)</span></span>

## <a name="error-handling"></a><span data-ttu-id="bb065-174">错误处理</span><span class="sxs-lookup"><span data-stu-id="bb065-174">Error handling</span></span>

<span data-ttu-id="bb065-175">必须确保在你的应用内正确处理这些Teams错误。</span><span class="sxs-lookup"><span data-stu-id="bb065-175">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="bb065-176">下表列出了错误代码以及生成错误的条件：</span><span class="sxs-lookup"><span data-stu-id="bb065-176">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="bb065-177">错误代码</span><span class="sxs-lookup"><span data-stu-id="bb065-177">Error code</span></span> |  <span data-ttu-id="bb065-178">错误名称</span><span class="sxs-lookup"><span data-stu-id="bb065-178">Error name</span></span>     | <span data-ttu-id="bb065-179">Condition</span><span class="sxs-lookup"><span data-stu-id="bb065-179">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="bb065-180">**100**</span><span class="sxs-lookup"><span data-stu-id="bb065-180">**100**</span></span> | <span data-ttu-id="bb065-181">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="bb065-181">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="bb065-182">API 在当前平台上不受支持。</span><span class="sxs-lookup"><span data-stu-id="bb065-182">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="bb065-183">**500**</span><span class="sxs-lookup"><span data-stu-id="bb065-183">**500**</span></span> | <span data-ttu-id="bb065-184">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="bb065-184">INTERNAL_ERROR</span></span> | <span data-ttu-id="bb065-185">执行所需操作时遇到内部错误。</span><span class="sxs-lookup"><span data-stu-id="bb065-185">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="bb065-186">**1000**</span><span class="sxs-lookup"><span data-stu-id="bb065-186">**1000**</span></span> | <span data-ttu-id="bb065-187">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="bb065-187">PERMISSION_DENIED</span></span> |<span data-ttu-id="bb065-188">用户拒绝权限。</span><span class="sxs-lookup"><span data-stu-id="bb065-188">Permission is denied by the user.</span></span>|
| <span data-ttu-id="bb065-189">**3000**</span><span class="sxs-lookup"><span data-stu-id="bb065-189">**3000**</span></span> | <span data-ttu-id="bb065-190">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="bb065-190">NO_HW_SUPPORT</span></span> | <span data-ttu-id="bb065-191">基础硬件不支持该功能。</span><span class="sxs-lookup"><span data-stu-id="bb065-191">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="bb065-192">**4000**</span><span class="sxs-lookup"><span data-stu-id="bb065-192">**4000**</span></span> | <span data-ttu-id="bb065-193">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="bb065-193">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="bb065-194">一个或多个参数无效。</span><span class="sxs-lookup"><span data-stu-id="bb065-194">One or more arguments are invalid.</span></span>|
| <span data-ttu-id="bb065-195">**8000**</span><span class="sxs-lookup"><span data-stu-id="bb065-195">**8000**</span></span> | <span data-ttu-id="bb065-196">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="bb065-196">USER_ABORT</span></span> |<span data-ttu-id="bb065-197">用户中止操作。</span><span class="sxs-lookup"><span data-stu-id="bb065-197">User aborts the operation.</span></span>|
| <span data-ttu-id="bb065-198">**8001**</span><span class="sxs-lookup"><span data-stu-id="bb065-198">**8001**</span></span> | <span data-ttu-id="bb065-199">OPERATION_TIMED_OUT</span><span class="sxs-lookup"><span data-stu-id="bb065-199">OPERATION_TIMED_OUT</span></span> | <span data-ttu-id="bb065-200">无法检测给定时间间隔的条形码。</span><span class="sxs-lookup"><span data-stu-id="bb065-200">Could not detect the barcode in the given time interval.</span></span>|
| <span data-ttu-id="bb065-201">**9000**</span><span class="sxs-lookup"><span data-stu-id="bb065-201">**9000**</span></span> | <span data-ttu-id="bb065-202">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="bb065-202">OLD_PLATFORM</span></span> | <span data-ttu-id="bb065-203">平台代码已过时，不实现此 API。</span><span class="sxs-lookup"><span data-stu-id="bb065-203">Platform code is outdated and does not implement this API.</span></span>|

## <a name="code-snippet"></a><span data-ttu-id="bb065-204">代码段</span><span class="sxs-lookup"><span data-stu-id="bb065-204">Code snippet</span></span>

<span data-ttu-id="bb065-205">**呼叫 `ScanBarCode()` 用于** 使用相机扫描 QR 或条形码的 API：</span><span class="sxs-lookup"><span data-stu-id="bb065-205">**Calling `ScanBarCode()` API** for scanning QR or barcode using camera:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="bb065-206">另请参阅</span><span class="sxs-lookup"><span data-stu-id="bb065-206">See also</span></span>

* [<span data-ttu-id="bb065-207">将媒体功能集成到Teams</span><span class="sxs-lookup"><span data-stu-id="bb065-207">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="bb065-208">在 Teams 中集成位置Teams</span><span class="sxs-lookup"><span data-stu-id="bb065-208">Integrate location capabilities in Teams</span></span>](location-capability.md)
