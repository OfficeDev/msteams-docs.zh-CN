---
title: 卡片中的文本格式
description: 介绍 Microsoft Teams 中的卡片文本格式
keywords: teams 自动程序卡格式
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: b50109ad664bda2fc130e08c53dd7fca2a3d54ef
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922515"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="04ad2-104">在 Teams 中设置卡片格式</span><span class="sxs-lookup"><span data-stu-id="04ad2-104">Format cards in Teams</span></span>

<span data-ttu-id="04ad2-105">可以使用 Markdown 或 HTML 将格式文本格式添加到卡片，具体取决于卡片类型。</span><span class="sxs-lookup"><span data-stu-id="04ad2-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="04ad2-106">卡片仅支持文本属性中的格式设置，不支持标题或副标题属性中的格式设置。</span><span class="sxs-lookup"><span data-stu-id="04ad2-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="04ad2-107">可以使用 XML 格式的子集或 HTML (格式) Markdown 来指定格式，具体取决于卡片类型。</span><span class="sxs-lookup"><span data-stu-id="04ad2-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="04ad2-108">对于当前和未来开发，建议使用 Markdown 格式的自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="04ad2-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="04ad2-109">不同卡类型之间的格式支持不同，并且桌面版和移动版 Teams 客户端以及桌面浏览器中的 Teams 的卡片呈现可能略有不同。</span><span class="sxs-lookup"><span data-stu-id="04ad2-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="04ad2-110">你可以将内联图像与任意 Teams 卡一起包含。</span><span class="sxs-lookup"><span data-stu-id="04ad2-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="04ad2-111">格式设置为 、 或 文件的图像不能超过  `.png` `.jpg` `.gif` 1024 像素× 1024 像素或 1 MB。</span><span class="sxs-lookup"><span data-stu-id="04ad2-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="04ad2-112">动态 GIF 不受正式支持。</span><span class="sxs-lookup"><span data-stu-id="04ad2-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="04ad2-113">*请参阅*[卡片参考](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="04ad2-113">*See* [Cards reference](./cards-reference.md#inline-card-images)</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="04ad2-114">使用 Markdown 格式化卡片</span><span class="sxs-lookup"><span data-stu-id="04ad2-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="04ad2-115">Teams 中支持 Markdown 的卡片类型有两种：</span><span class="sxs-lookup"><span data-stu-id="04ad2-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="04ad2-116">**自适应卡片**： Markdown 在自适应卡片字段中以及 和 `Textblock` `Fact.Title` 中受支持 `Fact.Value` 。</span><span class="sxs-lookup"><span data-stu-id="04ad2-116">**Adaptive cards**: Markdown is supported in Adaptive card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="04ad2-117">自适应卡片不支持 HTML。</span><span class="sxs-lookup"><span data-stu-id="04ad2-117">HTML is not supported in Adaptive cards.</span></span>
> * <span data-ttu-id="04ad2-118">**O365 连接器卡**：文本字段中的 Office 365 连接器卡支持 Markdown 和有限的 HTML。</span><span class="sxs-lookup"><span data-stu-id="04ad2-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="04ad2-119">**Markdown 格式：自适应卡片**</span><span class="sxs-lookup"><span data-stu-id="04ad2-119">**Markdown formatting: Adaptive cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="04ad2-120">和 `Textblock` 支持的 `Fact.Title` `Fact.Value` 样式包括：</span><span class="sxs-lookup"><span data-stu-id="04ad2-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="04ad2-121">样式</span><span class="sxs-lookup"><span data-stu-id="04ad2-121">Style</span></span> | <span data-ttu-id="04ad2-122">示例</span><span class="sxs-lookup"><span data-stu-id="04ad2-122">Example</span></span> | <span data-ttu-id="04ad2-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="04ad2-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="04ad2-124">bold</span><span class="sxs-lookup"><span data-stu-id="04ad2-124">bold</span></span> | <span data-ttu-id="04ad2-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="04ad2-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="04ad2-126">italic</span><span class="sxs-lookup"><span data-stu-id="04ad2-126">italic</span></span> | <span data-ttu-id="04ad2-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="04ad2-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="04ad2-128">无序列表</span><span class="sxs-lookup"><span data-stu-id="04ad2-128">unordered list</span></span> | <ul><li><span data-ttu-id="04ad2-129">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-129">text</span></span></li><li><span data-ttu-id="04ad2-130">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="04ad2-131">排序列表</span><span class="sxs-lookup"><span data-stu-id="04ad2-131">ordered list</span></span> | <ol><li><span data-ttu-id="04ad2-132">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-132">text</span></span></li><li><span data-ttu-id="04ad2-133">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="04ad2-134">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="04ad2-134">Hyperlinks</span></span> |[<span data-ttu-id="04ad2-135">必应</span><span class="sxs-lookup"><span data-stu-id="04ad2-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="04ad2-136">不支持以下 Markdown 标记：</span><span class="sxs-lookup"><span data-stu-id="04ad2-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="04ad2-137">标头</span><span class="sxs-lookup"><span data-stu-id="04ad2-137">Headers</span></span>
* <span data-ttu-id="04ad2-138">表格</span><span class="sxs-lookup"><span data-stu-id="04ad2-138">Tables</span></span>
* <span data-ttu-id="04ad2-139">图像</span><span class="sxs-lookup"><span data-stu-id="04ad2-139">Images</span></span>
* <span data-ttu-id="04ad2-140">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="04ad2-140">Preformatted text</span></span>
* <span data-ttu-id="04ad2-141">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="04ad2-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04ad2-142">自适应卡片不支持 HTML 格式。</span><span class="sxs-lookup"><span data-stu-id="04ad2-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="04ad2-143">自适应卡片的 Newlines</span><span class="sxs-lookup"><span data-stu-id="04ad2-143">Newlines for Adaptive cards</span></span>

<span data-ttu-id="04ad2-144">在列表中，可以将 `\r` 或 `\n` 转义序列用于新行。</span><span class="sxs-lookup"><span data-stu-id="04ad2-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="04ad2-145">在 `\n\n` 列表中使用 将导致列表中的下一个元素缩进。</span><span class="sxs-lookup"><span data-stu-id="04ad2-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="04ad2-146">如果你需要在 textblock 中的其他地方使用 newlines，请使用 `\n\n` 。</span><span class="sxs-lookup"><span data-stu-id="04ad2-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="04ad2-147">自适应卡片的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="04ad2-147">Mobile and desktop differences for Adaptive cards</span></span>

<span data-ttu-id="04ad2-148">桌面版和移动版 Teams 的格式略有不同。</span><span class="sxs-lookup"><span data-stu-id="04ad2-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="04ad2-149">在桌面上，自适应卡片 Markdown 格式在 Web 浏览器和 Teams 客户端应用程序中如下所示：</span><span class="sxs-lookup"><span data-stu-id="04ad2-149">On the desktop, Adaptive card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![桌面客户端中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="04ad2-151">在 iOS 上，自适应卡片 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="04ad2-151">On iOS, Adaptive card Markdown formatting appears like this:</span></span>

![iOS 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="04ad2-153">在 Android 上，自适应卡片 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="04ad2-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Android 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="04ad2-155">自适应卡片详细信息</span><span class="sxs-lookup"><span data-stu-id="04ad2-155">More information on Adaptive cards</span></span>

<span data-ttu-id="04ad2-156">[自适应卡片中的文本功能](/adaptive-cards/create/textfeatures) 本主题中提到的日期和本地化功能在 Teams 中不受支持。</span><span class="sxs-lookup"><span data-stu-id="04ad2-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="04ad2-157">自适应卡片的格式设置示例</span><span class="sxs-lookup"><span data-stu-id="04ad2-157">Formatting sample for Adaptive cards</span></span>

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

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="04ad2-158">自适应卡片 v1.2 中的提及支持</span><span class="sxs-lookup"><span data-stu-id="04ad2-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="04ad2-159">Web、桌面和移动客户端支持基于卡片的提及。</span><span class="sxs-lookup"><span data-stu-id="04ad2-159">Card based mentions are supported in web, desktop and mobile clients.</span></span> <span data-ttu-id="04ad2-160">你可以为机器人和消息传递扩展响应在自适应卡片正文中添加 @ 提及。</span><span class="sxs-lookup"><span data-stu-id="04ad2-160">You can add @ mentions within an adaptive card body for bots and messaging extension responses.</span></span> <span data-ttu-id="04ad2-161">若要在卡片中添加 @ 提及，请遵循与频道和群聊对话中基于消息的提及相同的通知 [逻辑和呈现](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)。</span><span class="sxs-lookup"><span data-stu-id="04ad2-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span></span>

<span data-ttu-id="04ad2-162">聊天机器人和消息传递扩展可以在 [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 和 [FactSet](https://adaptivecards.io/explorer/FactSet.html) 元素的卡片内容中包括提及。</span><span class="sxs-lookup"><span data-stu-id="04ad2-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="04ad2-163">[Teams 平台上](https://adaptivecards.io/explorer/Media.html) 的自适应卡片 v1.2 当前不支持媒体元素。</span><span class="sxs-lookup"><span data-stu-id="04ad2-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="04ad2-164">频道&团队提及在机器人消息中不受支持。</span><span class="sxs-lookup"><span data-stu-id="04ad2-164">Channel & Team mentions are not supported in bot messages.</span></span>

#### <a name="constructing-mentions"></a><span data-ttu-id="04ad2-165">构造提及</span><span class="sxs-lookup"><span data-stu-id="04ad2-165">Constructing mentions</span></span>

<span data-ttu-id="04ad2-166">若要在自适应卡片中包括提及，你的应用需要包括以下元素：</span><span class="sxs-lookup"><span data-stu-id="04ad2-166">To include a mention in an Adaptive Card your app needs to include the following elements:</span></span>

* <span data-ttu-id="04ad2-167">`<at>username</at>` 在支持的自适应卡片元素中。</span><span class="sxs-lookup"><span data-stu-id="04ad2-167">`<at>username</at>` in the supported Adaptive card elements.</span></span>
* <span data-ttu-id="04ad2-168">`mention`卡片内容 `msteams` 中属性内的对象，其中包括被提及用户的 Teams 用户 ID。</span><span class="sxs-lookup"><span data-stu-id="04ad2-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned.</span></span>
* <span data-ttu-id="04ad2-169">`userId`是自动程序 ID 和特定用户所特有的。</span><span class="sxs-lookup"><span data-stu-id="04ad2-169">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="04ad2-170">它可用于@mention用户。</span><span class="sxs-lookup"><span data-stu-id="04ad2-170">It can be used to @mention a particular user.</span></span> <span data-ttu-id="04ad2-171">`userId`可以使用获取用户 ID 中提到的选项之[一来检索](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id)。</span><span class="sxs-lookup"><span data-stu-id="04ad2-171">The `userId` can be retrieved using one of the options mentioned in [get the user ID](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="04ad2-172">带提及功能的示例自适应卡片</span><span class="sxs-lookup"><span data-stu-id="04ad2-172">Sample Adaptive card with a mention</span></span>

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

### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="04ad2-173">自适应卡片中的信息屏蔽</span><span class="sxs-lookup"><span data-stu-id="04ad2-173">Information masking in Adaptive cards</span></span>
<span data-ttu-id="04ad2-174">使用信息屏蔽属性可以屏蔽特定信息，如自适应卡片输入元素内用户的密码或 [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) 敏感信息。</span><span class="sxs-lookup"><span data-stu-id="04ad2-174">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span> 

> [!NOTE]
> <span data-ttu-id="04ad2-175">该功能仅支持客户端信息屏蔽，将屏蔽的输入文本作为纯文本发送到在机器人配置期间指定的 https [终结点地址](../../build-your-first-app/build-bot.md#4-configure-your-bot)。</span><span class="sxs-lookup"><span data-stu-id="04ad2-175">The feature only supports client side information masking, the masked input text is sent as clear text to the https endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md#4-configure-your-bot).</span></span> 

> [!NOTE]
> <span data-ttu-id="04ad2-176">信息屏蔽属性当前仅在开发人员预览版中可用。</span><span class="sxs-lookup"><span data-stu-id="04ad2-176">The information masking property is currently available in the developer preview only.</span></span>

<span data-ttu-id="04ad2-177">若要屏蔽自适应卡片中的信息，请添加 `isMasked` 属性以 **键入** `Input.Text` ，将其值设置为 *true*。</span><span class="sxs-lookup"><span data-stu-id="04ad2-177">To mask information in Adaptive cards, add the `isMasked` property to **type** `Input.Text`, and set its value to *true*.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="04ad2-178">具有屏蔽属性的示例自适应卡片</span><span class="sxs-lookup"><span data-stu-id="04ad2-178">Sample Adaptive card with masking property</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

<span data-ttu-id="04ad2-179">下图是自适应卡片中屏蔽信息的示例：</span><span class="sxs-lookup"><span data-stu-id="04ad2-179">The following image is an example of masking information in Adaptive cards:</span></span>

![屏蔽信息图像](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="04ad2-181">全宽自适应卡片</span><span class="sxs-lookup"><span data-stu-id="04ad2-181">Full width Adaptive card</span></span>
<span data-ttu-id="04ad2-182">可以使用 属性扩展自适应卡片的宽度， `msteams` 并占用额外的画布空间。</span><span class="sxs-lookup"><span data-stu-id="04ad2-182">You can use the `msteams` property to expand the width of an Adaptive card and make use of additional canvas space.</span></span> <span data-ttu-id="04ad2-183">有关如何使用 属性的信息，请参阅以下示例：</span><span class="sxs-lookup"><span data-stu-id="04ad2-183">For information on how to use the property, see the following example:</span></span>

#### <a name="constructing-full-width-cards"></a><span data-ttu-id="04ad2-184">构造全宽卡片</span><span class="sxs-lookup"><span data-stu-id="04ad2-184">Constructing full width cards</span></span>
<span data-ttu-id="04ad2-185">若要制作全宽自适应卡片，必须将卡片内容 `width` `msteams` 中的 属性中的 对象设置为 `Full` 。</span><span class="sxs-lookup"><span data-stu-id="04ad2-185">To make a full width Adaptive card the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>
<span data-ttu-id="04ad2-186">此外，你的应用必须包含以下元素：</span><span class="sxs-lookup"><span data-stu-id="04ad2-186">In addition, your app must include the following elements:</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="04ad2-187">全宽自适应卡片示例</span><span class="sxs-lookup"><span data-stu-id="04ad2-187">Sample adaptive card with full width</span></span>

``` json
{
    "type": "AdaptiveCard",
    "body": [{
        "type": "Container",
        "items": [{
            "type": "TextBlock",
            "text": "Digest card",
            "size": "Large",
            "weight": "Bolder"
        }]
    }],

    "msteams": {
        "width": "Full"
    },
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

<span data-ttu-id="04ad2-188">完整宽度自适应卡片如下所示： ![ 全宽自适应卡片视图](../../assets/images/cards/full-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="04ad2-188">A full width Adaptive Card appears as follows: ![Full width Adaptive Card view](../../assets/images/cards/full-width-adaptive-card.png)</span></span>

<span data-ttu-id="04ad2-189">如果尚未将属性设置为 `width` *Full，* 则自适应卡片的默认视图如下所示： ![ 小宽度自适应卡片视图](../../assets/images/cards/small-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="04ad2-189">If you have not set the `width` property to *Full*, then the default view of the Adaptive Card is as follows: ![Small width Adaptive Card view](../../assets/images/cards/small-width-adaptive-card.png)</span></span>

### <a name="typeahead-support"></a><span data-ttu-id="04ad2-190">Typeahead 支持</span><span class="sxs-lookup"><span data-stu-id="04ad2-190">Typeahead support</span></span>

<span data-ttu-id="04ad2-191">在架构元素中，要求用户通过大量选择进行筛选可能会显著降低 [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) 任务完成速度。</span><span class="sxs-lookup"><span data-stu-id="04ad2-191">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter through and select through a sizable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="04ad2-192">自适应卡片中的 Typeahead 支持可以在用户键入输入时缩小或筛选输入选项集，从而简化输入选择。</span><span class="sxs-lookup"><span data-stu-id="04ad2-192">Typeahead support within Adaptive cards can simplify input selection by narrowing or filtering the set of input choices as a user is typing the input.</span></span> 

#### <a name="enable-typeahead-in-adaptive-cards"></a><span data-ttu-id="04ad2-193">在自适应卡片中启用 typeahead</span><span class="sxs-lookup"><span data-stu-id="04ad2-193">Enable typeahead in Adaptive cards</span></span>

<span data-ttu-id="04ad2-194">若要在 设置为 内启用 `Input.Choiceset` `style` typeahead， `filtered` 并确保 `isMultiSelect` 设置为 `false` 。</span><span class="sxs-lookup"><span data-stu-id="04ad2-194">To enable typeahead within the `Input.Choiceset` set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span> 

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="04ad2-195">具有 typeahead 支持的示例自适应卡片</span><span class="sxs-lookup"><span data-stu-id="04ad2-195">Sample adaptive card with typeahead support</span></span>

``` json
{
   "type": "Input.ChoiceSet",
   "label": "Select a user",
   "isMultiSelect": false,
   "choices":  [
      { "title": "User 1", "value": "User1" },
      { "title": "User 2", "value": "User2" }
    ],
   "style": "filtered"
}
``` 

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="04ad2-196">自适应卡片中的图像阶段视图</span><span class="sxs-lookup"><span data-stu-id="04ad2-196">Stage view for images in Adaptive Cards</span></span>

> [!NOTE]
> <span data-ttu-id="04ad2-197">此功能目前仅在开发人员预览版中可用。</span><span class="sxs-lookup"><span data-stu-id="04ad2-197">This feature is currently available in developer preview only.</span></span>
 
<span data-ttu-id="04ad2-198">在自适应卡片中，可以使用 属性添加选择性地在阶段 `msteams` 视图中显示图像的能力。</span><span class="sxs-lookup"><span data-stu-id="04ad2-198">In an Adaptive card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="04ad2-199">当用户将鼠标悬停在图像上时，他们将看到展开图标，其 `allowExpand` 属性设置为 `true` 。</span><span class="sxs-lookup"><span data-stu-id="04ad2-199">When users hover over the images, they would see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="04ad2-200">有关如何使用 属性的信息，请参阅以下示例：</span><span class="sxs-lookup"><span data-stu-id="04ad2-200">For information on how to use the property, see the following example:</span></span>

``` json
{
    "type": "AdaptiveCard",
     "body": [
          {
            "type": "Image",
            "url": "https://picsum.photos/200/200?image=110",
            "msTeams": {
              "allowExpand": true
            }
          },
     ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

<span data-ttu-id="04ad2-201">当用户将鼠标悬停在图像上方时，图像右上角将显示展开图标：带可展开图像的自适应 ![ 卡片](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span><span class="sxs-lookup"><span data-stu-id="04ad2-201">When users hover over the image, an expand icon appears at top right corner of the image: ![Adaptive card with expandable image](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span></span>

<span data-ttu-id="04ad2-202">当用户选择展开按钮时，图像显示在阶段视图中：展开 ![ 到阶段视图的图像](../../assets/images/cards/adaptivecard-expand-image.png)</span><span class="sxs-lookup"><span data-stu-id="04ad2-202">The image appears in stage view when the user selects the expand button: ![Image expanded to stage view](../../assets/images/cards/adaptivecard-expand-image.png)</span></span>

<span data-ttu-id="04ad2-203">在阶段视图中，用户可以放大和缩小图像。</span><span class="sxs-lookup"><span data-stu-id="04ad2-203">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="04ad2-204">可以选择自适应卡片中的哪些图像需要具备此功能。</span><span class="sxs-lookup"><span data-stu-id="04ad2-204">You can select which images in your Adaptive card needs to have this capability.</span></span>

> [!NOTE]
> <span data-ttu-id="04ad2-205">放大和缩小功能仅适用于自适应卡片 (图像) 图像元素。</span><span class="sxs-lookup"><span data-stu-id="04ad2-205">Zoom in and zoom out capability applies only to the image elements (Image type) in an Adaptive card.</span></span>

> [!NOTE]
> <span data-ttu-id="04ad2-206">对于 Teams 移动应用，自适应卡片中的图像阶段视图功能默认可用，用户只需点击图像即可在阶段视图中查看自适应卡片图像，而不管属性是否 `allowExpand` 存在。</span><span class="sxs-lookup"><span data-stu-id="04ad2-206">For Teams mobile apps, stage view functionality for images in Adaptive Cards are available by default and users will be able to view Adaptive card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="04ad2-207">**Markdown 格式：O365 连接器卡**</span><span class="sxs-lookup"><span data-stu-id="04ad2-207">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="04ad2-208">连接器卡支持有限的 Markdown 和 HTML 格式。</span><span class="sxs-lookup"><span data-stu-id="04ad2-208">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="04ad2-209">HTML 支持在上一节中介绍。</span><span class="sxs-lookup"><span data-stu-id="04ad2-209">HTML support is described in the last section.</span></span>

| <span data-ttu-id="04ad2-210">样式</span><span class="sxs-lookup"><span data-stu-id="04ad2-210">Style</span></span> | <span data-ttu-id="04ad2-211">示例</span><span class="sxs-lookup"><span data-stu-id="04ad2-211">Example</span></span> | <span data-ttu-id="04ad2-212">Markdown</span><span class="sxs-lookup"><span data-stu-id="04ad2-212">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="04ad2-213">bold</span><span class="sxs-lookup"><span data-stu-id="04ad2-213">bold</span></span> | <span data-ttu-id="04ad2-214">**text**</span><span class="sxs-lookup"><span data-stu-id="04ad2-214">**text**</span></span> | `**text**` |
| <span data-ttu-id="04ad2-215">italic</span><span class="sxs-lookup"><span data-stu-id="04ad2-215">italic</span></span> | <span data-ttu-id="04ad2-216">*text*</span><span class="sxs-lookup"><span data-stu-id="04ad2-216">*text*</span></span> | `*text*` |
| <span data-ttu-id="04ad2-217">页眉 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="04ad2-217">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="04ad2-218">**Text**</span><span class="sxs-lookup"><span data-stu-id="04ad2-218">**Text**</span></span> | `### Text`|
| <span data-ttu-id="04ad2-219">strikethrough</span><span class="sxs-lookup"><span data-stu-id="04ad2-219">strikethrough</span></span> | <span data-ttu-id="04ad2-220">~~text~~</span><span class="sxs-lookup"><span data-stu-id="04ad2-220">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="04ad2-221">无序列表</span><span class="sxs-lookup"><span data-stu-id="04ad2-221">unordered list</span></span> | <ul><li><span data-ttu-id="04ad2-222">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-222">text</span></span></li><li><span data-ttu-id="04ad2-223">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-223">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="04ad2-224">排序列表</span><span class="sxs-lookup"><span data-stu-id="04ad2-224">ordered list</span></span> | <ol><li><span data-ttu-id="04ad2-225">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-225">text</span></span></li><li><span data-ttu-id="04ad2-226">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-226">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="04ad2-227">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="04ad2-227">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="04ad2-228">blockquote</span><span class="sxs-lookup"><span data-stu-id="04ad2-228">blockquote</span></span> | <span data-ttu-id="04ad2-229">>blockquote 文本</span><span class="sxs-lookup"><span data-stu-id="04ad2-229">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="04ad2-230">超链接</span><span class="sxs-lookup"><span data-stu-id="04ad2-230">hyperlink</span></span> | [<span data-ttu-id="04ad2-231">必应</span><span class="sxs-lookup"><span data-stu-id="04ad2-231">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="04ad2-232">图像链接</span><span class="sxs-lookup"><span data-stu-id="04ad2-232">image link</span></span> |![在一个地心上闪避](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="04ad2-234">在连接器卡中，为 呈现新行 `\n\n` ，但不为 或 `\n` 呈现 `\r` 。</span><span class="sxs-lookup"><span data-stu-id="04ad2-234">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="04ad2-235">使用 Markdown 的连接器卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="04ad2-235">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="04ad2-236">在桌面上，连接器卡的 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="04ad2-236">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![桌面客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="04ad2-238">在 iOS 上，连接器卡的 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="04ad2-238">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![iOS 客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="04ad2-240">问题：</span><span class="sxs-lookup"><span data-stu-id="04ad2-240">Issues:</span></span>

* <span data-ttu-id="04ad2-241">适用于 Teams 的 iOS 客户端不会在连接器卡中呈现 Markdown 或 HTML 内嵌图像。</span><span class="sxs-lookup"><span data-stu-id="04ad2-241">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="04ad2-242">Blockquotes 呈现为缩进，但不带灰色背景。</span><span class="sxs-lookup"><span data-stu-id="04ad2-242">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="04ad2-243">在 Android 上，连接器卡的 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="04ad2-243">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Android 客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="04ad2-245">Markdown 连接器卡的格式设置示例</span><span class="sxs-lookup"><span data-stu-id="04ad2-245">Formatting example for Markdown Connector Cards</span></span>

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

## <a name="formatting-cards-with-html"></a><span data-ttu-id="04ad2-246">使用 HTML 设置卡片格式</span><span class="sxs-lookup"><span data-stu-id="04ad2-246">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="04ad2-247">**HTML 格式：O365 连接器卡**</span><span class="sxs-lookup"><span data-stu-id="04ad2-247">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="04ad2-248">连接器卡支持有限的 Markdown 和 HTML 格式。</span><span class="sxs-lookup"><span data-stu-id="04ad2-248">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="04ad2-249">Markdown 将下一节介绍。</span><span class="sxs-lookup"><span data-stu-id="04ad2-249">Markdown is described in the next section.</span></span>

| <span data-ttu-id="04ad2-250">样式</span><span class="sxs-lookup"><span data-stu-id="04ad2-250">Style</span></span> | <span data-ttu-id="04ad2-251">示例</span><span class="sxs-lookup"><span data-stu-id="04ad2-251">Example</span></span> | <span data-ttu-id="04ad2-252">HTML</span><span class="sxs-lookup"><span data-stu-id="04ad2-252">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="04ad2-253">bold</span><span class="sxs-lookup"><span data-stu-id="04ad2-253">bold</span></span> | <span data-ttu-id="04ad2-254">**text**</span><span class="sxs-lookup"><span data-stu-id="04ad2-254">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="04ad2-255">italic</span><span class="sxs-lookup"><span data-stu-id="04ad2-255">italic</span></span> | <span data-ttu-id="04ad2-256">*text*</span><span class="sxs-lookup"><span data-stu-id="04ad2-256">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="04ad2-257">页眉 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="04ad2-257">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="04ad2-258">**Text**</span><span class="sxs-lookup"><span data-stu-id="04ad2-258">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="04ad2-259">strikethrough</span><span class="sxs-lookup"><span data-stu-id="04ad2-259">strikethrough</span></span> | <span data-ttu-id="04ad2-260">~~text~~</span><span class="sxs-lookup"><span data-stu-id="04ad2-260">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="04ad2-261">无序列表</span><span class="sxs-lookup"><span data-stu-id="04ad2-261">unordered list</span></span> | <ul><li><span data-ttu-id="04ad2-262">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-262">text</span></span></li><li><span data-ttu-id="04ad2-263">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-263">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="04ad2-264">排序列表</span><span class="sxs-lookup"><span data-stu-id="04ad2-264">ordered list</span></span> | <ol><li><span data-ttu-id="04ad2-265">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-265">text</span></span></li><li><span data-ttu-id="04ad2-266">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-266">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="04ad2-267">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="04ad2-267">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="04ad2-268">blockquote</span><span class="sxs-lookup"><span data-stu-id="04ad2-268">blockquote</span></span> | <blockquote><span data-ttu-id="04ad2-269">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-269">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="04ad2-270">超链接</span><span class="sxs-lookup"><span data-stu-id="04ad2-270">hyperlink</span></span> | [<span data-ttu-id="04ad2-271">必应</span><span class="sxs-lookup"><span data-stu-id="04ad2-271">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="04ad2-272">图像链接</span><span class="sxs-lookup"><span data-stu-id="04ad2-272">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="04ad2-273">在连接器卡中，使用 标记以 HTML 格式呈现 `<p>` 新行。</span><span class="sxs-lookup"><span data-stu-id="04ad2-273">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="04ad2-274">使用 HTML 的连接器卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="04ad2-274">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="04ad2-275">在桌面上，连接器卡的 HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="04ad2-275">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![桌面客户端中连接器卡的 HTML 格式](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="04ad2-277">在 iOS 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="04ad2-277">On iOS, HTML formatting looks like this:</span></span>

![iOS 客户端中连接器卡的 HTML 格式](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="04ad2-279">问题：</span><span class="sxs-lookup"><span data-stu-id="04ad2-279">Issues:</span></span>

* <span data-ttu-id="04ad2-280">内联图像不会使用连接器卡中的 Markdown 或 HTML 呈现在 iOS 上。</span><span class="sxs-lookup"><span data-stu-id="04ad2-280">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="04ad2-281">呈现预设格式的文本，但没有灰色背景。</span><span class="sxs-lookup"><span data-stu-id="04ad2-281">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="04ad2-282">在 Android 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="04ad2-282">On Android, HTML formatting looks like this:</span></span>

![Android 客户端中连接器卡的 HTML 格式](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="04ad2-284">HTML 连接器卡的格式设置示例</span><span class="sxs-lookup"><span data-stu-id="04ad2-284">Formatting sample for HTML Connector Cards</span></span>

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="04ad2-285">**HTML 格式：hero 和 thumbnail 卡片**</span><span class="sxs-lookup"><span data-stu-id="04ad2-285">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="04ad2-286">HTML 标记支持简单的卡片，如 hero 和 thumbnail 卡片。</span><span class="sxs-lookup"><span data-stu-id="04ad2-286">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="04ad2-287">不支持 Markdown。</span><span class="sxs-lookup"><span data-stu-id="04ad2-287">Markdown is not supported.</span></span>

| <span data-ttu-id="04ad2-288">样式</span><span class="sxs-lookup"><span data-stu-id="04ad2-288">Style</span></span> | <span data-ttu-id="04ad2-289">示例</span><span class="sxs-lookup"><span data-stu-id="04ad2-289">Example</span></span> | <span data-ttu-id="04ad2-290">HTML</span><span class="sxs-lookup"><span data-stu-id="04ad2-290">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="04ad2-291">bold</span><span class="sxs-lookup"><span data-stu-id="04ad2-291">bold</span></span> | <span data-ttu-id="04ad2-292">**text**</span><span class="sxs-lookup"><span data-stu-id="04ad2-292">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="04ad2-293">italic</span><span class="sxs-lookup"><span data-stu-id="04ad2-293">italic</span></span> | <span data-ttu-id="04ad2-294">*text*</span><span class="sxs-lookup"><span data-stu-id="04ad2-294">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="04ad2-295">页眉 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="04ad2-295">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="04ad2-296">**Text**</span><span class="sxs-lookup"><span data-stu-id="04ad2-296">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="04ad2-297">strikethrough</span><span class="sxs-lookup"><span data-stu-id="04ad2-297">strikethrough</span></span> | <span data-ttu-id="04ad2-298">~~text~~</span><span class="sxs-lookup"><span data-stu-id="04ad2-298">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="04ad2-299">无序列表</span><span class="sxs-lookup"><span data-stu-id="04ad2-299">unordered list</span></span> | <ul><li><span data-ttu-id="04ad2-300">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-300">text</span></span></li><li><span data-ttu-id="04ad2-301">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-301">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="04ad2-302">排序列表</span><span class="sxs-lookup"><span data-stu-id="04ad2-302">ordered list</span></span> | <ol><li><span data-ttu-id="04ad2-303">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-303">text</span></span></li><li><span data-ttu-id="04ad2-304">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-304">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="04ad2-305">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="04ad2-305">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="04ad2-306">blockquote</span><span class="sxs-lookup"><span data-stu-id="04ad2-306">blockquote</span></span> | <blockquote><span data-ttu-id="04ad2-307">text</span><span class="sxs-lookup"><span data-stu-id="04ad2-307">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="04ad2-308">超链接</span><span class="sxs-lookup"><span data-stu-id="04ad2-308">hyperlink</span></span> | [<span data-ttu-id="04ad2-309">必应</span><span class="sxs-lookup"><span data-stu-id="04ad2-309">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="04ad2-310">图像链接</span><span class="sxs-lookup"><span data-stu-id="04ad2-310">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="04ad2-311">简单卡片的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="04ad2-311">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="04ad2-312">由于桌面平台和移动平台的分辨率差异，桌面版和移动版 Teams 的格式不同。</span><span class="sxs-lookup"><span data-stu-id="04ad2-312">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="04ad2-313">在桌面上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="04ad2-313">On the desktop, HTML formatting appears like this:</span></span>

![桌面客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="04ad2-315">在 iOS 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="04ad2-315">On iOS, HTML formatting appears like this:</span></span>

![iOS 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="04ad2-317">问题：</span><span class="sxs-lookup"><span data-stu-id="04ad2-317">Issues:</span></span>

* <span data-ttu-id="04ad2-318">粗体和 italic 等字符格式不会呈现在 iOS 上。</span><span class="sxs-lookup"><span data-stu-id="04ad2-318">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="04ad2-319">在 Android 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="04ad2-319">On Android, HTML formatting appears like this:</span></span>

![Android 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="04ad2-321">在 Android 上正确显示粗体和 italic 等字符格式。</span><span class="sxs-lookup"><span data-stu-id="04ad2-321">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="04ad2-322">简单卡片中 HTML 格式的格式设置示例</span><span class="sxs-lookup"><span data-stu-id="04ad2-322">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="04ad2-323">这些屏幕截图是使用 Teams AppStudio 创建的，其中 Hero 卡片的文本属性设置为以下字符串。</span><span class="sxs-lookup"><span data-stu-id="04ad2-323">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="04ad2-324">可以通过修改此代码在你自己的卡片中测试格式。</span><span class="sxs-lookup"><span data-stu-id="04ad2-324">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
