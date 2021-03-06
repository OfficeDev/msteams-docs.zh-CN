---
title: 使用自适应卡的通用操作
description: 使用自适应卡片的通用操作。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 4361f1c7774837b728c6382df4e62e00ea912e35
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649697"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a>使用自适应卡的通用操作

自适应卡片的通用操作提供了一种为用户和用户实现基于自适应卡片Teams Outlook。 本文档涵盖以下内容：

* [用于自适应卡片的通用操作架构](#schema-for-universal-actions-for-adaptive-cards)
* [刷新模型](#refresh-model)
* [`adaptiveCard/action` 调用活动](#adaptivecardaction-invoke-activity)
* [向后兼容性](#backward-compatibility)

## <a name="quick-start-guide-to-leverage-universal-actions-for-adaptive-cards-in-teams"></a>快速入门指南，用于将通用操作用于自适应卡片Teams

1. 将 的所有 实例 `Action.Submit` 替换为 ， `Action.Execute` 以更新现有Teams。
2. 如果你希望利用自动刷新模型或你的方案需要特定于用户的视图，则向 `refresh` 自适应卡片中添加子句。

    >[!NOTE]
    > 指定 `userIds` 要标识哪些用户获得自动更新的属性。

3. 处理 `adaptiveCard/action` 机器人中的调用请求。
4. 使用调用请求的上下文通过专为用户创建的卡片进行响应。

    > [!NOTE]
    > 只要机器人处理 后返回新卡， `Action.Execute` 响应就必须符合响应格式。

## <a name="schema-for-universal-actions-for-adaptive-cards"></a>自适应卡片的通用操作架构

自适应卡片的通用操作在自适应卡片架构版本 1.4 中引入。 若要有效地使用自适应卡片，必须将自适应卡片的 属性 `version` 设置为 1.4。

> [!NOTE]
> 将 该属性设置为 1.4 会使自适应卡片与平台或应用程序（如 Outlook 和 Teams）的较旧客户端不兼容，因为它们不支持自适应卡片的通用操作 `version` 。

如果将卡版本设置为小于 1.4，并使用 属性 和 或 两者之一， `refresh` `Action.Execute` 将发生以下情况：

| 客户端 | 行为 |
| :-- | :-- |
| Teams | 你的卡片停止工作。 卡片不会刷新， `Action.Execute` 并且不会呈现，具体取决于 Teams 版本。 若要确保应用程序的最大Teams，请通过 回退 `Action.Execute` `Action.Submit` 属性中的 定义 。 |

若要详细了解如何支持旧客户端，请参阅 [向后兼容性](#backward-compatibility)。

### <a name="actionexecute"></a>Action.Execute

创作自适应卡片时，请将 和 `Action.Submit` `Action.Http` 替换为 `Action.Execute` 。 的 `Action.Execute` 架构类似于 `Action.Submit` 。

有关详细信息，请参阅Action.Exe[ 和属性](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)。

现在，可以使用刷新模型允许自适应卡片自动更新。

## <a name="refresh-model"></a>刷新模型

若要自动刷新自适应卡片，请定义其 `refresh` 属性，这将嵌入类型和 `Action.Execute` 数组 `userIds` 的操作。

有关详细信息，请参阅 [刷新架构和属性](/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism)。

## <a name="user-ids-in-refresh"></a>刷新中的用户 ID

以下是刷新中的 UserIds 的功能：

* UserIds 是用户 MRI 的数组，它是自适应卡片 `refresh` 中属性的一部分。

* 如果在卡片的刷新部分中指定了 list 属性，则不会自动 `userIds` `userIds: []` 刷新该卡片。 而是 **在** Web 或桌面的三点菜单和移动设备（即 Android 或 iOS）中的长按上下文菜单中向用户显示"刷新卡片"选项，以手动刷新卡片。

* 添加 UserIds 属性是因为Teams频道可以包含大量成员。 如果所有成员同时查看频道，则无条件自动刷新会导致对机器人进行许多并发呼叫。 若要避免这种情况，必须始终包括 属性，以确定哪些用户必须自动刷新，最多 `userIds` *60 (60*) MRIs 。

* 若要详细了解如何提取对话Teams用户 MRIs 以在自适应卡片刷新部分添加 userIds 列表，请参阅提取[名单或用户配置文件](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)。

* 用户 MRI Teams示例`29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`

> [!NOTE]
> 该属性 `userIds` 在属性Outlook， `refresh` 并且始终自动激活。 由于用户在不同时间查看Outlook，因此在卡片中不存在缩放问题。

下一步是使用 `adaptiveCard/action` 调用活动了解在执行后必须提出 `Action.Execute` 哪些请求。

## <a name="adaptivecardaction-invoke-activity"></a>`adaptiveCard/action` 调用活动

When `Action.Execute` is executed in the client， a new type of Invoke activity `adaptiveCard/action` is made to your bot.

有关详细信息，请参阅典型调用活动的请求 [格式 `adaptiveCard/action` 和属性](/adaptive-cards/authoring-cards/universal-action-model#request-format)。

有关详细信息，请参阅具有受支持的 [响应类型的典型 `adaptiveCard/action` 调用活动的响应格式和属性](/adaptive-cards/authoring-cards/universal-action-model#response-format)。

接下来，你可以跨不同平台将向后兼容性应用到较旧的客户端，并兼容自适应卡片。

## <a name="backward-compatibility"></a>向后兼容性

自适应卡片的通用操作允许你设置属性，以便向后兼容早期版本的 Outlook 和 Teams。

### <a name="teams"></a>Teams

若要确保自适应卡片与旧版卡片的向后Teams，必须包含 属性，并 `fallback` 设置其值 `Action.Submit` 。 此外，自动程序代码必须同时处理 `Action.Execute` 和 `Action.Submit` 。

有关详细信息，请参阅[上向后兼容性Teams。](/adaptive-cards/authoring-cards/universal-action-model#teams)

## <a name="code-sample"></a>代码示例

|示例名称 | 说明 | .NETCore |
|----------------|-----------------|--------------|
| Teams机器人 | 创建使用自适应卡片接受食物订单的简单机器人。 |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)|

## <a name="see-also"></a>另请参阅

* [用户中的自适应卡片Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [机器人的工作方式](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
