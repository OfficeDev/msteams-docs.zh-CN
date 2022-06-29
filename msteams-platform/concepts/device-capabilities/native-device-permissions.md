---
title: 为 Microsoft Teams 应用请求设备权限
description: 如何更新应用清单，以请求访问需要用户同意的本机功能，例如扫描 QR、条形码、图像、音频和视频功能
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: a573855b6512cdbfcebb12c305973f8ad23113d6
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2022
ms.locfileid: "66484486"
---
# <a name="request-device-permissions-for-your-teams-app"></a>请求 Teams 应用的设备权限

可使用本机设备功能（如摄像头、麦克风和位置）丰富 Teams 应用。 本文档指导如何请求用户同意和访问本机设备权限。

> [!NOTE]
>
> * 若要在 Microsoft Teams Web 客户端、桌面和移动设备中集成媒体功能，请参阅 [集成媒体功能](media-capabilities.md)。
> * 要在 Microsoft Teams 移动应用中集成 QR 或条形码扫描程序功能，请参阅 [在 Teams 中集成 QR 或条形码扫描程序功能](qr-barcode-scanner-capability.md)。
> * 若要在 Teams Web 客户端、桌面和移动设备中集成位置功能，请参阅 [集成位置功能](location-capability.md)。

## <a name="native-device-permissions"></a>本机设备权限

必须请求设备权限才能访问本机设备功能。 设备权限同样适用于所有应用构造，例如选项卡、任务模块或消息传递扩展。 用户必须转到 Teams 设置中的权限页面才能管理设备权限。 你可以借助设备功能在 Teams 平台上构建更丰富的体验，例如：必须请求设备权限才能访问本机设备功能。 设备权限对所有应用程序构造（如选项卡、任务模块或消息扩展）的作用类似。 用户必须转到 Teams 设置中的权限页面才能管理设备权限。
通过访问设备功能，您可以在 Teams 平台上构建更丰富的体验，例如：

* 捕获和查看图像。
* 扫描 QR 或条形码。
* 录制和分享短视频。
* 录制音频备忘录并将其保存以备日后使用。
* 使用用户的位置信息以显示相关信息。

> [!NOTE]
>
> * 目前，Teams 不支持多窗口应用、选项卡和会议侧面板的设备权限。
> * 浏览器中的设备权限不同。 有关详细信息，请参阅[浏览器设备权限](browser-device-permissions.md)。
> * 目前，Teams 支持 QR 条形码扫描程序功能仅适用于移动客户端。

## <a name="access-device-permissions"></a>访问设备权限

[Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) 提供 Teams 应用访问用户[设备权限](#manage-permissions)和构建更丰富的体验所需的工具。

虽然在 web 浏览器中一般都能访问这些功能，但必须通过更新应用清单来通知 Teams 你使用的功能。 此更新允许在应用在 Teams 桌面上运行时请求权限。

## <a name="manage-permissions"></a>管理权限

用户可以通过选择 **允许** 或 **拒绝** 特定应用的权限，在 Teams 设置中管理设备权限。

# <a name="mobile"></a>[移动设备](#tab/mobile)

1. 打开 Teams。
1. 转到“**设置**” > “**应用权限**”。
1. 请选择需要为其选择设置的应用。
1. 选择所需设置。

    <!-- ![Device permissions mobile settings screen](../../assets/images/tabs/MobilePermissions.png) -->

    :::image type="content" source="~/assets/images/tabs/MobilePermissions.png" alt-text="移动权限。" border="true":::

# <a name="desktop"></a>[桌面设备](#tab/desktop)

1. 打开 Teams 应用。
1. 选择窗口右上角的个人资料图标。
1. 从下拉菜单中选择“**设置**” > “**权限**”。
1. 选择所需设置。

   <!-- ![Device permissions desktop settings screen](~/assets/images/tabs/device-permissions.png) -->

   :::image type="content" source="~/assets/images/tabs/device-permissions.png" alt-text="设备权限。" border="true":::

---

## <a name="specify-permissions"></a>指定权限

通过添加 `devicePermissions` 并指定应用中使用的以下五个属性中的哪一个来更新应用的 `manifest.json`：

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
| 媒体         | 允许使用摄像头、麦克风、扬声器和访问媒体库。 |
| 地理位置   | 返回用户位置的权限。      |
| 通知 | 发送用户通知的权限。      |
| midi          | 允许从数字乐器发送和接收乐器数字接口 (MIDI) 信息。   |
| openExternal  | 在外部应用中打开链接的权限。  |

## <a name="check-permissions-from-your-app"></a>检查应用的权限

添加 `devicePermissions` 到应用清单后，请使用 **HTML5 权限 API** 检查权限，而不导致出现提示：

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

## <a name="use-teams-apis-to-get-device-permissions"></a>使用 Teams API 获取设备权限

利用适当的 HTML5 或 Teams API 显示获取访问设备权限许可的提示。

> [!IMPORTANT]
>
> * 通过 [**selectMedia API**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) 启用对 `camera`、`gallery`和 `microphone` 的支持。 使用 [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) 进行单一图像捕获。
> * 通过 [**getLocation API**](/javascript/api/@microsoft/teams-js/microsoftteams.location?.view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true) 启用对 `location` 的支持。 必须将此 `getLocation API` 位置用于位置，因为 Teams 桌面上当前不完全支持 HTML5 地理位置 API。

例如：

* 若要提示用户访问其位置，必须调用 `getCurrentPosition()`：

    ```JavaScript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

* 若要提示用户在桌面或 Web 上访问其相机，必须调用 `getUserMedia()`：

    ```JavaScript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

* 若要在移动设备上捕获映像，请在调用时向 Teams 移动版请求权限 `captureImage()`：

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

* 若要使用相机或访问照片库，Teams 应用会在调用时请求权限 `selectMedia()`：

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

* 要使用麦克风，Teams 移动版会在调用 `selectMedia()` 时请求权限：

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

* 若要提示用户在地图界面上共享位置，请在调用时向 Teams 应用请求权限 `getLocation()`：

    ```JavaScript
     function getLocation() {
     microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
         let currentLocation = JSON.stringify(location);
     });
     } 
    ```

# <a name="mobile"></a>[移动设备](#tab/mobile)

   <!-- ![Tabs mobile device permissions prompt](../../assets/images/tabs/MobileLocationPermission.png) -->

   :::image type="content" source="~/assets/images/tabs/MobileLocationPermission.png" alt-text="移动位置权限。" border="true":::

# <a name="desktop"></a>[桌面设备](#tab/desktop)

   <!-- ![Tabs desktop device permissions prompt](~/assets/images/tabs/device-permissions-prompt.png) -->

   :::image type="content" source="~/assets/images/tabs/device-permissions-prompt.png" alt-text="桌面中的设备权限。" border="true":::

---

## <a name="permission-behavior-across-login-sessions"></a>跨登录会话的权限行为

为每个登录会话存储设备权限。 这表示如果登录到 Teams 的另一个实例 (例如，在另一台计算机上)，先前会话中的设备权限将不可用。 因此，必须重新同意新会话的设备权限。 这也表示如果退出登录 Teams 或在 Teams 中切换租户，设备权限将从先前登录会话中删除。  

> [!NOTE]
> 同意本机设备权限时，它仅对 _当前_ 登录会话有效。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **Node.js** |
|---------------|--------------|--------|
|设备权限 | 使用 Microsoft Teams 选项卡示例应用演示设备权限 |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="see-also"></a>另请参阅

* [浏览器的设备权限](browser-device-permissions.md)
* [集成媒体功能](media-capabilities.md)
* [在 Teams 中集成 QR 或条形码扫描程序功能](qr-barcode-scanner-capability.md)
* [在 Teams 中集成位置功能](location-capability.md)
