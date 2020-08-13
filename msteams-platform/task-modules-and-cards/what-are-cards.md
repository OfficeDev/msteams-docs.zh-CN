---
title: 简介卡片
description: 描述卡片及其在 bot、连接器和邮件扩展中的使用方式
keywords: 连接器 bot 卡片消息传送
ms.openlocfilehash: 6d850f83183f12fa0c228a7a89b23e58f523e15b
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651654"
---
# <a name="cards"></a><span data-ttu-id="78876-104">卡</span><span class="sxs-lookup"><span data-stu-id="78876-104">Cards</span></span>

<span data-ttu-id="78876-105">*卡片*是用户界面 (UI) 容器，用于简短的或相关的信息片段。</span><span class="sxs-lookup"><span data-stu-id="78876-105">A *card* is a user-interface (UI) container for short or related pieces of information.</span></span> <span data-ttu-id="78876-106">卡片可以具有多个属性和附件。</span><span class="sxs-lookup"><span data-stu-id="78876-106">Cards can have multiple properties and attachments.</span></span> <span data-ttu-id="78876-107">卡片可以包含可触发 [卡片操作](~/task-modules-and-cards/cards/cards-actions.md)的按钮。</span><span class="sxs-lookup"><span data-stu-id="78876-107">Cards can include buttons which can trigger [Card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="78876-108">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="78876-108">Adaptive cards</span></span>

<span data-ttu-id="78876-109">[自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) 是 Microsoft 产品中卡片的一种新的矢量积规范，包括 Bot、Cortana、Outlook 和 Windows。</span><span class="sxs-lookup"><span data-stu-id="78876-109">[Adaptive cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) are a new cross product specification for cards in Microsoft products including Bots, Cortana, Outlook, and Windows.</span></span> <span data-ttu-id="78876-110">它们是新团队开发的推荐的卡片类型。</span><span class="sxs-lookup"><span data-stu-id="78876-110">They are the recommended card type for new Teams development.</span></span> <span data-ttu-id="78876-111">有关自适应卡片团队的一般信息，请参阅 [自适应卡片概述](/adaptive-cards)。</span><span class="sxs-lookup"><span data-stu-id="78876-111">For general information from the Adaptive cards team see [Adaptive Cards Overview](/adaptive-cards).</span></span> <span data-ttu-id="78876-112">您可以使用自适应卡片随时随地使用现有的英雄卡片、Office365 卡片和缩略图卡。</span><span class="sxs-lookup"><span data-stu-id="78876-112">You can use adaptive cards anywhere you can use existing Hero cards, Office365 cards, and Thumbnail cards.</span></span>

<span data-ttu-id="78876-113">除了自适应卡片之外，团队还支持其他两种类型的卡：</span><span class="sxs-lookup"><span data-stu-id="78876-113">In addition to Adaptive Cards, Teams supports two other types of cards:</span></span>

* <span data-ttu-id="78876-114">连接器卡，用作 Office 365 连接器的一部分。</span><span class="sxs-lookup"><span data-stu-id="78876-114">Connector Cards, used as part of Office 365 connectors.</span></span>
* <span data-ttu-id="78876-115">来自 bot 框架的简单卡片，如缩略图和英雄卡片。</span><span class="sxs-lookup"><span data-stu-id="78876-115">Simple cards from the bot framework, such as the thumbnail and hero cards.</span></span>

<span data-ttu-id="78876-116">这些卡类型在 [团队卡片参考](~/task-modules-and-cards/cards/cards-reference.md)中的说明更完整。</span><span class="sxs-lookup"><span data-stu-id="78876-116">These card types are described more fully in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

<span data-ttu-id="78876-117">团队在三个不同的位置使用卡片：</span><span class="sxs-lookup"><span data-stu-id="78876-117">Teams uses cards in three different places:</span></span>

* <span data-ttu-id="78876-118">连接器</span><span class="sxs-lookup"><span data-stu-id="78876-118">Connectors</span></span>
* <span data-ttu-id="78876-119">机器人</span><span class="sxs-lookup"><span data-stu-id="78876-119">Bots</span></span>
* <span data-ttu-id="78876-120">消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="78876-120">Messaging extensions</span></span>

## <a name="adaptive-cards-and-incoming-webhooks"></a><span data-ttu-id="78876-121">自适应卡片和传入 webhook</span><span class="sxs-lookup"><span data-stu-id="78876-121">Adaptive cards and incoming webhooks</span></span>

> [!NOTE]
> <span data-ttu-id="78876-122">在作为 [公共开发者预览版计划](../resources/dev-preview/developer-preview-intro.md)的一部分的传入 webhook 中支持自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="78876-122">Adaptive cards are supported in incoming webhooks as part of the [public developer preview program](../resources/dev-preview/developer-preview-intro.md).</span></span> <span data-ttu-id="78876-123">公共预览适用于早期访问和反馈。</span><span class="sxs-lookup"><span data-stu-id="78876-123">Public previews are available for early-access and feedback.</span></span> <span data-ttu-id="78876-124">尽管发布是稳定的，并且已进行了大量测试，但它并不适合在生产环境中使用。</span><span class="sxs-lookup"><span data-stu-id="78876-124">Although the release is stable and has undergone extensive testing, it is not intended for use in production.</span></span>
>
> <span data-ttu-id="78876-125">在开发人员预览中，完全支持除之外的所有本机自适应卡架构元素 `Action.Submit` 。✔</span><span class="sxs-lookup"><span data-stu-id="78876-125">✔ Within the developer preview, all native adaptive card schema elements, except `Action.Submit`, are fully supported.</span></span>
>
> <span data-ttu-id="78876-126">✔支持的操作为 [**OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html)、 [**ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)和 [**action.togglevisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)。</span><span class="sxs-lookup"><span data-stu-id="78876-126">✔ The supported Actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

## <a name="cards-in-connectors"></a><span data-ttu-id="78876-127">连接器中的卡片</span><span class="sxs-lookup"><span data-stu-id="78876-127">Cards in Connectors</span></span>

<span data-ttu-id="78876-128">卡片最初定义为 Outlook 和 Office 365 的一部分，并用作 Office 365 连接器的一部分。</span><span class="sxs-lookup"><span data-stu-id="78876-128">Cards were first defined as part of Outlook and Office 365, and are used as part of Office 365 Connectors.</span></span> <span data-ttu-id="78876-129">与许多 Office 365 应用程序一样，团队支持连接器。</span><span class="sxs-lookup"><span data-stu-id="78876-129">Like many Office 365 applications, Teams supports Connectors.</span></span> <span data-ttu-id="78876-130">可以在 [Microsoft 团队的 Office 365 连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)中了解有关连接器的详细信息，并在可 [操作邮件卡参考](/outlook/actionable-messages/card-reference)中查找连接器中的卡的规范。</span><span class="sxs-lookup"><span data-stu-id="78876-130">You can learn more about Connectors in [Office 365 Connectors for Microsoft Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md), and find the specification for cards in connectors in [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span>

## <a name="cards-in-bots"></a><span data-ttu-id="78876-131">Bot 中的卡片</span><span class="sxs-lookup"><span data-stu-id="78876-131">Cards in Bots</span></span>

<span data-ttu-id="78876-132">Microsoft Bot 框架通过添加一组预定义卡片来扩展智能卡规范，bot 可以将这些卡片用作 bot 邮件的一部分。</span><span class="sxs-lookup"><span data-stu-id="78876-132">The Microsoft Bot Framework extended the cards specification by adding a set of predefined cards that bots could use as part of bot messages.</span></span> <span data-ttu-id="78876-133">团队使用 Bot 框架支持 bot，但它支持的这些卡片集略有不同。</span><span class="sxs-lookup"><span data-stu-id="78876-133">Teams supports bots using the Bot Framework but it supports a slightly different set of these cards.</span></span> <span data-ttu-id="78876-134">可以在 [将丰富的卡片附件添加到邮件](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)中找到机器人框架中卡片的常规信息。</span><span class="sxs-lookup"><span data-stu-id="78876-134">General information on cards in Bot Framework can be found in [Add rich card attachments to messages](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards).</span></span> <span data-ttu-id="78876-135">这些卡片在团队中称为 *简单卡片* 。</span><span class="sxs-lookup"><span data-stu-id="78876-135">These cards are called *simple cards* in Teams.</span></span>

<span data-ttu-id="78876-136">团队中的 bot 可以使用任何类型的卡片：简单、连接器或自适应。</span><span class="sxs-lookup"><span data-stu-id="78876-136">Bots in Teams can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="78876-137">团队中的 bot 支持的卡片在 [团队卡片参考](~/task-modules-and-cards/cards/cards-reference.md)中详细介绍。</span><span class="sxs-lookup"><span data-stu-id="78876-137">Cards that are supported by bots in Teams are detailed in [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>  

## <a name="cards-in-messaging-extensions"></a><span data-ttu-id="78876-138">邮件分机中的卡片</span><span class="sxs-lookup"><span data-stu-id="78876-138">Cards in Messaging Extensions</span></span>

<span data-ttu-id="78876-139">[邮件扩展](~/messaging-extensions/what-are-messaging-extensions.md) 还可以返回一个卡片。</span><span class="sxs-lookup"><span data-stu-id="78876-139">[Messaging Extensions](~/messaging-extensions/what-are-messaging-extensions.md) can also return a card.</span></span> <span data-ttu-id="78876-140">邮件扩展可以使用任何类型的卡片：简单、连接器或自适应。</span><span class="sxs-lookup"><span data-stu-id="78876-140">Messaging extensions can use any type of card: simple, connector or adaptive.</span></span> <span data-ttu-id="78876-141">这些卡片位于 " [团队卡片参考](~/task-modules-and-cards/cards/cards-reference.md)" 中。</span><span class="sxs-lookup"><span data-stu-id="78876-141">These cards are found in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span>

## <a name="card-reference"></a><span data-ttu-id="78876-142">卡片参考</span><span class="sxs-lookup"><span data-stu-id="78876-142">Card reference</span></span>

<span data-ttu-id="78876-143">团队使用的所有卡片都列在 " [团队卡片" 参考](~/task-modules-and-cards/cards/cards-reference.md)中。</span><span class="sxs-lookup"><span data-stu-id="78876-143">All cards used by Teams are listed in the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md).</span></span> <span data-ttu-id="78876-144">本参考还介绍了在团队中的 Bot 框架卡片和智能卡之间的区别。</span><span class="sxs-lookup"><span data-stu-id="78876-144">This reference also describes differences between Bot Framework cards and cards in Teams.</span></span>
