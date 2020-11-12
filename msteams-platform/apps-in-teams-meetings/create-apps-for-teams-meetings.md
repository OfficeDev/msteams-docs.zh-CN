---
title: 创建适用于团队会议的应用
author: laujan
description: 创建团队会议的应用程序
ms.topic: conceptual
ms.author: lajanuar
keywords: 团队应用会议用户参与者角色 api
ms.openlocfilehash: d7dc812f715b6a7edbcc706946b8d80dd692daee
ms.sourcegitcommit: 0aeb60027f423d8ceff3b377db8c3efbb6da4d17
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2020
ms.locfileid: "48997970"
---
# <a name="create-apps-for-teams-meetings-developer-preview"></a><span data-ttu-id="7c481-104">创建团队相关应用程序会议 (开发人员预览版) </span><span class="sxs-lookup"><span data-stu-id="7c481-104">Create apps for Teams meetings (Developer Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="7c481-105">Microsoft 团队开发人员预览版中包含的功能仅用于早期访问、测试和反馈目的。</span><span class="sxs-lookup"><span data-stu-id="7c481-105">Features included in Microsoft Teams Developer Preview are provided for early-access, testing, and feedback purposes only.</span></span> <span data-ttu-id="7c481-106">他们可能会在公开发布之前进行更改，并且不应在生产应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="7c481-106">They may undergo changes before becoming available in the public release and should not be used in production applications.</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="7c481-107">先决条件和注意事项</span><span class="sxs-lookup"><span data-stu-id="7c481-107">Prerequisites and considerations</span></span>

