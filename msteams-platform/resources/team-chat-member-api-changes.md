---
title: 为团队和聊天成更改机器人 API
author: ojasvichoudhary
description: 介绍即将对用于检索团队和聊天成员的 Bot API 进行的更改和进行中的更改
keywords: 机器人框架 apis 团队成员名单
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: d55cbcdfea5e374c151c3eec82c52ac7f434c153
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034688"
---
# <a name="changes-to-teams-bot-apis-for-fetching-team-and-chat-members"></a><span data-ttu-id="6024c-104">对用于提取团队和聊天成员的 Teams 自动程序 API 的更改</span><span class="sxs-lookup"><span data-stu-id="6024c-104">Changes to Teams bot APIs for fetching team and chat members</span></span>

>[!NOTE]
> <span data-ttu-id="6024c-105">我们开始使用和 API 的弃 `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` 用过程。</span><span class="sxs-lookup"><span data-stu-id="6024c-105">We've started with the deprecation process for `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs.</span></span> <span data-ttu-id="6024c-106">最初，它们将被严格限制为每分钟 5 个请求，并且每个团队最多返回 10，000 个成员。</span><span class="sxs-lookup"><span data-stu-id="6024c-106">Initially, they will be heavily throttled to 5 requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="6024c-107">这样，随着团队规模增加，将不会返回整个名单。</span><span class="sxs-lookup"><span data-stu-id="6024c-107">This will result in the full roster not being returned as team size increases.</span></span> 
> 
> <span data-ttu-id="6024c-108">**必须更新到 4.10** 版或更高版本的 Bot Framework SDK，并切换到分页 API 终结点或 `TeamsInfo.GetMemberAsync` 单个用户 API。</span><span class="sxs-lookup"><span data-stu-id="6024c-108">**You must update to version 4.10 or higher of the Bot Framework SDK** and switch to the paginated API endpoints, or the `TeamsInfo.GetMemberAsync` single user API.</span></span> <span data-ttu-id="6024c-109">这也适用于自动程序，即使你没有直接使用这些 API，因为较旧的 SDK 在 [membersAdded](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) 事件期间调用这些 API。</span><span class="sxs-lookup"><span data-stu-id="6024c-109">This also applies to your bot even if you're not directly using these APIs, as older SDKs call these APIs during [membersAdded](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) events.</span></span> <span data-ttu-id="6024c-110">若要查看即将进行的更改的列表，请参阅 API [更改](team-chat-member-api-changes.md#api-changes)。</span><span class="sxs-lookup"><span data-stu-id="6024c-110">To view the list of upcoming changes, see [API changes](team-chat-member-api-changes.md#api-changes).</span></span> 

