---
title: 使用 Microsoft Graph 将外部平台邮件导入到团队
description: 介绍如何使用 Microsoft Graph 将邮件从外部平台导入到团队
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: 团队导入邮件 api 图 microsoft 迁移迁移发布
ms.openlocfilehash: 0f53e27ec849e18be49f233a754658587343f68b
ms.sourcegitcommit: 25afe104d10c9a6a2849decf5ec1d08969d827c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2020
ms.locfileid: "48465906"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="12874-104">使用 Microsoft Graph 将第三方平台消息导入 Teams</span><span class="sxs-lookup"><span data-stu-id="12874-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="12874-105">Microsoft Graph 和 Microsoft 团队公开预览版适用于早期访问和反馈。</span><span class="sxs-lookup"><span data-stu-id="12874-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="12874-106">尽管此版本已经历大量测试，但不适合在生产中使用。</span><span class="sxs-lookup"><span data-stu-id="12874-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="12874-107">使用 Microsoft Graph，可以将用户的现有邮件历史记录和数据从外部系统迁移到团队频道。</span><span class="sxs-lookup"><span data-stu-id="12874-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="12874-108">通过在团队内启用第三方平台邮件传递层次结构，用户可以采用无缝方式继续进行通信并继续进行而不会中断。</span><span class="sxs-lookup"><span data-stu-id="12874-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="12874-109">导入概述</span><span class="sxs-lookup"><span data-stu-id="12874-109">Import overview</span></span>

<span data-ttu-id="12874-110">从较高的层次来看，导入过程包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="12874-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="12874-111">创建具有后时间戳的团队</span><span class="sxs-lookup"><span data-stu-id="12874-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="12874-112">使用后向时间戳创建通道</span><span class="sxs-lookup"><span data-stu-id="12874-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="12874-113">导入外部定期邮件</span><span class="sxs-lookup"><span data-stu-id="12874-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="12874-114">完成团队和渠道迁移过程</span><span class="sxs-lookup"><span data-stu-id="12874-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="12874-115">添加团队成员</span><span class="sxs-lookup"><span data-stu-id="12874-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="12874-116">必需的要求</span><span class="sxs-lookup"><span data-stu-id="12874-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="12874-117">分析和准备邮件数据</span><span class="sxs-lookup"><span data-stu-id="12874-117">Analyze and prepare message data</span></span>

