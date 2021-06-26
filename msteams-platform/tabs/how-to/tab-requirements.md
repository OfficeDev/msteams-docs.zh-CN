---
title: 先决条件
author: surbhigupta
description: 每个选项卡Microsoft Teams都必须遵守这些要求。
keywords: teams 选项卡组频道可配置
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b54fc7235132a9253f6eecc62417f786bf4aa45c
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140185"
---
# <a name="prerequisites"></a><span data-ttu-id="c3224-104">先决条件</span><span class="sxs-lookup"><span data-stu-id="c3224-104">Prerequisites</span></span>

<span data-ttu-id="c3224-105">Teams选项卡必须遵循以下先决条件：</span><span class="sxs-lookup"><span data-stu-id="c3224-105">Teams tabs must adhere to the following prerequisites:</span></span>

* <span data-ttu-id="c3224-106">必须允许选项卡页使用 X-Frame-Options 和 Content-Security-Policy HTTP 响应标头显示在 iFrame 中。</span><span class="sxs-lookup"><span data-stu-id="c3224-106">You must allow your tab pages to be shown in an iFrame, using X-Frame-Options and Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="c3224-107">设置标头： `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="c3224-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="c3224-108">对于Internet Explorer 11 兼容性，请设置 `X-Content-Security-Policy` 。</span><span class="sxs-lookup"><span data-stu-id="c3224-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy`.</span></span>
  * <span data-ttu-id="c3224-109">或者，设置标头 `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。</span><span class="sxs-lookup"><span data-stu-id="c3224-109">Alternately, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="c3224-110">此标头已弃用，但仍被大多数浏览器接受。</span><span class="sxs-lookup"><span data-stu-id="c3224-110">This header is deprecated but still accepted by most browsers.</span></span>

* <span data-ttu-id="c3224-111">通常，作为防止点击劫持的安全措施，登录页不会呈现在 iFrame 中。</span><span class="sxs-lookup"><span data-stu-id="c3224-111">Typically, as a safeguard against clickjacking, login pages do not render in iFrames.</span></span> <span data-ttu-id="c3224-112">身份验证逻辑需使用重定向方法。</span><span class="sxs-lookup"><span data-stu-id="c3224-112">Your authentication logic needs to use a method other than redirect.</span></span> <span data-ttu-id="c3224-113">例如，使用基于令牌或基于 Cookie 的身份验证。</span><span class="sxs-lookup"><span data-stu-id="c3224-113">For example, use token-based or cookie-based authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c3224-114">Chrome 80 计划于 2020 年初发布，引入了新的 Cookie 值，并默认实施 Cookie 策略。</span><span class="sxs-lookup"><span data-stu-id="c3224-114">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="c3224-115">建议您设置 Cookie 的预定用途，而不是依赖默认浏览器行为。</span><span class="sxs-lookup"><span data-stu-id="c3224-115">It is recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="c3224-116">有关详细信息，请参阅 [SameSite cookie 属性](../../resources/samesite-cookie-update.md)。</span><span class="sxs-lookup"><span data-stu-id="c3224-116">For more information, see [SameSite cookie attribute](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="c3224-117">浏览器遵守同源策略限制。</span><span class="sxs-lookup"><span data-stu-id="c3224-117">Browsers adhere to a same-origin policy restriction.</span></span> <span data-ttu-id="c3224-118">它会阻止网页向与所提供网页不同的域提出请求。</span><span class="sxs-lookup"><span data-stu-id="c3224-118">It prevents webpages from making requests to different domains than the served web page.</span></span> <span data-ttu-id="c3224-119">但是，您可以将配置或内容页重定向到另一个域或子域。</span><span class="sxs-lookup"><span data-stu-id="c3224-119">However, you can redirect the configuration or content page to another domain or subdomain.</span></span> <span data-ttu-id="c3224-120">当加载或与选项卡通信时，跨域导航逻辑Teams客户端根据应用清单中的静态列表验证 `validDomains` 源。</span><span class="sxs-lookup"><span data-stu-id="c3224-120">Your cross-domain navigation logic must allow the Teams client to validate the origin against a static `validDomains` list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="c3224-121">您必须基于客户端的主题、Teams设计及意图设置选项卡的样式。</span><span class="sxs-lookup"><span data-stu-id="c3224-121">You must style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="c3224-122">通常，当选项卡专为满足特定需求而构建，并且侧重于一小组任务或与选项卡的通道位置相关的数据子集时，选项卡运行效果最佳。</span><span class="sxs-lookup"><span data-stu-id="c3224-122">Typically, tabs work best when they are built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="c3224-123">在内容页中，添加对使用脚本标记[Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)的引用。</span><span class="sxs-lookup"><span data-stu-id="c3224-123">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="c3224-124">加载页面后，调用 `microsoftTeams.initialize()` ，否则不显示页面。</span><span class="sxs-lookup"><span data-stu-id="c3224-124">After your page loads, make a call to `microsoftTeams.initialize()`, otherwise your page is not displayed.</span></span>

* <span data-ttu-id="c3224-125">若要在移动客户端上进行身份验证，必须将 Teams JavaScript SDK 升级到至少版本 1.4.1。</span><span class="sxs-lookup"><span data-stu-id="c3224-125">For authentication to work on mobile clients, you must upgrade Teams JavaScript SDK to at least version 1.4.1.</span></span>

* <span data-ttu-id="c3224-126">如果您选择让频道或组选项卡显示在Teams客户端上，则配置必须具有 `setSettings()` `websiteUrl` 属性的值。</span><span class="sxs-lookup"><span data-stu-id="c3224-126">If you choose to have your channel or group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span>

* <span data-ttu-id="c3224-127">MS Teams 选项卡不支持加载使用自签名证书的 Intranet 网站。</span><span class="sxs-lookup"><span data-stu-id="c3224-127">MS Teams tab does not support the ability to load intranet websites that use self-signed certificates.</span></span>

## <a name="see-also"></a><span data-ttu-id="c3224-128">另请参阅</span><span class="sxs-lookup"><span data-stu-id="c3224-128">See also</span></span>

* [<span data-ttu-id="c3224-129">Teams选项卡</span><span class="sxs-lookup"><span data-stu-id="c3224-129">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="c3224-130">创建频道或组选项卡</span><span class="sxs-lookup"><span data-stu-id="c3224-130">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="c3224-131">创建内容页</span><span class="sxs-lookup"><span data-stu-id="c3224-131">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="c3224-132">创建配置页</span><span class="sxs-lookup"><span data-stu-id="c3224-132">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [<span data-ttu-id="c3224-133">为选项卡创建删除页</span><span class="sxs-lookup"><span data-stu-id="c3224-133">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
* [<span data-ttu-id="c3224-134">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="c3224-134">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="c3224-135">获取选项卡的上下文</span><span class="sxs-lookup"><span data-stu-id="c3224-135">Get context for your tab</span></span>](~/tabs/how-to/access-teams-context.md)
* [<span data-ttu-id="c3224-136">具有自适应卡片的生成选项卡</span><span class="sxs-lookup"><span data-stu-id="c3224-136">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="c3224-137">选项卡链接展开和阶段视图</span><span class="sxs-lookup"><span data-stu-id="c3224-137">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)
* [<span data-ttu-id="c3224-138">创建对话选项卡</span><span class="sxs-lookup"><span data-stu-id="c3224-138">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)
* [<span data-ttu-id="c3224-139">选项卡边距更改</span><span class="sxs-lookup"><span data-stu-id="c3224-139">Tab margin changes</span></span>](~/resources/removing-tab-margins.md)

## <a name="next-step"></a><span data-ttu-id="c3224-140">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c3224-140">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c3224-141">创建个人选项卡</span><span class="sxs-lookup"><span data-stu-id="c3224-141">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
