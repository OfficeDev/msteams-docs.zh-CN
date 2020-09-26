---
title: 移动设备上的选项卡
description: 介绍设计适用于移动设备的选项卡的指南。
keywords: 团队设计准则参考框架个人应用移动选项卡
ms.openlocfilehash: a1939465b04a1fe4b803efaf83402852ca536059
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279792"
---
# <a name="tabs-on-mobile"></a>移动设备上的选项卡

> [!NOTE]
> 如果选择在工作组移动客户端上显示 "频道/组" 选项卡，则该 `setSettings()` 配置必须具有该属性的值 `websiteUrl` (请参阅下) 。

自定义选项卡可以是频道、组聊天或个人应用 (包含静态选项卡和/或一对一机器人) 的应用程序的一部分。

应用程序抽屉中的移动客户端提供了个人应用程序。 只能从桌面或 web 客户端安装应用程序，并且在移动客户端上可能需要长达24小时才能显示该应用程序。

移动设备上也提供频道选项卡。 默认行为是使用 `websiteUrl` ，在浏览器窗口中启动您的选项卡。 但是，可以通过单击选项卡旁边的 "溢出" 菜单，然后选择 "打开"，在移动客户端上加载这些用户 `...` ，这将使用您在**Open** `contentUrl` 团队移动客户端内加载该选项卡。

## <a name="accessing-personal-tabs"></a>访问个人选项卡

下图显示了如何在移动设备上访问个人选项卡。

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="显示团队移动应用程序抽屉的图示。" border="false":::

## <a name="accessing-channel-tabs"></a>访问频道选项卡

下图显示了如何访问移动设备上的 "频道" 选项卡。

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="显示 "工作组移动" 选项卡的图示。" border="false":::

## <a name="design-considerations"></a>设计注意事项

通过我们的移动平台，应用可以成为一种沉浸式体验，其中的应用程序内容除了主要团队导航之外，其他所有屏幕都占据了整个屏幕。 若要创建适合团队的沉浸式体验，请遵循以下准则。

### <a name="responsive-design"></a>响应式设计

由于您的选项卡可以在屏幕大小范围很广的设备上打开，因此它需要遵循 [快速响应设计](https://www.w3schools.com/html/html_responsive.asp) 原则。 所有关键构造在移动设备上都应该是可访问的，并且这些视图不应失真。 确保在移动设备上加载选项卡时，可以使用基于手指的导航轻松访问所有按钮和链接。

### <a name="layouts"></a>布局

为选项卡选择正确的布局非常重要。 您应考虑正在呈现的信息的类型，并选择一个布局来组织它以方便使用。 下面概述了一些可能的选项。

#### <a name="single-canvas"></a>单个画布

这是工作完成的一个大型区域。 团队 Wiki 应用程序遵循此模式。 如果您的应用程序不将内容分隔为较小的组件，这就是理想之地。

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="显示 "团队移动单个画布" 选项卡的图示。" border="false":::

#### <a name="list"></a>列表

列表非常适合于对大量数据进行排序和筛选，并且非常适合在顶部保留最重要的内容。 使用可排序列非常有用。 可以将操作添加到省略号菜单下的每个列表项。

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="显示团队移动列表选项卡的图示。" border="false":::

#### <a name="grid"></a>窗格

网格对于显示高度直观的元素很有用。 它有助于在顶部添加筛选器或搜索控件。

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="图示显示了具有网格布局的 "工作组移动" 选项卡。" border="false":::

### <a name="tabs-with-bots-on-mobile"></a>移动设备上带有 bot 的选项卡

下面的示例是包含选项卡和机器人的个人应用程序。

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="展示了具有选项卡和 bot 的移动团队应用程序的图示。" border="false":::

## <a name="ui-components"></a>UI 组件

### <a name="color-palettes"></a>调色板

使用我们为背景、通知、文本和按钮提供的已批准中性调色板，可帮助你的应用程序在团队家庭中更好地感觉。 由于团队 mobile 有两个颜色主题 (浅色和深色) ，因此最好确保您的应用程序在这两个方面看起来非常出色。

#### <a name="light-color"></a>浅色

![浅色调色板](../../assets/images/light-color.png)

#### <a name="dark-color"></a>深颜色

![深色调色板](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a>按钮和控件

按钮的样式方式有助于传达它们触发的操作类型。 我们维护各种格式的按钮，以显示不同的强调级别。 按钮可以有文本、图标或文本和图标的组合。 为了在层次结构中传达不同的级别，我们为每个类别中的主要和辅助按钮设计。

#### <a name="buttons"></a>按钮

主要和次要按钮。

![按钮图像](../../assets/images/buttons.png)

#### <a name="selection-controls"></a>选择控件

单选按钮、复选框和切换。

![选择控件](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a>Chiclets 和 pills

![chiclets 和 pills](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a>版式

版式应清晰和故意。 强调重要信息并避免使用多种字体和大小，以减少混淆。 我们建议使用句子事例，避免使用所有大写字母以实现本地化和可读性。

![移动 typograph](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a>字段和 flyouts

字段是用户可以在其中输入文本的区域。 Flyouts 比对话框更轻便，并显示在顶部窗格中。

#### <a name="list-controls"></a>列出控件

![移动列表控件](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a>字段控件

![移动字段控件](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a>开发人员注意事项

在构建包含选项卡的应用程序时，需要考虑 (并测试您的选项卡在 Android 和 iOS Microsoft 团队客户端上将如何运行的) 。 以下各节概述了您需要考虑的一些关键方案。

### <a name="testing-on-mobile-clients"></a>在移动客户端上进行测试

您需要验证您的选项卡在各种大小和质量的移动设备上是否正常工作。 对于 Android 设备，您可以使用 [DevTools](~/tabs/how-to/developer-tools.md) 在选项卡运行时对其进行调试。 我们建议您在高性能和低性能的设备以及平板电脑上进行测试。

### <a name="authentication"></a>身份验证

若要使身份验证在移动客户端上运行，您必须将 JavaScript SDK 升级到至少1.4.1 版本。

### <a name="low-bandwidth-and-intermittent-connections"></a>低带宽和间歇性连接

移动客户端需要在低带宽和间歇性连接中正常运行。 您的应用程序应通过向用户提供上下文相关消息来适当地处理任何超时。 此外，还应为用户提供对任何长时间运行的进程的反馈的用户进度指示器。
