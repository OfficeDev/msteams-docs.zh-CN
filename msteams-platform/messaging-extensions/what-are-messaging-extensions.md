---
title: 消息传递扩展
author: surbhigupta
description: 邮件扩展在 Microsoft Teams 概述
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 975a51850e7e9d0049de46fc8d77016166ffedab
ms.sourcegitcommit: 55d4b4b721a33bacfe503bc646b412f0e3b0203e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2022
ms.locfileid: "62185447"
---
# <a name="messaging-extensions"></a>消息传递扩展

邮件扩展允许用户通过客户端中的按钮和表单与 web Microsoft Teams交互。 他们可以从撰写邮件区域、命令框或直接从邮件搜索或启动外部系统中的操作。 你可以以格式丰富的卡片的形式将交互结果发送回Microsoft Teams客户端。 本文档概述了邮件扩展、在不同方案中执行的任务、邮件扩展的工作、操作和搜索命令以及链接取消点击。

下图显示了调用邮件扩展的位置：

![消息扩展调用位置](~/assets/images/messaging-extension-invoke-locations.png)

> [!NOTE]
> @mentioning撰写框中不再支持邮件扩展名。

## <a name="scenarios-where-messaging-extensions-are-used"></a>使用邮件扩展的方案

| 应用场景 | 示例 |
|:-----------------|:-----------------|
|您希望某些外部系统执行一个操作，并且此操作的结果将发送回您的对话。|预留资源并允许频道知道预留的时间段。|
|您希望在外部系统中查找内容，并与对话共享结果。|在工作组中搜索工作项Azure DevOps，并作为自适应卡片与组共享。|
|您希望完成涉及外部系统中多个步骤或大量信息的复杂任务，并与对话共享结果。|基于邮件创建跟踪系统中Teams Bug，将 bug 分配给 Bob，然后向对话线程发送包含 bug 详细信息的卡片。|

## <a name="understand-how-messaging-extensions-work"></a>了解邮件扩展如何工作

消息扩展由您托管的 Web 服务和应用程序清单组成，它定义 Web 服务在 Microsoft Teams 客户端中的调用位置。 Web 服务利用 Bot Framework 的消息架构和安全通信协议，因此你必须在 Bot Framework 中将 Web 服务注册为自动程序。 

> [!NOTE]
> 虽然可以手动创建 Web 服务，但使用 [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) 处理协议。

在应用程序应用Microsoft Teams中，使用最多十个不同的命令定义单个消息传递扩展。 每个命令都定义一种类型，如操作或搜索以及客户端中调用它的位置。 调用位置包括撰写邮件区域、命令栏和邮件。 在调用时，Web 服务会收到一条包含 JSON 有效负载的 HTTPS 消息，其中包括所有相关信息。 使用 JSON 有效负载响应，Teams客户端知道要启用的下一次交互。 

## <a name="types-of-messaging-extension-commands"></a>邮件扩展命令的类型

邮件扩展命令有两种类型：操作命令和搜索命令。 消息扩展命令类型定义可用于 Web 服务的 UI 元素和交互流。 某些交互（如身份验证和配置）可用于两种类型的命令。

### <a name="action-commands"></a>操作命令

操作命令用于向用户显示用于收集或显示信息的模式弹出窗口。 当用户提交表单时，Web 服务会通过直接将邮件插入对话或将邮件插入撰写邮件区域来做出响应。 之后，用户可以提交邮件。 您可以将多个表单链接在一起，以使用更复杂的工作流。

操作命令从撰写邮件区域、命令框或邮件中触发。 从邮件调用命令时，发送到自动程序的初始 JSON 有效负载包括从其中调用命令的整个消息。 下图显示了邮件扩展操作命令任务模块 ![ ：邮件扩展操作命令任务模块](~/assets/images/task-module.png)

### <a name="search-commands"></a>搜索命令

搜索命令允许用户通过搜索框手动搜索外部系统的信息，或者将受监视域的链接粘贴到撰写邮件区域，然后将搜索结果插入邮件中。 在最基本的搜索命令流中，初始调用消息包括用户提交的搜索字符串。 使用卡片和卡片预览列表进行响应。 客户端Teams为用户呈现卡片预览列表。 当用户从列表中选择卡片时，全尺寸卡片将插入到撰写邮件区域中。

卡片从撰写邮件区域或命令框触发，不会从邮件中触发。 无法从邮件中触发它们。
下图显示了邮件扩展搜索命令任务模块：

![邮件扩展搜索命令](~/assets/images/search-extension.png)

> [!NOTE]
> 有关卡片详细信息，请参阅 [什么是卡片](../task-modules-and-cards/what-are-cards.md)。

## <a name="link-unfurling"></a>链接展开

在撰写邮件区域中粘贴 URL 时，将调用 Web 服务。 此功能称为链接取消点击。 当包含特定域的 URL 粘贴到撰写邮件区域中时，可以订阅接收调用。 Web 服务可以将 URL"取消展开"为详细卡片，提供比标准网站预览卡更多的信息。 您可以添加按钮以允许用户立即采取措施，而无需离开 Microsoft Teams 客户端。
将链接粘贴到邮件扩展中时，以下图像显示链接展开功能：
 
![取消链接](../assets/images/messaging-extension/unfurl-link.png)

![链接取消点击](../assets/images/messaging-extension/link-unfurl.gif)

## <a name="code-snippets"></a>代码段

以下代码提供了基于邮件扩展的操作示例：

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

以下代码提供了基于邮件扩展的搜索示例：

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
| 使用基于操作的命令的邮件扩展 | 此示例演示如何构建基于操作的邮件扩展。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| 使用基于搜索的命令的邮件扩展 | 此示例演示如何构建基于搜索的消息扩展。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
|任务计划的邮件扩展操作|此示例说明如何从邮件扩展操作命令安排任务，以及如何在计划的日期和时间获取提醒卡片。|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/msgext-message-reminder/nodejs)|

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [定义操作消息传递扩展命令](~/messaging-extensions/how-to/action-commands/define-action-command.md)

## <a name="see-also"></a>另请参阅

* [定义搜索邮件扩展命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [创建邮件扩展](../build-your-first-app/build-messaging-extension.md)