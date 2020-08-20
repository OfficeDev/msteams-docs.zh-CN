---
title: 使用 Microsoft Graph 将外部平台消息导入到 Teams
description: 介绍如何使用 Microsoft Graph 将消息从外部平台导入到 Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams Slack 导入邮件 API 图形 Microsoft 迁移迁移后内容
ms.openlocfilehash: 8e8b21c9a38570d7ede745e27b9316b7aba29956
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "46820364"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="696e0-104">使用 Microsoft Graph 将第三方平台消息导入到 Teams</span><span class="sxs-lookup"><span data-stu-id="696e0-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="696e0-105">Microsoft Graph 和 Microsoft Teams 公共预览版可提供快速访问权限和反馈。</span><span class="sxs-lookup"><span data-stu-id="696e0-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="696e0-106">虽然此版本已经进行了扩展测试，但它不适合用于生产。</span><span class="sxs-lookup"><span data-stu-id="696e0-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="696e0-107">使用 Microsoft Graph，可以将用户的现有消息历史记录和数据从外部系统迁移到 Teams 频道。</span><span class="sxs-lookup"><span data-stu-id="696e0-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="696e0-108">通过在 Teams 中重新创建第三方平台消息传递层次结构，用户可以无缝地继续通信，并在不中断的情况下继续通信。</span><span class="sxs-lookup"><span data-stu-id="696e0-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="696e0-109">导入概述</span><span class="sxs-lookup"><span data-stu-id="696e0-109">Import overview</span></span>

<span data-ttu-id="696e0-110">从较高的层次上来说，导入过程包括：</span><span class="sxs-lookup"><span data-stu-id="696e0-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="696e0-111">创建具有后期时间戳的团队</span><span class="sxs-lookup"><span data-stu-id="696e0-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="696e0-112">创建具有后期时间戳的通道</span><span class="sxs-lookup"><span data-stu-id="696e0-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="696e0-113">导入外部后期时间过期的消息</span><span class="sxs-lookup"><span data-stu-id="696e0-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="696e0-114">完成团队和渠道迁移过程</span><span class="sxs-lookup"><span data-stu-id="696e0-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="696e0-115">添加团队成员</span><span class="sxs-lookup"><span data-stu-id="696e0-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="696e0-116">必需要求</span><span class="sxs-lookup"><span data-stu-id="696e0-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="696e0-117">分析和准备消息数据</span><span class="sxs-lookup"><span data-stu-id="696e0-117">Analyze and prepare message data</span></span>

