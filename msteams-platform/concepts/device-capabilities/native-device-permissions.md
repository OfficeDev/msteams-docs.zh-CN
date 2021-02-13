---
title: 请求 Microsoft Teams 应用的设备权限
keywords: teams 应用功能权限
description: 如何更新应用清单以请求访问通常需要用户同意的本机功能
ms.topic: how-to
ms.openlocfilehash: 0343754eacbb6088a3e44fa5df8ec90e3b10b076
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231608"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="57ddf-104">请求 Microsoft Teams 应用的设备权限</span><span class="sxs-lookup"><span data-stu-id="57ddf-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="57ddf-105">可以使用本机设备功能（如相机、麦克风和位置）丰富 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="57ddf-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="57ddf-106">本文档指导您如何请求用户同意和访问本机设备权限。</span><span class="sxs-lookup"><span data-stu-id="57ddf-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="57ddf-107">若要在 Microsoft Teams 移动应用中集成媒体功能，请参阅"[集成媒体功能"。](mobile-camera-image-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="57ddf-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="57ddf-108">本机设备权限</span><span class="sxs-lookup"><span data-stu-id="57ddf-108">Native device permissions</span></span>

<span data-ttu-id="57ddf-109">必须请求设备权限才能访问本机设备功能。</span><span class="sxs-lookup"><span data-stu-id="57ddf-109">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="57ddf-110">设备权限在所有应用构造（如选项卡、任务模块或消息扩展）中同样工作。</span><span class="sxs-lookup"><span data-stu-id="57ddf-110">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="57ddf-111">用户必须转到 Teams 设置中的权限页才能管理设备权限。</span><span class="sxs-lookup"><span data-stu-id="57ddf-111">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="57ddf-112">通过访问设备功能，可以在 Teams 平台上构建更丰富的体验，例如：</span><span class="sxs-lookup"><span data-stu-id="57ddf-112">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="57ddf-113">捕获和查看图像。</span><span class="sxs-lookup"><span data-stu-id="57ddf-113">Capture and view images.</span></span>
* <span data-ttu-id="57ddf-114">录制和共享短视频。</span><span class="sxs-lookup"><span data-stu-id="57ddf-114">Record and share short videos.</span></span>
* <span data-ttu-id="57ddf-115">录制音频备注并保存供以后使用。</span><span class="sxs-lookup"><span data-stu-id="57ddf-115">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="57ddf-116">使用用户的位置信息显示相关信息。</span><span class="sxs-lookup"><span data-stu-id="57ddf-116">Use the location information of the user to display relevant information.</span></span>

## <a name="access-device-permissions"></a><span data-ttu-id="57ddf-117">访问设备权限</span><span class="sxs-lookup"><span data-stu-id="57ddf-117">Access device permissions</span></span>

<span data-ttu-id="57ddf-118">[Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)提供了 Teams 移动应用访问用户设备权限和构建[](#manage-permissions)更丰富的体验所需的工具。</span><span class="sxs-lookup"><span data-stu-id="57ddf-118">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="57ddf-119">虽然新式 Web 浏览器中对这些功能的访问是标准访问，但你必须通过更新应用清单来通知 Teams 你使用的功能。</span><span class="sxs-lookup"><span data-stu-id="57ddf-119">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="57ddf-120">此更新允许你在应用在 Teams 桌面客户端上运行时请求权限。</span><span class="sxs-lookup"><span data-stu-id="57ddf-120">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="57ddf-121">目前，Microsoft Teams 对媒体功能的支持仅适用于移动客户端。</span><span class="sxs-lookup"><span data-stu-id="57ddf-121">Currently, Microsoft Teams support for media capabilities is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="57ddf-122">管理权限</span><span class="sxs-lookup"><span data-stu-id="57ddf-122">Manage permissions</span></span>

<span data-ttu-id="57ddf-123">用户可以通过在 Teams 设置中选择"允许或拒绝"权限来管理特定应用的设备权限。</span><span class="sxs-lookup"><span data-stu-id="57ddf-123">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="57ddf-124">桌面</span><span class="sxs-lookup"><span data-stu-id="57ddf-124">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="57ddf-125">打开 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="57ddf-125">Open your Teams app.</span></span>
1. <span data-ttu-id="57ddf-126">选择窗口右上角的配置文件图标。</span><span class="sxs-lookup"><span data-stu-id="57ddf-126">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="57ddf-127">从  >  **下拉菜单中选择**"设置权限"。</span><span class="sxs-lookup"><span data-stu-id="57ddf-127">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="57ddf-128">选择所需的设置。</span><span class="sxs-lookup"><span data-stu-id="57ddf-128">Select your desired settings.</span></span>

   ![设备权限桌面设置屏幕](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="57ddf-130">移动</span><span class="sxs-lookup"><span data-stu-id="57ddf-130">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="57ddf-131">打开 Teams。</span><span class="sxs-lookup"><span data-stu-id="57ddf-131">Open Teams.</span></span>
1. <span data-ttu-id="57ddf-132">转到 **"设置**  >  **应用权限"。**</span><span class="sxs-lookup"><span data-stu-id="57ddf-132">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="57ddf-133">选择要选择其设置的应用。</span><span class="sxs-lookup"><span data-stu-id="57ddf-133">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="57ddf-134">选择所需的设置。</span><span class="sxs-lookup"><span data-stu-id="57ddf-134">Select your desired settings.</span></span>

    ![设备权限移动设置屏幕](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="57ddf-136">指定权限</span><span class="sxs-lookup"><span data-stu-id="57ddf-136">Specify permissions</span></span>

<span data-ttu-id="57ddf-137">通过添加并指定在应用程序中使用的五个属性中的哪一个来 `manifest.json` `devicePermissions` 更新应用：</span><span class="sxs-lookup"><span data-stu-id="57ddf-137">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="57ddf-138">每个属性都允许您提示用户请求其同意：</span><span class="sxs-lookup"><span data-stu-id="57ddf-138">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="57ddf-139">属性</span><span class="sxs-lookup"><span data-stu-id="57ddf-139">Property</span></span>      | <span data-ttu-id="57ddf-140">说明</span><span class="sxs-lookup"><span data-stu-id="57ddf-140">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="57ddf-141">media</span><span class="sxs-lookup"><span data-stu-id="57ddf-141">media</span></span>         | <span data-ttu-id="57ddf-142">使用相机、麦克风、扬声器和访问媒体库的权限。</span><span class="sxs-lookup"><span data-stu-id="57ddf-142">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="57ddf-143">geolocation</span><span class="sxs-lookup"><span data-stu-id="57ddf-143">geolocation</span></span>   | <span data-ttu-id="57ddf-144">返回用户位置的权限。</span><span class="sxs-lookup"><span data-stu-id="57ddf-144">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="57ddf-145">通知</span><span class="sxs-lookup"><span data-stu-id="57ddf-145">notifications</span></span> | <span data-ttu-id="57ddf-146">发送用户通知的权限。</span><span class="sxs-lookup"><span data-stu-id="57ddf-146">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="57ddf-147">midi</span><span class="sxs-lookup"><span data-stu-id="57ddf-147">midi</span></span>          | <span data-ttu-id="57ddf-148">发送和接收来自数字音乐 (MIDI) 音乐界面数字接口的权限。</span><span class="sxs-lookup"><span data-stu-id="57ddf-148">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="57ddf-149">openExternal</span><span class="sxs-lookup"><span data-stu-id="57ddf-149">openExternal</span></span>  | <span data-ttu-id="57ddf-150">在外部应用程序中打开链接的权限。</span><span class="sxs-lookup"><span data-stu-id="57ddf-150">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="57ddf-151">从应用检查权限</span><span class="sxs-lookup"><span data-stu-id="57ddf-151">Check permissions from your app</span></span>

<span data-ttu-id="57ddf-152">添加到 `devicePermissions` 应用清单后，使用 **HTML5 权限 API** 检查权限，而不出现提示：</span><span class="sxs-lookup"><span data-stu-id="57ddf-152">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

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

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="57ddf-153">使用 Teams API 获取设备权限</span><span class="sxs-lookup"><span data-stu-id="57ddf-153">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="57ddf-154">利用相应的 HTML5 或 Teams API，显示请求同意访问设备权限的提示。</span><span class="sxs-lookup"><span data-stu-id="57ddf-154">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="57ddf-155">支持 `camera` ， `gallery` `microphone` 并且通过 [**selectMedia API 启用**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="57ddf-155">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="57ddf-156">将 [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) 用于单个图像捕获。</span><span class="sxs-lookup"><span data-stu-id="57ddf-156">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="57ddf-157">支持 `location` 是通过 [**getLocation API 启用的**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="57ddf-157">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="57ddf-158">你必须对位置使用此功能，因为 HTML5 地理位置 API 当前在 Teams 桌面客户端上 `getLocation API` 不受完全支持。</span><span class="sxs-lookup"><span data-stu-id="57ddf-158">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="57ddf-159">例如：</span><span class="sxs-lookup"><span data-stu-id="57ddf-159">For example:</span></span>
 * <span data-ttu-id="57ddf-160">若要提示用户访问其位置，必须调用 `getCurrentPosition()` ：</span><span class="sxs-lookup"><span data-stu-id="57ddf-160">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="57ddf-161">若要提示用户在桌面或 Web 上访问其相机，必须调用 `getUserMedia()` ：</span><span class="sxs-lookup"><span data-stu-id="57ddf-161">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="57ddf-162">若要在移动设备上捕获图像，Teams 移动版在调用时需要获取权限 `captureImage()` ：</span><span class="sxs-lookup"><span data-stu-id="57ddf-162">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="57ddf-163">调用以下消息时，通知将提示用户 `requestPermission()` ：</span><span class="sxs-lookup"><span data-stu-id="57ddf-163">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="57ddf-164">若要使用相机或访问照片库，Teams 移动版在调用时会询问权限 `selectMedia()` ：</span><span class="sxs-lookup"><span data-stu-id="57ddf-164">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="57ddf-165">若要使用麦克风，Teams 移动版会在您呼叫时请求权限 `selectMedia()` ：</span><span class="sxs-lookup"><span data-stu-id="57ddf-165">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="57ddf-166">若要提示用户共享地图界面上的位置，Teams 移动版在调用时请求权限 `getLocation()` ：</span><span class="sxs-lookup"><span data-stu-id="57ddf-166">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="57ddf-167">桌面</span><span class="sxs-lookup"><span data-stu-id="57ddf-167">Desktop</span></span>](#tab/desktop)

   ![选项卡桌面设备权限提示](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="57ddf-169">移动</span><span class="sxs-lookup"><span data-stu-id="57ddf-169">Mobile</span></span>](#tab/mobile)

   ![选项卡移动设备权限提示](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="57ddf-171">跨登录会话的权限行为</span><span class="sxs-lookup"><span data-stu-id="57ddf-171">Permission behavior across login sessions</span></span>

<span data-ttu-id="57ddf-172">将存储每个登录会话的设备权限。</span><span class="sxs-lookup"><span data-stu-id="57ddf-172">Device permissions are stored for every login session.</span></span> <span data-ttu-id="57ddf-173">这意味着，如果你登录到另一个 Teams 实例（例如，在另一台计算机中）时，之前会话中的设备权限将不可用。</span><span class="sxs-lookup"><span data-stu-id="57ddf-173">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="57ddf-174">因此，必须重新同意新会话的设备权限。</span><span class="sxs-lookup"><span data-stu-id="57ddf-174">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="57ddf-175">它还意味着，如果你注销 Teams 或在 Teams 中切换租户，你的设备权限将从以前的登录会话中删除。</span><span class="sxs-lookup"><span data-stu-id="57ddf-175">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="57ddf-176">当你同意本机设备权限时，它仅对当前的登录 _会话_ 有效。</span><span class="sxs-lookup"><span data-stu-id="57ddf-176">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-step"></a><span data-ttu-id="57ddf-177">后续步骤</span><span class="sxs-lookup"><span data-stu-id="57ddf-177">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="57ddf-178">在 Teams 中集成媒体功能</span><span class="sxs-lookup"><span data-stu-id="57ddf-178">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
