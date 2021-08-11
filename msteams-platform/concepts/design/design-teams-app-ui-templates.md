---
title: 使用 UI 模板设计应用
author: heath-hamilton
description: 使用通常在整个应用中看到的标准化 UI 组件、布局和模式更快地Microsoft Teams。
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 7d46829be50e6c88dc7629376437878a4b5fecf93d82e805a12093c96b3677ba
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2021
ms.locfileid: "57702842"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>使用 UI Microsoft Teams设计应用

使用 UI Microsoft Teams更快地设计应用。 这些模板是一组基于 ui Fluent的组件的集合，这些组件适用于常见Teams用例，让你有更多的时间来为用户找到最佳体验。

## <a name="getting-started-with-tools-and-samples"></a>工具和示例入门

以下资源可帮助你使用 UI 模板设计和开发应用。

### <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

从应用 UI 工具包中为应用设计获取 UI 模板Microsoft Teams，其中还包括有关用法、结构分析、辅助功能和最佳做法的广泛信息。

> [!div class="nextstepaction"]
> [获取图 (UI) ](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft TeamsUI 库

在浏览器中查看和测试Teams UI 模板和相关组件。

> [!div class="nextstepaction"]
> [尝试 UI 库 (场) ](https://dev-int.teams.microsoft.com/storybook/main/index.html)

将这些模板和相关组件直接导入到Teams应用项目中。

> [!div class="nextstepaction"]
> [获取 UI 库 (GitHub) ](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>示例应用

安装示例应用以查看 UI 模板在上下文中的外观Teams行为。

> [!div class="nextstepaction"]
> [获取示例应用 (GitHub) ](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="dashboard"></a>仪表板

仪表板在中心位置显示不同类型的内容， (Teams应用或选项卡) 。 用户至少应该能够自定义他们在仪表板上看到部分内容。

### <a name="top-use-cases"></a>热门用例

* 分析数据
* 报告指标
* 在一个地方组织不同的信息

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="示例显示桌面上的仪表板 UI 模板。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-dashboard.png" alt-text="示例显示移动设备上的仪表板 UI 模板。" border="false":::

---

## <a name="data-visualization"></a>数据可视化

可以使用不同的卡片大小 (、双精度和) ，以在同一页面上堆叠和组织数据可视化效果。 卡片可缩放以适合列布局并填充空白区域。

### <a name="top-use-cases"></a>热门用例

* 显示复杂信息
* 创建仪表板

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="示例显示桌面上的数据可视化 UI 模板。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-data-viz.png" alt-text="示例演示移动设备上的数据可视化 UI 模板。" border="false":::

---

## <a name="empty-state"></a>空状态

空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。 它非常灵活，可调整它以使用以下设计中一个组件、一些组件或所有组件。

### <a name="top-use-cases"></a>热门用例

* 登录
* 欢迎消息和首次运行体验
* 成功消息
* 错误消息

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="示例在桌面上显示空状态 UI 模板。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-empty-state.png" alt-text="示例显示移动设备上的空状态 UI 模板。" border="false":::

---

## <a name="filter"></a>筛选器

利用筛选器，您可以根据所选条件减少看到的信息。 您可以将筛选器与表、列表、卡片和其他用于组织内容的组件一起包含。

### <a name="top-use-cases"></a>热门用例

组织内容，包括：

* 列表
* 表格
* 仪表板
* 数据可视化

:::image type="content" source="../../assets/images/ui-templates/filter.png" alt-text="示例显示筛选器模板。" border="false":::

## <a name="form"></a>表单

表单用于以结构化方式收集、验证和提交用户输入。 对输入字段进行清晰标记和逻辑分组对于获得良好的用户体验至关重要。

### <a name="top-use-cases"></a>热门用例

* 登录
* 用户配置文件
* 设置
* 用户输入集合

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="示例在桌面上显示表单 UI 模板。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-form.png" alt-text="示例显示移动设备上的表单 UI 模板。" border="false":::

---

## <a name="list"></a>列表

可以使用列表以可扫描的格式显示相关项目，并允许用户对整个列表或单个项目采取操作。

### <a name="top-use-cases"></a>热门用例

* 显示数据
* 应用内容的上下文操作

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="示例显示桌面上的列表 UI 模板。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-list.png" alt-text="示例显示移动设备上的列表 UI 模板。" border="false":::

---

## <a name="sign-in"></a>登录

你可以为不同的上下文和标识提供程序设计Teams登录流。 以下示例包括单一登录 (SSO) ，建议这样做以简化身份验证体验。

### <a name="top-use-case"></a>热门用例

* 对用户进行身份验证

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="示例显示桌面上的登录 UI 模板。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-sign-in.png" alt-text="示例显示移动设备上的登录 UI 模板。" border="false":::

---

## <a name="settings"></a>设置

设置屏幕是用户可以使用你的应用配置其首选项的地方。  (注意：设置是基本[UI 组件的](~/concepts/design/design-teams-app-basic-ui-components.md)容器 。) 

### <a name="top-use-case"></a>热门用例

* 管理应用功能

:::image type="content" source="../../assets/images/ui-templates/settings.png" alt-text="示例显示设置模板。" border="false":::

## <a name="task-board"></a>任务板

任务板（有时称为看板或街道）是一组卡片，通常用于跟踪工作项或票证的状态。 它还可用于将任何类型的内容分类为类别。 可以在列之间编辑和移动卡片。

### <a name="top-use-cases"></a>热门用例

* 项目管理。 分配任务和跟踪状态
* 集体讨论。 在不同类别中添加想法
* 对练习进行排序。 将任何类型的信息组织到存储桶

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="示例在桌面上显示任务板 UI 模板。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-task-board.png" alt-text="示例显示移动设备上的任务板 UI 模板。" border="false":::

---

## <a name="wizard"></a>向导

向导将指导用户完成多个屏幕以完成任务 (如设置过程) 。

### <a name="top-use-cases"></a>热门用例

* 设置
* 载入
* 首次运行体验

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="示例在桌面上显示向导 UI 模板。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-wizard.png" alt-text="示例显示移动设备上的向导 UI 模板。" border="false":::

---
