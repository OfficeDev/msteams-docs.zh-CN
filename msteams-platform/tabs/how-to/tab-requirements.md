---
title: 选项卡要求
author: laujan
description: 每个选项卡Microsoft Teams都必须遵守这些要求。
keywords: teams 选项卡组频道可配置
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 50d529697a80ca9ba78921009405f18fa021e802
ms.sourcegitcommit: 45c66faef8145abb903ef7118b9fa914c12aba2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/03/2021
ms.locfileid: "52736759"
---
# <a name="tab-requirements"></a><span data-ttu-id="cd0d8-104">选项卡要求</span><span class="sxs-lookup"><span data-stu-id="cd0d8-104">Tab requirements</span></span>

<span data-ttu-id="cd0d8-105">Teams选项卡必须遵守以下要求：</span><span class="sxs-lookup"><span data-stu-id="cd0d8-105">Teams tabs must adhere to the following requirements:</span></span>

* <span data-ttu-id="cd0d8-106">你必须允许使用 X-Frame-Options 和 Content-Security-Policy HTTP 响应标头在 iFrame 中提供选项卡页。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-106">You must allow your tab pages to be served in an iFrame, using X-Frame-Options and Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="cd0d8-107">设置标头： `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="cd0d8-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="cd0d8-108">对于Internet Explorer 11 兼容性，请设置 `X-Content-Security-Policy` 。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy`.</span></span>
  * <span data-ttu-id="cd0d8-109">或者，设置标头 `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-109">Alternately, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="cd0d8-110">此标头已弃用，但仍被大多数浏览器接受。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-110">This header is deprecated but still accepted by most browsers.</span></span>
* <span data-ttu-id="cd0d8-111">通常，作为防止点击攻击的一种安全措施，登录页不会呈现在 iFrame 中。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-111">Typically, as a safeguard against click-jacking, login pages do not render in iFrames.</span></span> <span data-ttu-id="cd0d8-112">身份验证逻辑需使用重定向方法。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-112">Your authentication logic needs to use a method other than redirect.</span></span> <span data-ttu-id="cd0d8-113">例如，使用基于令牌或基于 Cookie 的身份验证。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-113">For example, use token-based or cookie-based authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cd0d8-114">Chrome 80 计划于 2020 年初发布，引入了新的 Cookie 值，并默认实施 Cookie 策略。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-114">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="cd0d8-115">建议您设置 Cookie 的预定用途，而不是依赖默认浏览器行为。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-115">It is recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="cd0d8-116">有关详细信息，请参阅 [SameSite cookie attribute 2020 update](../../resources/samesite-cookie-update.md)。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-116">For more information, see [SameSite cookie attribute 2020 update](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="cd0d8-117">浏览器遵守同源策略限制，该限制阻止网页向与提供网页的域不同的域提出请求。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-117">Browsers adhere to a same-origin policy restriction that prevents a webpage from making requests to a different domain than the one that served a web page.</span></span> <span data-ttu-id="cd0d8-118">但是，您可以将配置或内容页重定向到另一个域或子域。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-118">However, you can redirect the configuration or content page to another domain or subdomain.</span></span> <span data-ttu-id="cd0d8-119">当加载或与选项卡通信时，跨域导航逻辑必须允许 Teams 客户端针对应用程序清单中的静态 validDomains 列表验证源。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-119">Your cross-domain navigation logic must allow the Teams client to validate the origin against a static validDomains list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="cd0d8-120">若要创建无缝体验，你必须根据客户端的主题、设计和意图Teams设置选项卡的样式。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-120">To create a seamless experience, you must style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="cd0d8-121">通常，当选项卡专为满足特定需求而构建，并且侧重于一小组任务或与选项卡的通道位置相关的数据子集时，选项卡运行效果最佳。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-121">Typically, tabs work best when they are built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="cd0d8-122">在内容页中，添加对使用脚本标记[Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)的引用。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-122">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="cd0d8-123">加载页面后，调用 `microsoftTeams.initialize()` ，否则不显示页面。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-123">After your page loads, make a call to `microsoftTeams.initialize()`, otherwise your page is not displayed.</span></span>

* <span data-ttu-id="cd0d8-124">若要在移动客户端上进行身份验证，必须将 JavaScript SDK Teams至少升级到版本 1.4.1。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-124">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

* <span data-ttu-id="cd0d8-125">如果您选择让频道或组选项卡显示在Teams客户端上，则配置必须具有 `setSettings()` `websiteUrl` 属性的值。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-125">If you choose to have your channel or group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span>

* <span data-ttu-id="cd0d8-126">MS Teams 选项卡不支持加载使用自签名证书的 Intranet 网站。</span><span class="sxs-lookup"><span data-stu-id="cd0d8-126">MS Teams tab does not support the ability to load intranet websites that use self-signed certificates.</span></span>

## <a name="next-step"></a><span data-ttu-id="cd0d8-127">后续步骤</span><span class="sxs-lookup"><span data-stu-id="cd0d8-127">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cd0d8-128">使用 Yeoman 生成器和 Node.js 的 Yeoman 生成器创建自定义个人Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="cd0d8-128">Create a custom personal tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>](~/tabs/quickstarts/create-personal-tab-node-yeoman.md)
