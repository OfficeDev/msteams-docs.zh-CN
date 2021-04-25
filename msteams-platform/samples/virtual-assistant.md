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
# <a name="virtual-assistant-for-microsoft-teams"></a><span data-ttu-id="1b207-104">Microsoft Teams 虚拟助手</span><span class="sxs-lookup"><span data-stu-id="1b207-104">Virtual Assistant for Microsoft Teams</span></span>

<span data-ttu-id="1b207-105">虚拟助理是一个 Microsoft 开放源代码模板，它使您能够创建可靠的对话解决方案，同时保持对用户体验、组织品牌和必要数据的完全控制。</span><span class="sxs-lookup"><span data-stu-id="1b207-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="1b207-106">虚拟 [助手](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) 核心模板是基本构建基块，将构建虚拟助理所需的 Microsoft 技术汇集在一起，包括 [Bot Framework SDK、](https://github.com/microsoft/botframework-sdk)语言了解 [ () 、QnA ](https://www.luis.ai/) [Maker](https://www.qnamaker.ai/)以及基本功能，包括技能注册、链接帐户、为最终用户提供一系列无缝交互和体验的基本对话意图。</span><span class="sxs-lookup"><span data-stu-id="1b207-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), as well as essential capabilities including  skills registration, linked accounts, basic conversational intent to offer end users a range of seamless interactions and experiences.</span></span> <span data-ttu-id="1b207-107">此外，模板功能包括可重用对话技能的丰富 [示例](https://microsoft.github.io/botframework-solutions/overview/skills)。</span><span class="sxs-lookup"><span data-stu-id="1b207-107">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="1b207-108">个人技能可以集成到虚拟助理解决方案中，以启用多个方案。</span><span class="sxs-lookup"><span data-stu-id="1b207-108">Individual skills can be integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="1b207-109">使用 Bot Framework SDK，以源代码形式提供技能，使你可以根据需要自定义和扩展。</span><span class="sxs-lookup"><span data-stu-id="1b207-109">Using the Bot Framework SDK, Skills are presented in source code form enabling you to customize and extend as required.</span></span> <span data-ttu-id="1b207-110">请参阅 [什么是自动程序框架技能](https://microsoft.github.io/botframework-solutions/overview/skills/)。</span><span class="sxs-lookup"><span data-stu-id="1b207-110">See [What is a Bot Framework Skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span>

![虚拟助手概述图](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="1b207-112">使用调度模型的虚拟助理核心将短信活动 [路由到关联的](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) 技能。</span><span class="sxs-lookup"><span data-stu-id="1b207-112">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="1b207-113">实现注意事项</span><span class="sxs-lookup"><span data-stu-id="1b207-113">Implementation considerations</span></span>

<span data-ttu-id="1b207-114">添加虚拟助理的决定可包括许多决定因素，并且因组织不同而不同。</span><span class="sxs-lookup"><span data-stu-id="1b207-114">The decision to add a Virtual Assistant can include many determinants and differ for each organization.</span></span> <span data-ttu-id="1b207-115">以下是支持为组织实现虚拟助理的因素：</span><span class="sxs-lookup"><span data-stu-id="1b207-115">Here are the factors that support implementing a Virtual Assistant for your organization:</span></span>

- <span data-ttu-id="1b207-116">中央团队负责管理所有员工体验，并能够构建虚拟助理体验和管理核心体验的更新，包括新技能的添加。</span><span class="sxs-lookup"><span data-stu-id="1b207-116">A central team manages all employee experiences and has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
- <span data-ttu-id="1b207-117">多个应用程序存在于多个业务功能中，并且/或数量预计未来会增长。</span><span class="sxs-lookup"><span data-stu-id="1b207-117">Multiple applications exist across business functions and/or the number is expected to grow in the future.</span></span>
- <span data-ttu-id="1b207-118">现有应用程序可自定义，归组织所有，并可以转换为虚拟助理的技能。</span><span class="sxs-lookup"><span data-stu-id="1b207-118">Existing applications are customizable, owned by the organization, and can be converted into skills for a Virtual Assistant.</span></span>
- <span data-ttu-id="1b207-119">中央员工体验团队能够将自定义项影响现有应用，并提供必要指导，将现有应用程序作为虚拟助手体验中的技能进行集成</span><span class="sxs-lookup"><span data-stu-id="1b207-119">The central employee-experiences team is able to influence customizations to existing apps and provide necessary guidance for integrating existing applications as skills in Virtual Assistant experience</span></span>

![中央团队负责维护助手，业务职能团队贡献技能](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="1b207-121">创建以 Teams 为中心的虚拟助理</span><span class="sxs-lookup"><span data-stu-id="1b207-121">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="1b207-122">Microsoft [发布了一Visual Studio](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) 虚拟助手和技能的模板。</span><span class="sxs-lookup"><span data-stu-id="1b207-122">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="1b207-123">使用Visual Studio模板，可以创建一个虚拟助理，该虚拟助理由基于文本的体验提供支持，支持有限的富卡片和操作。</span><span class="sxs-lookup"><span data-stu-id="1b207-123">With the Visual Studio template, you can create a Virtual Assistant, powered by a text-based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="1b207-124">我们已增强基本Visual Studio模板，以包含 Microsoft Teams 平台功能并增强出色的 Teams 应用体验。</span><span class="sxs-lookup"><span data-stu-id="1b207-124">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="1b207-125">一些功能包括对丰富的自适应卡片、任务模块、团队/群组聊天和消息传递扩展的支持。</span><span class="sxs-lookup"><span data-stu-id="1b207-125">A few of the capabilities include support for rich adaptive cards, task modules, teams/group chats and messaging extensions.</span></span> <span data-ttu-id="1b207-126">*另请参阅* 教程 [：将虚拟助手扩展到 Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)。</span><span class="sxs-lookup"><span data-stu-id="1b207-126">*See also*, [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>

![虚拟助理解决方案高级关系图](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="1b207-128">将自适应卡片添加到虚拟助理</span><span class="sxs-lookup"><span data-stu-id="1b207-128">Add adaptive cards to your Virtual Assistant</span></span>

<span data-ttu-id="1b207-129">为了正确调度请求，你的虚拟助理需要识别正确的"显示"模型以及与之关联的相应技能。</span><span class="sxs-lookup"><span data-stu-id="1b207-129">To dispatch requests properly, your Virtual Assistant needs to identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="1b207-130">但是，调度机制不能用于卡片操作活动，因为与技能关联的函数函数模型可能无法针对卡片操作文本进行训练，因为这些文本是固定的预定义关键字，而不是来自用户的话。</span><span class="sxs-lookup"><span data-stu-id="1b207-130">However, the dispatching mechanism cannot be used for card action activities since the LUIS model associated with a skill may not be trained for card action texts since these are fixed, pre-defined keywords, not utterances from a user.</span></span>

<span data-ttu-id="1b207-131">我们通过将技能信息嵌入卡操作有效负载解决了这一问题。</span><span class="sxs-lookup"><span data-stu-id="1b207-131">We have resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="1b207-132">每个技能都应 `skillId` 嵌入卡片  `value` 操作字段中。</span><span class="sxs-lookup"><span data-stu-id="1b207-132">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="1b207-133">这是确保每个卡片操作活动都携带相关技能信息且虚拟助理可以利用此信息进行调度的最佳方法。</span><span class="sxs-lookup"><span data-stu-id="1b207-133">This is the best way to ensure that each card action activity carries the relevant skill information and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="1b207-134">以下是卡片操作数据示例。</span><span class="sxs-lookup"><span data-stu-id="1b207-134">Below is a card action data sample.</span></span> <span data-ttu-id="1b207-135">通过 `skillId` 提供构造函数，我们可以确保技能信息始终存在于卡片操作中。</span><span class="sxs-lookup"><span data-stu-id="1b207-135">By providing `skillId` in the constructor we ensure that skill information is always present in card actions.</span></span>

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

<span data-ttu-id="1b207-136">接下来，我们在 `SkillCardActionData` 虚拟助理模板中介绍从卡操作有效负载 `skillId` 中提取的类。</span><span class="sxs-lookup"><span data-stu-id="1b207-136">Next, we introduce `SkillCardActionData` class in the Virtual Assistant template to extract `skillId` from the card action payload.</span></span>

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

<span data-ttu-id="1b207-137">下面是从卡片操作数据  `skillId` 中提取的代码段。</span><span class="sxs-lookup"><span data-stu-id="1b207-137">Below is a code snippet to extract  `skillId` from card action data.</span></span> <span data-ttu-id="1b207-138">我们已在 Activity 类中将此方法作为扩展 [方法](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) 实现。</span><span class="sxs-lookup"><span data-stu-id="1b207-138">We implemented it as an  extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>

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

### <a name="handle-interruptions-gracefully"></a><span data-ttu-id="1b207-139">流畅地处理中断</span><span class="sxs-lookup"><span data-stu-id="1b207-139">Handle interruptions gracefully</span></span>

<span data-ttu-id="1b207-140">在用户尝试调用技能时，另一个技能当前处于活动状态时，虚拟助理可以处理中断。</span><span class="sxs-lookup"><span data-stu-id="1b207-140">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="1b207-141">我们已根据 Bot Framework 的 `TeamsSkillDialog` `TeamsSwitchSkillDialog` [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) 和 [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)引入了 和 ，以使用户能够从卡片操作切换技能体验。</span><span class="sxs-lookup"><span data-stu-id="1b207-141">we have introduced `TeamsSkillDialog` and `TeamsSwitchSkillDialog`, based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs), to enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="1b207-142">若要处理此请求，虚拟助理会提示用户发送确认消息以切换技能。</span><span class="sxs-lookup"><span data-stu-id="1b207-142">To handle this request the Virtual Assistant prompts the user with a confirmation message to switch skills.</span></span>

![切换到新技能时确认提示](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a><span data-ttu-id="1b207-144">处理任务模块请求</span><span class="sxs-lookup"><span data-stu-id="1b207-144">Handling task module requests</span></span>

<span data-ttu-id="1b207-145">若要将任务模块功能添加到虚拟助理，虚拟助理活动处理程序中包含另外两种方法： `OnTeamsTaskModuleFetchAsync` 和 `OnTeamsTaskModuleSubmitAsync` 。</span><span class="sxs-lookup"><span data-stu-id="1b207-145">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="1b207-146">这些方法侦听虚拟助理中与任务模块相关的活动，识别与请求关联的技能，将请求转发到标识的技能。</span><span class="sxs-lookup"><span data-stu-id="1b207-146">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="1b207-147">请求转发通过  [技能HttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true)方法 `PostActivityAsync` 完成。</span><span class="sxs-lookup"><span data-stu-id="1b207-147">Request forwarding is done via the  [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true), `PostActivityAsync` method.</span></span> <span data-ttu-id="1b207-148">它返回 响应， `InvokeResponse` 就像 解析并转换为 `TaskModuleResponse` 一样。</span><span class="sxs-lookup"><span data-stu-id="1b207-148">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>

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

<span data-ttu-id="1b207-149">卡片操作调度和任务模块响应也采用类似的方法。</span><span class="sxs-lookup"><span data-stu-id="1b207-149">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="1b207-150">任务模块提取和提交操作数据已更新为包含 `skillId` 。</span><span class="sxs-lookup"><span data-stu-id="1b207-150">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="1b207-151">Activity Extension `GetSkillId` 方法 `skillId` 从有效负载中提取，该负载提供有关需要调用的技能的详细信息。</span><span class="sxs-lookup"><span data-stu-id="1b207-151">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="1b207-152">下面是 和 方法的代码 `OnTeamsTaskModuleFetchAsync` `OnTeamsTaskModuleSubmitAsync` 段。</span><span class="sxs-lookup"><span data-stu-id="1b207-152">Below is a code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods.</span></span>

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

<span data-ttu-id="1b207-153">此外，所有技能域必须包含在虚拟助手清单文件的 部分中，以便通过技能调用的任务模块 `validDomains` 能够正确呈现。</span><span class="sxs-lookup"><span data-stu-id="1b207-153">Additionally, all skill domains must be included in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked via a skill render properly.</span></span>

### <a name="handling-collaborative-app-scopes"></a><span data-ttu-id="1b207-154">处理协作应用范围</span><span class="sxs-lookup"><span data-stu-id="1b207-154">Handling collaborative app scopes</span></span>

<span data-ttu-id="1b207-155">Teams 应用可以存在于多个范围，包括一对一聊天、群聊和频道。</span><span class="sxs-lookup"><span data-stu-id="1b207-155">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="1b207-156">核心虚拟助理模板专为一对一聊天设计。</span><span class="sxs-lookup"><span data-stu-id="1b207-156">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="1b207-157">作为载入体验的一部分，虚拟助理会提示用户输入名称并保持用户状态。</span><span class="sxs-lookup"><span data-stu-id="1b207-157">As part of the onboarding experience Virtual Assistant  prompts users for name and maintains user state.</span></span> <span data-ttu-id="1b207-158">由于该载入体验不适合群聊/频道范围，因此已将其删除。</span><span class="sxs-lookup"><span data-stu-id="1b207-158">Since that onboarding experience is not suited for group chat/channel scopes it has been removed.</span></span>

<span data-ttu-id="1b207-159">技能应处理 1：1 (、群聊和频道对话等多个) 。</span><span class="sxs-lookup"><span data-stu-id="1b207-159">Skills should handle activities in multiple scopes (1:1 chat, group chat, and channel conversation).</span></span> <span data-ttu-id="1b207-160">如果其中任何范围不受支持，技能应提供适当的消息进行响应。</span><span class="sxs-lookup"><span data-stu-id="1b207-160">If any of these scopes are not supported, skills should respond with an appropriate message.</span></span>

<span data-ttu-id="1b207-161">以下处理功能已添加到虚拟助理核心：</span><span class="sxs-lookup"><span data-stu-id="1b207-161">The following  processing functions have been added to Virtual Assistant core:</span></span>

- <span data-ttu-id="1b207-162">无需从群聊或频道调用任何文本消息，即可调用虚拟助理。</span><span class="sxs-lookup"><span data-stu-id="1b207-162">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
- <span data-ttu-id="1b207-163">在将邮件 (调度模块之前，@mention自动程序) 删除所需的自动程序。</span><span class="sxs-lookup"><span data-stu-id="1b207-163">Articulations are cleaned (i.e.,  remove the necessary @mention of the bot) before sending the message to the dispatch module.</span></span>

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

### <a name="handling-messaging-extensions"></a><span data-ttu-id="1b207-164">处理邮件扩展</span><span class="sxs-lookup"><span data-stu-id="1b207-164">Handling messaging extensions</span></span>

<span data-ttu-id="1b207-165">消息扩展的命令在应用清单文件中声明。</span><span class="sxs-lookup"><span data-stu-id="1b207-165">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="1b207-166">邮件扩展用户界面由这些命令支持。</span><span class="sxs-lookup"><span data-stu-id="1b207-166">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="1b207-167">若要使虚拟助理能够将消息传递扩展命令 (附加技能) ，虚拟助理自己的清单必须包含这些命令。</span><span class="sxs-lookup"><span data-stu-id="1b207-167">For a Virtual Assistant to power a messaging extension command (as an attached skill), a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="1b207-168">还应将单个技能清单中的命令添加到虚拟助理的清单中。</span><span class="sxs-lookup"><span data-stu-id="1b207-168">The commands from an individual skill's manifest should be added to the Virtual Assistant's manifest as well.</span></span> <span data-ttu-id="1b207-169">命令 ID 通过分隔符或参数来附加该技能的应用 ID，提供有关 `:` () 。</span><span class="sxs-lookup"><span data-stu-id="1b207-169">The command ID provides information about an associated skill by appending the skill's app ID via a separator (`:`).</span></span>

<span data-ttu-id="1b207-170">下面是技能清单文件的代码段。</span><span class="sxs-lookup"><span data-stu-id="1b207-170">Below is a snippet from a skill's manifest file.</span></span>

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

<span data-ttu-id="1b207-171">下面是相应的虚拟助理清单文件代码段。</span><span class="sxs-lookup"><span data-stu-id="1b207-171">And, below is the corresponding Virtual Assistant manifest file code snippet.</span></span>

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

<span data-ttu-id="1b207-172">用户调用命令后，虚拟助理可以通过分析命令 ID 来标识关联的技能，通过从命令 ID 中删除额外的后缀 () 来更新活动，然后将其转发到相应的技能。 `:<skill_id>`</span><span class="sxs-lookup"><span data-stu-id="1b207-172">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix (`:<skill_id>`) from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="1b207-173">技能的代码不需要处理额外的后缀，因此可以避免跨技能的命令标识发生冲突。</span><span class="sxs-lookup"><span data-stu-id="1b207-173">The code for a skill doesn't need to handle the extra suffix, thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="1b207-174">通过此方法，虚拟助理可以支持所有上下文中技能的所有搜索和操作 ("compose"、"commandBox"和"message") 。</span><span class="sxs-lookup"><span data-stu-id="1b207-174">With this approach, all the search and action commands of a skill within all contexts ("compose", "commandBox" and "message") can be powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="1b207-175">某些邮件扩展活动不包括命令 ID。</span><span class="sxs-lookup"><span data-stu-id="1b207-175">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="1b207-176">例如， `composeExtension/selectItem` 仅包含调用点击操作的值。</span><span class="sxs-lookup"><span data-stu-id="1b207-176">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="1b207-177">若要确定关联的技能， `skillId`  请附加到每个项目卡片，同时形成 对 的响应 `OnTeamsMessagingExtensionQueryAsync` 。</span><span class="sxs-lookup"><span data-stu-id="1b207-177">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="1b207-178"> (这类似于向虚拟助理添加自适应卡片 [的方法](#add-adaptive-cards-to-your-virtual-assistant)。</span><span class="sxs-lookup"><span data-stu-id="1b207-178">(This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a><span data-ttu-id="1b207-179">示例：将"预订房间"应用模板转换为虚拟助理技能</span><span class="sxs-lookup"><span data-stu-id="1b207-179">Example: Convert the Book-a-room app template to a Virtual Assistant skill</span></span>

<span data-ttu-id="1b207-180">[](app-templates.md#book-a-room)会议室预订是一个[Microsoft Teams](../bots/what-are-bots.md)自动程序，用户可以从当前时间开始快速查找会议室并保留 30 (默认) 、60 或 90 分钟的会议室。</span><span class="sxs-lookup"><span data-stu-id="1b207-180">[Book-a-room](app-templates.md#book-a-room) is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="1b207-181">Book-a-room bot 作用域为个人对话或 1：1 对话。</span><span class="sxs-lookup"><span data-stu-id="1b207-181">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

![具有"预订会议室"技能的虚拟助理](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="1b207-183">下面是引入的增量更改，以将其转换为可附加到虚拟助理的技能。</span><span class="sxs-lookup"><span data-stu-id="1b207-183">Followings are the delta changes introduced to convert it to a skill which can be attached to a Virtual Assistant.</span></span> <span data-ttu-id="1b207-184">可遵循类似的准则，将任何现有的 v4 机器人转换为技能。</span><span class="sxs-lookup"><span data-stu-id="1b207-184">Similar guidelines can be followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="1b207-185">技能清单</span><span class="sxs-lookup"><span data-stu-id="1b207-185">Skill manifest</span></span>

<span data-ttu-id="1b207-186">技能清单是一个 JSON 文件，用于公开技能的消息终结点、id、名称和其他相关元数据 (此清单与在 Microsoft Teams) 中旁加载应用的清单不同。虚拟助手需要此文件的路径作为输入来附加技能。</span><span class="sxs-lookup"><span data-stu-id="1b207-186">A skill manifest is a JSON file that exposes a skill's messaging endpoint, id, name, and other relevant metadata (this manifest is different than the manifest used for sideloading an app in Microsoft Teams) A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="1b207-187">我们已将以下清单添加到机器人的 wwwroot 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="1b207-187">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="1b207-188">实现"实现"的"实现"</span><span class="sxs-lookup"><span data-stu-id="1b207-188">LUIS Integration</span></span>

<span data-ttu-id="1b207-189">虚拟助理的调度模型基于附加技能的"函数""数字"模型构建。</span><span class="sxs-lookup"><span data-stu-id="1b207-189">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="1b207-190">调度模型可标识每个文本活动的意图，并找出与其关联的技能。</span><span class="sxs-lookup"><span data-stu-id="1b207-190">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="1b207-191">虚拟助手需要技能的" (模型 `.lu` "，) 附加技能时作为输入。</span><span class="sxs-lookup"><span data-stu-id="1b207-191">Virtual Assistant requires skill's LUIS model (in `.lu` format) as an input while attaching a skill.</span></span> <span data-ttu-id="1b207-192">可以使用 botframework-cli 工具将工作台 json 转换为 `.lu` 格式。</span><span class="sxs-lookup"><span data-stu-id="1b207-192">LUIS json can be converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="1b207-193">预订聊天室自动程序为用户提供了两个主要命令：</span><span class="sxs-lookup"><span data-stu-id="1b207-193">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="1b207-194">我们构建了一个了解这两个命令的"一个""一个"的"设计模型"。</span><span class="sxs-lookup"><span data-stu-id="1b207-194">We have built a LUIS model understanding these two commands.</span></span> <span data-ttu-id="1b207-195">需要在 中填充相应的密码 `cognitivemodels.json` 。</span><span class="sxs-lookup"><span data-stu-id="1b207-195">Corresponding secrets need to be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="1b207-196">可在此处找到相应的一个/或相应的[](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json)一个工作台 JSON 文件，这是对应 `.lu` 文件的外观。</span><span class="sxs-lookup"><span data-stu-id="1b207-196">The corresponding LUIS JSON file can be found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) and this is how the corresponding `.lu` file looks like.</span></span>

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

<span data-ttu-id="1b207-197">通过此方法，用户与虚拟助理相关的任何命令问题，或可标识为与书籍-聊天室自动程序关联的命令，并 `book room` `manage favorites` 转发到此技能。</span><span class="sxs-lookup"><span data-stu-id="1b207-197">With this approach, any command issues by a user to Virtual Assistant related to `book room` or `manage favorites` can be identified as a command associated with Book-a-room bot and is forwarded to this skill.</span></span>
<span data-ttu-id="1b207-198">另一方面，如果这些命令未像现在这样键入，则"预订会议室"机器人需要使用"会议室"模型来了解这些命令 (例如 `I want to manage my favorite rooms` ：) 。</span><span class="sxs-lookup"><span data-stu-id="1b207-198">On the other hand, Book-a-room room bot needs to use LUIS model to understand these commands if they are not typed as is (for example: `I want to manage my favorite rooms`).</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="1b207-199">多语言支持</span><span class="sxs-lookup"><span data-stu-id="1b207-199">Multi-Language support</span></span>

<span data-ttu-id="1b207-200">对于此示例，我们仅创建了一个具有英语区域性的"处理方式"模型。</span><span class="sxs-lookup"><span data-stu-id="1b207-200">For this example, we have only created a LUIS model with English culture.</span></span> <span data-ttu-id="1b207-201">你可以创建与其他语言对应的分卡模型，并添加条目 `cognitivemodels.json` 。</span><span class="sxs-lookup"><span data-stu-id="1b207-201">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="1b207-202">并行，在 `.lu` "用户文件夹路径"中添加相应的文件。</span><span class="sxs-lookup"><span data-stu-id="1b207-202">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="1b207-203">文件夹结构应如下所示：</span><span class="sxs-lookup"><span data-stu-id="1b207-203">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="1b207-204">按如下所示更新 botskills 命令以修改 `languages` 参数：</span><span class="sxs-lookup"><span data-stu-id="1b207-204">Update botskills command as follows to modify `languages` parameter:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="1b207-205">虚拟助理 `SetLocaleMiddleware` 用于标识当前区域设置并调用相应的调度模型。</span><span class="sxs-lookup"><span data-stu-id="1b207-205">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="1b207-206"> (自动程序框架活动具有此中间件所使用的区域设置字段。) 我们建议也使用相同的技能。</span><span class="sxs-lookup"><span data-stu-id="1b207-206">(Bot framework activity has locale field which is used by this middleware.) We recommend to use the same for your skill as well.</span></span> <span data-ttu-id="1b207-207">预订聊天室机器人不会使用此中间件，而是从 Bot 框架活动的 [clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)实体获取区域设置。</span><span class="sxs-lookup"><span data-stu-id="1b207-207">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="1b207-208">声明验证</span><span class="sxs-lookup"><span data-stu-id="1b207-208">Claim validation</span></span>

<span data-ttu-id="1b207-209">我们添加了 [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) 来限制呼叫者使用技能。</span><span class="sxs-lookup"><span data-stu-id="1b207-209">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="1b207-210">若要允许虚拟助理调用此技能，请用该特定 `AllowedCallers` `appsettings` 虚拟助理的应用 ID 填充数组。</span><span class="sxs-lookup"><span data-stu-id="1b207-210">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="1b207-211">允许的调用方数组可以限制使用者可以访问该技能的技能。</span><span class="sxs-lookup"><span data-stu-id="1b207-211">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="1b207-212">向此数组 `*` 添加单个条目，以接受来自任何技能使用者的呼叫。</span><span class="sxs-lookup"><span data-stu-id="1b207-212">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```
<span data-ttu-id="1b207-213">有关向技能添加声明验证的详细文档，请参阅[。](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="1b207-213">Detailed documentation for adding claims validation to a skill can be found [here](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).</span></span>

### <a name="card-refresh-limitation"></a><span data-ttu-id="1b207-214">卡片刷新限制</span><span class="sxs-lookup"><span data-stu-id="1b207-214">Card refresh limitation</span></span>

<span data-ttu-id="1b207-215">目前尚不 ([github](https://github.com/microsoft/botbuilder-dotnet/issues/3686) 问题) 虚拟助理更新 (刷新) 。</span><span class="sxs-lookup"><span data-stu-id="1b207-215">Updating activity (card refresh) is not supported yet via Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="1b207-216">因此，我们已使用发布新卡片呼叫 () 所有卡片刷新 `UpdateActivityAsync` `SendActivityAsync` () 。</span><span class="sxs-lookup"><span data-stu-id="1b207-216">Hence, we have replaced all card refresh calls (`UpdateActivityAsync`) with posting new card calls(`SendActivityAsync`).</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="1b207-217">卡片操作和任务模块流</span><span class="sxs-lookup"><span data-stu-id="1b207-217">Card actions and task module flows</span></span>

<span data-ttu-id="1b207-218">若要将卡片操作或任务模块活动转发到关联技能，技能需要嵌入 `skillId` 到该技能中。</span><span class="sxs-lookup"><span data-stu-id="1b207-218">To forward card action or task module activities to an associated skill, the skill needs to embed `skillId` to it.</span></span>
<span data-ttu-id="1b207-219">书籍-会议室自动程序卡操作、任务模块提取和提交操作有效负载被修改为包含 `skillId` 为参数。</span><span class="sxs-lookup"><span data-stu-id="1b207-219">Book-a-room bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="1b207-220">有关详细信息，请参阅 [本文档](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) 中的此部分。</span><span class="sxs-lookup"><span data-stu-id="1b207-220">For more information refer [this](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="1b207-221">处理群聊或频道范围中的活动</span><span class="sxs-lookup"><span data-stu-id="1b207-221">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="1b207-222">预订聊天室自动程序专为私人聊天 (/1：1 范围) 。</span><span class="sxs-lookup"><span data-stu-id="1b207-222">Book-a-room bot is designed for private chats (personal/1:1 scope) only.</span></span> <span data-ttu-id="1b207-223">由于我们已自定义虚拟助理以支持群聊和频道范围，因此可能会从这些范围调用虚拟助理，因此，预订聊天室机器人可能会获得相同的活动。</span><span class="sxs-lookup"><span data-stu-id="1b207-223">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant might be invoked from these scopes and thus, Book-a-room bot might get activities for the same.</span></span> <span data-ttu-id="1b207-224">因此，书籍聊天室自动程序已自定义为处理这些活动。</span><span class="sxs-lookup"><span data-stu-id="1b207-224">Hence Book-a-room bot is customized to handle those activities.</span></span> <span data-ttu-id="1b207-225">检查已放入 `OnMessageActivityAsync` Book-a-room bot 的活动处理程序的方法中。</span><span class="sxs-lookup"><span data-stu-id="1b207-225">The check has been put in `OnMessageActivityAsync` methods of Book-a-room bot's activity handler.</span></span>

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

<span data-ttu-id="1b207-226">还可以利用 Bot Framework [解决方案](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) 存储库中的现有技能，或从头开始创建新技能。</span><span class="sxs-lookup"><span data-stu-id="1b207-226">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="1b207-227">稍后的教程可在此处 [找到](https://microsoft.github.io/botframework-solutions/overview/skills/)。</span><span class="sxs-lookup"><span data-stu-id="1b207-227">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="1b207-228">请参阅虚拟 [助理和](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) 技能体系结构文档。</span><span class="sxs-lookup"><span data-stu-id="1b207-228">Please refer to [documentation](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) for Virtual Assistant and skills architecture.</span></span>

## <a name="code-sample"></a><span data-ttu-id="1b207-229">代码示例</span><span class="sxs-lookup"><span data-stu-id="1b207-229">Code sample</span></span>

| <span data-ttu-id="1b207-230">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="1b207-230">**Sample name**</span></span> | <span data-ttu-id="1b207-231">**说明**</span><span class="sxs-lookup"><span data-stu-id="1b207-231">**Description**</span></span> | <span data-ttu-id="1b207-232">**C#**</span><span class="sxs-lookup"><span data-stu-id="1b207-232">**C#**</span></span> | <span data-ttu-id="1b207-233">**.NET**</span><span class="sxs-lookup"><span data-stu-id="1b207-233">**.NET**</span></span> |
|----------|-----------------|----------|------------------|
| <span data-ttu-id="1b207-234">更新的 Visual Studio 模板</span><span class="sxs-lookup"><span data-stu-id="1b207-234">Updated visual studio template</span></span> | <span data-ttu-id="1b207-235">用于支持团队功能的自定义模板。</span><span class="sxs-lookup"><span data-stu-id="1b207-235">Customized template to support teams capabilities.</span></span> | [<span data-ttu-id="1b207-236">View</span><span class="sxs-lookup"><span data-stu-id="1b207-236">View</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |
| <span data-ttu-id="1b207-237">预订聊天室机器人技能代码</span><span class="sxs-lookup"><span data-stu-id="1b207-237">Book-a-room bot skill code</span></span> | <span data-ttu-id="1b207-238">可让你快速查找并预订会议室。</span><span class="sxs-lookup"><span data-stu-id="1b207-238">Lets you quickly find and book a meeting room on the go.</span></span> |  | [<span data-ttu-id="1b207-239">View</span><span class="sxs-lookup"><span data-stu-id="1b207-239">View</span></span>](https://github.com/nebhagat/msteams-virtual-assistant-dotnet) |



## <a name="virtual-assistant-known-limitations"></a><span data-ttu-id="1b207-240">虚拟助理已知限制</span><span class="sxs-lookup"><span data-stu-id="1b207-240">Virtual Assistant known limitations</span></span>

- <span data-ttu-id="1b207-241">**EndOfConversation**。</span><span class="sxs-lookup"><span data-stu-id="1b207-241">**EndOfConversation**.</span></span> <span data-ttu-id="1b207-242">技能应在对话 `endOfConversation` 完成时发送活动。</span><span class="sxs-lookup"><span data-stu-id="1b207-242">A skill should send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="1b207-243">虚拟助理将基于此活动结束具有该特定技能的上下文，并返回到虚拟助理的 (根) 上下文。</span><span class="sxs-lookup"><span data-stu-id="1b207-243">basis this activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's (root) context.</span></span> <span data-ttu-id="1b207-244">对于"预订聊天室"机器人，没有可以结束对话的清晰状态。</span><span class="sxs-lookup"><span data-stu-id="1b207-244">For Book-a-room bot, there is no clear state where conversation can be ended.</span></span> <span data-ttu-id="1b207-245">因此，我们尚未从 Book-a-room bot 发送，并且当用户想要返回根上下文时，他们 `endOfConversation` 只需通过命令 `start over` 执行。</span><span class="sxs-lookup"><span data-stu-id="1b207-245">Hence we have not sent `endOfConversation` from Book-a-room bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>
- <span data-ttu-id="1b207-246">**卡片刷新**。</span><span class="sxs-lookup"><span data-stu-id="1b207-246">**Card refresh**.</span></span> <span data-ttu-id="1b207-247">尚不支持通过虚拟助理进行卡片刷新。</span><span class="sxs-lookup"><span data-stu-id="1b207-247">Card refreshes is not yet supported through Virtual Assistant.</span></span>
- <span data-ttu-id="1b207-248">**邮件扩展 。：**</span><span class="sxs-lookup"><span data-stu-id="1b207-248">**Messaging extensions**.:</span></span>
  - <span data-ttu-id="1b207-249">目前，虚拟助理最多可支持 10 个邮件扩展命令。</span><span class="sxs-lookup"><span data-stu-id="1b207-249">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  - <span data-ttu-id="1b207-250">邮件扩展的配置范围不是单个命令，而是整个扩展本身。</span><span class="sxs-lookup"><span data-stu-id="1b207-250">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="1b207-251">这将通过虚拟助理限制各个技能的配置。</span><span class="sxs-lookup"><span data-stu-id="1b207-251">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  - <span data-ttu-id="1b207-252">消息扩展命令 ID 的最大长度为 [64 个字符](../resources/schema/manifest-schema.md#composeextensions) ，37 个字符将用于嵌入技能信息。</span><span class="sxs-lookup"><span data-stu-id="1b207-252">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters will be used for embedding skill information.</span></span> <span data-ttu-id="1b207-253">因此，命令 ID 的更新约束限制为 27 个字符。</span><span class="sxs-lookup"><span data-stu-id="1b207-253">Thus, updated constraints for command ID are limited to 27 characters.</span></span>
>
>
