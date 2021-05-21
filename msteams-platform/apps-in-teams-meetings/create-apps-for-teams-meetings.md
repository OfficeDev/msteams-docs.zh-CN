---
title: 创建适用于团队会议的应用
author: laujan
description: 创建团队会议应用
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams 应用会议用户参与者角色 api
ms.openlocfilehash: 84d0f5564d7e8e6e34dde1f3d59cc6e7a68d3332
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565912"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="a829f-104">创建适用于 Teams 会议的应用</span><span class="sxs-lookup"><span data-stu-id="a829f-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="a829f-105">先决条件和注意事项</span><span class="sxs-lookup"><span data-stu-id="a829f-105">Prerequisites and considerations</span></span>

<span data-ttu-id="a829f-106">为会议创建Teams之前，必须了解以下内容：</span><span class="sxs-lookup"><span data-stu-id="a829f-106">Before you create apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="a829f-107">你必须知道如何开发应用Teams知识。</span><span class="sxs-lookup"><span data-stu-id="a829f-107">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="a829f-108">有关详细信息，请参阅应用[Teams开发](../overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a829f-108">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="a829f-109">必须更新Teams清单，以指示该应用可用于会议。</span><span class="sxs-lookup"><span data-stu-id="a829f-109">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="a829f-110">有关详细信息，请参阅 [应用清单](#update-your-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="a829f-110">For more information, see [app manifest](#update-your-app-manifest).</span></span>

* <span data-ttu-id="a829f-111">若要使应用在会议生命周期中作为选项卡运行，它必须支持 groupchat 作用域中的可配置选项卡。</span><span class="sxs-lookup"><span data-stu-id="a829f-111">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the groupchat scope.</span></span> <span data-ttu-id="a829f-112">有关详细信息，请参阅 [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="a829f-112">For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="a829f-113">对于会议前和Teams方案，必须遵循常规选项卡设计准则。</span><span class="sxs-lookup"><span data-stu-id="a829f-113">You must adhere to general Teams tab design guidelines for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="a829f-114">有关会议期间的体验，请参阅会议内选项卡和会议内对话框设计指南。</span><span class="sxs-lookup"><span data-stu-id="a829f-114">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="a829f-115">有关详细信息，请参阅Teams[选项卡设计指南](../tabs/design/tabs.md)、会议中的[选项卡](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)设计指南和[会议中的对话框设计指南](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。</span><span class="sxs-lookup"><span data-stu-id="a829f-115">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="a829f-116">必须支持范围才能在会议前和会议后聊天 `groupchat` 中启用应用。</span><span class="sxs-lookup"><span data-stu-id="a829f-116">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="a829f-117">通过会议前应用体验，你可以查找和添加会议应用并执行会议前任务。</span><span class="sxs-lookup"><span data-stu-id="a829f-117">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="a829f-118">通过会议后应用体验，可以查看会议结果，如投票调查结果或反馈。</span><span class="sxs-lookup"><span data-stu-id="a829f-118">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="a829f-119">会议 API URL 参数必须具有 `meetingId` 、 `userId` 和 `tenantId` 。</span><span class="sxs-lookup"><span data-stu-id="a829f-119">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="a829f-120">它们作为客户端 SDK 和自动程序Teams的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="a829f-120">These are available as part of the Teams client SDK and bot activity.</span></span> <span data-ttu-id="a829f-121">此外，可以使用 Tab SSO 身份验证检索用户 ID 和租户 ID [的可靠信息](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="a829f-121">In addition, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="a829f-122">`GetParticipant`API 必须具有自动程序注册和 ID，以生成身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="a829f-122">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="a829f-123">有关详细信息，请参阅自动[程序注册和 ID。](../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="a829f-123">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="a829f-124">若要实时更新应用，应用必须基于会议中的活动活动是最新的。</span><span class="sxs-lookup"><span data-stu-id="a829f-124">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="a829f-125">这些事件可以位于会议中的对话框内以及整个会议生命周期的其他阶段。</span><span class="sxs-lookup"><span data-stu-id="a829f-125">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="a829f-126">有关会议中的对话框，请参阅 中的 `bot Id` 完成参数 `Notification Signal API` 。</span><span class="sxs-lookup"><span data-stu-id="a829f-126">For the in-meeting dialog box, see completion `bot Id` parameter in `Notification Signal API`.</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="a829f-127">会议应用 API 参考</span><span class="sxs-lookup"><span data-stu-id="a829f-127">Meeting apps API reference</span></span>

|<span data-ttu-id="a829f-128">API</span><span class="sxs-lookup"><span data-stu-id="a829f-128">API</span></span>|<span data-ttu-id="a829f-129">描述</span><span class="sxs-lookup"><span data-stu-id="a829f-129">Description</span></span>|<span data-ttu-id="a829f-130">请求</span><span class="sxs-lookup"><span data-stu-id="a829f-130">Request</span></span>|<span data-ttu-id="a829f-131">源</span><span class="sxs-lookup"><span data-stu-id="a829f-131">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="a829f-132">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="a829f-132">**GetUserContext**</span></span>| <span data-ttu-id="a829f-133">此 API 使你能够获取上下文信息，以在"开始"选项卡中Teams内容。</span><span class="sxs-lookup"><span data-stu-id="a829f-133">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="a829f-134">_**microsoftTeams.getContext ( ( ) => { /*...*/ } )**_</span><span class="sxs-lookup"><span data-stu-id="a829f-134">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="a829f-135">Microsoft Teams客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="a829f-135">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="a829f-136">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="a829f-136">**GetParticipant**</span></span>| <span data-ttu-id="a829f-137">此 API 允许机器人通过会议 ID 和参与者 ID 获取参与者信息。</span><span class="sxs-lookup"><span data-stu-id="a829f-137">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="a829f-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}？tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="a829f-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="a829f-139">Microsoft Bot FrameworkSDK</span><span class="sxs-lookup"><span data-stu-id="a829f-139">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="a829f-140">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="a829f-140">**NotificationSignal**</span></span> | <span data-ttu-id="a829f-141">此 API 使你能够提供使用用户-机器人聊天的现有对话通知 API 传递的会议信号。</span><span class="sxs-lookup"><span data-stu-id="a829f-141">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="a829f-142">它允许您根据显示会议内对话框的用户操作发出信号。</span><span class="sxs-lookup"><span data-stu-id="a829f-142">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="a829f-143">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="a829f-143">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="a829f-144">Microsoft Bot FrameworkSDK</span><span class="sxs-lookup"><span data-stu-id="a829f-144">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="a829f-145">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="a829f-145">GetUserContext</span></span>

<span data-ttu-id="a829f-146">若要标识和检索选项卡内容的上下文信息，请参阅获取选项卡Teams[上下文](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library)。`meetingId`在会议上下文中运行时选项卡使用，并添加响应有效负载。</span><span class="sxs-lookup"><span data-stu-id="a829f-146">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="a829f-147">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="a829f-147">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="a829f-148">不要缓存参与者角色，因为会议组织者可以随时更改角色。</span><span class="sxs-lookup"><span data-stu-id="a829f-148">Do not cache participant roles since the meeting organizer can change a role any time.</span></span>
> * <span data-ttu-id="a829f-149">Teams API 当前不支持超过 350 个参与者的大型通讯组列表或名单 `GetParticipant` 大小。</span><span class="sxs-lookup"><span data-stu-id="a829f-149">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="a829f-150">查询参数</span><span class="sxs-lookup"><span data-stu-id="a829f-150">Query parameters</span></span>

|<span data-ttu-id="a829f-151">值</span><span class="sxs-lookup"><span data-stu-id="a829f-151">Value</span></span>|<span data-ttu-id="a829f-152">类型</span><span class="sxs-lookup"><span data-stu-id="a829f-152">Type</span></span>|<span data-ttu-id="a829f-153">必需</span><span class="sxs-lookup"><span data-stu-id="a829f-153">Required</span></span>|<span data-ttu-id="a829f-154">说明</span><span class="sxs-lookup"><span data-stu-id="a829f-154">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="a829f-155">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="a829f-155">**meetingId**</span></span>| <span data-ttu-id="a829f-156">string</span><span class="sxs-lookup"><span data-stu-id="a829f-156">string</span></span> | <span data-ttu-id="a829f-157">是</span><span class="sxs-lookup"><span data-stu-id="a829f-157">Yes</span></span> | <span data-ttu-id="a829f-158">会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。</span><span class="sxs-lookup"><span data-stu-id="a829f-158">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="a829f-159">**participantId**</span><span class="sxs-lookup"><span data-stu-id="a829f-159">**participantId**</span></span>| <span data-ttu-id="a829f-160">string</span><span class="sxs-lookup"><span data-stu-id="a829f-160">string</span></span> | <span data-ttu-id="a829f-161">是</span><span class="sxs-lookup"><span data-stu-id="a829f-161">Yes</span></span> | <span data-ttu-id="a829f-162">参与者 ID 是用户 ID。</span><span class="sxs-lookup"><span data-stu-id="a829f-162">The participant ID is the user ID.</span></span> <span data-ttu-id="a829f-163">它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。</span><span class="sxs-lookup"><span data-stu-id="a829f-163">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="a829f-164">建议从选项卡 SSO 获取参与者 ID。</span><span class="sxs-lookup"><span data-stu-id="a829f-164">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="a829f-165">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="a829f-165">**tenantId**</span></span>| <span data-ttu-id="a829f-166">string</span><span class="sxs-lookup"><span data-stu-id="a829f-166">string</span></span> | <span data-ttu-id="a829f-167">是</span><span class="sxs-lookup"><span data-stu-id="a829f-167">Yes</span></span> | <span data-ttu-id="a829f-168">租户用户需要租户 ID。</span><span class="sxs-lookup"><span data-stu-id="a829f-168">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="a829f-169">它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。</span><span class="sxs-lookup"><span data-stu-id="a829f-169">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="a829f-170">建议从选项卡 SSO 获取租户 ID。</span><span class="sxs-lookup"><span data-stu-id="a829f-170">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="a829f-171">示例</span><span class="sxs-lookup"><span data-stu-id="a829f-171">Example</span></span>

# <a name="c"></a>[<span data-ttu-id="a829f-172">C#</span><span class="sxs-lookup"><span data-stu-id="a829f-172">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
  TeamsChannelAccount member = participant.User;
  MeetingParticipantInfo meetingInfo = participant.Meeting;
  ConversationAccount conversation = participant.Conversation;

  await turnContext.SendActivityAsync(MessageFactory.Text($"The participant role is: {meetingInfo.Role}"), cancellationToken);
}

```

# <a name="javascript"></a>[<span data-ttu-id="a829f-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="a829f-173">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="a829f-174">JSON</span><span class="sxs-lookup"><span data-stu-id="a829f-174">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

* * *

<span data-ttu-id="a829f-175">API 的 JSON 响应 `GetParticipant` 正文为：</span><span class="sxs-lookup"><span data-stu-id="a829f-175">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="a829f-176">响应代码</span><span class="sxs-lookup"><span data-stu-id="a829f-176">Response codes</span></span>

|<span data-ttu-id="a829f-177">响应代码</span><span class="sxs-lookup"><span data-stu-id="a829f-177">Response code</span></span>|<span data-ttu-id="a829f-178">描述</span><span class="sxs-lookup"><span data-stu-id="a829f-178">Description</span></span>|
|---|---|
| <span data-ttu-id="a829f-179">**403**</span><span class="sxs-lookup"><span data-stu-id="a829f-179">**403**</span></span> | <span data-ttu-id="a829f-180">不允许应用获取参与者信息。</span><span class="sxs-lookup"><span data-stu-id="a829f-180">The app is not allowed to get participant information.</span></span> <span data-ttu-id="a829f-181">这是最常见的错误响应，如果会议未安装应用，将触发此错误响应。</span><span class="sxs-lookup"><span data-stu-id="a829f-181">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="a829f-182">例如，如果租户管理员禁用应用或在实时网站迁移期间阻止应用。</span><span class="sxs-lookup"><span data-stu-id="a829f-182">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="a829f-183">**200**</span><span class="sxs-lookup"><span data-stu-id="a829f-183">**200**</span></span> | <span data-ttu-id="a829f-184">成功检索参与者信息。</span><span class="sxs-lookup"><span data-stu-id="a829f-184">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="a829f-185">**401**</span><span class="sxs-lookup"><span data-stu-id="a829f-185">**401**</span></span> | <span data-ttu-id="a829f-186">应用使用无效令牌进行响应。</span><span class="sxs-lookup"><span data-stu-id="a829f-186">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="a829f-187">**404**</span><span class="sxs-lookup"><span data-stu-id="a829f-187">**404**</span></span> | <span data-ttu-id="a829f-188">会议已过期或找不到参与者。</span><span class="sxs-lookup"><span data-stu-id="a829f-188">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="a829f-189">**500**</span><span class="sxs-lookup"><span data-stu-id="a829f-189">**500**</span></span> | <span data-ttu-id="a829f-190">会议自会议结束以来的 60 天以上已过期，或者参与者没有基于其角色的权限。</span><span class="sxs-lookup"><span data-stu-id="a829f-190">The meeting has either expired more than 60 days since the meeting ended or the participant does not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="a829f-191">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="a829f-191">NotificationSignal API</span></span>

<span data-ttu-id="a829f-192">会议中的所有用户都接收通过 API 发送 `NotificationSignal` 的通知。</span><span class="sxs-lookup"><span data-stu-id="a829f-192">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="a829f-193">调用会议内对话框时，内容将显示为聊天消息。</span><span class="sxs-lookup"><span data-stu-id="a829f-193">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="a829f-194">目前，不支持发送定向通知。</span><span class="sxs-lookup"><span data-stu-id="a829f-194">Currently, sending targeted notifications is not supported.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="a829f-195">查询参数</span><span class="sxs-lookup"><span data-stu-id="a829f-195">Query parameters</span></span>

|<span data-ttu-id="a829f-196">值</span><span class="sxs-lookup"><span data-stu-id="a829f-196">Value</span></span>|<span data-ttu-id="a829f-197">类型</span><span class="sxs-lookup"><span data-stu-id="a829f-197">Type</span></span>|<span data-ttu-id="a829f-198">必需</span><span class="sxs-lookup"><span data-stu-id="a829f-198">Required</span></span>|<span data-ttu-id="a829f-199">说明</span><span class="sxs-lookup"><span data-stu-id="a829f-199">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="a829f-200">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="a829f-200">**conversationId**</span></span>| <span data-ttu-id="a829f-201">string</span><span class="sxs-lookup"><span data-stu-id="a829f-201">string</span></span> | <span data-ttu-id="a829f-202">是</span><span class="sxs-lookup"><span data-stu-id="a829f-202">Yes</span></span> | <span data-ttu-id="a829f-203">对话标识符作为自动程序调用的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="a829f-203">The conversation identifier is available as part of bot invoke.</span></span> |

#### <a name="example"></a><span data-ttu-id="a829f-204">示例</span><span class="sxs-lookup"><span data-stu-id="a829f-204">Example</span></span>

<span data-ttu-id="a829f-205">`Bot ID`在清单中声明 ，机器人将接收结果对象。</span><span class="sxs-lookup"><span data-stu-id="a829f-205">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="a829f-206">`completionBotId`在请求 `externalResourceUrl` 的有效负载示例中，的 参数是可选的。</span><span class="sxs-lookup"><span data-stu-id="a829f-206">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="a829f-207">`Bot ID` 在清单中声明，机器人将接收结果对象。</span><span class="sxs-lookup"><span data-stu-id="a829f-207">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="a829f-208">`externalResourceUrl`宽度和高度参数必须以像素为单位。</span><span class="sxs-lookup"><span data-stu-id="a829f-208">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="a829f-209">若要确保尺寸在允许的限制内，请参阅 [设计指南](design/designing-apps-in-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="a829f-209">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="a829f-210">URL 是在会议对话框中作为 `<iframe>` 加载的页面。</span><span class="sxs-lookup"><span data-stu-id="a829f-210">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="a829f-211">域必须在你的应用清单 `validDomains` 的应用数组中。</span><span class="sxs-lookup"><span data-stu-id="a829f-211">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="c"></a>[<span data-ttu-id="a829f-212">C#</span><span class="sxs-lookup"><span data-stu-id="a829f-212">C#</span></span>](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");

activity.ChannelData = new TeamsChannelData
  {
    Notification = new NotificationInfo()
                    {
                        AlertInMeeting = true,
                        ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
                    }
  };
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[<span data-ttu-id="a829f-213">JavaScript</span><span class="sxs-lookup"><span data-stu-id="a829f-213">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="a829f-214">JSON</span><span class="sxs-lookup"><span data-stu-id="a829f-214">JSON</span></span>](#tab/json)

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

* * *

#### <a name="response-codes"></a><span data-ttu-id="a829f-215">响应代码</span><span class="sxs-lookup"><span data-stu-id="a829f-215">Response codes</span></span>

|<span data-ttu-id="a829f-216">响应代码</span><span class="sxs-lookup"><span data-stu-id="a829f-216">Response code</span></span>|<span data-ttu-id="a829f-217">描述</span><span class="sxs-lookup"><span data-stu-id="a829f-217">Description</span></span>|
|---|---|
| <span data-ttu-id="a829f-218">**201**</span><span class="sxs-lookup"><span data-stu-id="a829f-218">**201**</span></span> | <span data-ttu-id="a829f-219">具有信号的活动已成功发送。</span><span class="sxs-lookup"><span data-stu-id="a829f-219">The activity with signal is successfully sent.</span></span> |
| <span data-ttu-id="a829f-220">**401**</span><span class="sxs-lookup"><span data-stu-id="a829f-220">**401**</span></span> | <span data-ttu-id="a829f-221">应用使用无效令牌进行响应。</span><span class="sxs-lookup"><span data-stu-id="a829f-221">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="a829f-222">**403**</span><span class="sxs-lookup"><span data-stu-id="a829f-222">**403**</span></span> | <span data-ttu-id="a829f-223">应用无法发送信号。</span><span class="sxs-lookup"><span data-stu-id="a829f-223">The app is unable to send the signal.</span></span> <span data-ttu-id="a829f-224">发生这种情况的原因有多种，例如租户管理员禁用应用、实时网站迁移期间阻止应用等。</span><span class="sxs-lookup"><span data-stu-id="a829f-224">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="a829f-225">在这种情况下，有效负载包含详细的错误消息。</span><span class="sxs-lookup"><span data-stu-id="a829f-225">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="a829f-226">**404**</span><span class="sxs-lookup"><span data-stu-id="a829f-226">**404**</span></span> | <span data-ttu-id="a829f-227">会议聊天不存在。</span><span class="sxs-lookup"><span data-stu-id="a829f-227">The meeting chat does not exist.</span></span> |

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="a829f-228">为应用启用Teams会议</span><span class="sxs-lookup"><span data-stu-id="a829f-228">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="a829f-229">更新应用清单</span><span class="sxs-lookup"><span data-stu-id="a829f-229">Update your app manifest</span></span>

<span data-ttu-id="a829f-230">会议应用功能使用 、 和 数组在应用清单 `configurableTabs` `scopes` `context` 中声明。</span><span class="sxs-lookup"><span data-stu-id="a829f-230">The meetings app capabilities are declared in your app manifest using the `configurableTabs`, `scopes`, and `context` arrays.</span></span> <span data-ttu-id="a829f-231">范围定义谁，上下文定义你的应用的可用位置。</span><span class="sxs-lookup"><span data-stu-id="a829f-231">Scope defines to whom and context defines where your app is available.</span></span>

> [!NOTE]
> <span data-ttu-id="a829f-232">尝试使用清单架构更新 [应用清单](../resources/schema/manifest-schema-dev-preview.md)。</span><span class="sxs-lookup"><span data-stu-id="a829f-232">Try updating your app manifest with the [manifest schema](../resources/schema/manifest-schema-dev-preview.md).</span></span>
> <span data-ttu-id="a829f-233">会议中的应用程序需要 *群聊* 范围。</span><span class="sxs-lookup"><span data-stu-id="a829f-233">Apps in meetings need *groupchat* scope.</span></span> <span data-ttu-id="a829f-234">团队 *作用域* 仅适用于频道中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="a829f-234">The *team* scope works for tabs in channels only.</span></span>

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team",
        "groupchat"
      ],
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```
> [!NOTE]
> <span data-ttu-id="a829f-235">`meetingStage` 当前仅适用于开发人员预览版。</span><span class="sxs-lookup"><span data-stu-id="a829f-235">`meetingStage` is currently available in developer preview only.</span></span>

### <a name="context-property"></a><span data-ttu-id="a829f-236">Context 属性</span><span class="sxs-lookup"><span data-stu-id="a829f-236">Context property</span></span>

<span data-ttu-id="a829f-237">选项卡 `context` 和 `scopes` 属性使你可以确定应用必须出现在何处。</span><span class="sxs-lookup"><span data-stu-id="a829f-237">The tab `context` and `scopes` properties enable you to determine where your app must appear.</span></span> <span data-ttu-id="a829f-238">或 作用域 `team` `groupchat` 中的选项卡可以具有多个上下文。</span><span class="sxs-lookup"><span data-stu-id="a829f-238">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="a829f-239">以下是可以使用所有或部分 `context` 值的 属性的值：</span><span class="sxs-lookup"><span data-stu-id="a829f-239">Following are the values for the `context` property from which you can use all or some of the values:</span></span>

|<span data-ttu-id="a829f-240">值</span><span class="sxs-lookup"><span data-stu-id="a829f-240">Value</span></span>|<span data-ttu-id="a829f-241">说明</span><span class="sxs-lookup"><span data-stu-id="a829f-241">Description</span></span>|
|---|---|
| <span data-ttu-id="a829f-242">**channelTab**</span><span class="sxs-lookup"><span data-stu-id="a829f-242">**channelTab**</span></span> | <span data-ttu-id="a829f-243">团队频道标题中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="a829f-243">A tab in the header of a team channel.</span></span> |
| <span data-ttu-id="a829f-244">**privateChatTab**</span><span class="sxs-lookup"><span data-stu-id="a829f-244">**privateChatTab**</span></span> | <span data-ttu-id="a829f-245">一组不在团队或会议上下文中的用户之间的群聊标题中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="a829f-245">A tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span> |
| <span data-ttu-id="a829f-246">**meetingChatTab**</span><span class="sxs-lookup"><span data-stu-id="a829f-246">**meetingChatTab**</span></span> | <span data-ttu-id="a829f-247">计划会议上下文中的一组用户之间的群聊标题中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="a829f-247">A tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span> |
| <span data-ttu-id="a829f-248">**meetingDetailsTab**</span><span class="sxs-lookup"><span data-stu-id="a829f-248">**meetingDetailsTab**</span></span> | <span data-ttu-id="a829f-249">日历的会议详细信息视图标题中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="a829f-249">A tab in the header of the meeting details view of the calendar.</span></span> |
| <span data-ttu-id="a829f-250">**meetingSidePanel**</span><span class="sxs-lookup"><span data-stu-id="a829f-250">**meetingSidePanel**</span></span> | <span data-ttu-id="a829f-251">通过统一栏和 U 条形图 (打开的会议内) 。</span><span class="sxs-lookup"><span data-stu-id="a829f-251">An in-meeting panel opened via the unified bar (U-bar).</span></span> |
| <span data-ttu-id="a829f-252">**meetingStage**</span><span class="sxs-lookup"><span data-stu-id="a829f-252">**meetingStage**</span></span> | <span data-ttu-id="a829f-253">可以将来自侧窗格的应用共享到会议阶段。</span><span class="sxs-lookup"><span data-stu-id="a829f-253">An app from the sidepanel can be shared to the meeting stage.</span></span> |

> [!NOTE]
> <span data-ttu-id="a829f-254">`Context` 属性当前在移动客户端上不受支持。</span><span class="sxs-lookup"><span data-stu-id="a829f-254">`Context` property is currently not supported on mobile clients.</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="a829f-255">为会议方案配置应用</span><span class="sxs-lookup"><span data-stu-id="a829f-255">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="a829f-256">若要使应用在选项卡库中可见，它必须支持可配置的选项卡和群聊范围。</span><span class="sxs-lookup"><span data-stu-id="a829f-256">For your app to be visible in the tab gallery it must support configurable tabs and the group chat scope.</span></span>
> * <span data-ttu-id="a829f-257">移动客户端仅在会议前和会议后阶段支持选项卡。</span><span class="sxs-lookup"><span data-stu-id="a829f-257">Mobile clients support tabs only in pre and post meeting stages.</span></span>
> * <span data-ttu-id="a829f-258">移动客户端当前不支持会议内对话框和选项卡中的会议体验。</span><span class="sxs-lookup"><span data-stu-id="a829f-258">The in-meeting experiences that is in-meeting dialog box and tab is currently not supported on mobile clients.</span></span> <span data-ttu-id="a829f-259">有关详细信息，请参阅 [为移动设备创建选项卡](../tabs/design/tabs-mobile.md) 时移动选项卡指南。</span><span class="sxs-lookup"><span data-stu-id="a829f-259">For more information, see [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="a829f-260">会议前</span><span class="sxs-lookup"><span data-stu-id="a829f-260">Before a meeting</span></span>

<span data-ttu-id="a829f-261">在会议之前，用户可以向会议添加选项卡、聊天机器人和消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="a829f-261">Before a meeting, users can add tabs, bots and messaging extensions to a meeting.</span></span> <span data-ttu-id="a829f-262">具有组织者和演示者角色的用户可以向会议添加选项卡。</span><span class="sxs-lookup"><span data-stu-id="a829f-262">Users with organizer and presenter roles can add tabs to a meeting.</span></span>

<span data-ttu-id="a829f-263">**向会议添加选项卡**</span><span class="sxs-lookup"><span data-stu-id="a829f-263">**To add a tab to a meeting**</span></span>

1. <span data-ttu-id="a829f-264">在日历中，选择要添加选项卡的会议。</span><span class="sxs-lookup"><span data-stu-id="a829f-264">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="a829f-265">选择详细信息 **选项卡** 并选择加号</span><span class="sxs-lookup"><span data-stu-id="a829f-265">Select the **Details** tab and select plus</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="a829f-266">.</span><span class="sxs-lookup"><span data-stu-id="a829f-266">.</span></span> <span data-ttu-id="a829f-267">将显示选项卡库。</span><span class="sxs-lookup"><span data-stu-id="a829f-267">The tab gallery appears.</span></span>

    ![会议前体验](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="a829f-269">在选项卡库中，选择要添加的应用并按照所需步骤操作。</span><span class="sxs-lookup"><span data-stu-id="a829f-269">In the tab gallery, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="a829f-270">应用作为选项卡安装。</span><span class="sxs-lookup"><span data-stu-id="a829f-270">The app is installed as a tab.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="a829f-271">目前，在"会议"选项卡中，不支持获取会议详细信息和参与者信息。</span><span class="sxs-lookup"><span data-stu-id="a829f-271">Currently, in meetings tab, getting meeting details and participant information is not supported.</span></span>

<span data-ttu-id="a829f-272">**将消息传递扩展添加到会议**</span><span class="sxs-lookup"><span data-stu-id="a829f-272">**To add a messaging extension to a meeting**</span></span>

1. <span data-ttu-id="a829f-273">选择位于聊天的撰写 &#x25CF;&#x25CF;&#x25CF; 消息区域中的省略号或溢出菜单。</span><span class="sxs-lookup"><span data-stu-id="a829f-273">Select the ellipses or overflow menu &#x25CF;&#x25CF;&#x25CF; located in the compose message area in the chat.</span></span>
1. <span data-ttu-id="a829f-274">选择要添加的应用并按照所需步骤操作。</span><span class="sxs-lookup"><span data-stu-id="a829f-274">Select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="a829f-275">应用作为消息传递扩展进行安装。</span><span class="sxs-lookup"><span data-stu-id="a829f-275">The app is installed as a messaging extension.</span></span>

<span data-ttu-id="a829f-276">**将机器人添加到会议**</span><span class="sxs-lookup"><span data-stu-id="a829f-276">**To add a bot to a meeting**</span></span>

<span data-ttu-id="a829f-277">在会议聊天中， **@** 输入密钥并选择"**获取机器人"。**</span><span class="sxs-lookup"><span data-stu-id="a829f-277">In a meeting chat enter the **@** key and select **Get bots**.</span></span>

> [!NOTE]
> * <span data-ttu-id="a829f-278">必须使用选项卡 SSO 确认 [用户标识](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="a829f-278">The user identity must be confirmed using [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="a829f-279">身份验证后，应用可以使用 API 检索用户 `GetParticipant` 角色。</span><span class="sxs-lookup"><span data-stu-id="a829f-279">After authentication, the app can retrieve the user role using the `GetParticipant` API.</span></span>
> * <span data-ttu-id="a829f-280">根据用户角色，应用能够提供特定于角色的体验。</span><span class="sxs-lookup"><span data-stu-id="a829f-280">Based on the user role, the app has the capability to provide role specific experiences.</span></span> <span data-ttu-id="a829f-281">例如，轮询应用仅允许组织者和演示者创建新的轮询。</span><span class="sxs-lookup"><span data-stu-id="a829f-281">For example, a polling app allows only organizers and presenters to create a new poll.</span></span>
> * <span data-ttu-id="a829f-282">可以在会议进行时更改角色分配。</span><span class="sxs-lookup"><span data-stu-id="a829f-282">Role assignments can be changed while a meeting is in progress.</span></span> <span data-ttu-id="a829f-283">有关详细信息，请参阅[会议Teams角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。</span><span class="sxs-lookup"><span data-stu-id="a829f-283">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

### <a name="during-a-meeting"></a><span data-ttu-id="a829f-284">会议期间</span><span class="sxs-lookup"><span data-stu-id="a829f-284">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="a829f-285">sidePanel</span><span class="sxs-lookup"><span data-stu-id="a829f-285">sidePanel</span></span>

<span data-ttu-id="a829f-286">借助 sidePanel，你可以自定义会议体验，使组织者和演示者拥有一组不同的视图和操作。</span><span class="sxs-lookup"><span data-stu-id="a829f-286">With the sidePanel, you can customize experiences in a meeting that enable organizers and presenters to have different set of views and actions.</span></span> <span data-ttu-id="a829f-287">在应用清单中，必须将 sidePanel 添加到上下文数组。</span><span class="sxs-lookup"><span data-stu-id="a829f-287">In your app manifest, you must add sidePanel to the context array.</span></span> <span data-ttu-id="a829f-288">在会议以及所有方案中，应用在宽度为 320 像素的"会议内"选项卡中呈现。</span><span class="sxs-lookup"><span data-stu-id="a829f-288">In the meeting and in all scenarios, the app is rendered in an in-meeting tab that is 320 pixels in width.</span></span> <span data-ttu-id="a829f-289">有关详细信息，请参阅 [FrameContext 接口](/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)。</span><span class="sxs-lookup"><span data-stu-id="a829f-289">For more information, see [FrameContext interface](/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
).</span></span>

<span data-ttu-id="a829f-290">若要使用 `userContext` API 相应地路由请求，请参阅[Teams SDK。](../tabs/how-to/access-teams-context.md#user-context)</span><span class="sxs-lookup"><span data-stu-id="a829f-290">To use the `userContext` API to route requests accordingly, see [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span></span> <span data-ttu-id="a829f-291">请参阅[Teams的身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="a829f-291">See [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="a829f-292">选项卡的身份验证流与网站的身份验证流非常相似。</span><span class="sxs-lookup"><span data-stu-id="a829f-292">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="a829f-293">因此选项卡可以直接使用 OAuth 2.0。</span><span class="sxs-lookup"><span data-stu-id="a829f-293">So tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="a829f-294">请参阅Microsoft 标识平台[OAuth 2.0 授权代码流](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。</span><span class="sxs-lookup"><span data-stu-id="a829f-294">See, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="a829f-295">当用户在会议视图中并且用户可以发布撰写邮件扩展卡时，邮件扩展将按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="a829f-295">Messaging extension works as expected when a user is in an in-meeting view and the user can post compose message extension cards.</span></span> <span data-ttu-id="a829f-296">AppName 会议内是一个工具提示，用于指出会议 U 栏中的应用名称。</span><span class="sxs-lookup"><span data-stu-id="a829f-296">AppName in-meeting is a tooltip that states the app name in-meeting U-bar.</span></span>

> [!NOTE]
> <span data-ttu-id="a829f-297">使用版本 1.7.0 或更高版本[的 Teams SDK，](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)因为它之前的版本不支持侧面板。</span><span class="sxs-lookup"><span data-stu-id="a829f-297">Use version 1.7.0 or higher of [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), as versions prior to it do not support the side panel.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="a829f-298">会议内的对话框</span><span class="sxs-lookup"><span data-stu-id="a829f-298">In-meeting dialog</span></span>

<span data-ttu-id="a829f-299">会议内对话框可用于在会议期间与参与者互动，并收集会议期间的信息或反馈。</span><span class="sxs-lookup"><span data-stu-id="a829f-299">The in-meeting dialog box can be used to engage participants during the meeting and collect information or feedback during the meeting.</span></span> <span data-ttu-id="a829f-300">使用 [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API 指示必须触发气泡通知。</span><span class="sxs-lookup"><span data-stu-id="a829f-300">Use the [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification must be triggered.</span></span> <span data-ttu-id="a829f-301">作为通知请求有效负载的一部分，请包含要显示内容的托管 URL。</span><span class="sxs-lookup"><span data-stu-id="a829f-301">As part of the notification request payload, include the URL where the content to be shown is hosted.</span></span>

<span data-ttu-id="a829f-302">会议内对话框不得使用任务模块。</span><span class="sxs-lookup"><span data-stu-id="a829f-302">In-meeting dialog must not use task module.</span></span> <span data-ttu-id="a829f-303">会议聊天中不会调用任务模块。</span><span class="sxs-lookup"><span data-stu-id="a829f-303">Task module is not invoked in a meeting chat.</span></span> <span data-ttu-id="a829f-304">外部资源 URL 用于在会议中显示内容气泡。</span><span class="sxs-lookup"><span data-stu-id="a829f-304">An external resource URL is used to display content bubble in a meeting.</span></span> <span data-ttu-id="a829f-305">可以使用 方法 `submitTask` 在会议聊天中提交数据。</span><span class="sxs-lookup"><span data-stu-id="a829f-305">You can use the `submitTask` method to submit data in a meeting chat.</span></span>

> [!NOTE]
> * <span data-ttu-id="a829f-306">你必须调用 [submitTask () ](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 函数，以在用户执行 Web 视图中的操作后自动消除。</span><span class="sxs-lookup"><span data-stu-id="a829f-306">You must invoke the [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to dismiss automatically after a user takes an action in the web-view.</span></span> <span data-ttu-id="a829f-307">这是应用提交的要求。</span><span class="sxs-lookup"><span data-stu-id="a829f-307">This is a requirement for app submission.</span></span> <span data-ttu-id="a829f-308">有关详细信息，请参阅Teams [SDK 任务模块](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="a829f-308">For more information, see [Teams SDK task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
> * <span data-ttu-id="a829f-309">如果希望你的应用支持匿名用户，则初始调用请求有效负载必须依赖于 对象中的请求元数据， `from.id` `from` 而不是 `from.aadObjectId` 请求元数据。</span><span class="sxs-lookup"><span data-stu-id="a829f-309">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id` request metadata in the `from` object, not the `from.aadObjectId` request metadata.</span></span> <span data-ttu-id="a829f-310">`from.id`是用户 `from.aadObjectId` ID，也是Azure Active Directory (AAD) ID。</span><span class="sxs-lookup"><span data-stu-id="a829f-310">`from.id` is the user ID and `from.aadObjectId` is the Azure Active Directory (AAD) ID of the user.</span></span> <span data-ttu-id="a829f-311">有关详细信息，请参阅在 [选项卡中使用任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md) 以及 [创建和发送任务模块](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。</span><span class="sxs-lookup"><span data-stu-id="a829f-311">For more information, see [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

#### <a name="share-to-stage"></a><span data-ttu-id="a829f-312">共享到阶段</span><span class="sxs-lookup"><span data-stu-id="a829f-312">Share to stage</span></span> 

> [!NOTE]
> * <span data-ttu-id="a829f-313">此功能目前仅适用于开发人员预览版。</span><span class="sxs-lookup"><span data-stu-id="a829f-313">This capability is currently available in developer preview only.</span></span>
> * <span data-ttu-id="a829f-314">若要使用此功能，应用必须支持会议内侧窗格。</span><span class="sxs-lookup"><span data-stu-id="a829f-314">To use this feature, the app must support an in-meeting sidepanel.</span></span>


<span data-ttu-id="a829f-315">此功能使开发人员能够将应用共享到会议阶段。</span><span class="sxs-lookup"><span data-stu-id="a829f-315">This capability gives developers the ability to share an app to the meeting stage.</span></span> <span data-ttu-id="a829f-316">通过启用共享到会议阶段，会议参与者可以实时协作。</span><span class="sxs-lookup"><span data-stu-id="a829f-316">By enabling share to the meeting stage, meeting participants can collaborate in real-time.</span></span> 

<span data-ttu-id="a829f-317">必需的上下文 `meetingStage` 位于应用程序清单中。</span><span class="sxs-lookup"><span data-stu-id="a829f-317">The required context is `meetingStage` in the app manifest.</span></span> <span data-ttu-id="a829f-318">这样做的先决条件是拥有 `meetingSidePanel` 上下文。</span><span class="sxs-lookup"><span data-stu-id="a829f-318">A prerequisite for this is to have the `meetingSidePanel` context.</span></span> <span data-ttu-id="a829f-319">这将启用 **侧窗格** 的"共享"按钮，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="a829f-319">This enables the **Share** button in the sidepanel as depecited in the following image:</span></span>

  ![share_to_stage_during_meeting体验](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

<span data-ttu-id="a829f-321">启用此功能所需的清单更改如下所示：</span><span class="sxs-lookup"><span data-stu-id="a829f-321">The manifest change that is needed to enable this capability is as follows:</span></span> 

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "groupchat"
      ],
      "context":[
        
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```



### <a name="after-a-meeting"></a><span data-ttu-id="a829f-322">会议后</span><span class="sxs-lookup"><span data-stu-id="a829f-322">After a meeting</span></span>

<span data-ttu-id="a829f-323">会议后和会议前配置是等效的。</span><span class="sxs-lookup"><span data-stu-id="a829f-323">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="code-sample"></a><span data-ttu-id="a829f-324">代码示例</span><span class="sxs-lookup"><span data-stu-id="a829f-324">Code sample</span></span>

|<span data-ttu-id="a829f-325">示例名称</span><span class="sxs-lookup"><span data-stu-id="a829f-325">Sample name</span></span> | <span data-ttu-id="a829f-326">描述</span><span class="sxs-lookup"><span data-stu-id="a829f-326">Description</span></span> | <span data-ttu-id="a829f-327">.NET</span><span class="sxs-lookup"><span data-stu-id="a829f-327">.NET</span></span> | <span data-ttu-id="a829f-328">Node.js</span><span class="sxs-lookup"><span data-stu-id="a829f-328">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="a829f-329">会议可扩展性</span><span class="sxs-lookup"><span data-stu-id="a829f-329">Meetings extensibility</span></span> | <span data-ttu-id="a829f-330">Microsoft Teams令牌的会议扩展性示例。</span><span class="sxs-lookup"><span data-stu-id="a829f-330">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="a829f-331">View</span><span class="sxs-lookup"><span data-stu-id="a829f-331">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [<span data-ttu-id="a829f-332">View</span><span class="sxs-lookup"><span data-stu-id="a829f-332">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| <span data-ttu-id="a829f-333">会议内容气泡机器人</span><span class="sxs-lookup"><span data-stu-id="a829f-333">Meeting content bubble bot</span></span> | <span data-ttu-id="a829f-334">Microsoft Teams会议扩展性示例，用于与会议内容气泡机器人进行交互。</span><span class="sxs-lookup"><span data-stu-id="a829f-334">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="a829f-335">View</span><span class="sxs-lookup"><span data-stu-id="a829f-335">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="a829f-336">View</span><span class="sxs-lookup"><span data-stu-id="a829f-336">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| <span data-ttu-id="a829f-337">Meeting SidePanel</span><span class="sxs-lookup"><span data-stu-id="a829f-337">Meeting SidePanel</span></span> | <span data-ttu-id="a829f-338">Microsoft Teams会议扩展性示例，以在会议中通过侧面板进行激活。</span><span class="sxs-lookup"><span data-stu-id="a829f-338">Microsoft Teams meeting extensibility sample for iteracting with the side panel in-meeting.</span></span> | [<span data-ttu-id="a829f-339">View</span><span class="sxs-lookup"><span data-stu-id="a829f-339">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |

## <a name="see-also"></a><span data-ttu-id="a829f-340">另请参阅</span><span class="sxs-lookup"><span data-stu-id="a829f-340">See also</span></span>

* [<span data-ttu-id="a829f-341">会议内对话设计指南</span><span class="sxs-lookup"><span data-stu-id="a829f-341">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="a829f-342">Teams选项卡的身份验证流</span><span class="sxs-lookup"><span data-stu-id="a829f-342">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
