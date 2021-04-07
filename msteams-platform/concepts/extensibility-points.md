---
title: Teams 应用的入口点
author: heath-hamilton
description: 介绍用户可以在 Teams 中发现和使用应用的地方。
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 72ce2620160f854bbe458821db01e91d2d9f62cd
ms.sourcegitcommit: 098d38dd947e87e69d289b99e807bea2d95c42f9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2020
ms.locfileid: "49713625"
---
# <a name="entry-points-for-teams-apps"></a>Teams 应用的入口点

Teams 平台提供了一组灵活的入口点，用户可以在其中发现和使用你的应用。 应用程序非常简单，只需在选项卡或多维应用中嵌入现有 Web 内容，用户跨多个上下文进行交互。

最成功的应用将本机为 Teams，因此请仔细规划应用的入口点。

## <a name="teams-channels-and-chats"></a>团队、频道和聊天

团队、频道和聊天是协作空间。 这些上下文中的应用可供该空间的每个人使用，通常侧重于其他工作流或解锁新的社交交互。

下面说明在协作上下文中通常使用 Teams 应用功能的方式：

* [**选项卡**](~/tabs/what-are-tabs.md)为团队、频道或群组聊天配置全屏嵌入的 Web 体验。 所有成员交互处理基于 Web 的相同内容，因此普通单页应用体验。

* [**邮件扩展**](~/messaging-extensions/what-are-messaging-extensions.md)是一种快捷方式，适用于在对话中插入外部内容或在不离开 Teams 的情况下对邮件采取措施。 从公共 URL 共享内容时，取消链接将提供丰富的内容。

* [**自动**](~/bots/what-are-bots.md)通过聊天和响应事件（例如添加新成员或重命名频道）与对话成员交互。 团队、频道或组的所有成员都可以看到这些上下文中与机器人的对话，因此自动对话应该与所有人相关。

* [**Web 部件和连接器**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)外部服务将消息发布到对话中，用户可将邮件发送到服务。

* [**Microsoft Graph REST API**](https://docs.microsoft.com/graph/teams-concept-overview)团队、频道和群组聊天的数据，帮助自动执行和管理 Teams 流程。

## <a name="personal-apps"></a>个人应用

[个人应用](~/concepts/design/personal-apps.md) 专注于与单个用户的交互。 此上下文中的体验是每位用户所特有的。

下面说明在个人上下文中通常使用 Teams 功能的方法：

* [**自动**](~/bots/what-are-bots.md)用户进行一对一对话。 需要多次对话或提供仅与特定用户相关的通知的自动程序最适合个人应用。

* [**选项卡**](~/tabs/what-are-tabs.md)可提供全屏嵌入的 Web 体验，对查看该体验的用户有意义。

## <a name="examples"></a>示例

Teams 应用设计指南提供详细的视觉效果，展示用户在何处可以找到和使用 Teams 应用。

> [!div class="nextstepaction"]
> [查看 Teams 应用设计指南](../concepts/design/design-teams-app-overview.md)
