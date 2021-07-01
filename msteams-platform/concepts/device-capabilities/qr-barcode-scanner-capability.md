---
title: 集成 QR 或条码扫描仪功能
author: Rajeshwari-v
description: 如何使用 JavaScript Teams SDK 利用 QR 或条形码扫描仪功能
keywords: 相机媒体 qr 代码 qrcode 条形码条形码扫描仪扫描功能本机设备权限
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 4e34e75a6b439c67c831352e07344fd2cf011543
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211574"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a><span data-ttu-id="c817d-104">集成 QR 或条码扫描仪功能</span><span class="sxs-lookup"><span data-stu-id="c817d-104">Integrate QR or barcode scanner capability</span></span> 

<span data-ttu-id="c817d-105">条形码是一种以可视和机器可读的形式表示数据的方法。</span><span class="sxs-lookup"><span data-stu-id="c817d-105">Barcode is a method of representing data in a visual and machine-readable form.</span></span> <span data-ttu-id="c817d-106">条码包含有关产品的信息，如条形图和空格形式的类型、大小、制造商和来源国家/地区。</span><span class="sxs-lookup"><span data-stu-id="c817d-106">The barcode contains information about a product, such as a type, size, manufacturer, and Country of origin in the form of bars and spaces.</span></span> <span data-ttu-id="c817d-107">该代码使用本机设备相机上的光学扫描仪进行读取。</span><span class="sxs-lookup"><span data-stu-id="c817d-107">The code is read using the optical scanner on your native device camera.</span></span> <span data-ttu-id="c817d-108">为了获得更丰富的协作体验，你可以将 Teams 平台中提供的 QR 或条形码扫描仪功能与Teams集成。</span><span class="sxs-lookup"><span data-stu-id="c817d-108">For a richer collaborative experience, you can integrate the QR or barcode scanner capability provided in the Teams platform with your Teams app.</span></span>   

