---
title: 响应搜索命令
author: clearab
description: 如何从 Microsoft Teams 应用中的消息扩展响应搜索命令。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 4dff59d0bd923618a3079c81cbb6f9e7aea2bab4
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2021
ms.locfileid: "51996007"
---
# <a name="respond-to-search-command"></a><span data-ttu-id="022d5-103">响应搜索命令</span><span class="sxs-lookup"><span data-stu-id="022d5-103">Respond to search command</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="022d5-104">在用户提交搜索命令后，Web 服务会收到一条调用消息，其中包含包含 `composeExtension/query` `value` 搜索参数的对象。</span><span class="sxs-lookup"><span data-stu-id="022d5-104">After the user submits the search command, your web service receives a `composeExtension/query` invoke message that contains a `value` object with the search parameters.</span></span> <span data-ttu-id="022d5-105">此调用将触发，并满足以下条件：</span><span class="sxs-lookup"><span data-stu-id="022d5-105">This invoke is triggered with the following conditions:</span></span>

* <span data-ttu-id="022d5-106">在搜索框中输入字符时。</span><span class="sxs-lookup"><span data-stu-id="022d5-106">As characters are entered into the search box.</span></span>
* <span data-ttu-id="022d5-107">`initialRun` 在应用清单中设置为 true，一旦调用搜索命令，就会收到调用消息。</span><span class="sxs-lookup"><span data-stu-id="022d5-107">`initialRun` is set to true in your app manifest, you receive the invoke message as soon as the search command is invoked.</span></span> <span data-ttu-id="022d5-108">有关详细信息，请参阅默认 [查询](#default-query)。</span><span class="sxs-lookup"><span data-stu-id="022d5-108">For more information, see [default query](#default-query).</span></span>

<span data-ttu-id="022d5-109">本文档指导你了解如何以卡片和预览形式响应用户请求，以及 Microsoft Teams 发布默认查询的条件。</span><span class="sxs-lookup"><span data-stu-id="022d5-109">This document guides you on how to respond to user requests in the form of cards and previews, and the conditions under which Microsoft Teams issues a default query.</span></span>

<span data-ttu-id="022d5-110">请求参数位于请求中的 对象中 `value` ，其中包括以下属性：</span><span class="sxs-lookup"><span data-stu-id="022d5-110">The request parameters are found in the `value` object in the request, which includes the following properties:</span></span>

| <span data-ttu-id="022d5-111">属性名称</span><span class="sxs-lookup"><span data-stu-id="022d5-111">Property name</span></span> | <span data-ttu-id="022d5-112">用途</span><span class="sxs-lookup"><span data-stu-id="022d5-112">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="022d5-113">用户调用的命令的名称，与在应用清单中声明的命令之一匹配。</span><span class="sxs-lookup"><span data-stu-id="022d5-113">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="022d5-114">参数数组。</span><span class="sxs-lookup"><span data-stu-id="022d5-114">Array of parameters.</span></span> <span data-ttu-id="022d5-115">每个参数对象都包含参数名称以及用户提供的参数值。</span><span class="sxs-lookup"><span data-stu-id="022d5-115">Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="022d5-116">分页参数：</span><span class="sxs-lookup"><span data-stu-id="022d5-116">Pagination parameters:</span></span> <br><span data-ttu-id="022d5-117">`skip`：跳过此查询的计数</span><span class="sxs-lookup"><span data-stu-id="022d5-117">`skip`: Skip count for this query</span></span> <br><span data-ttu-id="022d5-118">`count`：要返回的元素数。</span><span class="sxs-lookup"><span data-stu-id="022d5-118">`count`: Number of elements to return.</span></span> |

# <a name="cnet"></a>[<span data-ttu-id="022d5-119">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="022d5-119">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="022d5-120">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="022d5-120">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="json"></a>[<span data-ttu-id="022d5-121">JSON</span><span class="sxs-lookup"><span data-stu-id="022d5-121">JSON</span></span>](#tab/json)

<span data-ttu-id="022d5-122">以下 JSON 已缩短，以突出显示最相关的部分。</span><span class="sxs-lookup"><span data-stu-id="022d5-122">The JSON below is shortened to highlight the most relevant sections.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "searchKeywords",
        "value": "Toronto"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
...
}
```

* * *

## <a name="respond-to-user-requests"></a><span data-ttu-id="022d5-123">响应用户请求</span><span class="sxs-lookup"><span data-stu-id="022d5-123">Respond to user requests</span></span>

<span data-ttu-id="022d5-124">当用户执行查询时，Microsoft Teams 会向服务发送同步 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="022d5-124">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="022d5-125">此时，代码有 `5` 几秒钟时间提供对请求的 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="022d5-125">At that point, your code has `5` seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="022d5-126">在此期间，你的服务可以执行其他查找，或执行为请求提供服务所需的任何其他业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="022d5-126">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="022d5-127">服务必须使用与用户查询匹配的结果进行响应。</span><span class="sxs-lookup"><span data-stu-id="022d5-127">Your service must respond with the results matching the user query.</span></span> <span data-ttu-id="022d5-128">该响应必须指示 的 HTTP 状态代码以及具有以下属性的有效 `200 OK` 应用程序或 JSON 对象：</span><span class="sxs-lookup"><span data-stu-id="022d5-128">The response must indicate an HTTP status code of `200 OK` and a valid application or JSON object with the following properties:</span></span>

|<span data-ttu-id="022d5-129">属性名称</span><span class="sxs-lookup"><span data-stu-id="022d5-129">Property name</span></span>|<span data-ttu-id="022d5-130">用途</span><span class="sxs-lookup"><span data-stu-id="022d5-130">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="022d5-131">顶级响应信封。</span><span class="sxs-lookup"><span data-stu-id="022d5-131">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="022d5-132">响应类型。</span><span class="sxs-lookup"><span data-stu-id="022d5-132">Type of response.</span></span> <span data-ttu-id="022d5-133">支持以下类型：</span><span class="sxs-lookup"><span data-stu-id="022d5-133">The following types are supported:</span></span> <br><span data-ttu-id="022d5-134">`result`：显示搜索结果列表</span><span class="sxs-lookup"><span data-stu-id="022d5-134">`result`: Displays a list of search results</span></span> <br><span data-ttu-id="022d5-135">`auth`：要求用户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="022d5-135">`auth`: Asks the user to authenticate</span></span> <br><span data-ttu-id="022d5-136">`config`：要求用户设置消息扩展</span><span class="sxs-lookup"><span data-stu-id="022d5-136">`config`: Asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="022d5-137">`message`：显示纯文本消息</span><span class="sxs-lookup"><span data-stu-id="022d5-137">`message`: Displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="022d5-138">指定附件的布局。</span><span class="sxs-lookup"><span data-stu-id="022d5-138">Specifies the layout of the attachments.</span></span> <span data-ttu-id="022d5-139">用于 类型 `result` 的响应。</span><span class="sxs-lookup"><span data-stu-id="022d5-139">Used for responses of type `result`.</span></span> <br><span data-ttu-id="022d5-140">目前支持以下类型：</span><span class="sxs-lookup"><span data-stu-id="022d5-140">Currently, the following types are supported:</span></span> <br><span data-ttu-id="022d5-141">`list`：包含缩略图、标题和文本字段的卡片对象列表</span><span class="sxs-lookup"><span data-stu-id="022d5-141">`list`: A list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="022d5-142">`grid`：缩略图图像的网格</span><span class="sxs-lookup"><span data-stu-id="022d5-142">`grid`: A grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="022d5-143">有效 attachment 对象的数组。</span><span class="sxs-lookup"><span data-stu-id="022d5-143">Array of valid attachment objects.</span></span> <span data-ttu-id="022d5-144">用于 类型 `result` 的响应。</span><span class="sxs-lookup"><span data-stu-id="022d5-144">Used for responses of type `result`.</span></span> <br><span data-ttu-id="022d5-145">目前支持以下类型：</span><span class="sxs-lookup"><span data-stu-id="022d5-145">Currently, the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="022d5-146">建议的操作。</span><span class="sxs-lookup"><span data-stu-id="022d5-146">Suggested actions.</span></span> <span data-ttu-id="022d5-147">用于 或 类型的 `auth` 响应 `config` 。</span><span class="sxs-lookup"><span data-stu-id="022d5-147">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="022d5-148">要显示的消息。</span><span class="sxs-lookup"><span data-stu-id="022d5-148">Message to display.</span></span> <span data-ttu-id="022d5-149">用于 类型 `message` 的响应。</span><span class="sxs-lookup"><span data-stu-id="022d5-149">Used for responses of type `message`.</span></span> |

### <a name="response-card-types-and-previews"></a><span data-ttu-id="022d5-150">响应卡类型和预览</span><span class="sxs-lookup"><span data-stu-id="022d5-150">Response card types and previews</span></span>

<span data-ttu-id="022d5-151">Teams 支持以下卡片类型：</span><span class="sxs-lookup"><span data-stu-id="022d5-151">Teams supports the following card types:</span></span>

* [<span data-ttu-id="022d5-152">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="022d5-152">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="022d5-153">Hero card</span><span class="sxs-lookup"><span data-stu-id="022d5-153">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="022d5-154">Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="022d5-154">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="022d5-155">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="022d5-155">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="022d5-156">若要更好地了解卡片并概览卡片，请参阅 [什么是卡片](~/task-modules-and-cards/what-are-cards.md)。</span><span class="sxs-lookup"><span data-stu-id="022d5-156">To have a better understanding and overview on cards, see [what are cards](~/task-modules-and-cards/what-are-cards.md).</span></span>

<span data-ttu-id="022d5-157">若要了解如何使用缩略图和 Hero 卡片类型，请参阅 [添加卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="022d5-157">To learn how to use the thumbnail and hero card types, see [add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="022d5-158">有关 Office 365 连接器卡的其他信息，请参阅使用 [Office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)。</span><span class="sxs-lookup"><span data-stu-id="022d5-158">For additional information regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="022d5-159">结果列表显示在 Microsoft Teams UI 中，并预览每个项目。</span><span class="sxs-lookup"><span data-stu-id="022d5-159">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="022d5-160">预览以以下两种方式之一生成：</span><span class="sxs-lookup"><span data-stu-id="022d5-160">The preview is generated in one of the two ways:</span></span>

* <span data-ttu-id="022d5-161">在 `preview` 对象内使用 `attachment` 属性。</span><span class="sxs-lookup"><span data-stu-id="022d5-161">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="022d5-162">附件 `preview` 只能是 Hero 或 Thumbnail 卡片。</span><span class="sxs-lookup"><span data-stu-id="022d5-162">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="022d5-163">从附件的基本 `title` 、 `text` 和 `image` 属性中提取。</span><span class="sxs-lookup"><span data-stu-id="022d5-163">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="022d5-164">只有在属性未设置且这些属性可用 `preview` 时，才使用这些属性。</span><span class="sxs-lookup"><span data-stu-id="022d5-164">These are used only if the `preview` property is not set and these properties are available.</span></span>
* <span data-ttu-id="022d5-165">预览卡片不支持 Hero 或 Thumbnail 卡片按钮和点击操作（调用除外）。</span><span class="sxs-lookup"><span data-stu-id="022d5-165">The Hero or Thumbnail card button and tap actions, except invoke, are not supported in the preview card.</span></span>

<span data-ttu-id="022d5-166">可以使用自适应卡片或 Office 365 连接器卡片的预览属性在结果列表中显示该卡片的预览。</span><span class="sxs-lookup"><span data-stu-id="022d5-166">You can display a preview of an Adaptive Card or Office 365 Connector card in the result list using its preview property.</span></span> <span data-ttu-id="022d5-167">如果结果已是 Hero 或 Thumbnail 卡片，则不需要预览属性。</span><span class="sxs-lookup"><span data-stu-id="022d5-167">The preview property is not necessary if the results are already Hero or Thumbnail cards.</span></span> <span data-ttu-id="022d5-168">如果使用预览附件，它必须是 Hero 或 Thumbnail 卡片。</span><span class="sxs-lookup"><span data-stu-id="022d5-168">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="022d5-169">如果未指定任何预览属性，则卡片预览将失败，并且不显示任何内容。</span><span class="sxs-lookup"><span data-stu-id="022d5-169">If no preview property is specified, the preview of the card fails and nothing is displayed.</span></span>

### <a name="response-example"></a><span data-ttu-id="022d5-170">响应示例</span><span class="sxs-lookup"><span data-stu-id="022d5-170">Response example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="022d5-171">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="022d5-171">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken) 
{
  var text = query?.Parameters?[0]?.Value as string ?? string.Empty;

  //searches NuGet for a package
  var obj = JObject.Parse(await (new HttpClient()).GetStringAsync($"https://azuresearch-usnc.nuget.org/query?q=id:{text}&prerelease=true"));
  var packages = obj["data"].Select(item => (item["id"].ToString(), item["version"].ToString(), item["description"].ToString()));

  // We take every row of the results and wrap them in cards wrapped in in MessagingExtensionAttachment objects.
  // The Preview is optional, if it includes a Tap, that will trigger the OnTeamsMessagingExtensionSelectItemAsync event back on this bot.
  var attachments = packages.Select(package => new MessagingExtensionAttachment
      {
          ContentType = HeroCard.ContentType,
          Content = new HeroCard { Title = package.Item1 },
          Preview = new HeroCard { Title = package.Item1, Tap = new CardAction { Type = "invoke", Value = package } }.ToAttachment()
      })
      .ToList();

  // The list of MessagingExtensionAttachments must we wrapped in a MessagingExtensionResult wrapped in a MessagingExtensionResponse.
  return new MessagingExtensionResponse
  {
      ComposeExtension = new MessagingExtensionResult
      {
          Type = "result",
          AttachmentLayout = "list",
          Attachments = attachments
      }
  };
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="022d5-172">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="022d5-172">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearchBot extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
        const searchQuery = query.parameters[0].value;
        const response = await axios.get(`http://registry.npmjs.com/-/v1/search?${ querystring.stringify({ text: searchQuery, size: 8 }) }`);

        const attachments = [];
        response.data.objects.forEach(obj => {
            const heroCard = CardFactory.heroCard(obj.package.name);
            const preview = CardFactory.heroCard(obj.package.name);
            const attachment = { ...heroCard, preview };
            attachments.push(attachment);
        });

        return {
            composeExtension: {
                type: 'result',
                attachmentLayout: 'list',
                attachments: attachments
            }
        };
    }
}
```

# <a name="json"></a>[<span data-ttu-id="022d5-173">JSON</span><span class="sxs-lookup"><span data-stu-id="022d5-173">JSON</span></span>](#tab/json)

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
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        }
      },
      {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Container",
              "items": [
                {
                  "type": "TextBlock",
                  "text": "Microsoft Corp (NASDAQ: MSFT)",
                  "size": "medium",
                  "isSubtle": true
                },
                {
                  "type": "TextBlock",
                  "text": "September 19, 4:00 PM EST",
                  "isSubtle": true
                }
              ]
            },
            {
              "type": "Container",
              "spacing": "none",
              "items": [
                {
                  "type": "ColumnSet",
                  "columns": [
                    {
                      "type": "Column",
                      "width": "stretch",
                      "items": [
                        {
                          "type": "TextBlock",
                          "text": "75.30",
                          "size": "extraLarge"
                        },
                        {
                          "type": "TextBlock",
                          "text": "▼ 0.20 (0.32%)",
                          "size": "small",
                          "color": "attention",
                          "spacing": "none"
                        }
                      ]
                    },
                    {
                      "type": "Column",
                      "width": "auto",
                      "items": [
                        {
                          "type": "FactSet",
                          "facts": [
                            {
                              "title": "Open",
                              "value": "62.24"
                            },
                            {
                              "title": "High",
                              "value": "62.98"
                            },
                            {
                              "title": "Low",
                              "value": "62.20"
                            }
                          ]
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ],
          "version": "1.0"
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "Microsoft Corp (NASDAQ: MSFT)",
            "text": "75.30 ▼ 0.20 (0.32%)"
          }
        }
      }
    ]
  }
}
```

