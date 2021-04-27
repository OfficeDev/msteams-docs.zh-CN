---
title: 卡片介绍
description: 介绍卡及其在机器人、连接器和消息传递扩展中的使用方式
localization_priority: Normal
ms.topic: conceptual
keywords: 连接器机器人卡片消息传递
ms.openlocfilehash: acf5dc95b742a433c092be9e293d589b5919bb4d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020266"
---
# <a name="cards"></a><span data-ttu-id="da268-104">卡</span><span class="sxs-lookup"><span data-stu-id="da268-104">Cards</span></span>

<span data-ttu-id="da268-105">*卡片* 是用户界面， (UI) 或相关信息的容器。</span><span class="sxs-lookup"><span data-stu-id="da268-105">A *card* is a user-interface (UI) container for short or related pieces of information.</span></span> <span data-ttu-id="da268-106">卡片可以有多个属性和附件。</span><span class="sxs-lookup"><span data-stu-id="da268-106">Cards can have multiple properties and attachments.</span></span> <span data-ttu-id="da268-107">卡片可以包括可触发卡片操作 [的按钮](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="da268-107">Cards can include buttons which can trigger [Card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="da268-108">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="da268-108">Adaptive cards</span></span>

<span data-ttu-id="da268-109">[自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) 是 Microsoft 产品（包括 Bot、Cortana、Outlook 和 Windows）中卡片的新的跨产品规范。</span><span class="sxs-lookup"><span data-stu-id="da268-109">[Adaptive cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) are a new cross product specification for cards in Microsoft products including Bots, Cortana, Outlook, and Windows.</span></span> <span data-ttu-id="da268-110">对于新的 Teams 开发，推荐使用它们。</span><span class="sxs-lookup"><span data-stu-id="da268-110">They are the recommended card type for new Teams development.</span></span> <span data-ttu-id="da268-111">有关自适应卡片团队的常规信息，请参阅 [自适应卡片概述](/adaptive-cards)。</span><span class="sxs-lookup"><span data-stu-id="da268-111">For general information from the Adaptive cards team see [Adaptive Cards Overview](/adaptive-cards).</span></span> <span data-ttu-id="da268-112">可以在可以使用现有 Hero 卡、Office365 卡和缩略图卡片的任何位置使用自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="da268-112">You can use adaptive cards anywhere you can use existing Hero cards, Office365 cards, and Thumbnail cards.</span></span>

<span data-ttu-id="da268-113">除了自适应卡片之外，Teams 还支持两种其他类型的卡片：</span><span class="sxs-lookup"><span data-stu-id="da268-113">In addition to Adaptive Cards, Teams supports two other types of cards:</span></span>

* <span data-ttu-id="da268-114">连接器卡，用作 Office 365 连接器的一部分。</span><span class="sxs-lookup"><span data-stu-id="da268-114">Connector Cards, used as part of Office 365 connectors.</span></span>
* <span data-ttu-id="da268-115">自动程序框架中的简单卡片，如缩略图和人物卡片。</span><span class="sxs-lookup"><span data-stu-id="da268-115">Simple cards from the bot framework, such as the thumbnail and hero cards.</span></span>

<span data-ttu-id="da268-116">这些卡片类型在 Teams 卡片参考 [中进行了更全面介绍](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="da268-116">These card types are described more fully in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

<span data-ttu-id="da268-117">Teams 在三个不同位置使用卡片：</span><span class="sxs-lookup"><span data-stu-id="da268-117">Teams uses cards in three different places:</span></span>

* <span data-ttu-id="da268-118">连接器</span><span class="sxs-lookup"><span data-stu-id="da268-118">Connectors</span></span>
* <span data-ttu-id="da268-119">机器人</span><span class="sxs-lookup"><span data-stu-id="da268-119">Bots</span></span>
* <span data-ttu-id="da268-120">消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="da268-120">Messaging extensions</span></span>

## <a name="adaptive-cards-and-incoming-webhooks"></a><span data-ttu-id="da268-121">自适应卡片和传入 Webhook</span><span class="sxs-lookup"><span data-stu-id="da268-121">Adaptive cards and incoming webhooks</span></span>

> [!NOTE]
>
> <span data-ttu-id="da268-122">✔ 完全支持所有本地自适应卡架构元素（`Action.Submit` 除外）。</span><span class="sxs-lookup"><span data-stu-id="da268-122">✔ All native adaptive card schema elements, except `Action.Submit`, are fully supported.</span></span>
>
> <span data-ttu-id="da268-123">✔支持的操作包括 [**Action.OpenURL、Action.ShowCard**](https://adaptivecards.io/explorer/Action.OpenUrl.html)和 [**Action.ToggleVisibility。**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) [](https://adaptivecards.io/explorer/Action.ShowCard.html)</span><span class="sxs-lookup"><span data-stu-id="da268-123">✔ The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

## <a name="cards-in-connectors"></a><span data-ttu-id="da268-124">连接器中的卡片</span><span class="sxs-lookup"><span data-stu-id="da268-124">Cards in Connectors</span></span>

<span data-ttu-id="da268-125">卡片最初定义为 Outlook 和 Office 365 的一部分，并用作 Office 365 连接器的一部分。</span><span class="sxs-lookup"><span data-stu-id="da268-125">Cards were first defined as part of Outlook and Office 365, and are used as part of Office 365 Connectors.</span></span> <span data-ttu-id="da268-126">与许多 Office 365 应用程序一样，Teams 支持连接器。</span><span class="sxs-lookup"><span data-stu-id="da268-126">Like many Office 365 applications, Teams supports Connectors.</span></span> <span data-ttu-id="da268-127">你可以了解有关适用于 Microsoft Teams [的 Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)连接器中的连接器的更多信息，并可在可操作邮件卡参考 中查找连接器中卡片 [的规范](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="da268-127">You can learn more about Connectors in [Office 365 Connectors for Microsoft Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md), and find the specification for cards in connectors in [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span>

## <a name="cards-in-bots"></a><span data-ttu-id="da268-128">自动程序中的卡片</span><span class="sxs-lookup"><span data-stu-id="da268-128">Cards in Bots</span></span>

<span data-ttu-id="da268-129">Microsoft Bot Framework 通过添加一组自动程序可用作自动程序消息一部分的预定义卡片来扩展卡片规范。</span><span class="sxs-lookup"><span data-stu-id="da268-129">The Microsoft Bot Framework extended the cards specification by adding a set of predefined cards that bots could use as part of bot messages.</span></span> <span data-ttu-id="da268-130">Teams 支持使用 Bot Framework 的聊天机器人，但它支持一组略有不同的这些卡。</span><span class="sxs-lookup"><span data-stu-id="da268-130">Teams supports bots using the Bot Framework but it supports a slightly different set of these cards.</span></span> <span data-ttu-id="da268-131">有关 Bot Framework 中的卡片的常规信息，请参阅向邮件 [添加富卡片附件](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)。</span><span class="sxs-lookup"><span data-stu-id="da268-131">General information on cards in Bot Framework can be found in [Add rich card attachments to messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards).</span></span> <span data-ttu-id="da268-132">这些卡片在 Teams *中称为简单* 卡片。</span><span class="sxs-lookup"><span data-stu-id="da268-132">These cards are called *simple cards* in Teams.</span></span>

<span data-ttu-id="da268-133">Teams 中的机器人可以使用任何类型的卡片：简单、连接器或自适应。</span><span class="sxs-lookup"><span data-stu-id="da268-133">Bots in Teams can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="da268-134">Teams 卡参考中详细介绍了 Teams 中机器人 [支持的卡](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="da268-134">Cards that are supported by bots in Teams are detailed in [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>  

## <a name="cards-in-messaging-extensions"></a><span data-ttu-id="da268-135">邮件扩展中的卡片</span><span class="sxs-lookup"><span data-stu-id="da268-135">Cards in Messaging Extensions</span></span>

<span data-ttu-id="da268-136">[邮件扩展还可以](~/messaging-extensions/what-are-messaging-extensions.md) 返回卡片。</span><span class="sxs-lookup"><span data-stu-id="da268-136">[Messaging Extensions](~/messaging-extensions/what-are-messaging-extensions.md) can also return a card.</span></span> <span data-ttu-id="da268-137">邮件扩展可以使用任何类型的卡片：简单、连接器或自适应。</span><span class="sxs-lookup"><span data-stu-id="da268-137">Messaging extensions can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="da268-138">这些卡片位于 Teams 卡片 [参考 中](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="da268-138">These cards are found in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

## <a name="card-reference"></a><span data-ttu-id="da268-139">卡片参考</span><span class="sxs-lookup"><span data-stu-id="da268-139">Card reference</span></span>

<span data-ttu-id="da268-140">Teams 卡参考中列出了 Teams [使用的所有卡片](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="da268-140">All cards used by Teams are listed in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span> <span data-ttu-id="da268-141">本参考还介绍了 Teams 中的自动程序框架卡和卡之间的差异。</span><span class="sxs-lookup"><span data-stu-id="da268-141">This reference also describes differences between Bot Framework cards and cards in Teams.</span></span>