<span data-ttu-id="12874-118">✔查看第三方数据以确定将迁移的内容。</span><span class="sxs-lookup"><span data-stu-id="12874-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="12874-119">✔从第三方聊天系统中提取所选数据。</span><span class="sxs-lookup"><span data-stu-id="12874-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="12874-120">✔将第三方聊天结构映射到团队结构。</span><span class="sxs-lookup"><span data-stu-id="12874-120">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="12874-121">✔将导入数据转换为迁移所需的格式。</span><span class="sxs-lookup"><span data-stu-id="12874-121">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="12874-122">设置 Office 365 租户</span><span class="sxs-lookup"><span data-stu-id="12874-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="12874-123">✔确保导入数据存在 Office 365 租户。</span><span class="sxs-lookup"><span data-stu-id="12874-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="12874-124">有关为团队设置 Office 365 租赁的详细信息，*请参阅*[准备 office 365 租户](../../concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="12874-124">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="12874-125">✔确保团队成员在 Azure Active Directory (AAD) 中。</span><span class="sxs-lookup"><span data-stu-id="12874-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="12874-126">有关详细信息， *请参阅*向 Azure Active Directory [添加新用户](/azure/active-directory/fundamentals/add-users-azure-active-directory) 。</span><span class="sxs-lookup"><span data-stu-id="12874-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="12874-127">第一步：创建团队</span><span class="sxs-lookup"><span data-stu-id="12874-127">Step One: Create a team</span></span>

<span data-ttu-id="12874-128">由于现有数据正在迁移，因此在迁移过程中维护原始邮件的时间戳并防止邮件活动是重新创建用户的现有邮件流的关键。</span><span class="sxs-lookup"><span data-stu-id="12874-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="12874-129">这是通过以下方式实现的：</span><span class="sxs-lookup"><span data-stu-id="12874-129">This is achieved as follows:</span></span>

> <span data-ttu-id="12874-130">使用 "团队" 资源属性创建具有 "后向时间戳" 的[新团队](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) `createdDateTime` 。</span><span class="sxs-lookup"><span data-stu-id="12874-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="12874-131">将新团队放在中 `migration mode` ，这是一种特殊状态，可从团队中的大多数活动中对用户进行横栏，直到迁移过程完成。</span><span class="sxs-lookup"><span data-stu-id="12874-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="12874-132">将 `teamCreationMode` 实例属性包含 `migration` 在 POST 请求中的值，以显式标识新团队为迁移而创建。</span><span class="sxs-lookup"><span data-stu-id="12874-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> <span data-ttu-id="12874-133">**注意**： `createdDateTime` 将仅为已迁移的团队或频道的实例填充字段。</span><span class="sxs-lookup"><span data-stu-id="12874-133">**NOTE**:  The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="12874-134">Permissions</span><span class="sxs-lookup"><span data-stu-id="12874-134">Permissions</span></span>

|<span data-ttu-id="12874-135">ScopeName</span><span class="sxs-lookup"><span data-stu-id="12874-135">ScopeName</span></span>|<span data-ttu-id="12874-136">DisplayName</span><span class="sxs-lookup"><span data-stu-id="12874-136">DisplayName</span></span>|<span data-ttu-id="12874-137">说明</span><span class="sxs-lookup"><span data-stu-id="12874-137">Description</span></span>|<span data-ttu-id="12874-138">类型</span><span class="sxs-lookup"><span data-stu-id="12874-138">Type</span></span>|<span data-ttu-id="12874-139">管理员同意？</span><span class="sxs-lookup"><span data-stu-id="12874-139">Admin Consent?</span></span>|<span data-ttu-id="12874-140">涵盖的实体/Api</span><span class="sxs-lookup"><span data-stu-id="12874-140">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="12874-141">管理迁移到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="12874-141">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="12874-142">创建、管理用于迁移到 Microsoft 团队的资源</span><span class="sxs-lookup"><span data-stu-id="12874-142">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="12874-143">**仅限应用程序**</span><span class="sxs-lookup"><span data-stu-id="12874-143">**Application-only**</span></span>|<span data-ttu-id="12874-144">**是**</span><span class="sxs-lookup"><span data-stu-id="12874-144">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="12874-145">请求 (在迁移状态中创建团队) </span><span class="sxs-lookup"><span data-stu-id="12874-145">Request (create a team in migration state)</span></span>

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description"
  "createdDateTime": "2020-03-14T11:22:17.043Z"
}
```

#### <a name="response"></a><span data-ttu-id="12874-146">响应</span><span class="sxs-lookup"><span data-stu-id="12874-146">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="12874-147">错误消息</span><span class="sxs-lookup"><span data-stu-id="12874-147">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="12874-148">`createdDateTime`  设置为 "将来"。</span><span class="sxs-lookup"><span data-stu-id="12874-148">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="12874-149">`createdDateTime`  正确指定，但 `teamCreationMode`  缺少实例属性或将实例属性设置为无效值。</span><span class="sxs-lookup"><span data-stu-id="12874-149">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="12874-150">步骤2：创建通道</span><span class="sxs-lookup"><span data-stu-id="12874-150">Step Two: Create a channel</span></span>

<span data-ttu-id="12874-151">为导入的邮件创建通道与创建团队方案类似：</span><span class="sxs-lookup"><span data-stu-id="12874-151">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="12874-152">使用 "信道" 资源属性创建具有 "后向时间戳" 的[新通道](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) `createdDateTime` 。</span><span class="sxs-lookup"><span data-stu-id="12874-152">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="12874-153">将新频道放置在中 `migration mode` ，这是一种特殊状态，可用于在迁移过程完成前，从频道内的大多数聊天活动中对用户进行横栏。</span><span class="sxs-lookup"><span data-stu-id="12874-153">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="12874-154">将 `channelCreationMode` 实例属性包含 `migration` 在 POST 请求中的值，以显式标识新团队为迁移而创建。</span><span class="sxs-lookup"><span data-stu-id="12874-154">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="12874-155">Permissions</span><span class="sxs-lookup"><span data-stu-id="12874-155">Permissions</span></span>

|<span data-ttu-id="12874-156">ScopeName</span><span class="sxs-lookup"><span data-stu-id="12874-156">ScopeName</span></span>|<span data-ttu-id="12874-157">DisplayName</span><span class="sxs-lookup"><span data-stu-id="12874-157">DisplayName</span></span>|<span data-ttu-id="12874-158">说明</span><span class="sxs-lookup"><span data-stu-id="12874-158">Description</span></span>|<span data-ttu-id="12874-159">类型</span><span class="sxs-lookup"><span data-stu-id="12874-159">Type</span></span>|<span data-ttu-id="12874-160">管理员同意？</span><span class="sxs-lookup"><span data-stu-id="12874-160">Admin Consent?</span></span>|<span data-ttu-id="12874-161">涵盖的实体/Api</span><span class="sxs-lookup"><span data-stu-id="12874-161">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="12874-162">管理迁移到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="12874-162">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="12874-163">创建、管理用于迁移到 Microsoft 团队的资源</span><span class="sxs-lookup"><span data-stu-id="12874-163">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="12874-164">**仅限应用程序**</span><span class="sxs-lookup"><span data-stu-id="12874-164">**Application-only**</span></span>|<span data-ttu-id="12874-165">**是**</span><span class="sxs-lookup"><span data-stu-id="12874-165">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="12874-166">请求 (在迁移状态中创建频道) </span><span class="sxs-lookup"><span data-stu-id="12874-166">Request (create a channel in migration state)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/{id}/channels

Content-Type: application/json
{
  "@microsoft.graph.channelCreationMode": "migration",
  "displayName": "Architecture Discussion",
  "description": "This channel is where we debate all future architecture plans",
  "membershipType": "standard",
  "createdDateTime": "2020-03-14T11:22:17.047Z"
}
```

