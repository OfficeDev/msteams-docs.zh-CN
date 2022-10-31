---
title: 消息扩展
author: surbhigupta
description: 了解如何使用消息扩展、其类型，以及它在 Microsoft Teams 平台上使用的方案。 有关操作和基于搜索的消息扩展的示例。
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 09dad55a4ca0b59e517f55e12f24d8ea8d687313
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791732"
---
# <a name="message-extensions"></a>消息扩展

消息扩展允许用户通过 Microsoft Teams 客户端中的按钮和表单与你的 Web 服务进行交互。 他们可以从撰写消息区域、命令框或直接从消息的外部系统中搜索或启动操作。 你可以以格式丰富的卡片形式将该交互的结果发送回 Teams 客户端。

> [!IMPORTANT]
> 消息扩展在政府社区云 (GCC) 和GCC-High环境中提供，但在国防部 (DoD) 环境中不可用。

本文档概述了消息扩展、在不同方案下执行的任务、处理消息扩展、操作和搜索命令以及链接展开。

下图显示了从中调用消息扩展的位置：

:::image type="content" source="~/assets/images/messaging-extension-invoke-locations.png" alt-text="消息扩展调用位置":::

> [!NOTE]
> 撰写框中不再支持@mentioning消息扩展。

## <a name="scenarios-where-message-extensions-are-used"></a>使用消息扩展的应用场景

| 应用场景 | 示例 |
|:-----------------|:-----------------|
|你希望某些外部系统执行操作，并将操作的结果发送回会话。|保留资源并允许通道知道保留的时间段。|
|你希望在外部系统中找到某些内容，并与对话共享结果。|在 Azure DevOps 中搜索工作项，并将其作为自适应卡片与组共享。|
|你希望完成一个复杂的任务，其中涉及外部系统中的多个步骤或大量信息，并与对话共享结果。|在跟踪系统中根据 Teams 消息创建漏洞，将该漏洞分配给用户，并向会话线程发送包含该漏洞详细信息的卡片。|

## <a name="understand-how-message-extensions-work"></a>了解消息扩展的工作原理

消息扩展由托管的 Web 服务和应用清单组成，该清单定义在 Teams 客户端中从何处调用 Web 服务。 他们利用 Bot Framework 的消息传递架构和安全通信协议，因此你还需要在 Bot Framework 中将 Web 服务注册为机器人。

> [!NOTE]
> 虽然可以手动创建 Web 服务，但请使用 [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) 来处理协议。

在 Teams 应用的应用清单中，使用最多 10 个不同的命令定义单个消息扩展。 每个命令定义一个类型，例如操作或搜索，以及客户端中调用它的位置。 调用位置为撰写消息区域、命令栏和消息。 调用时，Web 服务将接收包含 JSON 有效负载（包括所有相关信息）的 HTTPS 消息。 使用 JSON 有效负载进行响应，使 Teams 客户端能够知道要启用的下一个交互。

## <a name="types-of-message-extension-commands"></a>消息扩展命令的类型

消息扩展命令有两种类型：操作命令和搜索命令。 消息扩展命令类型定义可供 Web 服务使用的 UI 元素和交互流。 某些交互（例如身份验证和配置）可用于这两种类型的命令。

### <a name="action-commands"></a>操作命令

操作命令用于向用户显示用于收集或显示信息的模式弹出窗口。 当用户提交表单时，Web 服务可以通过直接在对话中插入消息来响应，或者将消息插入到撰写消息区域以允许用户提交消息。 之后，用户可以提交消息。 可以将多个表单链接在一起，以实现更复杂的工作流。

可在撰写消息区域、命令框或消息中触发操作命令。 从消息调用命令时，发送到机器人的初始 JSON 有效负载包括从中调用的整个消息。 下图显示了消息扩展操作命令任务模块:

:::image type="content" source="~/assets/images/task-module.png" alt-text="消息扩展操作命令任务模块":::

### <a name="search-commands"></a>搜索命令

搜索命令允许用户通过搜索框手动搜索外部系统中的信息，或通过将受监视域的链接粘贴到撰写消息区域并将搜索结果插入消息中。 在最基础的搜索命令流程中，初始调用消息将包含用户提交的搜索字符串。 你将以一个卡片列表和卡片预览回复。 Teams 客户端为用户呈现卡片预览列表。 当用户从列表中选择一张卡片时，全尺寸的卡片会被插入到消息撰写区域。

卡片从撰写消息区域或命令框触发，而不是从消息触发。 无法从消息触发它们。
下图显示了消息扩展搜索命令任务模块：

:::image type="content" source="~/assets/images/search-extension.png" alt-text="消息扩展搜索命令":::

> [!NOTE]
> 有关卡片的详细信息，请参阅 [什么是卡片](../task-modules-and-cards/what-are-cards.md)。

## <a name="link-unfurling"></a>链接展开

