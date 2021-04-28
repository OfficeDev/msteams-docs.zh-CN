---
title: Teams 应用的入口点
author: heath-hamilton
description: 介绍用户可以在 Teams 中发现和使用应用的地方。
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: f2bdb35c76bdb7487e66a0e6b9ad01c6da9e04f8
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058318"
---
# <a name="entry-points-for-teams-apps"></a>Teams 应用的入口点

Teams 平台提供了一组灵活的入口点，例如团队、频道和聊天，用户可以在这里发现和使用你的应用。 应用程序非常简单，只需在选项卡或多维应用中嵌入现有 Web 内容，用户跨多个上下文进行交互。
成功应用是 Teams 的原生应用，因此请谨慎选择应用的入口点。

## <a name="shared-app-experiences"></a>共享的应用体验

团队、频道和聊天是协作空间。 这些上下文中的应用程序可供该空间中的每个人使用。 协作空间通常侧重于其他工作流或解锁新的社交交互。

以下列表显示了 Teams 应用功能在协作上下文中的常见使用方式：

* [**选项卡**](~/tabs/what-are-tabs.md)为团队、频道或群组聊天配置全屏嵌入的 Web 体验。 所有成员与基于 Web 的相同内容进行交互，因此无状态单页应用体验很典型。

* [**邮件扩展**](~/messaging-extensions/what-are-messaging-extensions.md)是一种快捷方式，适用于在对话中插入外部内容或在不离开 Teams 的情况下对邮件采取措施。 [从公用 URL](~/messaging-extensions/how-to/link-unfurling.md) 共享内容时，链接展开可提供丰富的内容。

* [**机器人**](~/bots/what-are-bots.md) 通过聊天和响应事件（例如添加新成员或重命名频道）与对话成员进行交互。 
   > [!NOTE]
   > 与自动程序在这些上下文中的对话对团队、频道或组的所有成员都可见，因此自动程序对话必须与所有人相关。

* [**Web 部件和连接器**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)外部服务将消息发布到对话中，用户可将邮件发送到服务。

* [**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview)团队、频道和群组聊天的数据，帮助自动执行和管理 Teams 流程。

## <a name="personal-app-experiences"></a>个人应用体验

[个人应用](../concepts/design/personal-apps.md) 专注于与单个用户的交互。 此上下文中的体验是每位用户所特有的。

以下列表显示了 Teams 功能在个人上下文中的常见使用方式：

* [**自动**](~/bots/what-are-bots.md)用户进行一对一对话。 需要多次对话或提供仅与特定用户相关的通知的自动程序最适合个人应用。

* [**选项卡**](~/tabs/what-are-tabs.md) 提供对查看它的用户有意义的全屏嵌入式 Web 体验。

## <a name="see-also"></a>另请参阅

- [Teams 应用设计指南](../concepts/design/design-teams-app-overview.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [了解用例](../concepts/design/understand-use-cases.md)
