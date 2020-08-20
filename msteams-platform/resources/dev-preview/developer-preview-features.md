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
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Microsoft Teams 公共开发者预览版中的功能

开发人员预览包括以下新功能：

## <a name="adaptive-cards-v12-support"></a>自适应卡片 v1.2 支持

现已 [向正式公共提供对](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) Teams 中的自适应卡片 v1.2 的支持。 但是 [，Teams 平台](https://adaptivecards.io/explorer/Media.html) 上的自适应卡片 v1.2 中当前不支持媒体元素。

## <a name="tabs-single-sign-on-sso"></a>SSO 项目以选项卡 (单一) 

现在，你可以 [使用单一登录登录到 (SSO) ， ](~/tabs/how-to/authentication/auth-aad-sso.md) 以通过 Web 内容页中的 Teams JavaScript SDK 登录和移动台式用户和移动设备上的用户。 优势之一是，用户永远不必须登录;如果他们已使用其个人资料同意应用，就会自动登录 (包括移动应用商店页面的) 。

我们的开发人员预览版在清单版本 1.5 及更高版本中可用。 尽管我们的当前实现只能获取有限的 Graph API，但我们提供了一种解决办法，以使用我们现有的身份验证 API 获取额外的 Graph API。

## <a name="calls-and-online-meeting-bots"></a>呼叫和联机会议机器人

通过为呼叫和 [在线会议添加 Microsoft Graph API，Microsoft](/graph/api/resources/communications-api-overview?view=graph-rest-beta)Teams 应用现在可以使用语音和视频以丰富的方式与用户进行交互。 通过这些 API，可以添加新应用功能，如交互式语音响应 (IVR) 、呼叫控制，并访问通话和会议（包括桌面和应用共享）的实时音频和/或视频流。

我们添加了有关如何创建和开发电话和联机会议机器人（从概述开始）的新 [部分](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。
