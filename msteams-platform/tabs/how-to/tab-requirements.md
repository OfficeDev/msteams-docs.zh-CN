---
title: 了解选项卡要求
author: laujan
description: 每个选项卡Microsoft Teams都必须遵守这些要求。
keywords: teams 选项卡组频道可配置
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: a46a80401b29b5436807c9a5b94580beca3786f0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566661"
---
# <a name="tab-requirements"></a><span data-ttu-id="d20f6-104">选项卡要求</span><span class="sxs-lookup"><span data-stu-id="d20f6-104">Tab requirements</span></span>

<span data-ttu-id="d20f6-105">Teams选项卡必须遵守以下要求：</span><span class="sxs-lookup"><span data-stu-id="d20f6-105">Teams tabs must adhere to the following requirements:</span></span>

* <span data-ttu-id="d20f6-106">必须允许通过 X-Frame-Options 和/或 Content-Security-Policy HTTP 响应标头在 iFrame 中提供选项卡页。</span><span class="sxs-lookup"><span data-stu-id="d20f6-106">You must allow your tab pages to be served in an iFrame, via X-Frame-Options and/or Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="d20f6-107">设置标头： `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="d20f6-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="d20f6-108">对于Internet Explorer 11 兼容性，也 `X-Content-Security-Policy` 进行设置。</span><span class="sxs-lookup"><span data-stu-id="d20f6-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy` as well.</span></span>
  * <span data-ttu-id="d20f6-109">或者，设置标头 `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。</span><span class="sxs-lookup"><span data-stu-id="d20f6-109">Alternatively, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="d20f6-110">此标头已弃用，但仍受大多数浏览器支持。</span><span class="sxs-lookup"><span data-stu-id="d20f6-110">This header is deprecated but still respected by most browsers.</span></span>
* <span data-ttu-id="d20f6-111">通常，作为防止点击攻击的一种安全措施，登录页不会呈现在 iFrame 中。</span><span class="sxs-lookup"><span data-stu-id="d20f6-111">Typically, as a safeguard against click-jacking, login pages don't render in iFrames.</span></span> <span data-ttu-id="d20f6-112">因此，身份验证逻辑需使用重定向方法。</span><span class="sxs-lookup"><span data-stu-id="d20f6-112">Therefore, your authentication logic needs to use a method other than redirect.</span></span> <span data-ttu-id="d20f6-113">例如，使用基于令牌或基于 Cookie 的身份验证。</span><span class="sxs-lookup"><span data-stu-id="d20f6-113">For example, use token-based or cookie-based authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="d20f6-114">Chrome 80 计划于 2020 年初发布，引入了新的 Cookie 值，并默认实施 Cookie 策略。</span><span class="sxs-lookup"><span data-stu-id="d20f6-114">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="d20f6-115">建议设置 Cookie 的预定用途，而不是依赖默认浏览器行为。</span><span class="sxs-lookup"><span data-stu-id="d20f6-115">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="d20f6-116">有关详细信息，请参阅 [SameSite cookie attribute (2020 update) ](../../resources/samesite-cookie-update.md)。</span><span class="sxs-lookup"><span data-stu-id="d20f6-116">For more information, see [SameSite cookie attribute (2020 update)](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="d20f6-117">浏览器遵守同源策略限制，该限制阻止网页向与提供网页的域不同的域提出请求。</span><span class="sxs-lookup"><span data-stu-id="d20f6-117">Browsers adhere to a same-origin policy restriction that prevents a webpage from making requests to a different domain than the one that served a web page.</span></span> <span data-ttu-id="d20f6-118">但是，您可能需要将配置或内容页面重定向到另一个域或子域。</span><span class="sxs-lookup"><span data-stu-id="d20f6-118">However, you may need to redirect the configuration or content page to a another domain or subdomain.</span></span> <span data-ttu-id="d20f6-119">当加载或与选项卡通信时，跨域导航逻辑应允许 Teams 客户端针对应用程序清单中的静态 validDomains 列表验证源。</span><span class="sxs-lookup"><span data-stu-id="d20f6-119">Your cross-domain navigation logic should allow the Teams client to validate the origin against a static validDomains list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="d20f6-120">若要创建无缝体验，应基于客户端的主题、设计和意图Teams设置选项卡样式。</span><span class="sxs-lookup"><span data-stu-id="d20f6-120">To create a seamless experience, you should style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="d20f6-121">通常，当构建选项卡以解决特定需求并专注于一小组任务或与选项卡的通道位置相关的数据子集时，选项卡效果最佳。</span><span class="sxs-lookup"><span data-stu-id="d20f6-121">Typically, tabs work best when they're built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="d20f6-122">在内容页中，添加对使用脚本标记[Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)的引用。</span><span class="sxs-lookup"><span data-stu-id="d20f6-122">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="d20f6-123">加载页面后，调用 `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="d20f6-123">Following your page load, make a call to `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="d20f6-124">如果未显示，则不显示您的页面。</span><span class="sxs-lookup"><span data-stu-id="d20f6-124">Your page will not be displayed if you do not.</span></span>

* <span data-ttu-id="d20f6-125">若要在移动客户端上进行身份验证，必须将 JavaScript SDK Teams至少升级到版本 1.4.1。</span><span class="sxs-lookup"><span data-stu-id="d20f6-125">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

* <span data-ttu-id="d20f6-126">如果您选择让频道或组选项卡显示在Teams客户端上，则配置必须具有 `setSettings()` `websiteUrl` 属性的值。</span><span class="sxs-lookup"><span data-stu-id="d20f6-126">If you choose to have your channel or group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span>

## <a name="next-step"></a><span data-ttu-id="d20f6-127">后续步骤</span><span class="sxs-lookup"><span data-stu-id="d20f6-127">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d20f6-128">使用 Yeoman 生成器和 Node.js 的 Yeoman 生成器创建自定义个人Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d20f6-128">Create a custom personal tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>](~/tabs/quickstarts/create-personal-tab-node-yeoman.md)