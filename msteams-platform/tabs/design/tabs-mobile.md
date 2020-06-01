---
title: 移动设备上的选项卡
description: 介绍设计适用于移动设备的选项卡的指南。
keywords: 团队设计准则参考框架个人应用移动选项卡
ms.openlocfilehash: 6fe40b9cc5b6e898d0f0bce14b3dfedfd2c14032
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/31/2020
ms.locfileid: "44455518"
---
# <a name="tabs-on-mobile"></a>移动设备上的选项卡

自定义选项卡可以是频道、组聊天或个人应用（包含静态选项卡和/或一对一 bot 的应用程序）的一部分。

应用程序抽屉中的移动客户端提供了个人应用程序。 只能从桌面或 web 客户端安装应用程序，并且在移动客户端上可能需要长达24小时才能显示该应用程序。

组和频道选项卡也在移动客户端上可用。 默认行为是使用 `websiteUrl` ，在浏览器窗口中启动您的选项卡。 但是，可以通过单击选项卡旁边的 "溢出" 菜单，然后选择 "打开"，在移动客户端上加载这些用户 `...` ，这将使用您在**Open** `contentUrl` 团队移动客户端内加载该选项卡。

![移动应用程序抽屉](../../assets/images/personal-app-mobile.png)

## <a name="developer-considerations-for-mobile-support"></a>移动支持的开发人员注意事项

在构建包含选项卡的应用程序时，需要考虑（并测试）选项卡在 Android 和 iOS Microsoft 团队客户端上的工作方式。 以下各节概述了您需要考虑的一些关键方案。

### <a name="testing-on-mobile-clients"></a>在移动客户端上进行测试

您需要验证您的选项卡在各种大小和质量的移动设备上是否正常工作。 对于 Android 设备，您可以使用[DevTools](~/tabs/how-to/developer-tools.md)在选项卡运行时对其进行调试。 我们建议您在高性能和低性能的设备以及平板电脑上进行测试。

### <a name="responsive-design"></a>响应式设计

由于您的选项卡可以在屏幕大小范围很广的设备上打开，因此它需要遵循[快速响应设计](https://www.w3schools.com/html/html_responsive.asp)原则。 所有关键构造在移动设备上都应该是可访问的，并且这些视图不应失真。 确保在移动设备上加载选项卡时，可以使用基于手指的导航轻松访问所有按钮和链接。

### <a name="authentication"></a>身份验证

若要使身份验证在移动客户端上运行，您必须将团队 JS SDK 升级到至少版本1.4.1。

### <a name="low-bandwidth--intermittent-connections"></a>低带宽 & 间歇连接

移动客户端需要在低带宽和间歇性连接中正常运行。 您的应用程序应通过向用户提供上下文相关消息来适当地处理任何超时。 此外，还应为用户提供对任何长时间运行的进程的反馈的用户进度指示器。

## <a name="design-considerations-for-mobile"></a>移动的设计注意事项

通过我们的移动平台，应用可以成为一种沉浸式体验，其中的应用程序内容除了主要团队导航之外，其他所有屏幕都占据了整个屏幕。 若要创建在 Microsoft 团队客户端无缝适应的沉浸式体验，请遵循以下准则。

### <a name="layouts"></a>布局

为选项卡选择正确的布局非常重要。 您应考虑正在呈现的信息的类型，并选择一个布局来组织它以方便使用。 下面概述了一些可能的选项。

#### <a name="single-canvas"></a>单个画布

这是工作完成的一个大型区域。 Wiki 应用遵循此模式。 如果您的应用程序不将内容分隔为较小的组件，这就是理想之地。

![单个画布布局](~/assets/images/mobile-single-canvas.png)

#### <a name="list"></a>列表

列表非常适合于对大量数据进行排序和筛选，并且非常适合在顶部保留最重要的内容。 使用可排序列非常有用。 可以将操作添加到省略号菜单下的每个列表项。

![列表布局](~/assets/images/mobile-list.png)

#### <a name="grid"></a>窗格

网格对于显示高度直观的元素很有用。 它有助于在顶部添加筛选器或搜索控件。

![网格布局](~/assets/images/mobile-grid.png)

### <a name="tabs-with-bots-on-mobile"></a>移动设备上带有 bot 的选项卡

下面是一个包含两个静态选项卡和一个 bot 的个人应用示例。

![移动设备上的选项卡和 bot](~/assets/images/mobile-tab-with-bot.png)

### <a name="ui-components"></a>UI 组件

#### <a name="color-palettes"></a>调色板

使用我们为背景、通知、文本和按钮提供的已批准中性调色板，可帮助你的应用程序在团队家庭中更好地感觉。 由于团队 mobile 具有两种颜色主题（浅色和深色），因此最好确保您的应用程序在这两个方面看起来非常出色。

##### <a name="light-color"></a>浅色

![浅色调色板](~/assets/images/light-color.png)

##### <a name="dark-color"></a>深颜色

![深色调色板](~/assets/images/dark-color.png)

#### <a name="buttons-and-controls"></a>按钮和控件

按钮的样式方式有助于传达它们触发的操作类型。 我们维护各种格式的按钮，以显示不同的强调级别。 按钮可以有文本、图标或文本和图标的组合。 为了在层次结构中传达不同的级别，我们为每个类别中的主要和辅助按钮设计。

![按钮](~/assets/images/buttons.png)

![选择控件](~/assets/images/selection-controls.png)

![chiclets 和 pills](~/assets/images/chiclets-and-pills.png)

#### <a name="typography"></a>版式

版式应清晰和故意。 强调重要信息并避免使用多种字体和大小，以减少混淆。 我们建议使用句子事例，避免使用所有大写字母以实现本地化和可读性。

![移动 typograph](~/assets/images/mobile-typography.png)

#### <a name="fields-and-flyouts"></a>字段和浮出控件

字段是用户可以在其中输入文本的区域。 Flyouts 比对话框更轻便，显示在顶部窗格中。

##### <a name="list-controls"></a>列出控件

![移动列表控件](~/assets/images/mobile-list-controls.png)

##### <a name="field-controls"></a>字段控件

![移动字段控件](~/assets/images/mobile-field-controls.png)
