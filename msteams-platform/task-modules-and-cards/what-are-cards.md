---
title: 卡片
description: 介绍卡以及如何在机器人、连接器和消息传递扩展中使用
ms.localizationpriority: medium
keywords: 连接器机器人卡片消息传递
ms.topic: overview
ms.openlocfilehash: 1f443dd72acd263901d39311465a368fbeb59f1b
ms.sourcegitcommit: d247a03ff53f058f11b94958473ae2e8962f2984
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2021
ms.locfileid: "61061956"
---
# <a name="cards"></a>卡片

卡片是用户界面， (UI) 或相关信息的容器。 卡片可以有多个属性和附件，可以包含按钮，可触发 [卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。 使用卡片，您可以将信息组织到组中，并使用户能够与信息的特定部分进行交互。

适用于自动Teams支持以下类型的卡：
 
- 自适应卡片
- Hero card
- 列表卡
- Office 365 连接器卡
- 收据卡
- 登录卡
- 缩略图卡片
- 卡片集合

可以使用 Markdown 或 HTML 向卡片添加格式文本格式，具体取决于卡片类型。 聊天机器人和邮件扩展使用的卡片Microsoft Teams、添加和响应这些卡片操作、 `openUrl` `messageBack` 和 `imBack` `invoke` `signin` 。

Teams三个不同位置使用卡片：

* 连接器
* 机器人
* 消息传递扩展

## <a name="cards-in-connectors"></a>连接器中的卡

卡片最初定义为 Outlook 和 Office 365 的一部分，现在用作 Office 365 连接器的一部分。 与许多Office 365一样，Teams支持连接器。 有关详细信息，请参阅 Office 365 [Connectors for Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。 可以在可操作邮件卡参考 中查找连接器中卡片 [的规范](/outlook/actionable-messages/card-reference)。

## <a name="cards-in-bots"></a>机器人中的卡片

该Microsoft Bot Framework添加了一组自动程序可用作自动程序消息一部分的预定义卡片，从而扩展了卡片规范。 Teams使用 Bot Framework 支持自动程序，但它支持一组不同的这些卡。 有关 Bot Framework 中卡片的常规信息，请参阅向邮件 [添加富卡片附件](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)。 这些卡片在卡片中称为Teams。

自动程序Teams简单卡片、连接器卡或自适应卡片。 [卡片类型](~/task-modules-and-cards/cards/cards-reference.md)提供有关卡片的信息，受 Teams。

## <a name="cards-in-messaging-extensions"></a>邮件扩展中的卡片

[邮件扩展还可以](~/messaging-extensions/what-are-messaging-extensions.md) 返回卡片。 邮件扩展可以使用简单的卡片、连接器卡或自适应卡片。 这些卡片位于 [卡片类型中](~/task-modules-and-cards/cards/cards-reference.md)。

## <a name="types-of-cards"></a>卡片类型

所有卡片由Teams在[卡片类型中列出](~/task-modules-and-cards/cards/cards-reference.md)。 本参考还介绍了自动程序框架卡和自动程序中Teams。

## <a name="adaptive-cards"></a>自适应卡

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

[自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)是 Microsoft 产品中一种新的跨产品规范，适用于机器人、Cortana、Outlook和Windows。 对于新开发，推荐使用Teams类型。 有关自适应卡片团队的常规信息，请参阅 [自适应卡片概述](/adaptive-cards)。 你可在使用现有 Hero 卡片、卡片和缩略图卡Office 365任何位置使用自适应卡片。

除了自适应卡片，Teams支持两种其他类型的卡片：

* 连接器卡：用作连接器Office 365的一部分。
* 简单卡片：从 Bot Framework 使用，例如缩略图和 Hero 卡片。

### <a name="type-ahead-search-in-adaptive-cards"></a>在自适应卡片中键入提前搜索  

键入作为自适应卡片中的输入控件添加的提前 [搜索，从](~/task-modules-and-cards/cards/dynamic-search.md) 动态加载的数据集实现动态搜索体验。 它还允许用户在具有有限数量的选择的列表内执行提前键入静态搜索。 移动和桌面客户端支持提前键入动态搜索体验。 

### <a name="adaptive-cards-and-incoming-webhooks"></a>自适应卡片和传入 Webhook

> [!VIDEO https://www.youtube-nocookie.com/embed/y5pbJI43Zvg]

> [!NOTE]
> * 完全支持所有本机自适应卡片架构元素（除外 `Action.Submit` ）。
> * 支持的操作包括 Action.OpenURL、Action.ShowCard、Action.ToggleVisibility 和 [**Action.Execute。**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute) [](https://adaptivecards.io/explorer/Action.OpenUrl.html) [](https://adaptivecards.io/explorer/Action.ShowCard.html) [](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)

通过传入 Webhook 的自适应卡片，可以使用自适应卡片的丰富而灵活的功能。 它使用传入 Webhook 从 web 服务Teams传入 Webhook 发送数据。

## <a name="support-for-aad-object-id-and-upn-in-user-mention"></a>支持AAD提及中的对象 ID 和 UPN 

具有自适应卡片的机器人支持用户提及 ID，AAD对象 ID 和用户原则名称 (UPN) 以及现有 ID。 传入 Webhook 开始支持自适应卡片中的用户提及，AAD对象 ID 和 UPN。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [卡片类型](~/task-modules-and-cards/cards/cards-reference.md)

## <a name="see-also"></a>另请参阅

* [格式化卡片Teams](~/task-modules-and-cards/cards/cards-format.md)
* [设计自适应卡片](~/task-modules-and-cards/cards/design-effective-cards.md)
* [机器人中的自适应卡片](../bots/how-to/conversations/conversation-messages.md#adaptive-cards)