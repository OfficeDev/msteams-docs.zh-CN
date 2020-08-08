---
title: 链接展开
author: clearab
description: 如何在 Microsoft 团队应用中使用邮件扩展功能执行链接 unfurling。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 32d19fcd44f2475047539350706d2745aeec3691
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587802"
---
# <a name="link-unfurling"></a><span data-ttu-id="6ecb1-103">链接展开</span><span class="sxs-lookup"><span data-stu-id="6ecb1-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> <span data-ttu-id="6ecb1-104">目前，移动客户端上不支持链接 unfurling。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-104">Currently, Link unfurling is not supported on Mobile clients.</span></span>

<span data-ttu-id="6ecb1-105">通过链接 unfurling `invoke` 如果将特定域的 url 粘贴到撰写邮件区域中，应用可以注册接收活动。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-105">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="6ecb1-106">`invoke`将包含粘贴到撰写邮件区域中的完整 URL，您可以使用用户可以*unfurl*的卡片进行响应，并提供其他信息或操作。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-106">The `invoke` will contain the full URL that was pasted into the compose message area, and you can respond with a card the user can *unfurl*, providing additional information or actions.</span></span> <span data-ttu-id="6ecb1-107">此操作的工作方式与[搜索命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)非常相似，URL 充当搜索词。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-107">This works very similarly to a [search command](~/messaging-extensions/how-to/search-commands/define-search-command.md), with the URL serving as the search term.</span></span>

<span data-ttu-id="6ecb1-108">Azure DevOps 消息扩展使用 link unfurling 查找粘贴到指向工作项的撰写邮件区域中的 Url。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-108">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="6ecb1-109">在下面的屏幕截图中，用户已将 Azure DevOps 中的工作项的 URL 粘贴到邮件扩展已解析为卡片。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-109">In the screenshot below, a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Link unfurling 的示例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="6ecb1-111">向您的应用程序清单添加链接 unfurling</span><span class="sxs-lookup"><span data-stu-id="6ecb1-111">Add link unfurling to your app manifest</span></span>

<span data-ttu-id="6ecb1-112">为此，您需要将新的 `messageHandlers` 数组添加到 `composeExtensions` 应用程序清单 JSON 的部分。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-112">To do this you'll add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="6ecb1-113">您可以使用应用程序 Studio 的帮助或手动执行此操作。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-113">You can either do so with the help of App Studio, or manually.</span></span> <span data-ttu-id="6ecb1-114">例如，域列表可以包含通配符 `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-114">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="6ecb1-115">这与域的一段完全匹配;如果需要匹配， `a.b.example.com` 请使用 `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-115">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

### <a name="using-app-studio"></a><span data-ttu-id="6ecb1-116">使用 App Studio</span><span class="sxs-lookup"><span data-stu-id="6ecb1-116">Using App Studio</span></span>

1. <span data-ttu-id="6ecb1-117">在应用程序 Studio 中，在 "清单编辑器" 选项卡上，加载您的应用程序清单。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-117">In App Studio, on the Manifest editor tab, load your app manifest.</span></span>
1. <span data-ttu-id="6ecb1-118">在 "**邮件扩展**" 页上，在 "**邮件处理程序**" 部分添加要查找的域，如下面的屏幕截图所示。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-118">On the **Messaging Extension** page, add the domain you want to look for in the **Message handlers** section as in the screenshot below.</span></span>

![应用程序 Studio 中的 "邮件处理程序" 部分](~/assets/images/link-unfurling.png)

### <a name="manually"></a><span data-ttu-id="6ecb1-120">手动</span><span class="sxs-lookup"><span data-stu-id="6ecb1-120">Manually</span></span>

<span data-ttu-id="6ecb1-121">若要使您的邮件扩展能够与链接进行交互，这种方法首先需要将该 `messageHandlers` 数组添加到应用程序清单中，如以下示例中所示。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-121">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below.</span></span> <span data-ttu-id="6ecb1-122">本示例不是完整的清单，请参阅[清单参考](~/resources/schema/manifest-schema.md)，了解完整的清单示例。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-122">This example is not the complete manifest, see [manifest reference](~/resources/schema/manifest-schema.md) for a complete manifest example.</span></span>

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

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="6ecb1-123">处理 `composeExtension/queryLink` 调用</span><span class="sxs-lookup"><span data-stu-id="6ecb1-123">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="6ecb1-124">在添加了要侦听应用程序清单的域之后，您需要更新 web 服务代码以处理调用请求。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-124">Once you've added the domain to listen on to the app manifest, you'll need to update your web service code to handle the invoke request.</span></span> <span data-ttu-id="6ecb1-125">使用您收到的 URL 搜索您的服务并创建卡片响应。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-125">Use the URL you receive to search your service and create a card response.</span></span> <span data-ttu-id="6ecb1-126">如果使用多个卡进行响应，将仅使用第一个。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-126">If you respond with more than one card, only the first will be used.</span></span>

<span data-ttu-id="6ecb1-127">我们支持以下卡类型：</span><span class="sxs-lookup"><span data-stu-id="6ecb1-127">We support the following card types:</span></span>

* [<span data-ttu-id="6ecb1-128">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="6ecb1-128">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="6ecb1-129">英雄卡片</span><span class="sxs-lookup"><span data-stu-id="6ecb1-129">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="6ecb1-130">Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="6ecb1-130">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="6ecb1-131">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="6ecb1-131">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="6ecb1-132">有关概述，请参阅[什么是卡片](~/task-modules-and-cards/what-are-cards.md)。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-132">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6ecb1-133">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6ecb1-133">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6ecb1-134">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6ecb1-134">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="6ecb1-135">JSON</span><span class="sxs-lookup"><span data-stu-id="6ecb1-135">JSON</span></span>](#tab/json)

<span data-ttu-id="6ecb1-136">这是 `invoke` 发送到你的 bot 的一个示例。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-136">This is an example of the `invoke` sent to your bot.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="6ecb1-137">响应的示例如下所示。</span><span class="sxs-lookup"><span data-stu-id="6ecb1-137">An example of the response is shown below.</span></span>

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
