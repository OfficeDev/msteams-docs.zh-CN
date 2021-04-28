---
title: 创建虚拟助理
description: 如何创建虚拟助理机器人和技能以在 Microsoft Teams 中使用
localization_priority: Normal
ms.topic: how-to
keywords: teams 虚拟助理机器人
ms.openlocfilehash: 80a308050317e8a211b8f7a9e2dd459c1572af18
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058675"
---
# <a name="create-virtual-assistant"></a><span data-ttu-id="a6fce-104">创建虚拟助理</span><span class="sxs-lookup"><span data-stu-id="a6fce-104">Create Virtual Assistant</span></span> 

<span data-ttu-id="a6fce-105">虚拟助理是一个 Microsoft 开放源代码模板，它使您能够创建可靠的对话解决方案，同时保持对用户体验、组织品牌和必要数据的完全控制。</span><span class="sxs-lookup"><span data-stu-id="a6fce-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="a6fce-106">虚拟[助理核心](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template)模板是基本构建基块，将构建虚拟助理所需的 Microsoft 技术汇集在一起，包括[Bot Framework SDK、Language](https://github.com/microsoft/botframework-sdk) [Understanding (MICROSOFT) ](https://www.luis.ai/) [、QnA Maker。](https://www.qnamaker.ai/)</span><span class="sxs-lookup"><span data-stu-id="a6fce-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/).</span></span> <span data-ttu-id="a6fce-107">它还整合了基本功能，包括技能注册、链接帐户、基本对话意图，以便为用户提供一系列无缝交互和体验。</span><span class="sxs-lookup"><span data-stu-id="a6fce-107">It also brings together the essential capabilities including  skills registration, linked accounts, basic conversational intent to offer a range of seamless interactions and experiences to users.</span></span> <span data-ttu-id="a6fce-108">此外，模板功能包括可重用对话技能的丰富 [示例](https://microsoft.github.io/botframework-solutions/overview/skills)。</span><span class="sxs-lookup"><span data-stu-id="a6fce-108">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="a6fce-109">个人技能集成在虚拟助理解决方案中，以实现多个方案。</span><span class="sxs-lookup"><span data-stu-id="a6fce-109">Individual skills are integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="a6fce-110">使用 Bot Framework SDK，技能以源代码形式呈现，让你可以根据需要进行自定义和扩展。</span><span class="sxs-lookup"><span data-stu-id="a6fce-110">Using the Bot Framework SDK, skills are presented in source code form, enabling you to customize and extend as required.</span></span> <span data-ttu-id="a6fce-111">有关 Bot Framework 技能详细信息，请参阅 [什么是 Bot Framework 技能](https://microsoft.github.io/botframework-solutions/overview/skills/)。</span><span class="sxs-lookup"><span data-stu-id="a6fce-111">For more information on skills of Bot Framework, see [What is a Bot Framework skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="a6fce-112">本文档将指导你了解组织的虚拟助理实施注意事项、如何创建以 Teams 为中心的虚拟助理、相关示例、代码示例和虚拟助理的限制。</span><span class="sxs-lookup"><span data-stu-id="a6fce-112">This document guides you on Virtual Assistant implementation considerations for organizations, how to create a Teams focused Virtual Assistant, related example, code sample and limitations of Virtual Assistant.</span></span>
<span data-ttu-id="a6fce-113">下图显示了虚拟助理的概述：</span><span class="sxs-lookup"><span data-stu-id="a6fce-113">The following image displays the overview of virtual assistant:</span></span>

![虚拟助手概述图](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="a6fce-115">使用调度模型的虚拟助理核心将短信活动 [路由到关联的](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) 技能。</span><span class="sxs-lookup"><span data-stu-id="a6fce-115">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs&preserve-view=true) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="a6fce-116">实现注意事项</span><span class="sxs-lookup"><span data-stu-id="a6fce-116">Implementation considerations</span></span>

<span data-ttu-id="a6fce-117">添加虚拟助理的决定包括许多决定因素，并且每个组织有所不同。</span><span class="sxs-lookup"><span data-stu-id="a6fce-117">The decision to add a Virtual Assistant includes many determinants and differs for each organization.</span></span> <span data-ttu-id="a6fce-118">您的组织实现虚拟助理的支持因素如下所示：</span><span class="sxs-lookup"><span data-stu-id="a6fce-118">The supporting factors of a Virtual Assistant implementation for your organization are as follows:</span></span>

* <span data-ttu-id="a6fce-119">中央团队管理所有员工体验。</span><span class="sxs-lookup"><span data-stu-id="a6fce-119">A central team manages all employee experiences.</span></span> <span data-ttu-id="a6fce-120">它能够构建虚拟助理体验和管理核心体验的更新，包括新技能的添加。</span><span class="sxs-lookup"><span data-stu-id="a6fce-120">It has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
* <span data-ttu-id="a6fce-121">跨业务功能存在多个应用程序，预计数量今后会增长。</span><span class="sxs-lookup"><span data-stu-id="a6fce-121">Multiple applications exist across business functions and the number is expected to grow in the future.</span></span>
* <span data-ttu-id="a6fce-122">现有应用程序可自定义，归组织所有，并转换为虚拟助理的技能。</span><span class="sxs-lookup"><span data-stu-id="a6fce-122">Existing applications are customizable, owned by the organization, and are converted into skills for a Virtual Assistant.</span></span>
* <span data-ttu-id="a6fce-123">中央员工体验团队能够将自定义设置影响现有应用。</span><span class="sxs-lookup"><span data-stu-id="a6fce-123">The central employee experiences team is able to influence customizations to existing apps.</span></span> <span data-ttu-id="a6fce-124">它还提供有关将现有应用程序作为虚拟助理体验技能进行集成的必要指导。</span><span class="sxs-lookup"><span data-stu-id="a6fce-124">It also provides necessary guidance for integrating existing applications as skills in Virtual Assistant experience.</span></span>   
<span data-ttu-id="a6fce-125">下图显示了虚拟助理的业务功能：</span><span class="sxs-lookup"><span data-stu-id="a6fce-125">The following image displays the business functions of Virtual Assistant:</span></span> 

![中央团队负责维护助手，业务职能团队贡献技能](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="a6fce-127">创建以 Teams 为中心的虚拟助理</span><span class="sxs-lookup"><span data-stu-id="a6fce-127">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="a6fce-128">Microsoft [发布了一Visual Studio](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) 虚拟助手和技能的模板。</span><span class="sxs-lookup"><span data-stu-id="a6fce-128">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="a6fce-129">使用Visual Studio模板，可以创建虚拟助理，该虚拟助理由基于文本的体验提供支持，支持具有操作限制的富卡片。</span><span class="sxs-lookup"><span data-stu-id="a6fce-129">With the Visual Studio template, you can create a Virtual Assistant, powered by a text based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="a6fce-130">我们已增强基本Visual Studio模板，以包含 Microsoft Teams 平台功能并增强出色的 Teams 应用体验。</span><span class="sxs-lookup"><span data-stu-id="a6fce-130">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="a6fce-131">一些功能包括对丰富的自适应卡片、任务模块、团队或群聊以及消息传递扩展的支持。</span><span class="sxs-lookup"><span data-stu-id="a6fce-131">A few of the capabilities include support for rich Adaptive Cards, task modules, teams or group chats and messaging extensions.</span></span> <span data-ttu-id="a6fce-132">有关将虚拟助理扩展到 Microsoft Teams 中有关详细信息，请参阅[教程：将虚拟助理扩展到 Microsoft Teams。](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)</span><span class="sxs-lookup"><span data-stu-id="a6fce-132">For more information on extending Virtual Assistant to Microsoft Teams, see [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>    
<span data-ttu-id="a6fce-133">下图显示了虚拟助理解决方案高级图表：</span><span class="sxs-lookup"><span data-stu-id="a6fce-133">The following image displays the high level diagram of a Virtual Assistant solution:</span></span>

![虚拟助理解决方案高级关系图](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="a6fce-135">将自适应卡片添加到虚拟助理</span><span class="sxs-lookup"><span data-stu-id="a6fce-135">Add Adaptive Cards to your Virtual Assistant</span></span>

<span data-ttu-id="a6fce-136">为了正确调度请求，你的虚拟助理必须确定正确的"显示方式"模型以及与之关联的相应技能。</span><span class="sxs-lookup"><span data-stu-id="a6fce-136">To dispatch requests properly, your Virtual Assistant must identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="a6fce-137">但是，调度机制不能用于卡片操作活动，因为与技能关联的"图形模型"已经过卡片操作文本培训。</span><span class="sxs-lookup"><span data-stu-id="a6fce-137">However, the dispatching mechanism cannot be used for card action activities as the LUIS model associated with a skill, is trained for card action texts.</span></span> <span data-ttu-id="a6fce-138">卡片操作文本是固定的预定义关键字，不会从用户进行注释。</span><span class="sxs-lookup"><span data-stu-id="a6fce-138">The card action texts are fixed, pre-defined keywords, and not commented from a user.</span></span>

<span data-ttu-id="a6fce-139">通过将技能信息嵌入卡片操作有效负载中，可以解决此问题。</span><span class="sxs-lookup"><span data-stu-id="a6fce-139">This drawback is resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="a6fce-140">每个技能都应 `skillId` 嵌入卡片  `value` 操作字段中。</span><span class="sxs-lookup"><span data-stu-id="a6fce-140">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="a6fce-141">必须确保每个卡片操作活动都携带相关的技能信息，并且虚拟助理可以利用此信息进行调度。</span><span class="sxs-lookup"><span data-stu-id="a6fce-141">You must ensure that each card action activity carries the relevant skill information, and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="a6fce-142">你必须在 `skillId` 构造函数中提供，以确保技能信息始终存在于卡片操作中。</span><span class="sxs-lookup"><span data-stu-id="a6fce-142">You must provide `skillId` in the constructor to ensure that the skill information is always present in card actions.</span></span>
<span data-ttu-id="a6fce-143">卡片操作数据示例代码显示在以下部分中：</span><span class="sxs-lookup"><span data-stu-id="a6fce-143">A card action data sample code is shown in the following section:</span></span>
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

<span data-ttu-id="a6fce-144">接下来 `SkillCardActionData` ，将引入虚拟助理模板中的类以从 `skillId` 卡操作有效负载中提取。</span><span class="sxs-lookup"><span data-stu-id="a6fce-144">Next, `SkillCardActionData` class in the Virtual Assistant template is introduces to extract `skillId` from the card action payload.</span></span>
<span data-ttu-id="a6fce-145">以下部分显示了从  `skillId` 卡操作有效负载中提取的代码段：</span><span class="sxs-lookup"><span data-stu-id="a6fce-145">A code snippet to extract  `skillId` from card action payload is shown in the following section:</span></span>

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

<span data-ttu-id="a6fce-146">实现通过 Activity 类中的扩展 [方法](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) 完成。</span><span class="sxs-lookup"><span data-stu-id="a6fce-146">The implementation is done by an extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>
<span data-ttu-id="a6fce-147">以下部分显示了从  `skillId` 卡片操作数据中提取的代码段：</span><span class="sxs-lookup"><span data-stu-id="a6fce-147">A code snippet to extract  `skillId` from card action data is shown in the following section:</span></span>

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

### <a name="handle-interruptions"></a><span data-ttu-id="a6fce-148">处理中断</span><span class="sxs-lookup"><span data-stu-id="a6fce-148">Handle interruptions</span></span>

<span data-ttu-id="a6fce-149">在用户尝试调用技能时，另一个技能当前处于活动状态时，虚拟助理可以处理中断。</span><span class="sxs-lookup"><span data-stu-id="a6fce-149">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="a6fce-150">`TeamsSkillDialog`和 `TeamsSwitchSkillDialog` 基于 Bot Framework 的 [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) 和 [SwitchSkillDialog 引入](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)。</span><span class="sxs-lookup"><span data-stu-id="a6fce-150">`TeamsSkillDialog`, and `TeamsSwitchSkillDialog`are introduced based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs).</span></span> <span data-ttu-id="a6fce-151">它们使用户能够从卡片操作切换技能体验。</span><span class="sxs-lookup"><span data-stu-id="a6fce-151">They enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="a6fce-152">为了处理此请求，虚拟助理会向用户提示确认消息以切换技能。</span><span class="sxs-lookup"><span data-stu-id="a6fce-152">To handle this request, the Virtual Assistant prompts the user with a confirmation message to switch skills.</span></span>

![切换到新技能时确认提示](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handle-task-module-requests"></a><span data-ttu-id="a6fce-154">处理任务模块请求</span><span class="sxs-lookup"><span data-stu-id="a6fce-154">Handle task module requests</span></span>

<span data-ttu-id="a6fce-155">若要将任务模块功能添加到虚拟助理，虚拟助理活动处理程序中包含另外两种方法： `OnTeamsTaskModuleFetchAsync` 和 `OnTeamsTaskModuleSubmitAsync` 。</span><span class="sxs-lookup"><span data-stu-id="a6fce-155">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="a6fce-156">这些方法侦听虚拟助理中与任务模块相关的活动，识别与请求关联的技能，将请求转发到标识的技能。</span><span class="sxs-lookup"><span data-stu-id="a6fce-156">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="a6fce-157">请求转发通过 [技能HttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true)方法 `PostActivityAsync` 完成。</span><span class="sxs-lookup"><span data-stu-id="a6fce-157">Request forwarding is done through the [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable&preserve-view=true), `PostActivityAsync` method.</span></span> <span data-ttu-id="a6fce-158">它返回 响应， `InvokeResponse` 就像 解析并转换为 `TaskModuleResponse` 一样。</span><span class="sxs-lookup"><span data-stu-id="a6fce-158">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>


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

<span data-ttu-id="a6fce-159">卡片操作调度和任务模块响应也采用类似的方法。</span><span class="sxs-lookup"><span data-stu-id="a6fce-159">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="a6fce-160">任务模块提取和提交操作数据已更新为包含 `skillId` 。</span><span class="sxs-lookup"><span data-stu-id="a6fce-160">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="a6fce-161">Activity Extension `GetSkillId` 方法 `skillId` 从有效负载中提取，该负载提供有关需要调用的技能的详细信息。</span><span class="sxs-lookup"><span data-stu-id="a6fce-161">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="a6fce-162">以下部分提供了 `OnTeamsTaskModuleFetchAsync` 和 `OnTeamsTaskModuleSubmitAsync` 方法的代码段：</span><span class="sxs-lookup"><span data-stu-id="a6fce-162">The code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods are given in the following section:</span></span>

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

<span data-ttu-id="a6fce-163">此外，还必须在虚拟助理的清单文件的 部分包含所有技能域，以便通过技能调用的任务模块 `validDomains` 正确呈现。</span><span class="sxs-lookup"><span data-stu-id="a6fce-163">Additionally, you must include all skill domains in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked through a skill render properly.</span></span>

### <a name="handle-collaborative-app-scopes"></a><span data-ttu-id="a6fce-164">处理协作应用范围</span><span class="sxs-lookup"><span data-stu-id="a6fce-164">Handle collaborative app scopes</span></span>

<span data-ttu-id="a6fce-165">Teams 应用可以存在于多个范围，包括一对一聊天、群聊和频道。</span><span class="sxs-lookup"><span data-stu-id="a6fce-165">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="a6fce-166">核心虚拟助理模板专为一对一聊天设计。</span><span class="sxs-lookup"><span data-stu-id="a6fce-166">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="a6fce-167">作为载入体验的一部分，虚拟助理会提示用户输入名称并保持用户状态。</span><span class="sxs-lookup"><span data-stu-id="a6fce-167">As part of the onboarding experience Virtual Assistant prompts users for name and maintains user state.</span></span> <span data-ttu-id="a6fce-168">由于该载入体验不适合群聊或频道范围，因此已将其删除。</span><span class="sxs-lookup"><span data-stu-id="a6fce-168">Since that onboarding experience is not suited for group chat or channel scopes it has been removed.</span></span>

<span data-ttu-id="a6fce-169">技能应处理多个范围的活动，如一对一聊天、群聊和频道对话。</span><span class="sxs-lookup"><span data-stu-id="a6fce-169">Skills should handle activities in multiple scopes, such as 1:1 chat, group chat, and channel conversation.</span></span> <span data-ttu-id="a6fce-170">如果其中任何范围不受支持，技能必须通过相应的消息进行响应。</span><span class="sxs-lookup"><span data-stu-id="a6fce-170">If any of these scopes are not supported, skills must respond with an appropriate message.</span></span>

<span data-ttu-id="a6fce-171">以下处理功能已添加到虚拟助理核心：</span><span class="sxs-lookup"><span data-stu-id="a6fce-171">The following  processing functions have been added to Virtual Assistant core:</span></span>

* <span data-ttu-id="a6fce-172">无需从群聊或频道调用任何文本消息，即可调用虚拟助理。</span><span class="sxs-lookup"><span data-stu-id="a6fce-172">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
* <span data-ttu-id="a6fce-173">在将邮件发送到调度模块之前，先清除邮件。</span><span class="sxs-lookup"><span data-stu-id="a6fce-173">Articulations are cleaned before sending the message to the dispatch module.</span></span> <span data-ttu-id="a6fce-174">例如，删除@mention的必需文件。</span><span class="sxs-lookup"><span data-stu-id="a6fce-174">For example, remove the necessary @mention of the bot.</span></span>

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

### <a name="handle-messaging-extensions"></a><span data-ttu-id="a6fce-175">处理邮件扩展</span><span class="sxs-lookup"><span data-stu-id="a6fce-175">Handle messaging extensions</span></span>

<span data-ttu-id="a6fce-176">消息扩展的命令在应用清单文件中声明。</span><span class="sxs-lookup"><span data-stu-id="a6fce-176">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="a6fce-177">邮件扩展用户界面由这些命令支持。</span><span class="sxs-lookup"><span data-stu-id="a6fce-177">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="a6fce-178">虚拟助理必须包含这些命令，虚拟助理自己的清单才能作为附加技能来为消息传递扩展命令提供电源。</span><span class="sxs-lookup"><span data-stu-id="a6fce-178">For a Virtual Assistant to power a messaging extension command as an attached skill, a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="a6fce-179">必须将单个技能清单中的命令添加到虚拟助理的清单中。</span><span class="sxs-lookup"><span data-stu-id="a6fce-179">You must add the commands from an individual skill's manifest to the Virtual Assistant's manifest.</span></span> <span data-ttu-id="a6fce-180">命令 ID 通过分隔符附加该技能的应用 ID，提供有关关联技能的信息 `:` 。</span><span class="sxs-lookup"><span data-stu-id="a6fce-180">The command ID provides information about an associated skill by appending the skill's app ID through a separator `:`.</span></span>

<span data-ttu-id="a6fce-181">技能清单文件的代码段显示在以下部分中：</span><span class="sxs-lookup"><span data-stu-id="a6fce-181">The snippet from a skill's manifest file is shown in the following section:</span></span>

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

<span data-ttu-id="a6fce-182">以下部分显示了相应的虚拟助理清单文件代码段：</span><span class="sxs-lookup"><span data-stu-id="a6fce-182">The corresponding Virtual Assistant manifest file code snippet is shown in the following section:</span></span>

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

<span data-ttu-id="a6fce-183">用户调用命令后，虚拟助理可以通过分析命令 ID 来标识关联的技能，通过从命令 ID 中删除额外的后缀来更新活动，然后将其转发到相应的技能 `:<skill_id>` 。</span><span class="sxs-lookup"><span data-stu-id="a6fce-183">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix `:<skill_id>` from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="a6fce-184">技能的代码不需要处理额外的后缀。</span><span class="sxs-lookup"><span data-stu-id="a6fce-184">The code for a skill doesnot need to handle the extra suffix.</span></span> <span data-ttu-id="a6fce-185">因此，可以避免跨技能的命令 ID 冲突。</span><span class="sxs-lookup"><span data-stu-id="a6fce-185">Thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="a6fce-186">通过此方法，所有上下文中技能的所有搜索和操作命令（如 **compose、commandBox** 和 **message）** 都由虚拟助理提供支持。</span><span class="sxs-lookup"><span data-stu-id="a6fce-186">With this approach, all the search and action commands of a skill within all contexts, such as **compose**, **commandBox** and **message** are powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="a6fce-187">某些邮件扩展活动不包括命令 ID。</span><span class="sxs-lookup"><span data-stu-id="a6fce-187">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="a6fce-188">例如， `composeExtension/selectItem` 仅包含调用点击操作的值。</span><span class="sxs-lookup"><span data-stu-id="a6fce-188">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="a6fce-189">若要确定关联的技能， `skillId`  请附加到每个项目卡片，同时形成 对 的响应 `OnTeamsMessagingExtensionQueryAsync` 。</span><span class="sxs-lookup"><span data-stu-id="a6fce-189">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="a6fce-190">这类似于将自适应 [卡片添加到虚拟助理的方法](#add-adaptive-cards-to-your-virtual-assistant)。</span><span class="sxs-lookup"><span data-stu-id="a6fce-190">This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example"></a><span data-ttu-id="a6fce-191">示例</span><span class="sxs-lookup"><span data-stu-id="a6fce-191">Example</span></span>

<span data-ttu-id="a6fce-192">以下示例演示如何将"预订会议室"应用模板转换为虚拟助理技能：会议室预订是一种 Microsoft Teams，允许用户从当前时间开始快速查找和预留会议室 30、60 或 90 分钟。</span><span class="sxs-lookup"><span data-stu-id="a6fce-192">The following example shows how to convert the Book-a-room app template to a Virtual Assistant skill: Book-a-room is a Microsoft Teams that allows users quickly to find and reserve a meeting room for 30, 60, or 90 minutes starting from the current time.</span></span> <span data-ttu-id="a6fce-193">默认时间为 30 分钟。</span><span class="sxs-lookup"><span data-stu-id="a6fce-193">The default time is 30 minutes.</span></span> <span data-ttu-id="a6fce-194">Book-a-room bot scopes to personal o\*\*r 1：1 conversations.</span><span class="sxs-lookup"><span data-stu-id="a6fce-194">The Book-a-room bot scopes to personal o\*\*r 1:1 conversations.</span></span> <span data-ttu-id="a6fce-195">下图显示具有书籍的虚拟助理 **的聊天室技能** ：</span><span class="sxs-lookup"><span data-stu-id="a6fce-195">The following image displays a Virtual Assistant with a **book a room** skill:</span></span>

![具有"预订会议室"技能的虚拟助理](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="a6fce-197">下面是引入的增量更改，以将其转换为附加到虚拟助理的技能。</span><span class="sxs-lookup"><span data-stu-id="a6fce-197">Followings are the delta changes introduced to convert it to a skill which is attached to a Virtual Assistant.</span></span> <span data-ttu-id="a6fce-198">为了将任何现有的 v4 自动程序转换为技能，遵循类似的准则。</span><span class="sxs-lookup"><span data-stu-id="a6fce-198">Similar guidelines are followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="a6fce-199">技能清单</span><span class="sxs-lookup"><span data-stu-id="a6fce-199">Skill manifest</span></span>

<span data-ttu-id="a6fce-200">技能清单是公开技能的消息终结点、ID、名称和其他相关元数据的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="a6fce-200">A skill manifest is a JSON file that exposes a skill's messaging endpoint, ID, name, and other relevant metadata.</span></span> <span data-ttu-id="a6fce-201">此清单不同于在 Microsoft Teams 中旁加载应用的清单。</span><span class="sxs-lookup"><span data-stu-id="a6fce-201">This manifest is different than the manifest used for sideloading an app in Microsoft Teams.</span></span> <span data-ttu-id="a6fce-202">虚拟助手需要此文件的路径作为输入来附加技能。</span><span class="sxs-lookup"><span data-stu-id="a6fce-202">A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="a6fce-203">我们已将以下清单添加到机器人的 wwwroot 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="a6fce-203">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="a6fce-204">实现"实现"的"实现"</span><span class="sxs-lookup"><span data-stu-id="a6fce-204">LUIS Integration</span></span>

<span data-ttu-id="a6fce-205">虚拟助理的调度模型基于附加技能的"函数""数字"模型构建。</span><span class="sxs-lookup"><span data-stu-id="a6fce-205">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="a6fce-206">调度模型可标识每个文本活动的意图，并找出与其关联的技能。</span><span class="sxs-lookup"><span data-stu-id="a6fce-206">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="a6fce-207">虚拟助手要求在附加技能时，将技能的函数的"分卡模型"格式作为 `.lu` 输入。</span><span class="sxs-lookup"><span data-stu-id="a6fce-207">Virtual Assistant requires skill's LUIS model in `.lu` format as an input while attaching a skill.</span></span> <span data-ttu-id="a6fce-208">使用 botframework-cli 工具将工作台 json `.lu` 转换为格式。</span><span class="sxs-lookup"><span data-stu-id="a6fce-208">LUIS json is converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="a6fce-209">预订聊天室自动程序为用户提供了两个主要命令：</span><span class="sxs-lookup"><span data-stu-id="a6fce-209">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="a6fce-210">我们通过了解这两个命令构建了一个"一个""一个"的"设计"模型。</span><span class="sxs-lookup"><span data-stu-id="a6fce-210">We have built a LUIS model by understanding these two commands.</span></span> <span data-ttu-id="a6fce-211">必须在 中填充相应的密码 `cognitivemodels.json` 。</span><span class="sxs-lookup"><span data-stu-id="a6fce-211">Corresponding secrets must be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="a6fce-212">此处找到相应的"为"的 ["JSON"文件](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json)。</span><span class="sxs-lookup"><span data-stu-id="a6fce-212">The corresponding LUIS JSON file is found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json).</span></span>
<span data-ttu-id="a6fce-213">以下 `.lu` 部分显示了相应的文件：</span><span class="sxs-lookup"><span data-stu-id="a6fce-213">The corresponding `.lu` file is shown in the following section:</span></span>

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

<span data-ttu-id="a6fce-214">通过此方法，用户向虚拟助理发出的任何与机器人相关的命令或被标识为与机器人关联的命令，并 `book room` `manage favorites` `Book-a-room` 转发到此技能。</span><span class="sxs-lookup"><span data-stu-id="a6fce-214">With this approach, any command issued by a user to Virtual Assistant related to `book room` or `manage favorites` are identified as a command associated with `Book-a-room` bot and is forwarded to this skill.</span></span>
<span data-ttu-id="a6fce-215">另一方面，如果命令未完整键入，则机器人需要使用 `Book-a-room room` "分卡模型"了解这些命令。</span><span class="sxs-lookup"><span data-stu-id="a6fce-215">On the other hand, `Book-a-room room` bot needs to use LUIS model to understand these commands if they are not typed full.</span></span> <span data-ttu-id="a6fce-216">例如：`I want to manage my favorite rooms`。</span><span class="sxs-lookup"><span data-stu-id="a6fce-216">For example: `I want to manage my favorite rooms`.</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="a6fce-217">多语言支持</span><span class="sxs-lookup"><span data-stu-id="a6fce-217">Multi-Language support</span></span>

<span data-ttu-id="a6fce-218">例如，将创建一个仅包含英语区域性的"分公司"模型。</span><span class="sxs-lookup"><span data-stu-id="a6fce-218">As an example, a LUIS model with only English culture is created.</span></span> <span data-ttu-id="a6fce-219">你可以创建与其他语言对应的分卡模型，并添加条目 `cognitivemodels.json` 。</span><span class="sxs-lookup"><span data-stu-id="a6fce-219">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="a6fce-220">并行，在 `.lu` "用户文件夹路径"中添加相应的文件。</span><span class="sxs-lookup"><span data-stu-id="a6fce-220">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="a6fce-221">文件夹结构应如下所示：</span><span class="sxs-lookup"><span data-stu-id="a6fce-221">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="a6fce-222">若要修改 `languages` 参数，请更新 botskills 命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a6fce-222">To modify `languages` parameter, update botskills command as follows:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="a6fce-223">虚拟助理 `SetLocaleMiddleware` 用于标识当前区域设置并调用相应的调度模型。</span><span class="sxs-lookup"><span data-stu-id="a6fce-223">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="a6fce-224">自动程序框架活动具有此中间件使用的本地设置字段。</span><span class="sxs-lookup"><span data-stu-id="a6fce-224">Bot framework activity has locale field which is used by this middleware.</span></span> <span data-ttu-id="a6fce-225">也可以对技能使用相同。</span><span class="sxs-lookup"><span data-stu-id="a6fce-225">You can use the same for your skill as well.</span></span> <span data-ttu-id="a6fce-226">预订聊天室机器人不会使用此中间件，而是从 Bot 框架活动的 [clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)实体获取区域设置。</span><span class="sxs-lookup"><span data-stu-id="a6fce-226">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="a6fce-227">声明验证</span><span class="sxs-lookup"><span data-stu-id="a6fce-227">Claim validation</span></span>

<span data-ttu-id="a6fce-228">我们添加了 [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) 来限制呼叫者使用技能。</span><span class="sxs-lookup"><span data-stu-id="a6fce-228">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="a6fce-229">若要允许虚拟助理调用此技能，请用该特定 `AllowedCallers` `appsettings` 虚拟助理的应用 ID 填充数组。</span><span class="sxs-lookup"><span data-stu-id="a6fce-229">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="a6fce-230">允许的调用方数组可以限制使用者可以访问该技能的技能。</span><span class="sxs-lookup"><span data-stu-id="a6fce-230">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="a6fce-231">向此数组 `*` 添加单个条目，以接受来自任何技能使用者的呼叫。</span><span class="sxs-lookup"><span data-stu-id="a6fce-231">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```

<span data-ttu-id="a6fce-232">有关向技能添加声明验证详细信息，请参阅 [向技能添加声明验证](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="a6fce-232">For more information on adding claims validation to a skill, see [add claims validation to skill](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator&preserve-view=true).</span></span>

### <a name="limitation-of-card-refresh"></a><span data-ttu-id="a6fce-233">卡片刷新的限制</span><span class="sxs-lookup"><span data-stu-id="a6fce-233">Limitation of card refresh</span></span> 

<span data-ttu-id="a6fce-234">目前尚不支持通过虚拟助理或 [github](https://github.com/microsoft/botbuilder-dotnet/issues/3686) 问题中心 (更新活动，例如) 。</span><span class="sxs-lookup"><span data-stu-id="a6fce-234">Updating activity, such as card refresh is not supported yet through Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="a6fce-235">因此，我们已将所有卡刷新呼叫 `UpdateActivityAsync` 替换为发布新卡呼叫 `SendActivityAsync` 。</span><span class="sxs-lookup"><span data-stu-id="a6fce-235">Hence, we have replaced all card refresh calls `UpdateActivityAsync` with posting new card calls `SendActivityAsync`.</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="a6fce-236">卡片操作和任务模块流</span><span class="sxs-lookup"><span data-stu-id="a6fce-236">Card actions and task module flows</span></span>

<span data-ttu-id="a6fce-237">若要将卡片操作或任务模块活动转发到关联的技能，该技能必须 `skillId` 嵌入到该技能中。</span><span class="sxs-lookup"><span data-stu-id="a6fce-237">To forward card action or task module activities to an associated skill, the skill must embed `skillId` to it.</span></span>
<span data-ttu-id="a6fce-238">`Book-a-room` bot card action， task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span><span class="sxs-lookup"><span data-stu-id="a6fce-238">`Book-a-room` bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="a6fce-239">有关详细信息，请参阅 [本文档](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) 中的此部分。</span><span class="sxs-lookup"><span data-stu-id="a6fce-239">For more information refer [this](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="a6fce-240">处理群聊或频道范围中的活动</span><span class="sxs-lookup"><span data-stu-id="a6fce-240">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="a6fce-241">`Book-a-room bot` 专为私人聊天设计，例如个人聊天或 1：1 范围。</span><span class="sxs-lookup"><span data-stu-id="a6fce-241">`Book-a-room bot` is designed for private chats, such as personal or 1:1 scope only.</span></span> <span data-ttu-id="a6fce-242">由于我们已自定义虚拟助理以支持群聊和频道范围，因此必须从频道范围调用虚拟助理，因此机器人必须获取相同 `Book-a-room` 范围的活动。</span><span class="sxs-lookup"><span data-stu-id="a6fce-242">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant must be invoked from the channel scopes and thus, `Book-a-room` bot must get activities for the same scope.</span></span> <span data-ttu-id="a6fce-243">因此 `Book-a-room` ，自动程序会进行自定义以处理这些活动。</span><span class="sxs-lookup"><span data-stu-id="a6fce-243">Hence `Book-a-room`bot is customized to handle those activities.</span></span> <span data-ttu-id="a6fce-244">你可以找到自动程序的活动处理程序 `OnMessageActivityAsync` `Book-a-room` 的签入方法。</span><span class="sxs-lookup"><span data-stu-id="a6fce-244">You can find the check in `OnMessageActivityAsync` methods of `Book-a-room` bot's activity handler.</span></span>

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

<span data-ttu-id="a6fce-245">还可以利用 Bot Framework [解决方案](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) 存储库中的现有技能，或从头开始创建新技能。</span><span class="sxs-lookup"><span data-stu-id="a6fce-245">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="a6fce-246">有关创建新技能，请参阅 [创建新技能的教程](https://microsoft.github.io/botframework-solutions/overview/skills/)。</span><span class="sxs-lookup"><span data-stu-id="a6fce-246">For creating a new skill, see [tutorials to create a new skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="a6fce-247">有关虚拟助手和技能体系结构文档，请参阅[虚拟助手和技能体系结构](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="a6fce-247">For Virtual Assistant and skills architecture documentation, see[Virtual Assistant and skills architecture](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true).</span></span>  

## <a name="limitations-of-virtual-assistant"></a><span data-ttu-id="a6fce-248">虚拟助理的限制</span><span class="sxs-lookup"><span data-stu-id="a6fce-248">Limitations of Virtual Assistant</span></span> 

* <span data-ttu-id="a6fce-249">**EndOfConversation：** 技能必须在完成对话 `endOfConversation` 时发送活动。</span><span class="sxs-lookup"><span data-stu-id="a6fce-249">**EndOfConversation**: A skill must send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="a6fce-250">根据活动，虚拟助理会结束具有该特定技能的上下文，并返回到虚拟助理的根上下文。</span><span class="sxs-lookup"><span data-stu-id="a6fce-250">Based on the activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's root context.</span></span> <span data-ttu-id="a6fce-251">对于"预订聊天室"自动程序，没有结束对话的清晰状态。</span><span class="sxs-lookup"><span data-stu-id="a6fce-251">For Book-a-room bot, there is no clear state where conversation is ended.</span></span> <span data-ttu-id="a6fce-252">因此，我们尚未从自动程序发送，并且当用户希望返回到根上下文时 `endOfConversation` `Book-a-room` ，他们只需通过命令 `start over` 执行。</span><span class="sxs-lookup"><span data-stu-id="a6fce-252">Hence we have not sent `endOfConversation` from `Book-a-room` bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>  
* <span data-ttu-id="a6fce-253">**卡刷新**：尚不支持通过虚拟助理刷新卡片。</span><span class="sxs-lookup"><span data-stu-id="a6fce-253">**Card refresh**: Card refresh is not yet supported through Virtual Assistant.</span></span>  
* <span data-ttu-id="a6fce-254">**邮件扩展：**</span><span class="sxs-lookup"><span data-stu-id="a6fce-254">**Messaging extensions**:</span></span>
  * <span data-ttu-id="a6fce-255">目前，虚拟助理最多可支持 10 个邮件扩展命令。</span><span class="sxs-lookup"><span data-stu-id="a6fce-255">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  * <span data-ttu-id="a6fce-256">邮件扩展的配置范围不是单个命令，而是整个扩展本身。</span><span class="sxs-lookup"><span data-stu-id="a6fce-256">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="a6fce-257">这将通过虚拟助理限制各个技能的配置。</span><span class="sxs-lookup"><span data-stu-id="a6fce-257">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  * <span data-ttu-id="a6fce-258">消息扩展命令 ID 的最大长度为 [64 个字符](../resources/schema/manifest-schema.md#composeextensions) ，37 个字符用于嵌入技能信息。</span><span class="sxs-lookup"><span data-stu-id="a6fce-258">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters are used for embedding skill information.</span></span> <span data-ttu-id="a6fce-259">因此，命令 ID 的更新约束限制为 27 个字符。</span><span class="sxs-lookup"><span data-stu-id="a6fce-259">Thus, updated constraints for command ID are limited to 27 characters.</span></span>

<span data-ttu-id="a6fce-260">还可以利用 Bot Framework [解决方案](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) 存储库中的现有技能，或从头开始创建新技能。</span><span class="sxs-lookup"><span data-stu-id="a6fce-260">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="a6fce-261">稍后的教程可在此处 [找到](https://microsoft.github.io/botframework-solutions/overview/skills/)。</span><span class="sxs-lookup"><span data-stu-id="a6fce-261">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="a6fce-262">请参阅虚拟 [助理和](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) 技能体系结构文档。</span><span class="sxs-lookup"><span data-stu-id="a6fce-262">Please refer to [documentation](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0&preserve-view=true) for Virtual Assistant and skills architecture.</span></span>

## <a name="code-sample"></a><span data-ttu-id="a6fce-263">代码示例</span><span class="sxs-lookup"><span data-stu-id="a6fce-263">Code sample</span></span>

| <span data-ttu-id="a6fce-264">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="a6fce-264">**Sample name**</span></span> | <span data-ttu-id="a6fce-265">**说明**</span><span class="sxs-lookup"><span data-stu-id="a6fce-265">**Description**</span></span> | <span data-ttu-id="a6fce-266">**C#**</span><span class="sxs-lookup"><span data-stu-id="a6fce-266">**C#**</span></span> | <span data-ttu-id="a6fce-267">**.NET**</span><span class="sxs-lookup"><span data-stu-id="a6fce-267">**.NET**</span></span> |
|----------|-----------------|----------|------------------|
| <span data-ttu-id="a6fce-268">更新的 Visual Studio 模板</span><span class="sxs-lookup"><span data-stu-id="a6fce-268">Updated visual studio template</span></span> | <span data-ttu-id="a6fce-269">用于支持团队功能的自定义模板。</span><span class="sxs-lookup"><span data-stu-id="a6fce-269">Customized template to support teams capabilities.</span></span> | [<span data-ttu-id="a6fce-270">View</span><span class="sxs-lookup"><span data-stu-id="a6fce-270">View</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill) |
| <span data-ttu-id="a6fce-271">预订聊天室机器人技能代码</span><span class="sxs-lookup"><span data-stu-id="a6fce-271">Book-a-room bot skill code</span></span> | <span data-ttu-id="a6fce-272">可让你快速查找并预订会议室。</span><span class="sxs-lookup"><span data-stu-id="a6fce-272">Lets you quickly find and book a meeting room on the go.</span></span> |  | [<span data-ttu-id="a6fce-273">View</span><span class="sxs-lookup"><span data-stu-id="a6fce-273">View</span></span>](https://github.com/nebhagat/msteams-virtual-assistant-dotnet) |


## <a name="see-also"></a><span data-ttu-id="a6fce-274">另请参阅</span><span class="sxs-lookup"><span data-stu-id="a6fce-274">See also</span></span>

- [<span data-ttu-id="a6fce-275">集成 web 应用</span><span class="sxs-lookup"><span data-stu-id="a6fce-275">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)

- [<span data-ttu-id="a6fce-276">预订聊天室</span><span class="sxs-lookup"><span data-stu-id="a6fce-276">Book-a-room</span></span>](app-templates.md#book-a-room)

- [<span data-ttu-id="a6fce-277">Microsoft Teams 机器人</span><span class="sxs-lookup"><span data-stu-id="a6fce-277">Microsoft Teams bot</span></span>](../bots/what-are-bots.md)