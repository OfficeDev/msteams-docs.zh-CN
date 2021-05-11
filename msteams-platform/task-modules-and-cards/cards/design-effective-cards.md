---
title: 为应用设计自适应卡片
description: 了解如何为用户设计自适应Teams并获取 Microsoft Teams UI 工具包。
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 14ffff1264e716e04a1ffb5549b71a8b7ec5fc14
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101735"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="3e0b1-103">为应用设计自适应Microsoft Teams卡片</span><span class="sxs-lookup"><span data-stu-id="3e0b1-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="3e0b1-104">自适应卡片包含卡片元素和可选操作集的免费格式正文。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="3e0b1-105">自适应卡片是内容可操作的代码段，可以通过机器人或消息传递扩展添加到对话中。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="3e0b1-106">这些卡片使用文本、图形和按钮，向受众提供丰富的通信。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="3e0b1-107">自适应卡片框架适用于许多 Microsoft 产品，包括Teams。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="3e0b1-108">可以通过机器人或消息扩展向用户发送内部邮件卡片。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="3e0b1-109">存在此情况时，用户可以对卡片采取操作。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-109">Users can take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="自适应卡片的概述示例。" border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="3e0b1-111">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="3e0b1-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="3e0b1-112">你可以找到适用于 Teams 中的自适应卡片的更全面的设计指南，包括可根据需要获取和修改的元素，Microsoft Teams UI 工具包。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="3e0b1-113">UI 工具包还涵盖了主题设置、辅助功能和响应式大小调整等重要主题。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3e0b1-114">获取 Microsoft Teams UI Kit （用户）</span><span class="sxs-lookup"><span data-stu-id="3e0b1-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="3e0b1-115">自适应卡片设计器</span><span class="sxs-lookup"><span data-stu-id="3e0b1-115">Adaptive Cards designer</span></span>

<span data-ttu-id="3e0b1-116">还可以直接在浏览器中开始设计自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3e0b1-117">试用自适应卡片设计器</span><span class="sxs-lookup"><span data-stu-id="3e0b1-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="3e0b1-118">自适应卡片的类型</span><span class="sxs-lookup"><span data-stu-id="3e0b1-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="3e0b1-119">主图</span><span class="sxs-lookup"><span data-stu-id="3e0b1-119">Hero</span></span>

<span data-ttu-id="3e0b1-120">我们最大的卡片。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-120">Our largest card.</span></span> <span data-ttu-id="3e0b1-121">用于共享文章或场景，其中图像可以描述大部分情景。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="示例显示自适应卡片展示卡。" border="false":::

### <a name="thumbnail"></a><span data-ttu-id="3e0b1-123">缩略图</span><span class="sxs-lookup"><span data-stu-id="3e0b1-123">Thumbnail</span></span>

<span data-ttu-id="3e0b1-124">用于发送简单的可操作邮件。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-124">Use for sending a simple actionable message.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="示例显示自适应卡片缩略图卡片。" border="false":::

### <a name="list"></a><span data-ttu-id="3e0b1-126">列表</span><span class="sxs-lookup"><span data-stu-id="3e0b1-126">List</span></span>

<span data-ttu-id="3e0b1-127">在您希望用户从列表中选取项目，但项目不需要太多解释的情况下使用。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-127">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="示例显示自适应卡片列表卡片。" border="false":::

### <a name="digest"></a><span data-ttu-id="3e0b1-129">Digest</span><span class="sxs-lookup"><span data-stu-id="3e0b1-129">Digest</span></span>

<span data-ttu-id="3e0b1-130">用于新闻摘要和向上舍入帖子。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-130">Use for news digests and round-up posts.</span></span> <span data-ttu-id="3e0b1-131">注意：我们建议使用单个更新或新闻项的缩略图卡片。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-131">Note: We recommend the thumbnail card for a single update or news item.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="示例显示自适应卡片摘要卡片。" border="false":::

### <a name="media"></a><span data-ttu-id="3e0b1-133">媒体</span><span class="sxs-lookup"><span data-stu-id="3e0b1-133">Media</span></span>

<span data-ttu-id="3e0b1-134">在你想要组合文本和媒体（如音频或视频）时使用。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-134">Use when you want to combine text and media, like audio or video.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="示例显示自适应卡片媒体卡。" border="false":::

### <a name="people"></a><span data-ttu-id="3e0b1-136">人员</span><span class="sxs-lookup"><span data-stu-id="3e0b1-136">People</span></span>

<span data-ttu-id="3e0b1-137">最适用于有效传达任务涉及人员。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-137">Best used when you to efficiently convey who's involved with a task.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="示例显示自适应卡片人员卡片。" border="false":::

### <a name="request-ticket"></a><span data-ttu-id="3e0b1-139">请求票证</span><span class="sxs-lookup"><span data-stu-id="3e0b1-139">Request ticket</span></span>

<span data-ttu-id="3e0b1-140">用于从用户处获取快速输入，以自动创建任务或票证。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-140">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="示例显示自适应卡片请求票证卡。" border="false":::

