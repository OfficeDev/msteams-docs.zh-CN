---
title: 设置你的智能机器人邮件格式
author: surbhigupta
description: 向自动程序消息添加丰富的格式
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 56a34edee372cc6c5bcc5808015783f04867f141
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068984"
---
# <a name="format-your-bot-messages"></a><span data-ttu-id="8602d-103">设置你的智能机器人邮件格式</span><span class="sxs-lookup"><span data-stu-id="8602d-103">Format your bot messages</span></span>

<span data-ttu-id="8602d-104">邮件格式使您能够在自动程序消息中获得最佳效果。</span><span class="sxs-lookup"><span data-stu-id="8602d-104">Message formatting enables you to bring out the best in bot messages.</span></span> <span data-ttu-id="8602d-105">您可以设置自动程序消息的格式，以包含包含交互式元素（如按钮、文本、图像、音频、视频等）的附件的富卡片。</span><span class="sxs-lookup"><span data-stu-id="8602d-105">You can format your bot messages to include rich cards that are attachments that contain interactive elements, such as buttons, text, images, audio, video, and so on.</span></span>

## <a name="format-text-content"></a><span data-ttu-id="8602d-106">设置文本内容的格式</span><span class="sxs-lookup"><span data-stu-id="8602d-106">Format text content</span></span>

<span data-ttu-id="8602d-107">若要设置自动程序消息的格式，可以设置可选属性 [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) 以控制自动程序消息的文本内容的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="8602d-107">To format your bot messages, you can set the optional [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) property to control how your bot message's text content is rendered.</span></span>

<span data-ttu-id="8602d-108">Microsoft Teams支持以下格式选项：</span><span class="sxs-lookup"><span data-stu-id="8602d-108">Microsoft Teams supports the following formatting options:</span></span>

| <span data-ttu-id="8602d-109">`TextFormat` value</span><span class="sxs-lookup"><span data-stu-id="8602d-109">`TextFormat` value</span></span> | <span data-ttu-id="8602d-110">说明</span><span class="sxs-lookup"><span data-stu-id="8602d-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8602d-111">plain</span><span class="sxs-lookup"><span data-stu-id="8602d-111">plain</span></span> | <span data-ttu-id="8602d-112">必须将文本视为原始文本，不应用任何格式。</span><span class="sxs-lookup"><span data-stu-id="8602d-112">The text must be treated as raw text with no formatting applied.</span></span>|
| <span data-ttu-id="8602d-113">markdown</span><span class="sxs-lookup"><span data-stu-id="8602d-113">markdown</span></span> | <span data-ttu-id="8602d-114">文本必须视为 markdown 格式，并在适当时呈现在频道上。</span><span class="sxs-lookup"><span data-stu-id="8602d-114">The text must be treated as markdown formatting and rendered on the channel as appropriate.</span></span> |
| <span data-ttu-id="8602d-115">xml</span><span class="sxs-lookup"><span data-stu-id="8602d-115">xml</span></span> | <span data-ttu-id="8602d-116">文本是简单的 XML 标记。</span><span class="sxs-lookup"><span data-stu-id="8602d-116">The text is simple XML markup.</span></span> |

<span data-ttu-id="8602d-117">Teams markdown 和 XML 或 HTML 格式标记的子集。</span><span class="sxs-lookup"><span data-stu-id="8602d-117">Teams supports a subset of markdown and XML or HTML formatting tags.</span></span>

<span data-ttu-id="8602d-118">目前，以下限制适用于格式设置：</span><span class="sxs-lookup"><span data-stu-id="8602d-118">Currently, the following limitations apply to formatting:</span></span>

* <span data-ttu-id="8602d-119">纯文本邮件不支持表格格式。</span><span class="sxs-lookup"><span data-stu-id="8602d-119">Text-only messages do not support table formatting.</span></span>
* <span data-ttu-id="8602d-120">格式卡片仅支持文本属性中的格式设置，不支持标题或副标题属性中的格式设置。</span><span class="sxs-lookup"><span data-stu-id="8602d-120">Rich cards support formatting in the text property only, not in the title or subtitle properties.</span></span>
* <span data-ttu-id="8602d-121">富卡片不支持 markdown 或表格格式。</span><span class="sxs-lookup"><span data-stu-id="8602d-121">Rich cards do not support markdown or table formatting.</span></span>

<span data-ttu-id="8602d-122">设置文本内容格式后，请确保您的格式设置适用于所有受 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="8602d-122">After you format text content, ensure that your formatting works across all platforms supported by Microsoft Teams.</span></span>

## <a name="cross-platform-support"></a><span data-ttu-id="8602d-123">跨平台支持</span><span class="sxs-lookup"><span data-stu-id="8602d-123">Cross-platform support</span></span>

<span data-ttu-id="8602d-124">某些样式当前并非在所有平台上都受支持。</span><span class="sxs-lookup"><span data-stu-id="8602d-124">Some styles are currently not supported across all platforms.</span></span> <span data-ttu-id="8602d-125">下表提供了样式列表，以及纯文本消息和格式卡片支持哪些样式：</span><span class="sxs-lookup"><span data-stu-id="8602d-125">The following table provides a list of styles and which of these styles are supported in text-only messages and rich cards:</span></span>

