---
title: 使用自定义选项卡扩展团队应用程序
author: laujan
description: 如何使用应用程序 Studio 或手动为 Microsoft 团队创建选项卡。
keywords: 团队选项卡组频道可配置
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 78077a19c8597826ca6d10a7c1c6240fae3f3fbd
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "48209716"
---
# <a name="extend-your-teams-app-with-a-custom-tab"></a><span data-ttu-id="c7078-104">使用自定义选项卡扩展团队应用程序</span><span class="sxs-lookup"><span data-stu-id="c7078-104">Extend your Teams app with a custom tab</span></span>

<span data-ttu-id="c7078-105">自定义选项卡使您能够为您承载于频道、组聊天和个人用户的 web 内容提供服务。</span><span class="sxs-lookup"><span data-stu-id="c7078-105">Custom tabs allow you to serve web content that you host to your channel, group chat, and personal users.</span></span> <span data-ttu-id="c7078-106">在较高级别，需要完成以下步骤以创建选项卡：</span><span class="sxs-lookup"><span data-stu-id="c7078-106">At a high level, you'll need to complete the following steps to create a tab:</span></span>

1. <span data-ttu-id="c7078-107">准备开发环境。</span><span class="sxs-lookup"><span data-stu-id="c7078-107">Prepare your development environment.</span></span>
1. <span data-ttu-id="c7078-108"> (s) 创建页面。</span><span class="sxs-lookup"><span data-stu-id="c7078-108">Create your page(s).</span></span>
1. <span data-ttu-id="c7078-109">承载你的应用服务。</span><span class="sxs-lookup"><span data-stu-id="c7078-109">Host your app service.</span></span>
1. <span data-ttu-id="c7078-110">创建您的应用程序包并上传到 Microsoft 团队。</span><span class="sxs-lookup"><span data-stu-id="c7078-110">Create your app package and upload to Microsoft Teams.</span></span>

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-pages"></a><span data-ttu-id="c7078-111"> (s) 创建页面</span><span class="sxs-lookup"><span data-stu-id="c7078-111">Create your page(s)</span></span>

<span data-ttu-id="c7078-112">无论您是在个人还是频道/组作用域中提供选项卡，它都将包含一个或多个您承载的 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="c7078-112">Whether you present your tab within the personal or channel/group scope, it will consist of one or more HTML pages that you host.</span></span> <span data-ttu-id="c7078-113">包含个人作用域的选项卡由单个内容页面组成，而具有频道或组作用域的选项卡将需要配置页面，该页面将根据安装时的用户输入设置内容页面的 URL。</span><span class="sxs-lookup"><span data-stu-id="c7078-113">Tabs with a personal scope consist of a single content page, while tabs with a channel or group scope will require a configuration page that sets the URL of the content page based on user input at the time of installation.</span></span>

<span data-ttu-id="c7078-114">有三种类型的选项卡页。</span><span class="sxs-lookup"><span data-stu-id="c7078-114">There are three types of tab pages.</span></span> <span data-ttu-id="c7078-115">有关创建它们的完整详细信息，请参阅相应的文档页面。</span><span class="sxs-lookup"><span data-stu-id="c7078-115">See the corresponding documentation page for full details on creating them.</span></span>

1. <span data-ttu-id="c7078-116">[内容页](~/tabs/how-to/create-tab-pages/content-page.md)，在选项卡中显示的页面。</span><span class="sxs-lookup"><span data-stu-id="c7078-116">[Content page](~/tabs/how-to/create-tab-pages/content-page.md), the page displayed in a tab.</span></span>
1. <span data-ttu-id="c7078-117">[配置页面](~/tabs/how-to/create-tab-pages/configuration-page.md)，用于设置或更新内容页面 URL 的页面，并将其添加到频道/组选项卡。</span><span class="sxs-lookup"><span data-stu-id="c7078-117">[Configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md), the page used to set or update the content page URL, and add it to a channel/group tab.</span></span>
1. <span data-ttu-id="c7078-118">删除[页面](~/tabs/how-to/create-tab-pages/removal-page.md)，删除频道/组选项卡时显示的可选页面。</span><span class="sxs-lookup"><span data-stu-id="c7078-118">[Removal page](~/tabs/how-to/create-tab-pages/removal-page.md), an optional page that is displayed when a channel/group tab is removed.</span></span>

