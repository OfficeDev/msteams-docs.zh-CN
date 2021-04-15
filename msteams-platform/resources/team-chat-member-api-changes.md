---
title: 为团队和聊天成更改机器人 API
author: ojasvichoudhary
description: 介绍即将对用于检索团队和聊天成员的 Bot API 进行的更改和进行中的更改
keywords: 机器人框架 apis 团队成员名单
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: 38ccdd1d3052e906ceacaa47fa0cd14a1be7a41d
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696517"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a><span data-ttu-id="4d7a6-104">Teams 机器人 API 更改以提取团队或聊天成员</span><span class="sxs-lookup"><span data-stu-id="4d7a6-104">Teams bot API changes to fetch team or chat members</span></span>

>[!NOTE]
> <span data-ttu-id="4d7a6-105">和 API 的弃用 `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` 过程已启动。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-105">The deprecation process for `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs have started.</span></span> <span data-ttu-id="4d7a6-106">最初，它们被严格限制为每分钟五个请求，并且每个团队最多返回 10，000 个成员。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-106">Initially, they are heavily throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="4d7a6-107">这样，随着团队规模增加，不会返回全部名单。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-107">This results in the full roster not being returned as team size increases.</span></span>
> <span data-ttu-id="4d7a6-108">必须更新到 4.10 版或更高版本的 Bot Framework SDK，并切换到分页 API 终结点或 `TeamsInfo.GetMemberAsync` 单个用户 API。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-108">You must update to version 4.10 or higher of the Bot Framework SDK and switch to the paginated API endpoints, or the `TeamsInfo.GetMemberAsync` single user API.</span></span> <span data-ttu-id="4d7a6-109">这也适用于自动程序，即使你未直接使用这些 API，因为较旧的 SDK 在 [membersAdded](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) 事件期间调用这些 API。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-109">This also applies to your bot even if you are not directly using these APIs, as older SDKs call these APIs during [membersAdded](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) events.</span></span> <span data-ttu-id="4d7a6-110">若要查看即将进行的更改的列表，请参阅 API [更改](team-chat-member-api-changes.md#api-changes)。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-110">To view the list of upcoming changes, see [API changes](team-chat-member-api-changes.md#api-changes).</span></span> 

<span data-ttu-id="4d7a6-111">目前，想要检索聊天或团队的一个或多个成员信息的聊天机器人开发人员使用适用于 C# 或 TypeScript 或 Node.js API 的 Microsoft Teams `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` 自动程序 API。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-111">Currently, bot developers who want to retrieve information for one or more members of a chat or team use the Microsoft Teams bot APIs `TeamsInfo.GetMembersAsync` for C# or `TeamsInfo.getMembers` for TypeScript or Node.js APIs.</span></span> <span data-ttu-id="4d7a6-112">有关详细信息，请参阅提取 [名单或用户配置文件](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-112">For more information, see [fetch roster or user profile](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile).</span></span> <span data-ttu-id="4d7a6-113">这些 API 存在一些缺点。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-113">These APIs have several shortcomings.</span></span>

<span data-ttu-id="4d7a6-114">目前，如果你想要检索聊天或团队的一个或多个成员的信息，可以使用适用于 C# 或 TypeScript 或 Node.js API 的 [Microsoft Teams](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` 自动程序 API。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-114">Currently, if you want to retrieve information for one or more members of a chat or team, you can use the [Microsoft Teams bot APIs](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) `TeamsInfo.GetMembersAsync` for C# or `TeamsInfo.getMembers` for TypeScript or Node.js APIs.</span></span> <span data-ttu-id="4d7a6-115">这些 API 有以下缺点：</span><span class="sxs-lookup"><span data-stu-id="4d7a6-115">These APIs have the following shortcomings:</span></span>

* <span data-ttu-id="4d7a6-116">对于大型团队，性能较差且超时的可能性较大：自 2017 年初发布 Teams 以来，最大团队规模已大幅提升。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-116">For large teams, performance is poor and timeouts are more likely: The maximum team size has grown considerably since Teams was released in early 2017.</span></span> <span data-ttu-id="4d7a6-117">作为或返回整个成员列表，对于大型团队，API 调用需要很长时间来返回，并且调用通常要过长，必须 `GetMembersAsync` `getMembers` 重试。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-117">As `GetMembersAsync` or `getMembers` returns the entire member list, it takes a long time for the API call to return for large teams, and it is common for the call to time out and you have to try again.</span></span>
* <span data-ttu-id="4d7a6-118">获取单个用户的配置文件详细信息非常困难：若要获取单个用户的配置文件信息，您必须检索整个成员列表，然后搜索您想要的成员列表。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-118">Getting profile details for a single user is difficult: To get the profile information for a single user, you have to retrieve the entire member list and then search for the one you want.</span></span> <span data-ttu-id="4d7a6-119">Bot Framework SDK 中提供了一个帮助程序函数，使其更简单，但效率并不高。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-119">There is a helper function in the Bot Framework SDK to make it simpler, but it is not efficient.</span></span>

<span data-ttu-id="4d7a6-120">随着组织范围的团队的引入，需要更好地使这些 API 与 Office 365 隐私控制保持一致。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-120">With the introduction of organization wide teams, there is a requirement to better align these APIs with Office 365 privacy controls.</span></span> <span data-ttu-id="4d7a6-121">大型团队中使用的机器人能够检索类似于 Microsoft Graph 权限 `User.ReadBasic.All` 的基本个人资料信息。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-121">Bots used in large teams are able to retrieve basic profile information similar to the `User.ReadBasic.All` Microsoft Graph permission.</span></span> <span data-ttu-id="4d7a6-122">租户管理员可大量控制哪些应用和机器人可以在租户中使用，但这些设置不同于 Microsoft Graph。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-122">Tenant administrators have a great deal of control over which apps and bots can be used in their tenant, but these settings are different from Microsoft Graph.</span></span>

<span data-ttu-id="4d7a6-123">以下代码提供了 Teams 机器人 API 返回内容的示例 JSON 表示形式：</span><span class="sxs-lookup"><span data-stu-id="4d7a6-123">The following code provides a sample JSON representation of what is returned by Teams bot APIs:</span></span>

```json
[{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "Anon1 (Guest)",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
    "userRole": "anonymous"
}, {
    "id": "29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
    "objectId": "76b0b09f-d410-48fd-993e-84da521a597b",
    "givenName": "John",
    "surname": "Patterson",
    "email": "johnp@fabrikam.com",
    "userPrincipalName": "johnp@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
    "userRole": "user"
}, {
    "id": "29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
    "objectId": "6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
    "givenName": "Rick",
    "surname": "Stevens",
    "email": "Rick.Stevens@fabrikam.com",
    "userPrincipalName": "rstevens@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
    "userRole": "user"
}]
```

## <a name="api-changes"></a><span data-ttu-id="4d7a6-124">API 更改</span><span class="sxs-lookup"><span data-stu-id="4d7a6-124">API Changes</span></span>

<span data-ttu-id="4d7a6-125">以下是即将推出的 API 更改：</span><span class="sxs-lookup"><span data-stu-id="4d7a6-125">Following are the upcoming API changes:</span></span>

* <span data-ttu-id="4d7a6-126">将创建一个新的 [`TeamsInfo.GetPagedMembersAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) API，用于检索聊天或团队成员的配置文件信息。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-126">A new API is created [`TeamsInfo.GetPagedMembersAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) for retrieving profile information for members of a chat or team.</span></span> <span data-ttu-id="4d7a6-127">此 API 现已与 Bot Framework 4.8 SDK 一起提供。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-127">This API is now available with the Bot Framework 4.8 SDK.</span></span> <span data-ttu-id="4d7a6-128">对于所有其他版本中的开发，请使用 [`GetConversationPagedMembers`](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) 方法。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-128">For development in all other versions, use the [`GetConversationPagedMembers`](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) method.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4d7a6-129">在 v3 或 v4 中，最佳操作是升级到分别为 3.30.2 或 4.8 的最新点版本。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-129">In either v3 or v4, the best action is to upgrade to the latest point release that is 3.30.2 or 4.8 respectively.</span></span>

* <span data-ttu-id="4d7a6-130">将创建一个新的 [`TeamsInfo.GetMemberAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) API，用于检索单个用户的配置文件信息。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-130">A new API is created [`TeamsInfo.GetMemberAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) for retrieving the profile information for a single user.</span></span> <span data-ttu-id="4d7a6-131">它将团队或聊天的 ID 和 [UPN（](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) 即 Azure Active Directory 对象 ID）或 Teams 用户 ID 作为参数，并返回该用户 `userPrincipalName` `objectId` `id` 的个人资料信息。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-131">It takes the ID of the team or chat and a [UPN](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) that is `userPrincipalName`, Azure Active Directory Object ID `objectId`, or the Teams user ID `id` as parameters and returns the profile information for that user.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4d7a6-132">`objectId` 更改为匹配 `aadObjectId` Bot Framework 消息的对象 `Activity` 中调用的对象。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-132">`objectId` is changed to `aadObjectId` to match what is called in the `Activity` object of a Bot Framework message.</span></span> <span data-ttu-id="4d7a6-133">新 API 适用于 Bot Framework SDK 版本 4.8。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-133">The new API is available with version 4.8 of the Bot Framework SDK.</span></span> <span data-ttu-id="4d7a6-134">它还在 Teams SDK 扩展 Bot Framework 3.x 中提供。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-134">It is also available in the Teams SDK extension Bot Framework 3.x.</span></span> <span data-ttu-id="4d7a6-135">同时，您可以使用 [REST](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) 终结点。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-135">Meanwhile, you can use the [REST](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) endpoint.</span></span>

* <span data-ttu-id="4d7a6-136">`TeamsInfo.GetMembersAsync` 中C# TypeScript 或 `TeamsInfo.getMembers` Node.js已正式弃用。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-136">`TeamsInfo.GetMembersAsync` in C# and `TeamsInfo.getMembers` in TypeScript or Node.js is formally deprecated.</span></span> <span data-ttu-id="4d7a6-137">新 API 可用后，必须更新机器人以使用它。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-137">Once the new API is available, you must update your bots to use it.</span></span> <span data-ttu-id="4d7a6-138">这也适用于这些 API[使用的基础 REST API。](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)</span><span class="sxs-lookup"><span data-stu-id="4d7a6-138">This also applies to the [underlying REST API that these APIs use](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json).</span></span>
* <span data-ttu-id="4d7a6-139">到 2021 年底，聊天机器人无法主动检索 `userPrincipalName` 聊天或 `email` 团队成员的 或 属性。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-139">By late 2021, bots cannot proactively retrieve the `userPrincipalName` or `email` properties for members of a chat or team.</span></span> <span data-ttu-id="4d7a6-140">机器人必须使用 Graph 来检索它们。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-140">Bots must use Graph to retrieve them.</span></span> <span data-ttu-id="4d7a6-141">从 `userPrincipalName` `email` `GetConversationPagedMembers` 2021 年后期开始，不会从新 API 返回 和 属性。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-141">The `userPrincipalName` and `email` properties are not returned from the new `GetConversationPagedMembers` API starting in late 2021.</span></span> <span data-ttu-id="4d7a6-142">机器人必须借助访问令牌使用 Graph 来检索信息。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-142">Bots have to use Graph with an access token to retrieve information.</span></span> <span data-ttu-id="4d7a6-143">机器人必须更轻松地获取访问令牌，并简化和简化最终用户同意过程。</span><span class="sxs-lookup"><span data-stu-id="4d7a6-143">It must be made easier for bots to get an access token and streamline and simplify the end-user consent process.</span></span>
