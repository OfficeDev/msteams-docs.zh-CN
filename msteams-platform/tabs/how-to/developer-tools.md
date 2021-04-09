---
title: 适用于 Microsoft Teams 选项卡的 DevTools
description: 介绍如何在使用 Microsoft Teams 桌面客户端时访问 DevTools
ms.topic: how-to
keywords: devtools 调试移动部件版式桌面客户端开发人员工具
ms.openlocfilehash: 1c540c94adc080d9495097f8e3b427eeb14c56d8
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634739"
---
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="154d7-104">适用于 Microsoft Teams 选项卡的 DevTools</span><span class="sxs-lookup"><span data-stu-id="154d7-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="154d7-105">当 Teams 在浏览器中运行时，可以轻松访问浏览器的 DevTools：Windows 上的 F12 或 MacOS 上的 Command-Option-I。</span><span class="sxs-lookup"><span data-stu-id="154d7-105">When Teams is running in a browser, it is easy to access the browser's DevTools: F12 on Windows or Command-Option-I on MacOS.</span></span> <span data-ttu-id="154d7-106">DevTools 使你可以访问：</span><span class="sxs-lookup"><span data-stu-id="154d7-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="154d7-107">查看控制台日志。</span><span class="sxs-lookup"><span data-stu-id="154d7-107">View console logs.</span></span>
1. <span data-ttu-id="154d7-108">在运行时查看或修改 HTML、CSS 和网络请求。</span><span class="sxs-lookup"><span data-stu-id="154d7-108">View or modify HTML, CSS, and network requests during runtime.</span></span>
1. <span data-ttu-id="154d7-109">将断点添加到 JavaScript 代码并执行交互式调试。</span><span class="sxs-lookup"><span data-stu-id="154d7-109">Add breakpoints to your JavaScript code and perform interactive debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="154d7-110">启用此功能后，此功能仅在桌面开发者预览版 **Android** 客户端中可用。</span><span class="sxs-lookup"><span data-stu-id="154d7-110">The feature is only available in desktop and Android clients after **Developer Preview** has been enabled.</span></span> <span data-ttu-id="154d7-111">有关详细信息，请参阅如何 [启用开发人员预览](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="154d7-111">For more information, see [How do I enable developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="access-devtools-in-the-desktop"></a><span data-ttu-id="154d7-112">访问桌面版中的 DevTools</span><span class="sxs-lookup"><span data-stu-id="154d7-112">Access DevTools in the Desktop</span></span>

<span data-ttu-id="154d7-113">虽然 Teams 的 Web 版本和桌面版几乎完全相同，但身份验证方面存在一些差异。</span><span class="sxs-lookup"><span data-stu-id="154d7-113">While the web version and the desktop version of Teams are almost exactly the same, there are some differences with respect to authentication.</span></span> <span data-ttu-id="154d7-114">有时，了解所发生事件的唯一方法就是使用 DevTools。</span><span class="sxs-lookup"><span data-stu-id="154d7-114">Sometimes the only way to figure out what is going on is to use the DevTools.</span></span> <span data-ttu-id="154d7-115">若要在桌面客户端使用 DevTools，你必须：</span><span class="sxs-lookup"><span data-stu-id="154d7-115">To use DevTools in the desktop client, you must:</span></span>

1. <span data-ttu-id="154d7-116">确保你已启用 [开发人员预览](~/resources/dev-preview/developer-preview-intro.md)版。</span><span class="sxs-lookup"><span data-stu-id="154d7-116">Ensure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="154d7-117">打开一个选项卡，以便你有一些要检查的 DevTools。</span><span class="sxs-lookup"><span data-stu-id="154d7-117">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="154d7-118">通过下列方式之一打开 DevTools：</span><span class="sxs-lookup"><span data-stu-id="154d7-118">Open the DevTools in one of the following ways:</span></span>
    * <span data-ttu-id="154d7-119">**Windows：** 在桌面托盘中选择 Teams 图标。</span><span class="sxs-lookup"><span data-stu-id="154d7-119">**Windows**: Select the Teams icon in the desktop tray.</span></span>
    * <span data-ttu-id="154d7-120">**MacOS：** 选择扩展坞中的 Teams 图标。</span><span class="sxs-lookup"><span data-stu-id="154d7-120">**MacOS**: Select the Teams icon in the Dock.</span></span>
 
   <span data-ttu-id="154d7-121">下图显示了检查选项卡配置对话框中元素的 DevTools：</span><span class="sxs-lookup"><span data-stu-id="154d7-121">The following image shows DevTools inspecting an element in a tab configuration dialog:</span></span>

   ![Tab 和 DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-client"></a><span data-ttu-id="154d7-123">从 Android 客户端访问 DevTools</span><span class="sxs-lookup"><span data-stu-id="154d7-123">Access DevTools from an Android client</span></span>

<span data-ttu-id="154d7-124">还可以从 Teams Android 客户端启用 DevTools。</span><span class="sxs-lookup"><span data-stu-id="154d7-124">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="154d7-125">若要启用 DevTools，你必须：</span><span class="sxs-lookup"><span data-stu-id="154d7-125">To enable DevTools, you must:</span></span>

1. <span data-ttu-id="154d7-126">启用 [开发人员预览](~/resources/dev-preview/developer-preview-intro.md)版。</span><span class="sxs-lookup"><span data-stu-id="154d7-126">Enable the [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="154d7-127">将设备连接到台式计算机，并设置 Android 设备进行 [远程调试](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)。</span><span class="sxs-lookup"><span data-stu-id="154d7-127">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).</span></span>
1. <span data-ttu-id="154d7-128">在 Chrome 浏览器中，打开 `chrome://inspect/#devices` 。</span><span class="sxs-lookup"><span data-stu-id="154d7-128">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="154d7-129">选择要 **调试** 的选项卡下的"检查"，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="154d7-129">Select **inspect** under the tab you wish to debug, as in the following image:</span></span>

   ![Android DevTools](~/assets/images/android-devtools.png)
