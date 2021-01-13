---
title: 了解选项卡要求
author: laujan
description: Microsoft Teams 中的每个选项卡都必须遵守这些要求。
keywords: teams 选项卡组频道可配置
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 1f5a3eaa8ca16878944288d5dbbfa78cfe9fa3ce
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797911"
---
# <a name="tab-requirements"></a><span data-ttu-id="64b4e-104">选项卡要求</span><span class="sxs-lookup"><span data-stu-id="64b4e-104">Tab requirements</span></span>

<span data-ttu-id="64b4e-105">Teams 选项卡必须遵守以下要求：</span><span class="sxs-lookup"><span data-stu-id="64b4e-105">Teams tabs must adhere to the following requirements:</span></span>

* <span data-ttu-id="64b4e-106">必须允许通过 X-Frame-Options 和/或 Content-Security-Policy HTTP 响应标头在 iFrame 中提供选项卡页。</span><span class="sxs-lookup"><span data-stu-id="64b4e-106">You must allow your tab pages to be served in an iFrame, via X-Frame-Options and/or Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="64b4e-107">设置标头： `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="64b4e-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="64b4e-108">对于Internet Explorer 11 兼容性，也 `X-Content-Security-Policy` 进行设置。</span><span class="sxs-lookup"><span data-stu-id="64b4e-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy` as well.</span></span>
  * <span data-ttu-id="64b4e-109">或者，设置标头 `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。</span><span class="sxs-lookup"><span data-stu-id="64b4e-109">Alternatively, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="64b4e-110">此标头已弃用，但仍受到大多数浏览器的遵守。</span><span class="sxs-lookup"><span data-stu-id="64b4e-110">This header is deprecated but still respected by most browsers.</span></span>
* <span data-ttu-id="64b4e-111">通常，作为防止点击攻击的安全措施，登录页不会呈现在 iFrame 中。</span><span class="sxs-lookup"><span data-stu-id="64b4e-111">Typically, as a safeguard against click-jacking, login pages don't render in iFrames.</span></span> <span data-ttu-id="64b4e-112">因此，身份验证逻辑需要使用重定向方法 (例如，使用基于令牌或基于 Cookie 的身份验证) 。</span><span class="sxs-lookup"><span data-stu-id="64b4e-112">Therefore, your authentication logic needs to use a method other than redirect (e.g., use token-based or cookie-based authentication).</span></span>

> [!NOTE]
> <span data-ttu-id="64b4e-113">计划于 2020 年初发布的 Chrome 80 引入了新的 Cookie 值，并默认实施 Cookie 策略。</span><span class="sxs-lookup"><span data-stu-id="64b4e-113">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="64b4e-114">建议您设置 Cookie 的预定用途，而不是依赖默认浏览器行为。</span><span class="sxs-lookup"><span data-stu-id="64b4e-114">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="64b4e-115">*请参阅* [SameSite cookie 属性 (2020 update) 。](../../resources/samesite-cookie-update.md)</span><span class="sxs-lookup"><span data-stu-id="64b4e-115">*See* [SameSite cookie attribute (2020 update)](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="64b4e-116">浏览器遵守同源策略限制，该限制阻止网页向与提供网页的网页不同的域提出请求。</span><span class="sxs-lookup"><span data-stu-id="64b4e-116">Browsers adhere to a same-origin policy restriction that prevents a webpage from making requests to a different domain than the one that served a web page.</span></span> <span data-ttu-id="64b4e-117">但是，您可能需要将配置或内容页重定向到另一个域或子域。</span><span class="sxs-lookup"><span data-stu-id="64b4e-117">However, you may need to redirect the configuration or content page to a another domain or subdomain.</span></span> <span data-ttu-id="64b4e-118">在加载或与选项卡通信时，跨域导航逻辑应允许 Teams 客户端根据应用清单中的静态 validDomains 列表验证源。</span><span class="sxs-lookup"><span data-stu-id="64b4e-118">Your cross-domain navigation logic should allow the Teams client to validate the origin against a static validDomains list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="64b4e-119">若要创建无缝体验，你应该根据 Teams 客户端的主题、设计和意图设置选项卡的样式。</span><span class="sxs-lookup"><span data-stu-id="64b4e-119">To create a seamless experience, you should style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="64b4e-120">通常，当构建选项卡以解决特定需求并专注于与选项卡的通道位置相关的一小组任务或数据子集时，选项卡最运行。</span><span class="sxs-lookup"><span data-stu-id="64b4e-120">Typically, tabs work best when they're built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="64b4e-121">在内容页中，使用脚本标记添加对 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 的引用。</span><span class="sxs-lookup"><span data-stu-id="64b4e-121">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="64b4e-122">加载页面后，调用 `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="64b4e-122">Following your page load, make a call to `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="64b4e-123">如果不显示页面，则不显示页面。</span><span class="sxs-lookup"><span data-stu-id="64b4e-123">Your page will not be displayed if you do not.</span></span>
