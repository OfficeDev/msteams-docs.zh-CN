---
title: 设计桌面和 web 的选项卡
description: 了解如何设计 "团队" 选项卡 (桌面和 web) 并获取 Microsoft 团队 UI 工具包。
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 692a21c78dc86cbca5bf248e55d0332bd71c6b92
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604654"
---
# <a name="designing-your-tab-for-microsoft-teams-desktop-and-web"></a>设计用于 Microsoft 团队桌面和 web 的选项卡

选项卡是用于便于协作的内容的大型画布。 若要指导您的应用程序设计，以下信息介绍并说明了用户如何在团队中添加、使用和管理选项卡。

## <a name="microsoft-teams-ui-kit"></a>Microsoft 团队 UI 工具包

您可以在 Microsoft 团队 UI 工具包中找到全面的选项卡设计指南，包括您可以在需要时获取和修改的元素。 UI 工具包还包含此处未介绍的辅助功能和响应大小等基本主题。

> [!div class="nextstepaction"]
> [ (Figma) 获取 Microsoft 团队 UI 工具包 ](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-tab"></a>添加选项卡

您可以从 "团队" 存储 ("AppSource") 或以下上下文之一添加选项卡：

* 聊天
* 频道
* 会议 (之前、会议期间或会议之后) 

下面的示例演示如何在通道中添加制表符。

:::image type="content" source="../../assets/images/tabs/design-add-tab.png" alt-text="示例显示在通道中添加的选项卡。" border="false":::

## <a name="set-up-a-tab"></a>设置选项卡

有一个将应用添加为频道、聊天或会议选项卡的短安装过程。体验主要由你来掌握。 例如，您可以对如何使用应用程序和一些可选设置进行说明。 如果需要对用户进行身份验证，请在此处加入登录步骤。

### <a name="tab-configuration-modal"></a>选项卡配置模式

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-config.png" alt-text="示例显示了选项卡配置模式。" border="false":::

### <a name="anatomy-tab-configuration-modal"></a>剖析：选项卡配置模式

:::image type="content" source="../../assets/images/tabs/test.png" alt-text="显示选项卡配置模式的 UI 剖析的插图。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**应用徽标**：应用的完整颜色应用徽标。|
|2 |**应用程序名称**：应用程序的完整名称。|
|3 |**iframe**：应用内容的响应空间 (例如，选项卡设置或身份验证) 。|
|4 |**关于链接**：打开一个对话框，显示有关该应用程序的详细信息，如完整说明、应用程序所需的权限以及指向您的隐私策略和服务条款的链接。
|5 |"**关闭" 按钮**：关闭模式。|
|6 |**通知工作组成员选项**：模式询问您是否要创建一篇文章，让其他人知道您添加了一个选项卡。|
|7 |"**后退" 按钮**：根据对话框打开的位置转到上一步。|
|8 |"**保存" 按钮**：完成选项卡设置。|

### <a name="tab-authentication-with-single-sign-on"></a>单一登录的选项卡身份验证

您可以添加用户首次使用其 Microsoft 凭据登录时必须登录的步骤。 此身份验证方法称为 (SSO) 的单一登录。

:::image type="content" source="../../assets/images/tabs/design-set-up-tab-auth.png" alt-text="示例显示一个 tab 身份验证屏幕。" border="false":::

### <a name="designing-a-tab-setup-with-ui-templates"></a>使用 UI 模板设计选项卡设置

使用以下团队 UI 模板之一可帮助设计您的选项卡设置体验：

* [列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可浏览的格式显示相关项目，并允许用户对整个列表或单个项目执行操作。
* [表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单以结构化方式收集、验证和提交用户输入。
* [空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。

## <a name="view-a-tab"></a>查看选项卡

选项卡在团队中提供了全屏 web 体验，您可以在其中显示协作内容（如任务板和仪表板）以及重要信息。

:::image type="content" source="../../assets/images/tabs/design-view-tab.png" alt-text="示例显示带有任务板的选项卡。" border="false":::

### <a name="anatomy-tab"></a>剖析： Tab

:::image type="content" source="../../assets/images/tabs/design-view-tab-anatomy.png" alt-text="显示选项卡的 UI 剖析的插图。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**选项卡名称**：选项卡的导航标签。|
|2 |**选项卡溢出**：打开选项卡操作，例如 "重命名" 和 "删除"。|
|3 |**选项卡聊天**：在右侧打开聊天线程，使用户可以在内容旁边进行对话。|
|4 |**iframe**：显示您的选项卡的内容。

### <a name="designing-a-tab-with-ui-templates"></a>设计包含 UI 模板的选项卡

使用以下团队 UI 模板之一来帮助设计您的选项卡体验：

* [列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可浏览的格式显示相关项目，并允许用户对整个列表或单个项目执行操作。
* [任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board)：任务板（有时称为 "看板母板" 或 "泳道"）是用于跟踪工作项或票证状态的卡片的集合。
* [仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard)：仪表板是一个包含多个卡片的画布，可提供数据或内容的概述。
* [表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单以结构化方式收集、验证和提交用户输入。
* [空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。
* [左侧](../../concepts/design/design-teams-app-ui-templates.md#left-nav)导航：如果您的选项卡需要一些导航，则左侧导航模板可有所帮助。 通常情况下，应保持最小的选项卡导航。

## <a name="use-a-tab-to-collaborate"></a>使用选项卡进行协作

选项卡有助于促进有关中心位置中的内容的对话。

### <a name="thread-discussion"></a>线程讨论

用户在添加新选项卡后，可以自动将其发布到频道或聊天。这不仅会通知团队成员新内容并提供指向选项卡的链接，它还允许用户开始谈论选项卡。

:::image type="content" source="../../assets/images/tabs/design-use-tab-channel.png" alt-text="示例显示了在通道线程中讨论的选项卡。" border="false":::

### <a name="side-by-side-discussion"></a>并排讨论

在查看该选项卡的内容时，用户可以进行对话。

:::image type="content" source="../../assets/images/tabs/design-use-tab-side-chat.png" alt-text="示例显示右侧的 &quot;聊天&quot; 处于打开状态的选项卡。" border="false":::

### <a name="permissions-and-role-based-views"></a>权限和基于角色的视图

根据用户的权限，用户的选项卡体验可能有所不同。 例如，一个用户无需登录即可访问该选项卡。 但是，另一个用户必须签名，并且将看到略有不同的内容。

## <a name="manage-a-tab"></a>管理选项卡

可以包括用于重命名、删除或修改选项卡的选项。

### <a name="anatomy-tab-menu"></a>剖析：选项卡菜单

:::image type="content" source="../../assets/images/tabs/design-manage-tab-menu-anatomy.png" alt-text="显示选项卡菜单的 UI 剖析的插图。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**设置**： (可选) 允许用户在添加选项卡后修改该选项卡的设置。|
|2 |**重命名**：允许用户为选项卡提供对团队更有意义的名称。|
|3 |**删除**：从频道、聊天或会议中删除选项卡。|

## <a name="tab-notifications-and-deep-linking"></a>选项卡通知和深层链接

您可以向您的选项卡发送带有深层链接的邮件。例如，卡片显示了用户可以选择在选项卡中查看整个 bug 的 bug 数据的摘要。发送有关选项卡活动的邮件可提高感知功能，而无需明确通知每个人 (即，活动没有噪音) 。 如果需要，还可以 @mention 特定用户。

通过以下方式之一通知用户选项卡活动：

* **Bot**：此方法是首选的如果对 tab 线程线程设定。 该选项卡的线程对话在最近活动的视图中移动到视图中。 此方法还允许在通知的发送方式方面有一些复杂之处。
* **消息**：在用户的活动源中显示一条消息，其中包含 [指向该选项卡的深层链接](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true)。

## <a name="best-practices"></a>最佳做法

### <a name="collaboration"></a>协作

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-do.png" alt-text="图示演示如何处理选项卡导航设计。" border="false":::

#### <a name="do-facilitate-conversation"></a>Do：促进对话

包含人们可以谈论的内容和组件。 如果它不适合聊天、频道或会议的上下文，它不会显示在您的选项卡中。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-collaboration-dont.png" alt-text="图示演示了不使用选项卡导航设计。" border="false":::

#### <a name="dont-treat-your-tab-like-any-other-webpage"></a>请勿：像其他网页那样处理选项卡

一个选项卡不是某人可能只查看一次的网页。 选项卡应显示用户在实现这些功能时所需的最重要的相关内容。

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>导航

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-do.png" alt-text="图示演示如何处理选项卡导航设计。" border="false":::

#### <a name="do-limit-tasks-and-data"></a>操作：限制任务和数据

在满足特定需求时，选项卡的工作效果最佳。 包含与团队或组相关的一组有限的任务和数据。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-nav-dont.png" alt-text="图示演示了不使用选项卡导航设计。" border="false":::

#### <a name="dont-embed-your-entire-app"></a>请勿：嵌入整个应用程序

使用选项卡显示包含多级导航和复杂交互组件的整个应用程序将导致信息超载。

   :::column-end:::
:::row-end:::

### <a name="setup"></a>设置

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-do.png" alt-text="图中显示如何处理选项卡设置设计。" border="false":::

#### <a name="do-keep-it-simple"></a>操作：将其简化

如果您的应用程序需要身份验证，请尝试将 Microsoft single sign-on 集成 (SSO) ，以实现更无缝的登录体验。 此外，仅包含必要的信息和添加该选项卡的步骤。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-setup-dont.png" alt-text="图中显示与选项卡设置设计无关的操作。" border="false":::

#### <a name="dont-have-too-many-steps"></a>请勿：执行过多的步骤

删除添加选项卡的任何不必要的步骤。

   :::column-end:::
:::row-end:::

### <a name="theming"></a>主题

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-do.png" alt-text="图示演示如何处理选项卡主题。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a>Do：利用团队颜色令牌

每个团队主题都有自己的配色方案。 若要自动处理主题更改，请在设计中使用 <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank"> (熟知的 UI) 的颜色标记 </a> 。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/tabs/design-tab-theming-dont.png" alt-text="图中显示与选项卡主题无关的操作。" border="false":::

#### <a name="dont-hard-code-color-values"></a>不：硬编码颜色值

如果您不使用团队颜色令牌，则设计的可伸缩性较小并需要更多时间来管理。

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a>验证设计

如果计划将应用程序发布到 AppSource，则应了解通常会在提交期间导致应用程序失败的设计问题。

> [!div class="nextstepaction"]
> [检查设计验证准则](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
