---
title: 为 Microsoft "团队" 选项卡请求设备权限
description: 如何更新您的应用程序清单，以便请求对通常需要用户同意的本机功能的访问权限
keywords: 团队选项卡开发
ms.openlocfilehash: f0e19c0ed716147c097137c4ef0bf3454783b2eb
ms.sourcegitcommit: c4a7bc638e848a702cce92798cba84917fcecc35
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/24/2020
ms.locfileid: "42928515"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a>为 Microsoft "团队" 选项卡请求设备权限

您可能希望使用需要访问本机设备功能的功能来丰富您的选项卡，如下所示：

* 拍照
* 着
* 位置
* 通知

![设备权限设置屏幕](~/assets/images/tabs/device-permissions.png)

> [!IMPORTANT]
> 移动客户端上的选项卡目前不支持本机设备功能，但即将推出完全支持。 若要为此更改做准备，应按照移动选项卡[上的选项卡指南中](~/tabs/design/tabs-mobile.md)的步骤创建选项卡。 个人应用（静态选项卡）目前可在[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中使用。
>
> 释放对选项卡的完全支持时：
>
> * 所有选项卡将始终在移动设备上可用
> * 您`contentUrl` **将在移动团队客户端中加载**。
> * 对于频道/组选项卡，用户仍可以通过您`websiteUrl`在单独的浏览器中打开您的`contentUrl`选项卡，但您将首先加载。  

## <a name="device-permissions"></a>设备权限

通过访问用户的设备权限，您可以生成更丰富的体验，例如：

* 记录和共享简短视频
* 录制简短的音频备忘录并在以后保存它们
* 使用用户位置信息显示相关信息

[！重要说明] 虽然在大多数新式 web 浏览器中访问这些功能是标准的，但你需要让团队知道你要使用哪些功能来更新你的应用程序清单。 这样，您就可以像在浏览器中一样请求权限，而在团队桌面客户端上运行应用程序。

## <a name="properties"></a>属性

`manifest.json`通过添加`devicePermissions`和指定要在应用程序中使用的五个属性中的哪一个来更新应用程序：

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

每个属性都允许你提示用户提出同意

| 属性      | 说明   |
| --- | --- |
| media         | 使用摄像头、麦克风和扬声器的权限 |
| 地理位置   | 返回用户位置的权限      |
| 通知 | 发送用户通知的权限      |
| midi          | 从数字音乐仪器发送和接收 midi 信息的权限   |
| openExternal  | 在外部应用程序中打开链接的权限  |

## <a name="checking-permissions-from-your-tab"></a>从选项卡检查权限

添加`devicePermissions`到应用程序清单后，可以使用 HTML5 "权限" API 检查权限，而不会导致出现提示。

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

为了显示提示以获取访问设备权限的许可，您需要使用相应的 HTML5 API。 例如，为了提示用户访问其相机，您需要呼叫`getUserMedia`

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

调用时，地理位置将显示权限提示`getCurrentPosition`

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

调用时，通知将提示用户`requestPermission`

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![选项卡设备权限提示](~/assets/images/tabs/device-permissions-prompt.png)

## <a name="permission-behavior-across-login-sessions"></a>跨登录会话的权限行为

本机设备权限是按每个登录会话存储的。 这意味着，如果您登录到团队的另一个实例（例如，在另一台计算机上），您的设备权限将不可用。 相反，你将需要重新同意新登录 sessoin 的设备权限。 这也意味着，如果您注销团队（或团队内部的交换机租户），则将删除该先前登录会话的设备权限。 在开发本机设备权限时，请记住这一点：您同意的本机功能仅适用于您的_当前_登录 sessoin。