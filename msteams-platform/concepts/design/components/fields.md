---
title: 设计准则参考
description: 介绍在应用程序中使用字段和 flyouts 的准则
keywords: 团队设计准则引用组件字段和 flyouts
ms.openlocfilehash: 0f62d38bf961ae79b05c599638cefb3c76f46ed4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673425"
---
# <a name="fields-and-flyouts"></a>字段和 flyouts

---

## <a name="fields"></a>Fields

字段是用户可以在其中输入文本的区域。

### <a name="padding-and-size"></a>填充和大小

单行文本字段是32的固定高度，以匹配其他组件的高度。 一些文本字段（如 "说明" 字段）可能会垂直增加以允许更多的文本。
[!include[Padding and size](~/includes/design/fields-image-padding.html)]

### <a name="states"></a>市

这些是文本字段的状态。 文本字段存在于不同的状态中。 我们有专用于九种可能的方案的特定设计，包括（从上到下）：静止文本字段、焦点上的键盘以及字段中的光标、在焦点内输入文本的键盘、错误处理已成功、错误处理已成功、明文字段（包括 X 图标）、搜索字段（包括搜索图标）、加载字段和禁用的字段。
[!include[Field states](~/includes/design/fields-image-states.html)]

### <a name="formatting-help-text-and-labels"></a>设置帮助文本和标签的格式

字段可以包含占位符文本，以提供所需的信息类型的示例。 他们还可以保留为用户提供更多上下文的标签。 在字段中，文本应始终左对齐。 我们也在这里使用句子大小写。

我们将 Microsoft Yahei UI 常规的12磅（caption）和 $app-灰色-02 用于标签。 对于 "帮助" 文本，我们使用的是 14 pt （base）和 $app-灰阶-02 的 Microsoft Yahei UI。
[!include[Fields typography](~/includes/design/fields-image-typography.html)]

---

## <a name="flyouts"></a>Flyouts

Flyouts 比对话框更轻便，可以快速消除。 它们可以包含按钮、字段和其他组件。
[!include[Flyouts](~/includes/design/flyouts-image.html)]

### <a name="sizing-and-padding"></a>调整大小和填充

我们建议将16px 填充到内容的左侧和右侧。
[!include[Flyouts size and padding](~/includes/design/flyouts-image-sizepadding.html)]

### <a name="placement"></a>Placement

Flyouts 是上下文，应放置在触发它的元素的上方、下方或旁边。

### <a name="scrolling"></a>上下

标头保留在位置，以便为要滚动的内容提供上下文。
[!include[Flyouts scrolling](~/includes/design/flyouts-image-scrolling.html)]

## <a name="mobile"></a>移动设备

字段是接受用户输入的文本输入框。 飞出菜单是显示在顶部窗格中的水平弹出窗口，可用于显示有关项目的更多详细信息。

### <a name="field-controls"></a>字段控件

[!include[Mobile fields](~/includes/design/fields-mobile-image.html)]

### <a name="flyout-menu-list-controls"></a>浮出菜单列表控件

[!include[Mobile flyout menu controls](~/includes/design/flyout-menu-mobile-image.html)]
