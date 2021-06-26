---
title: 使用 Microsoft Graph将外部平台消息导入Teams
description: 介绍如何使用 Microsoft Graph将邮件从外部平台导入到Teams
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: Teams 导入消息 api 图形 Microsoft 迁移迁移帖子
ms.openlocfilehash: 95cbf6bf2deac4ea71e60fe0fece06c1dd3ad24c
ms.sourcegitcommit: 656a1de9e23e0ad90dddcb93a2bbfcc63848a856
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53130092"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="e2765-104">使用 Microsoft Graph 将第三方平台消息导入 Teams</span><span class="sxs-lookup"><span data-stu-id="e2765-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

<span data-ttu-id="e2765-105">使用 Microsoft Graph，可以将用户的现有邮件历史记录和数据从外部系统迁移到 Teams 通道。</span><span class="sxs-lookup"><span data-stu-id="e2765-105">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="e2765-106">通过支持在 Teams 内恢复第三方平台消息层次结构，用户可以无缝地继续通信并不间断地继续。</span><span class="sxs-lookup"><span data-stu-id="e2765-106">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

> [!NOTE]
> <span data-ttu-id="e2765-107">将来，Microsoft 可能要求你或你的客户根据导入的数据量支付其他费用。</span><span class="sxs-lookup"><span data-stu-id="e2765-107">In the future, Microsoft may require you or your customers to pay additional fees based on the amount of data imported.</span></span>

## <a name="import-overview"></a><span data-ttu-id="e2765-108">导入概述</span><span class="sxs-lookup"><span data-stu-id="e2765-108">Import overview</span></span>

<span data-ttu-id="e2765-109">在高级别上，导入过程由以下内容组成：</span><span class="sxs-lookup"><span data-stu-id="e2765-109">At a high level, the import process consists of the following:</span></span>

