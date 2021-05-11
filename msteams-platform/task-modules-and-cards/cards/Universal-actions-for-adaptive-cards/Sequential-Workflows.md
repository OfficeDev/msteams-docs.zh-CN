---
title: 顺序工作流
description: 使用通用操作的顺序工作流的示例
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 4b37e8603d34c070bdef3003c2f8ccb0bb41550b
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088822"
---
# <a name="sequential-workflows"></a><span data-ttu-id="5266c-103">顺序工作流</span><span class="sxs-lookup"><span data-stu-id="5266c-103">Sequential Workflows</span></span>

<span data-ttu-id="5266c-104">自适应卡片现在支持顺序工作流，在用户操作上更新自适应卡片时，用户可以在一系列需要用户输入的卡片中前进。</span><span class="sxs-lookup"><span data-stu-id="5266c-104">Adaptive Cards now support Sequential Workflows that is when Adaptive Cards are updated on user action and user can progress through a series of cards that require user input.</span></span> <span data-ttu-id="5266c-105">这通过 支持 `Action.Execute` ，这允许机器人开发人员返回自适应卡片以响应用户操作。</span><span class="sxs-lookup"><span data-stu-id="5266c-105">This is supported through `Action.Execute`, which allows bot developers to return Adaptive Cards in response to a user action.</span></span>

<span data-ttu-id="5266c-106">例如，假设自助餐厅想要为团队或频道下订单。</span><span class="sxs-lookup"><span data-stu-id="5266c-106">For example, take a scenario where the cafeteria wants to take an order for a team or channel.</span></span> <span data-ttu-id="5266c-107">通过用户对各种商品（如食物、食物等）的选择，可以 `Action.Execute` 按顺序进行记录。</span><span class="sxs-lookup"><span data-stu-id="5266c-107">With `Action.Execute` the user's choice for various items, such as food, drinks, and so on can be recorded sequentially.</span></span> <span data-ttu-id="5266c-108">用户还可以根据自动程序开发人员定义的逻辑来回浏览卡片。</span><span class="sxs-lookup"><span data-stu-id="5266c-108">User can also go back and forth through the cards as per the logic defined by the bot developer.</span></span> <br/>

<span data-ttu-id="5266c-109">下图显示了顺序工作流：</span><span class="sxs-lookup"><span data-stu-id="5266c-109">The following image shows the Sequential Workflow:</span></span>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

<span data-ttu-id="5266c-110">用户可以在工作流中推进，而无需修改其他用户的卡片。</span><span class="sxs-lookup"><span data-stu-id="5266c-110">A user can progress through their workflow without modifying the card for other users.</span></span> <span data-ttu-id="5266c-111">这还可用于使用顺序自适应卡片进行测验。</span><span class="sxs-lookup"><span data-stu-id="5266c-111">This is also useful for conducting quizzes using sequential Adaptive Cards.</span></span> <span data-ttu-id="5266c-112">如下图所示，不同用户可以处于工作流的不同阶段，并且可以看到卡片的不同状态：</span><span class="sxs-lookup"><span data-stu-id="5266c-112">As shown in the following image, different users can be at different stages of the workflow and they see different states of the card:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="适应机器人状态":::

> [!NOTE]
> <span data-ttu-id="5266c-114">若要跨设备同步用户的进度，请使用自适应卡片 `refresh` JSON 中的 属性。</span><span class="sxs-lookup"><span data-stu-id="5266c-114">In order to sync the user's progress across devices, use the `refresh` property in Adaptive Card JSON.</span></span>

## <a name="sequential-workflow-for-adaptive-cards"></a><span data-ttu-id="5266c-115">自适应卡片的顺序工作流</span><span class="sxs-lookup"><span data-stu-id="5266c-115">Sequential Workflow for Adaptive Cards</span></span>

<span data-ttu-id="5266c-116">以下代码提供了自适应卡片的示例：</span><span class="sxs-lookup"><span data-stu-id="5266c-116">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="5266c-117">`Action.Execute`调用机器人可以返回自适应卡片作为响应，这将替换现有Teams。</span><span class="sxs-lookup"><span data-stu-id="5266c-117">`Action.Execute` invoking the bot can return Adaptive Cards as a response, which replaces the existing card in Teams.</span></span>
<span data-ttu-id="5266c-118">以下示例提供了机器人在确认食物或食物选择或订单时返回内容：</span><span class="sxs-lookup"><span data-stu-id="5266c-118">The following example provides what the bot returns on food or drink selection or order confirmation:</span></span>

* <span data-ttu-id="5266c-119">在从卡片 1 选择食物时，机器人可以返回一张卡片，用于选择卡片 2。</span><span class="sxs-lookup"><span data-stu-id="5266c-119">On food selection from Card 1, bot can return a card for selection of drinks that is Card 2.</span></span>
* <span data-ttu-id="5266c-120">在从卡片 2 选择时，自动程序可以返回一个订单确认卡，即卡片 3。</span><span class="sxs-lookup"><span data-stu-id="5266c-120">On drink selection from Card 2, bot can return an order confirmation card that is Card 3.</span></span>
* <span data-ttu-id="5266c-121">在从卡片 3 确认订单后，自动程序可以返回已确认订单的卡片，即卡片 4。</span><span class="sxs-lookup"><span data-stu-id="5266c-121">On order confirmation from Card 3, bot can return an order confirmed card that is Card 4.</span></span>

## <a name="invoke-request-received-on-bot-side"></a><span data-ttu-id="5266c-122">调用在自动程序端收到的请求</span><span class="sxs-lookup"><span data-stu-id="5266c-122">Invoke request received on bot side</span></span>

<span data-ttu-id="5266c-123">以下代码提供了在自动程序端收到的调用请求的示例：</span><span class="sxs-lookup"><span data-stu-id="5266c-123">The following code provides an example of an invoke request received on bot side:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="5266c-124">调用响应以返回自适应卡片</span><span class="sxs-lookup"><span data-stu-id="5266c-124">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="5266c-125">以下代码提供了用于返回自适应卡片的调用响应示例：</span><span class="sxs-lookup"><span data-stu-id="5266c-125">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="5266c-126">另请参阅</span><span class="sxs-lookup"><span data-stu-id="5266c-126">See also</span></span>

* [<span data-ttu-id="5266c-127">用户中的自适应卡片Teams</span><span class="sxs-lookup"><span data-stu-id="5266c-127">Adaptive Card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [<span data-ttu-id="5266c-128">机器人的工作方式</span><span class="sxs-lookup"><span data-stu-id="5266c-128">How bots work</span></span>](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [<span data-ttu-id="5266c-129">使用自适应卡的通用操作</span><span class="sxs-lookup"><span data-stu-id="5266c-129">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
