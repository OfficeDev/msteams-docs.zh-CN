---
title: 设计个人应用
description: 了解如何设计个人Teams并获取 Microsoft Teams UI 工具包。
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 83fad746d71dd196f6efa6526f5c6c28ceac9e20
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644884"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>为用户设计个人Microsoft Teams

个人应用可以是自动程序、专用工作区，也可以同时为两者。 有时，它的功能与创建或查看内容的位置类似，其他时候，当应用被配置为多个频道中的选项卡时，它会为用户提供其所有内容的鸟眼视图。

为了指导你的应用设计，以下信息介绍了并说明了用户如何添加、使用和管理应用中的个人Teams。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

你可以找到全面的个人应用设计指南，包括你可以根据需要获取和修改的元素，Microsoft Teams UI 工具包。 UI 工具包还具有辅助功能和响应式大小调整等基本主题，此处未介绍这些主题。

> [!div class="nextstepaction"]
> [获取 Microsoft Teams UI Kit （用户）](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>添加个人应用

可以通过选择 Teams (左侧的"更多"图标从 Teams app) Source ( (应用商店或应用Teams (添加个人应用，如以下示例) 所示。

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="示例演示如何从应用飞出内容添加个人应用。" border="false":::

## <a name="use-a-personal-app-private-workspace"></a>使用个人应用 (工作区) 

使用专用工作区，可以在中心位置查看对你有意义的应用内容，而无需离开Teams。

 (：专用工作区基于个人 [*选项卡功能*](../../build-your-first-app/build-personal-tab.md) 。) 

### <a name="anatomy-personal-app-private-workspace"></a>分析：个人应用 (专用工作区) 

# <a name="desktop"></a>[桌面](#tab/desktop)

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="示例显示个人选项卡的组件分析。" border="false":::

|计数器|说明|
|----------|-----------|
|A|**应用属性**：应用徽标和名称。|
|B|**选项卡**：为个人应用提供导航。|
|C|**弹出视图**：将应用内容从父窗口推送到独立子窗口。|
|D|**更多菜单**：包括其他应用选项和信息。  (您也可以将选项卡设置 tab.) |

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="示例显示个人选项卡的结构结构分析。" border="false":::

|计数器|说明|
|----------|-----------|
|A|**选项卡**：为个人应用提供导航。|
|1|**iframe：** 显示应用内容。|

# <a name="mobile"></a>[移动](#tab/mobile)

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-component-anatomy.png" alt-text="示例显示个人选项卡的组件分析。" border="false":::

|计数器|说明|
|----------|-----------|
|A|**应用属性**：你的应用名称。|
|B|**选项卡**：为个人应用提供导航。|
|C|**更多菜单**：包括其他应用选项和信息。|
|D|**主导航**：提供对应用的其他主要导航Teams导航。|

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-structural-anatomy.png" alt-text="示例显示个人选项卡的结构结构分析。" border="false":::

|计数器|说明|
|----------|-----------|
|A|**选项卡**：为个人应用提供导航。|
|1|**webview：** 显示应用内容。|

---

### <a name="designing-with-ui-templates-and-advanced-components"></a>使用 UI 模板和高级组件进行设计

使用以下模板和Teams之一来帮助设计个人选项卡：

* [列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目采取操作。
* [任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board)：任务板（有时称为看板或街道）是一组卡片，通常用于跟踪工作项或票证的状态。
* [仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard)：仪表板是包含多个卡片的画布，可提供数据或内容的概述。
* [表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单用于以结构化方式收集、验证和提交用户输入。
* [空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。
* [左侧导航](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav)：如果你的个人应用需要一些导航，左侧导航组件可以提供帮助。 通常，应该将导航保持在最低程度。

## <a name="use-a-personal-app-bot"></a>使用个人应用 (自动) 

个人应用可以包含用于一对一对话的自动程序以及私人通知 (例如，当同事在剪贴板上发布评论时) 。 自动程序在指定的选项卡中可用。

### <a name="anatomy-personal-app-bot"></a>结构：个人应用 (自动) 

# <a name="desktop"></a>[桌面](#tab/desktop)

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="示例显示个人自动程序组件分析。" border="false":::

|计数器|说明|
|----------|-----------|
|A|**自动程序** 选项卡：例如，包括一个 **聊天选项卡** 来访问机器人对话和通知。|
|B|**自动程序** 消息：机器人通常以卡片形式发送消息和通知， (自适应卡片) 。|
|C|**撰写框**：用于向自动程序发送邮件的输入字段。|

# <a name="mobile"></a>[移动](#tab/mobile)

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-bot-anatomy.png" alt-text="示例显示个人自动程序组件分析。" border="false":::

|计数器|说明|
|----------|-----------|
|A|**自动程序入口点**：用户用于访问个人应用中的自动程序功能入口点。|
|B|**"后退**"按钮：让用户返回到专用工作区。|
|C|**自动程序** 消息：机器人通常以卡片形式发送消息和通知， (自适应卡片) 。|
|D|**撰写框**：用于向自动程序发送邮件的输入字段。|

---

## <a name="manage-a-personal-tab"></a>管理个人选项卡

在应用左侧Teams，用户可以右键单击个人应用以固定、删除和配置其他应用选项。

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="示例显示用于管理个人应用的选项。" border="false":::

## <a name="best-practices"></a>最佳做法

使用这些建议创建高质量的应用体验。

### <a name="tab-priority"></a>选项卡优先级

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>操作：显示第一个选项卡中最相关的内容

使用响应式大小调整时，右侧选项卡可能会被截断或退出视图。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="示例显示第一个选项卡中显示最相关内容的个人应用。" border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>请勿：使用辅助内容或元数据领导

与标准 Web 应用一样，选项卡导航应按有助于了解应用主要功能的顺序进行。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="示例显示以辅助内容或元数据作为前导的个人应用。" border="false":::

### <a name="tab-hierarchy"></a>选项卡层次结构

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>应做：选项卡的层次结构应相同，并代表关键应用页面

选项卡应分类应用的主要功能和内容。 使用响应式大小调整时，右侧的内容可能会被截断或退出视图。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="示例显示具有相同层次结构选项卡的个人应用。" border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>请勿：包括不同级别的层次结构

内容应按逻辑顺序进行，以帮助用户理解它。 如果您有两个紧密相关的选项卡，请考虑将它们合并到一个选项卡中。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="示例显示层次结构级别不同的个人应用。" border="false":::

### <a name="first-run-experience"></a>首次运行体验

#### <a name="do-include-a-first-run-experience"></a>应做：包括首次运行体验

首次使用个人应用时，应该至少有一个欢迎屏幕。 对于自动程序，描述自动程序可以执行哪些操作并提供快速操作，例如登录按钮。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="示例显示个人应用首次运行体验期间要执行哪些操作。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="另一个示例演示在个人应用首次运行体验期间要执行哪些操作。" border="false":::

#### <a name="dont-start-with-a-blank-screen"></a>不要：从空白屏幕开始

如果用户第一次运行你的应用时没有显示任何内容，用户可能会感到困惑。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="示例显示个人应用首次运行体验期间不执行哪些操作。" border="false":::

### <a name="personalized-content"></a>个性化内容

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>操作：聚合与用户相关的应用内容

无论是个人选项卡还是自动程序，在应用中仅显示与用户活动相关的内容。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="示例演示了使用个人应用和个性化内容要执行哪些操作。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="另一个示例演示了使用个人应用和个性化内容要执行哪些操作。" border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>请勿：显示不相关或过于宽泛的内容

在个人上下文中，请勿显示用户不是团队的一部分的内容。 个人自动程序内容应侧重于个人，而不是组。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="示例显示对个人应用和个性化内容不执行哪些操作。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="另一个示例演示了对个人应用和个性化内容不执行哪些操作。" border="false":::

### <a name="complex-app-features"></a>复杂的应用功能

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>应做：允许用户在浏览器中访问复杂功能

你的应用应专注于应用中的核心Teams，但你仍然可以在浏览器中查看完整的独立应用。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="示例演示如何使用个人应用处理复杂的应用功能。" border="false":::

#### <a name="dont-include-your-entire-app"></a>请勿：包括整个应用

除非你专门为用户创建了Teams，否则你在协作工具中可能没有意义的功能。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="示例演示如何不通过个人应用处理复杂的应用功能。" border="false":::

## <a name="see-also"></a>另请参阅

以下其他设计指南可能会有所帮助，具体取决于你的个人应用的范围：

* [设计选项卡](../../tabs/design/tabs.md)
* [正在设计自动程序](../../bots/design/bots.md)
