---
title: 设计有效的卡片
description: 介绍创建卡片的设计准则
keywords: 团队设计准则参考框架卡适应性轻型
ms.openlocfilehash: 33ee0b59a3a5a1490d6e2106f8532094ed852598
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673436"
---
# <a name="designing-effective-cards"></a><span data-ttu-id="bc9b5-104">设计有效的卡片</span><span class="sxs-lookup"><span data-stu-id="bc9b5-104">Designing effective cards</span></span>

<span data-ttu-id="bc9b5-105">卡片是可通过 bot、连接器或应用添加到对话中的可操作内容片段。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-105">Cards are actionable snippets of content that you can add to a conversation through a bot, a connector, or app.</span></span> <span data-ttu-id="bc9b5-106">通过使用文本、图形和按钮，卡片可以与访问群体进行通信。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-106">Using text, graphics, and buttons, cards allow you to communicate with an audience.</span></span>

<span data-ttu-id="bc9b5-107">我们的卡片框架消除了设计全功能 UX 的负担。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-107">Our card framework eliminates the burden of designing a fully functional UX.</span></span> <span data-ttu-id="bc9b5-108">我们开发了几种标准卡类型，每种类型都适合于受支持的平台。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-108">We developed several standard card types and each one fits within our supported platforms.</span></span> <span data-ttu-id="bc9b5-109">这意味着完全负责布局，并且无需跨平台开发不同的卡迭代。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-109">This means layout is completely taken care of, and you won’t need to develop different card iterations across platforms.</span></span> <span data-ttu-id="bc9b5-110">相反，你可以将精力集中在你的内容上拨。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-110">Instead, you can focus on dialing in your content.</span></span>

---

## <a name="guidelines"></a><span data-ttu-id="bc9b5-111">准则</span><span class="sxs-lookup"><span data-stu-id="bc9b5-111">Guidelines</span></span>

<span data-ttu-id="bc9b5-112">可将卡片视为对用户问题或设置的响应。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-112">Think of a card as a response to a user question or a setting.</span></span> <span data-ttu-id="bc9b5-113">卡片可以响应直接问题（例如，"我有多少个打开的 bug？"）或一个条件（如 "每日上午9点发送我打开的 bug 的列表"）。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-113">A card can respond to a direct question (like, “How many open bugs do I have?”) or to a condition (like, “Send a list of my open bugs at 9 am every day”).</span></span>

> [!TIP]
> <span data-ttu-id="bc9b5-114">使用我们的标准卡类型之一意味着你将了解所有响应将在每个受支持的平台上进行良好呈现。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-114">Using one of our standard card types means you’ll already know that all your responses will render nicely across each supported platform.</span></span>

<span data-ttu-id="bc9b5-115">卡片可以包含以下任何元素：</span><span class="sxs-lookup"><span data-stu-id="bc9b5-115">A card could include any of the following elements:</span></span><br />

[!include[Card anatomy](~/includes/design/card-image-anatomy.html)]

1. <span data-ttu-id="bc9b5-116">**信封文本**：最适用于聊天消息。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-116">**Envelope text**: Best used for chat messages.</span></span> <span data-ttu-id="bc9b5-117">例如，如果你想让 bot 说： "我找到了我找到的内容了！"</span><span class="sxs-lookup"><span data-stu-id="bc9b5-117">For example, if you want a bot to say: “Here’s what I found!”</span></span> <span data-ttu-id="bc9b5-118">或 "用于您的1:00 新闻摘要的时间"，该邮件最好显示在信封文本中。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-118">or “Time for your 1:00 news digest”, that message is best displayed in envelope text.</span></span>

   <span data-ttu-id="bc9b5-119">信封文本是一种很好的方法来向服务中注入一些个性，只需记住保持相对简短。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-119">Envelope text is a great way to inject a little personality into your service—just remember to keep it relatively short.</span></span>

2. <span data-ttu-id="bc9b5-120">**标题**：您的标题将始终为卡片中的最大文本。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-120">**Title**: Your title will always be the largest text in your card.</span></span> <span data-ttu-id="bc9b5-121">它还充当 "挂钩"，因此请尽量缩短标题，使其易于浏览。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-121">It also serves as your “hook”, so try to keep the title short, memorable, and easy to scan.</span></span>

