---
title: 适用于 Microsoft Teams 选项卡的 DevTools
description: 介绍如何在使用桌面客户端和调试Microsoft Teams访问 DevTools
ms.localizationpriority: medium
ms.topic: how-to
keywords: devtools 调试移动部件版式桌面客户端开发人员工具选项卡
ms.openlocfilehash: bec7b94b1db2492de9eaaa38ff62c0783c972f6e
ms.sourcegitcommit: d9daad3d5818d5774911b96fdc7bde45b04c9908
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2022
ms.locfileid: "64511214"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>适用于 Microsoft Teams 选项卡的 DevTools

当Teams运行时，可以轻松访问浏览器的 DevTools：Windows MacOS 上的 Command-Option-I。 DevTools 使你可以访问：

1. 查看控制台日志。
1. 在运行时查看或修改 HTML、CSS 和网络请求。
1. 将断点添加到 JavaScript 代码并执行交互式调试。

> [!NOTE]
> 启用此功能后，此功能仅适用于桌面 **开发者预览版 Android 客户端** 。 有关详细信息，请参阅启用[如何实现预览。](~/resources/dev-preview/developer-preview-intro.md)

## <a name="access-devtools-on-the-desktop"></a>访问桌面上的 DevTools

尽管 Web 版本和桌面版本的 Teams几乎相同，但身份验证存在一些差异。 有时，了解所发生事件的唯一方法就是使用 DevTools。 若要在桌面客户端使用 DevTools，你必须：

1. 确保已启用开发人员 [预览](~/resources/dev-preview/developer-preview-intro.md)。
1. 打开一个选项卡，以便你有一些要检查的 DevTools。
1. 打开 DevTools 以下方法之一：
    * 在Windows，通过桌面托盘中的Microsoft Teams图标打开 DevTools。

      :::image type="content" source="../../assets/images/dev-preview/devtools-right-click.png" alt-text="developer-tool-windows":::

    * 在 MacOS 上，选择Microsoft Teams扩展坞中的"选项"图标。

      :::image type="content" source="../../assets/images/dev-preview/mac-os-developer-tools.PNG" alt-text="mac-os-dev-tools":::

以下示例显示 DevTools 打开并检查选项卡配置对话框：

   [![Tab 和 DevTools](~/assets/images/dev-preview/tab-and-devtools.png)](~/assets/images/dev-preview/tab-and-devtools.png#lightbox)

## <a name="access-devtools-from-an-android-device"></a>从 Android 设备访问 DevTools

还可以从 Android 客户端启用 Teams工具。 若要启用 DevTools，你必须：

1. 启用 [开发人员预览](~/resources/dev-preview/developer-preview-intro.md)。
1. 连接设备连接到台式计算机，并设置 Android 设备进行[远程调试](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)。
1. 在 Chrome 浏览器中，打开 `chrome://inspect/#devices`。
1. 选择要 **调试** 的选项卡下的"检查"，如下图所示：

   ![Android DevTools](~/assets/images/android-devtools.png)
