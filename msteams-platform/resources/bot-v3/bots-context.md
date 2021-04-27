---
title: 获取 Microsoft Teams 自动程序上下文
description: 介绍如何在 Microsoft Teams 中获取机器人的上下文
keywords: teams 机器人上下文
ms.topic: conceptual
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: 154a276c65987955cfe20e5b7ce4ed2e8973cbfd
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020658"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a><span data-ttu-id="ddff1-104">获取 Microsoft Teams 自动程序上下文</span><span class="sxs-lookup"><span data-stu-id="ddff1-104">Get context for your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="ddff1-105">机器人可以访问有关团队或聊天的其他上下文，如用户配置文件。</span><span class="sxs-lookup"><span data-stu-id="ddff1-105">Your bot can access additional context about the team or chat, such as user profile.</span></span> <span data-ttu-id="ddff1-106">此信息可用于丰富自动程序的功能并提供更加个性化的体验。</span><span class="sxs-lookup"><span data-stu-id="ddff1-106">This information can be used to enrich your bot's functionality and provide a more personalized experience.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="ddff1-107">通过 Bot Builder SDK 的扩展，可以最好地访问特定于 Microsoft Teams 的机器人 API。</span><span class="sxs-lookup"><span data-stu-id="ddff1-107">Microsoft Teams-specific bot APIs are best accessed through our extensions for the Bot Builder SDK.</span></span>
> * <span data-ttu-id="ddff1-108">对于 C# .NET，请下载 [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet 程序包。</span><span class="sxs-lookup"><span data-stu-id="ddff1-108">For C# or .NET, download our [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>
> * <span data-ttu-id="ddff1-109">对于Node.js，适用于 Teams 的 Bot Builder 功能已合并到 [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) v4.6 中。</span><span class="sxs-lookup"><span data-stu-id="ddff1-109">For Node.js development, the Bot Builder for Teams functionality is incorporated into the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) v4.6.</span></span>

## <a name="fetch-the-team-roster"></a><span data-ttu-id="ddff1-110">提取团队名单</span><span class="sxs-lookup"><span data-stu-id="ddff1-110">Fetch the team roster</span></span>

<span data-ttu-id="ddff1-111">机器人可以查询团队成员及其基本个人资料的列表。</span><span class="sxs-lookup"><span data-stu-id="ddff1-111">Your bot can query for the list of team members and their basic profiles.</span></span> <span data-ttu-id="ddff1-112">基本配置文件包括 Teams 用户 ID 和 Azure Active Directory (AAD) 名称和对象 ID 等信息。</span><span class="sxs-lookup"><span data-stu-id="ddff1-112">The basic profiles include Teams user IDs and Azure Active Directory (AAD) information such as name and object ID.</span></span> <span data-ttu-id="ddff1-113">可以使用此信息来关联用户标识。</span><span class="sxs-lookup"><span data-stu-id="ddff1-113">You can use this information to correlate user identities.</span></span> <span data-ttu-id="ddff1-114">例如，检查通过 AAD 凭据登录选项卡的用户是否为团队成员。</span><span class="sxs-lookup"><span data-stu-id="ddff1-114">For example, check if a user logged into a tab through AAD credentials is a team member.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="ddff1-115">REST API 示例</span><span class="sxs-lookup"><span data-stu-id="ddff1-115">REST API example</span></span>

<span data-ttu-id="ddff1-116">直接在 上发出 GET 请求 [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) ，使用 `serviceUrl` 值作为终结点。</span><span class="sxs-lookup"><span data-stu-id="ddff1-116">Directly issue a GET request on [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="ddff1-117">可以在自动程序在下列情况下接收的活动有效负载的对象 `teamId` `channeldata` 中找到 ：</span><span class="sxs-lookup"><span data-stu-id="ddff1-117">The `teamId` can be found in the `channeldata` object of the activity payload that your bot receives in the following scenarios:</span></span>

* <span data-ttu-id="ddff1-118">当用户在团队上下文中向机器人发送消息或与之交互时。</span><span class="sxs-lookup"><span data-stu-id="ddff1-118">When a user messages or interacts with your bot in a team context.</span></span> <span data-ttu-id="ddff1-119">有关详细信息，请参阅 [接收邮件](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)。</span><span class="sxs-lookup"><span data-stu-id="ddff1-119">For more information, see [receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages).</span></span>
* <span data-ttu-id="ddff1-120">将新用户或机器人添加到团队时。</span><span class="sxs-lookup"><span data-stu-id="ddff1-120">When a new user or bot is added to a team.</span></span> <span data-ttu-id="ddff1-121">有关详细信息，请参阅添加到 [团队的机器人或用户](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)。</span><span class="sxs-lookup"><span data-stu-id="ddff1-121">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team).</span></span>

