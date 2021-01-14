---
title: 链接展开
author: clearab
description: 如何在 Microsoft Teams 应用中使用消息传递扩展执行链接取消链接。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 0d488638e63b8ec78bfa5bed8cf6f4f037883fb1
ms.sourcegitcommit: bf61ae5ad2afa4efdb0311158184d0cbb9c40174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2021
ms.locfileid: "49845635"
---
# <a name="link-unfurling"></a><span data-ttu-id="2be56-103">链接展开</span><span class="sxs-lookup"><span data-stu-id="2be56-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> <span data-ttu-id="2be56-104">目前，移动客户端不支持链接取消链接。</span><span class="sxs-lookup"><span data-stu-id="2be56-104">Currently, Link unfurling is not supported on Mobile clients.</span></span>

<span data-ttu-id="2be56-105">通过取消链接，应用可以注册以在将特定域的 URL 粘贴到撰写邮件区域中时 `invoke` 接收活动。</span><span class="sxs-lookup"><span data-stu-id="2be56-105">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="2be56-106">将包含粘贴到撰写邮件区域中的完整 URL，您可以使用用户可以取消展开的卡片进行响应，从而 `invoke` 提供其他信息或操作。</span><span class="sxs-lookup"><span data-stu-id="2be56-106">The `invoke` will contain the full URL that was pasted into the compose message area, and you can respond with a card the user can *unfurl*, providing additional information or actions.</span></span> <span data-ttu-id="2be56-107">这非常类似于搜索 [命令，URL](~/messaging-extensions/how-to/search-commands/define-search-command.md)充当搜索词。</span><span class="sxs-lookup"><span data-stu-id="2be56-107">This works very similarly to a [search command](~/messaging-extensions/how-to/search-commands/define-search-command.md), with the URL serving as the search term.</span></span>

