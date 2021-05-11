---
title: 公共服务中的开发者预览版
description: 详细介绍公共Microsoft Teams中的开发者预览版
ms.topic: reference
localization_priority: Normal
keywords: teams 预览开发人员功能
ms.openlocfilehash: 84683420a5c61bb1eb493f8191bfbcbe97f6fb46
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230902"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="d5e45-104">公共服务开发者预览版中的Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d5e45-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="d5e45-105">此页面将于 2021 年 6 月弃用。</span><span class="sxs-lookup"><span data-stu-id="d5e45-105">This page will be deprecated in June 2021.</span></span> <span data-ttu-id="d5e45-106">有关适用于开发人员预览的功能的信息，请参阅 [新增功能？](~/whats-new.md)</span><span class="sxs-lookup"><span data-stu-id="d5e45-106">For information on features available for developer preview, see [What's new?](~/whats-new.md)</span></span>

<span data-ttu-id="d5e45-107">开发人员预览版包括以下新功能：</span><span class="sxs-lookup"><span data-stu-id="d5e45-107">The developer preview includes the following new features:</span></span>

## <a name="app-customization"></a><span data-ttu-id="d5e45-108">应用自定义</span><span class="sxs-lookup"><span data-stu-id="d5e45-108">App customization</span></span>

<span data-ttu-id="d5e45-109">现在，您可以定义一组选定属性，Teams管理员可基于其组织需求自定义或重新品牌。</span><span class="sxs-lookup"><span data-stu-id="d5e45-109">You can now define a select set of properties, which a Teams admin can customize or rebrand based on their organization's need.</span></span> <span data-ttu-id="d5e45-110">有关详细信息，请参阅 [应用自定义功能](~/concepts/design/design-teams-app-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d5e45-110">For more information, see [app customization feature](~/concepts/design/design-teams-app-overview.md).</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="d5e45-111">选项卡单一登录 (SSO) </span><span class="sxs-lookup"><span data-stu-id="d5e45-111">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="d5e45-112">现在，可以使用[SSO](~/tabs/how-to/authentication/auth-aad-sso.md) (单一登录) Web 内容页中的 Teams JavaScript SDK 在桌面和移动设备上登录并验证用户身份。</span><span class="sxs-lookup"><span data-stu-id="d5e45-112">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="d5e45-113">其中一个好处是用户永远不登录;并且一旦他们同意使用其配置文件的应用：他们将自动登录到其选项卡 (包括移动) 。</span><span class="sxs-lookup"><span data-stu-id="d5e45-113">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="d5e45-114">我们的开发人员预览在清单版本 1.5 及更大版本中可用。</span><span class="sxs-lookup"><span data-stu-id="d5e45-114">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="d5e45-115">我们的当前实现只能获取有限数量的Graph API，但我们提供了一种解决方法，以便使用现有身份验证 API Graph其他应用程序 API。</span><span class="sxs-lookup"><span data-stu-id="d5e45-115">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="d5e45-116">通话和联机会议机器人</span><span class="sxs-lookup"><span data-stu-id="d5e45-116">Calls and online meeting bots</span></span>

<span data-ttu-id="d5e45-117">通过添加用于Graph和联机会议的[Microsoft](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)GRAPH API，Microsoft Teams应用现在可以使用语音和视频以丰富的方式与用户进行交互。</span><span class="sxs-lookup"><span data-stu-id="d5e45-117">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="d5e45-118">这些 API 允许你添加新的应用功能，如交互式语音响应 (IVR) 、呼叫控制，以及访问通话和会议实时音频流和/或视频流，包括桌面应用应用共享。</span><span class="sxs-lookup"><span data-stu-id="d5e45-118">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="d5e45-119">从概述 开始，我们添加了一个新部分，介绍了如何创建和开发通话和联机 [会议机器人](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d5e45-119">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>


## <a name="image-enlarge-support"></a><span data-ttu-id="d5e45-120">图像放大支持</span><span class="sxs-lookup"><span data-stu-id="d5e45-120">Image enlarge support</span></span>

<span data-ttu-id="d5e45-121">现在机器人可以指示在自适应卡片中共享的图像Teams放大。</span><span class="sxs-lookup"><span data-stu-id="d5e45-121">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="d5e45-122">这适用于通过机器人共享详细的分步视觉指南等方案，否则用户可能很难阅读这些指南。</span><span class="sxs-lookup"><span data-stu-id="d5e45-122">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="d5e45-123">若要使图像可展开，只需如下所示 `allowExpand: true` 标记它。</span><span class="sxs-lookup"><span data-stu-id="d5e45-123">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="d5e45-124">这会使Teams/桌面客户端将元素悬停在图像上，以允许用户展开图像。</span><span class="sxs-lookup"><span data-stu-id="d5e45-124">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>
