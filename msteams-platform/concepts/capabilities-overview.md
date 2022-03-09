---
title: 了解应用功能
author: heath-hamilton
description: 描述 Teams 应用功能，例如选项卡、机器人、消息传递扩展以及 Webhook 和连接器; 应用范围，例如个人应用和共享应用
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
ms.date: 09/22/2020
keywords: 选项卡机器人消息传递扩展 Webhook 连接器
ms.openlocfilehash: ecc7ddc9ff1a80aa4eb5b37c55088f5fa5721b37
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355543"
---
# <a name="understand-microsoft-teams-app-features"></a>了解 Microsoft Teams 应用功能

可通过多种方式扩展 Teams，因此每个应用都是唯一的。 Teams 应用可以以不同的方式向用户说明自身。 Teams 应用功能包括:

- 应用功能
- 应用程序范围

例如，用户可以在画布选项卡上与应用进行交互以执行活动，也可以选择使用对话机器人执行相同的操作。 仅能有一个功能 (如 Webhook) 而其他则具有多个功能，可为用户提供各种选项。

这些功能可以存在于不同作用域。例如，应用可以在中央共享位置 (即选项卡) 中显示数据，并通过个人对话界面 (即机器人) 显示相同的信息。

## <a name="app-capabilities"></a>应用功能

若要扩展应用，必须了解协作空间中的所有核心功能和工作切入点。 可以尝试使用扩展点来构建应用。 重要的应用项目组件可帮助你正确配置应用页面。

你的 Teams 应用具有以下一个或全部核心功能:

:::row:::
   :::column span="":::
### <a name="personal-apps"></a>个人应用

[个人应用](../concepts/design/personal-apps.md) 是一个专用空间或机器人，可帮助用户专注于自己的任务或查看对他们很重要的活动。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-personal-apps-2021.png" alt-text="Teams 客户端中个人应用的外观的概念表示形式。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

### <a name="tabs"></a>选项卡

在 [选项卡](../tabs/what-are-tabs.md) 中显示基于 Web 的内容，用户可以在其中一起讨论和处理它。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-channel-chat-apps-2021.png" alt-text="Teams 客户端中选项卡外观的概念表示形式。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a>机器人

对话通常会导致需要执行某些操作 (生成订单、查看我的代码、检查票证状态等)。 [机器人](../bots/what-are-bots.md)可以直接在 Teams 中启动这些类型的工作流。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-bots-2021.png" alt-text="在 Teams 客户端中机器人外观的概念表示形式。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>消息传递扩展

使用 [消息传递扩展](../messaging-extensions/what-are-messaging-extensions.md)，可以在对话中快速共享外部信息。 还可以对消息执行操作，例如基于频道帖子的内容创建帮助票证。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-messaging-extensions-2021.png" alt-text="消息传递扩展在 Teams 客户端中的外观的概念表示形式。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="meeting-extensions"></a>会议扩展

有一些 [将应用纳入 Teams 通话体验](../apps-in-teams-meetings/design/designing-apps-in-meetings.md) 的选项。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-meeting-extensions-2021.png" alt-text="Teams 客户端中会议扩展的外观的概念表示形式。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="webhooks-and-connectors"></a>Webhook 和连接器

[传入 Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) 是一种将通知从其他应用自动发送到 Teams 频道的简单方法。 使用 [传出 webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)，向 Web 服务发送@mention消息。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-connectors.png" alt-text="连接器在 Teams 客户端中的外观的概念表示形式。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph for Teams

[Microsoft Graph API for Teams](/graph/teams-concept-overview) 提供有关团队、频道、用户和消息的信息的访问权限，这些信息可帮助你为应用创建或增强功能 (如丰富通知)。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../assets/images/overview-graph.png" alt-text="适用于 Teams 的 Microsoft Graph API 的概念表示形式。" border="false":::

   :::column-end:::
:::row-end:::

> [!NOTE]
> Teams 应用商店更新了: 以前，LOB 应用是通过选择磁贴上的省略号来更新的。 借助更新的 Teams 应用商店体验，现在可以通过登录到 [Teams 管理中心](https://admin.teams.microsoft.com) 来更新 LOB 应用。

## <a name="choose-the-correct-scope-for-your-app"></a>为应用选择正确的范围

可从以下选项中选择应用范围:

- 个人应用体验: 个人应用是一个专用空间或机器人，可帮助用户专注于自己的任务或查看对他们很重要的活动。
- 共享应用体验: 团队、频道和聊天是协作空间。 这些上下文中的应用可供该空间中的每个人使用。 协作空间通常侧重于应用交互的工作流或解锁新的社交交互。

## <a name="see-also"></a>另请参阅

* [生成适用于 Teams 的应用](../overview.md)
* [构建第一个 Microsoft Teams 应用](../build-your-first-app/build-first-app-overview.md)