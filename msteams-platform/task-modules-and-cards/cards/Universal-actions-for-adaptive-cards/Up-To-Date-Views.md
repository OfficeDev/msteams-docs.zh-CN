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
# <a name="up-to-date-cards"></a><span data-ttu-id="53f3b-103">最新卡片</span><span class="sxs-lookup"><span data-stu-id="53f3b-103">Up to date cards</span></span>

<span data-ttu-id="53f3b-104">现在可以在自适应卡片上将刷新和邮件编辑组合在一起，为用户提供最新Teams。</span><span class="sxs-lookup"><span data-stu-id="53f3b-104">You can now provide latest information to your users on Adaptive Cards with a combination of refresh and message edits in Teams.</span></span> <span data-ttu-id="53f3b-105">这样，当服务发生变化时，你可以动态地将用户特定视图更新到其最新状态。</span><span class="sxs-lookup"><span data-stu-id="53f3b-105">With this you are able to update the User Specific Views dynamically to its latest state as and when there is a change on your service.</span></span> <span data-ttu-id="53f3b-106">例如，对于项目管理或票证卡，可以更新注释和任务的状态。</span><span class="sxs-lookup"><span data-stu-id="53f3b-106">For example, in the case of project management or ticketing cards, you can update comments and the status of the task.</span></span> <span data-ttu-id="53f3b-107">在批准的情况下，最新状态会反映出来，同时还提供不同的信息和操作。</span><span class="sxs-lookup"><span data-stu-id="53f3b-107">In case of approvals the latest state is reflected while also providing differentiated information and actions.</span></span>

<span data-ttu-id="53f3b-108">例如，用户可以在资源审批对话中Teams请求。</span><span class="sxs-lookup"><span data-stu-id="53f3b-108">For example, a user can create an asset approval request in a Teams conversation.</span></span> <span data-ttu-id="53f3b-109">Alex 创建审批请求并将其分配给 Megan 和 Nestor。</span><span class="sxs-lookup"><span data-stu-id="53f3b-109">Alex creates an approval request and assigns it to Megan and Nestor.</span></span> <span data-ttu-id="53f3b-110">以下是创建审批请求的两个部分：</span><span class="sxs-lookup"><span data-stu-id="53f3b-110">The following are the two parts to create the approval request:</span></span>

* <span data-ttu-id="53f3b-111">可以使用自适应卡片的 属性利用用户 `refresh` 特定视图。</span><span class="sxs-lookup"><span data-stu-id="53f3b-111">User Specific Views can be leveraged using the `refresh` property of the Adaptive Cards.</span></span>
<span data-ttu-id="53f3b-112">使用用户特定视图一个可以向一组用户显示具有"批准"或"拒绝"按钮的卡片，并且向其他用户显示没有这些按钮的卡片。</span><span class="sxs-lookup"><span data-stu-id="53f3b-112">Using User Specific Views one can show a card with **Approve** or **Reject** buttons to a set of users, and show a card without these buttons to other users.</span></span>

* <span data-ttu-id="53f3b-113">若要始终更新卡片状态，Teams邮件编辑机制。</span><span class="sxs-lookup"><span data-stu-id="53f3b-113">To keep the card state updated at all times, Teams message edit mechanism can be leveraged.</span></span> <span data-ttu-id="53f3b-114">例如，每次审批时，自动程序都可以触发对所有用户的邮件编辑。</span><span class="sxs-lookup"><span data-stu-id="53f3b-114">For example, each time there is an approval, bot can trigger a message edit to all users.</span></span> <span data-ttu-id="53f3b-115">此自动程序消息编辑会触发所有自动刷新用户的调用请求，自动程序可以使用更新的用户特定 `adaptiveCard/action` 卡片对此进行响应。</span><span class="sxs-lookup"><span data-stu-id="53f3b-115">This bot message edit triggers an `adaptiveCard/action` invoke request for all automatic refresh users, to which the bot can respond with the updated user specific card.</span></span>

