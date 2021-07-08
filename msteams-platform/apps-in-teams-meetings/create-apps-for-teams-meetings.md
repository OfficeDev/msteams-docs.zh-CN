---
title: Teams 会议中应用的先决条件和 API 参考
author: surbhigupta
description: 使用用于会议Teams应用程序
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams 应用会议用户参与者角色 api
ms.openlocfilehash: bc13fa7b8c3af9a7c48463eab7198e908164ffbe
ms.sourcegitcommit: 0a775ae12419f3bc7484e557f4b4ae815bab64ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2021
ms.locfileid: "53333685"
---
# <a name="prerequisites-and-api-references-for-apps-in-teams-meetings"></a><span data-ttu-id="2e92b-104">Teams 会议中应用的先决条件和 API 参考</span><span class="sxs-lookup"><span data-stu-id="2e92b-104">Prerequisites and API references for apps in Teams meetings</span></span>

<span data-ttu-id="2e92b-105">若要在会议生命周期内扩展应用功能，Teams使用会议Teams应用程序。</span><span class="sxs-lookup"><span data-stu-id="2e92b-105">To expand the capabilities of your apps across the meeting lifecycle, Teams enables you to work with apps for Teams meetings.</span></span> <span data-ttu-id="2e92b-106">必须完成先决条件，并且可以使用会议应用 API 引用来增强会议体验。</span><span class="sxs-lookup"><span data-stu-id="2e92b-106">You must  go through the prerequisites and you can use the meeting apps API references to enhance the meeting experience.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e92b-107">先决条件</span><span class="sxs-lookup"><span data-stu-id="2e92b-107">Prerequisites</span></span>

