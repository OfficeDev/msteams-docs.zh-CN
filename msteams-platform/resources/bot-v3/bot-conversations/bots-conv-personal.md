---
title: 具有 bot 的1开1对话
description: 介绍与 Microsoft 团队中的 bot 进行1开/1 开对话的端到端方案
keywords: 团队方案 1on1 1to1 对话机器人
ms.date: 05/20/2019
ms.openlocfilehash: e23bb98160125d7fdbb4521467e2f522d6b6ce40
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673489"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a><span data-ttu-id="a19a4-104">与 Microsoft 团队 bot 进行一次个人（一对一）对话</span><span class="sxs-lookup"><span data-stu-id="a19a4-104">Have a personal (one-on-one) conversation with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="a19a4-105">Microsoft 团队允许用户与在[Microsoft Bot 框架](/azure/bot-service/?view=azure-bot-service-3.0)上构建的 bot 进行直接对话。</span><span class="sxs-lookup"><span data-stu-id="a19a4-105">Microsoft Teams allows users to engage in direct conversations with bots built on the [Microsoft Bot Framework](/azure/bot-service/?view=azure-bot-service-3.0).</span></span> <span data-ttu-id="a19a4-106">用户可以在发现应用程序库中找到 bot，并将其添加到他们的团队体验个人对话中。</span><span class="sxs-lookup"><span data-stu-id="a19a4-106">Users can find bots in the Discover Apps gallery and add them to their Teams experience for personal conversations.</span></span> <span data-ttu-id="a19a4-107">具有相应权限的团队所有者和用户也可以添加作为团队成员的 bot （请参阅[在团队频道中进行交互](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)），这不仅会使它们在团队的频道中可用，还适用于所有用户的个人聊天。</span><span class="sxs-lookup"><span data-stu-id="a19a4-107">Team owners and users with the appropriate permissions can also add bots as team members (see [Interact in a team channel](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)), which not only makes them available in that team's channels, but for personal chat for all of those users as well.</span></span>

<span data-ttu-id="a19a4-108">个人聊天与频道中的聊天不同，因为用户无需 @mention 机器人。</span><span class="sxs-lookup"><span data-stu-id="a19a4-108">Personal chat differs from chat in channels in that the user does not need to @mention the bot.</span></span> <span data-ttu-id="a19a4-109">如果在多个上下文（个人、groupChat 或通道）中使用 bot，则需要检测 bot 是否在组聊天或频道中，并以略有不同的方式处理邮件。</span><span class="sxs-lookup"><span data-stu-id="a19a4-109">If a bot is used in multiple contexts (personal, groupChat or channel) you will need to detect if the bot is in a group chat or channel, and process messages a little differently.</span></span> <span data-ttu-id="a19a4-110">有关更多详细信息，请参阅[在团队频道或组聊天中进行交互](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。</span><span class="sxs-lookup"><span data-stu-id="a19a4-110">See [Interact in a team channel or group chat](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more details.</span></span>

## <a name="designing-a-great-personal-bot"></a><span data-ttu-id="a19a4-111">设计极大的个人 bot</span><span class="sxs-lookup"><span data-stu-id="a19a4-111">Designing a great personal bot</span></span>

<span data-ttu-id="a19a4-112">Microsoft 团队中的一个很棒的 bot 可帮助用户获取他们所需的信息，所有这些都在团队体验的上下文中。</span><span class="sxs-lookup"><span data-stu-id="a19a4-112">A great bot in Microsoft Teams helps users get the information they need, all within the context of the Teams experience.</span></span> <span data-ttu-id="a19a4-113">与 bot 的个人对话是 bot 与其用户之间的专用交换;它们是在个人上下文中提供有关该用户的特定信息和相关信息的好方法。</span><span class="sxs-lookup"><span data-stu-id="a19a4-113">Personal conversations with a bot are private exchanges between a bot and its user; they're a great way to provide information specific and relevant to that user in the personal context.</span></span> <span data-ttu-id="a19a4-114">个人聊天中的 bot 实际上是服务和个人之间的一个对话框，其中群中的 bot 可将所有内容广播给一组用户。</span><span class="sxs-lookup"><span data-stu-id="a19a4-114">A bot in personal chat is really a dialog between your service and the individual, where a bot in a group chat or channel broadcasts everything to a group of people.</span></span>

<span data-ttu-id="a19a4-115">根据您想要创建的体验，自动程序可能需要在多个范围内工作-个人、groupChat 和/或团队。</span><span class="sxs-lookup"><span data-stu-id="a19a4-115">Depending on the experience you want to create, the bot might need to work in multiple scopes - personal, groupChat and/or team.</span></span> <span data-ttu-id="a19a4-116">支持多个作用域的工作最少。</span><span class="sxs-lookup"><span data-stu-id="a19a4-116">The work to support more than one scope is minimal.</span></span> <span data-ttu-id="a19a4-117">由于你的 bot 在所有作用域中都无法正常运行，团队没有任何预期，但应确保你的 bot 有意义，并在你选择支持的任何范围内提供用户值。</span><span class="sxs-lookup"><span data-stu-id="a19a4-117">There is no expectation in Teams that your bot function in all scopes, but you should ensure that your bot makes sense and provides user value in whatever scope(s) you choose to support.</span></span>

## <a name="best-practice-welcome-messages-in-personal-conversations"></a><span data-ttu-id="a19a4-118">最佳实践：个人对话中的欢迎邮件</span><span class="sxs-lookup"><span data-stu-id="a19a4-118">Best practice: Welcome messages in personal conversations</span></span>

<span data-ttu-id="a19a4-119">你的 bot 应在首次（且仅在第一次）用户使用你的 bot 启动个人聊天时主动向个人聊天[发送](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)欢迎消息。</span><span class="sxs-lookup"><span data-stu-id="a19a4-119">Your bot should [proactively send](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) a welcome message to a personal chat the first time (and only the first time) a user initiates a personal chat with your bot.</span></span> <span data-ttu-id="a19a4-120">（此推荐不适用于频道中的首次联系人。）</span><span class="sxs-lookup"><span data-stu-id="a19a4-120">(This recommendation does not apply to first-time contacts in a channel.)</span></span>
