---
title: Teams 会议中应用的先决条件和 API 参考
author: laujan
description: 使用用于会议Teams应用程序
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams 应用会议用户参与者角色 api
ms.openlocfilehash: f42e827801e21bbd039f52dbb685d4559ae5cf81
ms.sourcegitcommit: 37325179a532897fafbe827dcf9a7ca5fa5e7d0b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2021
ms.locfileid: "52853506"
---
# <a name="prerequisites-and-api-references-for-apps-in-teams-meetings"></a><span data-ttu-id="46ad0-104">Teams 会议中应用的先决条件和 API 参考</span><span class="sxs-lookup"><span data-stu-id="46ad0-104">Prerequisites and API references for apps in Teams meetings</span></span>

<span data-ttu-id="46ad0-105">若要在会议生命周期内扩展应用功能，Teams使用会议Teams应用程序。</span><span class="sxs-lookup"><span data-stu-id="46ad0-105">To expand the capabilities of your apps across the meeting lifecycle, Teams enables you to work with apps for Teams meetings.</span></span> <span data-ttu-id="46ad0-106">必须完成先决条件，并且可以使用会议应用 API 引用来增强会议体验。</span><span class="sxs-lookup"><span data-stu-id="46ad0-106">You must  go through the prerequisites and you can use the meeting apps API references to enhance the meeting experience.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46ad0-107">先决条件</span><span class="sxs-lookup"><span data-stu-id="46ad0-107">Prerequisites</span></span>

