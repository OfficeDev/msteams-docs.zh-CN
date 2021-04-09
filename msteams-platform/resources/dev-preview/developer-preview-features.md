---
title: 公共服务中的开发者预览版
description: 详细介绍 Microsoft Teams 公共网站中的开发者预览版
ms.topic: reference
keywords: teams 预览开发人员功能
ms.openlocfilehash: 05954383931444cd0fb53dc37d9f790257f7dd39
ms.sourcegitcommit: b50f6d68482cad43a60642a9947d1be17809a7df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634514"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="82057-104">Microsoft Teams 公共开发者预览版中的功能</span><span class="sxs-lookup"><span data-stu-id="82057-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="82057-105">开发人员预览版包括以下新功能：</span><span class="sxs-lookup"><span data-stu-id="82057-105">The developer preview includes the following new features:</span></span>

## <a name="app-customization"></a><span data-ttu-id="82057-106">应用自定义</span><span class="sxs-lookup"><span data-stu-id="82057-106">App customization</span></span>

<span data-ttu-id="82057-107">现在，你可以定义一组精选属性，Teams 管理员可以根据组织需求自定义或重新品牌。</span><span class="sxs-lookup"><span data-stu-id="82057-107">You can now define a select set of properties, which a Teams admin can customize or rebrand based on their organization's need.</span></span> <span data-ttu-id="82057-108">有关详细信息，请参阅 [应用自定义功能](~/concepts/design/design-teams-app-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="82057-108">For more information, see [app customization feature](~/concepts/design/design-teams-app-overview.md).</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="82057-109">选项卡单一登录 (SSO) </span><span class="sxs-lookup"><span data-stu-id="82057-109">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="82057-110">现在，可以使用 [SSO ](~/tabs/how-to/authentication/auth-aad-sso.md) (单一登录) Web 内容页中的 Teams JavaScript SDK 在桌面和移动设备上登录并验证用户身份。</span><span class="sxs-lookup"><span data-stu-id="82057-110">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="82057-111">其中一个好处是用户永远不登录;并且一旦他们同意使用其配置文件的应用：他们将自动登录到其选项卡 (包括移动) 。</span><span class="sxs-lookup"><span data-stu-id="82057-111">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="82057-112">我们的开发人员预览在清单版本 1.5 及更大版本中可用。</span><span class="sxs-lookup"><span data-stu-id="82057-112">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="82057-113">我们的当前实现只能获取有限数量的 Graph API，但我们提供了一种解决方法，以使用现有的身份验证 API 获取其他 Graph API。</span><span class="sxs-lookup"><span data-stu-id="82057-113">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="82057-114">通话和联机会议机器人</span><span class="sxs-lookup"><span data-stu-id="82057-114">Calls and online meeting bots</span></span>

<span data-ttu-id="82057-115">通过添加用于通话和联机会议的 [Microsoft Graph API，Microsoft](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)Teams 应用现在可以通过多种使用语音和视频的方式与用户进行交互。</span><span class="sxs-lookup"><span data-stu-id="82057-115">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="82057-116">这些 API 允许你添加新的应用功能，如交互式语音响应 (IVR) 、呼叫控制，以及访问通话和会议实时音频流和/或视频流，包括桌面应用应用共享。</span><span class="sxs-lookup"><span data-stu-id="82057-116">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="82057-117">从概述 开始，我们添加了一个新部分，介绍了如何创建和开发通话和联机 [会议机器人](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="82057-117">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>


## <a name="image-enlarge-support"></a><span data-ttu-id="82057-118">图像放大支持</span><span class="sxs-lookup"><span data-stu-id="82057-118">Image enlarge support</span></span>

<span data-ttu-id="82057-119">现在机器人可以指示允许放大 Teams 自适应卡片中共享的图像。</span><span class="sxs-lookup"><span data-stu-id="82057-119">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="82057-120">这适用于通过机器人共享详细的分步视觉指南等方案，否则用户可能很难阅读这些指南。</span><span class="sxs-lookup"><span data-stu-id="82057-120">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="82057-121">若要使图像可展开，只需如下所示 `allowExpand: true` 标记它。</span><span class="sxs-lookup"><span data-stu-id="82057-121">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="82057-122">这会使 Teams Web/桌面客户端将元素悬停在图像上方，以允许用户展开图像。</span><span class="sxs-lookup"><span data-stu-id="82057-122">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>

