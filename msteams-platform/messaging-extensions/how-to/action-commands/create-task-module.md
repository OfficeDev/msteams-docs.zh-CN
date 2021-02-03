---
title: 创建并发送任务模块
author: clearab
description: 如何处理初始调用操作以及从操作消息扩展命令使用任务模块进行响应
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 58fb7e1ff5690b33c2e23f68529f05869afa9016
ms.sourcegitcommit: ce74f821660b1258c72b3c3f71c1cf177e7e92ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2021
ms.locfileid: "50072873"
---
# <a name="create-and-send-the-task-module"></a><span data-ttu-id="03802-103">创建并发送任务模块</span><span class="sxs-lookup"><span data-stu-id="03802-103">Create and send the task module</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="03802-104">如果未使用应用清单中定义的参数填充任务模块，则必须为用户创建任务模块。</span><span class="sxs-lookup"><span data-stu-id="03802-104">If you are not populating the task module with parameters defined in the app manifest, you must create the task module for users.</span></span> <span data-ttu-id="03802-105">使用自适应卡片或嵌入式 Web 视图。</span><span class="sxs-lookup"><span data-stu-id="03802-105">Use either an Adaptive Card or an embedded web view.</span></span>

## <a name="the-initial-invoke-request"></a><span data-ttu-id="03802-106">初始调用请求</span><span class="sxs-lookup"><span data-stu-id="03802-106">The initial invoke request</span></span>

<span data-ttu-id="03802-107">使用此方法，你的服务将收到一个类型对象，并且必须使用包含自适应卡片或嵌入 Web 视图 `Activity` `composeExtension/fetchTask` 的 URL `task` 的对象进行响应。</span><span class="sxs-lookup"><span data-stu-id="03802-107">Using this method your service will receive an `Activity` object of type `composeExtension/fetchTask`, and you must respond with a `task` object containing either the adaptive card or a URL to the embedded web view.</span></span> <span data-ttu-id="03802-108">除了标准自动程序活动属性外，初始调用负载还包含以下请求元数据：</span><span class="sxs-lookup"><span data-stu-id="03802-108">Along with the standard bot activity properties, the initial invoke payload contains the following request metadata:</span></span>

|<span data-ttu-id="03802-109">属性名称</span><span class="sxs-lookup"><span data-stu-id="03802-109">Property name</span></span>|<span data-ttu-id="03802-110">用途</span><span class="sxs-lookup"><span data-stu-id="03802-110">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="03802-111">请求的类型。</span><span class="sxs-lookup"><span data-stu-id="03802-111">Type of request.</span></span> <span data-ttu-id="03802-112">它必须是 `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="03802-112">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="03802-113">向服务发出的命令类型。</span><span class="sxs-lookup"><span data-stu-id="03802-113">Type of command that is issued to your service.</span></span> <span data-ttu-id="03802-114">它必须是 `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="03802-114">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="03802-115">发送请求的用户的 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-115">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="03802-116">发送请求的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="03802-116">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="03802-117">发送请求的用户的 Azure Active Directory 对象 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-117">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="03802-118">Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-118">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="03802-119">如果在 (通道中提出请求，通道 ID 将) 。</span><span class="sxs-lookup"><span data-stu-id="03802-119">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="03802-120">如果 (频道中提出请求，团队 ID) 。</span><span class="sxs-lookup"><span data-stu-id="03802-120">Team ID (if the request was made in a channel).</span></span> |
|`value.commandId` | <span data-ttu-id="03802-121">包含已调用的命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-121">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="03802-122">触发事件的上下文。</span><span class="sxs-lookup"><span data-stu-id="03802-122">The context that triggered the event.</span></span> <span data-ttu-id="03802-123">它必须是 `compose` 。</span><span class="sxs-lookup"><span data-stu-id="03802-123">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="03802-124">用户的客户端主题，可用于嵌入 Web 视图格式。</span><span class="sxs-lookup"><span data-stu-id="03802-124">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="03802-125">它必须是 `default` ， `contrast` 或 `dark` 。</span><span class="sxs-lookup"><span data-stu-id="03802-125">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-11-chat-are-listed-in-the-following-section"></a><span data-ttu-id="03802-126">以下部分列出了从 1：1 聊天调用任务模块时的有效负载活动属性：</span><span class="sxs-lookup"><span data-stu-id="03802-126">Payload activity properties when invoked a task module from 1:1 chat are listed in the following section:</span></span>

