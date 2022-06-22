---
title: 集成媒体功能
author: Rajeshwari-v
description: 了解如何使用 Teams JavaScript 客户端 SDK 来使用代码示例启用媒体功能，并了解集成媒体功能的优势。
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: 366c58ac283e687f8a297b8701b932f99550574e
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2022
ms.locfileid: "66190238"
---
# <a name="integrate-media-capabilities"></a>集成媒体功能

可以将本机设备功能（如相机和麦克风）与Teams应用集成。 对于集成，可以使用 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)，为应用提供访问用户[设备权限](native-device-permissions.md)所需的工具。 使用合适的媒体功能 API 将设备功能（例如相机和麦克风）与Microsoft Teams应用中的Teams平台集成，并构建更丰富的体验。 媒体功能可用于Teams Web 客户端、桌面和移动设备。 若要集成媒体功能，必须更新应用清单文件并调用媒体功能 API。

若要进行有效的集成，必须充分了解用于调用相应 API 的[代码片段](#code-snippets)，以便使用本机媒体功能。 请务必熟悉 [API 响应错误](#error-handling)，以处理 Teams 应用中的错误。

## <a name="advantages"></a>优点

在 Teams 应用中集成设备功能的主要优势在于，可利用本机 Teams 控件为用户提供沉浸式的丰富体验。 以下方案展示了媒体功能的优势：

* 允许用户通过手机捕获物理白板上绘制的粗略模拟，并在Teams群聊中使用捕获的图像作为轮询选项。

* 允许用户录制音频消息并将其附加到事件票证。

* 允许用户从智能手机扫描物理文档以提交汽车保险索赔。

> [!NOTE]
>
> * 目前，Teams不支持弹出聊天窗口、选项卡和会议侧面板中的设备权限。</br>
> * 浏览器中的设备权限不同。 有关详细信息，请参阅[浏览器设备权限](browser-device-permissions.md)。
> * 启动相关Teams API 时，会在移动设备上自动显示请求权限提示。 有关详细信息，请参阅[请求设备权限](native-device-permissions.md)。

## <a name="update-manifest"></a>更新清单

通过添加 `devicePermissions` 属性并指定 `media` 来更新 Teams 应用 [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) 文件。 它允许应用在用户开始使用相机捕获图像、打开库以选择要作为附件提交的图像或使用麦克风录制对话之前请求用户提供必要权限。 应用清单的更新如下所示：

``` json
"devicePermissions": [
    "media",
],
```

## <a name="media-capability-apis"></a>媒体功能 API

[selectMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true)、[getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true) 和 [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) API 使你能够使用本机媒体功能，如下所示：

* 使用本机 **麦克风** 允许用户从设备 **录制音频**（录制 10 分钟聊天）。
* 使用本机 **相机控件** 允许用户在移动中 **捕获和附加图像**。
* 使用本机 **库支持** 允许用户 **选择设备图像** 作为附件。
* 使用本机 **图像查看器控件** 一次 **预览多个图像**。
* 支持通过 SDK 桥进行 **大型图像传输**（从 1 MB 到 50 MB）。
* 通过允许用户预览和编辑图像来支持 **高级映像功能** 。
* 通过相机扫描文档、白板和名片。
  
> [!IMPORTANT]
>
> * 可以从多个 Teams 表面（例如任务模块、选项卡和个人应用）调用 `selectMedia`、`getMedia`、`viewImages` API。 有关详细信息，请参阅 [Teams 应用的入口点](../extensibility-points.md)。</br>
> * `selectMedia` API 通过不同的输入配置支持相机和麦克风功能。
> * `selectMedia`用于访问麦克风功能的 API 仅支持移动客户端。

下表列出了一组用于启用设备媒体功能的 API：

| API      | 说明   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true)（**相机）**| 此 API 允许用户 **从设备相机捕获或选择媒体**，并将其返回到 Web 应用。 用户可以在提交前编辑、裁剪、旋转、批注或绘制图像。 为响应 `selectMedia`，Web 应用接收所选图像的媒体 ID 和所选媒体的缩略图。 可以通过 [ImageProps](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true) 配置进一步配置此 API。 |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true)（**麦克风**）| 将 [mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) `4` `selectMedia` 设置为 API 以访问麦克风功能。 此 API 还允许用户从设备麦克风录制音频，并将录制的剪辑返回到 Web 应用。 用户可以在提交前暂停、重新录制和播放录制预览。 为响应  **selectMedia**，Web 应用接收所选音频录制文件的媒体 ID。 <br/> 如果需要为录制对话配置持续时间（以分钟为单位），请使用 `maxDuration`。 当前录制持续时间为 10 分钟，时间一到便终止录制。  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)| 无论媒体大小如何，此 API 都以区块检索由 `selectMedia` API 捕获的媒体。 这些区块将作为文件或二进制大型对象组装并发送回 Web 应用。 将媒体拆分为较小的区块有助于进行大型文件传输。 |
| [**viewImages**](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true)| 此 API 使用户能够以可滚动列表的方式在全屏模式下查看图像。|

# <a name="mobile"></a>[移动设备](#tab/mobile)

下图描绘了映像功能的 `selectMedia` API 的 Web 应用体验：

:::image type="content" source="~/assets/images/tabs/media-capability-mobile2.png" alt-text="此图显示了移动设备的图像功能。" border="true":::

> [!NOTE]
>
> 在Android版本低于 7 的设备中`selectMedia`，API 会启动本机Android相机体验，而不是本机Teams相机体验。

下图描绘了用于麦克风功能的 `selectMedia` API 的 Web 应用体验：

:::image type="content" source="~/assets/images/tabs/microphone-capability.png" alt-text="插图显示了移动设备的麦克风功能。" border="true":::

# <a name="desktop"></a>[桌面设备](#tab/desktop)

下图描绘了映像功能的 `selectMedia` API 的 Web 应用体验：

:::image type="content" source="~/assets/images/tabs/media-capability-desktop1.png" alt-text="插图显示了桌面的媒体功能。" border="true":::

---

## <a name="error-handling"></a>错误处理

请确保在Teams应用中正确处理这些错误。 下表列出了错误代码和生成错误的说明：

|错误代码 |  错误名称     | 说明|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | 当前平台不支持 API。|
| **404** | FILE_NOT_FOUND | 未在给定位置找到指定的文件。|
| **500** | INTERNAL_ERROR | 执行所需的操作时遇到内部错误。|
| **1000** | PERMISSION_DENIED |权限被用户拒绝。|
| **3000** | NO_HW_SUPPORT | 硬件不支持该功能。|
| **4000**| INVALID_ARGUMENTS | 一个或多个参数无效。|
|  **8000** | USER_ABORT |用户中止了该操作。|
| **9000**| OLD_PLATFORM | 平台代码已过时，且未实施此 API。|
| **10000**| SIZE_EXCEEDED |  返回值太大，已超出平台大小限制。|

## <a name="code-snippets"></a>代码段

* 调用 `selectMedia` API 以使用相机捕获图像：

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

* 调用 `getMedia` API 以分块检索大型媒体：

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

* 按 ID 调用 `viewImages` API，由 API 返回 `selectMedia` ：

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

* 按 URL 调用 `viewImages` API：

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

* 通过麦克风录制音频的呼叫 `selectMedia` 和 `getMedia` API：

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
* [集成人员选取器](people-picker-capability.md)
* [应用程序托管的媒体机器人的要求和注意事项](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)