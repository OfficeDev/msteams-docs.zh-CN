---
title: 公共开发人员预览版中的功能
description: 详细介绍 Microsoft 团队公开开发人员预览版中的功能
keywords: 团队预览开发人员功能
ms.openlocfilehash: 773e0334bddf45b7b86d31329b99607f3b70c534
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874840"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="50af3-104">Microsoft 团队的公共开发人员预览版中的功能</span><span class="sxs-lookup"><span data-stu-id="50af3-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="50af3-105">开发人员预览包括以下新功能：</span><span class="sxs-lookup"><span data-stu-id="50af3-105">The developer preview includes the following new features:</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="50af3-106"> (SSO) 的选项卡单一登录</span><span class="sxs-lookup"><span data-stu-id="50af3-106">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="50af3-107">现在，你可以使用 [单一登录 (SSO) ](~/tabs/how-to/authentication/auth-aad-sso.md) 使用 web 内容页中的团队 JavaScript SDK 登录桌面和手机上的用户并对其进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="50af3-107">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="50af3-108">其中一项好处是用户永远不需要登录;在用户使用其配置文件同意应用程序之后，将自动登录到其选项卡 (包括移动) 。</span><span class="sxs-lookup"><span data-stu-id="50af3-108">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="50af3-109">我们的开发人员预览版在清单版本1.5 及更高版本中可用。</span><span class="sxs-lookup"><span data-stu-id="50af3-109">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="50af3-110">我们的当前实施只能获取有限数量的图形 Api，但我们提供了使用我们现有的身份验证 API 获取其他图形 Api 的替代方法。</span><span class="sxs-lookup"><span data-stu-id="50af3-110">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="50af3-111">呼叫和联机会议 bot</span><span class="sxs-lookup"><span data-stu-id="50af3-111">Calls and online meeting bots</span></span>

<span data-ttu-id="50af3-112">通过添加 [用于呼叫和联机会议的 Microsoft Graph api](/graph/api/resources/communications-api-overview?view=graph-rest-beta)，microsoft 团队应用现在可以使用语音和视频以丰富的方式与用户进行交互。</span><span class="sxs-lookup"><span data-stu-id="50af3-112">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="50af3-113">这些 Api 允许您添加新的应用程序功能，如交互式语音响应 (IVR) 、呼叫控制以及对呼叫和会议（包括桌面和应用程序共享）的实时音频和/或视频流的访问。</span><span class="sxs-lookup"><span data-stu-id="50af3-113">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="50af3-114">我们已添加了有关如何创建和开发呼叫和联机会议 bot 的新部分，从 [概述](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)开始。</span><span class="sxs-lookup"><span data-stu-id="50af3-114">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>

## <a name="image-enlarge-support"></a><span data-ttu-id="50af3-115">图像放大支持</span><span class="sxs-lookup"><span data-stu-id="50af3-115">Image enlarge support</span></span>

<span data-ttu-id="50af3-116">现在，bot 可以指示允许放大团队中的自适应卡片中共享的图像。</span><span class="sxs-lookup"><span data-stu-id="50af3-116">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="50af3-117">这对诸如通过 bot 共享详细的分步可视化指南等方案很有用，否则用户可能很难阅读。</span><span class="sxs-lookup"><span data-stu-id="50af3-117">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="50af3-118">若要使图像可扩展，只需对其进行标记，如下 `allowExpand: true` 所示。</span><span class="sxs-lookup"><span data-stu-id="50af3-118">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="50af3-119">这将导致团队 web/桌面客户端在将鼠标悬停在图像上时呈现元素，以允许用户扩展图像。</span><span class="sxs-lookup"><span data-stu-id="50af3-119">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>

