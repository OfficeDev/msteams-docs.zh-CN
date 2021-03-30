---
title: 使用 Microsoft Graph 将外部平台消息导入 Teams
description: 介绍如何使用 Microsoft Graph 将邮件从外部平台导入到 Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams 导入消息 api 图形 Microsoft 迁移迁移帖子
ms.openlocfilehash: 1b5a8ccc243c795801552519b4b52f51366e047d
ms.sourcegitcommit: c9446200b8e76fbd434d012dc11dd9f191776d13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2021
ms.locfileid: "51403967"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="7093e-104">使用 Microsoft Graph 将第三方平台消息导入 Teams</span><span class="sxs-lookup"><span data-stu-id="7093e-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

<span data-ttu-id="7093e-105">使用 Microsoft Graph，可以将用户的现有邮件历史记录和数据从外部系统迁移到 Teams 频道。</span><span class="sxs-lookup"><span data-stu-id="7093e-105">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="7093e-106">通过支持在 Teams 内恢复第三方平台消息层次结构，用户可以无缝地继续通信并不间断地继续。</span><span class="sxs-lookup"><span data-stu-id="7093e-106">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

> [!NOTE] 
> <span data-ttu-id="7093e-107">将来，Microsoft 可能要求你或你的客户根据导入的数据量支付其他费用。</span><span class="sxs-lookup"><span data-stu-id="7093e-107">In the future, Microsoft may require you or your customers to pay additional fees based on the amount of data imported.</span></span>

## <a name="import-overview"></a><span data-ttu-id="7093e-108">导入概述</span><span class="sxs-lookup"><span data-stu-id="7093e-108">Import overview</span></span>

<span data-ttu-id="7093e-109">在高级别上，导入过程由以下内容组成：</span><span class="sxs-lookup"><span data-stu-id="7093e-109">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="7093e-110">创建具有返回时间戳的团队</span><span class="sxs-lookup"><span data-stu-id="7093e-110">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="7093e-111">创建具有返回时间戳的频道</span><span class="sxs-lookup"><span data-stu-id="7093e-111">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="7093e-112">导入外部实时日期消息</span><span class="sxs-lookup"><span data-stu-id="7093e-112">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="7093e-113">完成团队和频道迁移过程</span><span class="sxs-lookup"><span data-stu-id="7093e-113">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="7093e-114">添加团队成员</span><span class="sxs-lookup"><span data-stu-id="7093e-114">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="7093e-115">所需要求</span><span class="sxs-lookup"><span data-stu-id="7093e-115">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="7093e-116">分析和准备邮件数据</span><span class="sxs-lookup"><span data-stu-id="7093e-116">Analyze and prepare message data</span></span>

<span data-ttu-id="7093e-117">✔查看第三方数据，以决定要迁移哪些内容。</span><span class="sxs-lookup"><span data-stu-id="7093e-117">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="7093e-118">✔第三方聊天系统提取所选数据。</span><span class="sxs-lookup"><span data-stu-id="7093e-118">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="7093e-119">✔将第三方聊天结构映射到 Teams 结构。</span><span class="sxs-lookup"><span data-stu-id="7093e-119">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="7093e-120">✔将导入数据转换为迁移所需的格式。</span><span class="sxs-lookup"><span data-stu-id="7093e-120">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="7093e-121">设置 Office 365 租户</span><span class="sxs-lookup"><span data-stu-id="7093e-121">Set up your Office 365 tenant</span></span>