| <span data-ttu-id="8602d-126">样式</span><span class="sxs-lookup"><span data-stu-id="8602d-126">Style</span></span>                     | <span data-ttu-id="8602d-127">纯文本邮件</span><span class="sxs-lookup"><span data-stu-id="8602d-127">Text-only messages</span></span> | <span data-ttu-id="8602d-128">富卡片 - 仅 XML</span><span class="sxs-lookup"><span data-stu-id="8602d-128">Rich cards - XML only</span></span> |
| ---                       | :---: | :---: |
| <span data-ttu-id="8602d-129">粗体</span><span class="sxs-lookup"><span data-stu-id="8602d-129">Bold</span></span>                      | <span data-ttu-id="8602d-130">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-130">✔</span></span> | <span data-ttu-id="8602d-131">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-131">✖</span></span> |
| <span data-ttu-id="8602d-132">斜体</span><span class="sxs-lookup"><span data-stu-id="8602d-132">Italic</span></span>                    | <span data-ttu-id="8602d-133">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-133">✔</span></span> | <span data-ttu-id="8602d-134">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-134">✔</span></span> |
| <span data-ttu-id="8602d-135">页眉 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="8602d-135">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="8602d-136">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-136">✖</span></span> | <span data-ttu-id="8602d-137">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-137">✔</span></span> |
| <span data-ttu-id="8602d-138">删除线</span><span class="sxs-lookup"><span data-stu-id="8602d-138">Strikethrough</span></span>             | <span data-ttu-id="8602d-139">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-139">✖</span></span> | <span data-ttu-id="8602d-140">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-140">✔</span></span> |
| <span data-ttu-id="8602d-141">水平规则</span><span class="sxs-lookup"><span data-stu-id="8602d-141">Horizontal rule</span></span>           | <span data-ttu-id="8602d-142">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-142">✖</span></span> | <span data-ttu-id="8602d-143">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-143">✖</span></span> |
| <span data-ttu-id="8602d-144">未排序列表</span><span class="sxs-lookup"><span data-stu-id="8602d-144">Unordered list</span></span>            | <span data-ttu-id="8602d-145">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-145">✖</span></span> | <span data-ttu-id="8602d-146">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-146">✔</span></span> |
| <span data-ttu-id="8602d-147">已排序列表</span><span class="sxs-lookup"><span data-stu-id="8602d-147">Ordered list</span></span>              | <span data-ttu-id="8602d-148">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-148">✖</span></span> | <span data-ttu-id="8602d-149">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-149">✔</span></span> |
| <span data-ttu-id="8602d-150">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="8602d-150">Preformatted text</span></span>         | <span data-ttu-id="8602d-151">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-151">✔</span></span> | <span data-ttu-id="8602d-152">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-152">✔</span></span> |
| <span data-ttu-id="8602d-153">Blockquote</span><span class="sxs-lookup"><span data-stu-id="8602d-153">Blockquote</span></span>                | <span data-ttu-id="8602d-154">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-154">✔</span></span> | <span data-ttu-id="8602d-155">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-155">✔</span></span> |
| <span data-ttu-id="8602d-156">超链接</span><span class="sxs-lookup"><span data-stu-id="8602d-156">Hyperlink</span></span>                 | <span data-ttu-id="8602d-157">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-157">✔</span></span> | <span data-ttu-id="8602d-158">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-158">✔</span></span> |
| <span data-ttu-id="8602d-159">图像链接</span><span class="sxs-lookup"><span data-stu-id="8602d-159">Image link</span></span>                | <span data-ttu-id="8602d-160">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-160">✔</span></span> | <span data-ttu-id="8602d-161">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-161">✖</span></span> |

<span data-ttu-id="8602d-162">检查跨平台支持后，请确保各个平台也提供支持。</span><span class="sxs-lookup"><span data-stu-id="8602d-162">After checking cross-platform support, ensure that support by individual platforms is also available.</span></span>

## <a name="support-by-individual-platform"></a><span data-ttu-id="8602d-163">单个平台支持</span><span class="sxs-lookup"><span data-stu-id="8602d-163">Support by individual platform</span></span>

<span data-ttu-id="8602d-164">对文本格式的支持因邮件类型和平台而异。</span><span class="sxs-lookup"><span data-stu-id="8602d-164">Support for text formatting varies by type of message and platform.</span></span>

### <a name="text-only-messages"></a><span data-ttu-id="8602d-165">纯文本邮件</span><span class="sxs-lookup"><span data-stu-id="8602d-165">Text-only messages</span></span>

<span data-ttu-id="8602d-166">下表提供了样式列表，以及哪些样式在桌面、iOS 和 Android 上受支持：</span><span class="sxs-lookup"><span data-stu-id="8602d-166">The following table provides a list of styles and which of these styles are supported on desktop, iOS, and Android:</span></span>