* * *

## <a name="default-query"></a><span data-ttu-id="022d5-174">默认查询</span><span class="sxs-lookup"><span data-stu-id="022d5-174">Default query</span></span>

<span data-ttu-id="022d5-175">如果在清单中设置为 ，Microsoft Teams 将在用户首次打开消息传递扩展时发送 `initialRun` `true` 默认查询。 </span><span class="sxs-lookup"><span data-stu-id="022d5-175">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a **default** query when the user first opens the messaging extension.</span></span> <span data-ttu-id="022d5-176">你的服务可以使用一组预填充的结果来响应此查询。</span><span class="sxs-lookup"><span data-stu-id="022d5-176">Your service can respond to this query with a set of pre-populated results.</span></span> <span data-ttu-id="022d5-177">当搜索命令需要身份验证或配置、显示最近查看的项目、收藏夹或其他不依赖于用户输入的信息时，这非常有用。</span><span class="sxs-lookup"><span data-stu-id="022d5-177">This is useful when your search command requires authentication or configuration, displaying recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="022d5-178">默认查询的结构与任何常规用户查询相同，字段设置为 并设置为 `name` `initialRun` `value` `true` ，如以下对象所示：</span><span class="sxs-lookup"><span data-stu-id="022d5-178">The default query has the same structure as any regular user query, with the `name` field set to `initialRun` and `value` set to `true` as shown in the following object:</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "initialRun",
        "value": "true"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  ⋮
}
```

## <a name="code-sample"></a><span data-ttu-id="022d5-179">代码示例</span><span class="sxs-lookup"><span data-stu-id="022d5-179">Code sample</span></span>

| <span data-ttu-id="022d5-180">示例名称</span><span class="sxs-lookup"><span data-stu-id="022d5-180">Sample Name</span></span>           | <span data-ttu-id="022d5-181">说明</span><span class="sxs-lookup"><span data-stu-id="022d5-181">Description</span></span> | <span data-ttu-id="022d5-182">.NET</span><span class="sxs-lookup"><span data-stu-id="022d5-182">.NET</span></span>    | <span data-ttu-id="022d5-183">Node.js</span><span class="sxs-lookup"><span data-stu-id="022d5-183">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="022d5-184">Teams 消息传递扩展操作</span><span class="sxs-lookup"><span data-stu-id="022d5-184">Teams messaging extension action</span></span>| <span data-ttu-id="022d5-185">介绍如何定义操作命令、创建任务模块和响应任务模块提交操作。</span><span class="sxs-lookup"><span data-stu-id="022d5-185">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="022d5-186">View</span><span class="sxs-lookup"><span data-stu-id="022d5-186">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="022d5-187">View</span><span class="sxs-lookup"><span data-stu-id="022d5-187">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="022d5-188">Teams 消息传递扩展搜索</span><span class="sxs-lookup"><span data-stu-id="022d5-188">Teams messaging extension search</span></span>   |  <span data-ttu-id="022d5-189">介绍如何定义搜索命令并响应搜索。</span><span class="sxs-lookup"><span data-stu-id="022d5-189">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="022d5-190">View</span><span class="sxs-lookup"><span data-stu-id="022d5-190">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="022d5-191">View</span><span class="sxs-lookup"><span data-stu-id="022d5-191">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a><span data-ttu-id="022d5-192">另请参阅</span><span class="sxs-lookup"><span data-stu-id="022d5-192">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="022d5-193">向消息传递扩展添加配置</span><span class="sxs-lookup"><span data-stu-id="022d5-193">Add configuration to a messaging extension</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)
 
## <a name="next-step"></a><span data-ttu-id="022d5-194">后续步骤</span><span class="sxs-lookup"><span data-stu-id="022d5-194">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="022d5-195">向消息传递扩展添加身份验证</span><span class="sxs-lookup"><span data-stu-id="022d5-195">Add authentication to a messaging extension</span></span>](~/messaging-extensions/how-to/add-authentication.md)