<span data-ttu-id="c817d-109">可以使用[JavaScript Microsoft Teams SDK，](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)它提供应用访问用户的本机设备功能[所需的工具](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="c817d-109">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides the tools necessary for your app to access the user’s [native device capabilities](native-device-permissions.md).</span></span> <span data-ttu-id="c817d-110">使用 [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API 将扫描程序功能集成到你的应用中。</span><span class="sxs-lookup"><span data-stu-id="c817d-110">Use the [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API to integrate the scanner capability within your app.</span></span> 

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a><span data-ttu-id="c817d-111">集成 QR 或条形码扫描仪功能的优势</span><span class="sxs-lookup"><span data-stu-id="c817d-111">Advantage of integrating QR or barcode scanner capability</span></span>

<span data-ttu-id="c817d-112">以下是 QR 或条形码扫描仪功能集成的优势：</span><span class="sxs-lookup"><span data-stu-id="c817d-112">Following are the advantages of integration of QR or barcode scanner capabilities:</span></span> 

* <span data-ttu-id="c817d-113">集成使 Web 应用开发者Teams JavaScript 客户端 SDK 利用 QR 或条形码Teams功能。</span><span class="sxs-lookup"><span data-stu-id="c817d-113">The integration allows web app developers on Teams platform to leverage QR or barcode scanning functionality with Teams JavaScript client SDK.</span></span>
* <span data-ttu-id="c817d-114">使用此功能，用户只需在扫描仪 UI 中心的框架内对齐 QR 或条形码，代码将自动扫描。</span><span class="sxs-lookup"><span data-stu-id="c817d-114">With this feature, the user only needs to align a QR or barcode within a frame at the center of the scanner UI and the code gets scanned automatically.</span></span> <span data-ttu-id="c817d-115">存储的数据将重新与调用 Web 应用共享。</span><span class="sxs-lookup"><span data-stu-id="c817d-115">The stored data is shared back with the calling web app.</span></span> <span data-ttu-id="c817d-116">这样可以避免手动输入冗长的产品代码或其他相关信息带来的不便和人为错误。</span><span class="sxs-lookup"><span data-stu-id="c817d-116">This avoids the inconvenience and human-errors of entering lengthy product codes or other relevant information manually.</span></span>

<span data-ttu-id="c817d-117">若要集成 QR 或条形码扫描仪功能，必须更新应用清单文件并调用 [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API。</span><span class="sxs-lookup"><span data-stu-id="c817d-117">To integrate QR or barcode scanner capability, you must update the app manifest file and call the [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API.</span></span> <span data-ttu-id="c817d-118">为了进行有效的集成，你必须深入了解用于调用[scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API 的代码段，这允许你使用本机 QR 或条形码扫描仪功能。 [](#code-snippet)</span><span class="sxs-lookup"><span data-stu-id="c817d-118">For effective integration, you must have a good understanding of [code snippet](#code-snippet) for calling the [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API, which allows you to use native QR or barcode scanner capability.</span></span> <span data-ttu-id="c817d-119">API 为不支持的条形码标准提供错误。</span><span class="sxs-lookup"><span data-stu-id="c817d-119">The API gives an error for an unsupported barcode standard.</span></span>
<span data-ttu-id="c817d-120">熟悉 API 响应错误以处理应用[](#error-handling)内的错误Teams很重要。</span><span class="sxs-lookup"><span data-stu-id="c817d-120">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> <span data-ttu-id="c817d-121">目前，Microsoft Teams QR 或条形码扫描仪功能的支持仅适用于移动客户端。</span><span class="sxs-lookup"><span data-stu-id="c817d-121">Currently, Microsoft Teams support for QR or barcode scanner capability is only available for mobile clients.</span></span>

## <a name="update-manifest"></a><span data-ttu-id="c817d-122">更新清单</span><span class="sxs-lookup"><span data-stu-id="c817d-122">Update manifest</span></span>

<span data-ttu-id="c817d-123">通过添加 Teams 并[manifest.js](../../resources/schema/manifest-schema.md#devicepermissions) ，更新应用在 `devicePermissions` 文件上的应用 `media` 。</span><span class="sxs-lookup"><span data-stu-id="c817d-123">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="c817d-124">它允许你的应用在用户开始使用 QR 或条形码扫描仪功能之前向用户请求必要的权限。</span><span class="sxs-lookup"><span data-stu-id="c817d-124">It allows your app to ask for requisite permissions from users before they start using  the QR or barcode scanner capability.</span></span> <span data-ttu-id="c817d-125">应用清单的更新如下所示：</span><span class="sxs-lookup"><span data-stu-id="c817d-125">The update for app manifest is as follows:</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="c817d-126">启动 **相关应用程序** API 时，将自动显示Teams权限提示。</span><span class="sxs-lookup"><span data-stu-id="c817d-126">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="c817d-127">有关详细信息，请参阅请求 [设备权限](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="c817d-127">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="scanbarcode-api"></a><span data-ttu-id="c817d-128">ScanBarCode API</span><span class="sxs-lookup"><span data-stu-id="c817d-128">ScanBarCode API</span></span>

<span data-ttu-id="c817d-129">[scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API 调用扫描程序控件，使用户可以扫描不同类型的条形码，并返回字符串形式的结果。</span><span class="sxs-lookup"><span data-stu-id="c817d-129">The [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API invokes scanner control that enables the user to scan different types of barcode, and returns the result as a string.</span></span>

<span data-ttu-id="c817d-130">若要自定义条形码扫描体验，可选 [条形码配置](/javascript/api/@microsoft/teams-js/microsoftteams.media.barcodeconfig?view=msteams-client-js-latest&preserve-view=true) 作为输入传递到 [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API。</span><span class="sxs-lookup"><span data-stu-id="c817d-130">To customize the barcode scanning experience, optional [barcode configuration](/javascript/api/@microsoft/teams-js/microsoftteams.media.barcodeconfig?view=msteams-client-js-latest&preserve-view=true) is passed as input to [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) API.</span></span> <span data-ttu-id="c817d-131">可以使用 指定扫描的退出间隔（以秒为单位 `timeOutIntervalInSec` ）。</span><span class="sxs-lookup"><span data-stu-id="c817d-131">You can specify the scan time-out interval in seconds using `timeOutIntervalInSec`.</span></span> <span data-ttu-id="c817d-132">其默认值为 30 秒，最大值为 60 秒。</span><span class="sxs-lookup"><span data-stu-id="c817d-132">Its default value is 30 seconds and the maximum value is 60 seconds.</span></span>

<span data-ttu-id="c817d-133">**scanBarCode ()** API 支持以下条形码类型：</span><span class="sxs-lookup"><span data-stu-id="c817d-133">The **scanBarCode()** API supports the following barcode types:</span></span>

| <span data-ttu-id="c817d-134">条形码类型</span><span class="sxs-lookup"><span data-stu-id="c817d-134">Barcode Type</span></span> | <span data-ttu-id="c817d-135">在 Android 上受支持</span><span class="sxs-lookup"><span data-stu-id="c817d-135">Supported on Android</span></span> | <span data-ttu-id="c817d-136">在 iOS 上受支持</span><span class="sxs-lookup"><span data-stu-id="c817d-136">Supported on iOS</span></span> |
| ---------- | ---------- | ------------ |
| <span data-ttu-id="c817d-137">代码栏</span><span class="sxs-lookup"><span data-stu-id="c817d-137">Codebar</span></span> | <span data-ttu-id="c817d-138">是</span><span class="sxs-lookup"><span data-stu-id="c817d-138">Yes</span></span> | <span data-ttu-id="c817d-139">否</span><span class="sxs-lookup"><span data-stu-id="c817d-139">No</span></span> |
| <span data-ttu-id="c817d-140">代码 39</span><span class="sxs-lookup"><span data-stu-id="c817d-140">Code 39</span></span> | <span data-ttu-id="c817d-141">是</span><span class="sxs-lookup"><span data-stu-id="c817d-141">Yes</span></span> | <span data-ttu-id="c817d-142">是</span><span class="sxs-lookup"><span data-stu-id="c817d-142">Yes</span></span> | 
| <span data-ttu-id="c817d-143">代码 93</span><span class="sxs-lookup"><span data-stu-id="c817d-143">Code 93</span></span> | <span data-ttu-id="c817d-144">是</span><span class="sxs-lookup"><span data-stu-id="c817d-144">Yes</span></span> | <span data-ttu-id="c817d-145">是</span><span class="sxs-lookup"><span data-stu-id="c817d-145">Yes</span></span> |
| <span data-ttu-id="c817d-146">代码 128</span><span class="sxs-lookup"><span data-stu-id="c817d-146">Code 128</span></span> | <span data-ttu-id="c817d-147">是</span><span class="sxs-lookup"><span data-stu-id="c817d-147">Yes</span></span> | <span data-ttu-id="c817d-148">是</span><span class="sxs-lookup"><span data-stu-id="c817d-148">Yes</span></span> |
| <span data-ttu-id="c817d-149">EAN-13</span><span class="sxs-lookup"><span data-stu-id="c817d-149">EAN-13</span></span> | <span data-ttu-id="c817d-150">是</span><span class="sxs-lookup"><span data-stu-id="c817d-150">Yes</span></span> | <span data-ttu-id="c817d-151">是</span><span class="sxs-lookup"><span data-stu-id="c817d-151">Yes</span></span> |
| <span data-ttu-id="c817d-152">EAN-8</span><span class="sxs-lookup"><span data-stu-id="c817d-152">EAN-8</span></span> | <span data-ttu-id="c817d-153">是</span><span class="sxs-lookup"><span data-stu-id="c817d-153">Yes</span></span> | <span data-ttu-id="c817d-154">是</span><span class="sxs-lookup"><span data-stu-id="c817d-154">Yes</span></span> |
| <span data-ttu-id="c817d-155">ITF</span><span class="sxs-lookup"><span data-stu-id="c817d-155">ITF</span></span> | <span data-ttu-id="c817d-156">否</span><span class="sxs-lookup"><span data-stu-id="c817d-156">No</span></span> | <span data-ttu-id="c817d-157">是</span><span class="sxs-lookup"><span data-stu-id="c817d-157">Yes</span></span> |
| <span data-ttu-id="c817d-158">QR 码</span><span class="sxs-lookup"><span data-stu-id="c817d-158">QR Code</span></span> | <span data-ttu-id="c817d-159">是</span><span class="sxs-lookup"><span data-stu-id="c817d-159">Yes</span></span> | <span data-ttu-id="c817d-160">是</span><span class="sxs-lookup"><span data-stu-id="c817d-160">Yes</span></span> |
| <span data-ttu-id="c817d-161">RSS 展开</span><span class="sxs-lookup"><span data-stu-id="c817d-161">RSS Expanded</span></span> | <span data-ttu-id="c817d-162">是</span><span class="sxs-lookup"><span data-stu-id="c817d-162">Yes</span></span> | <span data-ttu-id="c817d-163">否</span><span class="sxs-lookup"><span data-stu-id="c817d-163">No</span></span> |
| <span data-ttu-id="c817d-164">RSS-14</span><span class="sxs-lookup"><span data-stu-id="c817d-164">RSS-14</span></span> | <span data-ttu-id="c817d-165">是</span><span class="sxs-lookup"><span data-stu-id="c817d-165">Yes</span></span> | <span data-ttu-id="c817d-166">否</span><span class="sxs-lookup"><span data-stu-id="c817d-166">No</span></span> |
| <span data-ttu-id="c817d-167">UPC-A</span><span class="sxs-lookup"><span data-stu-id="c817d-167">UPC-A</span></span> | <span data-ttu-id="c817d-168">是</span><span class="sxs-lookup"><span data-stu-id="c817d-168">Yes</span></span> | <span data-ttu-id="c817d-169">是</span><span class="sxs-lookup"><span data-stu-id="c817d-169">Yes</span></span> |
| <span data-ttu-id="c817d-170">UPC-E</span><span class="sxs-lookup"><span data-stu-id="c817d-170">UPC-E</span></span> | <span data-ttu-id="c817d-171">是</span><span class="sxs-lookup"><span data-stu-id="c817d-171">Yes</span></span> | <span data-ttu-id="c817d-172">是</span><span class="sxs-lookup"><span data-stu-id="c817d-172">Yes</span></span> |

<span data-ttu-id="c817d-173">下图描述了 QR 或条形码扫描仪功能 Web 应用体验：</span><span class="sxs-lookup"><span data-stu-id="c817d-173">The following image depicts web app experience of QR or barcode scanner capability:</span></span>

![qr 或条形码扫描仪功能 Web 应用体验](../../assets/images/tabs/qr-barcode-scanner-capability.png)

## <a name="error-handling"></a><span data-ttu-id="c817d-175">错误处理</span><span class="sxs-lookup"><span data-stu-id="c817d-175">Error handling</span></span>

<span data-ttu-id="c817d-176">必须确保在你的应用内正确处理这些Teams错误。</span><span class="sxs-lookup"><span data-stu-id="c817d-176">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="c817d-177">下表列出了错误代码以及生成错误的条件：</span><span class="sxs-lookup"><span data-stu-id="c817d-177">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="c817d-178">错误代码</span><span class="sxs-lookup"><span data-stu-id="c817d-178">Error code</span></span> |  <span data-ttu-id="c817d-179">错误名称</span><span class="sxs-lookup"><span data-stu-id="c817d-179">Error name</span></span>     | <span data-ttu-id="c817d-180">Condition</span><span class="sxs-lookup"><span data-stu-id="c817d-180">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="c817d-181">**100**</span><span class="sxs-lookup"><span data-stu-id="c817d-181">**100**</span></span> | <span data-ttu-id="c817d-182">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="c817d-182">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="c817d-183">API 在当前平台上不受支持。</span><span class="sxs-lookup"><span data-stu-id="c817d-183">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="c817d-184">**500**</span><span class="sxs-lookup"><span data-stu-id="c817d-184">**500**</span></span> | <span data-ttu-id="c817d-185">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="c817d-185">INTERNAL_ERROR</span></span> | <span data-ttu-id="c817d-186">执行所需操作时遇到内部错误。</span><span class="sxs-lookup"><span data-stu-id="c817d-186">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="c817d-187">**1000**</span><span class="sxs-lookup"><span data-stu-id="c817d-187">**1000**</span></span> | <span data-ttu-id="c817d-188">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="c817d-188">PERMISSION_DENIED</span></span> |<span data-ttu-id="c817d-189">用户拒绝权限。</span><span class="sxs-lookup"><span data-stu-id="c817d-189">Permission is denied by the user.</span></span>|
| <span data-ttu-id="c817d-190">**3000**</span><span class="sxs-lookup"><span data-stu-id="c817d-190">**3000**</span></span> | <span data-ttu-id="c817d-191">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="c817d-191">NO_HW_SUPPORT</span></span> | <span data-ttu-id="c817d-192">基础硬件不支持该功能。</span><span class="sxs-lookup"><span data-stu-id="c817d-192">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="c817d-193">**4000**</span><span class="sxs-lookup"><span data-stu-id="c817d-193">**4000**</span></span> | <span data-ttu-id="c817d-194">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="c817d-194">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="c817d-195">一个或多个参数无效。</span><span class="sxs-lookup"><span data-stu-id="c817d-195">One or more arguments are invalid.</span></span>|
| <span data-ttu-id="c817d-196">**8000**</span><span class="sxs-lookup"><span data-stu-id="c817d-196">**8000**</span></span> | <span data-ttu-id="c817d-197">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="c817d-197">USER_ABORT</span></span> |<span data-ttu-id="c817d-198">用户中止操作。</span><span class="sxs-lookup"><span data-stu-id="c817d-198">User aborts the operation.</span></span>|
| <span data-ttu-id="c817d-199">**8001**</span><span class="sxs-lookup"><span data-stu-id="c817d-199">**8001**</span></span> | <span data-ttu-id="c817d-200">OPERATION_TIMED_OUT</span><span class="sxs-lookup"><span data-stu-id="c817d-200">OPERATION_TIMED_OUT</span></span> | <span data-ttu-id="c817d-201">无法检测给定时间间隔的条形码。</span><span class="sxs-lookup"><span data-stu-id="c817d-201">Could not detect the barcode in the given time interval.</span></span>|
| <span data-ttu-id="c817d-202">**9000**</span><span class="sxs-lookup"><span data-stu-id="c817d-202">**9000**</span></span> | <span data-ttu-id="c817d-203">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="c817d-203">OLD_PLATFORM</span></span> | <span data-ttu-id="c817d-204">平台代码已过时，不实现此 API。</span><span class="sxs-lookup"><span data-stu-id="c817d-204">Platform code is outdated and does not implement this API.</span></span>|

## <a name="code-snippet"></a><span data-ttu-id="c817d-205">代码段</span><span class="sxs-lookup"><span data-stu-id="c817d-205">Code snippet</span></span>

<span data-ttu-id="c817d-206">**呼叫 `ScanBarCode()` 用于** 使用相机扫描 QR 或条形码的 API：</span><span class="sxs-lookup"><span data-stu-id="c817d-206">**Calling `ScanBarCode()` API** for scanning QR or barcode using camera:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="c817d-207">另请参阅</span><span class="sxs-lookup"><span data-stu-id="c817d-207">See also</span></span>

* [<span data-ttu-id="c817d-208">将媒体功能集成到Teams</span><span class="sxs-lookup"><span data-stu-id="c817d-208">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="c817d-209">在 Teams 中集成位置Teams</span><span class="sxs-lookup"><span data-stu-id="c817d-209">Integrate location capabilities in Teams</span></span>](location-capability.md)
* [<span data-ttu-id="c817d-210">将人员选取器功能集成到Teams</span><span class="sxs-lookup"><span data-stu-id="c817d-210">Integrate People Picker capability in Teams</span></span>](people-picker-capability.md)

