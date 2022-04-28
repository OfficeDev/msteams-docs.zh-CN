---
title: 消息扩展
author: surbhigupta
description: Microsoft Teams平台上的消息扩展概述
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: c81f8ec4b1158275ab796883b268d2c7fa6ecfe8
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104110"
---
# <a name="message-extensions"></a>消息扩展

消息扩展允许用户通过Microsoft Teams客户端中的按钮和窗体与 Web 服务交互。 他们可以从撰写消息区域、命令框或直接从消息搜索或启动外部系统中的操作。 可以以格式丰富的卡片的形式将该交互的结果发送回Microsoft Teams客户端。 本文档概述了消息扩展、在不同方案下执行的任务、处理消息扩展、操作和搜索命令以及链接展开。

下图显示了从中调用消息扩展的位置：

![消息扩展调用位置](~/assets/images/messaging-extension-invoke-locations.png)

> [!NOTE]
> 撰写框中不再支持@mentioning消息扩展。

## <a name="scenarios-where-message-extensions-are-used"></a>使用消息扩展的方案

| 应用场景 | 示例 |
|:-----------------|:-----------------|
|你希望某些外部系统执行操作，并将操作的结果发送回会话。|保留资源并允许通道知道保留的时间段。|
|你希望在外部系统中找到某些内容，并与对话共享结果。|在Azure DevOps中搜索工作项，并将其作为自适应卡片与组共享。|
|你希望完成一个复杂的任务，其中涉及外部系统中的多个步骤或大量信息，并与对话共享结果。|基于Teams消息在跟踪系统中创建 bug，将该 bug 分配给 Bob，并使用 bug 的详细信息将卡片发送到会话线程。|

## <a name="understand-how-message-extensions-work"></a>了解消息扩展的工作原理

消息扩展由托管的 Web 服务和应用清单组成，用于定义 Web 服务从Microsoft Teams客户端调用的位置。 Web 服务利用 Bot Framework 的消息传送架构和安全通信协议，因此必须在 Bot Framework 中将 Web 服务注册为机器人。

> [!NOTE]
> 虽然可以手动创建 Web 服务，但请使用 [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) 来处理协议。

在Microsoft Teams应用的应用清单中，最多定义了 10 个不同的命令的单个消息扩展。 每个命令定义一个类型，例如操作或搜索，以及从中调用它的客户端中的位置。 调用位置为撰写消息区域、命令栏和消息。 调用时，Web 服务将接收包含 JSON 有效负载（包括所有相关信息）的 HTTPS 消息。 使用 JSON 有效负载进行响应，使Teams客户端能够知道要启用的下一个交互。

## <a name="types-of-message-extension-commands"></a>消息扩展命令的类型

消息扩展命令有两种类型：操作命令和搜索命令。 消息扩展命令类型定义可供 Web 服务使用的 UI 元素和交互流。 某些交互（例如身份验证和配置）可用于这两种类型的命令。

### <a name="action-commands"></a>操作命令

操作命令用于向用户显示用于收集或显示信息的模式弹出窗口。 当用户提交表单时，Web 服务会通过直接将消息插入对话或将消息插入撰写消息区域来响应。 之后，用户可以提交消息。 可以将多个表单链接在一起，以实现更复杂的工作流。

操作命令从撰写消息区域、命令框或消息触发。 从消息调用命令时，发送到机器人的初始 JSON 有效负载包括从中调用的整个消息。 下图显示消息扩展操作命令任务模块： ![消息扩展操作命令任务模块](~/assets/images/task-module.png)

### <a name="search-commands"></a>搜索命令

使用搜索命令，用户可以通过搜索框手动搜索外部系统以获取信息，或者将链接粘贴到受监视的域中，然后将搜索结果插入消息中。 在最基本的搜索命令流中，初始调用消息包括用户提交的搜索字符串。 使用卡片和卡片预览列表进行响应。 Teams客户端为用户呈现卡片预览列表。 当用户从列表中选择卡片时，全尺寸卡会插入撰写消息区域。

卡片从撰写消息区域或命令框触发，而不是从消息触发。 无法从消息触发它们。
下图显示了消息扩展搜索命令任务模块：

![消息扩展搜索命令](~/assets/images/search-extension.png)

> [!NOTE]
> 有关卡片的详细信息，请参阅 [什么是卡](../task-modules-and-cards/what-are-cards.md)片。

## <a name="link-unfurling"></a>链接展开

粘贴在撰写消息区域中的 URL 时，将调用 Web 服务。 此功能称为链接展开。 当包含特定域的 URL 粘贴到撰写消息区域时，可以订阅接收调用。 Web 服务可以将 URL“展开”到详细卡片中，提供的信息比标准网站预览卡还多。 可以添加按钮，让用户在不离开Microsoft Teams客户端的情况下立即采取行动。
在消息扩展插件中粘贴链接时，以下图像显示链接展开功能：

![展开链接](../assets/images/messaging-extension/unfurl-link.png)

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
| 具有基于操作的命令的消息扩展 | 此示例演示如何生成基于操作的消息扩展。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| 具有基于搜索的命令的消息扩展 | 此示例演示如何生成基于搜索的消息扩展。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
|任务计划的消息扩展操作|此示例演示如何从消息扩展操作命令中计划任务，并在计划的日期和时间获取提醒卡。|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/nodejs)|

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [定义操作消息扩展命令](~/messaging-extensions/how-to/action-commands/define-action-command.md)

## <a name="see-also"></a>另请参阅

* [定义搜索消息扩展命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [创建消息扩展](../build-your-first-app/build-messaging-extension.md)
