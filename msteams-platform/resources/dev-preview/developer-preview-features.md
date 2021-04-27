---
title: 公共服务中的开发者预览版
description: 详细介绍 Microsoft Teams 公共网站中的开发者预览版
ms.topic: reference
localization_priority: Normal
keywords: teams 预览开发人员功能
ms.openlocfilehash: 38acccedacb86437f5e6c949b674c0a62bbbd63c
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020616"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Microsoft Teams 公共开发者预览版中的功能

开发人员预览版包括以下新功能：

## <a name="app-customization"></a>应用自定义

现在，你可以定义一组精选属性，Teams 管理员可以根据组织需求自定义或重新品牌。 有关详细信息，请参阅 [应用自定义功能](~/concepts/design/design-teams-app-overview.md)。

## <a name="tabs-single-sign-on-sso"></a>选项卡单一登录 (SSO) 

现在，可以使用 [SSO ](~/tabs/how-to/authentication/auth-aad-sso.md) (单一登录) Web 内容页中的 Teams JavaScript SDK 在桌面和移动设备上登录并验证用户身份。 其中一个好处是用户永远不登录;并且一旦他们同意使用其配置文件的应用：他们将自动登录到其选项卡 (包括移动) 。

我们的开发人员预览在清单版本 1.5 及更大版本中可用。 我们的当前实现只能获取有限数量的 Graph API，但我们提供了一种解决方法，以使用现有的身份验证 API 获取其他 Graph API。

## <a name="calls-and-online-meeting-bots"></a>通话和联机会议机器人

通过添加用于通话和联机会议的 [Microsoft Graph API，Microsoft](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)Teams 应用现在可以通过多种使用语音和视频的方式与用户进行交互。 这些 API 允许你添加新的应用功能，如交互式语音响应 (IVR) 、呼叫控制，以及访问通话和会议实时音频流和/或视频流，包括桌面应用应用共享。

从概述 开始，我们添加了一个新部分，介绍了如何创建和开发通话和联机 [会议机器人](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。


## <a name="image-enlarge-support"></a>图像放大支持

现在机器人可以指示允许放大 Teams 自适应卡片中共享的图像。 这适用于通过机器人共享详细的分步视觉指南等方案，否则用户可能很难阅读这些指南。 若要使图像可展开，只需如下所示 `allowExpand: true` 标记它。

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
这会使 Teams Web/桌面客户端将元素悬停在图像上方，以允许用户展开图像。