1. <span data-ttu-id="7c481-108">会议中的应用程序需要一些有关 [团队应用程序开发](../overview.md)的基本知识。</span><span class="sxs-lookup"><span data-stu-id="7c481-108">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="7c481-109">会议中的应用程序可以包含 [选项卡](../tabs/what-are-tabs.md)、 [bot](../bots/what-are-bots.md)和 [邮件扩展](../messaging-extensions/what-are-messaging-extensions.md) 功能，并将要求对团队 [应用程序清单](#update-your-app-manifest) 进行更新以指示该应用程序可用于会议</span><span class="sxs-lookup"><span data-stu-id="7c481-109">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

1. <span data-ttu-id="7c481-110">为了使您的应用程序在会议生命周期中作为选项卡运行，它必须支持 [groupchat 范围](../resources/schema/manifest-schema.md#configurabletabs)中可配置的选项卡。</span><span class="sxs-lookup"><span data-stu-id="7c481-110">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs).</span></span> <span data-ttu-id="7c481-111">*请参阅*[使用自定义选项卡扩展团队应用](../tabs/how-to/add-tab.md)。如果支持此 `groupchat` 范围，您的应用程序将在 [会议前](teams-apps-in-meetings.md#pre-meeting-app-experience)和 [会议后](teams-apps-in-meetings.md#post-meeting-app-experience)的聊天中启用。</span><span class="sxs-lookup"><span data-stu-id="7c481-111">*See* [Extend your Teams app with a custom tab](../tabs/how-to/add-tab.md). Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

1. <span data-ttu-id="7c481-112">会议 API URL 参数可能需要 `meetingId` 、 `userId` 和 [tenantId](/onedrive/find-your-office-365-tenant-id) 这些参数可用作团队客户端 SDK 和 bot 活动的一部分。</span><span class="sxs-lookup"><span data-stu-id="7c481-112">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="7c481-113">此外，还可以使用 [选项卡 SSO 身份验证](../tabs/how-to/authentication/auth-aad-sso.md)检索用户 ID 和租户 ID 的可靠信息。</span><span class="sxs-lookup"><span data-stu-id="7c481-113">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

1. <span data-ttu-id="7c481-114">某些会议 Api （如 `GetParticipant` 将需要 [机器人注册和 BOT 应用 ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) 生成身份验证令牌）。</span><span class="sxs-lookup"><span data-stu-id="7c481-114">Some meeting APIs, such as `GetParticipant` will require a [bot registration and bot app ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) to generate auth tokens.</span></span>

1. <span data-ttu-id="7c481-115">作为开发人员，您必须遵循在团队会议期间触发的会议前和会议中对话框[的 "常规](design/designing-in-meeting-dialog.md)[团队" 选项卡设计指导方针](../tabs/design/tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="7c481-115">As a developer, you must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios as well as the [in-meeting dialog guidelines](design/designing-in-meeting-dialog.md) for in-meeting dialog triggered during a Teams meeting.</span></span>

1. <span data-ttu-id="7c481-116">请注意，为了使您的应用程序实时更新，必须根据会议中的事件活动保持最新。</span><span class="sxs-lookup"><span data-stu-id="7c481-116">Please note that in order for your app to be updated in real-time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="7c481-117">这些事件可以在会议中的对话框 (引用 `bot Id` `Notification Signal API` 会议生命周期的) 和其他表面中的完成参数</span><span class="sxs-lookup"><span data-stu-id="7c481-117">These events can be within the in-meeting dialog (refer to completion `bot Id` parameter in `Notification Signal API`) and other surfaces across the meeting lifecycle</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="7c481-118">会议应用程序 API 参考</span><span class="sxs-lookup"><span data-stu-id="7c481-118">Meeting apps API reference</span></span>

|<span data-ttu-id="7c481-119">API</span><span class="sxs-lookup"><span data-stu-id="7c481-119">API</span></span>|<span data-ttu-id="7c481-120">说明</span><span class="sxs-lookup"><span data-stu-id="7c481-120">Description</span></span>|<span data-ttu-id="7c481-121">请求</span><span class="sxs-lookup"><span data-stu-id="7c481-121">Request</span></span>|<span data-ttu-id="7c481-122">源</span><span class="sxs-lookup"><span data-stu-id="7c481-122">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="7c481-123">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="7c481-123">**GetUserContext**</span></span>| <span data-ttu-id="7c481-124">获取上下文信息以在 "团队" 选项卡中显示相关内容。</span><span class="sxs-lookup"><span data-stu-id="7c481-124">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="7c481-125">_**microsoftTeams getContext ( ( ) => {/ *...* /} )**_</span><span class="sxs-lookup"><span data-stu-id="7c481-125">_**microsoftTeams.getContext( ( ) => {  / *...* / } )**_</span></span>|<span data-ttu-id="7c481-126">Microsoft 团队客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="7c481-126">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="7c481-127">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="7c481-127">**GetParticipant**</span></span>|<span data-ttu-id="7c481-128">此 API 允许 bot 按会议 id 和参与者 id 提取参与者信息。</span><span class="sxs-lookup"><span data-stu-id="7c481-128">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="7c481-129">**获取** _**/v1/meetings/{meetingId}/participants/{participantId}？ tenantId = {tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="7c481-129">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="7c481-130">Microsoft Bot 框架 SDK</span><span class="sxs-lookup"><span data-stu-id="7c481-130">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="7c481-131">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="7c481-131">**NotificationSignal**</span></span> |<span data-ttu-id="7c481-132">将使用以下现有对话通知 API 为用户-bot 聊天) 传递会议信号 (。</span><span class="sxs-lookup"><span data-stu-id="7c481-132">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="7c481-133">通过此 API，开发人员可以基于最终用户操作发出信号，以显示会议中的对话气泡图。</span><span class="sxs-lookup"><span data-stu-id="7c481-133">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="7c481-134">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="7c481-134">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="7c481-135">Microsoft Bot 框架 SDK</span><span class="sxs-lookup"><span data-stu-id="7c481-135">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="7c481-136">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="7c481-136">GetUserContext</span></span>

<span data-ttu-id="7c481-137">请参阅我们 [的 "获取团队上下文" 选项卡](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) 文档，获取有关标识和检索您的选项卡内容的上下文信息的指南。</span><span class="sxs-lookup"><span data-stu-id="7c481-137">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="7c481-138">作为会议扩展性的一部分，已为响应负载添加了一个新值：</span><span class="sxs-lookup"><span data-stu-id="7c481-138">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="7c481-139">✔ **meetingId** ：在会议上下文中运行时由选项卡使用。</span><span class="sxs-lookup"><span data-stu-id="7c481-139">✔ **meetingId** : used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="7c481-140">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="7c481-140">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="7c481-141">不缓存参与者角色，因为会议组织者可以在任何时间点更改角色。</span><span class="sxs-lookup"><span data-stu-id="7c481-141">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="7c481-142">团队目前不支持 API 的多350个参与者的大型通讯组列表或名单大小 `GetParticipant` 。</span><span class="sxs-lookup"><span data-stu-id="7c481-142">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>
>
> * <span data-ttu-id="7c481-143">即将推出对 Bot 框架 SDK 的支持。</span><span class="sxs-lookup"><span data-stu-id="7c481-143">Support for the Bot Framework SDK is coming soon.</span></span>


#### <a name="request"></a><span data-ttu-id="7c481-144">请求</span><span class="sxs-lookup"><span data-stu-id="7c481-144">Request</span></span>

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="7c481-145">*请参阅* [Bot 框架 API 参考](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="7c481-145">*See* the [Bot Framework API reference](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<!-- markdownlint-disable MD025 -->

<span data-ttu-id="7c481-146">**C # 示例**</span><span class="sxs-lookup"><span data-stu-id="7c481-146">**C# Example**</span></span>

```csharp
string meetingId = "meetingid?";
string participantId = "participantidhere";
var connectorClient = turnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage();
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
request.Method = new HttpMethod("GET");
request.RequestUri = new System.Uri(Path.Combine(connectorClient.BaseUri.OriginalString, $"/meetings/{meetingId}/participants/{participantId}"));
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, cancellationToken).ConfigureAwait(false);
if (response.StatusCode == System.Net.HttpStatusCode.OK)
{
    var content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
    var theObject = Rest.Serialization.SafeJsonConvert.DeserializeObject<WhateverObjectIsReturned>(content, connectorClient.DeserializationSettings);
}
```

* * *
<!-- markdownlint-disable MD001 -->

#### <a name="query-parameters"></a><span data-ttu-id="7c481-147">查询参数</span><span class="sxs-lookup"><span data-stu-id="7c481-147">Query parameters</span></span>

|<span data-ttu-id="7c481-148">值</span><span class="sxs-lookup"><span data-stu-id="7c481-148">Value</span></span>|<span data-ttu-id="7c481-149">类型</span><span class="sxs-lookup"><span data-stu-id="7c481-149">Type</span></span>|<span data-ttu-id="7c481-150">必需</span><span class="sxs-lookup"><span data-stu-id="7c481-150">Required</span></span>|<span data-ttu-id="7c481-151">说明</span><span class="sxs-lookup"><span data-stu-id="7c481-151">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="7c481-152">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="7c481-152">**meetingId**</span></span>| <span data-ttu-id="7c481-153">string</span><span class="sxs-lookup"><span data-stu-id="7c481-153">string</span></span> | <span data-ttu-id="7c481-154">是</span><span class="sxs-lookup"><span data-stu-id="7c481-154">Yes</span></span> | <span data-ttu-id="7c481-155">会议标识符可通过 Bot 调用和团队客户端 SDK 获取。</span><span class="sxs-lookup"><span data-stu-id="7c481-155">The meeting identifier is available via Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="7c481-156">**participantId**</span><span class="sxs-lookup"><span data-stu-id="7c481-156">**participantId**</span></span>| <span data-ttu-id="7c481-157">string</span><span class="sxs-lookup"><span data-stu-id="7c481-157">string</span></span> | <span data-ttu-id="7c481-158">是</span><span class="sxs-lookup"><span data-stu-id="7c481-158">Yes</span></span> | <span data-ttu-id="7c481-159">此字段是用户 ID，可在选项卡 SSO、Bot 调用和团队客户端 SDK 中使用。</span><span class="sxs-lookup"><span data-stu-id="7c481-159">This field is the User ID and it is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="7c481-160">强烈建议使用 Tab SSO</span><span class="sxs-lookup"><span data-stu-id="7c481-160">Tab SSO is highly recommended</span></span>|
|<span data-ttu-id="7c481-161">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="7c481-161">**tenantId**</span></span>| <span data-ttu-id="7c481-162">string</span><span class="sxs-lookup"><span data-stu-id="7c481-162">string</span></span> | <span data-ttu-id="7c481-163">是</span><span class="sxs-lookup"><span data-stu-id="7c481-163">Yes</span></span> | <span data-ttu-id="7c481-164">租户用户所需的。</span><span class="sxs-lookup"><span data-stu-id="7c481-164">This required for tenant users.</span></span> <span data-ttu-id="7c481-165">它在选项卡 SSO、Bot 调用和团队客户端 SDK 中可用。</span><span class="sxs-lookup"><span data-stu-id="7c481-165">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="7c481-166">强烈建议使用 Tab SSO</span><span class="sxs-lookup"><span data-stu-id="7c481-166">Tab SSO is highly recommended</span></span>|

#### <a name="response-payload"></a><span data-ttu-id="7c481-167">响应有效负载</span><span class="sxs-lookup"><span data-stu-id="7c481-167">Response Payload</span></span>
<!-- markdownlint-disable MD036 -->

<span data-ttu-id="7c481-168">"会议" 下的 **角色** 可以是 *组织者* 、 *演示者* 或 *与会者* 。</span><span class="sxs-lookup"><span data-stu-id="7c481-168">**role** under "meeting" can be *Organizer* , *Presenter* , or *Attendee*.</span></span>

<span data-ttu-id="7c481-169">**示例 1**</span><span class="sxs-lookup"><span data-stu-id="7c481-169">**Example 1**</span></span>

```json
{
  "user":
  {
      "id": "29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId": "6aebbad0-e5a5-424a-834a-20fb051f3c1a",
      "name": "Allan Deyoung",
      "givenName": "Allan",
      "surname": "Deyoung",
      "email": "Allan.Deyoung@microsoft.com",
      "userPrincipalName": "Allan.Deyoung@microsoft.com",
      "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
      "userRole": "user"
  },
  "meeting":
  {
      "role ": "Presenter",
      "inMeeting":true
  },
  "conversation":
  {
      "id": "<conversation id>"
  }
}
```
#### <a name="response-codes"></a><span data-ttu-id="7c481-170">响应代码</span><span class="sxs-lookup"><span data-stu-id="7c481-170">Response Codes</span></span>

<span data-ttu-id="7c481-171">**403** ：不允许应用获取参与者信息。</span><span class="sxs-lookup"><span data-stu-id="7c481-171">**403** : The app is not allowed to get participant information.</span></span> <span data-ttu-id="7c481-172">这是最常见的错误响应，当应用程序未安装在会议中时（如租户管理员禁用或在实时网站迁移过程中被阻止）时，会触发此响应。</span><span class="sxs-lookup"><span data-stu-id="7c481-172">This will be the most common error response and is triggered when the app is not installed in the meeting such as when it is disabled by tenant admin or blocked during live site migration.</span></span>  
<span data-ttu-id="7c481-173">**200** ：成功检索参与者信息。</span><span class="sxs-lookup"><span data-stu-id="7c481-173">**200** : Participant information successfully retrieved.</span></span>  
<span data-ttu-id="7c481-174">**401** ：令牌无效。</span><span class="sxs-lookup"><span data-stu-id="7c481-174">**401** : Invalid token.</span></span>  
<span data-ttu-id="7c481-175">**404** ：找不到参与者。</span><span class="sxs-lookup"><span data-stu-id="7c481-175">**404** : Participant cannot be found.</span></span> 
<span data-ttu-id="7c481-176">**500** ：会议已过期 (超过60天，自会议结束) 或参与者没有基于其角色的权限。</span><span class="sxs-lookup"><span data-stu-id="7c481-176">**500** : The meeting is either expired (more than 60 days since the meeting ended) or the participant does not have permissions based on their role.</span></span>

<span data-ttu-id="7c481-177">**即将推出**</span><span class="sxs-lookup"><span data-stu-id="7c481-177">**Coming Soon**</span></span>

<span data-ttu-id="7c481-178">**404** ：会议已过期，或者找不到参与者。</span><span class="sxs-lookup"><span data-stu-id="7c481-178">**404** : the meeting has either expired or participant cannot be found.</span></span> 

<!-- markdownlint-disable MD024 -->
### <a name="notificationsignal-api"></a><span data-ttu-id="7c481-179">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="7c481-179">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="7c481-180">在调用会议内对话时，相同的内容也会显示为聊天消息。</span><span class="sxs-lookup"><span data-stu-id="7c481-180">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="request"></a><span data-ttu-id="7c481-181">请求</span><span class="sxs-lookup"><span data-stu-id="7c481-181">Request</span></span>

```http
POST /v3/conversations/{conversationId}/activities
```

#### <a name="query-parameters"></a><span data-ttu-id="7c481-182">查询参数</span><span class="sxs-lookup"><span data-stu-id="7c481-182">Query parameters</span></span>

|<span data-ttu-id="7c481-183">值</span><span class="sxs-lookup"><span data-stu-id="7c481-183">Value</span></span>|<span data-ttu-id="7c481-184">类型</span><span class="sxs-lookup"><span data-stu-id="7c481-184">Type</span></span>|<span data-ttu-id="7c481-185">必需</span><span class="sxs-lookup"><span data-stu-id="7c481-185">Required</span></span>|<span data-ttu-id="7c481-186">说明</span><span class="sxs-lookup"><span data-stu-id="7c481-186">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="7c481-187">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="7c481-187">**conversationId**</span></span>| <span data-ttu-id="7c481-188">string</span><span class="sxs-lookup"><span data-stu-id="7c481-188">string</span></span> | <span data-ttu-id="7c481-189">是</span><span class="sxs-lookup"><span data-stu-id="7c481-189">Yes</span></span> | <span data-ttu-id="7c481-190">会话标识符作为机器人 invoke 的一部分提供</span><span class="sxs-lookup"><span data-stu-id="7c481-190">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="request-payload"></a><span data-ttu-id="7c481-191">请求有效负载</span><span class="sxs-lookup"><span data-stu-id="7c481-191">Request Payload</span></span>

> [!NOTE]
>
> *  <span data-ttu-id="7c481-192">在下面请求的负载中， `completionBotId` 的参数 `externalResourceUrl` 是可选的。</span><span class="sxs-lookup"><span data-stu-id="7c481-192">In the requested payload below, the `completionBotId` parameter of the `externalResourceUrl`is an optional.</span></span> <span data-ttu-id="7c481-193">它是 `Bot ID` 在清单中声明的。</span><span class="sxs-lookup"><span data-stu-id="7c481-193">It is the `Bot ID` that is declared in the manifest.</span></span> <span data-ttu-id="7c481-194">机器人将接收到一个 result 对象。</span><span class="sxs-lookup"><span data-stu-id="7c481-194">The bot will receive a result object.</span></span>
> * <span data-ttu-id="7c481-195">ExternalResourceUrl width 和 height 参数必须以像素为单位。</span><span class="sxs-lookup"><span data-stu-id="7c481-195">The externalResourceUrl width and height parameters must be in pixels.</span></span> <span data-ttu-id="7c481-196">请参阅 [设计准则](design/designing-in-meeting-dialog.md) ，以确保尺寸在允许的限制范围内。</span><span class="sxs-lookup"><span data-stu-id="7c481-196">Refer to the [design guidelines](design/designing-in-meeting-dialog.md) to ensure the dimensions are within the allowed limits.</span></span>
> * <span data-ttu-id="7c481-197">URL 是 `<iframe>` 在会议对话中加载的页面。</span><span class="sxs-lookup"><span data-stu-id="7c481-197">The URL is the page loaded as an `<iframe>` inside the in-meeting dialog.</span></span> <span data-ttu-id="7c481-198">URL 的域必须位于 `validDomains` 应用程序清单中的应用程序阵列中。</span><span class="sxs-lookup"><span data-stu-id="7c481-198">The URL's domain must be in the app's `validDomains` array in your app manifest.</span></span>


# <a name="json"></a>[<span data-ttu-id="7c481-199">JSON</span><span class="sxs-lookup"><span data-stu-id="7c481-199">JSON</span></span>](#tab/json)

```json
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

# <a name="cnet"></a>[<span data-ttu-id="7c481-200">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7c481-200">C#/.NET</span></span>](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
MeetingNotification notification = new MeetingNotification
  {
    AlertInMeeting = true,
    ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
  };
activity.ChannelData = new TeamsChannelData
  {
    Notification = notification
  };
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[<span data-ttu-id="7c481-201">JavaScript</span><span class="sxs-lookup"><span data-stu-id="7c481-201">JavaScript</span></span>](#tab/javascript)

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

* * *

> [!IMPORTANT]
> <span data-ttu-id="7c481-202">内容气泡 (taskInfo URL 中的 URL) 必须包含在团队应用程序清单中的 [有效域](../resources/schema/manifest-schema.md#validdomains) 列表中。</span><span class="sxs-lookup"><span data-stu-id="7c481-202">The URL in the content bubble (taskInfo URL) must be included in the [valid domains](../resources/schema/manifest-schema.md#validdomains) list included in the Teams app manifest.</span></span>

#### <a name="response-codes"></a><span data-ttu-id="7c481-203">响应代码</span><span class="sxs-lookup"><span data-stu-id="7c481-203">Response Codes</span></span>

<span data-ttu-id="7c481-204">**201** ：已成功发送信号活动</span><span class="sxs-lookup"><span data-stu-id="7c481-204">**201** : activity with signal is successfully sent</span></span>  
<span data-ttu-id="7c481-205">**401** ：令牌无效</span><span class="sxs-lookup"><span data-stu-id="7c481-205">**401** : invalid token</span></span>  
<span data-ttu-id="7c481-206">**403** ：不允许应用发送信号。</span><span class="sxs-lookup"><span data-stu-id="7c481-206">**403** : the app is not allowed to send the signal.</span></span> <span data-ttu-id="7c481-207">在这种情况下，有效负载应包含更详细的错误消息。</span><span class="sxs-lookup"><span data-stu-id="7c481-207">In this case, the payload should contain more detail error message.</span></span> <span data-ttu-id="7c481-208">可能有多种原因：应用程序因租户管理员而被禁用，在 live 网站缓解等过程中被阻止。</span><span class="sxs-lookup"><span data-stu-id="7c481-208">There can be many reasons: app disabled by tenant admin, blocked during live site mitigation, etc.</span></span>  
<span data-ttu-id="7c481-209">**404** ：会议聊天不存在</span><span class="sxs-lookup"><span data-stu-id="7c481-209">**404** : meeting chat doesn't exist</span></span>  

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="7c481-210">为团队会议启用您的应用程序</span><span class="sxs-lookup"><span data-stu-id="7c481-210">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="7c481-211">更新应用程序清单</span><span class="sxs-lookup"><span data-stu-id="7c481-211">Update your app manifest</span></span>

<span data-ttu-id="7c481-212">会议应用程序功能是通过 **configurableTabs**  ->  **作用域** 和 **上下文** 数组在应用程序清单中声明的。</span><span class="sxs-lookup"><span data-stu-id="7c481-212">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="7c481-213">*作用域* 定义了您的应用程序将在何处定义的人员和 *上下文* 。</span><span class="sxs-lookup"><span data-stu-id="7c481-213">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> * <span data-ttu-id="7c481-214">请使用 [开发人员预览版清单架构](../resources/schema/manifest-schema-dev-preview.md) 在你的应用程序清单中试用此架构。</span><span class="sxs-lookup"><span data-stu-id="7c481-214">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="7c481-215">Context 属性</span><span class="sxs-lookup"><span data-stu-id="7c481-215">Context property</span></span>

<span data-ttu-id="7c481-216">该选项卡 `context` 和 `scopes` 属性在协调中使用，以确定您希望应用程序的显示位置。</span><span class="sxs-lookup"><span data-stu-id="7c481-216">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="7c481-217">或范围中的选项卡 `team` `groupchat` 可以有多个上下文。</span><span class="sxs-lookup"><span data-stu-id="7c481-217">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="7c481-218">Context 属性的可能值如下所示：</span><span class="sxs-lookup"><span data-stu-id="7c481-218">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="7c481-219">**channelTab** ：团队频道标头中的一个选项卡。</span><span class="sxs-lookup"><span data-stu-id="7c481-219">**channelTab** : a tab in the header of a team channel.</span></span>
* <span data-ttu-id="7c481-220">**privateChatTab** ：组标头中的一个选项卡，在一组不在团队或会议的上下文中的一组用户之间聊天。</span><span class="sxs-lookup"><span data-stu-id="7c481-220">**privateChatTab** : a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="7c481-221">**meetingChatTab** ：组标头中的一个选项卡，在计划会议上下文中的一组用户之间聊天。</span><span class="sxs-lookup"><span data-stu-id="7c481-221">**meetingChatTab** : a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="7c481-222">**meetingDetailsTab** ：日历的 "会议详细信息" 视图标头中的一个选项卡。</span><span class="sxs-lookup"><span data-stu-id="7c481-222">**meetingDetailsTab** : a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="7c481-223">**meetingSidePanel** ：通过 (u) 的统一栏打开的会议面板。</span><span class="sxs-lookup"><span data-stu-id="7c481-223">**meetingSidePanel** : an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="7c481-224">"Context" 属性目前不受支持，因此在移动客户端上将被忽略</span><span class="sxs-lookup"><span data-stu-id="7c481-224">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="7c481-225">为会议方案配置应用程序</span><span class="sxs-lookup"><span data-stu-id="7c481-225">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="7c481-226">若要使您的应用程序在选项卡库中可见，它需要 **支持可配置的选项卡** 和 **组聊天作用域** 。</span><span class="sxs-lookup"><span data-stu-id="7c481-226">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>
>
> * <span data-ttu-id="7c481-227">移动客户端仅支持准备会议和投递会议表面中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="7c481-227">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="7c481-228">在会议中 (会议中的对话和面板) 的体验将很快推出。</span><span class="sxs-lookup"><span data-stu-id="7c481-228">The In-meeting experiences (in-meeting dialog and panel) on mobile will be available soon.</span></span> <span data-ttu-id="7c481-229">创建移动电话选项卡时，请遵循 [移动电话上的选项卡指南](../tabs/design/tabs-mobile.md) 。</span><span class="sxs-lookup"><span data-stu-id="7c481-229">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span> 

### <a name="pre-meeting"></a><span data-ttu-id="7c481-230">会议前</span><span class="sxs-lookup"><span data-stu-id="7c481-230">Pre-meeting</span></span>

<span data-ttu-id="7c481-231">拥有组织者和/或演示者角色的用户使用会议 **聊天** 和会议 **详细信息** 页中的加号➕按钮将选项卡添加到会议。</span><span class="sxs-lookup"><span data-stu-id="7c481-231">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="7c481-232">邮件扩展通过位于聊天的撰写邮件区域下的省略号/溢出菜单 &#x25CF;&#x25CF;&#x25CF; 添加到中。</span><span class="sxs-lookup"><span data-stu-id="7c481-232">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="7c481-233">将 bot 添加到会议聊天中，使用 " **@** " 键，然后选择 " **获取 bot** "。</span><span class="sxs-lookup"><span data-stu-id="7c481-233">Bots are added to a meeting chat using the " **@** " key and selecting **Get bots**.</span></span>

<span data-ttu-id="7c481-234">✔ *必须* 通过 [选项卡 SSO](../tabs/how-to/authentication/auth-aad-sso.md)确认用户标识。</span><span class="sxs-lookup"><span data-stu-id="7c481-234">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="7c481-235">遵循此身份验证后，应用可以通过 GetParticipant API 检索用户角色。</span><span class="sxs-lookup"><span data-stu-id="7c481-235">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="7c481-236">✔基于用户角色，应用现在将能够呈现特定于角色的体验。</span><span class="sxs-lookup"><span data-stu-id="7c481-236">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="7c481-237">例如，轮询应用程序可以仅允许组织者和演示者创建新的轮询。</span><span class="sxs-lookup"><span data-stu-id="7c481-237">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="7c481-238">**注意** ：在会议进行过程中，可以更改角色分配。</span><span class="sxs-lookup"><span data-stu-id="7c481-238">**NOTE** : Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="7c481-239">*请参阅*[团队会议中的角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。</span><span class="sxs-lookup"><span data-stu-id="7c481-239">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="in-meeting"></a><span data-ttu-id="7c481-240">会议中</span><span class="sxs-lookup"><span data-stu-id="7c481-240">In-meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="7c481-241">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="7c481-241">**sidePanel**</span></span>

<span data-ttu-id="7c481-242">在您的应用程序清单中✔将 **sidePanel** 添加到 **上下文** 阵列中，如上文所述。</span><span class="sxs-lookup"><span data-stu-id="7c481-242">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="7c481-243">✔在会议中以及在所有情况下，应用程序将呈现在320px 中的 "会议" 选项卡中，宽度为宽。</span><span class="sxs-lookup"><span data-stu-id="7c481-243">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="7c481-244">您的选项卡必须针对此进行优化。</span><span class="sxs-lookup"><span data-stu-id="7c481-244">Your tab must be optimized for this.</span></span> <span data-ttu-id="7c481-245">*请参阅* [FrameContext 接口](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="7c481-245">*See* , [FrameContext interface](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span></span>

<span data-ttu-id="7c481-246">✔请参阅 [团队 SDK](../tabs/how-to/access-teams-context.md#user-context) ，以使用 **userContext** API 进行相应的路由请求。</span><span class="sxs-lookup"><span data-stu-id="7c481-246">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="7c481-247">✔引用 [选项卡的团队身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="7c481-247">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="7c481-248">选项卡的身份验证流非常类似于网站的身份验证流。</span><span class="sxs-lookup"><span data-stu-id="7c481-248">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="7c481-249">因此，选项卡可以直接使用 OAuth 2.0。</span><span class="sxs-lookup"><span data-stu-id="7c481-249">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="7c481-250">*另请参阅* [Microsoft Identity platform 和 OAuth 2.0 授权代码流](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。</span><span class="sxs-lookup"><span data-stu-id="7c481-250">*See also* , [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="7c481-251">**会议对话**</span><span class="sxs-lookup"><span data-stu-id="7c481-251">**in-meeting dialog**</span></span>

<span data-ttu-id="7c481-252">✔您必须遵守 [会议中的对话框设计准则](design/designing-in-meeting-dialog.md)。</span><span class="sxs-lookup"><span data-stu-id="7c481-252">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-in-meeting-dialog.md).</span></span>

<span data-ttu-id="7c481-253">✔引用 [选项卡的团队身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="7c481-253">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="7c481-254">✔使用 [通知](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API 指示需要触发气泡通知。</span><span class="sxs-lookup"><span data-stu-id="7c481-254">✔ Use the [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="7c481-255">✔作为通知请求负载的一部分，请添加承载要 showcased 内容的 URL。</span><span class="sxs-lookup"><span data-stu-id="7c481-255">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="7c481-256">这些通知在本质上是永久性的。</span><span class="sxs-lookup"><span data-stu-id="7c481-256">These notifications are persistent in nature.</span></span> <span data-ttu-id="7c481-257">在用户在 web 视图中执行某项操作后，必须调用 [**submitTask ( # B1**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 函数以自动消除。</span><span class="sxs-lookup"><span data-stu-id="7c481-257">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="7c481-258">这是应用程序提交的必要条件。</span><span class="sxs-lookup"><span data-stu-id="7c481-258">This is a requirement for app submission.</span></span> <span data-ttu-id="7c481-259">*另请参阅*[团队 SDK：任务模块](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="7c481-259">*See also* , [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="7c481-260">如果您希望您的应用程序支持匿名用户，初始的调用请求负载必须依赖于 `from.id`  用户的 (ID) 对象中的请求元数据 `from` ，而不是 `from.aadObjectId` 用户) 请求元数据的 (AZURE Active Directory ID。</span><span class="sxs-lookup"><span data-stu-id="7c481-260">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="7c481-261">*请参阅*[在选项卡中使用任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md)和 [创建并发送任务模块](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。</span><span class="sxs-lookup"><span data-stu-id="7c481-261">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="post-meeting"></a><span data-ttu-id="7c481-262">会议后</span><span class="sxs-lookup"><span data-stu-id="7c481-262">Post-meeting</span></span>

<span data-ttu-id="7c481-263">会议后和会议前配置是等效的。</span><span class="sxs-lookup"><span data-stu-id="7c481-263">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="7c481-264">会议应用程序示例</span><span class="sxs-lookup"><span data-stu-id="7c481-264">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="7c481-265">会议令牌生成器应用</span><span class="sxs-lookup"><span data-stu-id="7c481-265">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
