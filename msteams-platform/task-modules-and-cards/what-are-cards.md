---
title: 卡
description: 介绍卡以及如何在机器人、连接器和消息传递扩展中使用
localization_priority: Normal
keywords: 连接器机器人卡片消息传递
ms.topic: overview
ms.openlocfilehash: f895423e5755dd85a7618b8907c4c3b0acbc3cf4
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140542"
---
# <a name="cards"></a><span data-ttu-id="4652e-104">卡</span><span class="sxs-lookup"><span data-stu-id="4652e-104">Cards</span></span>

<span data-ttu-id="4652e-105">卡片是用户界面， (UI) 或相关信息的容器。</span><span class="sxs-lookup"><span data-stu-id="4652e-105">A card is a user interface (UI) container for short or related pieces of information.</span></span> <span data-ttu-id="4652e-106">卡片可以有多个属性和附件，也可以包括按钮，可触发 [卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="4652e-106">Cards can have multiple properties and attachments and can include buttons, which trigger [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span> <span data-ttu-id="4652e-107">使用卡片，您可以将信息组织到组中，并使用户能够与信息的特定部分进行交互。</span><span class="sxs-lookup"><span data-stu-id="4652e-107">Using cards, you can organize information into groups and give users the opportunity to interact with specific parts of the information.</span></span>

<span data-ttu-id="4652e-108">适用于 Teams 的机器人支持以下类型的卡片：自适应卡片、人物卡片、列表卡、Office 365 连接器卡、回执卡、登录卡、缩略图卡和卡片集合。</span><span class="sxs-lookup"><span data-stu-id="4652e-108">The bots for Teams support the following types of cards: Adaptive Card, hero card, list card, Office 365 Connector card, receipt card, signin card, thumbnail card, and card collections.</span></span> <span data-ttu-id="4652e-109">可以使用 Markdown 或 HTML 将格式文本格式添加到卡片，具体取决于卡片类型。</span><span class="sxs-lookup"><span data-stu-id="4652e-109">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span> <span data-ttu-id="4652e-110">聊天机器人和邮件扩展中使用的Microsoft Teams、添加和响应这些卡片操作、 和 `openUrl` `messageBack` `imBack` `invoke` `signin` 。</span><span class="sxs-lookup"><span data-stu-id="4652e-110">Cards used by bots and messaging extensions in Microsoft Teams, add and respond to these card actions, `openUrl`, `messageBack`, `imBack`, `invoke`, and `signin`.</span></span>

<span data-ttu-id="4652e-111">Teams三个不同位置使用卡片：</span><span class="sxs-lookup"><span data-stu-id="4652e-111">Teams uses cards in three different places:</span></span>

* <span data-ttu-id="4652e-112">连接器</span><span class="sxs-lookup"><span data-stu-id="4652e-112">Connectors</span></span>
* <span data-ttu-id="4652e-113">机器人</span><span class="sxs-lookup"><span data-stu-id="4652e-113">Bots</span></span>
* <span data-ttu-id="4652e-114">消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="4652e-114">Messaging extensions</span></span>

## <a name="cards-in-connectors"></a><span data-ttu-id="4652e-115">连接器中的卡</span><span class="sxs-lookup"><span data-stu-id="4652e-115">Cards in connectors</span></span>

<span data-ttu-id="4652e-116">卡片最初定义为 Outlook 和 Office 365 的一部分，现在用作 Office 365 连接器的一部分。</span><span class="sxs-lookup"><span data-stu-id="4652e-116">Cards were first defined as part of Outlook and Office 365 and are now used as part of Office 365 Connectors.</span></span> <span data-ttu-id="4652e-117">与许多Office 365一样，Teams支持连接器。</span><span class="sxs-lookup"><span data-stu-id="4652e-117">Like many Office 365 applications, Teams supports connectors.</span></span> <span data-ttu-id="4652e-118">有关详细信息，请参阅 Office 365 [Connectors for Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="4652e-118">For more information, see [Office 365 Connectors for Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span> <span data-ttu-id="4652e-119">可以在可操作邮件卡参考 中查找连接器中卡片 [的规范](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="4652e-119">You can find the specification for cards in connectors in [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span>

## <a name="cards-in-bots"></a><span data-ttu-id="4652e-120">机器人中的卡片</span><span class="sxs-lookup"><span data-stu-id="4652e-120">Cards in bots</span></span>

<span data-ttu-id="4652e-121">该Microsoft Bot Framework添加了一组自动程序可用作自动程序消息一部分的预定义卡片，从而扩展了卡规范。</span><span class="sxs-lookup"><span data-stu-id="4652e-121">The Microsoft Bot Framework extends the cards specification by adding a set of predefined cards that bots can use as part of bot messages.</span></span> <span data-ttu-id="4652e-122">Teams使用 Bot Framework 支持自动程序，但它支持一组不同的这些卡。</span><span class="sxs-lookup"><span data-stu-id="4652e-122">Teams supports bots using the Bot Framework, but it supports a different set of these cards.</span></span> <span data-ttu-id="4652e-123">有关 Bot Framework 中卡片的常规信息，请参阅向邮件 [添加富卡片附件](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)。</span><span class="sxs-lookup"><span data-stu-id="4652e-123">General information on cards in Bot Framework can be found in [add rich card attachments to messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards).</span></span> <span data-ttu-id="4652e-124">这些卡片在卡片中称为Teams。</span><span class="sxs-lookup"><span data-stu-id="4652e-124">These cards are called simple cards in Teams.</span></span>

<span data-ttu-id="4652e-125">自动程序Teams简单卡片、连接器卡或自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="4652e-125">Bots in Teams can use simple cards, connector cards, or Adaptive Cards.</span></span> <span data-ttu-id="4652e-126">[卡片类型](~/task-modules-and-cards/cards/cards-reference.md)提供有关卡片的信息，受 Teams。</span><span class="sxs-lookup"><span data-stu-id="4652e-126">[Types of cards](~/task-modules-and-cards/cards/cards-reference.md) provides information on cards, supported by bots in Teams.</span></span>

## <a name="cards-in-messaging-extensions"></a><span data-ttu-id="4652e-127">邮件扩展中的卡片</span><span class="sxs-lookup"><span data-stu-id="4652e-127">Cards in messaging extensions</span></span>

<span data-ttu-id="4652e-128">[邮件扩展还可以](~/messaging-extensions/what-are-messaging-extensions.md) 返回卡片。</span><span class="sxs-lookup"><span data-stu-id="4652e-128">[Messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md) can also return a card.</span></span> <span data-ttu-id="4652e-129">邮件扩展可以使用简单的卡片、连接器卡或自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="4652e-129">Messaging extensions can use simple cards, connector cards, or Adaptive Cards.</span></span> <span data-ttu-id="4652e-130">这些卡片位于 [卡片类型中](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="4652e-130">These cards are found in [types of cards](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

## <a name="types-of-cards"></a><span data-ttu-id="4652e-131">卡片类型</span><span class="sxs-lookup"><span data-stu-id="4652e-131">Types of cards</span></span>

<span data-ttu-id="4652e-132">所有卡片由Teams在[卡片类型中列出](~/task-modules-and-cards/cards/cards-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="4652e-132">All cards used by Teams are listed in [types of cards](~/task-modules-and-cards/cards/cards-reference.md).</span></span> <span data-ttu-id="4652e-133">本参考还介绍了自动程序框架卡和自动程序中的Teams。</span><span class="sxs-lookup"><span data-stu-id="4652e-133">This reference also describes differences between Bot Framework cards and cards in Teams.</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="4652e-134">自适应卡</span><span class="sxs-lookup"><span data-stu-id="4652e-134">Adaptive Cards</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

<span data-ttu-id="4652e-135">[自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)是 Microsoft 产品中一种新的跨产品规范，适用于自动程序、Cortana、Outlook 和 Windows。</span><span class="sxs-lookup"><span data-stu-id="4652e-135">[Adaptive Cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) are a new cross product specification for cards in Microsoft products including bots, Cortana, Outlook, and Windows.</span></span> <span data-ttu-id="4652e-136">对于新开发，推荐使用Teams类型。</span><span class="sxs-lookup"><span data-stu-id="4652e-136">They are the recommended card type for new Teams development.</span></span> <span data-ttu-id="4652e-137">有关自适应卡片团队的常规信息，请参阅 [自适应卡片概述](/adaptive-cards)。</span><span class="sxs-lookup"><span data-stu-id="4652e-137">For general information from the Adaptive Cards team, see [Adaptive Cards overview](/adaptive-cards).</span></span> <span data-ttu-id="4652e-138">可在使用现有 Hero 卡片、卡片和缩略图卡Office 365任何位置使用自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="4652e-138">You can use Adaptive Cards anywhere you use existing hero cards, Office 365 cards, and thumbnail cards.</span></span>

<span data-ttu-id="4652e-139">除了自适应卡片，Teams支持两种其他类型的卡片：</span><span class="sxs-lookup"><span data-stu-id="4652e-139">In addition to Adaptive Cards, Teams supports two other types of cards:</span></span>

* <span data-ttu-id="4652e-140">连接器卡：用作连接器Office 365的一部分。</span><span class="sxs-lookup"><span data-stu-id="4652e-140">Connector cards: Used as part of Office 365 Connectors.</span></span>
* <span data-ttu-id="4652e-141">简单卡片：从 Bot Framework 使用，例如缩略图和 Hero 卡片。</span><span class="sxs-lookup"><span data-stu-id="4652e-141">Simple cards: Used from the Bot Framework, such as the thumbnail and hero cards.</span></span>

### <a name="adaptive-cards-and-incoming-webhooks"></a><span data-ttu-id="4652e-142">自适应卡片和传入 Webhook</span><span class="sxs-lookup"><span data-stu-id="4652e-142">Adaptive Cards and Incoming Webhooks</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/y5pbJI43Zvg]

> [!NOTE]
> * <span data-ttu-id="4652e-143">完全支持所有本机自适应卡片架构元素（除外 `Action.Submit` ）。</span><span class="sxs-lookup"><span data-stu-id="4652e-143">All native Adaptive Card schema elements, except `Action.Submit`, are fully supported.</span></span>
> * <span data-ttu-id="4652e-144">支持的操作包括 Action.OpenURL、Action.ShowCard、Action.ToggleVisibility [**和Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)。 [](https://adaptivecards.io/explorer/Action.OpenUrl.html) [](https://adaptivecards.io/explorer/Action.ShowCard.html) [](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)</span><span class="sxs-lookup"><span data-stu-id="4652e-144">The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html), and [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

<span data-ttu-id="4652e-145">通过传入 Webhook 的自适应卡片，可以使用自适应卡片的丰富而灵活的功能。</span><span class="sxs-lookup"><span data-stu-id="4652e-145">Adaptive Cards with Incoming Webhooks enables you to use the rich and flexible capabilities of Adaptive Cards.</span></span> <span data-ttu-id="4652e-146">它使用传入 Webhook 从 web 服务Teams传入 Webhook 发送数据。</span><span class="sxs-lookup"><span data-stu-id="4652e-146">It sends data using Incoming Webhooks in Teams from their web service.</span></span>

## <a name="see-also"></a><span data-ttu-id="4652e-147">另请参阅</span><span class="sxs-lookup"><span data-stu-id="4652e-147">See also</span></span>

* [<span data-ttu-id="4652e-148">格式化卡片Teams</span><span class="sxs-lookup"><span data-stu-id="4652e-148">Format cards in Teams</span></span>](~/task-modules-and-cards/cards/cards-format.md)
* [<span data-ttu-id="4652e-149">设计自适应卡片</span><span class="sxs-lookup"><span data-stu-id="4652e-149">Design Adaptive Cards</span></span>](~/task-modules-and-cards/cards/design-effective-cards.md)

## <a name="next-step"></a><span data-ttu-id="4652e-150">后续步骤</span><span class="sxs-lookup"><span data-stu-id="4652e-150">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4652e-151">卡片类型</span><span class="sxs-lookup"><span data-stu-id="4652e-151">Types of cards</span></span>](~/task-modules-and-cards/cards/cards-reference.md)