---
title: 用户特定视图
description: 了解将通用操作与代码示例结合使用的用户特定视图
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: b2e5b8d6dd00104fab819ba7d05d5913bb891d83
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073678"
---
# <a name="user-specific-views"></a>用户特定视图

如果在Teams对话中发送自适应卡片，则所有用户都会看到完全相同的卡片内容。 随着通用操作模型和 `refresh` 自适应卡片的引入，机器人开发人员现在可以向用户提供自适应卡片的用户特定视图。 同一自适应卡片现在可以刷新到用户特定的自适应卡片。 最多 60 个不同的用户可以查看其他信息或操作的不同版本的卡片。 自适应卡片提供强大的方案，如审批、投票创建者控制、票证、事件管理和项目管理卡。

> [!NOTE]
> 机器人发送的自适应卡支持用户特定视图，并且依赖于通用操作。

例如，Contoso 的安全检查员 Megan 想要创建事件并将其分配给 Alex。 梅根还希望团队中的每个人都能知道这一事件。 Megan 使用由自适应卡的通用操作支持的 Contoso 事件报告消息扩展。

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="移动用户特定视图" lightbox="../../../assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg":::

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="用户特定视图" lightbox="../../../assets/images/adaptive-cards/universal-bots-incident-management.png":::

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

若要发送自适应卡片，请刷新用户特定视图，并向机器人调用请求：

1. 当 Megan 创建新事件时，机器人会发送自适应卡片或常见卡片，其中包含Teams对话中的事件详细信息。
2. 现在，此卡会自动刷新到 Megan 和 Alex 的用户特定视图。 Alex 和 Megan 的用户 MRI 添加到自适应卡片 JSON 的`refresh`属性属性中`userIds`。 对于对话中的其他用户，卡片保持不变。
3. 对于 Megan，自动刷新会触发 `adaptiveCard/action` 对机器人的调用请求。 机器人可以返回事件创建者卡片， `Edit` 其中包含按钮作为对此调用请求的响应。
4. 同样，对于 Alex，自动刷新会触发对机器人的另一 `adaptiveCard/action` 个调用请求。 机器人可以返回事件所有者卡 `Resolve` 按钮作为对此调用请求的响应。

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>调用从Teams客户端发送到机器人的请求

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

## <a name="adaptivecardaction-invoke-response-card"></a>adaptiveCard/action invoke 响应卡

以下代码提供了 Megan 的 adaptiveCard/action 调用响应卡的示例：

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

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a>AdaptiveCard/action invoke response card for Alex

以下代码提供了 Alex 的 adaptiveCard/action 调用响应卡的示例：

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

### <a name="c"></a>[C#](#tab/C)

```csharp
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.adaptive.card",
    value = card
 });
```

### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
var card = "<adaptive card json>";
 
const cardRes = {
        statusCode: 200,
        type: 'application/vnd.microsoft.card.adaptive',
        value: card
    };
    const res = {
        status: 200,
        body: cardRes
    };
    return res;

```

***

在设计用户特定视图时要记住的卡片设计准则：

* 通过在部分中指定`userIds``refresh`特定卡片，最多可以创建 **60 个用户特定视图**。
* **基卡：** 机器人开发人员发送到聊天的卡的基本版本。 基本版本是本部分中 `userIds` 未指定的所有用户的自适应卡片版本。
* 消息更新可用于更新基卡并同时刷新用户特定卡。 打开聊天或频道也会刷新启用刷新功能的用户的卡片。
* 对于用户切换到操作视图（需要响应者动态更新）的较大组的方案，可以继续将最多 60 个用户添加到 `userIds` 列表中。 当第 61 个用户响应时，可以从列表中删除第一个响应者。 对于从列表中删除的 `userIds` 用户，可以提供手动刷新按钮或使用消息选项菜单中的刷新按钮来获取最新结果。
* 提示用户获取用户特定视图，在该视图中，用户只看到卡片的特定视图或某些操作。

## <a name="code-sample"></a>代码示例

|示例名称 | Description | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| 顺序工作流自适应卡片 | 演示如何在机器人中实现顺序工作流、用户特定视图和最新自适应卡片。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>另请参阅

* [使用自适应卡的通用操作](Work-with-universal-actions-for-adaptive-cards.md)
* [最新视图](Up-To-Date-Views.md)
* [表单完成反馈](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
