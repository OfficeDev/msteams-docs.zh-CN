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
# <a name="devtools-for-microsoft-teams-tabs"></a>适用于 Microsoft Teams 选项卡的 DevTools

当 Teams 在浏览器中运行时，可以轻松访问浏览器的 DevTools：Windows 上的 F12 或 MacOS 上的 Command-Option-I。 DevTools 使你可以访问：

1. 查看控制台日志。
1. 在运行时查看或修改 HTML、CSS 和网络请求。
1. 将断点添加到 JavaScript 代码并执行交互式调试。

> [!NOTE]
> 启用此功能后，此功能仅在桌面开发者预览版 **Android** 客户端中可用。 有关详细信息，请参阅如何 [启用开发人员预览](~/resources/dev-preview/developer-preview-intro.md)。

## <a name="access-devtools-in-the-desktop"></a>访问桌面版中的 DevTools

虽然 Teams 的 Web 版本和桌面版几乎完全相同，但身份验证方面存在一些差异。 有时，了解所发生事件的唯一方法就是使用 DevTools。 若要在桌面客户端使用 DevTools，你必须：

1. 确保你已启用 [开发人员预览](~/resources/dev-preview/developer-preview-intro.md)版。
1. 打开一个选项卡，以便你有一些要检查的 DevTools。
1. 通过下列方式之一打开 DevTools：
    * **Windows：** 在桌面托盘中选择 Teams 图标。
    * **MacOS：** 选择扩展坞中的 Teams 图标。
 
   下图显示了检查选项卡配置对话框中元素的 DevTools：

   ![Tab 和 DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-client"></a>从 Android 客户端访问 DevTools

还可以从 Teams Android 客户端启用 DevTools。 若要启用 DevTools，你必须：

1. 启用 [开发人员预览](~/resources/dev-preview/developer-preview-intro.md)版。
1. 将设备连接到台式计算机，并设置 Android 设备进行 [远程调试](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)。
1. 在 Chrome 浏览器中，打开 `chrome://inspect/#devices` 。
1. 选择要 **调试** 的选项卡下的"检查"，如下图所示：

   ![Android DevTools](~/assets/images/android-devtools.png)
