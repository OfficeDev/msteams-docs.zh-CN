---
title: 适用于 Microsoft Teams 选项卡的 DevTools
description: 介绍如何在使用 Microsoft Teams 桌面客户端时访问 DevTools
ms.topic: how-to
keywords: devtools 调试移动部件版式桌面客户端开发人员工具
ms.openlocfilehash: 1bf7d246136a24316309ae144ac9552c5fd4f57d
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596271"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>适用于 Microsoft Teams 选项卡的 DevTools

当 Teams 在浏览器中运行时，可以轻松访问浏览器的 DevTools：Windows (上的 F12) 或 MacOS (上的 Command-Option-I) 。 DevTools 使你可以访问：

1. 查看控制台日志。
1. 在运行时查看/修改 html、css 和网络请求。
1. 将断点添加到 JavaScript 代码，并执行交互式调试。

启用此功能后，此功能仅在桌面和 Android 开发者预览版可用。 有关详细信息 [，请参阅开发者预览版](~/resources/dev-preview/developer-preview-intro.md) 启用该设置。

## <a name="accessing-devtools-in-the-desktop"></a>访问桌面版中的 DevTools

虽然 Teams 的 Web 版本和桌面版团队几乎完全相同，但存在一些差异，尤其是在身份验证方面。 有时，了解所发生事件的唯一方法就是使用 DevTools。 下面将了解如何从 Teams 桌面客户端访问它们。 若要在桌面客户端使用 DevTools：

1. 确保已启用开发人员 [预览](~/resources/dev-preview/developer-preview-intro.md)
1. 打开一个选项卡，以便你有一些要检查的 DevTools。
1. 打开 DevTools 以下方法之一：
    * **Windows：** 在桌面托盘中选择 Teams 图标。
    * **macOS：** 选择扩展坞中的 Teams 图标。

以下屏幕截图显示了检查选项卡配置对话框中元素的 DevTools：

![Tab 和 DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a>从 Android 客户端访问 DevTools

还可以从 Teams Android 客户端启用 DevTools。

1. 确保已启用开发人员 [预览](~/resources/dev-preview/developer-preview-intro.md)
1. 将设备连接到台式计算机，并设置 Android 设备进行 [远程调试](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. 在 Chrome 浏览器中，打开 `chrome://inspect/#devices` 。
1. 单击 **要** 调试的选项卡下方的"检查"，如下面的屏幕截图所示。

![Android DevTools](~/assets/images/android-devtools.png)
