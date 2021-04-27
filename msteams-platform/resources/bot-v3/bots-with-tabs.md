---
title: 将机器人与选项卡组合在一起
description: 介绍如何将选项卡和自动程序一同使用
keywords: teams 机器人选项卡开发
ms.topic: conceptual
localization_priority: Normal
ms.date: 03/15/2018
ms.openlocfilehash: b33d0bfcae4b522fc9e0c7d17b3d082979a62647
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020623"
---
# <a name="combine-bots-with-tabs"></a><span data-ttu-id="3e8d9-104">将机器人与选项卡组合在一起</span><span class="sxs-lookup"><span data-stu-id="3e8d9-104">Combine bots with tabs</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="3e8d9-105">机器人和选项卡可以很好地协同工作，并且通常组合到单个后端服务中。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-105">Bots and tabs work well together, and are often combined into a single back-end service.</span></span> <span data-ttu-id="3e8d9-106">本节介绍将选项卡和聊天机器人一同使用的最佳方案及通用模式。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-106">This section describes best practices and common patterns for using tabs and bots together.</span></span>

## <a name="associating-user-identities-across-bot-and-tab"></a><span data-ttu-id="3e8d9-107">跨自动程序与选项卡关联用户标识</span><span class="sxs-lookup"><span data-stu-id="3e8d9-107">Associating user identities across bot and tab</span></span>

<span data-ttu-id="3e8d9-108">例如：假设您的选项卡应用程序使用专有 ID 系统保护其内容。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-108">For example: Suppose your tab application uses a proprietary ID system to secure its content.</span></span> <span data-ttu-id="3e8d9-109">假设您还有一个可以与用户交互的机器人。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-109">Suppose you also have a bot that can interact with the user.</span></span> <span data-ttu-id="3e8d9-110">通常，你需要在选项卡中显示特定于查看用户的内容。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-110">Typically, you’ll want to show content in the tab that is specific to the viewing user.</span></span> <span data-ttu-id="3e8d9-111">挑战在于，系统中用户 ID 可能不同于 Microsoft Teams 用户 ID。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-111">The challenge is that the user ID in your system is likely different from the Microsoft Teams user ID.</span></span> <span data-ttu-id="3e8d9-112">那么，如何关联这两个标识？</span><span class="sxs-lookup"><span data-stu-id="3e8d9-112">So how do you associate these two identities?</span></span>
<span data-ttu-id="3e8d9-113">通常，建议的方法是使用用于为选项卡内容提供身份验证的相同身份系统，使用自动程序让用户登录。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-113">In general, the recommended approach is to sign the user in with the bot using the same identity system used to provide authentication for the tab content.</span></span> <span data-ttu-id="3e8d9-114">可以通过登录操作实现此操作，此操作通常通过 OAuth 流在用户中登录。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-114">You can implement this via the sign-in action, which typically logs in the user via an OAuth flow.</span></span>

<span data-ttu-id="3e8d9-115">如果标识提供程序实现 OAuth 2.0 协议，则此流最有效。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-115">This flow works best if your identity provider implements the OAuth 2.0 protocol.</span></span> <span data-ttu-id="3e8d9-116">然后，可以将 Teams 用户 ID 与你自己的标识服务中的用户凭据关联。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-116">You can then associate the Teams user ID with the user’s credentials from your own identity service.</span></span>

   ![关联标识](~/assets/images/bots/associating_contexts.png)

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a><span data-ttu-id="3e8d9-118">从自动程序构造消息中选项卡的深层链接</span><span class="sxs-lookup"><span data-stu-id="3e8d9-118">Constructing deep links to tabs in messages from your bot</span></span>

