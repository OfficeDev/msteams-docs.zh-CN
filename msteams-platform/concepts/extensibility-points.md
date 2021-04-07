---
title: Teams 应用的入口点
author: heath-hamilton
description: 介绍用户可以在 Teams 中发现和使用应用的地方。
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 72ce2620160f854bbe458821db01e91d2d9f62cd
ms.sourcegitcommit: 098d38dd947e87e69d289b99e807bea2d95c42f9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2020
ms.locfileid: "49713625"
---
# <a name="entry-points-for-teams-apps"></a><span data-ttu-id="d9852-103">Teams 应用的入口点</span><span class="sxs-lookup"><span data-stu-id="d9852-103">Entry points for Teams apps</span></span>

<span data-ttu-id="d9852-104">Teams 平台提供了一组灵活的入口点，用户可以在其中发现和使用你的应用。</span><span class="sxs-lookup"><span data-stu-id="d9852-104">The Teams platform provides a flexible set of entry points where people can discover and use your app.</span></span> <span data-ttu-id="d9852-105">应用程序非常简单，只需在选项卡或多维应用中嵌入现有 Web 内容，用户跨多个上下文进行交互。</span><span class="sxs-lookup"><span data-stu-id="d9852-105">Your app can be as simple as embedding existing web content in a tab or a multi-faceted app that users interact with across several contexts.</span></span>

<span data-ttu-id="d9852-106">最成功的应用将本机为 Teams，因此请仔细规划应用的入口点。</span><span class="sxs-lookup"><span data-stu-id="d9852-106">The most successful apps feel native to Teams, so it's important to carefully plan your app's entry points.</span></span>

## <a name="teams-channels-and-chats"></a><span data-ttu-id="d9852-107">团队、频道和聊天</span><span class="sxs-lookup"><span data-stu-id="d9852-107">Teams, channels, and chats</span></span>

<span data-ttu-id="d9852-108">团队、频道和聊天是协作空间。</span><span class="sxs-lookup"><span data-stu-id="d9852-108">Teams, channels, and chats are collaboration spaces.</span></span> <span data-ttu-id="d9852-109">这些上下文中的应用可供该空间的每个人使用，通常侧重于其他工作流或解锁新的社交交互。</span><span class="sxs-lookup"><span data-stu-id="d9852-109">Apps in these contexts are available to everyone in that space and typically focus on additional workflows or unlocking new social interactions.</span></span>

<span data-ttu-id="d9852-110">下面说明在协作上下文中通常使用 Teams 应用功能的方式：</span><span class="sxs-lookup"><span data-stu-id="d9852-110">Here's how Teams app capabilities are commonly used in collaborative contexts:</span></span>

* <span data-ttu-id="d9852-111">[**选项卡**](~/tabs/what-are-tabs.md)为团队、频道或群组聊天配置全屏嵌入的 Web 体验。</span><span class="sxs-lookup"><span data-stu-id="d9852-111">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience configured for the team, channel, or group chat.</span></span> <span data-ttu-id="d9852-112">所有成员交互处理基于 Web 的相同内容，因此普通单页应用体验。</span><span class="sxs-lookup"><span data-stu-id="d9852-112">All members interact with the same web-based content, so a stateless single page app experience is typical.</span></span>

* <span data-ttu-id="d9852-113">[**邮件扩展**](~/messaging-extensions/what-are-messaging-extensions.md)是一种快捷方式，适用于在对话中插入外部内容或在不离开 Teams 的情况下对邮件采取措施。</span><span class="sxs-lookup"><span data-stu-id="d9852-113">[**Messaging extensions**](~/messaging-extensions/what-are-messaging-extensions.md) are shortcuts for inserting external content into a conversation or taking action on messages without leaving Teams.</span></span> <span data-ttu-id="d9852-114">从公共 URL 共享内容时，取消链接将提供丰富的内容。</span><span class="sxs-lookup"><span data-stu-id="d9852-114">Link unfurling provides rich content when sharing content from a common URL.</span></span>

