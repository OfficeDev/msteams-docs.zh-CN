---
title: 创建并发送任务模块
author: clearab
description: 如何处理初始调用操作，以及如何使用操作消息扩展命令中的任务模块进行响应
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: fbe90b3a3af8dbb053fdbaf6b4cd9b96344eaf00
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075589"
---
# <a name="create-and-send-the-task-module"></a><span data-ttu-id="ddf69-103">创建并发送任务模块</span><span class="sxs-lookup"><span data-stu-id="ddf69-103">Create and send the task module</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="ddf69-104">可以使用自适应卡片或嵌入式 Web 视图创建任务模块。</span><span class="sxs-lookup"><span data-stu-id="ddf69-104">You can create the task module using an Adaptive Card or an embedded web view.</span></span> <span data-ttu-id="ddf69-105">若要创建任务模块，必须执行称为初始调用请求的过程。</span><span class="sxs-lookup"><span data-stu-id="ddf69-105">To create a task module, you must perform the process called the initial invoke request.</span></span> <span data-ttu-id="ddf69-106">本文档涵盖初始调用请求、从一对一聊天、群聊、频道 (新帖子) 、频道 (回复线程) 和命令框调用任务模块时的有效负载活动属性。</span><span class="sxs-lookup"><span data-stu-id="ddf69-106">This document covers the initial invoke request, payload activity properties when a task module is invoked from 1:1 chat, group chat, channel (new post), channel (reply to thread), and command box.</span></span> 
> [!NOTE]
> <span data-ttu-id="ddf69-107">如果没有使用应用清单中定义的参数填充任务模块，则必须为具有自适应卡片或嵌入式 Web 视图的用户创建任务模块。</span><span class="sxs-lookup"><span data-stu-id="ddf69-107">If you are not populating the task module with parameters defined in the app manifest, you must create the task module for users with either an Adaptive Card or an embedded web view.</span></span>

## <a name="the-initial-invoke-request"></a><span data-ttu-id="ddf69-108">初始调用请求</span><span class="sxs-lookup"><span data-stu-id="ddf69-108">The initial invoke request</span></span>

<span data-ttu-id="ddf69-109">在初始调用请求过程中，你的服务接收一个类型 为 的对象，并且你必须使用包含自适应卡片或嵌入 Web 视图 `Activity` `composeExtension/fetchTask` 的 URL `task` 的对象进行响应。</span><span class="sxs-lookup"><span data-stu-id="ddf69-109">In the process of the initial invoke request, your service receives an `Activity` object of type `composeExtension/fetchTask`, and you must respond with a `task` object containing either an Adaptive Card or a URL to the embedded web view.</span></span> <span data-ttu-id="ddf69-110">与标准自动程序活动属性一起，初始调用有效负载包含以下请求元数据：</span><span class="sxs-lookup"><span data-stu-id="ddf69-110">Along with the standard bot activity properties, the initial invoke payload contains the following request metadata:</span></span>

|<span data-ttu-id="ddf69-111">属性名称</span><span class="sxs-lookup"><span data-stu-id="ddf69-111">Property name</span></span>|<span data-ttu-id="ddf69-112">用途</span><span class="sxs-lookup"><span data-stu-id="ddf69-112">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="ddf69-113">请求的类型。</span><span class="sxs-lookup"><span data-stu-id="ddf69-113">Type of request.</span></span> <span data-ttu-id="ddf69-114">它必须是 `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-114">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="ddf69-115">向服务发出的命令类型。</span><span class="sxs-lookup"><span data-stu-id="ddf69-115">Type of command that is issued to your service.</span></span> <span data-ttu-id="ddf69-116">它必须是 `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-116">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="ddf69-117">发送请求的用户的 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-117">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="ddf69-118">发送请求的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="ddf69-118">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="ddf69-119">Azure Active Directory发送请求的用户的对象 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-119">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="ddf69-120">Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-120">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="ddf69-121">如果 (通道请求，频道 ID 将) 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-121">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="ddf69-122">如果 (频道中提出请求，团队 ID 将) 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-122">Team ID (if the request was made in a channel).</span></span> |
|`value.commandId` | <span data-ttu-id="ddf69-123">包含已调用的命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-123">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="ddf69-124">触发事件的上下文。</span><span class="sxs-lookup"><span data-stu-id="ddf69-124">The context that triggered the event.</span></span> <span data-ttu-id="ddf69-125">它必须是 `compose` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-125">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="ddf69-126">用户的客户端主题，对嵌入式 Web 视图格式非常有用。</span><span class="sxs-lookup"><span data-stu-id="ddf69-126">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="ddf69-127">它必须是 `default` 、 `contrast` 或 `dark` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-127">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="ddf69-128">示例</span><span class="sxs-lookup"><span data-stu-id="ddf69-128">Example</span></span>

