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
# <a name="virtual-assistant-for-microsoft-teams"></a><span data-ttu-id="7d85f-104">Microsoft 团队的虚拟助手</span><span class="sxs-lookup"><span data-stu-id="7d85f-104">Virtual Assistant for Microsoft Teams</span></span>

<span data-ttu-id="7d85f-105">Virtual Assistant 是一款 Microsoft 开放源代码模板，使您能够在保持用户体验、组织品牌和必要数据的完全控制的同时，创建强大的会话解决方案。</span><span class="sxs-lookup"><span data-stu-id="7d85f-105">Virtual Assistant is a Microsoft open-source template that enables you to create a robust conversational solution while maintaining full control of user experience, organizational branding, and necessary data.</span></span> <span data-ttu-id="7d85f-106">[Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template)是基本构建基块，它汇集了构建虚拟助手所需的 Microsoft 技术，包括[Bot 框架 SDK](https://github.com/microsoft/botframework-sdk)、[语言理解（LUIS）](https://www.luis.ai/)、 [QnA Maker](https://www.qnamaker.ai/)以及基本功能，包括技能登记、链接的帐户、基本对话目的，以向最终用户提供一系列无缝交互和体验。</span><span class="sxs-lookup"><span data-stu-id="7d85f-106">The [Virtual Assistant core template](https://microsoft.github.io/botframework-solutions/overview/virtual-assistant-template) is the basic building block that brings together the Microsoft technologies required to build a Virtual Assistant, including the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk), [Language Understanding (LUIS)](https://www.luis.ai/), [QnA Maker](https://www.qnamaker.ai/), as well as essential capabilities including  skills registration, linked accounts, basic conversational intent to offer end users a range of seamless interactions and experiences.</span></span> <span data-ttu-id="7d85f-107">此外，模板功能包含可重用的对话[技能](https://microsoft.github.io/botframework-solutions/overview/skills)的丰富示例。</span><span class="sxs-lookup"><span data-stu-id="7d85f-107">In addition, the template capabilities include rich examples of reusable conversational [skills](https://microsoft.github.io/botframework-solutions/overview/skills).</span></span>  <span data-ttu-id="7d85f-108">可以将单个技能集成到虚拟助手解决方案中，以启用多种方案。</span><span class="sxs-lookup"><span data-stu-id="7d85f-108">Individual skills can be integrated in a Virtual Assistant solution to enable multiple scenarios.</span></span> <span data-ttu-id="7d85f-109">使用 Bot 框架 SDK，可在源代码表单中提供技能，使您能够根据需要自定义和扩展。</span><span class="sxs-lookup"><span data-stu-id="7d85f-109">Using the Bot Framework SDK, Skills are presented in source code form enabling you to customize and extend as required.</span></span> <span data-ttu-id="7d85f-110">请参阅[什么是 Bot 框架技能](https://microsoft.github.io/botframework-solutions/overview/skills/)。</span><span class="sxs-lookup"><span data-stu-id="7d85f-110">See [What is a Bot Framework Skill](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span>

![虚拟助手概述图](../assets/images/bots/virtual-assistant/overview.png)

<span data-ttu-id="7d85f-112">使用[调度](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs)模型将短信活动路由到虚拟助理核心的相关技能。</span><span class="sxs-lookup"><span data-stu-id="7d85f-112">Text message activities are routed to associated skills by the Virtual Assistant core using a [dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0&tabs=cs) model.</span></span> 

## <a name="implementation-considerations"></a><span data-ttu-id="7d85f-113">实现注意事项</span><span class="sxs-lookup"><span data-stu-id="7d85f-113">Implementation considerations</span></span>

<span data-ttu-id="7d85f-114">添加虚拟助理的决策可以包含多个 determinants，并且每个组织的不同之处。</span><span class="sxs-lookup"><span data-stu-id="7d85f-114">The decision to add a Virtual Assistant can include many determinants and differ for each organization.</span></span> <span data-ttu-id="7d85f-115">以下是支持实现组织的虚拟助手的因素：</span><span class="sxs-lookup"><span data-stu-id="7d85f-115">Here are the factors that support implementing a Virtual Assistant for your organization:</span></span>

- <span data-ttu-id="7d85f-116">中心团队负责管理所有员工体验，并能够构建虚拟助理体验并管理对核心体验的更新，包括新技能的添加。</span><span class="sxs-lookup"><span data-stu-id="7d85f-116">A central team manages all employee experiences and has the capability to build a Virtual Assistant experience and manage updates to the core experience including the addition of new skills.</span></span>
- <span data-ttu-id="7d85f-117">业务功能和/或数字预计未来增长的多个应用程序存在。</span><span class="sxs-lookup"><span data-stu-id="7d85f-117">Multiple applications exist across business functions and/or the number is expected to grow in the future.</span></span>
- <span data-ttu-id="7d85f-118">现有应用程序由组织拥有，可将其转换为虚拟助手的技能。</span><span class="sxs-lookup"><span data-stu-id="7d85f-118">Existing applications are customizable, owned by the organization, and can be converted into skills for a Virtual Assistant.</span></span>
- <span data-ttu-id="7d85f-119">中央员工体验团队可以影响现有应用的自定义项，并提供在虚拟助理体验中集成现有应用程序作为技能的必要指南。</span><span class="sxs-lookup"><span data-stu-id="7d85f-119">The central employee-experiences team is able to influence customizations to existing apps and provide necessary guidance for integrating existing applications as skills in Virtual Assistant experience</span></span>

![中心团队维护助理，业务职能团队参与技能](../assets/images/bots/virtual-assistant/business-functions.png)

## <a name="create-a-teams-focused-virtual-assistant"></a><span data-ttu-id="7d85f-121">创建以团队为中心的虚拟助手</span><span class="sxs-lookup"><span data-stu-id="7d85f-121">Create a Teams-focused Virtual Assistant</span></span>

<span data-ttu-id="7d85f-122">Microsoft 已发布用于构建虚拟助理和技能的[Visual Studio 模板](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate)。</span><span class="sxs-lookup"><span data-stu-id="7d85f-122">Microsoft has published a [Visual Studio template](https://marketplace.visualstudio.com/items?itemName=BotBuilder.VirtualAssistantTemplate) for building Virtual Assistants and skills.</span></span> <span data-ttu-id="7d85f-123">使用 Visual Studio 模板，您可以创建一个虚拟的助手，并通过基于文本的体验支持，并通过操作支持有限的丰富卡片。</span><span class="sxs-lookup"><span data-stu-id="7d85f-123">With the Visual Studio template, you can create a Virtual Assistant, powered by a text-based experience with support for limited rich cards with actions.</span></span> <span data-ttu-id="7d85f-124">我们已增强 Visual Studio 基本模板，以包含 Microsoft 团队平台功能和强大的团队应用体验。</span><span class="sxs-lookup"><span data-stu-id="7d85f-124">We have enhanced the Visual Studio base template to include Microsoft Teams platform capabilities and power great Teams app experiences.</span></span> <span data-ttu-id="7d85f-125">一些功能包括支持丰富的自适应卡片、任务模块、团队/组聊天和邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="7d85f-125">A few of the capabilities include support for rich adaptive cards, task modules, teams/group chats and messaging extensions.</span></span> <span data-ttu-id="7d85f-126">另*请参阅*[教程：将您的虚拟助手扩展到 Microsoft 团队](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/)。</span><span class="sxs-lookup"><span data-stu-id="7d85f-126">*See also*, [Tutorial: Extend Your Virtual Assistant to Microsoft Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro/).</span></span>

![虚拟助理解决方案的高级别关系图](../assets/images/bots/virtual-assistant/high-level-diagram.png)

### <a name="add-adaptive-cards-to-your-virtual-assistant"></a><span data-ttu-id="7d85f-128">将自适应卡片添加到虚拟助手</span><span class="sxs-lookup"><span data-stu-id="7d85f-128">Add adaptive cards to your Virtual Assistant</span></span>

<span data-ttu-id="7d85f-129">若要正确调度请求，您的虚拟助手需要确定正确的 LUIS 模型及其关联的相应技能。</span><span class="sxs-lookup"><span data-stu-id="7d85f-129">To dispatch requests properly, your Virtual Assistant needs to identify the correct LUIS model and corresponding skill associated with it.</span></span> <span data-ttu-id="7d85f-130">但是，由于与某项技能关联的 LUIS 模型是固定的、预定义的关键字，而不是来自用户的 utterances，因此无法将调度机制用于智能卡操作活动。</span><span class="sxs-lookup"><span data-stu-id="7d85f-130">However, the dispatching mechanism cannot be used for card action activities since the LUIS model associated with a skill may not be trained for card action texts since these are fixed, pre-defined keywords, not utterances from a user.</span></span>

<span data-ttu-id="7d85f-131">我们已通过在智能卡操作负载中嵌入技能信息来解决此情况。</span><span class="sxs-lookup"><span data-stu-id="7d85f-131">We have resolved this by embedding skill information in the card action payload.</span></span> <span data-ttu-id="7d85f-132">每项技能都应嵌入 `skillId` `value` 卡片操作的字段。</span><span class="sxs-lookup"><span data-stu-id="7d85f-132">Every skill should embed `skillId` in the  `value` field of card actions.</span></span> <span data-ttu-id="7d85f-133">这是确保每个卡片操作活动携带相关技能信息和虚拟助理可利用此信息进行派遣的最佳方法。</span><span class="sxs-lookup"><span data-stu-id="7d85f-133">This is the best way to ensure that each card action activity carries the relevant skill information and Virtual Assistant can utilize this information for dispatching.</span></span>

<span data-ttu-id="7d85f-134">以下是卡片操作数据示例。</span><span class="sxs-lookup"><span data-stu-id="7d85f-134">Below is a card action data sample.</span></span> <span data-ttu-id="7d85f-135">通过 `skillId` 在构造函数中提供，我们确保技能信息始终显示在卡片操作中。</span><span class="sxs-lookup"><span data-stu-id="7d85f-135">By providing `skillId` in the constructor we ensure that skill information is always present in card actions.</span></span>

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

<span data-ttu-id="7d85f-136">接下来，我们 `SkillCardActionData` 将在虚拟助手模板中引入类，以 `skillId` 从智能卡操作负载中提取。</span><span class="sxs-lookup"><span data-stu-id="7d85f-136">Next, we introduce `SkillCardActionData` class in the Virtual Assistant template to extract `skillId` from the card action payload.</span></span>

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

<span data-ttu-id="7d85f-137">下面是要 `skillId` 从卡片操作数据中提取的代码段。</span><span class="sxs-lookup"><span data-stu-id="7d85f-137">Below is a code snippet to extract  `skillId` from card action data.</span></span> <span data-ttu-id="7d85f-138">我们将其作为[活动](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md)类中的扩展方法实现。</span><span class="sxs-lookup"><span data-stu-id="7d85f-138">We implemented it as an  extension method in the [Activity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md) class.</span></span>

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

### <a name="handle-interruptions-gracefully"></a><span data-ttu-id="7d85f-139">妥善处理中断</span><span class="sxs-lookup"><span data-stu-id="7d85f-139">Handle interruptions gracefully</span></span>

<span data-ttu-id="7d85f-140">当用户尝试在其他技能当前处于活动状态时调用技能时，虚拟助理可以处理中断。</span><span class="sxs-lookup"><span data-stu-id="7d85f-140">Virtual Assistant can handle interruptions in cases where a user tries to invoke a skill while another skill is currently active.</span></span> <span data-ttu-id="7d85f-141">我们引入了 `TeamsSkillDialog` 并 `TeamsSwitchSkillDialog` 基于 Bot 框架的[SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs)和[SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs)，以使用户能够从卡片操作切换技能经验。</span><span class="sxs-lookup"><span data-stu-id="7d85f-141">we have introduced `TeamsSkillDialog` and `TeamsSwitchSkillDialog`, based on Bot Framework's [SkillDialog](https://github.com/microsoft/botframework-solutions/blob/5b46d73e220bbb4fba86c48be532e495535ca78a/sdk/csharp/libraries/microsoft.bot.solutions/Skills/SkillDialog.cs) and [SwitchSkillDialog](https://github.com/microsoft/botframework-solutions/blob/6d40fa8ae05f96b0c5e0464e01361a9e1deb696c/sdk/csharp/libraries/microsoft.bot.solutions/Skills/Dialogs/SwitchSkillDialog.cs), to enable users to switch a skill experience from card actions.</span></span> <span data-ttu-id="7d85f-142">若要处理此请求，虚拟助手将提示用户提供确认消息以切换技能。</span><span class="sxs-lookup"><span data-stu-id="7d85f-142">To handle this request the Virtual Assistant prompts the user with a confirmation message to switch skills.</span></span>

![切换到新技能时的确认提示](../assets/images/bots/virtual-assistant/switch-skills-prompt.png)

### <a name="handling-task-module-requests"></a><span data-ttu-id="7d85f-144">处理任务模块请求</span><span class="sxs-lookup"><span data-stu-id="7d85f-144">Handling task module requests</span></span>

<span data-ttu-id="7d85f-145">若要将任务模块功能添加到虚拟助手中，虚拟助手活动处理程序中还包含另外两个方法： `OnTeamsTaskModuleFetchAsync` 和 `OnTeamsTaskModuleSubmitAsync` 。</span><span class="sxs-lookup"><span data-stu-id="7d85f-145">To add task module capabilities to a Virtual Assistant, two additional methods are included in the Virtual Assistant activity handler: `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync`.</span></span> <span data-ttu-id="7d85f-146">这些方法从虚拟助理中侦听与任务模块相关的活动，确定与请求相关的技能，并将该请求转发给确定的技能。</span><span class="sxs-lookup"><span data-stu-id="7d85f-146">These methods listen to task module-related activities from Virtual Assistant, identify the skill associated with the request, and forward the request to the identified skill.</span></span> 

<span data-ttu-id="7d85f-147">请求转发是通过[SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable)和方法进行的 `PostActivityAsync` 。</span><span class="sxs-lookup"><span data-stu-id="7d85f-147">Request forwarding is done via the  [SkillHttpClient](/dotnet/api/microsoft.bot.builder.integration.aspnet.core.skills.skillhttpclient?view=botbuilder-dotnet-stable), `PostActivityAsync` method.</span></span> <span data-ttu-id="7d85f-148">它返回 `InvokeResponse` 解析和转换为的响应 `TaskModuleResponse` 。</span><span class="sxs-lookup"><span data-stu-id="7d85f-148">It returns the response as `InvokeResponse` which is parsed and converted to `TaskModuleResponse` .</span></span>

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

<span data-ttu-id="7d85f-149">对于卡操作调度和任务模块响应，遵循类似的方法。</span><span class="sxs-lookup"><span data-stu-id="7d85f-149">A similar approach is followed for card action dispatching and task module responses.</span></span> <span data-ttu-id="7d85f-150">任务模块的提取和提交操作数据已更新，以包括 `skillId` 。</span><span class="sxs-lookup"><span data-stu-id="7d85f-150">Task module fetch and submit action data is updated to include `skillId`.</span></span> <span data-ttu-id="7d85f-151">活动扩展方法 `GetSkillId` `skillId` 从提供有关需要调用的技能的详细信息的有效负载中提取。</span><span class="sxs-lookup"><span data-stu-id="7d85f-151">Activity Extension method `GetSkillId` extracts `skillId` from the payload which provides details about the skill that needs to be invoked.</span></span>

<span data-ttu-id="7d85f-152">下面是和方法的代码 `OnTeamsTaskModuleFetchAsync` 段 `OnTeamsTaskModuleSubmitAsync` 。</span><span class="sxs-lookup"><span data-stu-id="7d85f-152">Below is a code snippet for `OnTeamsTaskModuleFetchAsync` and `OnTeamsTaskModuleSubmitAsync` methods.</span></span>

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

<span data-ttu-id="7d85f-153">此外，所有技能域必须包含在 `validDomains` Virtual Assistant 的清单文件部分中，以便可以正确地通过技能呈现调用任务模块。</span><span class="sxs-lookup"><span data-stu-id="7d85f-153">Additionally, all skill domains must be included in the `validDomains` section in Virtual Assistant's manifest file so that task modules invoked via a skill render properly.</span></span>

### <a name="handling-collaborative-app-scopes"></a><span data-ttu-id="7d85f-154">处理协作应用程序范围</span><span class="sxs-lookup"><span data-stu-id="7d85f-154">Handling collaborative app scopes</span></span>

<span data-ttu-id="7d85f-155">团队应用可以存在于多个范围中，包括1:1 聊天、组聊天和频道。</span><span class="sxs-lookup"><span data-stu-id="7d85f-155">Teams apps can exist in multiple scopes including 1:1 chat, group chat, and channels.</span></span> <span data-ttu-id="7d85f-156">核心虚拟助手模板专为1:1 聊天而设计。</span><span class="sxs-lookup"><span data-stu-id="7d85f-156">The core Virtual Assistant template is designed for 1:1 chats.</span></span> <span data-ttu-id="7d85f-157">作为启动体验的一部分，Virtual Assistant 会提示用户输入名称并维护用户状态。</span><span class="sxs-lookup"><span data-stu-id="7d85f-157">As part of the onboarding experience Virtual Assistant  prompts users for name and maintains user state.</span></span> <span data-ttu-id="7d85f-158">由于该载入体验不适用于组聊天/频道范围，因此它已被删除。</span><span class="sxs-lookup"><span data-stu-id="7d85f-158">Since that onboarding experience is not suited for group chat/channel scopes it has been removed.</span></span>

<span data-ttu-id="7d85f-159">技能应处理多个范围内的活动（1:1 聊天、组聊天和频道对话）。</span><span class="sxs-lookup"><span data-stu-id="7d85f-159">Skills should handle activities in multiple scopes (1:1 chat, group chat, and channel conversation).</span></span> <span data-ttu-id="7d85f-160">如果不支持这些范围中的任何作用域，则技能应使用适当的消息进行响应。</span><span class="sxs-lookup"><span data-stu-id="7d85f-160">If any of these scopes are not supported, skills should respond with an appropriate message.</span></span>

<span data-ttu-id="7d85f-161">已将以下处理函数添加到 Virtual Assistant core：</span><span class="sxs-lookup"><span data-stu-id="7d85f-161">The following  processing functions have been added to Virtual Assistant core:</span></span>

- <span data-ttu-id="7d85f-162">可以在没有来自组聊天或频道的任何文本消息的情况下调用虚拟助手。</span><span class="sxs-lookup"><span data-stu-id="7d85f-162">Virtual Assistant can be invoked without any text message from a group chat or channel.</span></span>
- <span data-ttu-id="7d85f-163">在将邮件发送到派遣模块之前，将清除 Articulations （即，删除 @mention 必要的 "bot"）。</span><span class="sxs-lookup"><span data-stu-id="7d85f-163">Articulations are cleaned (i.e.,  remove the necessary @mention of the bot) before sending the message to the dispatch module.</span></span>

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

### <a name="handling-messaging-extensions"></a><span data-ttu-id="7d85f-164">处理邮件扩展</span><span class="sxs-lookup"><span data-stu-id="7d85f-164">Handling messaging extensions</span></span>

<span data-ttu-id="7d85f-165">邮件扩展的命令是在应用程序清单文件中声明的。</span><span class="sxs-lookup"><span data-stu-id="7d85f-165">The commands for a messaging extension are declared in your app manifest file.</span></span> <span data-ttu-id="7d85f-166">邮件扩展用户界面由这些命令供电。</span><span class="sxs-lookup"><span data-stu-id="7d85f-166">The messaging extension user interface is powered by those commands.</span></span> <span data-ttu-id="7d85f-167">为使虚拟助理能够接通邮件扩展命令（作为附加技能），虚拟助理自己的清单必须包含这些命令。</span><span class="sxs-lookup"><span data-stu-id="7d85f-167">For a Virtual Assistant to power a messaging extension command (as an attached skill), a Virtual Assistant's own manifest must contain those commands.</span></span> <span data-ttu-id="7d85f-168">还应将来自单个技能的清单中的命令添加到虚拟助理的清单中。</span><span class="sxs-lookup"><span data-stu-id="7d85f-168">The commands from an individual skill's manifest should be added to the Virtual Assistant's manifest as well.</span></span> <span data-ttu-id="7d85f-169">命令 ID 通过使用分隔符（）追加技能的应用 ID 来提供相关技能的相关信息 `:` 。</span><span class="sxs-lookup"><span data-stu-id="7d85f-169">The command ID provides information about an associated skill by appending the skill's app ID via a separator (`:`).</span></span>

<span data-ttu-id="7d85f-170">下面是技能清单文件中的一个代码段。</span><span class="sxs-lookup"><span data-stu-id="7d85f-170">Below is a snippet from a skill's manifest file.</span></span>

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

<span data-ttu-id="7d85f-171">和，下面是对应的虚拟助手清单文件代码段。</span><span class="sxs-lookup"><span data-stu-id="7d85f-171">And, below is the corresponding Virtual Assistant manifest file code snippet.</span></span>

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

<span data-ttu-id="7d85f-172">一旦用户调用命令，虚拟助理就可以通过分析命令 ID 来标识相关技能，通过从命令 ID 删除额外后缀（）来更新活动， `:<skill_id>` 并将其转发到相应的技能。</span><span class="sxs-lookup"><span data-stu-id="7d85f-172">Once the commands are invoked by a user, the Virtual Assistant can identify an associated skill by parsing the command ID, update the activity by removing the extra suffix (`:<skill_id>`) from the command ID,  and forward it to the corresponding skill.</span></span> <span data-ttu-id="7d85f-173">技能代码不需要处理额外的后缀，因此避免了跨技能的命令 Id 之间的冲突。</span><span class="sxs-lookup"><span data-stu-id="7d85f-173">The code for a skill doesn't need to handle the extra suffix, thus, conflicts between command IDs across skills are avoided.</span></span> <span data-ttu-id="7d85f-174">通过此方法，所有上下文（"撰写"、"commandBox" 和 "message"）内的技能的所有搜索和操作命令都可以通过虚拟助手来供电。</span><span class="sxs-lookup"><span data-stu-id="7d85f-174">With this approach, all the search and action commands of a skill within all contexts ("compose", "commandBox" and "message") can be powered by a Virtual Assistant.</span></span>

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

<span data-ttu-id="7d85f-175">某些邮件扩展活动不包含命令 ID。</span><span class="sxs-lookup"><span data-stu-id="7d85f-175">Some messaging extension activities do not include the command ID.</span></span> <span data-ttu-id="7d85f-176">例如， `composeExtension/selectItem` 仅包含 invoke 路器操作的值。</span><span class="sxs-lookup"><span data-stu-id="7d85f-176">For example, `composeExtension/selectItem` contains only the value of the invoke tap action.</span></span> <span data-ttu-id="7d85f-177">若要标识关联的技能，请在为 `skillId` 提供响应时将其附加到每个项目卡片 `OnTeamsMessagingExtensionQueryAsync` 。</span><span class="sxs-lookup"><span data-stu-id="7d85f-177">To identify the associated skill, `skillId`  is attached to each item card while forming a response for `OnTeamsMessagingExtensionQueryAsync`.</span></span> <span data-ttu-id="7d85f-178">（这类似于[将自适应卡片添加到虚拟助手](#add-adaptive-cards-to-your-virtual-assistant)的方法。</span><span class="sxs-lookup"><span data-stu-id="7d85f-178">(This is similar to the approach for [adding adaptive  cards to your Virtual Assistant](#add-adaptive-cards-to-your-virtual-assistant).</span></span>

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

## <a name="example-convert-the-book-a-room-app-template-to-a-virtual-assistant-skill"></a><span data-ttu-id="7d85f-179">示例：将聊天室应用模板转换为虚拟助理技能</span><span class="sxs-lookup"><span data-stu-id="7d85f-179">Example: Convert the Book-a-room app template to a Virtual Assistant skill</span></span>

<span data-ttu-id="7d85f-180">[会议室](app-templates.md#book-a-room)是[Microsoft 团队 bot](../bots/what-are-bots.md) ，可让用户快速查找和保留从当前时间起30（默认）、60或90分钟的会议室。</span><span class="sxs-lookup"><span data-stu-id="7d85f-180">[Book-a-room](app-templates.md#book-a-room) is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="7d85f-181">书籍-会议室的 bot 作用域到个人或1:1 对话。</span><span class="sxs-lookup"><span data-stu-id="7d85f-181">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

![具有 "书籍成为聊天室" 技能的虚拟助手](../assets/images/bots/virtual-assistant/book-a-room-skill.png)

<span data-ttu-id="7d85f-183">下面是引入的增量更改，用于将其转换为可附加到虚拟助理的技能。</span><span class="sxs-lookup"><span data-stu-id="7d85f-183">Followings are the delta changes introduced to convert it to a skill which can be attached to a Virtual Assistant.</span></span> <span data-ttu-id="7d85f-184">可遵循类似的准则将任何现有的 v4 机器人转换为技能。</span><span class="sxs-lookup"><span data-stu-id="7d85f-184">Similar guidelines can be followed to convert any existing v4 bot to a skill.</span></span>

### <a name="skill-manifest"></a><span data-ttu-id="7d85f-185">技能清单</span><span class="sxs-lookup"><span data-stu-id="7d85f-185">Skill manifest</span></span>

<span data-ttu-id="7d85f-186">技能清单是一个 JSON 文件，该文件公开技能的消息终结点、id、名称和其他相关元数据（此清单与用于在 Microsoft 团队中添加应用程序的清单不同）虚拟助理需要一个指向此文件的路径作为附加技能的输入。</span><span class="sxs-lookup"><span data-stu-id="7d85f-186">A skill manifest is a JSON file that exposes a skill's messaging endpoint, id, name, and other relevant metadata (this manifest is different than the manifest used for sideloading an app in Microsoft Teams) A Virtual Assistant requires a path to this file as an input to attach a skill.</span></span> <span data-ttu-id="7d85f-187">我们已将以下清单添加到 bot 的 wwwroot 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="7d85f-187">We have added the following manifest to the bot's wwwroot folder.</span></span>

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

### <a name="luis-integration"></a><span data-ttu-id="7d85f-188">LUIS 集成</span><span class="sxs-lookup"><span data-stu-id="7d85f-188">LUIS Integration</span></span>

<span data-ttu-id="7d85f-189">虚拟助手的调度模型建立在附加技能的 LUIS 模型之上。</span><span class="sxs-lookup"><span data-stu-id="7d85f-189">Virtual Assistant's dispatch model is built on top of attached skills' LUIS models.</span></span> <span data-ttu-id="7d85f-190">调度模型标识每个文本活动的目的，并找出与之相关的技能。</span><span class="sxs-lookup"><span data-stu-id="7d85f-190">The dispatch model identifies the intent for every text activity and finds out skill associated with it.</span></span>

<span data-ttu-id="7d85f-191">在附加技能时，虚拟助手需要技能的 LUIS 模型（ `.lu` 格式）作为输入。</span><span class="sxs-lookup"><span data-stu-id="7d85f-191">Virtual Assistant requires skill's LUIS model (in `.lu` format) as an input while attaching a skill.</span></span> <span data-ttu-id="7d85f-192">可以使用 botframework 工具将 LUIS json 转换为 `.lu` 格式。</span><span class="sxs-lookup"><span data-stu-id="7d85f-192">LUIS json can be converted to `.lu` format using botframework-cli  tool.</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to the folder containing your Skill's .lu files>" --languages "en-us" --cs
```

```bash
npm i -g @microsoft/botframework-cli
bf luis:convert --in <pathToLUIS.json> --out <pathToLuFile>
```

<span data-ttu-id="7d85f-193">为用户提供了两个主要命令的图书-一个聊天室：</span><span class="sxs-lookup"><span data-stu-id="7d85f-193">Book-a-room bot has two main commands for users:</span></span>

- `Book room`
- `Manage Favorites`

<span data-ttu-id="7d85f-194">我们构建了一个 LUIS 模型，了解这两个命令。</span><span class="sxs-lookup"><span data-stu-id="7d85f-194">We have built a LUIS model understanding these two commands.</span></span> <span data-ttu-id="7d85f-195">需要填写相应的密码 `cognitivemodels.json` 。</span><span class="sxs-lookup"><span data-stu-id="7d85f-195">Corresponding secrets need to be populated in `cognitivemodels.json`.</span></span> <span data-ttu-id="7d85f-196">可在[此处](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json)找到相应的 LUIS JSON 文件，这就是相应 `.lu` 文件的外观。</span><span class="sxs-lookup"><span data-stu-id="7d85f-196">The corresponding LUIS JSON file can be found [here](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/blob/nebhagat/microsoft-teams-apps-bookaroom-skill/Deployment/Resources/LU/book-a-meeting.json) and this is how the corresponding `.lu` file looks like.</span></span>

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

<span data-ttu-id="7d85f-197">使用此方法时，用户与的相关虚拟助理的任何命令问题， `book room` 或者 `manage favorites` 可以将其标识为与会议室 bot 相关联的命令，并将其转发到此技能。</span><span class="sxs-lookup"><span data-stu-id="7d85f-197">With this approach, any command issues by a user to Virtual Assistant related to `book room` or `manage favorites` can be identified as a command associated with Book-a-room bot and is forwarded to this skill.</span></span>
<span data-ttu-id="7d85f-198">另一方面，如果不键入 as （例如：），则书籍中的会议室 bot 需要使用 LUIS 模型来了解这些命令 `I want to manage my favorite rooms` 。</span><span class="sxs-lookup"><span data-stu-id="7d85f-198">On the other hand, Book-a-room room bot needs to use LUIS model to understand these commands if they are not typed as is (for example: `I want to manage my favorite rooms`).</span></span>

### <a name="multi-language-support"></a><span data-ttu-id="7d85f-199">多语言支持</span><span class="sxs-lookup"><span data-stu-id="7d85f-199">Multi-Language support</span></span>

<span data-ttu-id="7d85f-200">对于此示例，我们仅创建了一个英语区域性的 LUIS 模型。</span><span class="sxs-lookup"><span data-stu-id="7d85f-200">For this example, we have only created a LUIS model with English culture.</span></span> <span data-ttu-id="7d85f-201">您可以创建与其他语言相对应的 LUIS 模型，并向添加条目 `cognitivemodels.json` 。</span><span class="sxs-lookup"><span data-stu-id="7d85f-201">You can create LUIS models corresponding to other languages and add entry to `cognitivemodels.json`.</span></span>

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

<span data-ttu-id="7d85f-202">在 "luisFolder" 路径中，将并行添加相应的 `.lu` 文件。</span><span class="sxs-lookup"><span data-stu-id="7d85f-202">In parallel, add corresponding `.lu` file in luisFolder path.</span></span> <span data-ttu-id="7d85f-203">文件夹结构应如下所示：</span><span class="sxs-lookup"><span data-stu-id="7d85f-203">Folder structure should be as follows:</span></span>

```bash
| - luisFolder

        | - en-us

                | - book-a-meeting.lu

        | - your_language_culture

                | - book-a-meeting.lu
```

<span data-ttu-id="7d85f-204">按如下所示更新 botskills 命令以修改 `languages` 参数：</span><span class="sxs-lookup"><span data-stu-id="7d85f-204">Update botskills command as follows to modify `languages` parameter:</span></span>

```json
botskills connect --remoteManifest "<url to skill's manifest>" --luisFolder "<path to luisFolder>" --languages "en-us, your_language_culture" --cs
```

<span data-ttu-id="7d85f-205">Virtual Assistant 用于 `SetLocaleMiddleware` 标识当前区域设置并调用相应的调度模型。</span><span class="sxs-lookup"><span data-stu-id="7d85f-205">Virtual Assistant uses `SetLocaleMiddleware` to identify current locale and invoke corresponding dispatch model.</span></span> <span data-ttu-id="7d85f-206">（Bot 框架活动具有此中间件使用的区域设置字段。）我们建议您也为自己的技能使用相同的。</span><span class="sxs-lookup"><span data-stu-id="7d85f-206">(Bot framework activity has locale field which is used by this middleware.) We recommend to use the same for your skill as well.</span></span> <span data-ttu-id="7d85f-207">聊天室的 bot 不使用此中间件，而是从 Bot 框架活动的[clientInfo 实体](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)中获取区域设置。</span><span class="sxs-lookup"><span data-stu-id="7d85f-207">Book-a-room bot does not use this middleware and instead gets locale from Bot framework activity's [clientInfo entity](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>

### <a name="claim-validation"></a><span data-ttu-id="7d85f-208">声明验证</span><span class="sxs-lookup"><span data-stu-id="7d85f-208">Claim validation</span></span>

<span data-ttu-id="7d85f-209">我们已添加[claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) ，以将呼叫者限制为技能。</span><span class="sxs-lookup"><span data-stu-id="7d85f-209">We have added [claimsValidator](https://github.com/nebhagat/msteams-virtual-assistant-dotnet/blob/master/msteams-virtual-assistant-dotnet/Authentication/AllowedCallersClaimsValidator.cs) to restrict callers to the skill.</span></span> <span data-ttu-id="7d85f-210">若要允许虚拟助理调用此技能，请 `AllowedCallers` `appsettings` 使用该特定虚拟助理的应用 ID 填充数组。</span><span class="sxs-lookup"><span data-stu-id="7d85f-210">To allow a Virtual Assistant to call this skill, populate `AllowedCallers` array from `appsettings` with that particular Virtual Assistant's app ID.</span></span>

```
"AllowedCallers": [ "<caller_VA1_appId>", "<caller_VA2_appId>" ],
```

<span data-ttu-id="7d85f-211">允许的呼叫者阵列可以限制哪些技能使用者可以访问技能。</span><span class="sxs-lookup"><span data-stu-id="7d85f-211">The allowed callers array can restrict which skill consumers can access the skill.</span></span> <span data-ttu-id="7d85f-212">将单个条目添加 `*` 到此阵列，以接受来自任何技能使用者的呼叫。</span><span class="sxs-lookup"><span data-stu-id="7d85f-212">Add single entry `*` to this array, to accept calls from any skill consumer.</span></span>

```
"AllowedCallers": [ "*" ],
```
<span data-ttu-id="7d85f-213">可在[此处](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator)找到有关向技能添加声明验证的详细文档。</span><span class="sxs-lookup"><span data-stu-id="7d85f-213">Detailed documentation for adding claims validation to a skill can be found [here](https://docs.microsoft.com/azure/bot-service/skill-implement-skill?view=azure-bot-service-4.0&tabs=cs#claims-validator).</span></span>

### <a name="card-refresh-limitation"></a><span data-ttu-id="7d85f-214">卡片刷新限制</span><span class="sxs-lookup"><span data-stu-id="7d85f-214">Card refresh limitation</span></span>

<span data-ttu-id="7d85f-215">尚不支持通过虚拟助理（[github 问题](https://github.com/microsoft/botbuilder-dotnet/issues/3686)）更新活动（卡片刷新）。</span><span class="sxs-lookup"><span data-stu-id="7d85f-215">Updating activity (card refresh) is not supported yet via Virtual Assistant ([github issue](https://github.com/microsoft/botbuilder-dotnet/issues/3686)).</span></span> <span data-ttu-id="7d85f-216">因此，我们已将所有的卡片刷新呼叫（）替换为 `UpdateActivityAsync` 发布新的电话卡呼叫（ `SendActivityAsync` ）。</span><span class="sxs-lookup"><span data-stu-id="7d85f-216">Hence, we have replaced all card refresh calls (`UpdateActivityAsync`) with posting new card calls(`SendActivityAsync`).</span></span>

### <a name="card-actions-and-task-module-flows"></a><span data-ttu-id="7d85f-217">卡片操作和任务模块流</span><span class="sxs-lookup"><span data-stu-id="7d85f-217">Card actions and task module flows</span></span>

<span data-ttu-id="7d85f-218">若要将卡片操作或任务模块活动转发到相关联的技能，技能需要嵌入 `skillId` 到其中。</span><span class="sxs-lookup"><span data-stu-id="7d85f-218">To forward card action or task module activities to an associated skill, the skill needs to embed `skillId` to it.</span></span>
<span data-ttu-id="7d85f-219">将任务模块的 "读取" 和 "提交操作" 负载修改为包含一个参数的会议室的 bot 卡片操作 `skillId` 。</span><span class="sxs-lookup"><span data-stu-id="7d85f-219">Book-a-room bot card action, task module fetch and submit action payloads are modified to contain `skillId` as a parameter.</span></span> 

<span data-ttu-id="7d85f-220">有关详细信息，请参阅本文档中的[这](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards)一节。</span><span class="sxs-lookup"><span data-stu-id="7d85f-220">For more information refer [this](https://msteams-captain.visualstudio.com/xGrowth%20App%20Templates/_wiki/wikis/xGrowth.wiki/88/Virtual-Assistant-for-MS-Teams?anchor=rich-cards) section from this documentation.</span></span>

### <a name="handle-activities-from-group-chat-or-channel-scope"></a><span data-ttu-id="7d85f-221">处理来自组聊天或频道范围的活动</span><span class="sxs-lookup"><span data-stu-id="7d85f-221">Handle activities from group chat or channel scope</span></span>

<span data-ttu-id="7d85f-222">仅为私人聊天（个人/1：1作用域）设计了聊天室的 bot。</span><span class="sxs-lookup"><span data-stu-id="7d85f-222">Book-a-room bot is designed for private chats (personal/1:1 scope) only.</span></span> <span data-ttu-id="7d85f-223">由于已将 Virtual Assistant 自定义为支持组聊天和频道作用域，因此可能会从这些范围调用虚拟助理，因此，会议室 bot 可能会获取相同的活动。</span><span class="sxs-lookup"><span data-stu-id="7d85f-223">Since we have customized Virtual Assistant to support group chat and channel scopes, the Virtual Assistant might be invoked from these scopes and thus, Book-a-room bot might get activities for the same.</span></span> <span data-ttu-id="7d85f-224">因此，可自定义书本的聊天室 bot 来处理这些活动。</span><span class="sxs-lookup"><span data-stu-id="7d85f-224">Hence Book-a-room bot is customized to handle those activities.</span></span> <span data-ttu-id="7d85f-225">检查已被置于会议室的 `OnMessageActivityAsync` 活动处理程序的方法中。</span><span class="sxs-lookup"><span data-stu-id="7d85f-225">The check has been put in `OnMessageActivityAsync` methods of Book-a-room bot's activity handler.</span></span>

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

<span data-ttu-id="7d85f-226">您还可以利用[Bot 框架解决方案库](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp)中现有的技能，或从头开始创建新的技能。</span><span class="sxs-lookup"><span data-stu-id="7d85f-226">You can also leverage existing skills from [Bot Framework Solutions repository](https://github.com/microsoft/botframework-solutions/tree/master/skills/csharp) or create a new skill altogether from scratch.</span></span> <span data-ttu-id="7d85f-227">可在[此处](https://microsoft.github.io/botframework-solutions/overview/skills/)找到后续教程。</span><span class="sxs-lookup"><span data-stu-id="7d85f-227">Tutorials for the later can be found [here](https://microsoft.github.io/botframework-solutions/overview/skills/).</span></span> <span data-ttu-id="7d85f-228">请参阅有关虚拟助理和技能体系结构的[文档](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)。</span><span class="sxs-lookup"><span data-stu-id="7d85f-228">Please refer to [documentation](https://docs.microsoft.com/azure/bot-service/skills-conceptual?view=azure-bot-service-4.0)   for Virtual Assistant and skills architecture.</span></span>

## <a name="sample-code-to-get-started"></a><span data-ttu-id="7d85f-229">入门示例代码</span><span class="sxs-lookup"><span data-stu-id="7d85f-229">Sample code to get started</span></span>

- [<span data-ttu-id="7d85f-230">更新的 visual studio 模板</span><span class="sxs-lookup"><span data-stu-id="7d85f-230">Updated visual studio template</span></span>](https://github.com/nebhagat/msteams-virtual-assistant-dotnet)
- [<span data-ttu-id="7d85f-231">图书-会议室的技能代码</span><span class="sxs-lookup"><span data-stu-id="7d85f-231">Book-a-room bot skill code</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom/tree/nebhagat/microsoft-teams-apps-bookaroom-skill)

## <a name="virtual-assistant-known-limitations"></a><span data-ttu-id="7d85f-232">虚拟助理已知限制</span><span class="sxs-lookup"><span data-stu-id="7d85f-232">Virtual Assistant known limitations</span></span>

- <span data-ttu-id="7d85f-233">**EndOfConversation**。</span><span class="sxs-lookup"><span data-stu-id="7d85f-233">**EndOfConversation**.</span></span> <span data-ttu-id="7d85f-234">技能在 `endOfConversation` 完成对话时应发送活动。</span><span class="sxs-lookup"><span data-stu-id="7d85f-234">A skill should send an `endOfConversation` activity when it finishes a conversation.</span></span> <span data-ttu-id="7d85f-235">根据此活动，虚拟助理将结束与该特定技能相关的上下文，并返回到虚拟助理（根）上下文。</span><span class="sxs-lookup"><span data-stu-id="7d85f-235">basis this activity, a Virtual Assistant ends context with that particular skill and gets back into Virtual Assistant's (root) context.</span></span> <span data-ttu-id="7d85f-236">对于会议室 bot，在可以结束对话的情况下，没有明确的状态。</span><span class="sxs-lookup"><span data-stu-id="7d85f-236">For Book-a-room bot, there is no clear state where conversation can be ended.</span></span> <span data-ttu-id="7d85f-237">因此，我们不是 `endOfConversation` 从聊天室 bot 发送的，当用户想要返回到根上下文时，只需通过命令执行此操作即可 `start over` 。</span><span class="sxs-lookup"><span data-stu-id="7d85f-237">Hence we have not sent `endOfConversation` from Book-a-room bot and when user wants to go back to root context they can simply do that by `start over` command.</span></span>
- <span data-ttu-id="7d85f-238">**卡片刷新**。</span><span class="sxs-lookup"><span data-stu-id="7d85f-238">**Card refresh**.</span></span> <span data-ttu-id="7d85f-239">尚不支持通过虚拟助理进行卡片刷新。</span><span class="sxs-lookup"><span data-stu-id="7d85f-239">Card refreshes is not yet supported through Virtual Assistant.</span></span>
- <span data-ttu-id="7d85f-240">**邮件扩展**。：</span><span class="sxs-lookup"><span data-stu-id="7d85f-240">**Messaging extensions**.:</span></span>
  - <span data-ttu-id="7d85f-241">目前，虚拟助理最多可以支持十个命令用于邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="7d85f-241">Currently, a Virtual Assistant can support a maximum of ten commands for messaging extensions.</span></span>
  - <span data-ttu-id="7d85f-242">邮件扩展的配置不限定为单个命令，而是整个扩展本身。</span><span class="sxs-lookup"><span data-stu-id="7d85f-242">Configuration of messaging extensions is not scoped to individual commands but for the entire extension itself.</span></span> <span data-ttu-id="7d85f-243">这将通过虚拟助手限制每个单个技能的配置。</span><span class="sxs-lookup"><span data-stu-id="7d85f-243">This limits configuration for each individual skill through Virtual Assistant.</span></span>
  - <span data-ttu-id="7d85f-244">邮件扩展命令 Id 的最大长度为[64 个字符](../resources/schema/manifest-schema.md#composeextensions)，37字符将用于嵌入技能信息。</span><span class="sxs-lookup"><span data-stu-id="7d85f-244">Messaging extensions command IDs have a maximum length of [64 characters](../resources/schema/manifest-schema.md#composeextensions) and 37 characters will be used for embedding skill information.</span></span> <span data-ttu-id="7d85f-245">因此，针对命令 ID 的更新限制限制为27个字符。</span><span class="sxs-lookup"><span data-stu-id="7d85f-245">Thus, updated constraints for command ID are limited to 27 characters.</span></span>
>
>