|<span data-ttu-id="03802-127">属性名称</span><span class="sxs-lookup"><span data-stu-id="03802-127">Property name</span></span>|<span data-ttu-id="03802-128">用途</span><span class="sxs-lookup"><span data-stu-id="03802-128">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="03802-129">请求的类型。</span><span class="sxs-lookup"><span data-stu-id="03802-129">Type of request.</span></span> <span data-ttu-id="03802-130">它必须是 `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="03802-130">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="03802-131">向服务发出的命令类型。</span><span class="sxs-lookup"><span data-stu-id="03802-131">Type of command that is issued to your service.</span></span> <span data-ttu-id="03802-132">它必须是 `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="03802-132">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="03802-133">发送请求的用户的 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-133">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="03802-134">发送请求的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="03802-134">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="03802-135">发送请求的用户的 Azure Active Directory 对象 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-135">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="03802-136">Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-136">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="03802-137">调用任务模块的源名称。</span><span class="sxs-lookup"><span data-stu-id="03802-137">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="03802-138">获取或设置此邮件作为回复的邮件的 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-138">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="03802-139">包含已调用的命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-139">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="03802-140">触发事件的上下文。</span><span class="sxs-lookup"><span data-stu-id="03802-140">The context that triggered the event.</span></span> <span data-ttu-id="03802-141">它必须是 `compose` 。</span><span class="sxs-lookup"><span data-stu-id="03802-141">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="03802-142">用户的客户端主题，可用于嵌入 Web 视图格式。</span><span class="sxs-lookup"><span data-stu-id="03802-142">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="03802-143">它必须是 `default` ， `contrast` 或 `dark` 。</span><span class="sxs-lookup"><span data-stu-id="03802-143">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-group-chat-are-listed-in-the-following-section"></a><span data-ttu-id="03802-144">以下部分列出了从群聊调用任务模块时的有效负载活动属性：</span><span class="sxs-lookup"><span data-stu-id="03802-144">Payload activity properties when invoked a task module from a group chat are listed in the following section:</span></span>

|<span data-ttu-id="03802-145">属性名称</span><span class="sxs-lookup"><span data-stu-id="03802-145">Property name</span></span>|<span data-ttu-id="03802-146">用途</span><span class="sxs-lookup"><span data-stu-id="03802-146">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="03802-147">请求的类型。</span><span class="sxs-lookup"><span data-stu-id="03802-147">Type of request.</span></span> <span data-ttu-id="03802-148">它必须是 `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="03802-148">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="03802-149">向服务发出的命令类型。</span><span class="sxs-lookup"><span data-stu-id="03802-149">Type of command that is issued to your service.</span></span> <span data-ttu-id="03802-150">它必须是 `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="03802-150">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="03802-151">发送请求的用户的 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-151">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="03802-152">发送请求的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="03802-152">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="03802-153">发送请求的用户的 Azure Active Directory 对象 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-153">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="03802-154">Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-154">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="03802-155">调用任务模块的源名称。</span><span class="sxs-lookup"><span data-stu-id="03802-155">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="03802-156">获取或设置此邮件作为回复的邮件的 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-156">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="03802-157">包含已调用的命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-157">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="03802-158">触发事件的上下文。</span><span class="sxs-lookup"><span data-stu-id="03802-158">The context that triggered the event.</span></span> <span data-ttu-id="03802-159">它必须是 `compose` 。</span><span class="sxs-lookup"><span data-stu-id="03802-159">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="03802-160">用户的客户端主题，可用于嵌入 Web 视图格式。</span><span class="sxs-lookup"><span data-stu-id="03802-160">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="03802-161">它必须是 `default` ， `contrast` 或 `dark` 。</span><span class="sxs-lookup"><span data-stu-id="03802-161">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-new-post-are-listed-in-the-following-section"></a><span data-ttu-id="03802-162">从频道调用任务模块时， (新帖子) 下一节列出：</span><span class="sxs-lookup"><span data-stu-id="03802-162">Payload activity properties when invoked a task module from a channel (new post) are listed in the following section:</span></span>