#### <a name="response"></a><span data-ttu-id="12874-167">响应</span><span class="sxs-lookup"><span data-stu-id="12874-167">Response</span></span>

```http
HTTP/1.1 202 Accepted

{
   "@odata.context":"https://canary.graph.microsoft.com/testprodbetateamsgraphsvcncus/$metadata#teams('9cc6d6ab-07d8-4d14-bc2b-7db8995d6d23')/channels/$entity",
   "id":"19:e90f6814ce674072a4126206e7de485e@thread.tacv2",
   "createdDateTime":null,
   "displayName":"Architecture Discussion",
   "description":"This channel is where we debate all future architecture plans",
   "isFavoriteByDefault":null,
   "email":null,
   "webUrl":null,
   "membershipType":null,
   "moderationSettings":null
}

#### Error message

```http
400 Bad Request
```

* <span data-ttu-id="12874-168">`createdDateTime`  设置为 "将来"。</span><span class="sxs-lookup"><span data-stu-id="12874-168">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="12874-169">`createdDateTime`  正确指定 `channelCreationMode`  ，但缺少实例属性或将实例属性设置为无效值。</span><span class="sxs-lookup"><span data-stu-id="12874-169">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="12874-170">第三步：导入邮件</span><span class="sxs-lookup"><span data-stu-id="12874-170">Step Three: Import messages</span></span>

<span data-ttu-id="12874-171">在创建团队和频道之后，您可以开始使用 `createdDateTime`  请求正文中的和键发送回送邮件 `from`  。</span><span class="sxs-lookup"><span data-stu-id="12874-171">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="12874-172">**注意**： `createdDateTime` 不支持在邮件线程之前导入的邮件 `createdDateTime` 。</span><span class="sxs-lookup"><span data-stu-id="12874-172">**NOTE**: messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> <span data-ttu-id="12874-173">createdDateTime 在同一线程中的所有邮件中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="12874-173">createdDateTime must be unique across messages in the same thread.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="12874-174">请求 (张贴为纯文本的邮件) </span><span class="sxs-lookup"><span data-stu-id="12874-174">Request (POST message that is text-only)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

{
   "createdDateTime":"2019-02-04T19:58:15.511Z",
   "from":{
      "user":{
         "id":"id-value",
         "displayName":"Joh Doe",
         "userIdentityType":"aadUser"
      }
   },
   "body":{
      "contentType":"html",
      "content":"Hello World"
   }
}
```

