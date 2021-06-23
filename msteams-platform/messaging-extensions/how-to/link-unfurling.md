---
title: 链接展开
author: surbhigupta
description: 如何在应用程序应用中使用消息传递扩展Microsoft Teams链接。
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 7713fe794c9d15453438cfe3e1bde0238bde9d8c
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068946"
---
# <a name="link-unfurling"></a><span data-ttu-id="5afda-103">链接展开</span><span class="sxs-lookup"><span data-stu-id="5afda-103">Link unfurling</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="5afda-104">本文档指导你了解如何使用 App studio 手动将链接取消点击添加到应用清单。</span><span class="sxs-lookup"><span data-stu-id="5afda-104">This document guides you on how to add link unfurling to your app manifest using App studio and manually.</span></span> <span data-ttu-id="5afda-105">使用链接展开，当粘贴某一域的 URL 到撰写消息区域，你的应用可以注册接收`invoke`活动。</span><span class="sxs-lookup"><span data-stu-id="5afda-105">With link unfurling your app can register to receive an `invoke` activity when URLs with a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="5afda-106">包含粘贴到撰写邮件区域中的完整 URL，您可以使用用户可取消展开的卡片进行响应，从而 `invoke` 提供其他信息或操作。</span><span class="sxs-lookup"><span data-stu-id="5afda-106">The `invoke` contains the full URL that was pasted into the compose message area, and you can respond with a card that the user can unfurl, providing additional information or actions.</span></span> <span data-ttu-id="5afda-107">这类似于 URL 用作搜索词的搜索命令。</span><span class="sxs-lookup"><span data-stu-id="5afda-107">This works similar to a search command with the URL serving as the search term.</span></span>

> [!NOTE]
> * <span data-ttu-id="5afda-108">目前，移动客户端不支持链接取消展开。</span><span class="sxs-lookup"><span data-stu-id="5afda-108">Currently, link unfurling is not supported on Mobile clients.</span></span>
> * <span data-ttu-id="5afda-109">链接取消点击结果缓存 30 分钟。</span><span class="sxs-lookup"><span data-stu-id="5afda-109">The link unfurling result is cached for 30 minutes.</span></span>

<span data-ttu-id="5afda-110">邮件Azure DevOps扩展使用链接取消链接查找粘贴到指向工作项的撰写邮件区域中的 URL。</span><span class="sxs-lookup"><span data-stu-id="5afda-110">The Azure DevOps messaging extension uses link unfurling to look for URLs pasted into the compose message area pointing to a work item.</span></span> <span data-ttu-id="5afda-111">在下图中，用户已粘贴邮件扩展已解析为Azure DevOps中工作项的 URL：</span><span class="sxs-lookup"><span data-stu-id="5afda-111">In the following image, a user has pasted a URL for a work item in Azure DevOps, which the messaging extension has resolved into a card:</span></span>

