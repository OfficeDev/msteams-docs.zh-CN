---
title: 为 Microsoft "团队" 选项卡请求设备权限
description: 如何更新您的应用程序清单，以便请求对通常需要用户同意的本机功能的访问权限
keywords: 团队选项卡开发
ms.openlocfilehash: d6c66525ab0e81f0632df5e2c323926279e38a8e
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576868"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a>为 Microsoft "团队" 选项卡请求设备权限

您可能希望使用需要访问本机设备功能的功能来丰富您的选项卡，如下所示：

> [!div class="checklist"]
>
> * 拍照
> * 着
> * 位置
> * 通知

> [!IMPORTANT]
>
> * 目前，工作组移动客户端仅支持 `camera` 和 `location`  通过本机设备功能，并可在包括选项卡在内的所有应用程序结构中使用。 </br>
> * 对 `camera` 图像捕获的支持由 [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true)启用。
> * 目前，所有桌面客户端都不完全支持 [**地理位置 API**](../../resources/schema/manifest-schema.md#devicepermissions) 。

## <a name="device-permissions"></a>设备权限

通过访问用户的设备权限，您可以生成更丰富的体验，例如：

* 记录和共享简短视频
* 录制简短的音频备忘录并在以后保存它们
* 使用用户位置信息显示相关信息

[！重要说明] 虽然在大多数新式 web 浏览器中访问这些功能是标准的，但你需要让团队知道你要使用哪些功能来更新你的应用程序清单。 这样，您就可以像在浏览器中一样请求权限，而在团队桌面客户端上运行应用程序。

## <a name="manage-permissions"></a>管理权限

# <a name="desktop"></a>[桌面](#tab/desktop)

1. 打开团队。
1. 在窗口的右上角，选择您的配置文件图标。
1. 从下拉菜单中选择 "**设置**  ->  **权限**"。
1. 选择所需的设置。

![设备权限桌面设置屏幕](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[移动](#tab/mobile)

1. 打开团队。
1. 在屏幕左上角，选择 "&#9776;" 菜单图标。
1. 选择 "**设置**  ->  **设备**"。
1. 选择所需的设置。

![设备权限移动设置屏幕](../../assets/images/tabs/mobile-device-permissions-screen.png)

---

## <a name="properties"></a>属性

`manifest.json`通过添加 `devicePermissions` 和指定要在应用程序中使用的五个属性中的哪一个来更新应用程序：

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
> 媒体也可用于移动设备中的相机权限。

每个属性都允许你提示用户提出同意

| 属性      | 说明   |
| --- | --- |
| media         | 使用摄像头、麦克风和扬声器的权限 |
| 地理位置   | 返回用户位置的权限      |
| 通知 | 发送用户通知的权限      |
| midi          | 从数字音乐仪器发送和接收 midi 信息的权限   |
| openExternal  | 在外部应用程序中打开链接的权限  |

## <a name="checking-permissions-from-your-tab"></a>从选项卡检查权限

添加 `devicePermissions` 到应用程序清单后，可以使用 HTML5 "权限" API 检查权限，而不会导致出现提示。

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

若要显示提示以获取访问设备权限的许可，您需要利用相应的 HTML5 或团队 API。 例如，为了提示用户访问其相机，您需要呼叫 `getCurrentPosition`

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

若要在桌面或 web 上使用摄像头，团队会在您调用 getUserMedia 时显示权限提示。

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

若要在移动时捕获图像，团队移动将在调用 captureImage 时请求权限 ( # A1

```Typescript
function captureImage(callback: (error: SdkError, files: File[]) => void)
```

调用时，通知将提示用户 `requestPermission`

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![选项卡设备权限提示](~/assets/images/tabs/device-permissions-prompt.png)

## <a name="permission-behavior-across-login-sessions"></a>跨登录会话的权限行为

本机设备权限是按每个登录会话存储的。 这意味着，如果您登录到另一个团队实例 (ex：在另一台计算机) 上，您的设备权限将不可用。 相反，你将需要重新同意新登录会话的设备权限。 这也意味着，如果注销团队 (或在团队内部切换租户) ，将删除该以前的登录会话的设备权限。 在开发本机设备权限时，请记住这一点：您同意的本机功能仅适用于您的 _当前_ 登录会话。
