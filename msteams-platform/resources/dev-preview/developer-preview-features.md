---
title: 公共服务中的开发者预览版
description: 详细介绍 Microsoft Teams 公共服务开发者预览版
ms.topic: reference
keywords: teams 预览开发人员功能
ms.openlocfilehash: 3275ef7ac0d4ba052f417f6e852f48e2fdf267f5
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014353"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="c7c1f-104">Microsoft Teams 公共开发者预览版中的功能</span><span class="sxs-lookup"><span data-stu-id="c7c1f-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="c7c1f-105">开发人员预览版包括以下新功能：</span><span class="sxs-lookup"><span data-stu-id="c7c1f-105">The developer preview includes the following new features:</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="c7c1f-106">在 SSO 服务中 (单一) </span><span class="sxs-lookup"><span data-stu-id="c7c1f-106">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="c7c1f-107">现在，可以使用 [SSO ](~/tabs/how-to/authentication/auth-aad-sso.md) (单一登录) 通过 Web 内容页中的 Teams JavaScript SDK 在桌面和移动设备上登录用户并进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="c7c1f-107">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="c7c1f-108">其中一个好处是用户永远不一直登录;当他们使用个人资料同意应用后：将自动登录到其选项卡 (包括移动) 。</span><span class="sxs-lookup"><span data-stu-id="c7c1f-108">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="c7c1f-109">我们的开发人员预览在清单版本 1.5 及更大版本中可用。</span><span class="sxs-lookup"><span data-stu-id="c7c1f-109">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="c7c1f-110">我们的当前实现只能获取有限数量的 Graph API，但我们提供了使用现有身份验证 API 获取其他 Graph API 的解决方法。</span><span class="sxs-lookup"><span data-stu-id="c7c1f-110">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="c7c1f-111">呼叫和联机会议机器人</span><span class="sxs-lookup"><span data-stu-id="c7c1f-111">Calls and online meeting bots</span></span>

<span data-ttu-id="c7c1f-112">通过添加用于通话和联机会议的 [Microsoft Graph API，Microsoft](/graph/api/resources/communications-api-overview?view=graph-rest-beta)Teams 应用现在可以使用语音和视频以丰富的方式与用户进行交互。</span><span class="sxs-lookup"><span data-stu-id="c7c1f-112">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="c7c1f-113">这些 API 允许你添加新的应用功能，如交互式语音响应 (IVR) 、呼叫控制，以及访问呼叫和会议实时音频流和/或视频流，包括桌面和应用共享。</span><span class="sxs-lookup"><span data-stu-id="c7c1f-113">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="c7c1f-114">我们添加了一个新部分，介绍了如何创建和开发通话和联机会议机器人，从概述 [开始](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c7c1f-114">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>

## <a name="image-enlarge-support"></a><span data-ttu-id="c7c1f-115">图像放大支持</span><span class="sxs-lookup"><span data-stu-id="c7c1f-115">Image enlarge support</span></span>

<span data-ttu-id="c7c1f-116">现在机器人可以指示允许放大 Teams 自适应卡片中共享的图像。</span><span class="sxs-lookup"><span data-stu-id="c7c1f-116">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="c7c1f-117">这适用于通过自动程序共享详细的分步视觉指南等方案，否则用户可能很难阅读这些指南。</span><span class="sxs-lookup"><span data-stu-id="c7c1f-117">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="c7c1f-118">若要使图像可展开，只需标记它 `allowExpand: true` ，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c7c1f-118">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="c7c1f-119">这会使 Teams Web/桌面客户端在将鼠标悬停在图像上时呈现元素，以允许用户展开图像。</span><span class="sxs-lookup"><span data-stu-id="c7c1f-119">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>

