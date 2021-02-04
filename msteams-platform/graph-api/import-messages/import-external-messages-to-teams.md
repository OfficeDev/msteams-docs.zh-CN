---
title: 使用 Microsoft Graph 将外部平台消息导入 Teams
description: 介绍如何使用 Microsoft Graph 将邮件从外部平台导入 Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams 导入消息 api graph microsoft 迁移迁移文章
ms.openlocfilehash: 97f24c34ebb825aad0fd104c9a814e46f9b5fa0d
ms.sourcegitcommit: f74b74d5bed1df193e59f46121ada443fb57277b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093258"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="1bfd7-104">使用 Microsoft Graph 将第三方平台消息导入 Teams</span><span class="sxs-lookup"><span data-stu-id="1bfd7-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="1bfd7-105">Microsoft Graph 和 Microsoft Teams 公共预览版可用于早期访问和反馈。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="1bfd7-106">尽管此版本已经过大量测试，但不适合在生产中使用。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="1bfd7-107">使用 Microsoft Graph，可以将用户的现有邮件历史记录和数据从外部系统迁移到 Teams 频道。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="1bfd7-108">通过支持在 Teams 内恢复第三方平台消息层次结构，用户可以继续无缝通信，并且无需中断。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="1bfd7-109">导入概述</span><span class="sxs-lookup"><span data-stu-id="1bfd7-109">Import overview</span></span>

<span data-ttu-id="1bfd7-110">在高级别上，导入过程由以下内容组成：</span><span class="sxs-lookup"><span data-stu-id="1bfd7-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="1bfd7-111">创建具有返回时间戳的团队</span><span class="sxs-lookup"><span data-stu-id="1bfd7-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="1bfd7-112">创建具有返回时间戳的频道</span><span class="sxs-lookup"><span data-stu-id="1bfd7-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="1bfd7-113">导入外部实时日期消息</span><span class="sxs-lookup"><span data-stu-id="1bfd7-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="1bfd7-114">完成团队和频道迁移过程</span><span class="sxs-lookup"><span data-stu-id="1bfd7-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="1bfd7-115">添加团队成员</span><span class="sxs-lookup"><span data-stu-id="1bfd7-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="1bfd7-116">所需要求</span><span class="sxs-lookup"><span data-stu-id="1bfd7-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="1bfd7-117">分析和准备邮件数据</span><span class="sxs-lookup"><span data-stu-id="1bfd7-117">Analyze and prepare message data</span></span>

