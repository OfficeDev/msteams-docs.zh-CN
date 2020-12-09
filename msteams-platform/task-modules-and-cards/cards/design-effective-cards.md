---
title: 为你的应用程序设计自适应卡片
description: 了解如何为团队设计自适应卡片和获取 Microsoft 团队 UI 工具包。
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: bd48846284620415cc8cadabc59f2ab7b61d5189
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604505"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="26868-103">为 Microsoft 团队应用程序设计自适应卡片</span><span class="sxs-lookup"><span data-stu-id="26868-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="26868-104">自适应卡片包含卡片元素的任意多边形和可选的一组操作。</span><span class="sxs-lookup"><span data-stu-id="26868-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="26868-105">自适应卡片是可通过 bot 或邮件扩展添加到对话中的可操作内容片段。</span><span class="sxs-lookup"><span data-stu-id="26868-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="26868-106">通过使用文本、图形和按钮，这些卡片可为你的受众提供丰富的通信。</span><span class="sxs-lookup"><span data-stu-id="26868-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="26868-107">自适应卡片框架跨许多 Microsoft 产品（包括团队）使用。</span><span class="sxs-lookup"><span data-stu-id="26868-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="26868-108">您可以通过 bot 或邮件分机向用户发送邮件内部的卡片。</span><span class="sxs-lookup"><span data-stu-id="26868-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="26868-109">如果有，用户可以对卡片采取操作。</span><span class="sxs-lookup"><span data-stu-id="26868-109">Users can take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="示例显示了一个自适应卡片。" border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="26868-111">Microsoft 团队 UI 工具包</span><span class="sxs-lookup"><span data-stu-id="26868-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="26868-112">您可以在 Microsoft 团队 UI 工具包中找到有关团队中的自适应卡片的更全面的设计指南，包括可以在需要时获取和修改的元素。</span><span class="sxs-lookup"><span data-stu-id="26868-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="26868-113">UI 工具包还介绍了一些基本主题，如主题、辅助功能和响应大小调整。</span><span class="sxs-lookup"><span data-stu-id="26868-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="26868-114"> (Figma) 获取 Microsoft 团队 UI 工具包 </span><span class="sxs-lookup"><span data-stu-id="26868-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="26868-115">自适应卡片设计器</span><span class="sxs-lookup"><span data-stu-id="26868-115">Adaptive Cards designer</span></span>

<span data-ttu-id="26868-116">此外，还可以在浏览器中直接开始设计自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="26868-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="26868-117">尝试自适应卡片设计器</span><span class="sxs-lookup"><span data-stu-id="26868-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="26868-118">自适应卡片的类型</span><span class="sxs-lookup"><span data-stu-id="26868-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="26868-119">主图</span><span class="sxs-lookup"><span data-stu-id="26868-119">Hero</span></span>

<span data-ttu-id="26868-120">我们最大的卡片。</span><span class="sxs-lookup"><span data-stu-id="26868-120">Our largest card.</span></span> <span data-ttu-id="26868-121">用于共享在其中显示大部分文章的文章或场景。</span><span class="sxs-lookup"><span data-stu-id="26868-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="thumbnail"></a><span data-ttu-id="26868-123">缩略图</span><span class="sxs-lookup"><span data-stu-id="26868-123">Thumbnail</span></span>

<span data-ttu-id="26868-124">用于发送简单的可操作邮件。</span><span class="sxs-lookup"><span data-stu-id="26868-124">Use for sending a simple actionable message.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="list"></a><span data-ttu-id="26868-126">列表</span><span class="sxs-lookup"><span data-stu-id="26868-126">List</span></span>

<span data-ttu-id="26868-127">在希望用户从列表中选取项目的情况下使用，但这些项目不需要很多说明。</span><span class="sxs-lookup"><span data-stu-id="26868-127">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="digest"></a><span data-ttu-id="26868-129">Digest</span><span class="sxs-lookup"><span data-stu-id="26868-129">Digest</span></span>

<span data-ttu-id="26868-130">用于新闻摘要和向上舍入文章。</span><span class="sxs-lookup"><span data-stu-id="26868-130">Use for news digests and round-up posts.</span></span> <span data-ttu-id="26868-131">注意：我们建议单个更新或新闻项目的缩略图卡。</span><span class="sxs-lookup"><span data-stu-id="26868-131">Note: We recommend the thumbnail card for a single update or news item.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="media"></a><span data-ttu-id="26868-133">媒体</span><span class="sxs-lookup"><span data-stu-id="26868-133">Media</span></span>

<span data-ttu-id="26868-134">当您想要组合文本和媒体（如音频或视频）时使用。</span><span class="sxs-lookup"><span data-stu-id="26868-134">Use when you want to combine text and media, like audio or video.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="people"></a><span data-ttu-id="26868-136">人员</span><span class="sxs-lookup"><span data-stu-id="26868-136">People</span></span>

<span data-ttu-id="26868-137">最适用于有效传达任务所涉及的人员的情况。</span><span class="sxs-lookup"><span data-stu-id="26868-137">Best used when you to efficiently convey who's involved with a task.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="request-ticket"></a><span data-ttu-id="26868-139">请求票证</span><span class="sxs-lookup"><span data-stu-id="26868-139">Request ticket</span></span>

