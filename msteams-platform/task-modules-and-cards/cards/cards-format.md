---
title: 卡片中的文本格式
description: 介绍卡片文本格式Microsoft Teams
keywords: teams 自动程序卡格式
localization_priority: Normal
ms.topic: reference
ms.date: 03/29/2018
ms.openlocfilehash: 877a16f884e91138dc656434438a5fe1dd2ffd6e
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140590"
---
# <a name="format-cards-in-microsoft-teams"></a><span data-ttu-id="a4642-104">格式化卡片Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a4642-104">Format cards in Microsoft Teams</span></span>

<span data-ttu-id="a4642-105">以下是向卡片添加格式文本格式的两种方法：</span><span class="sxs-lookup"><span data-stu-id="a4642-105">Following are the two ways to add rich text formatting to your cards:</span></span>
* [<span data-ttu-id="a4642-106">Markdown</span><span class="sxs-lookup"><span data-stu-id="a4642-106">Markdown</span></span>](#format-cards-with-markdown)
* [<span data-ttu-id="a4642-107">HTML</span><span class="sxs-lookup"><span data-stu-id="a4642-107">HTML</span></span>](#format-cards-with-html)

<span data-ttu-id="a4642-108">卡片仅支持文本属性中的格式设置，不支持标题或副标题属性中的格式设置。</span><span class="sxs-lookup"><span data-stu-id="a4642-108">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="a4642-109">可以使用 XML 或 HTML 格式的子集或 Markdown 指定格式，具体取决于卡片类型。</span><span class="sxs-lookup"><span data-stu-id="a4642-109">Formatting can be specified using a subset of XML or HTML formatting or Markdown, depending on the card type.</span></span> <span data-ttu-id="a4642-110">对于自适应卡片的当前和未来开发，建议使用 Markdown 格式。</span><span class="sxs-lookup"><span data-stu-id="a4642-110">For current and future development of Adaptive Cards, Markdown formatting is recommended.</span></span>

<span data-ttu-id="a4642-111">卡片类型之间的格式支持不同。</span><span class="sxs-lookup"><span data-stu-id="a4642-111">Formatting support differs between card types.</span></span> <span data-ttu-id="a4642-112">桌面版和移动版客户端之间的卡片呈现可能略有不同Microsoft Teams客户端，Teams在桌面浏览器中呈现。</span><span class="sxs-lookup"><span data-stu-id="a4642-112">Rendering of the card can differ slightly between the desktop and the mobile Microsoft Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="a4642-113">你可以将内联图像与任意卡片Teams内。</span><span class="sxs-lookup"><span data-stu-id="a4642-113">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="a4642-114">图像的格式可以设置为 、 或 文件，并且不能超过 `.png` `.jpg` `.gif` 1024 像素× 1024 像素或 1 MB。</span><span class="sxs-lookup"><span data-stu-id="a4642-114">Images can be formatted as `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="a4642-115">不支持动态 GIF。</span><span class="sxs-lookup"><span data-stu-id="a4642-115">Animated GIF is not supported.</span></span> <span data-ttu-id="a4642-116">有关详细信息，请参阅 [卡片类型](./cards-reference.md#inline-card-images)。</span><span class="sxs-lookup"><span data-stu-id="a4642-116">For more information, see [types of cards](./cards-reference.md#inline-card-images).</span></span>

<span data-ttu-id="a4642-117">可以使用 Markdown 格式化自适应卡片Office 365连接器卡，其中包括某些受支持的样式。</span><span class="sxs-lookup"><span data-stu-id="a4642-117">You can format Adaptive Cards and Office 365 Connector cards with Markdown that include certain supported styles.</span></span>

## <a name="format-cards-with-markdown"></a><span data-ttu-id="a4642-118">使用 Markdown 格式化卡片</span><span class="sxs-lookup"><span data-stu-id="a4642-118">Format cards with Markdown</span></span>

<span data-ttu-id="a4642-119">以下卡片类型支持 Markdown 格式Teams：</span><span class="sxs-lookup"><span data-stu-id="a4642-119">The following card types support Markdown formatting in Teams:</span></span>

* <span data-ttu-id="a4642-120">自适应卡片：自适应卡片字段以及 和 中都支持 `Textblock` `Fact.Title` `Fact.Value` Markdown。</span><span class="sxs-lookup"><span data-stu-id="a4642-120">Adaptive Cards: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="a4642-121">自适应卡片不支持 HTML。</span><span class="sxs-lookup"><span data-stu-id="a4642-121">HTML is not supported in Adaptive Cards.</span></span>
* <span data-ttu-id="a4642-122">O365 连接器卡：文本字段中的 O365 连接器卡支持 Markdown 和有限的 HTML。</span><span class="sxs-lookup"><span data-stu-id="a4642-122">O365 Connector cards: Markdown and limited HTML is supported in O365 Connector cards in the text fields.</span></span>

<span data-ttu-id="a4642-123">你可以将新行用于自适应卡片，或者对列表中新行使用转 `\r` `\n` 义序列。</span><span class="sxs-lookup"><span data-stu-id="a4642-123">You can use newlines for Adaptive Cards using `\r` or `\n` escape sequences for newlines in lists.</span></span> <span data-ttu-id="a4642-124">适用于自适应卡片的桌面版和移动版Teams不同。</span><span class="sxs-lookup"><span data-stu-id="a4642-124">Formatting is different between the desktop and the mobile versions of Teams for Adaptive Cards.</span></span> <span data-ttu-id="a4642-125">Web、桌面和移动客户端支持基于卡片的提及。</span><span class="sxs-lookup"><span data-stu-id="a4642-125">Card-based mentions are supported in web, desktop, and mobile clients.</span></span> <span data-ttu-id="a4642-126">可以使用信息屏蔽属性来屏蔽特定信息，如自适应卡片输入元素内用户的密码或 `Input.Text` 敏感信息。</span><span class="sxs-lookup"><span data-stu-id="a4642-126">You can use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive Card `Input.Text` input element.</span></span> <span data-ttu-id="a4642-127">可以使用 对象扩展自适应卡片 `width` 的宽度。</span><span class="sxs-lookup"><span data-stu-id="a4642-127">You can expand the width of an Adaptive Card using the `width` object.</span></span> <span data-ttu-id="a4642-128">可以在自适应卡片中启用 typeahead 支持，在用户键入输入时筛选输入选项集。</span><span class="sxs-lookup"><span data-stu-id="a4642-128">You can enable typeahead support within Adaptive Cards and filter the set of input choices as the user types the input.</span></span> <span data-ttu-id="a4642-129">可以使用 属性 `msteams` 添加选择性地在阶段视图中显示图像的能力。</span><span class="sxs-lookup"><span data-stu-id="a4642-129">You can use the `msteams` property to add the ability to display images in stage view selectively.</span></span>

<span data-ttu-id="a4642-130">对于自适应卡片和连接器卡，桌面版和移动版Teams不同。</span><span class="sxs-lookup"><span data-stu-id="a4642-130">Formatting is different between the desktop and the mobile versions of Teams for Adaptive Cards and connector cards.</span></span> <span data-ttu-id="a4642-131">在此部分中，你可以浏览自适应卡片和连接器卡的 Markdown 格式示例。</span><span class="sxs-lookup"><span data-stu-id="a4642-131">In this section, you can go through the Markdown format example for Adaptive Cards and connector cards.</span></span>

# <a name="markdown-format-for-adaptive-cards"></a>[<span data-ttu-id="a4642-132">自适应卡片的 Markdown 格式</span><span class="sxs-lookup"><span data-stu-id="a4642-132">Markdown format for Adaptive Cards</span></span>](#tab/adaptive-md)

 <span data-ttu-id="a4642-133">下表提供了 、 和 `Textblock` 支持的 `Fact.Title` 样式 `Fact.Value` ：</span><span class="sxs-lookup"><span data-stu-id="a4642-133">The following table provides the supported styles for `Textblock`, `Fact.Title`, and `Fact.Value`:</span></span>

| <span data-ttu-id="a4642-134">样式</span><span class="sxs-lookup"><span data-stu-id="a4642-134">Style</span></span> | <span data-ttu-id="a4642-135">示例</span><span class="sxs-lookup"><span data-stu-id="a4642-135">Example</span></span> | <span data-ttu-id="a4642-136">Markdown</span><span class="sxs-lookup"><span data-stu-id="a4642-136">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a4642-137">粗体</span><span class="sxs-lookup"><span data-stu-id="a4642-137">Bold</span></span> | <span data-ttu-id="a4642-138">**Bold**</span><span class="sxs-lookup"><span data-stu-id="a4642-138">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="a4642-139">斜体</span><span class="sxs-lookup"><span data-stu-id="a4642-139">Italic</span></span> | <span data-ttu-id="a4642-140">_Italic_</span><span class="sxs-lookup"><span data-stu-id="a4642-140">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="a4642-141">未排序列表</span><span class="sxs-lookup"><span data-stu-id="a4642-141">Unordered list</span></span> | <ul><li><span data-ttu-id="a4642-142">text</span><span class="sxs-lookup"><span data-stu-id="a4642-142">text</span></span></li><li><span data-ttu-id="a4642-143">text</span><span class="sxs-lookup"><span data-stu-id="a4642-143">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="a4642-144">已排序列表</span><span class="sxs-lookup"><span data-stu-id="a4642-144">Ordered list</span></span> | <ol><li><span data-ttu-id="a4642-145">text</span><span class="sxs-lookup"><span data-stu-id="a4642-145">text</span></span></li><li><span data-ttu-id="a4642-146">text</span><span class="sxs-lookup"><span data-stu-id="a4642-146">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="a4642-147">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="a4642-147">Hyperlinks</span></span> |[<span data-ttu-id="a4642-148">必应</span><span class="sxs-lookup"><span data-stu-id="a4642-148">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="a4642-149">不支持以下 Markdown 标记：</span><span class="sxs-lookup"><span data-stu-id="a4642-149">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="a4642-150">标头</span><span class="sxs-lookup"><span data-stu-id="a4642-150">Headers</span></span>
* <span data-ttu-id="a4642-151">表格</span><span class="sxs-lookup"><span data-stu-id="a4642-151">Tables</span></span>
* <span data-ttu-id="a4642-152">图像</span><span class="sxs-lookup"><span data-stu-id="a4642-152">Images</span></span>
* <span data-ttu-id="a4642-153">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="a4642-153">Preformatted text</span></span>
* <span data-ttu-id="a4642-154">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="a4642-154">Blockquotes</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="a4642-155">自适应卡片的新行</span><span class="sxs-lookup"><span data-stu-id="a4642-155">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="a4642-156">可以将 或 `\r` `\n` 转义序列用于列表中新行。</span><span class="sxs-lookup"><span data-stu-id="a4642-156">You can use the `\r` or `\n` escape sequences for newlines in lists.</span></span> <span data-ttu-id="a4642-157">在 `\n\n` 列表中使用 会导致列表中的下一个元素缩进。</span><span class="sxs-lookup"><span data-stu-id="a4642-157">Using `\n\n` in lists causes the next element in the list to be indented.</span></span> <span data-ttu-id="a4642-158">如果需要 TextBlock 中其他位置的 newlines，请使用 `\n\n` 。</span><span class="sxs-lookup"><span data-stu-id="a4642-158">If you require newlines elsewhere in the TextBlock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="a4642-159">自适应卡片的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="a4642-159">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="a4642-160">在桌面上，自适应卡片 Markdown 格式显示如下图所示，在 Web 浏览器和 Teams 应用程序中：</span><span class="sxs-lookup"><span data-stu-id="a4642-160">On the desktop, Adaptive Card Markdown formatting appears as shown in the following image in both web browsers and in the Teams client application:</span></span>

![桌面客户端中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="a4642-162">在 iOS 上，自适应卡片 Markdown 格式显示如下图所示：</span><span class="sxs-lookup"><span data-stu-id="a4642-162">On iOS, Adaptive Card Markdown formatting appears as shown in the following image:</span></span>

![iOS 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="a4642-164">在 Android 上，自适应卡片 Markdown 格式显示如下图所示：</span><span class="sxs-lookup"><span data-stu-id="a4642-164">On Android, Adaptive Card Markdown formatting appears as shown in the following image:</span></span>

![Android 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-Android.png)

<span data-ttu-id="a4642-166">有关详细信息，请参阅自适应 [卡片中的文本功能](/adaptive-cards/create/textfeatures)。</span><span class="sxs-lookup"><span data-stu-id="a4642-166">For more information, see [text features in Adaptive Cards](/adaptive-cards/create/textfeatures).</span></span>

> [!NOTE]
> <span data-ttu-id="a4642-167">本节中提到的日期和本地化功能在 Teams。</span><span class="sxs-lookup"><span data-stu-id="a4642-167">The date and localization features mentioned in this section are not supported in Teams.</span></span>

### <a name="adaptive-cards-format-sample"></a><span data-ttu-id="a4642-168">自适应卡片格式示例</span><span class="sxs-lookup"><span data-stu-id="a4642-168">Adaptive Cards format sample</span></span>

<span data-ttu-id="a4642-169">以下代码显示了自适应卡片格式设置的示例：</span><span class="sxs-lookup"><span data-stu-id="a4642-169">The following code shows an example of Adaptive Cards formatting:</span></span>

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

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="a4642-170">自适应卡片 v1.2 中的提及支持</span><span class="sxs-lookup"><span data-stu-id="a4642-170">Mention support within Adaptive Cards v1.2</span></span>

<span data-ttu-id="a4642-171">你可以将@mentions自动程序和消息传递扩展响应的自适应卡片正文中。</span><span class="sxs-lookup"><span data-stu-id="a4642-171">You can add @mentions within an Adaptive Card body for bots and messaging extension responses.</span></span> <span data-ttu-id="a4642-172">若要在@mentions，请遵循与频道和群聊对话中基于消息的提及相同的通知 [逻辑和呈现](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)。</span><span class="sxs-lookup"><span data-stu-id="a4642-172">To add @mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions).</span></span>

<span data-ttu-id="a4642-173">聊天机器人和消息传递扩展可以在 [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 和 [FactSet](https://adaptivecards.io/explorer/FactSet.html) 元素的卡片内容中包括提及。</span><span class="sxs-lookup"><span data-stu-id="a4642-173">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="a4642-174">[媒体元素](https://adaptivecards.io/explorer/Media.html)当前在 Teams 平台上的自适应卡片 v1.2 中不受支持。</span><span class="sxs-lookup"><span data-stu-id="a4642-174">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive Cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="a4642-175">机器人消息不支持频道和团队提及。</span><span class="sxs-lookup"><span data-stu-id="a4642-175">Channel and team mentions are not supported in bot messages.</span></span>

<span data-ttu-id="a4642-176">若要在自适应卡片中包括提及，你的应用需要包括以下元素：</span><span class="sxs-lookup"><span data-stu-id="a4642-176">To include a mention in an Adaptive Card, your app needs to include the following elements:</span></span>

* <span data-ttu-id="a4642-177">`<at>username</at>` 在支持的自适应卡片元素中。</span><span class="sxs-lookup"><span data-stu-id="a4642-177">`<at>username</at>` in the supported Adaptive Card elements.</span></span>
* <span data-ttu-id="a4642-178">`mention`卡片内容 `msteams` 中属性内的对象包括Teams的用户 ID。</span><span class="sxs-lookup"><span data-stu-id="a4642-178">The `mention` object inside of an `msteams` property in the card content includes the Teams user ID of the user being mentioned.</span></span>
* <span data-ttu-id="a4642-179">`userId`是自动程序 ID 和特定用户所特有的。</span><span class="sxs-lookup"><span data-stu-id="a4642-179">The `userId` is unique to your bot ID and a particular user.</span></span> <span data-ttu-id="a4642-180">它可用于@mention用户。</span><span class="sxs-lookup"><span data-stu-id="a4642-180">It can be used to @mention a particular user.</span></span> <span data-ttu-id="a4642-181">`userId`可以使用获取用户 ID 中提到的选项之[一来检索](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id)。</span><span class="sxs-lookup"><span data-stu-id="a4642-181">The `userId` can be retrieved using one of the options mentioned in [get the user ID](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id).</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="a4642-182">带提及功能的示例自适应卡片</span><span class="sxs-lookup"><span data-stu-id="a4642-182">Sample Adaptive Card with a mention</span></span>

<span data-ttu-id="a4642-183">以下代码显示了带提及功能自适应卡片的示例：</span><span class="sxs-lookup"><span data-stu-id="a4642-183">The following code shows an example of Adaptive Card with a mention:</span></span>

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

### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="a4642-184">自适应卡片中的信息屏蔽</span><span class="sxs-lookup"><span data-stu-id="a4642-184">Information masking in Adaptive Cards</span></span>

<span data-ttu-id="a4642-185">使用信息屏蔽属性可以屏蔽特定信息，如自适应卡片输入元素内用户的密码或 [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) 敏感信息。</span><span class="sxs-lookup"><span data-stu-id="a4642-185">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive Card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span>

> [!NOTE]
> <span data-ttu-id="a4642-186">该功能仅支持客户端信息屏蔽。</span><span class="sxs-lookup"><span data-stu-id="a4642-186">The feature only supports client side information masking.</span></span> <span data-ttu-id="a4642-187">将屏蔽的输入文本作为纯文本发送到在机器人配置期间指定的 HTTPS [终结点地址](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint)。</span><span class="sxs-lookup"><span data-stu-id="a4642-187">The masked input text is sent as clear text to the HTTPS endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint).</span></span>

<span data-ttu-id="a4642-188">若要屏蔽自适应卡片中的信息，请 `isMasked` 添加属性以 **键入** `Input.Text` ，将其值设置为 **true**。</span><span class="sxs-lookup"><span data-stu-id="a4642-188">To mask information in Adaptive Cards, add the `isMasked` property to **type** `Input.Text`, and set its value to **true**.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="a4642-189">带屏蔽属性的示例自适应卡片</span><span class="sxs-lookup"><span data-stu-id="a4642-189">Sample Adaptive Card with masking property</span></span>

<span data-ttu-id="a4642-190">以下代码显示了具有屏蔽属性的自适应卡片的示例：</span><span class="sxs-lookup"><span data-stu-id="a4642-190">The following code shows an example of Adaptive Card with masking property:</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
},
```

<span data-ttu-id="a4642-191">下图是自适应卡片中屏蔽信息的示例：</span><span class="sxs-lookup"><span data-stu-id="a4642-191">The following image is an example of masking information in Adaptive Cards:</span></span>

![屏蔽信息图像](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="a4642-193">全宽自适应卡片</span><span class="sxs-lookup"><span data-stu-id="a4642-193">Full width Adaptive Card</span></span>

<span data-ttu-id="a4642-194">可以使用 属性扩展自适应卡片的宽度， `msteams` 并充分利用额外的画布空间。</span><span class="sxs-lookup"><span data-stu-id="a4642-194">You can use the `msteams` property to expand the width of an Adaptive Card and make use of additional canvas space.</span></span> <span data-ttu-id="a4642-195">下一节将提供有关如何使用 属性的信息。</span><span class="sxs-lookup"><span data-stu-id="a4642-195">The next section provides information on how to use the property.</span></span>

#### <a name="construct-full-width-cards"></a><span data-ttu-id="a4642-196">构造全宽卡片</span><span class="sxs-lookup"><span data-stu-id="a4642-196">Construct full width cards</span></span>

<span data-ttu-id="a4642-197">若要制作全宽自适应卡片，卡片内容 `width` 中的 `msteams` 属性中的 对象必须设置为 `Full` 。</span><span class="sxs-lookup"><span data-stu-id="a4642-197">To make a full width Adaptive Card, the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="a4642-198">全宽自适应卡片示例</span><span class="sxs-lookup"><span data-stu-id="a4642-198">Sample Adaptive Card with full width</span></span>

<span data-ttu-id="a4642-199">若要制作全宽自适应卡片，你的应用必须包含以下代码示例中的元素：</span><span class="sxs-lookup"><span data-stu-id="a4642-199">To make a full width Adaptive Card, your app must include the elements from the following code sample:</span></span>

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

<span data-ttu-id="a4642-200">下图显示了全宽自适应卡片：</span><span class="sxs-lookup"><span data-stu-id="a4642-200">The following image shows a full width Adaptive Card:</span></span>

![全宽自适应卡片视图](../../assets/images/cards/full-width-adaptive-card.png)

<span data-ttu-id="a4642-202">下图显示自适应卡片的默认视图，当你未将 属性设置为 `width` **Full 时**：</span><span class="sxs-lookup"><span data-stu-id="a4642-202">The following image shows the default view of the Adaptive Card when you have not set the `width` property to **Full**:</span></span>

![小宽度自适应卡片视图](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a><span data-ttu-id="a4642-204">Typeahead 支持</span><span class="sxs-lookup"><span data-stu-id="a4642-204">Typeahead support</span></span>

<span data-ttu-id="a4642-205">在 schema 元素中，要求用户筛选和选择大量选项会显著降低 [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) 任务完成速度。</span><span class="sxs-lookup"><span data-stu-id="a4642-205">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter and select a sizeable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="a4642-206">自适应卡片中的 Typeahead 支持可以在用户键入输入时缩小或筛选输入选项集，从而简化输入选择。</span><span class="sxs-lookup"><span data-stu-id="a4642-206">Typeahead support within Adaptive Cards can simplify input selection by narrowing or filtering the set of input choices as the user types the input.</span></span>

<span data-ttu-id="a4642-207">若要在 中启用 `Input.Choiceset` typeahead，请设置为 `style` `filtered` ，并确保 `isMultiSelect` 设置为 `false` 。</span><span class="sxs-lookup"><span data-stu-id="a4642-207">To enable typeahead within the `Input.Choiceset`, set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span>

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="a4642-208">具有字头支持的示例自适应卡片</span><span class="sxs-lookup"><span data-stu-id="a4642-208">Sample Adaptive Card with typeahead support</span></span>

<span data-ttu-id="a4642-209">以下代码显示了具有 typeahead 支持的自适应卡片的示例：</span><span class="sxs-lookup"><span data-stu-id="a4642-209">The following code shows an example of Adaptive Card with typeahead support:</span></span>

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

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="a4642-210">自适应卡片中的图像阶段视图</span><span class="sxs-lookup"><span data-stu-id="a4642-210">Stage view for images in Adaptive Cards</span></span>

<span data-ttu-id="a4642-211">在自适应卡片中，可以使用 属性添加选择性地在阶段 `msteams` 视图中显示图像的能力。</span><span class="sxs-lookup"><span data-stu-id="a4642-211">In an Adaptive Card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="a4642-212">当用户将鼠标悬停在图像上时，他们可以看到展开图标，其 `allowExpand` 属性设置为 `true` 。</span><span class="sxs-lookup"><span data-stu-id="a4642-212">When users hover over the images, they can see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="a4642-213">有关如何使用 属性的信息，请参阅以下示例：</span><span class="sxs-lookup"><span data-stu-id="a4642-213">For information on how to use the property, see the following example:</span></span>

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

<span data-ttu-id="a4642-214">当用户将鼠标悬停在图像上方时，右上角将显示展开图标，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="a4642-214">When users hover over the image, an expand icon appears at the top right corner as shown in the following image:</span></span>

![带可展开图像的自适应卡片](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

<span data-ttu-id="a4642-216">当用户选择展开图标时，图像将显示在阶段视图中，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="a4642-216">The image appears in stage view when the user selects the expand icon as shown in the following image:</span></span>

![展开到阶段视图的图像](../../assets/images/cards/adaptivecard-expand-image.png)

<span data-ttu-id="a4642-218">在阶段视图中，用户可以放大和缩小图像。</span><span class="sxs-lookup"><span data-stu-id="a4642-218">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="a4642-219">可以在自适应卡片中选择必须具有此功能的图像。</span><span class="sxs-lookup"><span data-stu-id="a4642-219">You can select the images in your Adaptive Card that must have this capability.</span></span>

> [!NOTE]
> * <span data-ttu-id="a4642-220">放大和缩小功能仅适用于自适应卡片中的图像类型图像元素。</span><span class="sxs-lookup"><span data-stu-id="a4642-220">Zoom in and zoom out capability applies only to the image elements that is image type in an Adaptive Card.</span></span>
> * <span data-ttu-id="a4642-221">对于Teams应用，自适应卡片中的图像阶段视图功能默认可用。</span><span class="sxs-lookup"><span data-stu-id="a4642-221">For Teams mobile apps, stage view functionality for images in Adaptive Cards is available by default.</span></span> <span data-ttu-id="a4642-222">用户只需点击图像即可在阶段视图中查看自适应卡片图像，无论属性 `allowExpand` 是否存在。</span><span class="sxs-lookup"><span data-stu-id="a4642-222">Users can view Adaptive Card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-format-for-o365-connector-cards"></a>[<span data-ttu-id="a4642-223">O365 连接器卡的 Markdown 格式</span><span class="sxs-lookup"><span data-stu-id="a4642-223">Markdown format for O365 Connector cards</span></span>](#tab/connector-md)

<span data-ttu-id="a4642-224">连接器卡支持有限的 Markdown 和 HTML 格式。</span><span class="sxs-lookup"><span data-stu-id="a4642-224">Connector cards support limited Markdown and HTML formatting.</span></span>

| <span data-ttu-id="a4642-225">样式</span><span class="sxs-lookup"><span data-stu-id="a4642-225">Style</span></span> | <span data-ttu-id="a4642-226">示例</span><span class="sxs-lookup"><span data-stu-id="a4642-226">Example</span></span> | <span data-ttu-id="a4642-227">Markdown</span><span class="sxs-lookup"><span data-stu-id="a4642-227">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a4642-228">粗体</span><span class="sxs-lookup"><span data-stu-id="a4642-228">Bold</span></span> | <span data-ttu-id="a4642-229">**text**</span><span class="sxs-lookup"><span data-stu-id="a4642-229">**text**</span></span> | `**text**` |
| <span data-ttu-id="a4642-230">斜体</span><span class="sxs-lookup"><span data-stu-id="a4642-230">Italic</span></span> | <span data-ttu-id="a4642-231">*text*</span><span class="sxs-lookup"><span data-stu-id="a4642-231">*text*</span></span> | `*text*` |
| <span data-ttu-id="a4642-232">页眉 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="a4642-232">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="a4642-233">**Text**</span><span class="sxs-lookup"><span data-stu-id="a4642-233">**Text**</span></span> | `### Text`|
| <span data-ttu-id="a4642-234">删除线</span><span class="sxs-lookup"><span data-stu-id="a4642-234">Strikethrough</span></span> | <span data-ttu-id="a4642-235">~~text~~</span><span class="sxs-lookup"><span data-stu-id="a4642-235">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="a4642-236">未排序列表</span><span class="sxs-lookup"><span data-stu-id="a4642-236">Unordered list</span></span> | <ul><li><span data-ttu-id="a4642-237">text</span><span class="sxs-lookup"><span data-stu-id="a4642-237">text</span></span></li><li><span data-ttu-id="a4642-238">text</span><span class="sxs-lookup"><span data-stu-id="a4642-238">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="a4642-239">已排序列表</span><span class="sxs-lookup"><span data-stu-id="a4642-239">Ordered list</span></span> | <ol><li><span data-ttu-id="a4642-240">text</span><span class="sxs-lookup"><span data-stu-id="a4642-240">text</span></span></li><li><span data-ttu-id="a4642-241">text</span><span class="sxs-lookup"><span data-stu-id="a4642-241">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="a4642-242">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="a4642-242">Preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="a4642-243">Blockquote</span><span class="sxs-lookup"><span data-stu-id="a4642-243">Blockquote</span></span> | <span data-ttu-id="a4642-244">>blockquote 文本</span><span class="sxs-lookup"><span data-stu-id="a4642-244">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="a4642-245">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="a4642-245">Hyperlink</span></span> | [<span data-ttu-id="a4642-246">必应</span><span class="sxs-lookup"><span data-stu-id="a4642-246">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="a4642-247">图像链接</span><span class="sxs-lookup"><span data-stu-id="a4642-247">Image link</span></span> |![在一个地心上闪避](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="a4642-249">在连接器卡中，为 呈现新行 `\n\n` ，但不为 或 `\n` 呈现 `\r` 。</span><span class="sxs-lookup"><span data-stu-id="a4642-249">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards"></a><span data-ttu-id="a4642-250">连接器卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="a4642-250">Mobile and desktop differences for connector cards</span></span>

<span data-ttu-id="a4642-251">在桌面上，连接器卡的 Markdown 格式显示如下图所示：</span><span class="sxs-lookup"><span data-stu-id="a4642-251">On the desktop, Markdown formatting for connector cards appears as shown in the following image:</span></span>

![桌面客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="a4642-253">在 iOS 上，连接器卡的 Markdown 格式将显示，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="a4642-253">On iOS, Markdown formatting for connector cards appears as shown in the following image:</span></span>

![iOS 客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="a4642-255">使用 Markdown for iOS 的连接器卡包括以下问题：</span><span class="sxs-lookup"><span data-stu-id="a4642-255">Connector cards using Markdown for iOS include the following issues:</span></span>

* <span data-ttu-id="a4642-256">iOS 客户端用于Teams连接器卡中呈现 Markdown 或 HTML 内嵌图像。</span><span class="sxs-lookup"><span data-stu-id="a4642-256">The iOS client for Teams does not render Markdown or HTML inline images in connector cards.</span></span>
* <span data-ttu-id="a4642-257">Blockquotes 呈现为缩进，但不带灰色背景。</span><span class="sxs-lookup"><span data-stu-id="a4642-257">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="a4642-258">在 Android 上，连接器卡的 Markdown 格式显示如下图所示：</span><span class="sxs-lookup"><span data-stu-id="a4642-258">On Android, Markdown formatting for connector cards appears as shown in the following image:</span></span>

![Android 客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="format-example-for-markdown-connector-cards"></a><span data-ttu-id="a4642-260">Markdown 连接器卡的格式示例</span><span class="sxs-lookup"><span data-stu-id="a4642-260">Format example for Markdown connector cards</span></span>

<span data-ttu-id="a4642-261">以下代码显示了 Markdown 连接器卡的格式设置示例：</span><span class="sxs-lookup"><span data-stu-id="a4642-261">The following code shows an example of formatting for Markdown connector cards:</span></span>

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

## <a name="format-cards-with-html"></a><span data-ttu-id="a4642-262">使用 HTML 格式化卡片</span><span class="sxs-lookup"><span data-stu-id="a4642-262">Format cards with HTML</span></span>

<span data-ttu-id="a4642-263">以下卡片类型支持 HTML 格式Teams：</span><span class="sxs-lookup"><span data-stu-id="a4642-263">The following card types support HTML formatting in Teams:</span></span>

* <span data-ttu-id="a4642-264">O365 连接器卡：连接器卡支持有限的 Markdown 和 HTML Office 365格式。</span><span class="sxs-lookup"><span data-stu-id="a4642-264">O365 Connector cards: Limited Markdown and HTML formatting is supported in Office 365 Connector cards.</span></span>
* <span data-ttu-id="a4642-265">Hero 和 thumbnail cards：简单卡片支持 HTML 标记，例如 hero 和 thumbnail 卡片。</span><span class="sxs-lookup"><span data-stu-id="a4642-265">Hero and thumbnail cards: HTML tags are supported for simple cards, such as the hero and thumbnail cards.</span></span>

<span data-ttu-id="a4642-266">适用于 O365 连接器卡和简单卡片的桌面和移动Teams格式不同。</span><span class="sxs-lookup"><span data-stu-id="a4642-266">Formatting is different between the desktop and the mobile versions of Teams for O365 Connector cards and simple cards.</span></span> <span data-ttu-id="a4642-267">在此部分中，您可以浏览连接器卡和简单卡片的 HTML 格式示例。</span><span class="sxs-lookup"><span data-stu-id="a4642-267">In this section, you can go through the HTML format example for connector cards and simple cards.</span></span>

# <a name="html-format-for-o365-connector-cards"></a>[<span data-ttu-id="a4642-268">O365 连接器卡的 HTML 格式</span><span class="sxs-lookup"><span data-stu-id="a4642-268">HTML format for O365 Connector cards</span></span>](#tab/connector-html)

<span data-ttu-id="a4642-269">连接器卡支持有限的 Markdown 和 HTML 格式。</span><span class="sxs-lookup"><span data-stu-id="a4642-269">Connector cards support limited Markdown and HTML formatting.</span></span>

| <span data-ttu-id="a4642-270">样式</span><span class="sxs-lookup"><span data-stu-id="a4642-270">Style</span></span> | <span data-ttu-id="a4642-271">示例</span><span class="sxs-lookup"><span data-stu-id="a4642-271">Example</span></span> | <span data-ttu-id="a4642-272">HTML</span><span class="sxs-lookup"><span data-stu-id="a4642-272">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a4642-273">粗体</span><span class="sxs-lookup"><span data-stu-id="a4642-273">Bold</span></span> | <span data-ttu-id="a4642-274">**text**</span><span class="sxs-lookup"><span data-stu-id="a4642-274">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="a4642-275">斜体</span><span class="sxs-lookup"><span data-stu-id="a4642-275">Italic</span></span> | <span data-ttu-id="a4642-276">*text*</span><span class="sxs-lookup"><span data-stu-id="a4642-276">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="a4642-277">页眉 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="a4642-277">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="a4642-278">**Text**</span><span class="sxs-lookup"><span data-stu-id="a4642-278">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="a4642-279">删除线</span><span class="sxs-lookup"><span data-stu-id="a4642-279">Strikethrough</span></span> | <span data-ttu-id="a4642-280">~~text~~</span><span class="sxs-lookup"><span data-stu-id="a4642-280">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="a4642-281">未排序列表</span><span class="sxs-lookup"><span data-stu-id="a4642-281">Unordered list</span></span> | <ul><li><span data-ttu-id="a4642-282">text</span><span class="sxs-lookup"><span data-stu-id="a4642-282">text</span></span></li><li><span data-ttu-id="a4642-283">text</span><span class="sxs-lookup"><span data-stu-id="a4642-283">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="a4642-284">已排序列表</span><span class="sxs-lookup"><span data-stu-id="a4642-284">Ordered list</span></span> | <ol><li><span data-ttu-id="a4642-285">text</span><span class="sxs-lookup"><span data-stu-id="a4642-285">text</span></span></li><li><span data-ttu-id="a4642-286">text</span><span class="sxs-lookup"><span data-stu-id="a4642-286">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="a4642-287">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="a4642-287">Preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="a4642-288">Blockquote</span><span class="sxs-lookup"><span data-stu-id="a4642-288">Blockquote</span></span> | <blockquote><span data-ttu-id="a4642-289">text</span><span class="sxs-lookup"><span data-stu-id="a4642-289">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="a4642-290">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="a4642-290">Hyperlink</span></span> | [<span data-ttu-id="a4642-291">必应</span><span class="sxs-lookup"><span data-stu-id="a4642-291">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="a4642-292">图像链接</span><span class="sxs-lookup"><span data-stu-id="a4642-292">Image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="a4642-293">在连接器卡中，使用 标记以 HTML 格式呈现 `<p>` 新行。</span><span class="sxs-lookup"><span data-stu-id="a4642-293">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards"></a><span data-ttu-id="a4642-294">连接器卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="a4642-294">Mobile and desktop differences for connector cards</span></span>

<span data-ttu-id="a4642-295">在桌面上，连接器卡的 HTML 格式将显示，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="a4642-295">On the desktop, HTML formatting for connector cards appears as shown in the following image:</span></span>

![桌面客户端中连接器卡的 HTML 格式](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="a4642-297">在 iOS 上，HTML 格式显示如下图所示：</span><span class="sxs-lookup"><span data-stu-id="a4642-297">On iOS, HTML formatting appears as shown in the following image:</span></span>

![iOS 客户端中连接器卡的 HTML 格式](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="a4642-299">使用 HTML for iOS 的连接器卡包括以下问题：</span><span class="sxs-lookup"><span data-stu-id="a4642-299">Connector cards using HTML for iOS include the following issues:</span></span>

* <span data-ttu-id="a4642-300">内联图像不会在 iOS 上使用 Markdown 或 HTML 在连接器卡上呈现。</span><span class="sxs-lookup"><span data-stu-id="a4642-300">Inline images are not rendered on iOS using either Markdown or HTML in connector cards.</span></span>
* <span data-ttu-id="a4642-301">呈现预设格式的文本，但没有灰色背景。</span><span class="sxs-lookup"><span data-stu-id="a4642-301">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="a4642-302">在 Android 上，HTML 格式显示如下图所示：</span><span class="sxs-lookup"><span data-stu-id="a4642-302">On Android, HTML formatting appears as shown in the following image:</span></span>

![Android 客户端中连接器卡的 HTML 格式](../../assets/images/cards/connector-android-html-combined.png)

### <a name="format-sample-for-html-connector-cards"></a><span data-ttu-id="a4642-304">HTML 连接器卡的格式示例</span><span class="sxs-lookup"><span data-stu-id="a4642-304">Format sample for HTML connector cards</span></span>

<span data-ttu-id="a4642-305">以下代码显示了 HTML 连接器卡的格式设置示例：</span><span class="sxs-lookup"><span data-stu-id="a4642-305">The following code shows an example of formatting for HTML connector cards:</span></span>

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

# <a name="html-format-for-hero-and-thumbnail-cards"></a>[<span data-ttu-id="a4642-306">Hero 和缩略图卡片的 HTML 格式</span><span class="sxs-lookup"><span data-stu-id="a4642-306">HTML format for hero and thumbnail cards</span></span>](#tab/simple-html)

<span data-ttu-id="a4642-307">简单卡片支持 HTML 标记，例如 hero 和 thumbnail 卡片。</span><span class="sxs-lookup"><span data-stu-id="a4642-307">HTML tags are supported for simple cards, such as the hero and thumbnail cards.</span></span> <span data-ttu-id="a4642-308">不支持 Markdown。</span><span class="sxs-lookup"><span data-stu-id="a4642-308">Markdown is not supported.</span></span>

| <span data-ttu-id="a4642-309">样式</span><span class="sxs-lookup"><span data-stu-id="a4642-309">Style</span></span> | <span data-ttu-id="a4642-310">示例</span><span class="sxs-lookup"><span data-stu-id="a4642-310">Example</span></span> | <span data-ttu-id="a4642-311">HTML</span><span class="sxs-lookup"><span data-stu-id="a4642-311">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a4642-312">粗体</span><span class="sxs-lookup"><span data-stu-id="a4642-312">Bold</span></span> | <span data-ttu-id="a4642-313">**text**</span><span class="sxs-lookup"><span data-stu-id="a4642-313">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="a4642-314">斜体</span><span class="sxs-lookup"><span data-stu-id="a4642-314">Italic</span></span> | <span data-ttu-id="a4642-315">*text*</span><span class="sxs-lookup"><span data-stu-id="a4642-315">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="a4642-316">页眉 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="a4642-316">Header (levels 1&ndash;3)</span></span> | <span data-ttu-id="a4642-317">**Text**</span><span class="sxs-lookup"><span data-stu-id="a4642-317">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="a4642-318">删除线</span><span class="sxs-lookup"><span data-stu-id="a4642-318">Strikethrough</span></span> | <span data-ttu-id="a4642-319">~~text~~</span><span class="sxs-lookup"><span data-stu-id="a4642-319">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="a4642-320">未排序列表</span><span class="sxs-lookup"><span data-stu-id="a4642-320">Unordered list</span></span> | <ul><li><span data-ttu-id="a4642-321">text</span><span class="sxs-lookup"><span data-stu-id="a4642-321">text</span></span></li><li><span data-ttu-id="a4642-322">text</span><span class="sxs-lookup"><span data-stu-id="a4642-322">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="a4642-323">已排序列表</span><span class="sxs-lookup"><span data-stu-id="a4642-323">Ordered list</span></span> | <ol><li><span data-ttu-id="a4642-324">text</span><span class="sxs-lookup"><span data-stu-id="a4642-324">text</span></span></li><li><span data-ttu-id="a4642-325">text</span><span class="sxs-lookup"><span data-stu-id="a4642-325">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="a4642-326">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="a4642-326">Preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="a4642-327">Blockquote</span><span class="sxs-lookup"><span data-stu-id="a4642-327">Blockquote</span></span> | <blockquote><span data-ttu-id="a4642-328">text</span><span class="sxs-lookup"><span data-stu-id="a4642-328">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="a4642-329">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="a4642-329">Hyperlink</span></span> | [<span data-ttu-id="a4642-330">必应</span><span class="sxs-lookup"><span data-stu-id="a4642-330">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="a4642-331">图像链接</span><span class="sxs-lookup"><span data-stu-id="a4642-331">Image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="a4642-332">简单卡片的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="a4642-332">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="a4642-333">由于桌面平台和移动平台之间存在解决方案差异，因此桌面和移动设备版本之间的格式设置Teams。</span><span class="sxs-lookup"><span data-stu-id="a4642-333">As there are resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="a4642-334">在桌面上，HTML 格式显示如下图所示：</span><span class="sxs-lookup"><span data-stu-id="a4642-334">On the desktop, HTML formatting appears as shown in the following image:</span></span>

![桌面客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="a4642-336">在 iOS 上，HTML 格式显示如下图所示：</span><span class="sxs-lookup"><span data-stu-id="a4642-336">On iOS, HTML formatting appears as shown in the following image:</span></span>

![iOS 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="a4642-338">字符格式（如粗体和 italic）不会呈现在 iOS 上。</span><span class="sxs-lookup"><span data-stu-id="a4642-338">Character formatting, such as bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="a4642-339">在 Android 上，HTML 格式显示如下图所示：</span><span class="sxs-lookup"><span data-stu-id="a4642-339">On Android, HTML formatting appears as shown in the following image:</span></span>

![Android 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="a4642-341">字符格式，如在 Android 上正确显示粗体和 italic。</span><span class="sxs-lookup"><span data-stu-id="a4642-341">Character formatting, such as bold and italic display correctly on Android.</span></span>

### <a name="format-example-for-simple-cards"></a><span data-ttu-id="a4642-342">简单卡片的格式示例</span><span class="sxs-lookup"><span data-stu-id="a4642-342">Format example for simple cards</span></span>

<span data-ttu-id="a4642-343">上一部分中的图像是使用 Teams **App Studio** 创建的，其中，hero 卡片的文本属性设置为以下字符串：</span><span class="sxs-lookup"><span data-stu-id="a4642-343">The images in the previous section were created using Teams **App Studio**, where the text property of a hero card is set to the following string:</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

<span data-ttu-id="a4642-344">可以通过修改此代码在你自己的卡片中测试格式。</span><span class="sxs-lookup"><span data-stu-id="a4642-344">You can test formatting in your own cards by modifying this code.</span></span>

---

## <a name="see-also"></a><span data-ttu-id="a4642-345">另请参阅</span><span class="sxs-lookup"><span data-stu-id="a4642-345">See also</span></span>

* [<span data-ttu-id="a4642-346">卡片操作</span><span class="sxs-lookup"><span data-stu-id="a4642-346">Card actions</span></span>](./cards-actions.md)
* [<span data-ttu-id="a4642-347">任务模块</span><span class="sxs-lookup"><span data-stu-id="a4642-347">Task modules</span></span>](~/task-modules-and-cards/cards/cards-format.md)
