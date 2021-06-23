---
title: 为你的应用设计自适应卡
description: 了解如何设计 Microsoft Teams 自适应卡并获取 Microsoft Teams UI Kit。
localization_priority: Priority
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8e56928da44e22006feb59715c8bdbf821ec4c42
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037654"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a><span data-ttu-id="0be81-103">为 Microsoft Teams 应用设计自适应卡</span><span class="sxs-lookup"><span data-stu-id="0be81-103">Designing Adaptive Cards for your Microsoft Teams app</span></span>

<span data-ttu-id="0be81-104">自适应卡片包含卡片元素的自由格式正文和一系列可选操作。</span><span class="sxs-lookup"><span data-stu-id="0be81-104">An Adaptive Card contains a freeform body of card elements and optional set of actions.</span></span> <span data-ttu-id="0be81-105">自适应卡片是可操作的内容片段，可通过机器人或消息传递扩展添加到对话。</span><span class="sxs-lookup"><span data-stu-id="0be81-105">Adaptive Cards are actionable snippets of content that you can add to a conversation through a bot or messaging extension.</span></span> <span data-ttu-id="0be81-106">这些卡片使用文本、图形和按钮为受众提供丰富的通信体验。</span><span class="sxs-lookup"><span data-stu-id="0be81-106">Using text, graphics, and buttons, these cards provide rich communication to your audience.</span></span>

<span data-ttu-id="0be81-107">自适应卡框架用于许多 Microsoft 产品，包括 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="0be81-107">The Adaptive Card framework is used across many Microsoft products, including Teams.</span></span> <span data-ttu-id="0be81-108">可以通过机器人或消息传递扩展向用户发送消息内的卡片。</span><span class="sxs-lookup"><span data-stu-id="0be81-108">You can send cards inside messages to users via bots or messaging extensions.</span></span> <span data-ttu-id="0be81-109">用户还可以在卡片上执行操作（如果存在）。</span><span class="sxs-lookup"><span data-stu-id="0be81-109">Users can also take actions on cards when present.</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="自适应卡概述示例。" border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="0be81-111">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="0be81-111">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="0be81-112">可在 Microsoft Teams UI Kit 中查看更全面的 Microsoft Teams 自适应卡设计指南，包括可根据需要获取和修改的元素。</span><span class="sxs-lookup"><span data-stu-id="0be81-112">You can find more comprehensive design guidelines for Adaptive Cards in Teams, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="0be81-113">UI 配套伯还涵盖主题、辅助功能和响应式大小等重要主题。</span><span class="sxs-lookup"><span data-stu-id="0be81-113">The UI kit also covers essential topics such as theming, accessibility, and responsive sizing.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0be81-114">获取 Microsoft Teams UI Kit（用户）</span><span class="sxs-lookup"><span data-stu-id="0be81-114">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a><span data-ttu-id="0be81-115">自适应卡设计器</span><span class="sxs-lookup"><span data-stu-id="0be81-115">Adaptive Cards designer</span></span>

<span data-ttu-id="0be81-116">还可以直接在浏览器中开始设计自适应卡。</span><span class="sxs-lookup"><span data-stu-id="0be81-116">You also can start designing your Adaptive Cards directly in the browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0be81-117">适用自适应卡设计器</span><span class="sxs-lookup"><span data-stu-id="0be81-117">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a><span data-ttu-id="0be81-118">自适应卡类型</span><span class="sxs-lookup"><span data-stu-id="0be81-118">Types of Adaptive Cards</span></span>

### <a name="hero"></a><span data-ttu-id="0be81-119">主图</span><span class="sxs-lookup"><span data-stu-id="0be81-119">Hero</span></span>