<span data-ttu-id="26868-140">用于获取来自用户的快速输入，以自动创建任务或票证。</span><span class="sxs-lookup"><span data-stu-id="26868-140">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="imageset"></a><span data-ttu-id="26868-142">ImageSet</span><span class="sxs-lookup"><span data-stu-id="26868-142">ImageSet</span></span>

<span data-ttu-id="26868-143">使用发送多个图像缩略图。</span><span class="sxs-lookup"><span data-stu-id="26868-143">Use to send multiple image thumbnails.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="actionset"></a><span data-ttu-id="26868-145">ActionSet</span><span class="sxs-lookup"><span data-stu-id="26868-145">ActionSet</span></span>

<span data-ttu-id="26868-146">在您希望用户选择按钮时使用，然后从同一卡片收集添加用户输入。</span><span class="sxs-lookup"><span data-stu-id="26868-146">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="choiceset"></a><span data-ttu-id="26868-148">ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="26868-148">ChoiceSet</span></span>

<span data-ttu-id="26868-149">使用收集用户的多个输入。</span><span class="sxs-lookup"><span data-stu-id="26868-149">Use to gather multiple inputs from the user.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

## <a name="anatomy"></a><span data-ttu-id="26868-151">解析</span><span class="sxs-lookup"><span data-stu-id="26868-151">Anatomy</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="显示自适应卡片的 UI 剖析的图示。" border="false":::

<span data-ttu-id="26868-153">自适应卡片具有很大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="26868-153">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="26868-154">但至少我们建议在每个卡片中包括以下组件：</span><span class="sxs-lookup"><span data-stu-id="26868-154">But at a minimum, we strongly suggest including the following components in every card:</span></span>

|<span data-ttu-id="26868-155">计数器</span><span class="sxs-lookup"><span data-stu-id="26868-155">Counter</span></span>|<span data-ttu-id="26868-156">描述</span><span class="sxs-lookup"><span data-stu-id="26868-156">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="26868-157">A</span><span class="sxs-lookup"><span data-stu-id="26868-157">A</span></span>|<span data-ttu-id="26868-158">**标头**：使标头清晰明了，但却是描述性的。</span><span class="sxs-lookup"><span data-stu-id="26868-158">**Header**: Make headers clear and concise, yet descriptive.</span></span>|
|<span data-ttu-id="26868-159">B</span><span class="sxs-lookup"><span data-stu-id="26868-159">B</span></span>|<span data-ttu-id="26868-160">**正文副本**：用于传递的详细信息太长或不够重要，无法包含在标头中。</span><span class="sxs-lookup"><span data-stu-id="26868-160">**Body copy**: Use to convey detail that is either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="26868-161">C</span><span class="sxs-lookup"><span data-stu-id="26868-161">C</span></span>|<span data-ttu-id="26868-162">**主要操作**：最佳实践包括1-3 主要操作。</span><span class="sxs-lookup"><span data-stu-id="26868-162">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="26868-163">最多允许6个。</span><span class="sxs-lookup"><span data-stu-id="26868-163">A maximum of six are allowed.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="26868-164">最佳做法</span><span class="sxs-lookup"><span data-stu-id="26868-164">Best practices</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="26868-165">主要操作和次要操作</span><span class="sxs-lookup"><span data-stu-id="26868-165">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="显示自适应卡片最佳实践的示例。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="26868-167">操作：使用最大6个主要操作</span><span class="sxs-lookup"><span data-stu-id="26868-167">Do: Use up to six primary actions</span></span>

<span data-ttu-id="26868-168">自适应卡可支持六个主要操作，而大多数卡片不需要。</span><span class="sxs-lookup"><span data-stu-id="26868-168">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="26868-169">操作应清晰、简明且直接向前。</span><span class="sxs-lookup"><span data-stu-id="26868-169">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="26868-170">越少越好。</span><span class="sxs-lookup"><span data-stu-id="26868-170">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="显示自适应卡片最佳实践的示例。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="26868-172">请勿：使用6个以上的主要操作</span><span class="sxs-lookup"><span data-stu-id="26868-172">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="26868-173">自适应卡片应提供快速的可操作内容。</span><span class="sxs-lookup"><span data-stu-id="26868-173">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="26868-174">操作过多可能会严重影响用户。</span><span class="sxs-lookup"><span data-stu-id="26868-174">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="26868-175">频率</span><span class="sxs-lookup"><span data-stu-id="26868-175">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="显示自适应卡片最佳实践的示例。" border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="26868-177">Do：简单明了</span><span class="sxs-lookup"><span data-stu-id="26868-177">Do: Be concise</span></span>

<span data-ttu-id="26868-178">可以轻松地将多个卡片发送到对话中，但一旦卡片从视图中滚出，它们就会变得不太有用。</span><span class="sxs-lookup"><span data-stu-id="26868-178">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="26868-179">尝试将自己限制为重点。</span><span class="sxs-lookup"><span data-stu-id="26868-179">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="26868-180">在用户对其感觉为 "干扰" 的程度较差的频道中，尤其如此。</span><span class="sxs-lookup"><span data-stu-id="26868-180">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>
