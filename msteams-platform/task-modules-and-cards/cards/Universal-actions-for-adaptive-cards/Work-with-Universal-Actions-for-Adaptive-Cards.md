---
title: 使用自适应卡的通用操作
description: 了解如何使用自适应卡的通用操作，包括自适应卡片的 UniversalActions 架构、刷新模型和向后兼容性
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 17dd7fd611c593c3f5de0237e0aa61885ac630c0
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143877"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a>使用自适应卡的通用操作

自适应卡的通用操作提供了一种为 Teams 和 Outlook 实施基于自适应卡的方案的方法。 本文档涵盖以下主题：

* [用于自适应卡的通用操作的架构](#schema-for-universal-actions-for-adaptive-cards)
* [刷新模型](#refresh-model)
* [`adaptiveCard/action` 调用活动](#adaptivecardaction-invoke-activity)
* [向后兼容性](#backward-compatibility)

## <a name="quick-start-guide-to-use-universal-actions-for-adaptive-cards-in-teams"></a>有关在 Teams 中使用自适应卡的通用操作的快速入门指南

1. 将 `Action.Submit` 的所有实例替换为 `Action.Execute` 以更新 Teams 上的现有方案。
2. 如果要使用自动刷新模型或方案需要用户特定视图，请向自适应卡添加 `refresh` 子句。

    >[!NOTE]
    > 指定属性以 `userIds` 标识哪些用户获取自动更新。

3. 处理机器人中的 `adaptiveCard/action` 调用请求。
4. 使用调用请求的上下文来响应为用户创建的卡片。

    > [!NOTE]
    > 每当机器人因处理 `Action.Execute` 而返回新卡片时，响应必须符合响应格式。

## <a name="schema-for-universal-actions-for-adaptive-cards"></a>自适应卡的通用操作架构

自适应卡架构版本 1.4 中引入了自适应卡的通用操作。 若要有效地使用自适应卡，自适应卡的 `version` 属性必须设置为 1.4。

> [!NOTE]
> 将 `version` 属性设置为 1.4 会使自适应卡与平台或应用程序的较旧客户端（例如 Outlook 和 Teams）不兼容，因为它们不支持自适应卡的通用操作。

如果将卡片版本设置为小于 1.4 并使用属性 `refresh` 和/或 `Action.Execute`，则会发生以下情况：

| Client | 行为 |
| :-- | :-- |
| Teams | 卡片停止工作。 卡片不会刷新，`Action.Execute` 也不会呈现，具体取决于Teams 客户端的版本。 为确保在 Teams 中实现最大兼容性，请在 fallback 属性中使用 `Action.Submit` 定义 `Action.Execute`。 |

有关如何支持旧客户端的详细信息，请参阅[向后兼容性](#backward-compatibility)。

### <a name="actionexecute"></a>Action.Execute

创作自适应卡片时，请将 `Action.Submit` 和 `Action.Http` 替换为 `Action.Execute`。 `Action.Execute` 的架构与 `Action.Submit` 类似。

有关详细信息，请参阅 [Action.Execute 架构和属性](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)。

现在，可以使用刷新模型允许自适应卡自动更新。

## <a name="refresh-model"></a>刷新模型

若要自动刷新自适应卡，请定义其 `refresh` 属性，该属性会嵌入类型为 `Action.Execute` 的操作和 `userIds` 数组。

有关详细信息，请参阅[刷新架构和属性](/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism)。

## <a name="user-ids-in-refresh"></a>刷新中的用户 ID

以下是刷新中 UserIds 的功能：

* UserIds 是一组用户 MRI，它是自适应卡中 `refresh` 属性的一部分。

* 如果 `userIds` 列表属性在卡片的刷新部分指定为 `userIds: []`，则卡片不会自动刷新。 相反，**刷新卡** 片选项将显示在Teams Web 客户端或桌面的三点菜单中，在移动Teams的长按下文菜单中，即Android或iOS手动刷新卡片。 或者，如果方案涉及Teams组聊天或频道中的 <=60 个成员，则可以选择完全跳过 `userIds` refresh 属性。 如果组或频道<=60 个用户，则Teams客户端会自动调用所有用户的刷新调用。

* 添加 UserIds 属性是因为 Teams 中的频道可以包含大量成员。 如果所有成员同时查看频道，则无条件的自动刷新会导致对机器人进行多次并发调用。 必须始终包含 `userIds` 属性，以确定哪些用户必须获得自动刷新，最多 *60 （六十）个用户 MRI*。

* 可以提取 Teams 对话成员的用户 MRI。 有关如何在自适应卡的刷新部分中添加 userIds 列表的详细信息，请参阅[提取名单或用户个人资料](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)。

 可以使用以下示例获取频道、群聊或 1:1 聊天的用户 MRI：

 1. 使用 TurnContext  

     `userMRI= turnContext.Activity.From.Id`

 1. 使用 GetMemberAsync 方法
  
     `var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);var userMRI = member.Id;`

* 示例 Teams 用户 MRI 为 `29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`

> [!NOTE]
> 在 Outlook 中忽略 `userIds` 属性，并且始终自动激活 `refresh` 属性。 Outlook 中没有缩放问题，因为用户在不同时间查看卡片。

下一步是使用 `adaptiveCard/action` 调用活动来了解执行 `Action.Execute` 后必须发出的请求。

## <a name="adaptivecardaction-invoke-activity"></a>`adaptiveCard/action` 调用活动

在客户端中执行 `Action.Execute` 时，会对机器人进行新类型的调用活动 `adaptiveCard/action`。

有关详细信息，请参阅[典型 `adaptiveCard/action` 调用活动的请求格式和属性](/adaptive-cards/authoring-cards/universal-action-model#request-format)。

有关详细信息，请参阅[典型 `adaptiveCard/action` 调用活动的响应格式和属性以及支持的响应类型](/adaptive-cards/authoring-cards/universal-action-model#response-format)。

接下来，可以跨不同平台向旧客户端应用向后兼容性，并使自适应卡兼容。

## <a name="backward-compatibility"></a>向后兼容性

利用自适应卡的通用操作，可以设置属性来实现与较旧版本的 Outlook 和 Teams 向后兼容。

### <a name="teams"></a>Teams

若要确保自适应卡与旧版 Teams 向后兼容，必须包括 `fallback` 属性并将其值设置为 `Action.Submit`。 此外，机器人代码必须同时处理 `Action.Execute` 和 `Action.Submit`。

有关详细信息，请参阅 [Teams 上的向后兼容性](/adaptive-cards/authoring-cards/universal-action-model#teams)。

## <a name="code-samples"></a>代码示例

|示例名称 | Description | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Teams 餐饮机器人 | 使用自适应卡片创建接受食品订单的机器人。 |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| 尚不可用 |
| 顺序工作流自适应卡片 | 演示如何在机器人中实施顺序工作流、用户特定视图和最新自适应卡。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [视图](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) 。|

## <a name="see-also"></a>另请参阅

* [Teams 中的自适应卡片操作](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [机器人的工作方式](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [顺序工作流](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/sequential-workflows.md)
* [最新卡片](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/up-to-date-views.md)
* [表单完成反馈](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
