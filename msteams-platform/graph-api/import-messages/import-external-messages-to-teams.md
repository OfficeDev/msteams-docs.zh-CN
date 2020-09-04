---
title: 使用 Microsoft Graph 将外部平台邮件导入到团队
description: 介绍如何使用 Microsoft Graph 将邮件从外部平台导入到团队
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: 工作组时差导入邮件 api 图 microsoft 迁移迁移发布
ms.openlocfilehash: 0e0aa96373d29f07893456adf54986ec23bdec3c
ms.sourcegitcommit: 02ab2cb7820dc8665bb4ec6a1a40c3b8b8f29d66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "47340947"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="83352-104">使用 Microsoft Graph 将第三方平台消息导入 Teams</span><span class="sxs-lookup"><span data-stu-id="83352-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="83352-105">Microsoft Graph 和 Microsoft 团队公开预览版适用于早期访问和反馈。</span><span class="sxs-lookup"><span data-stu-id="83352-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="83352-106">尽管此版本已经历大量测试，但不适合在生产中使用。</span><span class="sxs-lookup"><span data-stu-id="83352-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="83352-107">使用 Microsoft Graph，可以将用户的现有邮件历史记录和数据从外部系统迁移到团队频道。</span><span class="sxs-lookup"><span data-stu-id="83352-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="83352-108">通过在团队内启用第三方平台邮件传递层次结构，用户可以采用无缝方式继续进行通信并继续进行而不会中断。</span><span class="sxs-lookup"><span data-stu-id="83352-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="83352-109">导入概述</span><span class="sxs-lookup"><span data-stu-id="83352-109">Import overview</span></span>

<span data-ttu-id="83352-110">从较高的层次来看，导入过程包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="83352-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="83352-111">创建具有后时间戳的团队</span><span class="sxs-lookup"><span data-stu-id="83352-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="83352-112">使用后向时间戳创建通道</span><span class="sxs-lookup"><span data-stu-id="83352-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="83352-113">导入外部定期邮件</span><span class="sxs-lookup"><span data-stu-id="83352-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="83352-114">完成团队和渠道迁移过程</span><span class="sxs-lookup"><span data-stu-id="83352-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="83352-115">添加团队成员</span><span class="sxs-lookup"><span data-stu-id="83352-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="83352-116">必需的要求</span><span class="sxs-lookup"><span data-stu-id="83352-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="83352-117">分析和准备邮件数据</span><span class="sxs-lookup"><span data-stu-id="83352-117">Analyze and prepare message data</span></span>