<span data-ttu-id="0be81-120">我们最大的卡片。</span><span class="sxs-lookup"><span data-stu-id="0be81-120">Our largest card.</span></span> <span data-ttu-id="0be81-121">用于共享文章或应用场景，用一张图像讲述故事主体。</span><span class="sxs-lookup"><span data-stu-id="0be81-121">Use for sharing articles or scenarios where an image tells most of the story.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0be81-122">桌面设备</span><span class="sxs-lookup"><span data-stu-id="0be81-122">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="示例：自适应卡主图卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0be81-124">移动设备</span><span class="sxs-lookup"><span data-stu-id="0be81-124">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="示例：移动设备上的自适应卡主图卡。" border="false":::

---

### <a name="thumbnail"></a><span data-ttu-id="0be81-126">缩略图</span><span class="sxs-lookup"><span data-stu-id="0be81-126">Thumbnail</span></span>

<span data-ttu-id="0be81-127">用于发送简单的可操作消息。</span><span class="sxs-lookup"><span data-stu-id="0be81-127">Use for sending a simple actionable message.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0be81-128">桌面设备</span><span class="sxs-lookup"><span data-stu-id="0be81-128">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="示例：自适应卡缩略图卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0be81-130">移动设备</span><span class="sxs-lookup"><span data-stu-id="0be81-130">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="示例：移动设备上的自适应卡缩略图卡。" border="false":::

---

### <a name="list"></a><span data-ttu-id="0be81-132">列表</span><span class="sxs-lookup"><span data-stu-id="0be81-132">List</span></span>

<span data-ttu-id="0be81-133">当你希望用户从列表中选中一项，但项不需要大量解释时使用。</span><span class="sxs-lookup"><span data-stu-id="0be81-133">Use in scenarios where you want the user to pick an item from a list, but the items don’t need a lot of explanation.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0be81-134">桌面设备</span><span class="sxs-lookup"><span data-stu-id="0be81-134">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="示例：自适应卡列表卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0be81-136">移动设备</span><span class="sxs-lookup"><span data-stu-id="0be81-136">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="示例：移动设备上的自适应卡列表卡。" border="false":::

---
Use for news digests and round-up posts. Note: We recommend the thumbnail card for a single update or news item.
':::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Example shows an Adaptive Card digest card." border="false"::': null
':::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Example shows an Adaptive Card digest card on mobile." border="false"::': null
---

### <a name="media"></a><span data-ttu-id="0be81-138">媒体</span><span class="sxs-lookup"><span data-stu-id="0be81-138">Media</span></span>

<span data-ttu-id="0be81-139">在想要结合文本和媒体（如音频或视频）时使用。</span><span class="sxs-lookup"><span data-stu-id="0be81-139">Use when you want to combine text and media, like audio or video.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0be81-140">桌面设备</span><span class="sxs-lookup"><span data-stu-id="0be81-140">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="示例：自适应卡媒体卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0be81-142">移动设备</span><span class="sxs-lookup"><span data-stu-id="0be81-142">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="示例：移动设备上的自适应卡媒体卡。" border="false":::

---

### <a name="people"></a><span data-ttu-id="0be81-144">人员</span><span class="sxs-lookup"><span data-stu-id="0be81-144">People</span></span>

<span data-ttu-id="0be81-145">最适合用于有效传达任务相关人员。</span><span class="sxs-lookup"><span data-stu-id="0be81-145">Best used when you to efficiently convey who's involved with a task.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0be81-146">桌面设备</span><span class="sxs-lookup"><span data-stu-id="0be81-146">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="示例：自适应卡人员卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0be81-148">移动设备</span><span class="sxs-lookup"><span data-stu-id="0be81-148">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="示例：移动设备上的自适应卡人员卡。" border="false":::

---

### <a name="request-ticket"></a><span data-ttu-id="0be81-150">请求票证</span><span class="sxs-lookup"><span data-stu-id="0be81-150">Request ticket</span></span>

<span data-ttu-id="0be81-151">用于从用户获取快速输入以自动创建任务或票证。</span><span class="sxs-lookup"><span data-stu-id="0be81-151">Use to get quick inputs from a user to automatically create a task or ticket.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0be81-152">桌面设备</span><span class="sxs-lookup"><span data-stu-id="0be81-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="示例：自适应卡请求票证卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0be81-154">移动设备</span><span class="sxs-lookup"><span data-stu-id="0be81-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="示例：移动设备上的自适应卡请求票证卡。" border="false":::