<span data-ttu-id="53f3b-116">有关详细信息，请参阅 [如何执行自动程序消息编辑](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards)。</span><span class="sxs-lookup"><span data-stu-id="53f3b-116">For more information, see [how to do a bot message edit](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/update-and-delete-bot-messages?tabs=dotnet#update-cards).</span></span>

## <a name="approval-base-card"></a><span data-ttu-id="53f3b-117">审批基本卡</span><span class="sxs-lookup"><span data-stu-id="53f3b-117">Approval base card</span></span>

<span data-ttu-id="53f3b-118">以下代码提供了一个审批基本卡示例：</span><span class="sxs-lookup"><span data-stu-id="53f3b-118">The following code provides an example of an approval base card:</span></span>

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

## <a name="approval-card-with-approve-and-reject-buttons"></a><span data-ttu-id="53f3b-119">具有"批准"和"拒绝"按钮的审批卡片</span><span class="sxs-lookup"><span data-stu-id="53f3b-119">Approval card with Approve and Reject buttons</span></span>

<span data-ttu-id="53f3b-120">以下代码提供了一个包含"批准"和"拒绝"**按钮的审批卡片** 示例：</span><span class="sxs-lookup"><span data-stu-id="53f3b-120">The following code provides an example of an approval card with **Approve** and **Reject** buttons:</span></span>

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

<span data-ttu-id="53f3b-121">下面是根据用户参与审批请求而向用户显示的两个角色：</span><span class="sxs-lookup"><span data-stu-id="53f3b-121">Following are the two roles that are shown to users depending on their involvement in the approval request:</span></span>

* <span data-ttu-id="53f3b-122">审批基本卡：向以下用户显示：这些用户不是审批者列表的一部分，并且尚未批准或拒绝请求，并且不是自适应卡片 `userIds` JSON 属性中的 `refresh` 列表的一部分。</span><span class="sxs-lookup"><span data-stu-id="53f3b-122">Approval base card: Shown to users who are not part of approvers list and have not yet approved or rejected the request, and are not part of `userIds` list in `refresh` property of the Adaptive Card JSON.</span></span>
* <span data-ttu-id="53f3b-123">具有" **批准"** 或 **"** 拒绝"按钮的审批卡片：向作为审批者列表的一部分的用户和自适应卡片 JSON 的 属性中的列表 `userIds` `refresh` 显示。</span><span class="sxs-lookup"><span data-stu-id="53f3b-123">Approval card with **Approve** or **Reject** buttons: Shown to the users who are part of the approvers list and the `userIds` list in the `refresh` property of the Adaptive Card JSON.</span></span>

<span data-ttu-id="53f3b-124">**发送资产审批请求**</span><span class="sxs-lookup"><span data-stu-id="53f3b-124">**To send the asset approval request**</span></span>

1. <span data-ttu-id="53f3b-125">Alex 在资产审批对话中Teams资产审批请求，并将其分配给 Megan 和 Nestor。</span><span class="sxs-lookup"><span data-stu-id="53f3b-125">Alex raises an asset approval request in a Teams conversation and assigns it to Megan and Nestor.</span></span>
2. <span data-ttu-id="53f3b-126">机器人在对话中发送审批基本卡。</span><span class="sxs-lookup"><span data-stu-id="53f3b-126">Bot sends the approval base card in the conversation.</span></span>
3. <span data-ttu-id="53f3b-127">对话中的所有其他用户将看到机器人发送的卡片。</span><span class="sxs-lookup"><span data-stu-id="53f3b-127">All other users in the conversation see the card sent by the bot.</span></span> <span data-ttu-id="53f3b-128">为 Megan 和 Nestor 触发自动刷新，这些用户现在看到用户特定卡片包含"批准"或"拒绝"按钮，因为用户 MRIs 将添加到自适应卡片的 属性 `userIds` `refresh` 中的列表中。</span><span class="sxs-lookup"><span data-stu-id="53f3b-128">Automatic refresh is triggered for Megan and Nestor, who now see the user specific card with **Approve** or **Reject** buttons as their user MRIs are added to the `userIds` list in the `refresh` property of the Adaptive Card.</span></span>

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-1.png" alt-text="特定于用户的视图":::

4. <span data-ttu-id="53f3b-130">Nestor **选择使用** 进行电源的"批准"按钮 `Action.Execute` 。</span><span class="sxs-lookup"><span data-stu-id="53f3b-130">Nestor selects the **Approve** button which is powered with `Action.Execute`.</span></span> <span data-ttu-id="53f3b-131">机器人获取一 `adaptiveCard/action` 个调用请求，它可以返回自适应卡片作为响应。</span><span class="sxs-lookup"><span data-stu-id="53f3b-131">The bot gets an `adaptiveCard/action` invoke request to which it can return an Adaptive Card in response.</span></span>
5. <span data-ttu-id="53f3b-132">机器人使用更新的卡片触发邮件编辑，其中显示 Nestor 已批准请求，而 Megan 的审批挂起。</span><span class="sxs-lookup"><span data-stu-id="53f3b-132">The bot triggers a message edit with an updated card which says Nestor has approved the request while Megan's approval is pending.</span></span>
6. <span data-ttu-id="53f3b-133">自动程序消息编辑会触发 Megan 的自动刷新，她看到更新的用户特定卡片，其中显示 Nestor 已批准了请求，但还看到"批准"**或"** 拒绝"按钮。</span><span class="sxs-lookup"><span data-stu-id="53f3b-133">Bot message edit triggers an automatic refresh for Megan and she sees the updated user specific card, which says Nestor has approved the request, but also sees the **Approve** or **Reject** buttons.</span></span> <span data-ttu-id="53f3b-134">Nestor 的用户 MRI 从步骤 4 和 5 中此自适应 `userIds` 卡片 JSON 的 属性中删除 `refresh` 。</span><span class="sxs-lookup"><span data-stu-id="53f3b-134">Nestor's user MRI is removed from the `userIds` list in `refresh` property of this Adaptive Card JSON in steps 4 and 5.</span></span> <span data-ttu-id="53f3b-135">现在，仅针对 Megan 触发自动刷新。</span><span class="sxs-lookup"><span data-stu-id="53f3b-135">Now, automatic refresh is only triggered for Megan.</span></span>

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-2.png" alt-text="最新用户特定视图":::

7. <span data-ttu-id="53f3b-137">现在，Megan 选择" **批准** "按钮，该按钮由 支持 `Action.Execute` 。</span><span class="sxs-lookup"><span data-stu-id="53f3b-137">Now, Megan selects the **Approve** button, which is powered with `Action.Execute`.</span></span> <span data-ttu-id="53f3b-138">机器人获取一 `adaptiveCard/action` 个调用请求，它可以返回自适应卡片作为响应。</span><span class="sxs-lookup"><span data-stu-id="53f3b-138">The bot gets an `adaptiveCard/action` invoke request to which it can return an Adaptive Card in response.</span></span>
8. <span data-ttu-id="53f3b-139">机器人使用更新的卡片触发邮件编辑，其中显示 Nestor 和 Megan 已批准了请求。</span><span class="sxs-lookup"><span data-stu-id="53f3b-139">The bot triggers a message edit with an updated card, which says Nestor and Megan have approved the request.</span></span>
9. <span data-ttu-id="53f3b-140">自动程序消息编辑不会触发任何自动刷新。</span><span class="sxs-lookup"><span data-stu-id="53f3b-140">Bot message edit does not trigger any automatic refresh.</span></span> <span data-ttu-id="53f3b-141">还将从步骤 7 和 8 中此自适应卡片 JSON 的 属性中的列表中删除 Megan `userIds` 的用户 MRI。 `refresh`</span><span class="sxs-lookup"><span data-stu-id="53f3b-141">Megan's user MRI is also removed from the `userIds` list in `refresh` property of this Adaptive Card JSON in steps 7 and 8.</span></span>

    :::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views-3.png" alt-text="最新视图":::

## <a name="adaptive-card-sent-as-response-of-adaptivecardaction-and-message-edit"></a><span data-ttu-id="53f3b-143">作为 响应和 发送的自适应 `adaptiveCard/action` 卡片 `message edit`</span><span class="sxs-lookup"><span data-stu-id="53f3b-143">Adaptive Card sent as response of `adaptiveCard/action` and `message edit`</span></span>

<span data-ttu-id="53f3b-144">以下代码提供了作为响应和步骤 4 和 5 发送的自适应卡片 `adaptiveCard/action` `message edit` 的示例：</span><span class="sxs-lookup"><span data-stu-id="53f3b-144">The following code provides an example of Adaptive Cards sent as response of `adaptiveCard/action` and `message edit` for steps 4 and 5:</span></span>

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

<span data-ttu-id="53f3b-145">以下代码提供了通过步骤 6 的自动刷新作为调用响应发送的自适应 `adaptiveCard/action` 卡片示例：</span><span class="sxs-lookup"><span data-stu-id="53f3b-145">The following code provides an example of Adaptive Cards sent as response of `adaptiveCard/action` invoke through automatic refresh for step 6:</span></span>

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

<span data-ttu-id="53f3b-146">以下代码提供了作为 响应和步骤 7 和 8 发送的自适应卡片 `adaptiveCard/action` `message edit` 示例：</span><span class="sxs-lookup"><span data-stu-id="53f3b-146">The following code provides an example of Adaptive Cards sent as response of `adaptiveCard/action` and `message edit` for steps 7 and 8:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="53f3b-147">另请参阅</span><span class="sxs-lookup"><span data-stu-id="53f3b-147">See also</span></span>

* [<span data-ttu-id="53f3b-148">使用自适应卡片的通用操作</span><span class="sxs-lookup"><span data-stu-id="53f3b-148">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
* [<span data-ttu-id="53f3b-149">特定于用户的视图</span><span class="sxs-lookup"><span data-stu-id="53f3b-149">User Specific Views</span></span>](User-Specific-Views.md)
