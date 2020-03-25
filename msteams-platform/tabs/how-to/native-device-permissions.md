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
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="e4c63-104">为 Microsoft "团队" 选项卡请求设备权限</span><span class="sxs-lookup"><span data-stu-id="e4c63-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="e4c63-105">您可能希望使用需要访问本机设备功能的功能来丰富您的选项卡，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e4c63-105">You might want to enrich your tab with features that require access native device functionality like:</span></span>

* <span data-ttu-id="e4c63-106">拍照</span><span class="sxs-lookup"><span data-stu-id="e4c63-106">Camera</span></span>
* <span data-ttu-id="e4c63-107">着</span><span class="sxs-lookup"><span data-stu-id="e4c63-107">Microphone</span></span>
* <span data-ttu-id="e4c63-108">位置</span><span class="sxs-lookup"><span data-stu-id="e4c63-108">Location</span></span>
* <span data-ttu-id="e4c63-109">通知</span><span class="sxs-lookup"><span data-stu-id="e4c63-109">Notifications</span></span>

![设备权限设置屏幕](~/assets/images/tabs/device-permissions.png)

> [!IMPORTANT]
> <span data-ttu-id="e4c63-111">移动客户端上的选项卡目前不支持本机设备功能，但即将推出完全支持。</span><span class="sxs-lookup"><span data-stu-id="e4c63-111">Native device functionality is currently not supported for tabs on mobile clients but full support is coming soon.</span></span> <span data-ttu-id="e4c63-112">若要为此更改做准备，应按照移动选项卡[上的选项卡指南中](~/tabs/design/tabs-mobile.md)的步骤创建选项卡。</span><span class="sxs-lookup"><span data-stu-id="e4c63-112">To prepare for this change you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="e4c63-113">个人应用（静态选项卡）目前可在[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中使用。</span><span class="sxs-lookup"><span data-stu-id="e4c63-113">Personal apps (static tabs) are currently available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
>
> <span data-ttu-id="e4c63-114">释放对选项卡的完全支持时：</span><span class="sxs-lookup"><span data-stu-id="e4c63-114">When full support for tabs is released:</span></span>
>
> * <span data-ttu-id="e4c63-115">所有选项卡将始终在移动设备上可用</span><span class="sxs-lookup"><span data-stu-id="e4c63-115">All tabs will always be available on mobile</span></span>
> * <span data-ttu-id="e4c63-116">您`contentUrl` **将在移动团队客户端中加载**。</span><span class="sxs-lookup"><span data-stu-id="e4c63-116">Your `contentUrl` **will be loaded in the mobile Teams client**.</span></span>
> * <span data-ttu-id="e4c63-117">对于频道/组选项卡，用户仍可以通过您`websiteUrl`在单独的浏览器中打开您的`contentUrl`选项卡，但您将首先加载。</span><span class="sxs-lookup"><span data-stu-id="e4c63-117">For channel/group tabs, users can still open your tab in a separate browser via your `websiteUrl`, however your `contentUrl` will be loaded first.</span></span>  

## <a name="device-permissions"></a><span data-ttu-id="e4c63-118">设备权限</span><span class="sxs-lookup"><span data-stu-id="e4c63-118">Device permissions</span></span>

<span data-ttu-id="e4c63-119">通过访问用户的设备权限，您可以生成更丰富的体验，例如：</span><span class="sxs-lookup"><span data-stu-id="e4c63-119">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="e4c63-120">记录和共享简短视频</span><span class="sxs-lookup"><span data-stu-id="e4c63-120">Record and share short videos</span></span>
* <span data-ttu-id="e4c63-121">录制简短的音频备忘录并在以后保存它们</span><span class="sxs-lookup"><span data-stu-id="e4c63-121">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="e4c63-122">使用用户位置信息显示相关信息</span><span class="sxs-lookup"><span data-stu-id="e4c63-122">Use user location information to display relevant information</span></span>

<span data-ttu-id="e4c63-123">[！重要说明] 虽然在大多数新式 web 浏览器中访问这些功能是标准的，但你需要让团队知道你要使用哪些功能来更新你的应用程序清单。</span><span class="sxs-lookup"><span data-stu-id="e4c63-123">While access to these features are standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="e4c63-124">这样，您就可以像在浏览器中一样请求权限，而在团队桌面客户端上运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="e4c63-124">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="properties"></a><span data-ttu-id="e4c63-125">属性</span><span class="sxs-lookup"><span data-stu-id="e4c63-125">Properties</span></span>

<span data-ttu-id="e4c63-126">`manifest.json`通过添加`devicePermissions`和指定要在应用程序中使用的五个属性中的哪一个来更新应用程序：</span><span class="sxs-lookup"><span data-stu-id="e4c63-126">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="e4c63-127">每个属性都允许你提示用户提出同意</span><span class="sxs-lookup"><span data-stu-id="e4c63-127">Each property will allow you to prompt the user to ask for their consent</span></span>

| <span data-ttu-id="e4c63-128">属性</span><span class="sxs-lookup"><span data-stu-id="e4c63-128">Property</span></span>      | <span data-ttu-id="e4c63-129">说明</span><span class="sxs-lookup"><span data-stu-id="e4c63-129">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="e4c63-130">media</span><span class="sxs-lookup"><span data-stu-id="e4c63-130">media</span></span>         | <span data-ttu-id="e4c63-131">使用摄像头、麦克风和扬声器的权限</span><span class="sxs-lookup"><span data-stu-id="e4c63-131">permission to use the camera, microphone and speakers</span></span> |
| <span data-ttu-id="e4c63-132">地理位置</span><span class="sxs-lookup"><span data-stu-id="e4c63-132">geolocation</span></span>   | <span data-ttu-id="e4c63-133">返回用户位置的权限</span><span class="sxs-lookup"><span data-stu-id="e4c63-133">permission to return the user's location</span></span>      |
| <span data-ttu-id="e4c63-134">通知</span><span class="sxs-lookup"><span data-stu-id="e4c63-134">notifications</span></span> | <span data-ttu-id="e4c63-135">发送用户通知的权限</span><span class="sxs-lookup"><span data-stu-id="e4c63-135">permission to send the user notifications</span></span>      |
| <span data-ttu-id="e4c63-136">midi</span><span class="sxs-lookup"><span data-stu-id="e4c63-136">midi</span></span>          | <span data-ttu-id="e4c63-137">从数字音乐仪器发送和接收 midi 信息的权限</span><span class="sxs-lookup"><span data-stu-id="e4c63-137">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="e4c63-138">openExternal</span><span class="sxs-lookup"><span data-stu-id="e4c63-138">openExternal</span></span>  | <span data-ttu-id="e4c63-139">在外部应用程序中打开链接的权限</span><span class="sxs-lookup"><span data-stu-id="e4c63-139">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="e4c63-140">从选项卡检查权限</span><span class="sxs-lookup"><span data-stu-id="e4c63-140">Checking permissions from your tab</span></span>

<span data-ttu-id="e4c63-141">添加`devicePermissions`到应用程序清单后，可以使用 HTML5 "权限" API 检查权限，而不会导致出现提示。</span><span class="sxs-lookup"><span data-stu-id="e4c63-141">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="e4c63-142">提示用户</span><span class="sxs-lookup"><span data-stu-id="e4c63-142">Prompting the user</span></span>

<span data-ttu-id="e4c63-143">为了显示提示以获取访问设备权限的许可，您需要使用相应的 HTML5 API。</span><span class="sxs-lookup"><span data-stu-id="e4c63-143">In order to show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 API.</span></span> <span data-ttu-id="e4c63-144">例如，为了提示用户访问其相机，您需要呼叫`getUserMedia`</span><span class="sxs-lookup"><span data-stu-id="e4c63-144">For example, in order to prompt the user to access their camera you need to call `getUserMedia`</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="e4c63-145">调用时，地理位置将显示权限提示`getCurrentPosition`</span><span class="sxs-lookup"><span data-stu-id="e4c63-145">Geolocation will  show a permission prompt when you call `getCurrentPosition`</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="e4c63-146">调用时，通知将提示用户`requestPermission`</span><span class="sxs-lookup"><span data-stu-id="e4c63-146">Notifications will prompt the user when you call `requestPermission`</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![选项卡设备权限提示](~/assets/images/tabs/device-permissions-prompt.png)

## <a name="permission-behavior-across-login-sessions"></a><span data-ttu-id="e4c63-148">跨登录会话的权限行为</span><span class="sxs-lookup"><span data-stu-id="e4c63-148">Permission behavior across login sessions</span></span>

<span data-ttu-id="e4c63-149">本机设备权限是按每个登录会话存储的。</span><span class="sxs-lookup"><span data-stu-id="e4c63-149">Native device permissions are stored per login session.</span></span> <span data-ttu-id="e4c63-150">这意味着，如果您登录到团队的另一个实例（例如，在另一台计算机上），您的设备权限将不可用。</span><span class="sxs-lookup"><span data-stu-id="e4c63-150">This means that if you log into another instance of Teams (ex: on another computer), your device permissions from your previous sessions will not be available.</span></span> <span data-ttu-id="e4c63-151">相反，你将需要重新同意新登录 sessoin 的设备权限。</span><span class="sxs-lookup"><span data-stu-id="e4c63-151">Instead, you will need to re-consent to device permissions for the new login sessoin.</span></span> <span data-ttu-id="e4c63-152">这也意味着，如果您注销团队（或团队内部的交换机租户），则将删除该先前登录会话的设备权限。</span><span class="sxs-lookup"><span data-stu-id="e4c63-152">This also means, if you log out of Teams (or switch tenants inside of Teams), your device permissions will be deleted for that previous login session.</span></span> <span data-ttu-id="e4c63-153">在开发本机设备权限时，请记住这一点：您同意的本机功能仅适用于您的_当前_登录 sessoin。</span><span class="sxs-lookup"><span data-stu-id="e4c63-153">Please keep this in mind when developing native device permissions: the native capabilities you consent to are only for your _current_ login sessoin.</span></span>