---
title: 适用于 Microsoft Teams 选项卡的 DevTools
description: 介绍如何在使用桌面客户端时Microsoft Teams DevTools
localization_priority: Normal
ms.topic: how-to
keywords: devtools 调试移动部件版式桌面客户端开发人员工具
ms.openlocfilehash: 8cc881af102810744dfaf0ee3de077da5d40671068ab319575518f8978e5f791
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2021
ms.locfileid: "57701824"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>适用于 Microsoft Teams 选项卡的 DevTools

当Teams中运行时，可以轻松访问浏览器的 DevTools： F12 on Windows 或 Command-Option-I on MacOS。 DevTools 使你可以访问：

1. 查看控制台日志。
1. 在运行时查看或修改 HTML、CSS 和网络请求。
1. 将断点添加到 JavaScript 代码并执行交互式调试。

> [!NOTE]
> 启用此功能后，此功能仅适用于桌面开发者预览版 **Android** 客户端。 有关详细信息，请参阅如何 [启用开发人员预览](~/resources/dev-preview/developer-preview-intro.md)。

## <a name="access-devtools-on-the-desktop"></a>访问桌面上的 DevTools

虽然 Web 版本和桌面版本的 Teams几乎相同，但身份验证存在一些差异。 有时，了解所发生事件的唯一方法就是使用 DevTools。 若要在桌面客户端使用 DevTools，你必须：

1. 确保你已启用 [开发人员预览](~/resources/dev-preview/developer-preview-intro.md)版。
1. 打开一个选项卡，以便你有一些要检查的 DevTools。
1. 打开 DevTools 以下方法之一：
    * 在Windows，通过桌面托盘中的Microsoft Teams图标打开 DevTools：<br>
  ![右键单击以打开 DevTools](~/assets/images/dev-preview/devtools-right-click.png)
    * 在 MacOS 上，单击扩展Microsoft Teams图标。

以下示例显示 DevTools 打开并检查选项卡配置对话框：

   ![Tab 和 DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-device"></a>从 Android 设备访问 DevTools

还可以从 Android 客户端启用 Teams工具。 若要启用 DevTools，你必须：

1. 启用 [开发人员预览](~/resources/dev-preview/developer-preview-intro.md)版。
1. 连接设备连接到台式计算机，并设置 Android 设备进行[远程调试](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)。
1. 在 Chrome 浏览器中，打开 `chrome://inspect/#devices` 。
1. 选择要 **调试** 的选项卡下的"检查"，如下图所示：

   ![Android DevTools](~/assets/images/android-devtools.png)
