---
title: 请求应用的设备Microsoft Teams权限
keywords: teams 应用功能权限
description: 如何更新应用清单，以请求访问通常需要用户同意的本机功能
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 452840c5809da32a79c231f85cd1de9f8746367a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019851"
---
# <a name="request-device-permissions-for-your-microsoft-teams-app"></a><span data-ttu-id="eda1a-104">请求应用的设备Microsoft Teams权限</span><span class="sxs-lookup"><span data-stu-id="eda1a-104">Request device permissions for your Microsoft Teams app</span></span>

<span data-ttu-id="eda1a-105">可以使用本机设备Teams（如相机、麦克风和位置）丰富你的应用。</span><span class="sxs-lookup"><span data-stu-id="eda1a-105">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span> <span data-ttu-id="eda1a-106">本文档指导您如何请求用户同意和访问本机设备权限。</span><span class="sxs-lookup"><span data-stu-id="eda1a-106">This document guides you on how to request user consent and access the native device permissions.</span></span>

> [!NOTE]
> * <span data-ttu-id="eda1a-107">若要将媒体功能集成到Microsoft Teams移动应用中，请参阅[集成媒体功能](mobile-camera-image-permissions.md)。</span><span class="sxs-lookup"><span data-stu-id="eda1a-107">To integrate media capabilities within your Microsoft Teams mobile app, see [Integrate media capabilities](mobile-camera-image-permissions.md).</span></span>
> * <span data-ttu-id="eda1a-108">若要将 QR 或条形码扫描仪功能集成到 Microsoft Teams 移动应用中，请参阅在应用中集成 QR 或条形码[扫描仪Teams](qr-barcode-scanner-capability.md)</span><span class="sxs-lookup"><span data-stu-id="eda1a-108">To integrate QR or barcode scanner capability within your Microsoft Teams mobile app, see [Integrate QR or barcode scanner capability in Teams](qr-barcode-scanner-capability.md)</span></span>
> * <span data-ttu-id="eda1a-109">若要在移动应用中集成位置Microsoft Teams，请参阅[集成位置功能](location-capability.md)。</span><span class="sxs-lookup"><span data-stu-id="eda1a-109">To integrate location capabilities within your Microsoft Teams mobile app, see [Integrate location capabilities](location-capability.md).</span></span>

## <a name="native-device-permissions"></a><span data-ttu-id="eda1a-110">本机设备权限</span><span class="sxs-lookup"><span data-stu-id="eda1a-110">Native device permissions</span></span>

<span data-ttu-id="eda1a-111">必须请求设备权限才能访问本机设备功能。</span><span class="sxs-lookup"><span data-stu-id="eda1a-111">You must request the device permissions to access native device capabilities.</span></span> <span data-ttu-id="eda1a-112">设备权限对于所有应用构造（如选项卡、任务模块或消息传递扩展）的运行方式类似。</span><span class="sxs-lookup"><span data-stu-id="eda1a-112">The device permissions work similarly for all app constructs, such as tabs, task modules, or messaging extensions.</span></span> <span data-ttu-id="eda1a-113">用户必须转到设置中的权限Teams管理设备权限。</span><span class="sxs-lookup"><span data-stu-id="eda1a-113">The user must go to the permissions page in Teams settings to manage device permissions.</span></span>
<span data-ttu-id="eda1a-114">通过访问设备功能，你可以构建更丰富的体验，Teams平台，例如：</span><span class="sxs-lookup"><span data-stu-id="eda1a-114">By accessing the device capabilities, you can build richer experiences on the Teams platform, such as:</span></span>
* <span data-ttu-id="eda1a-115">捕获和查看图像。</span><span class="sxs-lookup"><span data-stu-id="eda1a-115">Capture and view images.</span></span>
* <span data-ttu-id="eda1a-116">扫描 QR 或条形码。</span><span class="sxs-lookup"><span data-stu-id="eda1a-116">Scan QR or barcode.</span></span>
* <span data-ttu-id="eda1a-117">录制和共享简短视频。</span><span class="sxs-lookup"><span data-stu-id="eda1a-117">Record and share short videos.</span></span>
* <span data-ttu-id="eda1a-118">录制音频备注并保存供以后使用。</span><span class="sxs-lookup"><span data-stu-id="eda1a-118">Record audio memos and save them for later use.</span></span>
* <span data-ttu-id="eda1a-119">使用用户的位置信息显示相关信息。</span><span class="sxs-lookup"><span data-stu-id="eda1a-119">Use the location information of the user to display relevant information.</span></span>

