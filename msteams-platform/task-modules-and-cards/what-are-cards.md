---
title: 卡
description: 介绍卡以及如何在机器人、连接器和消息传递扩展中使用
localization_priority: Normal
keywords: 连接器机器人卡片消息传递
ms.topic: overview
ms.openlocfilehash: f895423e5755dd85a7618b8907c4c3b0acbc3cf4
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140542"
---
# <a name="cards"></a>卡

卡片是用户界面， (UI) 或相关信息的容器。 卡片可以有多个属性和附件，也可以包括按钮，可触发 [卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。 使用卡片，您可以将信息组织到组中，并使用户能够与信息的特定部分进行交互。

适用于 Teams 的机器人支持以下类型的卡片：自适应卡片、人物卡片、列表卡、Office 365 连接器卡、回执卡、登录卡、缩略图卡和卡片集合。 可以使用 Markdown 或 HTML 将格式文本格式添加到卡片，具体取决于卡片类型。 聊天机器人和邮件扩展中使用的Microsoft Teams、添加和响应这些卡片操作、 和 `openUrl` `messageBack` `imBack` `invoke` `signin` 。

Teams三个不同位置使用卡片：

* 连接器
* 机器人
* 消息传递扩展

## <a name="cards-in-connectors"></a>连接器中的卡

卡片最初定义为 Outlook 和 Office 365 的一部分，现在用作 Office 365 连接器的一部分。 与许多Office 365一样，Teams支持连接器。 有关详细信息，请参阅 Office 365 [Connectors for Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。 可以在可操作邮件卡参考 中查找连接器中卡片 [的规范](/outlook/actionable-messages/card-reference)。

## <a name="cards-in-bots"></a>机器人中的卡片

该Microsoft Bot Framework添加了一组自动程序可用作自动程序消息一部分的预定义卡片，从而扩展了卡规范。 Teams使用 Bot Framework 支持自动程序，但它支持一组不同的这些卡。 有关 Bot Framework 中卡片的常规信息，请参阅向邮件 [添加富卡片附件](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)。 这些卡片在卡片中称为Teams。

自动程序Teams简单卡片、连接器卡或自适应卡片。 [卡片类型](~/task-modules-and-cards/cards/cards-reference.md)提供有关卡片的信息，受 Teams。

## <a name="cards-in-messaging-extensions"></a>邮件扩展中的卡片

[邮件扩展还可以](~/messaging-extensions/what-are-messaging-extensions.md) 返回卡片。 邮件扩展可以使用简单的卡片、连接器卡或自适应卡片。 这些卡片位于 [卡片类型中](~/task-modules-and-cards/cards/cards-reference.md)。

## <a name="types-of-cards"></a>卡片类型

所有卡片由Teams在[卡片类型中列出](~/task-modules-and-cards/cards/cards-reference.md)。 本参考还介绍了自动程序框架卡和自动程序中的Teams。

## <a name="adaptive-cards"></a>自适应卡

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

[自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)是 Microsoft 产品中一种新的跨产品规范，适用于自动程序、Cortana、Outlook 和 Windows。 对于新开发，推荐使用Teams类型。 有关自适应卡片团队的常规信息，请参阅 [自适应卡片概述](/adaptive-cards)。 可在使用现有 Hero 卡片、卡片和缩略图卡Office 365任何位置使用自适应卡片。

除了自适应卡片，Teams支持两种其他类型的卡片：

* 连接器卡：用作连接器Office 365的一部分。
* 简单卡片：从 Bot Framework 使用，例如缩略图和 Hero 卡片。

### <a name="adaptive-cards-and-incoming-webhooks"></a>自适应卡片和传入 Webhook

> [!VIDEO https://www.youtube-nocookie.com/embed/y5pbJI43Zvg]

> [!NOTE]
> * 完全支持所有本机自适应卡片架构元素（除外 `Action.Submit` ）。
> * 支持的操作包括 Action.OpenURL、Action.ShowCard、Action.ToggleVisibility [**和Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)。 [](https://adaptivecards.io/explorer/Action.OpenUrl.html) [](https://adaptivecards.io/explorer/Action.ShowCard.html) [](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)

通过传入 Webhook 的自适应卡片，可以使用自适应卡片的丰富而灵活的功能。 它使用传入 Webhook 从 web 服务Teams传入 Webhook 发送数据。

## <a name="see-also"></a>另请参阅

* [格式化卡片Teams](~/task-modules-and-cards/cards/cards-format.md)
* [设计自适应卡片](~/task-modules-and-cards/cards/design-effective-cards.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [卡片类型](~/task-modules-and-cards/cards/cards-reference.md)