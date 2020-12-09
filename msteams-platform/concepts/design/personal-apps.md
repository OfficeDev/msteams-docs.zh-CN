---
title: 正在设计你的个人应用
description: 了解如何设计工作组个人应用程序并获取 Microsoft 团队 UI 工具包。
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 971071be9f345815f5461646d7970efdf05fd5c4
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604973"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>为 Microsoft 团队设计个人应用程序

个人应用程序可以是 bot、专用工作区或两者。 有时它的工作方式类似于创建或查看内容的位置，而另一些时候它为用户提供了在将应用程序配置为多个频道中的选项卡时的所有内容的鸟瞰视图。

若要指导您的应用程序设计，以下信息介绍并说明了用户如何添加、使用和管理团队中的个人应用程序。

## <a name="microsoft-teams-ui-kit"></a>Microsoft 团队 UI 工具包

您可以在 Microsoft 团队 UI 工具包中找到全面的个人应用程序设计指南，包括可在需要时获取和修改的元素。 UI 工具包还包含此处未介绍的辅助功能和响应大小等基本主题。

> [!div class="nextstepaction"]
> [ (Figma) 获取 Microsoft 团队 UI 工具包 ](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>添加个人应用程序

您可以从团队存储 (AppSource ") " 或 "应用程序" 浮出控件中添加个人应用程序，方法是在团队左侧选择 " **更多** " 图标 (如以下示例) 所示。

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="示例演示如何从应用浮出控件添加个人应用程序。" border="false":::

## <a name="use-a-personal-app-private-workspace"></a>使用个人应用 (专用工作区) 

使用专用工作区，您可以查看在中心位置有意义的应用程序内容，而无需离开团队。

 (实现注意：专用工作区基于 " [*个人" 选项卡*](../../build-your-first-app/build-personal-tab.md) 功能。 ) 

### <a name="anatomy-personal-app-private-workspace"></a>剖析：个人应用程序 (专用工作区) 

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="示例显示了个人选项卡的组件解析。" border="false":::

|计数器|描述|
|----------|-----------|
|A|**应用程序归属**：您的应用程序徽标和名称。|
|B|**选项卡**：提供你的个人应用的导航。 例如，包括 " **关于** " 或 " **帮助** " 选项卡。|
|C|**弹出视图**：将您的应用程序内容从父窗口推送到独立子窗口。|
|D|"**更多" 菜单**：包含其他应用程序信息和选项。  (您也可以将 **设置设置** 为选项卡。 ) |

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="示例显示了个人选项卡的结构剖析。" border="false":::

|计数器|描述|
|----------|-----------|
|A|**选项卡**：提供你的个人应用的导航。|
|1 |**iframe**：显示应用内容。|

### <a name="designing-with-ui-templates"></a>使用 UI 模板进行设计

使用以下团队 UI 模板之一来帮助设计您的个人选项卡：

* [列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可浏览的格式显示相关项目，并允许用户对整个列表或单个项目执行操作。
* [任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board)：任务板（有时称为 "看板母板" 或 "泳道"）是用于跟踪工作项或票证状态的卡片的集合。
* [仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard)：仪表板是一个包含多个卡片的画布，可提供数据或内容的概述。
* [表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单以结构化方式收集、验证和提交用户输入。
* [空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。
* [左侧](../../concepts/design/design-teams-app-ui-templates.md#left-nav)导航：如果您的选项卡需要一些导航，则左侧导航模板可有所帮助。 通常情况下，应保持最小的选项卡导航。

## <a name="use-a-personal-app-bot"></a>使用个人应用 (bot) 

个人应用可以包括用于一对一对话和私人通知 (的 bot，例如，当同事将注释发布到美工板上时) 。 可以在指定的选项卡中使用 bot。

### <a name="anatomy-personal-app-bot"></a>剖析：个人应用程序 (bot) 

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="示例显示个人 bot 组件解析。" border="false":::

|计数器|描述|
|----------|-----------|
|A|**机器人选项卡**：例如，包含一个 " **聊天** " 选项卡来访问机器人对话和通知。|
|B|**Bot 邮件**： bot 通常以卡片形式发送邮件和通知 (例如，自适应卡片) 。|
|C|**"撰写" 框**：用于将邮件发送到 bot 的输入字段。|

## <a name="best-practices"></a>最佳做法

### <a name="tab-priority"></a>选项卡优先级

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>操作：在第一个选项卡中显示最相关的内容

通过快速响应调整大小，右侧的选项卡可能会被截断或无法查看。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>不：领导辅助内容或元数据

与标准 web 应用一样，选项卡导航按照有助于了解应用程序主要功能的顺序进行。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

### <a name="tab-hierarchy"></a>选项卡层次结构

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>操作：选项卡应具有相同的层次结构，并表示关键应用程序页面

你的选项卡应对你的应用程序的主要功能和内容进行分类。 使用快速响应大小，右侧的内容可能会被截断或无法查看。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>不：包含不同级别的层次结构

您的内容应以有助于用户理解的逻辑顺序进行。 如果您有两个密切相关的选项卡，请考虑将它们组合成一个选项卡。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

### <a name="first-run-experience"></a>首次运行体验

#### <a name="do-include-a-first-run-experience"></a>操作：包括首次运行体验

首次使用个人应用时，应该至少有一个欢迎屏幕。 对于 bot，说明你的 bot 可以执行的操作并提供快速操作，如登录按钮。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

#### <a name="dont-start-with-a-blank-screen"></a>不：从空白屏幕开始

如果在首次运行应用程序时没有显示任何内容，则可能会对用户感到困惑。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

### <a name="personalized-content"></a>个性化内容

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>操作：与用户相关的聚合应用内容

无论是个人选项卡还是 bot，仅显示与您的应用程序中的用户活动相关的内容。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>不：显示不相关或过于广泛的内容

在个人上下文中，不为不属于用户的团队显示内容。 个人 bot 内容应侧重于个人（而不是组）。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

### <a name="complex-app-features"></a>复杂的应用程序功能

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>Do：允许用户在浏览器中访问复杂功能

您的应用程序应重点关注团队中的核心任务，但您仍可以在浏览器中查看完整的独立应用程序。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

#### <a name="dont-include-your-entire-app"></a>请勿：包含整个应用程序

除非您专为工作组创建应用程序，否则在协作工具中可能没有意义的功能。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

## <a name="manage-a-personal-tab"></a>管理个人选项卡

在团队的左侧，用户可以右键单击个人应用以固定、删除和配置其他应用程序选项。

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="示例显示用于管理个人应用程序的选项。" border="false":::

## <a name="learn-more"></a>了解更多

根据个人应用程序的范围，这些其他设计准则可能会有所帮助：

* [设计选项卡](../../tabs/design/tabs.md)
* [设计机器人](../../bots/design/bots.md)

## <a name="validate-your-design"></a>验证设计

如果计划将应用程序发布到 AppSource，则应了解通常会在提交期间导致应用程序失败的设计问题。

> [!div class="nextstepaction"]
> [检查设计验证准则](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
