---
title: 适用于桌面、Web 和移动的设计选项卡
description: 了解如何为桌面、Teams和移动设备设计 Teams 选项卡，以及如何获取 Microsoft Teams UI 工具包。
author: heath-hamilton
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: f1823a064cd182d0271aa97bef58ec724c7819b3
ms.sourcegitcommit: 33a43c61f27ae750776616b2cf90159455d8ba6c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2021
ms.locfileid: "52721841"
---
# <a name="design-your-tab-for-microsoft-teams"></a>设计选项卡Microsoft Teams

选项卡是应用内容的大型画布。 为了指导应用设计，以下信息介绍了并说明了用户如何在应用中添加、使用和管理选项卡Teams。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

你可以找到全面的选项卡设计指南，包括你可以根据需要获取和修改的元素，Microsoft Teams UI 工具包。 UI 工具包还具有辅助功能和响应式大小调整等基本主题，此处未介绍这些主题。

> [!div class="nextstepaction"]
> [获取 Microsoft Teams UI Kit （用户）](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a>添加选项卡

你可以从 AppSource Teams应用商店 (选项卡) 以下上下文之一：

* 聊天
* 频道
* 会议 (之前、期间或之后) 

# <a name="desktop"></a>[桌面](#tab/desktop)

下面的示例展示了用户如何在频道中添加选项卡。

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="示例显示正在频道中添加的选项卡。" border="false":::

# <a name="mobile"></a>[移动](#tab/mobile)

用户可以通过选择频道中的"更多"按钮来访问选项卡 (例如) 添加这些选项卡的聊天或聊天。

:::image type="content" source="../../assets/images/tabs/mobile-design-access-tab.png" alt-text="示例显示正在频道中添加的移动选项卡。" border="false":::

---

## <a name="set-up-a-tab"></a>设置选项卡

有一个简短的设置过程，可以将应用添加为频道、聊天或会议选项卡。体验很大程度上取决于你。 例如，你可以拥有如何使用应用的说明和一些可选设置。 如果需要对用户进行身份验证，请在此处包括登录步骤。

### <a name="tab-configuration-dialog"></a>选项卡配置对话框

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="示例显示选项卡配置模式。" border="false":::

### <a name="anatomy-tab-configuration-dialog"></a>结构：选项卡配置对话框

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="显示选项卡配置模式 UI 分析的图示。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**应用徽标**：应用的全彩色应用徽标。|
|2|**应用名称**：应用的完整名称。|
|3|**iframe：** 应用内容响应空间 (例如选项卡设置或身份验证) 。|
|4 |**关于链接**：打开一个对话框，其中显示有关应用的详细信息，例如完整说明、应用所需的权限以及指向隐私策略和服务条款的链接。|
|5 |**关闭按钮**：关闭对话框。|
|6 |**通知团队成员选项**：对话框询问用户是否要创建一个帖子，让其他人知道他们添加了选项卡。|
|7 |**"后退**"按钮：根据对话框打开位置转到上一步。|
|8 |**保存按钮**：完成选项卡设置。|

### <a name="tab-authentication-with-single-sign-on"></a>使用单一登录的选项卡身份验证

你可以添加一个步骤，用户必须先使用其 Microsoft 凭据登录。 此身份验证方法称为 SSO (单一) 。

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="示例显示选项卡身份验证屏幕。" border="false":::

### <a name="design-a-tab-setup-with-ui-templates"></a>使用 UI 模板设计选项卡设置

使用以下 UI 模板Teams之一来帮助设计选项卡设置体验：

* [列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目采取操作。
* [表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单用于以结构化方式收集、验证和提交用户输入。
* [空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。

## <a name="view-a-tab"></a>查看选项卡

选项卡提供了全屏 Web 体验，Teams显示协作内容（如任务板和仪表板）和重要信息。

# <a name="desktop"></a>[桌面](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="示例显示一个包含任务板的选项卡。" border="false":::

# <a name="mobile"></a>[移动](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab.png" alt-text="示例显示一个包含任务板的移动选项卡。" border="false":::

---

### <a name="anatomy-tab"></a>结构：选项卡

# <a name="desktop"></a>[桌面](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="显示选项卡的 UI 分析的图示。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**选项卡名称**：选项卡的导航标签。|
|2|**Tab 溢出**：打开选项卡操作，如重命名和删除。|
|3|**选项卡聊天**：在右侧打开聊天，允许用户在内容旁边进行对话。|
|4 |**iframe：** 显示应用内容。|

# <a name="mobile"></a>[移动](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-view-tab-anatomy.png" alt-text="显示选项卡的 UI 分析的图示。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**选项卡名称**：选项卡的导航标签。|
|2|**选项卡聊天**：打开允许用户在内容旁进行对话的聊天。|
|3|**webview：** 显示应用内容。|

---

### <a name="designing-a-tab-with-ui-templates-and-advanced-components"></a>使用 UI 模板和高级组件设计选项卡

使用以下模板和Teams之一来帮助设计选项卡体验：

* [列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目采取操作。
* [任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board)：任务板（有时称为看板或街道）是一组卡片，通常用于跟踪工作项或票证的状态。
* [仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard)：仪表板是包含多个卡片的画布，可提供数据或内容的概述。
* [表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单用于以结构化方式收集、验证和提交用户输入。
* [空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。
* [左侧导航](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav)：如果你的选项卡需要一些导航，左侧导航组件会有所帮助。 通常，应使 Tab 键导航保持在最低程度。

## <a name="use-a-tab-to-collaborate"></a>使用选项卡进行协作

选项卡有助于就中心位置的内容展开对话。

### <a name="thread-discussion"></a>线程讨论

用户一旦添加了新选项卡，就可以自动发布至频道或聊天。这不仅向团队成员通知新内容并提供指向选项卡的链接，还允许用户开始讨论选项卡。

# <a name="desktop"></a>[桌面](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="示例显示正在频道线程中讨论的选项卡。" border="false":::

# <a name="mobile"></a>[移动](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-channel.png" alt-text="示例显示在频道线程中讨论的移动选项卡。" border="false":::

---

### <a name="tab-chat"></a>选项卡聊天

用户可以在正在查看的选项卡内容旁边进行对话。 在桌面上，聊天将打开到应用内容的一侧。

# <a name="desktop"></a>[桌面](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="示例显示一个在右侧打开聊天的选项卡。" border="false":::

# <a name="mobile"></a>[移动](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-use-tab-side-chat.png" alt-text="示例显示具有上下文内聊天区域的移动选项卡。" border="false":::

---

### <a name="permissions-and-role-based-views"></a>权限和基于角色的视图

选项卡体验可能因用户的权限不同而不同。 例如，一个用户无需登录即可访问选项卡。 但是，另一个用户必须登录并查看略有不同的内容。

## <a name="manage-a-tab"></a>管理选项卡

您可以包括用于重命名、删除或修改选项卡的选项。

### <a name="anatomy-tab-menu"></a>结构：选项卡菜单

# <a name="desktop"></a>[桌面](#tab/desktop)

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="显示选项卡菜单的 UI 分析的图示。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**设置**： (可选) 允许用户在添加选项卡后修改其设置。|
|2|**重命名**：用户可以为选项卡指定对频道、聊天或会议有意义的名称。|
|3|**删除**：从频道、聊天或会议中删除选项卡。|

# <a name="mobile"></a>[移动](#tab/mobile)

:::image type="content" source="../../assets/images/tabs/mobile-design-manage-tab-menu-anatomy.png" alt-text="显示移动选项卡菜单的 UI 分析的图示。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**在浏览器中打开**：在设备的默认浏览器中打开应用。|
|2|**复制链接**：用户可以复制并共享指向选项卡的链接。|
|3|**设置： (** 选项卡) 后修改选项卡的设置的可选选项。|
|4 |**重命名**：用户可以为选项卡指定对频道、聊天或会议有意义的名称。|
|5 |**删除**：从频道、聊天或会议中删除选项卡。|

---

## <a name="tab-notifications-and-deep-linking"></a>选项卡通知和深层链接

你可以向选项卡发送包含深层链接的邮件。例如，卡片显示用户可选择在选项卡中查看整个 Bug 的 Bug 数据的摘要。发送有关选项卡活动的消息可提升感知度，而无需明确通知 (，即无噪音活动) 。 如果需要，@mention特定用户。

通过以下方法之一通知用户选项卡活动：

* **Bot：** 此方法是首选方法，尤其是在选项卡线程具有目标时。 选项卡的线程对话将移动到最近处于活动状态的视图中。 此方法还允许通知发送方式的一些复杂程度。
* **消息**：用户的活动源中显示一条消息，包含指向选项卡 [的深层链接](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true)。

## <a name="best-practices"></a>最佳做法

使用这些建议创建高质量的应用体验：

### <a name="collaboration"></a>协作

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="插图显示选项卡导航设计如何操作。" border="false":::

#### <a name="do-facilitate-conversation"></a>应做：促进对话

包括用户可以讨论的内容和组件。 如果它不适合聊天、频道或会议上下文，则它不属于你的选项卡。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="示例显示不与选项卡导航设计一起执行哪些操作。" border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a>请勿：将选项卡视为任何其他网页

选项卡不是某人可能查看过一次的网页。 选项卡应显示用户共同完成某些任务所需的最重要的相关内容。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>导航

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="显示选项卡导航设计要执行哪些操作的示例。" border="false":::

#### <a name="do-limit-tasks-and-data"></a>操作：限制任务和数据

选项卡在满足特定需求时效果最佳。 包含一组有限的与团队或组相关的任务和数据。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="插图显示不与选项卡导航设计有关的内容。" border="false":::

#### <a name="dont-embed-your-entire-app"></a>请勿：嵌入整个应用

使用选项卡显示具有多级导航和复杂交互的整个应用会导致信息过载。

   :::column-end:::
:::row-end:::

### <a name="setup"></a>设置

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="插图显示选项卡设置设计要执行哪些操作。" border="false":::

#### <a name="do-keep-it-simple"></a>应做之事：保持简单

如果你的应用需要身份验证，请尝试将 Microsoft 单一登录 (SSO) 集成，实现更加无缝的登录体验。 此外，仅包括添加选项卡的必需信息和步骤。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="插图显示与选项卡设置设计不一样。" border="false":::

#### <a name="dont-have-too-many-steps"></a>不要：步骤过多

删除添加选项卡的不必要的步骤。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>主题

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="插图显示使用制表位设置要执行哪些操作。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>应做：利用Teams令牌

每个Teams主题都有自己的配色方案。 若要自动处理主题更改，请 <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank"> (Fluent UI </a>) 颜色标记。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="插图显示不与选项卡设置有关的内容。" border="false":::

#### <a name="dont-hard-code-color-values"></a>请勿：硬编码颜色值

如果不使用颜色令牌Teams，你的设计将不太可扩展，并且需要更多的时间进行管理。

   :::column-end:::
:::row-end:::