<span data-ttu-id="83352-118">✔查看第三方数据以确定将迁移的内容。</span><span class="sxs-lookup"><span data-stu-id="83352-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="83352-119">✔从第三方聊天系统中提取所选数据。</span><span class="sxs-lookup"><span data-stu-id="83352-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="83352-120">✔将导入数据转换为迁移所需的格式。</span><span class="sxs-lookup"><span data-stu-id="83352-120">✔ Convert import data into format needed for migration.</span></span>  
<span data-ttu-id="83352-121">✔将第三方聊天结构映射到团队结构。</span><span class="sxs-lookup"><span data-stu-id="83352-121">✔ Map the third-party chat structure to the Teams structure.</span></span>

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="83352-122">设置 Office 365 租户</span><span class="sxs-lookup"><span data-stu-id="83352-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="83352-123">✔确保导入数据存在 Office 365 租户。</span><span class="sxs-lookup"><span data-stu-id="83352-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="83352-124">有关为团队设置 Office 365 租赁的详细信息，*请参阅*[准备 office 365 租户](../../concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="83352-124">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="83352-125">✔确保团队成员在 Azure Active Directory (AAD) 中。</span><span class="sxs-lookup"><span data-stu-id="83352-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="83352-126">有关详细信息， *请参阅*向 Azure Active Directory [添加新用户](/azure/active-directory/fundamentals/add-users-azure-active-directory) 。</span><span class="sxs-lookup"><span data-stu-id="83352-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="83352-127">第一步：创建团队</span><span class="sxs-lookup"><span data-stu-id="83352-127">Step One: Create a team</span></span>

<span data-ttu-id="83352-128">由于现有数据正在迁移，因此在迁移过程中维护原始邮件的时间戳并防止邮件活动是重新创建用户的现有邮件流的关键。</span><span class="sxs-lookup"><span data-stu-id="83352-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="83352-129">这是通过以下方式实现的：</span><span class="sxs-lookup"><span data-stu-id="83352-129">This is achieved as follows:</span></span>

1. <span data-ttu-id="83352-130">使用 "团队" 资源属性创建具有 "后向时间戳" 的[新团队](/graph/api/team-post?view=graph-rest-beta&tabs=http) `createdDateTime` 。</span><span class="sxs-lookup"><span data-stu-id="83352-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span>  

1. <span data-ttu-id="83352-131">将新团队放在中 `migration mode` ，这是一种特殊状态，可从团队中的大多数活动中对用户进行横栏，直到迁移过程完成。</span><span class="sxs-lookup"><span data-stu-id="83352-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="83352-132">将 `teamCreationMode` 实例属性包含 `migration` 在 POST 请求中的值，以显式标识新团队为迁移而创建。</span><span class="sxs-lookup"><span data-stu-id="83352-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="83352-133">权限</span><span class="sxs-lookup"><span data-stu-id="83352-133">Permissions</span></span>

|<span data-ttu-id="83352-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="83352-134">ScopeName</span></span>|<span data-ttu-id="83352-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="83352-135">DisplayName</span></span>|<span data-ttu-id="83352-136">说明</span><span class="sxs-lookup"><span data-stu-id="83352-136">Description</span></span>|<span data-ttu-id="83352-137">类型</span><span class="sxs-lookup"><span data-stu-id="83352-137">Type</span></span>|<span data-ttu-id="83352-138">管理员同意？</span><span class="sxs-lookup"><span data-stu-id="83352-138">Admin Consent?</span></span>|<span data-ttu-id="83352-139">涵盖的实体/Api</span><span class="sxs-lookup"><span data-stu-id="83352-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="83352-140">管理到 Microsoft 团队的迁移</span><span class="sxs-lookup"><span data-stu-id="83352-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="83352-141">创建、管理用于迁移到 Microsoft 团队的资源</span><span class="sxs-lookup"><span data-stu-id="83352-141">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="83352-142">**仅限应用程序**</span><span class="sxs-lookup"><span data-stu-id="83352-142">**Application-only**</span></span>|<span data-ttu-id="83352-143">**是**</span><span class="sxs-lookup"><span data-stu-id="83352-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="83352-144">请求 (在迁移状态中创建团队) </span><span class="sxs-lookup"><span data-stu-id="83352-144">Request (create a team in migration state)</span></span>

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.067Z"
}
```

#### <a name="response"></a><span data-ttu-id="83352-145">响应</span><span class="sxs-lookup"><span data-stu-id="83352-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="83352-146">错误消息</span><span class="sxs-lookup"><span data-stu-id="83352-146">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="83352-147">`createdDateTime`  设置为 "将来"。</span><span class="sxs-lookup"><span data-stu-id="83352-147">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="83352-148">`createdDateTime`  正确指定，但 `teamCreationMode`  缺少实例属性或将实例属性设置为无效值。</span><span class="sxs-lookup"><span data-stu-id="83352-148">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="83352-149">步骤2：创建通道</span><span class="sxs-lookup"><span data-stu-id="83352-149">Step Two: Create a channel</span></span>

<span data-ttu-id="83352-150">为导入的邮件创建通道与创建团队方案类似：</span><span class="sxs-lookup"><span data-stu-id="83352-150">Creating a channel for the imported messages is similar to the create team scenario:</span></span> 

1. <span data-ttu-id="83352-151">使用 "信道" 资源属性创建具有 "后向时间戳" 的[新通道](/graph/api/channel-post?view=graph-rest-beta&tabs=http) `createdDateTime` 。</span><span class="sxs-lookup"><span data-stu-id="83352-151">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span>

1. <span data-ttu-id="83352-152">将新频道放置在中 `migration mode` ，这是一种特殊状态，可用于在迁移过程完成前，从频道内的大多数聊天活动中对用户进行横栏。</span><span class="sxs-lookup"><span data-stu-id="83352-152">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="83352-153">将 `channelCreationMode` 实例属性包含 `migration` 在 POST 请求中的值，以显式标识新团队为迁移而创建。</span><span class="sxs-lookup"><span data-stu-id="83352-153">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="83352-154">权限</span><span class="sxs-lookup"><span data-stu-id="83352-154">Permissions</span></span>

|<span data-ttu-id="83352-155">ScopeName</span><span class="sxs-lookup"><span data-stu-id="83352-155">ScopeName</span></span>|<span data-ttu-id="83352-156">DisplayName</span><span class="sxs-lookup"><span data-stu-id="83352-156">DisplayName</span></span>|<span data-ttu-id="83352-157">说明</span><span class="sxs-lookup"><span data-stu-id="83352-157">Description</span></span>|<span data-ttu-id="83352-158">类型</span><span class="sxs-lookup"><span data-stu-id="83352-158">Type</span></span>|<span data-ttu-id="83352-159">管理员同意？</span><span class="sxs-lookup"><span data-stu-id="83352-159">Admin Consent?</span></span>|<span data-ttu-id="83352-160">涵盖的实体/Api</span><span class="sxs-lookup"><span data-stu-id="83352-160">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="83352-161">管理到 Microsoft 团队的迁移</span><span class="sxs-lookup"><span data-stu-id="83352-161">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="83352-162">创建、管理用于迁移到 Microsoft 团队的资源</span><span class="sxs-lookup"><span data-stu-id="83352-162">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="83352-163">**仅限应用程序**</span><span class="sxs-lookup"><span data-stu-id="83352-163">**Application-only**</span></span>|<span data-ttu-id="83352-164">**是**</span><span class="sxs-lookup"><span data-stu-id="83352-164">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="83352-165">请求 (在迁移状态中创建频道) </span><span class="sxs-lookup"><span data-stu-id="83352-165">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="83352-166">响应</span><span class="sxs-lookup"><span data-stu-id="83352-166">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/channels/{channelId}/operations/{operationId}
Content-Location: /teams/{teamId}/channels/{channelId}
```

