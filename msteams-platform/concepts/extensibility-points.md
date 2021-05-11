---
title: Teams 应用的入口点
author: heath-hamilton
description: 介绍用户可以在 Teams 中发现和使用应用的地方。
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: f2bdb35c76bdb7487e66a0e6b9ad01c6da9e04f8
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058318"
---
# <a name="entry-points-for-teams-apps"></a><span data-ttu-id="78e0b-103">Teams 应用的入口点</span><span class="sxs-lookup"><span data-stu-id="78e0b-103">Entry points for Teams apps</span></span>

<span data-ttu-id="78e0b-104">the Teams platform provides a flexible set of entry points， such as team， channel， and chat where people can discover and use your app.</span><span class="sxs-lookup"><span data-stu-id="78e0b-104">The Teams platform provides a flexible set of entry points, such as team, channel, and chat where people can discover and use your app.</span></span> <span data-ttu-id="78e0b-105">应用程序非常简单，只需在选项卡或多维应用中嵌入现有 Web 内容，用户跨多个上下文进行交互。</span><span class="sxs-lookup"><span data-stu-id="78e0b-105">Your app can be as simple as embedding existing web content in a tab or a multi-faceted app that users interact with across several contexts.</span></span>
<span data-ttu-id="78e0b-106">成功应用是本机应用的Teams，因此请谨慎选择应用的入口点。</span><span class="sxs-lookup"><span data-stu-id="78e0b-106">The most successful apps are native to Teams, so choose your app's entry points carefully.</span></span>

## <a name="shared-app-experiences"></a><span data-ttu-id="78e0b-107">共享的应用体验</span><span class="sxs-lookup"><span data-stu-id="78e0b-107">Shared app experiences</span></span>

<span data-ttu-id="78e0b-108">团队、频道和聊天是协作空间。</span><span class="sxs-lookup"><span data-stu-id="78e0b-108">Team, channel, and chat are collaboration spaces.</span></span> <span data-ttu-id="78e0b-109">这些上下文中的应用程序可供该空间中的每个人使用。</span><span class="sxs-lookup"><span data-stu-id="78e0b-109">Apps in these contexts are available to everyone in that space.</span></span> <span data-ttu-id="78e0b-110">协作空间通常侧重于其他工作流或解锁新的社交交互。</span><span class="sxs-lookup"><span data-stu-id="78e0b-110">Collaboration spaces typically focus on additional workflows or unlocking new social interactions.</span></span>

<span data-ttu-id="78e0b-111">下表显示了如何在Teams上下文中使用应用程序功能：</span><span class="sxs-lookup"><span data-stu-id="78e0b-111">The following list shows how Teams app capabilities are commonly used in collaborative contexts:</span></span>

* <span data-ttu-id="78e0b-112">[**选项卡**](~/tabs/what-are-tabs.md)为团队、频道或群组聊天配置全屏嵌入的 Web 体验。</span><span class="sxs-lookup"><span data-stu-id="78e0b-112">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience configured for the team, channel, or group chat.</span></span> <span data-ttu-id="78e0b-113">所有成员与基于 Web 的相同内容进行交互，因此无状态单页应用体验很典型。</span><span class="sxs-lookup"><span data-stu-id="78e0b-113">All members interact with the same web-based content, so a stateless single-page app experience is typical.</span></span>

* <span data-ttu-id="78e0b-114">[**邮件扩展**](~/messaging-extensions/what-are-messaging-extensions.md)是一种快捷方式，适用于在对话中插入外部内容或在不离开 Teams 的情况下对邮件采取措施。</span><span class="sxs-lookup"><span data-stu-id="78e0b-114">[**Messaging extensions**](~/messaging-extensions/what-are-messaging-extensions.md) are shortcuts for inserting external content into a conversation or taking action on messages without leaving Teams.</span></span> <span data-ttu-id="78e0b-115">[从公用 URL](~/messaging-extensions/how-to/link-unfurling.md) 共享内容时，链接展开可提供丰富的内容。</span><span class="sxs-lookup"><span data-stu-id="78e0b-115">[Link unfurling](~/messaging-extensions/how-to/link-unfurling.md) provides rich content when sharing content from a common URL.</span></span>

