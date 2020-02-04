---
title: 将 bot 与选项卡合并
description: 介绍如何将选项卡和 bot 一起使用
keywords: 团队 bot 选项卡开发
ms.date: 03/15/2018
ms.openlocfilehash: 59ae8bc01f82c70dd7ea6869cb870e26acae1293
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673290"
---
# <a name="combine-bots-with-tabs"></a><span data-ttu-id="f6cf9-104">将 bot 与选项卡合并</span><span class="sxs-lookup"><span data-stu-id="f6cf9-104">Combine bots with tabs</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="f6cf9-105">Bot 和选项卡协同工作，并且通常组合到一个后端服务中。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-105">Bots and tabs work well together, and are often combined into a single back-end service.</span></span> <span data-ttu-id="f6cf9-106">本节介绍了将选项卡和 bot 一起使用的最佳实践和常见模式。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-106">This section describes best practices and common patterns for using tabs and bots together.</span></span>

## <a name="associating-user-identities-across-bot-and-tab"></a><span data-ttu-id="f6cf9-107">在 bot 和选项卡之间关联用户标识</span><span class="sxs-lookup"><span data-stu-id="f6cf9-107">Associating user identities across bot and tab</span></span>

<span data-ttu-id="f6cf9-108">例如：假设您的选项卡应用程序使用专用 ID 系统来保护其内容。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-108">For example: Suppose your tab application uses a proprietary ID system to secure its content.</span></span> <span data-ttu-id="f6cf9-109">假设您还具有可与用户进行交互的 bot。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-109">Suppose you also have a bot that can interact with the user.</span></span> <span data-ttu-id="f6cf9-110">通常情况下，您需要在特定于查看用户的选项卡中显示内容。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-110">Typically, you’ll want to show content in the tab that is specific to the viewing user.</span></span> <span data-ttu-id="f6cf9-111">困难在于，系统中的用户 ID 可能与 Microsoft 团队用户 ID 不同。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-111">The challenge is that the user ID in your system is likely different from the Microsoft Teams user ID.</span></span> <span data-ttu-id="f6cf9-112">那么，如何将这两种标识关联起来呢？</span><span class="sxs-lookup"><span data-stu-id="f6cf9-112">So how do you associate these two identities?</span></span>
<span data-ttu-id="f6cf9-113">通常情况下，建议的方法是使用与用于为选项卡内容提供身份验证的相同标识系统在 bot 中登录用户。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-113">In general, the recommended approach is to sign the user in with the bot using the same identity system used to provide authentication for the tab content.</span></span> <span data-ttu-id="f6cf9-114">您可以通过登录操作实现此目标，该操作通常通过 OAuth 流登录用户。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-114">You can implement this via the sign-in action, which typically logs in the user via an OAuth flow.</span></span>

<span data-ttu-id="f6cf9-115">如果您的标识提供程序实现 OAuth 2.0 协议，则此流最适用。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-115">This flow works best if your identity provider implements the OAuth 2.0 protocol.</span></span> <span data-ttu-id="f6cf9-116">然后，可以将团队用户 ID 与用户的凭据关联到您自己的标识服务。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-116">You can then associate the Teams user ID with the user’s credentials from your own identity service.</span></span>

   ![关联标识](~/assets/images/bots/associating_contexts.png)

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a><span data-ttu-id="f6cf9-118">构建指向你的 bot 发来的邮件中的选项卡的深层链接</span><span class="sxs-lookup"><span data-stu-id="f6cf9-118">Constructing deep links to tabs in messages from your bot</span></span>