<span data-ttu-id="ddf69-129">初始调用请求的代码如下例所示：</span><span class="sxs-lookup"><span data-stu-id="ddf69-129">The code for the initial invoke request is given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-11-chat"></a><span data-ttu-id="ddf69-130">从一对一聊天调用任务模块时的有效负载活动属性</span><span class="sxs-lookup"><span data-stu-id="ddf69-130">Payload activity properties when a task module is invoked from 1:1 chat</span></span> 

<span data-ttu-id="ddf69-131">从一对一聊天调用任务模块时的有效负载活动属性列出如下：</span><span class="sxs-lookup"><span data-stu-id="ddf69-131">The payload activity properties when a task module is invoked from 1:1 chat are listed as follows:</span></span>

|<span data-ttu-id="ddf69-132">属性名称</span><span class="sxs-lookup"><span data-stu-id="ddf69-132">Property name</span></span>|<span data-ttu-id="ddf69-133">用途</span><span class="sxs-lookup"><span data-stu-id="ddf69-133">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="ddf69-134">请求的类型。</span><span class="sxs-lookup"><span data-stu-id="ddf69-134">Type of request.</span></span> <span data-ttu-id="ddf69-135">它必须是 `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-135">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="ddf69-136">向服务发出的命令类型。</span><span class="sxs-lookup"><span data-stu-id="ddf69-136">Type of command that is issued to your service.</span></span> <span data-ttu-id="ddf69-137">它必须是 `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-137">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="ddf69-138">发送请求的用户的 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-138">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="ddf69-139">发送请求的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="ddf69-139">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="ddf69-140">Azure Active Directory发送请求的用户的对象 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-140">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="ddf69-141">Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-141">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="ddf69-142">调用任务模块的源名称。</span><span class="sxs-lookup"><span data-stu-id="ddf69-142">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="ddf69-143">获取或设置邮件的回复 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-143">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="ddf69-144">包含已调用的命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-144">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="ddf69-145">触发事件的上下文。</span><span class="sxs-lookup"><span data-stu-id="ddf69-145">The context that triggered the event.</span></span> <span data-ttu-id="ddf69-146">它必须是 `compose` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-146">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="ddf69-147">用户的客户端主题，对嵌入式 Web 视图格式非常有用。</span><span class="sxs-lookup"><span data-stu-id="ddf69-147">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="ddf69-148">它必须是 `default` 、 `contrast` 或 `dark` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-148">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="ddf69-149">示例</span><span class="sxs-lookup"><span data-stu-id="ddf69-149">Example</span></span>

<span data-ttu-id="ddf69-150">以下示例提供从一对一聊天调用任务模块时的有效负载活动属性：</span><span class="sxs-lookup"><span data-stu-id="ddf69-150">The payload activity properties when a task module is invoked from 1:1 chat are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```
## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-group-chat"></a><span data-ttu-id="ddf69-151">从群聊中调用任务模块时的有效负载活动属性</span><span class="sxs-lookup"><span data-stu-id="ddf69-151">Payload activity properties when a task module is invoked from a group chat</span></span> 

<span data-ttu-id="ddf69-152">从群聊中调用任务模块时的有效负载活动属性列出如下：</span><span class="sxs-lookup"><span data-stu-id="ddf69-152">The payload activity properties when a task module is invoked from a group chat are listed as follows:</span></span>

|<span data-ttu-id="ddf69-153">属性名称</span><span class="sxs-lookup"><span data-stu-id="ddf69-153">Property name</span></span>|<span data-ttu-id="ddf69-154">用途</span><span class="sxs-lookup"><span data-stu-id="ddf69-154">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="ddf69-155">请求的类型。</span><span class="sxs-lookup"><span data-stu-id="ddf69-155">Type of request.</span></span> <span data-ttu-id="ddf69-156">它必须是 `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-156">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="ddf69-157">向服务发出的命令类型。</span><span class="sxs-lookup"><span data-stu-id="ddf69-157">Type of command that is issued to your service.</span></span> <span data-ttu-id="ddf69-158">它必须是 `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-158">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="ddf69-159">发送请求的用户的 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-159">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="ddf69-160">发送请求的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="ddf69-160">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="ddf69-161">Azure Active Directory发送请求的用户的对象 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-161">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="ddf69-162">Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-162">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="ddf69-163">调用任务模块的源名称。</span><span class="sxs-lookup"><span data-stu-id="ddf69-163">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="ddf69-164">获取或设置邮件的回复 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-164">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="ddf69-165">包含已调用的命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-165">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="ddf69-166">触发事件的上下文。</span><span class="sxs-lookup"><span data-stu-id="ddf69-166">The context that triggered the event.</span></span> <span data-ttu-id="ddf69-167">它必须是 `compose` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-167">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="ddf69-168">用户的客户端主题，对嵌入式 Web 视图格式非常有用。</span><span class="sxs-lookup"><span data-stu-id="ddf69-168">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="ddf69-169">它必须是 `default` 、 `contrast` 或 `dark` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-169">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="ddf69-170">示例</span><span class="sxs-lookup"><span data-stu-id="ddf69-170">Example</span></span>