#### <a name="error-message"></a><span data-ttu-id="83352-167">错误消息</span><span class="sxs-lookup"><span data-stu-id="83352-167">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="83352-168">`createdDateTime`  设置为 "将来"。</span><span class="sxs-lookup"><span data-stu-id="83352-168">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="83352-169">`createdDateTime`  正确指定 `channelCreationMode`  ，但缺少实例属性或将实例属性设置为无效值。</span><span class="sxs-lookup"><span data-stu-id="83352-169">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="83352-170">第三步：导入邮件</span><span class="sxs-lookup"><span data-stu-id="83352-170">Step Three: Import messages</span></span>

<span data-ttu-id="83352-171">在创建团队和频道之后，您可以开始使用 `createdDateTime`  请求正文中的和键发送回送邮件 `from`  。</span><span class="sxs-lookup"><span data-stu-id="83352-171">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="83352-172">请求 (张贴为纯文本的邮件) </span><span class="sxs-lookup"><span data-stu-id="83352-172">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="83352-173">响应</span><span class="sxs-lookup"><span data-stu-id="83352-173">Response</span></span>

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

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="83352-174">请求 (发布包含内联 "图像) 的邮件</span><span class="sxs-lookup"><span data-stu-id="83352-174">Request (POST a message with inline \`image)</span></span>

> <span data-ttu-id="83352-175">**注意**：此方案中没有特殊的权限范围，因为该请求是了 chatmessage 的一部分;了 chatmessage 的作用域也适用于此处。</span><span class="sxs-lookup"><span data-stu-id="83352-175">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="83352-176">响应</span><span class="sxs-lookup"><span data-stu-id="83352-176">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="83352-177">步骤4：完成迁移模式</span><span class="sxs-lookup"><span data-stu-id="83352-177">Step Four: Complete migration mode</span></span>

<span data-ttu-id="83352-178">邮件迁移过程完成后，团队和通道将使用方法从迁移模式中去掉  `completeMigration`  。</span><span class="sxs-lookup"><span data-stu-id="83352-178">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="83352-179">此步骤将打开团队和渠道资源，以供工作组成员进行常规使用。</span><span class="sxs-lookup"><span data-stu-id="83352-179">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="83352-180">操作将绑定到 `team` 实例。</span><span class="sxs-lookup"><span data-stu-id="83352-180">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="83352-181">请求 (结束团队迁移模式) </span><span class="sxs-lookup"><span data-stu-id="83352-181">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="83352-182">响应</span><span class="sxs-lookup"><span data-stu-id="83352-182">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="83352-183">请求 (结束通道迁移模式) </span><span class="sxs-lookup"><span data-stu-id="83352-183">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="83352-184">响应</span><span class="sxs-lookup"><span data-stu-id="83352-184">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="83352-185">错误响应</span><span class="sxs-lookup"><span data-stu-id="83352-185">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="83352-186">在或上调用的操作 `team` `channel` 不在中 `migrationMode` 。</span><span class="sxs-lookup"><span data-stu-id="83352-186">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="83352-187">第5步：添加团队成员</span><span class="sxs-lookup"><span data-stu-id="83352-187">Step Five: Add team members</span></span>

<span data-ttu-id="83352-188">您可以 [使用 "团队 UI"](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) 或 Microsoft Graph [添加成员](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) API 将成员添加到团队中：</span><span class="sxs-lookup"><span data-stu-id="83352-188">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="83352-189">请求 (添加成员) </span><span class="sxs-lookup"><span data-stu-id="83352-189">Request (add member)</span></span>

```http
POST https://graph.microsoft.com/beta/groups/{id}/members/$ref
Content-type: application/json
Content-length: 30

{
  "@odata.id": "https://graph.microsoft.com/beta/directoryObjects/{id}"
}
```

#### <a name="response"></a><span data-ttu-id="83352-190">响应</span><span class="sxs-lookup"><span data-stu-id="83352-190">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="83352-191">提示和其他信息</span><span class="sxs-lookup"><span data-stu-id="83352-191">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="83352-192">您可以导入不在工作组中的用户的邮件。</span><span class="sxs-lookup"><span data-stu-id="83352-192">You can import messages from users who are not in Teams.</span></span>

* <span data-ttu-id="83352-193">`completeMigration`发出请求后，将无法再向团队中导入邮件。</span><span class="sxs-lookup"><span data-stu-id="83352-193">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="83352-194">只有在请求返回成功的响应后，才能将团队成员添加到新团队 `completeMigration` 。</span><span class="sxs-lookup"><span data-stu-id="83352-194">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="83352-195">限制：邮件将导入每通道5个 RPS。</span><span class="sxs-lookup"><span data-stu-id="83352-195">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="83352-196">如果需要对迁移结果进行更正，则需要删除团队并重复步骤以创建团队和频道并重新迁移邮件。</span><span class="sxs-lookup"><span data-stu-id="83352-196">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="83352-197">目前，嵌入式图像是导入邮件 API 架构支持的唯一媒体类型。</span><span class="sxs-lookup"><span data-stu-id="83352-197">Currently, Inline images is the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="83352-198">导入内容范围</span><span class="sxs-lookup"><span data-stu-id="83352-198">Import content scope</span></span>

|<span data-ttu-id="83352-199">范围内</span><span class="sxs-lookup"><span data-stu-id="83352-199">In-scope</span></span> | <span data-ttu-id="83352-200">当前超出范围</span><span class="sxs-lookup"><span data-stu-id="83352-200">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="83352-201">团队和频道消息</span><span class="sxs-lookup"><span data-stu-id="83352-201">Team and channel messages</span></span>|<span data-ttu-id="83352-202">1:1 和分组聊天消息</span><span class="sxs-lookup"><span data-stu-id="83352-202">1:1 and group chat messages</span></span>|
|<span data-ttu-id="83352-203">原始邮件的创建时间</span><span class="sxs-lookup"><span data-stu-id="83352-203">Created time of the original message</span></span>|<span data-ttu-id="83352-204">专用频道</span><span class="sxs-lookup"><span data-stu-id="83352-204">Private channels</span></span>|
|<span data-ttu-id="83352-205">作为邮件的一部分的嵌入式图像</span><span class="sxs-lookup"><span data-stu-id="83352-205">Inline images as part of the message</span></span>|<span data-ttu-id="83352-206">提到</span><span class="sxs-lookup"><span data-stu-id="83352-206">At mentions</span></span>|
|<span data-ttu-id="83352-207">指向 SPO/OneDrive 中的现有文件的链接</span><span class="sxs-lookup"><span data-stu-id="83352-207">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="83352-208">作出</span><span class="sxs-lookup"><span data-stu-id="83352-208">Reactions</span></span>|
|<span data-ttu-id="83352-209">带格式文本的邮件</span><span class="sxs-lookup"><span data-stu-id="83352-209">Messages with rich text</span></span>|<span data-ttu-id="83352-210">视频</span><span class="sxs-lookup"><span data-stu-id="83352-210">Videos</span></span>|
|<span data-ttu-id="83352-211">邮件答复链</span><span class="sxs-lookup"><span data-stu-id="83352-211">Message reply chain</span></span>|<span data-ttu-id="83352-212">公告</span><span class="sxs-lookup"><span data-stu-id="83352-212">Announcements</span></span>|
|<span data-ttu-id="83352-213">高吞吐量处理</span><span class="sxs-lookup"><span data-stu-id="83352-213">High throughput processing</span></span>|<span data-ttu-id="83352-214">代码段</span><span class="sxs-lookup"><span data-stu-id="83352-214">Code snippets</span></span>|
||<span data-ttu-id="83352-215">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="83352-215">Adaptive cards</span></span>|
||<span data-ttu-id="83352-216">不干胶</span><span class="sxs-lookup"><span data-stu-id="83352-216">Stickers</span></span>|
||<span data-ttu-id="83352-217">表情符号</span><span class="sxs-lookup"><span data-stu-id="83352-217">Emojis</span></span>|
||<span data-ttu-id="83352-218">股票</span><span class="sxs-lookup"><span data-stu-id="83352-218">Quotes</span></span>|
||<span data-ttu-id="83352-219">通道之间的跨文章</span><span class="sxs-lookup"><span data-stu-id="83352-219">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="83352-220">了解有关 Microsoft Graph 和团队集成的详细信息</span><span class="sxs-lookup"><span data-stu-id="83352-220">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