| <span data-ttu-id="8602d-167">样式</span><span class="sxs-lookup"><span data-stu-id="8602d-167">Style</span></span>                     | <span data-ttu-id="8602d-168">桌面</span><span class="sxs-lookup"><span data-stu-id="8602d-168">Desktop</span></span> | <span data-ttu-id="8602d-169">iOS</span><span class="sxs-lookup"><span data-stu-id="8602d-169">iOS</span></span> | <span data-ttu-id="8602d-170">Android</span><span class="sxs-lookup"><span data-stu-id="8602d-170">Android</span></span> |
| ---                       | :---: | :---: | :---: |
| <span data-ttu-id="8602d-171">粗体</span><span class="sxs-lookup"><span data-stu-id="8602d-171">Bold</span></span>                      | <span data-ttu-id="8602d-172">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-172">✔</span></span> | <span data-ttu-id="8602d-173">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-173">✔</span></span> | <span data-ttu-id="8602d-174">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-174">✔</span></span> |
| <span data-ttu-id="8602d-175">斜体</span><span class="sxs-lookup"><span data-stu-id="8602d-175">Italic</span></span>                    | <span data-ttu-id="8602d-176">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-176">✔</span></span> | <span data-ttu-id="8602d-177">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-177">✔</span></span> | <span data-ttu-id="8602d-178">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-178">✔</span></span> |
| <span data-ttu-id="8602d-179">页眉 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="8602d-179">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="8602d-180">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-180">✖</span></span> | <span data-ttu-id="8602d-181">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-181">✖</span></span> | <span data-ttu-id="8602d-182">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-182">✖</span></span> |
| <span data-ttu-id="8602d-183">删除线</span><span class="sxs-lookup"><span data-stu-id="8602d-183">Strikethrough</span></span>             | <span data-ttu-id="8602d-184">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-184">✔</span></span> | <span data-ttu-id="8602d-185">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-185">✔</span></span> | <span data-ttu-id="8602d-186">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-186">✖</span></span> |
| <span data-ttu-id="8602d-187">水平规则</span><span class="sxs-lookup"><span data-stu-id="8602d-187">Horizontal rule</span></span>           | <span data-ttu-id="8602d-188">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-188">✖</span></span> | <span data-ttu-id="8602d-189">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-189">✖</span></span> | <span data-ttu-id="8602d-190">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-190">✖</span></span> |
| <span data-ttu-id="8602d-191">未排序列表</span><span class="sxs-lookup"><span data-stu-id="8602d-191">Unordered list</span></span>            | <span data-ttu-id="8602d-192">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-192">✔</span></span> | <span data-ttu-id="8602d-193">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-193">✖</span></span> | <span data-ttu-id="8602d-194">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-194">✖</span></span> |
| <span data-ttu-id="8602d-195">已排序列表</span><span class="sxs-lookup"><span data-stu-id="8602d-195">Ordered list</span></span>              | <span data-ttu-id="8602d-196">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-196">✔</span></span> | <span data-ttu-id="8602d-197">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-197">✖</span></span> | <span data-ttu-id="8602d-198">✖</span><span class="sxs-lookup"><span data-stu-id="8602d-198">✖</span></span> |
| <span data-ttu-id="8602d-199">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="8602d-199">Preformatted text</span></span>         | <span data-ttu-id="8602d-200">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-200">✔</span></span> | <span data-ttu-id="8602d-201">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-201">✔</span></span> | <span data-ttu-id="8602d-202">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-202">✔</span></span> |
| <span data-ttu-id="8602d-203">Blockquote</span><span class="sxs-lookup"><span data-stu-id="8602d-203">Blockquote</span></span>                | <span data-ttu-id="8602d-204">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-204">✔</span></span> | <span data-ttu-id="8602d-205">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-205">✔</span></span> | <span data-ttu-id="8602d-206">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-206">✔</span></span> |
| <span data-ttu-id="8602d-207">超链接</span><span class="sxs-lookup"><span data-stu-id="8602d-207">Hyperlink</span></span>                 | <span data-ttu-id="8602d-208">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-208">✔</span></span> | <span data-ttu-id="8602d-209">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-209">✔</span></span> | <span data-ttu-id="8602d-210">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-210">✔</span></span> |
| <span data-ttu-id="8602d-211">图像链接</span><span class="sxs-lookup"><span data-stu-id="8602d-211">Image link</span></span>                | <span data-ttu-id="8602d-212">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-212">✔</span></span> | <span data-ttu-id="8602d-213">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-213">✔</span></span> | <span data-ttu-id="8602d-214">✔</span><span class="sxs-lookup"><span data-stu-id="8602d-214">✔</span></span> |

### <a name="cards"></a><span data-ttu-id="8602d-215">卡</span><span class="sxs-lookup"><span data-stu-id="8602d-215">Cards</span></span>

<span data-ttu-id="8602d-216">有关卡支持，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="8602d-216">For card support, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="8602d-217">后续步骤</span><span class="sxs-lookup"><span data-stu-id="8602d-217">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8602d-218">更新和删除机器人消息</span><span class="sxs-lookup"><span data-stu-id="8602d-218">Update and delete bot messages</span></span>](~/bots/how-to/update-and-delete-bot-messages.md)
