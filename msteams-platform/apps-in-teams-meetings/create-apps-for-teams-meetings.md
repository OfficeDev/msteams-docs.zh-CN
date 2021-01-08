---
title: 创建适用于团队会议的应用
author: laujan
description: 为团队会议创建应用
ms.topic: conceptual
ms.author: lajanuar
keywords: teams 应用会议用户参与者角色 api
ms.openlocfilehash: e768c2dc6722d006c89927adfe60e03243a076d0
ms.sourcegitcommit: f0dfae429385ef02f61896ad49172c4803ef6622
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2020
ms.locfileid: "49740869"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="b43af-104">创建适用于 Teams 会议的应用</span><span class="sxs-lookup"><span data-stu-id="b43af-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="b43af-105">先决条件和注意事项</span><span class="sxs-lookup"><span data-stu-id="b43af-105">Prerequisites and considerations</span></span>

1. <span data-ttu-id="b43af-106">会议中的应用需要一些 Teams [应用开发的基本知识](../overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b43af-106">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="b43af-107">会议中的应用可以包括[选项卡](../tabs/what-are-tabs.md)、聊天机器人和消息传递[](../bots/what-are-bots.md)扩展功能，并且[](../messaging-extensions/what-are-messaging-extensions.md)[需要更新](#update-your-app-manifest)Teams 应用清单以指示该应用可用于会议</span><span class="sxs-lookup"><span data-stu-id="b43af-107">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

1. <span data-ttu-id="b43af-108">若要使应用在会议生命周期中作为选项卡运行，它必须支持群聊作用域中的可 [配置选项卡](../resources/schema/manifest-schema.md#configurabletabs)。</span><span class="sxs-lookup"><span data-stu-id="b43af-108">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs).</span></span> <span data-ttu-id="b43af-109">*请参阅*["使用自定义选项卡扩展 Teams 应用"。](../tabs/how-to/add-tab.md)支持范围 `groupchat` 将启用会议前 [和](teams-apps-in-meetings.md#pre-meeting-app-experience)会议 [后聊天中的](teams-apps-in-meetings.md#post-meeting-app-experience)应用。</span><span class="sxs-lookup"><span data-stu-id="b43af-109">*See* [Extend your Teams app with a custom tab](../tabs/how-to/add-tab.md). Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

1. <span data-ttu-id="b43af-110">会议 API URL 参数可能需要 ，并且 tenantId These 作为 Teams 客户端 SDK 和聊天机器人活动的一 `meetingId` `userId` 部分提供。 [](/onedrive/find-your-office-365-tenant-id)</span><span class="sxs-lookup"><span data-stu-id="b43af-110">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="b43af-111">此外，可以使用 Tab SSO 身份验证检索用户 ID 和租户 ID [的可靠信息](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="b43af-111">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

1. <span data-ttu-id="b43af-112">某些会议 API（例如 `GetParticipant` ，将需要自动 [程序注册和自动程序应用 ID）](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) 来生成身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="b43af-112">Some meeting APIs, such as `GetParticipant` will require a [bot registration and bot app ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) to generate auth tokens.</span></span>

1. <span data-ttu-id="b43af-113">作为开发人员，你必须遵循 Teams 会议前和会后方案的常规[Teams](../tabs/design/tabs.md)选项卡设计准则，以及 Teams[](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)会议期间触发的会议内对话的会议对话指南。</span><span class="sxs-lookup"><span data-stu-id="b43af-113">As a developer, you must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios as well as the [in-meeting dialog guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) for in-meeting dialog triggered during a Teams meeting.</span></span>

1. <span data-ttu-id="b43af-114">请注意，若要实时更新应用，应用必须基于会议中的事件活动是最新的。</span><span class="sxs-lookup"><span data-stu-id="b43af-114">Please note that in order for your app to be updated in real-time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="b43af-115">这些事件可以位于会议内对话框内， (整个会议) 和其他图面中的 `bot Id` `Notification Signal API` 完成参数</span><span class="sxs-lookup"><span data-stu-id="b43af-115">These events can be within the in-meeting dialog (refer to completion `bot Id` parameter in `Notification Signal API`) and other surfaces across the meeting lifecycle</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="b43af-116">会议应用 API 参考</span><span class="sxs-lookup"><span data-stu-id="b43af-116">Meeting apps API reference</span></span>

|<span data-ttu-id="b43af-117">API</span><span class="sxs-lookup"><span data-stu-id="b43af-117">API</span></span>|<span data-ttu-id="b43af-118">说明</span><span class="sxs-lookup"><span data-stu-id="b43af-118">Description</span></span>|<span data-ttu-id="b43af-119">请求</span><span class="sxs-lookup"><span data-stu-id="b43af-119">Request</span></span>|<span data-ttu-id="b43af-120">Source</span><span class="sxs-lookup"><span data-stu-id="b43af-120">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="b43af-121">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="b43af-121">**GetUserContext**</span></span>| <span data-ttu-id="b43af-122">获取上下文信息以在 Teams 选项卡中显示相关内容。</span><span class="sxs-lookup"><span data-stu-id="b43af-122">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="b43af-123">_**microsoftTeams.getContext ( ( ) => { /*...*/ } )**_</span><span class="sxs-lookup"><span data-stu-id="b43af-123">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="b43af-124">Microsoft Teams 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="b43af-124">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="b43af-125">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="b43af-125">**GetParticipant**</span></span>|<span data-ttu-id="b43af-126">此 API 允许机器人通过会议 ID 和参与者 ID 获取参与者信息。</span><span class="sxs-lookup"><span data-stu-id="b43af-126">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="b43af-127">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}？tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="b43af-127">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="b43af-128">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="b43af-128">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="b43af-129">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="b43af-129">**NotificationSignal**</span></span> |<span data-ttu-id="b43af-130">会议信号将采用以下现有对话通知 API (用于用户聊天聊天) 。</span><span class="sxs-lookup"><span data-stu-id="b43af-130">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="b43af-131">此 API 允许开发人员根据最终用户操作发出信号，以显示会议内对话气泡。</span><span class="sxs-lookup"><span data-stu-id="b43af-131">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="b43af-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="b43af-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="b43af-133">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="b43af-133">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="b43af-134">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="b43af-134">GetUserContext</span></span>

<span data-ttu-id="b43af-135">请参阅 Teams 选项卡 [文档的"](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) 获取上下文"，获取有关标识和检索选项卡内容的上下文信息的指南。</span><span class="sxs-lookup"><span data-stu-id="b43af-135">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="b43af-136">作为会议扩展的一部分，为响应有效负载添加了一个新值：</span><span class="sxs-lookup"><span data-stu-id="b43af-136">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="b43af-137">✔ **meetingId**： 在会议上下文中运行时由选项卡使用。</span><span class="sxs-lookup"><span data-stu-id="b43af-137">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="b43af-138">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="b43af-138">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="b43af-139">不要缓存参与者角色，因为会议组织者可以在任何时间点更改角色。</span><span class="sxs-lookup"><span data-stu-id="b43af-139">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="b43af-140">Teams 当前不支持 API 参与者超过 350 人的大型通讯组列表或名单 `GetParticipant` 大小。</span><span class="sxs-lookup"><span data-stu-id="b43af-140">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="b43af-141">查询参数</span><span class="sxs-lookup"><span data-stu-id="b43af-141">Query parameters</span></span>

|<span data-ttu-id="b43af-142">值</span><span class="sxs-lookup"><span data-stu-id="b43af-142">Value</span></span>|<span data-ttu-id="b43af-143">类型</span><span class="sxs-lookup"><span data-stu-id="b43af-143">Type</span></span>|<span data-ttu-id="b43af-144">必需</span><span class="sxs-lookup"><span data-stu-id="b43af-144">Required</span></span>|<span data-ttu-id="b43af-145">说明</span><span class="sxs-lookup"><span data-stu-id="b43af-145">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="b43af-146">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="b43af-146">**meetingId**</span></span>| <span data-ttu-id="b43af-147">string</span><span class="sxs-lookup"><span data-stu-id="b43af-147">string</span></span> | <span data-ttu-id="b43af-148">是</span><span class="sxs-lookup"><span data-stu-id="b43af-148">Yes</span></span> | <span data-ttu-id="b43af-149">会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。</span><span class="sxs-lookup"><span data-stu-id="b43af-149">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="b43af-150">**participantId**</span><span class="sxs-lookup"><span data-stu-id="b43af-150">**participantId**</span></span>| <span data-ttu-id="b43af-151">string</span><span class="sxs-lookup"><span data-stu-id="b43af-151">string</span></span> | <span data-ttu-id="b43af-152">是</span><span class="sxs-lookup"><span data-stu-id="b43af-152">Yes</span></span> | <span data-ttu-id="b43af-153">participantId 是用户 ID。</span><span class="sxs-lookup"><span data-stu-id="b43af-153">The participantId is the user ID.</span></span> <span data-ttu-id="b43af-154">它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。</span><span class="sxs-lookup"><span data-stu-id="b43af-154">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="b43af-155">强烈建议从 Tab SSO 获取 participantId。</span><span class="sxs-lookup"><span data-stu-id="b43af-155">It is highly recommended to get a participantId from the Tab SSO.</span></span> |
|<span data-ttu-id="b43af-156">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="b43af-156">**tenantId**</span></span>| <span data-ttu-id="b43af-157">string</span><span class="sxs-lookup"><span data-stu-id="b43af-157">string</span></span> | <span data-ttu-id="b43af-158">是</span><span class="sxs-lookup"><span data-stu-id="b43af-158">Yes</span></span> | <span data-ttu-id="b43af-159">租户用户需要 tenantId。</span><span class="sxs-lookup"><span data-stu-id="b43af-159">The tenantId is required for the tenant users.</span></span> <span data-ttu-id="b43af-160">它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。</span><span class="sxs-lookup"><span data-stu-id="b43af-160">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="b43af-161">强烈建议从 Tab SSO 获取 tenantId。</span><span class="sxs-lookup"><span data-stu-id="b43af-161">It is highly recommended to get a tenantId from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="b43af-162">示例</span><span class="sxs-lookup"><span data-stu-id="b43af-162">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="b43af-163">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b43af-163">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="b43af-164">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b43af-164">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="b43af-165">JSON</span><span class="sxs-lookup"><span data-stu-id="b43af-165">JSON</span></span>](#tab/json)

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="b43af-166">响应正文为：</span><span class="sxs-lookup"><span data-stu-id="b43af-166">The response body is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="b43af-167">响应代码</span><span class="sxs-lookup"><span data-stu-id="b43af-167">Response codes</span></span>

* <span data-ttu-id="b43af-168">**403：** 不允许应用获取参与者信息。</span><span class="sxs-lookup"><span data-stu-id="b43af-168">**403**: The app is not allowed to get participant information.</span></span>  <span data-ttu-id="b43af-169">这是最常见的错误响应，如果未在会议中安装应用，将触发此错误响应。</span><span class="sxs-lookup"><span data-stu-id="b43af-169">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="b43af-170">例如，如果租户管理员禁用应用或在实时网站迁移过程中阻止应用。</span><span class="sxs-lookup"><span data-stu-id="b43af-170">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>
* <span data-ttu-id="b43af-171">**200：** 已成功检索参与者信息。</span><span class="sxs-lookup"><span data-stu-id="b43af-171">**200**: Participant information successfully retrieved.</span></span>
* <span data-ttu-id="b43af-172">**401：** 令牌无效。</span><span class="sxs-lookup"><span data-stu-id="b43af-172">**401**: Invalid token.</span></span>
* <span data-ttu-id="b43af-173">**404：** 找不到参与者。</span><span class="sxs-lookup"><span data-stu-id="b43af-173">**404**: Participant cannot be found.</span></span>
* <span data-ttu-id="b43af-174">**500：** 会议自 (结束以来已到期 60) 或者参与者没有基于其角色的权限。</span><span class="sxs-lookup"><span data-stu-id="b43af-174">**500**: The meeting has either expired (more than 60 days since the meeting ended) or the participant does not have permissions based on their role.</span></span>


<span data-ttu-id="b43af-175">**即将推出**</span><span class="sxs-lookup"><span data-stu-id="b43af-175">**Coming Soon**</span></span>

* <span data-ttu-id="b43af-176">**404：** 会议已过期或找不到参与者。</span><span class="sxs-lookup"><span data-stu-id="b43af-176">**404**: The meeting has either expired or participant cannot be found.</span></span>


### <a name="notificationsignal-api"></a><span data-ttu-id="b43af-177">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="b43af-177">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="b43af-178">调用会议内对话框时，相同的内容还将呈现为聊天消息。</span><span class="sxs-lookup"><span data-stu-id="b43af-178">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="b43af-179">查询参数</span><span class="sxs-lookup"><span data-stu-id="b43af-179">Query parameters</span></span>

|<span data-ttu-id="b43af-180">值</span><span class="sxs-lookup"><span data-stu-id="b43af-180">Value</span></span>|<span data-ttu-id="b43af-181">类型</span><span class="sxs-lookup"><span data-stu-id="b43af-181">Type</span></span>|<span data-ttu-id="b43af-182">必需</span><span class="sxs-lookup"><span data-stu-id="b43af-182">Required</span></span>|<span data-ttu-id="b43af-183">说明</span><span class="sxs-lookup"><span data-stu-id="b43af-183">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="b43af-184">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="b43af-184">**conversationId**</span></span>| <span data-ttu-id="b43af-185">string</span><span class="sxs-lookup"><span data-stu-id="b43af-185">string</span></span> | <span data-ttu-id="b43af-186">是</span><span class="sxs-lookup"><span data-stu-id="b43af-186">Yes</span></span> | <span data-ttu-id="b43af-187">对话标识符作为自动程序调用的一部分提供</span><span class="sxs-lookup"><span data-stu-id="b43af-187">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="b43af-188">示例</span><span class="sxs-lookup"><span data-stu-id="b43af-188">Example</span></span>

> [!NOTE]
>
<span data-ttu-id="b43af-189">在 `completionBotId` 请求 `externalResourceUrl` 的有效负载示例中，参数是可选的。</span><span class="sxs-lookup"><span data-stu-id="b43af-189">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="b43af-190">`Bot ID` 在清单中声明，机器人会收到结果对象。</span><span class="sxs-lookup"><span data-stu-id="b43af-190">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="b43af-191">externalResourceUrl 宽度和高度参数必须以像素为单位。</span><span class="sxs-lookup"><span data-stu-id="b43af-191">The externalResourceUrl width and height parameters must be in pixels.</span></span> <span data-ttu-id="b43af-192">请参阅 [设计指南](design/designing-apps-in-meetings.md) 以确保尺寸在允许的限制范围内。</span><span class="sxs-lookup"><span data-stu-id="b43af-192">Refer to the [design guidelines](design/designing-apps-in-meetings.md) to ensure the dimensions are within the allowed limits.</span></span>
> * <span data-ttu-id="b43af-193">URL 是作为会议 `<iframe>` 内对话框中的一个页面加载的页面。</span><span class="sxs-lookup"><span data-stu-id="b43af-193">The URL is the page loaded as an `<iframe>` in the in-meeting dialog.</span></span> <span data-ttu-id="b43af-194">域必须在你的应用清单 `validDomains` 中的应用数组中。</span><span class="sxs-lookup"><span data-stu-id="b43af-194">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="b43af-195">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="b43af-195">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="b43af-196">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b43af-196">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="b43af-197">JSON</span><span class="sxs-lookup"><span data-stu-id="b43af-197">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="b43af-198">响应代码</span><span class="sxs-lookup"><span data-stu-id="b43af-198">Response Codes</span></span>

* <span data-ttu-id="b43af-199">**201：** 具有信号的活动已成功发送</span><span class="sxs-lookup"><span data-stu-id="b43af-199">**201**: activity with signal is successfully sent</span></span>  
* <span data-ttu-id="b43af-200">**401**： 无效令牌</span><span class="sxs-lookup"><span data-stu-id="b43af-200">**401**: invalid token</span></span>  
* <span data-ttu-id="b43af-201">**201：** 已成功发送具有信号的活动。</span><span class="sxs-lookup"><span data-stu-id="b43af-201">**201**: Activity with signal is successfully sent.</span></span> 
* <span data-ttu-id="b43af-202">**401：** 令牌无效。</span><span class="sxs-lookup"><span data-stu-id="b43af-202">**401**: Invalid token.</span></span>
* <span data-ttu-id="b43af-203">**403：** 应用无法发送信号。</span><span class="sxs-lookup"><span data-stu-id="b43af-203">**403**: The app is unable to send the signal.</span></span> <span data-ttu-id="b43af-204">发生这种情况的原因有多种，如租户管理员禁用应用、实时网站迁移期间阻止应用等。</span><span class="sxs-lookup"><span data-stu-id="b43af-204">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="b43af-205">在这种情况下，有效负载包含详细的错误消息。</span><span class="sxs-lookup"><span data-stu-id="b43af-205">In this case, the payload contains a detailed error message.</span></span> 
* <span data-ttu-id="b43af-206">**404：** 会议聊天不存在。</span><span class="sxs-lookup"><span data-stu-id="b43af-206">**404**: Meeting chat doesn't exist.</span></span>
 

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="b43af-207">为 Teams 会议启用应用</span><span class="sxs-lookup"><span data-stu-id="b43af-207">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="b43af-208">更新应用清单</span><span class="sxs-lookup"><span data-stu-id="b43af-208">Update your app manifest</span></span>

<span data-ttu-id="b43af-209">会议应用功能通过 **configurableTabs** 作用域和上下文数组在应用清单  ->  **中** 声明。</span><span class="sxs-lookup"><span data-stu-id="b43af-209">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="b43af-210">*范围* 定义谁 *，上下文* 定义你的应用的可用位置。</span><span class="sxs-lookup"><span data-stu-id="b43af-210">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> <span data-ttu-id="b43af-211">请使用开发者预览版 [清单架构](../resources/schema/manifest-schema-dev-preview.md) 在应用清单中尝试此操作。</span><span class="sxs-lookup"><span data-stu-id="b43af-211">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="b43af-212">Context 属性</span><span class="sxs-lookup"><span data-stu-id="b43af-212">Context property</span></span>

<span data-ttu-id="b43af-213">选项卡 `context` 和 `scopes` 属性协调工作，以允许你确定希望应用显示在何处。</span><span class="sxs-lookup"><span data-stu-id="b43af-213">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="b43af-214">或作用域 `team` 中的 `groupchat` 选项卡可以具有多个上下文。</span><span class="sxs-lookup"><span data-stu-id="b43af-214">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="b43af-215">上下文属性的可能值如下所示：</span><span class="sxs-lookup"><span data-stu-id="b43af-215">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="b43af-216">**channelTab**：团队频道标题中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="b43af-216">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="b43af-217">**privateChatTab**：一组不在团队或会议上下文中的用户之间的群聊标题中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="b43af-217">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="b43af-218">**meetingChatTab**：计划会议上下文中一组用户之间的群聊标题中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="b43af-218">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="b43af-219">**meetingDetailsTab**：日历的会议详细信息视图标题中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="b43af-219">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="b43af-220">**meetingSidePanel**：通过统一栏打开的 (u-bar) 。</span><span class="sxs-lookup"><span data-stu-id="b43af-220">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="b43af-221">"Context"属性当前不受支持，因此将在移动客户端上被忽略</span><span class="sxs-lookup"><span data-stu-id="b43af-221">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="b43af-222">为会议方案配置应用</span><span class="sxs-lookup"><span data-stu-id="b43af-222">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="b43af-223">若要使应用在选项卡库中可见，它需要支持可 **配置的选项卡** 和 **群聊范围**。</span><span class="sxs-lookup"><span data-stu-id="b43af-223">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>
>
> * <span data-ttu-id="b43af-224">移动客户端仅在会议前和会议后支持选项卡。</span><span class="sxs-lookup"><span data-stu-id="b43af-224">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="b43af-225">即将在移动设备上 (会议内对话框和选项卡) 体验。</span><span class="sxs-lookup"><span data-stu-id="b43af-225">The in-meeting experiences (in-meeting dialog and tab) on mobile will be available soon.</span></span> <span data-ttu-id="b43af-226">在创建 [适用于移动的选项卡时](../tabs/design/tabs-mobile.md) ，请遵循移动选项卡指南。</span><span class="sxs-lookup"><span data-stu-id="b43af-226">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="b43af-227">会议之前</span><span class="sxs-lookup"><span data-stu-id="b43af-227">Before a meeting</span></span>

<span data-ttu-id="b43af-228">具有组织者和/或演示者角色的用户使用会议聊天和会议详细信息页面中的"➕"按钮将选项卡 **添加到会议**。 </span><span class="sxs-lookup"><span data-stu-id="b43af-228">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="b43af-229">消息扩展通过省略号/溢出菜单添加到 &#x25CF;&#x25CF;&#x25CF; 位于聊天的撰写消息区域下。</span><span class="sxs-lookup"><span data-stu-id="b43af-229">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="b43af-230">聊天机器人会使用""键并选择"获取机器人"添加到 **@** **会议聊天中**。</span><span class="sxs-lookup"><span data-stu-id="b43af-230">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="b43af-231">✔用户标识 *必须通过* 选项卡 [SSO 确认](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="b43af-231">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="b43af-232">在此身份验证后，应用可以通过 GetParticipant API 检索用户角色。</span><span class="sxs-lookup"><span data-stu-id="b43af-232">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="b43af-233">✔基于用户角色，应用现在能够呈现特定于角色的体验。</span><span class="sxs-lookup"><span data-stu-id="b43af-233">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="b43af-234">例如，轮询应用只允许组织者和演示者创建新轮询。</span><span class="sxs-lookup"><span data-stu-id="b43af-234">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="b43af-235">**注意**：可以在会议进行时更改角色分配。</span><span class="sxs-lookup"><span data-stu-id="b43af-235">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="b43af-236">*请参阅* [Teams 会议的角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。</span><span class="sxs-lookup"><span data-stu-id="b43af-236">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="during-a-meeting"></a><span data-ttu-id="b43af-237">会议期间</span><span class="sxs-lookup"><span data-stu-id="b43af-237">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="b43af-238">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="b43af-238">**sidePanel**</span></span>

<span data-ttu-id="b43af-239">✔在应用清单中向上下文数组添加 **sidePanel，** 如上所述。 </span><span class="sxs-lookup"><span data-stu-id="b43af-239">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="b43af-240">✔在会议以及所有方案中，应用程序将在宽度为 320px 的"会议内"选项卡中呈现。</span><span class="sxs-lookup"><span data-stu-id="b43af-240">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="b43af-241">必须针对这一点对选项卡进行优化。</span><span class="sxs-lookup"><span data-stu-id="b43af-241">Your tab must be optimized for this.</span></span> <span data-ttu-id="b43af-242">*请参阅* [，FrameContext 接口](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="b43af-242">*See*, [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span></span>

<span data-ttu-id="b43af-243">✔ Teams [SDK，](../tabs/how-to/access-teams-context.md#user-context) 以使用 **userContext** API 相应地路由请求。</span><span class="sxs-lookup"><span data-stu-id="b43af-243">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="b43af-244">✔选项卡 [的 Teams 身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="b43af-244">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="b43af-245">选项卡的身份验证流与网站的身份验证流非常相似。</span><span class="sxs-lookup"><span data-stu-id="b43af-245">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="b43af-246">因此，选项卡可以直接使用 OAuth 2.0。</span><span class="sxs-lookup"><span data-stu-id="b43af-246">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="b43af-247">*另请参阅* [，Microsoft 标识平台和 OAuth 2.0 授权代码流](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。</span><span class="sxs-lookup"><span data-stu-id="b43af-247">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="b43af-248">✔用户位于会议视图中时，邮件扩展应按预期工作，并且应该能够发布撰写邮件扩展卡。</span><span class="sxs-lookup"><span data-stu-id="b43af-248">✔ Message extension should work as expected when a user is in an in-meeting view and should be able to post compose message extension cards.</span></span>

<span data-ttu-id="b43af-249">✔ AppName- 工具提示应说明会议 U 栏中的应用名称。</span><span class="sxs-lookup"><span data-stu-id="b43af-249">✔ AppName in-meeting - Tooltip should state the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="b43af-250">**会议内的对话框**</span><span class="sxs-lookup"><span data-stu-id="b43af-250">**In-meeting dialog**</span></span>

<span data-ttu-id="b43af-251">✔必须遵守会议 [内对话框设计准则](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。</span><span class="sxs-lookup"><span data-stu-id="b43af-251">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

<span data-ttu-id="b43af-252">✔选项卡 [的 Teams 身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="b43af-252">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="b43af-253">✔ 使用 [通知](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API 发出需要触发气泡通知的信号。</span><span class="sxs-lookup"><span data-stu-id="b43af-253">✔ Use the [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="b43af-254">✔作为通知请求有效负载的一部分，请包含要展示内容的托管 URL。</span><span class="sxs-lookup"><span data-stu-id="b43af-254">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

<span data-ttu-id="b43af-255">✔会议内对话框不得使用任务模块。</span><span class="sxs-lookup"><span data-stu-id="b43af-255">✔ In-meeting dialog must not use task module.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="b43af-256">这些通知本质上是永久性的。</span><span class="sxs-lookup"><span data-stu-id="b43af-256">These notifications are persistent in nature.</span></span> <span data-ttu-id="b43af-257">您必须调用 [**submitTask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 函数，以在用户执行 Web 视图中的操作后自动消除。</span><span class="sxs-lookup"><span data-stu-id="b43af-257">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="b43af-258">这是应用提交的要求。</span><span class="sxs-lookup"><span data-stu-id="b43af-258">This is a requirement for app submission.</span></span> <span data-ttu-id="b43af-259">*另请参阅* [，Teams SDK：任务模块](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="b43af-259">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="b43af-260">如果希望应用支持匿名用户，初始调用请求有效负载必须依赖于对象中的用户) 请求元数据的 (ID，而不是用户请求元数据的 `from.id` `from` (Azure Active `from.aadObjectId` Directory) ID。</span><span class="sxs-lookup"><span data-stu-id="b43af-260">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="b43af-261">*请参阅*[使用选项卡中的任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md)[以及创建和发送任务模块](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。</span><span class="sxs-lookup"><span data-stu-id="b43af-261">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="after-a-meeting"></a><span data-ttu-id="b43af-262">会议后</span><span class="sxs-lookup"><span data-stu-id="b43af-262">After a meeting</span></span>

<span data-ttu-id="b43af-263">会后和会前配置是等效的。</span><span class="sxs-lookup"><span data-stu-id="b43af-263">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="b43af-264">会议应用程序示例</span><span class="sxs-lookup"><span data-stu-id="b43af-264">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="b43af-265">会议令牌生成器应用</span><span class="sxs-lookup"><span data-stu-id="b43af-265">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