<span data-ttu-id="696e0-118">✔检查第三方数据以决定要迁移的内容。</span><span class="sxs-lookup"><span data-stu-id="696e0-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="696e0-119">✔从第三方聊天系统提取所选数据。</span><span class="sxs-lookup"><span data-stu-id="696e0-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="696e0-120">✔将导入数据转换为迁移所需的格式。</span><span class="sxs-lookup"><span data-stu-id="696e0-120">✔ Convert import data into format needed for migration.</span></span>  
<span data-ttu-id="696e0-121">✔ 将第三方聊天结构映射到 Teams 结构。</span><span class="sxs-lookup"><span data-stu-id="696e0-121">✔ Map the third-party chat structure to the Teams structure.</span></span>

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="696e0-122">设置 Office 365 租户</span><span class="sxs-lookup"><span data-stu-id="696e0-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="696e0-123">✔确保存在 Office 365 租户以获取导入数据。</span><span class="sxs-lookup"><span data-stu-id="696e0-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="696e0-124">有关设置 Teams 的 Office 365 租用的详细信息，请参阅 *： 准备* [Office 365 租户](../../concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="696e0-124">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="696e0-125">✔确保团队成员在 Azure Active Directory (AAD) 。</span><span class="sxs-lookup"><span data-stu-id="696e0-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="696e0-126">有关详细信息，*请参阅"*[将新用户添加到](/azure/active-directory/fundamentals/add-users-azure-active-directory)Azure Active Directory"。</span><span class="sxs-lookup"><span data-stu-id="696e0-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="696e0-127">第 1 步：创建团队</span><span class="sxs-lookup"><span data-stu-id="696e0-127">Step One: Create a team</span></span>

<span data-ttu-id="696e0-128">由于正在迁移现有数据，请维护原始邮件时间戳并防止迁移过程中的邮件活动对重新创建 Teams 中用户现有的邮件流至至至多重要。</span><span class="sxs-lookup"><span data-stu-id="696e0-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="696e0-129">此操作实现如下：</span><span class="sxs-lookup"><span data-stu-id="696e0-129">This is achieved as follows:</span></span>

1. <span data-ttu-id="696e0-130">[使用团队资源](/graph/api/team-post?view=graph-rest-beta&tabs=http) 属性创建具有后期时间戳的新  `createdDateTime`  团队。</span><span class="sxs-lookup"><span data-stu-id="696e0-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span>  

1. <span data-ttu-id="696e0-131">将新团队置 `migration mode` 于一个特殊状态，可使用户从团队内的大多数活动中进行，直到迁移过程完成。</span><span class="sxs-lookup"><span data-stu-id="696e0-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="696e0-132">在 `teamCreationMode` POST 请求中包括 `migration` 实例属性以及值，明确标识新团队创建用于迁移的内容。</span><span class="sxs-lookup"><span data-stu-id="696e0-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="696e0-133">权限</span><span class="sxs-lookup"><span data-stu-id="696e0-133">Permissions</span></span>

|<span data-ttu-id="696e0-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="696e0-134">ScopeName</span></span>|<span data-ttu-id="696e0-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="696e0-135">DisplayName</span></span>|<span data-ttu-id="696e0-136">说明</span><span class="sxs-lookup"><span data-stu-id="696e0-136">Description</span></span>|<span data-ttu-id="696e0-137">类型</span><span class="sxs-lookup"><span data-stu-id="696e0-137">Type</span></span>|<span data-ttu-id="696e0-138">管理员同意？</span><span class="sxs-lookup"><span data-stu-id="696e0-138">Admin Consent?</span></span>|<span data-ttu-id="696e0-139">涵盖的实体/API</span><span class="sxs-lookup"><span data-stu-id="696e0-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="696e0-140">管理迁移到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="696e0-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="696e0-141">创建、管理要迁移到 Microsoft Teams 的资源</span><span class="sxs-lookup"><span data-stu-id="696e0-141">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="696e0-142">**仅限应用程序**</span><span class="sxs-lookup"><span data-stu-id="696e0-142">**Application-only**</span></span>|<span data-ttu-id="696e0-143">**是**</span><span class="sxs-lookup"><span data-stu-id="696e0-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="696e0-144">请求 (在迁移状态下创建) </span><span class="sxs-lookup"><span data-stu-id="696e0-144">Request (create a team in migration state)</span></span>

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description"
  "createdDateTime": "2020-03-14T11:22:17.067Z"
}
```

#### <a name="response"></a><span data-ttu-id="696e0-145">响应</span><span class="sxs-lookup"><span data-stu-id="696e0-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="696e0-146">错误消息</span><span class="sxs-lookup"><span data-stu-id="696e0-146">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="696e0-147">`createdDateTime`  将来设置。</span><span class="sxs-lookup"><span data-stu-id="696e0-147">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="696e0-148">`createdDateTime`  正确指定， `teamCreationMode`  但实例属性缺少或设置为无效值。</span><span class="sxs-lookup"><span data-stu-id="696e0-148">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="696e0-149">第 2 步：创建频道</span><span class="sxs-lookup"><span data-stu-id="696e0-149">Step Two: Create a channel</span></span>

<span data-ttu-id="696e0-150">为导入的消息创建频道与创建团队方案类似：</span><span class="sxs-lookup"><span data-stu-id="696e0-150">Creating a channel for the imported messages is similar to the create team scenario:</span></span> 

1. <span data-ttu-id="696e0-151">[使用通道资源](/graph/api/channel-post?view=graph-rest-beta&tabs=http) 属性，使用后期时间戳创建新 `createdDateTime` 频道。</span><span class="sxs-lookup"><span data-stu-id="696e0-151">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span>

1. <span data-ttu-id="696e0-152">将新频道置于 `migration mode` ，从频道内的大多数聊天活动中栏用户，直到完成迁移过程之前，其状态是一种特殊状态。</span><span class="sxs-lookup"><span data-stu-id="696e0-152">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="696e0-153">在 `channelCreationMode` POST 请求中包括 `migration` 实例属性以及值，明确标识新团队创建用于迁移的内容。</span><span class="sxs-lookup"><span data-stu-id="696e0-153">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="696e0-154">权限</span><span class="sxs-lookup"><span data-stu-id="696e0-154">Permissions</span></span>

|<span data-ttu-id="696e0-155">ScopeName</span><span class="sxs-lookup"><span data-stu-id="696e0-155">ScopeName</span></span>|<span data-ttu-id="696e0-156">DisplayName</span><span class="sxs-lookup"><span data-stu-id="696e0-156">DisplayName</span></span>|<span data-ttu-id="696e0-157">说明</span><span class="sxs-lookup"><span data-stu-id="696e0-157">Description</span></span>|<span data-ttu-id="696e0-158">类型</span><span class="sxs-lookup"><span data-stu-id="696e0-158">Type</span></span>|<span data-ttu-id="696e0-159">管理员同意？</span><span class="sxs-lookup"><span data-stu-id="696e0-159">Admin Consent?</span></span>|<span data-ttu-id="696e0-160">涵盖的实体/API</span><span class="sxs-lookup"><span data-stu-id="696e0-160">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="696e0-161">管理迁移到 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="696e0-161">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="696e0-162">创建、管理要迁移到 Microsoft Teams 的资源</span><span class="sxs-lookup"><span data-stu-id="696e0-162">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="696e0-163">**仅限应用程序**</span><span class="sxs-lookup"><span data-stu-id="696e0-163">**Application-only**</span></span>|<span data-ttu-id="696e0-164">**是**</span><span class="sxs-lookup"><span data-stu-id="696e0-164">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="696e0-165">请求 (在迁移状态下创建) </span><span class="sxs-lookup"><span data-stu-id="696e0-165">Request (create a channel in migration state)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/{id}/channels

Content-Type: application/json
{
  "@microsoft.graph.channelCreationMode": "migration",
  "displayName": "Architecture Discussion",
  "description": "This channel is where we debate all future architecture plans",
  "membershipType": "standard",
  "createdDateTime": "2020-03-14T11:22:17.067Z"
}
```

