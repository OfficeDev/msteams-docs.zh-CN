---
title: 用户特定视图
description: 了解使用通用操作和代码示例的用户特定视图
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: e6dc1cc87f5a9896933566475d69ce9ad311fbfb
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889200"
---
# <a name="user-specific-views"></a>用户特定视图

之前，如果自适应卡片是在Teams对话中发送的，则所有用户都可以看到完全相同的卡片内容。 随着通用操作模型和自适应卡片的引入，机器人开发人员现在可以为用户提供自适应卡片的用户 `refresh` 特定视图。 现在，相同的自适应卡片可以刷新到用户特定自适应卡片。 最多 60 个不同的用户可以看到不同版本的卡，并包含其他信息或操作。 自适应卡片提供功能强大的方案，如审批、投票创建者控件、票证、事件管理和项目管理卡。

例如，Contoso 的安全检查员 Megan 想要创建事件并将其分配给 Alex。 Megan 还希望团队中的每个人都了解事件。 Megan 使用 Contoso 事件报告邮件扩展，该扩展由自适应卡片的通用操作支持。

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="移动用户特定视图":::

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="用户特定视图":::

* * *

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
      }
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

1. 当 Megan 创建新事件时，自动程序在用户对话中发送包含事件详细信息的自适应卡片Teams卡片。
2. 现在，此卡片将自动刷新到 Megan 和 Alex 的用户特定视图。 Alex 和 Megan 的用户 MRIs 添加到自适应卡片 JSON 的 `userIds` `refresh` 属性中。 对于对话中的其他用户，该卡片保持不变。
3. 对于 Megan，自动刷新会触发 `adaptiveCard/action` 对机器人的调用请求。 机器人可以返回事件创建者卡片，并添加 `Edit` 按钮作为对此调用请求的响应。
4. 同样，对于 Alex，自动刷新将触发 `adaptiveCard/action` 对自动程序的另一个调用请求。 机器人可以返回事件所有者卡片 `Resolve` 按钮作为对此调用请求的响应。

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>调用从 Teams 客户端发送到自动程序的请求

以下代码提供了从 Alex 和 Megan 的 Teams 客户端发送到机器人的调用请求的示例：

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
    type = "application/vnd.microsoft.adaptive.card",
    value = card
 });
```

设计用户特定视图时请记住的卡片设计指南：

* 您可以通过在 部分中指定特定卡片，为发送到聊天或频道的特定卡片创建最多 **60** `userIds` 个用户特定 `refresh` 视图。
* **基本卡片：** 机器人开发人员发送到聊天的卡的基本版本。 基本版本是部分中未指定的所有用户的自适应卡片 `userIds` 版本。
* 邮件更新可用于更新基本卡并同时刷新用户特定卡片。 打开聊天或频道还会刷新已启用刷新功能的用户的卡片。
* 对于用户切换到操作视图的较大组（需要响应者的动态更新）的方案，你可以不断向列表中添加多达 60 `userIds` 个用户。 当第 61 个用户做出响应时，可以从列表中删除第一个响应器。 对于从列表中删除的用户，可以提供手动刷新按钮或使用消息选项菜单中的刷新按钮 `userIds` 获取最新结果。
* 提示用户获取用户特定视图，其中他们只能看到卡片的特定视图或一些操作。

## <a name="code-sample"></a>代码示例

|示例名称 | 描述 | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| 顺序工作流自适应卡片 | 演示如何在机器人中实现顺序工作流、用户特定视图和最新的自适应卡片。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>另请参阅

* [使用自适应卡的通用操作](Work-with-universal-actions-for-adaptive-cards.md)
* [最新视图](Up-To-Date-Views.md)
