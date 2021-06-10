---
title: 为应用设计自适应卡片
description: 了解如何为用户设计自适应Teams并获取 Microsoft Teams UI 工具包。
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b4d5f43268c7bd5afecb56d26eb0d49ed6c9002b
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630263"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="e866d-103">为应用设计自适应Microsoft Teams卡片</span><span class="sxs-lookup"><span data-stu-id="e866d-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="e866d-104">自适应卡片包含卡片元素和可选操作集的免费格式正文。</span><span class="sxs-lookup"><span data-stu-id="e866d-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="e866d-105">自适应卡片是内容可操作的代码段，可以通过机器人或消息传递扩展添加到对话中。</span><span class="sxs-lookup"><span data-stu-id="e866d-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="e866d-106">这些卡片使用文本、图形和按钮，向受众提供丰富的通信。</span><span class="sxs-lookup"><span data-stu-id="e866d-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="e866d-107">自适应卡片框架适用于许多 Microsoft 产品，包括Teams。</span><span class="sxs-lookup"><span data-stu-id="e866d-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="e866d-108">可以通过机器人或消息扩展向用户发送内部邮件卡片。</span><span class="sxs-lookup"><span data-stu-id="e866d-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="e866d-109">用户还可以在卡片上操作（存在）。</span><span class="sxs-lookup"><span data-stu-id="e866d-109">Users can also take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="自适应卡片的概述示例。" border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="e866d-111">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="e866d-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="e866d-112">你可以找到适用于 Teams 中的自适应卡片的更全面的设计指南，包括可根据需要获取和修改的元素，Microsoft Teams UI 工具包。</span><span class="sxs-lookup"><span data-stu-id="e866d-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="e866d-113">UI 工具包还涵盖了主题设置、辅助功能和响应式大小调整等重要主题。</span><span class="sxs-lookup"><span data-stu-id="e866d-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e866d-114">获取 Microsoft Teams UI Kit （用户）</span><span class="sxs-lookup"><span data-stu-id="e866d-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="e866d-115">自适应卡片设计器</span><span class="sxs-lookup"><span data-stu-id="e866d-115">Adaptive Cards designer</span></span>

<span data-ttu-id="e866d-116">还可以直接在浏览器中开始设计自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="e866d-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e866d-117">试用自适应卡片设计器</span><span class="sxs-lookup"><span data-stu-id="e866d-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="e866d-118">自适应卡片的类型</span><span class="sxs-lookup"><span data-stu-id="e866d-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="e866d-119">主图</span><span class="sxs-lookup"><span data-stu-id="e866d-119">Hero</span></span>

<span data-ttu-id="e866d-120">我们最大的卡片。</span><span class="sxs-lookup"><span data-stu-id="e866d-120">Our largest card.</span></span> <span data-ttu-id="e866d-121">用于共享文章或场景，其中图像可以描述大部分情景。</span><span class="sxs-lookup"><span data-stu-id="e866d-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e866d-122">桌面</span><span class="sxs-lookup"><span data-stu-id="e866d-122">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="示例显示自适应卡片展示卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e866d-124">移动</span><span class="sxs-lookup"><span data-stu-id="e866d-124">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="示例显示移动设备上的自适应卡片展示卡。" border="false":::

---

### <a name="thumbnail"></a><span data-ttu-id="e866d-126">缩略图</span><span class="sxs-lookup"><span data-stu-id="e866d-126">Thumbnail</span></span>

<span data-ttu-id="e866d-127">用于发送简单的可操作邮件。</span><span class="sxs-lookup"><span data-stu-id="e866d-127">Use for sending a simple actionable message.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e866d-128">桌面</span><span class="sxs-lookup"><span data-stu-id="e866d-128">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="示例显示自适应卡片缩略图卡片。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e866d-130">移动</span><span class="sxs-lookup"><span data-stu-id="e866d-130">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="示例显示移动版自适应卡片缩略图卡片。" border="false":::

---

### <a name="list"></a><span data-ttu-id="e866d-132">列表</span><span class="sxs-lookup"><span data-stu-id="e866d-132">List</span></span>

<span data-ttu-id="e866d-133">在您希望用户从列表中选取项目，但项目不需要太多解释的情况下使用。</span><span class="sxs-lookup"><span data-stu-id="e866d-133">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e866d-134">桌面</span><span class="sxs-lookup"><span data-stu-id="e866d-134">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="示例显示自适应卡片列表卡片。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e866d-136">移动</span><span class="sxs-lookup"><span data-stu-id="e866d-136">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="示例显示移动设备上的自适应卡片列表卡。" border="false":::