* <span data-ttu-id="d9852-115">[**自动**](~/bots/what-are-bots.md)通过聊天和响应事件（例如添加新成员或重命名频道）与对话成员交互。</span><span class="sxs-lookup"><span data-stu-id="d9852-115">[**Bots**](~/bots/what-are-bots.md) interact with members of the conversation through chat and responding to events (like adding a new member or renaming a channel).</span></span> <span data-ttu-id="d9852-116">团队、频道或组的所有成员都可以看到这些上下文中与机器人的对话，因此自动对话应该与所有人相关。</span><span class="sxs-lookup"><span data-stu-id="d9852-116">Conversations with a bot in these contexts are visible to all members of the team, channel, or group, so bot conversations should be relevant to everyone.</span></span>

* <span data-ttu-id="d9852-117">[**Web 部件和连接器**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)外部服务将消息发布到对话中，用户可将邮件发送到服务。</span><span class="sxs-lookup"><span data-stu-id="d9852-117">[**Webhooks and connectors**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) allow an external service to post messages into a conversation and users to send messages to a service.</span></span>

* <span data-ttu-id="d9852-118">[**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview)团队、频道和群组聊天的数据，帮助自动执行和管理 Teams 流程。</span><span class="sxs-lookup"><span data-stu-id="d9852-118">[**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview) for getting data about teams, channels, and group chats to help automate and manage Teams processes.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="d9852-119">个人应用</span><span class="sxs-lookup"><span data-stu-id="d9852-119">Personal apps</span></span>

<span data-ttu-id="d9852-120">[个人应用](~/concepts/design/personal-apps.md) 专注于与单个用户的交互。</span><span class="sxs-lookup"><span data-stu-id="d9852-120">[Personal apps](~/concepts/design/personal-apps.md) focus on interactions with a single user.</span></span> <span data-ttu-id="d9852-121">此上下文中的体验是每位用户所特有的。</span><span class="sxs-lookup"><span data-stu-id="d9852-121">The experience in this context is unique to each user.</span></span>

<span data-ttu-id="d9852-122">下面说明在个人上下文中通常使用 Teams 功能的方法：</span><span class="sxs-lookup"><span data-stu-id="d9852-122">Here's how Teams capabilities are commonly used in personal contexts:</span></span>

* <span data-ttu-id="d9852-123">[**自动**](~/bots/what-are-bots.md)用户进行一对一对话。</span><span class="sxs-lookup"><span data-stu-id="d9852-123">[**Bots**](~/bots/what-are-bots.md) have one-on-one conversations with a user.</span></span> <span data-ttu-id="d9852-124">需要多次对话或提供仅与特定用户相关的通知的自动程序最适合个人应用。</span><span class="sxs-lookup"><span data-stu-id="d9852-124">Bots that require multi-turn conversations or provide notifications relevant only to a specific user are best suited in personal apps.</span></span>

* <span data-ttu-id="d9852-125">[**选项卡**](~/tabs/what-are-tabs.md)可提供全屏嵌入的 Web 体验，对查看该体验的用户有意义。</span><span class="sxs-lookup"><span data-stu-id="d9852-125">[**Tabs**](~/tabs/what-are-tabs.md) provide a full-screen embedded web experience that's meaningful to the user looking at it.</span></span>

## <a name="examples"></a><span data-ttu-id="d9852-126">示例</span><span class="sxs-lookup"><span data-stu-id="d9852-126">Examples</span></span>

<span data-ttu-id="d9852-127">Teams 应用设计指南提供详细的视觉效果，展示用户在何处可以找到和使用 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="d9852-127">The Teams app design guidelines provide detailed visuals showing you where people can find and use Teams apps.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d9852-128">查看 Teams 应用设计指南</span><span class="sxs-lookup"><span data-stu-id="d9852-128">See the Teams app design guidelines</span></span>](../concepts/design/design-teams-app-overview.md)