粘贴在撰写消息区域中的 URL 时，将调用 Web 服务。 此功能称为链接展开。 当粘贴某一域的 URL 到撰写消息区域，可以订阅以接收调用。 Web 服务可以将 URL“展开”到详细卡片中，提供的信息比标准网站预览卡还多。 可以添加按钮以允许用户在不离开 Teams 客户端的情况下立即执行操作。
在消息扩展插件中粘贴链接时，以下图像显示链接展开功能：

:::image type="content" source="../assets/images/messaging-extension/unfurl-link.png" alt-text="展开链接":::

![链接展开](../assets/images/messaging-extension/link-unfurl.gif)

## <a name="code-snippets"></a>代码段

以下代码提供了基于消息扩展的操作示例：

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

 protected override Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
        {
            // Handle different actions using switch
            switch (action.CommandId)
            {
                case "HTML":
                    return new MessagingExtensionActionResponse
                    {
                        Task = new TaskModuleContinueResponse
                        {
                            Value = new TaskModuleTaskInfo
                            {
                                Height = 200,
                                Width = 400,
                                Title = "Task Module HTML Page",
                                Url = baseUrl + "/htmlpage.html",
                            },
                        },
                    };
                // return TaskModuleHTMLPage(turnContext, action);
                default:
                    string memberName = "";
                    var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
                    memberName = member.Name;
                    return new MessagingExtensionActionResponse
                    {
                        Task = new TaskModuleContinueResponse
                        {
                            Value = new TaskModuleTaskInfo
                            {
                                Card = <<AdaptiveAction card json>>,
                                Height = 200,
                                Width = 400,
                                Title = $"Welcome {memberName}",
                            },
                        },
                    };
            }
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

    async handleTeamsMessagingExtensionFetchTask(context, action) {
        switch (action.commandId) {
            case 'Static HTML':
                return staticHtmlPage();
        }
    }

    staticHtmlPage(){
        return {
            task: {
                type: 'continue',
                value: {
                    width: 450,
                    height: 125,
                    title: 'Task module Static HTML',
                    url: `${baseurl}/StaticPage.html`
                }
            }
        };
    }

```

---

以下代码提供了基于消息扩展的搜索示例：

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
        {
            var text = query?.Parameters?[0]?.Value as string ?? string.Empty;

            var packages = new[] {
            new { title = "A very extensive set of extension methods", value = "FluentAssertions" },
            new { title = "Fluent UI Library", value = "FluentUI" }};

            // We take every row of the results and wrap them in cards wrapped in MessagingExtensionAttachment objects.
            // The Preview is optional, if it includes a Tap, that will trigger the OnTeamsMessagingExtensionSelectItemAsync event back on this bot.
            var attachments = packages.Select(package =>
            {
                var previewCard = new ThumbnailCard { Title = package.title, Tap = new CardAction { Type = "invoke", Value = package } };
                if (!string.IsNullOrEmpty(package.title))
                {
                    previewCard.Images = new List<CardImage>() { new CardImage(package.title, "Icon") };
                }

                var attachment = new MessagingExtensionAttachment
                {
                    ContentType = HeroCard.ContentType,
                    Content = new HeroCard { Title = package.title },
                    Preview = previewCard.ToAttachment()
                };

                return attachment;
            }).ToList();

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

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

async handleTeamsMessagingExtensionQuery(context, query) {
        const searchQuery = query.parameters[0].value;     
        const attachments = [];
                const response = await axios.get(`http://registry.npmjs.com/-/v1/search?${ querystring.stringify({ text: searchQuery, size: 8 }) }`);
                
                response.data.objects.forEach(obj => {
                        const heroCard = CardFactory.heroCard(obj.package.name);
                        const preview = CardFactory.heroCard(obj.package.name);
                        preview.content.tap = { type: 'invoke', value: { description: obj.package.description } };
                        const attachment = { ...heroCard, preview };
                        attachments.push(attachment);
                });
    
                return {
                    composeExtension:  {
                           type: 'result',
                           attachmentLayout: 'list',
                           attachments: attachments
                    }
                };
            }       
        }
```

---

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **.NET** | **Node.js** | **Python** |
|------------|-------------|----------------|------------|------------|
| 具有基于操作命令的消息扩展 | 此示例演示如何生成基于操作的消息扩展。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| 具有基于搜索命令的消息扩展 | 此示例演示如何生成基于搜索的消息扩展。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
|任务计划的消息扩展操作|此示例演示如何从消息扩展操作命令中计划任务，并在计划的日期和时间获取提醒卡。|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/nodejs)| 不适用 |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [定义操作消息扩展命令](~/messaging-extensions/how-to/action-commands/define-action-command.md)

## <a name="see-also"></a>另请参阅

* [定义搜索消息扩展命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [创建消息扩展](../build-your-first-app/build-messaging-extension.md)
* [基于搜索的消息传送扩展的通用操作](how-to/search-commands/universal-actions-for-search-based-message-extensions.md)