### <a name="imageset"></a><span data-ttu-id="3e0b1-142">ImageSet</span><span class="sxs-lookup"><span data-stu-id="3e0b1-142">ImageSet</span></span>

<span data-ttu-id="3e0b1-143">用于发送多个图像缩略图。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-143">Use to send multiple image thumbnails.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="示例显示自适应卡片图像集卡。" border="false":::

### <a name="actionset"></a><span data-ttu-id="3e0b1-145">ActionSet</span><span class="sxs-lookup"><span data-stu-id="3e0b1-145">ActionSet</span></span>

<span data-ttu-id="3e0b1-146">当你希望用户选择一个按钮，然后从同一卡片收集添加的用户输入时，使用 。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-146">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="示例显示自适应卡片操作集卡片。" border="false":::

### <a name="choiceset"></a><span data-ttu-id="3e0b1-148">ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="3e0b1-148">ChoiceSet</span></span>

<span data-ttu-id="3e0b1-149">用于收集用户的多个输入。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-149">Use to gather multiple inputs from the user.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="示例显示自适应卡片选择集卡。" border="false":::

## <a name="anatomy"></a><span data-ttu-id="3e0b1-151">解剖</span><span class="sxs-lookup"><span data-stu-id="3e0b1-151">Anatomy</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="示例显示自适应卡片分析卡。" border="false":::

<span data-ttu-id="3e0b1-153">自适应卡片具有很多灵活性。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-153">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="3e0b1-154">但是，我们强烈建议至少将以下组件包括在每张卡片中：</span><span class="sxs-lookup"><span data-stu-id="3e0b1-154">But at minimum, we strongly suggest including the following components in every card:</span></span>

|<span data-ttu-id="3e0b1-155">计数器</span><span class="sxs-lookup"><span data-stu-id="3e0b1-155">Counter</span></span>|<span data-ttu-id="3e0b1-156">说明</span><span class="sxs-lookup"><span data-stu-id="3e0b1-156">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="3e0b1-157">A</span><span class="sxs-lookup"><span data-stu-id="3e0b1-157">A</span></span>|<span data-ttu-id="3e0b1-158">**标头**：使标题简洁明了，但具有描述性。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-158">**Header**: Make headers clear and concise, yet descriptive.</span></span>|
|<span data-ttu-id="3e0b1-159">B</span><span class="sxs-lookup"><span data-stu-id="3e0b1-159">B</span></span>|<span data-ttu-id="3e0b1-160">**正文** 副本：用于传达太长或不够重要以包括在标头中的详细信息。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-160">**Body copy**: Use to convey detail that is either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="3e0b1-161">C</span><span class="sxs-lookup"><span data-stu-id="3e0b1-161">C</span></span>|<span data-ttu-id="3e0b1-162">**主要操作**：最佳做法包括 1-3 个主要操作。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-162">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="3e0b1-163">最多允许六个。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-163">A maximum of six are allowed.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="3e0b1-164">最佳做法</span><span class="sxs-lookup"><span data-stu-id="3e0b1-164">Best practices</span></span>

<span data-ttu-id="3e0b1-165">使用这些建议创建高质量的应用体验。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-165">Use these recommendations to create a quality app experience.</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="3e0b1-166">主要操作和辅助操作</span><span class="sxs-lookup"><span data-stu-id="3e0b1-166">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="有关如何在自适应卡片上仅包含一小组操作的最佳操作。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="3e0b1-168">操作：最多使用六个主要操作</span><span class="sxs-lookup"><span data-stu-id="3e0b1-168">Do: Use up to six primary actions</span></span>

<span data-ttu-id="3e0b1-169">自适应卡片可以支持六个主要操作，但大多数卡片不需要这一点。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-169">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="3e0b1-170">操作应简洁明了。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-170">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="3e0b1-171">"少"表示"更多"。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-171">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="有关在自适应卡片上不使用户不知所措以及操作太多的最佳操作。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="3e0b1-173">请勿：使用超过 6 个主要操作</span><span class="sxs-lookup"><span data-stu-id="3e0b1-173">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="3e0b1-174">自适应卡片应显示快速且可操作的内容。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-174">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="3e0b1-175">操作太多可能会使用户感到不知所措。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-175">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="3e0b1-176">频率</span><span class="sxs-lookup"><span data-stu-id="3e0b1-176">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="自适应卡片频率的最佳实践。" border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="3e0b1-178">应做：简洁</span><span class="sxs-lookup"><span data-stu-id="3e0b1-178">Do: Be concise</span></span>

<span data-ttu-id="3e0b1-179">向对话中发送多个卡片很容易，但在卡片滚动到视图外后，它们变得不太有用。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-179">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="3e0b1-180">尝试将自己限制为基本功能。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-180">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="3e0b1-181">在用户对"噪音"所感知的容忍度较低的频道中尤其如此。</span><span class="sxs-lookup"><span data-stu-id="3e0b1-181">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>
