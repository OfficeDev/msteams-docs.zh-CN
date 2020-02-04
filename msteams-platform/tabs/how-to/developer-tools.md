---
title: Microsoft 团队选项卡的 DevTools
description: 介绍如何在使用 Microsoft 团队桌面客户端时获取 DevTools
keywords: devtools 调试 mobile chrome 桌面客户端开发人员工具
ms.openlocfilehash: 6c8ac15caf64c979b23155be847e8791988486e6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673244"
---
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="480a6-104">Microsoft 团队选项卡的 DevTools</span><span class="sxs-lookup"><span data-stu-id="480a6-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="480a6-105">当工作组在浏览器中运行时，很容易访问浏览器的 DevTools： F12 （在 Windows 中）或命令-Option-I （在 MacOS 上）。</span><span class="sxs-lookup"><span data-stu-id="480a6-105">When Teams is running in a browser, it’s easy to access the browser's DevTools: F12 (on Windows) or Command-Option-I (on MacOS).</span></span> <span data-ttu-id="480a6-106">DevTools 使您可以访问：</span><span class="sxs-lookup"><span data-stu-id="480a6-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="480a6-107">查看控制台日志。</span><span class="sxs-lookup"><span data-stu-id="480a6-107">View console logs.</span></span>
1. <span data-ttu-id="480a6-108">在运行时查看/修改 html、css 和网络请求。</span><span class="sxs-lookup"><span data-stu-id="480a6-108">View/modify html, css, and network requests during runtime.</span></span>
1. <span data-ttu-id="480a6-109">将断点添加到 JavaScript 代码，并执行交互式调试。</span><span class="sxs-lookup"><span data-stu-id="480a6-109">Add breakpoints to your JavaScript code, and perform interactive debugging.</span></span>

<span data-ttu-id="480a6-110">仅在启用开发人员预览版后，桌面和 Android 客户端中才会提供此功能。</span><span class="sxs-lookup"><span data-stu-id="480a6-110">The feature is only available in desktop and Android clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="480a6-111">有关详细信息，请参阅[如何启用开发人员预览](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="480a6-111">See [How do I enable Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

## <a name="accessing-devtools-in-the-desktop"></a><span data-ttu-id="480a6-112">访问桌面中的 DevTools</span><span class="sxs-lookup"><span data-stu-id="480a6-112">Accessing DevTools in the Desktop</span></span>

<span data-ttu-id="480a6-113">虽然团队的 web 版本和团队的桌面版本几乎完全相同，但在某些方面存在差异，尤其是对于身份验证。</span><span class="sxs-lookup"><span data-stu-id="480a6-113">While the web version of Teams and the desktop version of teams are almost exactly the same, there are some differences, particularly with respect to authentication.</span></span> <span data-ttu-id="480a6-114">有时，确定要执行的操作的唯一方法是使用 DevTools。</span><span class="sxs-lookup"><span data-stu-id="480a6-114">Sometimes the only way to figure out what’s going on is to use the DevTools.</span></span> <span data-ttu-id="480a6-115">下面介绍了如何从团队桌面客户端获取它们。</span><span class="sxs-lookup"><span data-stu-id="480a6-115">Here's how to get to them from the Teams desktop client.</span></span> <span data-ttu-id="480a6-116">在桌面客户端中使用 DevTools：</span><span class="sxs-lookup"><span data-stu-id="480a6-116">To use DevTools in the desktop client:</span></span>

1. <span data-ttu-id="480a6-117">请确保已启用[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="480a6-117">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="480a6-118">打开 "选项卡"，让您有一些要使用 DevTools 检查的内容。</span><span class="sxs-lookup"><span data-stu-id="480a6-118">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="480a6-119">打开 DevTools</span><span class="sxs-lookup"><span data-stu-id="480a6-119">Open the DevTools</span></span>
    * <span data-ttu-id="480a6-120">在 Windows 中，你可以通过桌面托盘中的 Microsoft 团队图标打开 DevTools：</span><span class="sxs-lookup"><span data-stu-id="480a6-120">On Windows, you open DevTools via the Microsoft Teams icon in the desktop tray:</span></span>

  ![右键单击打开 DevTools](~/assets/images/dev-preview/devtools-right-click.png)

    * <span data-ttu-id="480a6-122">在 MacOS 上，单击插接中的 "Microsoft 团队" 图标。</span><span class="sxs-lookup"><span data-stu-id="480a6-122">On MacOS, click on the Microsoft Teams icon in the Dock.</span></span>

<span data-ttu-id="480a6-123">以下是在打开 DevTools 并选择一个元素时的示例选项卡的外观：</span><span class="sxs-lookup"><span data-stu-id="480a6-123">Here’s what a sample tab looks like with the DevTools open and an element selected:</span></span>

![Tab 和 DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a><span data-ttu-id="480a6-125">从 Android 客户端访问 DevTools</span><span class="sxs-lookup"><span data-stu-id="480a6-125">Accessing DevTools from an Android client</span></span>

<span data-ttu-id="480a6-126">您还可以从 "团队 Android 客户端" 启用 DevTools。</span><span class="sxs-lookup"><span data-stu-id="480a6-126">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="480a6-127">为此，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="480a6-127">To do so:</span></span>

1. <span data-ttu-id="480a6-128">请确保已启用[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="480a6-128">Make sure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md)</span></span>
1. <span data-ttu-id="480a6-129">将设备连接到桌面计算机，并将您的 Android 设备设置为进行[远程调试](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span><span class="sxs-lookup"><span data-stu-id="480a6-129">Connect your device to your desktop computer, and setup your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)</span></span>
1. <span data-ttu-id="480a6-130">在 Chrome 浏览器中， `chrome://inspect/#devices`打开。</span><span class="sxs-lookup"><span data-stu-id="480a6-130">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="480a6-131">在您希望调试的选项卡下方单击 "**检查**"，如下面的屏幕截图所示。</span><span class="sxs-lookup"><span data-stu-id="480a6-131">Click **inspect** below the tab you wish to debug, as in the screenshot below.</span></span>

![Android DevTools](~/assets/images/android-devtools.png)
