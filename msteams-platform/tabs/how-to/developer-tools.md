---
title: 适用于 Microsoft Teams 选项卡的 DevTools
description: 介绍如何在使用 Microsoft Teams 桌面客户端时访问 DevTools
ms.topic: how-to
keywords: devtools 调试移动部件版式桌面客户端开发人员工具
ms.openlocfilehash: 7bd9403a74fd33619a2f8ac1b4b3a4c74a21175d
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654384"
---
# <a name="devtools-for-microsoft-teams-tabs"></a><span data-ttu-id="78b96-104">适用于 Microsoft Teams 选项卡的 DevTools</span><span class="sxs-lookup"><span data-stu-id="78b96-104">DevTools for Microsoft Teams tabs</span></span>

<span data-ttu-id="78b96-105">当 Teams 在浏览器中运行时，可以轻松访问浏览器的 DevTools：Windows 上的 F12 或 MacOS 上的 Command-Option-I。</span><span class="sxs-lookup"><span data-stu-id="78b96-105">When Teams is running in a browser, it is easy to access the browser's DevTools: F12 on Windows or Command-Option-I on MacOS.</span></span> <span data-ttu-id="78b96-106">DevTools 使你可以访问：</span><span class="sxs-lookup"><span data-stu-id="78b96-106">The DevTools gives you access to:</span></span>

1. <span data-ttu-id="78b96-107">查看控制台日志。</span><span class="sxs-lookup"><span data-stu-id="78b96-107">View console logs.</span></span>
1. <span data-ttu-id="78b96-108">在运行时查看或修改 HTML、CSS 和网络请求。</span><span class="sxs-lookup"><span data-stu-id="78b96-108">View or modify HTML, CSS, and network requests during runtime.</span></span>
1. <span data-ttu-id="78b96-109">将断点添加到 JavaScript 代码并执行交互式调试。</span><span class="sxs-lookup"><span data-stu-id="78b96-109">Add breakpoints to your JavaScript code and perform interactive debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="78b96-110">启用此功能后，此功能仅适用于桌面开发者预览版 **Android** 客户端。</span><span class="sxs-lookup"><span data-stu-id="78b96-110">The feature is only available for desktop and Android clients after the **Developer Preview** has been enabled.</span></span> <span data-ttu-id="78b96-111">有关详细信息，请参阅如何 [启用开发人员预览](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="78b96-111">For more information, see [How do I enable developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="access-devtools-in-the-desktop"></a><span data-ttu-id="78b96-112">访问桌面版中的 DevTools</span><span class="sxs-lookup"><span data-stu-id="78b96-112">Access DevTools in the Desktop</span></span>

<span data-ttu-id="78b96-113">虽然 Teams 的 Web 版本和桌面版几乎相同，但身份验证存在一些差异。</span><span class="sxs-lookup"><span data-stu-id="78b96-113">While the web version and the desktop version of Teams are almost the same, there are some differences concerning authentication.</span></span> <span data-ttu-id="78b96-114">有时，了解所发生事件的唯一方法就是使用 DevTools。</span><span class="sxs-lookup"><span data-stu-id="78b96-114">Sometimes the only way to figure out what is going on is to use the DevTools.</span></span> <span data-ttu-id="78b96-115">若要在桌面客户端使用 DevTools，你必须：</span><span class="sxs-lookup"><span data-stu-id="78b96-115">To use DevTools in the desktop client, you must:</span></span>

1. <span data-ttu-id="78b96-116">确保你已启用 [开发人员预览](~/resources/dev-preview/developer-preview-intro.md)版。</span><span class="sxs-lookup"><span data-stu-id="78b96-116">Ensure you have enabled [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="78b96-117">打开一个选项卡，以便你有一些要检查的 DevTools。</span><span class="sxs-lookup"><span data-stu-id="78b96-117">Open up a tab so you have something to inspect with the DevTools.</span></span>
1. <span data-ttu-id="78b96-118">通过下列方式之一打开 DevTools：</span><span class="sxs-lookup"><span data-stu-id="78b96-118">Open the DevTools in one of the following ways:</span></span>
    * <span data-ttu-id="78b96-119">**Windows：** 在桌面托盘中选择 Teams 图标。</span><span class="sxs-lookup"><span data-stu-id="78b96-119">**Windows**: Select the Teams icon in the desktop tray.</span></span>
    * <span data-ttu-id="78b96-120">**macOS：** 选择扩展坞中的 Teams 图标。</span><span class="sxs-lookup"><span data-stu-id="78b96-120">**macOS**: Select the Teams icon in the Dock.</span></span>
 
   <span data-ttu-id="78b96-121">下图显示了检查选项卡配置对话框中元素的 DevTools：</span><span class="sxs-lookup"><span data-stu-id="78b96-121">The following image shows DevTools inspecting an element in a tab configuration dialog:</span></span>

   ![Tab 和 DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-client"></a><span data-ttu-id="78b96-123">从 Android 客户端访问 DevTools</span><span class="sxs-lookup"><span data-stu-id="78b96-123">Access DevTools from an Android client</span></span>

<span data-ttu-id="78b96-124">还可以从 Teams Android 客户端启用 DevTools。</span><span class="sxs-lookup"><span data-stu-id="78b96-124">You can also enable the DevTools from the Teams Android client.</span></span> <span data-ttu-id="78b96-125">若要启用 DevTools，你必须：</span><span class="sxs-lookup"><span data-stu-id="78b96-125">To enable DevTools, you must:</span></span>

1. <span data-ttu-id="78b96-126">启用 [开发人员预览](~/resources/dev-preview/developer-preview-intro.md)版。</span><span class="sxs-lookup"><span data-stu-id="78b96-126">Enable the [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
1. <span data-ttu-id="78b96-127">将设备连接到台式计算机，并设置 Android 设备进行 [远程调试](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)。</span><span class="sxs-lookup"><span data-stu-id="78b96-127">Connect your device to your desktop computer, and set up your Android device for [remote debugging](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).</span></span>
1. <span data-ttu-id="78b96-128">在 Chrome 浏览器中，打开 `chrome://inspect/#devices` 。</span><span class="sxs-lookup"><span data-stu-id="78b96-128">In your Chrome browser, open `chrome://inspect/#devices`.</span></span>
1. <span data-ttu-id="78b96-129">选择要 **调试** 的选项卡下的"检查"，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="78b96-129">Select **inspect** under the tab you wish to debug, as in the following image:</span></span>

   ![Android DevTools](~/assets/images/android-devtools.png)
