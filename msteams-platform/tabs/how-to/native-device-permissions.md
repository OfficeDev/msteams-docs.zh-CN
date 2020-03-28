---
title: 为 Microsoft "团队" 选项卡请求设备权限
description: 如何更新您的应用程序清单，以便请求对通常需要用户同意的本机功能的访问权限
keywords: 团队选项卡开发
ms.openlocfilehash: e9dc6c6f177e3a87e2846bcb836cc38601c9a50e
ms.sourcegitcommit: b13b38a104946c32cd5245a7af706070e534927d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2020
ms.locfileid: "43034034"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="096e8-104">为 Microsoft "团队" 选项卡请求设备权限</span><span class="sxs-lookup"><span data-stu-id="096e8-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="096e8-105">您可能希望使用需要访问本机设备功能的功能来丰富您的选项卡，如下所示：</span><span class="sxs-lookup"><span data-stu-id="096e8-105">You might want to enrich your tab with features that require access native device functionality like:</span></span>

* <span data-ttu-id="096e8-106">拍照</span><span class="sxs-lookup"><span data-stu-id="096e8-106">Camera</span></span>
* <span data-ttu-id="096e8-107">着</span><span class="sxs-lookup"><span data-stu-id="096e8-107">Microphone</span></span>
* <span data-ttu-id="096e8-108">位置</span><span class="sxs-lookup"><span data-stu-id="096e8-108">Location</span></span>
* <span data-ttu-id="096e8-109">通知</span><span class="sxs-lookup"><span data-stu-id="096e8-109">Notifications</span></span>

![设备权限设置屏幕](~/assets/images/tabs/device-permissions.png)

> [!IMPORTANT]
>
> <span data-ttu-id="096e8-111">移动客户端上的选项卡目前不支持本机设备功能。</span><span class="sxs-lookup"><span data-stu-id="096e8-111">Native device functionality is currently not supported for tabs on mobile clients.</span></span>
>
> <span data-ttu-id="096e8-112">目前，所有桌面客户端都不完全支持地理位置 API。</span><span class="sxs-lookup"><span data-stu-id="096e8-112">The geolocation API is currently not fully supported on all desktop clients.</span></span>

## <a name="device-permissions"></a><span data-ttu-id="096e8-113">设备权限</span><span class="sxs-lookup"><span data-stu-id="096e8-113">Device permissions</span></span>

<span data-ttu-id="096e8-114">通过访问用户的设备权限，您可以生成更丰富的体验，例如：</span><span class="sxs-lookup"><span data-stu-id="096e8-114">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="096e8-115">记录和共享简短视频</span><span class="sxs-lookup"><span data-stu-id="096e8-115">Record and share short videos</span></span>
* <span data-ttu-id="096e8-116">录制简短的音频备忘录并在以后保存它们</span><span class="sxs-lookup"><span data-stu-id="096e8-116">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="096e8-117">使用用户位置信息显示相关信息</span><span class="sxs-lookup"><span data-stu-id="096e8-117">Use user location information to display relevant information</span></span>

<span data-ttu-id="096e8-118">[！重要说明] 虽然在大多数新式 web 浏览器中访问这些功能是标准的，但你需要让团队知道你要使用哪些功能来更新你的应用程序清单。</span><span class="sxs-lookup"><span data-stu-id="096e8-118">While access to these features are standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="096e8-119">这样，您就可以像在浏览器中一样请求权限，而在团队桌面客户端上运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="096e8-119">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="properties"></a><span data-ttu-id="096e8-120">属性</span><span class="sxs-lookup"><span data-stu-id="096e8-120">Properties</span></span>

<span data-ttu-id="096e8-121">`manifest.json`通过添加`devicePermissions`和指定要在应用程序中使用的五个属性中的哪一个来更新应用程序：</span><span class="sxs-lookup"><span data-stu-id="096e8-121">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="096e8-122">每个属性都允许你提示用户提出同意</span><span class="sxs-lookup"><span data-stu-id="096e8-122">Each property will allow you to prompt the user to ask for their consent</span></span>