<span data-ttu-id="ddf69-171">以下示例中提供从群聊调用任务模块时的有效负载活动属性：</span><span class="sxs-lookup"><span data-stu-id="ddf69-171">The payload activity properties when a task module is invoked from a group chat are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:bf72031f-a17e-f99c-48dc-5c0714950d87",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "groupChat",
    "id": "19:d77be72390a1416e9644261e9064fa00@thread.skype",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "213167a1e3b6428b93e186ea5407c759",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-new-post"></a><span data-ttu-id="ddf69-172">从频道调用任务模块时的有效负载活动属性 (发布) </span><span class="sxs-lookup"><span data-stu-id="ddf69-172">Payload activity properties when a task module is invoked from a channel (new post)</span></span> 

<span data-ttu-id="ddf69-173">从频道调用任务模块时的有效负载活动属性 (发布) 如下所示：</span><span class="sxs-lookup"><span data-stu-id="ddf69-173">The payload activity properties when a task module is invoked from a channel (new post) are listed as follows:</span></span>

|<span data-ttu-id="ddf69-174">属性名称</span><span class="sxs-lookup"><span data-stu-id="ddf69-174">Property name</span></span>|<span data-ttu-id="ddf69-175">用途</span><span class="sxs-lookup"><span data-stu-id="ddf69-175">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="ddf69-176">请求的类型。</span><span class="sxs-lookup"><span data-stu-id="ddf69-176">Type of request.</span></span> <span data-ttu-id="ddf69-177">它必须是 `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-177">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="ddf69-178">向服务发出的命令类型。</span><span class="sxs-lookup"><span data-stu-id="ddf69-178">Type of command that is issued to your service.</span></span> <span data-ttu-id="ddf69-179">它必须是 `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-179">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="ddf69-180">发送请求的用户的 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-180">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="ddf69-181">发送请求的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="ddf69-181">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="ddf69-182">Azure Active Directory发送请求的用户的对象 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-182">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="ddf69-183">Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-183">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="ddf69-184">如果 (通道请求，频道 ID 将) 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-184">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="ddf69-185">如果 (频道中提出请求，团队 ID 将) 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-185">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="ddf69-186">调用任务模块的源名称。</span><span class="sxs-lookup"><span data-stu-id="ddf69-186">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="ddf69-187">获取或设置邮件的回复 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-187">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="ddf69-188">包含已调用的命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-188">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="ddf69-189">触发事件的上下文。</span><span class="sxs-lookup"><span data-stu-id="ddf69-189">The context that triggered the event.</span></span> <span data-ttu-id="ddf69-190">它必须是 `compose` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-190">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="ddf69-191">用户的客户端主题，对嵌入式 Web 视图格式非常有用。</span><span class="sxs-lookup"><span data-stu-id="ddf69-191">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="ddf69-192">它必须是 `default` 、 `contrast` 或 `dark` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-192">It must be `default`, `contrast`, or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="ddf69-193">示例</span><span class="sxs-lookup"><span data-stu-id="ddf69-193">Example</span></span>

<span data-ttu-id="ddf69-194">从频道调用任务模块时的有效负载活动属性 (以下示例) 文章时的有效负载活动属性：</span><span class="sxs-lookup"><span data-stu-id="ddf69-194">The payload activity properties when a task module is invoked from a channel (new post) are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:a5fbb109-c989-c449-ee83-71ac99919d4b",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "5336640edc7748b28ce2df43f5b45963",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-reply-to-thread"></a><span data-ttu-id="ddf69-195">从频道调用任务模块时的有效负载活动属性 (线程) </span><span class="sxs-lookup"><span data-stu-id="ddf69-195">Payload activity properties when a task module is invoked from a channel (reply to thread)</span></span> 

<span data-ttu-id="ddf69-196">从频道调用任务模块时的有效负载活动属性 (主题) 如下所示：</span><span class="sxs-lookup"><span data-stu-id="ddf69-196">The payload activity properties when a task module is invoked from a channel (reply to thread) are listed as follows:</span></span>

|<span data-ttu-id="ddf69-197">属性名称</span><span class="sxs-lookup"><span data-stu-id="ddf69-197">Property name</span></span>|<span data-ttu-id="ddf69-198">用途</span><span class="sxs-lookup"><span data-stu-id="ddf69-198">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="ddf69-199">请求的类型。</span><span class="sxs-lookup"><span data-stu-id="ddf69-199">Type of request.</span></span> <span data-ttu-id="ddf69-200">它必须是 `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-200">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="ddf69-201">向服务发出的命令类型。</span><span class="sxs-lookup"><span data-stu-id="ddf69-201">Type of command that is issued to your service.</span></span> <span data-ttu-id="ddf69-202">它必须是 `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-202">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="ddf69-203">发送请求的用户的 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-203">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="ddf69-204">发送请求的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="ddf69-204">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="ddf69-205">Azure Active Directory发送请求的用户的对象 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-205">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="ddf69-206">Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-206">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="ddf69-207">如果 (通道请求，频道 ID 将) 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-207">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="ddf69-208">如果 (频道中提出请求，团队 ID 将) 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-208">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="ddf69-209">调用任务模块的源名称。</span><span class="sxs-lookup"><span data-stu-id="ddf69-209">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="ddf69-210">获取或设置邮件的回复 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-210">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="ddf69-211">包含已调用的命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-211">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="ddf69-212">触发事件的上下文。</span><span class="sxs-lookup"><span data-stu-id="ddf69-212">The context that triggered the event.</span></span> <span data-ttu-id="ddf69-213">它必须是 `compose` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-213">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="ddf69-214">用户的客户端主题，对嵌入式 Web 视图格式非常有用。</span><span class="sxs-lookup"><span data-stu-id="ddf69-214">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="ddf69-215">它必须是 `default` 、 `contrast` 或 `dark` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-215">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="ddf69-216">示例</span><span class="sxs-lookup"><span data-stu-id="ddf69-216">Example</span></span>

