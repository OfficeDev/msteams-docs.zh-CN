---
title: 自动程序消息格式
description: 介绍自动程序消息格式的详细信息
keywords: teams 方案频道对话机器人消息
ms.topic: reference
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: a9566331b259ba77f6770ff6394e8a788769af5d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566472"
---
# <a name="message-formatting-for-bots"></a><span data-ttu-id="4b9a7-104">自动程序的邮件格式</span><span class="sxs-lookup"><span data-stu-id="4b9a7-104">Message formatting for bots</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="4b9a7-105">可以设置可选 [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) 属性来控制邮件文本内容的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="4b9a7-105">You can set the optional [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) property to control how your message's text content is rendered.</span></span>

<span data-ttu-id="4b9a7-106">Microsoft Teams支持以下格式选项：</span><span class="sxs-lookup"><span data-stu-id="4b9a7-106">Microsoft Teams supports the following formatting options:</span></span>

| <span data-ttu-id="4b9a7-107">TextFormat 值</span><span class="sxs-lookup"><span data-stu-id="4b9a7-107">TextFormat value</span></span> | <span data-ttu-id="4b9a7-108">描述</span><span class="sxs-lookup"><span data-stu-id="4b9a7-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b9a7-109">plain</span><span class="sxs-lookup"><span data-stu-id="4b9a7-109">plain</span></span> | <span data-ttu-id="4b9a7-110">文本应视为原始文本，而未应用任何格式。</span><span class="sxs-lookup"><span data-stu-id="4b9a7-110">The text should be treated as raw text with no formatting applied at all.</span></span> |
| <span data-ttu-id="4b9a7-111">markdown</span><span class="sxs-lookup"><span data-stu-id="4b9a7-111">markdown</span></span> | <span data-ttu-id="4b9a7-112">文本应视为 Markdown 格式，并在适当时呈现在频道上;请参阅 [格式化支持样式](#formatting-text-content) 的文本内容。</span><span class="sxs-lookup"><span data-stu-id="4b9a7-112">The text should be treated as Markdown formatting and rendered on the channel as appropriate; see [Formatting text content](#formatting-text-content) for supported styles.</span></span> |
| <span data-ttu-id="4b9a7-113">xml</span><span class="sxs-lookup"><span data-stu-id="4b9a7-113">xml</span></span> | <span data-ttu-id="4b9a7-114">文本是简单的 XML 标记;请参阅 [格式化支持样式](#formatting-text-content) 的文本内容。</span><span class="sxs-lookup"><span data-stu-id="4b9a7-114">The text is simple XML markup; see [Formatting text content](#formatting-text-content) for supported styles.</span></span> |

## <a name="formatting-text-content"></a><span data-ttu-id="4b9a7-115">设置文本内容的格式</span><span class="sxs-lookup"><span data-stu-id="4b9a7-115">Formatting text content</span></span>

<span data-ttu-id="4b9a7-116">Microsoft Teams一部分 Markdown 和 XML (HTML) 格式标记。</span><span class="sxs-lookup"><span data-stu-id="4b9a7-116">Microsoft Teams supports a subset of Markdown and XML (HTML) formatting tags.</span></span>

<span data-ttu-id="4b9a7-117">目前，存在以下限制：</span><span class="sxs-lookup"><span data-stu-id="4b9a7-117">Currently, the following limitations apply:</span></span>

* <span data-ttu-id="4b9a7-118">纯文本邮件不支持表格格式。</span><span class="sxs-lookup"><span data-stu-id="4b9a7-118">Text-only messages do not support table formatting.</span></span>
* <span data-ttu-id="4b9a7-119">格式卡片仅支持文本属性中的格式设置，不支持标题或副标题属性中的格式设置。</span><span class="sxs-lookup"><span data-stu-id="4b9a7-119">Rich cards support formatting in the text property only, not in the title or subtitle properties.</span></span>
* <span data-ttu-id="4b9a7-120">富卡片不支持 Markdown 或表格格式。</span><span class="sxs-lookup"><span data-stu-id="4b9a7-120">Rich cards do not support Markdown or table formatting.</span></span>

## <a name="cross-platform-support"></a><span data-ttu-id="4b9a7-121">跨平台支持</span><span class="sxs-lookup"><span data-stu-id="4b9a7-121">Cross-platform support</span></span>

<span data-ttu-id="4b9a7-122">为了确保格式设置在所有受 Microsoft Teams支持的平台中运行，请注意某些样式当前并非在所有平台上都受支持。</span><span class="sxs-lookup"><span data-stu-id="4b9a7-122">To ensure that your formatting works across all platforms supported by Microsoft Teams, be aware that some styles are not currently supported across all platforms.</span></span>

| <span data-ttu-id="4b9a7-123">样式</span><span class="sxs-lookup"><span data-stu-id="4b9a7-123">Style</span></span>                     | <span data-ttu-id="4b9a7-124">纯文本邮件</span><span class="sxs-lookup"><span data-stu-id="4b9a7-124">Text-only messages</span></span> | <span data-ttu-id="4b9a7-125">富卡 (XML) </span><span class="sxs-lookup"><span data-stu-id="4b9a7-125">Rich cards (XML only)</span></span> |
| ---                       | :---: | :---: |
| <span data-ttu-id="4b9a7-126">bold</span><span class="sxs-lookup"><span data-stu-id="4b9a7-126">bold</span></span>                      | <span data-ttu-id="4b9a7-127">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-127">✔</span></span> | <span data-ttu-id="4b9a7-128">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-128">✖</span></span> |
| <span data-ttu-id="4b9a7-129">italic</span><span class="sxs-lookup"><span data-stu-id="4b9a7-129">italic</span></span>                    | <span data-ttu-id="4b9a7-130">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-130">✔</span></span> | <span data-ttu-id="4b9a7-131">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-131">✔</span></span> |
| <span data-ttu-id="4b9a7-132">页眉 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="4b9a7-132">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="4b9a7-133">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-133">✖</span></span> | <span data-ttu-id="4b9a7-134">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-134">✔</span></span> |
| <span data-ttu-id="4b9a7-135">strikethrough</span><span class="sxs-lookup"><span data-stu-id="4b9a7-135">strikethrough</span></span>             | <span data-ttu-id="4b9a7-136">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-136">✖</span></span> | <span data-ttu-id="4b9a7-137">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-137">✔</span></span> |
| <span data-ttu-id="4b9a7-138">水平规则</span><span class="sxs-lookup"><span data-stu-id="4b9a7-138">horizontal rule</span></span>           | <span data-ttu-id="4b9a7-139">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-139">✖</span></span> | <span data-ttu-id="4b9a7-140">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-140">✖</span></span> |
| <span data-ttu-id="4b9a7-141">无序列表</span><span class="sxs-lookup"><span data-stu-id="4b9a7-141">unordered list</span></span>            | <span data-ttu-id="4b9a7-142">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-142">✖</span></span> | <span data-ttu-id="4b9a7-143">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-143">✔</span></span> |
| <span data-ttu-id="4b9a7-144">排序列表</span><span class="sxs-lookup"><span data-stu-id="4b9a7-144">ordered list</span></span>              | <span data-ttu-id="4b9a7-145">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-145">✖</span></span> | <span data-ttu-id="4b9a7-146">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-146">✔</span></span> |
| <span data-ttu-id="4b9a7-147">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="4b9a7-147">preformatted text</span></span>         | <span data-ttu-id="4b9a7-148">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-148">✔</span></span> | <span data-ttu-id="4b9a7-149">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-149">✔</span></span> |
| <span data-ttu-id="4b9a7-150">blockquote</span><span class="sxs-lookup"><span data-stu-id="4b9a7-150">blockquote</span></span>                | <span data-ttu-id="4b9a7-151">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-151">✔</span></span> | <span data-ttu-id="4b9a7-152">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-152">✔</span></span> |
| <span data-ttu-id="4b9a7-153">超链接</span><span class="sxs-lookup"><span data-stu-id="4b9a7-153">hyperlink</span></span>                 | <span data-ttu-id="4b9a7-154">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-154">✔</span></span> | <span data-ttu-id="4b9a7-155">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-155">✔</span></span> |
| <span data-ttu-id="4b9a7-156">图像链接</span><span class="sxs-lookup"><span data-stu-id="4b9a7-156">image link</span></span>                | <span data-ttu-id="4b9a7-157">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-157">✔</span></span> | <span data-ttu-id="4b9a7-158">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-158">✖</span></span> |

## <a name="support-by-individual-platform"></a><span data-ttu-id="4b9a7-159">单个平台支持</span><span class="sxs-lookup"><span data-stu-id="4b9a7-159">Support by individual platform</span></span>

<span data-ttu-id="4b9a7-160">对文本格式的支持因邮件类型和平台而异。</span><span class="sxs-lookup"><span data-stu-id="4b9a7-160">Support for text formatting varies by type of message and by platform.</span></span>

### <a name="text-only-messages"></a><span data-ttu-id="4b9a7-161">纯文本邮件</span><span class="sxs-lookup"><span data-stu-id="4b9a7-161">Text-only messages</span></span>

| <span data-ttu-id="4b9a7-162">样式</span><span class="sxs-lookup"><span data-stu-id="4b9a7-162">Style</span></span>                     | <span data-ttu-id="4b9a7-163">桌面</span><span class="sxs-lookup"><span data-stu-id="4b9a7-163">Desktop</span></span> | <span data-ttu-id="4b9a7-164">iOS</span><span class="sxs-lookup"><span data-stu-id="4b9a7-164">iOS</span></span> | <span data-ttu-id="4b9a7-165">Android</span><span class="sxs-lookup"><span data-stu-id="4b9a7-165">Android</span></span> |
| ---                       | :---: | :---: | :---: |
| <span data-ttu-id="4b9a7-166">bold</span><span class="sxs-lookup"><span data-stu-id="4b9a7-166">bold</span></span>                      | <span data-ttu-id="4b9a7-167">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-167">✔</span></span> | <span data-ttu-id="4b9a7-168">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-168">✔</span></span> | <span data-ttu-id="4b9a7-169">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-169">✔</span></span> |
| <span data-ttu-id="4b9a7-170">italic</span><span class="sxs-lookup"><span data-stu-id="4b9a7-170">italic</span></span>                    | <span data-ttu-id="4b9a7-171">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-171">✔</span></span> | <span data-ttu-id="4b9a7-172">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-172">✔</span></span> | <span data-ttu-id="4b9a7-173">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-173">✔</span></span> |
| <span data-ttu-id="4b9a7-174">页眉 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="4b9a7-174">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="4b9a7-175">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-175">✖</span></span> | <span data-ttu-id="4b9a7-176">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-176">✖</span></span> | <span data-ttu-id="4b9a7-177">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-177">✖</span></span> |
| <span data-ttu-id="4b9a7-178">strikethrough</span><span class="sxs-lookup"><span data-stu-id="4b9a7-178">strikethrough</span></span>             | <span data-ttu-id="4b9a7-179">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-179">✔</span></span> | <span data-ttu-id="4b9a7-180">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-180">✔</span></span> | <span data-ttu-id="4b9a7-181">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-181">✖</span></span> |
| <span data-ttu-id="4b9a7-182">水平规则</span><span class="sxs-lookup"><span data-stu-id="4b9a7-182">horizontal rule</span></span>           | <span data-ttu-id="4b9a7-183">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-183">✖</span></span> | <span data-ttu-id="4b9a7-184">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-184">✖</span></span> | <span data-ttu-id="4b9a7-185">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-185">✖</span></span> |
| <span data-ttu-id="4b9a7-186">无序列表</span><span class="sxs-lookup"><span data-stu-id="4b9a7-186">unordered list</span></span>            | <span data-ttu-id="4b9a7-187">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-187">✔</span></span> | <span data-ttu-id="4b9a7-188">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-188">✖</span></span> | <span data-ttu-id="4b9a7-189">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-189">✖</span></span> |
| <span data-ttu-id="4b9a7-190">排序列表</span><span class="sxs-lookup"><span data-stu-id="4b9a7-190">ordered list</span></span>              | <span data-ttu-id="4b9a7-191">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-191">✔</span></span> | <span data-ttu-id="4b9a7-192">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-192">✖</span></span> | <span data-ttu-id="4b9a7-193">✖</span><span class="sxs-lookup"><span data-stu-id="4b9a7-193">✖</span></span> |
| <span data-ttu-id="4b9a7-194">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="4b9a7-194">preformatted text</span></span>         | <span data-ttu-id="4b9a7-195">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-195">✔</span></span> | <span data-ttu-id="4b9a7-196">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-196">✔</span></span> | <span data-ttu-id="4b9a7-197">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-197">✔</span></span> |
| <span data-ttu-id="4b9a7-198">blockquote</span><span class="sxs-lookup"><span data-stu-id="4b9a7-198">blockquote</span></span>                | <span data-ttu-id="4b9a7-199">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-199">✔</span></span> | <span data-ttu-id="4b9a7-200">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-200">✔</span></span> | <span data-ttu-id="4b9a7-201">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-201">✔</span></span> |
| <span data-ttu-id="4b9a7-202">超链接</span><span class="sxs-lookup"><span data-stu-id="4b9a7-202">hyperlink</span></span>                 | <span data-ttu-id="4b9a7-203">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-203">✔</span></span> | <span data-ttu-id="4b9a7-204">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-204">✔</span></span> | <span data-ttu-id="4b9a7-205">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-205">✔</span></span> |
| <span data-ttu-id="4b9a7-206">图像链接</span><span class="sxs-lookup"><span data-stu-id="4b9a7-206">image link</span></span>                | <span data-ttu-id="4b9a7-207">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-207">✔</span></span> | <span data-ttu-id="4b9a7-208">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-208">✔</span></span> | <span data-ttu-id="4b9a7-209">✔</span><span class="sxs-lookup"><span data-stu-id="4b9a7-209">✔</span></span> |

### <a name="cards"></a><span data-ttu-id="4b9a7-210">卡</span><span class="sxs-lookup"><span data-stu-id="4b9a7-210">Cards</span></span>

<span data-ttu-id="4b9a7-211">有关详细信息，请参阅 [卡片格式，](~/task-modules-and-cards/cards/cards-format.md) 获取卡片支持。</span><span class="sxs-lookup"><span data-stu-id="4b9a7-211">For more information, see [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for support in cards.</span></span>
