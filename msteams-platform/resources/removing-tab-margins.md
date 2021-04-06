---
title: 删除 Microsoft Teams 中的选项卡边距
author: laujan
description: 介绍删除制表位将如何增强开发人员的体验。
keywords: 删除边距填充的选项卡
ms.topic: reference
ms.author: lomeybur
ms.openlocfilehash: 953dcf0a0edd47a0bf65bbd0db5901c5b98b11c3
ms.sourcegitcommit: e78c9f51c4538212c53bb6c6a45a09d994896f09
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2021
ms.locfileid: "51585818"
---
# <a name="tab-margin-changes"></a><span data-ttu-id="ef233-104">选项卡边距更改</span><span class="sxs-lookup"><span data-stu-id="ef233-104">Tab margin changes</span></span>

<span data-ttu-id="ef233-105">本文档介绍在 Microsoft Teams 中删除所有选项卡的边距将如何增强开发人员在生成应用时的体验。</span><span class="sxs-lookup"><span data-stu-id="ef233-105">This document describes how the removal of margins around all tabs in Microsoft Teams will enhance the developer's experience when building apps.</span></span> <span data-ttu-id="ef233-106">这是 Microsoft Teams 在 2021 年引入的增强功能。</span><span class="sxs-lookup"><span data-stu-id="ef233-106">This is an enhancement introduced in Microsoft Teams in 2021.</span></span>
<span data-ttu-id="ef233-107">删除所有选项卡周围的边距将允许开发人员生成看起来更原生于 Teams 的应用。</span><span class="sxs-lookup"><span data-stu-id="ef233-107">Removing the margins around all tabs will allow developers to build apps that look more native to Teams.</span></span> <span data-ttu-id="ef233-108">这也符合我们的 UI [工具包设计](~/tabs/design/tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="ef233-108">This will also align with our [UI kit designs](~/tabs/design/tabs.md).</span></span> <span data-ttu-id="ef233-109">大多数应用已看起来更好，没有围绕其体验的边距。</span><span class="sxs-lookup"><span data-stu-id="ef233-109">Most apps already look better without the margins surrounding their experiences.</span></span> <span data-ttu-id="ef233-110">但是，某些选项卡会受此更改的视觉影响，开发人员必须进行必要的更改。</span><span class="sxs-lookup"><span data-stu-id="ef233-110">However, some tabs are visually affected by this change, and developers must make the necessary changes.</span></span>

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="选项卡上没有边距" border="false":::

> [!NOTE]
> <span data-ttu-id="ef233-112">此功能不适用于移动客户端，因为移动客户端中查看的选项卡没有边距。</span><span class="sxs-lookup"><span data-stu-id="ef233-112">This feature is not applicable to mobile clients, as the tabs viewed in the mobile clients do not have margins.</span></span> 

## <a name="timelines"></a><span data-ttu-id="ef233-113">日程表</span><span class="sxs-lookup"><span data-stu-id="ef233-113">Timelines</span></span>

* <span data-ttu-id="ef233-114">2021 年 3 月 5 日 - 在 Public 开发者预览版 [中删除边距](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="ef233-114">March 5, 2021 - Margins removed in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
* <span data-ttu-id="ef233-115">2021 年 6 月 15 日 - 将在生产中删除边距。</span><span class="sxs-lookup"><span data-stu-id="ef233-115">June 15, 2021 - Margins will be removed in production.</span></span>

## <a name="guidelines"></a><span data-ttu-id="ef233-116">准则</span><span class="sxs-lookup"><span data-stu-id="ef233-116">Guidelines</span></span>

<span data-ttu-id="ef233-117">此更改将影响使用选项卡的 Microsoft Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="ef233-117">Microsoft Teams apps that use tabs will be affected by this change.</span></span> <span data-ttu-id="ef233-118">开发人员必须切换到 [公共开发者预览版，](~/resources/dev-preview/developer-preview-intro.md) 以确定其选项卡会受到哪些影响，并进行必要的更改。</span><span class="sxs-lookup"><span data-stu-id="ef233-118">Developers must switch to [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) in order to determine how their tabs are affected and make the necessary changes.</span></span>

<span data-ttu-id="ef233-119">选项卡开发人员不得依赖 Teams 提供其选项卡周围的边距。</span><span class="sxs-lookup"><span data-stu-id="ef233-119">Tab developers must not rely on Teams to provide margins surrounding their tabs.</span></span> <span data-ttu-id="ef233-120">建议开发人员根据需要在选项卡设计周围添加边距。</span><span class="sxs-lookup"><span data-stu-id="ef233-120">Developers are encouraged to add margins around their tab designs where it is required.</span></span> <span data-ttu-id="ef233-121">生产中的应用设计可能看起来有额外的填充，即 Teams 提供的边距和选项卡提供的边距。但是，额外的填充只是临时的，将在几周后消失，仅留下应用提供的填充。</span><span class="sxs-lookup"><span data-stu-id="ef233-121">App designs in production can look like there is extra padding, that is, margins provided by Teams and margins provided by the tab. However, the extra padding is only temporary and will go away in a few weeks, leaving only the app's provided padding.</span></span>

## <a name="faq"></a><span data-ttu-id="ef233-122">常见问题</span><span class="sxs-lookup"><span data-stu-id="ef233-122">FAQ</span></span>

<span data-ttu-id="ef233-123">**应用部件版式（如标题栏或任务栏）是否适合触摸我们设计的边缘？**</span><span class="sxs-lookup"><span data-stu-id="ef233-123">**Is it OK for app chrome, such as header bar or taskbar, to touch the edges of our designs?**</span></span>

<span data-ttu-id="ef233-124">是的，这很好，建议这样做。</span><span class="sxs-lookup"><span data-stu-id="ef233-124">Yes, this is fine and encouraged.</span></span> <span data-ttu-id="ef233-125">这有助于应用感觉本机。</span><span class="sxs-lookup"><span data-stu-id="ef233-125">This helps the app feel native.</span></span>

<span data-ttu-id="ef233-126">**对于文本、徽标和图像等应用内容，触摸设计的左右边缘是否正常？**</span><span class="sxs-lookup"><span data-stu-id="ef233-126">**Is it OK for app content, such as text, logos, and images, to touch the left and right edges of our designs?**</span></span>

<span data-ttu-id="ef233-127">否，你必须在所有应用内容的左侧和右侧提供自己的填充或边距，以确保它不会触摸 UI 的边缘。</span><span class="sxs-lookup"><span data-stu-id="ef233-127">No, you must provide your own padding or margins to the left and right of all app content to ensure it does not touch the edges of your UI.</span></span> <span data-ttu-id="ef233-128">如果需要，还可以在选项卡顶部添加边距。</span><span class="sxs-lookup"><span data-stu-id="ef233-128">You can also add margins at the top of your tab, if required.</span></span>

<span data-ttu-id="ef233-129">**Teams 之前应用的边距大小如何？**</span><span class="sxs-lookup"><span data-stu-id="ef233-129">**What's the size of the margins Teams previously applied?**</span></span>

* <span data-ttu-id="ef233-130">左右：20px</span><span class="sxs-lookup"><span data-stu-id="ef233-130">Left and right: 20px</span></span>
* <span data-ttu-id="ef233-131">顶部：16px</span><span class="sxs-lookup"><span data-stu-id="ef233-131">Top: 16px</span></span>
* <span data-ttu-id="ef233-132">底部：0px</span><span class="sxs-lookup"><span data-stu-id="ef233-132">Bottom: 0px</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="ef233-133">删除所有选项卡的边距：个人选项卡、 (组) 聊天选项卡、会议选项卡和频道选项卡。</span><span class="sxs-lookup"><span data-stu-id="ef233-133">All tabs have their margins removed: personal tabs, (group) chat tabs, meeting tabs, and channel tabs.</span></span>
> * <span data-ttu-id="ef233-134">无法选择加入或选择退出此更改。</span><span class="sxs-lookup"><span data-stu-id="ef233-134">There is no way to opt-in or opt-out of this change.</span></span> <span data-ttu-id="ef233-135">它将应用于所有选项卡。</span><span class="sxs-lookup"><span data-stu-id="ef233-135">It will apply to all tabs.</span></span>
> * <span data-ttu-id="ef233-136">此更改可能会影响依赖 Microsoft Teams 提供其 UI 周围的边距的选项卡。</span><span class="sxs-lookup"><span data-stu-id="ef233-136">This change can affect tabs that rely on Microsoft Teams to provide margins surrounding their UI.</span></span>
