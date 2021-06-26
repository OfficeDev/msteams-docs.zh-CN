---
title: 设计应用 - 了解应用结构
description: 了解在设计应用时，可以在 Microsoft Teams自定义哪些内容。
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: a574ebeb5416e614152bb24d52cc798f0032943c
ms.sourcegitcommit: 0fe60b3fd406a5768b18977df53d1f4c665e5300
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53133380"
---
# <a name="understand-the-microsoft-teams-app-structure"></a><span data-ttu-id="14937-103">了解Microsoft Teams结构</span><span class="sxs-lookup"><span data-stu-id="14937-103">Understand the Microsoft Teams app structure</span></span>

<span data-ttu-id="14937-104">生成应用时，了解在应用中可以自定义和不能自定义Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="14937-104">When building your app, it's important to know what you can and can't customize in Microsoft Teams.</span></span> <span data-ttu-id="14937-105">此信息可帮助你更好地了解你控制的应用体验的哪些部分。</span><span class="sxs-lookup"><span data-stu-id="14937-105">This information can help you better understand which parts of the app experience you control.</span></span>

<span data-ttu-id="14937-106">以下框架图显示：</span><span class="sxs-lookup"><span data-stu-id="14937-106">The following wireframes show you:</span></span>

* <span data-ttu-id="14937-107">你可以在每个应用功能中自定义Teams， (粉色) 。</span><span class="sxs-lookup"><span data-stu-id="14937-107">The surfaces you can customize in each Teams app capability (outlined in pink).</span></span>
* <span data-ttu-id="14937-108">每个功能支持的范围。</span><span class="sxs-lookup"><span data-stu-id="14937-108">The scopes each capability supports.</span></span>

> [!TIP]
> <span data-ttu-id="14937-109">**范围意味着什么？**</span><span class="sxs-lookup"><span data-stu-id="14937-109">**What does scope mean?**</span></span> <span data-ttu-id="14937-110">范围是用户Teams应用中的一个区域。</span><span class="sxs-lookup"><span data-stu-id="14937-110">A scope is an area in Teams where people can use your app.</span></span> <span data-ttu-id="14937-111">应用可以具有一个或多个范围，包括个人、频道、聊天和会议。</span><span class="sxs-lookup"><span data-stu-id="14937-111">Apps can have one or many scopes, including personal, channels, chats, and meetings.</span></span>

## <a name="personal-apps"></a><span data-ttu-id="14937-112">个人应用</span><span class="sxs-lookup"><span data-stu-id="14937-112">Personal apps</span></span>

<span data-ttu-id="14937-113">个人应用提供一个大型画布来为单个用户托管你的应用内容。</span><span class="sxs-lookup"><span data-stu-id="14937-113">Personal apps provide a large canvas to host your app content for individual users.</span></span>

<span data-ttu-id="14937-114">\***支持的范围**：个人\*</span><span class="sxs-lookup"><span data-stu-id="14937-114">\***Supported scopes**: Personal\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="14937-115">桌面设备</span><span class="sxs-lookup"><span data-stu-id="14937-115">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="14937-116">画布是 iframe，因此你可以完全自定义体验。</span><span class="sxs-lookup"><span data-stu-id="14937-116">The canvas is an iframe so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="概念图像，显示开发人员可针对桌面Teams自定义的前端区域。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="14937-118">移动设备</span><span class="sxs-lookup"><span data-stu-id="14937-118">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="14937-119">画布是 Web 视图，因此你可以完全自定义体验。</span><span class="sxs-lookup"><span data-stu-id="14937-119">The canvas is a webview so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="显示开发人员可针对移动版个人Teams自定义的前端区域的概念图像。" border="false":::

---

## <a name="tabs"></a><span data-ttu-id="14937-121">选项卡</span><span class="sxs-lookup"><span data-stu-id="14937-121">Tabs</span></span>

<span data-ttu-id="14937-122">选项卡提供了一个大型画布，用于为一组用户托管你的应用内容。</span><span class="sxs-lookup"><span data-stu-id="14937-122">Tabs provide a large canvas to host your app content for a group of users.</span></span> <span data-ttu-id="14937-123">可以在共享空间（如频道、聊天和会议邀请）中包括选项卡。</span><span class="sxs-lookup"><span data-stu-id="14937-123">You can include tabs in shared spaces such as channels, chats, and meeting invites.</span></span>

<span data-ttu-id="14937-124">\***支持的范围**：频道、聊天、会议\*</span><span class="sxs-lookup"><span data-stu-id="14937-124">\***Supported scopes**: Channels, Chats, Meetings\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="14937-125">桌面设备</span><span class="sxs-lookup"><span data-stu-id="14937-125">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="14937-126">画布是 iframe，因此你可以完全自定义体验。</span><span class="sxs-lookup"><span data-stu-id="14937-126">The canvas is an iframe so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="概念图像，显示开发人员可以自定义Teams桌面选项卡的前端区域。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="14937-128">移动设备</span><span class="sxs-lookup"><span data-stu-id="14937-128">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="14937-129">画布是 Web 视图，因此你可以完全自定义体验。</span><span class="sxs-lookup"><span data-stu-id="14937-129">The canvas is a webview so you can completely customize the experience.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="概念图像，显示开发人员可以针对Teams选项卡自定义的前端区域。" border="false":::

