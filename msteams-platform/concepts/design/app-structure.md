---
title: 设计应用 - 了解应用结构
description: 了解在设计应用时，可以在 Microsoft Teams自定义哪些内容。
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: bf84ad1d52cf46e9242bf4122dc5e900461ab806
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631261"
---
# <a name="understand-the-microsoft-teams-app-structure"></a><span data-ttu-id="15100-103">了解Microsoft Teams结构</span><span class="sxs-lookup"><span data-stu-id="15100-103">Understand the Microsoft Teams app structure</span></span>

<span data-ttu-id="15100-104">生成应用时，了解在应用中可以自定义和不能自定义Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="15100-104">When building your app, it's important to know what you can and can't customize in Microsoft Teams.</span></span> <span data-ttu-id="15100-105">此信息可帮助你更好地了解你控制的应用体验的哪些部分。</span><span class="sxs-lookup"><span data-stu-id="15100-105">This information can help you better understand which parts of the app experience you control.</span></span>

<span data-ttu-id="15100-106">以下框架图显示：</span><span class="sxs-lookup"><span data-stu-id="15100-106">The following wireframes show you:</span></span>

* <span data-ttu-id="15100-107">你可以在每个应用功能中自定义Teams以蓝色 (轮廓的) 。</span><span class="sxs-lookup"><span data-stu-id="15100-107">The surfaces you can customize in each Teams app capability (outlined in blue).</span></span>
* <span data-ttu-id="15100-108">每个功能支持的范围。</span><span class="sxs-lookup"><span data-stu-id="15100-108">The scopes each capability supports.</span></span>

> [!NOTE]
> <span data-ttu-id="15100-109">**范围意味着什么？**</span><span class="sxs-lookup"><span data-stu-id="15100-109">**What does scope mean?**</span></span> <span data-ttu-id="15100-110">范围是用户Teams应用中的一个区域。</span><span class="sxs-lookup"><span data-stu-id="15100-110">A scope is an area in Teams where people can use your app.</span></span> <span data-ttu-id="15100-111">应用可以具有一个或多个范围，包括个人、频道、聊天和会议。</span><span class="sxs-lookup"><span data-stu-id="15100-111">Apps can have one or many scopes, including personal, channels, chats, and meetings.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="15100-112">个人应用</span><span class="sxs-lookup"><span data-stu-id="15100-112">Personal apps</span></span>

<span data-ttu-id="15100-113">个人应用提供一个大型画布来为单个用户托管你的应用内容。</span><span class="sxs-lookup"><span data-stu-id="15100-113">Personal apps provide a large canvas to host your app content for individual users.</span></span> <span data-ttu-id="15100-114">画布是 iframe，因此你可以完全自定义体验。</span><span class="sxs-lookup"><span data-stu-id="15100-114">The canvas is an iframe so you can completely customize the experience.</span></span>

<span data-ttu-id="15100-115">\***支持的范围**：个人\*</span><span class="sxs-lookup"><span data-stu-id="15100-115">\***Supported scopes**: Personal\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps.png" alt-text="概念图像，显示开发人员可自定义Teams应用中的前端区域。" border="false":::

## <a name="tabs"></a><span data-ttu-id="15100-117">选项卡</span><span class="sxs-lookup"><span data-stu-id="15100-117">Tabs</span></span>

<span data-ttu-id="15100-118">选项卡提供了一个大型画布，用于为一组用户托管你的应用内容。</span><span class="sxs-lookup"><span data-stu-id="15100-118">Tabs provide a large canvas to host your app content for a group of users.</span></span> <span data-ttu-id="15100-119">可以在共享空间（如频道、聊天和会议邀请）中包括选项卡。</span><span class="sxs-lookup"><span data-stu-id="15100-119">You can include tabs in shared spaces such as channels, chats, and meeting invites.</span></span> <span data-ttu-id="15100-120">画布是 iframe，因此你可以完全自定义体验。</span><span class="sxs-lookup"><span data-stu-id="15100-120">The canvas is an iframe so you can completely customize the experience.</span></span>