### <a name="tab-requirements"></a><span data-ttu-id="c7078-119">选项卡要求</span><span class="sxs-lookup"><span data-stu-id="c7078-119">Tab requirements</span></span>

<span data-ttu-id="c7078-120">无论页面的类型如何，您都需要遵循以下要求：</span><span class="sxs-lookup"><span data-stu-id="c7078-120">Regardless of the type of page, you're tab will need to adhere to the following requirements:</span></span>

* <span data-ttu-id="c7078-121">您必须允许通过 X 框架选项和/或内容安全策略 HTTP 响应标头在 IFrame 中提供页面。</span><span class="sxs-lookup"><span data-stu-id="c7078-121">You must allow your pages to be served in an IFrame, via X-Frame-Options and/or Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="c7078-122">设置标头： `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="c7078-122">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>        
  * <span data-ttu-id="c7078-123">对于 Internet Explorer 11 兼容性， `X-Content-Security-Policy` 也设置。</span><span class="sxs-lookup"><span data-stu-id="c7078-123">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy` as well.</span></span>    
  * <span data-ttu-id="c7078-124">或者，设置标头 `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` 。</span><span class="sxs-lookup"><span data-stu-id="c7078-124">Alternatively, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="c7078-125">此标头已弃用，但仍受大多数浏览器的考虑。</span><span class="sxs-lookup"><span data-stu-id="c7078-125">This header is deprecated but still respected by most browsers.</span></span>
* <span data-ttu-id="c7078-126">通常，作为针对 jacking 的安全措施，登录页面不会呈现在 Iframe 中。</span><span class="sxs-lookup"><span data-stu-id="c7078-126">Typically, as a safeguard against click-jacking, login pages don't render in IFrames.</span></span> <span data-ttu-id="c7078-127">因此，身份验证逻辑需要使用重定向 (以外的方法，例如，使用基于令牌的身份验证或基于 cookie 的身份验证) 。</span><span class="sxs-lookup"><span data-stu-id="c7078-127">Therefore, your authentication logic needs to use a method other than redirect (e.g., use token-based or cookie-based authentication).</span></span>