<span data-ttu-id="2be56-108">Azure DevOps 邮件扩展使用链接取消链接查找粘贴到指向工作项的撰写邮件区域中的 URL。</span><span class="sxs-lookup"><span data-stu-id="2be56-108">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="2be56-109">在下面屏幕截图中，用户已粘贴 Azure DevOps 中某个工作项的 URL，邮件扩展已解析为卡片。</span><span class="sxs-lookup"><span data-stu-id="2be56-109">In the screenshot below, a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![链接取消链接示例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="2be56-111">向应用清单添加链接取消链接</span><span class="sxs-lookup"><span data-stu-id="2be56-111">Add link unfurling to your app manifest</span></span>

 <span data-ttu-id="2be56-112">若要向应用清单添加链接，请向应用清单 `messageHandlers` `composeExtensions` JSON 部分添加新数组。</span><span class="sxs-lookup"><span data-stu-id="2be56-112">To add link unfurling to your app manifest add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="2be56-113">可以在 App Studio 的帮助下或手动添加数组。</span><span class="sxs-lookup"><span data-stu-id="2be56-113">You can add the array either with the help of App Studio or manually.</span></span> <span data-ttu-id="2be56-114">域列表可以包括通配符，例如 `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="2be56-114">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="2be56-115">这完全匹配域的一个段;如果需要匹配，请使用 `a.b.example.com` `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="2be56-115">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

> [!NOTE]
> <span data-ttu-id="2be56-116">不要直接添加或通过通配符添加超出控件的域。</span><span class="sxs-lookup"><span data-stu-id="2be56-116">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="2be56-117">例如，yourapp.onmicrosoft.com有效，但 \*.onmicrosoft.com 为 无效。</span><span class="sxs-lookup"><span data-stu-id="2be56-117">For example, yourapp.onmicrosoft.com is valid, but \*.onmicrosoft.com is not valid.</span></span> <span data-ttu-id="2be56-118">此外，还禁止顶级域。</span><span class="sxs-lookup"><span data-stu-id="2be56-118">Also, the top-level domains are prohibited.</span></span> <span data-ttu-id="2be56-119">例如*.com、*.org。</span><span class="sxs-lookup"><span data-stu-id="2be56-119">For example, \*.com, \*.org.</span></span>

### <a name="using-app-studio"></a><span data-ttu-id="2be56-120">使用 App Studio</span><span class="sxs-lookup"><span data-stu-id="2be56-120">Using App Studio</span></span>

1. <span data-ttu-id="2be56-121">在 App Studio 的清单编辑器选项卡上，加载应用清单。</span><span class="sxs-lookup"><span data-stu-id="2be56-121">In App Studio, on the Manifest editor tab, load your app manifest.</span></span>
1. <span data-ttu-id="2be56-122">在 **"消息扩展**"页上，在"邮件处理程序"部分添加要查找的域，如下面的屏幕截图所示。</span><span class="sxs-lookup"><span data-stu-id="2be56-122">On the **Messaging Extension** page, add the domain you want to look for in the **Message handlers** section as in the screenshot below.</span></span>

![App Studio 中的邮件处理程序部分](~/assets/images/link-unfurling.png)

### <a name="manually"></a><span data-ttu-id="2be56-124">手动</span><span class="sxs-lookup"><span data-stu-id="2be56-124">Manually</span></span>

<span data-ttu-id="2be56-125">若要使邮件扩展可以这样与链接进行交互，你首先需要将数组添加到应用清单， `messageHandlers` 如以下示例所示。</span><span class="sxs-lookup"><span data-stu-id="2be56-125">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below.</span></span> <span data-ttu-id="2be56-126">此示例不是完整的清单 [，请参阅完整](~/resources/schema/manifest-schema.md) 清单示例的清单参考。</span><span class="sxs-lookup"><span data-stu-id="2be56-126">This example is not the complete manifest, see [manifest reference](~/resources/schema/manifest-schema.md) for a complete manifest example.</span></span>

```json
...
"composeExtensions": [
  {
    "botId": "abc123456-ab12-ab12-ab12-abcdef123456",
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "*.trackeddomain.com"
          ]
        }
      }
    ]
  }
],
...
```

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="2be56-127">处理 `composeExtension/queryLink` 调用</span><span class="sxs-lookup"><span data-stu-id="2be56-127">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="2be56-128">添加域以侦听应用程序清单后，需要更新 Web 服务代码以处理调用请求。</span><span class="sxs-lookup"><span data-stu-id="2be56-128">Once you've added the domain to listen on to the app manifest, you'll need to update your web service code to handle the invoke request.</span></span> <span data-ttu-id="2be56-129">使用收到的 URL 搜索服务并创建卡片响应。</span><span class="sxs-lookup"><span data-stu-id="2be56-129">Use the URL you receive to search your service and create a card response.</span></span> <span data-ttu-id="2be56-130">如果使用多张卡片进行响应，则仅使用第一张。</span><span class="sxs-lookup"><span data-stu-id="2be56-130">If you respond with more than one card, only the first will be used.</span></span>

<span data-ttu-id="2be56-131">我们支持以下卡片类型：</span><span class="sxs-lookup"><span data-stu-id="2be56-131">We support the following card types:</span></span>

* [<span data-ttu-id="2be56-132">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="2be56-132">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="2be56-133">Hero 卡片</span><span class="sxs-lookup"><span data-stu-id="2be56-133">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="2be56-134">Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="2be56-134">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="2be56-135">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="2be56-135">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="2be56-136">有关 [概述，请参阅什么是](~/task-modules-and-cards/what-are-cards.md) 卡片。</span><span class="sxs-lookup"><span data-stu-id="2be56-136">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="2be56-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="2be56-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsAppBasedLinkQueryAsync(ITurnContext<IInvokeActivity> turnContext, AppBasedLinkQuery query, CancellationToken cancellationToken)
{
    //You'll use the query.link value to search your service and create a card response
    var card = new HeroCard
    {
        Title = "Hero Card",
        Text = query.Url,
        Images = new List<CardImage> { new CardImage("https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png") },
    };

    var attachments = new MessagingExtensionAttachment(HeroCard.ContentType, null, card);
    var result = new MessagingExtensionResult(AttachmentLayoutTypes.List, "result", new[] { attachments }, null, "test unfurl");

    return new MessagingExtensionResponse(result);
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="2be56-138">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="2be56-138">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsLinkUnfurlingBot extends TeamsActivityHandler {
  handleTeamsAppBasedLinkQuery(context, query) {
    const attachment = CardFactory.thumbnailCard('Thumbnail Card',
      query.url,
      ['https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png']);

    const result = {
      attachmentLayout: 'list',
      type: 'result',
      attachments: [attachment]
    };

    const response = {
      composeExtension: result
    };
    return response;
  }
}
```

# <a name="json"></a>[<span data-ttu-id="2be56-139">JSON</span><span class="sxs-lookup"><span data-stu-id="2be56-139">JSON</span></span>](#tab/json)

<span data-ttu-id="2be56-140">这是发送到机器人 `invoke` 的示例。</span><span class="sxs-lookup"><span data-stu-id="2be56-140">This is an example of the `invoke` sent to your bot.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="2be56-141">下面显示了一个响应示例。</span><span class="sxs-lookup"><span data-stu-id="2be56-141">An example of the response is shown below.</span></span>

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "attachments": [
      {
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        }
      }
    ]
  }
}
```

* * *
