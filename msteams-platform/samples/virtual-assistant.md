---
title: 创建虚拟助手
description: 了解如何使用具有自适应卡片等功能的代码示例和代码片段创建虚拟助理机器人Microsoft Teams;使用技能清单处理中断、任务模块请求、协作应用范围和消息扩展;支持多种语言、声明验证、LUIS 集成和模式。
ms.localizationpriority: medium
ms.topic: how-to
keywords: teams 虚拟助理机器人
ms.openlocfilehash: e473fd8166be6285ec90d78401b1df028d81b5b0
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104103"
---
# <a name="create-virtual-assistant"></a>创建虚拟助手

虚拟助理是一个 Microsoft 开源模板，可用于创建可靠的对话解决方案，同时保持对用户体验、组织品牌和必要数据的完全控制。 [虚拟助理核心模板](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template)是将生成虚拟助理所需的 Microsoft 技术（包括 [Bot Framework SDK](https://github.com/microsoft/botframework-sdk)、[语言理解 (LUIS) ](https://www.luis.ai/)和 [QnA Maker）](https://www.qnamaker.ai/)汇集在一起的基本构建基块。 它还汇集了基本功能，包括技能注册、链接帐户、基本聊天意向，以便为用户提供一系列无缝交互和体验。 此外，模板功能还包括可重用对话 [技能](https://microsoft.github.io/botframework-solutions/overview/skills)的丰富示例。  单个技能集成在虚拟助理解决方案中，以启用多个方案。 使用 Bot Framework SDK，技能以源代码形式呈现，使你可以根据需要自定义和扩展。 有关 Bot Framework 技能的详细信息， [请参阅什么是 Bot Framework 技能](https://microsoft.github.io/botframework-solutions/overview/skills/)。 本文档介绍组织虚拟助理实现注意事项、如何创建Teams重点虚拟助理、相关示例、代码示例和虚拟助理限制。
下图显示了虚拟助手的概述：

![虚拟助理概述图](../assets/images/bots/virtual-assistant/overview.png)

文本消息活动通过虚拟助理核心使用[调度](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true)模型路由到关联的技能。

## <a name="implementation-considerations"></a>实现注意事项

添加虚拟助理的决定包括许多确定因素，并且对每个组织都不同。 组织虚拟助理实现的支持因素如下：

* 中心团队管理所有员工体验。 它能够生成虚拟助理体验并管理核心体验的更新，包括添加新技能。
* 跨业务功能存在多个应用程序，预计未来数量会增长。
* 现有应用程序可自定义，由组织拥有，并转换为虚拟助理技能。
* 中心员工体验团队能够影响现有应用的自定义。 它还为将现有应用程序集成为虚拟助理体验中的技能提供了必要的指导。

下图显示了虚拟助理的业务功能：

![中心团队维护助理，业务职能团队贡献技能](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>创建Teams重点虚拟助理

Microsoft 发布了用于构建虚拟助手和技能[的Microsoft Visual Studio模板](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate)。 使用Visual Studio模板，可以创建一个虚拟助理，该虚拟助理由基于文本的体验提供支持，并支持具有操作的有限富卡。 我们增强了Visual Studio基础模板，包括Microsoft Teams平台功能和强大的Teams应用体验。 其中一些功能包括对丰富的自适应卡片、任务模块、团队或组聊天以及消息扩展的支持。 有关将虚拟助理扩展到Microsoft Teams的详细信息，请[参阅教程：将虚拟助理扩展到Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)。
下图显示了虚拟助理解决方案的高级关系图：

![虚拟助理解决方案的高级关系图](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>将自适应卡片添加到虚拟助理

若要正确调度请求，虚拟助理必须标识正确的 LUIS 模型和与之关联的相应技能。 但是，调度机制不能用于卡片操作活动，因为与技能关联的 LUIS 模型是针对卡片操作文本训练的。 卡片操作文本是固定的、预定义的关键字，不会从用户中进行注释。

通过在卡片操作有效负载中嵌入技能信息来解决此缺点。 每个技能都应嵌 `skillId` 入到卡片操作字段中  `value` 。 必须确保每个卡片操作活动都包含相关的技能信息，虚拟助理可以利用此信息进行调度。

必须在构造函数中提供 `skillId` ，以确保技能信息始终存在于卡片操作中。
以下部分显示了卡片操作数据示例代码：

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

接下来，`SkillCardActionData`引入虚拟助理模板中的类以从卡片操作有效负载中提取`skillId`。
以下部分显示了从卡片操作有效负载中提取  `skillId` 的代码片段：

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

实现由 [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) 类中的扩展方法完成。
以下部分显示了从卡片操作数据中提取  `skillId` 的代码片段：

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

### <a name="handle-interruptions"></a>处理中断

虚拟助理可在用户尝试调用技能（而其他技能当前处于活动状态）的情况下处理中断。 `TeamsSkillDialog`，并 `TeamsSwitchSkillDialog`基于 Bot Framework 的 [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) 和 [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs) 进行引入。 它们使用户能够从卡片操作切换技能体验。 若要处理此请求，虚拟助理使用确认消息提示用户切换技能：

![切换到新技能时的确认提示](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a>处理任务模块请求

若要将任务模块功能添加到虚拟助理，虚拟助理活动处理程序中还包含两个附加方法：`OnTeamsTaskModuleFetchAsync`和 `OnTeamsTaskModuleSubmitAsync`。 这些方法侦听虚拟助理中的任务模块相关的活动，确定与请求关联的技能，并将请求转发到标识的技能。

请求转发是通过 [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true)`PostActivityAsync` 方法完成的。 它返回已分析并转换为`TaskModuleResponse`的响应`InvokeResponse`。

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

对于卡片操作调度和任务模块响应，也遵循了类似的方法。 任务模块提取和提交操作数据将更新为包含 `skillId`。
活动扩展方法 `GetSkillId` 从有效负载中 `skillId` 提取，该有效负载提供有关需要调用的技能的详细信息。

以下部分提供了代码 `OnTeamsTaskModuleFetchAsync` 片段和 `OnTeamsTaskModuleSubmitAsync` 方法：

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

            return invokeResponse.GetTaskModuleResponse();
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

此外，必须在虚拟助理清单文件中`validDomains`包含该部分中的所有技能域，以便通过技能正确呈现调用的任务模块。

### <a name="handle-collaborative-app-scopes"></a>处理协作应用范围

Teams应用可以存在于多个范围，包括 1：1 聊天、群聊和频道。 核心虚拟助理模板专为 1：1 聊天而设计。 作为载入体验的一部分虚拟助理提示用户输入名称并保持用户状态。 由于载入体验不适用于群聊或频道范围，因此已被删除。

技能应处理多个范围的活动，例如 1：1 聊天、群聊和频道对话。 如果这些范围中的任何一个不受支持，技能必须使用适当的消息进行响应。

已将以下处理函数添加到虚拟助理核心：

* 可以调用虚拟助理，而无需来自群聊或频道的任何短信。
* 在将消息发送到调度模块之前，会清理表达式。 例如，删除机器人所需的@mention。

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

### <a name="handle-message-extensions"></a>处理消息扩展插件

消息扩展的命令在应用清单文件中声明。 消息扩展用户界面由这些命令提供支持。 若要虚拟助理以附加技能为消息扩展命令提供电源，虚拟助理自己的清单必须包含这些命令。 必须将单个技能清单中的命令添加到虚拟助理的清单中。 命令 ID 通过分隔符 `:`追加技能的应用 ID 来提供有关关联技能的信息。

技能清单文件中的代码片段如下部分所示：

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

以下部分显示了相应的虚拟助理清单文件代码片段：

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

用户调用命令后，虚拟助理可以通过分析命令 ID 来标识关联的技能，通过从命令 ID 中删除额外后缀`:<skill_id>`来更新活动，并将其转发到相应的技能。 技能的代码不需要处理额外的后缀。 因此，可以避免跨技能的命令 ID 之间的冲突。 使用此方法，所有上下文中技能的所有搜索和操作命令（如 **compose**、**commandBox** 和 **消息**）都由虚拟助理提供支持。

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

某些消息扩展活动不包括命令 ID。 例如， `composeExtension/selectItem` 仅包含调用点击操作的值。 若要标识关联的技能， `skillId`  请在为其形成响应 `OnTeamsMessagingExtensionQueryAsync`时附加到每个项卡。 这类似于将[自适应卡片添加到虚拟助理](#add-adaptive-cards-to-your-virtual-assistant)的方法。

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

## <a name="example"></a>示例

以下示例演示如何将书房应用模板转换为虚拟助理技能：书房是一种Microsoft Teams，用户可以从当前时间开始快速查找和保留会议室 30、60 或 90 分钟。 默认时间为 30 分钟。 Book-a-room 机器人的作用域为个人对话或 1：1 对话。
下图显示了一个虚拟助理，**其中包含一本具有房间技能的书**：

![虚拟助理“预订房间”技能](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

以下是为将其转换为附加到虚拟助理的技能而引入的增量更改。 遵循类似的准则将任何现有 v4 机器人转换为技能。

### <a name="skill-manifest"></a>技能清单

技能清单是公开技能消息终结点、ID、名称和其他相关元数据的 JSON 文件。 此清单不同于用于在Microsoft Teams中旁加载应用的清单。 虚拟助理需要将此文件的路径作为输入来附加技能。 我们已将以下清单添加到机器人的 wwwroot 文件夹中。

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

### <a name="luis-integration"></a>LUIS 集成

虚拟助理的调度模型基于附加技能的 LUIS 模型构建。 调度模型标识每个文本活动的意向，并找出与之关联的技能。

虚拟助理在附加技能时需要技能的 LUIS 模型`.lu`（格式为输入）。 LUIS json 使用 botframework-cli 工具转换为 `.lu` 格式。

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

书房机器人有两个主要命令供用户使用：

* `Book room`
* `Manage Favorites`

我们通过了解这两个命令构建了 LUIS 模型。 必须在其中填充 `cognitivemodels.json`相应的机密。 此 [处找到相应的](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/en-us/book-a-meeting.json) LUIS JSON 文件。
以下部分显示了相应的 `.lu` 文件：

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

使用此方法，用户发出的任何命令虚拟助理与`book room`机器人相关或`manage favorites`标识为与`Book-a-room`机器人关联的命令，并转发到此技能。
另一方面， `Book-a-room room` 机器人需要使用 LUIS 模型来了解这些命令（如果未完全键入）。 例如：`I want to manage my favorite rooms`。

### <a name="multi-language-support"></a>多语言支持

例如，创建了仅包含英语区域性的 LUIS 模型。 可以创建与其他语言对应的 LUIS 模型，并向其添加条目 `cognitivemodels.json`。

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

并行在 luisFolder 路径中添加相应的 `.lu` 文件。 文件夹结构应如下所示：

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

若要修改 `languages` 参数，请更新 botskills 命令，如下所示：

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

虚拟助理用于`SetLocaleMiddleware`标识当前区域设置并调用相应的调度模型。 机器人框架活动具有此中间件使用的区域设置字段。 也可以对技能使用相同的功能。 书房机器人不使用此中间件，而是从 Bot Framework 活动的 [clientInfo 实体](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)获取区域设置。

### <a name="claim-validation"></a>声明验证

我们添加了 [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) 以限制调用方的技能。 若要允许虚拟助理调用此技能，请使用`appsettings`该特定虚拟助理的应用 ID 填充`AllowedCallers`数组。

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

允许的调用方数组可以限制哪些技能使用者可以访问技能。 将单个条目 `*` 添加到此数组，以接受来自任何技能使用者的调用。

```
"AllowedCallers": [ "*" ],
```

有关将声明验证添加到技能的详细信息，请 [参阅向技能添加声明验证](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true)。

### <a name="limitation-of-card-refresh"></a>卡刷新限制

更新活动（如卡刷新）尚不支持通过虚拟助理 ([github 问题](https://github.com/microsoft/botbuilder-dotnet/issues/3686)) 。 因此，我们已将所有卡刷新呼叫 `UpdateActivityAsync` 替换为发布新卡呼叫 `SendActivityAsync`。

### <a name="card-actions-and-task-module-flows"></a>卡片操作和任务模块流

若要将卡片操作或任务模块活动转发到关联的技能，该技能必须嵌入 `skillId` 到其中。
`Book-a-room` 机器人卡操作、任务模块提取和提交操作有效负载被修改为包含 `skillId` 为参数。

有关详细信息，请参阅本文档中的 [本](/microsoftteams/platform/samples/virtual-assistant#add-adaptive-cards-to-your-virtual-assistant) 部分。

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>处理群组聊天或频道范围的活动

`Book-a-room bot` 专为私人聊天而设计，例如个人聊天或仅 1：1 范围。 由于我们已自定义虚拟助理以支持群聊和频道范围，因此必须从通道范围调用虚拟助理，因此机器人`Book-a-room`必须获取相同范围的活动。 因此 `Book-a-room`，将自定义机器人来处理这些活动。 可以找到机器人活动处理程序的签入 `OnMessageActivityAsync` 方法 `Book-a-room` 。

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

还可以利用 [Bot Framework Solutions 存储库中的](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) 现有技能，或从头开始创建新技能。 若要创建新技能，请参阅 [教程以创建新技能](https://microsoft.github.io/botframework-solutions/overview/skills/)。 有关虚拟助理和技能体系结构文档，请[参阅虚拟助理和技能体系结构](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)。  

## <a name="limitations-of-virtual-assistant"></a>虚拟助理的限制

* **EndOfConversation**：技能在完成对话时必须发送 `endOfConversation` 活动。 根据活动，虚拟助理以该特定技能结束上下文，并返回到虚拟助理的根上下文中。 对于书房机器人，没有结束聊天的明确状态。 因此，我们没有从`Book-a-room`机器人发送`endOfConversation`，当用户想要返回到根上下文时，他们只需通过`start over`命令执行此操作。  
* **卡刷新**：尚不支持通过虚拟助理刷新卡片。  
* **消息扩展**：
  * 目前，虚拟助理最多可以支持 10 个用于消息扩展的命令。
  * 消息扩展的配置范围不限于单个命令，而适用于整个扩展本身。 这会通过虚拟助理限制每个技能的配置。
  * 消息扩展命令 ID 的最大长度为 [64 个字符](../resources/schema/manifest-schema.md#composeextensions) ，37 个字符用于嵌入技能信息。 因此，命令 ID 的更新约束限制为 27 个字符。

还可以利用 [Bot Framework Solutions 存储库中的](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) 现有技能，或从头开始创建新技能。 稍后的教程可 [在此](https://microsoft.github.io/botframework-solutions/overview/skills/)处找到。 请参阅有关虚拟助理和技能体系结构的[文档](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **C#**  **.NET** |
|----------|-----------------|---------------------------|
| 更新了 Visual Studio 模板 | 自定义模板以支持团队功能。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-virtual-assistant/csharp) |
| 预订会议室机器人技能代码 | 你可以快速查找并预订一个会议室。 | [View](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |

## <a name="see-also"></a>另请参阅

* [集成 web 应用](~/samples/integrate-web-apps-overview.md)
* [书房](app-templates.md#app-template-code-samples)
* [Microsoft Teams机器人](../bots/what-are-bots.md)