---

### Digest

Use for news digests and round-up posts. Note: We recommend the thumbnail card for a single update or news item.

# [Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Example shows an Adaptive Card digest card." border="false":::

# [Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Example shows an Adaptive Card digest card on mobile." border="false":::

---

### <a name="media"></a><span data-ttu-id="e866d-138">媒体</span><span class="sxs-lookup"><span data-stu-id="e866d-138">Media</span></span>

<span data-ttu-id="e866d-139">在你想要组合文本和媒体（如音频或视频）时使用。</span><span class="sxs-lookup"><span data-stu-id="e866d-139">Use when you want to combine text and media, like audio or video.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e866d-140">桌面</span><span class="sxs-lookup"><span data-stu-id="e866d-140">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="示例显示自适应卡片媒体卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e866d-142">移动</span><span class="sxs-lookup"><span data-stu-id="e866d-142">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="示例显示移动设备上的自适应卡片媒体卡。" border="false":::

---

### <a name="people"></a><span data-ttu-id="e866d-144">人员</span><span class="sxs-lookup"><span data-stu-id="e866d-144">People</span></span>

<span data-ttu-id="e866d-145">最适用于有效传达任务涉及人员。</span><span class="sxs-lookup"><span data-stu-id="e866d-145">Best used when you to efficiently convey who's involved with a task.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e866d-146">桌面</span><span class="sxs-lookup"><span data-stu-id="e866d-146">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="示例显示自适应卡片人员卡片。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e866d-148">移动</span><span class="sxs-lookup"><span data-stu-id="e866d-148">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="示例显示移动设备上的自适应卡片人员卡片。" border="false":::

---

### <a name="request-ticket"></a><span data-ttu-id="e866d-150">请求票证</span><span class="sxs-lookup"><span data-stu-id="e866d-150">Request ticket</span></span>

<span data-ttu-id="e866d-151">用于从用户处获取快速输入，以自动创建任务或票证。</span><span class="sxs-lookup"><span data-stu-id="e866d-151">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e866d-152">桌面</span><span class="sxs-lookup"><span data-stu-id="e866d-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="示例显示自适应卡片请求票证卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e866d-154">移动</span><span class="sxs-lookup"><span data-stu-id="e866d-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="示例显示移动版自适应卡片请求票证卡。" border="false":::

---

### <a name="image-set"></a><span data-ttu-id="e866d-156">图像集</span><span class="sxs-lookup"><span data-stu-id="e866d-156">Image set</span></span>

<span data-ttu-id="e866d-157">用于发送多个图像缩略图。</span><span class="sxs-lookup"><span data-stu-id="e866d-157">Use to send multiple image thumbnails.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e866d-158">桌面</span><span class="sxs-lookup"><span data-stu-id="e866d-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="示例显示自适应卡片图像集卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e866d-160">移动</span><span class="sxs-lookup"><span data-stu-id="e866d-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="示例显示移动设备上的自适应卡片图像集卡。" border="false":::

---

### <a name="action-set"></a><span data-ttu-id="e866d-162">操作集</span><span class="sxs-lookup"><span data-stu-id="e866d-162">Action set</span></span>

<span data-ttu-id="e866d-163">当你希望用户选择一个按钮，然后从同一卡片收集添加的用户输入时，使用 。</span><span class="sxs-lookup"><span data-stu-id="e866d-163">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e866d-164">桌面</span><span class="sxs-lookup"><span data-stu-id="e866d-164">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="示例显示自适应卡片操作集卡片。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e866d-166">移动</span><span class="sxs-lookup"><span data-stu-id="e866d-166">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="示例显示移动设备上的自适应卡片操作集卡片。" border="false":::

---

### <a name="choice-set"></a><span data-ttu-id="e866d-168">选项集</span><span class="sxs-lookup"><span data-stu-id="e866d-168">Choice set</span></span>

<span data-ttu-id="e866d-169">用于收集用户的多个输入。</span><span class="sxs-lookup"><span data-stu-id="e866d-169">Use to gather multiple inputs from the user.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e866d-170">桌面</span><span class="sxs-lookup"><span data-stu-id="e866d-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="示例显示自适应卡片选择集卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e866d-172">移动</span><span class="sxs-lookup"><span data-stu-id="e866d-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="示例显示移动设备上的自适应卡片选择集卡。" border="false":::

---

