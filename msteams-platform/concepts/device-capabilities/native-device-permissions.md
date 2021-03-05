---
title: 请求 Microsoft Teams 应用的设备权限
keywords: teams 应用功能权限
description: 如何更新应用清单以请求访问通常需要用户同意的本机功能
ms.topic: how-to
ms.openlocfilehash: e7c5f7ff477bc193924cdf11700c77ae620cd1c0
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449434"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>请求 Microsoft Teams 应用的设备权限

可以使用本机设备功能（如相机、麦克风和位置）丰富 Teams 应用。 本文档指导您如何请求用户同意和访问本机设备权限。

> [!NOTE]
> * 若要在 Microsoft Teams 移动应用中集成媒体功能，请参阅"[集成媒体功能"。](mobile-camera-image-permissions.md)
> * 若要在 Microsoft Teams 移动应用中集成 QR 或条形码扫描仪功能，请参阅在 Teams 中集成 [QR 或条形码扫描仪功能](qr-barcode-scanner-capability.md)
> * 若要在 Microsoft Teams 移动应用中集成位置功能，请参阅["集成位置功能"。](location-capability.md)

## <a name="native-device-permissions"></a>本机设备权限

必须请求设备权限才能访问本机设备功能。 设备权限在所有应用构造（如选项卡、任务模块或邮件扩展）中同样工作。 用户必须转到 Teams 设置中的权限页才能管理设备权限。
通过访问设备功能，可以在 Teams 平台上构建更丰富的体验，例如：
* 捕获和查看图像。
* 扫描 QR 或条形码。
* 录制和共享短视频。
* 录制音频备注并保存供以后使用。
* 使用用户的位置信息显示相关信息。

## <a name="access-device-permissions"></a>访问设备权限

[Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)提供了 Teams 移动应用访问用户设备权限和构建[](#manage-permissions)更丰富的体验所需的工具。

虽然新式 Web 浏览器中对这些功能的访问是标准访问，但你必须通过更新应用清单来通知 Teams 你使用的功能。 此更新允许你在应用在 Teams 桌面客户端上运行时请求权限。

> [!NOTE] 
> 目前，Microsoft Teams 对媒体功能和 QR 条形码扫描仪功能的支持仅适用于移动客户端。

## <a name="manage-permissions"></a>管理权限

用户可以通过在 Teams 设置中选择"允许或拒绝"权限来管理特定应用的设备权限。
 
# <a name="desktop"></a>[桌面](#tab/desktop)

1. 打开 Teams 应用。
1. 选择窗口右上角的配置文件图标。
1. 从  >  **下拉菜单中选择**"设置权限"。
1. 选择所需的设置。

   ![设备权限桌面设置屏幕](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[移动](#tab/mobile)

1. 打开 Teams。
1. 转到 **"设置**  >  **应用权限"。**
1. 选择要选择其设置的应用。
1. 选择所需的设置。

    ![设备权限移动设置屏幕](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a>指定权限

通过添加并指定在应用程序中使用的五个属性中的哪一个来 `manifest.json` `devicePermissions` 更新应用：

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

每个属性都允许您提示用户请求其同意：

| 属性      | 说明   |
| --- | --- |
| media         | 使用相机、麦克风、扬声器和访问媒体库的权限。 |
| geolocation   | 返回用户位置的权限。      |
| 通知 | 发送用户通知的权限。      |
| midi          | 从数字音乐设备发送和接收 MIDI (数字) 接收音乐音乐数字接口的权限。   |
| openExternal  | 在外部应用程序中打开链接的权限。  |

## <a name="check-permissions-from-your-app"></a>从应用检查权限

添加到 `devicePermissions` 应用清单后，使用 **HTML5** 权限 API 检查权限，而不出现提示：

``` Javascript
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

利用相应的 HTML5 或 Teams API，显示请求同意访问设备权限的提示。

> [!IMPORTANT]
> * 支持 `camera` ， `gallery` `microphone` 并且通过 [**selectMedia API 启用**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)。 将 [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) 用于单个图像捕获。
> * 支持 `location` 是通过 [**getLocation API 启用的**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)。 你必须对位置使用此功能，因为 HTML5 地理位置 API 当前在 Teams 桌面客户端上 `getLocation API` 不受完全支持。

例如：
 * 若要提示用户访问其位置，必须调用 `getCurrentPosition()` ：

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * 若要提示用户在桌面或 Web 上访问其相机，必须调用 `getUserMedia()` ：

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * 若要在移动设备上捕获图像，Teams 移动版在调用时需要获取权限 `captureImage()` ：

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * 调用以下消息时，通知将提示用户 `requestPermission()` ：

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* 若要使用相机或访问照片库，Teams 移动版在调用时会询问权限 `selectMedia()` ：

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* 若要使用麦克风，Teams 移动版在呼叫时请求权限 `selectMedia()` ：

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* 若要提示用户共享地图界面上的位置，Teams 移动版在调用时请求权限 `getLocation()` ：

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[桌面](#tab/desktop)

   ![选项卡桌面设备权限提示](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[移动](#tab/mobile)

   ![选项卡移动设备权限提示](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a>跨登录会话的权限行为

将存储每个登录会话的设备权限。 这意味着，如果你登录到另一个 Teams 实例（例如，在另一台计算机中）时，之前会话中的设备权限将不可用。 因此，必须重新同意新会话的设备权限。 它还意味着，如果你注销 Teams 或在 Teams 中切换租户，你的设备权限将从以前的登录会话中删除。  

> [!NOTE]
> 当你同意本机设备权限时，它仅对当前的登录 _会话_ 有效。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [在 Teams 中集成媒体功能](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [在 Teams 中集成 QR 或条形码扫描仪功能](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [在 Teams 中集成位置功能](location-capability.md)
