---
title: 卡片中的文本格式
description: 描述 Microsoft 团队中的卡片文本格式
keywords: 团队 bot 卡片格式
ms.date: 03/29/2018
ms.openlocfilehash: fcf0692fe033cd3c30ea1e3ac7bda8ddd06297ca
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346705"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="d729f-104">设置团队中卡片的格式</span><span class="sxs-lookup"><span data-stu-id="d729f-104">Format cards in Teams</span></span>

<span data-ttu-id="d729f-105">您可以使用 Markdown 或 HTML 向卡片添加格式文本格式，具体取决于卡片类型。</span><span class="sxs-lookup"><span data-stu-id="d729f-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="d729f-106">卡片仅支持 text 属性中的格式设置，而不支持标题或副标题属性中的格式设置。</span><span class="sxs-lookup"><span data-stu-id="d729f-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="d729f-107">可以使用 XML (HTML) 格式或 Markdown 的子集指定格式，具体取决于卡片类型。</span><span class="sxs-lookup"><span data-stu-id="d729f-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="d729f-108">对于当前和将来使用 Markdown 格式的开发自适应卡片，建议使用格式设置。</span><span class="sxs-lookup"><span data-stu-id="d729f-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="d729f-109">不同的卡片类型之间的格式支持不同，在桌面和移动团队客户端以及桌面浏览器中的团队之间，卡片的呈现可能略有不同。</span><span class="sxs-lookup"><span data-stu-id="d729f-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="d729f-110">可以在任何团队卡片中添加内嵌图像。</span><span class="sxs-lookup"><span data-stu-id="d729f-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="d729f-111">图像的格式为  `.png` 、 `.jpg` 或文件， `.gif` 不得超过1024× 1024 PX 或 1 MB。</span><span class="sxs-lookup"><span data-stu-id="d729f-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="d729f-112">不正式支持动画 GIF。</span><span class="sxs-lookup"><span data-stu-id="d729f-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="d729f-113">*请参阅*[卡片参考](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="d729f-113">*See* [Cards reference](./cards-reference.md#inline-card-images)</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="d729f-114">使用 Markdown 设置卡片格式</span><span class="sxs-lookup"><span data-stu-id="d729f-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="d729f-115">有两种卡类型支持团队中的 Markdown：</span><span class="sxs-lookup"><span data-stu-id="d729f-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d729f-116">**自适应卡片**： Markdown 在自适应卡片 `Textblock` 字段以及和中受 `Fact.Title` 支持 `Fact.Value` 。</span><span class="sxs-lookup"><span data-stu-id="d729f-116">**Adaptive Cards**: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="d729f-117">自适应卡片中不支持 HTML。</span><span class="sxs-lookup"><span data-stu-id="d729f-117">HTML is not supported in adaptive cards.</span></span>
> * <span data-ttu-id="d729f-118">**O365 连接器卡片**：文本字段中的 Office 365 连接器卡片支持 Markdown 和有限的 HTML。</span><span class="sxs-lookup"><span data-stu-id="d729f-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="d729f-119">**Markdown 格式：自适应卡片**</span><span class="sxs-lookup"><span data-stu-id="d729f-119">**Markdown formatting: Adaptive Cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="d729f-120">支持的和的 `Textblock` 样式 `Fact.Title` `Fact.Value` 如下：</span><span class="sxs-lookup"><span data-stu-id="d729f-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="d729f-121">样式</span><span class="sxs-lookup"><span data-stu-id="d729f-121">Style</span></span> | <span data-ttu-id="d729f-122">示例</span><span class="sxs-lookup"><span data-stu-id="d729f-122">Example</span></span> | <span data-ttu-id="d729f-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="d729f-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d729f-124">bold</span><span class="sxs-lookup"><span data-stu-id="d729f-124">bold</span></span> | <span data-ttu-id="d729f-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="d729f-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="d729f-126">italic</span><span class="sxs-lookup"><span data-stu-id="d729f-126">italic</span></span> | <span data-ttu-id="d729f-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="d729f-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="d729f-128">无序列表</span><span class="sxs-lookup"><span data-stu-id="d729f-128">unordered list</span></span> | <ul><li><span data-ttu-id="d729f-129">text</span><span class="sxs-lookup"><span data-stu-id="d729f-129">text</span></span></li><li><span data-ttu-id="d729f-130">text</span><span class="sxs-lookup"><span data-stu-id="d729f-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="d729f-131">排序列表</span><span class="sxs-lookup"><span data-stu-id="d729f-131">ordered list</span></span> | <ol><li><span data-ttu-id="d729f-132">text</span><span class="sxs-lookup"><span data-stu-id="d729f-132">text</span></span></li><li><span data-ttu-id="d729f-133">text</span><span class="sxs-lookup"><span data-stu-id="d729f-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="d729f-134">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="d729f-134">Hyperlinks</span></span> |[<span data-ttu-id="d729f-135">必应</span><span class="sxs-lookup"><span data-stu-id="d729f-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="d729f-136">以下 Markdown 标记不受支持：</span><span class="sxs-lookup"><span data-stu-id="d729f-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="d729f-137">标头</span><span class="sxs-lookup"><span data-stu-id="d729f-137">Headers</span></span>
* <span data-ttu-id="d729f-138">表格</span><span class="sxs-lookup"><span data-stu-id="d729f-138">Tables</span></span>
* <span data-ttu-id="d729f-139">图像</span><span class="sxs-lookup"><span data-stu-id="d729f-139">Images</span></span>
* <span data-ttu-id="d729f-140">预设格式文本</span><span class="sxs-lookup"><span data-stu-id="d729f-140">Preformatted text</span></span>
* <span data-ttu-id="d729f-141">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="d729f-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d729f-142">自适应卡片不支持 HTML 格式。</span><span class="sxs-lookup"><span data-stu-id="d729f-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="d729f-143">自适应卡片的换行符</span><span class="sxs-lookup"><span data-stu-id="d729f-143">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="d729f-144">在 "列表" 中，可以对 `\r` 换行符使用或 `\n` 转义序列。</span><span class="sxs-lookup"><span data-stu-id="d729f-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="d729f-145">`\n\n`在列表中使用将导致缩进列表中的下一个元素。</span><span class="sxs-lookup"><span data-stu-id="d729f-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="d729f-146">如果需要在 textblock 中的其他位置使用换行符，请使用 `\n\n` 。</span><span class="sxs-lookup"><span data-stu-id="d729f-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="d729f-147">自适应卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="d729f-147">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="d729f-148">桌面和团队的移动版之间的格式略有不同。</span><span class="sxs-lookup"><span data-stu-id="d729f-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="d729f-149">在桌面上，自适应卡片 Markdown 格式在 web 浏览器和团队客户端应用程序中的显示格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="d729f-149">On the desktop, Adaptive Card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![自适应卡片 Markdown 桌面客户端中的格式设置](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="d729f-151">在 iOS 上，自适应卡片 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="d729f-151">On iOS, Adaptive Card Markdown formatting appears like this:</span></span>

![自适应卡片 Markdown 格式在 iOS 中](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="d729f-153">在 Android 上，自适应卡片 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="d729f-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Android 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="d729f-155">有关自适应卡片的详细信息</span><span class="sxs-lookup"><span data-stu-id="d729f-155">More information on Adaptive Cards</span></span>

<span data-ttu-id="d729f-156">[自适应卡片中的文本功能](/adaptive-cards/create/textfeatures) 团队不支持本主题中提及的日期和本地化功能。</span><span class="sxs-lookup"><span data-stu-id="d729f-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="d729f-157">自适应卡片的格式设置示例</span><span class="sxs-lookup"><span data-stu-id="d729f-157">Formatting sample for Adaptive cards</span></span>

``` json
{
    "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "TextBlock",
            "text": "This is some **bold** text"
        },
        {
            "type": "TextBlock",
            "text": "This is some _italic_ text"
        },
        {
            "type": "TextBlock",
            "text": "- Bullet \r- List \r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "1. Numbered\r2. List\r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "Check out [Adaptive Cards](https://adaptivecards.io)"
        }
    ]
}
```

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="d729f-158">提及自适应卡片中的支持 1.2 1。2</span><span class="sxs-lookup"><span data-stu-id="d729f-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="d729f-159">基于卡片的提及在 Web、桌面和移动客户端中受支持。</span><span class="sxs-lookup"><span data-stu-id="d729f-159">Card based mentions are supported in Web, Desktop and mobile clients.</span></span> <span data-ttu-id="d729f-160">您可以在自适应卡片正文中添加用于 bot 和邮件扩展响应的 @ 提及。</span><span class="sxs-lookup"><span data-stu-id="d729f-160">You can add @ mentions within an adaptive card body for bots and messaging extension responses.</span></span>  <span data-ttu-id="d729f-161">若要在卡片中添加 @ 提及，请在 [通道和组聊天对话中](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions )遵循与基于邮件的提及相同的通知逻辑和呈现。</span><span class="sxs-lookup"><span data-stu-id="d729f-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions ).</span></span>

<span data-ttu-id="d729f-162">Bot 和邮件扩展可以在 [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 和 [FactSet](https://adaptivecards.io/explorer/FactSet.html) 元素的卡片内容中包括提及。</span><span class="sxs-lookup"><span data-stu-id="d729f-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="d729f-163">目前，工作组平台上的自适应卡版1.2 中不支持[媒体元素](https://adaptivecards.io/explorer/Media.html)。</span><span class="sxs-lookup"><span data-stu-id="d729f-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="d729f-164">在 bot 消息中不支持频道 & 的团队提及。</span><span class="sxs-lookup"><span data-stu-id="d729f-164">Channel & Team mentions are not supported in bot messages.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="d729f-165">构建提及</span><span class="sxs-lookup"><span data-stu-id="d729f-165">Constructing mentions</span></span>

<span data-ttu-id="d729f-166">若要在自适应卡片中添加提及的内容，应用需要包含以下元素</span><span class="sxs-lookup"><span data-stu-id="d729f-166">To include a mention in an Adaptive Card your app needs to include the following elements</span></span>

* <span data-ttu-id="d729f-167">`<at>username</at>` 在支持的自适应卡片元素中</span><span class="sxs-lookup"><span data-stu-id="d729f-167">`<at>username</at>` in the supported adaptive card elements</span></span>
* <span data-ttu-id="d729f-168">`mention` `msteams` 卡片内容中属性内的对象，其中包括所提及用户的团队用户 id</span><span class="sxs-lookup"><span data-stu-id="d729f-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="d729f-169">带提及的示例自适应卡片</span><span class="sxs-lookup"><span data-stu-id="d729f-169">Sample Adaptive card with a mention</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.card.adaptive",
  "content": {
    "type": "AdaptiveCard",
    "body": [
      {
        "type": "TextBlock",
        "text": "Hi <at>John Doe</at>"
      }
    ],
    "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.0",
    "msteams": {
      "entities": [
        {
          "type": "mention",
          "text": "<at>John Doe</at>",
          "mentioned": {
            "id": "29:123124124124",
            "name": "John Doe"
          }
        }
      ]
    }
  }
}
```

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="d729f-170">**Markdown 格式： O365 连接器卡**</span><span class="sxs-lookup"><span data-stu-id="d729f-170">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="d729f-171">连接器卡支持有限的 Markdown 和 HTML 格式设置。</span><span class="sxs-lookup"><span data-stu-id="d729f-171">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="d729f-172">上一节中介绍了 HTML 支持。</span><span class="sxs-lookup"><span data-stu-id="d729f-172">HTML support is described in the last section.</span></span>

| <span data-ttu-id="d729f-173">样式</span><span class="sxs-lookup"><span data-stu-id="d729f-173">Style</span></span> | <span data-ttu-id="d729f-174">示例</span><span class="sxs-lookup"><span data-stu-id="d729f-174">Example</span></span> | <span data-ttu-id="d729f-175">Markdown</span><span class="sxs-lookup"><span data-stu-id="d729f-175">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d729f-176">bold</span><span class="sxs-lookup"><span data-stu-id="d729f-176">bold</span></span> | <span data-ttu-id="d729f-177">**text**</span><span class="sxs-lookup"><span data-stu-id="d729f-177">**text**</span></span> | `**text**` |
| <span data-ttu-id="d729f-178">italic</span><span class="sxs-lookup"><span data-stu-id="d729f-178">italic</span></span> | <span data-ttu-id="d729f-179">*text*</span><span class="sxs-lookup"><span data-stu-id="d729f-179">*text*</span></span> | `*text*` |
| <span data-ttu-id="d729f-180">标头 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="d729f-180">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="d729f-181">**Text**</span><span class="sxs-lookup"><span data-stu-id="d729f-181">**Text**</span></span> | `### Text`|
| <span data-ttu-id="d729f-182">删除</span><span class="sxs-lookup"><span data-stu-id="d729f-182">strikethrough</span></span> | <span data-ttu-id="d729f-183">~~text~~</span><span class="sxs-lookup"><span data-stu-id="d729f-183">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="d729f-184">无序列表</span><span class="sxs-lookup"><span data-stu-id="d729f-184">unordered list</span></span> | <ul><li><span data-ttu-id="d729f-185">text</span><span class="sxs-lookup"><span data-stu-id="d729f-185">text</span></span></li><li><span data-ttu-id="d729f-186">text</span><span class="sxs-lookup"><span data-stu-id="d729f-186">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="d729f-187">排序列表</span><span class="sxs-lookup"><span data-stu-id="d729f-187">ordered list</span></span> | <ol><li><span data-ttu-id="d729f-188">text</span><span class="sxs-lookup"><span data-stu-id="d729f-188">text</span></span></li><li><span data-ttu-id="d729f-189">text</span><span class="sxs-lookup"><span data-stu-id="d729f-189">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="d729f-190">预设格式文本</span><span class="sxs-lookup"><span data-stu-id="d729f-190">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="d729f-191">blockquote</span><span class="sxs-lookup"><span data-stu-id="d729f-191">blockquote</span></span> | <span data-ttu-id="d729f-192">>blockquote 文本</span><span class="sxs-lookup"><span data-stu-id="d729f-192">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="d729f-193">超链接</span><span class="sxs-lookup"><span data-stu-id="d729f-193">hyperlink</span></span> | [<span data-ttu-id="d729f-194">必应</span><span class="sxs-lookup"><span data-stu-id="d729f-194">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="d729f-195">图像链接</span><span class="sxs-lookup"><span data-stu-id="d729f-195">image link</span></span> |![在摇滚上的工作](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="d729f-197">在连接器卡中，将为 `\n\n` （而不是为或）呈现换行符 `\n` `\r` 。</span><span class="sxs-lookup"><span data-stu-id="d729f-197">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="d729f-198">使用 Markdown 的连接器卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="d729f-198">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="d729f-199">在桌面上，连接器卡的 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="d729f-199">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![桌面客户端中的连接器卡的 Markdown 格式](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="d729f-201">在 iOS 上，连接器卡的 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="d729f-201">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![IOS 客户端中的连接器卡的 Markdown 格式](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="d729f-203">问题：</span><span class="sxs-lookup"><span data-stu-id="d729f-203">Issues:</span></span>

* <span data-ttu-id="d729f-204">团队的 iOS 客户端不会在连接器卡片中呈现 Markdown 或 HTML 嵌入式图像。</span><span class="sxs-lookup"><span data-stu-id="d729f-204">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="d729f-205">Blockquotes 呈现为缩进但不带灰色背景。</span><span class="sxs-lookup"><span data-stu-id="d729f-205">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="d729f-206">在 Android 上，连接器卡的 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="d729f-206">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Android 客户端中的连接器卡的 Markdown 格式](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="d729f-208">Markdown 连接器卡的格式示例</span><span class="sxs-lookup"><span data-stu-id="d729f-208">Formatting example for Markdown Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "https://schema.org/extensions",
    "summary": "Summary",
    "title": "Connector Card Markdown formatting",
    "sections": [
        {
            "text": "This is some **bold** text"
        },
        {
            "text": "This is some _italic_ text"
        },
        {
            "text": "# Header 1\r## Header 2\r### Header 3"
        },
        {
            "text": "- Bullet \r- List \r"
        },
        {
            "text": "1. Numbered\r1. List \r"
        },
        {
            "text": "Link: [Bing](https://www.bing.com)"
        },
        {
            "text": "embedded image link: ![Duck on a rock](https://aka.ms/Fo983c)"
        },
        {
            "text": "`preformatted text`"
        },
        {
            "text": "Newlines (backslash n, backslash n):\n\nline a\n\nline b\n\nline c"
        },
        {
            "text": ">This is a blockquote"
        }
     ]
  }
}

```

---

## <a name="formatting-cards-with-html"></a><span data-ttu-id="d729f-209">使用 HTML 格式化卡片</span><span class="sxs-lookup"><span data-stu-id="d729f-209">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="d729f-210">**HTML 格式： O365 连接器卡**</span><span class="sxs-lookup"><span data-stu-id="d729f-210">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="d729f-211">连接器卡支持有限的 Markdown 和 HTML 格式设置。</span><span class="sxs-lookup"><span data-stu-id="d729f-211">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="d729f-212">Markdown 将在下一节中介绍。</span><span class="sxs-lookup"><span data-stu-id="d729f-212">Markdown is described in the next section.</span></span>

| <span data-ttu-id="d729f-213">样式</span><span class="sxs-lookup"><span data-stu-id="d729f-213">Style</span></span> | <span data-ttu-id="d729f-214">示例</span><span class="sxs-lookup"><span data-stu-id="d729f-214">Example</span></span> | <span data-ttu-id="d729f-215">HTML</span><span class="sxs-lookup"><span data-stu-id="d729f-215">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d729f-216">bold</span><span class="sxs-lookup"><span data-stu-id="d729f-216">bold</span></span> | <span data-ttu-id="d729f-217">**text**</span><span class="sxs-lookup"><span data-stu-id="d729f-217">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="d729f-218">italic</span><span class="sxs-lookup"><span data-stu-id="d729f-218">italic</span></span> | <span data-ttu-id="d729f-219">*text*</span><span class="sxs-lookup"><span data-stu-id="d729f-219">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="d729f-220">标头 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="d729f-220">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="d729f-221">**Text**</span><span class="sxs-lookup"><span data-stu-id="d729f-221">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="d729f-222">删除</span><span class="sxs-lookup"><span data-stu-id="d729f-222">strikethrough</span></span> | <span data-ttu-id="d729f-223">~~text~~</span><span class="sxs-lookup"><span data-stu-id="d729f-223">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="d729f-224">无序列表</span><span class="sxs-lookup"><span data-stu-id="d729f-224">unordered list</span></span> | <ul><li><span data-ttu-id="d729f-225">text</span><span class="sxs-lookup"><span data-stu-id="d729f-225">text</span></span></li><li><span data-ttu-id="d729f-226">text</span><span class="sxs-lookup"><span data-stu-id="d729f-226">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="d729f-227">排序列表</span><span class="sxs-lookup"><span data-stu-id="d729f-227">ordered list</span></span> | <ol><li><span data-ttu-id="d729f-228">text</span><span class="sxs-lookup"><span data-stu-id="d729f-228">text</span></span></li><li><span data-ttu-id="d729f-229">text</span><span class="sxs-lookup"><span data-stu-id="d729f-229">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="d729f-230">预设格式文本</span><span class="sxs-lookup"><span data-stu-id="d729f-230">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="d729f-231">blockquote</span><span class="sxs-lookup"><span data-stu-id="d729f-231">blockquote</span></span> | <blockquote><span data-ttu-id="d729f-232">text</span><span class="sxs-lookup"><span data-stu-id="d729f-232">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="d729f-233">超链接</span><span class="sxs-lookup"><span data-stu-id="d729f-233">hyperlink</span></span> | [<span data-ttu-id="d729f-234">必应</span><span class="sxs-lookup"><span data-stu-id="d729f-234">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="d729f-235">图像链接</span><span class="sxs-lookup"><span data-stu-id="d729f-235">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="d729f-236">在连接器卡中，使用标记在 HTML 中呈现的换行符 `<p>` 。</span><span class="sxs-lookup"><span data-stu-id="d729f-236">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="d729f-237">使用 HTML 的连接器卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="d729f-237">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="d729f-238">在桌面上，连接器卡的 HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="d729f-238">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![桌面客户端中的连接器卡的 HTML 格式](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="d729f-240">在 iOS 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="d729f-240">On iOS, HTML formatting looks like this:</span></span>

![IOS 客户端中的连接器卡的 HTML 格式](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="d729f-242">问题：</span><span class="sxs-lookup"><span data-stu-id="d729f-242">Issues:</span></span>

* <span data-ttu-id="d729f-243">嵌入式图像不是使用 Markdown 或 HTML in 连接器卡片呈现在 iOS 上。</span><span class="sxs-lookup"><span data-stu-id="d729f-243">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="d729f-244">预设格式的文本将呈现，但不具有灰色背景。</span><span class="sxs-lookup"><span data-stu-id="d729f-244">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="d729f-245">在 Android 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="d729f-245">On Android, HTML formatting looks like this:</span></span>

![Android 客户端中的连接器卡的 HTML 格式](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="d729f-247">HTML 连接器卡的格式示例</span><span class="sxs-lookup"><span data-stu-id="d729f-247">Formatting sample for HTML Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "https://schema.org/extensions",
    "summary": "Summary",
    "title": "Connector Card HTML formatting",
    "sections": [
        {
            "text": "This is some <strong>bold</strong> text"
        },
        {
            "text": "This is some <em>italic</em> text"
        },
        {
            "text": "This is some <strike>strikethrough</strike> text"
        },
        {
            "text": "<h1>Header 1</h1>\r<h2>Header 2</h2>\r <h3>Header 3</h3>"
        },
        {
            "text": "bullet list <ul><li>text</li><li>text</li></ul>"
        },
        {
            "text": "ordered list <ol><li>text</li><li>text</li></ol>"
        },
        {
            "text": "hyperlink <a href=\"https://www.bing.com/\">Bing</a>"
        },
        {
            "text": "embedded image <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img>"
        },
        {
            "text": "preformatted text <pre>text</pre>"
        },
        {
            "text": "Paragraphs <p>Line a</p><p>Line b</p>"
        },
        {
            "text": "<blockquote>Blockquote text</blockquote>"
        }
     ]
  }
}

```

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="d729f-248">**HTML 格式：英雄和缩略图卡片**</span><span class="sxs-lookup"><span data-stu-id="d729f-248">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="d729f-249">简单卡片（如英雄和缩略图卡片）支持 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="d729f-249">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="d729f-250">不支持 Markdown。</span><span class="sxs-lookup"><span data-stu-id="d729f-250">Markdown is not supported.</span></span>

| <span data-ttu-id="d729f-251">样式</span><span class="sxs-lookup"><span data-stu-id="d729f-251">Style</span></span> | <span data-ttu-id="d729f-252">示例</span><span class="sxs-lookup"><span data-stu-id="d729f-252">Example</span></span> | <span data-ttu-id="d729f-253">HTML</span><span class="sxs-lookup"><span data-stu-id="d729f-253">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d729f-254">bold</span><span class="sxs-lookup"><span data-stu-id="d729f-254">bold</span></span> | <span data-ttu-id="d729f-255">**text**</span><span class="sxs-lookup"><span data-stu-id="d729f-255">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="d729f-256">italic</span><span class="sxs-lookup"><span data-stu-id="d729f-256">italic</span></span> | <span data-ttu-id="d729f-257">*text*</span><span class="sxs-lookup"><span data-stu-id="d729f-257">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="d729f-258">标头 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="d729f-258">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="d729f-259">**Text**</span><span class="sxs-lookup"><span data-stu-id="d729f-259">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="d729f-260">删除</span><span class="sxs-lookup"><span data-stu-id="d729f-260">strikethrough</span></span> | <span data-ttu-id="d729f-261">~~text~~</span><span class="sxs-lookup"><span data-stu-id="d729f-261">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="d729f-262">无序列表</span><span class="sxs-lookup"><span data-stu-id="d729f-262">unordered list</span></span> | <ul><li><span data-ttu-id="d729f-263">text</span><span class="sxs-lookup"><span data-stu-id="d729f-263">text</span></span></li><li><span data-ttu-id="d729f-264">text</span><span class="sxs-lookup"><span data-stu-id="d729f-264">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="d729f-265">排序列表</span><span class="sxs-lookup"><span data-stu-id="d729f-265">ordered list</span></span> | <ol><li><span data-ttu-id="d729f-266">text</span><span class="sxs-lookup"><span data-stu-id="d729f-266">text</span></span></li><li><span data-ttu-id="d729f-267">text</span><span class="sxs-lookup"><span data-stu-id="d729f-267">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="d729f-268">预设格式文本</span><span class="sxs-lookup"><span data-stu-id="d729f-268">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="d729f-269">blockquote</span><span class="sxs-lookup"><span data-stu-id="d729f-269">blockquote</span></span> | <blockquote><span data-ttu-id="d729f-270">text</span><span class="sxs-lookup"><span data-stu-id="d729f-270">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="d729f-271">超链接</span><span class="sxs-lookup"><span data-stu-id="d729f-271">hyperlink</span></span> | [<span data-ttu-id="d729f-272">必应</span><span class="sxs-lookup"><span data-stu-id="d729f-272">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="d729f-273">图像链接</span><span class="sxs-lookup"><span data-stu-id="d729f-273">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="d729f-274">简单卡片的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="d729f-274">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="d729f-275">由于桌面和移动平台之间的分辨率不同，因此桌面和团队的移动版之间的格式不同。</span><span class="sxs-lookup"><span data-stu-id="d729f-275">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="d729f-276">在桌面上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="d729f-276">On the desktop, HTML formatting appears like this:</span></span>

![桌面客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="d729f-278">在 iOS 上，HTML 格式的外观如下所示：</span><span class="sxs-lookup"><span data-stu-id="d729f-278">On iOS, HTML formatting appears like this:</span></span>

![IOS 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="d729f-280">问题：</span><span class="sxs-lookup"><span data-stu-id="d729f-280">Issues:</span></span>

* <span data-ttu-id="d729f-281">在 iOS 上不呈现粗体和斜体等字符格式。</span><span class="sxs-lookup"><span data-stu-id="d729f-281">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="d729f-282">在 Android 上，HTML 格式的外观如下所示：</span><span class="sxs-lookup"><span data-stu-id="d729f-282">On Android, HTML formatting appears like this:</span></span>

![Android 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="d729f-284">Android 上正确显示的字符格式（如粗体和斜体）。</span><span class="sxs-lookup"><span data-stu-id="d729f-284">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="d729f-285">简单卡片中的 HTML 格式的格式示例</span><span class="sxs-lookup"><span data-stu-id="d729f-285">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="d729f-286">这些屏幕截图是使用团队 AppStudio 创建的，其中，将一个英雄卡片的 text 属性设置为以下字符串。</span><span class="sxs-lookup"><span data-stu-id="d729f-286">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="d729f-287">您可以通过修改此代码来测试自己的卡片中的格式设置。</span><span class="sxs-lookup"><span data-stu-id="d729f-287">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
