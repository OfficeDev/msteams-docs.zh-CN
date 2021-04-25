---
title: Microsoft Teams 虚拟助手
description: 如何创建虚拟助理机器人和技能以在 Microsoft Teams 中使用
ms.topic: how-to
keywords: teams 虚拟助理机器人
ms.openlocfilehash: 52591435c5a7e1c65a8f86a7c41fe4a3a4fa5c83
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2021
ms.locfileid: "51996021"
---
# <a name="virtual-assistant-for-microsoft-teams"></a>Microsoft Teams 虚拟助手

虚拟助理是一个 Microsoft 开放源代码模板，它使您能够创建可靠的对话解决方案，同时保持对用户体验、组织品牌和必要数据的完全控制。 虚拟 [助手](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) 核心模板是基本构建基块，将构建虚拟助理所需的 Microsoft 技术汇集在一起，包括 [Bot Framework SDK、](https://github.com/microsoft/botframework-sdk)语言了解 [ () 、QnA ](https://www.luis.ai/) [Maker](https://www.qnamaker.ai/)以及基本功能，包括技能注册、链接帐户、为最终用户提供一系列无缝交互和体验的基本对话意图。 此外，模板功能包括可重用对话技能的丰富 [示例](https://microsoft.github.io/botframework-solutions/overview/skills)。  个人技能可以集成到虚拟助理解决方案中，以启用多个方案。 使用 Bot Framework SDK，以源代码形式提供技能，使你可以根据需要自定义和扩展。 请参阅 [什么是自动程序框架技能](https://microsoft.github.io/botframework-solutions/overview/skills/)。

![虚拟助手概述图](../assets/images/bots/virtual-assistant/overview.png)

使用调度模型的虚拟助理核心将短信活动 [路由到关联的](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) 技能。 

## <a name="implementation-considerations"></a>实现注意事项

添加虚拟助理的决定可包括许多决定因素，并且因组织不同而不同。 以下是支持为组织实现虚拟助理的因素：

- 中央团队负责管理所有员工体验，并能够构建虚拟助理体验和管理核心体验的更新，包括新技能的添加。
- 多个应用程序存在于多个业务功能中，并且/或数量预计未来会增长。
- 现有应用程序可自定义，归组织所有，并可以转换为虚拟助理的技能。
- 中央员工体验团队能够将自定义项影响现有应用，并提供必要指导，将现有应用程序作为虚拟助手体验中的技能进行集成

![中央团队负责维护助手，业务职能团队贡献技能](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>创建以 Teams 为中心的虚拟助理

Microsoft [发布了一Visual Studio](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) 虚拟助手和技能的模板。 使用Visual Studio模板，可以创建一个虚拟助理，该虚拟助理由基于文本的体验提供支持，支持有限的富卡片和操作。 我们已增强基本Visual Studio模板，以包含 Microsoft Teams 平台功能并增强出色的 Teams 应用体验。 一些功能包括对丰富的自适应卡片、任务模块、团队/群组聊天和消息传递扩展的支持。 *另请参阅* 教程 [：将虚拟助手扩展到 Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)。

![虚拟助理解决方案高级关系图](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>将自适应卡片添加到虚拟助理

为了正确调度请求，你的虚拟助理需要识别正确的"显示"模型以及与之关联的相应技能。 但是，调度机制不能用于卡片操作活动，因为与技能关联的函数函数模型可能无法针对卡片操作文本进行训练，因为这些文本是固定的预定义关键字，而不是来自用户的话。

我们通过将技能信息嵌入卡操作有效负载解决了这一问题。 每个技能都应 `skillId` 嵌入卡片  `value` 操作字段中。 这是确保每个卡片操作活动都携带相关技能信息且虚拟助理可以利用此信息进行调度的最佳方法。

以下是卡片操作数据示例。 通过 `skillId` 提供构造函数，我们可以确保技能信息始终存在于卡片操作中。

```csharp
    public class CardActionData
    {
        public CardActionData(string skillId)
        {
            this.SkillId = skillId;
        }

        [JsonProperty("skillId")]
        public string SkillId { get; set; }
    }

    ...
    var button = new CardAction
    {
        Type = ActionTypes.MessageBack,
        Title = "Card action button",
        Text = "card action button text",
        Value = new CardActionData(<SkillId>),
    };
```

接下来，我们在 `SkillCardActionData` 虚拟助理模板中介绍从卡操作有效负载 `skillId` 中提取的类。

```csharp
    // Skill Card action data should contain skillId parameter
    // This class is used to deserialize it and get skillId 
    public class SkillCardActionData
    {
        /// <summary>
        /// Gets the ID of the skil that should handle this card
        /// </summary>
        [JsonProperty("skillId")]
        public string SkillId { get; set; }
    }
```

下面是从卡片操作数据  `skillId` 中提取的代码段。 我们已在 Activity 类中将此方法作为扩展 [方法](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) 实现。

```csharp
    public static class ActivityExtensions
    {
        // Fetches skillId from CardAction data if present
        public static string GetSkillId(this Activity activity)
        {
            string skillId = string.Empty;

            try
            {
                if (activity.Type.Equals(ActivityTypes.Message) && activity.Value != null)
                {
                    var data = JsonConvert.DeserializeObject<SkillCardActionData>(activity.Value.ToString());
                    skillId = data.SkillId;
                }
                else if (activity.Type.Equals(ActivityTypes.Invoke) && activity.Value != null)
                {
                    var data = JsonConvert.DeserializeObject<SkillCardActionData>(JObject.Parse(activity.Value.ToString()).SelectToken("data").ToString());
                    skillId = data.SkillId;
                }
            }
            catch
            {
                // If not able to retrive skillId, empty skillId should be returned
            }

            return skillId;
        }
    }
```

### <a name="handle-interruptions-gracefully"></a>流畅地处理中断

在用户尝试调用技能时，另一个技能当前处于活动状态时，虚拟助理可以处理中断。 我们已根据 Bot Framework 的 `TeamsSkillDialog` `TeamsSwitchSkillDialog` [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) 和 [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)引入了 和 ，以使用户能够从卡片操作切换技能体验。 若要处理此请求，虚拟助理会提示用户发送确认消息以切换技能。

![切换到新技能时确认提示](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a>处理任务模块请求

若要将任务模块功能添加到虚拟助理，虚拟助理活动处理程序中包含另外两种方法： `OnTeamsTaskModuleFetchAsync` 和 `OnTeamsTaskModuleSubmitAsync` 。 这些方法侦听虚拟助理中与任务模块相关的活动，识别与请求关联的技能，将请求转发到标识的技能。 

请求转发通过  [技能HttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true)方法 `PostActivityAsync` 完成。 它返回 响应， `InvokeResponse` 就像 解析并转换为 `TaskModuleResponse` 一样。

```csharp
    public static TaskModuleResponse GetTaskModuleRespose(this InvokeResponse invokeResponse)
    {
        if (invokeResponse.Body != null)
        {
            return new TaskModuleResponse()
            {
                Task = GetTask(invokeResponse.Body),
            };
        }

        return null;
    }

    private static TaskModuleResponseBase GetTask(object invokeResponseBody)
        {
            JObject resposeBody = (JObject)JToken.FromObject(invokeResponseBody);
            var task = resposeBody.GetValue("task");
            var taskType = task.SelectToken("type").ToString();

            return taskType switch
            {
                "continue" => new TaskModuleContinueResponse()
                {
                    Type = taskType,
                    Value = task.SelectToken("value").ToObject<TaskModuleTaskInfo>(),
                },
                "message" => new TaskModuleMessageResponse()
                {
                    Type = taskType,
                    Value = task.SelectToken("value").ToString(),
                },
                _ => null,
            };
        }
```

卡片操作调度和任务模块响应也采用类似的方法。 任务模块提取和提交操作数据已更新为包含 `skillId` 。 Activity Extension `GetSkillId` 方法 `skillId` 从有效负载中提取，该负载提供有关需要调用的技能的详细信息。

下面是 和 方法的代码 `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` 段。

```csharp
    // Invoked when a "task/fetch" event is received to invoke task module.
    protected override async Task<TaskModuleResponse> OnTeamsTaskModuleFetchAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
    {
        try
        {
            string skillId = (turnContext.Activity as Activity).GetSkillId();
            var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == skillId).First().Value;

            // Forward request to correct skill
            var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken);

            return invokeResponse.GetTaskModuleRespose();
        }
        catch (Exception exception)
        {
            await turnContext.SendActivityAsync(_templateEngine.GenerateActivityForLocale("ErrorMessage"));
            _telemetryClient.TrackException(exception);

            return null;
        }
    }

    // Invoked when a 'task/submit' invoke activity is received for task module submit actions.
    protected override async Task<TaskModuleResponse> OnTeamsTaskModuleSubmitAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
    {
        try
        {
            string skillId = (turnContext.Activity as Activity).GetSkillId();
            var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == skillId).First().Value;

            // Forward request to correct skill
            var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken).ConfigureAwait(false);

            return invokeResponse.GetTaskModuleRespose();
        }
        catch (Exception exception)
        {
            await turnContext.SendActivityAsync(_templateEngine.GenerateActivityForLocale("ErrorMessage"));
            _telemetryClient.TrackException(exception);

            return null;
        }
    }
```

此外，所有技能域必须包含在虚拟助手清单文件的 部分中，以便通过技能调用的任务模块 `validDomains` 能够正确呈现。

### <a name="handling-collaborative-app-scopes"></a>处理协作应用范围

Teams 应用可以存在于多个范围，包括一对一聊天、群聊和频道。 核心虚拟助理模板专为一对一聊天设计。 作为载入体验的一部分，虚拟助理会提示用户输入名称并保持用户状态。 由于该载入体验不适合群聊/频道范围，因此已将其删除。

技能应处理 1：1 (、群聊和频道对话等多个) 。 如果其中任何范围不受支持，技能应提供适当的消息进行响应。

以下处理功能已添加到虚拟助理核心：

- 无需从群聊或频道调用任何文本消息，即可调用虚拟助理。
- 在将邮件 (调度模块之前，@mention自动程序) 删除所需的自动程序。

```csharp
    if (innerDc.Context.Activity.Conversation?.IsGroup == true)
    {
        // Remove bot atmentions for teams/groupchat scope
        innerDc.Context.Activity.RemoveRecipientMention();

        // If bot is invoked without any text, reply with FirstPromptMessage
        if (string.IsNullOrWhiteSpace(innerDc.Context.Activity.Text))
        {
            await innerDc.Context.SendActivityAsync(_templateEngine.GenerateActivityForLocale("FirstPromptMessage"));
            return EndOfTurn;
        }
    }
```

### <a name="handling-messaging-extensions"></a>处理邮件扩展

消息扩展的命令在应用清单文件中声明。 邮件扩展用户界面由这些命令支持。 若要使虚拟助理能够将消息传递扩展命令 (附加技能) ，虚拟助理自己的清单必须包含这些命令。 还应将单个技能清单中的命令添加到虚拟助理的清单中。 命令 ID 通过分隔符或参数来附加该技能的应用 ID，提供有关 `:` () 。

下面是技能清单文件的代码段。

```json
 "composeExtensions": [
    {
        "botId": "<Skil_App_Id>",
        "commands": [
            {
                "id": "searchQuery",
                "context": [ "compose", "commandBox" ],
                "description": "Test command to run query",
    ....
```

下面是相应的虚拟助理清单文件代码段。

```json
 "composeExtensions": [
    {
        "botId": "<VA_App_Id>",
        "commands": [
            {
                "id": "searchQuery:<skill_id>",
                "context": [ "compose", "commandBox" ],
                "description": "Test command to run query",
    ....
```

用户调用命令后，虚拟助理可以通过分析命令 ID 来标识关联的技能，通过从命令 ID 中删除额外的后缀 () 来更新活动，然后将其转发到相应的技能。 `:<skill_id>` 技能的代码不需要处理额外的后缀，因此可以避免跨技能的命令标识发生冲突。 通过此方法，虚拟助理可以支持所有上下文中技能的所有搜索和操作 ("compose"、"commandBox"和"message") 。

```csharp
    const string MessagingExtensionCommandIdSeparator = ":";

    // Invoked when a 'composeExtension/submitAction' invoke activity is received for a messaging extension action command
    protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
    {
        return await ForwardMessagingExtensionActionCommandActivityToSkill(turnContext, action, cancellationToken);
    }

    // Forwards invoke activity to right skill for messaging extension action commands.
    private async Task<MessagingExtensionActionResponse> ForwardMessagingExtensionActionCommandActivityToSkill(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
    {
        var skillId = ExtractSkillIdFromMessagingExtensionActionCommand(turnContext, action);
        var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == skillId).First().Value;
        var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken).ConfigureAwait(false);

        return invokeResponse.GetMessagingExtensionActionResponse();
    }

    // Extracts skill Id from messaging extension command and updates activity value
    private string ExtractSkillIdFromMessagingExtensionActionCommand(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action)
    {
        var commandArray = action.CommandId.Split(MessagingExtensionCommandIdSeparator);
        var skillId = commandArray.Last();

        // Update activity value by removing skill id before forwarding to the skill.
        var activityValue = JsonConvert.DeserializeObject<MessagingExtensionAction>(turnContext.Activity.Value.ToString());
        activityValue.CommandId = string.Join(MessagingExtensionCommandIdSeparator, commandArray, 0 commandArray.Length - 1);
        turnContext.Activity.Value = activityValue;

        return skillId;
    }
```

某些邮件扩展活动不包括命令 ID。 例如， `composeExtension/selectItem` 仅包含调用点击操作的值。 若要确定关联的技能， `skillId`  请附加到每个项目卡片，同时形成 对 的响应 `OnTeamsMessagingExtensionQueryAsync` 。  (这类似于向虚拟助理添加自适应卡片 [的方法](#add-adaptive-cards-to-your-virtual-assistant)。

```csharp
    // Invoked when a 'composeExtension/selectItem' invoke activity is received for compose extension query command.
    protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionSelectItemAsync(ITurnContext<IInvokeActivity> turnContext, JObject query, CancellationToken cancellationToken)
    {
        var data = JsonConvert.DeserializeObject<SkillCardActionData>(query.ToString());
        var skill = _skillsConfig.Skills.Where(s => s.Value.AppId == data.SkillId).First().Value;
        var invokeResponse = await _skillHttpClient.PostActivityAsync(this._appId, skill, _skillsConfig.SkillHostEndpoint, turnContext.Activity as Activity, cancellationToken).ConfigureAwait(false);

        return invokeResponse.GetMessagingExtensionResponse();
    }
```

---

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a>示例：将"预订房间"应用模板转换为虚拟助理技能

[](app-templates.md#book-a-room)会议室预订是一个[Microsoft Teams](../bots/what-are-bots.md)自动程序，用户可以从当前时间开始快速查找会议室并保留 30 (默认) 、60 或 90 分钟的会议室。 Book-a-room bot 作用域为个人对话或 1：1 对话。

![具有"预订会议室"技能的虚拟助理](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

下面是引入的增量更改，以将其转换为可附加到虚拟助理的技能。 可遵循类似的准则，将任何现有的 v4 机器人转换为技能。

### <a name="skill-manifest"></a>技能清单

技能清单是一个 JSON 文件，用于公开技能的消息终结点、id、名称和其他相关元数据 (此清单与在 Microsoft Teams) 中旁加载应用的清单不同。虚拟助手需要此文件的路径作为输入来附加技能。 我们已将以下清单添加到机器人的 wwwroot 文件夹中。

```bash
botskills connect --remoteManifest "<url to skill's manifest>" ..
```

```json
{
  "$schema": "https://schemas.botframework.com/schemas/skills/skill-manifest-2.1.preview-0.json",
  "$id": "microsoft_teams_apps_bookaroom",
  "name": "microsoft-teams-apps-bookaroom",
  "description": "microsoft-teams-apps-bookaroom description",
  "publisherName": "Your Company",
  "version": "1.1",
  "iconUrl": "<icon url>",
  "copyright": "Copyright (c) Microsoft Corporation. All rights reserved.",
  "license": "",
  "privacyUrl": "<privacy url>",
  "endpoints": [
    {
      "name": "production",
      "protocol": "BotFrameworkV3",
      "description": "Production endpoint for the skill",
      "endpointUrl": "<endpoint url>",
      "msAppId": "skill app id"
    }
  ],
  "dispatchModels": {
    "languages": {
      "en-us": [
        {
          "id": "microsoft-teams-apps-bookaroom-en",
          "name": "microsoft-teams-apps-bookaroom LU (English)",
          "contentType": "application/lu",
          "url": "file://book-a-meeting.lu",
          "description": "English language model for the skill"
        }
      ]
    }
  },
  "activities": {
    "message": {
      "type": "message",
      "description": "Receives the users utterance and attempts to resolve it using the skill's LU models"
    }
  }
}
```

### <a name="luis-integration"></a>实现"实现"的"实现"

虚拟助理的调度模型基于附加技能的"函数""数字"模型构建。 调度模型可标识每个文本活动的意图，并找出与其关联的技能。

虚拟助手需要技能的" (模型 `.lu` "，) 附加技能时作为输入。 可以使用 botframework-cli 工具将工作台 json 转换为 `.lu` 格式。

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

预订聊天室自动程序为用户提供了两个主要命令：

- `Book room`
- `Manage Favorites`

我们构建了一个了解这两个命令的"一个""一个"的"设计模型"。 需要在 中填充相应的密码 `cognitivemodels.json` 。 可在此处找到相应的一个/或相应的[](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json)一个工作台 JSON 文件，这是对应 `.lu` 文件的外观。

```
> ! Automatically generated by [LUDown CLI](https://github.com/Microsoft/botbuilder-tools/tree/master/Ludown), Tue Mar 31 2020 17:30:32 GMT+0530 (India Standard Time)

> ! Source LUIS JSON file: book-a-meeting.json

> ! Source QnA TSV file: Not Specified

> ! Source QnA Alterations file: Not Specified


> # Intent definitions

## BOOK ROOM
- book a room
- book room
- please book a room
- reserve a room
- i want to book a room
- i want to book a room please
- get me a room please
- get me a room


## MANAGE FAVORITES
- manage favorites
- manage favorite
- please manage my favorite rooms
- manage my favorite rooms please
- manage my favorite rooms
- i want to manage my favorite rooms

## None


> # Entity definitions


> # PREBUILT Entity definitions


> # Phrase list definitions


> # List entities

> # RegEx entities
```

通过此方法，用户与虚拟助理相关的任何命令问题，或可标识为与书籍-聊天室自动程序关联的命令，并 `book room` `manage favorites` 转发到此技能。
另一方面，如果这些命令未像现在这样键入，则"预订会议室"机器人需要使用"会议室"模型来了解这些命令 (例如 `I want to manage my favorite rooms` ：) 。

### <a name="multi-language-support"></a>多语言支持

对于此示例，我们仅创建了一个具有英语区域性的"处理方式"模型。 你可以创建与其他语言对应的分卡模型，并添加条目 `cognitivemodels.json` 。

```json
{
  "defaultLocale": "en-us",
  "languageModels": {
    "en-us": {
      "luisAppId": "",
      "luisApiKey": "",
      "luisApiHost": ""
    },
    "<your_language_culture>": {
      "luisAppId": "",
      "luisApiKey": "",
      "luisApiHost": ""
    }
  }
}
```

并行，在 `.lu` "用户文件夹路径"中添加相应的文件。 文件夹结构应如下所示：

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

按如下所示更新 botskills 命令以修改 `languages` 参数：

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

虚拟助理 `SetLocaleMiddleware` 用于标识当前区域设置并调用相应的调度模型。  (自动程序框架活动具有此中间件所使用的区域设置字段。) 我们建议也使用相同的技能。 预订聊天室机器人不会使用此中间件，而是从 Bot 框架活动的 [clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)实体获取区域设置。

### <a name="claim-validation"></a>声明验证

我们添加了 [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) 来限制呼叫者使用技能。 若要允许虚拟助理调用此技能，请用该特定 `AllowedCallers` `appsettings` 虚拟助理的应用 ID 填充数组。

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

允许的调用方数组可以限制使用者可以访问该技能的技能。 向此数组 `*` 添加单个条目，以接受来自任何技能使用者的呼叫。

```
"AllowedCallers": [ "*" ],
```
有关向技能添加声明验证的详细文档，请参阅[。](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true)

### <a name="card-refresh-limitation"></a>卡片刷新限制

目前尚不 ([github](https://github.com/microsoft/botbuilder-dotnet/issues/3686) 问题) 虚拟助理更新 (刷新) 。 因此，我们已使用发布新卡片呼叫 () 所有卡片刷新 `UpdateActivityAsync` `SendActivityAsync` () 。

### <a name="card-actions-and-task-module-flows"></a>卡片操作和任务模块流

若要将卡片操作或任务模块活动转发到关联技能，技能需要嵌入 `skillId` 到该技能中。
书籍-会议室自动程序卡操作、任务模块提取和提交操作有效负载被修改为包含 `skillId` 为参数。 

有关详细信息，请参阅 [本文档](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) 中的此部分。

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>处理群聊或频道范围中的活动

预订聊天室自动程序专为私人聊天 (/1：1 范围) 。 由于我们已自定义虚拟助理以支持群聊和频道范围，因此可能会从这些范围调用虚拟助理，因此，预订聊天室机器人可能会获得相同的活动。 因此，书籍聊天室自动程序已自定义为处理这些活动。 检查已放入 `OnMessageActivityAsync` Book-a-room bot 的活动处理程序的方法中。

```csharp
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        // Check if activities are from groupchat/ teams scope. This might happen when the bot is consumed by Virtual Assistant.
        if (turnContext.Activity.Conversation.IsGroup == true)
        {
            await ShowNotSupportedInGroupChatCardAsync(turnContext).ConfigureAwait(false);
        }
        else
        {
            ...
        }
    }
```

还可以利用 Bot Framework [解决方案](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) 存储库中的现有技能，或从头开始创建新技能。 稍后的教程可在此处 [找到](https://microsoft.github.io/botframework-solutions/overview/skills/)。 请参阅虚拟 [助理和](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) 技能体系结构文档。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **C#** | **.NET** |
|----------|-----------------|----------|------------------|
| 更新的 Visual Studio 模板 | 用于支持团队功能的自定义模板。 | [View](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |
| 预订聊天室机器人技能代码 | 可让你快速查找并预订会议室。 |  | [View](https://github.com/nebhagat/msteams-virtual-assistant-dotnet) |



## <a name="virtual-assistant-known-limitations"></a>虚拟助理已知限制

- **EndOfConversation**。 技能应在对话 `endOfConversation` 完成时发送活动。 虚拟助理将基于此活动结束具有该特定技能的上下文，并返回到虚拟助理的 (根) 上下文。 对于"预订聊天室"机器人，没有可以结束对话的清晰状态。 因此，我们尚未从 Book-a-room bot 发送，并且当用户想要返回根上下文时，他们 `endOfConversation` 只需通过命令 `start over` 执行。
- **卡片刷新**。 尚不支持通过虚拟助理进行卡片刷新。
- **邮件扩展 。：**
  - 目前，虚拟助理最多可支持 10 个邮件扩展命令。
  - 邮件扩展的配置范围不是单个命令，而是整个扩展本身。 这将通过虚拟助理限制各个技能的配置。
  - 消息扩展命令 ID 的最大长度为 [64 个字符](../resources/schema/manifest-schema.md#composeextensions) ，37 个字符将用于嵌入技能信息。 因此，命令 ID 的更新约束限制为 27 个字符。
>
>
