---
title: 顺序工作流
description: 使用通用操作的顺序工作流的示例
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 7f285bf76aac4f0ca276321aee2ce4b4e5c3e7e4
ms.sourcegitcommit: 9ef3b415cbba484c2201abe9c6927e08d974388e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52555400"
---
# <a name="sequential-workflows"></a>顺序工作流

自适应卡片现在支持顺序工作流，在用户操作上更新自适应卡片时，用户可以在一系列需要用户输入的卡片中前进。 这通过 支持 `Action.Execute` ，这允许机器人开发人员返回自适应卡片以响应用户操作。

例如，假设自助餐厅想要为团队或频道下订单。 通过用户对各种商品（如食物、食物等）的选择，可以 `Action.Execute` 按顺序进行记录。 用户还可以根据自动程序开发人员定义的逻辑来回浏览卡片。 <br/>

下图显示了顺序工作流：

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

用户可以在工作流中推进，而无需修改其他用户的卡片。 这还可用于使用顺序自适应卡片进行测验。 如下图所示，不同用户可以处于工作流的不同阶段，并且可以看到卡片的不同状态：

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="适应机器人状态":::

> [!NOTE]
> 若要跨设备同步用户的进度，请使用自适应卡片 `refresh` JSON 中的 属性。

## <a name="sequential-workflow-for-adaptive-cards"></a>自适应卡片的顺序工作流

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

`Action.Execute`调用机器人可以返回自适应卡片作为响应，这将替换现有Teams。
以下示例提供了机器人在确认食物或食物选择或订单时返回内容：

* 在从卡片 1 选择食物时，机器人可以返回一张卡片，用于选择卡片 2。
* 在从卡片 2 选择时，自动程序可以返回一个订单确认卡，即卡片 3。
* 在从卡片 3 确认订单后，自动程序可以返回已确认订单的卡片，即卡片 4。

## <a name="invoke-request-received-on-bot-side"></a>调用在自动程序端收到的请求

以下代码提供了在自动程序端收到的调用请求的示例：

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

## <a name="see-also"></a>另请参阅

* [用户中的自适应卡片Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [机器人的工作方式](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [使用自适应卡的通用操作](Work-with-universal-actions-for-adaptive-cards.md)
