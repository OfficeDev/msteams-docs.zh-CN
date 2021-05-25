---
title: 移动设备上的选项卡
description: 介绍在移动设备上实现选项卡的开发人员Microsoft Teams注意事项。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 41ba96b64bd31f3b226aeba72969bc44c1ae8955
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630654"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="75573-103">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="75573-103">Tabs on mobile</span></span>

<span data-ttu-id="75573-104">生成包含选项卡的 Microsoft Teams 应用时，必须考虑 (并测试) 选项卡在 Android 和 iOS Microsoft Teams 上的运行方式。</span><span class="sxs-lookup"><span data-stu-id="75573-104">When you're building a Microsoft Teams app that includes a tab, you must consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="75573-105">以下各节概述了需要考虑的一些关键方案。</span><span class="sxs-lookup"><span data-stu-id="75573-105">The sections below outline some of the key scenarios you need to consider.</span></span>

## <a name="authentication"></a><span data-ttu-id="75573-106">身份验证</span><span class="sxs-lookup"><span data-stu-id="75573-106">Authentication</span></span>

<span data-ttu-id="75573-107">若要在移动客户端上进行身份验证，必须将 JavaScript SDK Teams至少升级到版本 1.4.1。</span><span class="sxs-lookup"><span data-stu-id="75573-107">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

## <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="75573-108">低带宽和间歇性连接</span><span class="sxs-lookup"><span data-stu-id="75573-108">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="75573-109">移动客户端经常需要在低带宽和间歇性连接下运行。</span><span class="sxs-lookup"><span data-stu-id="75573-109">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="75573-110">应用应该通过向用户提供上下文消息来适当地处理任何超时。</span><span class="sxs-lookup"><span data-stu-id="75573-110">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="75573-111">您还应使用用户进度指示器，以针对任何长时间运行的过程向用户提供反馈。</span><span class="sxs-lookup"><span data-stu-id="75573-111">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

## <a name="testing-on-mobile-clients"></a><span data-ttu-id="75573-112">在移动客户端上测试</span><span class="sxs-lookup"><span data-stu-id="75573-112">Testing on mobile clients</span></span>

<span data-ttu-id="75573-113">需要验证选项卡在各种大小和质量的移动设备上是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="75573-113">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="75573-114">对于 Android 设备，可以在选项卡运行时使用 [DevTools](~/tabs/how-to/developer-tools.md) 调试选项卡。</span><span class="sxs-lookup"><span data-stu-id="75573-114">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="75573-115">建议在高性能和低性能设备（包括平板电脑）上进行测试。</span><span class="sxs-lookup"><span data-stu-id="75573-115">We recommend that you test on both high- and low-performance devices, including a tablet.</span></span>

## <a name="distribution"></a><span data-ttu-id="75573-116">分发</span><span class="sxs-lookup"><span data-stu-id="75573-116">Distribution</span></span>

<span data-ttu-id="75573-117">应用商店中列出的Teams必须经过批准，供移动使用，以在移动Teams正常运行。</span><span class="sxs-lookup"><span data-stu-id="75573-117">Apps listed on the Teams store must be approved for mobile use to function properly in the Teams mobile client.</span></span> <span data-ttu-id="75573-118">选项卡可用性和行为取决于你的应用是否已获得批准。</span><span class="sxs-lookup"><span data-stu-id="75573-118">Tab availability and behavior depends on whether your app is approved.</span></span>

### <a name="apps-on-teams-store-approved-for-mobile"></a><span data-ttu-id="75573-119">经批准Teams移动的应用商店上的应用</span><span class="sxs-lookup"><span data-stu-id="75573-119">Apps on Teams store approved for mobile</span></span>

<span data-ttu-id="75573-120">下表介绍了当应用在应用商店中列出并批准Teams时选项卡可用性和行为：</span><span class="sxs-lookup"><span data-stu-id="75573-120">The following table describes tab availability and behavior when the app is listed on the Teams store and approved for mobile use:</span></span>