<span data-ttu-id="7093e-122">✔确保导入数据存在 Office 365 租户。</span><span class="sxs-lookup"><span data-stu-id="7093e-122">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="7093e-123">有关为 Teams 设置 Office 365 租户的信息，请参阅准备[Office 365 租户](../../concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="7093e-123">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="7093e-124">✔确保团队成员在 Azure Active Directory (AAD) 。</span><span class="sxs-lookup"><span data-stu-id="7093e-124">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="7093e-125">有关详细信息，*请参阅将*[新用户添加到](/azure/active-directory/fundamentals/add-users-azure-active-directory)Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="7093e-125">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="7093e-126">步骤 1：创建团队</span><span class="sxs-lookup"><span data-stu-id="7093e-126">Step One: Create a team</span></span>

<span data-ttu-id="7093e-127">由于正在迁移现有数据，因此在迁移过程中保留原始邮件时间戳并阻止邮件活动对于在 Teams 中重新创建用户的现有邮件流很关键。</span><span class="sxs-lookup"><span data-stu-id="7093e-127">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="7093e-128">实现此目的：：</span><span class="sxs-lookup"><span data-stu-id="7093e-128">This is achieved as follows:</span></span>

> <span data-ttu-id="7093e-129">[使用 team 资源](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) 属性创建具有返回时间戳的新  `createdDateTime`  团队。</span><span class="sxs-lookup"><span data-stu-id="7093e-129">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="7093e-130">将新团队放在 `migration mode` 中，这是一种特殊状态，可禁止用户参与团队中的大多数活动，直到迁移过程完成。</span><span class="sxs-lookup"><span data-stu-id="7093e-130">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="7093e-131">在 POST 请求中包括具有 值的 instance 属性，以明确标识正在创建 `teamCreationMode` `migration` 用于迁移的新团队。</span><span class="sxs-lookup"><span data-stu-id="7093e-131">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> <span data-ttu-id="7093e-132">**注意** `createdDateTime` ：将仅为已迁移的团队或频道的实例填充该字段。</span><span class="sxs-lookup"><span data-stu-id="7093e-132">**NOTE**:  The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="7093e-133">权限</span><span class="sxs-lookup"><span data-stu-id="7093e-133">Permissions</span></span>

|<span data-ttu-id="7093e-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="7093e-134">ScopeName</span></span>|<span data-ttu-id="7093e-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="7093e-135">DisplayName</span></span>|<span data-ttu-id="7093e-136">说明</span><span class="sxs-lookup"><span data-stu-id="7093e-136">Description</span></span>|<span data-ttu-id="7093e-137">类型</span><span class="sxs-lookup"><span data-stu-id="7093e-137">Type</span></span>|<span data-ttu-id="7093e-138">管理员同意？</span><span class="sxs-lookup"><span data-stu-id="7093e-138">Admin Consent?</span></span>|<span data-ttu-id="7093e-139">涵盖的实体/API</span><span class="sxs-lookup"><span data-stu-id="7093e-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="7093e-140">管理迁移到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7093e-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="7093e-141">创建、管理迁移到 Microsoft Teams 的资源</span><span class="sxs-lookup"><span data-stu-id="7093e-141">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="7093e-142">**仅应用程序**</span><span class="sxs-lookup"><span data-stu-id="7093e-142">**Application-only**</span></span>|<span data-ttu-id="7093e-143">**是**</span><span class="sxs-lookup"><span data-stu-id="7093e-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="7093e-144">请求 (迁移状态创建) </span><span class="sxs-lookup"><span data-stu-id="7093e-144">Request (create a team in migration state)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/v1.0/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.043Z"
}
```

#### <a name="response"></a><span data-ttu-id="7093e-145">响应</span><span class="sxs-lookup"><span data-stu-id="7093e-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{team-id}/operations/{operation-id}
Content-Location: /teams/{team-id}
```

#### <a name="error-messages"></a><span data-ttu-id="7093e-146">错误消息</span><span class="sxs-lookup"><span data-stu-id="7093e-146">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="7093e-147">`createdDateTime`  设置供将来使用。</span><span class="sxs-lookup"><span data-stu-id="7093e-147">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="7093e-148">`createdDateTime`  正确指定，但 `teamCreationMode`  实例属性缺失或设置为无效值。</span><span class="sxs-lookup"><span data-stu-id="7093e-148">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="7093e-149">步骤 2：创建通道</span><span class="sxs-lookup"><span data-stu-id="7093e-149">Step Two: Create a channel</span></span>

