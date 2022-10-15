---
title: 设计个人应用
description: 了解如何实现设计准则，包括使用 Microsoft Teams UI 工具包设计个人应用的 UI 元素。
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: 4646d47c5aa325291f060ea192dcc1705b414ac7
ms.sourcegitcommit: bd96080c78f25eb0a67ce176df5e255be348f7b1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2022
ms.locfileid: "68575784"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>为 Microsoft Teams 设计个人应用

个人应用可以是机器人、专用工作区或两者。 有时，它充当创建或查看内容的位置。 其他时候，当应用在多个通道中配置为选项卡时，它会为用户提供对其所有内容的鸟瞰视图。

为指导应用设计，以下信息描述并说明用户可以如何在 Teams 中添加、使用和管理个人应用。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

可在 Microsoft Teams UI Kit 中查看全面的个人应用设计指南，包括可根据需要获取和修改的元素。 UI 工具包还包含基本主题，如此处未介绍的辅助功能和响应式大小调整。

> [!div class="nextstepaction"]
> [获取 Microsoft Teams UI Kit (用户)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>添加个人应用

用户可以通过选择 Teams 左侧的“**更多**”图标（如以下示例所示）从 Teams 应用商店或应用浮出控件添加个人应用。

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="示例显示如何从应用浮出控件添加个人应用。":::

## <a name="use-a-personal-app-private-workspace"></a>使用个人应用（专用工作区）

使用专用工作区，用户可以在中心位置查看对他们有意义的应用内容，无需离开 Teams。

（实现说明：专用工作区基于 [*个人选项卡*](../../tabs/how-to/create-personal-tab.md)功能。）

### <a name="anatomy-personal-app-private-workspace"></a>剖析: 个人应用（专用工作区）

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-component-anatomy.png" alt-text="示例显示个人选项卡的组件剖析。":::

|计数器|说明|
|----------|-----------|
|A|**应用属性**：应用名称。|
|B|**选项卡**：为个人应用提供导航。|
|C|**更多菜单**：包括其他应用选项和信息。|
|D|**主导航**： 向应用提供其他主要 Teams 功能的导航。|

#### <a name="configure-and-add-multiple-actions-in-navbar"></a>**在 NavBar 中配置和添加多个操作**

可以将多个操作添加到右上角的 NavBar，并生成溢出菜单，以便在应用中执行额外的操作。

>[!NOTE]
> 导航栏中最多可以添加五个操作，包括溢出菜单。

:::image type="content" source="../../assets/images/overflow-menu-and-multiple-actionsoptions.png" alt-text="屏幕截图是描述导航栏和溢出菜单的示例。":::

若要 **在 NavBar 中配置和添加多个操作**，请调用 [setNavBarMenu](/javascript/api/@microsoft/teams-js/microsoftteams.menus?view=msteams-client-js-1.12.1&preserve-view=true) API。 并将属性 `displayMode enum` 添加到 `MenuItem`. 定义 `displayMode enum` 了如何在 NavBar 中显示菜单。 的默认值 `displayMode enum` 设置为 `ifRoom`。

根据 NavBar 中可用的要求和空间，请考虑 `displayMode enum` 下列操作之一。

* 如果有房间，请设置 `ifRoom = 0` 为将项放置在 NavBar 中。
* 如果没有空间，请设置 `overflowOnly = 1`，以便始终将该项目放置在 NavBar 的溢出菜单中，但不会放在 NavBar 中。

下面是使用多个操作的溢出菜单配置 NavBar 的示例：

```typescript
const menuItems = [item1, item2, item3, item4, item5]
microsoftTeams.menus.setNavBarMenu(menuItems, (id: string) => {
  output(`Clicked ${id}`)
  return true;
})
```

> [!NOTE]
> API `setNavBarMenu` 不控制 **“刷新** ”按钮。 默认情况下会显示它。

:::image type="content" source="../../assets/images/overflow-menu-and-multple-actions.png" alt-text="屏幕截图是显示溢出菜单中的导航栏和多个操作的示例。":::

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-structural-anatomy.png" alt-text="示例显示个人选项卡的结构剖析。":::

|计数器|说明|
|----------|-----------|
|A|**选项卡**：为个人应用提供导航。|
|1|**webview**: 显示应用内容。|

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="此示例显示个人选项卡的组件剖析。":::

|计数器|说明|
|----------|-----------|
|A|**应用属性**： 应用徽标和名称。|
|B|**选项卡**：为个人应用提供导航。|
|C|**弹出视图**：将应用内容从父窗口推送到独立子窗口。|
|D|**更多菜单**：包括其他应用选项和信息。 （也可以将 **设置** 设置为选项卡。）|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="此示例显示个人选项卡的结构剖析。":::

|计数器|说明|
|----------|-----------|
|A|**选项卡**：为个人应用提供导航。|
|1|**iframe**: 显示应用内容。|

### <a name="design-with-ui-templates-and-advanced-components"></a>使用 UI 模板和高级组件设计

使用以下 Teams 模板和组件之一来帮助设计你的个人选项卡：

* [列表](../../concepts/design/design-teams-app-ui-templates.md#list): 列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目执行操作。
* [任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board): 任务板 (有时称为看板或泳道) 是通常用于跟踪工作项或票证状态的卡片集合。
* [仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard): 仪表板是包含多个卡片的画布，可提供数据或内容的概述。
* [表单](../../concepts/design/design-teams-app-ui-templates.md#form): 表单是用于收集、验证和提交用户输入的结构化方式。
* [空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空状态模板可用于许多方案，包括登录、首次运行体验、错误消息等。
* [左侧导航](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav): 如果个人应用需要导航，左侧导航组件可提供帮助。 通常，应将导航保持在最低限度。

## <a name="use-a-personal-app-bot"></a>使用个人应用 （机器人）

Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on artboard). Users interact with the bot in a tab you specify.

### <a name="anatomy-personal-app-bot"></a>剖析：个人应用（机器人）

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-bot-anatomy.png" alt-text="示例显示个人机器人组件剖析。":::

|计数器|说明|
|----------|-----------|
|A|**机器人入口点**：用户在个人应用中访问机器人功能的入口点。|
|B|**后退按钮**：将用户带回专用工作区。|
|C|**机器人消息**：机器人通常以卡片的形式发送消息和通知 （如自适应卡片）。|
|D|**撰写框**：用于向机器人发送消息的输入字段。|

#### <a name="configure-back-button"></a>配置后退按钮

在 Teams 应用中选择后退按钮时，将返回到 Teams 平台，而无需在应用内导航。

若要在应用中导航，请配置后退按钮，以便在选择后退按钮时，可以返回到以前的步骤并在应用中导航。

若要 **配置后退按钮**，请调用 [registerBackButtonHandler](/javascript/api/@microsoft/teams-js/pages.backstack?view=msteams-client-js-latest&preserve-view=true&branch=pr-en-us-6801&preserve-view=true) API，该 API 根据以下条件之一处理后退按钮的功能：

* 设置为 `false`JavaScript SDK 时`registerBackButtonHandler`调用 `navigateBack` API，Teams 平台处理后退按钮。
* 设置为`true`后`registerBackButtonHandler`退按钮时，应用将处理后退按钮的功能 (可以返回到以前的步骤并在应用) 中导航，而 Teams 平台不会执行进一步的操作。

下面是配置后退按钮的示例：

```typescript
microsoftTeams.registerBackButtonHandler(() => {
  const selectOption = registerBackReturn.options[registerBackReturn.selectedIndex].value
  var isHandled = false
  if (selectOption == 'true') 
    isHandled = true;
  output(`onBack isHandled ${isHandled}`)
  return isHandled;
})
```

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="示例显示个人机器人组件的剖析。":::

|计数器|说明|
|----------|-----------|
|A|**机器人选项卡**：例如，包括用于访问机器人对话和通知的 **聊天** 选项卡。|
|B|**机器人消息**：机器人通常以卡片的形式发送消息和通知 （如自适应卡片）。|
|C|**撰写框**：用于向机器人发送消息的输入字段。|

## <a name="manage-a-personal-tab"></a>管理个人选项卡

在 Teams 左侧，用户可以右键单击个人应用以固定、删除和配置其他应用选项。

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="示例显示用于管理个人应用的选项。":::

## <a name="best-practices"></a>最佳做法

使用上述建议打造优质应用体验。

### <a name="tab-priority"></a>Tab 优先级

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>确保:在第一个选项卡中显示最相关内容

使用响应式大小调整时，右侧的选项卡可能会被截断或无法查看。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="示例显示了在第一个选项卡中显示最相关内容的个人应用。":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>请勿:以次要内容或元数据为开始

与标准 Web 应用一样，选项卡导航应按有助于理解应用主要功能的顺序进行。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="示例显示以辅助内容或元数据为主导的个人应用。":::

### <a name="tab-hierarchy"></a>选项卡层次结构

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>确保: 选项卡的层次结构应相等，并表示关键应用页

选项卡应按照应用的主要功能和内容进行分类。 使用响应式大小调整时，右侧的内容可能会被截断或无法查看。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="示例显示具有相同层次结构选项卡的个人应用。":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>请勿: 包括不同层次结构级别

内容应按逻辑顺序进行，以方便用户理解。 如果有两个密切相关的选项卡，请考虑将它们组合到一个选项卡中。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="示例显示了具有不同层次结构级别的个人应用。":::

### <a name="first-run-experience"></a>首次运行体验

#### <a name="do-include-a-first-run-experience"></a>确保: 包括首次运行体验

首次使用个人应用时，至少应有一个欢迎界面。 对于机器人，请描述机器人可以执行的操作并提供快速操作，例如登录按钮。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="示例显示在个人应用首次运行体验期间要执行的操作。":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="另一个示例显示在个人应用首次运行体验期间要执行的操作。":::

#### <a name="dont-start-with-a-blank-screen"></a>请勿: 从空白屏幕开始

如果用户在首次运行你的应用时未显示任何内容，可能会感到困惑。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="示例显示在个人应用首次运行体验期间不执行的操作。":::

### <a name="personalized-content"></a>个性化内容

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>确保: 聚合与用户相关的应用内容

无论是个人选项卡还是机器人，都可以在应用中仅显示与用户活动相关的内容。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="示例显示对个人应用和个性化内容执行的操作。":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="另一个示例显示对个人应用和个性化内容执行的操作。":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>请勿:显示不相关或过于宽泛的内容

在个人上下文中，不显示用户非所属团队的内容。 个人机器人内容应侧重于个人，而不是组。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="示例显示不对个人应用和个性化内容执行的操作。":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="另一个示例显示不对个人应用和个性化内容执行的操作。":::

### <a name="complex-app-features"></a>复杂应用功能

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>确保: 允许用户访问浏览器中的复杂功能

你的应用应专注于 Teams 中的核心任务，但仍然可以在浏览器中查看完整的独立应用。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="示例显示如何使用个人应用处理复杂的应用功能。":::

#### <a name="dont-include-your-entire-app"></a>请勿:包括整个应用

除非专门为 Teams 创建应用，否则可能具有在协作工具中没有意义的功能。

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="示例显示如何不使用个人应用处理复杂的应用功能。":::

## <a name="see-also"></a>另请参阅

根据个人应用的作用域，这些其他设计准则可能会有所帮助：

* [设计选项卡](../../tabs/design/tabs.md)
* [设计机器人](../../bots/design/bots.md)
* [registerBackButtonHandler](/javascript/api/@microsoft/teams-js/pages.backstack?view=msteams-client-js-latest&preserve-view=true&branch=pr-en-us-6801&preserve-view=true)
* [DisplayMode 枚举](/javascript/api/@microsoft/teams-js/menus.displaymode?view=msteams-client-js-latest&preserve-view=true)