<span data-ttu-id="2e92b-108">使用用于会议Teams，您必须了解以下内容：</span><span class="sxs-lookup"><span data-stu-id="2e92b-108">Before you work with apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="2e92b-109">你必须知道如何开发应用Teams知识。</span><span class="sxs-lookup"><span data-stu-id="2e92b-109">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="2e92b-110">有关详细信息，请参阅应用[Teams开发](../overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2e92b-110">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="2e92b-111">必须更新Teams清单，以指示该应用可用于会议。</span><span class="sxs-lookup"><span data-stu-id="2e92b-111">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="2e92b-112">有关详细信息，请参阅 [应用清单](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="2e92b-112">For more information, see [app manifest](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest).</span></span>

* <span data-ttu-id="2e92b-113">您的应用程序必须支持 groupchat 作用域中的可配置选项卡，你的应用必须在会议生命周期中作为选项卡运行。有关详细信息，请参阅 [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="2e92b-113">Your app must support configurable tabs in the groupchat scope, for your app to function in the meeting lifecycle as a tab. For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="2e92b-114">对于会议前和Teams方案，必须遵循常规选项卡设计准则。</span><span class="sxs-lookup"><span data-stu-id="2e92b-114">You must adhere to general Teams tab design guidelines for pre and post-meeting scenarios.</span></span> <span data-ttu-id="2e92b-115">有关会议期间的体验，请参阅会议内选项卡和会议内对话框设计指南。</span><span class="sxs-lookup"><span data-stu-id="2e92b-115">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="2e92b-116">有关详细信息，请参阅Teams[选项卡设计指南](../tabs/design/tabs.md)、会议中的[选项卡](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)设计指南和[会议中的对话框设计指南](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。</span><span class="sxs-lookup"><span data-stu-id="2e92b-116">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab), and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="2e92b-117">必须支持范围才能在会议前和会议后聊天 `groupchat` 中启用应用。</span><span class="sxs-lookup"><span data-stu-id="2e92b-117">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="2e92b-118">通过会议前应用体验，你可以查找和添加会议应用并执行会议前任务。</span><span class="sxs-lookup"><span data-stu-id="2e92b-118">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="2e92b-119">通过会议后应用体验，可以查看会议结果，如投票调查结果或反馈。</span><span class="sxs-lookup"><span data-stu-id="2e92b-119">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="2e92b-120">会议 API URL 参数必须具有 `meetingId` 、 `userId` 和 `tenantId` 。</span><span class="sxs-lookup"><span data-stu-id="2e92b-120">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="2e92b-121">它们作为客户端 SDK 和自动程序Teams的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="2e92b-121">These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="2e92b-122">此外，您可以使用选项卡 SSO 身份验证检索用户 ID 和租户 ID [的可靠信息](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="2e92b-122">In addition, you can retrieve reliable information for user ID and tenant ID using [tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="2e92b-123">`GetParticipant`API 必须具有自动程序注册和 ID，以生成身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="2e92b-123">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="2e92b-124">有关详细信息，请参阅自动[程序注册和 ID。](../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="2e92b-124">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="2e92b-125">若要实时更新应用，应用必须基于会议中的活动活动是最新的。</span><span class="sxs-lookup"><span data-stu-id="2e92b-125">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="2e92b-126">这些事件可以位于会议中的对话框内以及整个会议生命周期的其他阶段。</span><span class="sxs-lookup"><span data-stu-id="2e92b-126">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="2e92b-127">有关会议中的对话框，请参阅 `bot Id` API 中的完成 `NotificationSignal` 参数。</span><span class="sxs-lookup"><span data-stu-id="2e92b-127">For the in-meeting dialog box, see completion `bot Id` parameter in `NotificationSignal` API.</span></span>

* <span data-ttu-id="2e92b-128">会议详细信息 API 必须具有自动程序注册和自动程序 ID。</span><span class="sxs-lookup"><span data-stu-id="2e92b-128">Meeting Details API must have a bot registration and bot ID.</span></span> <span data-ttu-id="2e92b-129">它需要 Bot SDK 才能获取 `TurnContext` 。</span><span class="sxs-lookup"><span data-stu-id="2e92b-129">It requires Bot SDK to get `TurnContext`.</span></span>

* <span data-ttu-id="2e92b-130">对于实时会议事件，你必须熟悉通过 `TurnContext` Bot SDK 提供的对象。</span><span class="sxs-lookup"><span data-stu-id="2e92b-130">For real-time meeting events, you must be familiar with the `TurnContext` object available through the Bot SDK.</span></span> <span data-ttu-id="2e92b-131">`Activity`中的 对象 `TurnContext` 包含具有实际开始时间和结束时间的有效负载。</span><span class="sxs-lookup"><span data-stu-id="2e92b-131">The `Activity` object in `TurnContext` contains the payload with the actual start and end time.</span></span> <span data-ttu-id="2e92b-132">实时会议事件需要来自会议平台的已注册Teams ID。</span><span class="sxs-lookup"><span data-stu-id="2e92b-132">Real-time meeting events require a registered bot ID from the Teams platform.</span></span>

<span data-ttu-id="2e92b-133">完成先决条件后，可以使用会议应用 API 引用、 和会议详细信息 API，以便使用属性访问信息并显示 `GetUserContext` `GetParticipant` `NotificationSignal` 相关内容。</span><span class="sxs-lookup"><span data-stu-id="2e92b-133">After you have gone through the prerequisites, you can use the meeting apps API references `GetUserContext`, `GetParticipant`, `NotificationSignal`, and Meeting Details API that enable you to access information using attributes and display relevant content.</span></span>

## <a name="meeting-apps-api-references"></a><span data-ttu-id="2e92b-134">会议应用 API 参考</span><span class="sxs-lookup"><span data-stu-id="2e92b-134">Meeting apps API references</span></span>

<span data-ttu-id="2e92b-135">新的会议可扩展性为您提供了可转换会议体验的 API。</span><span class="sxs-lookup"><span data-stu-id="2e92b-135">The new meeting extensibilities provide you with APIs that transform the meeting experience.</span></span> <span data-ttu-id="2e92b-136">借助此新功能，可以在会议生命周期内生成应用或集成现有应用。</span><span class="sxs-lookup"><span data-stu-id="2e92b-136">With this new capability, you can build apps or integrate existing apps within the meeting lifecycle.</span></span> <span data-ttu-id="2e92b-137">可以使用 API 让应用了解会议。</span><span class="sxs-lookup"><span data-stu-id="2e92b-137">You can use the APIs to make your app aware of the meeting.</span></span> <span data-ttu-id="2e92b-138">你可以选择想要用于增强会议体验的 API。</span><span class="sxs-lookup"><span data-stu-id="2e92b-138">You can choose which APIs you want to use to enhance the meeting experience.</span></span>

<span data-ttu-id="2e92b-139">下表提供了这些 API 的列表：</span><span class="sxs-lookup"><span data-stu-id="2e92b-139">The following table provides a list of these APIs:</span></span>

|<span data-ttu-id="2e92b-140">API</span><span class="sxs-lookup"><span data-stu-id="2e92b-140">API</span></span>|<span data-ttu-id="2e92b-141">说明</span><span class="sxs-lookup"><span data-stu-id="2e92b-141">Description</span></span>|<span data-ttu-id="2e92b-142">请求</span><span class="sxs-lookup"><span data-stu-id="2e92b-142">Request</span></span>|<span data-ttu-id="2e92b-143">Source</span><span class="sxs-lookup"><span data-stu-id="2e92b-143">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="2e92b-144">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="2e92b-144">**GetUserContext**</span></span>| <span data-ttu-id="2e92b-145">此 API 使你能够获取上下文信息，以在"开始"选项卡中Teams内容。</span><span class="sxs-lookup"><span data-stu-id="2e92b-145">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="2e92b-146">_**microsoftTeams.getContext ( ( ) => { /*...*/ } )**_</span><span class="sxs-lookup"><span data-stu-id="2e92b-146">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="2e92b-147">Microsoft Teams客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="2e92b-147">Microsoft Teams Client SDK</span></span>|
|<span data-ttu-id="2e92b-148">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="2e92b-148">**GetParticipant**</span></span>| <span data-ttu-id="2e92b-149">此 API 允许机器人通过会议 ID 和参与者 ID 获取参与者信息。</span><span class="sxs-lookup"><span data-stu-id="2e92b-149">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="2e92b-150">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}？tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="2e92b-150">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="2e92b-151">Microsoft Bot FrameworkSDK</span><span class="sxs-lookup"><span data-stu-id="2e92b-151">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="2e92b-152">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="2e92b-152">**NotificationSignal**</span></span> | <span data-ttu-id="2e92b-153">此 API 使你能够提供使用用户-机器人聊天的现有对话通知 API 传递的会议信号。</span><span class="sxs-lookup"><span data-stu-id="2e92b-153">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="2e92b-154">它允许您根据显示会议内对话框的用户操作发出信号。</span><span class="sxs-lookup"><span data-stu-id="2e92b-154">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="2e92b-155">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="2e92b-155">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="2e92b-156">Microsoft Bot FrameworkSDK</span><span class="sxs-lookup"><span data-stu-id="2e92b-156">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="2e92b-157">**会议详细信息**</span><span class="sxs-lookup"><span data-stu-id="2e92b-157">**Meeting Details**</span></span> | <span data-ttu-id="2e92b-158">此 API 使你能够获取静态会议元数据。</span><span class="sxs-lookup"><span data-stu-id="2e92b-158">This API enables you to get static meeting metadata.</span></span> |<span data-ttu-id="2e92b-159">**GET** _**/v1/meetings/{meetingId}**_</span><span class="sxs-lookup"><span data-stu-id="2e92b-159">**GET** _**/v1/meetings/{meetingId}**_</span></span>| <span data-ttu-id="2e92b-160">Bot SDK</span><span class="sxs-lookup"><span data-stu-id="2e92b-160">Bot SDK</span></span> |

### <a name="getusercontext-api"></a><span data-ttu-id="2e92b-161">GetUserContext API</span><span class="sxs-lookup"><span data-stu-id="2e92b-161">GetUserContext API</span></span>

<span data-ttu-id="2e92b-162">若要标识和检索选项卡内容的上下文信息，请参阅获取选项卡Teams[上下文](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library)。`meetingId`在会议上下文中运行时选项卡使用，并添加响应有效负载。</span><span class="sxs-lookup"><span data-stu-id="2e92b-162">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="2e92b-163">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="2e92b-163">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="2e92b-164">不要缓存参与者角色，因为会议组织者可以随时更改角色。</span><span class="sxs-lookup"><span data-stu-id="2e92b-164">Do not cache participant roles since the meeting organizer can change the roles any time.</span></span>
> * <span data-ttu-id="2e92b-165">Teams API 当前不支持超过 350 个参与者的大型通讯组列表或名单 `GetParticipant` 大小。</span><span class="sxs-lookup"><span data-stu-id="2e92b-165">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

<span data-ttu-id="2e92b-166">API `GetParticipant` 允许机器人通过会议 ID 和参与者 ID 获取参与者信息。</span><span class="sxs-lookup"><span data-stu-id="2e92b-166">The `GetParticipant` API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> <span data-ttu-id="2e92b-167">API 包括查询参数、示例和响应代码。</span><span class="sxs-lookup"><span data-stu-id="2e92b-167">The API includes query parameters, examples, and response codes.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="2e92b-168">查询参数</span><span class="sxs-lookup"><span data-stu-id="2e92b-168">Query parameters</span></span>

<span data-ttu-id="2e92b-169">`GetParticipant`API 包括以下查询参数：</span><span class="sxs-lookup"><span data-stu-id="2e92b-169">The `GetParticipant` API includes the following query parameters:</span></span>

|<span data-ttu-id="2e92b-170">值</span><span class="sxs-lookup"><span data-stu-id="2e92b-170">Value</span></span>|<span data-ttu-id="2e92b-171">类型</span><span class="sxs-lookup"><span data-stu-id="2e92b-171">Type</span></span>|<span data-ttu-id="2e92b-172">必需</span><span class="sxs-lookup"><span data-stu-id="2e92b-172">Required</span></span>|<span data-ttu-id="2e92b-173">说明</span><span class="sxs-lookup"><span data-stu-id="2e92b-173">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="2e92b-174">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="2e92b-174">**meetingId**</span></span>| <span data-ttu-id="2e92b-175">字符串</span><span class="sxs-lookup"><span data-stu-id="2e92b-175">String</span></span> | <span data-ttu-id="2e92b-176">是</span><span class="sxs-lookup"><span data-stu-id="2e92b-176">Yes</span></span> | <span data-ttu-id="2e92b-177">会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。</span><span class="sxs-lookup"><span data-stu-id="2e92b-177">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="2e92b-178">**participantId**</span><span class="sxs-lookup"><span data-stu-id="2e92b-178">**participantId**</span></span>| <span data-ttu-id="2e92b-179">字符串</span><span class="sxs-lookup"><span data-stu-id="2e92b-179">String</span></span> | <span data-ttu-id="2e92b-180">是</span><span class="sxs-lookup"><span data-stu-id="2e92b-180">Yes</span></span> | <span data-ttu-id="2e92b-181">参与者 ID 是用户 ID。</span><span class="sxs-lookup"><span data-stu-id="2e92b-181">The participant ID is the user ID.</span></span> <span data-ttu-id="2e92b-182">它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。</span><span class="sxs-lookup"><span data-stu-id="2e92b-182">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="2e92b-183">建议从选项卡 SSO 获取参与者 ID。</span><span class="sxs-lookup"><span data-stu-id="2e92b-183">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="2e92b-184">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="2e92b-184">**tenantId**</span></span>| <span data-ttu-id="2e92b-185">字符串</span><span class="sxs-lookup"><span data-stu-id="2e92b-185">String</span></span> | <span data-ttu-id="2e92b-186">是</span><span class="sxs-lookup"><span data-stu-id="2e92b-186">Yes</span></span> | <span data-ttu-id="2e92b-187">租户用户需要租户 ID。</span><span class="sxs-lookup"><span data-stu-id="2e92b-187">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="2e92b-188">它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。</span><span class="sxs-lookup"><span data-stu-id="2e92b-188">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="2e92b-189">建议从选项卡 SSO 获取租户 ID。</span><span class="sxs-lookup"><span data-stu-id="2e92b-189">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="2e92b-190">示例</span><span class="sxs-lookup"><span data-stu-id="2e92b-190">Example</span></span>

<span data-ttu-id="2e92b-191">`GetParticipant`API 包括以下示例：</span><span class="sxs-lookup"><span data-stu-id="2e92b-191">The `GetParticipant` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="2e92b-192">C#</span><span class="sxs-lookup"><span data-stu-id="2e92b-192">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  TeamsMeetingParticipant participant = await TeamsInfo.GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourParticipantTenantId").ConfigureAwait(false);
  TeamsChannelAccount member = participant.User;
  MeetingParticipantInfo meetingInfo = participant.Meeting;
  ConversationAccount conversation = participant.Conversation;

  await turnContext.SendActivityAsync(MessageFactory.Text($"The participant role is: {meetingInfo.Role}"), cancellationToken);
}

```

# <a name="javascript"></a>[<span data-ttu-id="2e92b-193">JavaScript</span><span class="sxs-lookup"><span data-stu-id="2e92b-193">JavaScript</span></span>](#tab/javascript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            TeamsMeetingParticipant participant = getMeetingParticipant(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
            let member = participant.user;
            let meetingInfo = participant.meeting;
            let conversation = participant.conversation;
            
            await context.sendActivity(`The participant role is: '${meetingInfo.role}'`);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="2e92b-194">JSON</span><span class="sxs-lookup"><span data-stu-id="2e92b-194">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

---

<span data-ttu-id="2e92b-195">API 的 JSON 响应 `GetParticipant` 正文为：</span><span class="sxs-lookup"><span data-stu-id="2e92b-195">The JSON response body for `GetParticipant` API is:</span></span>

```json
{
   "user":{
      "id":"29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId":"e236c4bf-88b1-4f3a-b1d7-8891dfc332b5",
      "name":"Bob Young",
      "givenName":"Bob",
      "surname":"Young",
      "email":"Bob.young@microsoft.com",
      "userPrincipalName":"Bob.young@microsoft.com",
      "tenantId":"2fe477ab-0efc-4dfd-bde2-484374e2c373",
      "userRole":"user"
   },
   "meeting":{
      "role ":"Presenter",
      "inMeeting":true
   },
   "conversation":{
      "id":"<conversation id>",
      "isGroup":true
   }
}
```

#### <a name="response-codes"></a><span data-ttu-id="2e92b-196">响应代码</span><span class="sxs-lookup"><span data-stu-id="2e92b-196">Response codes</span></span>

<span data-ttu-id="2e92b-197">`GetParticipant`API 返回以下响应代码：</span><span class="sxs-lookup"><span data-stu-id="2e92b-197">The `GetParticipant` API returns the following response codes:</span></span>

|<span data-ttu-id="2e92b-198">响应代码</span><span class="sxs-lookup"><span data-stu-id="2e92b-198">Response code</span></span>|<span data-ttu-id="2e92b-199">说明</span><span class="sxs-lookup"><span data-stu-id="2e92b-199">Description</span></span>|
|---|---|
| <span data-ttu-id="2e92b-200">**403**</span><span class="sxs-lookup"><span data-stu-id="2e92b-200">**403**</span></span> | <span data-ttu-id="2e92b-201">不允许应用获取参与者信息。</span><span class="sxs-lookup"><span data-stu-id="2e92b-201">The app is not allowed to get participant information.</span></span> <span data-ttu-id="2e92b-202">这是最常见的错误响应，如果会议未安装应用，将触发此错误响应。</span><span class="sxs-lookup"><span data-stu-id="2e92b-202">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="2e92b-203">例如，如果租户管理员禁用应用或在实时网站迁移期间阻止应用。</span><span class="sxs-lookup"><span data-stu-id="2e92b-203">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="2e92b-204">**200**</span><span class="sxs-lookup"><span data-stu-id="2e92b-204">**200**</span></span> | <span data-ttu-id="2e92b-205">成功检索参与者信息。</span><span class="sxs-lookup"><span data-stu-id="2e92b-205">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="2e92b-206">**401**</span><span class="sxs-lookup"><span data-stu-id="2e92b-206">**401**</span></span> | <span data-ttu-id="2e92b-207">应用使用无效令牌进行响应。</span><span class="sxs-lookup"><span data-stu-id="2e92b-207">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="2e92b-208">**404**</span><span class="sxs-lookup"><span data-stu-id="2e92b-208">**404**</span></span> | <span data-ttu-id="2e92b-209">会议已过期或找不到参与者。</span><span class="sxs-lookup"><span data-stu-id="2e92b-209">The meeting has either expired or participant cannot be found.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="2e92b-210">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="2e92b-210">NotificationSignal API</span></span>

<span data-ttu-id="2e92b-211">会议中的所有用户都接收通过 API 发送 `NotificationSignal` 的通知。</span><span class="sxs-lookup"><span data-stu-id="2e92b-211">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="2e92b-212">调用会议内对话框时，内容将显示为聊天消息。</span><span class="sxs-lookup"><span data-stu-id="2e92b-212">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="2e92b-213">目前，不支持发送定向通知。</span><span class="sxs-lookup"><span data-stu-id="2e92b-213">Currently, sending targeted notifications is not supported.</span></span>

<span data-ttu-id="2e92b-214">`NotificationSignal` API 使你能够提供使用用户-机器人聊天的现有对话通知 API 传递的会议信号。</span><span class="sxs-lookup"><span data-stu-id="2e92b-214">`NotificationSignal` API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="2e92b-215">此 API 允许你根据显示会议内对话框的用户操作发出信号。</span><span class="sxs-lookup"><span data-stu-id="2e92b-215">This API allows you to signal based on user action that shows an in-meeting dialog box.</span></span> <span data-ttu-id="2e92b-216">API 包括查询参数、示例和响应代码。</span><span class="sxs-lookup"><span data-stu-id="2e92b-216">The API includes query parameter, examples, and response codes.</span></span>

#### <a name="query-parameter"></a><span data-ttu-id="2e92b-217">查询参数</span><span class="sxs-lookup"><span data-stu-id="2e92b-217">Query parameter</span></span>

<span data-ttu-id="2e92b-218">`NotificationSignal`API 包括以下查询参数：</span><span class="sxs-lookup"><span data-stu-id="2e92b-218">The `NotificationSignal` API includes the following query parameter:</span></span>

|<span data-ttu-id="2e92b-219">值</span><span class="sxs-lookup"><span data-stu-id="2e92b-219">Value</span></span>|<span data-ttu-id="2e92b-220">类型</span><span class="sxs-lookup"><span data-stu-id="2e92b-220">Type</span></span>|<span data-ttu-id="2e92b-221">必需</span><span class="sxs-lookup"><span data-stu-id="2e92b-221">Required</span></span>|<span data-ttu-id="2e92b-222">说明</span><span class="sxs-lookup"><span data-stu-id="2e92b-222">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="2e92b-223">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="2e92b-223">**conversationId**</span></span>| <span data-ttu-id="2e92b-224">字符串</span><span class="sxs-lookup"><span data-stu-id="2e92b-224">String</span></span> | <span data-ttu-id="2e92b-225">是</span><span class="sxs-lookup"><span data-stu-id="2e92b-225">Yes</span></span> | <span data-ttu-id="2e92b-226">对话标识符作为 Bot Invoke 的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="2e92b-226">The conversation identifier is available as part of Bot Invoke.</span></span> |

#### <a name="examples"></a><span data-ttu-id="2e92b-227">示例</span><span class="sxs-lookup"><span data-stu-id="2e92b-227">Examples</span></span>

<span data-ttu-id="2e92b-228">`Bot ID`在清单中声明 ，机器人将接收结果对象。</span><span class="sxs-lookup"><span data-stu-id="2e92b-228">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="2e92b-229">`completionBotId`在请求 `externalResourceUrl` 的有效负载示例中，的 参数是可选的。</span><span class="sxs-lookup"><span data-stu-id="2e92b-229">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="2e92b-230">`Bot ID` 在清单中声明，机器人将接收结果对象。</span><span class="sxs-lookup"><span data-stu-id="2e92b-230">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="2e92b-231">`externalResourceUrl`宽度和高度参数必须以像素为单位。</span><span class="sxs-lookup"><span data-stu-id="2e92b-231">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="2e92b-232">若要确保尺寸在允许的限制内，请参阅 [设计指南](design/designing-apps-in-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="2e92b-232">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="2e92b-233">URL 是在会议对话框中作为 `<iframe>` 加载的页面。</span><span class="sxs-lookup"><span data-stu-id="2e92b-233">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="2e92b-234">域必须在你的应用清单 `validDomains` 的应用数组中。</span><span class="sxs-lookup"><span data-stu-id="2e92b-234">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

<span data-ttu-id="2e92b-235">`NotificationSignal`API 包括以下示例：</span><span class="sxs-lookup"><span data-stu-id="2e92b-235">The `NotificationSignal` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="2e92b-236">C#</span><span class="sxs-lookup"><span data-stu-id="2e92b-236">C#</span></span>](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
activity.TeamsNotifyUser(true, "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID");
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[<span data-ttu-id="2e92b-237">JavaScript</span><span class="sxs-lookup"><span data-stu-id="2e92b-237">JavaScript</span></span>](#tab/javascript)

```javascript

const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
replyActivity.channelData = {
    notification: {
        alertInMeeting: true,
        externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID’
    }
};
await context.sendActivity(replyActivity);
```

# <a name="json"></a>[<span data-ttu-id="2e92b-238">JSON</span><span class="sxs-lookup"><span data-stu-id="2e92b-238">JSON</span></span>](#tab/json)

```http
POST /v3/conversations/{conversationId}/activities

{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
        }
    },
    "replyToId": "1493070356924"
}
```

---

#### <a name="response-codes"></a><span data-ttu-id="2e92b-239">响应代码</span><span class="sxs-lookup"><span data-stu-id="2e92b-239">Response codes</span></span>

<span data-ttu-id="2e92b-240">`NotificationSignal`API 包括以下响应代码：</span><span class="sxs-lookup"><span data-stu-id="2e92b-240">The `NotificationSignal` API includes the following response codes:</span></span>

|<span data-ttu-id="2e92b-241">响应代码</span><span class="sxs-lookup"><span data-stu-id="2e92b-241">Response code</span></span>|<span data-ttu-id="2e92b-242">说明</span><span class="sxs-lookup"><span data-stu-id="2e92b-242">Description</span></span>|
|---|---|
| <span data-ttu-id="2e92b-243">**201**</span><span class="sxs-lookup"><span data-stu-id="2e92b-243">**201**</span></span> | <span data-ttu-id="2e92b-244">具有信号的活动已成功发送。</span><span class="sxs-lookup"><span data-stu-id="2e92b-244">The activity with signal is successfully sent.</span></span> |
| <span data-ttu-id="2e92b-245">**401**</span><span class="sxs-lookup"><span data-stu-id="2e92b-245">**401**</span></span> | <span data-ttu-id="2e92b-246">应用使用无效令牌进行响应。</span><span class="sxs-lookup"><span data-stu-id="2e92b-246">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="2e92b-247">**403**</span><span class="sxs-lookup"><span data-stu-id="2e92b-247">**403**</span></span> | <span data-ttu-id="2e92b-248">应用无法发送信号。</span><span class="sxs-lookup"><span data-stu-id="2e92b-248">The app is unable to send the signal.</span></span> <span data-ttu-id="2e92b-249">发生这种情况的原因有多种，例如租户管理员禁用应用、实时网站迁移期间阻止应用等。</span><span class="sxs-lookup"><span data-stu-id="2e92b-249">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="2e92b-250">在这种情况下，有效负载包含详细的错误消息。</span><span class="sxs-lookup"><span data-stu-id="2e92b-250">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="2e92b-251">**404**</span><span class="sxs-lookup"><span data-stu-id="2e92b-251">**404**</span></span> | <span data-ttu-id="2e92b-252">会议聊天不存在。</span><span class="sxs-lookup"><span data-stu-id="2e92b-252">The meeting chat does not exist.</span></span> |

### <a name="meeting-details-api"></a><span data-ttu-id="2e92b-253">会议详细信息 API</span><span class="sxs-lookup"><span data-stu-id="2e92b-253">Meeting Details API</span></span>

> [!NOTE]
> <span data-ttu-id="2e92b-254">此功能目前仅适用于公共 [开发人员预览](../resources/dev-preview/developer-preview-intro.md) 版。</span><span class="sxs-lookup"><span data-stu-id="2e92b-254">This feature is currently available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="2e92b-255">会议详细信息 API 使你的应用能够获取静态会议元数据。</span><span class="sxs-lookup"><span data-stu-id="2e92b-255">The Meeting Details API enables your app to get static meeting metadata.</span></span> <span data-ttu-id="2e92b-256">这些是不会动态更改的数据点。</span><span class="sxs-lookup"><span data-stu-id="2e92b-256">These are data points that do not change dynamically.</span></span>
<span data-ttu-id="2e92b-257">API 通过 Bot Services 提供。</span><span class="sxs-lookup"><span data-stu-id="2e92b-257">The API is available through Bot Services.</span></span>

#### <a name="prerequisite"></a><span data-ttu-id="2e92b-258">先决条件</span><span class="sxs-lookup"><span data-stu-id="2e92b-258">Prerequisite</span></span>

<span data-ttu-id="2e92b-259">若要使用会议详细信息 API，必须获取 RSC 权限。</span><span class="sxs-lookup"><span data-stu-id="2e92b-259">To use the Meeting Details API, you must obtain RSC permissions.</span></span> <span data-ttu-id="2e92b-260">使用以下示例配置应用清单 `webApplicationInfo` 的属性：</span><span class="sxs-lookup"><span data-stu-id="2e92b-260">Use the following example to configure your app manifest's `webApplicationInfo` property:</span></span>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```
 
#### <a name="query-parameter"></a><span data-ttu-id="2e92b-261">查询参数</span><span class="sxs-lookup"><span data-stu-id="2e92b-261">Query parameter</span></span>

<span data-ttu-id="2e92b-262">会议详细信息 API 包括以下查询参数：</span><span class="sxs-lookup"><span data-stu-id="2e92b-262">The Meeting Details API includes the following query parameter:</span></span>

|<span data-ttu-id="2e92b-263">值</span><span class="sxs-lookup"><span data-stu-id="2e92b-263">Value</span></span>|<span data-ttu-id="2e92b-264">类型</span><span class="sxs-lookup"><span data-stu-id="2e92b-264">Type</span></span>|<span data-ttu-id="2e92b-265">必需</span><span class="sxs-lookup"><span data-stu-id="2e92b-265">Required</span></span>|<span data-ttu-id="2e92b-266">说明</span><span class="sxs-lookup"><span data-stu-id="2e92b-266">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="2e92b-267">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="2e92b-267">**meetingId**</span></span>| <span data-ttu-id="2e92b-268">字符串</span><span class="sxs-lookup"><span data-stu-id="2e92b-268">String</span></span> | <span data-ttu-id="2e92b-269">是</span><span class="sxs-lookup"><span data-stu-id="2e92b-269">Yes</span></span> | <span data-ttu-id="2e92b-270">会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。</span><span class="sxs-lookup"><span data-stu-id="2e92b-270">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span> |

#### <a name="example"></a><span data-ttu-id="2e92b-271">示例</span><span class="sxs-lookup"><span data-stu-id="2e92b-271">Example</span></span>

<span data-ttu-id="2e92b-272">会议详细信息 API 包括以下示例：</span><span class="sxs-lookup"><span data-stu-id="2e92b-272">The Meeting Details API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="2e92b-273">C#</span><span class="sxs-lookup"><span data-stu-id="2e92b-273">C#</span></span>](#tab/dotnet)

```csharp
var connectorClient = turnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage(HttpMethod.Get, new Uri(new Uri(connectorClient.BaseUri.OriginalString), $"v1/meetings/{meetingId}"));
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, CancellationToken.None).ConfigureAwait(false);
string content;
if (response.Content != null)
{
    content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
}
```

# <a name="javascript"></a>[<span data-ttu-id="2e92b-274">JavaScript</span><span class="sxs-lookup"><span data-stu-id="2e92b-274">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="2e92b-275">不可用</span><span class="sxs-lookup"><span data-stu-id="2e92b-275">Not available</span></span>

# <a name="json"></a>[<span data-ttu-id="2e92b-276">JSON</span><span class="sxs-lookup"><span data-stu-id="2e92b-276">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}
```

---

<span data-ttu-id="2e92b-277">会议详细信息 API 的 JSON 响应正文如下所示：</span><span class="sxs-lookup"><span data-stu-id="2e92b-277">The JSON response body for Meeting Details API is as follows:</span></span>

```json
{ 
   "details": { 
        "id": "meeting ID", 
        "msGraphResourceId": "", 
        "scheduledStartTime": "2020-08-21T02:30:00+00:00", 
        "scheduledEndTime": "2020-08-21T03:00:00+00:00", 
        "joinUrl": "https://teams.microsoft.com/l/xx", 
        "title": "All Hands", 
        "type": "Scheduled" 
    }, 
    "conversation": { 
            "isGroup": true, 
            “conversationType”: “groupchat”, 
            "id": "meeting chat ID" 
    }, 
    "organizer": { 
        "id": "<organizer user ID>", 
        "aadObjectId": "<AAD ID>", 
        "tenantId": "<Tenant ID>" 
    }
} 
```

## <a name="real-time-teams-meeting-events"></a><span data-ttu-id="2e92b-278">实时Teams会议事件</span><span class="sxs-lookup"><span data-stu-id="2e92b-278">Real-time Teams meeting events</span></span>

> [!NOTE]
> <span data-ttu-id="2e92b-279">此功能目前仅适用于公共 [开发人员预览](../resources/dev-preview/developer-preview-intro.md) 版。</span><span class="sxs-lookup"><span data-stu-id="2e92b-279">This feature is currently available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="2e92b-280">用户可以接收实时会议事件。</span><span class="sxs-lookup"><span data-stu-id="2e92b-280">The user can receive real-time meeting events.</span></span> <span data-ttu-id="2e92b-281">只要任何应用与会议关联，就会与机器人共享实际会议开始时间和会议结束时间。</span><span class="sxs-lookup"><span data-stu-id="2e92b-281">As soon as any app is associated with a meeting, the actual meeting start and meeting end time are shared with the bot.</span></span>

<span data-ttu-id="2e92b-282">会议的实际开始时间和结束时间与计划的开始时间和结束时间不同。</span><span class="sxs-lookup"><span data-stu-id="2e92b-282">Actual start and end time of a meeting are different from the scheduled start and end time.</span></span> <span data-ttu-id="2e92b-283">会议详细信息 API 提供计划的开始时间和结束时间，而事件提供实际的开始时间和结束时间。</span><span class="sxs-lookup"><span data-stu-id="2e92b-283">The meeting details API provides the scheduled start and end time while the event provides the actual start and end time.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="2e92b-284">先决条件</span><span class="sxs-lookup"><span data-stu-id="2e92b-284">Prerequisite</span></span>

<span data-ttu-id="2e92b-285">应用清单必须具有 `webApplicationInfo` 属性，以接收会议开始和结束事件。</span><span class="sxs-lookup"><span data-stu-id="2e92b-285">Your app manifest must have the `webApplicationInfo` property to receive the meeting start and end events.</span></span> <span data-ttu-id="2e92b-286">使用以下示例配置清单：</span><span class="sxs-lookup"><span data-stu-id="2e92b-286">Use the following example to configure your manifest:</span></span>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

### <a name="example-of-meeting-start-event-payload"></a><span data-ttu-id="2e92b-287">会议开始事件有效负载的示例</span><span class="sxs-lookup"><span data-stu-id="2e92b-287">Example of meeting start event payload</span></span>

<span data-ttu-id="2e92b-288">以下代码提供了会议开始事件有效负载的示例：</span><span class="sxs-lookup"><span data-stu-id="2e92b-288">The following code provides an example of meeting start event payload:</span></span>

```json
{ 
    "name": "application/vnd.microsoft.meetingStart", 
    "type": "event", 
    "timestamp": "2021-04-29T16:10:41.1252256Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "userID", 
        "aadObjectId": "aadOnjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user Id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event", 
        "Id":"meeting id", 
        "JoinUrl": "url" 
        "StartTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

### <a name="example-of-meeting-end-event-payload"></a><span data-ttu-id="2e92b-289">会议结束事件有效负载的示例</span><span class="sxs-lookup"><span data-stu-id="2e92b-289">Example of meeting end event payload</span></span>

<span data-ttu-id="2e92b-290">以下代码提供了会议结束事件有效负载的示例：</span><span class="sxs-lookup"><span data-stu-id="2e92b-290">The following code provides an example of meeting end event payload:</span></span>

```json
{ 
    "name": "application/vnd.microsoft.meetingEnd", 
    "type": "event", 
    "timestamp": "2021-04-29T16:17:17.4388966Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "user id", 
        "aadObjectId": "aadObjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting Id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event in Canary", 
        "Id": "19:meeting_NTM3ZDJjOTUtZGRhOS00MzYxLTk5NDAtMzY4M2IzZWFjZGE1@thread.v2", 
        "JoinUrl": "url", 
        "EndTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

### <a name="example-of-getting-metadata-of-a-meeting"></a><span data-ttu-id="2e92b-291">获取会议元数据的示例</span><span class="sxs-lookup"><span data-stu-id="2e92b-291">Example of getting metadata of a meeting</span></span>

<span data-ttu-id="2e92b-292">机器人通过处理程序接收 `OnEventActivityAsync` 事件。</span><span class="sxs-lookup"><span data-stu-id="2e92b-292">Your bot receives the event through the `OnEventActivityAsync` handler.</span></span>

<span data-ttu-id="2e92b-293">为了反初始化 json 有效负载，引入了一个模型对象，用于获取会议元数据。</span><span class="sxs-lookup"><span data-stu-id="2e92b-293">To deserialize the json payload, a model object is introduced to get the metadata of a meeting.</span></span> <span data-ttu-id="2e92b-294">会议元数据驻留在事件有效 `value` 负载中的 属性中。</span><span class="sxs-lookup"><span data-stu-id="2e92b-294">The metadata of a meeting resides in the `value` property in the event payload.</span></span> <span data-ttu-id="2e92b-295">将 `MeetingStartEndEventvalue` 创建模型对象，其成员变量对应于事件有效负载 `value` 中的 属性下的键。</span><span class="sxs-lookup"><span data-stu-id="2e92b-295">The `MeetingStartEndEventvalue` model object is created, whose member variables correspond to the keys under the `value` property in the event payload.</span></span>

<span data-ttu-id="2e92b-296">以下代码演示如何从会议开始和结束事件捕获会议元数据，即 、 和 `MeetingType` `Title` `Id` `JoinUrl` `StartTime` `EndTime` ：</span><span class="sxs-lookup"><span data-stu-id="2e92b-296">The following code shows how to capture the metadata of a meeting that is `MeetingType`, `Title`, `Id`, `JoinUrl`, `StartTime`, and `EndTime` from a meeting start and end event:</span></span>

```csharp
protected override async Task OnEventActivityAsync(
ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    // Event Name is either 'application/vnd.microsoft.meetingStart' or 'application/vnd.microsoft.meetingEnd'
    var meetingEventName = turnContext.Activity.Name;
    // Value contains meeting information (ex: meeting type, start time, etc).
    var meetingEventInfo = turnContext.Activity.Value as JObject; 
    var meetingEventInfoObject =
meetingEventInfo.ToObject<MeetingStartEndEventValue>();
    // Create a very simple adaptive card with meeting information
var attachmentCard = createMeetingStartOrEndEventAttachment(meetingEventName,
meetingEventInfoObject);
    await turnContext.SendActivityAsync(MessageFactory.Attachment(attachmentCard));
}
```

<span data-ttu-id="2e92b-297">MeetingStartEndEventvalue.cs 包括以下代码：</span><span class="sxs-lookup"><span data-stu-id="2e92b-297">The MeetingStartEndEventvalue.cs includes the following code:</span></span>

```csharp
public class MeetingStartEndEventValue
{
    public string Id { get; set; }
    public string Title { get; set; }
    public string MeetingType { get; set; }
    public string JoinUrl { get; set; }
    public string StartTime { get; set; }
    public string EndTime { get; set; }
}
```

## <a name="code-sample"></a><span data-ttu-id="2e92b-298">代码示例</span><span class="sxs-lookup"><span data-stu-id="2e92b-298">Code sample</span></span>

|<span data-ttu-id="2e92b-299">示例名称</span><span class="sxs-lookup"><span data-stu-id="2e92b-299">Sample name</span></span> | <span data-ttu-id="2e92b-300">说明</span><span class="sxs-lookup"><span data-stu-id="2e92b-300">Description</span></span> | <span data-ttu-id="2e92b-301">.NET</span><span class="sxs-lookup"><span data-stu-id="2e92b-301">.NET</span></span> | <span data-ttu-id="2e92b-302">Node.js</span><span class="sxs-lookup"><span data-stu-id="2e92b-302">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="2e92b-303">会议可扩展性</span><span class="sxs-lookup"><span data-stu-id="2e92b-303">Meetings extensibility</span></span> | <span data-ttu-id="2e92b-304">Microsoft Teams令牌的会议扩展性示例。</span><span class="sxs-lookup"><span data-stu-id="2e92b-304">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="2e92b-305">View</span><span class="sxs-lookup"><span data-stu-id="2e92b-305">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [<span data-ttu-id="2e92b-306">View</span><span class="sxs-lookup"><span data-stu-id="2e92b-306">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| <span data-ttu-id="2e92b-307">会议内容气泡机器人</span><span class="sxs-lookup"><span data-stu-id="2e92b-307">Meeting content bubble bot</span></span> | <span data-ttu-id="2e92b-308">Microsoft Teams会议扩展性示例，用于与会议内容气泡机器人进行交互。</span><span class="sxs-lookup"><span data-stu-id="2e92b-308">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="2e92b-309">View</span><span class="sxs-lookup"><span data-stu-id="2e92b-309">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="2e92b-310">View</span><span class="sxs-lookup"><span data-stu-id="2e92b-310">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| <span data-ttu-id="2e92b-311">Meeting meetingSidePanel</span><span class="sxs-lookup"><span data-stu-id="2e92b-311">Meeting meetingSidePanel</span></span> | <span data-ttu-id="2e92b-312">Microsoft Teams与会议中的侧面板交互的会议扩展性示例。</span><span class="sxs-lookup"><span data-stu-id="2e92b-312">Microsoft Teams meeting extensibility sample for interacting with the side panel in-meeting.</span></span> | [<span data-ttu-id="2e92b-313">View</span><span class="sxs-lookup"><span data-stu-id="2e92b-313">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [<span data-ttu-id="2e92b-314">View</span><span class="sxs-lookup"><span data-stu-id="2e92b-314">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| <span data-ttu-id="2e92b-315">会议详细信息选项卡</span><span class="sxs-lookup"><span data-stu-id="2e92b-315">Details Tab in Meeting</span></span> | <span data-ttu-id="2e92b-316">Microsoft Teams会议扩展性示例，以在会议中通过详细信息选项卡进行激活。</span><span class="sxs-lookup"><span data-stu-id="2e92b-316">Microsoft Teams meeting extensibility sample for iteracting with Details Tab in-meeting.</span></span> | [<span data-ttu-id="2e92b-317">View</span><span class="sxs-lookup"><span data-stu-id="2e92b-317">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [<span data-ttu-id="2e92b-318">View</span><span class="sxs-lookup"><span data-stu-id="2e92b-318">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|

## <a name="see-also"></a><span data-ttu-id="2e92b-319">另请参阅</span><span class="sxs-lookup"><span data-stu-id="2e92b-319">See also</span></span>

* [<span data-ttu-id="2e92b-320">会议内对话设计指南</span><span class="sxs-lookup"><span data-stu-id="2e92b-320">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="2e92b-321">Teams选项卡的身份验证流</span><span class="sxs-lookup"><span data-stu-id="2e92b-321">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
* [<span data-ttu-id="2e92b-322">会议Teams应用程序</span><span class="sxs-lookup"><span data-stu-id="2e92b-322">Apps for Teams meetings</span></span>](teams-apps-in-meetings.md)

## <a name="next-step"></a><span data-ttu-id="2e92b-323">后续步骤</span><span class="sxs-lookup"><span data-stu-id="2e92b-323">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2e92b-324">为会议启用和配置Teams应用程序</span><span class="sxs-lookup"><span data-stu-id="2e92b-324">Enable and configure your apps for Teams meetings</span></span>](enable-and-configure-your-app-for-teams-meetings.md)
