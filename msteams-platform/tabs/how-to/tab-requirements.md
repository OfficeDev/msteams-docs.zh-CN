---
title: 了解选项卡要求
author: laujan
description: Microsoft Teams 中的每个选项卡都必须遵守这些要求。
keywords: teams 选项卡组频道可配置
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8013c10050ae81ada0f2a27576cd43077eafe1e0
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019578"
---
# <a name="tab-requirements"></a><span data-ttu-id="38e15-104">选项卡要求</span><span class="sxs-lookup"><span data-stu-id="38e15-104">Tab requirements</span></span>

<span data-ttu-id="38e15-105">Teams 选项卡必须遵循以下要求：</span><span class="sxs-lookup"><span data-stu-id="38e15-105">Teams tabs must adhere to the following requirements:</span></span>

* <span data-ttu-id="38e15-106">必须允许通过 X-Frame-Options 和/或 Content-Security-Policy HTTP 响应标头在 iFrame 中提供选项卡页。</span><span class="sxs-lookup"><span data-stu-id="38e15-106">You must allow your tab pages to be served in an iFrame, via X-Frame-Options and/or Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="38e15-107">设置标头： `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="38e15-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="38e15-108">对于Internet Explorer 11 兼容性，也 `X-Content-Security-Policy` 进行设置。</span><span class="sxs-lookup"><span data-stu-id="38e15-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy` as well.</span></span>
  * <span data-ttu-id="38e15-109">或者，设置标头 `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。</span><span class="sxs-lookup"><span data-stu-id="38e15-109">Alternatively, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="38e15-110">此标头已弃用，但仍受大多数浏览器支持。</span><span class="sxs-lookup"><span data-stu-id="38e15-110">This header is deprecated but still respected by most browsers.</span></span>
* <span data-ttu-id="38e15-111">通常，作为防止点击攻击的一种安全措施，登录页不会呈现在 iFrame 中。</span><span class="sxs-lookup"><span data-stu-id="38e15-111">Typically, as a safeguard against click-jacking, login pages don't render in iFrames.</span></span> <span data-ttu-id="38e15-112">因此，身份验证逻辑需要使用重定向策略 (，例如，使用基于令牌或基于 Cookie 的身份验证) 。</span><span class="sxs-lookup"><span data-stu-id="38e15-112">Therefore, your authentication logic needs to use a method other than redirect (e.g., use token-based or cookie-based authentication).</span></span>

> [!NOTE]
> <span data-ttu-id="38e15-113">Chrome 80 计划于 2020 年初发布，引入了新的 Cookie 值，并默认实施 Cookie 策略。</span><span class="sxs-lookup"><span data-stu-id="38e15-113">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="38e15-114">建议设置 Cookie 的预定用途，而不是依赖默认浏览器行为。</span><span class="sxs-lookup"><span data-stu-id="38e15-114">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="38e15-115">*请参阅* [SameSite cookie attribute (2020 update)](../../resources/samesite-cookie-update.md)。</span><span class="sxs-lookup"><span data-stu-id="38e15-115">*See* [SameSite cookie attribute (2020 update)](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="38e15-116">浏览器遵守同源策略限制，该限制阻止网页向与提供网页的域不同的域提出请求。</span><span class="sxs-lookup"><span data-stu-id="38e15-116">Browsers adhere to a same-origin policy restriction that prevents a webpage from making requests to a different domain than the one that served a web page.</span></span> <span data-ttu-id="38e15-117">但是，您可能需要将配置或内容页面重定向到另一个域或子域。</span><span class="sxs-lookup"><span data-stu-id="38e15-117">However, you may need to redirect the configuration or content page to a another domain or subdomain.</span></span> <span data-ttu-id="38e15-118">当加载或与选项卡通信时，跨域导航逻辑应允许 Teams 客户端针对应用清单中的静态 validDomains 列表验证源。</span><span class="sxs-lookup"><span data-stu-id="38e15-118">Your cross-domain navigation logic should allow the Teams client to validate the origin against a static validDomains list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="38e15-119">若要创建无缝体验，你应基于 Teams 客户端的主题、设计和意图设置选项卡的样式。</span><span class="sxs-lookup"><span data-stu-id="38e15-119">To create a seamless experience, you should style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="38e15-120">通常，当构建选项卡以解决特定需求并专注于一小组任务或与选项卡的通道位置相关的数据子集时，选项卡效果最佳。</span><span class="sxs-lookup"><span data-stu-id="38e15-120">Typically, tabs work best when they're built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="38e15-121">在内容页中，使用脚本标记添加 [对 Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 的引用。</span><span class="sxs-lookup"><span data-stu-id="38e15-121">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="38e15-122">加载页面后，调用 `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="38e15-122">Following your page load, make a call to `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="38e15-123">如果未显示，则不显示您的页面。</span><span class="sxs-lookup"><span data-stu-id="38e15-123">Your page will not be displayed if you do not.</span></span>

* <span data-ttu-id="38e15-124">若要在移动客户端上进行身份验证，必须将 Teams JavaScript SDK 至少升级到版本 1.4.1。</span><span class="sxs-lookup"><span data-stu-id="38e15-124">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

* <span data-ttu-id="38e15-125">如果选择让频道或组选项卡显示在 Teams 移动客户端上，则配置 `setSettings()` 必须具有 `websiteUrl` 属性的值。</span><span class="sxs-lookup"><span data-stu-id="38e15-125">If you choose to have your channel or group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span>