> [!NOTE]
>
>* <span data-ttu-id="ddff1-122">调用 API 时始终使用团队 ID。</span><span class="sxs-lookup"><span data-stu-id="ddff1-122">Always use the team ID when calling the API.</span></span>
>* <span data-ttu-id="ddff1-123">`serviceUrl`值往往很稳定，但可能会更改。</span><span class="sxs-lookup"><span data-stu-id="ddff1-123">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="ddff1-124">当新消息到达时，机器人必须验证其存储 `serviceUrl` 值。</span><span class="sxs-lookup"><span data-stu-id="ddff1-124">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

```json
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members

Response body
[{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
    "givenName": "Larry",
    "surname": "Brown",
    "email": "Larry.Brown@fabrikam.com",
    "userPrincipalName": "labrown@fabrikam.com"
}, {
    "id": "29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
    "objectId": "76b0b09f-d410-48fd-993e-84da521a597b",
    "givenName": "John",
    "surname": "Patterson",
    "email": "johnp@fabrikam.com",
    "userPrincipalName": "johnp@fabrikam.com"
}, {
    "id": "29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
    "objectId": "6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
    "givenName": "Rick",
    "surname": "Stevens",
    "email": "Rick.Stevens@fabrikam.com",
    "userPrincipalName": "rstevens@fabrikam.com"
}]
```

### <a name="net-example"></a><span data-ttu-id="ddff1-125">.NET 示例</span><span class="sxs-lookup"><span data-stu-id="ddff1-125">.NET example</span></span>

<span data-ttu-id="ddff1-126">调用 `GetConversationMembersAsync` using `Team.Id` 可返回用户 ID 列表。</span><span class="sxs-lookup"><span data-stu-id="ddff1-126">Call `GetConversationMembersAsync` using `Team.Id` to return a list of user IDs.</span></span>

```csharp
// Fetch the members in the current conversation
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));
var teamId = context.Activity.GetChannelData<TeamsChannelData>().Team.Id;
var members = await connector.Conversations.GetConversationMembersAsync(teamId);

// Concatenate information about all members into a string
var sb = new StringBuilder();
foreach (var member in members.AsTeamsChannelAccounts())
{
    sb.AppendFormat(
        "GivenName = {0}, TeamsMemberId = {1}",
        member.Name, member.Id);

    sb.AppendLine();
}

// Post the member info back into the conversation
await context.PostAsync($"People in this conversation: {sb.ToString()}");
```

### <a name="nodejs-or-typescript-example"></a><span data-ttu-id="ddff1-127">Node.js或 TypeScript 示例</span><span class="sxs-lookup"><span data-stu-id="ddff1-127">Node.js or TypeScript example</span></span>

```typescript

[...]
import * as builder from "botbuilder";
[...]

var teamId = session.message.sourceEvent.team.id;
connector.fetchMembers(
  (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
  teamId,
  (err, result) => {
    if (err) {
      session.endDialog('There is some error');
    }
    else {
      session.endDialog('%s', JSON.stringify(result));
    }
  }
);
```

