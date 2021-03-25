---
title: 使用 Microsoft Graph 将外部平台消息导入 Teams
description: 介绍如何使用 Microsoft Graph 将邮件从外部平台导入到 Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams 导入消息 api 图形 Microsoft 迁移迁移帖子
ms.openlocfilehash: 8cf4f964aba7ce9375b1b259ae88a7fbcb620631
ms.sourcegitcommit: f6e4a303828224a702138753a8e5e27c8a094c82
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/24/2021
ms.locfileid: "51176954"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="c558c-104">使用 Microsoft Graph 将第三方平台消息导入 Teams</span><span class="sxs-lookup"><span data-stu-id="c558c-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="c558c-105">Microsoft Graph 和 Microsoft Teams 公共预览版可用于早期访问和反馈。</span><span class="sxs-lookup"><span data-stu-id="c558c-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="c558c-106">尽管此版本已经过大量测试，但不适合在生产中使用。</span><span class="sxs-lookup"><span data-stu-id="c558c-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="c558c-107">使用 Microsoft Graph，可以将用户的现有邮件历史记录和数据从外部系统迁移到 Teams 频道。</span><span class="sxs-lookup"><span data-stu-id="c558c-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="c558c-108">通过支持在 Teams 内恢复第三方平台消息层次结构，用户可以无缝地继续通信并不间断地继续。</span><span class="sxs-lookup"><span data-stu-id="c558c-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

> [!NOTE] 
> <span data-ttu-id="c558c-109">将来，Microsoft 可能要求你或你的客户根据导入的数据量支付其他费用。</span><span class="sxs-lookup"><span data-stu-id="c558c-109">In the future, Microsoft may require you or your customers to pay additional fees based on the amount of data imported.</span></span>

## <a name="import-overview"></a><span data-ttu-id="c558c-110">导入概述</span><span class="sxs-lookup"><span data-stu-id="c558c-110">Import overview</span></span>

<span data-ttu-id="c558c-111">在高级别上，导入过程由以下内容组成：</span><span class="sxs-lookup"><span data-stu-id="c558c-111">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="c558c-112">创建具有返回时间戳的团队</span><span class="sxs-lookup"><span data-stu-id="c558c-112">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="c558c-113">创建具有返回时间戳的频道</span><span class="sxs-lookup"><span data-stu-id="c558c-113">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="c558c-114">导入外部实时日期消息</span><span class="sxs-lookup"><span data-stu-id="c558c-114">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="c558c-115">完成团队和频道迁移过程</span><span class="sxs-lookup"><span data-stu-id="c558c-115">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="c558c-116">添加团队成员</span><span class="sxs-lookup"><span data-stu-id="c558c-116">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="c558c-117">所需要求</span><span class="sxs-lookup"><span data-stu-id="c558c-117">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="c558c-118">分析和准备邮件数据</span><span class="sxs-lookup"><span data-stu-id="c558c-118">Analyze and prepare message data</span></span>

<span data-ttu-id="c558c-119">✔查看第三方数据，以决定要迁移哪些内容。</span><span class="sxs-lookup"><span data-stu-id="c558c-119">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="c558c-120">✔第三方聊天系统提取所选数据。</span><span class="sxs-lookup"><span data-stu-id="c558c-120">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="c558c-121">✔将第三方聊天结构映射到 Teams 结构。</span><span class="sxs-lookup"><span data-stu-id="c558c-121">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="c558c-122">✔将导入数据转换为迁移所需的格式。</span><span class="sxs-lookup"><span data-stu-id="c558c-122">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="c558c-123">设置 Office 365 租户</span><span class="sxs-lookup"><span data-stu-id="c558c-123">Set up your Office 365 tenant</span></span>

