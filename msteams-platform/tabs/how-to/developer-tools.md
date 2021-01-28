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
# <a name="devtools-for-microsoft-teams-tabs"></a>适用于 Microsoft Teams 选项卡的 DevTools

当 Teams 在浏览器中运行时，可以轻松访问浏览器的 DevTools：Windows (上的 F12) 或 MacOS (上的 Command-Option-I) 。 DevTools 使你可以访问：

1. 查看控制台日志。
1. 在运行时查看/修改 html、css 和网络请求。
1. 将断点添加到 JavaScript 代码，并执行交互式调试。

此功能仅在启用此功能后在桌面开发者预览版 Android 客户端中可用。 有关详细信息 [，请参阅开发者预览版](~/resources/dev-preview/developer-preview-intro.md) 启用该设置。

## <a name="accessing-devtools-in-the-desktop"></a>访问桌面版中的 DevTools

虽然 Teams 的 Web 版本和团队的桌面版本几乎完全相同，但存在一些差异，尤其是在身份验证方面。 有时，确定发生事件的唯一方法就是使用 DevTools。 下面将了解如何从 Teams 桌面客户端访问它们。 若要在桌面客户端中使用 DevTools：

1. 确保已启用开发人员 [预览](~/resources/dev-preview/developer-preview-intro.md)
1. 打开一个选项卡，以便使用 DevTools 检查某些内容。
1. 打开 DevTools
    * 在 Windows 上，通过桌面托盘中的 Microsoft Teams 图标打开 DevTools：

  ![右键单击以打开 DevTools](~/assets/images/dev-preview/devtools-right-click.png)

    * 在 MacOS 上，单击扩展坞中的 Microsoft Teams 图标。

下面是打开 DevTools 并选中元素后的示例选项卡的外观：

![Tab 和 DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a>从 Android 客户端访问 DevTools

还可以从 Teams Android 客户端启用 DevTools。 为此，请执行以下操作：

1. 确保已启用开发人员 [预览](~/resources/dev-preview/developer-preview-intro.md)
1. 将设备连接到台式计算机，并设置 Android 设备进行 [远程调试](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. 在 Chrome 浏览器中，打开 `chrome://inspect/#devices` 。
1. 单击 **要** 调试的选项卡下方的"检查"，如下面的屏幕截图所示。

![Android DevTools](~/assets/images/android-devtools.png)