<span data-ttu-id="15100-121">\***支持的范围**：频道、聊天、会议\*</span><span class="sxs-lookup"><span data-stu-id="15100-121">\***Supported scopes**: Channels, Chats, Meetings\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs.png" alt-text="显示开发人员可以自定义选项卡的Teams区域的概念图像。" border="false":::

## <a name="bots"></a><span data-ttu-id="15100-123">机器人</span><span class="sxs-lookup"><span data-stu-id="15100-123">Bots</span></span>

<span data-ttu-id="15100-124">自动程序是对话应用，Teams本机消息传递功能集成，因此会处理 UI 工作。</span><span class="sxs-lookup"><span data-stu-id="15100-124">Bots are conversational apps that integrate with Teams native messaging features, so the UI work is handled for you.</span></span> <span data-ttu-id="15100-125">从设计的角度来看，仍有机会使用我们的自然语言处理 (NLP) 和自适应卡片平台添加个性、自定义功能和丰富且可操作的信息。</span><span class="sxs-lookup"><span data-stu-id="15100-125">From a design standpoint, there are still opportunities to add personality, custom functionality, and rich, actionable information with our natural language processing (NLP) support and Adaptive Cards platform.</span></span>

<span data-ttu-id="15100-126">\***支持的范围**：个人、频道、聊天、会议\*</span><span class="sxs-lookup"><span data-stu-id="15100-126">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots.png" alt-text="概念图像，显示开发人员可以自定义Teams中的前端区域。" border="false":::

## <a name="messaging-extensions"></a><span data-ttu-id="15100-128">消息扩展</span><span class="sxs-lookup"><span data-stu-id="15100-128">Messaging extensions</span></span>

<span data-ttu-id="15100-129">消息传递扩展是插入应用内容或在离开对话的情况下对消息操作快捷方式。</span><span class="sxs-lookup"><span data-stu-id="15100-129">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span> <span data-ttu-id="15100-130">基于操作的邮件扩展可让你更加控制体验，Teams处理大部分基于搜索的邮件扩展呈现内容。</span><span class="sxs-lookup"><span data-stu-id="15100-130">Action-based messaging extensions give you more control of the experience, while Teams handles much of what renders for search-based messaging extensions.</span></span>

<span data-ttu-id="15100-131">\***支持的范围**：个人、频道、聊天、会议\*</span><span class="sxs-lookup"><span data-stu-id="15100-131">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions.png" alt-text="概念图像，显示开发人员可Teams邮件扩展自定义的前端区域。" border="false":::

## <a name="meeting-extensions"></a><span data-ttu-id="15100-133">会议扩展</span><span class="sxs-lookup"><span data-stu-id="15100-133">Meeting extensions</span></span>

<span data-ttu-id="15100-134">会议扩展是增强实时会议的应用。</span><span class="sxs-lookup"><span data-stu-id="15100-134">Meeting extensions are apps to enhance live meetings.</span></span> <span data-ttu-id="15100-135">可以在多种方案中托管应用内容，包括会议之前、期间和之后。</span><span class="sxs-lookup"><span data-stu-id="15100-135">You can host your app content in several scenarios, including before, during, and after meetings.</span></span> <span data-ttu-id="15100-136">图面是 iframe，可让你自定义体验，但请记住，这些应用在会议期间深色且较窄。</span><span class="sxs-lookup"><span data-stu-id="15100-136">The surface is an iframe, allowing you to customize the experience, but keep in mind that these apps are dark themed and narrow during meetings.</span></span>

<span data-ttu-id="15100-137">\***支持的范围**：会议、聊天\*</span><span class="sxs-lookup"><span data-stu-id="15100-137">\***Supported scopes**: Meetings, Chats\*</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions.png" alt-text="概念图像，显示开发人员可针对会议Teams自定义的前端区域。" border="false":::
