---
title: 公共开发人员预览版中的功能
description: 介绍 Microsoft 团队的公共开发人员预览版中的功能
keywords: 团队预览开发人员功能
ms.openlocfilehash: 7ed442072779917dcc5db3ebcb4afaac9db0407f
ms.sourcegitcommit: b9e8839858ea8e9e33fe5e20e14bbe86c75fd510
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "44210699"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="4b2f5-104">Microsoft 团队的公共开发人员预览版中的功能</span><span class="sxs-lookup"><span data-stu-id="4b2f5-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="4b2f5-105">开发人员预览包括以下新功能：</span><span class="sxs-lookup"><span data-stu-id="4b2f5-105">The developer preview includes the following new features:</span></span>

## <a name="adaptive-cards-v12-support"></a><span data-ttu-id="4b2f5-106">自适应卡片 1.2 1.2 支持</span><span class="sxs-lookup"><span data-stu-id="4b2f5-106">Adaptive cards v1.2 support</span></span>

<span data-ttu-id="4b2f5-107">团队中的[自适应卡片 v 1.2](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)的支持现在可供一般大众使用。</span><span class="sxs-lookup"><span data-stu-id="4b2f5-107">Support for [Adaptive cards v1.2](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) in Teams is now available to the general public.</span></span> <span data-ttu-id="4b2f5-108">但是，在团队平台上，自适应卡上的1.2 版中目前不支持[媒体元素](https://adaptivecards.io/explorer/Media.html)。</span><span class="sxs-lookup"><span data-stu-id="4b2f5-108">However, [Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="4b2f5-109">选项卡单一登录（SSO）</span><span class="sxs-lookup"><span data-stu-id="4b2f5-109">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="4b2f5-110">现在，您可以使用[单一登录（SSO）](~/tabs/how-to/authentication/auth-aad-sso.md) ，在桌面和移动设备上使用 web 内容页中的团队 JavaScript SDK 登录并验证用户。</span><span class="sxs-lookup"><span data-stu-id="4b2f5-110">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="4b2f5-111">其中一项好处是用户永远不需要登录;在用户使用其配置文件同意应用程序之后，将自动登录到其选项卡（包括移动设备）。</span><span class="sxs-lookup"><span data-stu-id="4b2f5-111">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="4b2f5-112">我们的开发人员预览版在清单版本1.5 及更高版本中可用。</span><span class="sxs-lookup"><span data-stu-id="4b2f5-112">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="4b2f5-113">我们的当前实施只能获取有限数量的图形 Api，但我们提供了使用我们现有的身份验证 API 获取其他图形 Api 的替代方法。</span><span class="sxs-lookup"><span data-stu-id="4b2f5-113">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="personal-apps-static-tabs-and-1-1-bots-enabled-on-mobile"></a><span data-ttu-id="4b2f5-114">移动设备上启用的个人应用（静态选项卡和 1-1 bot）</span><span class="sxs-lookup"><span data-stu-id="4b2f5-114">Personal apps (static tabs and 1-1 bots) enabled on mobile</span></span>

<span data-ttu-id="4b2f5-115">安装的个人应用（静态选项卡和 1-1 bot）现在在移动设备上的应用程序托盘中可用。</span><span class="sxs-lookup"><span data-stu-id="4b2f5-115">Installed personal apps (static tabs and 1-1 bots) are now available in the app tray on mobile devices.</span></span> <span data-ttu-id="4b2f5-116">请参阅[mobile 的设计指南以](~/tabs/design/tabs-mobile.md)了解设计指南。</span><span class="sxs-lookup"><span data-stu-id="4b2f5-116">See [Design guidelines for mobile](~/tabs/design/tabs-mobile.md) for design guidance.</span></span> <span data-ttu-id="4b2f5-117">只能从桌面或 web 客户端安装应用程序，安装后最长可在移动设备上使用4小时。</span><span class="sxs-lookup"><span data-stu-id="4b2f5-117">Apps can only be installed from a desktop or web client, and can take up to 4 hours to be available on mobile after installation.</span></span>

<span data-ttu-id="4b2f5-118">这包括系统管理员通过[应用安装策略](/microsoftteams/teams-app-setup-policies)预固定应用的能力。</span><span class="sxs-lookup"><span data-stu-id="4b2f5-118">This includes the ability for a system administrator to pre-pin an app via [app setup policies](/microsoftteams/teams-app-setup-policies).</span></span> <span data-ttu-id="4b2f5-119">已固定的应用程序将显示在应用抽屉中。</span><span class="sxs-lookup"><span data-stu-id="4b2f5-119">Apps that have pinned will be displayed in the app drawer.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="4b2f5-120">呼叫和联机会议 bot</span><span class="sxs-lookup"><span data-stu-id="4b2f5-120">Calls and online meeting bots</span></span>

<span data-ttu-id="4b2f5-121">通过添加[用于呼叫和联机会议的 Microsoft Graph api](/graph/api/resources/communications-api-overview?view=graph-rest-beta)，microsoft 团队应用现在可以使用语音和视频以丰富的方式与用户进行交互。</span><span class="sxs-lookup"><span data-stu-id="4b2f5-121">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="4b2f5-122">这些 Api 允许您添加新的应用程序功能，如交互式语音响应（IVR）、呼叫控制以及对呼叫和会议（包括桌面和应用程序共享）的实时音频和/或视频流的访问。</span><span class="sxs-lookup"><span data-stu-id="4b2f5-122">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="4b2f5-123">我们已添加了有关如何创建和开发呼叫和联机会议 bot 的新部分，从[概述](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)开始。</span><span class="sxs-lookup"><span data-stu-id="4b2f5-123">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>
