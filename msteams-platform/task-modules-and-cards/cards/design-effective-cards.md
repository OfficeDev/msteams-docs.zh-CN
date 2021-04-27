---
title: 为应用设计自适应卡片
description: 了解如何为 Teams 设计自适应卡片并获取 Microsoft Teams UI 工具包。
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 67a2882a0a687d5ccb48759419ecefcdf9396fc3
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020280"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="71889-103">为 Microsoft Teams 应用设计自适应卡片</span><span class="sxs-lookup"><span data-stu-id="71889-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="71889-104">自适应卡片包含卡片元素和可选操作集的免费格式正文。</span><span class="sxs-lookup"><span data-stu-id="71889-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="71889-105">自适应卡片是内容可操作的代码段，可以通过机器人或消息传递扩展添加到对话中。</span><span class="sxs-lookup"><span data-stu-id="71889-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="71889-106">这些卡片使用文本、图形和按钮，向受众提供丰富的通信。</span><span class="sxs-lookup"><span data-stu-id="71889-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="71889-107">自适应卡片框架适用于许多 Microsoft 产品，包括 Teams。</span><span class="sxs-lookup"><span data-stu-id="71889-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="71889-108">可以通过机器人或消息扩展向用户发送内部邮件卡片。</span><span class="sxs-lookup"><span data-stu-id="71889-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="71889-109">存在此情况时，用户可以对卡片采取操作。</span><span class="sxs-lookup"><span data-stu-id="71889-109">Users can take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="示例显示自适应卡片。" border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="71889-111">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="71889-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="71889-112">可以在 Microsoft Teams UI 工具包中查找有关 Teams 中自适应卡片的更全面的设计指南，包括可根据需要获取和修改的元素。</span><span class="sxs-lookup"><span data-stu-id="71889-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="71889-113">UI 工具包还涵盖了主题设置、辅助功能和响应式大小调整等重要主题。</span><span class="sxs-lookup"><span data-stu-id="71889-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="71889-114">获取 Microsoft Teams UI Kit （用户）</span><span class="sxs-lookup"><span data-stu-id="71889-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="71889-115">自适应卡片设计器</span><span class="sxs-lookup"><span data-stu-id="71889-115">Adaptive Cards designer</span></span>

<span data-ttu-id="71889-116">还可以直接在浏览器中开始设计自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="71889-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="71889-117">试用自适应卡片设计器</span><span class="sxs-lookup"><span data-stu-id="71889-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="71889-118">自适应卡片的类型</span><span class="sxs-lookup"><span data-stu-id="71889-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="71889-119">主图</span><span class="sxs-lookup"><span data-stu-id="71889-119">Hero</span></span>

<span data-ttu-id="71889-120">我们最大的卡片。</span><span class="sxs-lookup"><span data-stu-id="71889-120">Our largest card.</span></span> <span data-ttu-id="71889-121">用于共享文章或场景，其中图像可以描述大部分情景。</span><span class="sxs-lookup"><span data-stu-id="71889-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="示例显示自适应卡片。" border="false":::

### <a name="thumbnail"></a><span data-ttu-id="71889-123">缩略图</span><span class="sxs-lookup"><span data-stu-id="71889-123">Thumbnail</span></span>

<span data-ttu-id="71889-124">用于发送简单的可操作邮件。</span><span class="sxs-lookup"><span data-stu-id="71889-124">Use for sending a simple actionable message.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="自适应卡片的示例。" border="false":::

### <a name="list"></a><span data-ttu-id="71889-126">列表</span><span class="sxs-lookup"><span data-stu-id="71889-126">List</span></span>

<span data-ttu-id="71889-127">在您希望用户从列表中选取项目，但项目不需要太多解释的情况下使用。</span><span class="sxs-lookup"><span data-stu-id="71889-127">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="自适应卡片示例。" border="false":::

### <a name="digest"></a><span data-ttu-id="71889-129">Digest</span><span class="sxs-lookup"><span data-stu-id="71889-129">Digest</span></span>

<span data-ttu-id="71889-130">用于新闻摘要和向上舍入帖子。</span><span class="sxs-lookup"><span data-stu-id="71889-130">Use for news digests and round-up posts.</span></span> <span data-ttu-id="71889-131">注意：我们建议使用单个更新或新闻项的缩略图卡片。</span><span class="sxs-lookup"><span data-stu-id="71889-131">Note: We recommend the thumbnail card for a single update or news item.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="插图显示自适应卡片。" border="false":::

### <a name="media"></a><span data-ttu-id="71889-133">媒体</span><span class="sxs-lookup"><span data-stu-id="71889-133">Media</span></span>

<span data-ttu-id="71889-134">在你想要组合文本和媒体（如音频或视频）时使用。</span><span class="sxs-lookup"><span data-stu-id="71889-134">Use when you want to combine text and media, like audio or video.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="插图显示自适应卡片。" border="false":::

### <a name="people"></a><span data-ttu-id="71889-136">人员</span><span class="sxs-lookup"><span data-stu-id="71889-136">People</span></span>

<span data-ttu-id="71889-137">最适用于有效传达任务涉及人员。</span><span class="sxs-lookup"><span data-stu-id="71889-137">Best used when you to efficiently convey who's involved with a task.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="自适应卡片的图示。" border="false":::

### <a name="request-ticket"></a><span data-ttu-id="71889-139">请求票证</span><span class="sxs-lookup"><span data-stu-id="71889-139">Request ticket</span></span>