---

### <a name="image-set"></a><span data-ttu-id="0be81-156">图像集</span><span class="sxs-lookup"><span data-stu-id="0be81-156">Image set</span></span>

<span data-ttu-id="0be81-157">用于发送多个图像缩略图。</span><span class="sxs-lookup"><span data-stu-id="0be81-157">Use to send multiple image thumbnails.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0be81-158">桌面设备</span><span class="sxs-lookup"><span data-stu-id="0be81-158">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="示例：自适应卡图像集卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0be81-160">移动设备</span><span class="sxs-lookup"><span data-stu-id="0be81-160">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="示例：移动设备上的自适应卡图像集卡。" border="false":::

---

### <a name="action-set"></a><span data-ttu-id="0be81-162">操作集</span><span class="sxs-lookup"><span data-stu-id="0be81-162">Action set</span></span>

<span data-ttu-id="0be81-163">当希望用户选择按钮，然后从同一张卡中收集添加用户输入时使用。</span><span class="sxs-lookup"><span data-stu-id="0be81-163">Use when you want to the user to select a button, then gather addition user input from the same card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0be81-164">桌面设备</span><span class="sxs-lookup"><span data-stu-id="0be81-164">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="示例：自适应卡操作集卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0be81-166">移动设备</span><span class="sxs-lookup"><span data-stu-id="0be81-166">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="示例：移动设备上的自适应卡操作集卡。" border="false":::

---

### <a name="choice-set"></a><span data-ttu-id="0be81-168">选择集</span><span class="sxs-lookup"><span data-stu-id="0be81-168">Choice set</span></span>

<span data-ttu-id="0be81-169">用于从一个用户收集多个输入。</span><span class="sxs-lookup"><span data-stu-id="0be81-169">Use to gather multiple inputs from the user.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0be81-170">桌面设备</span><span class="sxs-lookup"><span data-stu-id="0be81-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="示例：自适应卡选择集卡。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0be81-172">移动设备</span><span class="sxs-lookup"><span data-stu-id="0be81-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="示例：移动设备上的自适应卡选择集卡。" border="false":::

---

## <a name="anatomy"></a><span data-ttu-id="0be81-174">解剖</span><span class="sxs-lookup"><span data-stu-id="0be81-174">Anatomy</span></span>

<span data-ttu-id="0be81-175">自适应卡片具有极强的灵活性。</span><span class="sxs-lookup"><span data-stu-id="0be81-175">Adaptive Cards have a lot of flexibility.</span></span> <span data-ttu-id="0be81-176">但作为最低要求，我们强烈建议在每张卡片中包含以下组件。</span><span class="sxs-lookup"><span data-stu-id="0be81-176">But at minimum, we strongly suggest including the following components in every card.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0be81-177">桌面设备</span><span class="sxs-lookup"><span data-stu-id="0be81-177">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="示例：自适应卡片解剖。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0be81-179">移动设备</span><span class="sxs-lookup"><span data-stu-id="0be81-179">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="示例：移动设备上的自适应卡片解剖。" border="false":::

---