<span data-ttu-id="6024c-111">目前，想要检索聊天或团队的一个或多个成员信息的聊天机器人开发人员使用 microsoft Teams 自动程序 API (for C#) 或 `TeamsInfo.GetMembersAsync` (`TeamsInfo.getMembers` for TypeScript/Node.js) API [ (](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile)记录在此处) 。</span><span class="sxs-lookup"><span data-stu-id="6024c-111">Currently, bot developers who want to retrieve information for one or more members of a chat or team use the Microsoft Teams bot APIs `TeamsInfo.GetMembersAsync` (for C#) or `TeamsInfo.getMembers` (for TypeScript/Node.js) APIs [(documented here)](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile).</span></span> <span data-ttu-id="6024c-112">这些 API 现在存在一些缺点：</span><span class="sxs-lookup"><span data-stu-id="6024c-112">These APIs have several shortcomings today:</span></span>

* <span data-ttu-id="6024c-113">**对于大型团队，性能较差，超时的可能性较大。**</span><span class="sxs-lookup"><span data-stu-id="6024c-113">**For large teams, performance is poor and timeouts are more likely.**</span></span> <span data-ttu-id="6024c-114">自 Microsoft Teams 于 2017 年初发布以来，最大团队规模已大幅提升。</span><span class="sxs-lookup"><span data-stu-id="6024c-114">The maximum team size has grown considerably since Microsoft Teams was released in early 2017.</span></span> <span data-ttu-id="6024c-115">由于 `GetMembersAsync` 返回整个成员列表，因此 API 调用需要很长时间来为大型团队返回，并且调用会花费很长时间来退出，因此必须 / `getMembers` 重试。</span><span class="sxs-lookup"><span data-stu-id="6024c-115">Since `GetMembersAsync`/`getMembers` returns the entire member list, it takes a long time for the API call to return for large teams, and it’s not uncommon for the call to time out and you have to try again.</span></span>
* <span data-ttu-id="6024c-116">**获取单个用户的配置文件详细信息很麻烦。**</span><span class="sxs-lookup"><span data-stu-id="6024c-116">**Getting profile details for a single user is cumbersome.**</span></span> <span data-ttu-id="6024c-117">若要获取单个用户的配置文件信息，您必须检索整个成员列表，然后搜索您想要的成员列表。</span><span class="sxs-lookup"><span data-stu-id="6024c-117">To get the profile information for a single user, you have to retrieve the entire member list and then search for the one you want.</span></span> <span data-ttu-id="6024c-118">如果为 True，则 Bot Framework SDK 中提供了帮助程序函数，使其更简单，但实际上效率并不高。</span><span class="sxs-lookup"><span data-stu-id="6024c-118">True, there’s a helper function in the Bot Framework SDK to make it simpler, but under the covers it’s not efficient.</span></span>

<span data-ttu-id="6024c-119">另外，随着组织范围的团队的引入，我们意识到应该更好地将这些 API 与 Office 365 隐私控件保持一致：大型团队中使用的机器人能够检索基本个人资料信息，这类似于 Microsoft Graph 权限。 `User.ReadBasic.All`</span><span class="sxs-lookup"><span data-stu-id="6024c-119">Separately, with the introduction of org-wide teams, we realized it was time to better align these APIs with Office 365 privacy controls: bots used in large teams are able to retrieve basic profile information, which is similar to the `User.ReadBasic.All` Microsoft Graph permission.</span></span> <span data-ttu-id="6024c-120">租户管理员可大量控制哪些应用和机器人可以在租户中使用，但这些设置不同于管理 Microsoft Graph 的设置。</span><span class="sxs-lookup"><span data-stu-id="6024c-120">Tenant administrators have a great deal of control over which apps and bots can be used in their tenant, but these settings are different than the ones governing Microsoft Graph.</span></span>

<span data-ttu-id="6024c-121">下面是这些 API 今天返回的示例 JSON 表示形式。</span><span class="sxs-lookup"><span data-stu-id="6024c-121">Here’s a sample JSON representation of what’s returned by these APIs today.</span></span> <span data-ttu-id="6024c-122">我将参考下面的一些字段。</span><span class="sxs-lookup"><span data-stu-id="6024c-122">I’ll refer to some of the fields below.</span></span>

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

## <a name="api-changes"></a><span data-ttu-id="6024c-123">API 更改</span><span class="sxs-lookup"><span data-stu-id="6024c-123">API Changes</span></span>
<span data-ttu-id="6024c-124">下面是即将推出的 API 更改：</span><span class="sxs-lookup"><span data-stu-id="6024c-124">Here are the upcoming API changes:</span></span>

* <span data-ttu-id="6024c-125">我们创建了一个新的 [`TeamsInfo.GetPagedMembersAsync`](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile) API，用于检索聊天/团队成员的个人资料信息。</span><span class="sxs-lookup"><span data-stu-id="6024c-125">We've created a new API [`TeamsInfo.GetPagedMembersAsync`](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile) for retrieving profile information for members of a chat/team.</span></span> <span data-ttu-id="6024c-126">此 API 现已与 Bot Framework 4.10 SDK 一起提供。</span><span class="sxs-lookup"><span data-stu-id="6024c-126">This API is now available with the Bot Framework 4.10 SDK.</span></span> <span data-ttu-id="6024c-127">对于所有其他版本中的开发，请使用 [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) 方法。</span><span class="sxs-lookup"><span data-stu-id="6024c-127">For development in all other versions use the [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) method.</span></span> 
  > [!NOTE]
  > <span data-ttu-id="6024c-128">在 v3 或 v4 中，最佳操作是升级到最新点版本。</span><span class="sxs-lookup"><span data-stu-id="6024c-128">In either v3 or v4, the best action is to upgrade to the latest point release.</span></span> 
* <span data-ttu-id="6024c-129">我们创建了一个新的 [`TeamsInfo.GetMemberAsync`](../bots/how-to/get-teams-context.md#get-single-member-details) API，用于检索单个用户的配置文件信息。</span><span class="sxs-lookup"><span data-stu-id="6024c-129">We've created a new API [`TeamsInfo.GetMemberAsync`](../bots/how-to/get-teams-context.md#get-single-member-details) for retrieving the profile information for a single user.</span></span> <span data-ttu-id="6024c-130">它将团队/聊天的 ID 和[UPN](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) (（请参阅上面的 `userPrincipalName`) 、Azure Active Directory 对象ID (、) 或 Teams 用户 ID `objectId` (，请参阅上面的 `id`) 作为参数，并返回该用户的配置文件信息。</span><span class="sxs-lookup"><span data-stu-id="6024c-130">It takes the ID of the team/chat and a [UPN](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) (`userPrincipalName`, *see above*), Azure Active Directory Object ID (`objectId`, *see above*), or the Teams user ID (`id`, *see above*) as parameters and returns the profile information for that user.</span></span> 
  > [!NOTE]
  > <span data-ttu-id="6024c-131">我们正在更改 `objectId` 以匹配在 Bot Framework 消息的对象 `aadObjectId` `Activity` 中调用的对象。</span><span class="sxs-lookup"><span data-stu-id="6024c-131">We're changing `objectId` to `aadObjectId` to match what it's called in the `Activity` object of a Bot Framework message.</span></span> <span data-ttu-id="6024c-132">新 API 适用于 Bot Framework SDK 版本 4.10。</span><span class="sxs-lookup"><span data-stu-id="6024c-132">The new API is available with version 4.10 of the Bot Framework SDK.</span></span> <span data-ttu-id="6024c-133">它将很快在 Teams SDK 扩展 Bot Framework 3.x 中提供;，您可以使用 [REST](../bots/how-to/get-teams-context.md?get-single-member-details) 终结点。</span><span class="sxs-lookup"><span data-stu-id="6024c-133">It will soon be available in the Teams SDK extension Bot Framework 3.x as well; meanwhile you can use the [REST](../bots/how-to/get-teams-context.md?get-single-member-details) endpoint.</span></span>
* <span data-ttu-id="6024c-134">`TeamsInfo.GetMembersAsync` (C#)  (TypeScript/Node.js) 已正式弃用，并 `TeamsInfo.getMembers` 将于 2021 年后期停止工作。</span><span class="sxs-lookup"><span data-stu-id="6024c-134">`TeamsInfo.GetMembersAsync` (C#) and `TeamsInfo.getMembers` (TypeScript/Node.js) is formally deprecated and will stop working in late 2021.</span></span> <span data-ttu-id="6024c-135">Please update your bots to use the paged APIs.</span><span class="sxs-lookup"><span data-stu-id="6024c-135">Please update your bots to use the paged APIs.</span></span> <span data-ttu-id="6024c-136"> (这也适用于这些 API 使用 [.) ](../bots/how-to/get-teams-context.md)的基础 REST API</span><span class="sxs-lookup"><span data-stu-id="6024c-136">(This also applies to the [underlying REST API these APIs use](../bots/how-to/get-teams-context.md).)</span></span>
* <span data-ttu-id="6024c-137">到 2021 年底，聊天机器人将无法主动检索聊天/团队成员的 或 属性，并且将需要使用 Microsoft Graph 来 `userPrincipalName` `email` 检索它们。</span><span class="sxs-lookup"><span data-stu-id="6024c-137">By late 2021, bots will not be able to proactively retrieve the `userPrincipalName` or `email` properties for members of a chat/team and will need to use Microsoft Graph to retrieve them.</span></span> <span data-ttu-id="6024c-138">具体而言 `userPrincipalName` ， `email` 自 2021 年后期起，将不会从新 API 返回 `GetConversationPagedMembers` 属性。</span><span class="sxs-lookup"><span data-stu-id="6024c-138">Specifically, `userPrincipalName` and `email` properties won't be returned from the new `GetConversationPagedMembers` API starting in late 2021.</span></span> <span data-ttu-id="6024c-139">机器人必须借助访问令牌使用 Microsoft Graph 来检索此信息。</span><span class="sxs-lookup"><span data-stu-id="6024c-139">Bots will have to use Microsoft Graph with an access token to retrieve this information.</span></span> <span data-ttu-id="6024c-140">这明显是一个主要更改：我们必须让机器人更轻松地获取访问令牌，并且必须简化和简化最终用户同意过程。</span><span class="sxs-lookup"><span data-stu-id="6024c-140">This is obviously a major change: We must make it easier for bots to get an access token, and we must streamline and simplify the end-user consent process.</span></span>

## <a name="feedback-and-more-information"></a><span data-ttu-id="6024c-141">反馈和详细信息</span><span class="sxs-lookup"><span data-stu-id="6024c-141">Feedback and More Information</span></span>
<span data-ttu-id="6024c-142">我们将使用此页提供有关这些更改最新信息。</span><span class="sxs-lookup"><span data-stu-id="6024c-142">We'll use this page for providing up to date information on these changes.</span></span> <span data-ttu-id="6024c-143">如果你有问题，请使用以下反馈部分>在此页面上发送 **反馈** "。</span><span class="sxs-lookup"><span data-stu-id="6024c-143">If you have questions, use the "Send feedback > on this page" in the **Feedback** section below.</span></span> 