<span data-ttu-id="c558c-124">✔确保导入数据存在 Office 365 租户。</span><span class="sxs-lookup"><span data-stu-id="c558c-124">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="c558c-125">有关为 Teams 设置 Office 365 租户的信息，请参阅准备[Office 365 租户](../../concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="c558c-125">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="c558c-126">✔确保团队成员在 Azure Active Directory (AAD) 。</span><span class="sxs-lookup"><span data-stu-id="c558c-126">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="c558c-127">有关详细信息，*请参阅将*[新用户添加到](/azure/active-directory/fundamentals/add-users-azure-active-directory)Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="c558c-127">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="c558c-128">步骤 1：创建团队</span><span class="sxs-lookup"><span data-stu-id="c558c-128">Step One: Create a team</span></span>

<span data-ttu-id="c558c-129">由于正在迁移现有数据，因此在迁移过程中保留原始邮件时间戳并阻止邮件活动对于在 Teams 中重新创建用户的现有邮件流很关键。</span><span class="sxs-lookup"><span data-stu-id="c558c-129">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="c558c-130">实现此目的：：</span><span class="sxs-lookup"><span data-stu-id="c558c-130">This is achieved as follows:</span></span>

> <span data-ttu-id="c558c-131">[使用 team 资源](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) 属性创建具有返回时间戳的新  `createdDateTime`  团队。</span><span class="sxs-lookup"><span data-stu-id="c558c-131">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="c558c-132">将新团队放在 `migration mode` 中，这是一种特殊状态，可禁止用户参与团队中的大多数活动，直到迁移过程完成。</span><span class="sxs-lookup"><span data-stu-id="c558c-132">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="c558c-133">在 POST 请求中包括具有 值的 instance 属性，以明确标识正在创建 `teamCreationMode` `migration` 用于迁移的新团队。</span><span class="sxs-lookup"><span data-stu-id="c558c-133">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> <span data-ttu-id="c558c-134">**注意** `createdDateTime` ：将仅为已迁移的团队或频道的实例填充该字段。</span><span class="sxs-lookup"><span data-stu-id="c558c-134">**NOTE**:  The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="c558c-135">权限</span><span class="sxs-lookup"><span data-stu-id="c558c-135">Permissions</span></span>

|<span data-ttu-id="c558c-136">ScopeName</span><span class="sxs-lookup"><span data-stu-id="c558c-136">ScopeName</span></span>|<span data-ttu-id="c558c-137">DisplayName</span><span class="sxs-lookup"><span data-stu-id="c558c-137">DisplayName</span></span>|<span data-ttu-id="c558c-138">说明</span><span class="sxs-lookup"><span data-stu-id="c558c-138">Description</span></span>|<span data-ttu-id="c558c-139">类型</span><span class="sxs-lookup"><span data-stu-id="c558c-139">Type</span></span>|<span data-ttu-id="c558c-140">管理员同意？</span><span class="sxs-lookup"><span data-stu-id="c558c-140">Admin Consent?</span></span>|<span data-ttu-id="c558c-141">涵盖的实体/API</span><span class="sxs-lookup"><span data-stu-id="c558c-141">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="c558c-142">管理迁移到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c558c-142">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="c558c-143">创建、管理迁移到 Microsoft Teams 的资源</span><span class="sxs-lookup"><span data-stu-id="c558c-143">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="c558c-144">**仅应用程序**</span><span class="sxs-lookup"><span data-stu-id="c558c-144">**Application-only**</span></span>|<span data-ttu-id="c558c-145">**是**</span><span class="sxs-lookup"><span data-stu-id="c558c-145">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="c558c-146">请求 (迁移状态创建) </span><span class="sxs-lookup"><span data-stu-id="c558c-146">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="c558c-147">响应</span><span class="sxs-lookup"><span data-stu-id="c558c-147">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="c558c-148">错误消息</span><span class="sxs-lookup"><span data-stu-id="c558c-148">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="c558c-149">`createdDateTime`  设置供将来使用。</span><span class="sxs-lookup"><span data-stu-id="c558c-149">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="c558c-150">`createdDateTime`  正确指定，但 `teamCreationMode`  实例属性缺失或设置为无效值。</span><span class="sxs-lookup"><span data-stu-id="c558c-150">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="c558c-151">步骤 2：创建通道</span><span class="sxs-lookup"><span data-stu-id="c558c-151">Step Two: Create a channel</span></span>

<span data-ttu-id="c558c-152">为导入的消息创建频道与创建团队方案类似：</span><span class="sxs-lookup"><span data-stu-id="c558c-152">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="c558c-153">[使用 channel 资源](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) 属性创建具有返回时间戳的新 `createdDateTime` 频道。</span><span class="sxs-lookup"><span data-stu-id="c558c-153">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="c558c-154">将新频道放在 中，这是一种特殊状态，可禁止用户参与频道内大多数聊天活动，直到 `migration mode` 迁移过程完成。</span><span class="sxs-lookup"><span data-stu-id="c558c-154">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="c558c-155">在 POST 请求中包括具有 值的 instance 属性，以明确标识正在创建 `channelCreationMode` `migration` 用于迁移的新团队。</span><span class="sxs-lookup"><span data-stu-id="c558c-155">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="c558c-156">权限</span><span class="sxs-lookup"><span data-stu-id="c558c-156">Permissions</span></span>

|<span data-ttu-id="c558c-157">ScopeName</span><span class="sxs-lookup"><span data-stu-id="c558c-157">ScopeName</span></span>|<span data-ttu-id="c558c-158">DisplayName</span><span class="sxs-lookup"><span data-stu-id="c558c-158">DisplayName</span></span>|<span data-ttu-id="c558c-159">说明</span><span class="sxs-lookup"><span data-stu-id="c558c-159">Description</span></span>|<span data-ttu-id="c558c-160">类型</span><span class="sxs-lookup"><span data-stu-id="c558c-160">Type</span></span>|<span data-ttu-id="c558c-161">管理员同意？</span><span class="sxs-lookup"><span data-stu-id="c558c-161">Admin Consent?</span></span>|<span data-ttu-id="c558c-162">涵盖的实体/API</span><span class="sxs-lookup"><span data-stu-id="c558c-162">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="c558c-163">管理迁移到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c558c-163">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="c558c-164">创建、管理迁移到 Microsoft Teams 的资源</span><span class="sxs-lookup"><span data-stu-id="c558c-164">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="c558c-165">**仅应用程序**</span><span class="sxs-lookup"><span data-stu-id="c558c-165">**Application-only**</span></span>|<span data-ttu-id="c558c-166">**是**</span><span class="sxs-lookup"><span data-stu-id="c558c-166">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="c558c-167">请求 (在迁移状态创建) </span><span class="sxs-lookup"><span data-stu-id="c558c-167">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="c558c-168">响应</span><span class="sxs-lookup"><span data-stu-id="c558c-168">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="c558c-169">错误消息</span><span class="sxs-lookup"><span data-stu-id="c558c-169">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="c558c-170">`createdDateTime`  设置供将来使用。</span><span class="sxs-lookup"><span data-stu-id="c558c-170">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="c558c-171">`createdDateTime`  正确指定， `channelCreationMode`  但实例属性缺失或设置为无效值。</span><span class="sxs-lookup"><span data-stu-id="c558c-171">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="c558c-172">步骤 3：导入邮件</span><span class="sxs-lookup"><span data-stu-id="c558c-172">Step Three: Import messages</span></span>

<span data-ttu-id="c558c-173">创建团队和频道后，可以使用 请求正文中的 和 键开始发送返回 `createdDateTime` `from`  时间消息。</span><span class="sxs-lookup"><span data-stu-id="c558c-173">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="c558c-174">**注意**：不支持使用早于 `createdDateTime` 消息线程导入 `createdDateTime` 的邮件。</span><span class="sxs-lookup"><span data-stu-id="c558c-174">**NOTE**: messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> * <span data-ttu-id="c558c-175">`createdDateTime` 对于同一线程中的消息，必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="c558c-175">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="c558c-176">`createdDateTime` 支持具有毫秒精度的时间戳。</span><span class="sxs-lookup"><span data-stu-id="c558c-176">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="c558c-177">例如，如果传入请求邮件的值设置为 `createdDateTime` *2020-09-16T05：50：31.0025302Z，* 那么在接收邮件时，它将转换为 *2020-09-16T05：50：31.002Z。*</span><span class="sxs-lookup"><span data-stu-id="c558c-177">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="c558c-178">请求 (纯文本的 POST) </span><span class="sxs-lookup"><span data-stu-id="c558c-178">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="c558c-179">响应</span><span class="sxs-lookup"><span data-stu-id="c558c-179">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="c558c-180">错误消息</span><span class="sxs-lookup"><span data-stu-id="c558c-180">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="c558c-181">请求 (内联图像消息 POST) </span><span class="sxs-lookup"><span data-stu-id="c558c-181">Request (POST a message with inline image)</span></span>

> <span data-ttu-id="c558c-182">**注意**：此方案中没有特殊权限范围，因为请求是 chatMessage 的一部分;chatMessage 的范围也适用于此处。</span><span class="sxs-lookup"><span data-stu-id="c558c-182">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="c558c-183">响应</span><span class="sxs-lookup"><span data-stu-id="c558c-183">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="c558c-184">步骤 4：完成迁移模式</span><span class="sxs-lookup"><span data-stu-id="c558c-184">Step Four: Complete migration mode</span></span>

<span data-ttu-id="c558c-185">完成邮件迁移过程后，团队和频道均会使用 方法退出迁移  `completeMigration`  模式。</span><span class="sxs-lookup"><span data-stu-id="c558c-185">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="c558c-186">此步骤将打开工作组和频道资源，供工作组成员常规使用。</span><span class="sxs-lookup"><span data-stu-id="c558c-186">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="c558c-187">操作绑定到 `team` 实例。</span><span class="sxs-lookup"><span data-stu-id="c558c-187">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="c558c-188">请求 (团队迁移模式) </span><span class="sxs-lookup"><span data-stu-id="c558c-188">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="c558c-189">响应</span><span class="sxs-lookup"><span data-stu-id="c558c-189">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="c558c-190">请求 (通道迁移模式) </span><span class="sxs-lookup"><span data-stu-id="c558c-190">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="c558c-191">响应</span><span class="sxs-lookup"><span data-stu-id="c558c-191">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="c558c-192">错误响应</span><span class="sxs-lookup"><span data-stu-id="c558c-192">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="c558c-193">对 不在 `team` 中的 或 `channel` 调用的操作 `migrationMode` 。</span><span class="sxs-lookup"><span data-stu-id="c558c-193">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="c558c-194">步骤 5：添加团队成员</span><span class="sxs-lookup"><span data-stu-id="c558c-194">Step Five: Add team members</span></span>

<span data-ttu-id="c558c-195">可以使用 Teams UI 或 Microsoft Graph 添加成员 [API](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) 将成员 [添加到](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) 团队：</span><span class="sxs-lookup"><span data-stu-id="c558c-195">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="c558c-196">请求 (添加成员) </span><span class="sxs-lookup"><span data-stu-id="c558c-196">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="c558c-197">响应</span><span class="sxs-lookup"><span data-stu-id="c558c-197">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="c558c-198">提示和其他信息</span><span class="sxs-lookup"><span data-stu-id="c558c-198">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="c558c-199">你可以从不在 Teams 中的用户导入消息。</span><span class="sxs-lookup"><span data-stu-id="c558c-199">You can import messages from users who are not in Teams.</span></span> <span data-ttu-id="c558c-200">**注意**：在公共预览版期间，为租户中不存在的用户导入的消息在 Teams 客户端或合规性门户中不可搜索。</span><span class="sxs-lookup"><span data-stu-id="c558c-200">**NOTE**: Messages imported for users not present in the tenant will not be searchable in the Teams client or compliance portals during Public Preview.</span></span>

* <span data-ttu-id="c558c-201">提出 `completeMigration` 请求后，你将无法将进一步的消息导入团队。</span><span class="sxs-lookup"><span data-stu-id="c558c-201">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="c558c-202">仅在请求返回成功响应后，才能将团队成员 `completeMigration` 添加到新团队。</span><span class="sxs-lookup"><span data-stu-id="c558c-202">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="c558c-203">限制：邮件以每个通道 5 RPS 的速度导入。</span><span class="sxs-lookup"><span data-stu-id="c558c-203">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="c558c-204">如果需要更正迁移结果，则需要删除该团队，并重复这些步骤以创建团队和频道，然后重新迁移邮件。</span><span class="sxs-lookup"><span data-stu-id="c558c-204">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="c558c-205">目前，内联图像是导入邮件 API 架构支持的唯一媒体类型。</span><span class="sxs-lookup"><span data-stu-id="c558c-205">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="c558c-206">导入内容范围</span><span class="sxs-lookup"><span data-stu-id="c558c-206">Import content scope</span></span>

|<span data-ttu-id="c558c-207">范围内</span><span class="sxs-lookup"><span data-stu-id="c558c-207">In-scope</span></span> | <span data-ttu-id="c558c-208">当前超出范围</span><span class="sxs-lookup"><span data-stu-id="c558c-208">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="c558c-209">团队和频道消息</span><span class="sxs-lookup"><span data-stu-id="c558c-209">Team and channel messages</span></span>|<span data-ttu-id="c558c-210">1：1 和群聊消息</span><span class="sxs-lookup"><span data-stu-id="c558c-210">1:1 and group chat messages</span></span>|
|<span data-ttu-id="c558c-211">原始邮件的创建时间</span><span class="sxs-lookup"><span data-stu-id="c558c-211">Created time of the original message</span></span>|<span data-ttu-id="c558c-212">专用频道</span><span class="sxs-lookup"><span data-stu-id="c558c-212">Private channels</span></span>|
|<span data-ttu-id="c558c-213">作为邮件一部分的内联图像</span><span class="sxs-lookup"><span data-stu-id="c558c-213">Inline images as part of the message</span></span>|<span data-ttu-id="c558c-214">在提及时</span><span class="sxs-lookup"><span data-stu-id="c558c-214">At mentions</span></span>|
|<span data-ttu-id="c558c-215">指向 SPO/OneDrive 中的现有文件的链接</span><span class="sxs-lookup"><span data-stu-id="c558c-215">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="c558c-216">反应</span><span class="sxs-lookup"><span data-stu-id="c558c-216">Reactions</span></span>|
|<span data-ttu-id="c558c-217">包含格式文本的邮件</span><span class="sxs-lookup"><span data-stu-id="c558c-217">Messages with rich text</span></span>|<span data-ttu-id="c558c-218">视频</span><span class="sxs-lookup"><span data-stu-id="c558c-218">Videos</span></span>|
|<span data-ttu-id="c558c-219">邮件回复链</span><span class="sxs-lookup"><span data-stu-id="c558c-219">Message reply chain</span></span>|<span data-ttu-id="c558c-220">公告</span><span class="sxs-lookup"><span data-stu-id="c558c-220">Announcements</span></span>|
|<span data-ttu-id="c558c-221">高吞吐量处理</span><span class="sxs-lookup"><span data-stu-id="c558c-221">High throughput processing</span></span>|<span data-ttu-id="c558c-222">代码段</span><span class="sxs-lookup"><span data-stu-id="c558c-222">Code snippets</span></span>|
||<span data-ttu-id="c558c-223">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="c558c-223">Adaptive cards</span></span>|
||<span data-ttu-id="c558c-224">贴纸</span><span class="sxs-lookup"><span data-stu-id="c558c-224">Stickers</span></span>|
||<span data-ttu-id="c558c-225">表情符号</span><span class="sxs-lookup"><span data-stu-id="c558c-225">Emojis</span></span>|
||<span data-ttu-id="c558c-226">引号</span><span class="sxs-lookup"><span data-stu-id="c558c-226">Quotes</span></span>|
||<span data-ttu-id="c558c-227">跨渠道发布</span><span class="sxs-lookup"><span data-stu-id="c558c-227">Cross posts between channels</span></span>|


## <a name="see-also"></a><span data-ttu-id="c558c-228">另请参阅</span><span class="sxs-lookup"><span data-stu-id="c558c-228">See also</span></span>
> [!div class="nextstepaction"]
>[<span data-ttu-id="c558c-229">详细了解 Microsoft Graph 和 Teams 集成</span><span class="sxs-lookup"><span data-stu-id="c558c-229">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
