---
title: 删除 Microsoft Teams 中的选项卡边距
author: laujan
description: 描述删除选项卡边距将如何增强开发人员的体验。
keywords: 选项卡删除边距填充
ms.topic: reference
ms.author: lomeybur
ms.openlocfilehash: 87766a40730fdaa2da80c2e0031eab655a993c33
ms.sourcegitcommit: 9cfbc44912980a33d2d7c7c85739aeea6ccb41de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "50479951"
---
# <a name="tab-margin-changes"></a><span data-ttu-id="0c0dc-104">制表位边距更改</span><span class="sxs-lookup"><span data-stu-id="0c0dc-104">Tab margin changes</span></span>

<span data-ttu-id="0c0dc-105">本文档介绍删除 Microsoft Teams 中所有选项卡的边距如何增强开发人员在生成应用时的体验。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-105">This document describes how the removal of margins around all tabs in Microsoft Teams will enhance the developer's experience when building apps.</span></span> <span data-ttu-id="0c0dc-106">这是 2021 年 Microsoft Teams 中引入的增强功能。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-106">This is an enhancement introduced in Microsoft Teams in 2021.</span></span>
<span data-ttu-id="0c0dc-107">删除所有选项卡周围的边距将允许开发人员生成对 Teams 来说更本机的应用。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-107">Removing the margins around all tabs will allow developers to build apps that look more native to Teams.</span></span> <span data-ttu-id="0c0dc-108">这也符合我们的 UI [工具包设计](~/tabs/design/tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-108">This will also align with our [UI kit designs](~/tabs/design/tabs.md).</span></span> <span data-ttu-id="0c0dc-109">大多数应用已经看起来更好，没有围绕其体验的边距。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-109">Most apps already look better without the margins surrounding their experiences.</span></span> <span data-ttu-id="0c0dc-110">但是，某些选项卡受此更改的视觉影响，开发人员必须进行必要的更改。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-110">However, some tabs are visually affected by this change, and developers must make the necessary changes.</span></span>

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="制表符和无边距" border="false":::

## <a name="timelines"></a><span data-ttu-id="0c0dc-112">日程表</span><span class="sxs-lookup"><span data-stu-id="0c0dc-112">Timelines</span></span>

* <span data-ttu-id="0c0dc-113">2021 年 3 月 5 日 - 在[公共开发者预览版。](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="0c0dc-113">March 5, 2021 - Margins removed in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
* <span data-ttu-id="0c0dc-114">2021 年 5 月 1 日 - 将在生产中删除边距。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-114">May 1, 2021 - Margins will be removed in production.</span></span>

## <a name="guidelines"></a><span data-ttu-id="0c0dc-115">准则</span><span class="sxs-lookup"><span data-stu-id="0c0dc-115">Guidelines</span></span>

<span data-ttu-id="0c0dc-116">使用选项卡的 Microsoft Teams 应用将受此更改的影响。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-116">Microsoft Teams apps that use tabs will be affected by this change.</span></span> <span data-ttu-id="0c0dc-117">开发人员应切换到 [公共开发者预览版，](~/resources/dev-preview/developer-preview-intro.md) 以确定其选项卡如何受到影响，并进行必要的更改。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-117">Developers should switch to [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) in order to determine how their tabs are affected and make the necessary changes.</span></span>

<span data-ttu-id="0c0dc-118">选项卡开发人员不得依赖 Teams 提供其选项卡周围的边距。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-118">Tab developers must not rely on Teams to provide margins surrounding their tabs.</span></span> <span data-ttu-id="0c0dc-119">建议开发人员根据需要添加选项卡设计周围的边距。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-119">Developers are encouraged to add margins around their tab designs where it is required.</span></span> <span data-ttu-id="0c0dc-120">生产中的应用设计可能看起来有额外的填充，即 Teams 提供的边距和选项卡提供的边距。但是，额外的填充只是临时的，将在几周后消失，仅留下应用提供的填充。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-120">App designs in production can look like there is extra padding, that is, margins provided by Teams and margins provided by the tab. However, the extra padding is only temporary and will go away in a few weeks, leaving only the app's provided padding.</span></span>

## <a name="faq"></a><span data-ttu-id="0c0dc-121">常见问题</span><span class="sxs-lookup"><span data-stu-id="0c0dc-121">FAQ</span></span>

<span data-ttu-id="0c0dc-122">**应用部件版式（如标题栏或任务栏）是否适合触摸我们设计的边缘？**</span><span class="sxs-lookup"><span data-stu-id="0c0dc-122">**Is it OK for app chrome, such as header bar or taskbar, to touch the edges of our designs?**</span></span>

<span data-ttu-id="0c0dc-123">是的，这很好，建议这样做。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-123">Yes, this is fine and encouraged.</span></span> <span data-ttu-id="0c0dc-124">这有助于应用感觉本机。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-124">This helps the app feel native.</span></span>

<span data-ttu-id="0c0dc-125">**应用内容（如文本、徽标和图像）可以触摸我们设计的左右边缘吗？**</span><span class="sxs-lookup"><span data-stu-id="0c0dc-125">**Is it OK for app content, such as text, logos, and images, to touch the left and right edges of our designs?**</span></span>

<span data-ttu-id="0c0dc-126">否，你必须在所有应用内容的左侧和右侧提供自己的填充或边距，以确保它不会接触 UI 的边缘。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-126">No, you must provide your own padding or margins to the left and right of all app content to ensure it does not touch the edges of your UI.</span></span> <span data-ttu-id="0c0dc-127">如果需要，还可以在选项卡顶部添加边距。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-127">You can also add margins at the top of your tab, if required.</span></span>

<span data-ttu-id="0c0dc-128">**Teams 之前应用的边距大小如何？**</span><span class="sxs-lookup"><span data-stu-id="0c0dc-128">**What's the size of the margins Teams previously applied?**</span></span>

* <span data-ttu-id="0c0dc-129">左右：20px</span><span class="sxs-lookup"><span data-stu-id="0c0dc-129">Left and right: 20px</span></span>
* <span data-ttu-id="0c0dc-130">顶部：16px</span><span class="sxs-lookup"><span data-stu-id="0c0dc-130">Top: 16px</span></span>
* <span data-ttu-id="0c0dc-131">底部：0px</span><span class="sxs-lookup"><span data-stu-id="0c0dc-131">Bottom: 0px</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="0c0dc-132">所有选项卡都删除了其边距：个人选项卡、 (组) 聊天选项卡、会议选项卡和频道选项卡。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-132">All tabs have their margins removed: personal tabs, (group) chat tabs, meeting tabs, and channel tabs.</span></span>
> * <span data-ttu-id="0c0dc-133">无法选择加入或选择退出此更改。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-133">There is no way to opt-in or opt-out of this change.</span></span> <span data-ttu-id="0c0dc-134">它将应用于所有选项卡。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-134">It will apply to all tabs.</span></span>
> * <span data-ttu-id="0c0dc-135">此更改可能会影响依赖 Microsoft Teams 提供 UI 周围边距的选项卡。</span><span class="sxs-lookup"><span data-stu-id="0c0dc-135">This change can affect tabs that rely on Microsoft Teams to provide margins surrounding their UI.</span></span>
