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
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Microsoft Teams 公共开发者预览版中的功能

开发人员预览版包括以下新功能：

## <a name="tabs-single-sign-on-sso"></a>在 SSO 服务中 (单一) 

现在，可以使用 [SSO ](~/tabs/how-to/authentication/auth-aad-sso.md) (单一登录) 通过 Web 内容页中的 Teams JavaScript SDK 在桌面和移动设备上登录用户并进行身份验证。 其中一个好处是用户永远不一直登录;当他们使用个人资料同意应用后：将自动登录到其选项卡 (包括移动) 。

我们的开发人员预览在清单版本 1.5 及更大版本中可用。 我们的当前实现只能获取有限数量的 Graph API，但我们提供了使用现有身份验证 API 获取其他 Graph API 的解决方法。

## <a name="calls-and-online-meeting-bots"></a>呼叫和联机会议机器人

通过添加用于通话和联机会议的 [Microsoft Graph API，Microsoft](/graph/api/resources/communications-api-overview?view=graph-rest-beta)Teams 应用现在可以使用语音和视频以丰富的方式与用户进行交互。 这些 API 允许你添加新的应用功能，如交互式语音响应 (IVR) 、呼叫控制，以及访问呼叫和会议实时音频流和/或视频流，包括桌面和应用共享。

我们添加了一个新部分，介绍了如何创建和开发通话和联机会议机器人，从概述 [开始](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。

## <a name="image-enlarge-support"></a>图像放大支持

现在机器人可以指示允许放大 Teams 自适应卡片中共享的图像。 这适用于通过自动程序共享详细的分步视觉指南等方案，否则用户可能很难阅读这些指南。 若要使图像可展开，只需标记它 `allowExpand: true` ，如下所示。

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
这会使 Teams Web/桌面客户端在将鼠标悬停在图像上时呈现元素，以允许用户展开图像。

