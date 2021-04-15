---
title: 链接展开
author: clearab
description: 如何在 Microsoft Teams 应用中使用消息传递扩展执行链接取消链接。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 628c5e760a4bc038443a20714e6960f1ffe8a2ad
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696226"
---
# <a name="link-unfurling"></a><span data-ttu-id="1888b-103">链接展开</span><span class="sxs-lookup"><span data-stu-id="1888b-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="1888b-104">本文档指导你了解如何使用 App studio 手动将链接取消点击添加到应用清单。</span><span class="sxs-lookup"><span data-stu-id="1888b-104">This document guides you on how to add link unfurling to your app manifest using App studio and manually.</span></span> <span data-ttu-id="1888b-105">使用链接展开，当粘贴某一域的 URL 到撰写消息区域，你的应用可以注册接收`invoke`活动。</span><span class="sxs-lookup"><span data-stu-id="1888b-105">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="1888b-106">包含粘贴到撰写邮件区域中的完整 URL，您可以使用用户可取消展开的卡片进行响应，从而 `invoke` 提供其他信息或操作。</span><span class="sxs-lookup"><span data-stu-id="1888b-106">The `invoke` contains the full URL that was pasted into the compose message area, and you can respond with a card that the user can unfurl, providing additional information or actions.</span></span> <span data-ttu-id="1888b-107">这类似于 URL 用作搜索词的搜索命令。</span><span class="sxs-lookup"><span data-stu-id="1888b-107">This works similar to a search command with the URL serving as the search term.</span></span>

> [!NOTE]
> <span data-ttu-id="1888b-108">目前，移动客户端不支持链接取消展开。</span><span class="sxs-lookup"><span data-stu-id="1888b-108">Currently, link unfurling is not supported on Mobile clients.</span></span>

<span data-ttu-id="1888b-109">Azure DevOps 邮件扩展使用链接取消点击查找粘贴到指向工作项的撰写邮件区域中的 URL。</span><span class="sxs-lookup"><span data-stu-id="1888b-109">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="1888b-110">在下图中，用户已粘贴 Azure DevOps 中工作项的 URL，邮件扩展已解析为卡片：</span><span class="sxs-lookup"><span data-stu-id="1888b-110">In the following image, a user has pasted a URL for a work item in Azure DevOps, which the messaging extension has resolved into a card:</span></span>

