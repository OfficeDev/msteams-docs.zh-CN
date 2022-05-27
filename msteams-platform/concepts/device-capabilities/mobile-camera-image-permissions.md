---
title: 集成媒体功能
author: Rajeshwari-v
description: 了解如何使用代码示例利用 Teams JavaScript 客户端 SDK 启用媒体功能
keywords: 相机图像麦克风功能本机设备权限媒体 API
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: a65f39d3796bc0dacaa80f6badba7a011716edbf
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756756"
---
# <a name="integrate-media-capabilities"></a>集成媒体功能

可以与 Teams 应用集成本机设备功能，如 **相机** 和 **麦克风**。 对于集成，可以使用 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)，该 SDK 提供应用访问用户[设备权限](native-device-permissions.md)所需的工具。 使用合适的媒体功能 API 将设备功能（如 **相机** 和 **麦克风**）与 Microsoft Teams 移动应用中的 Teams 平台集成，并构建更丰富的体验。

## <a name="advantage-of-integrating-media-capabilities"></a>集成媒体功能的优势

在 Teams 应用中集成设备功能的主要优势在于，可利用本机 Teams 控件为用户提供沉浸式的丰富体验。
若要集成媒体功能，必须更新应用清单文件并调用媒体功能 API。

若要进行有效的集成，必须充分了解用于调用相应 API 的[代码片段](#code-snippets)，以便使用本机媒体功能。

请务必熟悉 [API 响应错误](#error-handling)，以处理Teams应用中的错误。

> [!NOTE]
>
> * 目前，媒体功能Microsoft Teams支持仅适用于移动客户端。
> * 目前，Teams 不支持多窗口应用、选项卡和会议侧面板的设备权限。
> * 在浏览器中，设备权限不同。 有关详细信息，请参阅[浏览器设备权限](browser-device-permissions.md)。

## <a name="update-manifest"></a>更新清单

通过添加 `devicePermissions` 属性并指定 `media` 来更新 Teams 应用 [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) 文件。 它允许应用在用户开始使用 **相机** 捕获图像、打开库以选择要作为附件提交的图像或使用 **麦克风** 录制对话之前请求用户提供必要权限。 应用清单的更新如下所示：

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> 启动相关 Teams API 时，将自动显示“**请求权限**”提示。 有关详细信息，请参阅[请求设备权限](native-device-permissions.md)。

## <a name="media-capability-apis"></a>媒体功能 API

[selectMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true)、[getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true) 和 [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) API 使你能够使用本机媒体功能，如下所示：

* 使用本机 **麦克风** 允许用户从设备 **录制音频**（录制 10 分钟聊天）。
* 使用本机 **相机控件** 允许用户在移动中 **捕获和附加图像**。
* 使用本机 **库支持** 允许用户 **选择设备图像** 作为附件。
* 使用本机 **图像查看器控件** 一次 **预览多个图像**。
* 支持通过 SDK 桥进行 **大型图像传输**（从 1 MB 到 50 MB）。
* 支持 **高级图像功能**，用户可以预览和编辑图像：
  * 通过相机扫描文档、白板和名片。
  
> [!IMPORTANT]
>
> * 可以从多个 Teams 表面（例如任务模块、选项卡和个人应用）调用 `selectMedia`、`getMedia`、`viewImages` API。 有关详细信息，请参阅[Teams应用的入口点](../extensibility-points.md)。
> * `selectMedia` API 已扩展为支持麦克风和音频属性。

必须使用以下一组 API 来启用设备的媒体功能：

| API      | 说明   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true)（**相机）**| 此 API 允许用户 **从设备相机捕获或选择媒体**，并将其返回到 Web 应用。 用户可以在提交前编辑、裁剪、旋转、批注或绘制图像。 为响应 `selectMedia`，Web 应用接收所选图像的媒体 ID 和所选媒体的缩略图。 可以通过 [ImageProps](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true) 配置进一步配置此 API。 |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true)（**麦克风**）| 在 `selectMedia` API 中将 [mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) 设置为 `4`，以访问麦克风功能。 此 API 还允许用户从设备麦克风录制音频，并将录制的剪辑返回到 Web 应用。 用户可以在提交前暂停、重新录制和播放录制预览。 为响应  **selectMedia**，Web 应用接收所选音频录制文件的媒体 ID。 <br/> 如果需要为录制对话配置持续时间（以分钟为单位），请使用 `maxDuration`。 当前录制持续时间为 10 分钟，时间一到便终止录制。  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)| 无论媒体大小如何，此 API 都以区块检索由 `selectMedia` API 捕获的媒体。 这些区块将作为文件或二进制大型对象组装并发送回 Web 应用。 将媒体拆分为较小的区块有助于进行大型文件传输。 |
| [**viewImages**](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true)| 此 API 使用户能够以可滚动列表的方式在全屏模式下查看图像。|

下图描绘了用于图像功能的 `selectMedia` API 的 Web 应用体验：

![Teams 中的设备相机和图像体验](../../assets/images/tabs/image-capability.png)

下图描绘了用于麦克风功能的 `selectMedia` API 的 Web 应用体验：

![麦克风功能的 Web 应用体验](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a>错误处理

必须确保在 Teams 应用中正确处理这些错误。 下表列出了错误代码和产生错误的条件：

|错误代码 |  错误名称     | 条件|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | 当前平台不支持 API。|
| **404** | FILE_NOT_FOUND | 指定的文件在给定位置中找不到。|
| **500** | INTERNAL_ERROR | 执行所需的操作时遇到内部错误。|
| **1000** | PERMISSION_DENIED |权限被用户拒绝。|
| **3000** | NO_HW_SUPPORT | 基础硬件不支持此功能。|
| **4000**| INVALID_ARGUMENTS | 一个或多个参数无效。|
|  **8000** | USER_ABORT |用户中止了该操作。|
| **9000**| OLD_PLATFORM | 平台代码已过时，不实现此 API。|
| **10000**| SIZE_EXCEEDED |  返回值太大，已超出平台大小限制。|

## <a name="code-snippets"></a>代码段

**调用 `selectMedia` API** 用于使用相机捕获图像：

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

**调用 `getMedia` API** 用于按区块检索大型媒体：

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

**按 `selectMedia` API 返回的 ID 调用 `viewImages` API**：

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

**按 URL 调用 `viewImages` API**：

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

**调用用于通过麦克风录制音频的 `selectMedia` 和 `getMedia` API**：

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

* [在 Teams 中集成 QR 或条形码扫描程序功能](qr-barcode-scanner-capability.md)
* [在 Teams 中集成位置功能](location-capability.md)
* [在 Teams 中集成人员选取器](people-picker-capability.md)
* [应用程序托管的媒体机器人的要求和注意事项](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
