---
title: 请求 Microsoft Teams 选项卡的设备权限
description: 如何更新应用清单以请求访问通常需要用户同意的本机功能
keywords: teams 选项卡开发
ms.openlocfilehash: 6be183d2610616f3bd3bdf32554976322193c132
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731977"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="1d120-104">请求 Microsoft Teams 选项卡的设备权限</span><span class="sxs-lookup"><span data-stu-id="1d120-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="1d120-105">你可能想要使用需要访问本机设备功能的功能来丰富选项卡，例如：</span><span class="sxs-lookup"><span data-stu-id="1d120-105">You might want to enrich your tab with features that require access to native device functionality like:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="1d120-106">相机</span><span class="sxs-lookup"><span data-stu-id="1d120-106">Camera</span></span>
> * <span data-ttu-id="1d120-107">麦克风</span><span class="sxs-lookup"><span data-stu-id="1d120-107">Microphone</span></span>
> * <span data-ttu-id="1d120-108">位置</span><span class="sxs-lookup"><span data-stu-id="1d120-108">Location</span></span>
> * <span data-ttu-id="1d120-109">通知</span><span class="sxs-lookup"><span data-stu-id="1d120-109">Notifications</span></span>

[!Note] <span data-ttu-id="1d120-110">若要在 Microsoft Teams 移动应用中集成相机和图像功能，请参阅 [Teams 中的相机和图像功能。](../../concepts/device-capabilities/mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="1d120-110">To integrate camera and image capabilities within your Microsoft Teams mobile app, refer [Camera and image capabilities in Teams.](../../concepts/device-capabilities/mobile-camera-image-permissions.md)</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="1d120-111">目前，Teams 移动客户端仅支持访问 、和通过本机设备功能，并且可用于所有应用构造（ `camera` `gallery` `mic` `location` 包括选项卡）。</span><span class="sxs-lookup"><span data-stu-id="1d120-111">At present, Teams mobile client only supports access to `camera`, `gallery`, `mic`, and `location` through native device capabilities and is available on all app constructs including tabs.</span></span> </br>
> * <span data-ttu-id="1d120-112">支持 `camera` ， `gallery` 并且 `mic` 通过 [**selectMedia API 启用**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="1d120-112">Support for `camera`, `gallery`, and `mic` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="1d120-113">对于单个图像捕获，可以使用 [**captureImage API。**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="1d120-113">For single image capture you may use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true).</span></span>
> * <span data-ttu-id="1d120-114">通过 `location` [**getLocation API 启用对的支持**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="1d120-114">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="1d120-115">建议使用此 API，因为当前并非所有桌面[](../../resources/schema/manifest-schema.md#devicepermissions)客户端都完全支持地理位置 API。</span><span class="sxs-lookup"><span data-stu-id="1d120-115">It's recommended you use this API as [**geolocation API**](../../resources/schema/manifest-schema.md#devicepermissions) is currently not fully supported on all desktop clients.</span></span>

## <a name="device-permissions"></a><span data-ttu-id="1d120-116">设备权限</span><span class="sxs-lookup"><span data-stu-id="1d120-116">Device permissions</span></span>

<span data-ttu-id="1d120-117">通过访问用户的设备权限，你可以构建更丰富的体验，例如：</span><span class="sxs-lookup"><span data-stu-id="1d120-117">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="1d120-118">录制和共享简短视频</span><span class="sxs-lookup"><span data-stu-id="1d120-118">Record and share short videos</span></span>
* <span data-ttu-id="1d120-119">录制简短的音频备注并将其保存供以后使用</span><span class="sxs-lookup"><span data-stu-id="1d120-119">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="1d120-120">使用用户位置信息显示相关信息</span><span class="sxs-lookup"><span data-stu-id="1d120-120">Use user location information to display relevant information</span></span>

<span data-ttu-id="1d120-121">虽然在大多数新式 Web 浏览器中访问这些功能是标准功能，但你需要通过更新应用清单让 Teams 知道要使用哪些功能。</span><span class="sxs-lookup"><span data-stu-id="1d120-121">While access to these features is standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="1d120-122">这将允许你请求权限，与在浏览器中请求权限的方式相同，同时你的应用在 Teams 桌面客户端上运行。</span><span class="sxs-lookup"><span data-stu-id="1d120-122">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="1d120-123">管理权限</span><span class="sxs-lookup"><span data-stu-id="1d120-123">Manage permissions</span></span>

# <a name="desktop"></a>[<span data-ttu-id="1d120-124">桌面</span><span class="sxs-lookup"><span data-stu-id="1d120-124">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="1d120-125">打开 Teams。</span><span class="sxs-lookup"><span data-stu-id="1d120-125">Open Teams.</span></span>
1. <span data-ttu-id="1d120-126">在窗口的右上角，选择配置文件图标。</span><span class="sxs-lookup"><span data-stu-id="1d120-126">In the upper right corner of the window, select your profile icon.</span></span>
1. <span data-ttu-id="1d120-127">从  ->  **下拉菜单中选择**"设置权限"。</span><span class="sxs-lookup"><span data-stu-id="1d120-127">Select **Settings** -> **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="1d120-128">选择所需的设置。</span><span class="sxs-lookup"><span data-stu-id="1d120-128">Choose your desired settings.</span></span>

![设备权限桌面设置屏幕](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="1d120-130">移动</span><span class="sxs-lookup"><span data-stu-id="1d120-130">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="1d120-131">打开 Teams。</span><span class="sxs-lookup"><span data-stu-id="1d120-131">Open Teams.</span></span>
1. <span data-ttu-id="1d120-132">转到 **"设置**  ->  **应用权限"。**</span><span class="sxs-lookup"><span data-stu-id="1d120-132">Go to **Settings** -> **App Permissions**.</span></span>
1. <span data-ttu-id="1d120-133">选择你需要选择其设置的应用。</span><span class="sxs-lookup"><span data-stu-id="1d120-133">Select the app you need to choose settings for.</span></span>
1. <span data-ttu-id="1d120-134">选择所需的设置。</span><span class="sxs-lookup"><span data-stu-id="1d120-134">Choose your desired settings.</span></span>

![设备权限移动设置屏幕](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="properties"></a><span data-ttu-id="1d120-136">属性</span><span class="sxs-lookup"><span data-stu-id="1d120-136">Properties</span></span>

<span data-ttu-id="1d120-137">通过添加并指定你要在应用程序中使用的五个属性中的哪一个来更新 `manifest.json` `devicePermissions` 应用：</span><span class="sxs-lookup"><span data-stu-id="1d120-137">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

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
> <span data-ttu-id="1d120-138">媒体还用于移动版上的相机权限。</span><span class="sxs-lookup"><span data-stu-id="1d120-138">Media is also used for camera permissions on mobile.</span></span>

<span data-ttu-id="1d120-139">每个属性都允许您提示用户请求其同意：</span><span class="sxs-lookup"><span data-stu-id="1d120-139">Each property will allow you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="1d120-140">属性</span><span class="sxs-lookup"><span data-stu-id="1d120-140">Property</span></span>      | <span data-ttu-id="1d120-141">说明</span><span class="sxs-lookup"><span data-stu-id="1d120-141">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="1d120-142">media</span><span class="sxs-lookup"><span data-stu-id="1d120-142">media</span></span>         | <span data-ttu-id="1d120-143">使用相机、麦克风、扬声器和访问媒体库的权限</span><span class="sxs-lookup"><span data-stu-id="1d120-143">permission to use the camera, microphone, speakers, and access media gallery</span></span> |
| <span data-ttu-id="1d120-144">geolocation</span><span class="sxs-lookup"><span data-stu-id="1d120-144">geolocation</span></span>   | <span data-ttu-id="1d120-145">返回用户位置的权限</span><span class="sxs-lookup"><span data-stu-id="1d120-145">permission to return the user's location</span></span>      |
| <span data-ttu-id="1d120-146">通知</span><span class="sxs-lookup"><span data-stu-id="1d120-146">notifications</span></span> | <span data-ttu-id="1d120-147">发送用户通知的权限</span><span class="sxs-lookup"><span data-stu-id="1d120-147">permission to send the user notifications</span></span>      |
| <span data-ttu-id="1d120-148">midi</span><span class="sxs-lookup"><span data-stu-id="1d120-148">midi</span></span>          | <span data-ttu-id="1d120-149">从数字音乐设备发送和接收中间信息的权限</span><span class="sxs-lookup"><span data-stu-id="1d120-149">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="1d120-150">openExternal</span><span class="sxs-lookup"><span data-stu-id="1d120-150">openExternal</span></span>  | <span data-ttu-id="1d120-151">在外部应用程序中打开链接的权限</span><span class="sxs-lookup"><span data-stu-id="1d120-151">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="1d120-152">检查选项卡中的权限</span><span class="sxs-lookup"><span data-stu-id="1d120-152">Checking permissions from your tab</span></span>

<span data-ttu-id="1d120-153">添加到应用清单后，即可使用 `devicePermissions` HTML5"权限"API 检查权限，而不会引发提示。</span><span class="sxs-lookup"><span data-stu-id="1d120-153">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="1d120-154">提示用户</span><span class="sxs-lookup"><span data-stu-id="1d120-154">Prompting the user</span></span>

<span data-ttu-id="1d120-155">若要显示请求同意访问设备权限的提示，你需要利用相应的 HTML5 或 Teams API。</span><span class="sxs-lookup"><span data-stu-id="1d120-155">To show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 or Teams API.</span></span> 

<span data-ttu-id="1d120-156">例如，要提示用户访问其位置，你需要调用 `getCurrentPosition` ：</span><span class="sxs-lookup"><span data-stu-id="1d120-156">For example, to prompt the user to access their location you need to call `getCurrentPosition`:</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="1d120-157">若要在桌面或 Web 上使用相机，Teams 将在你调用时显示权限提示 `getUserMedia` ：</span><span class="sxs-lookup"><span data-stu-id="1d120-157">To use the camera on desktop or web, Teams will show a permission prompt when you call `getUserMedia`:</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="1d120-158">若要在移动设备上捕获图像，Teams 移动版将在你调用时请求权限 `captureImage()` ：</span><span class="sxs-lookup"><span data-stu-id="1d120-158">To capture the image on mobile, Teams mobile will ask for permission when you call `captureImage()`:</span></span>

```Javascript
microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
  /* ... */
});
```

<span data-ttu-id="1d120-159">调用以下消息时，通知将提示用户 `requestPermission` ：</span><span class="sxs-lookup"><span data-stu-id="1d120-159">Notifications will prompt the user when you call `requestPermission`:</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

<span data-ttu-id="1d120-160">若要使用相机或访问照片库，Teams 移动版将在你调用时请求权限 `selectMedia()` ：</span><span class="sxs-lookup"><span data-stu-id="1d120-160">To use camera or access photo gallery, Teams mobile will ask permission when you call `selectMedia()`:</span></span>

```JavaScript
microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

<span data-ttu-id="1d120-161">若要使用麦克风，Teams 移动将在你调用时请求权限 `selectMedia()` ：</span><span class="sxs-lookup"><span data-stu-id="1d120-161">To use mic, Teams mobile will ask permission when you call `selectMedia()`:</span></span>

```JavaScript 
microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
  /* ... */
});
```

<span data-ttu-id="1d120-162">若要提示用户在地图上共享位置，Teams 移动将在你调用时请求权限 `getLocation()` ：</span><span class="sxs-lookup"><span data-stu-id="1d120-162">To prompt user to share location on map interface, Teams mobile will ask permission when you call `getLocation()`:</span></span>

```JavaScript 
microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
  /* ... *
/});
```

# <a name="desktop"></a>[<span data-ttu-id="1d120-163">桌面</span><span class="sxs-lookup"><span data-stu-id="1d120-163">Desktop</span></span>](#tab/desktop)

![选项卡桌面设备权限提示](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="1d120-165">移动</span><span class="sxs-lookup"><span data-stu-id="1d120-165">Mobile</span></span>](#tab/mobile)

![选项卡移动设备权限提示](../../assets/images/tabs/MobileLocationPermission.png)


## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="1d120-167">跨登录会话的权限行为</span><span class="sxs-lookup"><span data-stu-id="1d120-167">Permission behavior across login sessions</span></span>

<span data-ttu-id="1d120-168">将存储每个登录会话的本机设备权限。</span><span class="sxs-lookup"><span data-stu-id="1d120-168">Native device permissions are stored for every login session.</span></span> <span data-ttu-id="1d120-169">这意味着，如果你登录到 Teams (实例，例如，在另一) ，之前会话中的设备权限将不可用。</span><span class="sxs-lookup"><span data-stu-id="1d120-169">It means that if you log into another instance of Teams (ex: on another computer), your device permissions from your previous sessions will not be available.</span></span> <span data-ttu-id="1d120-170">相反，你需要重新同意新登录会话的设备权限。</span><span class="sxs-lookup"><span data-stu-id="1d120-170">Instead, you will need to re-consent to device permissions for the new login session.</span></span> <span data-ttu-id="1d120-171">它还意味着，如果你注销 Teams (或在 Teams) 中切换租户，你的设备权限将删除该上一登录会话。</span><span class="sxs-lookup"><span data-stu-id="1d120-171">It also means, if you log out of Teams (or switch tenants inside of Teams), your device permissions will be deleted for that previous login session.</span></span> <span data-ttu-id="1d120-172">开发本机设备权限时请记住这一点：你同意的本机功能仅适用于你的当前 _登录_ 会话。</span><span class="sxs-lookup"><span data-stu-id="1d120-172">Please keep this in mind when developing native device permissions: the native capabilities you consent to are only for your _current_ login session.</span></span>