<span data-ttu-id="ddf69-217">从频道调用任务模块时的有效负载活动属性 (以下示例) 主题响应：</span><span class="sxs-lookup"><span data-stu-id="ddf69-217">The payload activity properties when a task module is invoked from a channel (reply to thread) are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:19ccc884-c792-35ef-2f40-d0ff43dcca71",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype;messageid=1611060744833",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "message",
    "requestId": "7f7d22efe5414818becebcec649a7912",
    "messagePayload": {
      "linkToMessage": "https://teams.microsoft.com/l/message/19:6decf54d86d945e4b3924b63a9161a78@thread.skype/1611060744833",
      "id": "1611060744833",
      "replyToId": null,
      "createdDateTime": "2021-01-19T12:52:24.833Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "<div><div><at id=\"0\">Testing outgoing Webhook-Nikitha</at> - Hi</div>\n</div>"
      },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc",
          "displayName": "Olo Brockhouse"
        },
        "application": null
      },
      "reactions": [],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Testing outgoing Webhook-Nikitha",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": null,
            "application": {
              "applicationIdentityType": "webhook",
              "id": "b8c1c68c-e290-4bdd-81c3-266f310751dc",
              "displayName": "Testing outgoing Webhook-Nikitha"
            }
          }
        }
      ],
      "attachments": []
    },
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-command-box"></a><span data-ttu-id="ddf69-218">从命令框调用任务模块时的有效负载活动属性</span><span class="sxs-lookup"><span data-stu-id="ddf69-218">Payload activity properties when a task module is invoked from a command box</span></span> 

<span data-ttu-id="ddf69-219">从命令框调用任务模块时的有效负载活动属性列出如下：</span><span class="sxs-lookup"><span data-stu-id="ddf69-219">The payload activity properties when a task module is invoked from a command box are listed as follows:</span></span>

|<span data-ttu-id="ddf69-220">属性名称</span><span class="sxs-lookup"><span data-stu-id="ddf69-220">Property name</span></span>|<span data-ttu-id="ddf69-221">用途</span><span class="sxs-lookup"><span data-stu-id="ddf69-221">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="ddf69-222">请求的类型。</span><span class="sxs-lookup"><span data-stu-id="ddf69-222">Type of request.</span></span> <span data-ttu-id="ddf69-223">它必须是 `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-223">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="ddf69-224">向服务发出的命令类型。</span><span class="sxs-lookup"><span data-stu-id="ddf69-224">Type of command that is issued to your service.</span></span> <span data-ttu-id="ddf69-225">它必须是 `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-225">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="ddf69-226">发送请求的用户的 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-226">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="ddf69-227">发送请求的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="ddf69-227">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="ddf69-228">Azure Active Directory发送请求的用户的对象 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-228">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="ddf69-229">Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-229">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="ddf69-230">调用任务模块的源名称。</span><span class="sxs-lookup"><span data-stu-id="ddf69-230">The source name from where task module is invoked.</span></span> |
|`value.commandId` | <span data-ttu-id="ddf69-231">包含已调用的命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="ddf69-231">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="ddf69-232">触发事件的上下文。</span><span class="sxs-lookup"><span data-stu-id="ddf69-232">The context that triggered the event.</span></span> <span data-ttu-id="ddf69-233">它必须是 `compose` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-233">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="ddf69-234">用户的客户端主题，对嵌入式 Web 视图格式非常有用。</span><span class="sxs-lookup"><span data-stu-id="ddf69-234">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="ddf69-235">它必须是 `default` 、 `contrast` 或 `dark` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-235">It must be `default`, `contrast`, or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="ddf69-236">示例</span><span class="sxs-lookup"><span data-stu-id="ddf69-236">Example</span></span>

<span data-ttu-id="ddf69-237">下面的示例提供从命令框调用任务模块时的有效负载活动属性：</span><span class="sxs-lookup"><span data-stu-id="ddf69-237">The payload activity properties when a task module is invoked from a command box are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:172560f1-95f9-3189-edb2-b7612cd1a3cd",
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "compose",
    "requestId": "d2ce690cdc2b4920a538e75882610a30",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