#### <a name="response"></a><span data-ttu-id="696e0-166">响应</span><span class="sxs-lookup"><span data-stu-id="696e0-166">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/channels/{channelId}/operations/{operationId}
Content-Location: /teams/{teamId}/channels/{channelId}
```

#### <a name="error-message"></a><span data-ttu-id="696e0-167">错误消息</span><span class="sxs-lookup"><span data-stu-id="696e0-167">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="696e0-168">`createdDateTime`  将来设置。</span><span class="sxs-lookup"><span data-stu-id="696e0-168">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="696e0-169">`createdDateTime`  正确指定 `channelCreationMode`  ，但实例属性缺少或设置为无效值。</span><span class="sxs-lookup"><span data-stu-id="696e0-169">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="696e0-170">步骤 3：导入邮件</span><span class="sxs-lookup"><span data-stu-id="696e0-170">Step Three: Import messages</span></span>

<span data-ttu-id="696e0-171">创建团队和频道后，你可以开始使用请求正文中的密钥 `createdDateTime` `from`  发送返回时消息。</span><span class="sxs-lookup"><span data-stu-id="696e0-171">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="696e0-172">请求 (文本的 POST 消息) </span><span class="sxs-lookup"><span data-stu-id="696e0-172">Request (POST message that is text-only)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

{
    "replyToId": null,
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
        "content": "Hello World"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

#### <a name="response"></a><span data-ttu-id="696e0-173">响应</span><span class="sxs-lookup"><span data-stu-id="696e0-173">Response</span></span>

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
        "content": "Hello World"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="696e0-174">请求 (嵌入式图像) 消息</span><span class="sxs-lookup"><span data-stu-id="696e0-174">Request (POST a message with inline \`image)</span></span>

> <span data-ttu-id="696e0-175">**注意**：此方案中没有特殊的权限范围，因为请求是 chatMessage 的一部分;chatMessage 的范围也在此适用。</span><span class="sxs-lookup"><span data-stu-id="696e0-175">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="696e0-176">响应</span><span class="sxs-lookup"><span data-stu-id="696e0-176">Response</span></span>

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
    {
      "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"https://graph.microsoft.com/teams/teamId/channels/channelId/messages/id-value/hostedContents/hostedContentId/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="696e0-177">步骤 4：完成迁移模式</span><span class="sxs-lookup"><span data-stu-id="696e0-177">Step Four: Complete migration mode</span></span>

<span data-ttu-id="696e0-178">消息迁移过程完成后，团队和渠道都使用该方法退出迁移  `completeMigration`  模式。</span><span class="sxs-lookup"><span data-stu-id="696e0-178">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="696e0-179">此步骤将打开团队和频道资源，以供团队成员使用。</span><span class="sxs-lookup"><span data-stu-id="696e0-179">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="696e0-180">操作绑定到 `team` 该实例。</span><span class="sxs-lookup"><span data-stu-id="696e0-180">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="696e0-181">请求 (团队迁移模式) </span><span class="sxs-lookup"><span data-stu-id="696e0-181">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="696e0-182">响应</span><span class="sxs-lookup"><span data-stu-id="696e0-182">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="696e0-183">请求结束 (频道迁移模式) </span><span class="sxs-lookup"><span data-stu-id="696e0-183">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="696e0-184">响应</span><span class="sxs-lookup"><span data-stu-id="696e0-184">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="696e0-185">错误响应</span><span class="sxs-lookup"><span data-stu-id="696e0-185">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="696e0-186">对中或 `team` 不在 `channel` 中的操作 `migrationMode` 调用。</span><span class="sxs-lookup"><span data-stu-id="696e0-186">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="696e0-187">步骤 5：添加团队成员</span><span class="sxs-lookup"><span data-stu-id="696e0-187">Step Five: Add team members</span></span>

<span data-ttu-id="696e0-188">你可以使用 Teams UI 或 Microsoft Graph [添加成员 API](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) 向 [团队添加](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) 成员：</span><span class="sxs-lookup"><span data-stu-id="696e0-188">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="696e0-189">添加 (请求) </span><span class="sxs-lookup"><span data-stu-id="696e0-189">Request (add member)</span></span>

```http
POST https://graph.microsoft.com/beta/groups/{id}/members/$ref
Content-type: application/json
Content-length: 30