|<span data-ttu-id="0be81-181">计数器</span><span class="sxs-lookup"><span data-stu-id="0be81-181">Counter</span></span>|<span data-ttu-id="0be81-182">说明</span><span class="sxs-lookup"><span data-stu-id="0be81-182">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="0be81-183">A</span><span class="sxs-lookup"><span data-stu-id="0be81-183">A</span></span>|<span data-ttu-id="0be81-184">**标题**：让标题清晰简洁。</span><span class="sxs-lookup"><span data-stu-id="0be81-184">**Header**: Make your headers clear and concise.</span></span>|
|<span data-ttu-id="0be81-185">B</span><span class="sxs-lookup"><span data-stu-id="0be81-185">B</span></span>|<span data-ttu-id="0be81-186">**正文文案**：传达过长或不够重要，不足以放在标题中的内容。</span><span class="sxs-lookup"><span data-stu-id="0be81-186">**Body copy**: Convey details that are either too long or not important enough to include in the header.</span></span>|
|<span data-ttu-id="0be81-187">C</span><span class="sxs-lookup"><span data-stu-id="0be81-187">C</span></span>|<span data-ttu-id="0be81-188">**主要操作**：作为最佳做法，包括 1-3 个主要操作。</span><span class="sxs-lookup"><span data-stu-id="0be81-188">**Primary actions**: As a best practice, include 1-3 primary actions.</span></span> <span data-ttu-id="0be81-189">可最多有 6 个。</span><span class="sxs-lookup"><span data-stu-id="0be81-189">You can have up to six.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="0be81-190">最佳实践</span><span class="sxs-lookup"><span data-stu-id="0be81-190">Best practices</span></span>

<span data-ttu-id="0be81-191">使用上述建议打造优质应用体验。</span><span class="sxs-lookup"><span data-stu-id="0be81-191">Use these recommendations to create a quality app experience.</span></span>

### <a name="primary-and-secondary-actions"></a><span data-ttu-id="0be81-192">主要和次要操作</span><span class="sxs-lookup"><span data-stu-id="0be81-192">Primary and secondary actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="有关如何在自适应卡上仅包含一小组操作的最佳实践。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a><span data-ttu-id="0be81-194">建议：最多使用六个主要操作</span><span class="sxs-lookup"><span data-stu-id="0be81-194">Do: Use up to six primary actions</span></span>

<span data-ttu-id="0be81-195">虽然自适应卡可以支持六个主要操作，但大多数卡并不需要这么多。</span><span class="sxs-lookup"><span data-stu-id="0be81-195">While Adaptive Cards can support six primary actions, most cards don’t need that.</span></span> <span data-ttu-id="0be81-196">操作应做到清晰、简洁且直接。</span><span class="sxs-lookup"><span data-stu-id="0be81-196">Actions should be clear, concise, and straight forward.</span></span> <span data-ttu-id="0be81-197">操作越少，效率越高。</span><span class="sxs-lookup"><span data-stu-id="0be81-197">Less is more.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="有关如何避免在自适应卡上添加过多操作，而让用户感到不知所措的最佳实践。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a><span data-ttu-id="0be81-199">不建议：使用超过六个主要操作</span><span class="sxs-lookup"><span data-stu-id="0be81-199">Don't: Use more than six primary actions</span></span>

<span data-ttu-id="0be81-200">自适应卡应提供快速、可操作的内容。</span><span class="sxs-lookup"><span data-stu-id="0be81-200">Adaptive Cards should present quick, actionable content.</span></span> <span data-ttu-id="0be81-201">操作过多可能会使用户不知所措。</span><span class="sxs-lookup"><span data-stu-id="0be81-201">Too many actions can overwhelm a user.</span></span>

   :::column-end:::
:::row-end:::

### <a name="frequency"></a><span data-ttu-id="0be81-202">频率</span><span class="sxs-lookup"><span data-stu-id="0be81-202">Frequency</span></span>

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="有关自适应卡频率的最佳实践。" border="false":::

#### <a name="do-be-concise"></a><span data-ttu-id="0be81-204">建议：做到简洁</span><span class="sxs-lookup"><span data-stu-id="0be81-204">Do: Be concise</span></span>

<span data-ttu-id="0be81-205">将多个卡片发送到对话很容易，但一旦卡片滚动出视图，就会变得没那么有用。</span><span class="sxs-lookup"><span data-stu-id="0be81-205">It's easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="0be81-206">尝试限制自己只传达必要内容。</span><span class="sxs-lookup"><span data-stu-id="0be81-206">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="0be81-207">在用户对自己认为是“干扰”的内容，容忍度更低的频道中尤其应注意这一点。</span><span class="sxs-lookup"><span data-stu-id="0be81-207">This is especially true in a channel where users have less tolerance for what they perceive as "noise".</span></span>
