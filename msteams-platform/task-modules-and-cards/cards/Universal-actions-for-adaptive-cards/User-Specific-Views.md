---
title: 用户特定视图
description: 使用通用操作的用户特定视图示例
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: cadf66082582cfd9009a0497b3eb5e58f0a2ef02
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649622"
---
# <a name="user-specific-views"></a><span data-ttu-id="12201-103">用户特定视图</span><span class="sxs-lookup"><span data-stu-id="12201-103">User Specific Views</span></span>

<span data-ttu-id="12201-104">之前，如果自适应卡片是在Teams对话中发送的，则所有用户都可以看到完全相同的卡片内容。</span><span class="sxs-lookup"><span data-stu-id="12201-104">Earlier if Adaptive Cards was sent in a Teams conversation, all users see the exact same card content.</span></span> <span data-ttu-id="12201-105">随着通用操作模型和自适应卡片的引入，机器人开发人员现在可以为用户提供自适应卡片的用户 `refresh` 特定视图。</span><span class="sxs-lookup"><span data-stu-id="12201-105">With the introduction of the Universal Actions model and `refresh` for Adaptive Cards, bot developers can now provide User Specific Views of Adaptive Cards to users.</span></span> <span data-ttu-id="12201-106">现在，相同的自适应卡片可以刷新到用户特定自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="12201-106">The same Adaptive Card can now refresh to a User Specific Adaptive Card.</span></span>

<span data-ttu-id="12201-107">例如，Contoso 的安全检查员 Megan 想要创建事件并将其分配给 Alex。</span><span class="sxs-lookup"><span data-stu-id="12201-107">For example, Megan, a safety inspector at Contoso, wants to create an incident and assign it to Alex.</span></span> <span data-ttu-id="12201-108">她还希望团队中的每个人都了解事件。</span><span class="sxs-lookup"><span data-stu-id="12201-108">She also wants everyone in the team to be aware about the incident.</span></span> <span data-ttu-id="12201-109">Megan 使用 Contoso 事件报告邮件扩展，该扩展由自适应卡片的通用操作支持。</span><span class="sxs-lookup"><span data-stu-id="12201-109">Megan uses Contoso incident reporting message extension powered by Universal Actions for Adaptive Cards.</span></span>

# <a name="mobile"></a>[<span data-ttu-id="12201-110">移动</span><span class="sxs-lookup"><span data-stu-id="12201-110">Mobile</span></span>](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="移动用户特定视图":::

# <a name="desktop"></a>[<span data-ttu-id="12201-112">桌面</span><span class="sxs-lookup"><span data-stu-id="12201-112">Desktop</span></span>](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="用户特定视图":::

* * *

## <a name="user-specific-views-for-adaptive-cards"></a><span data-ttu-id="12201-114">自适应卡片的用户特定视图</span><span class="sxs-lookup"><span data-stu-id="12201-114">User Specific Views for Adaptive Cards</span></span>

<span data-ttu-id="12201-115">以下代码提供了自适应卡片的示例：</span><span class="sxs-lookup"><span data-stu-id="12201-115">The following code provides an example of Adaptive Cards:</span></span>

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

<span data-ttu-id="12201-116">**若要发送自适应卡片，请刷新用户特定视图，并调用对自动程序的请求**</span><span class="sxs-lookup"><span data-stu-id="12201-116">**To send Adaptive Cards, refresh User Specific Views, and invoke requests to the bot**</span></span>