| <span data-ttu-id="096e8-123">属性</span><span class="sxs-lookup"><span data-stu-id="096e8-123">Property</span></span>      | <span data-ttu-id="096e8-124">说明</span><span class="sxs-lookup"><span data-stu-id="096e8-124">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="096e8-125">media</span><span class="sxs-lookup"><span data-stu-id="096e8-125">media</span></span>         | <span data-ttu-id="096e8-126">使用摄像头、麦克风和扬声器的权限</span><span class="sxs-lookup"><span data-stu-id="096e8-126">permission to use the camera, microphone and speakers</span></span> |
| <span data-ttu-id="096e8-127">地理位置</span><span class="sxs-lookup"><span data-stu-id="096e8-127">geolocation</span></span>   | <span data-ttu-id="096e8-128">返回用户位置的权限</span><span class="sxs-lookup"><span data-stu-id="096e8-128">permission to return the user's location</span></span>      |
| <span data-ttu-id="096e8-129">通知</span><span class="sxs-lookup"><span data-stu-id="096e8-129">notifications</span></span> | <span data-ttu-id="096e8-130">发送用户通知的权限</span><span class="sxs-lookup"><span data-stu-id="096e8-130">permission to send the user notifications</span></span>      |
| <span data-ttu-id="096e8-131">midi</span><span class="sxs-lookup"><span data-stu-id="096e8-131">midi</span></span>          | <span data-ttu-id="096e8-132">从数字音乐仪器发送和接收 midi 信息的权限</span><span class="sxs-lookup"><span data-stu-id="096e8-132">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="096e8-133">openExternal</span><span class="sxs-lookup"><span data-stu-id="096e8-133">openExternal</span></span>  | <span data-ttu-id="096e8-134">在外部应用程序中打开链接的权限</span><span class="sxs-lookup"><span data-stu-id="096e8-134">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="096e8-135">从选项卡检查权限</span><span class="sxs-lookup"><span data-stu-id="096e8-135">Checking permissions from your tab</span></span>

<span data-ttu-id="096e8-136">添加`devicePermissions`到应用程序清单后，可以使用 HTML5 "权限" API 检查权限，而不会导致出现提示。</span><span class="sxs-lookup"><span data-stu-id="096e8-136">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="096e8-137">提示用户</span><span class="sxs-lookup"><span data-stu-id="096e8-137">Prompting the user</span></span>

<span data-ttu-id="096e8-138">为了显示提示以获取访问设备权限的许可，您需要使用相应的 HTML5 API。</span><span class="sxs-lookup"><span data-stu-id="096e8-138">In order to show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 API.</span></span> <span data-ttu-id="096e8-139">例如，为了提示用户访问其相机，您需要呼叫`getUserMedia`</span><span class="sxs-lookup"><span data-stu-id="096e8-139">For example, in order to prompt the user to access their camera you need to call `getUserMedia`</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="096e8-140">调用时，地理位置将显示权限提示`getCurrentPosition`</span><span class="sxs-lookup"><span data-stu-id="096e8-140">Geolocation will  show a permission prompt when you call `getCurrentPosition`</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="096e8-141">调用时，通知将提示用户`requestPermission`</span><span class="sxs-lookup"><span data-stu-id="096e8-141">Notifications will prompt the user when you call `requestPermission`</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![选项卡设备权限提示](~/assets/images/tabs/device-permissions-prompt.png)

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="096e8-143">跨登录会话的权限行为</span><span class="sxs-lookup"><span data-stu-id="096e8-143">Permission behavior across login sessions</span></span>

<span data-ttu-id="096e8-144">本机设备权限是按每个登录会话存储的。</span><span class="sxs-lookup"><span data-stu-id="096e8-144">Native device permissions are stored per login session.</span></span> <span data-ttu-id="096e8-145">这意味着，如果您登录到团队的另一个实例（例如，在另一台计算机上），您的设备权限将不可用。</span><span class="sxs-lookup"><span data-stu-id="096e8-145">This means that if you log into another instance of Teams (ex: on another computer), your device permissions from your previous sessions will not be available.</span></span> <span data-ttu-id="096e8-146">相反，你将需要重新同意新登录会话的设备权限。</span><span class="sxs-lookup"><span data-stu-id="096e8-146">Instead, you will need to re-consent to device permissions for the new login session.</span></span> <span data-ttu-id="096e8-147">这也意味着，如果您注销团队（或团队内部的交换机租户），则将删除该先前登录会话的设备权限。</span><span class="sxs-lookup"><span data-stu-id="096e8-147">This also means, if you log out of Teams (or switch tenants inside of Teams), your device permissions will be deleted for that previous login session.</span></span> <span data-ttu-id="096e8-148">在开发本机设备权限时，请记住这一点：您同意的本机功能仅适用于您的_当前_登录会话。</span><span class="sxs-lookup"><span data-stu-id="096e8-148">Please keep this in mind when developing native device permissions: the native capabilities you consent to are only for your _current_ login session.</span></span>