## <a name="access-device-permissions"></a><span data-ttu-id="eda1a-120">访问设备权限</span><span class="sxs-lookup"><span data-stu-id="eda1a-120">Access device permissions</span></span>

<span data-ttu-id="eda1a-121">JavaScript [Microsoft Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)提供了您的 Teams 移动应用访问用户设备权限和构建更丰富的体验所需的工具。 [](#manage-permissions)</span><span class="sxs-lookup"><span data-stu-id="eda1a-121">The [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) provides the tools necessary for your Teams mobile app to access the user’s [device permissions](#manage-permissions) and build a richer experience.</span></span>

<span data-ttu-id="eda1a-122">虽然新式 Web 浏览器中对这些功能的访问是标准操作，但你必须Teams更新应用清单来向用户通知你使用的功能。</span><span class="sxs-lookup"><span data-stu-id="eda1a-122">While access to these features is standard in modern web browsers, you must inform Teams about the features you use by updating your app manifest.</span></span> <span data-ttu-id="eda1a-123">此更新允许你在桌面客户端上运行应用时Teams权限。</span><span class="sxs-lookup"><span data-stu-id="eda1a-123">This update allows you to ask for permissions while your app runs on the Teams desktop client.</span></span>

> [!NOTE] 
> <span data-ttu-id="eda1a-124">目前Microsoft Teams媒体功能和 QR 条形码扫描仪功能的支持仅适用于移动客户端。</span><span class="sxs-lookup"><span data-stu-id="eda1a-124">Currently, Microsoft Teams support for media capabilities and QR barcode scanner capability is only available for mobile clients.</span></span>

## <a name="manage-permissions"></a><span data-ttu-id="eda1a-125">管理权限</span><span class="sxs-lookup"><span data-stu-id="eda1a-125">Manage permissions</span></span>

<span data-ttu-id="eda1a-126">用户可以通过选择"允许"或"拒绝Teams特定应用来管理设备权限。 </span><span class="sxs-lookup"><span data-stu-id="eda1a-126">A user can manage device permissions in Teams settings by selecting **Allow** or **Deny** permissions to specific apps.</span></span>
 
# <a name="desktop"></a>[<span data-ttu-id="eda1a-127">桌面</span><span class="sxs-lookup"><span data-stu-id="eda1a-127">Desktop</span></span>](#tab/desktop)

1. <span data-ttu-id="eda1a-128">打开你的Teams应用。</span><span class="sxs-lookup"><span data-stu-id="eda1a-128">Open your Teams app.</span></span>
1. <span data-ttu-id="eda1a-129">选择窗口右上角的配置文件图标。</span><span class="sxs-lookup"><span data-stu-id="eda1a-129">Select your profile icon in the upper right corner of the window.</span></span>
1. <span data-ttu-id="eda1a-130">Select **设置**  >  **Permissions** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="eda1a-130">Select **Settings** > **Permissions** from the drop-down menu.</span></span>
1. <span data-ttu-id="eda1a-131">选择所需的设置。</span><span class="sxs-lookup"><span data-stu-id="eda1a-131">Select your desired settings.</span></span>

   ![设备权限桌面设置屏幕](../../assets/images/tabs/device-permissions.png)

# <a name="mobile"></a>[<span data-ttu-id="eda1a-133">移动</span><span class="sxs-lookup"><span data-stu-id="eda1a-133">Mobile</span></span>](#tab/mobile)

1. <span data-ttu-id="eda1a-134">打开Teams。</span><span class="sxs-lookup"><span data-stu-id="eda1a-134">Open Teams.</span></span>
1. <span data-ttu-id="eda1a-135">转到 **设置**  >  **应用权限"。**</span><span class="sxs-lookup"><span data-stu-id="eda1a-135">Go to **Settings** > **App Permissions**.</span></span>
1. <span data-ttu-id="eda1a-136">选择要选择其设置的应用。</span><span class="sxs-lookup"><span data-stu-id="eda1a-136">Select the app for which you need to choose the settings.</span></span>
1. <span data-ttu-id="eda1a-137">选择所需的设置。</span><span class="sxs-lookup"><span data-stu-id="eda1a-137">Select your desired settings.</span></span>

    ![设备权限移动设置屏幕](../../assets/images/tabs/MobilePermissions.png)

---

## <a name="specify-permissions"></a><span data-ttu-id="eda1a-139">指定权限</span><span class="sxs-lookup"><span data-stu-id="eda1a-139">Specify permissions</span></span>

<span data-ttu-id="eda1a-140">通过添加并指定在应用程序中使用的五个属性中的哪一个来更新 `manifest.json` `devicePermissions` 应用：</span><span class="sxs-lookup"><span data-stu-id="eda1a-140">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties that you use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="eda1a-141">每个属性都允许您提示用户请求其同意：</span><span class="sxs-lookup"><span data-stu-id="eda1a-141">Each property allows you to prompt the user to ask for their consent:</span></span>

| <span data-ttu-id="eda1a-142">属性</span><span class="sxs-lookup"><span data-stu-id="eda1a-142">Property</span></span>      | <span data-ttu-id="eda1a-143">说明</span><span class="sxs-lookup"><span data-stu-id="eda1a-143">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="eda1a-144">media</span><span class="sxs-lookup"><span data-stu-id="eda1a-144">media</span></span>         | <span data-ttu-id="eda1a-145">使用相机、麦克风、扬声器和访问媒体库的权限。</span><span class="sxs-lookup"><span data-stu-id="eda1a-145">Permission to use the camera, microphone, speakers, and access media gallery.</span></span> |
| <span data-ttu-id="eda1a-146">地理位置</span><span class="sxs-lookup"><span data-stu-id="eda1a-146">geolocation</span></span>   | <span data-ttu-id="eda1a-147">返回用户位置的权限。</span><span class="sxs-lookup"><span data-stu-id="eda1a-147">Permission to return the user's location.</span></span>      |
| <span data-ttu-id="eda1a-148">通知</span><span class="sxs-lookup"><span data-stu-id="eda1a-148">notifications</span></span> | <span data-ttu-id="eda1a-149">发送用户通知的权限。</span><span class="sxs-lookup"><span data-stu-id="eda1a-149">Permission to send the user notifications.</span></span>      |
| <span data-ttu-id="eda1a-150">midi</span><span class="sxs-lookup"><span data-stu-id="eda1a-150">midi</span></span>          | <span data-ttu-id="eda1a-151">从数字音乐 (MIDI) 和接收音乐音乐数字接口的权限。</span><span class="sxs-lookup"><span data-stu-id="eda1a-151">Permission to send and receive  Musical Instrument Digital Interface (MIDI) information from a digital musical instrument.</span></span>   |
| <span data-ttu-id="eda1a-152">openExternal</span><span class="sxs-lookup"><span data-stu-id="eda1a-152">openExternal</span></span>  | <span data-ttu-id="eda1a-153">在外部应用程序中打开链接的权限。</span><span class="sxs-lookup"><span data-stu-id="eda1a-153">Permission to open links in external applications.</span></span>  |

## <a name="check-permissions-from-your-app"></a><span data-ttu-id="eda1a-154">检查应用的权限</span><span class="sxs-lookup"><span data-stu-id="eda1a-154">Check permissions from your app</span></span>

<span data-ttu-id="eda1a-155">添加到 `devicePermissions` 应用程序清单后，使用 **HTML5** 权限 API 检查权限，而不出现提示：</span><span class="sxs-lookup"><span data-stu-id="eda1a-155">After adding `devicePermissions` to your app manifest, check permissions using the **HTML5 permissions API** without causing a prompt:</span></span>

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

## <a name="use-teams-apis-to-get-device-permissions"></a><span data-ttu-id="eda1a-156">使用 Teams API 获取设备权限</span><span class="sxs-lookup"><span data-stu-id="eda1a-156">Use Teams APIs to get device permissions</span></span>

<span data-ttu-id="eda1a-157">利用适当的 HTML5 或 Teams API，显示获取访问设备权限同意的提示。</span><span class="sxs-lookup"><span data-stu-id="eda1a-157">Leverage appropriate HTML5 or Teams API, to display a prompt for getting consent to access device permissions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="eda1a-158">对 `camera` 、 `gallery` 和 `microphone` 的支持通过 [**selectMedia API 启用**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="eda1a-158">Support for `camera`, `gallery`, and `microphone` is enabled through [**selectMedia API**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true).</span></span> <span data-ttu-id="eda1a-159">将 [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) 用于单个映像捕获。</span><span class="sxs-lookup"><span data-stu-id="eda1a-159">Use [**captureImage API**](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#captureimage--error--sdkerror--files--file-------void-&preserve-view=true) for a single image capture.</span></span>
> * <span data-ttu-id="eda1a-160">通过 `location` [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true)启用对 的支持。</span><span class="sxs-lookup"><span data-stu-id="eda1a-160">Support for `location` is enabled through [**getLocation API**](/javascript/api/@microsoft/teams-js/location?view=msteams-client-js-latest#getLocation_LocationProps___error__SdkError__location__Location_____void_&preserve-view=true).</span></span> <span data-ttu-id="eda1a-161">你必须将此功能用于位置，因为 HTML5 地理位置 API 当前在桌面客户端上Teams `getLocation API` 受到完全支持。</span><span class="sxs-lookup"><span data-stu-id="eda1a-161">You must use this `getLocation API` for location, as HTML5 geolocation API is currently not fully supported on Teams desktop client.</span></span>

<span data-ttu-id="eda1a-162">例如：</span><span class="sxs-lookup"><span data-stu-id="eda1a-162">For example:</span></span>
 * <span data-ttu-id="eda1a-163">若要提示用户访问其位置，你必须调用 `getCurrentPosition()` ：</span><span class="sxs-lookup"><span data-stu-id="eda1a-163">To prompt the user to access their location you must call `getCurrentPosition()`:</span></span>

    ```Javascript
    navigator.geolocation.getCurrentPosition    (function (position) { /*... */ });
    ```

 * <span data-ttu-id="eda1a-164">若要提示用户访问桌面或 Web 上的相机，必须调用 `getUserMedia()` ：</span><span class="sxs-lookup"><span data-stu-id="eda1a-164">To prompt the user to access their camera on desktop or web you must call `getUserMedia()`:</span></span>

    ```Javascript
    navigator.mediaDevices.getUserMedia({ audio: true, video: true });
    ```

 * <span data-ttu-id="eda1a-165">若要在移动设备上捕获图像，Teams调用 时请求获取权限 `captureImage()` ：</span><span class="sxs-lookup"><span data-stu-id="eda1a-165">To capture the image on mobile, Teams mobile asks for permission when you call `captureImage()`:</span></span>

    ```Javascript
    microsoftTeams.media.captureImage((error: microsoftTeams.SdkError, files: microsoftTeams.media.File[]) => {
      /* ... */
    });
    ```

 * <span data-ttu-id="eda1a-166">当你调用 时，通知将提示用户 `requestPermission()` ：</span><span class="sxs-lookup"><span data-stu-id="eda1a-166">Notifications will prompt the user when you call `requestPermission()`:</span></span>

    ```Javascript
    Notification.requestPermission(function(result) { /* ... */ });
    ```




* <span data-ttu-id="eda1a-167">若要使用相机或访问照片库，Teams时，移动会询问权限 `selectMedia()` ：</span><span class="sxs-lookup"><span data-stu-id="eda1a-167">To use the camera or access photo gallery, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript
    microsoftTeams.media.selectMedia({ maxMediaCount: 10, mediaType: microsoftTeams.media.MediaType.Image }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    );
    ```

* <span data-ttu-id="eda1a-168">若要使用麦克风，Teams时，移动设备会询问权限 `selectMedia()` ：</span><span class="sxs-lookup"><span data-stu-id="eda1a-168">To use the microphone, Teams mobile asks permission when you call `selectMedia()`:</span></span>

    ```JavaScript 
    microsoftTeams.media.selectMedia({ maxMediaCount: 1, mediaType: microsoftTeams.media.MediaType.Audio }, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
      /* ... */
    });
    ```

* <span data-ttu-id="eda1a-169">若要提示用户在地图界面上共享位置，Teams调用 时请求权限 `getLocation()` ：</span><span class="sxs-lookup"><span data-stu-id="eda1a-169">To prompt the user to share location on the map interface, Teams mobile asks permission when you call `getLocation()`:</span></span>

    ```JavaScript 
    microsoftTeams.location.getLocation({ allowChooseLocation: true, showMap: true }, (error: microsoftTeams.SdkError, location: microsoftTeams.location.Location) => {
      /* ... *
    /});
    ```
# <a name="desktop"></a>[<span data-ttu-id="eda1a-170">桌面</span><span class="sxs-lookup"><span data-stu-id="eda1a-170">Desktop</span></span>](#tab/desktop)

   ![选项卡桌面设备权限提示](~/assets/images/tabs/device-permissions-prompt.png)

# <a name="mobile"></a>[<span data-ttu-id="eda1a-172">移动</span><span class="sxs-lookup"><span data-stu-id="eda1a-172">Mobile</span></span>](#tab/mobile)

   ![选项卡移动设备权限提示](../../assets/images/tabs/MobileLocationPermission.png)

* * * 

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="eda1a-174">跨登录会话的权限行为</span><span class="sxs-lookup"><span data-stu-id="eda1a-174">Permission behavior across login sessions</span></span>

<span data-ttu-id="eda1a-175">将存储每个登录会话的设备权限。</span><span class="sxs-lookup"><span data-stu-id="eda1a-175">Device permissions are stored for every login session.</span></span> <span data-ttu-id="eda1a-176">这意味着，如果你登录到另一个 Teams（例如，在另一台计算机中）时，之前会话中的设备权限将不可用。</span><span class="sxs-lookup"><span data-stu-id="eda1a-176">It means that if you sign in to another instance of Teams, for example, on another computer, your device permissions from your previous sessions are not available.</span></span> <span data-ttu-id="eda1a-177">因此，必须重新同意新会话的设备权限。</span><span class="sxs-lookup"><span data-stu-id="eda1a-177">Therefore, you must re-consent to device permissions for the new session.</span></span> <span data-ttu-id="eda1a-178">这也意味着，如果你注销Teams或切换租户Teams，你的设备权限将从以前的登录会话中删除。</span><span class="sxs-lookup"><span data-stu-id="eda1a-178">It also means, if you sign out of Teams or switch tenants in Teams, your device permissions are deleted from the previous login session.</span></span>  

> [!NOTE]
> <span data-ttu-id="eda1a-179">当你同意本机设备权限时，它仅对当前的登录 _会话_ 有效。</span><span class="sxs-lookup"><span data-stu-id="eda1a-179">When you consent to the native device permissions, it is valid only for your _current_ login session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eda1a-180">后续步骤</span><span class="sxs-lookup"><span data-stu-id="eda1a-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eda1a-181">将媒体功能集成到Teams</span><span class="sxs-lookup"><span data-stu-id="eda1a-181">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="eda1a-182">将 QR 或条形码扫描仪功能集成到 Teams</span><span class="sxs-lookup"><span data-stu-id="eda1a-182">Integrate QR or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="eda1a-183">在 Teams 中集成位置Teams</span><span class="sxs-lookup"><span data-stu-id="eda1a-183">Integrate location capabilities in Teams</span></span>](location-capability.md)
