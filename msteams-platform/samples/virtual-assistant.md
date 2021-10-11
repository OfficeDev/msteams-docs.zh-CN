---
title: 创建虚拟助手
description: 如何创建虚拟助理聊天机器人和技能以用于Microsoft Teams
ms.localizationpriority: medium
ms.topic: how-to
keywords: teams 虚拟助理机器人
ms.openlocfilehash: 1231520278f97fc48ad53937af80c127021bd9c2
ms.sourcegitcommit: 25a88715d9b06b2afeac14de86177bb34161b0cf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2021
ms.locfileid: "60266632"
---
# <a name="create-virtual-assistant"></a>创建虚拟助手 

虚拟助理是一个 Microsoft 开源模板，它使您能够创建可靠的对话解决方案，同时保持对用户体验、组织品牌和必要数据的完全控制。 the[虚拟助理 core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that bring together the Microsoft technologies required to build a 虚拟助理， including the Bot Framework [SDK，](https://github.com/microsoft/botframework-sdk) [Language Understanding (MICROD) ， ](https://www.luis.ai/)and [QnA Maker](https://www.qnamaker.ai/). 它还整合了基本功能，包括技能注册、链接帐户、基本对话意图，以便为用户提供一系列无缝交互和体验。 此外，模板功能包括可重用对话技能的丰富 [示例](https://microsoft.github.io/botframework-solutions/overview/skills)。  个人技能集成在一个虚拟助理解决方案中，以实现多个方案。 使用 Bot Framework SDK，技能以源代码的形式呈现，让你可以根据需要进行自定义和扩展。 有关 Bot Framework 技能详细信息，请参阅 [什么是 Bot Framework 技能](https://microsoft.github.io/botframework-solutions/overview/skills/)。 本文档指导您虚拟助理组织的实现注意事项、如何创建一个Teams重点 虚拟助理、相关示例、代码示例和 虚拟助理。
下图显示了虚拟助理的概述：

![虚拟助理概述图](../assets/images/bots/virtual-assistant/overview.png)

短信活动通过调度模型由虚拟助理核心[路由到关联的](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true)技能。 

## <a name="implementation-considerations"></a>实现注意事项

决定添加一个虚拟助理包括许多决定因素，并且因组织不同而不同。 组织实施虚拟助理支持因素如下所示：

* 中央团队管理所有员工体验。 它能够构建虚拟助理体验和管理核心体验的更新，包括新技能的添加。
* 跨业务功能存在多个应用程序，预计数量今后会增长。
* 现有应用程序可自定义，归组织所有，并转换为组织虚拟助理。
* 中央员工体验团队能够将自定义设置影响现有应用。 它还提供有关将现有应用程序作为体验技能虚拟助理指南。

下图显示了企业业务虚拟助理： 

![中央团队负责维护助手，业务职能团队贡献技能](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>创建Teams关注虚拟助理

Microsoft[发布了一Visual Studio](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate)虚拟助手和技能的模板。 借助Visual Studio模板，可以创建一个虚拟助理，该模板由基于文本的体验提供支持，支持具有操作限制的富卡片。 我们增强了基本Visual Studio模板，Microsoft Teams出色的平台功能，并Teams出色的应用体验。 一些功能包括对丰富的自适应卡片、任务模块、团队或群聊以及消息传递扩展的支持。 若要详细了解如何扩展虚拟助理Microsoft Teams，请参阅[教程：](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)将虚拟助理扩展Microsoft Teams。    
下图显示了解决方案解决方案虚拟助理图：

![解决方案高级虚拟助理图](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>将自适应卡片添加到你的虚拟助理

若要正确调度请求，虚拟助理必须标识正确的分时系统模型以及与之关联的相应技能。 但是，调度机制不能用于卡片操作活动，因为与技能关联的"图形模型"已经过卡片操作文本培训。 卡片操作文本是固定的预定义关键字，不会从用户进行注释。

通过将技能信息嵌入卡片操作有效负载中，可以解决此问题。 每个技能都应 `skillId` 嵌入卡片  `value` 操作字段中。 必须确保每个卡片操作活动都携带相关的技能信息，并且虚拟助理此信息进行调度。

你必须在 `skillId` 构造函数中提供，以确保技能信息始终存在于卡片操作中。
卡片操作数据示例代码显示在以下部分中：
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

接下来 `SkillCardActionData` ，将引入虚拟助理模板中的类以从 `skillId` 卡操作有效负载中提取。
以下部分显示了从  `skillId` 卡操作有效负载中提取的代码段：

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

实现通过 Activity 类中的扩展 [方法](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) 完成。
以下部分显示了从  `skillId` 卡片操作数据中提取的代码段：

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

虚拟助理在用户尝试调用技能时，另一个技能当前处于活动状态时，用户可以处理中断。 `TeamsSkillDialog`和 `TeamsSwitchSkillDialog` 基于 Bot Framework 的 [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) 和 [SwitchSkillDialog 引入](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)。 它们使用户能够从卡片操作切换技能体验。 若要处理此请求，虚拟助理向用户提示确认消息以切换技能：

![切换到新技能时确认提示](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a>处理任务模块请求

若要将任务模块功能添加到虚拟助理，活动处理程序中还包括两虚拟助理方法： 和 `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` 。 这些方法侦听来自用户的任务虚拟助理活动，确定与请求关联的技能，以及将请求转发给标识的技能。 

请求转发通过 [技能HttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true)方法 `PostActivityAsync` 完成。 它将返回 响应， `InvokeResponse` 就像 解析并转换为 `TaskModuleResponse` 一样。


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

卡片操作调度和任务模块响应也采用类似的方法。 任务模块提取和提交操作数据已更新为包括 `skillId` 。 Activity Extension `GetSkillId` 方法 `skillId` 从有效负载中提取，该负载提供有关需要调用的技能的详细信息。

以下部分提供了 `OnTeamsTaskModuleFetchAsync` 和 `OnTeamsTaskModuleSubmitAsync` 方法的代码段：

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

此外，还必须在清单文件的 部分虚拟助理所有技能域，以便通过技能调用的任务模块 `validDomains` 正确呈现。

### <a name="handle-collaborative-app-scopes"></a>处理协作应用范围

Teams应用可以存在于多个范围，包括一对一聊天、群聊和频道。 核心虚拟助理模板专为一对一聊天设计。 作为载入体验的一虚拟助理提示用户命名并维护用户状态。 由于该载入体验不适合群聊或频道范围，因此已将其删除。

技能应处理多个范围的活动，如一对一聊天、群聊和频道对话。 如果其中任何范围不受支持，技能必须通过相应的消息进行响应。

以下处理函数已添加到虚拟助理核心：

* 虚拟助理群聊或频道中没有任何文本消息即可调用。
* 在将邮件发送到调度模块之前，先清除邮件。 例如，删除@mention的必需文件。

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

### <a name="handle-messaging-extensions"></a>处理邮件扩展

消息扩展的命令在应用清单文件中声明。 邮件扩展用户界面由这些命令支持。 若要虚拟助理附加技能来为消息传递扩展命令提供电源，虚拟助理自己的清单必须包含这些命令。 必须将单个技能的清单中的命令添加到虚拟助理清单中。 命令 ID 通过分隔符附加该技能的应用 ID，提供有关关联技能的信息 `:` 。

技能清单文件的代码段显示在以下部分中：

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

以下虚拟助理显示了对应的清单文件代码段：

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

用户调用命令后，虚拟助理可以通过分析命令 ID 来标识关联的技能，通过从命令 ID 中删除额外的后缀来更新活动，然后将其转发到相应的 `:<skill_id>` 技能。 技能的代码不需要处理额外的后缀。 因此，可以避免跨技能的命令 ID 冲突。 通过此方法，所有上下文中技能的所有搜索和操作命令（如 **compose、commandBox** 和 **message）** 都由虚拟助理。

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

某些邮件扩展活动不包括命令 ID。 例如， `composeExtension/selectItem` 仅包含调用点击操作的值。 若要确定关联的技能， `skillId`  请附加到每个项目卡片，同时形成 对 的响应 `OnTeamsMessagingExtensionQueryAsync` 。 这类似于将自适应[卡片添加到](#add-adaptive-cards-to-your-virtual-assistant)你的虚拟助理。

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

以下示例演示如何将"预订-会议室"应用模板转换为 虚拟助理 技能：书籍-会议室是一种 Microsoft Teams，它允许用户从当前时间开始快速查找和预留会议室 30、60 或 90 分钟。 默认时间为 30 分钟。 Book-a-room bot 作用域为个人对话或 1：1 对话。 下图显示了一个虚拟助理 **具有会议室技能的书籍** 图片：

![虚拟助理"预订聊天室"技能](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

下面是引入的增量更改，以将其转换为附加到技能虚拟助理。 为了将任何现有的 v4 自动程序转换为技能，遵循类似的准则。

### <a name="skill-manifest"></a>技能清单

技能清单是公开技能的消息终结点、ID、名称和其他相关元数据的 JSON 文件。 此清单不同于在应用中旁加载应用的Microsoft Teams。 A 虚拟助理 requires a path to this file as an input to attach a skill. 我们已将以下清单添加到机器人的 wwwroot 文件夹中。

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

虚拟助理的调度模型基于附加技能的"的"分列模型"构建。 调度模型可标识每个文本活动的意图，并找出与其关联的技能。

虚拟助理附加技能时，需要采用格式作为输入的技能的"显示方式"的"中"" `.lu` 使用 botframework-cli 工具将工作台 json `.lu` 转换为格式。

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

我们通过了解这两个命令来构建了一个"一个""一个"区"模型。 必须在 中填充相应的密码 `cognitivemodels.json` 。 此处找到相应的"为"的 ["JSON"文件](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/en-us/book-a-meeting.json)。
以下 `.lu` 部分显示了相应的文件：

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

通过此方法，用户发出的任何命令虚拟助理与聊天机器人相关或标识为与自动程序关联的命令，并 `book room` `manage favorites` `Book-a-room` 转发到此技能。
另一方面，如果命令未完整键入，则机器人需要使用 `Book-a-room room` "采用""设计"模型来了解这些命令。 例如：`I want to manage my favorite rooms`。

### <a name="multi-language-support"></a>多语言支持

例如，将创建一个仅包含英语区域性的"分公司"模型。 你可以创建与其他语言对应的分卡模型，并添加条目 `cognitivemodels.json` 。

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

若要修改 `languages` 参数，请更新 botskills 命令，如下所示：

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

虚拟助理用于 `SetLocaleMiddleware` 标识当前区域设置并调用相应的调度模型。 自动程序框架活动具有此中间件使用的本地设置字段。 也可以对技能使用相同。 预订聊天室机器人不会使用此中间件，而是从 Bot 框架活动的 [clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)实体获取区域设置。

### <a name="claim-validation"></a>声明验证

我们添加了 [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) 来限制呼叫者使用技能。 若要允许虚拟助理此技能，请用该特定用户的应用 ID 虚拟助理 `AllowedCallers` `appsettings` 数组。

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

允许的调用方数组可以限制使用者可以访问该技能的技能。 向此数组 `*` 添加单个条目，以接受来自任何技能使用者的呼叫。

```
"AllowedCallers": [ "*" ],
```

有关向技能添加声明验证详细信息，请参阅 [向技能添加声明验证](/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true)。

### <a name="limitation-of-card-refresh"></a>卡片刷新的限制 

目前尚不支持通过[github](https://github.com/microsoft/botbuilder-dotnet/issues/3686)问题中心虚拟助理 (更新活动，例如) 。 因此，我们已将所有卡刷新呼叫 `UpdateActivityAsync` 替换为发布新卡呼叫 `SendActivityAsync` 。

### <a name="card-actions-and-task-module-flows"></a>卡片操作和任务模块流

若要将卡片操作或任务模块活动转发到关联的技能，该技能必须 `skillId` 嵌入到该技能中。
`Book-a-room` bot card action， task module fetch and submit action payloads are modified to contain `skillId` as a parameter. 

有关详细信息，请参阅 [本文档](/microsoftteams/platform/samples/virtual-assistant#add-adaptive-cards-to-your-virtual-assistant) 中的此部分。

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>处理群聊或频道范围中的活动

`Book-a-room bot` 专为私人聊天（如个人聊天或 1：1 范围）设计。 由于我们已自定义虚拟助理支持群聊和频道范围，因此必须从频道范围调用 虚拟助理，因此机器人必须获取相同 `Book-a-room` 范围的活动。 因此 `Book-a-room` ，自动程序会进行自定义以处理这些活动。 你可以找到自动程序的活动处理程序 `OnMessageActivityAsync` `Book-a-room` 的签入方法。

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

还可以利用 Bot Framework [解决方案](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) 存储库中的现有技能，或从头开始创建新技能。 有关创建新技能，请参阅 [创建新技能的教程](https://microsoft.github.io/botframework-solutions/overview/skills/)。 有关虚拟助理和技能体系结构文档，请参阅虚拟助理[和技能体系结构](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)。  

## <a name="limitations-of-virtual-assistant"></a>限制虚拟助理 

* **EndOfConversation：** 技能必须在完成对话 `endOfConversation` 时发送活动。 根据活动，虚拟助理结束具有该特定技能的上下文，并返回到虚拟助理根上下文。 对于"预订聊天室机器人"，没有结束对话的清晰状态。 因此，我们尚未从自动程序发送，并且当用户希望返回到根上下文时 `endOfConversation` `Book-a-room` ，他们只需通过命令 `start over` 执行。  
* **卡片刷新**：尚不支持通过刷新虚拟助理。  
* **邮件扩展：**
  * 目前，虚拟助理最多可支持 10 个邮件扩展命令。
  * 邮件扩展的配置范围不是单个命令，而是整个扩展本身。 这将限制每个单个技能的配置，虚拟助理。
  * 消息扩展命令 ID 的最大长度为 [64 个字符](../resources/schema/manifest-schema.md#composeextensions) ，37 个字符用于嵌入技能信息。 因此，命令 ID 的更新约束限制为 27 个字符。

还可以利用 Bot Framework [解决方案](https://github.com/microsoft/botframework-components/tree/main/skills/csharp) 存储库中的现有技能，或从头开始创建新技能。 稍后的教程可在此处 [找到](https://microsoft.github.io/botframework-solutions/overview/skills/)。 请参阅有关[技能](/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)体系结构虚拟助理文档。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **C#**  **.NET** |
|----------|-----------------|---------------------------|
| 更新的 Visual Studio 模板 | 用于支持团队功能的自定义模板。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-virtual-assistant/csharp) |
| 预订聊天室机器人技能代码 | 可让你快速查找并预订会议室。 | [View](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |


## <a name="see-also"></a>另请参阅

* [集成 web 应用](~/samples/integrate-web-apps-overview.md)
* [预订聊天室](app-templates.md#app-template-code-samples)
* [Microsoft Teams自动程序](../bots/what-are-bots.md)
