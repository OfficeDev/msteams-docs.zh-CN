---
title: Microsoft 团队的虚拟助手
description: 如何创建在 Microsoft 团队中使用的虚拟助手 bot 和技能
keywords: 团队虚拟助理 bot
ms.openlocfilehash: 0bb1ad832fd33675e607874fcc50f20ffbb96943
ms.sourcegitcommit: 26b7404142706290810064f8216abaa1c262d1e5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "45145996"
---
# <a name="virtual-assistant-for-microsoft-teams"></a>Microsoft 团队的虚拟助手

Virtual Assistant 是一款 Microsoft 开放源代码模板，使您能够在保持用户体验、组织品牌和必要数据的完全控制的同时，创建强大的会话解决方案。 [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template)是基本构建基块，它汇集了构建虚拟助手所需的 Microsoft 技术，包括[Bot 框架 SDK](https://github.com/microsoft/botframework-sdk)、[语言理解（LUIS）](https://www.luis.ai/)、 [QnA Maker](https://www.qnamaker.ai/)以及基本功能，包括技能登记、链接的帐户、基本对话目的，以向最终用户提供一系列无缝交互和体验。 此外，模板功能包含可重用的对话[技能](https://microsoft.github.io/botframework-solutions/overview/skills)的丰富示例。  可以将单个技能集成到虚拟助手解决方案中，以启用多种方案。 使用 Bot 框架 SDK，可在源代码表单中提供技能，使您能够根据需要自定义和扩展。 请参阅[什么是 Bot 框架技能](https://microsoft.github.io/botframework-solutions/overview/skills/)。

![虚拟助手概述图](../assets/images/bots/virtual-assistant/overview.png)

使用[调度](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs)模型将短信活动路由到虚拟助理核心的相关技能。 

## <a name="implementation-considerations"></a>实现注意事项

添加虚拟助理的决策可以包含多个 determinants，并且每个组织的不同之处。 以下是支持实现组织的虚拟助手的因素：

- 中心团队负责管理所有员工体验，并能够构建虚拟助理体验并管理对核心体验的更新，包括新技能的添加。
- 业务功能和/或数字预计未来增长的多个应用程序存在。
- 现有应用程序由组织拥有，可将其转换为虚拟助手的技能。
- 中央员工体验团队可以影响现有应用的自定义项，并提供在虚拟助理体验中集成现有应用程序作为技能的必要指南。

![中心团队维护助理，业务职能团队参与技能](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a>创建以团队为中心的虚拟助手

Microsoft 已发布用于构建虚拟助理和技能的[Visual Studio 模板](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate)。 使用 Visual Studio 模板，您可以创建一个虚拟的助手，并通过基于文本的体验支持，并通过操作支持有限的丰富卡片。 我们已增强 Visual Studio 基本模板，以包含 Microsoft 团队平台功能和强大的团队应用体验。 一些功能包括支持丰富的自适应卡片、任务模块、团队/组聊天和邮件扩展。 另*请参阅*[教程：将您的虚拟助手扩展到 Microsoft 团队](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)。

![虚拟助理解决方案的高级别关系图](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a>将自适应卡片添加到虚拟助手

若要正确调度请求，您的虚拟助手需要确定正确的 LUIS 模型及其关联的相应技能。 但是，由于与某项技能关联的 LUIS 模型是固定的、预定义的关键字，而不是来自用户的 utterances，因此无法将调度机制用于智能卡操作活动。

我们已通过在智能卡操作负载中嵌入技能信息来解决此情况。 每项技能都应嵌入 `skillId` `value` 卡片操作的字段。 这是确保每个卡片操作活动携带相关技能信息和虚拟助理可利用此信息进行派遣的最佳方法。

以下是卡片操作数据示例。 通过 `skillId` 在构造函数中提供，我们确保技能信息始终显示在卡片操作中。

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

接下来，我们 `SkillCardActionData` 将在虚拟助手模板中引入类，以 `skillId` 从智能卡操作负载中提取。

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

下面是要 `skillId` 从卡片操作数据中提取的代码段。 我们将其作为[活动](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)类中的扩展方法实现。

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

### <a name="handle-interruptions-gracefully"></a>妥善处理中断

当用户尝试在其他技能当前处于活动状态时调用技能时，虚拟助理可以处理中断。 我们引入了 `TeamsSkillDialog` 并 `TeamsSwitchSkillDialog` 基于 Bot 框架的[SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs)和[SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)，以使用户能够从卡片操作切换技能经验。 若要处理此请求，虚拟助手将提示用户提供确认消息以切换技能。

![切换到新技能时的确认提示](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a>处理任务模块请求

若要将任务模块功能添加到虚拟助手中，虚拟助手活动处理程序中还包含另外两个方法： `OnTeamsTaskModuleFetchAsync` 和 `OnTeamsTaskModuleSubmitAsync` 。 这些方法从虚拟助理中侦听与任务模块相关的活动，确定与请求相关的技能，并将该请求转发给确定的技能。 

请求转发是通过[SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable)和方法进行的 `PostActivityAsync` 。 它返回 `InvokeResponse` 解析和转换为的响应 `TaskModuleResponse` 。

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

对于卡操作调度和任务模块响应，遵循类似的方法。 任务模块的提取和提交操作数据已更新，以包括 `skillId` 。 活动扩展方法 `GetSkillId` `skillId` 从提供有关需要调用的技能的详细信息的有效负载中提取。

下面是和方法的代码 `OnTeamsTaskModuleFetchAsync` 段 `OnTeamsTaskModuleSubmitAsync` 。

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

此外，所有技能域必须包含在 `validDomains` Virtual Assistant 的清单文件部分中，以便可以正确地通过技能呈现调用任务模块。

### <a name="handling-collaborative-app-scopes"></a>处理协作应用程序范围

团队应用可以存在于多个范围中，包括1:1 聊天、组聊天和频道。 核心虚拟助手模板专为1:1 聊天而设计。 作为启动体验的一部分，Virtual Assistant 会提示用户输入名称并维护用户状态。 由于该载入体验不适用于组聊天/频道范围，因此它已被删除。

技能应处理多个范围内的活动（1:1 聊天、组聊天和频道对话）。 如果不支持这些范围中的任何作用域，则技能应使用适当的消息进行响应。

已将以下处理函数添加到 Virtual Assistant core：

- 可以在没有来自组聊天或频道的任何文本消息的情况下调用虚拟助手。
- 在将邮件发送到派遣模块之前，将清除 Articulations （即，删除 @mention 必要的 "bot"）。

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

邮件扩展的命令是在应用程序清单文件中声明的。 邮件扩展用户界面由这些命令供电。 为使虚拟助理能够接通邮件扩展命令（作为附加技能），虚拟助理自己的清单必须包含这些命令。 还应将来自单个技能的清单中的命令添加到虚拟助理的清单中。 命令 ID 通过使用分隔符（）追加技能的应用 ID 来提供相关技能的相关信息 `:` 。

下面是技能清单文件中的一个代码段。

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

和，下面是对应的虚拟助手清单文件代码段。

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

一旦用户调用命令，虚拟助理就可以通过分析命令 ID 来标识相关技能，通过从命令 ID 删除额外后缀（）来更新活动， `:<skill_id>` 并将其转发到相应的技能。 技能代码不需要处理额外的后缀，因此避免了跨技能的命令 Id 之间的冲突。 通过此方法，所有上下文（"撰写"、"commandBox" 和 "message"）内的技能的所有搜索和操作命令都可以通过虚拟助手来供电。

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

某些邮件扩展活动不包含命令 ID。 例如， `composeExtension/selectItem` 仅包含 invoke 路器操作的值。 若要标识关联的技能，请在为 `skillId` 提供响应时将其附加到每个项目卡片 `OnTeamsMessagingExtensionQueryAsync` 。 （这类似于[将自适应卡片添加到虚拟助手](#add-adaptive-cards-to-your-virtual-assistant)的方法。

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a>示例：将聊天室应用模板转换为虚拟助理技能

[会议室](app-templates.md#book-a-room)是[Microsoft 团队 bot](../bots/what-are-bots.md) ，可让用户快速查找和保留从当前时间起30（默认）、60或90分钟的会议室。 书籍-会议室的 bot 作用域到个人或1:1 对话。

![具有 "书籍成为聊天室" 技能的虚拟助手](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

下面是引入的增量更改，用于将其转换为可附加到虚拟助理的技能。 可遵循类似的准则将任何现有的 v4 机器人转换为技能。

### <a name="skill-manifest"></a>技能清单

技能清单是一个 JSON 文件，该文件公开技能的消息终结点、id、名称和其他相关元数据（此清单与用于在 Microsoft 团队中添加应用程序的清单不同）虚拟助理需要一个指向此文件的路径作为附加技能的输入。 我们已将以下清单添加到 bot 的 wwwroot 文件夹中。

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

虚拟助手的调度模型建立在附加技能的 LUIS 模型之上。 调度模型标识每个文本活动的目的，并找出与之相关的技能。

在附加技能时，虚拟助手需要技能的 LUIS 模型（ `.lu` 格式）作为输入。 可以使用 botframework 工具将 LUIS json 转换为 `.lu` 格式。

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

为用户提供了两个主要命令的图书-一个聊天室：

- `Book room`
- `Manage Favorites`

我们构建了一个 LUIS 模型，了解这两个命令。 需要填写相应的密码 `cognitivemodels.json` 。 可在[此处](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json)找到相应的 LUIS JSON 文件，这就是相应 `.lu` 文件的外观。

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

使用此方法时，用户与的相关虚拟助理的任何命令问题， `book room` 或者 `manage favorites` 可以将其标识为与会议室 bot 相关联的命令，并将其转发到此技能。
另一方面，如果不键入 as （例如：），则书籍中的会议室 bot 需要使用 LUIS 模型来了解这些命令 `I want to manage my favorite rooms` 。

### <a name="multi-language-support"></a>多语言支持

对于此示例，我们仅创建了一个英语区域性的 LUIS 模型。 您可以创建与其他语言相对应的 LUIS 模型，并向添加条目 `cognitivemodels.json` 。

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

在 "luisFolder" 路径中，将并行添加相应的 `.lu` 文件。 文件夹结构应如下所示：

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

Virtual Assistant 用于 `SetLocaleMiddleware` 标识当前区域设置并调用相应的调度模型。 （Bot 框架活动具有此中间件使用的区域设置字段。）我们建议您也为自己的技能使用相同的。 聊天室的 bot 不使用此中间件，而是从 Bot 框架活动的[clientInfo 实体](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)中获取区域设置。

### <a name="claim-validation"></a>声明验证

我们已添加[claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) ，以将呼叫者限制为技能。 若要允许虚拟助理调用此技能，请 `AllowedCallers` `appsettings` 使用该特定虚拟助理的应用 ID 填充数组。

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

允许的呼叫者阵列可以限制哪些技能使用者可以访问技能。 将单个条目添加 `*` 到此阵列，以接受来自任何技能使用者的呼叫。

```
"AllowedCallers": [ "*" ],
```
可在[此处](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator)找到有关向技能添加声明验证的详细文档。

### <a name="card-refresh-limitation"></a>卡片刷新限制

尚不支持通过虚拟助理（[github 问题](https://github.com/microsoft/botbuilder-dotnet/issues/3686)）更新活动（卡片刷新）。 因此，我们已将所有的卡片刷新呼叫（）替换为 `UpdateActivityAsync` 发布新的电话卡呼叫（ `SendActivityAsync` ）。

### <a name="card-actions-and-task-module-flows"></a>卡片操作和任务模块流

若要将卡片操作或任务模块活动转发到相关联的技能，技能需要嵌入 `skillId` 到其中。
将任务模块的 "读取" 和 "提交操作" 负载修改为包含一个参数的会议室的 bot 卡片操作 `skillId` 。 

有关详细信息，请参阅本文档中的[这](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards)一节。

### <a name="handle-activities-from-group-chat-or-channel-scope"></a>处理来自组聊天或频道范围的活动

仅为私人聊天（个人/1：1作用域）设计了聊天室的 bot。 由于已将 Virtual Assistant 自定义为支持组聊天和频道作用域，因此可能会从这些范围调用虚拟助理，因此，会议室 bot 可能会获取相同的活动。 因此，可自定义书本的聊天室 bot 来处理这些活动。 检查已被置于会议室的 `OnMessageActivityAsync` 活动处理程序的方法中。

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

您还可以利用[Bot 框架解决方案库](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp)中现有的技能，或从头开始创建新的技能。 可在[此处](https://microsoft.github.io/botframework-solutions/overview/skills/)找到后续教程。 请参阅有关虚拟助理和技能体系结构的[文档](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)。

## <a name="sample-code-to-get-started"></a>入门示例代码

- [更新的 visual studio 模板](https://github.com/nebhagat/msteams-virtual-assistant-dotnet)
- [图书-会议室的技能代码](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill)

## <a name="virtual-assistant-known-limitations"></a>虚拟助理已知限制

- **EndOfConversation**。 技能在 `endOfConversation` 完成对话时应发送活动。 根据此活动，虚拟助理将结束与该特定技能相关的上下文，并返回到虚拟助理（根）上下文。 对于会议室 bot，在可以结束对话的情况下，没有明确的状态。 因此，我们不是 `endOfConversation` 从聊天室 bot 发送的，当用户想要返回到根上下文时，只需通过命令执行此操作即可 `start over` 。
- **卡片刷新**。 尚不支持通过虚拟助理进行卡片刷新。
- **邮件扩展**。：
  - 目前，虚拟助理最多可以支持十个命令用于邮件扩展。
  - 邮件扩展的配置不限定为单个命令，而是整个扩展本身。 这将通过虚拟助手限制每个单个技能的配置。
  - 邮件扩展命令 Id 的最大长度为[64 个字符](../resources/schema/manifest-schema.md#composeextensions)，37字符将用于嵌入技能信息。 因此，针对命令 ID 的更新限制限制为27个字符。
>
>
