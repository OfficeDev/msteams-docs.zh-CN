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
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>公共服务开发者预览版中的Microsoft Teams

> [!NOTE]
> 此页面将于 2021 年 6 月弃用。 有关适用于开发人员预览的功能的信息，请参阅 [新增功能？](~/whats-new.md)

开发人员预览版包括以下新功能：

## <a name="app-customization"></a>应用自定义

现在，您可以定义一组选定属性，Teams管理员可基于其组织需求自定义或重新品牌。 有关详细信息，请参阅 [应用自定义功能](~/concepts/design/design-teams-app-overview.md)。

## <a name="tabs-single-sign-on-sso"></a>选项卡单一登录 (SSO) 

现在，可以使用[SSO](~/tabs/how-to/authentication/auth-aad-sso.md) (单一登录) Web 内容页中的 Teams JavaScript SDK 在桌面和移动设备上登录并验证用户身份。 其中一个好处是用户永远不登录;并且一旦他们同意使用其配置文件的应用：他们将自动登录到其选项卡 (包括移动) 。

我们的开发人员预览在清单版本 1.5 及更大版本中可用。 我们的当前实现只能获取有限数量的Graph API，但我们提供了一种解决方法，以便使用现有身份验证 API Graph其他应用程序 API。

## <a name="calls-and-online-meeting-bots"></a>通话和联机会议机器人

通过添加用于Graph和联机会议的[Microsoft](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)GRAPH API，Microsoft Teams应用现在可以使用语音和视频以丰富的方式与用户进行交互。 这些 API 允许你添加新的应用功能，如交互式语音响应 (IVR) 、呼叫控制，以及访问通话和会议实时音频流和/或视频流，包括桌面应用应用共享。

从概述 开始，我们添加了一个新部分，介绍了如何创建和开发通话和联机 [会议机器人](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。


## <a name="image-enlarge-support"></a>图像放大支持

现在机器人可以指示在自适应卡片中共享的图像Teams放大。 这适用于通过机器人共享详细的分步视觉指南等方案，否则用户可能很难阅读这些指南。 若要使图像可展开，只需如下所示 `allowExpand: true` 标记它。

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
这会使Teams/桌面客户端将元素悬停在图像上，以允许用户展开图像。