<span data-ttu-id="3e8d9-119">您可能需要使用选项卡来显示比卡片内部容纳更多的内容，或者提供一种使用选项卡画布完成复杂表单填写任务的方法。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-119">You may want to use tabs to show more content than can fit inside of a card, or provide a way to complete complex form-filling tasks using the tab canvas.</span></span> <span data-ttu-id="3e8d9-120">例如，当用户从自动程序单击卡片时，请考虑将用户导航到选项卡。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-120">For example, consider navigating the user to the tab when he or she clicks on the card from your bot.</span></span> <span data-ttu-id="3e8d9-121">为此，你需要对自动程序的消息进行编码，以包括深层链接 [URL（](~/concepts/build-and-test/deep-links.md) 通过标记或作为 openUrl 操作的目标）。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-121">For this to happen, you’ll need to encode your bot’s message to include a [deep link](~/concepts/build-and-test/deep-links.md) URL, either via markup or as the target of the openUrl action.</span></span>

<span data-ttu-id="3e8d9-122">深度链接依赖于 entityId，它是映射到系统中唯一实体的不透明值。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-122">Deep links rely on an entityId, which is an opaque value that maps to a unique entity in your system.</span></span> <span data-ttu-id="3e8d9-123">创建选项卡时，最好存储一些简单的状态 (例如，) 标记标记指示该选项卡已在通道中创建。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-123">When the tab is created, you ideally store some simple state (e.g. flag) on your backend indicating the tab has been created in the channel.</span></span> <span data-ttu-id="3e8d9-124">当机器人构造消息时，它可以面向与该选项卡关联的 entityId。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-124">When your bot constructs a message, it can target the entityId associated with that tab.</span></span>

<span data-ttu-id="3e8d9-125">**注意：** 在个人聊天中，由于选项卡是"静态"的，并且随应用一起安装，因此你始终可以假定它们存在，从而相应地构造深层链接。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-125">**Note:** in personal chats, because tabs are “static” and installed with the app, you can always assume their existence and thus construct deep links accordingly.</span></span>

## <a name="sending-notifications-for-tab-updates"></a><span data-ttu-id="3e8d9-126">发送选项卡更新通知</span><span class="sxs-lookup"><span data-stu-id="3e8d9-126">Sending notifications for tab updates</span></span>

<span data-ttu-id="3e8d9-127">通常，每当选项卡中发生更新或用户操作时，你会希望通知最终用户。示例方案是向同事团队成员分配任务或票证，然后通知该团队成员。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-127">Often you’ll want to notify the end user whenever an update or a user action occurs in a tab. An example scenario is assigning a task or ticket to a fellow team member and then notifying that team member.</span></span>

<span data-ttu-id="3e8d9-128">有两种方法可以实现此方案：</span><span class="sxs-lookup"><span data-stu-id="3e8d9-128">There are two ways of achieving this scenario:</span></span>

1. <span data-ttu-id="3e8d9-129">如果你想要通知整个频道，机器人可以异步向频道发布消息。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-129">If you wish to notify an entire channel your bot can asynchronously post a message to the channel.</span></span> <span data-ttu-id="3e8d9-130">如果没有使用选项卡创建选项卡对话，则自动程序无法主动创建该对话。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-130">There is no way for a bot to proactively create the tab conversation if it wasn't created with the tab.</span></span>

2. <span data-ttu-id="3e8d9-131">如果你希望仅通知收件人或参与该操作的各方，则机器人可以向用户发送个人聊天消息。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-131">If you wish to only notify the recipient or interested parties involved with the action, your bot can send a personal chat message to the user.</span></span> <span data-ttu-id="3e8d9-132">应首先检查机器人和用户之间的个人对话是否存在。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-132">You should first check to see if a personal conversation between your bot and the user exists.</span></span> <span data-ttu-id="3e8d9-133">如果没有，可以调用 `CreateConversation` 以启动个人聊天。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-133">If not, you can call `CreateConversation` to initiate the personal chat.</span></span>

<span data-ttu-id="3e8d9-134">在这两种情况下，请明智使用事件通知，并且不要向用户发送不必要的更新。</span><span class="sxs-lookup"><span data-stu-id="3e8d9-134">In both cases, use event notifications wisely and never spam the user with unnecessary updates.</span></span>
