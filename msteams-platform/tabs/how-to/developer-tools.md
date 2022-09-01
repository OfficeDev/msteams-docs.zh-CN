---
title: 适用于 Microsoft Teams 选项卡的 DevTools
description: 在本模块中，了解如何在使用 Microsoft Teams 桌面客户端和调试时访问 DevTools
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: a0d5e3ea15fd796c2c426f1cf1457171f0abe7b2
ms.sourcegitcommit: 024be23411bc0f2573d19f48f9266021f9b76f0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2022
ms.locfileid: "67488269"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>适用于 Microsoft Teams 选项卡的 DevTools

当 Teams 在浏览器中运行时，可以轻松访问浏览器的 DevTools：Windows 上的 F12 或 MacOS 上的 Command-Option-I。 DevTools 允许你访问：

1. 查看控制台日志。
1. 在运行时查看或修改 HTML、CSS 和网络请求。
1. 将断点添加到 JavaScript 代码并执行交互式调试。

> [!NOTE]
> 该功能仅在启用 **开发人员预览** 后才可用于桌面和 Android 客户端。 有关详细信息，请参阅[如何启用开发人员预览](~/resources/dev-preview/developer-preview-intro.md)。

## <a name="access-devtools-on-the-desktop"></a>在桌面上访问 DevTools

虽然 Web 版本和桌面版本的 Teams 几乎完全相同，但身份验证方面存在一些差异。 有时，了解运行情况的唯一方法是使用 DevTools。 若要在桌面客户端中使用 DevTools，必须：

1. 确保已启用 [开发人员预览](~/resources/dev-preview/developer-preview-intro.md)。
1. 打开一个选项卡，以便使用 DevTools 进行检查。
1. 通过以下方式之一打开 DevTools：
    * 在 Windows 中，可以通过桌面托盘中的 Microsoft Teams 图标打开 DevTools。

      :::image type="content" source="../../assets/images/dev-preview/devtools-right-click.png" alt-text="developer-tool-windows":::

    * 在 MacOS 中，选择 Dock 中的 Microsoft Teams 图标。

      :::image type="content" source="../../assets/images/dev-preview/mac-os-developer-tools.PNG" alt-text="mac-os-dev-tools":::

以下示例显示 DevTools 已打开并正在检查选项卡配置对话框：

   [![选项卡和 DevTools](~/assets/images/dev-preview/tab-and-devtools.png)](~/assets/images/dev-preview/tab-and-devtools.png#lightbox)

## <a name="access-devtools-from-an-android-device"></a>从 Android 设备访问 DevTools

还可以从 Teams Android 客户端启用 DevTools。 若要启用 DevTools，必须：

1. 启用[开发人员预览](~/resources/dev-preview/developer-preview-intro.md)。
1. 将设备连接到桌面计算机，并将 Android 设备设置为用于[远程调试](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)。
1. 在 Chrome 浏览器中，打开 `chrome://inspect/#devices`。
1. 选择要调试的选项卡下的 **检查** ，如下图所示：

   ![Android DevTools](~/assets/images/android-devtools.png)

## <a name="see-also"></a>另请参阅

[清除 Teams 客户端缓存](/microsoftteams/troubleshoot/teams-administration/clear-teams-cache)