<span data-ttu-id="1bfd7-118">✔查看第三方数据，以决定要迁移哪些内容。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="1bfd7-119">✔从第三方聊天系统提取所选数据。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="1bfd7-120">✔将第三方聊天结构映射到 Teams 结构。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-120">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="1bfd7-121">✔将导入数据转换为迁移所需的格式。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-121">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="1bfd7-122">设置 Office 365 租户</span><span class="sxs-lookup"><span data-stu-id="1bfd7-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="1bfd7-123">✔确保导入数据存在 Office 365 租户。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="1bfd7-124">有关为 Teams 设置 Office 365 租户详细信息，请参阅"[准备 Office 365 租户"。](../../concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="1bfd7-124">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="1bfd7-125">✔确保团队成员在 Azure Active Directory (AAD) 。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="1bfd7-126">有关详细信息，*请参阅将*[新用户添加到](/azure/active-directory/fundamentals/add-users-azure-active-directory)Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="1bfd7-127">步骤 1：创建团队</span><span class="sxs-lookup"><span data-stu-id="1bfd7-127">Step One: Create a team</span></span>

<span data-ttu-id="1bfd7-128">由于正在迁移现有数据，因此在迁移过程中维护原始邮件时间戳并阻止邮件活动是在 Teams 中重新创建用户的现有邮件流的关键。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="1bfd7-129">实现此目的，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1bfd7-129">This is achieved as follows:</span></span>

> <span data-ttu-id="1bfd7-130">[使用工作组资源](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) 属性创建一个时间戳返回的新  `createdDateTime`  团队。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="1bfd7-131">将新团队放在一种特殊状态中，在迁移过程完成之前，会禁止用户参与团队中的 `migration mode` 大多数活动。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="1bfd7-132">在 POST 请求中将实例属性与值一起包含，以明确标识要创建的 `teamCreationMode` `migration` 迁移新团队。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> <span data-ttu-id="1bfd7-133">**注意**：将仅为已迁移的团队或频道的实例 `createdDateTime` 填充该字段。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-133">**NOTE**:  The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="1bfd7-134">权限</span><span class="sxs-lookup"><span data-stu-id="1bfd7-134">Permissions</span></span>

|<span data-ttu-id="1bfd7-135">ScopeName</span><span class="sxs-lookup"><span data-stu-id="1bfd7-135">ScopeName</span></span>|<span data-ttu-id="1bfd7-136">DisplayName</span><span class="sxs-lookup"><span data-stu-id="1bfd7-136">DisplayName</span></span>|<span data-ttu-id="1bfd7-137">说明</span><span class="sxs-lookup"><span data-stu-id="1bfd7-137">Description</span></span>|<span data-ttu-id="1bfd7-138">类型</span><span class="sxs-lookup"><span data-stu-id="1bfd7-138">Type</span></span>|<span data-ttu-id="1bfd7-139">管理员同意？</span><span class="sxs-lookup"><span data-stu-id="1bfd7-139">Admin Consent?</span></span>|<span data-ttu-id="1bfd7-140">涵盖的实体/API</span><span class="sxs-lookup"><span data-stu-id="1bfd7-140">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="1bfd7-141">管理迁移到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1bfd7-141">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="1bfd7-142">创建、管理迁移到 Microsoft Teams 的资源</span><span class="sxs-lookup"><span data-stu-id="1bfd7-142">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="1bfd7-143">**仅应用程序**</span><span class="sxs-lookup"><span data-stu-id="1bfd7-143">**Application-only**</span></span>|<span data-ttu-id="1bfd7-144">**是**</span><span class="sxs-lookup"><span data-stu-id="1bfd7-144">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="1bfd7-145">请求 (迁移状态创建) </span><span class="sxs-lookup"><span data-stu-id="1bfd7-145">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="1bfd7-146">响应</span><span class="sxs-lookup"><span data-stu-id="1bfd7-146">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="1bfd7-147">错误消息</span><span class="sxs-lookup"><span data-stu-id="1bfd7-147">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="1bfd7-148">`createdDateTime`  设置为将来。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-148">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="1bfd7-149">`createdDateTime`  正确指定，但 `teamCreationMode`  实例属性缺失或设置为无效值。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-149">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="1bfd7-150">步骤 2：创建通道</span><span class="sxs-lookup"><span data-stu-id="1bfd7-150">Step Two: Create a channel</span></span>

<span data-ttu-id="1bfd7-151">为导入的邮件创建频道与创建团队方案类似：</span><span class="sxs-lookup"><span data-stu-id="1bfd7-151">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="1bfd7-152">[使用通道资源](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) 属性创建一个时间戳返回的新 `createdDateTime` 通道。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-152">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="1bfd7-153">将新频道放在一种特殊状态中，在迁移过程完成之前，会禁止用户参与频道内大多数 `migration mode` 聊天活动。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-153">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="1bfd7-154">在 POST 请求中将实例属性与值一起包含，以明确标识要创建的 `channelCreationMode` `migration` 迁移新团队。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-154">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="1bfd7-155">权限</span><span class="sxs-lookup"><span data-stu-id="1bfd7-155">Permissions</span></span>

|<span data-ttu-id="1bfd7-156">ScopeName</span><span class="sxs-lookup"><span data-stu-id="1bfd7-156">ScopeName</span></span>|<span data-ttu-id="1bfd7-157">DisplayName</span><span class="sxs-lookup"><span data-stu-id="1bfd7-157">DisplayName</span></span>|<span data-ttu-id="1bfd7-158">说明</span><span class="sxs-lookup"><span data-stu-id="1bfd7-158">Description</span></span>|<span data-ttu-id="1bfd7-159">类型</span><span class="sxs-lookup"><span data-stu-id="1bfd7-159">Type</span></span>|<span data-ttu-id="1bfd7-160">管理员同意？</span><span class="sxs-lookup"><span data-stu-id="1bfd7-160">Admin Consent?</span></span>|<span data-ttu-id="1bfd7-161">涵盖的实体/API</span><span class="sxs-lookup"><span data-stu-id="1bfd7-161">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="1bfd7-162">管理迁移到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1bfd7-162">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="1bfd7-163">创建、管理迁移到 Microsoft Teams 的资源</span><span class="sxs-lookup"><span data-stu-id="1bfd7-163">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="1bfd7-164">**仅应用程序**</span><span class="sxs-lookup"><span data-stu-id="1bfd7-164">**Application-only**</span></span>|<span data-ttu-id="1bfd7-165">**是**</span><span class="sxs-lookup"><span data-stu-id="1bfd7-165">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="1bfd7-166">请求 (在迁移状态创建) </span><span class="sxs-lookup"><span data-stu-id="1bfd7-166">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="1bfd7-167">响应</span><span class="sxs-lookup"><span data-stu-id="1bfd7-167">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="1bfd7-168">错误消息</span><span class="sxs-lookup"><span data-stu-id="1bfd7-168">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="1bfd7-169">`createdDateTime`  设置为将来。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-169">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="1bfd7-170">`createdDateTime`  正确指定， `channelCreationMode`  但实例属性缺失或设置为无效值。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-170">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="1bfd7-171">步骤 3：导入邮件</span><span class="sxs-lookup"><span data-stu-id="1bfd7-171">Step Three: Import messages</span></span>

<span data-ttu-id="1bfd7-172">创建团队和频道后，可以使用请求正文中的 and 键开始发送返回 `createdDateTime` `from`  时间消息。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-172">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="1bfd7-173">**注意**：不支持使用邮件 `createdDateTime` 线程之前导入 `createdDateTime` 的邮件。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-173">**NOTE**: messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> * <span data-ttu-id="1bfd7-174">`createdDateTime` 在同一线程中的邮件之间必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-174">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="1bfd7-175">`createdDateTime` 支持精度为毫秒的时间戳。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-175">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="1bfd7-176">例如，如果传入请求邮件的值设置为 `createdDateTime` *2020-09-16T05：50：31.0025302Z，* 那么在接收邮件时，它将转换为 *2020-09-16T05：50：31.002Z。*</span><span class="sxs-lookup"><span data-stu-id="1bfd7-176">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="1bfd7-177">请求 (文本格式的 POST) </span><span class="sxs-lookup"><span data-stu-id="1bfd7-177">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="1bfd7-178">响应</span><span class="sxs-lookup"><span data-stu-id="1bfd7-178">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="1bfd7-179">错误消息</span><span class="sxs-lookup"><span data-stu-id="1bfd7-179">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="1bfd7-180">请求 (内联图像消息的 POST) </span><span class="sxs-lookup"><span data-stu-id="1bfd7-180">Request (POST a message with inline image)</span></span>

> <span data-ttu-id="1bfd7-181">**注意**：此方案中没有特殊权限范围，因为请求是 chatMessage 的一部分;chatMessage 的范围也适用于此处。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-181">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="1bfd7-182">响应</span><span class="sxs-lookup"><span data-stu-id="1bfd7-182">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="1bfd7-183">步骤 4：完成迁移模式</span><span class="sxs-lookup"><span data-stu-id="1bfd7-183">Step Four: Complete migration mode</span></span>

<span data-ttu-id="1bfd7-184">邮件迁移过程完成后，使用该方法将团队和频道从迁移  `completeMigration`  模式退出。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-184">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="1bfd7-185">此步骤将打开团队和频道资源，供团队成员常规使用。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-185">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="1bfd7-186">该操作绑定到 `team` 实例。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-186">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="1bfd7-187">请求 (团队迁移模式) </span><span class="sxs-lookup"><span data-stu-id="1bfd7-187">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="1bfd7-188">响应</span><span class="sxs-lookup"><span data-stu-id="1bfd7-188">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="1bfd7-189">请求 (通道迁移模式) </span><span class="sxs-lookup"><span data-stu-id="1bfd7-189">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="1bfd7-190">响应</span><span class="sxs-lookup"><span data-stu-id="1bfd7-190">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="1bfd7-191">错误响应</span><span class="sxs-lookup"><span data-stu-id="1bfd7-191">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="1bfd7-192">对或不在 `team` `channel` 中调用的操作 `migrationMode` 。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-192">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="1bfd7-193">步骤 5：添加团队成员</span><span class="sxs-lookup"><span data-stu-id="1bfd7-193">Step Five: Add team members</span></span>

<span data-ttu-id="1bfd7-194">可以使用 Teams [UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) 或 Microsoft Graph 添加成员 API 将成员 [添加到团队](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) ：</span><span class="sxs-lookup"><span data-stu-id="1bfd7-194">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="1bfd7-195">请求 (成员) </span><span class="sxs-lookup"><span data-stu-id="1bfd7-195">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="1bfd7-196">响应</span><span class="sxs-lookup"><span data-stu-id="1bfd7-196">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="1bfd7-197">提示和其他信息</span><span class="sxs-lookup"><span data-stu-id="1bfd7-197">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="1bfd7-198">你可以从不在 Teams 中的用户导入邮件。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-198">You can import messages from users who are not in Teams.</span></span> <span data-ttu-id="1bfd7-199">**注意**：为租户中不存在的用户导入的邮件在公共预览版期间在 Teams 客户端或合规性门户中不可搜索。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-199">**NOTE**: Messages imported for users not present in the tenant will not be searchable in the Teams client or compliance portals during Public Preview.</span></span>

* <span data-ttu-id="1bfd7-200">提出 `completeMigration` 请求后，无法向团队导入进一步的消息。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-200">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="1bfd7-201">只有在请求返回成功响应后，才能将团队成员 `completeMigration` 添加到新团队。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-201">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="1bfd7-202">限制：邮件按每个通道 5 RPS 导入。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-202">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="1bfd7-203">如果需要更正迁移结果，需要删除该团队，并重复这些步骤以创建团队和频道并重新迁移邮件。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-203">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="1bfd7-204">目前，内联图像是导入邮件 API 架构唯一支持的媒体类型。</span><span class="sxs-lookup"><span data-stu-id="1bfd7-204">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="1bfd7-205">导入内容范围</span><span class="sxs-lookup"><span data-stu-id="1bfd7-205">Import content scope</span></span>

|<span data-ttu-id="1bfd7-206">作用域内</span><span class="sxs-lookup"><span data-stu-id="1bfd7-206">In-scope</span></span> | <span data-ttu-id="1bfd7-207">当前超出范围</span><span class="sxs-lookup"><span data-stu-id="1bfd7-207">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="1bfd7-208">团队和频道消息</span><span class="sxs-lookup"><span data-stu-id="1bfd7-208">Team and channel messages</span></span>|<span data-ttu-id="1bfd7-209">1：1 和群聊消息</span><span class="sxs-lookup"><span data-stu-id="1bfd7-209">1:1 and group chat messages</span></span>|
|<span data-ttu-id="1bfd7-210">原始邮件的创建时间</span><span class="sxs-lookup"><span data-stu-id="1bfd7-210">Created time of the original message</span></span>|<span data-ttu-id="1bfd7-211">专用频道</span><span class="sxs-lookup"><span data-stu-id="1bfd7-211">Private channels</span></span>|
|<span data-ttu-id="1bfd7-212">作为邮件一部分的内联图像</span><span class="sxs-lookup"><span data-stu-id="1bfd7-212">Inline images as part of the message</span></span>|<span data-ttu-id="1bfd7-213">在提及时</span><span class="sxs-lookup"><span data-stu-id="1bfd7-213">At mentions</span></span>|
|<span data-ttu-id="1bfd7-214">指向 SPO/OneDrive 中的现有文件的链接</span><span class="sxs-lookup"><span data-stu-id="1bfd7-214">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="1bfd7-215">反应</span><span class="sxs-lookup"><span data-stu-id="1bfd7-215">Reactions</span></span>|
|<span data-ttu-id="1bfd7-216">包含格式文本的邮件</span><span class="sxs-lookup"><span data-stu-id="1bfd7-216">Messages with rich text</span></span>|<span data-ttu-id="1bfd7-217">视频</span><span class="sxs-lookup"><span data-stu-id="1bfd7-217">Videos</span></span>|
|<span data-ttu-id="1bfd7-218">邮件回复链</span><span class="sxs-lookup"><span data-stu-id="1bfd7-218">Message reply chain</span></span>|<span data-ttu-id="1bfd7-219">公告</span><span class="sxs-lookup"><span data-stu-id="1bfd7-219">Announcements</span></span>|
|<span data-ttu-id="1bfd7-220">高吞吐量处理</span><span class="sxs-lookup"><span data-stu-id="1bfd7-220">High throughput processing</span></span>|<span data-ttu-id="1bfd7-221">代码段</span><span class="sxs-lookup"><span data-stu-id="1bfd7-221">Code snippets</span></span>|
||<span data-ttu-id="1bfd7-222">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="1bfd7-222">Adaptive cards</span></span>|
||<span data-ttu-id="1bfd7-223">贴纸</span><span class="sxs-lookup"><span data-stu-id="1bfd7-223">Stickers</span></span>|
||<span data-ttu-id="1bfd7-224">表情符号</span><span class="sxs-lookup"><span data-stu-id="1bfd7-224">Emojis</span></span>|
||<span data-ttu-id="1bfd7-225">引号</span><span class="sxs-lookup"><span data-stu-id="1bfd7-225">Quotes</span></span>|
||<span data-ttu-id="1bfd7-226">跨渠道发布</span><span class="sxs-lookup"><span data-stu-id="1bfd7-226">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="1bfd7-227">详细了解 Microsoft Graph 和 Teams 集成</span><span class="sxs-lookup"><span data-stu-id="1bfd7-227">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