3. <span data-ttu-id="bc9b5-122">**副标题**：最适合用于特性、taglines 或辅助指令。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-122">**Subtitle**: Best used for attribution, taglines, or as a secondary directive.</span></span> <span data-ttu-id="bc9b5-123">此组件显示在标题的正下方。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-123">This component appears just below your title.</span></span>

4. <span data-ttu-id="bc9b5-124">**图像**：图像根据其容器进行缩放。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-124">**Image**: Images scale to fit their container.</span></span> <span data-ttu-id="bc9b5-125">这些英雄卡片的最大宽度为420px，缩略图的最大宽度为100px，列表视图仅允许在桌面模式下进行32。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-125">Hero cards have a max width of 420px, thumbnails have a max width of 100px, and list views only allow for 32px in desktop mode.</span></span>

5. <span data-ttu-id="bc9b5-126">**文本**：最适合用于卡片正文中的纯文本。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-126">**Text**: Best used for plain text in the body of your card.</span></span> <span data-ttu-id="bc9b5-127">您的最大长度取决于所选的卡片类型。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-127">Your max length depends on the card type you’ve selected.</span></span>

6. <span data-ttu-id="bc9b5-128">**按钮**：最适合用于打开网页、选项卡或其他聊天内容。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-128">**Buttons**: Best used to open web pages, tabs, or additional chat content.</span></span> <span data-ttu-id="bc9b5-129">确保将按钮文本保持简短和点。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-129">Make sure to keep your button text short and to the point.</span></span>

   <span data-ttu-id="bc9b5-130">每个卡片最多可以包含6个按钮，但我们建议在此处 "更小的" 理念。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-130">You can include up to 6 buttons per card, but we’d recommend following a ‘less is more’ philosophy here.</span></span>

7. <span data-ttu-id="bc9b5-131">**点击区域**：这是卡片的可单击区域。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-131">**Tap region**: This is the clickable region of your card.</span></span> <span data-ttu-id="bc9b5-132">大多数用户都希望自动单击图像，因此请尝试并手工创建文本，以便他们知道应该点击或单击的位置。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-132">Most users will want to click on images automatically, so try and craft your text so they know where they should tap or click.</span></span>

> [!TIP]
> <span data-ttu-id="bc9b5-133">无需在您创建的每个卡片中包含每个元素。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-133">There’s no need to include every element in each card you create.</span></span> <span data-ttu-id="bc9b5-134">让你的内容为你的元素做决定。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-134">Let your content dictate your elements.</span></span>

---

## <a name="types-of-cards"></a><span data-ttu-id="bc9b5-135">卡片类型</span><span class="sxs-lookup"><span data-stu-id="bc9b5-135">Types of cards</span></span>

### <a name="hero"></a><span data-ttu-id="bc9b5-136">主图</span><span class="sxs-lookup"><span data-stu-id="bc9b5-136">Hero</span></span>

<span data-ttu-id="bc9b5-137">我们最大的卡片。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-137">Our largest card.</span></span> <span data-ttu-id="bc9b5-138">最适合用于您的图像告诉大多数情景的文章、详细说明或场景。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-138">Best used for articles, long descriptions, or scenarios where your image is telling most of the story.</span></span>

[!include[Card anatomy](~/includes/design/card-image-hero.html)]

### <a name="thumbnail"></a><span data-ttu-id="bc9b5-139">缩略图</span><span class="sxs-lookup"><span data-stu-id="bc9b5-139">Thumbnail</span></span>

<span data-ttu-id="bc9b5-140">简单明了。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-140">Short and sweet.</span></span> <span data-ttu-id="bc9b5-141">这些卡片是简短答案的理想选择，或者，如果您希望一次返回几张卡片，以便用户可以从一组选项中进行选择。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-141">These cards are ideal for short answers, or if you want to return several cards at once so the user can choose from a bunch of options.</span></span> <span data-ttu-id="bc9b5-142">我们认为，这是一个很好的深度链接到另一个选项卡或 web 服务的方法。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-142">We think these are a great way to deep link to another tab or a web service.</span></span>

[!include[Card anatomy](~/includes/design/card-image-thumbnail.html)]

