---
title: 适用于 Microsoft Teams 选项卡的 DevTools
description: 介绍如何在使用 Microsoft Teams 桌面客户端时访问 DevTools
ms.topic: how-to
keywords: devtools 调试移动部件版式桌面客户端开发人员工具
ms.openlocfilehash: 8f23a5d56faa00d40451d2bbeadde32f6a5d0f7f
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014577"
---
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="c9cc3-104">适用于 Microsoft Teams 选项卡的 DevTools</span><span class="sxs-lookup"><span data-stu-id="c9cc3-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="c9cc3-105">当 Teams 在浏览器中运行时，可以轻松访问浏览器的 DevTools：Windows (上的 F12) 或 MacOS (上的 Command-Option-I) 。</span><span class="sxs-lookup"><span data-stu-id="c9cc3-105">When Teams is running in a browser, it’s easy to access the browser's DevTools: F12 (on Windows) or Command-Option-I (on MacOS).</span></span> <span data-ttu-id="c9cc3-106">DevTools 使你可以访问：</span><span class="sxs-lookup"><span data-stu-id="c9cc3-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="c9cc3-107">查看控制台日志。</span><span class="sxs-lookup"><span data-stu-id="c9cc3-107">View console logs.</span></span>
1. <span data-ttu-id="c9cc3-108">在运行时查看/修改 html、css 和网络请求。</span><span class="sxs-lookup"><span data-stu-id="c9cc3-108">View/modify html, css, and network requests during runtime.</span></span>
1. <span data-ttu-id="c9cc3-109">将断点添加到 JavaScript 代码，并执行交互式调试。</span><span class="sxs-lookup"><span data-stu-id="c9cc3-109">Add breakpoints to your JavaScript code, and perform interactive debugging.</span></span>

<span data-ttu-id="c9cc3-110">此功能仅在启用此功能后在桌面开发者预览版 Android 客户端中可用。</span><span class="sxs-lookup"><span data-stu-id="c9cc3-110">The feature is only available in desktop and Android clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="c9cc3-111">有关详细信息 [，请参阅开发者预览版](~/resources/dev-preview/developer-preview-intro.md) 启用该设置。</span><span class="sxs-lookup"><span data-stu-id="c9cc3-111">See [How do I enable Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

## <a name="accessing-devtools-in-the-desktop"></a><span data-ttu-id="c9cc3-112">访问桌面版中的 DevTools</span><span class="sxs-lookup"><span data-stu-id="c9cc3-112">Accessing DevTools in the Desktop</span></span>

<span data-ttu-id="c9cc3-113">虽然 Teams 的 Web 版本和团队的桌面版本几乎完全相同，但存在一些差异，尤其是在身份验证方面。</span><span class="sxs-lookup"><span data-stu-id="c9cc3-113">While the web version of Teams and the desktop version of teams are almost exactly the same, there are some differences, particularly with respect to authentication.</span></span> <span data-ttu-id="c9cc3-114">有时，确定发生事件的唯一方法就是使用 DevTools。</span><span class="sxs-lookup"><span data-stu-id="c9cc3-114">Sometimes the only way to figure out what’s going on is to use the DevTools.</span></span> <span data-ttu-id="c9cc3-115">下面将了解如何从 Teams 桌面客户端访问它们。</span><span class="sxs-lookup"><span data-stu-id="c9cc3-115">Here's how to get to them from the Teams desktop client.</span></span> <span data-ttu-id="c9cc3-116">若要在桌面客户端中使用 DevTools：</span><span class="sxs-lookup"><span data-stu-id="c9cc3-116">To use DevTools in the desktop client:</span></span>

1. <span data-ttu-id="c9cc3-117">确保已启用开发人员 [预览](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="c9cc3-117">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="c9cc3-118">打开一个选项卡，以便使用 DevTools 检查某些内容。</span><span class="sxs-lookup"><span data-stu-id="c9cc3-118">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="c9cc3-119">打开 DevTools</span><span class="sxs-lookup"><span data-stu-id="c9cc3-119">Open the DevTools</span></span>
    * <span data-ttu-id="c9cc3-120">在 Windows 上，通过桌面托盘中的 Microsoft Teams 图标打开 DevTools：</span><span class="sxs-lookup"><span data-stu-id="c9cc3-120">On Windows, you open DevTools via the Microsoft Teams icon in the desktop tray:</span></span>

  ![右键单击以打开 DevTools](~/assets/images/dev-preview/devtools-right-click.png)

    * <span data-ttu-id="c9cc3-122">在 MacOS 上，单击扩展坞中的 Microsoft Teams 图标。</span><span class="sxs-lookup"><span data-stu-id="c9cc3-122">On MacOS, click on the Microsoft Teams icon in the Dock.</span></span>

<span data-ttu-id="c9cc3-123">下面是打开 DevTools 并选中元素后的示例选项卡的外观：</span><span class="sxs-lookup"><span data-stu-id="c9cc3-123">Here’s what a sample tab looks like with the DevTools open and an element selected:</span></span>

![Tab 和 DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a><span data-ttu-id="c9cc3-125">从 Android 客户端访问 DevTools</span><span class="sxs-lookup"><span data-stu-id="c9cc3-125">Accessing DevTools from an Android client</span></span>

<span data-ttu-id="c9cc3-126">还可以从 Teams Android 客户端启用 DevTools。</span><span class="sxs-lookup"><span data-stu-id="c9cc3-126">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="c9cc3-127">为此，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="c9cc3-127">To do so:</span></span>

1. <span data-ttu-id="c9cc3-128">确保已启用开发人员 [预览](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="c9cc3-128">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="c9cc3-129">将设备连接到台式计算机，并设置 Android 设备进行 [远程调试](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="c9cc3-129">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span></span>
1. <span data-ttu-id="c9cc3-130">在 Chrome 浏览器中，打开 `chrome://inspect/#devices` 。</span><span class="sxs-lookup"><span data-stu-id="c9cc3-130">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="c9cc3-131">单击 **要** 调试的选项卡下方的"检查"，如下面的屏幕截图所示。</span><span class="sxs-lookup"><span data-stu-id="c9cc3-131">Click **inspect** below the tab you wish to debug, as in the screenshot below.</span></span>

![Android DevTools](~/assets/images/android-devtools.png)