### <a name="example"></a><span data-ttu-id="ddf69-238">示例</span><span class="sxs-lookup"><span data-stu-id="ddf69-238">Example</span></span> 

<span data-ttu-id="ddf69-239">以下代码部分是请求 `fetchTask` 的一个示例：</span><span class="sxs-lookup"><span data-stu-id="ddf69-239">The following code section is an example of `fetchTask` request:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="ddf69-240">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ddf69-240">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="ddf69-241">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="ddf69-241">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[<span data-ttu-id="ddf69-242">JSON</span><span class="sxs-lookup"><span data-stu-id="ddf69-242">JSON</span></span>](#tab/json)

```json
{
  "name": "composeExtension/fetchTask",
  "type": "invoke",
  "timestamp": "2019-07-01T22:57:22.175Z",
  "localTimestamp": "2019-07-01T15:57:22.175-07:00",
  "id": "f:0123456878990178955",
  "channelId": "msteams",
  "serviceURL": "https://smba.trafficmanager.net/amer/",
  "from": {
    "id": "29:1test2GgHIa0DXzDT_OGwL5vSMZdAxDlGR7hYxZ6_JBVqHz2Zq9Nm44FUNWqHCdGBwHg8WrlFRsYrd0cCAS7dig",
    "name": "John Smith",
    "aadObjectId": "1234567d-1234-462a-8952-35b75f16f1e1"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "tenantId": "1234abcd-1234-12ab-12ab-35b75f16f1e1",
    "id": "19:83ed1d507cb5427c93495cf914326310@thread.skype"
  },
  "recipient": {
    "id": "28:049566e0-4401-4bcf-86a1-ce22082ce03a",
    "name": "mess"
  },
  "entities": [
    {
      "locale": "en-US",
      "country": "US",
      "platform": "Windows",
      "type": "clientInfo"
    }
  ],
  "channelData": {
    "channel": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "team": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "tenant": {
      "id": "1234abcd-1234-12ab-12ab-35b75f16f1e1"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "hello",
    "commandContext": "compose",
    "context": {
      "theme": "dark"
    }
  },
  "locale": "en-US"
}
```

* * *

## <a name="initial-invoke-request-from-a-message"></a><span data-ttu-id="ddf69-243">来自邮件的初始调用请求</span><span class="sxs-lookup"><span data-stu-id="ddf69-243">Initial invoke request from a message</span></span>

