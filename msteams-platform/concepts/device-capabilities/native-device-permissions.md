---
title: 请求 Microsoft Teams 选项卡的设备权限
description: 如何更新应用清单以请求访问通常需要用户同意的本机功能
keywords: Teams 选项卡开发
ms.openlocfilehash: b021ae4ae8b50ddd1f3603f696922c129eb25f10
ms.sourcegitcommit: 84f408aa2854aa7a5cefaa66ce9a373b19e0864a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2021
ms.locfileid: "49886742"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a>请求 Microsoft Teams 选项卡的设备权限

你可能想要使用需要访问本机设备功能的功能来丰富选项卡，例如：

> [!div class="checklist"]
>
> * 相机
> * 麦克风
> * 位置
> * 通知

> [!NOTE]
> 若要在 Microsoft Teams 移动应用中集成相机和图像功能，请参阅 [Teams 中的相机和图像功能。](../../concepts/device-capabilities/mobile-camera-image-permissions.md)

> [!IMPORTANT]
>
> * 目前，Teams 移动客户端仅支持访问 、和通过本机设备功能，并且可用于所有应用构造（ `camera` `gallery` `mic` `location` 包括选项卡）。 </br>
> * 支持 `camera` ， `gallery` 并且 `mic` 通过 [**selectMedia API 启用**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)。 对于单个图像捕获，可以使用 [**captureImage API。**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true)
> * 通过 `location` [**getLocation API 启用对的支持**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)。 建议使用此 API，因为地理位置 [**API**](../../resources/schema/manifest-schema.md#devicepermissions) 当前并非在所有桌面客户端上受到完全支持。

## <a name="device-permissions"></a>设备权限

通过访问用户的设备权限，你可以构建更丰富的体验，例如：

* 录制和共享简短视频
* 录制简短的音频备注并将其保存供以后使用
* 使用用户位置信息显示相关信息

虽然在大多数新式 Web 浏览器中访问这些功能是标准功能，但你需要通过更新应用清单让 Teams 知道要使用哪些功能。 这将允许你请求权限，与在浏览器中请求权限的方式相同，同时你的应用在 Teams 桌面客户端上运行。

## <a name="manage-permissions"></a>管理权限

# <a name="desktop"></a>[桌面](#tab/desktop)

1. 打开 Teams。
1. 在窗口的右上角，选择配置文件图标。
1. 从  ->  **下拉菜单中选择**"设置权限"。
1. 选择所需的设置。

![设备权限桌面设置屏幕](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[移动](#tab/mobile)

1. 打开 Teams。
1. 转到 **"设置**  ->  **应用权限"。**
1. 选择你需要选择其设置的应用。
1. 选择所需的设置。

![设备权限移动设置屏幕](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="properties"></a>属性

通过添加并指定你要在应用程序中使用的五个属性中的哪一个来更新 `manifest.json` `devicePermissions` 应用：

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```
> [!Note]
>
> 媒体还用于移动版上的相机权限。

每个属性都允许您提示用户请求其同意：

| 属性      | 说明   |
| --- | --- |
| media         | 使用相机、麦克风、扬声器和访问媒体库的权限 |
| geolocation   | 返回用户位置的权限      |
| 通知 | 发送用户通知的权限      |
| midi          | 从数字音乐设备发送和接收中间信息的权限   |
| openExternal  | 在外部应用程序中打开链接的权限  |

## <a name="checking-permissions-from-your-tab"></a>检查选项卡中的权限

添加到应用清单后，即可使用 `devicePermissions` HTML5"权限"API 检查权限，而不会引发提示。

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

## <a name="prompting-the-user"></a>提示用户

若要显示请求同意访问设备权限的提示，你需要利用相应的 HTML5 或 Teams API。 

例如，要提示用户访问其位置，你需要调用 `getCurrentPosition` ：

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

若要在桌面或 Web 上使用相机，Teams 将在你调用时显示权限提示 `getUserMedia` ：

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

若要在移动设备上捕获图像，Teams 移动版将在你调用时请求权限 `captureImage()` ：

```Javascript
microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
  /* ... */
});
```

调用以下消息时，通知将提示用户 `requestPermission` ：

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

若要使用相机或访问照片库，Teams 移动将在你调用时请求权限 `selectMedia()` ：

```JavaScript
microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

若要使用麦克风，Teams 移动将在你调用时请求权限 `selectMedia()` ：

```JavaScript 
microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

若要提示用户在地图上共享位置，Teams 移动将在你调用时请求权限 `getLocation()` ：

```JavaScript 
microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
  /* ... *
/});
```

# <a name="desktop"></a>[桌面](#tab/desktop)

![选项卡桌面设备权限提示](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[移动](#tab/mobile)

![选项卡移动设备权限提示](../../assets/images/tabs/MobileLocationPermission.png)


## <a name="permission-behavior-across-login-sessions"></a>跨登录会话的权限行为

将存储每个登录会话的本机设备权限。 这意味着，如果你登录到 Teams (实例，例如，在另一) ，之前会话中的设备权限将不可用。 相反，你需要重新同意新登录会话的设备权限。 它还意味着，如果你注销 Teams (或在 Teams) 中切换租户，你的设备权限将删除该上一登录会话。 开发本机设备权限时请记住这一点：你同意的本机功能仅适用于你的当前 _登录_ 会话。
