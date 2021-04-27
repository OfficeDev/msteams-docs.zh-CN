---
title: 使用 UI 模板设计应用
author: heath-hamilton
description: 使用 Microsoft Teams 中常见的标准化 UI 组件、布局和模式更快地设计应用。
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: d627ce3b29ffa071d0d7e238c572c7cb69fa4cd9
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020763"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a>使用 UI 模板设计 Microsoft Teams 应用

使用 UI 模板更快地设计 Microsoft Teams 应用。 模板是基于 Fluent UI 的组件的集合，这些组件适用于常见的 Teams 用例，让你有更多的时间来为用户找到最佳体验。

## <a name="getting-started-with-tools-and-samples"></a>工具和示例入门

以下资源可帮助你使用 UI 模板设计和开发应用。

### <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

从 Microsoft Teams UI 工具包获取应用设计的 UI 模板，其中还包括有关用法、结构分析、辅助功能和最佳做法的广泛信息。

> [!div class="nextstepaction"]
> [获取图 (UI) ](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft Teams UI 库

在浏览器中查看和测试单个 Teams UI 模板和相关组件。

> [!div class="nextstepaction"]
> [尝试 UI 库 (场) ](https://dev-int.teams.microsoft.com/storybook/main/index.html)

直接将这些模板和相关组件导入到 Teams 应用项目中。

> [!div class="nextstepaction"]
> [使用 GitHub (获取 UI) ](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>示例应用

安装示例应用以查看 UI 模板在 Teams 上下文中的外观和行为。

> [!div class="nextstepaction"]
> [从 GitHub (获取) ](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a>列表

可以使用列表以可扫描的格式显示相关项目，并允许用户对整个列表或单个项目采取操作。

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="示例显示列表 UI 模板。" border="false":::

### <a name="top-use-cases"></a>热门用例

* 显示数据
* 应用内容的上下文操作

## <a name="dashboard"></a>仪表板

仪表板在 Teams 个人应用或选项卡 (集中显示不同类型的) 。 用户至少应该能够自定义他们在仪表板上看到部分内容。

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="示例显示仪表板 UI 模板。" border="false":::

### <a name="top-use-cases"></a>热门用例

* 分析数据
* 报告指标
* 在一个地方组织不同的信息

## <a name="form"></a>表单

表单用于以结构化方式收集、验证和提交用户输入。 对输入字段进行清晰标记和逻辑分组对于获得良好的用户体验至关重要。

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="示例显示表单 UI 模板。" border="false":::

### <a name="top-use-cases"></a>热门用例

* 登录
* 用户配置文件
* 设置
* 用户输入集合

## <a name="sign-in"></a>登录

你可以为不同的 Teams 上下文和标识提供程序设计应用登录流。 以下示例包括单一登录 (SSO) ，建议这样做以简化身份验证体验。

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="示例显示登录 UI 模板。" border="false":::

### <a name="top-use-case"></a>热门用例

* 对用户进行身份验证

## <a name="task-board"></a>任务板

任务板（有时称为看板或街道）是一组卡片，通常用于跟踪工作项或票证的状态。 它还可用于将任何类型的内容分类为类别。 可以在列之间编辑和移动卡片。

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="示例显示任务板 UI 模板。" border="false":::

### <a name="top-use-cases"></a>热门用例

* 项目管理。 分配任务和跟踪状态
* 集体讨论。 在不同类别中添加想法
* 对练习进行排序。 将任何类型的信息组织到存储桶

## <a name="data-visualization"></a>数据可视化

可以使用不同的卡片大小 (、双精度和) ，以在同一页面上堆叠和组织数据可视化效果。 卡片可缩放以适合列布局并填充空白区域。

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="示例显示数据可视化 UI 模板。" border="false":::

### <a name="top-use-cases"></a>热门用例

* 显示复杂信息
* 创建仪表板

## <a name="wizard"></a>向导

向导将指导用户完成多个屏幕以完成任务 (如设置过程) 。

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="示例显示向导 UI 模板。" border="false":::

### <a name="top-use-cases"></a>热门用例

* 设置
* 载入
* 首次运行体验

## <a name="empty-state"></a>空状态

空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。 它非常灵活，可调整它以使用以下设计中一个组件、一些组件或所有组件。

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="示例显示空状态 UI 模板。" border="false":::

### <a name="top-use-cases"></a>热门用例

* 登录
* 欢迎消息和首次运行体验
* 成功消息
* 错误消息

## <a name="notification-bar"></a>通知栏

通知栏是一个专用区域，用于显示无需用户立即采取措施的简短重要消息。 特定背景颜色和图标与特定类型的邮件相关联， (请参阅下面的) 。

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="示例显示通知栏模板。" border="false":::

### <a name="top-use-cases"></a>热门用例

* 关键消息、错误和警告
* 成功消息
* 信息性或促销性消息

## <a name="left-nav"></a>左导航

使用左侧导航键浏览 Teams 选项卡内的多个页面。在下面的示例中，左侧导航位于通道列表和选项卡内容之间。

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="示例显示左侧导航模板。" border="false":::

### <a name="top-use-cases"></a>热门用例

* 浏览 Teams 选项卡内的多个页面
* 将复杂应用分解为多个页面

## <a name="breadcrumb"></a>痕迹导航栏

痕迹导航是一种导航帮助，可传达应用的层次结构。 它们可帮助用户了解他们查看的页面如何适应整体体验，并提供了对层次结构中较高级别的一键访问。

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="示例显示痕迹导航模板。" border="false":::

### <a name="top-use-cases"></a>热门用例

* 通信层次结构
* 导航

## <a name="toolbar"></a>工具栏

工具栏是一个容器，用于对一组控件进行分组。

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="示例显示工具栏模板。" border="false":::

### <a name="top-use-cases"></a>热门用例

* 应用内容的上下文操作
* 上下文筛选器和查找
* 导航和痕迹导航

## <a name="stage"></a>阶段

Stage 为用户提供了一种在 Teams 中打开实体（如图像、文件或网站）的方法，而不是在另一个应用或浏览器中打开它。 阶段的主要用例是查看;图面不应用于复杂的交互。

 (实现说明：使用大型任务模块[.) ](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="示例显示阶段模板。" border="false":::

### <a name="top-use-cases"></a>热门用例

* 在 Teams 中打开实体，而不是其他应用或浏览器
* 聚焦媒体或其他内容
