---
title: 使用自适应卡的通用操作
description: 使用自适应卡片的通用操作。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 8c260a4893d38ad365cbb3bdd5a7613a1b42654f
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088821"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a><span data-ttu-id="6e6df-103">使用自适应卡的通用操作</span><span class="sxs-lookup"><span data-stu-id="6e6df-103">Work with Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="6e6df-104">自适应卡片的通用操作提供了一种为用户和用户实现基于自适应卡片Teams Outlook。</span><span class="sxs-lookup"><span data-stu-id="6e6df-104">Universal Actions for Adaptive Cards provides a way to implement Adaptive Card based scenarios for both, Teams and Outlook.</span></span> <span data-ttu-id="6e6df-105">本文档涵盖以下内容：</span><span class="sxs-lookup"><span data-stu-id="6e6df-105">This document covers the following:</span></span>

* [<span data-ttu-id="6e6df-106">用于自适应卡片的通用操作架构</span><span class="sxs-lookup"><span data-stu-id="6e6df-106">Schema used for Universal Actions for Adaptive Cards</span></span>](#schema-for-universal-actions-for-adaptive-cards)
* [<span data-ttu-id="6e6df-107">刷新模型</span><span class="sxs-lookup"><span data-stu-id="6e6df-107">Refresh model</span></span>](#refresh-model)
* [<span data-ttu-id="6e6df-108">`adaptiveCard/action` 调用活动</span><span class="sxs-lookup"><span data-stu-id="6e6df-108">`adaptiveCard/action` invoke activity</span></span>](#adaptivecardaction-invoke-activity)
* [<span data-ttu-id="6e6df-109">向后兼容性</span><span class="sxs-lookup"><span data-stu-id="6e6df-109">Backward compatibility</span></span>](#backward-compatibility)

## <a name="quick-start-guide-to-leverage-universal-actions-for-adaptive-cards-in-teams"></a><span data-ttu-id="6e6df-110">快速入门指南，用于将通用操作用于自适应卡片Teams</span><span class="sxs-lookup"><span data-stu-id="6e6df-110">Quick start guide to leverage Universal Actions for Adaptive Cards in Teams</span></span>

1. <span data-ttu-id="6e6df-111">将 的所有 实例 `Action.Submit` 替换为 ， `Action.Execute` 以更新现有Teams。</span><span class="sxs-lookup"><span data-stu-id="6e6df-111">Replace all instances of `Action.Submit` with `Action.Execute` to update an existing scenario on Teams.</span></span>
2. <span data-ttu-id="6e6df-112">如果你希望利用自动刷新模型或你的方案需要特定于用户的视图，则向 `refresh` 自适应卡片中添加子句。</span><span class="sxs-lookup"><span data-stu-id="6e6df-112">Add a `refresh` clause to your Adaptive Card, if you want to leverage the automatic refresh model or if your scenario requires User Specific Views.</span></span>

    >[!NOTE]
    > <span data-ttu-id="6e6df-113">指定 `userIds` 要标识哪些用户获得自动更新的属性。</span><span class="sxs-lookup"><span data-stu-id="6e6df-113">Specify the `userIds` property to identify, which users get automatic updates.</span></span>

3. <span data-ttu-id="6e6df-114">处理 `adaptiveCard/action` 机器人中的调用请求。</span><span class="sxs-lookup"><span data-stu-id="6e6df-114">Handle `adaptiveCard/action` invoke requests in your bot.</span></span>
4. <span data-ttu-id="6e6df-115">使用调用请求的上下文通过专为用户创建的卡片进行响应。</span><span class="sxs-lookup"><span data-stu-id="6e6df-115">Use the invoke request's context to respond back with cards that are specifically created for a user.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6e6df-116">只要机器人处理 后返回新卡， `Action.Execute` 响应就必须符合响应格式。</span><span class="sxs-lookup"><span data-stu-id="6e6df-116">Whenever your bot returns a new card as a result of processing an `Action.Execute`, the response must conform to the response format.</span></span>

## <a name="schema-for-universal-actions-for-adaptive-cards"></a><span data-ttu-id="6e6df-117">自适应卡片的通用操作架构</span><span class="sxs-lookup"><span data-stu-id="6e6df-117">Schema for Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="6e6df-118">自适应卡片的通用操作在自适应卡片架构版本 1.4 中引入。</span><span class="sxs-lookup"><span data-stu-id="6e6df-118">Universal Actions for Adaptive Cards is introduced in the Adaptive Cards schema version 1.4.</span></span> <span data-ttu-id="6e6df-119">若要有效地使用自适应卡片，必须将自适应卡片的 属性 `version` 设置为 1.4。</span><span class="sxs-lookup"><span data-stu-id="6e6df-119">To use Adaptive Card effectively, the `version` property of your Adaptive Card must be set to 1.4.</span></span>

> [!NOTE]
> <span data-ttu-id="6e6df-120">将 该属性设置为 1.4 会使自适应卡片与平台或应用程序（如 Outlook 和 Teams）的较旧客户端不兼容，因为它们不支持自适应卡片的通用操作 `version` 。</span><span class="sxs-lookup"><span data-stu-id="6e6df-120">Setting the `version` property to 1.4 makes your Adaptive Card incompatible with older clients of the platforms or applications, such as Outlook and Teams, as they do not support the Universal Actions for Adaptive Cards.</span></span>

<span data-ttu-id="6e6df-121">如果将卡版本设置为小于 1.4，并使用 属性 和 或 两者之一， `refresh` `Action.Execute` 将发生以下情况：</span><span class="sxs-lookup"><span data-stu-id="6e6df-121">If you set the card version to less than 1.4 and use either or both, `refresh` property and `Action.Execute`, the following happens:</span></span>

| <span data-ttu-id="6e6df-122">Client</span><span class="sxs-lookup"><span data-stu-id="6e6df-122">Client</span></span> | <span data-ttu-id="6e6df-123">行为</span><span class="sxs-lookup"><span data-stu-id="6e6df-123">Behavior</span></span> |
| :-- | :-- |
| <span data-ttu-id="6e6df-124">Teams</span><span class="sxs-lookup"><span data-stu-id="6e6df-124">Teams</span></span> | <span data-ttu-id="6e6df-125">你的卡片停止工作。</span><span class="sxs-lookup"><span data-stu-id="6e6df-125">Your card stops working.</span></span> <span data-ttu-id="6e6df-126">卡片不会刷新， `Action.Execute` 并且不会呈现，具体取决于 Teams 版本。</span><span class="sxs-lookup"><span data-stu-id="6e6df-126">Card is not refreshed and `Action.Execute` does not render depending on the version of the Teams client.</span></span> <span data-ttu-id="6e6df-127">若要确保应用程序的最大Teams，请通过 回退 `Action.Execute` `Action.Submit` 属性中的 定义 。</span><span class="sxs-lookup"><span data-stu-id="6e6df-127">To ensure maximum compatibility in Teams, define `Action.Execute` with an `Action.Submit` in the fallback property.</span></span> |

<span data-ttu-id="6e6df-128">若要详细了解如何支持旧客户端，请参阅 [向后兼容性](#backward-compatibility)。</span><span class="sxs-lookup"><span data-stu-id="6e6df-128">For more information on how to support older clients, see [backward compatibility](#backward-compatibility).</span></span>

### <a name="actionexecute"></a><span data-ttu-id="6e6df-129">Action.Execute</span><span class="sxs-lookup"><span data-stu-id="6e6df-129">Action.Execute</span></span>

<span data-ttu-id="6e6df-130">创作自适应卡片时，请将 和 `Action.Submit` `Action.Http` 替换为 `Action.Execute` 。</span><span class="sxs-lookup"><span data-stu-id="6e6df-130">When authoring Adaptive Cards, replace `Action.Submit` and `Action.Http` with `Action.Execute`.</span></span> <span data-ttu-id="6e6df-131">的 `Action.Execute` 架构类似于 `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="6e6df-131">The schema for `Action.Execute` is similar to that of `Action.Submit`.</span></span>

<span data-ttu-id="6e6df-132">有关详细信息，请参阅Action.Exe[ 和属性](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute)。</span><span class="sxs-lookup"><span data-stu-id="6e6df-132">For more information, see [Action.Execute schema and properties](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

<span data-ttu-id="6e6df-133">现在，可以使用刷新模型允许自适应卡片自动更新。</span><span class="sxs-lookup"><span data-stu-id="6e6df-133">Now, you can use the refresh model to allow Adaptive Cards to update automatically.</span></span>

## <a name="refresh-model"></a><span data-ttu-id="6e6df-134">刷新模型</span><span class="sxs-lookup"><span data-stu-id="6e6df-134">Refresh model</span></span>

<span data-ttu-id="6e6df-135">若要自动刷新自适应卡片，请定义其 `refresh` 属性，这将嵌入类型和 `Action.Execute` 数组 `userIds` 的操作。</span><span class="sxs-lookup"><span data-stu-id="6e6df-135">To automatically refresh your Adaptive Card, define its `refresh` property, which embeds an action of type `Action.Execute` and an `userIds` array.</span></span>

<span data-ttu-id="6e6df-136">有关详细信息，请参阅 [刷新架构和属性](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism)。</span><span class="sxs-lookup"><span data-stu-id="6e6df-136">For more information, see [refresh schema and properties](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism).</span></span>

## <a name="user-ids-in-refresh"></a><span data-ttu-id="6e6df-137">刷新中的用户 ID</span><span class="sxs-lookup"><span data-stu-id="6e6df-137">User IDs in refresh</span></span>

<span data-ttu-id="6e6df-138">以下是刷新中的 UserIds 的功能：</span><span class="sxs-lookup"><span data-stu-id="6e6df-138">The following are the features of UserIds in refresh:</span></span>

* <span data-ttu-id="6e6df-139">UserIds 是用户 MRI 的数组，它是自适应卡片 `refresh` 中属性的一部分。</span><span class="sxs-lookup"><span data-stu-id="6e6df-139">UserIds is an array of user MRI's which is part of the `refresh` property in Adaptive Cards.</span></span>

* <span data-ttu-id="6e6df-140">如果在卡片的刷新部分中指定了 list 属性，则不会自动 `userIds` `userIds: []` 刷新该卡片。</span><span class="sxs-lookup"><span data-stu-id="6e6df-140">If the `userIds` list property is specified as `userIds: []` in the refresh section of the card, the card is not automatically refreshed.</span></span> <span data-ttu-id="6e6df-141">而是 **在** Web 或桌面的三点菜单和移动设备（即 Android 或 iOS）中的长按上下文菜单中向用户显示"刷新卡片"选项，以手动刷新卡片。</span><span class="sxs-lookup"><span data-stu-id="6e6df-141">Instead, a **Refresh Card** option is displayed to the user in the triple dot menu in web or desktop and in the long press context menu in mobile, that is, Android or iOS to manually refresh the card.</span></span>

* <span data-ttu-id="6e6df-142">添加 UserIds 属性是因为Teams频道可以包含大量成员。</span><span class="sxs-lookup"><span data-stu-id="6e6df-142">UserIds property is added because channels in Teams can include a large number of members.</span></span> <span data-ttu-id="6e6df-143">如果所有成员同时查看频道，则无条件自动刷新会导致对机器人进行许多并发呼叫。</span><span class="sxs-lookup"><span data-stu-id="6e6df-143">If all members are viewing the channel at the same time, an unconditional automatic refresh results in many concurrent calls to the bot.</span></span> <span data-ttu-id="6e6df-144">若要避免这种情况，必须始终包括 属性，以确定哪些用户必须自动刷新，最多 `userIds` *60 (60*) MRIs 。</span><span class="sxs-lookup"><span data-stu-id="6e6df-144">To avoid this, the `userIds` property must always be included to identify which users must get an automatic refresh with a maximum of *60 (sixty) user MRIs*.</span></span>

* <span data-ttu-id="6e6df-145">若要详细了解如何提取对话Teams用户 MRIs 以在自适应卡片刷新部分添加 userIds 列表，请参阅提取[名单或用户配置文件](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)。</span><span class="sxs-lookup"><span data-stu-id="6e6df-145">For more information on how you can fetch Teams conversation member's user MRIs to add in userIds list in refresh section of Adaptive Card, see [fetch roster or user profile](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).</span></span>

* <span data-ttu-id="6e6df-146">用户 MRI Teams示例`29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`</span><span class="sxs-lookup"><span data-stu-id="6e6df-146">Sample Teams user MRI is `29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`</span></span>

> [!NOTE]
> <span data-ttu-id="6e6df-147">该属性 `userIds` 在属性Outlook， `refresh` 并且始终自动激活。</span><span class="sxs-lookup"><span data-stu-id="6e6df-147">The `userIds` property is ignored in Outlook, and the `refresh` property is always automatically activated.</span></span> <span data-ttu-id="6e6df-148">由于用户在不同时间查看Outlook，因此在卡片中不存在缩放问题。</span><span class="sxs-lookup"><span data-stu-id="6e6df-148">There is no scale issue in Outlook because users view the card at different times.</span></span>

<span data-ttu-id="6e6df-149">下一步是使用 `adaptiveCard/action` 调用活动了解在执行后必须提出 `Action.Execute` 哪些请求。</span><span class="sxs-lookup"><span data-stu-id="6e6df-149">Next step is to use the `adaptiveCard/action` invoke activity to understand what request must be made after `Action.Execute` is executed.</span></span>

## <a name="adaptivecardaction-invoke-activity"></a><span data-ttu-id="6e6df-150">`adaptiveCard/action` 调用活动</span><span class="sxs-lookup"><span data-stu-id="6e6df-150">`adaptiveCard/action` invoke activity</span></span>

<span data-ttu-id="6e6df-151">When `Action.Execute` is executed in the client， a new type of Invoke activity `adaptiveCard/action` is made to your bot.</span><span class="sxs-lookup"><span data-stu-id="6e6df-151">When `Action.Execute` is executed in the client, a new type of Invoke activity `adaptiveCard/action` is made to your bot.</span></span>

<span data-ttu-id="6e6df-152">有关详细信息，请参阅典型调用活动的请求 [格式 `adaptiveCard/action` 和属性](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#request-format)。</span><span class="sxs-lookup"><span data-stu-id="6e6df-152">For more information, see [request format and properties for a typical `adaptiveCard/action` invoke activity](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#request-format).</span></span>

<span data-ttu-id="6e6df-153">有关详细信息，请参阅具有受支持的 [响应类型的典型 `adaptiveCard/action` 调用活动的响应格式和属性](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#response-format)。</span><span class="sxs-lookup"><span data-stu-id="6e6df-153">For more information, see [response format and properties for a typical `adaptiveCard/action` invoke activity with supported response types](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#response-format).</span></span>

<span data-ttu-id="6e6df-154">接下来，你可以跨不同平台将向后兼容性应用到较旧的客户端，并兼容自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="6e6df-154">Next, you can apply backward compatibility to older clients across different platforms and make your Adaptive Card compatible.</span></span>

## <a name="backward-compatibility"></a><span data-ttu-id="6e6df-155">向后兼容性</span><span class="sxs-lookup"><span data-stu-id="6e6df-155">Backward compatibility</span></span>

<span data-ttu-id="6e6df-156">自适应卡片的通用操作允许你设置属性，以便向后兼容早期版本的 Outlook 和 Teams。</span><span class="sxs-lookup"><span data-stu-id="6e6df-156">Universal Actions for Adaptive Cards allows you to set properties that enable backward compatibility with older versions of Outlook and Teams.</span></span>

### <a name="teams"></a><span data-ttu-id="6e6df-157">Teams</span><span class="sxs-lookup"><span data-stu-id="6e6df-157">Teams</span></span>

<span data-ttu-id="6e6df-158">若要确保自适应卡片与旧版卡片的向后Teams，必须包含 属性，并 `fallback` 设置其值 `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="6e6df-158">To ensure backward compatibility of your Adaptive Cards with older versions of Teams, you must include the `fallback` property and set its value to `Action.Submit`.</span></span> <span data-ttu-id="6e6df-159">此外，自动程序代码必须同时处理 `Action.Execute` 和 `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="6e6df-159">Also, your bot code must process both `Action.Execute` and `Action.Submit`.</span></span>

<span data-ttu-id="6e6df-160">有关详细信息，请参阅[上向后兼容性Teams。](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#teams)</span><span class="sxs-lookup"><span data-stu-id="6e6df-160">For more information, see [backward compatibility on Teams](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#teams).</span></span>

## <a name="see-also"></a><span data-ttu-id="6e6df-161">另请参阅</span><span class="sxs-lookup"><span data-stu-id="6e6df-161">See also</span></span>

* [<span data-ttu-id="6e6df-162">用户中的自适应卡片Teams</span><span class="sxs-lookup"><span data-stu-id="6e6df-162">Adaptive Card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [<span data-ttu-id="6e6df-163">机器人的工作方式</span><span class="sxs-lookup"><span data-stu-id="6e6df-163">How bots work</span></span>](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