1. <span data-ttu-id="12201-117">当 Megan 创建新事件时，机器人会发送自适应卡片或公用卡片（包含事件详细信息）Teams对话。</span><span class="sxs-lookup"><span data-stu-id="12201-117">When Megan creates a new incident, the bot sends the Adaptive Card or common card with incident details in the Teams conversation.</span></span>
2. <span data-ttu-id="12201-118">现在，此卡片将自动刷新到 Megan 和 Alex 的用户特定视图。</span><span class="sxs-lookup"><span data-stu-id="12201-118">Now this card automatically refreshes to User Specific View for Megan and Alex.</span></span> <span data-ttu-id="12201-119">Alex 和 Megan 的用户 MRIs 添加到自适应卡片 JSON 的 `userIds` `refresh` 属性中。</span><span class="sxs-lookup"><span data-stu-id="12201-119">Alex's and Megan's user MRIs are added in `userIds` property of `refresh` property of the Adaptive Card JSON.</span></span> <span data-ttu-id="12201-120">对于对话中的其他用户，该卡片保持不变。</span><span class="sxs-lookup"><span data-stu-id="12201-120">The card remains the same for other users in the conversation.</span></span>
3. <span data-ttu-id="12201-121">对于 Megan，自动刷新会触发 `adaptiveCard/action` 对机器人的调用请求。</span><span class="sxs-lookup"><span data-stu-id="12201-121">For Megan, automatic refresh triggers an `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="12201-122">机器人可以返回事件创建者卡片，并添加 `Edit` 按钮作为对此调用请求的响应。</span><span class="sxs-lookup"><span data-stu-id="12201-122">The bot can return an incident creator card with `Edit` button as a response to this invoke request.</span></span>
4. <span data-ttu-id="12201-123">同样，对于 Alex，自动刷新将触发 `adaptiveCard/action` 对自动程序的另一个调用请求。</span><span class="sxs-lookup"><span data-stu-id="12201-123">Similarly for Alex, automatic refresh triggers another `adaptiveCard/action` invoke request to the bot.</span></span> <span data-ttu-id="12201-124">机器人可以返回事件所有者卡片 `Resolve` 按钮作为对此调用请求的响应。</span><span class="sxs-lookup"><span data-stu-id="12201-124">The bot can return an incident owner card `Resolve` button as a response to this invoke request.</span></span>

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a><span data-ttu-id="12201-125">调用从 Teams 客户端发送到自动程序的请求</span><span class="sxs-lookup"><span data-stu-id="12201-125">Invoke request sent from Teams client to the bot</span></span>

<span data-ttu-id="12201-126">以下代码提供了从 Alex 和 Megan 的 Teams 客户端发送到机器人的调用请求示例：</span><span class="sxs-lookup"><span data-stu-id="12201-126">The following code provides an example of an invoke request sent from Alex's and Megan's Teams client to the bot:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card"></a><span data-ttu-id="12201-127">adaptiveCard/action 调用响应卡</span><span class="sxs-lookup"><span data-stu-id="12201-127">adaptiveCard/action invoke response card</span></span>

<span data-ttu-id="12201-128">以下代码为 Megan 提供了自适应卡片/操作调用响应卡的示例：</span><span class="sxs-lookup"><span data-stu-id="12201-128">The following code provides an example of an adaptiveCard/action invoke response card for Megan:</span></span>

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

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a><span data-ttu-id="12201-129">adaptiveCard/action 调用 Alex 的响应卡片</span><span class="sxs-lookup"><span data-stu-id="12201-129">adaptiveCard/action invoke response card for Alex</span></span>

<span data-ttu-id="12201-130">以下代码为 Alex 提供了自适应卡片/操作调用响应卡的示例：</span><span class="sxs-lookup"><span data-stu-id="12201-130">The following code provides an example of an adaptiveCard/action invoke response card for Alex:</span></span>

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

## <a name="invoke-response-to-return-adaptive-cards"></a><span data-ttu-id="12201-131">调用响应以返回自适应卡片</span><span class="sxs-lookup"><span data-stu-id="12201-131">Invoke response to return Adaptive Cards</span></span>

<span data-ttu-id="12201-132">以下代码提供了用于返回自适应卡片的调用响应示例：</span><span class="sxs-lookup"><span data-stu-id="12201-132">The following code provides an example of an invoke response to return Adaptive Cards:</span></span>

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

<span data-ttu-id="12201-133">设计用户特定视图时请记住的卡片设计指南：</span><span class="sxs-lookup"><span data-stu-id="12201-133">Card design guidelines to keep in mind while designing User Specific Views:</span></span>

* <span data-ttu-id="12201-134">您可以通过在 部分中指定特定卡片，为发送到聊天或频道的特定卡片创建最多 **60** `userIds` 个用户特定 `refresh` 视图。</span><span class="sxs-lookup"><span data-stu-id="12201-134">You can create a maximum of **60 User Specific Views** for a particular card being sent to a chat or channel by specifying their `userIds` in the `refresh` section.</span></span>
* <span data-ttu-id="12201-135">**基本卡片：** 机器人开发人员发送到聊天的卡的基本版本。</span><span class="sxs-lookup"><span data-stu-id="12201-135">**Base Card:** The base version of the card that the bot developer sends to the chat.</span></span> <span data-ttu-id="12201-136">这是部分中未指定的所有用户的自适应卡片 `userIds` 版本。</span><span class="sxs-lookup"><span data-stu-id="12201-136">This is the version of the Adaptive Card for all users who are not specified in the `userIds` section.</span></span>
* <span data-ttu-id="12201-137">邮件更新或编辑可用于更新基本卡并同时刷新用户特定卡片。</span><span class="sxs-lookup"><span data-stu-id="12201-137">A message update or edit can be used to update the base card and simultaneously refresh the User Specific Card.</span></span>

## <a name="see-also"></a><span data-ttu-id="12201-138">另请参阅</span><span class="sxs-lookup"><span data-stu-id="12201-138">See also</span></span>

* [<span data-ttu-id="12201-139">使用自适应卡的通用操作</span><span class="sxs-lookup"><span data-stu-id="12201-139">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
* [<span data-ttu-id="12201-140">最新视图</span><span class="sxs-lookup"><span data-stu-id="12201-140">Up to date views</span></span>](Up-To-Date-Views.md)
