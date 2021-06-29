---
title: 移动设备上的选项卡
description: 介绍在移动设备上实现选项卡的开发人员Microsoft Teams注意事项。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 5053160f2456a5d1c5f68cb74ea3ccc5c5eabca5
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179718"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="9a849-103">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="9a849-103">Tabs on mobile</span></span>

<span data-ttu-id="9a849-104">生成包含选项卡Microsoft Teams应用时，必须测试选项卡在 Android 和 iOS 客户端上Microsoft Teams运行。</span><span class="sxs-lookup"><span data-stu-id="9a849-104">When you are building a Microsoft Teams app that includes a tab, you must test how your tab functions on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="9a849-105">本文概述了必须考虑的一些关键方案。</span><span class="sxs-lookup"><span data-stu-id="9a849-105">This article outlines some of the key scenarios you must consider.</span></span>

<span data-ttu-id="9a849-106">如果您选择让频道或组选项卡显示在Teams客户端上，则配置必须具有 `setSettings()` `websiteUrl` 属性的值。</span><span class="sxs-lookup"><span data-stu-id="9a849-106">If you choose to have your channel or group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span> <span data-ttu-id="9a849-107">为了确保最佳的用户体验，在创建选项卡时，必须遵循本文中针对移动选项卡的指南。</span><span class="sxs-lookup"><span data-stu-id="9a849-107">To ensure optimal user experience, you must follow the guidance for tabs on mobile in this article when creating your tabs.</span></span>

<span data-ttu-id="9a849-108">通过[应用商店分发Teams](~/concepts/deploy-and-publish/appsource/publish.md)对移动客户端具有单独的审批流程。</span><span class="sxs-lookup"><span data-stu-id="9a849-108">Apps [distributed through the Teams store](~/concepts/deploy-and-publish/appsource/publish.md) have a separate approval process for mobile clients.</span></span> <span data-ttu-id="9a849-109">此类应用的默认行为如下所示：</span><span class="sxs-lookup"><span data-stu-id="9a849-109">The default behavior of such apps is as follows:</span></span>

| <span data-ttu-id="9a849-110">**应用功能**</span><span class="sxs-lookup"><span data-stu-id="9a849-110">**App capability**</span></span> | <span data-ttu-id="9a849-111">**应用获得批准时的行为**</span><span class="sxs-lookup"><span data-stu-id="9a849-111">**Behavior if app is approved**</span></span> | <span data-ttu-id="9a849-112">**应用未获得批准时的行为**</span><span class="sxs-lookup"><span data-stu-id="9a849-112">**Behavior if app is not approved**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9a849-113">**个人选项卡**</span><span class="sxs-lookup"><span data-stu-id="9a849-113">**Personal tabs**</span></span> | <span data-ttu-id="9a849-114">应用显示在移动客户端的底部栏中。</span><span class="sxs-lookup"><span data-stu-id="9a849-114">App appears in the bottom bar of the mobile clients.</span></span> <span data-ttu-id="9a849-115">选项卡在 Teams 中打开。</span><span class="sxs-lookup"><span data-stu-id="9a849-115">Tabs open in the Teams client.</span></span> | <span data-ttu-id="9a849-116">应用不显示在移动客户端的底部栏中。</span><span class="sxs-lookup"><span data-stu-id="9a849-116">App does not appear in the bottom bar of the mobile clients.</span></span> |
| <span data-ttu-id="9a849-117">**频道和组选项卡**</span><span class="sxs-lookup"><span data-stu-id="9a849-117">**Channel and group tabs**</span></span> | <span data-ttu-id="9a849-118">选项卡使用 在 Teams 客户端中打开 `contentUrl` 。</span><span class="sxs-lookup"><span data-stu-id="9a849-118">The tab opens in the Teams client using `contentUrl`.</span></span> | <span data-ttu-id="9a849-119">选项卡使用 在 Teams 客户端外部的浏览器中打开 `websiteUrl` 。</span><span class="sxs-lookup"><span data-stu-id="9a849-119">The tab opens in a browser outside the Teams client using `websiteUrl`.</span></span> |