* <span data-ttu-id="78e0b-116">[**机器人**](~/bots/what-are-bots.md) 通过聊天和响应事件（例如添加新成员或重命名频道）与对话成员进行交互。</span><span class="sxs-lookup"><span data-stu-id="78e0b-116">[**Bots**](~/bots/what-are-bots.md) interact with members of the conversation through chat and responding to events, such as adding a new member or renaming a channel.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="78e0b-117">与自动程序在这些上下文中的对话对团队、频道或组的所有成员都可见，因此自动程序对话必须与所有人相关。</span><span class="sxs-lookup"><span data-stu-id="78e0b-117">Conversations with a bot in these contexts are visible to all members of the team, channel, or group, so bot conversations must be relevant to everyone.</span></span>

* <span data-ttu-id="78e0b-118">[**Web 部件和连接器**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)外部服务将消息发布到对话中，用户可将邮件发送到服务。</span><span class="sxs-lookup"><span data-stu-id="78e0b-118">[**Webhooks and connectors**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) allow an external service to post messages into a conversation and users to send messages to a service.</span></span>

* <span data-ttu-id="78e0b-119">[**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview)团队、频道和群组聊天的数据，帮助自动执行和管理 Teams 流程。</span><span class="sxs-lookup"><span data-stu-id="78e0b-119">[**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview) for getting data about teams, channels, and group chats to help automate and manage Teams processes.</span></span>

## <a name="personal-app-experiences"></a><span data-ttu-id="78e0b-120">个人应用体验</span><span class="sxs-lookup"><span data-stu-id="78e0b-120">Personal app experiences</span></span>

<span data-ttu-id="78e0b-121">[个人应用](../concepts/design/personal-apps.md) 专注于与单个用户的交互。</span><span class="sxs-lookup"><span data-stu-id="78e0b-121">[Personal apps](../concepts/design/personal-apps.md) focus on interactions with a single user.</span></span> <span data-ttu-id="78e0b-122">此上下文中的体验是每位用户所特有的。</span><span class="sxs-lookup"><span data-stu-id="78e0b-122">The experience in this context is unique to each user.</span></span>

<span data-ttu-id="78e0b-123">以下列表显示了Teams个人上下文中如何使用这些功能：</span><span class="sxs-lookup"><span data-stu-id="78e0b-123">The following list shows how Teams capabilities are commonly used in personal contexts:</span></span>

* <span data-ttu-id="78e0b-124">[**自动**](~/bots/what-are-bots.md)用户进行一对一对话。</span><span class="sxs-lookup"><span data-stu-id="78e0b-124">[**Bots**](~/bots/what-are-bots.md) have one-on-one conversations with a user.</span></span> <span data-ttu-id="78e0b-125">需要多次对话或提供仅与特定用户相关的通知的自动程序最适合个人应用。</span><span class="sxs-lookup"><span data-stu-id="78e0b-125">Bots that require multi-turn conversations or provide notifications relevant only to a specific user are best suited in personal apps.</span></span>

* <span data-ttu-id="78e0b-126">[**选项卡**](~/tabs/what-are-tabs.md) 提供对查看它的用户有意义的全屏嵌入式 Web 体验。</span><span class="sxs-lookup"><span data-stu-id="78e0b-126">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience that is meaningful to the user looking at it.</span></span>

## <a name="see-also"></a><span data-ttu-id="78e0b-127">另请参阅</span><span class="sxs-lookup"><span data-stu-id="78e0b-127">See also</span></span>

- [<span data-ttu-id="78e0b-128">Teams应用设计指南</span><span class="sxs-lookup"><span data-stu-id="78e0b-128">Teams app design guidelines</span></span>](../concepts/design/design-teams-app-overview.md)

## <a name="next-step"></a><span data-ttu-id="78e0b-129">后续步骤</span><span class="sxs-lookup"><span data-stu-id="78e0b-129">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="78e0b-130">了解用例</span><span class="sxs-lookup"><span data-stu-id="78e0b-130">Understand use cases</span></span>](../concepts/design/understand-use-cases.md)
