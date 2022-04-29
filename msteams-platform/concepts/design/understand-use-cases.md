---
title: 了解应用的用例和 Teams 功能
author: heath-hamilton
description: 本文介绍 Microsoft Teams 应用功能、规划 Teams 应用、了解应用用户及其需求、了解 Teams 应用将解决的用户问题、规划用户身份验证及其载入体验。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: dbed78461fd39f4442c67ac7ec7523ca5cc09ba5
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104376"
---
# <a name="understand-your-use-cases"></a>了解用例

在 Teams 的协作社交框架中，你可以使用 Teams 应用解决各种用户需求。 例如，在实现有效协作方面弥补差距的应用非常合适。

应用用户及其应用要求是确定你将要进行的所有应用选择的基本准则。 构建应用设计、选择功能、确定生成和测试环境以及应用分发遵循用户对应用的要求。

如果要通过应用满足用户要求，首先需要了解这些要求。

- **了解你的用户**:
  - 识别用户问题并确定用户遇到的一些常见问题的解决方案。
  - 通过查找 Teams 功能的正确组合来建立 Teams 应用，以满足用户的需求。
  - 了解用例，了解最终用户如何与应用进行交互。

- **了解问题**: 解决应用必须解决的核心问题。

- **请考虑集成**: 标识应用所需的应用和服务，例如身份验证、Microsoft Graph 或 Web 应用。

## <a name="microsoft-teams-app-features"></a>Microsoft Teams 应用功能

有多种扩展 Teams 的方法，因此每个应用都是唯一的。Teams 应用功能提供了：

- [应用功能](#app-capabilities)
- [应用程序范围](#app-scope)

### <a name="app-capabilities"></a>应用功能

功能是可在应用中生成的核心功能。 它们也称为入口点或扩展点，因为它们启用了集成和交互。

你的 Teams 应用具有以下一个或全部核心功能:

:::row:::
   :::column span="":::

#### <a name="personal-apps"></a>个人应用

[个人应用](../../concepts/design/personal-apps.md) 是一个专用空间或机器人，可帮助用户专注于自己的任务或查看相关活动。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-personal-apps-2021.png" alt-text="Teams 客户端中个人应用的外观的概念表示形式。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

#### <a name="tabs"></a>选项卡

在 [选项卡](../../tabs/what-are-tabs.md) 中显示基于 Web 的内容，用户可以在其中一起讨论和处理它。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-channel-chat-apps-2021.png" alt-text="Teams 客户端中选项卡外观的概念表示形式。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::
   :::column span="":::

#### <a name="bots"></a>机器人

对话通常会导致需要执行某些操作 (生成订单、查看代码、检查票证状态等)。 [机器人](../../bots/what-are-bots.md)可以直接在 Teams 中启动这些类型的工作流。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-bots-2021.png" alt-text="在 Teams 客户端中机器人外观的概念表示形式。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

#### <a name="message-extensions"></a>消息扩展

使用[消息扩展](../../messaging-extensions/what-are-messaging-extensions.md)，可以搜索和共享外部信息。 还可以对消息执行操作，例如基于频道帖子的内容创建帮助票证。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-messaging-extensions-2021.png" alt-text="消息扩展在 Teams 客户端中的外观的概念表示形式。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

#### <a name="meeting-extensions"></a>会议扩展

有一些 [将应用纳入 Teams 通话体验](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md) 的选项。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-meeting-extensions-2021.png" alt-text="Teams 客户端中会议扩展的外观的概念表示形式。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

#### <a name="webhooks-and-connectors"></a>Webhook 和连接器

[传入 Webhook](../../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) 是一种将通知从其他应用自动发送到 Teams 频道的简单方法。 使用 [传出 webhook](../../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)，可以向 Web 服务发送 @提及消息。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-connectors.png" alt-text="连接器在 Teams 客户端中的外观的概念表示形式。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

#### <a name="microsoft-graph-for-teams"></a>Microsoft Graph for Teams

[Microsoft Graph API for Teams](/graph/teams-concept-overview) 提供有关团队、频道、用户和消息的信息的访问权限，这些信息将帮助你为应用创建或增强功能。

   :::column-end:::

   :::column span="":::

:::image type="content" source="../../assets/images/overview-graph.png" alt-text="适用于 Teams 的 Microsoft Graph API 的概念表示形式。" border="false":::

   :::column-end:::
:::row-end:::

> [!NOTE]
> Teams 应用商店已演变:
>
> 以前，LOB 应用是通过选择磁贴上的省略号来更新的。 借助更新的 Teams 应用商店体验，现在可以通过登录到 [Teams 管理中心](https://admin.teams.microsoft.com) 来更新 LOB 应用。

### <a name="app-scope"></a>应用程序范围

应用可以具有以下范围之一:

- **个人应用体验**: 个人应用是一个专用空间或机器人，可帮助用户专注于自己的任务或查看对他们很重要的活动。
- **共享应用体验**: 团队、频道和聊天是协作空间。 这些上下文中的应用可供该空间中的每个人使用。 协作空间通常侧重于应用交互的工作流或解锁新的社交交互。

应用可以存在于不同的范围内。例如：

- 应用可以在中央共享位置 (即选项卡) 中显示数据。
- 它还可以通过个人对话界面 (即机器人) 显示相同的信息。

用户可以在画布选项卡上与应用进行交互以执行活动，也可以选择使用对话机器人执行相同的操作。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [映射用例](../../concepts/design/map-use-cases.md)

## <a name="see-also"></a>另请参阅

[集成设备功能](~/concepts/device-capabilities/device-capabilities-overview.md)
