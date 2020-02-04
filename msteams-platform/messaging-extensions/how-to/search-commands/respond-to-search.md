---
title: 响应搜索命令
author: clearab
description: 如何在 Microsoft 团队应用中的邮件扩展中响应搜索命令。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: e8b40dd8f422ffbd2537e8fa76a38c15eb6208de
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673492"
---
# <a name="respond-to-the-search-command"></a><span data-ttu-id="68b4e-103">响应搜索命令</span><span class="sxs-lookup"><span data-stu-id="68b4e-103">Respond to the search command</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="68b4e-104">您的 web 服务将接收`composeExtension/query`包含具有搜索参数的`value`对象的调用消息。</span><span class="sxs-lookup"><span data-stu-id="68b4e-104">Your web service will receive a `composeExtension/query` invoke message that contains a `value` object with the search parameters.</span></span> <span data-ttu-id="68b4e-105">触发此调用：</span><span class="sxs-lookup"><span data-stu-id="68b4e-105">This invoke is triggered:</span></span>

* <span data-ttu-id="68b4e-106">在搜索框中输入字符时。</span><span class="sxs-lookup"><span data-stu-id="68b4e-106">As characters are entered into the search box.</span></span>
* <span data-ttu-id="68b4e-107">如果`initialRun`在应用程序清单中将设置为 true，则会在调用搜索命令后立即收到调用消息。</span><span class="sxs-lookup"><span data-stu-id="68b4e-107">If `initialRun` is set to true in your app manifest, you'll receive the invoke message as soon as the search command is invoked.</span></span> <span data-ttu-id="68b4e-108">请参阅[默认查询](#default-query)。</span><span class="sxs-lookup"><span data-stu-id="68b4e-108">See [default query](#default-query).</span></span>

<span data-ttu-id="68b4e-109">请求参数本身位于请求的`value`对象中，其中包括以下属性：</span><span class="sxs-lookup"><span data-stu-id="68b4e-109">The request parameters itself are found in the `value` object in the request, which includes the following properties:</span></span>

| <span data-ttu-id="68b4e-110">属性名称</span><span class="sxs-lookup"><span data-stu-id="68b4e-110">Property name</span></span> | <span data-ttu-id="68b4e-111">用途</span><span class="sxs-lookup"><span data-stu-id="68b4e-111">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="68b4e-112">用户调用的命令的名称，与应用程序清单中声明的命令之一相匹配。</span><span class="sxs-lookup"><span data-stu-id="68b4e-112">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="68b4e-113">参数数组。</span><span class="sxs-lookup"><span data-stu-id="68b4e-113">Array of parameters.</span></span> <span data-ttu-id="68b4e-114">每个 parameter 对象包含参数名称，以及用户提供的参数值。</span><span class="sxs-lookup"><span data-stu-id="68b4e-114">Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="68b4e-115">分页参数：</span><span class="sxs-lookup"><span data-stu-id="68b4e-115">Pagination parameters:</span></span> <br><span data-ttu-id="68b4e-116">`skip`：跳过此查询的计数</span><span class="sxs-lookup"><span data-stu-id="68b4e-116">`skip`: skip count for this query</span></span> <br><span data-ttu-id="68b4e-117">`count`：要返回的元素数</span><span class="sxs-lookup"><span data-stu-id="68b4e-117">`count`: number of elements to return</span></span> |

# <a name="cnettabdotnet"></a>[<span data-ttu-id="68b4e-118">C #/.NET</span><span class="sxs-lookup"><span data-stu-id="68b4e-118">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="68b4e-119">TypeScript/node.js</span><span class="sxs-lookup"><span data-stu-id="68b4e-119">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="68b4e-120">JSON</span><span class="sxs-lookup"><span data-stu-id="68b4e-120">JSON</span></span>](#tab/json)

<span data-ttu-id="68b4e-121">下面的 JSON 将被缩短，以突出显示最相关的部分。</span><span class="sxs-lookup"><span data-stu-id="68b4e-121">The JSON below is shortened to highlight the most relevant sections.</span></span>

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

## <a name="respond-to-user-requests"></a><span data-ttu-id="68b4e-122">响应用户请求</span><span class="sxs-lookup"><span data-stu-id="68b4e-122">Respond to user requests</span></span>

<span data-ttu-id="68b4e-123">当用户执行查询时，Microsoft 团队会向您的服务发出同步 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="68b4e-123">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="68b4e-124">在这种情况下，您的代码有5秒的时间来提供对请求的 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="68b4e-124">At that point, your code has 5 seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="68b4e-125">在这段时间内，您的服务可以执行其他查找，或提供服务请求所需的任何其他业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="68b4e-125">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="68b4e-126">您的服务应使用与用户查询匹配的结果进行响应。</span><span class="sxs-lookup"><span data-stu-id="68b4e-126">Your service should respond with the results matching the user query.</span></span> <span data-ttu-id="68b4e-127">响应必须指示 HTTP 状态代码`200 OK` ，以及具有以下正文的有效 application/json 对象：</span><span class="sxs-lookup"><span data-stu-id="68b4e-127">The response must indicate an HTTP status code of `200 OK` and a valid application/json object with the following body:</span></span>

