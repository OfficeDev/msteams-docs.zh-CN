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
# <a name="camera-and-image-capabilities-in-teams"></a>团队中的照相机和图像功能

>[!IMPORTANT]
>
> * 目前，仅对移动客户端提供摄像头和图像功能的团队支持。
>* `selectMedia`、 `getMedia` 和 `viewImages` api 可从多个团队图面（例如任务模块、选项卡和个人应用程序）中进行调用。 有关更多详细信息，_请参阅_[团队应用程序的入口点](../extensibility-points.md)

您可以使用  [Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)轻松地将相机和图像功能集成到 microsoft team mobile 应用程序中。 SDK 为您的应用程序提供了访问用户的 [设备权限](native-device-permissions.md?tabs=desktop#device-permissions) 并生成更丰富的体验所需的工具。

[SelectMedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)、 [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)和[viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) api 使您能够使用本机相机/图像功能，如下所示：

* 使用本机 **相机控制** 允许用户在旅途中 **捕获和附加图像** 。
* 使用本机 **库支持** ，以允许用户 **选择设备图像** 作为附件。
* 使用本机 **图像查看器控件** 一次 **预览多个图像** 。
* 支持通过 SDK 桥) 的 **大图像传输** (最多为 50 MB
* 支持 **高级图像功能** ，允许用户预览和编辑图像：
  * 通过相机扫描文档、白板、名片等。
  * 裁剪并旋转图像。
  * 将文本、墨迹或手绘批注添加到图像中。

## <a name="get-started"></a>入门

通过添加属性和指定来更新文件的团队应用 [manifest.js](../../resources/schema/manifest-schema.md#devicepermissions) `devicePermissions` `media` 。 这样，您的应用程序就可以在最终用户使用相机捕获图像或打开库以选择要作为附件提交的图像之前，要求提供来自最终用户的必要权限。

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> 当相关的团队 API 启动时，将自动显示 " _请求权限_ " 提示。 有关更多详细信息，*请参阅*[请求设备权限](native-device-permissions.md)。

## <a name="using-camera-and-image-capability-apis"></a>使用相机和图像功能 Api

您可以使用以下 Api 集来启用相机和图像设备功能：

| API      | 说明   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest&branch=master#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)| 此 API 允许用户 **捕获或选择来自本机设备的媒体** 并返回到 web 应用程序。 用户可以选择在提交前编辑、裁剪、旋转、批注或绘制图像。 为响应 **selectMedia**，web 应用将接收所选图像的媒体 id，并且可能会收到选定媒体的缩略图。 |
| [**getMedia**](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest&branch=master#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| 此 API 以不考虑大小的块形式检索媒体。 组合这些区块并以文件/blob 的形式将其发送回 web 应用程序。 使用此 API，可以将图像分成多个较小的块，以方便进行大型图像传输。 |
| [**viewImages**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| 此 API 使用户能够以可滚动列表的形式查看全屏模式图像。|

**SELECTMEDIA API** 
 ![ 的 Web 应用程序体验团队中的设备照相机和图像体验](../../assets/images/tabs/image-capability-screenshot.jpg)

## <a name="error-handling"></a>错误处理

您应了解 API 响应错误代码并适当地处理它们。 以下是平台可能返回的错误代码的列表：

|错误代码 |  错误名称     | Condition|
| --- | --- | --- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | 当前平台中不支持 API。|
| **404** | FILE_NOT_FOUND | 在给定位置找不到指定的文件。|
| **500** | INTERNAL_ERROR | 执行所需操作时遇到内部错误。|
| **1000** | PERMISSION_DENIED |用户拒绝的权限。|
| **2000** |NETWORK_ERROR | 网络问题。|
| **3000** | NO_HW_SUPPORT | 底层硬件不支持该功能。|
| **4000**| INVALID_ARGUMENTS | 一个或多个参数无效。|
| **5000** | UNAUTHORIZED_USER_OPERATION | 用户无权完成此操作。|
| **6000** |INSUFFICIENT_RESOURCES | 由于资源不足，无法完成该操作。|
|**7000** | THROTTLE | 平台限制了请求，因为调用 API 的频率过于频繁。|
|  **8000** | USER_ABORT |用户中止了该操作。|
| **9000**| OLD_PLATFORM | 平台代码已过时，无法实现此 API。|
| **10000**| SIZE_EXCEEDED |  返回值太大，已超过平台大小边界。|

## <a name="sample-code-snippets"></a>示例代码片段

**调用 `selectMedia` API**

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

**调用 `getMedia` API**

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

**`viewImages`按 ID 调用 API**

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

**通过 URL 调用 viewImages API**

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
