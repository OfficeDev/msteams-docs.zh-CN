---
title: 适用于 Microsoft Teams 选项卡的 DevTools
description: 介绍如何在使用桌面客户端时Microsoft Teams DevTools
localization_priority: Normal
ms.topic: how-to
keywords: devtools 调试移动部件版式桌面客户端开发人员工具
ms.openlocfilehash: 70c9a2bab94ceb97e8dcd5cf5cdb98261d037f74
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101826"
---
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="12400-104">适用于 Microsoft Teams 选项卡的 DevTools</span><span class="sxs-lookup"><span data-stu-id="12400-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="12400-105">当Teams中运行时，可以轻松访问浏览器的 DevTools： F12 on Windows 或 Command-Option-I on MacOS。</span><span class="sxs-lookup"><span data-stu-id="12400-105">When Teams is running in a browser, it is easy to access the browser's DevTools: F12 on Windows or Command-Option-I on MacOS.</span></span> <span data-ttu-id="12400-106">DevTools 使你可以访问：</span><span class="sxs-lookup"><span data-stu-id="12400-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="12400-107">查看控制台日志。</span><span class="sxs-lookup"><span data-stu-id="12400-107">View console logs.</span></span>
1. <span data-ttu-id="12400-108">在运行时查看或修改 HTML、CSS 和网络请求。</span><span class="sxs-lookup"><span data-stu-id="12400-108">View or modify HTML, CSS, and network requests during runtime.</span></span>
1. <span data-ttu-id="12400-109">将断点添加到 JavaScript 代码并执行交互式调试。</span><span class="sxs-lookup"><span data-stu-id="12400-109">Add breakpoints to your JavaScript code and perform interactive debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="12400-110">启用此功能后，此功能仅适用于桌面开发者预览版 **Android** 客户端。</span><span class="sxs-lookup"><span data-stu-id="12400-110">The feature is only available for desktop and Android clients after the **Developer Preview** has been enabled.</span></span> <span data-ttu-id="12400-111">有关详细信息，请参阅如何 [启用开发人员预览](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="12400-111">For more information, see [How do I enable developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="access-devtools-on-the-desktop"></a><span data-ttu-id="12400-112">访问桌面上的 DevTools</span><span class="sxs-lookup"><span data-stu-id="12400-112">Access DevTools on the desktop</span></span>

<span data-ttu-id="12400-113">虽然 Web 版本和桌面版本的 Teams几乎相同，但身份验证存在一些差异。</span><span class="sxs-lookup"><span data-stu-id="12400-113">While the web version and the desktop version of Teams are almost the same, there are some differences concerning authentication.</span></span> <span data-ttu-id="12400-114">有时，了解所发生事件的唯一方法就是使用 DevTools。</span><span class="sxs-lookup"><span data-stu-id="12400-114">Sometimes the only way to figure out what is going on is to use the DevTools.</span></span> <span data-ttu-id="12400-115">若要在桌面客户端使用 DevTools，你必须：</span><span class="sxs-lookup"><span data-stu-id="12400-115">To use DevTools in the desktop client, you must:</span></span>

1. <span data-ttu-id="12400-116">确保你已启用 [开发人员预览](~/resources/dev-preview/developer-preview-intro.md)版。</span><span class="sxs-lookup"><span data-stu-id="12400-116">Ensure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="12400-117">打开一个选项卡，以便你有一些要检查的 DevTools。</span><span class="sxs-lookup"><span data-stu-id="12400-117">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="12400-118">打开 DevTools 以下方法之一：</span><span class="sxs-lookup"><span data-stu-id="12400-118">Open the DevTools one of the following ways:</span></span>
    * <span data-ttu-id="12400-119">在Windows，通过桌面托盘中的Microsoft Teams图标打开 DevTools：</span><span class="sxs-lookup"><span data-stu-id="12400-119">On Windows, you open DevTools via the Microsoft Teams icon in the desktop tray:</span></span><br>
  <span data-ttu-id="12400-120">![右键单击以打开 DevTools](~/assets/images/dev-preview/devtools-right-click.png)</span><span class="sxs-lookup"><span data-stu-id="12400-120">![Right-click to open DevTools](~/assets/images/dev-preview/devtools-right-click.png)</span></span>
    * <span data-ttu-id="12400-121">在 MacOS 上，单击扩展Microsoft Teams图标。</span><span class="sxs-lookup"><span data-stu-id="12400-121">On MacOS, click on the Microsoft Teams icon in the Dock.</span></span>

<span data-ttu-id="12400-122">以下示例显示 DevTools 打开并检查选项卡配置对话框：</span><span class="sxs-lookup"><span data-stu-id="12400-122">The following example shows DevTools open and inspecting a tab configuration dialog:</span></span>

   ![Tab 和 DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-device"></a><span data-ttu-id="12400-124">从 Android 设备访问 DevTools</span><span class="sxs-lookup"><span data-stu-id="12400-124">Access DevTools from an Android device</span></span>

<span data-ttu-id="12400-125">还可以从 Android 客户端启用 Teams工具。</span><span class="sxs-lookup"><span data-stu-id="12400-125">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="12400-126">若要启用 DevTools，你必须：</span><span class="sxs-lookup"><span data-stu-id="12400-126">To enable DevTools, you must:</span></span>

1. <span data-ttu-id="12400-127">启用 [开发人员预览](~/resources/dev-preview/developer-preview-intro.md)版。</span><span class="sxs-lookup"><span data-stu-id="12400-127">Enable the [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="12400-128">连接设备连接到台式计算机，并设置 Android 设备进行[远程调试](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)。</span><span class="sxs-lookup"><span data-stu-id="12400-128">Connect your device to your desktop computer, and set up your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).</span></span>
1. <span data-ttu-id="12400-129">在 Chrome 浏览器中，打开 `chrome://inspect/#devices` 。</span><span class="sxs-lookup"><span data-stu-id="12400-129">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="12400-130">选择要 **调试** 的选项卡下的"检查"，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="12400-130">Select **inspect** under the tab you wish to debug, as in the following image:</span></span>

   ![Android DevTools](~/assets/images/android-devtools.png)