|<span data-ttu-id="68b4e-128">属性名称</span><span class="sxs-lookup"><span data-stu-id="68b4e-128">Property name</span></span>|<span data-ttu-id="68b4e-129">用途</span><span class="sxs-lookup"><span data-stu-id="68b4e-129">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="68b4e-130">顶级响应信封。</span><span class="sxs-lookup"><span data-stu-id="68b4e-130">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="68b4e-131">响应的类型。</span><span class="sxs-lookup"><span data-stu-id="68b4e-131">Type of response.</span></span> <span data-ttu-id="68b4e-132">支持以下类型：</span><span class="sxs-lookup"><span data-stu-id="68b4e-132">The following types are supported:</span></span> <br><span data-ttu-id="68b4e-133">`result`：显示搜索结果列表</span><span class="sxs-lookup"><span data-stu-id="68b4e-133">`result`: displays a list of search results</span></span> <br><span data-ttu-id="68b4e-134">`auth`：要求用户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="68b4e-134">`auth`: asks the user to authenticate</span></span> <br><span data-ttu-id="68b4e-135">`config`：要求用户设置邮件扩展</span><span class="sxs-lookup"><span data-stu-id="68b4e-135">`config`: asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="68b4e-136">`message`：显示纯文本消息</span><span class="sxs-lookup"><span data-stu-id="68b4e-136">`message`: displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="68b4e-137">指定附件的布局。</span><span class="sxs-lookup"><span data-stu-id="68b4e-137">Specifies the layout of the attachments.</span></span> <span data-ttu-id="68b4e-138">用于类型`result`的响应。</span><span class="sxs-lookup"><span data-stu-id="68b4e-138">Used for responses of type `result`.</span></span> <br><span data-ttu-id="68b4e-139">目前支持以下类型：</span><span class="sxs-lookup"><span data-stu-id="68b4e-139">Currently the following types are supported:</span></span> <br><span data-ttu-id="68b4e-140">`list`：包含缩略图、标题和文本字段的卡片对象的列表</span><span class="sxs-lookup"><span data-stu-id="68b4e-140">`list`: a list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="68b4e-141">`grid`：缩略图图像的网格</span><span class="sxs-lookup"><span data-stu-id="68b4e-141">`grid`: a grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="68b4e-142">有效的附件对象的数组。</span><span class="sxs-lookup"><span data-stu-id="68b4e-142">Array of valid attachment objects.</span></span> <span data-ttu-id="68b4e-143">用于类型`result`的响应。</span><span class="sxs-lookup"><span data-stu-id="68b4e-143">Used for responses of type `result`.</span></span> <br><span data-ttu-id="68b4e-144">目前支持以下类型：</span><span class="sxs-lookup"><span data-stu-id="68b4e-144">Currently the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="68b4e-145">建议的操作。</span><span class="sxs-lookup"><span data-stu-id="68b4e-145">Suggested actions.</span></span> <span data-ttu-id="68b4e-146">用于类型`auth`或`config`的响应。</span><span class="sxs-lookup"><span data-stu-id="68b4e-146">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="68b4e-147">要显示的消息。</span><span class="sxs-lookup"><span data-stu-id="68b4e-147">Message to display.</span></span> <span data-ttu-id="68b4e-148">用于类型`message`的响应。</span><span class="sxs-lookup"><span data-stu-id="68b4e-148">Used for responses of type `message`.</span></span> |

### <a name="response-card-types-and-previews"></a><span data-ttu-id="68b4e-149">响应卡片类型和预览</span><span class="sxs-lookup"><span data-stu-id="68b4e-149">Response card types and previews</span></span>

<span data-ttu-id="68b4e-150">我们支持以下附件类型：</span><span class="sxs-lookup"><span data-stu-id="68b4e-150">We support the following attachment types:</span></span>

