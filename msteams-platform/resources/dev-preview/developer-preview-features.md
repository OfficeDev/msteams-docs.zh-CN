---
title: 公共网站中的开发者预览版
description: 介绍了 Microsoft Teams 的公共开发者预览版功能
keywords: Teams 预览开发人员功能
ms.openlocfilehash: e607a6c65253a5fd94f8a805f1264a567bb8fd24
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819173"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="5fdf0-104">Microsoft Teams 公共开发者预览版中的功能</span><span class="sxs-lookup"><span data-stu-id="5fdf0-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="5fdf0-105">开发人员预览包括以下新功能：</span><span class="sxs-lookup"><span data-stu-id="5fdf0-105">The developer preview includes the following new features:</span></span>

## <a name="adaptive-cards-v12-support"></a><span data-ttu-id="5fdf0-106">自适应卡片 v1.2 支持</span><span class="sxs-lookup"><span data-stu-id="5fdf0-106">Adaptive cards v1.2 support</span></span>

<span data-ttu-id="5fdf0-107">现已 [向正式公共提供对](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) Teams 中的自适应卡片 v1.2 的支持。</span><span class="sxs-lookup"><span data-stu-id="5fdf0-107">Support for [Adaptive cards v1.2](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) in Teams is now available to the general public.</span></span> <span data-ttu-id="5fdf0-108">但是 [，Teams 平台](https://adaptivecards.io/explorer/Media.html) 上的自适应卡片 v1.2 中当前不支持媒体元素。</span><span class="sxs-lookup"><span data-stu-id="5fdf0-108">However, [Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="5fdf0-109">SSO 项目以选项卡 (单一) </span><span class="sxs-lookup"><span data-stu-id="5fdf0-109">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="5fdf0-110">现在，你可以 [使用单一登录登录到 (SSO) ， ](~/tabs/how-to/authentication/auth-aad-sso.md) 以通过 Web 内容页中的 Teams JavaScript SDK 登录和移动台式用户和移动设备上的用户。</span><span class="sxs-lookup"><span data-stu-id="5fdf0-110">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="5fdf0-111">优势之一是，用户永远不必须登录;如果他们已使用其个人资料同意应用，就会自动登录 (包括移动应用商店页面的) 。</span><span class="sxs-lookup"><span data-stu-id="5fdf0-111">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="5fdf0-112">我们的开发人员预览版在清单版本 1.5 及更高版本中可用。</span><span class="sxs-lookup"><span data-stu-id="5fdf0-112">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="5fdf0-113">尽管我们的当前实现只能获取有限的 Graph API，但我们提供了一种解决办法，以使用我们现有的身份验证 API 获取额外的 Graph API。</span><span class="sxs-lookup"><span data-stu-id="5fdf0-113">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="5fdf0-114">呼叫和联机会议机器人</span><span class="sxs-lookup"><span data-stu-id="5fdf0-114">Calls and online meeting bots</span></span>

<span data-ttu-id="5fdf0-115">通过为呼叫和 [在线会议添加 Microsoft Graph API，Microsoft](/graph/api/resources/communications-api-overview?view=graph-rest-beta)Teams 应用现在可以使用语音和视频以丰富的方式与用户进行交互。</span><span class="sxs-lookup"><span data-stu-id="5fdf0-115">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="5fdf0-116">通过这些 API，可以添加新应用功能，如交互式语音响应 (IVR) 、呼叫控制，并访问通话和会议（包括桌面和应用共享）的实时音频和/或视频流。</span><span class="sxs-lookup"><span data-stu-id="5fdf0-116">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="5fdf0-117">我们添加了有关如何创建和开发电话和联机会议机器人（从概述开始）的新 [部分](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5fdf0-117">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>