<span data-ttu-id="71889-140">用于从用户处获取快速输入，以自动创建任务或票证。</span><span class="sxs-lookup"><span data-stu-id="71889-140">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="自适应卡片的图示。" border="false":::

### <a name="imageset"></a><span data-ttu-id="71889-142">ImageSet</span><span class="sxs-lookup"><span data-stu-id="71889-142">ImageSet</span></span>

<span data-ttu-id="71889-143">用于发送多个图像缩略图。</span><span class="sxs-lookup"><span data-stu-id="71889-143">Use to send multiple image thumbnails.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="自适应卡片示例。" border="false":::

### <a name="actionset"></a><span data-ttu-id="71889-145">ActionSet</span><span class="sxs-lookup"><span data-stu-id="71889-145">ActionSet</span></span>

<span data-ttu-id="71889-146">当你希望用户选择一个按钮，然后从同一卡片收集添加的用户输入时，使用 。</span><span class="sxs-lookup"><span data-stu-id="71889-146">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="示例显示自适应卡片。" border="false":::

### <a name="choiceset"></a><span data-ttu-id="71889-148">ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="71889-148">ChoiceSet</span></span>

<span data-ttu-id="71889-149">用于收集用户的多个输入。</span><span class="sxs-lookup"><span data-stu-id="71889-149">Use to gather multiple inputs from the user.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="示例显示自适应卡片。" border="false":::

## <a name="anatomy"></a><span data-ttu-id="71889-151">解剖</span><span class="sxs-lookup"><span data-stu-id="71889-151">Anatomy</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="显示自适应卡片的 UI 分析的图示。" border="false":::

<span data-ttu-id="71889-153">自适应卡片具有很多灵活性。</span><span class="sxs-lookup"><span data-stu-id="71889-153">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="71889-154">但是，我们强烈建议至少将以下组件包括在每张卡片中：</span><span class="sxs-lookup"><span data-stu-id="71889-154">But at minimum, we strongly suggest including the following components in every card:</span></span>

|<span data-ttu-id="71889-155">计数器</span><span class="sxs-lookup"><span data-stu-id="71889-155">Counter</span></span>|<span data-ttu-id="71889-156">说明</span><span class="sxs-lookup"><span data-stu-id="71889-156">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="71889-157">A</span><span class="sxs-lookup"><span data-stu-id="71889-157">A</span></span>|<span data-ttu-id="71889-158">**标头**：使标题简洁明了，但具有描述性。</span><span class="sxs-lookup"><span data-stu-id="71889-158">**Header**: Make headers clear and concise, yet descriptive.</span></span>|
|<span data-ttu-id="71889-159">B</span><span class="sxs-lookup"><span data-stu-id="71889-159">B</span></span>|<span data-ttu-id="71889-160">**正文** 副本：用于传达太长或不够重要以包括在标头中的详细信息。</span><span class="sxs-lookup"><span data-stu-id="71889-160">**Body copy**: Use to convey detail that is either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="71889-161">C</span><span class="sxs-lookup"><span data-stu-id="71889-161">C</span></span>|<span data-ttu-id="71889-162">**主要操作**：最佳做法包括 1-3 个主要操作。</span><span class="sxs-lookup"><span data-stu-id="71889-162">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="71889-163">最多允许六个。</span><span class="sxs-lookup"><span data-stu-id="71889-163">A maximum of six are allowed.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="71889-164">最佳做法</span><span class="sxs-lookup"><span data-stu-id="71889-164">Best practices</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="71889-165">主要操作和辅助操作</span><span class="sxs-lookup"><span data-stu-id="71889-165">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="显示自适应卡片最佳实践的示例。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="71889-167">操作：最多使用六个主要操作</span><span class="sxs-lookup"><span data-stu-id="71889-167">Do: Use up to six primary actions</span></span>

<span data-ttu-id="71889-168">自适应卡片可以支持六个主要操作，但大多数卡片不需要这一点。</span><span class="sxs-lookup"><span data-stu-id="71889-168">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="71889-169">操作应简洁明了。</span><span class="sxs-lookup"><span data-stu-id="71889-169">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="71889-170">"少"表示"更多"。</span><span class="sxs-lookup"><span data-stu-id="71889-170">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="示例展示了自适应卡片最佳实践。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="71889-172">请勿：使用超过 6 个主要操作</span><span class="sxs-lookup"><span data-stu-id="71889-172">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="71889-173">自适应卡片应显示快速且可操作的内容。</span><span class="sxs-lookup"><span data-stu-id="71889-173">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="71889-174">操作太多可能会使用户感到不知所措。</span><span class="sxs-lookup"><span data-stu-id="71889-174">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="71889-175">频率</span><span class="sxs-lookup"><span data-stu-id="71889-175">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="显示自适应卡片最佳实践的图示。" border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="71889-177">应做：简洁</span><span class="sxs-lookup"><span data-stu-id="71889-177">Do: Be concise</span></span>

<span data-ttu-id="71889-178">向对话中发送多个卡片很容易，但在卡片滚动到视图外后，它们变得不太有用。</span><span class="sxs-lookup"><span data-stu-id="71889-178">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="71889-179">尝试将自己限制为基本功能。</span><span class="sxs-lookup"><span data-stu-id="71889-179">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="71889-180">在用户对"噪音"所感知的容忍度较低的频道中尤其如此。</span><span class="sxs-lookup"><span data-stu-id="71889-180">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>