---

## <a name="bots"></a><span data-ttu-id="14937-131">机器人</span><span class="sxs-lookup"><span data-stu-id="14937-131">Bots</span></span>

<span data-ttu-id="14937-132">自动程序是对话应用，Teams本机消息传递功能集成，因此会处理 UI 工作。</span><span class="sxs-lookup"><span data-stu-id="14937-132">Bots are conversational apps that integrate with Teams native messaging features, so the UI work is handled for you.</span></span> <span data-ttu-id="14937-133">从设计的角度来看，仍有机会使用我们的自然语言处理 (NLP) 和自适应卡片平台添加个性、自定义功能和丰富且可操作的信息。</span><span class="sxs-lookup"><span data-stu-id="14937-133">From a design standpoint, there are still opportunities to add personality, custom functionality, and rich, actionable information with our natural language processing (NLP) support and Adaptive Cards platform.</span></span>

<span data-ttu-id="14937-134">\***支持的范围**：个人、频道、聊天、会议\*</span><span class="sxs-lookup"><span data-stu-id="14937-134">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="14937-135">桌面设备</span><span class="sxs-lookup"><span data-stu-id="14937-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="显示开发人员可在桌面上为Teams自动程序自定义的前端区域的概念图像。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="14937-137">移动设备</span><span class="sxs-lookup"><span data-stu-id="14937-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="概念图像，显示开发人员可以针对Teams自动程序自定义的前端区域。" border="false":::

---

## <a name="messaging-extensions"></a><span data-ttu-id="14937-139">消息扩展</span><span class="sxs-lookup"><span data-stu-id="14937-139">Messaging extensions</span></span>

<span data-ttu-id="14937-140">消息传递是插入应用程序内容或对消息采取行动的快捷方式，而无需从对话中导航。</span><span class="sxs-lookup"><span data-stu-id="14937-140">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span> <span data-ttu-id="14937-141">基于操作的邮件扩展可让你更加控制体验，Teams处理大部分基于搜索的邮件扩展呈现内容。</span><span class="sxs-lookup"><span data-stu-id="14937-141">Action-based messaging extensions give you more control of the experience, while Teams handles much of what renders for search-based messaging extensions.</span></span>

<span data-ttu-id="14937-142">\***支持的范围**：个人、频道、聊天、会议\*</span><span class="sxs-lookup"><span data-stu-id="14937-142">\***Supported scopes**: Personal, Channels, Chats, Meetings\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="14937-143">桌面设备</span><span class="sxs-lookup"><span data-stu-id="14937-143">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="概念图像，显示开发人员可自定义Teams桌面消息扩展的前端区域。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="14937-145">移动设备</span><span class="sxs-lookup"><span data-stu-id="14937-145">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="概念图像，显示开发人员可针对Teams邮件扩展自定义的前端区域。" border="false":::

---

## <a name="meeting-extensions"></a><span data-ttu-id="14937-147">会议扩展</span><span class="sxs-lookup"><span data-stu-id="14937-147">Meeting extensions</span></span>

<span data-ttu-id="14937-148">会议扩展是增强实时会议的应用。</span><span class="sxs-lookup"><span data-stu-id="14937-148">Meeting extensions are apps to enhance live meetings.</span></span> <span data-ttu-id="14937-149">可以在多种方案中托管应用内容，包括会议之前、期间和之后。</span><span class="sxs-lookup"><span data-stu-id="14937-149">You can host your app content in several scenarios, including before, during, and after meetings.</span></span>

<span data-ttu-id="14937-150">\***支持的范围**：会议、聊天\*</span><span class="sxs-lookup"><span data-stu-id="14937-150">\***Supported scopes**: Meetings, Chats\*</span></span>

# <a name="desktop"></a>[<span data-ttu-id="14937-151">桌面设备</span><span class="sxs-lookup"><span data-stu-id="14937-151">Desktop</span></span>](#tab/desktop)

<span data-ttu-id="14937-152">图面是 iframe，可让你自定义体验，但请记住，在会议期间，这些应用使用深色主题且较窄。</span><span class="sxs-lookup"><span data-stu-id="14937-152">The surface is an iframe, allowing you to customize the experience, but keep in mind that during meetings these apps use dark theme and are narrow.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="概念图像，显示开发人员可自定义Teams桌面会议扩展的前端区域。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="14937-154">移动设备</span><span class="sxs-lookup"><span data-stu-id="14937-154">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="14937-155">图面是 Web 视图，可让你自定义体验，但请记住，在会议期间，这些应用使用深色主题。</span><span class="sxs-lookup"><span data-stu-id="14937-155">The surface is a webview, allowing you to customize the experience, but keep in mind that during meetings these apps use dark theme.</span></span>

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="概念图像，显示开发人员可Teams移动版会议扩展自定义的前端区域。" border="false":::

---
