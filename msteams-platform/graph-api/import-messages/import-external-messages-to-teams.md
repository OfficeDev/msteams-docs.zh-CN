---
title: 使用 Microsoft Graph 将外部平台邮件导入到团队
description: 介绍如何使用 Microsoft Graph 将邮件从外部平台导入到团队
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: 团队导入邮件 api 图 microsoft 迁移迁移发布
ms.openlocfilehash: 934e00541773140c90c270a616d6bc50aacac6e1
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796293"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="3653f-104">使用 Microsoft Graph 将第三方平台消息导入 Teams</span><span class="sxs-lookup"><span data-stu-id="3653f-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="3653f-105">Microsoft Graph 和 Microsoft 团队公开预览版适用于早期访问和反馈。</span><span class="sxs-lookup"><span data-stu-id="3653f-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="3653f-106">尽管此版本已经历大量测试，但不适合在生产中使用。</span><span class="sxs-lookup"><span data-stu-id="3653f-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="3653f-107">使用 Microsoft Graph，可以将用户的现有邮件历史记录和数据从外部系统迁移到团队频道。</span><span class="sxs-lookup"><span data-stu-id="3653f-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="3653f-108">通过在团队内启用第三方平台邮件传递层次结构，用户可以采用无缝方式继续进行通信并继续进行而不会中断。</span><span class="sxs-lookup"><span data-stu-id="3653f-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="3653f-109">导入概述</span><span class="sxs-lookup"><span data-stu-id="3653f-109">Import overview</span></span>

<span data-ttu-id="3653f-110">从较高的层次来看，导入过程包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="3653f-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="3653f-111">创建具有后时间戳的团队</span><span class="sxs-lookup"><span data-stu-id="3653f-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="3653f-112">使用后向时间戳创建通道</span><span class="sxs-lookup"><span data-stu-id="3653f-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="3653f-113">导入外部定期邮件</span><span class="sxs-lookup"><span data-stu-id="3653f-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="3653f-114">完成团队和渠道迁移过程</span><span class="sxs-lookup"><span data-stu-id="3653f-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="3653f-115">添加团队成员</span><span class="sxs-lookup"><span data-stu-id="3653f-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="3653f-116">必需的要求</span><span class="sxs-lookup"><span data-stu-id="3653f-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="3653f-117">分析和准备邮件数据</span><span class="sxs-lookup"><span data-stu-id="3653f-117">Analyze and prepare message data</span></span>