> [!NOTE]
> <span data-ttu-id="c7078-128">Chrome 80，安排在早期2020中发布，默认引入新的 cookie 值并强加 cookie 策略。</span><span class="sxs-lookup"><span data-stu-id="c7078-128">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="c7078-129">建议您为 cookie 设置预期用途，而不是依赖于默认浏览器行为。</span><span class="sxs-lookup"><span data-stu-id="c7078-129">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="c7078-130">*请参阅* [SameSite cookie 属性 (2020 update) ](../../resources/samesite-cookie-update.md)。</span><span class="sxs-lookup"><span data-stu-id="c7078-130">*See* [SameSite cookie attribute (2020 update)](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="c7078-131">浏览器遵循同一个源策略限制，以防止网页发出请求，而不是为 web 页提供服务的其他域。</span><span class="sxs-lookup"><span data-stu-id="c7078-131">Browsers adhere to a same-origin policy restriction that prevents a webpage from making requests to a different domain than the one that served a web page.</span></span> <span data-ttu-id="c7078-132">但是，您可能需要将配置或内容页面重定向到另一个域或子域。</span><span class="sxs-lookup"><span data-stu-id="c7078-132">However, you may need to redirect the configuration or content page to a another domain or subdomain.</span></span> <span data-ttu-id="c7078-133">您的跨域导航逻辑应允许团队客户端在加载或与选项卡通信时，针对应用程序清单中的静态 validDomains 列表验证源。</span><span class="sxs-lookup"><span data-stu-id="c7078-133">Your cross-domain navigation logic should allow the Teams client to validate the origin against a static validDomains list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="c7078-134">若要创建无缝体验，应根据团队客户端的主题、设计和意图来设计选项卡的样式。</span><span class="sxs-lookup"><span data-stu-id="c7078-134">To create a seamless experience, you should style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="c7078-135">通常，在构建以满足特定需求并将重点放在一小部分任务或与选项卡的频道位置相关的数据子集时，选项卡的工作效果最佳。</span><span class="sxs-lookup"><span data-stu-id="c7078-135">Typically, tabs work best when they're built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="c7078-136">在内容页面中，添加对 [Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) （使用脚本标记）的引用。</span><span class="sxs-lookup"><span data-stu-id="c7078-136">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="c7078-137">在页面加载后，对进行调用 `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="c7078-137">Following your page load, make a call to `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="c7078-138">如果不显示页面，则不会显示。</span><span class="sxs-lookup"><span data-stu-id="c7078-138">Your page will not be displayed if you do not.</span></span>

## <a name="host-your-app-service"></a><span data-ttu-id="c7078-139">承载你的应用服务</span><span class="sxs-lookup"><span data-stu-id="c7078-139">Host your app service</span></span>

<span data-ttu-id="c7078-140">需要将你的内容托管在可使用 HTTPS 的公开可用 URL 上。</span><span class="sxs-lookup"><span data-stu-id="c7078-140">Your content needs to be hosted on a publicly available URL available using HTTPS.</span></span> <span data-ttu-id="c7078-141">对于测试，可以使用反向代理（如 [ngrok](https://ngrok.com/)）将本地端口公开给面向 INTERNET 的 URL。</span><span class="sxs-lookup"><span data-stu-id="c7078-141">For testing, you can use a reverse proxy, such as [ngrok](https://ngrok.com/), to expose your local port to an internet-facing URL.</span></span>

## <a name="create-your-app-package-with-app-studio"></a><span data-ttu-id="c7078-142">使用应用程序 Studio 创建应用程序包</span><span class="sxs-lookup"><span data-stu-id="c7078-142">Create your app package with App Studio</span></span>

<span data-ttu-id="c7078-143">您可以使用 Microsoft 团队客户端中的应用程序 Studio 应用来帮助创建应用程序清单。</span><span class="sxs-lookup"><span data-stu-id="c7078-143">You can use the App Studio app from within the Microsoft Teams client to help create your app manifest.</span></span> <span data-ttu-id="c7078-144">如果未在团队中安装应用程序 studio，请选择 "团队" 应用的左下角的 " **应用** ![ 商店应用"， ](/microsoftteams/platform/assets/images/tab-images/storeApp.png) 然后搜索应用程序 studio。</span><span class="sxs-lookup"><span data-stu-id="c7078-144">If you do not have App studio installed in Teams, select **Apps** ![Store App](/microsoftteams/platform/assets/images/tab-images/storeApp.png) at the bottom-left corner of the Teams app, and search for App Studio.</span></span> <span data-ttu-id="c7078-145">找到该磁贴后，选择它并在弹出窗口对话框中选择 "安装"。</span><span class="sxs-lookup"><span data-stu-id="c7078-145">Once you find the tile, select it and choose install in the pop-up window dialog box.</span></span>

1. <span data-ttu-id="c7078-146">打开 Microsoft 团队客户端—使用 [基于 web 的版本](https://teams.microsoft.com) ，您可以使用浏览器的 [开发人员工具](~/tabs/how-to/developer-tools.md)检查您的前端代码。</span><span class="sxs-lookup"><span data-stu-id="c7078-146">Open the Microsoft Teams client—using the [web based version](https://teams.microsoft.com) will enable you to inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
1. <span data-ttu-id="c7078-147">打开应用程序 Studio 并选择 " **清单编辑器** " 选项卡。</span><span class="sxs-lookup"><span data-stu-id="c7078-147">Open App Studio and select the **Manifest editor** tab.</span></span>
1. <span data-ttu-id="c7078-148">选择 " **创建新的应用程序** " 磁贴。</span><span class="sxs-lookup"><span data-stu-id="c7078-148">Choose the **Create a new app** tile.</span></span>
1. <span data-ttu-id="c7078-149">添加应用程序详细信息 (请参阅 [清单架构定义](~/resources/schema/manifest-schema.md) ，以获取每个字段) 的完整说明。</span><span class="sxs-lookup"><span data-stu-id="c7078-149">Add your app details (see the [manifest schema definition](~/resources/schema/manifest-schema.md) for full description of each field).</span></span>
1. <span data-ttu-id="c7078-150">在 "功能" 部分，选择 " **选项卡**"。</span><span class="sxs-lookup"><span data-stu-id="c7078-150">In the capabilities section select **Tabs**.</span></span>
    * <span data-ttu-id="c7078-151">对于 "个人" 选项卡，选择 " *添加个人" 选项卡* ，然后选择 " **添加**"。</span><span class="sxs-lookup"><span data-stu-id="c7078-151">For a personal tab, choose *Add a personal tab* and select **Add**.</span></span> <span data-ttu-id="c7078-152">将显示一个弹出对话框窗口，可在其中添加选项卡详细信息。</span><span class="sxs-lookup"><span data-stu-id="c7078-152">You will be presented with a pop-up dialogue window where you can add your tab details.</span></span>
    * <span data-ttu-id="c7078-153">对于 "通道/组" 选项卡，在 " *团队"* 选项卡下选择 " **添加** " 并完成 "团队" 选项卡弹出窗口中的选项卡详细信息字段。</span><span class="sxs-lookup"><span data-stu-id="c7078-153">For a channel/group tab, under *Team Tab* select **Add** and complete the tab details fields in the Team tab pop-up window.</span></span> <span data-ttu-id="c7078-154">请确保 *可以更新配置？* 选中 "工作组" 和 " *组" 聊天* 框，然后选择 " **保存**"。</span><span class="sxs-lookup"><span data-stu-id="c7078-154">Make sure the *can update configuration? Team* and *Group chat* boxes are checked and select **Save**.</span></span>
1. <span data-ttu-id="c7078-155">在 " *域和权限* " 部分中，" *选项卡* " 字段中的域应包含不带 HTTPS 前缀的主机或反向代理 URL。</span><span class="sxs-lookup"><span data-stu-id="c7078-155">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your host or reverse proxy URL without the HTTPS prefix.</span></span>
1. <span data-ttu-id="c7078-156">在 "**完成**  =>  **测试和分布**" 选项卡上，您可以**下载**应用程序包，将包**安装**到团队中，或**提交**到团队应用商店以供审批。</span><span class="sxs-lookup"><span data-stu-id="c7078-156">From the **Finish** => **Test and distribute** tab you can **Download** your app package, **Install** the package into a team, or **Submit** to the Teams app store for approval.</span></span> <span data-ttu-id="c7078-157">*如果使用反向代理，将在右侧的 " **说明** " 字段中收到警告。在测试选项卡时可以忽略此警告*。</span><span class="sxs-lookup"><span data-stu-id="c7078-157">*If you are using a reverse proxy you will get a warning in the **Description** field on the right. The warning can be ignored while testing your tab*.</span></span>

## <a name="create-your-app-package-manually"></a><span data-ttu-id="c7078-158">手动创建应用程序包</span><span class="sxs-lookup"><span data-stu-id="c7078-158">Create your app package manually</span></span>

<span data-ttu-id="c7078-159">与 bot 和邮件扩展一样，您可以更新应用程序 [清单](~/resources/schema/manifest-schema.md) 以包含选项卡属性。</span><span class="sxs-lookup"><span data-stu-id="c7078-159">As with bots and messaging extensions, you update the [app manifest](~/resources/schema/manifest-schema.md) of your app to include the tab properties.</span></span> <span data-ttu-id="c7078-160">这些属性控制您的选项卡在中可用的范围、要使用的 Url 以及各种其他属性。</span><span class="sxs-lookup"><span data-stu-id="c7078-160">These properties govern the scopes your tab is available in, the URLs to be used, and various other properties.</span></span>

### <a name="personal-tabs"></a><span data-ttu-id="c7078-161">个人选项卡</span><span class="sxs-lookup"><span data-stu-id="c7078-161">Personal Tabs</span></span>

<span data-ttu-id="c7078-162">"个人" 选项卡的显示内容对于所有用户都是相同的，并在阵列中进行配置 `staticTabs` 。</span><span class="sxs-lookup"><span data-stu-id="c7078-162">The displayed content for personal tabs is the same for all users and is configured in the `staticTabs` array.</span></span> <span data-ttu-id="c7078-163">您可以在应用程序中声明最高 16 (16) 个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="c7078-163">You may declare up to sixteen (16) personal tabs in an app.</span></span>

|<span data-ttu-id="c7078-164">名称</span><span class="sxs-lookup"><span data-stu-id="c7078-164">Name</span></span>| <span data-ttu-id="c7078-165">类型</span><span class="sxs-lookup"><span data-stu-id="c7078-165">Type</span></span>| <span data-ttu-id="c7078-166">最大大小</span><span class="sxs-lookup"><span data-stu-id="c7078-166">Maximum size</span></span> | <span data-ttu-id="c7078-167">必需</span><span class="sxs-lookup"><span data-stu-id="c7078-167">Required</span></span> | <span data-ttu-id="c7078-168">说明</span><span class="sxs-lookup"><span data-stu-id="c7078-168">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="c7078-169">字符串</span><span class="sxs-lookup"><span data-stu-id="c7078-169">String</span></span>|<span data-ttu-id="c7078-170">64 个字符</span><span class="sxs-lookup"><span data-stu-id="c7078-170">64 characters</span></span>|<span data-ttu-id="c7078-171">✔</span><span class="sxs-lookup"><span data-stu-id="c7078-171">✔</span></span>|<span data-ttu-id="c7078-172">选项卡显示的实体的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="c7078-172">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="c7078-173">字符串</span><span class="sxs-lookup"><span data-stu-id="c7078-173">String</span></span>|<span data-ttu-id="c7078-174">128个字符</span><span class="sxs-lookup"><span data-stu-id="c7078-174">128 characters</span></span>|<span data-ttu-id="c7078-175">✔</span><span class="sxs-lookup"><span data-stu-id="c7078-175">✔</span></span>|<span data-ttu-id="c7078-176">该选项卡在通道接口中的显示名称。</span><span class="sxs-lookup"><span data-stu-id="c7078-176">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="c7078-177">字符串</span><span class="sxs-lookup"><span data-stu-id="c7078-177">String</span></span>|<span data-ttu-id="c7078-178">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="c7078-178">2048 characters</span></span>|<span data-ttu-id="c7078-179">✔</span><span class="sxs-lookup"><span data-stu-id="c7078-179">✔</span></span>|<span data-ttu-id="c7078-180">指向要在团队画布中显示的实体 UI 的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="c7078-180">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="c7078-181">字符串</span><span class="sxs-lookup"><span data-stu-id="c7078-181">String</span></span>|<span data-ttu-id="c7078-182">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="c7078-182">2048 characters</span></span>||<span data-ttu-id="c7078-183">要指向的 https://URL，如果用户要在浏览器中查看。</span><span class="sxs-lookup"><span data-stu-id="c7078-183">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="c7078-184">枚举数组</span><span class="sxs-lookup"><span data-stu-id="c7078-184">Array of enum</span></span>|<span data-ttu-id="c7078-185">1</span><span class="sxs-lookup"><span data-stu-id="c7078-185">1</span></span>|<span data-ttu-id="c7078-186">✔</span><span class="sxs-lookup"><span data-stu-id="c7078-186">✔</span></span>|<span data-ttu-id="c7078-187">静态选项卡仅支持 `personal` 作用域，这意味着只能将其设置为个人应用程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="c7078-187">Static tabs support only the `personal` scope, which means it can be provisioned only as part of a personal app.</span></span>|

#### <a name="simple-personal-tab-manifest-example"></a><span data-ttu-id="c7078-188">简单的个人选项卡清单示例</span><span class="sxs-lookup"><span data-stu-id="c7078-188">Simple personal tab manifest example</span></span>

<span data-ttu-id="c7078-189">下面的示例仅展示了 `staticTabs` 应用程序清单中的数组。</span><span class="sxs-lookup"><span data-stu-id="c7078-189">The example below shows just the `staticTabs` array from an app manifest.</span></span>

```json
...
"staticTabs": [
    {
      "entityId": "idForPage",
      "name": "Display name for tab",
      "contentUrl": "https:// yourURL.com/content ",
      "websiteUrl": "https://yourURL.com/website",
      "scopes": [ "personal" ]
    }
...
```

### <a name="channelgroup-tabs"></a><span data-ttu-id="c7078-190">通道/组选项卡</span><span class="sxs-lookup"><span data-stu-id="c7078-190">Channel/group tabs</span></span>

<span data-ttu-id="c7078-191">在阵列中添加通道/组选项卡 `configurableTabs` 。</span><span class="sxs-lookup"><span data-stu-id="c7078-191">Channel/group tabs are added in the `configurableTabs` array.</span></span> <span data-ttu-id="c7078-192">您只能在数组中声明一个通道/组选项卡 `configurableTabs` 。</span><span class="sxs-lookup"><span data-stu-id="c7078-192">You may declare only one channel/group tab in the `configurableTabs` array.</span></span>

|<span data-ttu-id="c7078-193">名称</span><span class="sxs-lookup"><span data-stu-id="c7078-193">Name</span></span>| <span data-ttu-id="c7078-194">类型</span><span class="sxs-lookup"><span data-stu-id="c7078-194">Type</span></span>| <span data-ttu-id="c7078-195">最大大小</span><span class="sxs-lookup"><span data-stu-id="c7078-195">Maximum size</span></span> | <span data-ttu-id="c7078-196">必需</span><span class="sxs-lookup"><span data-stu-id="c7078-196">Required</span></span> | <span data-ttu-id="c7078-197">说明</span><span class="sxs-lookup"><span data-stu-id="c7078-197">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="c7078-198">字符串</span><span class="sxs-lookup"><span data-stu-id="c7078-198">String</span></span>|<span data-ttu-id="c7078-199">2048 个字符</span><span class="sxs-lookup"><span data-stu-id="c7078-199">2048 characters</span></span>|<span data-ttu-id="c7078-200">✔</span><span class="sxs-lookup"><span data-stu-id="c7078-200">✔</span></span>|<span data-ttu-id="c7078-201">指向 "配置" 页的 https://URL。</span><span class="sxs-lookup"><span data-stu-id="c7078-201">The https:// URL to configuration page.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="c7078-202">布尔值</span><span class="sxs-lookup"><span data-stu-id="c7078-202">Boolean</span></span>|||<span data-ttu-id="c7078-203">一个值，指示是否可在用户创建之后更新该选项卡的配置实例。</span><span class="sxs-lookup"><span data-stu-id="c7078-203">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="c7078-204">设置 `true`</span><span class="sxs-lookup"><span data-stu-id="c7078-204">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="c7078-205">枚举数组</span><span class="sxs-lookup"><span data-stu-id="c7078-205">Array of enum</span></span>|<span data-ttu-id="c7078-206">1</span><span class="sxs-lookup"><span data-stu-id="c7078-206">1</span></span>|<span data-ttu-id="c7078-207">✔</span><span class="sxs-lookup"><span data-stu-id="c7078-207">✔</span></span>|<span data-ttu-id="c7078-208">可配置的选项卡仅支持 `team` 和 `groupchat` 范围。</span><span class="sxs-lookup"><span data-stu-id="c7078-208">Configurable tabs support only the `team` and `groupchat` scopes.</span></span> |

#### <a name="simple-channelgroup-tab-manifest-example"></a><span data-ttu-id="c7078-209">简单通道/组选项卡清单示例</span><span class="sxs-lookup"><span data-stu-id="c7078-209">Simple channel/group tab manifest example</span></span>

<span data-ttu-id="c7078-210">下面的示例仅展示了 `configurableTabs` 应用程序清单中的数组。</span><span class="sxs-lookup"><span data-stu-id="c7078-210">The example below shows just the `configurableTabs` array from an app manifest.</span></span>

```json
...
"configurableTabs": [
    {
      "configurationUrl": "https://yourURL.com/configure",
      "canUpdateConfiguration": true,
      "scopes": [ "team", "groupchat" ]
    }
...
```

<span data-ttu-id="c7078-211">将 `manifest.json` 其捆绑到 zip 文件夹中，并将它与两个必需的图标组合在一起。</span><span class="sxs-lookup"><span data-stu-id="c7078-211">Once you have completed your `manifest.json` bundle it in a zip folder along with your two required icons.</span></span>

### <a name="upload-app-package-directly-to-a-team"></a><span data-ttu-id="c7078-212">将应用程序包直接上载到团队</span><span class="sxs-lookup"><span data-stu-id="c7078-212">Upload app package directly to a team</span></span>

1. <span data-ttu-id="c7078-213">打开 Microsoft 团队客户端。</span><span class="sxs-lookup"><span data-stu-id="c7078-213">Open the Microsoft Teams client.</span></span> <span data-ttu-id="c7078-214">如果您使用的是 [基于 web 的版本](https://teams.microsoft.com) ，则可以使用浏览器的 [开发人员工具](~/tabs/how-to/developer-tools.md)检查您的前端代码。</span><span class="sxs-lookup"><span data-stu-id="c7078-214">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
1. <span data-ttu-id="c7078-215">在左侧的 " *YourTeams* " 面板中，选择要用于 `...` 测试选项卡的团队旁边的菜单，然后选择 " **管理团队**"。</span><span class="sxs-lookup"><span data-stu-id="c7078-215">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
1. <span data-ttu-id="c7078-216">在主面板中，从选项卡栏中选择 " **应用** "，然后选择 "上载" 位于页面右下角的 **自定义应用程序** 。</span><span class="sxs-lookup"><span data-stu-id="c7078-216">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
1. <span data-ttu-id="c7078-217">打开您的项目目录，浏览到 " **/package** " 文件夹，选择 "应用程序包" zip 文件夹，然后选择 " **打开**"。</span><span class="sxs-lookup"><span data-stu-id="c7078-217">Open your project directory, browse to the **./package** folder, select the app package zip folder and choose **Open**.</span></span> <span data-ttu-id="c7078-218">您的选项卡将上传到团队。</span><span class="sxs-lookup"><span data-stu-id="c7078-218">Your tab will upload into Teams.</span></span>

### <a name="view-your-tab-in-teams"></a><span data-ttu-id="c7078-219">在团队中查看您的选项卡</span><span class="sxs-lookup"><span data-stu-id="c7078-219">View your tab in Teams</span></span>

1. <span data-ttu-id="c7078-220">查看您的个人选项卡：</span><span class="sxs-lookup"><span data-stu-id="c7078-220">View your personal tab:</span></span>
    * <span data-ttu-id="c7078-221">在位于团队客户端最左侧的导航栏中，选择 `...` 菜单并从列表中选择您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c7078-221">In the navbar located at the far-left of the Teams client, select the `...` menu and choose your app from the list.</span></span>

1. <span data-ttu-id="c7078-222">查看频道/组选项卡：</span><span class="sxs-lookup"><span data-stu-id="c7078-222">View your channel/group tab:</span></span>
    * <span data-ttu-id="c7078-223">返回到您的团队，选择要在其中显示选项卡的频道，从选项卡栏中选择 "➕"，然后从库中选择您的选项卡。</span><span class="sxs-lookup"><span data-stu-id="c7078-223">Return to your team, choose the channel where you would like to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
    * <span data-ttu-id="c7078-224">按照有关添加选项卡的说明操作。请注意，"通道/组" 选项卡有一个自定义配置对话框。选择 " **保存** "，您的选项卡将添加到频道的选项卡栏中。</span><span class="sxs-lookup"><span data-stu-id="c7078-224">Follow the directions for adding a tab. Note that there's a custom configuration dialog for your channel/group tab. Select **Save** and your tab will be added to the channel's tab bar.</span></span>

## <a name="learn-more"></a><span data-ttu-id="c7078-225">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="c7078-225">Learn more</span></span>

* [<span data-ttu-id="c7078-226">创建选项卡的内容页</span><span class="sxs-lookup"><span data-stu-id="c7078-226">Create a content page for your tab</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="c7078-227">创建选项卡的配置页</span><span class="sxs-lookup"><span data-stu-id="c7078-227">Create a configuration page for your tab</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [<span data-ttu-id="c7078-228">更新或删除选项卡</span><span class="sxs-lookup"><span data-stu-id="c7078-228">Update or remove a tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