> [!NOTE]
> * <span data-ttu-id="9a849-120">提交到[AppSource](https://appsource.microsoft.com)以在应用上Teams将自动评估移动响应能力。</span><span class="sxs-lookup"><span data-stu-id="9a849-120">Apps submitted to the [AppSource](https://appsource.microsoft.com) for publishing on Teams are evaluated automatically for mobile responsiveness.</span></span> <span data-ttu-id="9a849-121">对于任何查询，请通过联系 teamsubm@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="9a849-121">For any queries, reach out to teamsubm@microsoft.com.</span></span>
> * <span data-ttu-id="9a849-122">对于未通过 AppSource 分发的所有应用，默认情况下，选项卡在 Teams 客户端的应用内 Webview 中打开，并且不需要单独的审批流程。</span><span class="sxs-lookup"><span data-stu-id="9a849-122">For all apps that are not distributed through the AppSource, the tabs open in an in-app webview within the Teams clients by default and there is no separate approval process required.</span></span>
> * <span data-ttu-id="9a849-123">应用的默认行为仅在通过应用商店分发时Teams适用。</span><span class="sxs-lookup"><span data-stu-id="9a849-123">The default behavior of apps is only applicable if distributed through the Teams store.</span></span> <span data-ttu-id="9a849-124">默认情况下，所有选项卡在 Teams 中打开。</span><span class="sxs-lookup"><span data-stu-id="9a849-124">By default, all tabs open in the Teams client.</span></span>
> * <span data-ttu-id="9a849-125">若要开始对应用进行移动友好评估，请通过 teamsubm@microsoft.com 与应用详细信息联系。</span><span class="sxs-lookup"><span data-stu-id="9a849-125">To initiate an evaluation of your app for mobile-friendliness, reach out to teamsubm@microsoft.com with your app details.</span></span>

## <a name="authentication"></a><span data-ttu-id="9a849-126">身份验证</span><span class="sxs-lookup"><span data-stu-id="9a849-126">Authentication</span></span>

<span data-ttu-id="9a849-127">若要在移动客户端上进行身份验证，必须将 JavaScript SDK Teams至少升级到版本 1.4.1。</span><span class="sxs-lookup"><span data-stu-id="9a849-127">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

## <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="9a849-128">低带宽和间歇性连接</span><span class="sxs-lookup"><span data-stu-id="9a849-128">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="9a849-129">移动客户端在低带宽和间歇性连接下工作。</span><span class="sxs-lookup"><span data-stu-id="9a849-129">Mobile clients function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="9a849-130">应用必须通过向用户提供上下文消息来适当地处理任何超时。</span><span class="sxs-lookup"><span data-stu-id="9a849-130">Your app must handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="9a849-131">还必须使用进度指示器为用户提供任何长时间运行的过程的反馈。</span><span class="sxs-lookup"><span data-stu-id="9a849-131">You must also use progress indicators to provide feedback to your users for any long-running processes.</span></span>

## <a name="testing-on-mobile-clients"></a><span data-ttu-id="9a849-132">在移动客户端上测试</span><span class="sxs-lookup"><span data-stu-id="9a849-132">Testing on mobile clients</span></span>

<span data-ttu-id="9a849-133">必须验证选项卡在各种大小和质量的移动设备上是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="9a849-133">You must validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="9a849-134">对于 Android 设备，可以在选项卡运行时使用 [DevTools](~/tabs/how-to/developer-tools.md) 调试选项卡。</span><span class="sxs-lookup"><span data-stu-id="9a849-134">For Android devices, you can use [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="9a849-135">建议在高性能和低性能设备（包括平板电脑）上进行测试。</span><span class="sxs-lookup"><span data-stu-id="9a849-135">It is recommended that you test on both high and low-performance devices, including a tablet.</span></span>

## <a name="distribution"></a><span data-ttu-id="9a849-136">分发</span><span class="sxs-lookup"><span data-stu-id="9a849-136">Distribution</span></span>

<span data-ttu-id="9a849-137">应用商店中列出的Teams必须经过批准，供移动使用，以在移动Teams正常运行。</span><span class="sxs-lookup"><span data-stu-id="9a849-137">Apps listed on the Teams store must be approved for mobile use to function properly in the Teams mobile client.</span></span> <span data-ttu-id="9a849-138">选项卡可用性和行为取决于你的应用是否已获得批准。</span><span class="sxs-lookup"><span data-stu-id="9a849-138">Tab availability and behavior depends on whether your app is approved.</span></span>

### <a name="apps-on-teams-store-approved-for-mobile"></a><span data-ttu-id="9a849-139">经批准Teams移动的应用商店上的应用</span><span class="sxs-lookup"><span data-stu-id="9a849-139">Apps on Teams store approved for mobile</span></span>

<span data-ttu-id="9a849-140">下表介绍了当应用在应用商店中列出并批准Teams时选项卡可用性和行为：</span><span class="sxs-lookup"><span data-stu-id="9a849-140">The following table describes tab availability and behavior when the app is listed on the Teams store and approved for mobile use:</span></span>

|<span data-ttu-id="9a849-141">功能</span><span class="sxs-lookup"><span data-stu-id="9a849-141">Capability</span></span>   |<span data-ttu-id="9a849-142">移动可用性？</span><span class="sxs-lookup"><span data-stu-id="9a849-142">Mobile availability?</span></span>   |<span data-ttu-id="9a849-143">移动行为</span><span class="sxs-lookup"><span data-stu-id="9a849-143">Mobile behavior</span></span>|
|----------|-----------|------------|
|<span data-ttu-id="9a849-144">频道</span><span class="sxs-lookup"><span data-stu-id="9a849-144">Channel</span></span> <br /> <span data-ttu-id="9a849-145">和组选项卡</span><span class="sxs-lookup"><span data-stu-id="9a849-145">and group tab</span></span>|<span data-ttu-id="9a849-146">是</span><span class="sxs-lookup"><span data-stu-id="9a849-146">Yes</span></span>|<span data-ttu-id="9a849-147">选项卡使用Teams在移动客户端中 `contentUrl` 打开。</span><span class="sxs-lookup"><span data-stu-id="9a849-147">Tab opens in the Teams mobile client using your app's `contentUrl` configuration.</span></span>|
|<span data-ttu-id="9a849-148">个人应用</span><span class="sxs-lookup"><span data-stu-id="9a849-148">Personal app</span></span>|<span data-ttu-id="9a849-149">是</span><span class="sxs-lookup"><span data-stu-id="9a849-149">Yes</span></span>|<span data-ttu-id="9a849-150">"个人应用"选项卡中的每个选项卡使用各自的Teams在移动客户端中 `contentUrl` 打开。</span><span class="sxs-lookup"><span data-stu-id="9a849-150">Each tab in the personal app tab opens in the Teams mobile client using its respective `contentUrl` configuration.</span></span>|

### <a name="apps-on-teams-store-not-approved-for-mobile"></a><span data-ttu-id="9a849-151">未批准Teams移动的应用商店上的应用</span><span class="sxs-lookup"><span data-stu-id="9a849-151">Apps on Teams store not approved for mobile</span></span>

<span data-ttu-id="9a849-152">下表介绍了当应用在应用商店中列出但Teams未批准的移动用途时选项卡可用性和行为：</span><span class="sxs-lookup"><span data-stu-id="9a849-152">The following table describes tab availability and behavior when the app is listed on the Teams store but not approved for mobile use:</span></span>

| <span data-ttu-id="9a849-153">功能</span><span class="sxs-lookup"><span data-stu-id="9a849-153">Capability</span></span> | <span data-ttu-id="9a849-154">移动可用性？</span><span class="sxs-lookup"><span data-stu-id="9a849-154">Mobile availability?</span></span> | <span data-ttu-id="9a849-155">移动行为</span><span class="sxs-lookup"><span data-stu-id="9a849-155">Mobile behavior</span></span> |
|----------|-----------|------------|
|<span data-ttu-id="9a849-156">"频道和组"选项卡</span><span class="sxs-lookup"><span data-stu-id="9a849-156">Channel and group tab</span></span>|<span data-ttu-id="9a849-157">是</span><span class="sxs-lookup"><span data-stu-id="9a849-157">Yes</span></span>|<span data-ttu-id="9a849-158">选项卡在设备的默认浏览器中打开，而不是Teams应用的配置打开，这还必须包含在源代码 `websiteUrl` 的 `setSettings()` [函数中](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="9a849-158">Tab opens in the device's default browser instead of the Teams mobile client using your app's `websiteUrl` configuration, which must also be included in your source code's `setSettings()` [function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true).</span></span> <span data-ttu-id="9a849-159">但是，用户可以在移动Teams中查看选项卡，方法为选择应用旁边的"更多"并选择"打开"，这将触发应用的 `contentUrl` 配置。</span><span class="sxs-lookup"><span data-stu-id="9a849-159">However, users can view the tab in the Teams mobile client by selecting **More** next to the app and choosing **Open**, which triggers your app’s `contentUrl` configuration.</span></span>|
|<span data-ttu-id="9a849-160">个人应用</span><span class="sxs-lookup"><span data-stu-id="9a849-160">Personal app</span></span>|<span data-ttu-id="9a849-161">不支持</span><span class="sxs-lookup"><span data-stu-id="9a849-161">No</span></span>|<span data-ttu-id="9a849-162">不适用</span><span class="sxs-lookup"><span data-stu-id="9a849-162">Not applicable</span></span>|

### <a name="apps-not-on-teams-store"></a><span data-ttu-id="9a849-163">不在应用商店Teams应用</span><span class="sxs-lookup"><span data-stu-id="9a849-163">Apps not on Teams store</span></span>

<span data-ttu-id="9a849-164">如果要将应用旁加载或发布到组织的应用程序目录，选项卡行为Teams Microsoft 批准的移动应用商店应用的行为相同。</span><span class="sxs-lookup"><span data-stu-id="9a849-164">If you are sideloading your app or publishing to an organization's app catalog, tab behavior is the same as Teams store apps approved by Microsoft for mobile.</span></span>

## <a name="see-also"></a><span data-ttu-id="9a849-165">另请参阅</span><span class="sxs-lookup"><span data-stu-id="9a849-165">See also</span></span>

* [<span data-ttu-id="9a849-166">选项卡设计指南</span><span class="sxs-lookup"><span data-stu-id="9a849-166">Tab design guidelines</span></span>](~/tabs/design/tabs.md)
* [<span data-ttu-id="9a849-167">Teams选项卡</span><span class="sxs-lookup"><span data-stu-id="9a849-167">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="9a849-168">创建个人选项卡</span><span class="sxs-lookup"><span data-stu-id="9a849-168">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="9a849-169">创建频道或组选项卡</span><span class="sxs-lookup"><span data-stu-id="9a849-169">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)

## <a name="next-step"></a><span data-ttu-id="9a849-170">后续步骤</span><span class="sxs-lookup"><span data-stu-id="9a849-170">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9a849-171">获取选项卡的上下文</span><span class="sxs-lookup"><span data-stu-id="9a849-171">Get context for your tab</span></span>](~/tabs/how-to/access-teams-context.md)