|<span data-ttu-id="03802-163">属性名称</span><span class="sxs-lookup"><span data-stu-id="03802-163">Property name</span></span>|<span data-ttu-id="03802-164">用途</span><span class="sxs-lookup"><span data-stu-id="03802-164">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="03802-165">请求的类型。</span><span class="sxs-lookup"><span data-stu-id="03802-165">Type of request.</span></span> <span data-ttu-id="03802-166">它必须是 `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="03802-166">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="03802-167">向服务发出的命令类型。</span><span class="sxs-lookup"><span data-stu-id="03802-167">Type of command that is issued to your service.</span></span> <span data-ttu-id="03802-168">它必须是 `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="03802-168">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="03802-169">发送请求的用户的 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-169">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="03802-170">发送请求的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="03802-170">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="03802-171">发送请求的用户的 Azure Active Directory 对象 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-171">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="03802-172">Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-172">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="03802-173">如果在 (通道中提出请求，通道 ID 将) 。</span><span class="sxs-lookup"><span data-stu-id="03802-173">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="03802-174">如果 (频道中提出请求，团队 ID) 。</span><span class="sxs-lookup"><span data-stu-id="03802-174">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="03802-175">调用任务模块的源名称。</span><span class="sxs-lookup"><span data-stu-id="03802-175">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="03802-176">获取或设置此邮件作为回复的邮件的 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-176">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="03802-177">包含已调用的命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-177">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="03802-178">触发事件的上下文。</span><span class="sxs-lookup"><span data-stu-id="03802-178">The context that triggered the event.</span></span> <span data-ttu-id="03802-179">它必须是 `compose` 。</span><span class="sxs-lookup"><span data-stu-id="03802-179">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="03802-180">用户的客户端主题，可用于嵌入 Web 视图格式。</span><span class="sxs-lookup"><span data-stu-id="03802-180">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="03802-181">它必须是 `default` ， `contrast` 或 `dark` 。</span><span class="sxs-lookup"><span data-stu-id="03802-181">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-reply-to-thread-are-listed-in-the-following-section"></a><span data-ttu-id="03802-182">从频道调用任务模块时， (主题) 将列在以下部分中：</span><span class="sxs-lookup"><span data-stu-id="03802-182">Payload activity properties when invoked a task module from a channel (reply to thread) are listed in the following section:</span></span>

