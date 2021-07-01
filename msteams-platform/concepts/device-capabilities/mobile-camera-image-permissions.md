---
title: 集成媒体功能
author: Rajeshwari-v
description: 如何使用 JavaScript Teams SDK 启用媒体功能
keywords: 相机图像麦克风功能本机设备权限媒体
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 22d4a791e83cf36f18b75a3846865835b0ee024f
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211623"
---
# <a name="integrate-media-capabilities"></a><span data-ttu-id="43706-104">集成媒体功能</span><span class="sxs-lookup"><span data-stu-id="43706-104">Integrate media capabilities</span></span> 

<span data-ttu-id="43706-105">你可以将本机设备功能（如相机和 **麦克风**）与你的应用Teams集成。</span><span class="sxs-lookup"><span data-stu-id="43706-105">You can integrate native device capabilities, such as the **camera** and **microphone** with your Teams app.</span></span> <span data-ttu-id="43706-106">对于集成，可以使用[javaScript Microsoft Teams SDK，](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)它提供应用访问用户设备权限[所需的工具](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="43706-106">For integration, you can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), that provides the tools necessary for your app to access a user’s [device permissions](native-device-permissions.md).</span></span> <span data-ttu-id="43706-107">使用合适的媒体功能 API 将设备功能（如相机和麦克风）与Microsoft Teams 移动应用中的 Teams 平台集成，并构建更丰富的体验。</span><span class="sxs-lookup"><span data-stu-id="43706-107">Use suitable media capability APIs to integrate the device capabilities, such as **camera** and **microphone** with the Teams platform within your Microsoft Teams mobile app, and build a richer experience.</span></span> 

## <a name="advantage-of-integrating-media-capabilities"></a><span data-ttu-id="43706-108">集成媒体功能的优势</span><span class="sxs-lookup"><span data-stu-id="43706-108">Advantage of integrating media capabilities</span></span>

<span data-ttu-id="43706-109">将设备功能集成到 Teams 应用中的主要优点是它利用本机 Teams 控件为用户提供丰富且沉浸式的体验。</span><span class="sxs-lookup"><span data-stu-id="43706-109">The main advantage of integrating device capabilities in your Teams apps is it leverages native Teams controls to provide a rich and immersive experience to your users.</span></span>
<span data-ttu-id="43706-110">若要集成媒体功能，必须更新应用清单文件并调用媒体功能 API。</span><span class="sxs-lookup"><span data-stu-id="43706-110">To integrate media capabilities you must update the app manifest file and call the media capability APIs.</span></span> 