<span data-ttu-id="46ad0-108">使用用于会议Teams，您必须了解以下内容：</span><span class="sxs-lookup"><span data-stu-id="46ad0-108">Before you work with apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="46ad0-109">你必须知道如何开发应用Teams知识。</span><span class="sxs-lookup"><span data-stu-id="46ad0-109">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="46ad0-110">有关详细信息，请参阅应用[Teams开发](../overview.md)。</span><span class="sxs-lookup"><span data-stu-id="46ad0-110">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="46ad0-111">必须更新Teams清单，以指示该应用可用于会议。</span><span class="sxs-lookup"><span data-stu-id="46ad0-111">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="46ad0-112">有关详细信息，请参阅 [应用清单](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="46ad0-112">For more information, see [app manifest](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest).</span></span>

* <span data-ttu-id="46ad0-113">您的应用程序必须支持 groupchat 作用域中的可配置选项卡，你的应用必须在会议生命周期中作为选项卡运行。有关详细信息，请参阅 [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="46ad0-113">Your app must support configurable tabs in the groupchat scope, for your app to function in the meeting lifecycle as a tab. For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="46ad0-114">对于会议前和Teams方案，必须遵循常规选项卡设计准则。</span><span class="sxs-lookup"><span data-stu-id="46ad0-114">You must adhere to general Teams tab design guidelines for pre and post-meeting scenarios.</span></span> <span data-ttu-id="46ad0-115">有关会议期间的体验，请参阅会议内选项卡和会议内对话框设计指南。</span><span class="sxs-lookup"><span data-stu-id="46ad0-115">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="46ad0-116">有关详细信息，请参阅Teams[选项卡设计指南](../tabs/design/tabs.md)、会议中的[选项卡](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)设计指南和[会议中的对话框设计指南](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。</span><span class="sxs-lookup"><span data-stu-id="46ad0-116">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab), and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="46ad0-117">必须支持范围才能在会议前和会议后聊天 `groupchat` 中启用应用。</span><span class="sxs-lookup"><span data-stu-id="46ad0-117">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="46ad0-118">通过会议前应用体验，你可以查找和添加会议应用并执行会议前任务。</span><span class="sxs-lookup"><span data-stu-id="46ad0-118">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="46ad0-119">通过会议后应用体验，可以查看会议结果，如投票调查结果或反馈。</span><span class="sxs-lookup"><span data-stu-id="46ad0-119">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="46ad0-120">会议 API URL 参数必须具有 `meetingId` 、 `userId` 和 `tenantId` 。</span><span class="sxs-lookup"><span data-stu-id="46ad0-120">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="46ad0-121">它们作为客户端 SDK 和自动程序Teams的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="46ad0-121">These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="46ad0-122">此外，您可以使用选项卡 SSO 身份验证检索用户 ID 和租户 ID [的可靠信息](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="46ad0-122">In addition, you can retrieve reliable information for user ID and tenant ID using [tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="46ad0-123">`GetParticipant`API 必须具有自动程序注册和 ID，以生成身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="46ad0-123">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="46ad0-124">有关详细信息，请参阅自动[程序注册和 ID。](../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="46ad0-124">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="46ad0-125">若要实时更新应用，应用必须基于会议中的活动活动是最新的。</span><span class="sxs-lookup"><span data-stu-id="46ad0-125">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="46ad0-126">这些事件可以位于会议中的对话框内以及整个会议生命周期的其他阶段。</span><span class="sxs-lookup"><span data-stu-id="46ad0-126">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="46ad0-127">有关会议中的对话框，请参阅 `bot Id` API 中的完成 `NotificationSignal` 参数。</span><span class="sxs-lookup"><span data-stu-id="46ad0-127">For the in-meeting dialog box, see completion `bot Id` parameter in `NotificationSignal` API.</span></span>

<span data-ttu-id="46ad0-128">完成先决条件后，可以使用会议应用 API 引用 、 和 ，以便使用属性访问信息并显示 `GetUserContext` `GetParticipant` `NotificationSignal` 相关内容。</span><span class="sxs-lookup"><span data-stu-id="46ad0-128">After you have gone through the prerequisites, you can use the meeting apps API references `GetUserContext`, `GetParticipant`, and `NotificationSignal` that enable you to access information using attributes and display relevant content.</span></span>

## <a name="meeting-apps-api-references"></a><span data-ttu-id="46ad0-129">会议应用 API 参考</span><span class="sxs-lookup"><span data-stu-id="46ad0-129">Meeting apps API references</span></span>

<span data-ttu-id="46ad0-130">新的会议可扩展性为您提供了可转换会议体验的 API。</span><span class="sxs-lookup"><span data-stu-id="46ad0-130">The new meeting extensibilities provide you with APIs that transform the meeting experience.</span></span> <span data-ttu-id="46ad0-131">借助此新功能，可以在会议生命周期内生成应用或集成现有应用。</span><span class="sxs-lookup"><span data-stu-id="46ad0-131">With this new capability, you can build apps or integrate existing apps within the meeting lifecycle.</span></span> <span data-ttu-id="46ad0-132">可以使用 API 让应用了解会议。</span><span class="sxs-lookup"><span data-stu-id="46ad0-132">You can use the APIs to make your app aware of the meeting.</span></span> <span data-ttu-id="46ad0-133">你可以选择想要用于增强会议体验的 API。</span><span class="sxs-lookup"><span data-stu-id="46ad0-133">You can choose which APIs you want to use to enhance the meeting experience.</span></span>

<span data-ttu-id="46ad0-134">下表提供了这些 API 的列表：</span><span class="sxs-lookup"><span data-stu-id="46ad0-134">The following table provides a list of these APIs:</span></span>

|<span data-ttu-id="46ad0-135">API</span><span class="sxs-lookup"><span data-stu-id="46ad0-135">API</span></span>|<span data-ttu-id="46ad0-136">说明</span><span class="sxs-lookup"><span data-stu-id="46ad0-136">Description</span></span>|<span data-ttu-id="46ad0-137">请求</span><span class="sxs-lookup"><span data-stu-id="46ad0-137">Request</span></span>|<span data-ttu-id="46ad0-138">源</span><span class="sxs-lookup"><span data-stu-id="46ad0-138">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="46ad0-139">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="46ad0-139">**GetUserContext**</span></span>| <span data-ttu-id="46ad0-140">此 API 使你能够获取上下文信息，以在"开始"选项卡中Teams内容。</span><span class="sxs-lookup"><span data-stu-id="46ad0-140">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="46ad0-141">_**microsoftTeams.getContext ( ( ) => { /*...*/ } )**_</span><span class="sxs-lookup"><span data-stu-id="46ad0-141">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="46ad0-142">Microsoft Teams客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="46ad0-142">Microsoft Teams Client SDK</span></span>|
|<span data-ttu-id="46ad0-143">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="46ad0-143">**GetParticipant**</span></span>| <span data-ttu-id="46ad0-144">此 API 允许机器人通过会议 ID 和参与者 ID 获取参与者信息。</span><span class="sxs-lookup"><span data-stu-id="46ad0-144">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="46ad0-145">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}？tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="46ad0-145">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="46ad0-146">Microsoft Bot FrameworkSDK</span><span class="sxs-lookup"><span data-stu-id="46ad0-146">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="46ad0-147">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="46ad0-147">**NotificationSignal**</span></span> | <span data-ttu-id="46ad0-148">此 API 使你能够提供使用用户-机器人聊天的现有对话通知 API 传递的会议信号。</span><span class="sxs-lookup"><span data-stu-id="46ad0-148">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="46ad0-149">它允许您根据显示会议内对话框的用户操作发出信号。</span><span class="sxs-lookup"><span data-stu-id="46ad0-149">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="46ad0-150">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="46ad0-150">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="46ad0-151">Microsoft Bot FrameworkSDK</span><span class="sxs-lookup"><span data-stu-id="46ad0-151">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext-api"></a><span data-ttu-id="46ad0-152">GetUserContext API</span><span class="sxs-lookup"><span data-stu-id="46ad0-152">GetUserContext API</span></span>

<span data-ttu-id="46ad0-153">若要标识和检索选项卡内容的上下文信息，请参阅获取选项卡Teams[上下文](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library)。`meetingId`在会议上下文中运行时选项卡使用，并添加响应有效负载。</span><span class="sxs-lookup"><span data-stu-id="46ad0-153">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="46ad0-154">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="46ad0-154">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="46ad0-155">不要缓存参与者角色，因为会议组织者可以随时更改角色。</span><span class="sxs-lookup"><span data-stu-id="46ad0-155">Do not cache participant roles since the meeting organizer can change the roles any time.</span></span>
> * <span data-ttu-id="46ad0-156">Teams API 当前不支持超过 350 个参与者的大型通讯组列表或名单 `GetParticipant` 大小。</span><span class="sxs-lookup"><span data-stu-id="46ad0-156">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

<span data-ttu-id="46ad0-157">API `GetParticipant` 允许机器人通过会议 ID 和参与者 ID 获取参与者信息。</span><span class="sxs-lookup"><span data-stu-id="46ad0-157">The `GetParticipant` API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> <span data-ttu-id="46ad0-158">API 包括查询参数、示例和响应代码。</span><span class="sxs-lookup"><span data-stu-id="46ad0-158">The API includes query parameters, examples, and response codes.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="46ad0-159">查询参数</span><span class="sxs-lookup"><span data-stu-id="46ad0-159">Query parameters</span></span>

<span data-ttu-id="46ad0-160">`GetParticipant`API 包括以下查询参数：</span><span class="sxs-lookup"><span data-stu-id="46ad0-160">The `GetParticipant` API includes the following query parameters:</span></span>

|<span data-ttu-id="46ad0-161">值</span><span class="sxs-lookup"><span data-stu-id="46ad0-161">Value</span></span>|<span data-ttu-id="46ad0-162">类型</span><span class="sxs-lookup"><span data-stu-id="46ad0-162">Type</span></span>|<span data-ttu-id="46ad0-163">必需</span><span class="sxs-lookup"><span data-stu-id="46ad0-163">Required</span></span>|<span data-ttu-id="46ad0-164">说明</span><span class="sxs-lookup"><span data-stu-id="46ad0-164">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="46ad0-165">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="46ad0-165">**meetingId**</span></span>| <span data-ttu-id="46ad0-166">字符串</span><span class="sxs-lookup"><span data-stu-id="46ad0-166">String</span></span> | <span data-ttu-id="46ad0-167">是</span><span class="sxs-lookup"><span data-stu-id="46ad0-167">Yes</span></span> | <span data-ttu-id="46ad0-168">会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。</span><span class="sxs-lookup"><span data-stu-id="46ad0-168">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="46ad0-169">**participantId**</span><span class="sxs-lookup"><span data-stu-id="46ad0-169">**participantId**</span></span>| <span data-ttu-id="46ad0-170">字符串</span><span class="sxs-lookup"><span data-stu-id="46ad0-170">String</span></span> | <span data-ttu-id="46ad0-171">是</span><span class="sxs-lookup"><span data-stu-id="46ad0-171">Yes</span></span> | <span data-ttu-id="46ad0-172">参与者 ID 是用户 ID。</span><span class="sxs-lookup"><span data-stu-id="46ad0-172">The participant ID is the user ID.</span></span> <span data-ttu-id="46ad0-173">它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。</span><span class="sxs-lookup"><span data-stu-id="46ad0-173">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="46ad0-174">建议从选项卡 SSO 获取参与者 ID。</span><span class="sxs-lookup"><span data-stu-id="46ad0-174">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="46ad0-175">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="46ad0-175">**tenantId**</span></span>| <span data-ttu-id="46ad0-176">字符串</span><span class="sxs-lookup"><span data-stu-id="46ad0-176">String</span></span> | <span data-ttu-id="46ad0-177">是</span><span class="sxs-lookup"><span data-stu-id="46ad0-177">Yes</span></span> | <span data-ttu-id="46ad0-178">租户用户需要租户 ID。</span><span class="sxs-lookup"><span data-stu-id="46ad0-178">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="46ad0-179">它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。</span><span class="sxs-lookup"><span data-stu-id="46ad0-179">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="46ad0-180">建议从选项卡 SSO 获取租户 ID。</span><span class="sxs-lookup"><span data-stu-id="46ad0-180">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="46ad0-181">示例</span><span class="sxs-lookup"><span data-stu-id="46ad0-181">Example</span></span>

<span data-ttu-id="46ad0-182">`GetParticipant`API 包括以下示例：</span><span class="sxs-lookup"><span data-stu-id="46ad0-182">The `GetParticipant` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="46ad0-183">C#</span><span class="sxs-lookup"><span data-stu-id="46ad0-183">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="46ad0-184">JavaScript</span><span class="sxs-lookup"><span data-stu-id="46ad0-184">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="46ad0-185">JSON</span><span class="sxs-lookup"><span data-stu-id="46ad0-185">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

* * *

<span data-ttu-id="46ad0-186">API 的 JSON 响应 `GetParticipant` 正文为：</span><span class="sxs-lookup"><span data-stu-id="46ad0-186">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="46ad0-187">响应代码</span><span class="sxs-lookup"><span data-stu-id="46ad0-187">Response codes</span></span>

<span data-ttu-id="46ad0-188">`GetParticipant`API 包括以下响应代码：</span><span class="sxs-lookup"><span data-stu-id="46ad0-188">The `GetParticipant` API includes the following response codes:</span></span>

|<span data-ttu-id="46ad0-189">响应代码</span><span class="sxs-lookup"><span data-stu-id="46ad0-189">Response code</span></span>|<span data-ttu-id="46ad0-190">说明</span><span class="sxs-lookup"><span data-stu-id="46ad0-190">Description</span></span>|
|---|---|
| <span data-ttu-id="46ad0-191">**403**</span><span class="sxs-lookup"><span data-stu-id="46ad0-191">**403**</span></span> | <span data-ttu-id="46ad0-192">不允许应用获取参与者信息。</span><span class="sxs-lookup"><span data-stu-id="46ad0-192">The app is not allowed to get participant information.</span></span> <span data-ttu-id="46ad0-193">这是最常见的错误响应，如果会议未安装应用，将触发此错误响应。</span><span class="sxs-lookup"><span data-stu-id="46ad0-193">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="46ad0-194">例如，如果租户管理员禁用应用或在实时网站迁移期间阻止应用。</span><span class="sxs-lookup"><span data-stu-id="46ad0-194">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="46ad0-195">**200**</span><span class="sxs-lookup"><span data-stu-id="46ad0-195">**200**</span></span> | <span data-ttu-id="46ad0-196">成功检索参与者信息。</span><span class="sxs-lookup"><span data-stu-id="46ad0-196">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="46ad0-197">**401**</span><span class="sxs-lookup"><span data-stu-id="46ad0-197">**401**</span></span> | <span data-ttu-id="46ad0-198">应用使用无效令牌进行响应。</span><span class="sxs-lookup"><span data-stu-id="46ad0-198">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="46ad0-199">**404**</span><span class="sxs-lookup"><span data-stu-id="46ad0-199">**404**</span></span> | <span data-ttu-id="46ad0-200">会议已过期或找不到参与者。</span><span class="sxs-lookup"><span data-stu-id="46ad0-200">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="46ad0-201">**500**</span><span class="sxs-lookup"><span data-stu-id="46ad0-201">**500**</span></span> | <span data-ttu-id="46ad0-202">自会议结束以来 (超过 60) 会议已过期，或者参与者没有基于其角色的权限。</span><span class="sxs-lookup"><span data-stu-id="46ad0-202">The meeting has either expired (more than 60 days) since the meeting ended or the participants do not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="46ad0-203">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="46ad0-203">NotificationSignal API</span></span>

<span data-ttu-id="46ad0-204">会议中的所有用户都接收通过 API 发送 `NotificationSignal` 的通知。</span><span class="sxs-lookup"><span data-stu-id="46ad0-204">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="46ad0-205">调用会议内对话框时，内容将显示为聊天消息。</span><span class="sxs-lookup"><span data-stu-id="46ad0-205">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="46ad0-206">目前，不支持发送定向通知。</span><span class="sxs-lookup"><span data-stu-id="46ad0-206">Currently, sending targeted notifications is not supported.</span></span>

<span data-ttu-id="46ad0-207">`NotificationSignal` API 使你能够提供使用用户-机器人聊天的现有对话通知 API 传递的会议信号。</span><span class="sxs-lookup"><span data-stu-id="46ad0-207">`NotificationSignal` API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="46ad0-208">此 API 允许你根据显示会议内对话框的用户操作发出信号。</span><span class="sxs-lookup"><span data-stu-id="46ad0-208">This API allows you to signal based on user action that shows an in-meeting dialog box.</span></span> <span data-ttu-id="46ad0-209">API 包括查询参数、示例和响应代码。</span><span class="sxs-lookup"><span data-stu-id="46ad0-209">The API includes query parameter, examples, and response codes.</span></span>

#### <a name="query-parameter"></a><span data-ttu-id="46ad0-210">查询参数</span><span class="sxs-lookup"><span data-stu-id="46ad0-210">Query parameter</span></span>

<span data-ttu-id="46ad0-211">`NotificationSignal`API 包括以下查询参数：</span><span class="sxs-lookup"><span data-stu-id="46ad0-211">The `NotificationSignal` API includes the following query parameter:</span></span>

|<span data-ttu-id="46ad0-212">值</span><span class="sxs-lookup"><span data-stu-id="46ad0-212">Value</span></span>|<span data-ttu-id="46ad0-213">类型</span><span class="sxs-lookup"><span data-stu-id="46ad0-213">Type</span></span>|<span data-ttu-id="46ad0-214">必需</span><span class="sxs-lookup"><span data-stu-id="46ad0-214">Required</span></span>|<span data-ttu-id="46ad0-215">说明</span><span class="sxs-lookup"><span data-stu-id="46ad0-215">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="46ad0-216">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="46ad0-216">**conversationId**</span></span>| <span data-ttu-id="46ad0-217">字符串</span><span class="sxs-lookup"><span data-stu-id="46ad0-217">String</span></span> | <span data-ttu-id="46ad0-218">是</span><span class="sxs-lookup"><span data-stu-id="46ad0-218">Yes</span></span> | <span data-ttu-id="46ad0-219">对话标识符作为 Bot Invoke 的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="46ad0-219">The conversation identifier is available as part of Bot Invoke.</span></span> |

#### <a name="examples"></a><span data-ttu-id="46ad0-220">示例</span><span class="sxs-lookup"><span data-stu-id="46ad0-220">Examples</span></span>

<span data-ttu-id="46ad0-221">`Bot ID`在清单中声明 ，机器人将接收结果对象。</span><span class="sxs-lookup"><span data-stu-id="46ad0-221">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="46ad0-222">`completionBotId`在请求 `externalResourceUrl` 的有效负载示例中，的 参数是可选的。</span><span class="sxs-lookup"><span data-stu-id="46ad0-222">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="46ad0-223">`Bot ID` 在清单中声明，机器人将接收结果对象。</span><span class="sxs-lookup"><span data-stu-id="46ad0-223">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="46ad0-224">`externalResourceUrl`宽度和高度参数必须以像素为单位。</span><span class="sxs-lookup"><span data-stu-id="46ad0-224">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="46ad0-225">若要确保尺寸在允许的限制内，请参阅 [设计指南](design/designing-apps-in-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="46ad0-225">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="46ad0-226">URL 是在会议对话框中作为 `<iframe>` 加载的页面。</span><span class="sxs-lookup"><span data-stu-id="46ad0-226">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="46ad0-227">域必须在你的应用清单 `validDomains` 的应用数组中。</span><span class="sxs-lookup"><span data-stu-id="46ad0-227">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

<span data-ttu-id="46ad0-228">`NotificationSignal`API 包括以下示例：</span><span class="sxs-lookup"><span data-stu-id="46ad0-228">The `NotificationSignal` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="46ad0-229">C#</span><span class="sxs-lookup"><span data-stu-id="46ad0-229">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="46ad0-230">JavaScript</span><span class="sxs-lookup"><span data-stu-id="46ad0-230">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="46ad0-231">JSON</span><span class="sxs-lookup"><span data-stu-id="46ad0-231">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="46ad0-232">响应代码</span><span class="sxs-lookup"><span data-stu-id="46ad0-232">Response codes</span></span>

<span data-ttu-id="46ad0-233">`NotificationSignal`API 包括以下响应代码：</span><span class="sxs-lookup"><span data-stu-id="46ad0-233">The `NotificationSignal` API includes the following response codes:</span></span>

|<span data-ttu-id="46ad0-234">响应代码</span><span class="sxs-lookup"><span data-stu-id="46ad0-234">Response code</span></span>|<span data-ttu-id="46ad0-235">说明</span><span class="sxs-lookup"><span data-stu-id="46ad0-235">Description</span></span>|
|---|---|
| <span data-ttu-id="46ad0-236">**201**</span><span class="sxs-lookup"><span data-stu-id="46ad0-236">**201**</span></span> | <span data-ttu-id="46ad0-237">具有信号的活动已成功发送。</span><span class="sxs-lookup"><span data-stu-id="46ad0-237">The activity with signal is successfully sent.</span></span> |
| <span data-ttu-id="46ad0-238">**401**</span><span class="sxs-lookup"><span data-stu-id="46ad0-238">**401**</span></span> | <span data-ttu-id="46ad0-239">应用使用无效令牌进行响应。</span><span class="sxs-lookup"><span data-stu-id="46ad0-239">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="46ad0-240">**403**</span><span class="sxs-lookup"><span data-stu-id="46ad0-240">**403**</span></span> | <span data-ttu-id="46ad0-241">应用无法发送信号。</span><span class="sxs-lookup"><span data-stu-id="46ad0-241">The app is unable to send the signal.</span></span> <span data-ttu-id="46ad0-242">发生这种情况的原因有多种，例如租户管理员禁用应用、实时网站迁移期间阻止应用等。</span><span class="sxs-lookup"><span data-stu-id="46ad0-242">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="46ad0-243">在这种情况下，有效负载包含详细的错误消息。</span><span class="sxs-lookup"><span data-stu-id="46ad0-243">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="46ad0-244">**404**</span><span class="sxs-lookup"><span data-stu-id="46ad0-244">**404**</span></span> | <span data-ttu-id="46ad0-245">会议聊天不存在。</span><span class="sxs-lookup"><span data-stu-id="46ad0-245">The meeting chat does not exist.</span></span> |

## <a name="code-sample"></a><span data-ttu-id="46ad0-246">代码示例</span><span class="sxs-lookup"><span data-stu-id="46ad0-246">Code sample</span></span>

|<span data-ttu-id="46ad0-247">示例名称</span><span class="sxs-lookup"><span data-stu-id="46ad0-247">Sample name</span></span> | <span data-ttu-id="46ad0-248">说明</span><span class="sxs-lookup"><span data-stu-id="46ad0-248">Description</span></span> | <span data-ttu-id="46ad0-249">.NET</span><span class="sxs-lookup"><span data-stu-id="46ad0-249">.NET</span></span> | <span data-ttu-id="46ad0-250">Node.js</span><span class="sxs-lookup"><span data-stu-id="46ad0-250">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="46ad0-251">会议可扩展性</span><span class="sxs-lookup"><span data-stu-id="46ad0-251">Meetings extensibility</span></span> | <span data-ttu-id="46ad0-252">Microsoft Teams令牌的会议扩展性示例。</span><span class="sxs-lookup"><span data-stu-id="46ad0-252">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="46ad0-253">View</span><span class="sxs-lookup"><span data-stu-id="46ad0-253">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [<span data-ttu-id="46ad0-254">View</span><span class="sxs-lookup"><span data-stu-id="46ad0-254">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| <span data-ttu-id="46ad0-255">会议内容气泡机器人</span><span class="sxs-lookup"><span data-stu-id="46ad0-255">Meeting content bubble bot</span></span> | <span data-ttu-id="46ad0-256">Microsoft Teams会议扩展性示例，用于与会议内容气泡机器人进行交互。</span><span class="sxs-lookup"><span data-stu-id="46ad0-256">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="46ad0-257">View</span><span class="sxs-lookup"><span data-stu-id="46ad0-257">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="46ad0-258">View</span><span class="sxs-lookup"><span data-stu-id="46ad0-258">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| <span data-ttu-id="46ad0-259">Meeting meetingSidePanel</span><span class="sxs-lookup"><span data-stu-id="46ad0-259">Meeting meetingSidePanel</span></span> | <span data-ttu-id="46ad0-260">Microsoft Teams与会议中的侧面板交互的会议扩展性示例。</span><span class="sxs-lookup"><span data-stu-id="46ad0-260">Microsoft Teams meeting extensibility sample for interacting with the side panel in-meeting.</span></span> | [<span data-ttu-id="46ad0-261">View</span><span class="sxs-lookup"><span data-stu-id="46ad0-261">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [<span data-ttu-id="46ad0-262">View</span><span class="sxs-lookup"><span data-stu-id="46ad0-262">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|

## <a name="see-also"></a><span data-ttu-id="46ad0-263">另请参阅</span><span class="sxs-lookup"><span data-stu-id="46ad0-263">See also</span></span>

* [<span data-ttu-id="46ad0-264">会议内对话设计指南</span><span class="sxs-lookup"><span data-stu-id="46ad0-264">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="46ad0-265">Teams选项卡的身份验证流</span><span class="sxs-lookup"><span data-stu-id="46ad0-265">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
* [<span data-ttu-id="46ad0-266">会议Teams应用程序</span><span class="sxs-lookup"><span data-stu-id="46ad0-266">Apps for Teams meetings</span></span>](teams-apps-in-meetings.md)

## <a name="next-step"></a><span data-ttu-id="46ad0-267">后续步骤</span><span class="sxs-lookup"><span data-stu-id="46ad0-267">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="46ad0-268">为会议启用和配置Teams应用程序</span><span class="sxs-lookup"><span data-stu-id="46ad0-268">Enable and configure your apps for Teams meetings</span></span>](enable-and-configure-your-app-for-teams-meetings.md)