## <a name="anatomy"></a><span data-ttu-id="e866d-174">解剖</span><span class="sxs-lookup"><span data-stu-id="e866d-174">Anatomy</span></span>

<span data-ttu-id="e866d-175">自适应卡片具有很多灵活性。</span><span class="sxs-lookup"><span data-stu-id="e866d-175">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="e866d-176">但是，我们强烈建议至少将以下组件包括在每张卡中。</span><span class="sxs-lookup"><span data-stu-id="e866d-176">But at minimum, we strongly suggest including the following components in every card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="e866d-177">桌面</span><span class="sxs-lookup"><span data-stu-id="e866d-177">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="EExample 显示自适应卡片分析。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="e866d-179">移动</span><span class="sxs-lookup"><span data-stu-id="e866d-179">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="示例演示移动版自适应卡片分析。" border="false":::

---

|<span data-ttu-id="e866d-181">计数器</span><span class="sxs-lookup"><span data-stu-id="e866d-181">Counter</span></span>|<span data-ttu-id="e866d-182">说明</span><span class="sxs-lookup"><span data-stu-id="e866d-182">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="e866d-183">A</span><span class="sxs-lookup"><span data-stu-id="e866d-183">A</span></span>|<span data-ttu-id="e866d-184">**标头**：使标题简洁明了。</span><span class="sxs-lookup"><span data-stu-id="e866d-184">**Header**: Make your headers clear and concise.</span></span>|
|<span data-ttu-id="e866d-185">B</span><span class="sxs-lookup"><span data-stu-id="e866d-185">B</span></span>|<span data-ttu-id="e866d-186">**正文副本**：传达太长或不够重要以包括在标头中的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e866d-186">**Body copy**: Convey details that are either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="e866d-187">C</span><span class="sxs-lookup"><span data-stu-id="e866d-187">C</span></span>|<span data-ttu-id="e866d-188">**主要操作**：最佳做法包括 1-3 个主要操作。</span><span class="sxs-lookup"><span data-stu-id="e866d-188">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="e866d-189">你最多可以拥有六个。</span><span class="sxs-lookup"><span data-stu-id="e866d-189">You can have up to six.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="e866d-190">最佳做法</span><span class="sxs-lookup"><span data-stu-id="e866d-190">Best practices</span></span>

<span data-ttu-id="e866d-191">使用这些建议创建高质量的应用体验。</span><span class="sxs-lookup"><span data-stu-id="e866d-191">Use these recommendations to create a quality app experience.</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="e866d-192">主要操作和辅助操作</span><span class="sxs-lookup"><span data-stu-id="e866d-192">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="有关如何在自适应卡片上仅包含一小组操作的最佳操作。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="e866d-194">操作：最多使用六个主要操作</span><span class="sxs-lookup"><span data-stu-id="e866d-194">Do: Use up to six primary actions</span></span>

<span data-ttu-id="e866d-195">自适应卡片可以支持六个主要操作，但大多数卡片不需要这一点。</span><span class="sxs-lookup"><span data-stu-id="e866d-195">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="e866d-196">操作应简洁明了。</span><span class="sxs-lookup"><span data-stu-id="e866d-196">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="e866d-197">"少"表示"更多"。</span><span class="sxs-lookup"><span data-stu-id="e866d-197">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="有关在自适应卡片上不使用户不知所措以及操作太多的最佳操作。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="e866d-199">请勿：使用超过 6 个主要操作</span><span class="sxs-lookup"><span data-stu-id="e866d-199">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="e866d-200">自适应卡片应显示快速且可操作的内容。</span><span class="sxs-lookup"><span data-stu-id="e866d-200">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="e866d-201">操作太多可能会使用户感到不知所措。</span><span class="sxs-lookup"><span data-stu-id="e866d-201">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="e866d-202">频率</span><span class="sxs-lookup"><span data-stu-id="e866d-202">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="自适应卡片频率的最佳实践。" border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="e866d-204">应做：简洁</span><span class="sxs-lookup"><span data-stu-id="e866d-204">Do: Be concise</span></span>

<span data-ttu-id="e866d-205">向对话中发送多个卡片很容易，但在卡片滚动到视图外后，它们变得不太有用。</span><span class="sxs-lookup"><span data-stu-id="e866d-205">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="e866d-206">尝试将自己限制为基本功能。</span><span class="sxs-lookup"><span data-stu-id="e866d-206">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="e866d-207">在用户对"噪音"所感知的容忍度较低的频道中尤其如此。</span><span class="sxs-lookup"><span data-stu-id="e866d-207">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>
