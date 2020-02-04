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
# <a name="devtools-for-microsoft-teams-tabs"></a>Microsoft 团队选项卡的 DevTools

当工作组在浏览器中运行时，很容易访问浏览器的 DevTools： F12 （在 Windows 中）或命令-Option-I （在 MacOS 上）。 DevTools 使您可以访问：

1. 查看控制台日志。
1. 在运行时查看/修改 html、css 和网络请求。
1. 将断点添加到 JavaScript 代码，并执行交互式调试。

仅在启用开发人员预览版后，桌面和 Android 客户端中才会提供此功能。 有关详细信息，请参阅[如何启用开发人员预览](~/resources/dev-preview/developer-preview-intro.md)。

## <a name="accessing-devtools-in-the-desktop"></a>访问桌面中的 DevTools

虽然团队的 web 版本和团队的桌面版本几乎完全相同，但在某些方面存在差异，尤其是对于身份验证。 有时，确定要执行的操作的唯一方法是使用 DevTools。 下面介绍了如何从团队桌面客户端获取它们。 在桌面客户端中使用 DevTools：

1. 请确保已启用[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)
1. 打开 "选项卡"，让您有一些要使用 DevTools 检查的内容。
1. 打开 DevTools
    * 在 Windows 中，你可以通过桌面托盘中的 Microsoft 团队图标打开 DevTools：

  ![右键单击打开 DevTools](~/assets/images/dev-preview/devtools-right-click.png)

    * 在 MacOS 上，单击插接中的 "Microsoft 团队" 图标。

以下是在打开 DevTools 并选择一个元素时的示例选项卡的外观：

![Tab 和 DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a>从 Android 客户端访问 DevTools

您还可以从 "团队 Android 客户端" 启用 DevTools。 为此，请执行以下操作：

1. 请确保已启用[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)
1. 将设备连接到桌面计算机，并将您的 Android 设备设置为进行[远程调试](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. 在 Chrome 浏览器中， `chrome://inspect/#devices`打开。
1. 在您希望调试的选项卡下方单击 "**检查**"，如下面的屏幕截图所示。

![Android DevTools](~/assets/images/android-devtools.png)