|<span data-ttu-id="75573-121">功能</span><span class="sxs-lookup"><span data-stu-id="75573-121">Capability</span></span>   |<span data-ttu-id="75573-122">移动可用性？</span><span class="sxs-lookup"><span data-stu-id="75573-122">Mobile availability?</span></span>   |<span data-ttu-id="75573-123">移动行为</span><span class="sxs-lookup"><span data-stu-id="75573-123">Mobile behavior</span></span>|
|----------|-----------|------------|
|<span data-ttu-id="75573-124">频道</span><span class="sxs-lookup"><span data-stu-id="75573-124">Channel</span></span> <br /> <span data-ttu-id="75573-125">和组选项卡</span><span class="sxs-lookup"><span data-stu-id="75573-125">and group tab</span></span>|<span data-ttu-id="75573-126">是</span><span class="sxs-lookup"><span data-stu-id="75573-126">Yes</span></span>|<span data-ttu-id="75573-127">选项卡使用Teams在移动客户端中 `contentUrl` 打开。</span><span class="sxs-lookup"><span data-stu-id="75573-127">Tab opens in the Teams mobile client using your app's `contentUrl` configuration.</span></span>|
|<span data-ttu-id="75573-128">个人应用</span><span class="sxs-lookup"><span data-stu-id="75573-128">Personal app</span></span>|<span data-ttu-id="75573-129">是</span><span class="sxs-lookup"><span data-stu-id="75573-129">Yes</span></span>|<span data-ttu-id="75573-130">"个人应用"选项卡中的每个选项卡使用各自的Teams在移动客户端中 `contentUrl` 打开。</span><span class="sxs-lookup"><span data-stu-id="75573-130">Each tab in the personal app tab opens in the Teams mobile client using its respective `contentUrl` configuration.</span></span>|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a><span data-ttu-id="75573-131">未批准Teams移动的应用商店上的应用</span><span class="sxs-lookup"><span data-stu-id="75573-131">Apps on Teams store not approved for mobile</span></span>

<span data-ttu-id="75573-132">下表介绍了当应用在应用商店中列出但Teams未批准的移动用途时选项卡可用性和行为：</span><span class="sxs-lookup"><span data-stu-id="75573-132">The following table describes tab availability and behavior when the app is listed on the Teams store but not approved for mobile use:</span></span>

| <span data-ttu-id="75573-133">功能</span><span class="sxs-lookup"><span data-stu-id="75573-133">Capability</span></span> | <span data-ttu-id="75573-134">移动可用性？</span><span class="sxs-lookup"><span data-stu-id="75573-134">Mobile availability?</span></span> | <span data-ttu-id="75573-135">移动行为</span><span class="sxs-lookup"><span data-stu-id="75573-135">Mobile behavior</span></span> |
|----------|-----------|------------|
|<span data-ttu-id="75573-136">"频道和组"选项卡</span><span class="sxs-lookup"><span data-stu-id="75573-136">Channel and group tab</span></span>|<span data-ttu-id="75573-137">是</span><span class="sxs-lookup"><span data-stu-id="75573-137">Yes</span></span>|<span data-ttu-id="75573-138">选项卡将在设备的默认浏览器中打开，而不是Teams应用的配置（还必须包含在源代码的 函数中）中的移动 `websiteUrl` `setSettings()` [客户端](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="75573-138">Tab opens in the device's default browser instead of the Teams mobile client using your app's `websiteUrl` configuration, which also must be included in your source code's `setSettings()` [function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true).</span></span> <span data-ttu-id="75573-139">但是，用户仍可在移动客户端Teams选项卡，方法为选择应用旁边的"更多"并选择"打开"，这将触发应用的 `contentUrl` 配置。</span><span class="sxs-lookup"><span data-stu-id="75573-139">However, users can still view the tab in the Teams mobile client by selecting **More** next to the app and choosing **Open**, which triggers your app’s `contentUrl` configuration.</span></span>|
|<span data-ttu-id="75573-140">个人应用</span><span class="sxs-lookup"><span data-stu-id="75573-140">Personal app</span></span>|<span data-ttu-id="75573-141">不支持</span><span class="sxs-lookup"><span data-stu-id="75573-141">No</span></span>|<span data-ttu-id="75573-142">不适用</span><span class="sxs-lookup"><span data-stu-id="75573-142">Not applicable</span></span>|

### <a name="apps-not-on-teams-store"></a><span data-ttu-id="75573-143">不在应用商店Teams应用</span><span class="sxs-lookup"><span data-stu-id="75573-143">Apps not on Teams store</span></span>

<span data-ttu-id="75573-144">如果要将应用旁加载或发布到组织的应用程序目录，选项卡行为将Teams Microsoft 批准的移动应用商店应用的行为相同。</span><span class="sxs-lookup"><span data-stu-id="75573-144">If you're sideloading your app or publishing to an org's app catalog, tab behavior will be the same as Teams store apps approved by Microsoft for mobile.</span></span>

## <a name="see-also"></a><span data-ttu-id="75573-145">另请参阅</span><span class="sxs-lookup"><span data-stu-id="75573-145">See also</span></span>

* [<span data-ttu-id="75573-146">选项卡设计指南</span><span class="sxs-lookup"><span data-stu-id="75573-146">Tab design guidelines</span></span>](~/tabs/design/tabs.md)
