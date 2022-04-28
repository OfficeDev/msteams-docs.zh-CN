---
title: 请求Microsoft Teams应用的设备权限
keywords: teams 应用功能权限设备本机扫描 qr 条形码图像音频视频
description: 如何更新应用清单以请求访问通常需要用户同意的本机功能，例如扫描 qr、条形码、图像、音频、视频功能
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 5269aed130714bc9afbe97b170d955d79d79abc8
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103304"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>请求Microsoft Teams应用的设备权限

可以使用本机设备功能（如相机、麦克风和位置）丰富Teams应用。 本文档介绍如何请求用户同意和访问本机设备权限。

> [!NOTE]
>
> * 若要在Microsoft Teams移动应用中集成媒体功能，请参阅[集成媒体功能](mobile-camera-image-permissions.md)。
> * 若要在Microsoft Teams移动应用中集成 QR 或条形码扫描程序功能，请参阅 [Teams 中的集成 QR 或条形码扫描程序功能](qr-barcode-scanner-capability.md)。
> * 若要集成Microsoft Teams移动应用中的位置功能，请参阅[集成位置功能](location-capability.md)。

## <a name="native-device-permissions"></a>本机设备权限

必须请求设备权限才能访问本机设备功能。 设备权限同样适用于所有应用构造，例如选项卡、任务模块或消息扩展。 用户必须转到Teams设置中的权限页才能管理设备权限。
通过访问设备功能，可以在Teams平台上构建更丰富的体验，例如：

* 捕获和查看图像。
* 扫描 QR 或条形码。
* 录制和共享短视频。
* 录制音频备忘录并保存以供以后使用。
* 使用用户的位置信息显示相关信息。

> [!NOTE]
> * 目前，Teams不支持多窗口应用、选项卡和会议侧面板的设备权限。
> * 在浏览器中，设备权限不同。 有关详细信息，请参阅 [浏览器设备权限](browser-device-permissions.md)。

## <a name="access-device-permissions"></a>访问设备权限

[Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) 提供了Teams移动应用访问用户设备[权限](#manage-permissions)和构建更丰富的体验所需的工具。

虽然新式 Web 浏览器中对这些功能的访问是标准的，但必须通过更新应用清单来告知Teams你使用的功能。 此更新允许在应用在桌面客户端Teams上运行时请求权限。

> [!NOTE]
> 目前，Microsoft Teams支持媒体功能和 QR 条形码扫描程序功能仅适用于移动客户端。

## <a name="manage-permissions"></a>管理权限

用户可以通过选择特定应用的 **“允许**”或 **“拒绝**”权限来管理Teams设置中的设备权限。

# <a name="mobile"></a>[移动设备](#tab/mobile)

1. 打开Teams。
1. 转到 **设置** > **应用权限**。
1. 选择需要为其选择设置的应用。
1. 选择所需的设置。

    ![“设备权限移动设置”屏幕](../../assets/images/tabs/MobilePermissions.png)

# <a name="desktop"></a>[桌面设备](#tab/desktop)

1. 打开Teams应用。
1. 选择窗口右上角的配置文件图标。
1. 从下拉菜单中选择 **设置** > **功能**。
1. 选择所需的设置。

   ![设备权限桌面设置屏幕](~/assets/images/tabs/device-permissions.png)

---

## <a name="specify-permissions"></a>指定权限

通过添加`devicePermissions`并指定在应用程序中使用的以下五个属性中的哪一个来更新应用`manifest.json`：

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

每个属性都允许提示用户请求其同意：

| 属性      | 说明   |
| --- | --- |
| 媒体         | 使用相机、麦克风、扬声器和访问媒体库的权限。 |
| 地理位置   | 返回用户位置的权限。      |
| 通知 | 发送用户通知的权限。      |
| Midi          | 从数字乐器发送和接收乐器数字界面 (MIDI) 信息的权限。   |
| openExternal  | 在外部应用程序中打开链接的权限。  |

## <a name="check-permissions-from-your-app"></a>检查应用的权限

添加 `devicePermissions` 到应用清单后，使用 **HTML5 权限 API** 检查权限，而不会引起提示：

``` JavaScript
// Different query options:
navigator.permissions.query({ name: 'camera' });
navigator.permissions.query({ name: 'microphone' });
navigator.permissions.query({ name: 'geolocation' });
navigator.permissions.query({ name: 'notifications' });
navigator.permissions.query({ name: 'midi', sysex: true });

// Example:
navigator.permissions.query({name:'geolocation'}).then(function(result) {
  if (result.state == 'granted') {
    // Access granted
  } else if (result.state == 'prompt') {
    // Access has not been granted
  }
});
```

## <a name="use-teams-apis-to-get-device-permissions"></a>使用Teams API 获取设备权限

利用适当的 HTML5 或 Teams API，显示获取设备权限许可的提示。

> [!IMPORTANT]
>
> * `camera`支持，`gallery`并通过 `microphone` [**selectMedia API**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) 启用。 对单个映像捕获使用 [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) 。
> * `location`支持是通过 [**getLocation API**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) 启用的。 必须将其用于`getLocation API`位置，因为 HTML5 地理位置 API 当前在桌面客户端Teams上不受完全支持。

例如：

* 若要提示用户访问其位置，必须调用 `getCurrentPosition()`：

    ```JavaScript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

* 若要提示用户在桌面或 Web 上访问其相机，必须调用 `getUserMedia()`：

    ```JavaScript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

* 若要在移动设备上捕获映像，Teams移动设备在调用时请求权限`captureImage()`：

    ```JavaScript
            function captureImage() {
            microsoftTeams.media.captureImage((error, files) => {
                // If there's any error, an alert shows the error message/code
                if (error) {
                    if (error.message) {
                        alert(" ErrorCode: " + error.errorCode + error.message);
                    } else {
                        alert(" ErrorCode: " + error.errorCode);
                    }
                } else if (files) {
                    image = files[0].content;
                    // Adding this image string in src attr of image tag will display the image on web page.
                    let imageString = "data:" + item.mimeType + ";base64," + image;
                }
            });
        } 
    ```

* 当你调用 `requestPermission()`时，通知会提示用户：

    ```JavaScript
    Notification.requestPermission(function(result) { /* ... */ });
    ```

* 若要使用相机或访问照片库，Teams移动设备在调用时请求权限`selectMedia()`：

    ```JavaScript
     function selectMedia() {
     microsoftTeams.media.selectMedia(mediaInput, (error, attachments) => {
         // If there's any error, an alert shows the error message/code
         if (error) {
             if (error.message) {
                 alert(" ErrorCode: " + error.errorCode + error.message);
             } else {
                 alert(" ErrorCode: " + error.errorCode);
             }
         } else if (attachments) {
             // creating image array which contains image string for all attached images. 
             const imageArray = attachments.map((item, index) => {
                 return ("data:" + item.mimeType + ";base64," + item.preview)
             })
         }
     });
    } 
  ```

* 若要使用麦克风，Teams移动设备在调用时请求权限`selectMedia()`：

    ```JavaScript
     function selectMedia() {
     microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
         // If there's any error, an alert shows the error message/code
         if (error) {
             if (error.message) {
                 alert(" ErrorCode: " + error.errorCode + error.message);
             } else {
                 alert(" ErrorCode: " + error.errorCode);
             }
         }

         if (attachments) {
             // taking the first attachment  
             let audioResult = attachments[0];

             // setting audio string which can be used in Video tag
             let audioData = "data:" + audioResult.mimeType + ";base64," + audioResult.preview
         }
     });
     }
    ```

* 若要提示用户共享地图界面上的位置，Teams移动请求权限时调用`getLocation()`：

    ```JavaScript
     function getLocation() {
     microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
         let currentLocation = JSON.stringify(location);
     });
     } 
    ```

# <a name="mobile"></a>[移动设备](#tab/mobile)

   ![选项卡移动设备权限提示](../../assets/images/tabs/MobileLocationPermission.png)

# <a name="desktop"></a>[桌面设备](#tab/desktop)

   ![Tabs 桌面设备权限提示](~/assets/images/tabs/device-permissions-prompt.png)

---

## <a name="permission-behavior-across-login-sessions"></a>跨登录会话的权限行为

为每个登录会话存储设备权限。 这意味着，如果登录到另一个Teams实例（例如在另一台计算机上），则以前的会话中的设备权限不可用。 因此，必须重新同意新会话的设备权限。 这也意味着，如果在Teams中注销Teams或切换租户，则设备权限将从上一个登录会话中删除。  

> [!NOTE]
> 当你同意本机设备权限时，它仅对 _当前_ 登录会话有效。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **Node.js** |
|---------------|--------------|--------|
|设备权限 | 使用Microsoft Teams选项卡示例应用演示设备权限 |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="see-also"></a>另请参阅

* [浏览器的设备权限](browser-device-permissions.md)
* [在 Teams 中集成媒体功能](mobile-camera-image-permissions.md)
* [在 Teams 中集成 QR 或条形码扫描程序功能](qr-barcode-scanner-capability.md)
* [在 Teams 中集成位置功能](location-capability.md)
