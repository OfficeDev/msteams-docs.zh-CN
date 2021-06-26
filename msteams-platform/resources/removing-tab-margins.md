---
title: 删除选项卡页边距Microsoft Teams
author: surbhigupta
description: 介绍删除制表位将如何增强开发人员的体验。
keywords: 删除边距填充的选项卡
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: 086ce3a375416291a64e3222e698d7e363a651e6
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140570"
---
# <a name="tab-margin-changes"></a><span data-ttu-id="d8da1-104">选项卡边距更改</span><span class="sxs-lookup"><span data-stu-id="d8da1-104">Tab margin changes</span></span>

<span data-ttu-id="d8da1-105">本文档介绍删除文档中所有选项卡的边距Microsoft Teams如何在生成应用时增强开发人员的体验。</span><span class="sxs-lookup"><span data-stu-id="d8da1-105">This document describes how the removal of margins around all tabs in Microsoft Teams will enhance the developer's experience when building apps.</span></span> <span data-ttu-id="d8da1-106">这是 2021 年 Microsoft Teams中引入的增强功能。</span><span class="sxs-lookup"><span data-stu-id="d8da1-106">This is an enhancement introduced in Microsoft Teams in 2021.</span></span>
<span data-ttu-id="d8da1-107">删除所有选项卡周围的边距将允许开发人员生成看起来更本机的Teams。</span><span class="sxs-lookup"><span data-stu-id="d8da1-107">Removing the margins around all tabs will allow developers to build apps that look more native to Teams.</span></span> <span data-ttu-id="d8da1-108">这也符合我们的 UI [工具包设计](~/tabs/design/tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="d8da1-108">This will also align with our [UI kit designs](~/tabs/design/tabs.md).</span></span> <span data-ttu-id="d8da1-109">大多数应用已看起来更好，没有围绕其体验的边距。</span><span class="sxs-lookup"><span data-stu-id="d8da1-109">Most apps already look better without the margins surrounding their experiences.</span></span> <span data-ttu-id="d8da1-110">但是，某些选项卡会受此更改的视觉影响，开发人员必须进行必要的更改。</span><span class="sxs-lookup"><span data-stu-id="d8da1-110">However, some tabs are visually affected by this change, and developers must make the necessary changes.</span></span>

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="选项卡上没有边距" border="false":::

> [!NOTE]
> <span data-ttu-id="d8da1-112">此功能不适用于移动客户端，因为移动客户端中查看的选项卡没有边距。</span><span class="sxs-lookup"><span data-stu-id="d8da1-112">This feature is not applicable to mobile clients, as the tabs viewed in the mobile clients do not have margins.</span></span> 

## <a name="timelines"></a><span data-ttu-id="d8da1-113">日程表</span><span class="sxs-lookup"><span data-stu-id="d8da1-113">Timelines</span></span>

* <span data-ttu-id="d8da1-114">2021 年 3 月 5 日 - 在 Public 开发者预览版 [中删除边距](~/resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="d8da1-114">March 5, 2021 - Margins removed in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
* <span data-ttu-id="d8da1-115">2021 年 6 月 15 日 - 将在生产中删除边距。</span><span class="sxs-lookup"><span data-stu-id="d8da1-115">June 15, 2021 - Margins will be removed in production.</span></span>

## <a name="guidelines"></a><span data-ttu-id="d8da1-116">准则</span><span class="sxs-lookup"><span data-stu-id="d8da1-116">Guidelines</span></span>

<span data-ttu-id="d8da1-117">Microsoft Teams选项卡的应用将受此更改的影响。</span><span class="sxs-lookup"><span data-stu-id="d8da1-117">Microsoft Teams apps that use tabs will be affected by this change.</span></span> <span data-ttu-id="d8da1-118">开发人员必须切换到 [公共开发者预览版，](~/resources/dev-preview/developer-preview-intro.md) 以确定其选项卡会受到哪些影响，并进行必要的更改。</span><span class="sxs-lookup"><span data-stu-id="d8da1-118">Developers must switch to [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) in order to determine how their tabs are affected and make the necessary changes.</span></span>

<span data-ttu-id="d8da1-119">选项卡开发人员不得依赖Teams选项卡周围的边距。</span><span class="sxs-lookup"><span data-stu-id="d8da1-119">Tab developers must not rely on Teams to provide margins surrounding their tabs.</span></span> <span data-ttu-id="d8da1-120">建议开发人员根据需要在选项卡设计周围添加边距。</span><span class="sxs-lookup"><span data-stu-id="d8da1-120">Developers are encouraged to add margins around their tab designs where it is required.</span></span> <span data-ttu-id="d8da1-121">生产中的应用设计可能看起来有额外的填充，即由Teams提供的边距和选项卡提供的边距。但是，额外的填充只是临时的，将在几周后消失，仅留下应用提供的填充。</span><span class="sxs-lookup"><span data-stu-id="d8da1-121">App designs in production can look like there is extra padding, that is, margins provided by Teams and margins provided by the tab. However, the extra padding is only temporary and will go away in a few weeks, leaving only the app's provided padding.</span></span>

## <a name="faq"></a><span data-ttu-id="d8da1-122">常见问题</span><span class="sxs-lookup"><span data-stu-id="d8da1-122">FAQ</span></span>

<span data-ttu-id="d8da1-123">**应用部件版式（如标题栏或任务栏）是否适合触摸我们设计的边缘？**</span><span class="sxs-lookup"><span data-stu-id="d8da1-123">**Is it OK for app chrome, such as header bar or taskbar, to touch the edges of our designs?**</span></span>

<span data-ttu-id="d8da1-124">是的，这很好，建议这样做。</span><span class="sxs-lookup"><span data-stu-id="d8da1-124">Yes, this is fine and encouraged.</span></span> <span data-ttu-id="d8da1-125">这有助于应用感觉本机。</span><span class="sxs-lookup"><span data-stu-id="d8da1-125">This helps the app feel native.</span></span>

<span data-ttu-id="d8da1-126">**对于文本、徽标和图像等应用内容，触摸设计的左右边缘是否正常？**</span><span class="sxs-lookup"><span data-stu-id="d8da1-126">**Is it OK for app content, such as text, logos, and images, to touch the left and right edges of our designs?**</span></span>

<span data-ttu-id="d8da1-127">否，你必须在所有应用内容的左侧和右侧提供自己的填充或边距，以确保它不会触摸 UI 的边缘。</span><span class="sxs-lookup"><span data-stu-id="d8da1-127">No, you must provide your own padding or margins to the left and right of all app content to ensure it does not touch the edges of your UI.</span></span> <span data-ttu-id="d8da1-128">如果需要，还可以在选项卡顶部添加边距。</span><span class="sxs-lookup"><span data-stu-id="d8da1-128">You can also add margins at the top of your tab, if required.</span></span>

<span data-ttu-id="d8da1-129">**之前应用的边距Teams的大小？**</span><span class="sxs-lookup"><span data-stu-id="d8da1-129">**What's the size of the margins Teams previously applied?**</span></span>

* <span data-ttu-id="d8da1-130">左右：20px</span><span class="sxs-lookup"><span data-stu-id="d8da1-130">Left and right: 20px</span></span>
* <span data-ttu-id="d8da1-131">顶部：16px</span><span class="sxs-lookup"><span data-stu-id="d8da1-131">Top: 16px</span></span>
* <span data-ttu-id="d8da1-132">底部：0px</span><span class="sxs-lookup"><span data-stu-id="d8da1-132">Bottom: 0px</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="d8da1-133">删除所有选项卡的边距：个人选项卡、 (组) 聊天选项卡、会议选项卡和频道选项卡。</span><span class="sxs-lookup"><span data-stu-id="d8da1-133">All tabs have their margins removed: personal tabs, (group) chat tabs, meeting tabs, and channel tabs.</span></span>
> * <span data-ttu-id="d8da1-134">无法选择加入或选择退出此更改。</span><span class="sxs-lookup"><span data-stu-id="d8da1-134">There is no way to opt-in or opt-out of this change.</span></span> <span data-ttu-id="d8da1-135">它将应用于所有选项卡。</span><span class="sxs-lookup"><span data-stu-id="d8da1-135">It will apply to all tabs.</span></span>
> * <span data-ttu-id="d8da1-136">此更改可能会影响依赖其 UI Microsoft Teams提供边距的选项卡。</span><span class="sxs-lookup"><span data-stu-id="d8da1-136">This change can affect tabs that rely on Microsoft Teams to provide margins surrounding their UI.</span></span>

## <a name="see-also"></a><span data-ttu-id="d8da1-137">另请参阅</span><span class="sxs-lookup"><span data-stu-id="d8da1-137">See also</span></span>

* [<span data-ttu-id="d8da1-138">Teams选项卡</span><span class="sxs-lookup"><span data-stu-id="d8da1-138">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="d8da1-139">先决条件</span><span class="sxs-lookup"><span data-stu-id="d8da1-139">Prerequisites</span></span>](~/tabs/how-to/tab-requirements.md)
* [<span data-ttu-id="d8da1-140">创建个人选项卡</span><span class="sxs-lookup"><span data-stu-id="d8da1-140">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="d8da1-141">创建频道或组选项卡</span><span class="sxs-lookup"><span data-stu-id="d8da1-141">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="d8da1-142">创建内容页</span><span class="sxs-lookup"><span data-stu-id="d8da1-142">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="d8da1-143">创建配置页</span><span class="sxs-lookup"><span data-stu-id="d8da1-143">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [<span data-ttu-id="d8da1-144">为选项卡创建删除页</span><span class="sxs-lookup"><span data-stu-id="d8da1-144">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
* [<span data-ttu-id="d8da1-145">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="d8da1-145">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="d8da1-146">获取选项卡的上下文</span><span class="sxs-lookup"><span data-stu-id="d8da1-146">Get context for your tab</span></span>](~/tabs/how-to/access-teams-context.md)
* [<span data-ttu-id="d8da1-147">具有自适应卡片的生成选项卡</span><span class="sxs-lookup"><span data-stu-id="d8da1-147">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="d8da1-148">选项卡链接展开和阶段视图</span><span class="sxs-lookup"><span data-stu-id="d8da1-148">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)
* [<span data-ttu-id="d8da1-149">创建对话选项卡</span><span class="sxs-lookup"><span data-stu-id="d8da1-149">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)
