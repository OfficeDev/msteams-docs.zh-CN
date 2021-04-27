---
title: 自动程序消息格式
description: 介绍自动程序消息格式的详细信息
keywords: teams 方案频道对话机器人消息
ms.topic: reference
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: 06037bd3fb23ace11eea763747dc64d763ac3c42
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020644"
---
# <a name="message-formatting-for-bots"></a><span data-ttu-id="c01ee-104">自动程序的邮件格式</span><span class="sxs-lookup"><span data-stu-id="c01ee-104">Message formatting for bots</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="c01ee-105">可以设置可选 [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) 属性来控制邮件文本内容的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="c01ee-105">You can set the optional [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) property to control how your message's text content is rendered.</span></span>

<span data-ttu-id="c01ee-106">Microsoft Teams 支持以下格式选项：</span><span class="sxs-lookup"><span data-stu-id="c01ee-106">Microsoft Teams supports the following formatting options:</span></span>

| <span data-ttu-id="c01ee-107">TextFormat 值</span><span class="sxs-lookup"><span data-stu-id="c01ee-107">TextFormat value</span></span> | <span data-ttu-id="c01ee-108">说明</span><span class="sxs-lookup"><span data-stu-id="c01ee-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c01ee-109">plain</span><span class="sxs-lookup"><span data-stu-id="c01ee-109">plain</span></span> | <span data-ttu-id="c01ee-110">文本应视为原始文本，而未应用任何格式</span><span class="sxs-lookup"><span data-stu-id="c01ee-110">The text should be treated as raw text with no formatting applied at all</span></span> |
| <span data-ttu-id="c01ee-111">markdown</span><span class="sxs-lookup"><span data-stu-id="c01ee-111">markdown</span></span> | <span data-ttu-id="c01ee-112">文本应视为 Markdown 格式，并在适当时呈现在频道上;请参阅 [格式化支持样式](#formatting-text-content) 的文本内容</span><span class="sxs-lookup"><span data-stu-id="c01ee-112">The text should be treated as Markdown formatting and rendered on the channel as appropriate; see [Formatting text content](#formatting-text-content) for supported styles</span></span> |
| <span data-ttu-id="c01ee-113">xml</span><span class="sxs-lookup"><span data-stu-id="c01ee-113">xml</span></span> | <span data-ttu-id="c01ee-114">文本是简单的 XML 标记;请参阅 [格式化支持样式](#formatting-text-content) 的文本内容</span><span class="sxs-lookup"><span data-stu-id="c01ee-114">The text is simple XML markup; see [Formatting text content](#formatting-text-content) for supported styles</span></span> |

## <a name="formatting-text-content"></a><span data-ttu-id="c01ee-115">设置文本内容的格式</span><span class="sxs-lookup"><span data-stu-id="c01ee-115">Formatting text content</span></span>

<span data-ttu-id="c01ee-116">Microsoft Teams 支持 Markdown 和 XML 代码的一 (HTML) 格式标记。</span><span class="sxs-lookup"><span data-stu-id="c01ee-116">Microsoft Teams supports a subset of Markdown and XML (HTML) formatting tags.</span></span>

<span data-ttu-id="c01ee-117">目前，存在以下限制：</span><span class="sxs-lookup"><span data-stu-id="c01ee-117">Currently, the following limitations apply:</span></span>

* <span data-ttu-id="c01ee-118">纯文本邮件不支持表格式设置</span><span class="sxs-lookup"><span data-stu-id="c01ee-118">Text-only messages do not support table formatting</span></span>
* <span data-ttu-id="c01ee-119">格式卡片仅支持文本属性中的格式设置，不支持标题或副标题属性中的格式设置</span><span class="sxs-lookup"><span data-stu-id="c01ee-119">Rich cards support formatting in the text property only, not in the title or subtitle properties</span></span>
* <span data-ttu-id="c01ee-120">富卡不支持 Markdown 或表格格式</span><span class="sxs-lookup"><span data-stu-id="c01ee-120">Rich cards do not support Markdown or table formatting</span></span>

## <a name="cross-platform-support"></a><span data-ttu-id="c01ee-121">跨平台支持</span><span class="sxs-lookup"><span data-stu-id="c01ee-121">Cross-platform support</span></span>

<span data-ttu-id="c01ee-122">若要确保你的格式可以在 Microsoft Teams 支持的所有平台上运行，请注意某些样式当前并非在所有平台上都受支持。</span><span class="sxs-lookup"><span data-stu-id="c01ee-122">To ensure that your formatting works across all platforms supported by Microsoft Teams, be aware that some styles are not currently supported across all platforms.</span></span>

| <span data-ttu-id="c01ee-123">样式</span><span class="sxs-lookup"><span data-stu-id="c01ee-123">Style</span></span>                     | <span data-ttu-id="c01ee-124">纯文本邮件</span><span class="sxs-lookup"><span data-stu-id="c01ee-124">Text-only messages</span></span> | <span data-ttu-id="c01ee-125">富卡 (XML) </span><span class="sxs-lookup"><span data-stu-id="c01ee-125">Rich cards (XML only)</span></span> |
| ---                       | :---: | :---: |
| <span data-ttu-id="c01ee-126">bold</span><span class="sxs-lookup"><span data-stu-id="c01ee-126">bold</span></span>                      | <span data-ttu-id="c01ee-127">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-127">✔</span></span> | <span data-ttu-id="c01ee-128">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-128">✖</span></span> |
| <span data-ttu-id="c01ee-129">italic</span><span class="sxs-lookup"><span data-stu-id="c01ee-129">italic</span></span>                    | <span data-ttu-id="c01ee-130">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-130">✔</span></span> | <span data-ttu-id="c01ee-131">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-131">✔</span></span> |
| <span data-ttu-id="c01ee-132">页眉 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="c01ee-132">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="c01ee-133">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-133">✖</span></span> | <span data-ttu-id="c01ee-134">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-134">✔</span></span> |
| <span data-ttu-id="c01ee-135">strikethrough</span><span class="sxs-lookup"><span data-stu-id="c01ee-135">strikethrough</span></span>             | <span data-ttu-id="c01ee-136">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-136">✖</span></span> | <span data-ttu-id="c01ee-137">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-137">✔</span></span> |
| <span data-ttu-id="c01ee-138">水平规则</span><span class="sxs-lookup"><span data-stu-id="c01ee-138">horizontal rule</span></span>           | <span data-ttu-id="c01ee-139">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-139">✖</span></span> | <span data-ttu-id="c01ee-140">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-140">✖</span></span> |
| <span data-ttu-id="c01ee-141">无序列表</span><span class="sxs-lookup"><span data-stu-id="c01ee-141">unordered list</span></span>            | <span data-ttu-id="c01ee-142">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-142">✖</span></span> | <span data-ttu-id="c01ee-143">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-143">✔</span></span> |
| <span data-ttu-id="c01ee-144">排序列表</span><span class="sxs-lookup"><span data-stu-id="c01ee-144">ordered list</span></span>              | <span data-ttu-id="c01ee-145">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-145">✖</span></span> | <span data-ttu-id="c01ee-146">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-146">✔</span></span> |
| <span data-ttu-id="c01ee-147">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="c01ee-147">preformatted text</span></span>         | <span data-ttu-id="c01ee-148">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-148">✔</span></span> | <span data-ttu-id="c01ee-149">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-149">✔</span></span> |
| <span data-ttu-id="c01ee-150">blockquote</span><span class="sxs-lookup"><span data-stu-id="c01ee-150">blockquote</span></span>                | <span data-ttu-id="c01ee-151">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-151">✔</span></span> | <span data-ttu-id="c01ee-152">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-152">✔</span></span> |
| <span data-ttu-id="c01ee-153">超链接</span><span class="sxs-lookup"><span data-stu-id="c01ee-153">hyperlink</span></span>                 | <span data-ttu-id="c01ee-154">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-154">✔</span></span> | <span data-ttu-id="c01ee-155">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-155">✔</span></span> |
| <span data-ttu-id="c01ee-156">图像链接</span><span class="sxs-lookup"><span data-stu-id="c01ee-156">image link</span></span>                | <span data-ttu-id="c01ee-157">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-157">✔</span></span> | <span data-ttu-id="c01ee-158">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-158">✖</span></span> |

## <a name="support-by-individual-platform"></a><span data-ttu-id="c01ee-159">单个平台支持</span><span class="sxs-lookup"><span data-stu-id="c01ee-159">Support by individual platform</span></span>

<span data-ttu-id="c01ee-160">对文本格式的支持因邮件类型和平台而异。</span><span class="sxs-lookup"><span data-stu-id="c01ee-160">Support for text formatting varies by type of message and by platform.</span></span>

### <a name="text-only-messages"></a><span data-ttu-id="c01ee-161">纯文本邮件</span><span class="sxs-lookup"><span data-stu-id="c01ee-161">Text-only messages</span></span>

| <span data-ttu-id="c01ee-162">样式</span><span class="sxs-lookup"><span data-stu-id="c01ee-162">Style</span></span>                     | <span data-ttu-id="c01ee-163">桌面</span><span class="sxs-lookup"><span data-stu-id="c01ee-163">Desktop</span></span> | <span data-ttu-id="c01ee-164">iOS</span><span class="sxs-lookup"><span data-stu-id="c01ee-164">iOS</span></span> | <span data-ttu-id="c01ee-165">Android</span><span class="sxs-lookup"><span data-stu-id="c01ee-165">Android</span></span> |
| ---                       | :---: | :---: | :---: |
| <span data-ttu-id="c01ee-166">bold</span><span class="sxs-lookup"><span data-stu-id="c01ee-166">bold</span></span>                      | <span data-ttu-id="c01ee-167">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-167">✔</span></span> | <span data-ttu-id="c01ee-168">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-168">✔</span></span> | <span data-ttu-id="c01ee-169">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-169">✔</span></span> |
| <span data-ttu-id="c01ee-170">italic</span><span class="sxs-lookup"><span data-stu-id="c01ee-170">italic</span></span>                    | <span data-ttu-id="c01ee-171">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-171">✔</span></span> | <span data-ttu-id="c01ee-172">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-172">✔</span></span> | <span data-ttu-id="c01ee-173">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-173">✔</span></span> |
| <span data-ttu-id="c01ee-174">页眉 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="c01ee-174">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="c01ee-175">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-175">✖</span></span> | <span data-ttu-id="c01ee-176">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-176">✖</span></span> | <span data-ttu-id="c01ee-177">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-177">✖</span></span> |
| <span data-ttu-id="c01ee-178">strikethrough</span><span class="sxs-lookup"><span data-stu-id="c01ee-178">strikethrough</span></span>             | <span data-ttu-id="c01ee-179">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-179">✔</span></span> | <span data-ttu-id="c01ee-180">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-180">✔</span></span> | <span data-ttu-id="c01ee-181">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-181">✖</span></span> |
| <span data-ttu-id="c01ee-182">水平规则</span><span class="sxs-lookup"><span data-stu-id="c01ee-182">horizontal rule</span></span>           | <span data-ttu-id="c01ee-183">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-183">✖</span></span> | <span data-ttu-id="c01ee-184">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-184">✖</span></span> | <span data-ttu-id="c01ee-185">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-185">✖</span></span> |
| <span data-ttu-id="c01ee-186">无序列表</span><span class="sxs-lookup"><span data-stu-id="c01ee-186">unordered list</span></span>            | <span data-ttu-id="c01ee-187">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-187">✔</span></span> | <span data-ttu-id="c01ee-188">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-188">✖</span></span> | <span data-ttu-id="c01ee-189">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-189">✖</span></span> |
| <span data-ttu-id="c01ee-190">排序列表</span><span class="sxs-lookup"><span data-stu-id="c01ee-190">ordered list</span></span>              | <span data-ttu-id="c01ee-191">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-191">✔</span></span> | <span data-ttu-id="c01ee-192">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-192">✖</span></span> | <span data-ttu-id="c01ee-193">✖</span><span class="sxs-lookup"><span data-stu-id="c01ee-193">✖</span></span> |
| <span data-ttu-id="c01ee-194">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="c01ee-194">preformatted text</span></span>         | <span data-ttu-id="c01ee-195">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-195">✔</span></span> | <span data-ttu-id="c01ee-196">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-196">✔</span></span> | <span data-ttu-id="c01ee-197">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-197">✔</span></span> |
| <span data-ttu-id="c01ee-198">blockquote</span><span class="sxs-lookup"><span data-stu-id="c01ee-198">blockquote</span></span>                | <span data-ttu-id="c01ee-199">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-199">✔</span></span> | <span data-ttu-id="c01ee-200">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-200">✔</span></span> | <span data-ttu-id="c01ee-201">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-201">✔</span></span> |
| <span data-ttu-id="c01ee-202">超链接</span><span class="sxs-lookup"><span data-stu-id="c01ee-202">hyperlink</span></span>                 | <span data-ttu-id="c01ee-203">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-203">✔</span></span> | <span data-ttu-id="c01ee-204">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-204">✔</span></span> | <span data-ttu-id="c01ee-205">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-205">✔</span></span> |
| <span data-ttu-id="c01ee-206">图像链接</span><span class="sxs-lookup"><span data-stu-id="c01ee-206">image link</span></span>                | <span data-ttu-id="c01ee-207">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-207">✔</span></span> | <span data-ttu-id="c01ee-208">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-208">✔</span></span> | <span data-ttu-id="c01ee-209">✔</span><span class="sxs-lookup"><span data-stu-id="c01ee-209">✔</span></span> |

### <a name="cards"></a><span data-ttu-id="c01ee-210">卡</span><span class="sxs-lookup"><span data-stu-id="c01ee-210">Cards</span></span>

<span data-ttu-id="c01ee-211">有关 [卡片支持，](~/task-modules-and-cards/cards/cards-format.md) 请参阅卡片格式。</span><span class="sxs-lookup"><span data-stu-id="c01ee-211">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for support in cards.</span></span>