* [<span data-ttu-id="68b4e-151">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="68b4e-151">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="68b4e-152">英雄卡片</span><span class="sxs-lookup"><span data-stu-id="68b4e-152">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="68b4e-153">Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="68b4e-153">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="68b4e-154">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="68b4e-154">Adaptive Card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="68b4e-155">有关概述，请参阅[什么是卡片](~/task-modules-and-cards/what-are-cards.md)。</span><span class="sxs-lookup"><span data-stu-id="68b4e-155">See [What are cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

<span data-ttu-id="68b4e-156">若要了解如何使用缩略图和英雄卡片类型，请参阅[添加卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="68b4e-156">To learn how to use the thumbnail and hero card types, see [Add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="68b4e-157">有关 Office 365 连接器卡的其他文档，请参阅[使用 office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)。</span><span class="sxs-lookup"><span data-stu-id="68b4e-157">For additional documentation regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="68b4e-158">结果列表显示在 Microsoft 团队 UI 中，每个项目都有一个预览。</span><span class="sxs-lookup"><span data-stu-id="68b4e-158">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="68b4e-159">将通过以下两种方式之一生成预览：</span><span class="sxs-lookup"><span data-stu-id="68b4e-159">The preview is generated in one of two ways:</span></span>

* <span data-ttu-id="68b4e-160">在`attachment`对象`preview`中使用属性。</span><span class="sxs-lookup"><span data-stu-id="68b4e-160">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="68b4e-161">该`preview`附件只能是一个英雄或缩略图卡片。</span><span class="sxs-lookup"><span data-stu-id="68b4e-161">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="68b4e-162">从附件的基本`title`、 `text`和`image`属性中提取。</span><span class="sxs-lookup"><span data-stu-id="68b4e-162">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="68b4e-163">仅当未设置该`preview`属性且这些属性可用时，才使用这些属性。</span><span class="sxs-lookup"><span data-stu-id="68b4e-163">These are used only if the `preview` property is not set and these properties are available.</span></span>

<span data-ttu-id="68b4e-164">您可以仅通过其 preview 属性在结果列表中显示自适应卡片或 Office 365 连接器卡片的预览。</span><span class="sxs-lookup"><span data-stu-id="68b4e-164">You can display a preview of an Adaptive Card or Office 365 Connector card in the result list simply by its preview property.</span></span> <span data-ttu-id="68b4e-165">如果结果已经是英雄或缩略图卡片，则无需执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="68b4e-165">This is not necessary if the results are already hero or thumbnail cards.</span></span> <span data-ttu-id="68b4e-166">如果使用预览附件，则它必须是英雄或缩略图卡片。</span><span class="sxs-lookup"><span data-stu-id="68b4e-166">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="68b4e-167">如果未指定 preview 属性，卡片的预览将会失败，并且不会显示任何内容。</span><span class="sxs-lookup"><span data-stu-id="68b4e-167">If no preview property is specified, the preview of the card will fail and nothing will be displayed.</span></span>

### <a name="response-example"></a><span data-ttu-id="68b4e-168">响应示例</span><span class="sxs-lookup"><span data-stu-id="68b4e-168">Response example</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="68b4e-169">C #/.NET</span><span class="sxs-lookup"><span data-stu-id="68b4e-169">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="68b4e-170">TypeScript/node.js</span><span class="sxs-lookup"><span data-stu-id="68b4e-170">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="68b4e-171">JSON</span><span class="sxs-lookup"><span data-stu-id="68b4e-171">JSON</span></span>](#tab/json)

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

## <a name="default-query"></a><span data-ttu-id="68b4e-172">默认查询</span><span class="sxs-lookup"><span data-stu-id="68b4e-172">Default query</span></span>

<span data-ttu-id="68b4e-173">如果在清单`initialRun`中`true`设置为，Microsoft 团队会在用户第一次打开邮件扩展时发出 "默认" 查询。</span><span class="sxs-lookup"><span data-stu-id="68b4e-173">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a "default" query when the user first opens the messaging extension.</span></span> <span data-ttu-id="68b4e-174">您的服务可以使用一组预填充的结果对此查询做出响应。</span><span class="sxs-lookup"><span data-stu-id="68b4e-174">Your service can respond to this query with a set of pre-populated results.</span></span> <span data-ttu-id="68b4e-175">当您的搜索命令需要进行身份验证或配置、显示最近查看的项目、收藏夹或任何其他不依赖于用户输入的信息时，这可能很有用。</span><span class="sxs-lookup"><span data-stu-id="68b4e-175">This can be useful when your search command requires authentication or configuration, displaying recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="68b4e-176">默认查询的结构与任何常规用户`name`查询相同，字段在下面的对象中设置`initialRun`为`value`和设置`true`为。</span><span class="sxs-lookup"><span data-stu-id="68b4e-176">The default query has the same structure as any regular user query, with the `name` field set to `initialRun` and `value` set to `true` as in the object below.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="68b4e-177">后续步骤</span><span class="sxs-lookup"><span data-stu-id="68b4e-177">Next Steps</span></span>

<span data-ttu-id="68b4e-178">添加身份验证和/或配置</span><span class="sxs-lookup"><span data-stu-id="68b4e-178">Add authentication and/or configuration</span></span>

* [<span data-ttu-id="68b4e-179">向邮件扩展添加身份验证</span><span class="sxs-lookup"><span data-stu-id="68b4e-179">Add authentication to a messaging extension</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="68b4e-180">向邮件扩展添加配置</span><span class="sxs-lookup"><span data-stu-id="68b4e-180">Add configuration to a messaging extension</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="68b4e-181">部署配置</span><span class="sxs-lookup"><span data-stu-id="68b4e-181">Deploy configuration</span></span>

* [<span data-ttu-id="68b4e-182">部署应用程序包</span><span class="sxs-lookup"><span data-stu-id="68b4e-182">Deploy your app package</span></span>](~/concepts/deploy-and-publish/apps-upload.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