1. <span data-ttu-id="e2765-110">[创建具有返回时间戳](#step-1-create-a-team)的团队。</span><span class="sxs-lookup"><span data-stu-id="e2765-110">[Create a team with a back-in-time timestamp](#step-1-create-a-team).</span></span>
1. <span data-ttu-id="e2765-111">[创建具有返回时间戳的频道](#step-2-create-a-channel)。</span><span class="sxs-lookup"><span data-stu-id="e2765-111">[Create a channel with a back-in-time timestamp](#step-2-create-a-channel).</span></span>
1. <span data-ttu-id="e2765-112">[导入外部的反时日期消息](#step-3-import-messages)。</span><span class="sxs-lookup"><span data-stu-id="e2765-112">[Import external back-in-time dated messages](#step-3-import-messages).</span></span>
1. <span data-ttu-id="e2765-113">[完成团队和频道迁移过程](#step-4-complete-migration-mode)。</span><span class="sxs-lookup"><span data-stu-id="e2765-113">[Complete the team and channel migration process](#step-4-complete-migration-mode).</span></span>
1. <span data-ttu-id="e2765-114">[添加团队成员](#step-five-add-team-members)。</span><span class="sxs-lookup"><span data-stu-id="e2765-114">[Add team members](#step-five-add-team-members).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2765-115">先决条件</span><span class="sxs-lookup"><span data-stu-id="e2765-115">Prerequisites</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="e2765-116">分析和准备邮件数据</span><span class="sxs-lookup"><span data-stu-id="e2765-116">Analyze and prepare message data</span></span>

* <span data-ttu-id="e2765-117">查看第三方数据，确定要迁移哪些内容。</span><span class="sxs-lookup"><span data-stu-id="e2765-117">Review the third-party data to decide what will be migrated.</span></span>  
* <span data-ttu-id="e2765-118">从第三方聊天系统提取所选数据。</span><span class="sxs-lookup"><span data-stu-id="e2765-118">Extract the selected data from the third-party chat system.</span></span>  
* <span data-ttu-id="e2765-119">将第三方聊天结构映射到Teams结构。</span><span class="sxs-lookup"><span data-stu-id="e2765-119">Map the third-party chat structure to the Teams structure.</span></span>  
* <span data-ttu-id="e2765-120">将导入数据转换为迁移所需的格式。</span><span class="sxs-lookup"><span data-stu-id="e2765-120">Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="e2765-121">设置 Office 365 租户</span><span class="sxs-lookup"><span data-stu-id="e2765-121">Set up your Office 365 tenant</span></span>

* <span data-ttu-id="e2765-122">确保导入Office 365租户存在。</span><span class="sxs-lookup"><span data-stu-id="e2765-122">Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="e2765-123">有关为租户设置Office 365租户Teams，请参阅[准备Office 365租户](../../concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="e2765-123">For more information on setting up an Office 365 tenancy for Teams, see [prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>
* <span data-ttu-id="e2765-124">确保团队成员在 AAD Azure Active Directory () 。</span><span class="sxs-lookup"><span data-stu-id="e2765-124">Make sure that team members are in Azure Active Directory (AAD).</span></span> <span data-ttu-id="e2765-125">有关详细信息，请参阅向 AAD [添加新](/azure/active-directory/fundamentals/add-users-azure-active-directory) 用户。</span><span class="sxs-lookup"><span data-stu-id="e2765-125">For more information, see [add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to AAD.</span></span>

## <a name="step-1-create-a-team"></a><span data-ttu-id="e2765-126">步骤 1：创建团队</span><span class="sxs-lookup"><span data-stu-id="e2765-126">Step 1: Create a team</span></span>

<span data-ttu-id="e2765-127">由于要迁移现有数据，因此在迁移过程中保留原始邮件时间戳并阻止邮件活动对于在 Teams 中重新创建用户的现有邮件流Teams。</span><span class="sxs-lookup"><span data-stu-id="e2765-127">Since you are migrating existing data, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="e2765-128">实现此目的：：</span><span class="sxs-lookup"><span data-stu-id="e2765-128">This is achieved as follows:</span></span>

> <span data-ttu-id="e2765-129">[使用 team 资源](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) 属性创建具有返回时间戳的新 `createdDateTime` 团队。</span><span class="sxs-lookup"><span data-stu-id="e2765-129">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource `createdDateTime` property.</span></span> <span data-ttu-id="e2765-130">将新团队放在 中，这是一种特殊状态，可限制用户在迁移过程完成之前 `migration mode` 参与团队中的大多数活动。</span><span class="sxs-lookup"><span data-stu-id="e2765-130">Place the new team in `migration mode`, a special state that restricts users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="e2765-131">在 POST 请求中包括具有 值的 instance 属性，以明确标识正在创建 `teamCreationMode` `migration` 用于迁移的新团队。</span><span class="sxs-lookup"><span data-stu-id="e2765-131">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> [!NOTE]
> <span data-ttu-id="e2765-132">`createdDateTime`将仅为已迁移的团队或频道的实例填充该字段。</span><span class="sxs-lookup"><span data-stu-id="e2765-132">The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permission"></a><span data-ttu-id="e2765-133">权限</span><span class="sxs-lookup"><span data-stu-id="e2765-133">Permission</span></span>

|<span data-ttu-id="e2765-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="e2765-134">ScopeName</span></span>|<span data-ttu-id="e2765-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="e2765-135">DisplayName</span></span>|<span data-ttu-id="e2765-136">说明</span><span class="sxs-lookup"><span data-stu-id="e2765-136">Description</span></span>|<span data-ttu-id="e2765-137">类型</span><span class="sxs-lookup"><span data-stu-id="e2765-137">Type</span></span>|<span data-ttu-id="e2765-138">管理员同意？</span><span class="sxs-lookup"><span data-stu-id="e2765-138">Admin Consent?</span></span>|<span data-ttu-id="e2765-139">涵盖的实体/API</span><span class="sxs-lookup"><span data-stu-id="e2765-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="e2765-140">管理迁移到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e2765-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="e2765-141">创建和管理资源以迁移到Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="e2765-141">Creating and managing resources for migration to Microsoft Teams.</span></span>|<span data-ttu-id="e2765-142">**仅应用程序**</span><span class="sxs-lookup"><span data-stu-id="e2765-142">**Application-only**</span></span>|<span data-ttu-id="e2765-143">**是**</span><span class="sxs-lookup"><span data-stu-id="e2765-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="e2765-144">请求 (迁移状态创建) </span><span class="sxs-lookup"><span data-stu-id="e2765-144">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="e2765-145">响应</span><span class="sxs-lookup"><span data-stu-id="e2765-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{team-id}/operations/{operation-id}
Content-Location: /teams/{team-id}
```

#### <a name="error-message"></a><span data-ttu-id="e2765-146">错误消息</span><span class="sxs-lookup"><span data-stu-id="e2765-146">Error message</span></span>

```http
400 Bad Request
```

<span data-ttu-id="e2765-147">您可以在以下情况下收到错误消息：</span><span class="sxs-lookup"><span data-stu-id="e2765-147">You can receive the error message in the following scenarios:</span></span>

* <span data-ttu-id="e2765-148">为 `createdDateTime` 将来设置 If。</span><span class="sxs-lookup"><span data-stu-id="e2765-148">If `createdDateTime` is set for future.</span></span>
* <span data-ttu-id="e2765-149">如果 `createdDateTime` 已正确指定，但 `teamCreationMode` 实例属性缺失或设置为无效值。</span><span class="sxs-lookup"><span data-stu-id="e2765-149">If `createdDateTime` is correctly specified, but `teamCreationMode` instance attribute is missing or set to invalid value.</span></span>

## <a name="step-2-create-a-channel"></a><span data-ttu-id="e2765-150">步骤 2：创建频道</span><span class="sxs-lookup"><span data-stu-id="e2765-150">Step 2: Create a channel</span></span>

<span data-ttu-id="e2765-151">为导入的消息创建频道与创建团队方案类似：</span><span class="sxs-lookup"><span data-stu-id="e2765-151">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="e2765-152">[使用 channel 资源](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) 属性创建具有返回时间戳的新 `createdDateTime` 频道。</span><span class="sxs-lookup"><span data-stu-id="e2765-152">[Create a new channel](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="e2765-153">将新频道放在 中，这是一种特殊状态，可限制用户在迁移过程完成之前参与频道内的 `migration mode` 大多数聊天活动。</span><span class="sxs-lookup"><span data-stu-id="e2765-153">Place the new channel in `migration mode`, a special state that restricts users from most chat activities within the channel until the migration process is complete.</span></span> <span data-ttu-id="e2765-154">在 POST 请求中包括具有 值的 instance 属性，以明确标识正在创建 `channelCreationMode` `migration` 用于迁移的新团队。</span><span class="sxs-lookup"><span data-stu-id="e2765-154">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permission"></a><span data-ttu-id="e2765-155">权限</span><span class="sxs-lookup"><span data-stu-id="e2765-155">Permission</span></span>

|<span data-ttu-id="e2765-156">ScopeName</span><span class="sxs-lookup"><span data-stu-id="e2765-156">ScopeName</span></span>|<span data-ttu-id="e2765-157">DisplayName</span><span class="sxs-lookup"><span data-stu-id="e2765-157">DisplayName</span></span>|<span data-ttu-id="e2765-158">说明</span><span class="sxs-lookup"><span data-stu-id="e2765-158">Description</span></span>|<span data-ttu-id="e2765-159">类型</span><span class="sxs-lookup"><span data-stu-id="e2765-159">Type</span></span>|<span data-ttu-id="e2765-160">管理员同意？</span><span class="sxs-lookup"><span data-stu-id="e2765-160">Admin Consent?</span></span>|<span data-ttu-id="e2765-161">涵盖的实体/API</span><span class="sxs-lookup"><span data-stu-id="e2765-161">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="e2765-162">管理迁移到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e2765-162">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="e2765-163">创建和管理资源以迁移到Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="e2765-163">Creating and managing resources for migration to Microsoft Teams.</span></span>|<span data-ttu-id="e2765-164">**仅应用程序**</span><span class="sxs-lookup"><span data-stu-id="e2765-164">**Application-only**</span></span>|<span data-ttu-id="e2765-165">**是**</span><span class="sxs-lookup"><span data-stu-id="e2765-165">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="e2765-166">请求 (在迁移状态创建) </span><span class="sxs-lookup"><span data-stu-id="e2765-166">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="e2765-167">响应</span><span class="sxs-lookup"><span data-stu-id="e2765-167">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="e2765-168">错误消息</span><span class="sxs-lookup"><span data-stu-id="e2765-168">Error message</span></span>

```http
400 Bad Request
```
<span data-ttu-id="e2765-169">您可以在以下情况下收到错误消息：</span><span class="sxs-lookup"><span data-stu-id="e2765-169">You can receive the error message in the following scenarios:</span></span>

* <span data-ttu-id="e2765-170">为 `createdDateTime` 将来设置 If。</span><span class="sxs-lookup"><span data-stu-id="e2765-170">If `createdDateTime` is set for future.</span></span>
* <span data-ttu-id="e2765-171">如果 `createdDateTime` 已正确指定，但 `channelCreationMode` 实例属性缺失或设置为无效值。</span><span class="sxs-lookup"><span data-stu-id="e2765-171">If `createdDateTime` is correctly specified but `channelCreationMode` instance attribute is missing or set to invalid value.</span></span>

## <a name="step-3-import-messages"></a><span data-ttu-id="e2765-172">步骤 3：导入邮件</span><span class="sxs-lookup"><span data-stu-id="e2765-172">Step 3: Import messages</span></span>

<span data-ttu-id="e2765-173">创建团队和频道后，可以使用 请求正文中的 和 键开始发送返回 `createdDateTime` `from` 时间消息。</span><span class="sxs-lookup"><span data-stu-id="e2765-173">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from` keys in the request body.</span></span>

> [!NOTE]
> * <span data-ttu-id="e2765-174">不支持使用早于 `createdDateTime` 邮件线程导入 `createdDateTime` 的邮件。</span><span class="sxs-lookup"><span data-stu-id="e2765-174">Messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>
> * <span data-ttu-id="e2765-175">`createdDateTime` 对于同一线程中的消息，必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="e2765-175">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="e2765-176">`createdDateTime` 支持具有毫秒精度的时间戳。</span><span class="sxs-lookup"><span data-stu-id="e2765-176">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="e2765-177">例如，如果传入请求邮件的值设置为 `createdDateTime` *2020-09-16T05：50：31.0025302Z，* 那么在接收邮件时，它将转换为 *2020-09-16T05：50：31.002Z。*</span><span class="sxs-lookup"><span data-stu-id="e2765-177">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="e2765-178">请求 (纯文本的 POST) </span><span class="sxs-lookup"><span data-stu-id="e2765-178">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="e2765-179">响应</span><span class="sxs-lookup"><span data-stu-id="e2765-179">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="e2765-180">错误消息</span><span class="sxs-lookup"><span data-stu-id="e2765-180">Error message</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="e2765-181">请求 (内联图像消息 POST) </span><span class="sxs-lookup"><span data-stu-id="e2765-181">Request (POST a message with inline image)</span></span>

> [!NOTE]
> * <span data-ttu-id="e2765-182">此方案中没有特殊权限范围，因为请求是 的一部分 `chatMessage` 。</span><span class="sxs-lookup"><span data-stu-id="e2765-182">There are no special permission scopes in this scenario since the request is part of `chatMessage`.</span></span>
> * <span data-ttu-id="e2765-183">此处适用于 `chatMessage` 的范围。</span><span class="sxs-lookup"><span data-stu-id="e2765-183">The scopes for `chatMessage` apply here.</span></span>

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

#### <a name="response"></a><span data-ttu-id="e2765-184">响应</span><span class="sxs-lookup"><span data-stu-id="e2765-184">Response</span></span>

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

## <a name="step-4-complete-migration-mode"></a><span data-ttu-id="e2765-185">步骤 4：完成迁移模式</span><span class="sxs-lookup"><span data-stu-id="e2765-185">Step 4: Complete migration mode</span></span>

<span data-ttu-id="e2765-186">完成邮件迁移过程后，团队和频道均会使用 方法退出迁移  `completeMigration` 模式。</span><span class="sxs-lookup"><span data-stu-id="e2765-186">After the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration` method.</span></span> <span data-ttu-id="e2765-187">此步骤将打开工作组和频道资源，供工作组成员常规使用。</span><span class="sxs-lookup"><span data-stu-id="e2765-187">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="e2765-188">操作绑定到 `team` 实例。</span><span class="sxs-lookup"><span data-stu-id="e2765-188">The action is bound to the `team` instance.</span></span> <span data-ttu-id="e2765-189">在团队完成之前，必须在迁移模式下完成所有频道。</span><span class="sxs-lookup"><span data-stu-id="e2765-189">Before the team completes, all channels must be completed out of migration mode.</span></span>

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="e2765-190">请求 (通道迁移模式) </span><span class="sxs-lookup"><span data-stu-id="e2765-190">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a><span data-ttu-id="e2765-191">响应</span><span class="sxs-lookup"><span data-stu-id="e2765-191">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="e2765-192">请求 (团队迁移模式) </span><span class="sxs-lookup"><span data-stu-id="e2765-192">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a><span data-ttu-id="e2765-193">响应</span><span class="sxs-lookup"><span data-stu-id="e2765-193">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

<span data-ttu-id="e2765-194">对 不在 `team` 中的 或 `channel` 调用的操作 `migrationMode` 。</span><span class="sxs-lookup"><span data-stu-id="e2765-194">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="e2765-195">步骤 5：添加团队成员</span><span class="sxs-lookup"><span data-stu-id="e2765-195">Step five: Add team members</span></span>

<span data-ttu-id="e2765-196">可以使用以下 UI 将成员添加到团队[Teams](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) Microsoft Graph[添加成员](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true)API：</span><span class="sxs-lookup"><span data-stu-id="e2765-196">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="e2765-197">请求 (添加成员) </span><span class="sxs-lookup"><span data-stu-id="e2765-197">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="e2765-198">响应</span><span class="sxs-lookup"><span data-stu-id="e2765-198">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="e2765-199">使用技巧和其他信息</span><span class="sxs-lookup"><span data-stu-id="e2765-199">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="e2765-200">提出 `completeMigration` 请求后，无法将进一步的消息导入团队。</span><span class="sxs-lookup"><span data-stu-id="e2765-200">After the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="e2765-201">在请求返回成功响应后，只能将团队成员 `completeMigration` 添加到新团队。</span><span class="sxs-lookup"><span data-stu-id="e2765-201">You can only add team members to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="e2765-202">限制：邮件按每个通道 5 RPS 导入。</span><span class="sxs-lookup"><span data-stu-id="e2765-202">Throttling: Messages import at five RPS per channel.</span></span>

* <span data-ttu-id="e2765-203">如果需要更正迁移结果，则必须删除该团队，并重复这些步骤以创建团队和频道，然后重新迁移邮件。</span><span class="sxs-lookup"><span data-stu-id="e2765-203">If you need to make a correction to the migration results, you must delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="e2765-204">目前，内联图像是导入邮件 API 架构支持的唯一媒体类型。</span><span class="sxs-lookup"><span data-stu-id="e2765-204">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="e2765-205">导入内容范围</span><span class="sxs-lookup"><span data-stu-id="e2765-205">Import content scope</span></span>

<span data-ttu-id="e2765-206">下表提供了内容范围：</span><span class="sxs-lookup"><span data-stu-id="e2765-206">The following table provides the content scope:</span></span>

|<span data-ttu-id="e2765-207">范围内</span><span class="sxs-lookup"><span data-stu-id="e2765-207">In-scope</span></span> | <span data-ttu-id="e2765-208">当前超出范围</span><span class="sxs-lookup"><span data-stu-id="e2765-208">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="e2765-209">团队和频道消息</span><span class="sxs-lookup"><span data-stu-id="e2765-209">Team and channel messages</span></span>|<span data-ttu-id="e2765-210">1：1 和群聊消息</span><span class="sxs-lookup"><span data-stu-id="e2765-210">1:1 and group chat messages</span></span>|
|<span data-ttu-id="e2765-211">原始邮件的创建时间</span><span class="sxs-lookup"><span data-stu-id="e2765-211">Created time of the original message</span></span>|<span data-ttu-id="e2765-212">专用频道</span><span class="sxs-lookup"><span data-stu-id="e2765-212">Private channels</span></span>|
|<span data-ttu-id="e2765-213">作为邮件一部分的内联图像</span><span class="sxs-lookup"><span data-stu-id="e2765-213">Inline images as part of the message</span></span>|<span data-ttu-id="e2765-214">在提及时</span><span class="sxs-lookup"><span data-stu-id="e2765-214">At mentions</span></span>|
|<span data-ttu-id="e2765-215">指向 SPO 或 SPO 中的现有文件OneDrive</span><span class="sxs-lookup"><span data-stu-id="e2765-215">Links to existing files in SPO or OneDrive</span></span>|<span data-ttu-id="e2765-216">反应</span><span class="sxs-lookup"><span data-stu-id="e2765-216">Reactions</span></span>|
|<span data-ttu-id="e2765-217">包含格式文本的邮件</span><span class="sxs-lookup"><span data-stu-id="e2765-217">Messages with rich text</span></span>|<span data-ttu-id="e2765-218">视频</span><span class="sxs-lookup"><span data-stu-id="e2765-218">Videos</span></span>|
|<span data-ttu-id="e2765-219">邮件回复链</span><span class="sxs-lookup"><span data-stu-id="e2765-219">Message reply chain</span></span>|<span data-ttu-id="e2765-220">公告</span><span class="sxs-lookup"><span data-stu-id="e2765-220">Announcements</span></span>|
|<span data-ttu-id="e2765-221">高吞吐量处理</span><span class="sxs-lookup"><span data-stu-id="e2765-221">High throughput processing</span></span>|<span data-ttu-id="e2765-222">代码段</span><span class="sxs-lookup"><span data-stu-id="e2765-222">Code snippets</span></span>|
||<span data-ttu-id="e2765-223">贴纸</span><span class="sxs-lookup"><span data-stu-id="e2765-223">Stickers</span></span>|
||<span data-ttu-id="e2765-224">表情符号</span><span class="sxs-lookup"><span data-stu-id="e2765-224">Emojis</span></span>|
||<span data-ttu-id="e2765-225">报价单</span><span class="sxs-lookup"><span data-stu-id="e2765-225">Quotes</span></span>|
||<span data-ttu-id="e2765-226">跨渠道发布</span><span class="sxs-lookup"><span data-stu-id="e2765-226">Cross posts between channels</span></span>|


## <a name="see-also"></a><span data-ttu-id="e2765-227">另请参阅</span><span class="sxs-lookup"><span data-stu-id="e2765-227">See also</span></span>

[<span data-ttu-id="e2765-228">Microsoft Graph 和 Teams 集成</span><span class="sxs-lookup"><span data-stu-id="e2765-228">Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