<span data-ttu-id="ddf69-244">从邮件调用自动程序时，初始调用请求中的对象必须包含从其中调用消息扩展 `value` 的消息的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ddf69-244">When your bot is invoked from a message,  the `value` object in the initial invoke request must contain the details of the message that your messaging extension is invoked from.</span></span> <span data-ttu-id="ddf69-245">和 数组是可选的，如果原始邮件中没有任何反应或提及，则它们 `reactions` `mentions` 不存在。</span><span class="sxs-lookup"><span data-stu-id="ddf69-245">The `reactions` and `mentions` arrays are optional, and they are not present if there are no reactions or mentions in the original message.</span></span> <span data-ttu-id="ddf69-246">以下部分是 对象 `value` 的示例：</span><span class="sxs-lookup"><span data-stu-id="ddf69-246">The following section is an example of the `value` object:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="ddf69-247">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ddf69-247">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="ddf69-248">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="ddf69-248">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[<span data-ttu-id="ddf69-249">JSON</span><span class="sxs-lookup"><span data-stu-id="ddf69-249">JSON</span></span>](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "This is the message the messaging extension was invoked from."
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

* * *

## <a name="respond-to-the-fetchtask"></a><span data-ttu-id="ddf69-250">响应 fetchTask</span><span class="sxs-lookup"><span data-stu-id="ddf69-250">Respond to the fetchTask</span></span>

<span data-ttu-id="ddf69-251">使用包含具有自适应卡片或 Web URL 的对象或简单的字符串消息的对象响应 `task` `taskInfo` 调用请求。</span><span class="sxs-lookup"><span data-stu-id="ddf69-251">Respond to the invoke request with a `task` object that contains either a `taskInfo` object with the Adaptive Card or web URL, or a simple string message.</span></span>

|<span data-ttu-id="ddf69-252">属性名称</span><span class="sxs-lookup"><span data-stu-id="ddf69-252">Property name</span></span>|<span data-ttu-id="ddf69-253">用途</span><span class="sxs-lookup"><span data-stu-id="ddf69-253">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="ddf69-254">可以是显示 `continue` 窗体，也可以 `message` 用于简单的弹出式窗体。</span><span class="sxs-lookup"><span data-stu-id="ddf69-254">Can be either `continue` to present a form, or `message` for a simple popup.</span></span> |
|`value`| <span data-ttu-id="ddf69-255">窗体 `taskInfo` 的对象或邮件 `string` 的 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-255">Either a `taskInfo` object for a form, or a `string` for a message.</span></span> |

<span data-ttu-id="ddf69-256">taskInfo 对象的架构为：</span><span class="sxs-lookup"><span data-stu-id="ddf69-256">The schema for the taskInfo object is:</span></span>

|<span data-ttu-id="ddf69-257">属性名称</span><span class="sxs-lookup"><span data-stu-id="ddf69-257">Property name</span></span>|<span data-ttu-id="ddf69-258">用途</span><span class="sxs-lookup"><span data-stu-id="ddf69-258">Purpose</span></span>|
|---|---|
|`title`| <span data-ttu-id="ddf69-259">任务模块的标题。</span><span class="sxs-lookup"><span data-stu-id="ddf69-259">The title of the task module.</span></span>|
|`height`| <span data-ttu-id="ddf69-260">它必须是整数值 (以像素为单位) 或 `small` 、 `medium` 、 `large` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-260">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`width`| <span data-ttu-id="ddf69-261">它必须是整数值 (以像素为单位) 或 `small` 、 `medium` 、 `large` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-261">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`card`| <span data-ttu-id="ddf69-262">定义表单的自适应卡片 (使用一个) 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-262">The adaptive card defining the form (if using one).</span></span>
|`url`| <span data-ttu-id="ddf69-263">在任务模块内作为嵌入 Web 视图打开的 URL。</span><span class="sxs-lookup"><span data-stu-id="ddf69-263">The URL to be opened inside of the task module as an embedded web view.</span></span>|
|`fallbackUrl`| <span data-ttu-id="ddf69-264">如果客户端不支持任务模块功能，此 URL 在浏览器选项卡中打开。</span><span class="sxs-lookup"><span data-stu-id="ddf69-264">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |

### <a name="respond-to-the-fetchtask-with-an-adaptive-card"></a><span data-ttu-id="ddf69-265">使用自适应卡片响应 fetchTask</span><span class="sxs-lookup"><span data-stu-id="ddf69-265">Respond to the fetchTask with an Adaptive Card</span></span>

<span data-ttu-id="ddf69-266">使用自适应卡片时，必须使用对象响应包含自适应卡片 `task` `value` 的对象。</span><span class="sxs-lookup"><span data-stu-id="ddf69-266">When using an adaptive card, you must respond with a `task` object with the `value` object containing an Adaptive Card.</span></span>

#### <a name="example"></a><span data-ttu-id="ddf69-267">示例</span><span class="sxs-lookup"><span data-stu-id="ddf69-267">Example</span></span>

<span data-ttu-id="ddf69-268">以下代码部分是使用自适应 `fetchTask` 卡片响应的示例：</span><span class="sxs-lookup"><span data-stu-id="ddf69-268">The following code section is an example to `fetchTask` response with an adaptive card:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="ddf69-269">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ddf69-269">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="ddf69-270">此示例除了使用 Bot Framework SDK NuGet还使用[AdaptiveCards](https://www.nuget.org/packages/AdaptiveCards) NuGet包。</span><span class="sxs-lookup"><span data-stu-id="ddf69-270">This sample uses the [AdaptiveCards NuGet package](https://www.nuget.org/packages/AdaptiveCards) in addition to the Bot Framework SDK.</span></span>

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Card = new Attachment()
        {
          ContentType = AdaptiveCard.ContentType,
          Content = new AdaptiveCard("1.0")
          {
            Body = new List<AdaptiveElement>()
            {
              new AdaptiveTextInput() { Id = "FormField1", Placeholder = placeholder},
              new AdaptiveTextInput() { Id = "FormField2", Placeholder = "FormField2"},
              new AdaptiveTextInput() { Id = "FormField3", Placeholder = "FormField3"},
            },
            Actions = new List<AdaptiveAction>()
            {
              new AdaptiveSubmitAction()
              {
                Type = AdaptiveSubmitAction.TypeName,
                Title = "Submit",
              },
            },
          },
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="ddf69-271">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="ddf69-271">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    handleTeamsMessagingExtensionFetchTask(context, action) {
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [{
          data: { submitLocation: 'messagingExtensionFetchTask'},
          title: 'Submit',
          type: 'Action.Submit'
        }],
        body: [
          { text: 'Task Module', type: 'TextBlock', weight: 'bolder'},
          { type: 'TextBlock', text: 'Enter text for Question:' },
          { id: 'Question', placeholder: 'Question text here', type: 'Input.Text', value: userText },
          { type: 'TextBlock', text: 'Options for Question:' },
          { type: 'TextBlock', text: 'Is Multi-Select:' },
          {
            choices: [{ title: 'True', value: 'true' }, { title: 'False', value: 'false' }],
            id: 'MultiSelect',
            isMultiSelect: false,
            style: 'expanded',
            type: 'Input.ChoiceSet',
            value: isMultiSelect ? 'true' : 'false'
          },
          { id: 'Option1', placeholder: 'Option 1 here', type: 'Input.Text', value: option1 },
          { id: 'Option2', placeholder: 'Option 2 here', type: 'Input.Text', value: option2 }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });

      return {
        task: {
          type: 'continue',
          value: {
            card: adaptiveCard,
            height: 450,
            title: 'Task Module Fetch Example',
            url: null,
            width: 500
          }
        }
      };
    }
}
```

# <a name="json"></a>[<span data-ttu-id="ddf69-272">JSON</span><span class="sxs-lookup"><span data-stu-id="ddf69-272">JSON</span></span>](#tab/json)

```json
 {
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "card": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Input.Text",
            "placeholder": "FormField1",
            "id": "FormField1"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField2",
            "id": "FormField2"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField3",
            "id": "FormField3"
          },
          {
            "type": "ActionSet",
            "actions": [
              {
                "type": "Action.Submit",
                "title": "Action.Submit",
                "id": "submitAction"
              }
            ]
          }
        ]
      }
    }
  }
}
```

* * *

### <a name="create-a-task-module-with-an-embedded-web-view"></a><span data-ttu-id="ddf69-273">使用嵌入式 Web 视图创建任务模块</span><span class="sxs-lookup"><span data-stu-id="ddf69-273">Create a task module with an embedded web view</span></span>

<span data-ttu-id="ddf69-274">使用嵌入的 Web 视图时，必须使用对象（该对象包含要加载的 Web 表单 `task` `value` 的 URL）进行响应。</span><span class="sxs-lookup"><span data-stu-id="ddf69-274">When using an embedded web view, you must respond with a `task` object with the `value` object containing the URL to the web form that you want to load.</span></span> <span data-ttu-id="ddf69-275">要加载的任何 URL 的域必须包含在应用清单的数组 `validDomains` 中。</span><span class="sxs-lookup"><span data-stu-id="ddf69-275">The domains of any URL you want to load must be included in the `validDomains` array in your app's manifest.</span></span> <span data-ttu-id="ddf69-276">有关生成嵌入式 Web 视图的信息，请参阅 [任务模块文档](~/task-modules-and-cards/what-are-task-modules.md)。</span><span class="sxs-lookup"><span data-stu-id="ddf69-276">For more information on building your embedded web view, see the [task module documentation](~/task-modules-and-cards/what-are-task-modules.md).</span></span> 

# <a name="cnet"></a>[<span data-ttu-id="ddf69-277">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ddf69-277">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Url = "https://contoso.com/msteams/taskmodules/newcustomer",
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="ddf69-278">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="ddf69-278">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    return {
      task: {
        type: 'continue',
        value: {
          width: 500,
          height: 450,
          title: 'Task Module Fetch Example',
          url: 'https://contoso.com/msteams/taskmodules/newcustomer',
          fallbackUrl: 'https://contoso.com/msteams/taskmodules/newcustomer'
        }
      }
    };
  }
}
```

