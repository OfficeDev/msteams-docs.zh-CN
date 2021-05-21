---
title: 移动设备上的选项卡
description: 介绍设计适用于移动设备的选项卡的指南。
ms.topic: conceptual
localization_priority: Normal
keywords: teams 设计指南参考框架个人应用移动应用选项卡
ms.openlocfilehash: 853ab2c52edd1f4faedcc92e6f0e8d0821b580c7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566696"
---
# <a name="tabs-on-mobile"></a>移动设备上的选项卡

你可以将选项卡包括在Teams、聊天和个人应用中。

## <a name="accessing-personal-tabs"></a>访问个人选项卡

你可以访问应用箱中的个人选项卡。

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="插图显示Teams移动应用箱。" border="false":::

## <a name="accessing-channel-tabs"></a>访问频道选项卡

可以通过选择频道或已添加这些选项卡的聊天中的"更多"按钮来访问频道和组选项卡。

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="显示移动Teams的图示。" border="false":::

## <a name="design-considerations"></a>设计注意事项

我们的移动平台允许应用成为沉浸式体验，其中应用内容从主导航导航Teams屏幕。 若要创建适合你的体验的沉浸Teams，请遵循以下指南。

### <a name="responsive-design"></a>响应式设计

由于你的选项卡可以在具有各种屏幕大小的设备上打开，它需要遵循 [响应式设计](https://www.w3schools.com/html/html_responsive.asp) 原则。 所有关键构造都应可在移动设备上访问，并且不应使视图失真。 确保在移动设备上加载选项卡时，所有按钮和链接都可以通过基于手指的导航轻松访问。

### <a name="layouts"></a>布局

为选项卡选择正确的布局非常重要。 你应该考虑你呈现的信息类型，并选择一个布局来组织这些信息以方便使用。 下面概述了一些潜在的选项。

#### <a name="single-canvas"></a>单画布

这是完成工作的一个大区域。 Wiki Teams应用遵循此模式。 如果你的应用不将内容分为较小的组件，这非常适合。

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="显示移动Teams画布选项卡的图示。" border="false":::

#### <a name="list"></a>列表

列表对于对大量的数据进行排序和筛选都十分重要，并且非常能将最重要的内容放在最上面。 使用可排序列非常有用。 可以将操作添加到省略号菜单下的每个列表项。

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="显示&quot;移动Teams选项卡的图示。" border="false":::

#### <a name="grid"></a>网格

网格对于显示高度可视的元素非常有用。 这有助于在顶部包含筛选器或搜索控件。

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="插图显示一Teams网格布局的移动设备选项卡。" border="false":::

### <a name="tabs-with-bots-on-mobile"></a>在移动设备上使用机器人的选项卡

以下示例是包含选项卡和自动程序的个人应用：

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="插图显示移动设备Teams选项卡和自动程序的应用。" border="false":::

## <a name="ui-components"></a>UI 组件

### <a name="color-palettes"></a>调色板

将已批准的中性调色板用于背景、通知、文本和按钮将有助于你的应用在Teams。 由于Teams手机具有 (浅色和深色) 主题，因此，建议确保你的应用在两者中都外观良好。

#### <a name="light-color"></a>浅色

![浅色调色板](../../assets/images/light-color.png)

#### <a name="dark-color"></a>深色

![深色调色板](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a>按钮和控件

设置按钮样式的方式有助于传达它们触发的操作类型。 我们保留各种按钮，这些按钮经过格式化以显示不同级别的强调。 按钮可以有文本、图标或文本和图标的组合。 为了传达层次结构中的不同级别，我们设计了每个类别中的主按钮和辅助按钮。

#### <a name="buttons"></a>按钮

主按钮和辅助按钮。

![按钮图像](../../assets/images/buttons.png)

#### <a name="selection-controls"></a>选择控件

单选按钮、复选框和切换。

![选择控件](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a>小红包和装饰

![一些子项目](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a>版式

版式应清晰且有目的。 强调重要信息并避免使用多个字体和大小以减少混淆。 我们建议使用句大小写，并避免使用全部大写字母进行本地化和易读。

![移动版式](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a>字段和飞出

字段是用户可以输入文本的区域。 弹出框比对话框更轻量，并且从顶部窗格中显示。

#### <a name="list-controls"></a>列出控件

![移动列表控件](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a>字段控件

![移动字段控件](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a>开发人员注意事项

生成包含选项卡的应用时，需要考虑 (和测试) 在 Android 和 iOS Microsoft Teams上如何工作。 以下各节概述了需要考虑的一些关键方案。

### <a name="authentication"></a>身份验证

若要在移动客户端上进行身份验证，必须将 JavaScript SDK Teams至少升级到版本 1.4.1。

### <a name="low-bandwidth-and-intermittent-connections"></a>低带宽和间歇性连接

移动客户端经常需要在低带宽和间歇性连接下运行。 应用应该通过向用户提供上下文消息来适当地处理任何超时。 您还应使用用户进度指示器，以针对任何长时间运行的过程向用户提供反馈。

> [!NOTE]
> 只有在根据审批团队的输入将应用程序添加到允许列表后，才能在移动设备上启用选项卡。 要检查移动响应，请联系 teamsubm@microsoft.com。

### <a name="testing-on-mobile-clients"></a>在移动客户端上测试

需要验证选项卡在各种大小和质量的移动设备上是否正常工作。 对于 Android 设备，可以在选项卡运行时使用 [DevTools](~/tabs/how-to/developer-tools.md) 调试选项卡。 建议在高性能和低性能设备（包括平板电脑）上进行测试。

### <a name="distribution"></a>分发

应用商店中列出的Teams必须经过批准，供移动使用，以在移动Teams正常运行。 选项卡可用性和行为取决于你的应用是否已获得批准。

#### <a name="apps-on-teams-store-approved-for-mobile"></a>经批准Teams移动的应用商店上的应用

下表介绍了当应用在应用商店中列出并批准Teams时选项卡可用性和行为：

|功能   |移动可用性？   |移动行为|
|----------|-----------|------------|
|频道 <br /> 和组选项卡|是|选项卡使用Teams在移动客户端中 `contentUrl` 打开。|
|个人应用|是|"个人应用"选项卡中的每个选项卡使用各自的Teams在移动客户端中 `contentUrl` 打开。|

#### <a name="apps-on-teams-store-not-approved-for-mobile"></a>未批准Teams移动的应用商店上的应用

下表介绍了当应用在应用商店中列出但Teams未批准的移动用途时选项卡可用性和行为：

| 功能 | 移动可用性？ | 移动行为 |
|----------|-----------|------------|
|"频道和组"选项卡|是|选项卡将在设备的默认浏览器中打开，而不是Teams应用的配置（还必须包含在源代码的 函数中）中的移动 `websiteUrl` `setSettings()` [客户端](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true)。 但是，用户仍可在移动客户端Teams选项卡，方法为选择应用旁边的"更多"并选择"打开"，这将触发应用的 `contentUrl` 配置。|
|个人应用|不支持|不适用|

#### <a name="apps-not-on-teams-store"></a>不在应用商店Teams应用

如果要将应用旁加载或发布到组织的应用程序目录，选项卡行为将Teams Microsoft 批准的移动应用商店应用的行为相同。