|<span data-ttu-id="03802-183">属性名称</span><span class="sxs-lookup"><span data-stu-id="03802-183">Property name</span></span>|<span data-ttu-id="03802-184">用途</span><span class="sxs-lookup"><span data-stu-id="03802-184">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="03802-185">请求的类型。</span><span class="sxs-lookup"><span data-stu-id="03802-185">Type of request.</span></span> <span data-ttu-id="03802-186">它必须是 `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="03802-186">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="03802-187">向服务发出的命令类型。</span><span class="sxs-lookup"><span data-stu-id="03802-187">Type of command that is issued to your service.</span></span> <span data-ttu-id="03802-188">它必须是 `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="03802-188">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="03802-189">发送请求的用户的 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-189">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="03802-190">发送请求的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="03802-190">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="03802-191">发送请求的用户的 Azure Active Directory 对象 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-191">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="03802-192">Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-192">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="03802-193">如果在 (通道中提出请求，通道 ID 将) 。</span><span class="sxs-lookup"><span data-stu-id="03802-193">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="03802-194">如果 (频道中提出请求，团队 ID) 。</span><span class="sxs-lookup"><span data-stu-id="03802-194">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="03802-195">调用任务模块的源名称。</span><span class="sxs-lookup"><span data-stu-id="03802-195">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="03802-196">获取或设置此邮件作为回复的邮件的 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-196">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="03802-197">包含已调用的命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-197">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="03802-198">触发事件的上下文。</span><span class="sxs-lookup"><span data-stu-id="03802-198">The context that triggered the event.</span></span> <span data-ttu-id="03802-199">它必须是 `compose` 。</span><span class="sxs-lookup"><span data-stu-id="03802-199">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="03802-200">用户的客户端主题，可用于嵌入 Web 视图格式。</span><span class="sxs-lookup"><span data-stu-id="03802-200">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="03802-201">它必须是 `default` ， `contrast` 或 `dark` 。</span><span class="sxs-lookup"><span data-stu-id="03802-201">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-command-box-are-listed-in-the-following-section"></a><span data-ttu-id="03802-202">以下部分列出了从命令框调用任务模块时的有效负载活动属性：</span><span class="sxs-lookup"><span data-stu-id="03802-202">Payload activity properties when invoked a task module from a command box are listed in the following section:</span></span>

