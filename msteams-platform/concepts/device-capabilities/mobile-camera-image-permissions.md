---
title: 集成媒体功能
author: Rajeshwari-v
description: 如何使用 JavaScript Teams SDK 启用媒体功能
keywords: 相机图像麦克风功能本机设备权限媒体
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 74ebeee5392272021f2a9977709fc0b1df2a50b1
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345730"
---
# <a name="integrate-media-capabilities"></a>集成媒体功能 

你可以将本机设备功能（如相机和 **麦克风**）与你的应用Teams集成。 对于集成，可以使用[javaScript Microsoft Teams SDK，](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)它提供应用访问用户设备权限[所需的工具](native-device-permissions.md)。 使用合适的媒体功能 API 将设备功能（如相机和麦克风）与Microsoft Teams 移动应用中的 Teams 平台集成，并构建更丰富的体验。 

## <a name="advantage-of-integrating-media-capabilities"></a>集成媒体功能的优势

将设备功能集成到 Teams 应用中的主要优点是它利用本机 Teams 控件为用户提供丰富且沉浸式的体验。
若要集成媒体功能，必须更新应用清单文件并调用媒体功能 API。 

为了进行有效的集成，你必须深入了解用于调用相应[](#code-snippets)API 的代码段，这允许你使用本机媒体功能。

熟悉 API 响应错误以处理应用[](#error-handling)内的错误Teams很重要。

> [!NOTE] 
> * 目前Microsoft Teams媒体功能的支持仅适用于移动客户端。   
> * 目前，Teams不支持多窗口应用、选项卡和会议侧窗格的设备权限。    

## <a name="update-manifest"></a>更新清单

通过添加 Teams 并[manifest.js](../../resources/schema/manifest-schema.md#devicepermissions) `devicePermissions` ，更新文件上的应用 `media` 。 它允许你的应用在用户开始使用相机捕获图像之前，向用户请求必要的权限，打开库以选择要作为附件提交的图像，或使用麦克风录制对话。  应用清单的更新如下所示：

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> 启动 **相关应用程序** API 时，将自动显示Teams权限提示。 有关详细信息，请参阅请求 [设备权限](native-device-permissions.md)。

## <a name="media-capability-apis"></a>媒体功能 API

[selectMedia、getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true)和[viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) API 使您可以使用本机媒体功能，如下所示： [](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)

* 使用本机 **麦克风** 允许用户从设备 **录制 (** 10 分钟的对话) 录制音频。
* 使用 **本机相机控件** 允许用户 **在移动时捕获和** 附加图像。
* 使用 **本机库支持** 以允许用户 **选择设备图像作为** 附件。
* 使用本机 **图像查看器控件一****次预览** 多个图像。
* 通过 SDK **桥** (从 1 MB 到 50 MB) 大图像传输。
* 支持 **允许用户预览** 和编辑图像的高级图像功能：
  * 通过相机扫描文档、白板和名片。
  
> [!IMPORTANT]
> * 、和 API 可以从多个Teams接口（如任务 `selectMedia` `getMedia` 模块、选项卡和个人应用） `viewImages` 调用。 有关详细信息，请参阅应用[Teams点](../extensibility-points.md)。
> * `selectMedia` API 已扩展以支持麦克风和音频属性。

你必须使用以下一组 API 来启用设备的媒体功能：

| API      | 说明   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Camera)**| 此 API 允许用户从 **设备相机捕获** 或选择媒体，并返回到 Web 应用。 用户可以在提交之前编辑、裁剪、旋转、批注或绘制图像。 作为响应，Web 应用接收所选图像的媒体 `selectMedia` ID 和所选媒体的缩略图。 可以通过 [ImageProps](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true) 配置进一步配置此 API。 |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**麦克风**) | 在 [API 中将 mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) `4` 设置为 `selectMedia` ，以访问麦克风功能。 此 API 还允许用户从设备麦克风录制音频，将录制的剪辑返回到 Web 应用。 用户可以在提交之前暂停、重新录制和播放录制预览。 作为对 **selectMedia 的响应**，Web 应用接收所选音频录制的媒体 ID。 <br/> 如果需要 `maxDuration` 为录制对话配置持续时间（以分钟表示）。请使用 。 录制的当前持续时间为 10 分钟，之后将终止录制。  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)| 此 API 检索 API 以区块捕获的媒体， `selectMedia` 而不考虑媒体大小。 这些区块将组合在一起，作为文件或 blob 发送回 Web 应用。 将媒体分成较小的区块便于大型文件传输。 |
| [**viewImages**](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true)| 此 API 使用户能够在全屏模式下以可滚动列表的方式查看图像。|

下图描述了 API 的 Web 应用体验 `selectMedia` ，用于图像功能：

![设备相机和图像体验在Teams](../../assets/images/tabs/image-capability.png)

下图描述了 API 的麦克风功能 `selectMedia` Web 应用体验：

![麦克风功能 Web 应用体验](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a>错误处理

必须确保在你的应用内正确处理这些Teams错误。 下表列出了错误代码以及生成错误的条件： 

|错误代码 |  错误名称     | 条件|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API 在当前平台上不受支持。|
| **404** | FILE_NOT_FOUND | 在给定位置找不到指定的文件。|
| **500** | INTERNAL_ERROR | 执行所需操作时遇到内部错误。|
| **1000** | PERMISSION_DENIED |用户拒绝权限。|
| **3000** | NO_HW_SUPPORT | 基础硬件不支持该功能。|
| **4000**| INVALID_ARGUMENTS | 一个或多个参数无效。|
|  **8000** | USER_ABORT |用户中止操作。|
| **9000**| OLD_PLATFORM | 平台代码已过时，不实现此 API。|
| **10000**| SIZE_EXCEEDED |  返回值太大，已超出平台大小边界。|

## <a name="code-snippets"></a>代码段

**呼叫 `selectMedia` 用于** 使用相机捕获图像的 API：

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

**呼叫 `getMedia` 用于** 检索区块中的大型媒体的 API：

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

**呼叫 `viewImages`API 返回的按 ID `selectMedia` 表示的 API：**

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

**呼叫 `viewImages`按 URL 的 API：**

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

**用于 `selectMedia` 通过 `getMedia` 麦克风录制音频的呼叫和 API：**

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

## <a name="see-also"></a>另请参阅

* [将 QR 或条形码扫描仪功能集成到 Teams](qr-barcode-scanner-capability.md)
* [将位置功能集成到Teams](location-capability.md)
* [将人员选取器集成到Teams](people-picker-capability.md)

