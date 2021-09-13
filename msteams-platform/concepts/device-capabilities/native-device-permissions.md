---
title: 请求应用的设备Microsoft Teams权限
keywords: teams 应用功能权限
description: 如何更新应用清单，以请求访问通常需要用户同意的本机功能
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 33a0fc390dc2123ccb77901acb7967b1b9732e77
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155835"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a>请求应用的设备Microsoft Teams权限

可以使用本机设备Teams（如相机、麦克风和位置）丰富你的应用。 本文档指导你了解如何请求用户同意和访问本机设备权限。

> [!NOTE]
> * 若要将媒体功能集成到Microsoft Teams移动应用中，请参阅[集成媒体功能](mobile-camera-image-permissions.md)。
> * 若要将 QR 或条形码扫描仪功能集成到 Microsoft Teams 移动应用中，请参阅在应用中集成[QR 或条形码扫描仪Teams。](qr-barcode-scanner-capability.md)
> * 若要在移动应用中集成位置Microsoft Teams，请参阅[集成位置功能](location-capability.md)。

## <a name="native-device-permissions"></a>本机设备权限

必须请求设备权限才能访问本机设备功能。 设备权限对于所有应用构造（如选项卡、任务模块或消息传递扩展）的运行方式类似。 用户必须转到"权限"页，Teams设置才能管理设备权限。
通过访问设备功能，你可以构建更丰富的体验，Teams平台，例如：

* 捕获和查看图像。
* 扫描 QR 或条形码。
* 录制和共享简短视频。
* 录制音频备注并保存供以后使用。
* 使用用户的位置信息显示相关信息。

> [!NOTE]
> 目前Teams不支持多窗口应用、选项卡和会议侧面板的设备权限。

## <a name="access-device-permissions"></a>访问设备权限

JavaScript [Microsoft Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)提供了您的 Teams 移动应用访问用户设备权限和构建更丰富的体验所需的工具。 [](#manage-permissions)

虽然新式 Web 浏览器中对这些功能的访问是标准操作，但你必须Teams更新应用清单来通知用户有关使用的功能的信息。 此更新允许你在桌面客户端上运行应用时Teams权限。

> [!NOTE]
> 目前Microsoft Teams媒体功能和 QR 条形码扫描仪功能的支持仅适用于移动客户端。

## <a name="manage-permissions"></a>管理权限

用户可以通过选择"允许"或"拒绝Teams **设置来管理设备** 权限。 

# <a name="mobile"></a>[移动设备](#tab/mobile)

1. 打开Teams。
1. 转到 **设置**  >  **应用权限"。**
1. 选择要选择其设置的应用。
1. 选择所需的设置。

    ![设备权限移动设置屏幕](../../assets/images/tabs/MobilePermissions.png)

# <a name="desktop"></a>[桌面设备](#tab/desktop)

1. 打开你的Teams应用。
1. 选择窗口右上角的配置文件图标。
1. Select **设置**  >  **Permissions** from the drop-down menu.
1. 选择所需的设置。

   ![设备权限桌面设置屏幕](~/assets/images/tabs/device-permissions.png)

---

## <a name="specify-permissions"></a>指定权限

通过添加并指定在应用程序中使用的以下五个属性中的哪一个来 `manifest.json` `devicePermissions` 更新应用：

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
| 地理位置   | 返回用户位置的权限。      |
| 通知 | 发送用户通知的权限。      |
| midi          | 从数字音乐 (MIDI) 和接收音乐音乐数字接口的权限。   |
| openExternal  | 在外部应用程序中打开链接的权限。  |

## <a name="check-permissions-from-your-app"></a>检查应用的权限

添加到 `devicePermissions` 应用程序清单后，使用 **HTML5** 权限 API 检查权限，而不出现提示：

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

## <a name="use-teams-apis-to-get-device-permissions"></a>使用Teams API 获取设备权限

利用相应的 HTML5 或 Teams API，显示获取访问设备权限同意的提示。

> [!IMPORTANT]
> * 对 `camera` 、 `gallery` 和 `microphone` 的支持通过 [**selectMedia API 启用**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true)。 将 [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) 用于单个映像捕获。
> * 通过 `location` [**getLocation API**](/javascript/api/@microsoft/teams-js/microsoftteams.location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)启用对 的支持。 你必须将此功能用于位置，因为 HTML5 地理位置 API 当前在桌面客户端上Teams `getLocation API` 完全受支持。

例如：
 * 若要提示用户访问其位置，你必须调用 `getCurrentPosition()` ：

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * 若要提示用户访问桌面或 Web 上的相机，必须调用 `getUserMedia()` ：

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * 若要在移动设备上捕获图像，Teams调用 时请求获取权限 `captureImage()` ：

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * 当你调用 时，通知将提示用户 `requestPermission()` ：

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```

* 若要使用相机或访问照片库，Teams时，移动会询问权限 `selectMedia()` ：

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* 若要使用麦克风，Teams时，移动设备会询问权限 `selectMedia()` ：

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* 若要提示用户在地图界面上共享位置，Teams调用 时请求权限 `getLocation()` ：

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```

# <a name="mobile"></a>[移动设备](#tab/mobile)

   ![选项卡移动设备权限提示](../../assets/images/tabs/MobileLocationPermission.png)

# <a name="desktop"></a>[桌面设备](#tab/desktop)

   ![选项卡桌面设备权限提示](~/assets/images/tabs/device-permissions-prompt.png)

---

## <a name="permission-behavior-across-login-sessions"></a>跨登录会话的权限行为

将存储每个登录会话的设备权限。 这意味着，如果你登录到另一个 Teams 实例（例如，在另一台计算机中）时，之前会话中的设备权限将不可用。 因此，必须重新同意新会话的设备权限。 这也意味着，如果你注销 Teams 或切换租户Teams，你的设备权限将从以前的登录会话中删除。  

> [!NOTE]
> 当你同意本机设备权限时，它仅对当前的登录 _会话_ 有效。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **Node.js** |
|---------------|--------------|--------|
|设备权限 | 使用Microsoft Teams选项卡示例应用演示设备权限 |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [集成媒体中的媒体Teams](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [将 QR 或条形码扫描仪功能集成到 Teams](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [在 Teams 中集成位置Teams](location-capability.md)