|<span data-ttu-id="03802-203">属性名称</span><span class="sxs-lookup"><span data-stu-id="03802-203">Property name</span></span>|<span data-ttu-id="03802-204">用途</span><span class="sxs-lookup"><span data-stu-id="03802-204">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="03802-205">请求的类型。</span><span class="sxs-lookup"><span data-stu-id="03802-205">Type of request.</span></span> <span data-ttu-id="03802-206">它必须是 `invoke` 。</span><span class="sxs-lookup"><span data-stu-id="03802-206">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="03802-207">向服务发出的命令类型。</span><span class="sxs-lookup"><span data-stu-id="03802-207">Type of command that is issued to your service.</span></span> <span data-ttu-id="03802-208">它必须是 `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="03802-208">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="03802-209">发送请求的用户的 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-209">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="03802-210">发送请求的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="03802-210">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="03802-211">发送请求的用户的 Azure Active Directory 对象 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-211">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="03802-212">Azure Active Directory 租户 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-212">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="03802-213">调用任务模块的源名称。</span><span class="sxs-lookup"><span data-stu-id="03802-213">The source name from where task module is invoked.</span></span> |
|`value.commandId` | <span data-ttu-id="03802-214">包含已调用的命令的 ID。</span><span class="sxs-lookup"><span data-stu-id="03802-214">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="03802-215">触发事件的上下文。</span><span class="sxs-lookup"><span data-stu-id="03802-215">The context that triggered the event.</span></span> <span data-ttu-id="03802-216">它必须是 `compose` 。</span><span class="sxs-lookup"><span data-stu-id="03802-216">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="03802-217">用户的客户端主题，可用于嵌入 Web 视图格式。</span><span class="sxs-lookup"><span data-stu-id="03802-217">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="03802-218">它必须是 `default` ， `contrast` 或 `dark` 。</span><span class="sxs-lookup"><span data-stu-id="03802-218">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example-fetchtask-request"></a><span data-ttu-id="03802-219">fetchTask 请求示例</span><span class="sxs-lookup"><span data-stu-id="03802-219">Example fetchTask request</span></span>

# <a name="cnet"></a>[<span data-ttu-id="03802-220">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="03802-220">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="03802-221">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="03802-221">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[<span data-ttu-id="03802-222">JSON</span><span class="sxs-lookup"><span data-stu-id="03802-222">JSON</span></span>](#tab/json)

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

## <a name="initial-invoke-request-from-a-message"></a><span data-ttu-id="03802-223">来自邮件的初始调用请求</span><span class="sxs-lookup"><span data-stu-id="03802-223">Initial invoke request from a message</span></span>

<span data-ttu-id="03802-224">When your bot is invoked from a message rather than the compose area or the command bar， the object in the initial request must contain the details `value` of the message of the message extension is invoked from.</span><span class="sxs-lookup"><span data-stu-id="03802-224">When your bot is invoked from a message rather than the compose area or the command bar, the `value` object in the initial request must contain the details of the message your messaging extension is invoked from.</span></span> <span data-ttu-id="03802-225">有关此对象的示例，请参阅以下部分。</span><span class="sxs-lookup"><span data-stu-id="03802-225">See the following section  for the example of this object .</span></span> <span data-ttu-id="03802-226">和数组是可选的，如果原始邮件中没有任何反应或提及，则它们 `reactions` `mentions` 不存在。</span><span class="sxs-lookup"><span data-stu-id="03802-226">The `reactions` and `mentions` arrays are optional, and they are not present if there are no reactions or mentions in the original message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="03802-227">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="03802-227">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="03802-228">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="03802-228">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[<span data-ttu-id="03802-229">JSON</span><span class="sxs-lookup"><span data-stu-id="03802-229">JSON</span></span>](#tab/json)

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

## <a name="respond-to-the-fetchtask"></a><span data-ttu-id="03802-230">响应 fetchTask</span><span class="sxs-lookup"><span data-stu-id="03802-230">Respond to the fetchTask</span></span>

<span data-ttu-id="03802-231">使用包含具有自适应卡片或 Web URL 的对象或简单的字符串消息的对象响应 `task` `taskInfo` 调用请求。</span><span class="sxs-lookup"><span data-stu-id="03802-231">Respond to the invoke request with a `task` object that contains either a `taskInfo` object with the adaptive card or web URL, or a simple string message.</span></span>

|<span data-ttu-id="03802-232">属性名称</span><span class="sxs-lookup"><span data-stu-id="03802-232">Property name</span></span>|<span data-ttu-id="03802-233">用途</span><span class="sxs-lookup"><span data-stu-id="03802-233">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="03802-234">可以是呈现 `continue` 窗体，也可以 `message` 用于简单的弹出式窗体。</span><span class="sxs-lookup"><span data-stu-id="03802-234">Can be either `continue` to present a form, or `message` for a simple popup.</span></span> |
|`value`| <span data-ttu-id="03802-235">窗体 `taskInfo` 的对象或邮件 `string` 的对象。</span><span class="sxs-lookup"><span data-stu-id="03802-235">Either a `taskInfo` object for a form, or a `string` for a message.</span></span> |

<span data-ttu-id="03802-236">taskInfo 对象的架构为：</span><span class="sxs-lookup"><span data-stu-id="03802-236">The schema for the taskInfo object is:</span></span>

|<span data-ttu-id="03802-237">属性名称</span><span class="sxs-lookup"><span data-stu-id="03802-237">Property name</span></span>|<span data-ttu-id="03802-238">用途</span><span class="sxs-lookup"><span data-stu-id="03802-238">Purpose</span></span>|
|---|---|
|`title`| <span data-ttu-id="03802-239">任务模块的标题。</span><span class="sxs-lookup"><span data-stu-id="03802-239">The title of the task module.</span></span>|
|`height`| <span data-ttu-id="03802-240">它必须是一个整数 (以像素为单位) 或 `small` ， `medium` `large` 。</span><span class="sxs-lookup"><span data-stu-id="03802-240">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`width`| <span data-ttu-id="03802-241">它必须是一个整数 (以像素为单位) 或 `small` ， `medium` `large` 。</span><span class="sxs-lookup"><span data-stu-id="03802-241">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`card`| <span data-ttu-id="03802-242">定义表单的自适应卡片 (使用一个) 。</span><span class="sxs-lookup"><span data-stu-id="03802-242">The adaptive card defining the form (if using one).</span></span>
|`url`| <span data-ttu-id="03802-243">作为嵌入式 Web 视图在任务模块内打开的 URL。</span><span class="sxs-lookup"><span data-stu-id="03802-243">The URL to be opened inside of the task module as an embedded web view.</span></span>|
|`fallbackUrl`| <span data-ttu-id="03802-244">如果客户端不支持任务模块功能，则此 URL 在浏览器选项卡中打开。</span><span class="sxs-lookup"><span data-stu-id="03802-244">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |

### <a name="with-an-adaptive-card"></a><span data-ttu-id="03802-245">使用自适应卡片</span><span class="sxs-lookup"><span data-stu-id="03802-245">With an adaptive card</span></span>

<span data-ttu-id="03802-246">使用自适应卡片时，必须使用包含自适应卡片的对象响应 `task` `value` 对象。</span><span class="sxs-lookup"><span data-stu-id="03802-246">When using an adaptive card, you must respond with a `task` object with the `value` object containing an adaptive card.</span></span>

#### <a name="example-fetchtask-response-with-an-adaptive-card"></a><span data-ttu-id="03802-247">带自适应卡片的 fetchTask 响应示例</span><span class="sxs-lookup"><span data-stu-id="03802-247">Example fetchTask response with an adaptive card</span></span>

# <a name="cnet"></a>[<span data-ttu-id="03802-248">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="03802-248">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="03802-249">此示例除使用 Bot Framework SDK 外，还使用 [AdaptiveCards NuGet](https://www.nuget.org/packages/AdaptiveCards) 程序包。</span><span class="sxs-lookup"><span data-stu-id="03802-249">This sample uses the [AdaptiveCards NuGet package](https://www.nuget.org/packages/AdaptiveCards) in addition to the Bot Framework SDK.</span></span>

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="03802-250">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="03802-250">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="03802-251">JSON</span><span class="sxs-lookup"><span data-stu-id="03802-251">JSON</span></span>](#tab/json)

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

### <a name="with-an-embedded-web-view"></a><span data-ttu-id="03802-252">使用嵌入式 Web 视图</span><span class="sxs-lookup"><span data-stu-id="03802-252">With an embedded web view</span></span>

<span data-ttu-id="03802-253">使用嵌入式 Web 视图时，必须使用包含要加载的 Web 表单 URL 的对象响应 `task` `value` 对象。</span><span class="sxs-lookup"><span data-stu-id="03802-253">When using an embedded web view, you must respond with a `task` object with the `value` object containing the URL to the web form you'd like to load.</span></span> <span data-ttu-id="03802-254">要加载的任何 URL 的域必须包含在应用 `validDomains` 清单的数组中。</span><span class="sxs-lookup"><span data-stu-id="03802-254">The domains of any URL you want to load must be included in the `validDomains` array in your app's manifest.</span></span> <span data-ttu-id="03802-255">有关 [生成嵌入式 Web](~/task-modules-and-cards/what-are-task-modules.md) 视图的完整信息，请参阅任务模块文档。</span><span class="sxs-lookup"><span data-stu-id="03802-255">See the [task module documentation](~/task-modules-and-cards/what-are-task-modules.md) for complete information on building your embedded web view.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="03802-256">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="03802-256">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="03802-257">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="03802-257">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="03802-258">JSON</span><span class="sxs-lookup"><span data-stu-id="03802-258">JSON</span></span>](#tab/json)

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

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="03802-259">请求安装对话机器人</span><span class="sxs-lookup"><span data-stu-id="03802-259">Request to install your conversational bot</span></span>

<span data-ttu-id="03802-260">如果应用包含对话机器人，则先在对话中安装自动程序，然后再加载任务模块。</span><span class="sxs-lookup"><span data-stu-id="03802-260">If the app contains a conversational bot, install the bot in the conversation before loading the task module.</span></span> <span data-ttu-id="03802-261">获取任务模块的其他上下文很有用。</span><span class="sxs-lookup"><span data-stu-id="03802-261">It is useful to get additional context for the task module.</span></span> <span data-ttu-id="03802-262">此方案的典型示例是提取名单以填充人员选取器控件或团队中的频道列表。</span><span class="sxs-lookup"><span data-stu-id="03802-262">Typical example for this scenario is to fetch the roster to populate a people picker control or the list of channels in a team.</span></span>

<span data-ttu-id="03802-263">当消息扩展收到调用时，请检查机器人是否安装在当前上下文中以便于 `composeExtension/fetchTask` 流。</span><span class="sxs-lookup"><span data-stu-id="03802-263">When the messaging extension receives the `composeExtension/fetchTask` invoke, check if the bot is installed in the current context to facilitate the flow.</span></span> <span data-ttu-id="03802-264">例如，使用获取名单呼叫检查流程。</span><span class="sxs-lookup"><span data-stu-id="03802-264">For example, check the flow with a get roster call.</span></span> <span data-ttu-id="03802-265">如果未安装自动程序，请返回自适应卡片，并返回一个请求用户安装自动程序的操作。</span><span class="sxs-lookup"><span data-stu-id="03802-265">If the bot is not installed, return an Adaptive Card with an action that requests the user to install the bot.</span></span> <span data-ttu-id="03802-266">请参阅以下示例中的操作。</span><span class="sxs-lookup"><span data-stu-id="03802-266">See the action in the following example.</span></span> <span data-ttu-id="03802-267">用户必须有权将应用安装在该位置进行检查。</span><span class="sxs-lookup"><span data-stu-id="03802-267">The user must have permission to install the apps in that location for checking.</span></span> <span data-ttu-id="03802-268">如果应用安装不成功，用户将收到一条消息，联系管理员。</span><span class="sxs-lookup"><span data-stu-id="03802-268">If the app installation is unsuccessful, the user receives a message to contact the administrator.</span></span>

#### <a name="example-of-the-response"></a><span data-ttu-id="03802-269">响应示例：</span><span class="sxs-lookup"><span data-stu-id="03802-269">Example of the response:</span></span>

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

<span data-ttu-id="03802-270">安装后，自动程序会收到另一条调用消息，消息包含 `name = composeExtension/submitAction` 和 `value.data.msteams.justInTimeInstall = true` 。</span><span class="sxs-lookup"><span data-stu-id="03802-270">After the installation, the bot receives another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

#### <a name="example-of-the-invoke"></a><span data-ttu-id="03802-271">调用示例：</span><span class="sxs-lookup"><span data-stu-id="03802-271">Example of the invoke:</span></span>

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

<span data-ttu-id="03802-272">对调用的任务响应必须类似于已安装的自动程序。</span><span class="sxs-lookup"><span data-stu-id="03802-272">The task response to the invoke must be similar to that of the installed bot.</span></span>

#### <a name="example-of-just-in-time-installation-of-app-with-adaptive-card"></a><span data-ttu-id="03802-273">使用自适应卡片实时安装应用的示例：</span><span class="sxs-lookup"><span data-stu-id="03802-273">Example of just-in time installation of app with Adaptive card:</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="03802-274">后续步骤</span><span class="sxs-lookup"><span data-stu-id="03802-274">Next steps</span></span>

<span data-ttu-id="03802-275">如果允许用户从任务模块发送回响应，则必须处理提交操作。</span><span class="sxs-lookup"><span data-stu-id="03802-275">If you allow your users to send a response back from the task module, you must handle the submit action.</span></span>

* [<span data-ttu-id="03802-276">使用任务模块创建和响应</span><span class="sxs-lookup"><span data-stu-id="03802-276">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