<span data-ttu-id="7093e-150">为导入的消息创建频道与创建团队方案类似：</span><span class="sxs-lookup"><span data-stu-id="7093e-150">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="7093e-151">[使用 channel 资源](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) 属性创建具有返回时间戳的新 `createdDateTime` 频道。</span><span class="sxs-lookup"><span data-stu-id="7093e-151">[Create a new channel](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="7093e-152">将新频道放在 中，这是一种特殊状态，可禁止用户参与频道内大多数聊天活动，直到 `migration mode` 迁移过程完成。</span><span class="sxs-lookup"><span data-stu-id="7093e-152">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="7093e-153">在 POST 请求中包括具有 值的 instance 属性，以明确标识正在创建 `channelCreationMode` `migration` 用于迁移的新团队。</span><span class="sxs-lookup"><span data-stu-id="7093e-153">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="7093e-154">权限</span><span class="sxs-lookup"><span data-stu-id="7093e-154">Permissions</span></span>

|<span data-ttu-id="7093e-155">ScopeName</span><span class="sxs-lookup"><span data-stu-id="7093e-155">ScopeName</span></span>|<span data-ttu-id="7093e-156">DisplayName</span><span class="sxs-lookup"><span data-stu-id="7093e-156">DisplayName</span></span>|<span data-ttu-id="7093e-157">说明</span><span class="sxs-lookup"><span data-stu-id="7093e-157">Description</span></span>|<span data-ttu-id="7093e-158">类型</span><span class="sxs-lookup"><span data-stu-id="7093e-158">Type</span></span>|<span data-ttu-id="7093e-159">管理员同意？</span><span class="sxs-lookup"><span data-stu-id="7093e-159">Admin Consent?</span></span>|<span data-ttu-id="7093e-160">涵盖的实体/API</span><span class="sxs-lookup"><span data-stu-id="7093e-160">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="7093e-161">管理迁移到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7093e-161">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="7093e-162">创建、管理迁移到 Microsoft Teams 的资源</span><span class="sxs-lookup"><span data-stu-id="7093e-162">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="7093e-163">**仅应用程序**</span><span class="sxs-lookup"><span data-stu-id="7093e-163">**Application-only**</span></span>|<span data-ttu-id="7093e-164">**是**</span><span class="sxs-lookup"><span data-stu-id="7093e-164">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="7093e-165">请求 (在迁移状态创建) </span><span class="sxs-lookup"><span data-stu-id="7093e-165">Request (create a channel in migration state)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/{team-id}/channels

Content-Type: application/json
{
  "@microsoft.graph.channelCreationMode": "migration",
  "displayName": "Architecture Discussion",
  "description": "This channel is where we debate all future architecture plans",
  "membershipType": "standard",
  "createdDateTime": "2020-03-14T11:22:17.047Z"
}
```

#### <a name="response"></a><span data-ttu-id="7093e-166">响应</span><span class="sxs-lookup"><span data-stu-id="7093e-166">Response</span></span>

```http
HTTP/1.1 202 Accepted

{
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels/$entity",
   "id":"id-value",
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

#### <a name="error-message"></a><span data-ttu-id="7093e-167">错误消息</span><span class="sxs-lookup"><span data-stu-id="7093e-167">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="7093e-168">`createdDateTime`  设置供将来使用。</span><span class="sxs-lookup"><span data-stu-id="7093e-168">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="7093e-169">`createdDateTime`  正确指定， `channelCreationMode`  但实例属性缺失或设置为无效值。</span><span class="sxs-lookup"><span data-stu-id="7093e-169">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="7093e-170">步骤 3：导入邮件</span><span class="sxs-lookup"><span data-stu-id="7093e-170">Step Three: Import messages</span></span>

<span data-ttu-id="7093e-171">创建团队和频道后，可以使用 请求正文中的 和 键开始发送返回 `createdDateTime` `from`  时间消息。</span><span class="sxs-lookup"><span data-stu-id="7093e-171">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="7093e-172">**注意**：不支持使用早于 `createdDateTime` 消息线程导入 `createdDateTime` 的邮件。</span><span class="sxs-lookup"><span data-stu-id="7093e-172">**NOTE**: messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> * <span data-ttu-id="7093e-173">`createdDateTime` 对于同一线程中的消息，必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="7093e-173">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="7093e-174">`createdDateTime` 支持具有毫秒精度的时间戳。</span><span class="sxs-lookup"><span data-stu-id="7093e-174">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="7093e-175">例如，如果传入请求邮件的值设置为 `createdDateTime` *2020-09-16T05：50：31.0025302Z，* 那么在接收邮件时，它将转换为 *2020-09-16T05：50：31.002Z。*</span><span class="sxs-lookup"><span data-stu-id="7093e-175">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="7093e-176">请求 (纯文本的 POST) </span><span class="sxs-lookup"><span data-stu-id="7093e-176">Request (POST message that is text-only)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/messages

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

#### <a name="response"></a><span data-ttu-id="7093e-177">响应</span><span class="sxs-lookup"><span data-stu-id="7093e-177">Response</span></span>

```http
HTTP/1.1 200 OK

{
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels('channel-id')/messages/$entity",
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

#### <a name="error-messages"></a><span data-ttu-id="7093e-178">错误消息</span><span class="sxs-lookup"><span data-stu-id="7093e-178">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="7093e-179">请求 (内联图像消息 POST) </span><span class="sxs-lookup"><span data-stu-id="7093e-179">Request (POST a message with inline image)</span></span>

> <span data-ttu-id="7093e-180">**注意**：此方案中没有特殊权限范围，因为请求是 chatMessage 的一部分;chatMessage 的范围也适用于此处。</span><span class="sxs-lookup"><span data-stu-id="7093e-180">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/messages

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

#### <a name="response"></a><span data-ttu-id="7093e-181">响应</span><span class="sxs-lookup"><span data-stu-id="7093e-181">Response</span></span>

```http
HTTP/1.1 200 OK

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels('channel-id')/messages/$entity",
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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="7093e-182">步骤 4：完成迁移模式</span><span class="sxs-lookup"><span data-stu-id="7093e-182">Step Four: Complete migration mode</span></span>

<span data-ttu-id="7093e-183">完成邮件迁移过程后，团队和频道均会使用 方法退出迁移  `completeMigration`  模式。</span><span class="sxs-lookup"><span data-stu-id="7093e-183">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="7093e-184">此步骤将打开工作组和频道资源，供工作组成员常规使用。</span><span class="sxs-lookup"><span data-stu-id="7093e-184">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="7093e-185">操作绑定到 `team` 实例。</span><span class="sxs-lookup"><span data-stu-id="7093e-185">The action is bound to the `team` instance.</span></span> <span data-ttu-id="7093e-186">所有频道都必须在迁移模式下完成，然后才能完成团队。</span><span class="sxs-lookup"><span data-stu-id="7093e-186">All channels must be completed out of migration mode before the team can be completed.</span></span>

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="7093e-187">请求 (通道迁移模式) </span><span class="sxs-lookup"><span data-stu-id="7093e-187">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a><span data-ttu-id="7093e-188">响应</span><span class="sxs-lookup"><span data-stu-id="7093e-188">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="7093e-189">请求 (团队迁移模式) </span><span class="sxs-lookup"><span data-stu-id="7093e-189">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a><span data-ttu-id="7093e-190">响应</span><span class="sxs-lookup"><span data-stu-id="7093e-190">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

* <span data-ttu-id="7093e-191">对 不在 `team` 中的 或 `channel` 调用的操作 `migrationMode` 。</span><span class="sxs-lookup"><span data-stu-id="7093e-191">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="7093e-192">步骤 5：添加团队成员</span><span class="sxs-lookup"><span data-stu-id="7093e-192">Step Five: Add team members</span></span>

<span data-ttu-id="7093e-193">可以使用 Teams UI 或 Microsoft Graph 添加成员 [API](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) 将成员 [添加到](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) 团队：</span><span class="sxs-lookup"><span data-stu-id="7093e-193">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="7093e-194">请求 (添加成员) </span><span class="sxs-lookup"><span data-stu-id="7093e-194">Request (add member)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/{team-id}/members
Content-type: application/json
Content-length: 30
{
"@odata.type": "#microsoft.graph.aadUserConversationMember",
"roles": [],
"user@odata.bind": "https://graph.microsoft.com/beta/users/{user-id}"
}
```

#### <a name="response"></a><span data-ttu-id="7093e-195">响应</span><span class="sxs-lookup"><span data-stu-id="7093e-195">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="7093e-196">提示和其他信息</span><span class="sxs-lookup"><span data-stu-id="7093e-196">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="7093e-197">提出 `completeMigration` 请求后，你将无法将进一步的消息导入团队。</span><span class="sxs-lookup"><span data-stu-id="7093e-197">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="7093e-198">仅在请求返回成功响应后，才能将团队成员 `completeMigration` 添加到新团队。</span><span class="sxs-lookup"><span data-stu-id="7093e-198">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="7093e-199">限制：邮件以每个通道 5 RPS 的速度导入。</span><span class="sxs-lookup"><span data-stu-id="7093e-199">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="7093e-200">如果需要更正迁移结果，则需要删除该团队，并重复这些步骤以创建团队和频道，然后重新迁移邮件。</span><span class="sxs-lookup"><span data-stu-id="7093e-200">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="7093e-201">目前，内联图像是导入邮件 API 架构支持的唯一媒体类型。</span><span class="sxs-lookup"><span data-stu-id="7093e-201">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="7093e-202">导入内容范围</span><span class="sxs-lookup"><span data-stu-id="7093e-202">Import content scope</span></span>

|<span data-ttu-id="7093e-203">范围内</span><span class="sxs-lookup"><span data-stu-id="7093e-203">In-scope</span></span> | <span data-ttu-id="7093e-204">当前超出范围</span><span class="sxs-lookup"><span data-stu-id="7093e-204">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="7093e-205">团队和频道消息</span><span class="sxs-lookup"><span data-stu-id="7093e-205">Team and channel messages</span></span>|<span data-ttu-id="7093e-206">1：1 和群聊消息</span><span class="sxs-lookup"><span data-stu-id="7093e-206">1:1 and group chat messages</span></span>|
|<span data-ttu-id="7093e-207">原始邮件的创建时间</span><span class="sxs-lookup"><span data-stu-id="7093e-207">Created time of the original message</span></span>|<span data-ttu-id="7093e-208">专用频道</span><span class="sxs-lookup"><span data-stu-id="7093e-208">Private channels</span></span>|
|<span data-ttu-id="7093e-209">作为邮件一部分的内联图像</span><span class="sxs-lookup"><span data-stu-id="7093e-209">Inline images as part of the message</span></span>|<span data-ttu-id="7093e-210">在提及时</span><span class="sxs-lookup"><span data-stu-id="7093e-210">At mentions</span></span>|
|<span data-ttu-id="7093e-211">指向 SPO/OneDrive 中的现有文件的链接</span><span class="sxs-lookup"><span data-stu-id="7093e-211">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="7093e-212">反应</span><span class="sxs-lookup"><span data-stu-id="7093e-212">Reactions</span></span>|
|<span data-ttu-id="7093e-213">包含格式文本的邮件</span><span class="sxs-lookup"><span data-stu-id="7093e-213">Messages with rich text</span></span>|<span data-ttu-id="7093e-214">视频</span><span class="sxs-lookup"><span data-stu-id="7093e-214">Videos</span></span>|
|<span data-ttu-id="7093e-215">邮件回复链</span><span class="sxs-lookup"><span data-stu-id="7093e-215">Message reply chain</span></span>|<span data-ttu-id="7093e-216">公告</span><span class="sxs-lookup"><span data-stu-id="7093e-216">Announcements</span></span>|
|<span data-ttu-id="7093e-217">高吞吐量处理</span><span class="sxs-lookup"><span data-stu-id="7093e-217">High throughput processing</span></span>|<span data-ttu-id="7093e-218">代码段</span><span class="sxs-lookup"><span data-stu-id="7093e-218">Code snippets</span></span>|
||<span data-ttu-id="7093e-219">贴纸</span><span class="sxs-lookup"><span data-stu-id="7093e-219">Stickers</span></span>|
||<span data-ttu-id="7093e-220">表情符号</span><span class="sxs-lookup"><span data-stu-id="7093e-220">Emojis</span></span>|
||<span data-ttu-id="7093e-221">引号</span><span class="sxs-lookup"><span data-stu-id="7093e-221">Quotes</span></span>|
||<span data-ttu-id="7093e-222">跨渠道发布</span><span class="sxs-lookup"><span data-stu-id="7093e-222">Cross posts between channels</span></span>|


## <a name="see-also"></a><span data-ttu-id="7093e-223">另请参阅</span><span class="sxs-lookup"><span data-stu-id="7093e-223">See also</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="7093e-224">详细了解 Microsoft Graph 和 Teams 集成</span><span class="sxs-lookup"><span data-stu-id="7093e-224">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
