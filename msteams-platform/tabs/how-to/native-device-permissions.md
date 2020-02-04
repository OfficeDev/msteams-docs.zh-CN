---
title: 为 Microsoft "团队" 选项卡请求设备权限
description: 如何更新您的应用程序清单，以便请求对通常需要用户同意的本机功能的访问权限
keywords: 团队选项卡开发
ms.openlocfilehash: 454466ff17ecf275f6ae6c7413df8e117335f3c8
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41672997"
---
# <a name="request-device-permissions-for-your-microsoft-teams-tab"></a><span data-ttu-id="9b18d-104">为 Microsoft "团队" 选项卡请求设备权限</span><span class="sxs-lookup"><span data-stu-id="9b18d-104">Request device permissions for your Microsoft Teams tab</span></span>

<span data-ttu-id="9b18d-105">您可能希望使用需要访问本机设备功能的功能来丰富您的选项卡，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9b18d-105">You might want to enrich your tab with features that require access native device functionality like:</span></span>

* <span data-ttu-id="9b18d-106">拍照</span><span class="sxs-lookup"><span data-stu-id="9b18d-106">Camera</span></span>
* <span data-ttu-id="9b18d-107">着</span><span class="sxs-lookup"><span data-stu-id="9b18d-107">Microphone</span></span>
* <span data-ttu-id="9b18d-108">位置</span><span class="sxs-lookup"><span data-stu-id="9b18d-108">Location</span></span>
* <span data-ttu-id="9b18d-109">通知</span><span class="sxs-lookup"><span data-stu-id="9b18d-109">Notifications</span></span>

![设备权限设置屏幕](~/assets/images/tabs/device-permissions.png)

