---
title: 特定于用户的视图
description: 使用通用操作的用户特定视图示例
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 984b32511dda544942df11f7c5d8a25cca8e9a8a
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088820"
---
# <a name="user-specific-views"></a>特定于用户的视图

之前，如果自适应卡片是在Teams对话中发送的，则所有用户都可以看到完全相同的卡片内容。 随着通用操作模型和自适应卡片的引入，机器人开发人员现在可以为用户提供自适应卡片的用户 `refresh` 特定视图。 现在，相同的自适应卡片可以刷新到用户特定自适应卡片。

例如，Contoso 的安全检查员 Megan 想要创建事件并将其分配给 Alex。 她还希望团队中的每个人都了解事件。 Megan 使用 Contoso 事件报告邮件扩展，该扩展由自适应卡片的通用操作支持。

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="特定于用户的视图":::

## <a name="user-specific-views-for-adaptive-cards"></a>自适应卡片的用户特定视图

以下代码提供了自适应卡片的示例：

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView",
      "data": {
              "refresh info": "<refresh info>"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ]
}
```

**若要发送自适应卡片，请刷新用户特定视图，并调用对自动程序的请求**

1. 当 Megan 创建新事件时，机器人会发送自适应卡片或公用卡片（包含事件详细信息）Teams对话。
2. 现在，此卡片将自动刷新到 Megan 和 Alex 的用户特定视图。 Alex 和 Megan 的用户 MRIs 添加到自适应卡片 JSON 的 `userIds` `refresh` 属性中。 对于对话中的其他用户，该卡片保持不变。
3. 对于 Megan，自动刷新会触发 `adaptiveCard/action` 对机器人的调用请求。 机器人可以返回事件创建者卡片，并添加 `Edit` 按钮作为对此调用请求的响应。
4. 同样，对于 Alex，自动刷新将触发 `adaptiveCard/action` 对自动程序的另一个调用请求。 机器人可以返回事件所有者卡片 `Resolve` 按钮作为对此调用请求的响应。

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>调用从 Teams 客户端发送到自动程序的请求

以下代码提供了从 Alex 和 Megan 的 Teams 客户端发送到机器人的调用请求示例：

```JSON
{ 
  "type": "invoke",
  "name": "adaptiveCard/action",

  // ... other properties omitted for brevity

  "value": { 
    "action": { 
      "type": "Action.Execute", 
      "id": "", 
      "verb": "editOrResolveView",
      "data": { 
            "refresh info": "<refresh info>"
      } 
    },
    "trigger": "automatic" 
  }
}
```

## <a name="adaptivecardaction-invoke-response-card"></a>adaptiveCard/action 调用响应卡

以下代码为 Megan 提供了自适应卡片/操作调用响应卡的示例：

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Edit",
      "verb": "edit",
      "data": {
            "additional info": "<additional info>",
            ...
      }
    }
  ]
}
```

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a>adaptiveCard/action 调用 Alex 的响应卡片

以下代码为 Alex 提供了自适应卡片/操作调用响应卡的示例：

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Resolve",
      "verb": "resolve",
      "data": {
            "additional info": "<additional info>",
            ...
      }
    }
  ]
}
```

## <a name="invoke-response-to-return-adaptive-cards"></a>调用响应以返回自适应卡片

以下代码提供了用于返回自适应卡片的调用响应示例：

```C#
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.card.adaptive",
    value = card
 });
```

设计用户特定视图时请记住的卡片设计指南：

* 您可以通过在 部分中指定特定卡片，为发送到聊天或频道的特定卡片创建最多 **60** `userIds` 个用户特定 `refresh` 视图。
* **基本卡片：** 机器人开发人员发送到聊天的卡的基本版本。 这是部分中未指定的所有用户的自适应卡片 `userIds` 版本。
* 邮件更新或编辑可用于更新基本卡并同时刷新用户特定卡片。

## <a name="see-also"></a>另请参阅

* [使用自适应卡片的通用操作](Work-with-universal-actions-for-adaptive-cards.md)
* [最新视图](Up-To-Date-Views.md)
