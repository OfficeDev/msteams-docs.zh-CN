---
title: 顺序工作流
description: 了解使用通用操作和代码示例的自适应卡的顺序工作流
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 32200fc7a4df12567ba4000aad34e5a229dbc466
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073779"
---
# <a name="sequential-workflows"></a>顺序工作流

自适应卡片现在支持按用户操作更新的顺序工作流。 使用顺序工作流，自适应卡在用户操作上更新，用户可以通过一系列需要用户输入的卡进行进度。 `Action.Execute` 支持顺序工作流，这允许机器人开发人员返回自适应卡片以响应用户操作。

例如，采用自助餐厅想要为团队或频道订购的方案。 根据 `Action.Execute` 用户对各种项目（如食品和饮料）的选择，可以按顺序记录。 用户还可以根据机器人开发人员定义的逻辑来回浏览卡片。 <br/>

下图显示了顺序工作流：

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

用户无需修改其他用户的卡片即可完成其工作流。 工作流还可用于使用顺序自适应卡片进行测验。 下图显示了不同的用户可能处于工作流的不同阶段和卡片的状态：

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="餐饮机器人状态" lightbox="../../../assets/images/adaptive-cards/universal-bots-catering-bot.png":::

> [!NOTE]
> 若要跨设备同步用户的进度，请在自适应卡片 JSON 中使用该 `refresh` 属性。

## <a name="sequential-workflow-for-adaptive-cards"></a>自适应卡的顺序工作流

以下代码提供了自适应卡片的示例：

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "body": [
    {
      "type": "TextBlock",
      "text": "Select from food options"
    },
    { 
      "type": "ActionSet",
      "actions": [
        {
          "type": "Action.Execute",
          "title": "Chicken",
          "verb": "food",
          "data": {
              "item": "chicken"
          }
        },
        {
          "type": "Action.Execute",
          "title": "Beef",
          "verb": "food",
          "data": {
              "item": "beef"
          }
        },
        {
          "type": "Action.Execute",
          "title": "Vegan",
          "verb": "food",
          "data": {
              "item": "vegan"
          }
        }
      ]
    }
  ]
}
```

`Action.Execute`调用机器人可以返回自适应卡作为响应，从而替换Teams中的现有卡片。
以下示例提供机器人在食品或饮料选择或订单确认时返回的内容：

* 从卡 1 选择食物时，机器人可以返回一张卡片，用于选择卡 2 的饮料。
* 从卡 2 中选择饮料时，机器人可以返回一张订单确认卡，即卡 3。
* 根据卡 3 的订单确认，机器人可以返回订单确认卡 4。

## <a name="invoke-request-received-on-bot-side"></a>调用在机器人端收到的请求

以下代码提供了在机器人端收到的调用请求的示例：

```JSON
{ 
  "type": "invoke",
  "name": "adaptiveCard/action",

  // ... other properties omitted for brevity

  "value": { 
    "action": { 
      "type": "Action.Execute", 
      "id": "", 
      "verb": "food",
      "data": { 
            "item": "vegan"
      } 
    },
    "trigger": "manual" 
  }
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

## <a name="code-samples"></a>代码示例

|示例名称 | Description | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Teams餐饮机器人 | 使用自适应卡片创建接受食品订单的机器人。 |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| 尚不可用 |
| 顺序工作流自适应卡片 | 演示如何在机器人中实现顺序工作流、用户特定视图和最新自适应卡片。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>另请参阅

* [Teams中的自适应卡片操作](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [机器人的工作方式](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [使用自适应卡的通用操作](Work-with-universal-actions-for-adaptive-cards.md)
* [表单完成反馈](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
