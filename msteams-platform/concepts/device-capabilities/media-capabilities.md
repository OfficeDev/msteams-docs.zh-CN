---
title: 集成媒体功能
author: Rajeshwari-v
description: 了解如何使用 Teams JavaScript 客户端 SDK 使用代码示例启用媒体功能，并了解集成媒体功能的优势。
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: bfa63b42383e507f004b0225c64f381e47e547f0
ms.sourcegitcommit: 1ea035bc20303070268db38472839584ad4280b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2022
ms.locfileid: "68653369"
---
# <a name="integrate-media-capabilities"></a>集成媒体功能

可以将本机设备功能（例如相机和麦克风）与 Teams 应用集成。 为了进行集成，可以使用 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) 为应用提供访问用户 [设备权限](native-device-permissions.md)所需的工具。 使用合适的媒体功能 API 将设备功能（例如相机和麦克风）与 Microsoft Teams 应用中的 Teams 平台集成，并构建更丰富的体验。 媒体功能适用于 Teams Web 客户端、桌面和移动设备。 若要集成媒体功能，必须更新应用清单文件并调用媒体功能 API。

若要进行有效的集成，必须充分了解用于调用相应 API [的代码片段](#code-snippets) ，这样就可以使用本机媒体功能。 请务必熟悉 [API 响应错误](#error-handling)，以处理 Teams 应用中的错误。

## <a name="advantages"></a>优点

将设备功能集成到 Teams 应用中的优点在于，它使用本机 Teams 控件为用户提供丰富而身临其境的体验。 以下方案展示了媒体功能的优势：

* 允许用户通过手机捕获物理白板上绘制的粗略模型，并使用捕获的图像作为 Teams 群聊中的轮询选项。

* 允许用户录制音频消息并将其附加到事件票证。

* 允许用户从智能手机扫描物理文档以提交汽车保险索赔。

* 允许用户在工作现场录制视频并上传该视频以供出席。

> [!NOTE]
>
> * 目前，Teams 不支持弹出聊天窗口、选项卡和会议侧面板中的设备权限。</br>
> * 浏览器中的设备权限不同。 有关详细信息，请参阅[浏览器设备权限](browser-device-permissions.md)。
> * 启动相关 Teams API 时，将自动在移动设备上显示请求权限提示。 有关详细信息，请参阅[请求设备权限](native-device-permissions.md)。

## <a name="update-manifest"></a>更新清单

通过添加 `devicePermissions` 属性并指定 `media` 来更新 Teams 应用 [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) 文件。 它允许应用在用户开始使用相机捕获图像、打开库以选择要作为附件提交的图像或使用麦克风录制对话之前请求用户提供必要权限。 应用清单的更新如下所示：

``` json
"devicePermissions": [
    "media",
],
```

## <a name="media-capability-apis"></a>媒体功能 API

[selectMedia](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-selectmedia)、[getMedia](/javascript/api/@microsoft/teams-js/media.media#@microsoft-teams-js-media-media-getmedia) 和 [viewImages](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-viewimages) API 使你能够使用本机媒体功能，如下所示：

* 使用本机 **麦克风** 允许用户从设备 **录制音频**（录制 10 分钟聊天）。
* 使用本机 **相机控件** 允许用户 **捕获和附加图像** ，并 **捕获视频** (录制最多 5 分钟的视频) 。
* 使用本机 **库支持** 允许用户 **选择设备图像** 作为附件。
* 使用本机 **图像查看器控件** 一次 **预览多个图像**。
* 支持通过 SDK 桥进行 **大型图像传输**（从 1 MB 到 50 MB）。
* 通过允许用户预览和编辑图像来支持 **高级映像功能** 。
* 通过相机扫描文档、白板和名片。
  
> [!IMPORTANT]
>
> * 可以从多个 Teams 表面（例如任务模块、选项卡和个人应用）调用 `selectMedia`、`getMedia`、`viewImages` API。 有关详细信息，请参阅 [Teams 应用的入口点](../extensibility-points.md)。</br>
> * API `selectMedia` 通过不同的输入配置支持相机和麦克风功能。
> * `selectMedia`用于访问麦克风功能的 API 仅支持移动客户端。
> * 上传的图像的最大计数由 [`maxMediaCount`](/javascript/api/@microsoft/teams-js/media.mediainputs#@microsoft-teams-js-media-mediainputs-maxmediacount) API 返回的数组总大小决定，也由 `selectMedia` 该 API 返回的总大小决定。 确保数组大小不超过 4 MB，如果数组大小超过 4 MB，则 API 将生成错误代码 10000，SIZE_EXCEEDED错误。

下表列出了一组用于启用设备媒体功能的 API：

| API      | 说明   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-selectmedia)（**相机）**| 此 API 允许用户 **从设备相机捕获或选择媒体**，并将其返回到 Web 应用。 用户可以在提交前编辑、裁剪、旋转、批注或绘制图像。 为响应 `selectMedia`，Web 应用接收所选图像的媒体 ID 和所选媒体的缩略图。 可以通过 [ImageProps](/javascript/api/@microsoft/teams-js/media.imageprops) 配置进一步配置此 API。 |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-selectmedia)（**麦克风**）| 将 [mediaType](/javascript/api/@microsoft/teams-js/media.mediatype) 设置为 `4` 在 API 中 (音频) `selectMedia` 以访问麦克风功能。 此 API 还允许用户从设备麦克风录制音频，并将录制的剪辑返回到 Web 应用。 用户可以在提交前暂停、重新录制和播放录制预览。 作为对 **selectMedia** 的响应，Web 应用接收所选录音的媒体 ID。 <br/> 如果需要为录制对话配置持续时间（以分钟为单位），请使用 `maxDuration`。 当前录制持续时间为 10 分钟，时间一到便终止录制。  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/media.media#@microsoft-teams-js-media-media-getmedia)| 无论媒体大小如何，此 API 都以区块检索由 `selectMedia` API 捕获的媒体。 这些区块将作为文件或二进制大型对象组装并发送回 Web 应用。 将媒体拆分为较小的区块有助于进行大型文件传输。 |
| [**viewImages**](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-viewimages)| 此 API 使用户能够以可滚动列表的方式在全屏模式下查看图像。|

# <a name="mobile"></a>[移动设备](#tab/mobile)

下图描绘了映像功能的 `selectMedia` API 的 Web 应用体验：

:::image type="content" source="~/assets/images/tabs/media-capability-mobile2.png" alt-text="此图显示了移动设备的图像功能。":::

> [!NOTE]
> 在 Android 版本低于 7 的设备中 `selectMedia` ，API 会启动本机 Android 相机体验，而不是本机 Teams 相机体验。

下图描绘了用于麦克风功能的 `selectMedia` API 的 Web 应用体验：

:::image type="content" source="~/assets/images/tabs/microphone-capability.png" alt-text="插图显示了移动设备的麦克风功能。":::

# <a name="desktop"></a>[桌面设备](#tab/desktop)

下图描绘了映像功能的 `selectMedia` API 的 Web 应用体验：

:::image type="content" source="~/assets/images/tabs/media-capability-desktop1.png" alt-text="插图显示了桌面的媒体功能。":::

---

## <a name="error-handling"></a>错误处理

请确保在 Teams 应用中正确处理这些错误。 下表列出了错误代码和生成错误的说明：

|错误代码 |  错误名称     | 说明|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | 当前平台不支持 API。|
| **404** | FILE_NOT_FOUND | 指定的文件在给定位置中找不到。|
| **500** | INTERNAL_ERROR | 执行所需的操作时遇到内部错误。|
| **1000** | PERMISSION_DENIED |权限被用户拒绝。|
| **3000** | NO_HW_SUPPORT | 硬件不支持该功能。|
| **4000**| INVALID_ARGUMENTS | 一个或多个参数无效。|
|  **8000** | USER_ABORT |用户中止了该操作。|
| **9000**| OLD_PLATFORM | 平台代码已过时，不实现此 API。|
| **10000**| SIZE_EXCEEDED |  返回值太大，已超出平台大小边界。|

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

* 使用相机调用 `selectMedia` API 捕获视频：

  * `fullscreen: true`使用：

       `fullscreen: true` 在视频录制模式下打开相机。 它提供了使用前置和后置摄像头的选项，还提供以下示例中所述的其他属性：

       ```javascript
        
         const defaultLensVideoProps: microsoftTeams.media.VideoProps = {
             sources: [microsoftTeams.media.Source.Camera, microsoftTeams.media.Source.Gallery],
             startMode: microsoftTeams.media.CameraStartMode.Video,
             cameraSwitcher: true,
             maxDuration: 30
        }
         const defaultLensVideoMediaInput: microsoftTeams.media.MediaInputs = {
             mediaType: microsoftTeams.media.MediaType.Video,
             maxMediaCount: 6,
             videoProps: defaultLensVideoProps
        }
       ```

  * `fullscreen: false`使用：

       `fullscreen: false` 在视频录制模式下打开相机，并仅使用前置摄像头。 通常 `fullscreen: false` 当用户想要在设备屏幕上阅读内容时录制视频时使用。

       此模式还支持 `isStopButtonVisible: true` 在屏幕上添加一个可让用户停止录制的停止按钮。 如果 `isStopButtonVisible: false`可以调用 mediaController API 或在录制持续时间达到 `maxDuration` 指定时间时停止录制。

       下面是一个示例，用于在指定的时间内停止录制 `maxDuration` ：

       ```javascript
          const defaultNativeVideoProps: microsoftTeams.media.VideoProps = {
             maxDuration: 30,
             isFullScreenMode: false,
             isStopButtonVisible: false,
             videoController: new microsoftTeams.media.VideoController(videoControllerCallback)
         }
          const defaultNativeVideoMediaInput: microsoftTeams.media.MediaInputs = {
             mediaType: microsoftTeams.media.MediaType.Video,
             maxMediaCount: 1,
             videoProps: defaultNativeVideoProps
         }
       ```

       下面是通过调用 mediaController API 来停止录制的示例：

       ```javascript
          const defaultNativeVideoProps: microsoftTeams.media.VideoProps = {
             videoController.stop(),
             isFullScreenMode: false,
             isStopButtonVisible: false,
             videoController: new microsoftTeams.media.VideoController(videoControllerCallback)
         }
          const defaultNativeVideoMediaInput: microsoftTeams.media.MediaInputs = {
             mediaType: microsoftTeams.media.MediaType.Video,
             maxMediaCount: 1,
             videoProps: defaultNativeVideoProps
         }
       ```

* 调用 `selectMedia` API 以使用相机捕获图像和视频：

  这允许用户在捕获图像或视频之间进行选择。

    ```javascript
    
      const defaultVideoAndImageProps: microsoftTeams.media.VideoAndImageProps = {
        sources: [microsoftTeams.media.Source.Camera, microsoftTeams.media.Source.Gallery],
        startMode: microsoftTeams.media.CameraStartMode.Photo,
        ink: true,
        cameraSwitcher: true,
        textSticker: true,
        enableFilter: true,
        maxDuration: 30
      }
    
      const defaultVideoAndImageMediaInput: microsoftTeams.media.MediaInputs = {
        mediaType: microsoftTeams.media.MediaType.VideoAndImage,
        maxMediaCount: 6,
        videoAndImageProps: defaultVideoAndImageProps
      }
    
      let videoControllerCallback: microsoftTeams.media.VideoControllerCallback = {
        onRecordingStarted() {
          console.log('onRecordingStarted Callback Invoked');
        },
      };
    
      microsoftTeams.media.selectMedia(defaultVideoAndImageMediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
        if (error) {
            if (error.message) {
                alert(" ErrorCode: " + error.errorCode + error.message);
            } else {
                alert(" ErrorCode: " + error.errorCode);
            }
        }
        
        var videoElement = document.createElement("video");
        attachments[0].getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
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
        videoElement.setAttribute("src", ("data:" + audioResult.mimeType + ";base64," + audioResult.preview));
        audioResult.getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
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
    });
    ```

## <a name="file-download-on-teams-mobile"></a>Teams 移动版上的文件下载

可以配置应用，使用户能够将文件从 Webview 下载到其移动设备。

>[!NOTE]
> 下载文件仅在 Android Teams 移动客户端上受支持，只能下载未经身份验证的文件。

若要启用，请执行以下步骤：

1. 通过添加`devicePermissions`属性并指定更新[清单](#update-manifest)中所示，`media`更新 Teams 应用 [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) 文件。

2. 使用以下格式，并将 HMTL 下载属性添加到网页：

    ```html
    <a href="path_to_file" download="download">Download</a>
    ```

## <a name="see-also"></a>另请参阅

* [在 Teams 中集成 QR 或条形码扫描程序功能](qr-barcode-scanner-capability.md)
* [在 Teams 中集成位置功能](location-capability.md)
* [集成人员选取器](people-picker-capability.md)
* [应用程序托管的媒体机器人的要求和注意事项](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
