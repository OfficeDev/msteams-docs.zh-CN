---
title: 团队中的照相机和图像功能
description: 如何使用团队 Javascript 客户端 SDK 启用本机相机和图像功能
keywords: 相机图像功能本机设备权限
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d0ca4dc9c289ec525aa99ea0e156a9f91f5b5d4a
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576874"
---
# <a name="camera-and-image-capabilities-in-teams"></a><span data-ttu-id="be729-104">团队中的照相机和图像功能</span><span class="sxs-lookup"><span data-stu-id="be729-104">Camera and image capabilities in Teams</span></span>

>[!IMPORTANT]
>
> * <span data-ttu-id="be729-105">目前，仅对移动客户端提供摄像头和图像功能的团队支持。</span><span class="sxs-lookup"><span data-stu-id="be729-105">At present, Teams support for camera and image capabilities is only available for mobile clients.</span></span>
>* <span data-ttu-id="be729-106">`selectMedia`、 `getMedia` 和 `viewImages` api 可从多个团队图面（例如任务模块、选项卡和个人应用程序）中进行调用。</span><span class="sxs-lookup"><span data-stu-id="be729-106">The `selectMedia`, `getMedia`, and `viewImages` APIs can be invoked from multiple Teams surfaces such as task modules, tabs, and personal apps.</span></span> <span data-ttu-id="be729-107">有关更多详细信息，_请参阅_[团队应用程序的入口点](../extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="be729-107">For more details, _see_ [Entry points for Teams apps](../extensibility-points.md)</span></span>

<span data-ttu-id="be729-108">您可以使用  [Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)轻松地将相机和图像功能集成到 microsoft team mobile 应用程序中。</span><span class="sxs-lookup"><span data-stu-id="be729-108">You can use the  [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), to easily integrate camera and image capabilities within your Microsoft Teams mobile app.</span></span> <span data-ttu-id="be729-109">SDK 为您的应用程序提供了访问用户的 [设备权限](native-device-permissions.md?tabs=desktop#device-permissions) 并生成更丰富的体验所需的工具。</span><span class="sxs-lookup"><span data-stu-id="be729-109">The SDK provides the tools necessary for your app to access a user’s [device permissions](native-device-permissions.md?tabs=desktop#device-permissions) and build a richer experience.</span></span>

<span data-ttu-id="be729-110">[SelectMedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)、 [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)和[viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) api 使您能够使用本机相机/图像功能，如下所示：</span><span class="sxs-lookup"><span data-stu-id="be729-110">The [selectMedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true), and [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) APIs enable you to use native camera/image capabilities as follows:</span></span>

* <span data-ttu-id="be729-111">使用本机 **相机控制** 允许用户在旅途中 **捕获和附加图像** 。</span><span class="sxs-lookup"><span data-stu-id="be729-111">Use native **camera control** to allow users to **capture and attach images** on the go.</span></span>
* <span data-ttu-id="be729-112">使用本机 **库支持** ，以允许用户 **选择设备图像** 作为附件。</span><span class="sxs-lookup"><span data-stu-id="be729-112">Use native **gallery support** to allow users to **select device images** as attachments.</span></span>
* <span data-ttu-id="be729-113">使用本机 **图像查看器控件** 一次 **预览多个图像** 。</span><span class="sxs-lookup"><span data-stu-id="be729-113">Use native **image viewer control** to **preview multiple images** at one time.</span></span>
* <span data-ttu-id="be729-114">支持通过 SDK 桥) 的 **大图像传输** (最多为 50 MB</span><span class="sxs-lookup"><span data-stu-id="be729-114">Support **large image transfer** (up to 50 MB) via the SDK bridge</span></span>
* <span data-ttu-id="be729-115">支持 **高级图像功能** ，允许用户预览和编辑图像：</span><span class="sxs-lookup"><span data-stu-id="be729-115">Support **advanced image capabilities** allowing users to preview and edit images:</span></span>
  * <span data-ttu-id="be729-116">通过相机扫描文档、白板、名片等。</span><span class="sxs-lookup"><span data-stu-id="be729-116">Scan document, whiteboard, business cards, etc., through the camera.</span></span>
  * <span data-ttu-id="be729-117">裁剪并旋转图像。</span><span class="sxs-lookup"><span data-stu-id="be729-117">Crop and rotate the images.</span></span>
  * <span data-ttu-id="be729-118">将文本、墨迹或手绘批注添加到图像中。</span><span class="sxs-lookup"><span data-stu-id="be729-118">Add text, ink, or freehand annotation to the image.</span></span>

## <a name="get-started"></a><span data-ttu-id="be729-119">入门</span><span class="sxs-lookup"><span data-stu-id="be729-119">Get started</span></span>

<span data-ttu-id="be729-120">通过添加属性和指定来更新文件的团队应用 [manifest.js](../../resources/schema/manifest-schema.md#devicepermissions) `devicePermissions` `media` 。</span><span class="sxs-lookup"><span data-stu-id="be729-120">Update your Teams app [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) file by adding the `devicePermissions`  property and specifying `media`.</span></span> <span data-ttu-id="be729-121">这样，您的应用程序就可以在最终用户使用相机捕获图像或打开库以选择要作为附件提交的图像之前，要求提供来自最终用户的必要权限。</span><span class="sxs-lookup"><span data-stu-id="be729-121">This allows your app to ask for requisite permissions from end-users before they use the camera to capture the image or open the gallery to select an image to submit as an attachment.</span></span>

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> <span data-ttu-id="be729-122">当相关的团队 API 启动时，将自动显示 " _请求权限_ " 提示。</span><span class="sxs-lookup"><span data-stu-id="be729-122">The _Request Permissions_ prompt is automatically displayed when a relevant Teams API is initiated.</span></span> <span data-ttu-id="be729-123">有关更多详细信息，*请参阅*[请求设备权限](native-device-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="be729-123">For more details, *see* [Request device permissions](native-device-permissions.md).</span></span>

## <a name="using-camera-and-image-capability-apis"></a><span data-ttu-id="be729-124">使用相机和图像功能 Api</span><span class="sxs-lookup"><span data-stu-id="be729-124">Using camera and image capability APIs</span></span>

<span data-ttu-id="be729-125">您可以使用以下 Api 集来启用相机和图像设备功能：</span><span class="sxs-lookup"><span data-stu-id="be729-125">You can use the following set of APIs to enable camera and image device capabilities:</span></span>

| <span data-ttu-id="be729-126">API</span><span class="sxs-lookup"><span data-stu-id="be729-126">API</span></span>      | <span data-ttu-id="be729-127">说明</span><span class="sxs-lookup"><span data-stu-id="be729-127">Description</span></span>   |
| --- | --- |
| [<span data-ttu-id="be729-128">**selectMedia**</span><span class="sxs-lookup"><span data-stu-id="be729-128">**selectMedia**</span></span>](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest&branch=master#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)| <span data-ttu-id="be729-129">此 API 允许用户 **捕获或选择来自本机设备的媒体** 并返回到 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="be729-129">This API allows users to **capture or select media from a native device** and return to the web-app.</span></span> <span data-ttu-id="be729-130">用户可以选择在提交前编辑、裁剪、旋转、批注或绘制图像。</span><span class="sxs-lookup"><span data-stu-id="be729-130">Users may choose to edit, crop, rotate, annotate, or draw over images before submission.</span></span> <span data-ttu-id="be729-131">为响应 **selectMedia**，web 应用将接收所选图像的媒体 id，并且可能会收到选定媒体的缩略图。</span><span class="sxs-lookup"><span data-stu-id="be729-131">In response to **selectMedia**, the web-app will receive media ids of selected images and may receive a thumbnail of the selected media.</span></span> |
| [<span data-ttu-id="be729-132">**getMedia**</span><span class="sxs-lookup"><span data-stu-id="be729-132">**getMedia**</span></span>](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest&branch=master#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| <span data-ttu-id="be729-133">此 API 以不考虑大小的块形式检索媒体。</span><span class="sxs-lookup"><span data-stu-id="be729-133">This API retrieves the media in chunks irrespective of size.</span></span> <span data-ttu-id="be729-134">组合这些区块并以文件/blob 的形式将其发送回 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="be729-134">These chunks are assembled and sent back to the web app as a file/blob.</span></span> <span data-ttu-id="be729-135">使用此 API，可以将图像分成多个较小的块，以方便进行大型图像传输。</span><span class="sxs-lookup"><span data-stu-id="be729-135">With this API an image is broken into smaller chunks to facilitate large image transfer.</span></span> |
| [<span data-ttu-id="be729-136">**viewImages**</span><span class="sxs-lookup"><span data-stu-id="be729-136">**viewImages**</span></span>](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| <span data-ttu-id="be729-137">此 API 使用户能够以可滚动列表的形式查看全屏模式图像。</span><span class="sxs-lookup"><span data-stu-id="be729-137">This API enables the user to view images full-screen mode as a scrollable list.</span></span>|

<span data-ttu-id="be729-138">**SELECTMEDIA API** 
 ![ 的 Web 应用程序体验团队中的设备照相机和图像体验](../../assets/images/tabs/image-capability-screenshot.jpg)</span><span class="sxs-lookup"><span data-stu-id="be729-138">**Web app experience for selectMedia API**
![device camera and image experience in Teams](../../assets/images/tabs/image-capability-screenshot.jpg)</span></span>

## <a name="error-handling"></a><span data-ttu-id="be729-139">错误处理</span><span class="sxs-lookup"><span data-stu-id="be729-139">Error handling</span></span>

<span data-ttu-id="be729-140">您应了解 API 响应错误代码并适当地处理它们。</span><span class="sxs-lookup"><span data-stu-id="be729-140">You should understand the API response error codes and handle them appropriately.</span></span> <span data-ttu-id="be729-141">以下是平台可能返回的错误代码的列表：</span><span class="sxs-lookup"><span data-stu-id="be729-141">Below is a list of error codes that may be returned by the platform:</span></span>

|<span data-ttu-id="be729-142">错误代码</span><span class="sxs-lookup"><span data-stu-id="be729-142">Error code</span></span> |  <span data-ttu-id="be729-143">错误名称</span><span class="sxs-lookup"><span data-stu-id="be729-143">Error Name</span></span>     | <span data-ttu-id="be729-144">Condition</span><span class="sxs-lookup"><span data-stu-id="be729-144">Condition</span></span>|
| --- | --- | --- |
| <span data-ttu-id="be729-145">**100**</span><span class="sxs-lookup"><span data-stu-id="be729-145">**100**</span></span> | <span data-ttu-id="be729-146">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="be729-146">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="be729-147">当前平台中不支持 API。</span><span class="sxs-lookup"><span data-stu-id="be729-147">API not supported in the current platform.</span></span>|
| <span data-ttu-id="be729-148">**404**</span><span class="sxs-lookup"><span data-stu-id="be729-148">**404**</span></span> | <span data-ttu-id="be729-149">FILE_NOT_FOUND</span><span class="sxs-lookup"><span data-stu-id="be729-149">FILE_NOT_FOUND</span></span> | <span data-ttu-id="be729-150">在给定位置找不到指定的文件。</span><span class="sxs-lookup"><span data-stu-id="be729-150">The file specified was not found on the given location.</span></span>|
| <span data-ttu-id="be729-151">**500**</span><span class="sxs-lookup"><span data-stu-id="be729-151">**500**</span></span> | <span data-ttu-id="be729-152">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="be729-152">INTERNAL_ERROR</span></span> | <span data-ttu-id="be729-153">执行所需操作时遇到内部错误。</span><span class="sxs-lookup"><span data-stu-id="be729-153">Internal error encountered while performing the required operation.</span></span>|
| <span data-ttu-id="be729-154">**1000**</span><span class="sxs-lookup"><span data-stu-id="be729-154">**1000**</span></span> | <span data-ttu-id="be729-155">PERMISSION_DENIED</span><span class="sxs-lookup"><span data-stu-id="be729-155">PERMISSION_DENIED</span></span> |<span data-ttu-id="be729-156">用户拒绝的权限。</span><span class="sxs-lookup"><span data-stu-id="be729-156">Permissions denied by the user.</span></span>|
| <span data-ttu-id="be729-157">**2000**</span><span class="sxs-lookup"><span data-stu-id="be729-157">**2000**</span></span> |<span data-ttu-id="be729-158">NETWORK_ERROR</span><span class="sxs-lookup"><span data-stu-id="be729-158">NETWORK_ERROR</span></span> | <span data-ttu-id="be729-159">网络问题。</span><span class="sxs-lookup"><span data-stu-id="be729-159">Network issue.</span></span>|
| <span data-ttu-id="be729-160">**3000**</span><span class="sxs-lookup"><span data-stu-id="be729-160">**3000**</span></span> | <span data-ttu-id="be729-161">NO_HW_SUPPORT</span><span class="sxs-lookup"><span data-stu-id="be729-161">NO_HW_SUPPORT</span></span> | <span data-ttu-id="be729-162">底层硬件不支持该功能。</span><span class="sxs-lookup"><span data-stu-id="be729-162">Underlying hardware doesn't support the capability.</span></span>|
| <span data-ttu-id="be729-163">**4000**</span><span class="sxs-lookup"><span data-stu-id="be729-163">**4000**</span></span>| <span data-ttu-id="be729-164">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="be729-164">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="be729-165">一个或多个参数无效。</span><span class="sxs-lookup"><span data-stu-id="be729-165">One or more arguments is invalid.</span></span>|
| <span data-ttu-id="be729-166">**5000**</span><span class="sxs-lookup"><span data-stu-id="be729-166">**5000**</span></span> | <span data-ttu-id="be729-167">UNAUTHORIZED_USER_OPERATION</span><span class="sxs-lookup"><span data-stu-id="be729-167">UNAUTHORIZED_USER_OPERATION</span></span> | <span data-ttu-id="be729-168">用户无权完成此操作。</span><span class="sxs-lookup"><span data-stu-id="be729-168">User is not authorized to complete this operation.</span></span>|
| <span data-ttu-id="be729-169">**6000**</span><span class="sxs-lookup"><span data-stu-id="be729-169">**6000**</span></span> |<span data-ttu-id="be729-170">INSUFFICIENT_RESOURCES</span><span class="sxs-lookup"><span data-stu-id="be729-170">INSUFFICIENT_RESOURCES</span></span> | <span data-ttu-id="be729-171">由于资源不足，无法完成该操作。</span><span class="sxs-lookup"><span data-stu-id="be729-171">The operation couldn't be completed due to insufficient resources.</span></span>|
|<span data-ttu-id="be729-172">**7000**</span><span class="sxs-lookup"><span data-stu-id="be729-172">**7000**</span></span> | <span data-ttu-id="be729-173">THROTTLE</span><span class="sxs-lookup"><span data-stu-id="be729-173">THROTTLE</span></span> | <span data-ttu-id="be729-174">平台限制了请求，因为调用 API 的频率过于频繁。</span><span class="sxs-lookup"><span data-stu-id="be729-174">The platform throttled the request because the API was invoked too frequently.</span></span>|
|  <span data-ttu-id="be729-175">**8000**</span><span class="sxs-lookup"><span data-stu-id="be729-175">**8000**</span></span> | <span data-ttu-id="be729-176">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="be729-176">USER_ABORT</span></span> |<span data-ttu-id="be729-177">用户中止了该操作。</span><span class="sxs-lookup"><span data-stu-id="be729-177">User aborted the operation.</span></span>|
| <span data-ttu-id="be729-178">**9000**</span><span class="sxs-lookup"><span data-stu-id="be729-178">**9000**</span></span>| <span data-ttu-id="be729-179">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="be729-179">OLD_PLATFORM</span></span> | <span data-ttu-id="be729-180">平台代码已过时，无法实现此 API。</span><span class="sxs-lookup"><span data-stu-id="be729-180">The platform code is outdated and doesn't implement this API.</span></span>|
| <span data-ttu-id="be729-181">**10000**</span><span class="sxs-lookup"><span data-stu-id="be729-181">**10000**</span></span>| <span data-ttu-id="be729-182">SIZE_EXCEEDED</span><span class="sxs-lookup"><span data-stu-id="be729-182">SIZE_EXCEEDED</span></span> |  <span data-ttu-id="be729-183">返回值太大，已超过平台大小边界。</span><span class="sxs-lookup"><span data-stu-id="be729-183">The return value is too big and has exceeded the platform size boundaries.</span></span>|

## <a name="sample-code-snippets"></a><span data-ttu-id="be729-184">示例代码片段</span><span class="sxs-lookup"><span data-stu-id="be729-184">Sample code snippets</span></span>

<span data-ttu-id="be729-185">**调用 `selectMedia` API**</span><span class="sxs-lookup"><span data-stu-id="be729-185">**Calling `selectMedia` API**</span></span>

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

<span data-ttu-id="be729-186">**调用 `getMedia` API**</span><span class="sxs-lookup"><span data-stu-id="be729-186">**Calling `getMedia` API**</span></span>

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

<span data-ttu-id="be729-187">**`viewImages`按 ID 调用 API**</span><span class="sxs-lookup"><span data-stu-id="be729-187">**Calling `viewImages`  API by ID**</span></span>

```javascript
view images by id:
    assumption: attachmentArray = select Media API Outputlet uriList = [];
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

<span data-ttu-id="be729-188">**通过 URL 调用 viewImages API**</span><span class="sxs-lookup"><span data-stu-id="be729-188">**Calling viewImages API by URL**</span></span>

```javascript
View Images by URL:
    // Assumption 2 urls, url1 and url2let uriList = [];
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
}
```