#### <a name="response"></a><span data-ttu-id="12874-175">响应</span><span class="sxs-lookup"><span data-stu-id="12874-175">Response</span></span>

```http
HTTP/1.1 200 OK

{
   "@odata.context":"https://graph.microsoft.com/beta/$metadata#teams('teamId')/channels('channelId')/messages/$entity",
   "id":"id-value",
   "replyToId":null,
   "etag":"id-value",
   "messageType":"message",
   "createdDateTime":"2019-02-04T19:58:15.58Z",
   "lastModifiedDateTime":null,
   "deleted":false,
   "subject":null,
   "summary":null,
   "importance":"normal",
   "locale":"en-us",
   "policyViolation":null,
   "from":{
      "application":null,
      "device":null,
      "conversation":null,
      "user":{
         "id":"id-value",
         "displayName":"Joh Doe",
         "userIdentityType":"aadUser"
      }
   },
   "body":{
      "contentType":"html",
      "content":"Hello World"
   },
   "attachments":[
   ],
   "mentions":[
   ],
   "reactions":[
   ]
}
```

#### <a name="error-messages"></a><span data-ttu-id="12874-176">错误消息</span><span class="sxs-lookup"><span data-stu-id="12874-176">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="12874-177">请求 (将包含内联图像的邮件发布) </span><span class="sxs-lookup"><span data-stu-id="12874-177">Request (POST a message with inline image)</span></span>

> <span data-ttu-id="12874-178">**注意**：此方案中没有特殊的权限范围，因为该请求是了 chatmessage 的一部分;了 chatmessage 的作用域也适用于此处。</span><span class="sxs-lookup"><span data-stu-id="12874-178">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

{
  "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"../hostedContents/1/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "hostedContents":[
        {
            "@microsoft.graph.temporaryId": "1",
            "contentBytes": "iVBORw0KGgoAAAANSUhEUgAAANcAAAExCAYAAADvFzeeAAAXjklEQVR4Ae2d/XNU1RnH+9e0FFrA0RCIyaS8hRA0HV5KbS1gHRgVpjMClY4GHJ3yYm1HCmXaWttaaZUZtIIFKYi8lFAkvOQ9u5vN225IARVBbX9/Os9NbrLZbMjmhCfJPX5+2Lmb3T25y3O+n/M599x7w9f+++UXwoMakIF7n4GvUdR7X1RqSk01A8CFuZm5GGUAuIwKi72wF3ABF+YyygBwGRUWc2Eu4AIuzGWUAeAyKizmwlzABVyYyygDwGVUWMyFuYALuDCXUQaAy6iwmAtzARdwfWXMdeuzT+TGxz3Sfb1LunrapL07IW3pePDQ5/qavqef0c+OdYAELuAac4jGGkLL9rdvfyo9N9ODQAqBGmmrwGlb/R0u3xG4gMspOC5hG882CoRaaCSA8n1ff9doIQMu4PIOrus3u+8ZVNnw6e/Od5AALuDKOyz5hmqiPnfnzi1J9bSbgRWCpvvQfY307wQu4BoxJCOFaDK8rwsQmQsUIQhWW93XSIsewAVckYdLQ24F0Ui/926AARdwRRounZ6Np7GyYdN9DzdFBC7gijRc43GMlQ1U9s/6HXJNjYELuHI<<-----Removed----->>>>",
            "contentType": "image/png"
        }
    ]
}
```

#### <a name="response"></a><span data-ttu-id="12874-179">响应</span><span class="sxs-lookup"><span data-stu-id="12874-179">Response</span></span>

```http
HTTP/1.1 200 OK

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#teams('teamId')/channels('channelId')/messages/$entity",
    "id": "id-value",
    "replyToId": null,
    "etag": "id-value",
    "messageType": "message",
    "createdDateTime": "2019-02-04T19:58:15.511Z",
    "lastModifiedDateTime": null,
    "deleted": false,
    "subject": null,
    "summary": null,
    "importance": "normal",
    "locale": "en-us",
    "policyViolation": null,
    "from": {
        "application": null,
        "device": null,
        "conversation": null,
        "user": {
            "id": "id-value",
            "displayName": "Joh Doe",
            "userIdentityType": "aadUser"
        }
    },
      "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"https://graph.microsoft.com/teams/teamId/channels/channelId/messages/id-value/hostedContents/hostedContentId/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="12874-180">步骤4：完成迁移模式</span><span class="sxs-lookup"><span data-stu-id="12874-180">Step Four: Complete migration mode</span></span>

