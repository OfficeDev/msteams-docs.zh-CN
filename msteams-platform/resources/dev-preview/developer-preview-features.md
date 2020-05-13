---
title: 公共开发人员预览版中的功能
description: 介绍 Microsoft 团队的公共开发人员预览版中的功能
keywords: 团队预览开发人员功能
ms.openlocfilehash: 7ed442072779917dcc5db3ebcb4afaac9db0407f
ms.sourcegitcommit: b9e8839858ea8e9e33fe5e20e14bbe86c75fd510
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "44210699"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Microsoft 团队的公共开发人员预览版中的功能

开发人员预览包括以下新功能：

## <a name="adaptive-cards-v12-support"></a>自适应卡片 1.2 1.2 支持

团队中的[自适应卡片 v 1.2](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)的支持现在可供一般大众使用。 但是，在团队平台上，自适应卡上的1.2 版中目前不支持[媒体元素](https://adaptivecards.io/explorer/Media.html)。

## <a name="tabs-single-sign-on-sso"></a>选项卡单一登录（SSO）

现在，您可以使用[单一登录（SSO）](~/tabs/how-to/authentication/auth-aad-sso.md) ，在桌面和移动设备上使用 web 内容页中的团队 JavaScript SDK 登录并验证用户。 其中一项好处是用户永远不需要登录;在用户使用其配置文件同意应用程序之后，将自动登录到其选项卡（包括移动设备）。

我们的开发人员预览版在清单版本1.5 及更高版本中可用。 我们的当前实施只能获取有限数量的图形 Api，但我们提供了使用我们现有的身份验证 API 获取其他图形 Api 的替代方法。

## <a name="personal-apps-static-tabs-and-1-1-bots-enabled-on-mobile"></a>移动设备上启用的个人应用（静态选项卡和 1-1 bot）

安装的个人应用（静态选项卡和 1-1 bot）现在在移动设备上的应用程序托盘中可用。 请参阅[mobile 的设计指南以](~/tabs/design/tabs-mobile.md)了解设计指南。 只能从桌面或 web 客户端安装应用程序，安装后最长可在移动设备上使用4小时。

这包括系统管理员通过[应用安装策略](/microsoftteams/teams-app-setup-policies)预固定应用的能力。 已固定的应用程序将显示在应用抽屉中。

## <a name="calls-and-online-meeting-bots"></a>呼叫和联机会议 bot

通过添加[用于呼叫和联机会议的 Microsoft Graph api](/graph/api/resources/communications-api-overview?view=graph-rest-beta)，microsoft 团队应用现在可以使用语音和视频以丰富的方式与用户进行交互。 这些 Api 允许您添加新的应用程序功能，如交互式语音响应（IVR）、呼叫控制以及对呼叫和会议（包括桌面和应用程序共享）的实时音频和/或视频流的访问。

我们已添加了有关如何创建和开发呼叫和联机会议 bot 的新部分，从[概述](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)开始。