<span data-ttu-id="ddff1-128">另请参阅 [Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="ddff1-128">Also, see [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a><span data-ttu-id="ddff1-129">在个人或群组聊天中提取用户配置文件或名单</span><span class="sxs-lookup"><span data-stu-id="ddff1-129">Fetch user profile or roster in personal or group chat</span></span>

<span data-ttu-id="ddff1-130">你可以对任意个人聊天进行 API 调用，以获取与机器人聊天的用户的个人资料信息。</span><span class="sxs-lookup"><span data-stu-id="ddff1-130">You can make the API call for any personal chat to obtain the profile information of the user chatting with your bot.</span></span>

<span data-ttu-id="ddff1-131">API 调用、SDK 方法和响应对象与提取团队名单完全相同。</span><span class="sxs-lookup"><span data-stu-id="ddff1-131">The API call, SDK methods, and the response object are identical to fetching the team roster.</span></span> <span data-ttu-id="ddff1-132">唯一的区别是传递 `conversationId` ，而不是 `teamId` 传递 。</span><span class="sxs-lookup"><span data-stu-id="ddff1-132">The only difference is you pass the `conversationId` instead of the `teamId`.</span></span>

## <a name="fetch-the-list-of-channels-in-a-team"></a><span data-ttu-id="ddff1-133">获取团队中的频道列表</span><span class="sxs-lookup"><span data-stu-id="ddff1-133">Fetch the list of channels in a team</span></span>

<span data-ttu-id="ddff1-134">机器人可以查询团队中的频道列表。</span><span class="sxs-lookup"><span data-stu-id="ddff1-134">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="ddff1-135">返回默认"常规"频道的名称， `null` 以允许本地化。</span><span class="sxs-lookup"><span data-stu-id="ddff1-135">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="ddff1-136">常规频道的频道 ID 始终与团队 ID 匹配。</span><span class="sxs-lookup"><span data-stu-id="ddff1-136">The channel ID for the General channel always matches the team ID.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="ddff1-137">REST API 示例</span><span class="sxs-lookup"><span data-stu-id="ddff1-137">REST API example</span></span>

<span data-ttu-id="ddff1-138">直接在 上发出 GET 请求 `/teams/{teamId}/conversations/` ，使用 `serviceUrl` 值作为终结点。</span><span class="sxs-lookup"><span data-stu-id="ddff1-138">Directly issue a GET request on `/teams/{teamId}/conversations/`, using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="ddff1-139">的唯一 `teamId` 来源是团队上下文中的消息。</span><span class="sxs-lookup"><span data-stu-id="ddff1-139">The only source for `teamId` is a message from the team context.</span></span> <span data-ttu-id="ddff1-140">该消息可以是来自用户的消息，或者是机器人在添加到团队时收到的消息。</span><span class="sxs-lookup"><span data-stu-id="ddff1-140">The message is either a message from a user or the message that your bot receives when it is added to a team.</span></span> <span data-ttu-id="ddff1-141">有关详细信息，请参阅添加到 [团队的机器人或用户](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)。</span><span class="sxs-lookup"><span data-stu-id="ddff1-141">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition).</span></span>

> [!NOTE]
> <span data-ttu-id="ddff1-142">`serviceUrl`值往往很稳定，但可能会更改。</span><span class="sxs-lookup"><span data-stu-id="ddff1-142">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="ddff1-143">当新消息到达时，机器人必须验证其存储 `serviceUrl` 值。</span><span class="sxs-lookup"><span data-stu-id="ddff1-143">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

```json
GET /v3/teams/19%3A033451497ea84fcc83d17ed7fb08a1b6%40thread.skype/conversations

Response body
{
    "conversations": [{
        "id": "19:033451497ea84fcc83d17ed7fb08a1b6@thread.skype",
        "name": null
    }, {
        "id": "19:cc25e4aae50746ecbb11473bba24c70a@thread.skype",
        "name": "Materials"
    }, {
        "id": "19:b7b84cba410c406ba671dbbf5e0a3519@thread.skype",
        "name": "Design"
    }, {
        "id": "19:fc5db2aed489454e8f8c06829ed6c986@thread.skype",
        "name": "Marketing"
    }]
}
```

#### <a name="net-example"></a><span data-ttu-id="ddff1-144">.NET 示例</span><span class="sxs-lookup"><span data-stu-id="ddff1-144">.NET example</span></span>

<span data-ttu-id="ddff1-145">以下示例使用来自适用于 `FetchChannelList` .NET 的 Bot Builder SDK 的 Teams [扩展的调用](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)：</span><span class="sxs-lookup"><span data-stu-id="ddff1-145">The following example uses the `FetchChannelList` call from the [Teams extensions for the Bot Builder SDK for .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span></span>

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a><span data-ttu-id="ddff1-146">Node.js示例</span><span class="sxs-lookup"><span data-stu-id="ddff1-146">Node.js example</span></span>

<span data-ttu-id="ddff1-147">以下示例使用 Teams `fetchChannelList` 扩展中的 [适用于 ](https://www.npmjs.com/package/botbuilder-teams)自动程序生成器 SDK 的Node.js：</span><span class="sxs-lookup"><span data-stu-id="ddff1-147">The following example uses `fetchChannelList` call from the [Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams):</span></span>

```javascript
var teamId = session.message.sourceEvent.team.id;
connector.fetchChannelList(
  (session.message.address).serviceUrl,
  teamId,
  (err, result) => {
    if (err) {
      session.endDialog('There is an error');
    }
    else {
      session.endDialog('%s', JSON.stringify(result));
    }
  }
);
```

## <a name="get-clientinfo-in-your-bot-context"></a><span data-ttu-id="ddff1-148">在自动程序上下文中获取 clientInfo</span><span class="sxs-lookup"><span data-stu-id="ddff1-148">Get clientInfo in your bot context</span></span>

<span data-ttu-id="ddff1-149">可以在自动程序的活动内获取 clientInfo。</span><span class="sxs-lookup"><span data-stu-id="ddff1-149">You can fetch the clientInfo within your bot's activity.</span></span> <span data-ttu-id="ddff1-150">clientInfo 包含以下属性：</span><span class="sxs-lookup"><span data-stu-id="ddff1-150">The clientInfo contains the following properties:</span></span>

* <span data-ttu-id="ddff1-151">Locale</span><span class="sxs-lookup"><span data-stu-id="ddff1-151">Locale</span></span>
* <span data-ttu-id="ddff1-152">国家/地区</span><span class="sxs-lookup"><span data-stu-id="ddff1-152">Country</span></span>
* <span data-ttu-id="ddff1-153">平台</span><span class="sxs-lookup"><span data-stu-id="ddff1-153">Platform</span></span>
* <span data-ttu-id="ddff1-154">Timezone</span><span class="sxs-lookup"><span data-stu-id="ddff1-154">Timezone</span></span>

### <a name="json-example"></a><span data-ttu-id="ddff1-155">JSON 示例</span><span class="sxs-lookup"><span data-stu-id="ddff1-155">JSON example</span></span>

```json
[
    {
        "type": "clientInfo",
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "Asia/Calcutta"
    }
]
```

### <a name="c-example"></a><span data-ttu-id="ddff1-156">C#示例</span><span class="sxs-lookup"><span data-stu-id="ddff1-156">C# example</span></span>

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```