<span data-ttu-id="12874-181">邮件迁移过程完成后，团队和通道将使用方法从迁移模式中去掉  `completeMigration`  。</span><span class="sxs-lookup"><span data-stu-id="12874-181">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="12874-182">此步骤将打开团队和渠道资源，以供工作组成员进行常规使用。</span><span class="sxs-lookup"><span data-stu-id="12874-182">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="12874-183">操作将绑定到 `team` 实例。</span><span class="sxs-lookup"><span data-stu-id="12874-183">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="12874-184">请求 (结束团队迁移模式) </span><span class="sxs-lookup"><span data-stu-id="12874-184">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="12874-185">响应</span><span class="sxs-lookup"><span data-stu-id="12874-185">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="12874-186">请求 (结束通道迁移模式) </span><span class="sxs-lookup"><span data-stu-id="12874-186">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="12874-187">响应</span><span class="sxs-lookup"><span data-stu-id="12874-187">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="12874-188">错误响应</span><span class="sxs-lookup"><span data-stu-id="12874-188">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="12874-189">在或上调用的操作 `team` `channel` 不在中 `migrationMode` 。</span><span class="sxs-lookup"><span data-stu-id="12874-189">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="12874-190">第5步：添加团队成员</span><span class="sxs-lookup"><span data-stu-id="12874-190">Step Five: Add team members</span></span>