<span data-ttu-id="43706-111">为了进行有效的集成，你必须深入了解用于调用相应[](#code-snippets)API 的代码段，这允许你使用本机媒体功能。</span><span class="sxs-lookup"><span data-stu-id="43706-111">For effective integration, you must have a good understanding of [code snippets](#code-snippets) for calling the respective APIs, which allow you to use native media capabilities.</span></span>

<span data-ttu-id="43706-112">熟悉 API 响应错误以处理应用[](#error-handling)内的错误Teams很重要。</span><span class="sxs-lookup"><span data-stu-id="43706-112">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your Teams app.</span></span>

> [!NOTE] 
> * <span data-ttu-id="43706-113">目前Microsoft Teams媒体功能的支持仅适用于移动客户端。</span><span class="sxs-lookup"><span data-stu-id="43706-113">Currently, Microsoft Teams support for media capabilities is available for mobile clients only.</span></span>   
> * <span data-ttu-id="43706-114">目前，Teams不支持多窗口应用、选项卡和会议侧窗格的设备权限。</span><span class="sxs-lookup"><span data-stu-id="43706-114">Currently, Teams does not support device permissions for multi window apps, tabs, and the meeting sidepanel.</span></span>    

## <a name="update-manifest"></a><span data-ttu-id="43706-115">更新清单</span><span class="sxs-lookup"><span data-stu-id="43706-115">Update manifest</span></span>

<span data-ttu-id="43706-116">通过添加 Teams 并[manifest.js](../../resources/schema/manifest-schema.md#devicepermissions) ，更新应用在 `devicePermissions` 文件上的应用 `media` 。</span><span class="sxs-lookup"><span data-stu-id="43706-116">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions` property and specifying `media`.</span></span> <span data-ttu-id="43706-117">它允许你的应用在用户开始使用相机捕获图像之前，向用户请求必要的权限，打开库以选择要作为附件提交的图像，或使用麦克风录制对话。 </span><span class="sxs-lookup"><span data-stu-id="43706-117">It allows your app to ask for requisite permissions from users before they start using  the **camera** to capture the image, open the gallery to select an image to submit as an attachment, or use the **microphone** to record the conversation.</span></span> <span data-ttu-id="43706-118">应用清单的更新如下所示：</span><span class="sxs-lookup"><span data-stu-id="43706-118">The update for app manifest is as follows:</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="43706-119">启动 **相关应用程序** API 时，将自动显示Teams权限提示。</span><span class="sxs-lookup"><span data-stu-id="43706-119">The **Request Permissions** prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="43706-120">有关详细信息，请参阅请求 [设备权限](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="43706-120">For more information, see [Request device permissions](native-device-permissions.md).</span></span>

## <a name="media-capability-apis"></a><span data-ttu-id="43706-121">媒体功能 API</span><span class="sxs-lookup"><span data-stu-id="43706-121">Media capability APIs</span></span>

<span data-ttu-id="43706-122">[selectMedia、getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true)和[viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) API 使您可以使用本机媒体功能，如下所示： [](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="43706-122">The [selectMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true), and [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) APIs enable you to use native media capabilities as follows:</span></span>

* <span data-ttu-id="43706-123">使用本机 **麦克风** 允许用户从设备 **录制 (录制** 10 分钟) 对话。</span><span class="sxs-lookup"><span data-stu-id="43706-123">Use the native **microphone** to allow users to **record audio** (record 10 minutes of conversation) from the device.</span></span>
* <span data-ttu-id="43706-124">使用 **本机相机控件** 允许用户 **在移动时捕获和** 附加图像。</span><span class="sxs-lookup"><span data-stu-id="43706-124">Use native **camera control** to allow users to **capture and attach images** on the go.</span></span>
* <span data-ttu-id="43706-125">使用 **本机库支持** 以允许用户 **选择设备图像作为** 附件。</span><span class="sxs-lookup"><span data-stu-id="43706-125">Use native **gallery support** to allow users to **select device images** as attachments.</span></span>
* <span data-ttu-id="43706-126">使用本机 **图像查看器控件一\*\*\*\*次预览** 多个图像。</span><span class="sxs-lookup"><span data-stu-id="43706-126">Use native **image viewer control** to **preview multiple images** at one time.</span></span>
* <span data-ttu-id="43706-127">通过 SDK **桥** (从 1 MB 到 50 MB) 大图像传输。</span><span class="sxs-lookup"><span data-stu-id="43706-127">Support **large image transfer** (from 1 MB to 50 MB) through the SDK bridge.</span></span>
* <span data-ttu-id="43706-128">支持 **允许用户预览** 和编辑图像的高级图像功能：</span><span class="sxs-lookup"><span data-stu-id="43706-128">Support **advanced image capabilities** allowing users to preview and edit images:</span></span>
  * <span data-ttu-id="43706-129">通过相机扫描文档、白板和名片。</span><span class="sxs-lookup"><span data-stu-id="43706-129">Scan document, whiteboard, and business cards  through the camera.</span></span>
  
> [!IMPORTANT]
> * <span data-ttu-id="43706-130">可以从 `selectMedia` 多个任务Teams，如任务模块、选项卡和个人应用调用 、 和 `getMedia` `viewImages` API。</span><span class="sxs-lookup"><span data-stu-id="43706-130">The `selectMedia`, `getMedia`, and `viewImages` APIs can be invoked from multiple Teams surfaces, such as task modules, tabs, and personal apps.</span></span> <span data-ttu-id="43706-131">有关详细信息，请参阅应用[Teams点](../extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="43706-131">For more details, see [Entry points for Teams apps](../extensibility-points.md).</span></span>
> * <span data-ttu-id="43706-132">`selectMedia` API 已扩展以支持麦克风和音频属性。</span><span class="sxs-lookup"><span data-stu-id="43706-132">`selectMedia` API has been extended to support microphone and audio properties.</span></span>

<span data-ttu-id="43706-133">你必须使用以下一组 API 来启用设备的媒体功能：</span><span class="sxs-lookup"><span data-stu-id="43706-133">You must use the following set of APIs to enable your device's media capabilities:</span></span>

| <span data-ttu-id="43706-134">API</span><span class="sxs-lookup"><span data-stu-id="43706-134">API</span></span>      | <span data-ttu-id="43706-135">说明</span><span class="sxs-lookup"><span data-stu-id="43706-135">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="43706-136">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Camera)**</span><span class="sxs-lookup"><span data-stu-id="43706-136">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Camera)**</span></span>| <span data-ttu-id="43706-137">此 API 允许用户从 **设备相机捕获或** 选择媒体，并返回到 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="43706-137">This API allows users to **capture or select media from the device camera** and return it to the web-app.</span></span> <span data-ttu-id="43706-138">用户可以在提交之前编辑、裁剪、旋转、批注或绘制图像。</span><span class="sxs-lookup"><span data-stu-id="43706-138">The users can edit, crop, rotate, annotate, or draw over images before submission.</span></span> <span data-ttu-id="43706-139">作为响应，Web 应用接收所选图像的媒体 `selectMedia` ID 和所选媒体的缩略图。</span><span class="sxs-lookup"><span data-stu-id="43706-139">In response to `selectMedia`, the web-app receives the media IDs of selected images and a thumbnail of the selected media.</span></span> <span data-ttu-id="43706-140">可以通过 [ImageProps](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true) 配置进一步配置此 API。</span><span class="sxs-lookup"><span data-stu-id="43706-140">This API can be further configured through the [ImageProps](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true) configuration.</span></span> |
| <span data-ttu-id="43706-141">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**麦克风**) </span><span class="sxs-lookup"><span data-stu-id="43706-141">[**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Microphone**)</span></span>| <span data-ttu-id="43706-142">在 [API 中将 mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) `4` 设置为 `selectMedia` ，以访问麦克风功能。</span><span class="sxs-lookup"><span data-stu-id="43706-142">Set the [mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) to `4` in `selectMedia` API for accessing microphone  capability.</span></span> <span data-ttu-id="43706-143">此 API 还允许用户从设备麦克风录制音频，将录制的剪辑返回到 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="43706-143">This API also allows users to record audio from the device microphone and return recorded clips to the web-app.</span></span> <span data-ttu-id="43706-144">用户可以在提交之前暂停、重新录制和播放录制预览。</span><span class="sxs-lookup"><span data-stu-id="43706-144">The users can pause, re-record, and play recording preview before submission.</span></span> <span data-ttu-id="43706-145">作为对 **selectMedia 的响应**，Web 应用接收所选音频录制的媒体 ID。</span><span class="sxs-lookup"><span data-stu-id="43706-145">In response to **selectMedia**, the web-app receives media IDs of the selected audio recording.</span></span> <br/> <span data-ttu-id="43706-146">如果需要 `maxDuration` 为录制对话配置持续时间（以分钟表示）。请使用 。</span><span class="sxs-lookup"><span data-stu-id="43706-146">Use `maxDuration`, if you require to configure a duration in minutes for recording the conversation.</span></span> <span data-ttu-id="43706-147">录制的当前持续时间为 10 分钟，之后将终止录制。</span><span class="sxs-lookup"><span data-stu-id="43706-147">The current duration for recording is 10 minutes, after which the recording terminates.</span></span>  |
| [<span data-ttu-id="43706-148">**getMedia**</span><span class="sxs-lookup"><span data-stu-id="43706-148">**getMedia**</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)| <span data-ttu-id="43706-149">此 API 检索 API 以区块捕获的媒体， `selectMedia` 而不考虑媒体大小。</span><span class="sxs-lookup"><span data-stu-id="43706-149">This API retrieves the media captured by `selectMedia` API in chunks, irrespective of the media size.</span></span> <span data-ttu-id="43706-150">这些区块将组合在一起，作为文件或 blob 发送回 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="43706-150">These chunks are assembled and sent back to the web app as a file or blob.</span></span> <span data-ttu-id="43706-151">将媒体分成较小的区块便于大型文件传输。</span><span class="sxs-lookup"><span data-stu-id="43706-151">Breaking of media into smaller chunks facilitates large file transfer.</span></span> |
| [<span data-ttu-id="43706-152">**viewImages**</span><span class="sxs-lookup"><span data-stu-id="43706-152">**viewImages**</span></span>](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true)| <span data-ttu-id="43706-153">此 API 使用户能够在全屏模式下以可滚动列表的方式查看图像。</span><span class="sxs-lookup"><span data-stu-id="43706-153">This API enables the user to view images in  full-screen mode as a scrollable list.</span></span>|

<span data-ttu-id="43706-154">下图描述了 API 的 Web 应用体验 `selectMedia` ，用于图像功能：</span><span class="sxs-lookup"><span data-stu-id="43706-154">The following image depicts web app experience of `selectMedia` API for image capability:</span></span>

![设备相机和图像体验Teams](../../assets/images/tabs/image-capability.png)

<span data-ttu-id="43706-156">下图描述了 API 的麦克风功能 `selectMedia` Web 应用体验：</span><span class="sxs-lookup"><span data-stu-id="43706-156">The following image depicts web app experience of `selectMedia` API for microphone capability:</span></span>

![麦克风功能 Web 应用体验](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a><span data-ttu-id="43706-158">错误处理</span><span class="sxs-lookup"><span data-stu-id="43706-158">Error handling</span></span>

<span data-ttu-id="43706-159">必须确保在你的应用内正确处理这些Teams错误。</span><span class="sxs-lookup"><span data-stu-id="43706-159">You must ensure to handle these errors appropriately in your Teams app.</span></span> <span data-ttu-id="43706-160">下表列出了错误代码以及生成错误的条件：</span><span class="sxs-lookup"><span data-stu-id="43706-160">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="43706-161">错误代码</span><span class="sxs-lookup"><span data-stu-id="43706-161">Error code</span></span> |  <span data-ttu-id="43706-162">错误名称</span><span class="sxs-lookup"><span data-stu-id="43706-162">Error name</span></span>     | <span data-ttu-id="43706-163">Condition</span><span class="sxs-lookup"><span data-stu-id="43706-163">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="43706-164">**100**</span><span class="sxs-lookup"><span data-stu-id="43706-164">**100**</span></span> | <span data-ttu-id="43706-165">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="43706-165">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="43706-166">API 在当前平台上不受支持。</span><span class="sxs-lookup"><span data-stu-id="43706-166">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="43706-167">**404**</span><span class="sxs-lookup"><span data-stu-id="43706-167">**404**</span></span> | <span data-ttu-id="43706-168">FILE_NOT_FOUND</span><span class="sxs-lookup"><span data-stu-id="43706-168">FILE_NOT_FOUND</span></span> | <span data-ttu-id="43706-169">在给定位置找不到指定的文件。</span><span class="sxs-lookup"><span data-stu-id="43706-169">File specified is not found in the given location.</span></span>|
| <span data-ttu-id="43706-170">**500**</span><span class="sxs-lookup"><span data-stu-id="43706-170">**500**</span></span> | <span data-ttu-id="43706-171">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="43706-171">INTERNAL_ERROR</span></span> | <span data-ttu-id="43706-172">执行所需操作时遇到内部错误。</span><span class="sxs-lookup"><span data-stu-id="43706-172">Internal error is encountered while performing the required operation.</span></span>|
| <span data-ttu-id="43706-173">**1000**</span><span class="sxs-lookup"><span data-stu-id="43706-173">**1000**</span></span> | <span data-ttu-id="43706-174">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="43706-174">PERMISSION_DENIED</span></span> |<span data-ttu-id="43706-175">用户拒绝权限。</span><span class="sxs-lookup"><span data-stu-id="43706-175">Permission is denied by the user.</span></span>|
| <span data-ttu-id="43706-176">**3000**</span><span class="sxs-lookup"><span data-stu-id="43706-176">**3000**</span></span> | <span data-ttu-id="43706-177">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="43706-177">NO_HW_SUPPORT</span></span> | <span data-ttu-id="43706-178">基础硬件不支持该功能。</span><span class="sxs-lookup"><span data-stu-id="43706-178">Underlying hardware does not support the capability.</span></span>|
| <span data-ttu-id="43706-179">**4000**</span><span class="sxs-lookup"><span data-stu-id="43706-179">**4000**</span></span>| <span data-ttu-id="43706-180">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="43706-180">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="43706-181">一个或多个参数无效。</span><span class="sxs-lookup"><span data-stu-id="43706-181">One or more arguments are invalid.</span></span>|
|  <span data-ttu-id="43706-182">**8000**</span><span class="sxs-lookup"><span data-stu-id="43706-182">**8000**</span></span> | <span data-ttu-id="43706-183">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="43706-183">USER_ABORT</span></span> |<span data-ttu-id="43706-184">用户中止操作。</span><span class="sxs-lookup"><span data-stu-id="43706-184">User aborts the operation.</span></span>|
| <span data-ttu-id="43706-185">**9000**</span><span class="sxs-lookup"><span data-stu-id="43706-185">**9000**</span></span>| <span data-ttu-id="43706-186">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="43706-186">OLD_PLATFORM</span></span> | <span data-ttu-id="43706-187">平台代码已过时，不实现此 API。</span><span class="sxs-lookup"><span data-stu-id="43706-187">Platform code is outdated and does not implement this API.</span></span>|
| <span data-ttu-id="43706-188">**10000**</span><span class="sxs-lookup"><span data-stu-id="43706-188">**10000**</span></span>| <span data-ttu-id="43706-189">SIZE_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="43706-189">SIZE_EXCEEDED</span></span> |  <span data-ttu-id="43706-190">返回值太大，已超出平台大小边界。</span><span class="sxs-lookup"><span data-stu-id="43706-190">Return value is too big and has exceeded the platform size boundaries.</span></span>|

## <a name="code-snippets"></a><span data-ttu-id="43706-191">代码段</span><span class="sxs-lookup"><span data-stu-id="43706-191">Code snippets</span></span>

<span data-ttu-id="43706-192">**呼叫 `selectMedia` 用于** 使用相机捕获图像的 API：</span><span class="sxs-lookup"><span data-stu-id="43706-192">**Calling `selectMedia` API** for capturing images using camera:</span></span>

```javascript
let imageProp: microsoftTeams.media.ImageProps = {
    sources: [microsoftTeams.media.Source.Camera, microsoftTeams.media.Source.Gallery],
    startMode: microsoftTeams.media.CameraStartMode.Photo,
    ink: false,
    cameraSwitcher: false,
    textSticker: false,
    enableFilter: true,
};
let mediaInput: microsoftTeams.media.MediaInputs = {
    mediaType: microsoftTeams.media.MediaType.Image,
    maxMediaCount: 10,
    imageProps: imageProp
};
microsoftTeams.media.selectMedia(mediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
    if (attachments) {
        let y = attachments[0];
        img.src = ("data:" + y.mimeType + ";base64," + y.preview);
    }
});
```

<span data-ttu-id="43706-193">**呼叫 `getMedia` 用于** 检索区块中的大型媒体的 API：</span><span class="sxs-lookup"><span data-stu-id="43706-193">**Calling `getMedia` API** to retrieve large media in chunks:</span></span>

```javascript
let media: microsoftTeams.media.Media = attachments[0]
media.getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
    if (blob) {
        if (blob.type.includes("image")) {
            img.src = (URL.createObjectURL(blob));
        }
    }
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
});
```

<span data-ttu-id="43706-194">**呼叫 `viewImages`API 返回的按 ID `selectMedia` 表示的 API：**</span><span class="sxs-lookup"><span data-stu-id="43706-194">**Calling `viewImages` API by ID returned by `selectMedia` API**:</span></span>

```javascript
// View images by id:
// Assumption: attachmentArray = select Media API Output
let uriList = [];
if (attachmentArray && attachmentArray.length > 0) {
    for (let i = 0; i < attachmentArray.length; i++) {
        let file = attachmentArray[i];
        if (file.mimeType.includes("image")) {
            let imageUri = {
                value: file.content,
                type: 1,
            }
            uriList.push(imageUri);
        } else {
            alert("File type is not image");
        }
    }
}
if (uriList.length > 0) {
    microsoftTeams.media.viewImages(uriList, (error: microsoftTeams.SdkError) => {
        if (error) {
            if (error.message) {
                output(" ErrorCode: " + error.errorCode + error.message);
            } else {
                output(" ErrorCode: " + error.errorCode);
            }
        }
    });
} else {
    output("Url list is empty");
}
```

<span data-ttu-id="43706-195">**呼叫 `viewImages`按 URL 的 API：**</span><span class="sxs-lookup"><span data-stu-id="43706-195">**Calling `viewImages` API by URL**:</span></span>

```javascript
// View Images by URL:
// Assumption 2 urls, url1 and url2
let uriList = [];
if (URL1 != null && URL1.length > 0) {
    let imageUri = {
        value: URL1,
        type: 2,
    }
    uriList.push(imageUri);
}
if (URL2 != null && URL2.length > 0) {
    let imageUri = {
        value: URL2,
        type: 2,
    }
    uriList.push(imageUri);
}
if (uriList.length > 0) {
    microsoftTeams.media.viewImages(uriList, (error: microsoftTeams.SdkError) => {
        if (error) {
            if (error.message) {
                output(" ErrorCode: " + error.errorCode + error.message);
            } else {
                output(" ErrorCode: " + error.errorCode);
            }
        }
    });
} else {
    output("Url list is empty");
}
```

<span data-ttu-id="43706-196">**用于 `selectMedia` 通过 `getMedia` 麦克风录制音频的呼叫和 API：**</span><span class="sxs-lookup"><span data-stu-id="43706-196">**Calling `selectMedia` and `getMedia` APIs for recording audio through microphone**:</span></span>

```javascript
let mediaInput: microsoftTeams.media.MediaInputs = {
    mediaType: microsoftTeams.media.MediaType.Audio,
    maxMediaCount: 1,
};
microsoftTeams.media.selectMedia(mediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
    // If you want to directly use the audio file (for smaller file sizes (~4MB))    if (attachments) {
    let audioResult = attachments[0];
    var videoElement = document.createElement("video");
    videoElement.setAttribute("src", ("data:" + y.mimeType + ";base64," + y.preview));
    //To use the audio file via get Media API for bigger audio file sizes greater than 4MB        audioResult.getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
    if (blob) {
        if (blob.type.includes("video")) {
            videoElement.setAttribute("src", URL.createObjectURL(blob));
        }
    }
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
});
```

## <a name="see-also"></a><span data-ttu-id="43706-197">另请参阅</span><span class="sxs-lookup"><span data-stu-id="43706-197">See also</span></span>

* [<span data-ttu-id="43706-198">将 QR 或条形码扫描仪功能集成到 Teams</span><span class="sxs-lookup"><span data-stu-id="43706-198">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
* [<span data-ttu-id="43706-199">在 Teams 中集成位置Teams</span><span class="sxs-lookup"><span data-stu-id="43706-199">Integrate location capabilities in Teams</span></span>](location-capability.md)
* [<span data-ttu-id="43706-200">将人员选取器功能集成到Teams</span><span class="sxs-lookup"><span data-stu-id="43706-200">Integrate People Picker capability in Teams</span></span>](people-picker-capability.md)

