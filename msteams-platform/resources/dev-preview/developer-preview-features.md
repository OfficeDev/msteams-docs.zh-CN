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
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Microsoft 团队的公共开发人员预览版中的功能

开发人员预览包括以下新功能：

## <a name="tabs-single-sign-on-sso"></a> (SSO) 的选项卡单一登录

现在，你可以使用 [单一登录 (SSO) ](~/tabs/how-to/authentication/auth-aad-sso.md) 使用 web 内容页中的团队 JavaScript SDK 登录桌面和手机上的用户并对其进行身份验证。 其中一项好处是用户永远不需要登录;在用户使用其配置文件同意应用程序之后，将自动登录到其选项卡 (包括移动) 。

我们的开发人员预览版在清单版本1.5 及更高版本中可用。 我们的当前实施只能获取有限数量的图形 Api，但我们提供了使用我们现有的身份验证 API 获取其他图形 Api 的替代方法。

## <a name="calls-and-online-meeting-bots"></a>呼叫和联机会议 bot

通过添加 [用于呼叫和联机会议的 Microsoft Graph api](/graph/api/resources/communications-api-overview?view=graph-rest-beta)，microsoft 团队应用现在可以使用语音和视频以丰富的方式与用户进行交互。 这些 Api 允许您添加新的应用程序功能，如交互式语音响应 (IVR) 、呼叫控制以及对呼叫和会议（包括桌面和应用程序共享）的实时音频和/或视频流的访问。

我们已添加了有关如何创建和开发呼叫和联机会议 bot 的新部分，从 [概述](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)开始。

## <a name="image-enlarge-support"></a>图像放大支持

现在，bot 可以指示允许放大团队中的自适应卡片中共享的图像。 这对诸如通过 bot 共享详细的分步可视化指南等方案很有用，否则用户可能很难阅读。 若要使图像可扩展，只需对其进行标记，如下 `allowExpand: true` 所示。

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
这将导致团队 web/桌面客户端在将鼠标悬停在图像上时呈现元素，以允许用户扩展图像。

