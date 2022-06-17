---
title: 最新视图
description: 在本模块中，了解如何在Microsoft Teams中使用通用机器人和代码示例查看最新的卡片视图
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 5c6f7d13cd884baf9ffbc1fd30cafb7cfab33295
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143618"
---
# <a name="up-to-date-cards"></a>最新卡片

现在可以在自适应卡片上向用户提供最新信息。 在Teams中包括刷新和消息编辑的组合。 在服务发生更改时动态将用户特定视图更新为其最新状态。 例如，对于项目管理或票证卡，更新注释和任务状态。 对于审批，将反映最新状态，同时提供差异化的信息和操作。

例如，用户可以在Teams对话中创建资产审批请求。 Alex 创建审批请求并将其分配给 Megan 和 Nestor。 下面是创建审批请求的两个部分：

* 可以使用 `refresh` 自适应卡片的属性应用用户特定视图。
使用用户特定视图，可以向一组用户显示带有 **“批准** ”或“ **拒绝** ”按钮的卡，并向其他用户显示没有这些按钮的卡片。

* 若要使卡片状态始终保持更新，可以使用Teams消息编辑机制。 例如，对于每次审批，机器人都可以触发对所有用户的消息编辑。 此机器人消息编辑会触发 `adaptiveCard/action` 所有自动刷新用户的调用请求，机器人可以使用更新的用户特定卡对其做出响应。

有关详细信息，请参阅 [如何执行机器人消息编辑](/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards)。

## <a name="approval-base-card"></a>审批基卡

以下代码提供了审批基卡的示例：

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>", "<Nestor's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan and Nestor**"
    }
  ]
}
```

## <a name="approval-card-with-approve-and-reject-buttons"></a>带有“审批”和“拒绝”按钮的审批卡

以下代码提供了一个带有 **“审批** ”和“ **拒绝** ”按钮的审批卡的示例：

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Nestor's user MRI>", "<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Approval Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan and Nestor**"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Approve",
      "verb": "approve",
      "data": {
            "more info": "<more info>"
      }
    },
    {
      "type": "Action.Execute",
      "title": "Reject",
      "verb": "reject",
      "data": {
            "more info": "<more info>"
      }
    }
  ]
}
```

下面是根据审批请求向用户显示的两个角色：

* 审批基卡：向不属于审批者列表的用户显示，但请求尚未获得批准或拒绝，并且不是自适应卡 JSON 属性中的`refresh`列表的一部分`userIds`。
* 带有 **“批准** ”或“ **拒绝** ”按钮的审批卡：显示给审批者列表的用户和 `userIds` 自适应卡片 JSON 属性中的 `refresh` 列表。

若要发送资产审批请求，请执行以下操作：

1. Alex 在Teams对话中提出了资产审批请求，并将其分配给 Megan 和 Nestor。
2. 机器人在会话中发送审批基卡。
3. 对话中的所有其他用户都会看到机器人发送的卡片。 为 Megan 和 Nestor 触发自动刷新，现在，当用户 MRI 添加到`userIds`自适应卡的属性中的列表中`refresh`时，他们看到具有 **“批准**”或“**拒绝**”按钮的用户特定卡片。

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="用户特定视图":::

4. Nestor 选择“ **批准** ”按钮，该按钮由该按钮提供支持 `Action.Execute`。 机器人会收到一个 `adaptiveCard/action` 调用请求，可在该请求中返回自适应卡片作为响应。
5. 机器人使用更新的卡片触发消息编辑，该卡片显示 Nestor 已批准请求，而梅根的批准正在等待。
6. 机器人消息编辑会触发 Megan 的自动刷新，她看到更新后的用户特定卡片，该卡片显示 Nestor 已批准请求，但也看到 **“批准** ”或“ **拒绝** ”按钮。 在步骤 4 和 5 中，Nestor 的用户 MRI 将从 `userIds` 此自适应卡片 JSON 的属性列表 `refresh` 中删除。 现在，仅为 Megan 触发自动刷新。

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-2.png" alt-text="最新的用户特定视图":::

7. 现在，梅根选择 **“批准** ”按钮，该按钮由它提供支持 `Action.Execute`。 机器人会收到一个 `adaptiveCard/action` 调用请求，可在该请求中返回自适应卡片作为响应。
8. 机器人使用更新的卡片触发消息编辑，该卡片显示 Nestor 和 Megan 已批准请求。
9. 机器人消息编辑不会触发任何自动刷新。 在步骤 7 和 8 中，Megan 的用户 MRI 也会从 `userIds` 此自适应卡片 JSON 的属性列表 `refresh` 中删除。

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-3.png" alt-text="最新视图":::

## <a name="adaptive-card-sent-as-response-of-adaptivecardaction-and-message-edit"></a>作为响应发送的 `adaptiveCard/action` 自适应卡片和 `message edit`

以下代码提供了作为响应发送的自适应卡片的 `adaptiveCard/action` 示例，以及 `message edit` 步骤 4 和 5 的示例：

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor**"
    }
  ]
}
```

以下代码提供了一个示例，说明通过步骤 6 的自动刷新作为调用响应发送的 `adaptiveCard/action` 自适应卡片：

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": ["<Megan's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Approval Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approval pending from **Megan**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor**"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Approve",
      "verb": "approve",
      "data": {
            "more info": "<more info>"
      }
    },
    {
      "type": "Action.Execute",
      "title": "Reject",
      "verb": "reject",
      "data": {
            "more info": "<more info>"
      }
    }
  ]
}
```

以下代码提供了作为响应发送的自适应卡片的 `adaptiveCard/action` 示例，以及 `message edit` 步骤 7 和 8 的示例：

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "acceptRejectView"
    },
    "userIds": []
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Asset Request B12"
    },
    {
      "type": "TextBlock",
      "text": "Submitted by **Alex**"
    },
    {
      "type": "TextBlock",
      "text": "Approved by **Nestor and Megan**"
    }
  ]
}
```

## <a name="code-sample"></a>代码示例

|示例名称 | Description | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| 顺序工作流自适应卡片 | 演示如何在机器人中实施顺序工作流、用户特定视图和最新自适应卡。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>另请参阅

* [使用自适应卡的通用操作](Work-with-universal-actions-for-adaptive-cards.md)
* [用户特定视图](User-Specific-Views.md)
* [表单完成反馈](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