### <a name="sign-in"></a><span data-ttu-id="bc9b5-143">登录</span><span class="sxs-lookup"><span data-stu-id="bc9b5-143">Sign in</span></span>

<span data-ttu-id="bc9b5-144">某些服务要求用户独立于我们的身份验证进行登录。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-144">Some services require users to sign in independently of our authentication.</span></span> <span data-ttu-id="bc9b5-145">在这种情况下，您将在用户可以连接到您的服务之前提供一个登录卡。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-145">In that event, you would present a sign-in card before the user can connect to your service.</span></span>

[!include[Card anatomy](~/includes/design/card-image-signin.html)]

> [!TIP]
> <span data-ttu-id="bc9b5-146">限制其他登录卡的出现次数，因为它们会给新用户带来明显的速度增加。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-146">Limit the occurrences of an additional sign-in card since they pose a significant speed bump for new users.</span></span>

---

## <a name="card-collections"></a><span data-ttu-id="bc9b5-147">卡片集合</span><span class="sxs-lookup"><span data-stu-id="bc9b5-147">Card collections</span></span>

<span data-ttu-id="bc9b5-148">当您希望一次显示多个内容或以快速连续显示多个内容时，我们还提供了最适合使用的标准卡片类型。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-148">We also have standard card types that are best used when you want to present several pieces of content at once or in quick succession.</span></span> <span data-ttu-id="bc9b5-149">为此，我们提供了一个轮播、摘要、列表以及我们称之为 "气泡合并" 的内容。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-149">For that purpose, we have a carousel, a digest, a list, and what we call a ‘bubble merge’.</span></span>

### <a name="carousel"></a><span data-ttu-id="bc9b5-150">旋转式传送</span><span class="sxs-lookup"><span data-stu-id="bc9b5-150">Carousel</span></span>

<span data-ttu-id="bc9b5-151">最适合用于文章、购物和通过卡片浏览。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-151">Best used for articles, shopping, and browsing through cards.</span></span>

[!include[Card anatomy](~/includes/design/card-image-carousel.html)]

> [!TIP]
> <span data-ttu-id="bc9b5-152">轮播将成为最大卡片的最大高度。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-152">The carousel will be the max height of your largest card.</span></span> <span data-ttu-id="bc9b5-153">我们建议在中使用相同的卡片类型和内容字段。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-153">We recommend using the same card type and content fields throughout.</span></span>

### <a name="digest"></a><span data-ttu-id="bc9b5-154">Digest</span><span class="sxs-lookup"><span data-stu-id="bc9b5-154">Digest</span></span>

<span data-ttu-id="bc9b5-155">最适合用于新闻、摘要以及您希望用户一次查看多张卡片的情况。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-155">Best used for news, digests, and whenever you want the user to view multiple cards at once.</span></span> <span data-ttu-id="bc9b5-156">建议使用摘要的缩略图卡片。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-156">We recommend using thumbnail cards for digests.</span></span>

[!include[Card anatomy](~/includes/design/card-image-digest.html)]

### <a name="lists"></a><span data-ttu-id="bc9b5-157">列表</span><span class="sxs-lookup"><span data-stu-id="bc9b5-157">Lists</span></span>

<span data-ttu-id="bc9b5-158">列表是在 "选择其中一个" 方案中呈现一组可浏览对象的绝佳方式。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-158">Lists are a great way to present a scannable set of objects in a “pick one of these” scenario.</span></span> <span data-ttu-id="bc9b5-159">最适用于不需要大量说明的项目的列表。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-159">Lists are best used for items that don’t need a lot of explanation.</span></span>

[!include[Card anatomy](~/includes/design/card-image-list.html)]

### <a name="bubble-merge"></a><span data-ttu-id="bc9b5-160">气泡合并</span><span class="sxs-lookup"><span data-stu-id="bc9b5-160">Bubble merge</span></span>

<span data-ttu-id="bc9b5-161">可通过快速连续发送一个英雄和几个缩略图来实现一些有趣的效果。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-161">Some interesting effects can be achieved by sending one hero and several thumbnails in quick succession.</span></span> <span data-ttu-id="bc9b5-162">当您希望为主结果提供服务但包含更多相关的项目时，建议采用这种方法。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-162">We recommend this approach when you want to serve a main result but include a few more related items.</span></span>

