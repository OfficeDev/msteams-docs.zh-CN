---
title: 卡片介绍
description: 介绍卡及其在机器人、连接器和邮件扩展中的使用方式
keywords: 连接器机器人卡片消息传递
ms.openlocfilehash: 00c649a1339f05b782e03a2c0db5cba2445f66bc
ms.sourcegitcommit: 23ceb25d07a76f03ffe92cf1ac578b7c50b0bafc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/07/2021
ms.locfileid: "49777922"
---
# <a name="cards"></a>卡

*卡片* 是用户界面， (UI) 容器提供简短或相关的信息。 卡片可以有多个属性和附件。 卡片可以包括可触发卡片操作 [按钮](~/task-modules-and-cards/cards/cards-actions.md)。

## <a name="adaptive-cards"></a>自适应卡片

[自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) 是 Microsoft 产品（包括 Bot、Cortana、Outlook 和 Windows）中卡片的一种新的跨产品规范。 它们是新 Teams 开发的建议卡片类型。 有关自适应卡片团队的常规信息，请参阅 [自适应卡片概述](/adaptive-cards)。 可以在可以使用现有 Hero 卡、Office365 卡和缩略图卡片的任何位置使用自适应卡片。

除了自适应卡片之外，Teams 还支持两种其他类型的卡片：

* 连接器卡，用作 Office 365 连接器的一部分。
* 自动程序框架中的简单卡片，如缩略图和 Hero 卡片。

这些卡片类型在 Teams 卡片参考中 [进行了更全面介绍](~/task-modules-and-cards/cards/cards-reference.md)。

Teams 在三个不同位置使用卡片：

* 连接器
* 机器人
* 消息传递扩展

## <a name="adaptive-cards-and-incoming-webhooks"></a>自适应卡片和传入 Webhook

> [!NOTE]
>
> ✔ 完全支持所有本地自适应卡架构元素（`Action.Submit` 除外）。
>
> ✔操作包括 [**Action.OpenURL、Action.ShowCard**](https://adaptivecards.io/explorer/Action.OpenUrl.html)和 [**Action.ToggleVisibility。**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) [](https://adaptivecards.io/explorer/Action.ShowCard.html)

## <a name="cards-in-connectors"></a>连接器中的卡片

卡片最初定义为 Outlook 和 Office 365 的一部分，并用作 Office 365 连接器的一部分。 与许多 Office 365 应用程序一样，Teams 支持连接器。 你可以了解有关适用于 Microsoft Teams [的 Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)连接器中连接器的更多信息，并可在可操作邮件卡参考中查找连接器中卡片 [的规范](/outlook/actionable-messages/card-reference)。

## <a name="cards-in-bots"></a>聊天机器人中的卡片

Microsoft Bot Framework 通过添加一组自动程序可用作自动程序消息一部分的预定义卡片来扩展卡片规范。 Teams 支持使用 Bot Framework 的机器人，但它支持一组略有不同的这些卡。 有关 Bot Framework 中卡片的常规信息，请参阅"向邮件[添加富卡片附件"。](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards) 这些卡片在 Teams *中称为* 简单卡片。

Teams 中的机器人可以使用任何类型的卡片：简单、连接器或自适应。 Teams 中的机器人支持的卡片在 Teams 卡片参考 [中详细说明](~/task-modules-and-cards/cards/cards-reference.md)。  

## <a name="cards-in-messaging-extensions"></a>邮件扩展中的卡片

[邮件扩展还可以](~/messaging-extensions/what-are-messaging-extensions.md) 返回卡片。 邮件扩展可以使用任何类型的卡片：简单、连接器或自适应。 这些卡片位于 Teams 卡片 [参考中](~/task-modules-and-cards/cards/cards-reference.md)。

## <a name="card-reference"></a>卡片参考

Teams 使用的所有卡片都列在 Teams 卡片 [参考中](~/task-modules-and-cards/cards/cards-reference.md)。 此参考还介绍了 Teams 中的自动程序框架卡和卡之间的差异。