{
  "@odata.id": "https://graph.microsoft.com/beta/directoryObjects/{id}"
}
```

#### <a name="response"></a><span data-ttu-id="696e0-190">响应</span><span class="sxs-lookup"><span data-stu-id="696e0-190">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="696e0-191">提示和其他信息</span><span class="sxs-lookup"><span data-stu-id="696e0-191">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="696e0-192">可导入来自 Teams 外部用户的消息。</span><span class="sxs-lookup"><span data-stu-id="696e0-192">You can import messages from users who are not in Teams.</span></span>

* <span data-ttu-id="696e0-193">发出请求 `completeMigration` 后，无法将进一步的邮件导入到团队。</span><span class="sxs-lookup"><span data-stu-id="696e0-193">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="696e0-194">工作组成员只能在请求返回成功 `completeMigration` 的响应后添加到新团队。</span><span class="sxs-lookup"><span data-stu-id="696e0-194">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="696e0-195">限制：每渠道 5 个 RPS 导入邮件。</span><span class="sxs-lookup"><span data-stu-id="696e0-195">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="696e0-196">如需更正迁移结果，需要删除团队并重复创建团队和频道并重新迁移消息的步骤。</span><span class="sxs-lookup"><span data-stu-id="696e0-196">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="696e0-197">目前，嵌入式图像是导入消息 API 架构唯一支持的媒体类型。</span><span class="sxs-lookup"><span data-stu-id="696e0-197">Currently, Inline images is the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="696e0-198">导入内容范围</span><span class="sxs-lookup"><span data-stu-id="696e0-198">Import content scope</span></span>

|<span data-ttu-id="696e0-199">范围内</span><span class="sxs-lookup"><span data-stu-id="696e0-199">In-scope</span></span> | <span data-ttu-id="696e0-200">目前超出范围</span><span class="sxs-lookup"><span data-stu-id="696e0-200">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="696e0-201">团队消息和频道消息</span><span class="sxs-lookup"><span data-stu-id="696e0-201">Team and channel messages</span></span>|<span data-ttu-id="696e0-202">1：1 和群组聊天消息</span><span class="sxs-lookup"><span data-stu-id="696e0-202">1:1 and group chat messages</span></span>|
|<span data-ttu-id="696e0-203">创建原始邮件的时间</span><span class="sxs-lookup"><span data-stu-id="696e0-203">Created time of the original message</span></span>|<span data-ttu-id="696e0-204">专用频道</span><span class="sxs-lookup"><span data-stu-id="696e0-204">Private channels</span></span>|
|<span data-ttu-id="696e0-205">作为邮件的一部分的嵌入式图像</span><span class="sxs-lookup"><span data-stu-id="696e0-205">Inline images as part of the message</span></span>|<span data-ttu-id="696e0-206">提及</span><span class="sxs-lookup"><span data-stu-id="696e0-206">At mentions</span></span>|
|<span data-ttu-id="696e0-207">指向 SPO/OneDrive 中的现有文件的链接</span><span class="sxs-lookup"><span data-stu-id="696e0-207">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="696e0-208">反应</span><span class="sxs-lookup"><span data-stu-id="696e0-208">Reactions</span></span>|
|<span data-ttu-id="696e0-209">包含 RTF 的邮件</span><span class="sxs-lookup"><span data-stu-id="696e0-209">Messages with rich text</span></span>|<span data-ttu-id="696e0-210">视频</span><span class="sxs-lookup"><span data-stu-id="696e0-210">Videos</span></span>|
|<span data-ttu-id="696e0-211">邮件答复链</span><span class="sxs-lookup"><span data-stu-id="696e0-211">Message reply chain</span></span>|<span data-ttu-id="696e0-212">公告</span><span class="sxs-lookup"><span data-stu-id="696e0-212">Announcements</span></span>|
|<span data-ttu-id="696e0-213">高吞吐量处理</span><span class="sxs-lookup"><span data-stu-id="696e0-213">High throughput processing</span></span>|<span data-ttu-id="696e0-214">代码段</span><span class="sxs-lookup"><span data-stu-id="696e0-214">Code snippets</span></span>|
||<span data-ttu-id="696e0-215">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="696e0-215">Adaptive cards</span></span>|
||<span data-ttu-id="696e0-216">Stickers</span><span class="sxs-lookup"><span data-stu-id="696e0-216">Stickers</span></span>|
||<span data-ttu-id="696e0-217">情注</span><span class="sxs-lookup"><span data-stu-id="696e0-217">Emojis</span></span>|
||<span data-ttu-id="696e0-218">引号</span><span class="sxs-lookup"><span data-stu-id="696e0-218">Quotes</span></span>|
||<span data-ttu-id="696e0-219">在通道之间交叉帖子</span><span class="sxs-lookup"><span data-stu-id="696e0-219">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="696e0-220">了解有关 Microsoft Graph 和 Teams 集成的详细信息</span><span class="sxs-lookup"><span data-stu-id="696e0-220">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