[!include[Card anatomy](~/includes/design/card-image-bubble-merge.html)]

---

## <a name="best-practices"></a><span data-ttu-id="bc9b5-163">最佳做法</span><span class="sxs-lookup"><span data-stu-id="bc9b5-163">Best practices</span></span>

### <a name="keep-the-noise-down"></a><span data-ttu-id="bc9b5-164">将噪音降低</span><span class="sxs-lookup"><span data-stu-id="bc9b5-164">Keep the noise down</span></span>

<span data-ttu-id="bc9b5-165">可以轻松地将多个卡片发送到对话中，但一旦卡片从视图中滚出，它们就会变得不太有用。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-165">It’s easy to send multiple cards into a conversation, but once cards scroll out of view, they become less useful.</span></span> <span data-ttu-id="bc9b5-166">尝试将自己限制为重点。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-166">Try to limit yourself to the essentials.</span></span> <span data-ttu-id="bc9b5-167">在用户对其感觉为 "干扰" 的程度较差的频道中，尤其如此。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-167">This is especially true in a channel where users have less tolerance for what they perceive as “noise”.</span></span>

### <a name="test-on-mobile"></a><span data-ttu-id="bc9b5-168">在移动设备上测试</span><span class="sxs-lookup"><span data-stu-id="bc9b5-168">Test on mobile</span></span>

<span data-ttu-id="bc9b5-169">移动环境具有空间和带宽限制，因此请注意在列表和 carousels 中包含过多的图像和大型数据集。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-169">Mobile environments are space- and bandwidth-constrained, so be cautious about including oversized images and large data sets in lists and carousels.</span></span> <span data-ttu-id="bc9b5-170">此外，标题宽度和文本长度将在移动时截断，因此，另一件事就是要保持关注。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-170">Also, title widths and text lengths will truncate on mobile, so that’s another thing to keep an eye on.</span></span>

### <a name="check-your-graphics"></a><span data-ttu-id="bc9b5-171">检查图形</span><span class="sxs-lookup"><span data-stu-id="bc9b5-171">Check your graphics</span></span>

<span data-ttu-id="bc9b5-172">将缩放图形，因此请务必在所有平台上进行预览。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-172">Graphics are going to scale, so be sure to preview them on all platforms.</span></span>

### <a name="avoid-including-text-in-a-graphic"></a><span data-ttu-id="bc9b5-173">避免在图形中包含文本</span><span class="sxs-lookup"><span data-stu-id="bc9b5-173">Avoid including text in a graphic</span></span>

<span data-ttu-id="bc9b5-174">用户需要阅读的任何内容都应包含在文本字段中。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-174">Anything that needs to be read by a user should be included in a text field.</span></span> <span data-ttu-id="bc9b5-175">动态缩放图像后，添加到图形中的任何文本都可能变得无法理解。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-175">Once an image is dynamically scaled, any text you add to a graphic may become unintelligible.</span></span>

### <a name="use-mentions-if-you-want-the-attention-of-specific-users"></a><span data-ttu-id="bc9b5-176">如果您希望特定用户注意，请使用提及</span><span class="sxs-lookup"><span data-stu-id="bc9b5-176">Use mentions if you want the attention of specific users</span></span>

> [!NOTE]
> <span data-ttu-id="bc9b5-177">在[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中，目前仅支持对卡片中提及支持。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-177">Mention support in cards is currently supported in [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="bc9b5-178">提及是在团队或群聊天中通知特定用户的一种极好的方法。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-178">Mentions are a great way to notify specific users in a Team or group chat.</span></span> <span data-ttu-id="bc9b5-179">您可以在类似、分配给用户的任务或向 teammate 提供荣誉的方案中包括提及的卡片。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-179">You can include a mention in card in scenarios like, a task thats assigned to a user or giving Kudos to a teammate.</span></span> <span data-ttu-id="bc9b5-180">了解如何在[卡片格式页](~/task-modules-and-cards/cards/cards-format.md)的卡片中添加提及。</span><span class="sxs-lookup"><span data-stu-id="bc9b5-180">Learn how to include mentions in cards in the [card formatting page](~/task-modules-and-cards/cards/cards-format.md).</span></span> 