![链接取消链接示例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a><span data-ttu-id="5afda-113">向应用清单添加链接取消链接</span><span class="sxs-lookup"><span data-stu-id="5afda-113">Add link unfurling to your app manifest</span></span>

<span data-ttu-id="5afda-114">若要向应用清单添加链接取消链接，请向应用清单 JSON 的 部分 `messageHandlers` `composeExtensions` 添加新数组。</span><span class="sxs-lookup"><span data-stu-id="5afda-114">To add link unfurling to your app manifest, add a new `messageHandlers` array to the `composeExtensions` section of your app manifest JSON.</span></span> <span data-ttu-id="5afda-115">可以在 App Studio 的帮助下或手动添加数组。</span><span class="sxs-lookup"><span data-stu-id="5afda-115">You can add the array either with the help of App Studio or manually.</span></span> <span data-ttu-id="5afda-116">域列表可以包含通配符，例如 `*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="5afda-116">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="5afda-117">这完全匹配域的一个段;如果需要匹配，请使用 `a.b.example.com` `*.*.example.com` 。</span><span class="sxs-lookup"><span data-stu-id="5afda-117">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span>

> [!NOTE]
> <span data-ttu-id="5afda-118">不要直接添加或通过通配符添加不在控件中的域。</span><span class="sxs-lookup"><span data-stu-id="5afda-118">Donot add domains that are not in your control, either directly or through wildcards.</span></span> <span data-ttu-id="5afda-119">例如， `yourapp.onmicrosoft.com` 有效，但 `*.onmicrosoft.com` 无效。</span><span class="sxs-lookup"><span data-stu-id="5afda-119">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span> <span data-ttu-id="5afda-120">此外，还禁止顶级域。</span><span class="sxs-lookup"><span data-stu-id="5afda-120">Also, the top-level domains are prohibited.</span></span> <span data-ttu-id="5afda-121">例如 `*.com` ，、 `*.org` 。</span><span class="sxs-lookup"><span data-stu-id="5afda-121">For example, `*.com`, `*.org`.</span></span>

### <a name="add-link-unfurling-using-app-studio"></a><span data-ttu-id="5afda-122">使用 App Studio 添加链接取消链接</span><span class="sxs-lookup"><span data-stu-id="5afda-122">Add link unfurling using App Studio</span></span>

1. <span data-ttu-id="5afda-123">从 **客户端** 打开 App Studio Microsoft Teams，然后选择"**清单编辑器"** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="5afda-123">Open **App Studio** from the Microsoft Teams client, and select the **Manifest Editor** tab.</span></span>
1. <span data-ttu-id="5afda-124">加载应用清单。</span><span class="sxs-lookup"><span data-stu-id="5afda-124">Load your app manifest.</span></span>
1. <span data-ttu-id="5afda-125">在 **"消息扩展** "页上，在"邮件处理程序"部分添加 **要查找的** 域。</span><span class="sxs-lookup"><span data-stu-id="5afda-125">On the **Messaging Extension** page, add the domain that you want to look for in the **Message handlers** section.</span></span> <span data-ttu-id="5afda-126">下图说明了此过程：</span><span class="sxs-lookup"><span data-stu-id="5afda-126">The following image explains the process:</span></span>

    ![App Studio 中的邮件处理程序部分](~/assets/images/link-unfurling.png)
    
### <a name="add-link-unfurling-manually"></a><span data-ttu-id="5afda-128">手动添加链接取消链接</span><span class="sxs-lookup"><span data-stu-id="5afda-128">Add link unfurling manually</span></span>

<span data-ttu-id="5afda-129">若要使邮件扩展能够与链接进行交互，首先必须将 `messageHandlers` 数组添加到应用清单。</span><span class="sxs-lookup"><span data-stu-id="5afda-129">To enable your messaging extension to interact with links, first you must add the `messageHandlers` array to your app manifest.</span></span> <span data-ttu-id="5afda-130">以下示例说明如何手动添加链接取消链接：</span><span class="sxs-lookup"><span data-stu-id="5afda-130">The following example explains how to add link unfurling manually:</span></span> 


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

<span data-ttu-id="5afda-131">有关完整的清单示例，请参阅 [清单参考](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="5afda-131">For a complete manifest example, see [manifest reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="handle-the-composeextensionquerylink-invoke"></a><span data-ttu-id="5afda-132">处理 `composeExtension/queryLink` 调用</span><span class="sxs-lookup"><span data-stu-id="5afda-132">Handle the `composeExtension/queryLink` invoke</span></span>

<span data-ttu-id="5afda-133">将域添加到应用程序清单后，必须更新 Web 服务代码以处理调用请求。</span><span class="sxs-lookup"><span data-stu-id="5afda-133">After adding the domain to the app manifest, you must update your web service code to handle the invoke request.</span></span> <span data-ttu-id="5afda-134">使用收到的 URL 搜索服务并创建卡片响应。</span><span class="sxs-lookup"><span data-stu-id="5afda-134">Use the received URL to search your service and create a card response.</span></span> <span data-ttu-id="5afda-135">如果使用多张卡片进行响应，则仅使用第一个卡片响应。</span><span class="sxs-lookup"><span data-stu-id="5afda-135">If you respond with more than one card, only the first card response is used.</span></span>

<span data-ttu-id="5afda-136">支持以下卡片类型：</span><span class="sxs-lookup"><span data-stu-id="5afda-136">The following card types are supported:</span></span>

* [<span data-ttu-id="5afda-137">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="5afda-137">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="5afda-138">Hero card</span><span class="sxs-lookup"><span data-stu-id="5afda-138">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="5afda-139">Office 365连接器卡</span><span class="sxs-lookup"><span data-stu-id="5afda-139">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="5afda-140">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="5afda-140">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

### <a name="example"></a><span data-ttu-id="5afda-141">示例</span><span class="sxs-lookup"><span data-stu-id="5afda-141">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="5afda-142">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="5afda-142">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="5afda-143">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="5afda-143">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="5afda-144">JSON</span><span class="sxs-lookup"><span data-stu-id="5afda-144">JSON</span></span>](#tab/json)

<span data-ttu-id="5afda-145">下面是发送到 `invoke` 自动程序的示例：</span><span class="sxs-lookup"><span data-stu-id="5afda-145">Following is an example of the `invoke` sent to your bot:</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="5afda-146">下面是一个响应示例：</span><span class="sxs-lookup"><span data-stu-id="5afda-146">Following is an example of the response:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="5afda-147">另请参阅</span><span class="sxs-lookup"><span data-stu-id="5afda-147">See also</span></span> 

* [<span data-ttu-id="5afda-148">卡</span><span class="sxs-lookup"><span data-stu-id="5afda-148">Cards</span></span>](~/task-modules-and-cards/what-are-cards.md)
* [<span data-ttu-id="5afda-149">选项卡链接展开和阶段视图</span><span class="sxs-lookup"><span data-stu-id="5afda-149">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)
