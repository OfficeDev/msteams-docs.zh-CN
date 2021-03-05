---
title: 创建适用于团队会议的应用
author: laujan
description: 为团队会议创建应用
ms.topic: conceptual
ms.author: lajanuar
keywords: Teams 应用会议用户参与者角色 api
ms.openlocfilehash: bd0f53ae34a23bdbbdc2e6f3992c7dd0836e9f28
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449491"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="02b9a-104">创建适用于 Teams 会议的应用</span><span class="sxs-lookup"><span data-stu-id="02b9a-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="02b9a-105">先决条件和注意事项</span><span class="sxs-lookup"><span data-stu-id="02b9a-105">Prerequisites and considerations</span></span>

* <span data-ttu-id="02b9a-106">会议中的应用需要 Teams 应用开发 [方面的一些基本知识](../overview.md)。</span><span class="sxs-lookup"><span data-stu-id="02b9a-106">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="02b9a-107">会议中的应用可以包括[选项卡](../tabs/what-are-tabs.md)、聊天机器人和消息传递[](../bots/what-are-bots.md)扩展功能，并且[](../messaging-extensions/what-are-messaging-extensions.md)需要[Teams](#update-your-app-manifest)应用清单更新，以指示该应用可用于会议</span><span class="sxs-lookup"><span data-stu-id="02b9a-107">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

* <span data-ttu-id="02b9a-108">若要使应用在会议生命周期中作为选项卡运行，它必须支持组聊天范围中的可配置[选项卡 (了解如何](../resources/schema/manifest-schema.md#configurabletabs)生成组选项卡) 。 [](../build-your-first-app/build-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="02b9a-108">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) (see how to [build a group tab](../build-your-first-app/build-channel-tab.md)).</span></span> <span data-ttu-id="02b9a-109">支持范围 `groupchat` 将启用会议前 [和](teams-apps-in-meetings.md#pre-meeting-app-experience) 会议 [后聊天中的](teams-apps-in-meetings.md#post-meeting-app-experience) 应用。</span><span class="sxs-lookup"><span data-stu-id="02b9a-109">Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

* <span data-ttu-id="02b9a-110">会议 API URL 参数可能需要 `meetingId` 和 `userId` [tenantId，](/onedrive/find-your-office-365-tenant-id) 这些参数作为 Teams 客户端 SDK 和自动程序活动的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="02b9a-110">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="02b9a-111">此外，可以使用 Tab SSO 身份验证检索用户 ID 和租户 ID [的可靠信息](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="02b9a-111">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="02b9a-112">某些会议 API（例如 `GetParticipant` ，需要自动 [程序注册和 ID）](../build-your-first-app/build-bot.md) 才能生成身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="02b9a-112">Some meeting APIs, such as `GetParticipant`, require a [bot registration and ID](../build-your-first-app/build-bot.md) to generate auth tokens.</span></span>

* <span data-ttu-id="02b9a-113">您必须遵守针对会议前 [和会议后](../tabs/design/tabs.md) 方案的 Teams 选项卡设计一般准则。</span><span class="sxs-lookup"><span data-stu-id="02b9a-113">You must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="02b9a-114">有关会议期间的体验，请参阅会议内 [选项卡](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) 和 [会议内对话框](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) 设计指南。</span><span class="sxs-lookup"><span data-stu-id="02b9a-114">For experiences during meetings, refer to the [in-meeting tab](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) design guidelines.</span></span>

* <span data-ttu-id="02b9a-115">若要实时更新应用，应用必须基于会议中的事件活动是最新的。</span><span class="sxs-lookup"><span data-stu-id="02b9a-115">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="02b9a-116">这些事件可以位于会议对话框内， (在会议生命周期中的) 和其他图面中引用 `bot Id` `Notification Signal API` 完成参数</span><span class="sxs-lookup"><span data-stu-id="02b9a-116">These events can be within the in-meeting dialog (refer to completion `bot Id` parameter in `Notification Signal API`) and other surfaces across the meeting lifecycle</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="02b9a-117">会议应用 API 参考</span><span class="sxs-lookup"><span data-stu-id="02b9a-117">Meeting apps API reference</span></span>

|<span data-ttu-id="02b9a-118">API</span><span class="sxs-lookup"><span data-stu-id="02b9a-118">API</span></span>|<span data-ttu-id="02b9a-119">说明</span><span class="sxs-lookup"><span data-stu-id="02b9a-119">Description</span></span>|<span data-ttu-id="02b9a-120">请求</span><span class="sxs-lookup"><span data-stu-id="02b9a-120">Request</span></span>|<span data-ttu-id="02b9a-121">源</span><span class="sxs-lookup"><span data-stu-id="02b9a-121">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="02b9a-122">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="02b9a-122">**GetUserContext**</span></span>| <span data-ttu-id="02b9a-123">获取上下文信息以在 Teams 选项卡中显示相关内容。</span><span class="sxs-lookup"><span data-stu-id="02b9a-123">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="02b9a-124">_**microsoftTeams.getContext ( ( ) => { /*...*/ } )**_</span><span class="sxs-lookup"><span data-stu-id="02b9a-124">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="02b9a-125">Microsoft Teams 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="02b9a-125">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="02b9a-126">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="02b9a-126">**GetParticipant**</span></span>|<span data-ttu-id="02b9a-127">此 API 允许机器人通过会议 ID 和参与者 ID 获取参与者信息。</span><span class="sxs-lookup"><span data-stu-id="02b9a-127">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="02b9a-128">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}？tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="02b9a-128">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="02b9a-129">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="02b9a-129">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="02b9a-130">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="02b9a-130">**NotificationSignal**</span></span> |<span data-ttu-id="02b9a-131">会议信号将采用以下现有对话通知 API (用于用户聊天聊天) 。</span><span class="sxs-lookup"><span data-stu-id="02b9a-131">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="02b9a-132">此 API 允许开发人员根据最终用户操作发出信号，以显示会议内对话气泡。</span><span class="sxs-lookup"><span data-stu-id="02b9a-132">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="02b9a-133">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="02b9a-133">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="02b9a-134">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="02b9a-134">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="02b9a-135">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="02b9a-135">GetUserContext</span></span>

<span data-ttu-id="02b9a-136">请参阅 Teams 选项卡 [文档的"](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) 获取上下文"，获取有关标识和检索选项卡内容的上下文信息的指南。</span><span class="sxs-lookup"><span data-stu-id="02b9a-136">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="02b9a-137">作为会议可扩展性的一部分，为响应有效负载添加了一个新值：</span><span class="sxs-lookup"><span data-stu-id="02b9a-137">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="02b9a-138">✔ **meetingId**： 在会议上下文中运行时由选项卡使用。</span><span class="sxs-lookup"><span data-stu-id="02b9a-138">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="02b9a-139">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="02b9a-139">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="02b9a-140">不要缓存参与者角色，因为会议组织者可以随时更改角色。</span><span class="sxs-lookup"><span data-stu-id="02b9a-140">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="02b9a-141">Teams 当前不支持 API 参与者超过 350 人的大型通讯组列表或名单 `GetParticipant` 。</span><span class="sxs-lookup"><span data-stu-id="02b9a-141">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="02b9a-142">查询参数</span><span class="sxs-lookup"><span data-stu-id="02b9a-142">Query parameters</span></span>

|<span data-ttu-id="02b9a-143">值</span><span class="sxs-lookup"><span data-stu-id="02b9a-143">Value</span></span>|<span data-ttu-id="02b9a-144">类型</span><span class="sxs-lookup"><span data-stu-id="02b9a-144">Type</span></span>|<span data-ttu-id="02b9a-145">必需</span><span class="sxs-lookup"><span data-stu-id="02b9a-145">Required</span></span>|<span data-ttu-id="02b9a-146">说明</span><span class="sxs-lookup"><span data-stu-id="02b9a-146">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="02b9a-147">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="02b9a-147">**meetingId**</span></span>| <span data-ttu-id="02b9a-148">string</span><span class="sxs-lookup"><span data-stu-id="02b9a-148">string</span></span> | <span data-ttu-id="02b9a-149">是</span><span class="sxs-lookup"><span data-stu-id="02b9a-149">Yes</span></span> | <span data-ttu-id="02b9a-150">会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。</span><span class="sxs-lookup"><span data-stu-id="02b9a-150">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="02b9a-151">**participantId**</span><span class="sxs-lookup"><span data-stu-id="02b9a-151">**participantId**</span></span>| <span data-ttu-id="02b9a-152">string</span><span class="sxs-lookup"><span data-stu-id="02b9a-152">string</span></span> | <span data-ttu-id="02b9a-153">是</span><span class="sxs-lookup"><span data-stu-id="02b9a-153">Yes</span></span> | <span data-ttu-id="02b9a-154">participantId 是用户 ID。</span><span class="sxs-lookup"><span data-stu-id="02b9a-154">The participantId is the user ID.</span></span> <span data-ttu-id="02b9a-155">它在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中可用。</span><span class="sxs-lookup"><span data-stu-id="02b9a-155">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="02b9a-156">强烈建议从 Tab SSO 获取 participantId。</span><span class="sxs-lookup"><span data-stu-id="02b9a-156">It is highly recommended to get a participantId from the Tab SSO.</span></span> |
|<span data-ttu-id="02b9a-157">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="02b9a-157">**tenantId**</span></span>| <span data-ttu-id="02b9a-158">string</span><span class="sxs-lookup"><span data-stu-id="02b9a-158">string</span></span> | <span data-ttu-id="02b9a-159">是</span><span class="sxs-lookup"><span data-stu-id="02b9a-159">Yes</span></span> | <span data-ttu-id="02b9a-160">租户用户需要 tenantId。</span><span class="sxs-lookup"><span data-stu-id="02b9a-160">The tenantId is required for the tenant users.</span></span> <span data-ttu-id="02b9a-161">它在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中可用。</span><span class="sxs-lookup"><span data-stu-id="02b9a-161">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="02b9a-162">强烈建议从 Tab SSO 获取 tenantId。</span><span class="sxs-lookup"><span data-stu-id="02b9a-162">It is highly recommended to get a tenantId from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="02b9a-163">示例</span><span class="sxs-lookup"><span data-stu-id="02b9a-163">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="02b9a-164">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="02b9a-164">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="02b9a-165">JavaScript</span><span class="sxs-lookup"><span data-stu-id="02b9a-165">JavaScript</span></span>](#tab/javascript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
            let member = participant.user;
            let meetingInfo = participant.meeting;
            let conversation = participant.conversation;
            
            await context.sendActivity(`The participant role is: '${meetingInfo.role}'`);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="02b9a-166">JSON</span><span class="sxs-lookup"><span data-stu-id="02b9a-166">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="02b9a-167">响应正文为：</span><span class="sxs-lookup"><span data-stu-id="02b9a-167">The response body is:</span></span>

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

* * *

#### <a name="response-codes"></a><span data-ttu-id="02b9a-168">响应代码</span><span class="sxs-lookup"><span data-stu-id="02b9a-168">Response codes</span></span>

* <span data-ttu-id="02b9a-169">**403：** 不允许应用获取参与者信息。</span><span class="sxs-lookup"><span data-stu-id="02b9a-169">**403**: The app is not allowed to get participant information.</span></span> <span data-ttu-id="02b9a-170">这是最常见的错误响应，如果未在会议中安装应用，将触发此错误响应。</span><span class="sxs-lookup"><span data-stu-id="02b9a-170">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="02b9a-171">例如，如果租户管理员禁用应用或在网站缓解期间阻止应用。</span><span class="sxs-lookup"><span data-stu-id="02b9a-171">For example, if the app is disabled by tenant admin or blocked during livesite mitigation.</span></span>
* <span data-ttu-id="02b9a-172">**200：** 已成功检索参与者信息。</span><span class="sxs-lookup"><span data-stu-id="02b9a-172">**200**: Participant information successfully retrieved.</span></span>
* <span data-ttu-id="02b9a-173">**401：** 令牌无效。</span><span class="sxs-lookup"><span data-stu-id="02b9a-173">**401**: Invalid token.</span></span>
* <span data-ttu-id="02b9a-174">**404：** 找不到参与者。</span><span class="sxs-lookup"><span data-stu-id="02b9a-174">**404**: Participant cannot be found.</span></span>
* <span data-ttu-id="02b9a-175">**500：** 会议自 (结束以来超过 60 天) 或者参与者没有基于其角色的权限。</span><span class="sxs-lookup"><span data-stu-id="02b9a-175">**500**: The meeting has either expired (more than 60 days since the meeting ended) or the participant does not have permissions based on their role.</span></span>


<span data-ttu-id="02b9a-176">**即将推出**</span><span class="sxs-lookup"><span data-stu-id="02b9a-176">**Coming Soon**</span></span>

* <span data-ttu-id="02b9a-177">**404：** 会议已过期或找不到参与者。</span><span class="sxs-lookup"><span data-stu-id="02b9a-177">**404**: The meeting has either expired or participant cannot be found.</span></span>


### <a name="notificationsignal-api"></a><span data-ttu-id="02b9a-178">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="02b9a-178">NotificationSignal API</span></span>

<span data-ttu-id="02b9a-179">会议中的所有用户都接收通过 NotificationSignal API 发送的通知。</span><span class="sxs-lookup"><span data-stu-id="02b9a-179">All users in a meeting receive the notifications sent through the NotificationSignal API.</span></span>

> [!NOTE]
> <span data-ttu-id="02b9a-180">目前，不支持发送定向通知。</span><span class="sxs-lookup"><span data-stu-id="02b9a-180">Currently, sending targetted notifications is not supported.</span></span>
> <span data-ttu-id="02b9a-181">调用会议内对话框时，相同的内容还将呈现为聊天消息。</span><span class="sxs-lookup"><span data-stu-id="02b9a-181">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="02b9a-182">查询参数</span><span class="sxs-lookup"><span data-stu-id="02b9a-182">Query parameters</span></span>

|<span data-ttu-id="02b9a-183">值</span><span class="sxs-lookup"><span data-stu-id="02b9a-183">Value</span></span>|<span data-ttu-id="02b9a-184">类型</span><span class="sxs-lookup"><span data-stu-id="02b9a-184">Type</span></span>|<span data-ttu-id="02b9a-185">必需</span><span class="sxs-lookup"><span data-stu-id="02b9a-185">Required</span></span>|<span data-ttu-id="02b9a-186">说明</span><span class="sxs-lookup"><span data-stu-id="02b9a-186">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="02b9a-187">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="02b9a-187">**conversationId**</span></span>| <span data-ttu-id="02b9a-188">string</span><span class="sxs-lookup"><span data-stu-id="02b9a-188">string</span></span> | <span data-ttu-id="02b9a-189">是</span><span class="sxs-lookup"><span data-stu-id="02b9a-189">Yes</span></span> | <span data-ttu-id="02b9a-190">对话标识符作为自动程序调用的一部分提供</span><span class="sxs-lookup"><span data-stu-id="02b9a-190">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="02b9a-191">示例</span><span class="sxs-lookup"><span data-stu-id="02b9a-191">Example</span></span>

<span data-ttu-id="02b9a-192">在 `Bot ID` 清单中声明，自动程序接收结果对象。</span><span class="sxs-lookup"><span data-stu-id="02b9a-192">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span> <span data-ttu-id="02b9a-193">在下面的示例中，所请求的有效负载中的参数 `completionBotId` `externalResourceUrl` 是可选的：</span><span class="sxs-lookup"><span data-stu-id="02b9a-193">In the following example, the `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload:</span></span>

> [!NOTE]
> * <span data-ttu-id="02b9a-194">`externalResourceUrl`宽度和高度参数必须以像素为单位。</span><span class="sxs-lookup"><span data-stu-id="02b9a-194">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="02b9a-195">若要确保尺寸在允许的限制内，请参阅 [设计指南](design/designing-apps-in-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="02b9a-195">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="02b9a-196">URL 是在会议对话框中作为 `<iframe>` 页面加载的页面。</span><span class="sxs-lookup"><span data-stu-id="02b9a-196">The URL is the page loaded as an `<iframe>` in the in-meeting dialog.</span></span> <span data-ttu-id="02b9a-197">域必须在你的应用清单 `validDomains` 中的应用数组中。</span><span class="sxs-lookup"><span data-stu-id="02b9a-197">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="02b9a-198">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="02b9a-198">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="02b9a-199">JavaScript</span><span class="sxs-lookup"><span data-stu-id="02b9a-199">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="02b9a-200">JSON</span><span class="sxs-lookup"><span data-stu-id="02b9a-200">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="02b9a-201">响应代码</span><span class="sxs-lookup"><span data-stu-id="02b9a-201">Response Codes</span></span>

* <span data-ttu-id="02b9a-202">**201：** 已成功发送具有信号的活动。</span><span class="sxs-lookup"><span data-stu-id="02b9a-202">**201**: Activity with signal is successfully sent.</span></span> 
* <span data-ttu-id="02b9a-203">**401：** 令牌无效。</span><span class="sxs-lookup"><span data-stu-id="02b9a-203">**401**: Invalid token.</span></span>
* <span data-ttu-id="02b9a-204">**403：** 应用无法发送信号。</span><span class="sxs-lookup"><span data-stu-id="02b9a-204">**403**: The app is unable to send the signal.</span></span> <span data-ttu-id="02b9a-205">由于各种原因（如租户管理员禁用应用、应用在实时网站迁移期间被阻止等）可能会发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="02b9a-205">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="02b9a-206">在这种情况下，有效负载包含详细的错误消息。</span><span class="sxs-lookup"><span data-stu-id="02b9a-206">In this case, the payload contains a detailed error message.</span></span> 
* <span data-ttu-id="02b9a-207">**404：** 会议聊天不存在。</span><span class="sxs-lookup"><span data-stu-id="02b9a-207">**404**: Meeting chat does not exist.</span></span>
 

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="02b9a-208">为 Teams 会议启用应用</span><span class="sxs-lookup"><span data-stu-id="02b9a-208">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="02b9a-209">更新应用清单</span><span class="sxs-lookup"><span data-stu-id="02b9a-209">Update your app manifest</span></span>

<span data-ttu-id="02b9a-210">会议应用功能通过 **configurableTabs** 作用域和上下文数组在应用清单  ->  **中** 声明。</span><span class="sxs-lookup"><span data-stu-id="02b9a-210">The meetings app capabilities are declared in your app manifest through the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="02b9a-211">*范围* 定义谁， *上下文* 定义你的应用的可用位置。</span><span class="sxs-lookup"><span data-stu-id="02b9a-211">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> <span data-ttu-id="02b9a-212">请使用 [开发者预览版清单架构](../resources/schema/manifest-schema-dev-preview.md) 在应用清单中尝试此操作。</span><span class="sxs-lookup"><span data-stu-id="02b9a-212">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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
        "meetingSidePanel"
     ]
    }
  ]
```

### <a name="context-property"></a><span data-ttu-id="02b9a-213">Context 属性</span><span class="sxs-lookup"><span data-stu-id="02b9a-213">Context property</span></span>

<span data-ttu-id="02b9a-214">选项卡 `context` 和 `scopes` 属性协调工作，允许你确定希望应用显示在何处。</span><span class="sxs-lookup"><span data-stu-id="02b9a-214">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="02b9a-215">或作用域 `team` 中的 `groupchat` 选项卡可以具有多个上下文。</span><span class="sxs-lookup"><span data-stu-id="02b9a-215">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="02b9a-216">上下文属性的可能值如下所示：</span><span class="sxs-lookup"><span data-stu-id="02b9a-216">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="02b9a-217">**channelTab**：团队频道标题中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="02b9a-217">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="02b9a-218">**privateChatTab**：不在团队或会议上下文中的一组用户之间的群聊标题中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="02b9a-218">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="02b9a-219">**meetingChatTab**：计划会议上下文中一组用户之间的群聊标题中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="02b9a-219">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="02b9a-220">**meetingDetailsTab：** 日历的会议详细信息视图标题中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="02b9a-220">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="02b9a-221">**meetingSidePanel：** 通过统一栏打开的 (u 栏) 。</span><span class="sxs-lookup"><span data-stu-id="02b9a-221">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="02b9a-222">"Context"属性当前不受支持，因此将在移动客户端上被忽略</span><span class="sxs-lookup"><span data-stu-id="02b9a-222">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="02b9a-223">为会议方案配置应用</span><span class="sxs-lookup"><span data-stu-id="02b9a-223">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="02b9a-224">若要使应用在选项卡库中可见，需要支持可 **配置的选项卡** 和 **群聊范围**。</span><span class="sxs-lookup"><span data-stu-id="02b9a-224">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>
>
> * <span data-ttu-id="02b9a-225">移动客户端仅支持会议前和会议后 Surface 中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="02b9a-225">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="02b9a-226">即将在移动设备上 (会议内对话框和选项卡) 体验。</span><span class="sxs-lookup"><span data-stu-id="02b9a-226">The in-meeting experiences (in-meeting dialog and tab) on mobile will be available soon.</span></span> <span data-ttu-id="02b9a-227">在创建 [适用于移动设备的选项卡时](../tabs/design/tabs-mobile.md) ，请遵循移动选项卡指南。</span><span class="sxs-lookup"><span data-stu-id="02b9a-227">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="02b9a-228">在会议之前</span><span class="sxs-lookup"><span data-stu-id="02b9a-228">Before a meeting</span></span>

<span data-ttu-id="02b9a-229">具有组织者和/或演示者角色的用户使用会议聊天和会议详细信息➕中的加号 **按钮将选项卡\*\*\*\*添加到会议。**</span><span class="sxs-lookup"><span data-stu-id="02b9a-229">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="02b9a-230">消息扩展通过位于聊天中的撰写消息 &#x25CF;&#x25CF;&#x25CF; 下的省略号/溢出菜单添加到。</span><span class="sxs-lookup"><span data-stu-id="02b9a-230">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="02b9a-231">使用""键并选择"获取机器人"将聊天机器人添加到 **@** **会议聊天** 中。</span><span class="sxs-lookup"><span data-stu-id="02b9a-231">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="02b9a-232">✔必须通过选项卡 SSO确认[用户标识](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="02b9a-232">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="02b9a-233">在此身份验证后，应用可以通过 GetParticipant API 检索用户角色。</span><span class="sxs-lookup"><span data-stu-id="02b9a-233">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="02b9a-234">✔基于用户角色，应用现在能够呈现角色特定体验。</span><span class="sxs-lookup"><span data-stu-id="02b9a-234">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="02b9a-235">例如，轮询应用只允许组织者和演示者创建新轮询。</span><span class="sxs-lookup"><span data-stu-id="02b9a-235">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="02b9a-236">**注意**：可以在会议进行时更改角色分配。</span><span class="sxs-lookup"><span data-stu-id="02b9a-236">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="02b9a-237">*请参阅* [Teams 会议的角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。</span><span class="sxs-lookup"><span data-stu-id="02b9a-237">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="during-a-meeting"></a><span data-ttu-id="02b9a-238">会议期间</span><span class="sxs-lookup"><span data-stu-id="02b9a-238">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="02b9a-239">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="02b9a-239">**sidePanel**</span></span>

<span data-ttu-id="02b9a-240">✔在应用清单中向上下文数组添加 **sidePanel，** 如上所述。 </span><span class="sxs-lookup"><span data-stu-id="02b9a-240">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="02b9a-241">✔会议以及所有方案中，应用程序将在宽度为 320px 的会议内选项卡中呈现。</span><span class="sxs-lookup"><span data-stu-id="02b9a-241">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="02b9a-242">您的选项卡必须针对这一点进行优化。</span><span class="sxs-lookup"><span data-stu-id="02b9a-242">Your tab must be optimized for this.</span></span> <span data-ttu-id="02b9a-243">*请参阅* [，FrameContext 接口](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="02b9a-243">*See*, [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span></span>

<span data-ttu-id="02b9a-244">✔ Teams [SDK，](../tabs/how-to/access-teams-context.md#user-context) 以使用 **userContext** API 相应地路由请求。</span><span class="sxs-lookup"><span data-stu-id="02b9a-244">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="02b9a-245">✔选项卡 [的 Teams 身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="02b9a-245">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="02b9a-246">选项卡的身份验证流与网站的身份验证流非常相似。</span><span class="sxs-lookup"><span data-stu-id="02b9a-246">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="02b9a-247">因此，选项卡可以直接使用 OAuth 2.0。</span><span class="sxs-lookup"><span data-stu-id="02b9a-247">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="02b9a-248">*另请参阅* [，Microsoft 标识平台和 OAuth 2.0 授权代码流](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。</span><span class="sxs-lookup"><span data-stu-id="02b9a-248">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="02b9a-249">✔用户位于会议视图中时，邮件扩展应按预期工作，并且应该能够发布撰写邮件扩展卡。</span><span class="sxs-lookup"><span data-stu-id="02b9a-249">✔ Message extension should work as expected when a user is in an in-meeting view and should be able to post compose message extension cards.</span></span>

<span data-ttu-id="02b9a-250">✔ AppName- 工具提示应指出会议 U 栏中的应用名称。</span><span class="sxs-lookup"><span data-stu-id="02b9a-250">✔ AppName in-meeting - Tooltip should state the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="02b9a-251">**会议内的对话框**</span><span class="sxs-lookup"><span data-stu-id="02b9a-251">**In-meeting dialog**</span></span>

<span data-ttu-id="02b9a-252">✔必须遵守会议 [对话设计准则](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。</span><span class="sxs-lookup"><span data-stu-id="02b9a-252">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

<span data-ttu-id="02b9a-253">✔选项卡 [的 Teams 身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="02b9a-253">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="02b9a-254">✔ [使用 NotificationSignal API](create-apps-for-teams-meetings.md#notificationsignal-api) 发出需要触发气泡通知的信号。</span><span class="sxs-lookup"><span data-stu-id="02b9a-254">✔ Use the [NotificationSignal API](create-apps-for-teams-meetings.md#notificationsignal-api) to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="02b9a-255">✔作为通知请求有效负载的一部分，包括要展示内容的托管 URL。</span><span class="sxs-lookup"><span data-stu-id="02b9a-255">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

<span data-ttu-id="02b9a-256">✔会议对话不得使用任务模块。</span><span class="sxs-lookup"><span data-stu-id="02b9a-256">✔ In-meeting dialog must not use task module.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="02b9a-257">这些通知本质上是永久性的。</span><span class="sxs-lookup"><span data-stu-id="02b9a-257">These notifications are persistent in nature.</span></span> <span data-ttu-id="02b9a-258">您必须调用 [**submitTask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 函数，以在用户执行 Web 视图中的操作后自动消除。</span><span class="sxs-lookup"><span data-stu-id="02b9a-258">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="02b9a-259">这是应用提交的要求。</span><span class="sxs-lookup"><span data-stu-id="02b9a-259">This is a requirement for app submission.</span></span> <span data-ttu-id="02b9a-260">*另请参阅* [，Teams SDK：任务模块](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="02b9a-260">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="02b9a-261">如果希望应用支持匿名用户，初始调用请求有效负载必须依赖于用户) 请求元数据的 () ID，而不是用户请求元数据的 `from.id` `from` (Azure Active `from.aadObjectId` Directory) ID。</span><span class="sxs-lookup"><span data-stu-id="02b9a-261">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="02b9a-262">*请参阅*[使用选项卡中的任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md)[以及创建和发送任务模块](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。</span><span class="sxs-lookup"><span data-stu-id="02b9a-262">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="after-a-meeting"></a><span data-ttu-id="02b9a-263">会议后</span><span class="sxs-lookup"><span data-stu-id="02b9a-263">After a meeting</span></span>

<span data-ttu-id="02b9a-264">会议后和会前配置是等效的。</span><span class="sxs-lookup"><span data-stu-id="02b9a-264">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="02b9a-265">会议应用示例</span><span class="sxs-lookup"><span data-stu-id="02b9a-265">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="02b9a-266">会议令牌生成器应用</span><span class="sxs-lookup"><span data-stu-id="02b9a-266">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