<span data-ttu-id="3653f-118">✔查看第三方数据以确定将迁移的内容。</span><span class="sxs-lookup"><span data-stu-id="3653f-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="3653f-119">✔从第三方聊天系统中提取所选数据。</span><span class="sxs-lookup"><span data-stu-id="3653f-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="3653f-120">✔将第三方聊天结构映射到团队结构。</span><span class="sxs-lookup"><span data-stu-id="3653f-120">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="3653f-121">✔将导入数据转换为迁移所需的格式。</span><span class="sxs-lookup"><span data-stu-id="3653f-121">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="3653f-122">设置 Office 365 租户</span><span class="sxs-lookup"><span data-stu-id="3653f-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="3653f-123">✔确保导入数据存在 Office 365 租户。</span><span class="sxs-lookup"><span data-stu-id="3653f-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="3653f-124">有关为团队设置 Office 365 租赁的详细信息， *请参阅*[准备 office 365 租户](../../concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="3653f-124">For more information on setting up an Office 365 tenancy for Teams, *see* , [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="3653f-125">✔确保团队成员在 Azure Active Directory (AAD) 中。</span><span class="sxs-lookup"><span data-stu-id="3653f-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="3653f-126">有关详细信息， *请参阅* 向 Azure Active Directory [添加新用户](/azure/active-directory/fundamentals/add-users-azure-active-directory) 。</span><span class="sxs-lookup"><span data-stu-id="3653f-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="3653f-127">第一步：创建团队</span><span class="sxs-lookup"><span data-stu-id="3653f-127">Step One: Create a team</span></span>

<span data-ttu-id="3653f-128">由于现有数据正在迁移，因此在迁移过程中维护原始邮件的时间戳并防止邮件活动是重新创建用户的现有邮件流的关键。</span><span class="sxs-lookup"><span data-stu-id="3653f-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="3653f-129">这是通过以下方式实现的：</span><span class="sxs-lookup"><span data-stu-id="3653f-129">This is achieved as follows:</span></span>

> <span data-ttu-id="3653f-130">使用 "团队" 资源属性创建具有 "后向时间戳" 的[新团队](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) `createdDateTime` 。</span><span class="sxs-lookup"><span data-stu-id="3653f-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="3653f-131">将新团队放在中 `migration mode` ，这是一种特殊状态，可从团队中的大多数活动中对用户进行横栏，直到迁移过程完成。</span><span class="sxs-lookup"><span data-stu-id="3653f-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="3653f-132">将 `teamCreationMode` 实例属性包含 `migration` 在 POST 请求中的值，以显式标识新团队为迁移而创建。</span><span class="sxs-lookup"><span data-stu-id="3653f-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> <span data-ttu-id="3653f-133">**注意** ： `createdDateTime` 将仅为已迁移的团队或频道的实例填充字段。</span><span class="sxs-lookup"><span data-stu-id="3653f-133">**NOTE** :  The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="3653f-134">权限</span><span class="sxs-lookup"><span data-stu-id="3653f-134">Permissions</span></span>

|<span data-ttu-id="3653f-135">ScopeName</span><span class="sxs-lookup"><span data-stu-id="3653f-135">ScopeName</span></span>|<span data-ttu-id="3653f-136">DisplayName</span><span class="sxs-lookup"><span data-stu-id="3653f-136">DisplayName</span></span>|<span data-ttu-id="3653f-137">说明</span><span class="sxs-lookup"><span data-stu-id="3653f-137">Description</span></span>|<span data-ttu-id="3653f-138">类型</span><span class="sxs-lookup"><span data-stu-id="3653f-138">Type</span></span>|<span data-ttu-id="3653f-139">管理员同意？</span><span class="sxs-lookup"><span data-stu-id="3653f-139">Admin Consent?</span></span>|<span data-ttu-id="3653f-140">涵盖的实体/Api</span><span class="sxs-lookup"><span data-stu-id="3653f-140">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="3653f-141">管理迁移到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3653f-141">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="3653f-142">创建、管理用于迁移到 Microsoft 团队的资源</span><span class="sxs-lookup"><span data-stu-id="3653f-142">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="3653f-143">**仅限应用程序**</span><span class="sxs-lookup"><span data-stu-id="3653f-143">**Application-only**</span></span>|<span data-ttu-id="3653f-144">**是**</span><span class="sxs-lookup"><span data-stu-id="3653f-144">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="3653f-145">请求 (在迁移状态中创建团队) </span><span class="sxs-lookup"><span data-stu-id="3653f-145">Request (create a team in migration state)</span></span>

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.043Z"
}
```

#### <a name="response"></a><span data-ttu-id="3653f-146">响应</span><span class="sxs-lookup"><span data-stu-id="3653f-146">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="3653f-147">错误消息</span><span class="sxs-lookup"><span data-stu-id="3653f-147">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="3653f-148">`createdDateTime`  设置为 "将来"。</span><span class="sxs-lookup"><span data-stu-id="3653f-148">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="3653f-149">`createdDateTime`  正确指定，但 `teamCreationMode`  缺少实例属性或将实例属性设置为无效值。</span><span class="sxs-lookup"><span data-stu-id="3653f-149">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="3653f-150">步骤2：创建通道</span><span class="sxs-lookup"><span data-stu-id="3653f-150">Step Two: Create a channel</span></span>

<span data-ttu-id="3653f-151">为导入的邮件创建通道与创建团队方案类似：</span><span class="sxs-lookup"><span data-stu-id="3653f-151">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="3653f-152">使用 "信道" 资源属性创建具有 "后向时间戳" 的[新通道](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) `createdDateTime` 。</span><span class="sxs-lookup"><span data-stu-id="3653f-152">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="3653f-153">将新频道放置在中 `migration mode` ，这是一种特殊状态，可用于在迁移过程完成前，从频道内的大多数聊天活动中对用户进行横栏。</span><span class="sxs-lookup"><span data-stu-id="3653f-153">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="3653f-154">将 `channelCreationMode` 实例属性包含 `migration` 在 POST 请求中的值，以显式标识新团队为迁移而创建。</span><span class="sxs-lookup"><span data-stu-id="3653f-154">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="3653f-155">权限</span><span class="sxs-lookup"><span data-stu-id="3653f-155">Permissions</span></span>

|<span data-ttu-id="3653f-156">ScopeName</span><span class="sxs-lookup"><span data-stu-id="3653f-156">ScopeName</span></span>|<span data-ttu-id="3653f-157">DisplayName</span><span class="sxs-lookup"><span data-stu-id="3653f-157">DisplayName</span></span>|<span data-ttu-id="3653f-158">说明</span><span class="sxs-lookup"><span data-stu-id="3653f-158">Description</span></span>|<span data-ttu-id="3653f-159">类型</span><span class="sxs-lookup"><span data-stu-id="3653f-159">Type</span></span>|<span data-ttu-id="3653f-160">管理员同意？</span><span class="sxs-lookup"><span data-stu-id="3653f-160">Admin Consent?</span></span>|<span data-ttu-id="3653f-161">涵盖的实体/Api</span><span class="sxs-lookup"><span data-stu-id="3653f-161">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="3653f-162">管理迁移到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3653f-162">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="3653f-163">创建、管理用于迁移到 Microsoft 团队的资源</span><span class="sxs-lookup"><span data-stu-id="3653f-163">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="3653f-164">**仅限应用程序**</span><span class="sxs-lookup"><span data-stu-id="3653f-164">**Application-only**</span></span>|<span data-ttu-id="3653f-165">**是**</span><span class="sxs-lookup"><span data-stu-id="3653f-165">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="3653f-166">请求 (在迁移状态中创建频道) </span><span class="sxs-lookup"><span data-stu-id="3653f-166">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="3653f-167">响应</span><span class="sxs-lookup"><span data-stu-id="3653f-167">Response</span></span>

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
```

#### <a name="error-message"></a><span data-ttu-id="3653f-168">错误消息</span><span class="sxs-lookup"><span data-stu-id="3653f-168">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="3653f-169">`createdDateTime`  设置为 "将来"。</span><span class="sxs-lookup"><span data-stu-id="3653f-169">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="3653f-170">`createdDateTime`  正确指定 `channelCreationMode`  ，但缺少实例属性或将实例属性设置为无效值。</span><span class="sxs-lookup"><span data-stu-id="3653f-170">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="3653f-171">第三步：导入邮件</span><span class="sxs-lookup"><span data-stu-id="3653f-171">Step Three: Import messages</span></span>

<span data-ttu-id="3653f-172">在创建团队和频道之后，您可以开始使用 `createdDateTime`  请求正文中的和键发送回送邮件 `from`  。</span><span class="sxs-lookup"><span data-stu-id="3653f-172">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="3653f-173">**注意** ： `createdDateTime` 不支持在邮件线程之前导入的邮件 `createdDateTime` 。</span><span class="sxs-lookup"><span data-stu-id="3653f-173">**NOTE** : messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> <span data-ttu-id="3653f-174">createdDateTime 在同一线程中的所有邮件中必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="3653f-174">createdDateTime must be unique across messages in the same thread.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="3653f-175">请求 (张贴为纯文本的邮件) </span><span class="sxs-lookup"><span data-stu-id="3653f-175">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="3653f-176">响应</span><span class="sxs-lookup"><span data-stu-id="3653f-176">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="3653f-177">错误消息</span><span class="sxs-lookup"><span data-stu-id="3653f-177">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="3653f-178">请求 (将包含内联图像的邮件发布) </span><span class="sxs-lookup"><span data-stu-id="3653f-178">Request (POST a message with inline image)</span></span>

> <span data-ttu-id="3653f-179">**注意** ：此方案中没有特殊的权限范围，因为该请求是了 chatmessage 的一部分;了 chatmessage 的作用域也适用于此处。</span><span class="sxs-lookup"><span data-stu-id="3653f-179">**Note** : There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="3653f-180">响应</span><span class="sxs-lookup"><span data-stu-id="3653f-180">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="3653f-181">步骤4：完成迁移模式</span><span class="sxs-lookup"><span data-stu-id="3653f-181">Step Four: Complete migration mode</span></span>

<span data-ttu-id="3653f-182">邮件迁移过程完成后，团队和通道将使用方法从迁移模式中去掉  `completeMigration`  。</span><span class="sxs-lookup"><span data-stu-id="3653f-182">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="3653f-183">此步骤将打开团队和渠道资源，以供工作组成员进行常规使用。</span><span class="sxs-lookup"><span data-stu-id="3653f-183">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="3653f-184">操作将绑定到 `team` 实例。</span><span class="sxs-lookup"><span data-stu-id="3653f-184">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="3653f-185">请求 (结束团队迁移模式) </span><span class="sxs-lookup"><span data-stu-id="3653f-185">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="3653f-186">响应</span><span class="sxs-lookup"><span data-stu-id="3653f-186">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="3653f-187">请求 (结束通道迁移模式) </span><span class="sxs-lookup"><span data-stu-id="3653f-187">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="3653f-188">响应</span><span class="sxs-lookup"><span data-stu-id="3653f-188">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="3653f-189">错误响应</span><span class="sxs-lookup"><span data-stu-id="3653f-189">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="3653f-190">在或上调用的操作 `team` `channel` 不在中 `migrationMode` 。</span><span class="sxs-lookup"><span data-stu-id="3653f-190">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="3653f-191">第5步：添加团队成员</span><span class="sxs-lookup"><span data-stu-id="3653f-191">Step Five: Add team members</span></span>

<span data-ttu-id="3653f-192">您可以 [使用 "团队 UI"](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) 或 Microsoft Graph [添加成员](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API 将成员添加到团队中：</span><span class="sxs-lookup"><span data-stu-id="3653f-192">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="3653f-193">请求 (添加成员) </span><span class="sxs-lookup"><span data-stu-id="3653f-193">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="3653f-194">响应</span><span class="sxs-lookup"><span data-stu-id="3653f-194">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="3653f-195">提示和其他信息</span><span class="sxs-lookup"><span data-stu-id="3653f-195">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="3653f-196">您可以导入不在工作组中的用户的邮件。</span><span class="sxs-lookup"><span data-stu-id="3653f-196">You can import messages from users who are not in Teams.</span></span> <span data-ttu-id="3653f-197">**注意** ：在公共预览过程中，不会在团队客户端或合规性门户中搜索为用户导入的邮件。</span><span class="sxs-lookup"><span data-stu-id="3653f-197">**NOTE** : Messages imported for users not present in the tenant will not be searchable in the Teams client or compliance portals during Public Preview.</span></span>

* <span data-ttu-id="3653f-198">`completeMigration`发出请求后，将无法再向团队中导入邮件。</span><span class="sxs-lookup"><span data-stu-id="3653f-198">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="3653f-199">只有在请求返回成功的响应后，才能将团队成员添加到新团队 `completeMigration` 。</span><span class="sxs-lookup"><span data-stu-id="3653f-199">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="3653f-200">限制：邮件将导入每通道5个 RPS。</span><span class="sxs-lookup"><span data-stu-id="3653f-200">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="3653f-201">如果需要对迁移结果进行更正，则需要删除团队并重复步骤以创建团队和频道并重新迁移邮件。</span><span class="sxs-lookup"><span data-stu-id="3653f-201">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="3653f-202">目前，嵌入式图像是导入邮件 API 架构支持的唯一媒体类型。</span><span class="sxs-lookup"><span data-stu-id="3653f-202">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="3653f-203">导入内容范围</span><span class="sxs-lookup"><span data-stu-id="3653f-203">Import content scope</span></span>

|<span data-ttu-id="3653f-204">范围内</span><span class="sxs-lookup"><span data-stu-id="3653f-204">In-scope</span></span> | <span data-ttu-id="3653f-205">当前超出范围</span><span class="sxs-lookup"><span data-stu-id="3653f-205">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="3653f-206">团队和频道消息</span><span class="sxs-lookup"><span data-stu-id="3653f-206">Team and channel messages</span></span>|<span data-ttu-id="3653f-207">1:1 和分组聊天消息</span><span class="sxs-lookup"><span data-stu-id="3653f-207">1:1 and group chat messages</span></span>|
|<span data-ttu-id="3653f-208">原始邮件的创建时间</span><span class="sxs-lookup"><span data-stu-id="3653f-208">Created time of the original message</span></span>|<span data-ttu-id="3653f-209">专用频道</span><span class="sxs-lookup"><span data-stu-id="3653f-209">Private channels</span></span>|
|<span data-ttu-id="3653f-210">作为邮件的一部分的嵌入式图像</span><span class="sxs-lookup"><span data-stu-id="3653f-210">Inline images as part of the message</span></span>|<span data-ttu-id="3653f-211">提到</span><span class="sxs-lookup"><span data-stu-id="3653f-211">At mentions</span></span>|
|<span data-ttu-id="3653f-212">指向 SPO/OneDrive 中的现有文件的链接</span><span class="sxs-lookup"><span data-stu-id="3653f-212">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="3653f-213">作出</span><span class="sxs-lookup"><span data-stu-id="3653f-213">Reactions</span></span>|
|<span data-ttu-id="3653f-214">带格式文本的邮件</span><span class="sxs-lookup"><span data-stu-id="3653f-214">Messages with rich text</span></span>|<span data-ttu-id="3653f-215">视频</span><span class="sxs-lookup"><span data-stu-id="3653f-215">Videos</span></span>|
|<span data-ttu-id="3653f-216">邮件答复链</span><span class="sxs-lookup"><span data-stu-id="3653f-216">Message reply chain</span></span>|<span data-ttu-id="3653f-217">公告</span><span class="sxs-lookup"><span data-stu-id="3653f-217">Announcements</span></span>|
|<span data-ttu-id="3653f-218">高吞吐量处理</span><span class="sxs-lookup"><span data-stu-id="3653f-218">High throughput processing</span></span>|<span data-ttu-id="3653f-219">代码段</span><span class="sxs-lookup"><span data-stu-id="3653f-219">Code snippets</span></span>|
||<span data-ttu-id="3653f-220">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="3653f-220">Adaptive cards</span></span>|
||<span data-ttu-id="3653f-221">不干胶</span><span class="sxs-lookup"><span data-stu-id="3653f-221">Stickers</span></span>|
||<span data-ttu-id="3653f-222">表情符号</span><span class="sxs-lookup"><span data-stu-id="3653f-222">Emojis</span></span>|
||<span data-ttu-id="3653f-223">股票</span><span class="sxs-lookup"><span data-stu-id="3653f-223">Quotes</span></span>|
||<span data-ttu-id="3653f-224">通道之间的跨文章</span><span class="sxs-lookup"><span data-stu-id="3653f-224">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="3653f-225">了解有关 Microsoft Graph 和团队集成的详细信息</span><span class="sxs-lookup"><span data-stu-id="3653f-225">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