# <a name="json"></a>[<span data-ttu-id="ddf69-279">JSON</span><span class="sxs-lookup"><span data-stu-id="ddf69-279">JSON</span></span>](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "url": "https://contoso.com/msteams/taskmodules/newcustomer",
      "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
    }
  }
}
```

* * *

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="ddf69-280">请求安装对话机器人</span><span class="sxs-lookup"><span data-stu-id="ddf69-280">Request to install your conversational bot</span></span>

<span data-ttu-id="ddf69-281">如果应用包含对话机器人，则安装对话中的机器人，然后加载任务模块。</span><span class="sxs-lookup"><span data-stu-id="ddf69-281">If the app contains a conversational bot, install the bot in the conversation and then load the task module.</span></span> <span data-ttu-id="ddf69-282">自动程序可用于获取任务模块的其他上下文。</span><span class="sxs-lookup"><span data-stu-id="ddf69-282">The bot is useful to get additional context for the task module.</span></span> <span data-ttu-id="ddf69-283">此方案的一个示例是提取名单以填充人员选取器控件或团队中的频道列表。</span><span class="sxs-lookup"><span data-stu-id="ddf69-283">An example for this scenario is to fetch the roster to populate a people picker control or the list of channels in a team.</span></span>

<span data-ttu-id="ddf69-284">当消息扩展收到调用时，请检查自动程序是否安装在当前上下文中以便于 `composeExtension/fetchTask` 流。</span><span class="sxs-lookup"><span data-stu-id="ddf69-284">When the messaging extension receives the `composeExtension/fetchTask` invoke, check if the bot is installed in the current context to facilitate the flow.</span></span> <span data-ttu-id="ddf69-285">例如，使用获取名单呼叫检查流程。</span><span class="sxs-lookup"><span data-stu-id="ddf69-285">For example, check the flow with a get roster call.</span></span> <span data-ttu-id="ddf69-286">如果未安装自动程序，则返回自适应卡片以及请求用户安装自动程序的操作。</span><span class="sxs-lookup"><span data-stu-id="ddf69-286">If the bot is not installed, return an Adaptive Card with an action that requests the user to install the bot.</span></span> <span data-ttu-id="ddf69-287">用户必须有权将应用安装到该位置进行检查。</span><span class="sxs-lookup"><span data-stu-id="ddf69-287">The user must have the permission to install the apps in that location for checking.</span></span> <span data-ttu-id="ddf69-288">如果应用安装不成功，用户将收到一条消息，联系管理员。</span><span class="sxs-lookup"><span data-stu-id="ddf69-288">If the app installation is unsuccessful, the user receives a message to contact the administrator.</span></span>

#### <a name="example"></a><span data-ttu-id="ddf69-289">示例</span><span class="sxs-lookup"><span data-stu-id="ddf69-289">Example</span></span> 

<span data-ttu-id="ddf69-290">以下代码部分是响应的一个示例：</span><span class="sxs-lookup"><span data-stu-id="ddf69-290">The following code section is an example of the response:</span></span>

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

<span data-ttu-id="ddf69-291">安装对话机器人后，它会收到另一条使用 和 的调用 `name = composeExtension/submitAction` 消息 `value.data.msteams.justInTimeInstall = true` 。</span><span class="sxs-lookup"><span data-stu-id="ddf69-291">After the installation of conversational bot, it receives another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

#### <a name="example"></a><span data-ttu-id="ddf69-292">示例</span><span class="sxs-lookup"><span data-stu-id="ddf69-292">Example</span></span> 

<span data-ttu-id="ddf69-293">以下代码部分是调用的任务响应示例：</span><span class="sxs-lookup"><span data-stu-id="ddf69-293">The following code section is an example of the task response to the invoke:</span></span>

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

<span data-ttu-id="ddf69-294">对调用的任务响应必须类似于已安装的机器人。</span><span class="sxs-lookup"><span data-stu-id="ddf69-294">The task response to the invoke must be similar to that of the installed bot.</span></span>

#### <a name="example"></a><span data-ttu-id="ddf69-295">示例</span><span class="sxs-lookup"><span data-stu-id="ddf69-295">Example</span></span> 

<span data-ttu-id="ddf69-296">以下代码部分是一个使用自适应卡片实时安装应用的示例：</span><span class="sxs-lookup"><span data-stu-id="ddf69-296">The following code section is an example of just-in time installation of app with Adaptive card:</span></span> 

```csharp
private static Attachment GetAdaptiveCardAttachmentFromFile(string fileName)
  {
      //Read the card json and create attachment.
         string[] paths = { ".", "Resources", fileName };
         var adaptiveCardJson = File.ReadAllText(Path.Combine(paths));
         var adaptiveCardAttachment = new Attachment()
            {
                ContentType = "application/vnd.microsoft.card.adaptive",
                Content = JsonConvert.DeserializeObject(adaptiveCardJson),
            };
            return adaptiveCardAttachment;
        }