<span data-ttu-id="f6cf9-119">您可能需要使用选项卡来显示超出卡片内所能包含的内容的内容，或提供使用 tab 画布填写复杂表单填充任务的方法。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-119">You may want to use tabs to show more content than can fit inside of a card, or provide a way to complete complex form-filling tasks using the tab canvas.</span></span> <span data-ttu-id="f6cf9-120">例如，当用户在你的 bot 上单击卡片时，请考虑将该用户导航到该选项卡。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-120">For example, consider navigating the user to the tab when he or she clicks on the card from your bot.</span></span> <span data-ttu-id="f6cf9-121">为此，需要对你的 bot 的邮件进行编码，以包含[深层链接](~/concepts/build-and-test/deep-links.md)URL （通过标记）或 openUrl 操作的目标。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-121">For this to happen, you’ll need to encode your bot’s message to include a [deep link](~/concepts/build-and-test/deep-links.md) URL, either via markup or as the target of the openUrl action.</span></span>

<span data-ttu-id="f6cf9-122">Deep links 依赖于 entityId，这是一个不透明的值，映射到系统中的唯一实体。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-122">Deep links rely on an entityId, which is an opaque value that maps to a unique entity in your system.</span></span> <span data-ttu-id="f6cf9-123">创建选项卡后，您最好在后端存储一些简单的状态（例如标志），指示该选项卡已在通道中创建。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-123">When the tab is created, you ideally store some simple state (e.g. flag) on your backend indicating the tab has been created in the channel.</span></span> <span data-ttu-id="f6cf9-124">当你的 bot 构造一条消息时，它可以将与该选项卡关联的 entityId 作为目标。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-124">When your bot constructs a message, it can target the entityId associated with that tab.</span></span>

<span data-ttu-id="f6cf9-125">**注意：** 在个人聊天中，由于选项卡是 "静态" 的，并且随应用程序一起安装，因此您可以始终假定其存在，从而相应地构建深层链接。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-125">**Note:** in personal chats, because tabs are “static” and installed with the app, you can always assume their existence and thus construct deep links accordingly.</span></span>

## <a name="sending-notifications-for-tab-updates"></a><span data-ttu-id="f6cf9-126">发送选项卡更新通知</span><span class="sxs-lookup"><span data-stu-id="f6cf9-126">Sending notifications for tab updates</span></span>

<span data-ttu-id="f6cf9-127">通常，每当在选项卡中发生更新或用户操作时，您都需要通知最终用户。示例方案将任务或票证分配给同事的团队成员，然后通知团队成员。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-127">Often you’ll want to notify the end user whenever an update or a user action occurs in a tab. An example scenario is assigning a task or ticket to a fellow team member and then notifying that team member.</span></span>

<span data-ttu-id="f6cf9-128">有两种方法可以实现此方案：</span><span class="sxs-lookup"><span data-stu-id="f6cf9-128">There are two ways of achieving this scenario:</span></span>

1. <span data-ttu-id="f6cf9-129">如果要通知整个频道，你的 bot 可以将邮件异步发布到频道。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-129">If you wish to notify an entire channel your bot can asynchronously post a message to the channel.</span></span> <span data-ttu-id="f6cf9-130">如果 bot 不是通过选项卡创建的，则自动创建的选项卡对话将无法主动创建。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-130">There is no way for a bot to proactively create the tab conversation if it wasn't created with the tab.</span></span>

2. <span data-ttu-id="f6cf9-131">如果你希望仅通知收件人或相关人员参与操作，你的 bot 可以向用户发送个人聊天消息。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-131">If you wish to only notify the recipient or interested parties involved with the action, your bot can send a personal chat message to the user.</span></span> <span data-ttu-id="f6cf9-132">您应首先查看您的 bot 和用户之间是否存在个人对话。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-132">You should first check to see if a personal conversation between your bot and the user exists.</span></span> <span data-ttu-id="f6cf9-133">如果不是，则可以`CreateConversation`调用来启动个人聊天。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-133">If not, you can call `CreateConversation` to initiate the personal chat.</span></span>

<span data-ttu-id="f6cf9-134">在这两种情况下，可合理地使用事件通知，并且决不会对用户发送不必要的更新。</span><span class="sxs-lookup"><span data-stu-id="f6cf9-134">In both cases, use event notifications wisely and never spam the user with unnecessary updates.</span></span>