![链接取消链接示例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="1888b-112">向应用清单添加链接取消链接</span><span class="sxs-lookup"><span data-stu-id="1888b-112">Add link unfurling to your app manifest</span></span>

<span data-ttu-id="1888b-113">若要向应用清单添加链接取消链接，请向应用清单 JSON 的 部分 `messageHandlers` `composeExtensions` 添加新数组。</span><span class="sxs-lookup"><span data-stu-id="1888b-113">To add link unfurling to your app manifest, add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="1888b-114">可以在 App Studio 的帮助下或手动添加数组。</span><span class="sxs-lookup"><span data-stu-id="1888b-114">You can add the array either with the help of App Studio or manually.</span></span> <span data-ttu-id="1888b-115">域列表可以包含通配符，例如 `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="1888b-115">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="1888b-116">这完全匹配域的一个段;如果需要匹配，请使用 `a.b.example.com` `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="1888b-116">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

> [!NOTE]
> <span data-ttu-id="1888b-117">不要直接添加或通过通配符添加不在控件中的域。</span><span class="sxs-lookup"><span data-stu-id="1888b-117">Donot add domains that are not in your control, either directly or through wildcards.</span></span> <span data-ttu-id="1888b-118">例如， `yourapp.onmicrosoft.com` 有效，但 `*.onmicrosoft.com` 无效。</span><span class="sxs-lookup"><span data-stu-id="1888b-118">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span> <span data-ttu-id="1888b-119">此外，还禁止顶级域。</span><span class="sxs-lookup"><span data-stu-id="1888b-119">Also, the top-level domains are prohibited.</span></span> <span data-ttu-id="1888b-120">例如 `*.com` ，、 `*.org` 。</span><span class="sxs-lookup"><span data-stu-id="1888b-120">For example, `*.com`, `*.org`.</span></span>

### <a name="add-link-unfurling-using-app-studio"></a><span data-ttu-id="1888b-121">使用 App Studio 添加链接取消链接</span><span class="sxs-lookup"><span data-stu-id="1888b-121">Add link unfurling using App Studio</span></span>

1. <span data-ttu-id="1888b-122">从 Microsoft Teams 客户端打开 **App Studio，** 然后选择清单 **编辑器** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="1888b-122">Open **App Studio** from the Microsoft Teams client, and select the **Manifest Editor** tab.</span></span>
1. <span data-ttu-id="1888b-123">加载应用清单。</span><span class="sxs-lookup"><span data-stu-id="1888b-123">Load your app manifest.</span></span>
1. <span data-ttu-id="1888b-124">在 **"消息扩展** "页上，在"邮件处理程序"部分添加 **要查找的** 域。</span><span class="sxs-lookup"><span data-stu-id="1888b-124">On the **Messaging Extension** page, add the domain that you want to look for in the **Message handlers** section.</span></span> <span data-ttu-id="1888b-125">下图说明了此过程：</span><span class="sxs-lookup"><span data-stu-id="1888b-125">The following image explains the process:</span></span>

    ![App Studio 中的邮件处理程序部分](~/assets/images/link-unfurling.png)
    
### <a name="add-link-unfurling-manually"></a><span data-ttu-id="1888b-127">手动添加链接取消链接</span><span class="sxs-lookup"><span data-stu-id="1888b-127">Add link unfurling manually</span></span>

<span data-ttu-id="1888b-128">若要使邮件扩展能够与链接进行交互，首先必须将 `messageHandlers` 数组添加到应用清单。</span><span class="sxs-lookup"><span data-stu-id="1888b-128">To enable your messaging extension to interact with links, first you must add the `messageHandlers` array to your app manifest.</span></span> <span data-ttu-id="1888b-129">以下示例说明如何手动添加链接取消链接：</span><span class="sxs-lookup"><span data-stu-id="1888b-129">The following example explains how to add link unfurling manually:</span></span> 


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

<span data-ttu-id="1888b-130">有关完整的清单示例，请参阅 [清单参考](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="1888b-130">For a complete manifest example, see [manifest reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="1888b-131">处理 `composeExtension/queryLink` 调用</span><span class="sxs-lookup"><span data-stu-id="1888b-131">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="1888b-132">将域添加到应用程序清单后，必须更新 Web 服务代码以处理调用请求。</span><span class="sxs-lookup"><span data-stu-id="1888b-132">After adding the domain to the app manifest, you must update your web service code to handle the invoke request.</span></span> <span data-ttu-id="1888b-133">使用收到的 URL 搜索服务并创建卡片响应。</span><span class="sxs-lookup"><span data-stu-id="1888b-133">Use the received URL to search your service and create a card response.</span></span> <span data-ttu-id="1888b-134">如果使用多张卡片进行响应，则仅使用第一个卡片响应。</span><span class="sxs-lookup"><span data-stu-id="1888b-134">If you respond with more than one card, only the first card response is used.</span></span>

<span data-ttu-id="1888b-135">支持以下卡片类型：</span><span class="sxs-lookup"><span data-stu-id="1888b-135">The following card types are supported:</span></span>

* [<span data-ttu-id="1888b-136">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="1888b-136">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="1888b-137">Hero card</span><span class="sxs-lookup"><span data-stu-id="1888b-137">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="1888b-138">Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="1888b-138">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="1888b-139">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="1888b-139">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

### <a name="example"></a><span data-ttu-id="1888b-140">示例</span><span class="sxs-lookup"><span data-stu-id="1888b-140">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="1888b-141">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="1888b-141">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="1888b-142">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="1888b-142">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="1888b-143">JSON</span><span class="sxs-lookup"><span data-stu-id="1888b-143">JSON</span></span>](#tab/json)

<span data-ttu-id="1888b-144">下面是发送到 `invoke` 自动程序的示例：</span><span class="sxs-lookup"><span data-stu-id="1888b-144">Following is an example of the `invoke` sent to your bot:</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="1888b-145">下面是一个响应示例：</span><span class="sxs-lookup"><span data-stu-id="1888b-145">Following is an example of the response:</span></span>

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
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
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

## <a name="see-also"></a><span data-ttu-id="1888b-146">另请参阅</span><span class="sxs-lookup"><span data-stu-id="1888b-146">See also</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="1888b-147">什么是卡片</span><span class="sxs-lookup"><span data-stu-id="1888b-147">What are cards</span></span>](~/task-modules-and-cards/what-are-cards.md)
