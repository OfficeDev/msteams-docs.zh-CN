---
title: 桌面、Web 和移动设备的设计选项卡
description: 了解如何为桌面、Web 和移动设备设计选项卡，并获得 Microsoft Teams UI Kit。 了解选项卡、生成用户身份验证、选项卡通知和深层链接。
author: heath-hamilton
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8002b5ddf2fcb403978587819855468915813684
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558322"
---
# <a name="design-your-tab-for-microsoft-teams"></a>为 Microsoft Teams 设计选项卡

选项卡是应用内容的大型画布。 为指导应用设计，以下信息描述并说明用户可以如何在 Teams 中添加、使用和管理选项卡。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

可在 Microsoft Teams UI Kit 中查看全面的选项卡设计指南，包括可根据需要获取和修改的元素。 UI 工具包还包含基本主题，如此处未介绍的辅助功能和响应式大小调整。

> [!div class="nextstepaction"]
> [获取 Microsoft Teams UI Kit (用户)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a>添加选项卡

可以从 Teams 应用商店 (AppSource) 或以下上下文之一添加选项卡: 

* 聊天
* 频道
* 会议 (会议之前、期间或之后) 

### <a name="mobile"></a>移动设备

用户可以通过选择频道中的 **更多** 按钮 (如下所示) 或已添加选项卡的聊天来访问选项卡。

:::image type="content" source="../../assets/images/tabs/mobile-design-access-tab.png" alt-text="示例显示在频道中添加的移动选项卡。":::

### <a name="desktop"></a>桌面

以下示例演示用户如何在频道中添加选项卡。

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="示例显示在频道中添加的选项卡。":::

## <a name="set-up-a-tab"></a>设置选项卡

将应用添加为频道、聊天或会议选项卡需要一个简短的设置过程。体验主要取决于你。 例如，可以提供有关如何使用应用的说明和一些可选设置。 如果需要对用户进行身份验证，请在此处添加登录步骤。

### <a name="tab-configuration-dialog"></a>选项卡配置对话框

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="示例显示选项卡配置模式。":::

#### <a name="anatomy-tab-configuration-dialog"></a>解剖: 选项卡配置对话框

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="插图显示了选项卡配置模式的 UI 解剖。":::

|计数器|说明|
|----------|-----------|
|1|**应用徽标**: 应用的全色应用徽标。|
|2|**应用名称**：应用的全名。|
|3|**iframe**: 为应用的内容提供响应的空间 (例如，选项卡设置或身份验证)。|
|4|**关于链接**: 打开一个对话框，其中显示有关应用的详细信息，例如完整说明、应用所需的权限，以及指向隐私策略和服务条款的链接。|
|5|**关闭按钮**: 关闭对话框。|
|6 |**通知团队成员选项**: 对话框询问用户是否要创建一个帖子让其他人知道他们添加了选项卡。|
|7 |**后退按钮**: 根据对话框打开的位置转到上一步。|
|8 |**保存按钮**: 完成选项卡设置。|

### <a name="tab-authentication-with-single-sign-on"></a>使用单一登录的选项卡身份验证

可以添加一个步骤，用户必须先使用其 Microsoft 凭据登录。 此身份验证方法称为单一登录 (SSO)。

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="示例显示了选项卡身份验证屏幕。":::

### <a name="design-a-tab-setup-with-ui-templates"></a>使用 UI 模板设计选项卡设置

使用以下 Teams UI 模板之一来帮助设计选项卡设置体验: 

* [列表](../../concepts/design/design-teams-app-ui-templates.md#list): 列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目执行操作。
* [表单](../../concepts/design/design-teams-app-ui-templates.md#form): 表单是用于收集、验证和提交用户输入的结构化方式。
* [空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空状态模板可用于许多方案，包括登录、首次运行体验、错误消息等。

## <a name="view-a-tab"></a>查看选项卡

选项卡在 Teams 中提供全屏 Web 体验，可以在其中显示协作内容—如任务板和仪表板—以及重要信息。

### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab.png" alt-text="示例显示包含任务板的移动选项卡。":::

### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="例如显示使用任务板的选项卡。":::

### <a name="anatomy-tab"></a>剖析: 选项卡

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab-anatomy.png" alt-text="插图显示了选项卡的 UI 解剖。":::

|计数器|说明|
|----------|-----------|
|1|**选项卡名称**: 选项卡的导航标签。|
|2|**选项卡聊天**: 打开一个允许用户在内容旁边进行的聊天。|
|3|**webview**: 显示应用内容。|

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="插图显示了选项卡的 UI 解剖。":::

|计数器|说明|
|----------|-----------|
|1|**选项卡名称**: 选项卡的导航标签。|
|2|**选项卡溢出**: 打开选项卡操作，如重命名和删除。|
|3|**选项卡聊天**: 在右边打开一个允许用户在内容旁边进行的聊天。|
|4|**iframe**: 显示应用内容。|

### <a name="design-a-tab-with-ui-templates-and-advanced-components"></a>使用 UI 模板和高级组件设计选项卡

使用以下 Teams 模板和组件之一来帮助设计选项卡设置体验: 

* [列表](../../concepts/design/design-teams-app-ui-templates.md#list): 列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目执行操作。
* [任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board): 任务板 (有时称为看板或泳道) 是通常用于跟踪工作项或票证状态的卡片集合。
* [仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard): 仪表板是包含多个卡片的画布，可提供数据或内容的概述。
* [表单](../../concepts/design/design-teams-app-ui-templates.md#form): 表单是用于收集、验证和提交用户输入的结构化方式。
* [空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state): 空状态模板可用于许多方案，包括登录、首次运行体验、错误消息等。
* [左侧导航](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): 如果选项卡需要导航，左侧导航组件可提供帮助。 通常，应将选项卡导航保持在最低限度。

## <a name="use-a-tab-to-collaborate"></a>使用选项卡进行协作

选项卡有助于促进中心位置中有关内容的对话。

### <a name="thread-discussion"></a>线程讨论

添加新选项卡后，用户可以自动发布到频道或聊天。这不仅会通知团队成员新内容并提供指向选项卡的链接，还允许用户开始谈论选项卡。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-channel.png" alt-text="示例显示在频道线程中讨论的移动选项卡。":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="示例显示在频道线程中讨论的选项卡。":::

### <a name="tab-chat"></a>选项卡聊天

用户可以在正在查看的选项卡内容旁边进行对话。 在桌面上，聊天将打开在应用内容的一侧。

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-side-chat.png" alt-text="示例显示了带有上下文中聊天区域的移动选项卡。":::

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="示例显示了右侧有一个打开了聊天的选项卡。":::

### <a name="permissions-and-role-based-views"></a>权限和基于角色的视图

选项卡体验可能因用户权限而异。 例如，用户无需登录即可访问选项卡。 然而，另一个用户必须登录并且看到的内容略有不同。

## <a name="manage-a-tab"></a>管理选项卡

可以包含用于重命名、删除或修改选项卡的选项。

### <a name="anatomy-tab-menu"></a>剖析: 选项卡菜单

#### <a name="mobile"></a>移动设备

:::image type="content" source="../../assets/images/tabs/mobile-design-manage-tab-menu-anatomy.png" alt-text="插图显示了移动选项卡菜单的 UI 解剖。":::

|计数器|说明|
|----------|-----------|
|1|**在浏览器中打开**: 在设备的默认浏览器中打开应用。|
|2|**复制链接**: 用户可以复制和共享指向选项卡的链接。|
|3|**设置**: (可选) 添加选项卡后修改选项卡设置。|
|4|**重命名**: 用户可以为选项卡提供对频道、聊天或会议有意义的名称。|
|5|**删除**: 从频道、聊天或会议中删除选项卡。|

#### <a name="desktop"></a>桌面

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="插图显示了选项卡菜单的 UI 解剖。":::

|计数器|说明|
|----------|-----------|
|1|**设置**: (可选) 允许用户添加选项卡后修改选项卡设置。|
|2|**重命名**: 用户可以为选项卡提供对频道、聊天或会议有意义的名称。|
|3|**移除**: 从频道、聊天或会议中移除选项卡。|

## <a name="tab-notifications-and-deep-linking"></a>选项卡通知和深层链接

可以发送包含指向选项卡的深层链接消息。例如，卡片显示用户可以选择在选项卡中查看整个漏洞的漏洞数据摘要。发送有关选项卡活动的消息可在无需明确通知所有人 (即不带干扰的活动) 的情况下提高感知。 如果需要，还可以@提及特定用户。

通过以下方式之一通知用户选项卡活动:

* **机器人**: 此方法是首选方法，尤其是在选项卡线程为目标时。 选项卡的线程会话作为最近活动状态移动到视图中。 此方法还允许对通知的发送方式进行一些复杂化。
* **Message**: 用户的活动源中会显示一条包含 [选项卡深层链接](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true) 的消息。

## <a name="best-practices"></a>最佳实践

使用上述建议打造优质应用体验:

### <a name="collaboration"></a>协作

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="插图显示了如何使用选项卡导航设计。":::

#### <a name="do-facilitate-conversation"></a>执行: 促进对话

包括人们可以讨论的内容和组件。 如果它不适合在聊天、频道或会议的上下文中，则它不属于你的选项卡。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="示例显示了不使用选项卡导航设计的事物。":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a>请勿执行: 像对待任何其他网页一样对待你的选项卡

选项卡不是某人可能查看过一次的网页。 选项卡应显示用户一起完成操作所需的最重要的相关内容。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>导航

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="示例显示了如何使用选项卡导航设计。":::

#### <a name="do-limit-tasks-and-data"></a>执行: 限制任务和数据

选项卡在满足特定需求时效果最佳。 包括一组与团队或组相关的有限任务和数据。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="插图显示了不使用选项卡导航设计的事物。":::

#### <a name="dont-embed-your-entire-app"></a>请勿执行: 嵌入整个应用

使用选项卡显示具有多级导航和复杂交互的整个应用会导致信息重载。

   :::column-end:::
:::row-end:::

### <a name="setup"></a>安装

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="显示如何使用选项卡安装设计的插图。":::

#### <a name="do-keep-it-simple"></a>请执行: 保持简单

如果应用需要身份验证，请尝试集成 Microsoft 单一登录 (SSO)， 以获得更无缝的登录体验。 此外，仅包括基本信息和步骤以添加选项卡。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="插图显示了不使用选项卡安装设计的事物。":::

#### <a name="dont-have-too-many-steps"></a>请勿执行: 步骤太多

移除添加选项卡的任何不必要的步骤。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>主题

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="显示如何使用选项卡主题的插图。":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>建议：充分利用 Teams 颜色令牌

每个 Teams 主题都有自己的配色方案。 若要自动处理主题更改，请在设计中使用<a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">颜色令牌 (Fluent UI)</a>。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="插图显示了不使用选项卡主题的事物。":::

#### <a name="dont-hard-code-color-values"></a>请勿执行: 硬编码颜色值

如果不使用 Teams 颜色令牌，则设计将无法缩放，并需要更多时间进行管理。

   :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅

[选项卡边距更改](~/resources/removing-tab-margins.md)