> [!IMPORTANT]
> <span data-ttu-id="9b18d-111">移动客户端上的选项卡目前不支持本机设备功能，但即将推出完全支持。</span><span class="sxs-lookup"><span data-stu-id="9b18d-111">Native device functionality is currently not supported for tabs on mobile clients but full support is coming soon.</span></span> <span data-ttu-id="9b18d-112">若要为此更改做准备，应按照移动选项卡[上的选项卡指南中](~/tabs/design/tabs-mobile.md)的步骤创建选项卡。</span><span class="sxs-lookup"><span data-stu-id="9b18d-112">To prepare for this change you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="9b18d-113">个人应用（静态选项卡）目前可在[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中使用。</span><span class="sxs-lookup"><span data-stu-id="9b18d-113">Personal apps (static tabs) are currently available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
>
> <span data-ttu-id="9b18d-114">释放对选项卡的完全支持时：</span><span class="sxs-lookup"><span data-stu-id="9b18d-114">When full support for tabs is released:</span></span>
>
> * <span data-ttu-id="9b18d-115">所有选项卡将始终在移动设备上可用</span><span class="sxs-lookup"><span data-stu-id="9b18d-115">All tabs will always be available on mobile</span></span>
> * <span data-ttu-id="9b18d-116">您`contentUrl` **将在移动团队客户端中加载**。</span><span class="sxs-lookup"><span data-stu-id="9b18d-116">Your `contentUrl` **will be loaded in the mobile Teams client**.</span></span>
> * <span data-ttu-id="9b18d-117">对于频道/组选项卡，用户仍可以通过您`websiteUrl`在单独的浏览器中打开您的`contentUrl`选项卡，但您将首先加载。</span><span class="sxs-lookup"><span data-stu-id="9b18d-117">For channel/group tabs, users can still open your tab in a separate browser via your `websiteUrl`, however your `contentUrl` will be loaded first.</span></span>  

## <a name="device-permissions"></a><span data-ttu-id="9b18d-118">设备权限</span><span class="sxs-lookup"><span data-stu-id="9b18d-118">Device permissions</span></span>

<span data-ttu-id="9b18d-119">通过访问用户的设备权限，您可以生成更丰富的体验，例如：</span><span class="sxs-lookup"><span data-stu-id="9b18d-119">Accessing a user’s device permissions allows you to build much richer experiences, for example:</span></span>

* <span data-ttu-id="9b18d-120">记录和共享简短视频</span><span class="sxs-lookup"><span data-stu-id="9b18d-120">Record and share short videos</span></span>
* <span data-ttu-id="9b18d-121">录制简短的音频备忘录并在以后保存它们</span><span class="sxs-lookup"><span data-stu-id="9b18d-121">Record short audio memos and save them for later</span></span>
* <span data-ttu-id="9b18d-122">使用用户位置信息显示相关信息</span><span class="sxs-lookup"><span data-stu-id="9b18d-122">Use user location information to display relevant information</span></span>

<span data-ttu-id="9b18d-123">[！重要说明] 虽然在大多数新式 web 浏览器中访问这些功能是标准的，但你需要让团队知道你要使用哪些功能来更新你的应用程序清单。</span><span class="sxs-lookup"><span data-stu-id="9b18d-123">While access to these features are standard in most modern web browsers, you need to let Teams know which features you’d like to use by updating your app manifest.</span></span> <span data-ttu-id="9b18d-124">这样，您就可以像在浏览器中一样请求权限，而在团队桌面客户端上运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="9b18d-124">This will allow you to ask for permissions, the same way you would in a browser, while your app is running on the Teams desktop client.</span></span>

## <a name="properties"></a><span data-ttu-id="9b18d-125">属性</span><span class="sxs-lookup"><span data-stu-id="9b18d-125">Properties</span></span>

<span data-ttu-id="9b18d-126">`manifest.json`通过添加`devicePermissions`和指定要在应用程序中使用的五个属性中的哪一个来更新应用程序：</span><span class="sxs-lookup"><span data-stu-id="9b18d-126">Update your app's `manifest.json` by adding `devicePermissions` and specifying which of the five properties you’d like to use in your application:</span></span>

``` json
"devicePermissions": [
    "media",
    "geolocation",
    "notifications",
    "midi",
    "openExternal"
],
```

<span data-ttu-id="9b18d-127">每个属性都允许你提示用户提出同意</span><span class="sxs-lookup"><span data-stu-id="9b18d-127">Each property will allow you to prompt the user to ask for their consent</span></span>

| <span data-ttu-id="9b18d-128">属性</span><span class="sxs-lookup"><span data-stu-id="9b18d-128">Property</span></span>      | <span data-ttu-id="9b18d-129">说明</span><span class="sxs-lookup"><span data-stu-id="9b18d-129">Description</span></span>   |
| --- | --- |
| <span data-ttu-id="9b18d-130">光盘</span><span class="sxs-lookup"><span data-stu-id="9b18d-130">media</span></span>         | <span data-ttu-id="9b18d-131">使用摄像头、麦克风和扬声器的权限</span><span class="sxs-lookup"><span data-stu-id="9b18d-131">permission to use the camera, microphone and speakers</span></span> |
| <span data-ttu-id="9b18d-132">地理位置</span><span class="sxs-lookup"><span data-stu-id="9b18d-132">geolocation</span></span>   | <span data-ttu-id="9b18d-133">返回用户位置的权限</span><span class="sxs-lookup"><span data-stu-id="9b18d-133">permission to return the user's location</span></span>      |
| <span data-ttu-id="9b18d-134">通知</span><span class="sxs-lookup"><span data-stu-id="9b18d-134">notifications</span></span> | <span data-ttu-id="9b18d-135">发送用户通知的权限</span><span class="sxs-lookup"><span data-stu-id="9b18d-135">permission to send the user notifications</span></span>      |
| <span data-ttu-id="9b18d-136">midi</span><span class="sxs-lookup"><span data-stu-id="9b18d-136">midi</span></span>          | <span data-ttu-id="9b18d-137">从数字音乐仪器发送和接收 midi 信息的权限</span><span class="sxs-lookup"><span data-stu-id="9b18d-137">permission to send and receive midi information from a digital musical instrument</span></span>   |
| <span data-ttu-id="9b18d-138">openExternal</span><span class="sxs-lookup"><span data-stu-id="9b18d-138">openExternal</span></span>  | <span data-ttu-id="9b18d-139">在外部应用程序中打开链接的权限</span><span class="sxs-lookup"><span data-stu-id="9b18d-139">permission to open links in external applications</span></span>  |

## <a name="checking-permissions-from-your-tab"></a><span data-ttu-id="9b18d-140">从选项卡检查权限</span><span class="sxs-lookup"><span data-stu-id="9b18d-140">Checking permissions from your tab</span></span>

<span data-ttu-id="9b18d-141">添加`devicePermissions`到应用程序清单后，可以使用 HTML5 "权限" API 检查权限，而不会导致出现提示。</span><span class="sxs-lookup"><span data-stu-id="9b18d-141">Once you’ve added `devicePermissions` to your app manifest, you can check permissions using the HTML5 “permissions” API without causing a prompt.</span></span>

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

## <a name="prompting-the-user"></a><span data-ttu-id="9b18d-142">提示用户</span><span class="sxs-lookup"><span data-stu-id="9b18d-142">Prompting the user</span></span>

<span data-ttu-id="9b18d-143">为了显示提示以获取访问设备权限的许可，您需要使用相应的 HTML5 API。</span><span class="sxs-lookup"><span data-stu-id="9b18d-143">In order to show a prompt to get consent to access device permissions you need to leverage the appropriate HTML5 API.</span></span> <span data-ttu-id="9b18d-144">例如，为了提示用户访问其相机，您需要呼叫`getUserMedia`</span><span class="sxs-lookup"><span data-stu-id="9b18d-144">For example, in order to prompt the user to access their camera you need to call `getUserMedia`</span></span>

```Javascript
navigator.mediaDevices.getUserMedia({ audio: true, video: true });
```

<span data-ttu-id="9b18d-145">调用时，地理位置将显示权限提示`getCurrentPosition`</span><span class="sxs-lookup"><span data-stu-id="9b18d-145">Geolocation will  show a permission prompt when you call `getCurrentPosition`</span></span>

```Javascript
navigator.geolocation.getCurrentPosition(function (position) { /*... */ });
```

<span data-ttu-id="9b18d-146">调用时，通知将提示用户`requestPermission`</span><span class="sxs-lookup"><span data-stu-id="9b18d-146">Notifications will prompt the user when you call `requestPermission`</span></span>

```Javascript
Notification.requestPermission(function(result) { /* ... */ });
```

![选项卡设备权限提示](~/assets/images/tabs/device-permissions-prompt.png)