<span data-ttu-id="12874-191">您可以 [使用 "团队 UI"](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) 或 Microsoft Graph [添加成员](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API 将成员添加到团队中：</span><span class="sxs-lookup"><span data-stu-id="12874-191">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="12874-192">请求 (添加成员) </span><span class="sxs-lookup"><span data-stu-id="12874-192">Request (add member)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/{id}/members
Content-type: application/json
Content-length: 30
{
"@odata.type": "#microsoft.graph.aadUserConversationMember",
"roles": [],
"user@odata.bind": "https://graph.microsoft.com/beta/users/{user-id}"
}
```

#### <a name="response"></a><span data-ttu-id="12874-193">响应</span><span class="sxs-lookup"><span data-stu-id="12874-193">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="12874-194">提示和其他信息</span><span class="sxs-lookup"><span data-stu-id="12874-194">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="12874-195">您可以导入不在工作组中的用户的邮件。</span><span class="sxs-lookup"><span data-stu-id="12874-195">You can import messages from users who are not in Teams.</span></span> <span data-ttu-id="12874-196">**注意**：在公共预览过程中，不会在团队客户端或合规性门户中搜索为用户导入的邮件。</span><span class="sxs-lookup"><span data-stu-id="12874-196">**NOTE**: Messages imported for users not present in the tenant will not be searchable in the Teams client or compliance portals during Public Preview.</span></span>

* <span data-ttu-id="12874-197">`completeMigration`发出请求后，将无法再向团队中导入邮件。</span><span class="sxs-lookup"><span data-stu-id="12874-197">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="12874-198">只有在请求返回成功的响应后，才能将团队成员添加到新团队 `completeMigration` 。</span><span class="sxs-lookup"><span data-stu-id="12874-198">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="12874-199">限制：邮件将导入每通道5个 RPS。</span><span class="sxs-lookup"><span data-stu-id="12874-199">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="12874-200">如果需要对迁移结果进行更正，则需要删除团队并重复步骤以创建团队和频道并重新迁移邮件。</span><span class="sxs-lookup"><span data-stu-id="12874-200">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="12874-201">目前，嵌入式图像是导入邮件 API 架构支持的唯一媒体类型。</span><span class="sxs-lookup"><span data-stu-id="12874-201">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="12874-202">导入内容范围</span><span class="sxs-lookup"><span data-stu-id="12874-202">Import content scope</span></span>

|<span data-ttu-id="12874-203">范围内</span><span class="sxs-lookup"><span data-stu-id="12874-203">In-scope</span></span> | <span data-ttu-id="12874-204">当前超出范围</span><span class="sxs-lookup"><span data-stu-id="12874-204">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="12874-205">团队和频道消息</span><span class="sxs-lookup"><span data-stu-id="12874-205">Team and channel messages</span></span>|<span data-ttu-id="12874-206">1:1 和分组聊天消息</span><span class="sxs-lookup"><span data-stu-id="12874-206">1:1 and group chat messages</span></span>|
|<span data-ttu-id="12874-207">原始邮件的创建时间</span><span class="sxs-lookup"><span data-stu-id="12874-207">Created time of the original message</span></span>|<span data-ttu-id="12874-208">专用频道</span><span class="sxs-lookup"><span data-stu-id="12874-208">Private channels</span></span>|
|<span data-ttu-id="12874-209">作为邮件的一部分的嵌入式图像</span><span class="sxs-lookup"><span data-stu-id="12874-209">Inline images as part of the message</span></span>|<span data-ttu-id="12874-210">提到</span><span class="sxs-lookup"><span data-stu-id="12874-210">At mentions</span></span>|
|<span data-ttu-id="12874-211">指向 SPO/OneDrive 中的现有文件的链接</span><span class="sxs-lookup"><span data-stu-id="12874-211">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="12874-212">作出</span><span class="sxs-lookup"><span data-stu-id="12874-212">Reactions</span></span>|
|<span data-ttu-id="12874-213">带格式文本的邮件</span><span class="sxs-lookup"><span data-stu-id="12874-213">Messages with rich text</span></span>|<span data-ttu-id="12874-214">视频</span><span class="sxs-lookup"><span data-stu-id="12874-214">Videos</span></span>|
|<span data-ttu-id="12874-215">邮件答复链</span><span class="sxs-lookup"><span data-stu-id="12874-215">Message reply chain</span></span>|<span data-ttu-id="12874-216">公告</span><span class="sxs-lookup"><span data-stu-id="12874-216">Announcements</span></span>|
|<span data-ttu-id="12874-217">高吞吐量处理</span><span class="sxs-lookup"><span data-stu-id="12874-217">High throughput processing</span></span>|<span data-ttu-id="12874-218">代码段</span><span class="sxs-lookup"><span data-stu-id="12874-218">Code snippets</span></span>|
||<span data-ttu-id="12874-219">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="12874-219">Adaptive cards</span></span>|
||<span data-ttu-id="12874-220">不干胶</span><span class="sxs-lookup"><span data-stu-id="12874-220">Stickers</span></span>|
||<span data-ttu-id="12874-221">表情符号</span><span class="sxs-lookup"><span data-stu-id="12874-221">Emojis</span></span>|
||<span data-ttu-id="12874-222">股票</span><span class="sxs-lookup"><span data-stu-id="12874-222">Quotes</span></span>|
||<span data-ttu-id="12874-223">通道之间的跨文章</span><span class="sxs-lookup"><span data-stu-id="12874-223">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="12874-224">了解有关 Microsoft Graph 和团队集成的详细信息</span><span class="sxs-lookup"><span data-stu-id="12874-224">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