```

* * *

## <a name="code-sample"></a><span data-ttu-id="ddf69-297">代码示例</span><span class="sxs-lookup"><span data-stu-id="ddf69-297">Code sample</span></span>

| <span data-ttu-id="ddf69-298">示例名称</span><span class="sxs-lookup"><span data-stu-id="ddf69-298">Sample Name</span></span>           | <span data-ttu-id="ddf69-299">说明</span><span class="sxs-lookup"><span data-stu-id="ddf69-299">Description</span></span> | <span data-ttu-id="ddf69-300">.NET</span><span class="sxs-lookup"><span data-stu-id="ddf69-300">.NET</span></span>    | <span data-ttu-id="ddf69-301">Node.js</span><span class="sxs-lookup"><span data-stu-id="ddf69-301">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="ddf69-302">Teams邮件扩展操作</span><span class="sxs-lookup"><span data-stu-id="ddf69-302">Teams messaging extension action</span></span>| <span data-ttu-id="ddf69-303">介绍如何定义操作命令、创建任务模块和响应任务模块提交操作。</span><span class="sxs-lookup"><span data-stu-id="ddf69-303">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="ddf69-304">View</span><span class="sxs-lookup"><span data-stu-id="ddf69-304">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="ddf69-305">View</span><span class="sxs-lookup"><span data-stu-id="ddf69-305">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="ddf69-306">Teams邮件扩展搜索</span><span class="sxs-lookup"><span data-stu-id="ddf69-306">Teams messaging extension search</span></span>   |  <span data-ttu-id="ddf69-307">介绍如何定义搜索命令并响应搜索。</span><span class="sxs-lookup"><span data-stu-id="ddf69-307">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="ddf69-308">View</span><span class="sxs-lookup"><span data-stu-id="ddf69-308">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="ddf69-309">View</span><span class="sxs-lookup"><span data-stu-id="ddf69-309">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a><span data-ttu-id="ddf69-310">另请参阅</span><span class="sxs-lookup"><span data-stu-id="ddf69-310">See also</span></span>

[<span data-ttu-id="ddf69-311">定义操作命令</span><span class="sxs-lookup"><span data-stu-id="ddf69-311">Define action commands</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)


## <a name="next-step"></a><span data-ttu-id="ddf69-312">后续步骤</span><span class="sxs-lookup"><span data-stu-id="ddf69-312">Next step</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="ddf69-313">响应操作命令</span><span class="sxs-lookup"><span data-stu-id="ddf69-313">Respond to action command</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

