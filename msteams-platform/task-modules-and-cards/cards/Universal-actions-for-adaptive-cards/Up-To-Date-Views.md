---
title: 最新视图
description: 使用通用自动程序查看最新视图的示例
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 2027d07961929fb40e7afc3ee268e1267b235a02
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088825"
---
# <a name="up-to-date-cards"></a>最新卡片

现在可以在自适应卡片上将刷新和邮件编辑组合在一起，为用户提供最新Teams。 这样，当服务发生变化时，你可以动态地将用户特定视图更新到其最新状态。 例如，对于项目管理或票证卡，可以更新注释和任务的状态。 在批准的情况下，最新状态会反映出来，同时还提供不同的信息和操作。

例如，用户可以在资源审批对话中Teams请求。 Alex 创建审批请求并将其分配给 Megan 和 Nestor。 以下是创建审批请求的两个部分：

* 可以使用自适应卡片的 属性利用用户 `refresh` 特定视图。
使用用户特定视图一个可以向一组用户显示具有"批准"或"拒绝"按钮的卡片，并且向其他用户显示没有这些按钮的卡片。

* 若要始终更新卡片状态，Teams邮件编辑机制。 例如，每次审批时，自动程序都可以触发对所有用户的邮件编辑。 此自动程序消息编辑会触发所有自动刷新用户的调用请求，自动程序可以使用更新的用户特定 `adaptiveCard/action` 卡片对此进行响应。

有关详细信息，请参阅 [如何执行自动程序消息编辑](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards)。

## <a name="approval-base-card"></a>审批基本卡

以下代码提供了一个审批基本卡示例：

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

## <a name="approval-card-with-approve-and-reject-buttons"></a>具有"批准"和"拒绝"按钮的审批卡片

以下代码提供了一个包含"批准"和"拒绝"**按钮的审批卡片** 示例：

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

下面是根据用户参与审批请求而向用户显示的两个角色：

* 审批基本卡：向以下用户显示：这些用户不是审批者列表的一部分，并且尚未批准或拒绝请求，并且不是自适应卡片 `userIds` JSON 属性中的 `refresh` 列表的一部分。
* 具有" **批准"** 或 **"** 拒绝"按钮的审批卡片：向作为审批者列表的一部分的用户和自适应卡片 JSON 的 属性中的列表 `userIds` `refresh` 显示。

**发送资产审批请求**

1. Alex 在资产审批对话中Teams资产审批请求，并将其分配给 Megan 和 Nestor。
2. 机器人在对话中发送审批基本卡。
3. 对话中的所有其他用户将看到机器人发送的卡片。 为 Megan 和 Nestor 触发自动刷新，这些用户现在看到用户特定卡片包含"批准"或"拒绝"按钮，因为用户 MRIs 将添加到自适应卡片的 属性 `userIds` `refresh` 中的列表中。

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="用户特定视图":::

4. Nestor **选择使用** 进行电源的"批准"按钮 `Action.Execute` 。 机器人获取一 `adaptiveCard/action` 个调用请求，它可以返回自适应卡片作为响应。
5. 机器人使用更新的卡片触发邮件编辑，其中显示 Nestor 已批准请求，而 Megan 的审批挂起。
6. 自动程序消息编辑会触发 Megan 的自动刷新，她看到更新的用户特定卡片，其中显示 Nestor 已批准了请求，但还看到"批准"**或"** 拒绝"按钮。 Nestor 的用户 MRI 从步骤 4 和 5 中此自适应 `userIds` 卡片 JSON 的 属性中删除 `refresh` 。 现在，仅针对 Megan 触发自动刷新。

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-2.png" alt-text="最新用户特定视图":::

7. 现在，Megan 选择" **批准** "按钮，该按钮由 支持 `Action.Execute` 。 机器人获取一 `adaptiveCard/action` 个调用请求，它可以返回自适应卡片作为响应。
8. 机器人使用更新的卡片触发邮件编辑，其中显示 Nestor 和 Megan 已批准了请求。
9. 自动程序消息编辑不会触发任何自动刷新。 还将从步骤 7 和 8 中此自适应卡片 JSON 的 属性中的列表中删除 Megan `userIds` 的用户 MRI。 `refresh`

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-3.png" alt-text="最新视图":::

## <a name="adaptive-card-sent-as-response-of-adaptivecardaction-and-message-edit"></a>作为 响应和 发送的自适应 `adaptiveCard/action` 卡片 `message edit`

以下代码提供了作为响应和步骤 4 和 5 发送的自适应卡片 `adaptiveCard/action` `message edit` 的示例：

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

以下代码提供了通过步骤 6 的自动刷新作为调用响应发送的自适应 `adaptiveCard/action` 卡片示例：

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

以下代码提供了作为 响应和步骤 7 和 8 发送的自适应卡片 `adaptiveCard/action` `message edit` 示例：

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

## <a name="see-also"></a>另请参阅

* [使用自适应卡的通用操作](Work-with-universal-actions-for-adaptive-cards.md)
* [用户特定视图](User-Specific-Views.md)
