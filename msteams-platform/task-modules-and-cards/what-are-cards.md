---
title: 卡片介绍
description: 介绍卡及其在机器人、连接器和消息传递扩展中的使用方式
localization_priority: Normal
ms.topic: conceptual
keywords: 连接器机器人卡片消息传递
ms.openlocfilehash: 77dcbb7d0472b584623e878df956a6165296f4cf
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088750"
---
# <a name="cards"></a>卡

*卡片* 是用户界面， (UI) 或相关信息的容器。 卡片可以有多个属性和附件。 卡片可以包括可触发卡片操作 [的按钮](~/task-modules-and-cards/cards/cards-actions.md)。

## <a name="adaptive-cards"></a>自适应卡片

[自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)是 Microsoft 产品中新的跨产品规范，适用于机器人、Cortana、Outlook和Windows。 对于新开发，推荐使用Teams类型。 有关自适应卡片团队的常规信息，请参阅 [自适应卡片概述](/adaptive-cards)。 可以在可以使用现有 Hero 卡、Office365 卡和缩略图卡片的任何位置使用自适应卡片。

除了自适应卡片，Teams支持两种其他类型的卡片：

* 连接器卡，用作连接Office 365的一部分。
* 自动程序框架中的简单卡片，如缩略图和人物卡片。

这些卡片类型在卡片参考中[Teams更加完整](~/task-modules-and-cards/cards/cards-reference.md)。

Teams三个不同位置使用卡片：

* 连接器
* 机器人
* 消息传递扩展

## <a name="adaptive-cards-and-incoming-webhooks"></a>自适应卡片和传入 Webhook

> [!NOTE]
>
> ✔ 完全支持所有本地自适应卡架构元素（`Action.Submit` 除外）。
>
> ✔支持的操作包括 [**Action.OpenURL、Action.ShowCard、Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.OpenUrl.html)和Action.Exe [**cute**](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute)。 [](https://adaptivecards.io/explorer/Action.ShowCard.html) [](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)

## <a name="cards-in-connectors"></a>连接器中的卡片

卡片最初定义为 Outlook 和 Office 365 的一部分，并用作 Office 365 连接器的一部分。 与许多Office 365一样，Teams支持连接器。 可以了解有关 Office 365 [Connectors for Microsoft Teams](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)中连接器的更多信息，并可在可操作邮件卡参考 中查找连接器中的[卡规范](/outlook/actionable-messages/card-reference)。

## <a name="cards-in-bots"></a>自动程序中的卡片

该Microsoft Bot Framework添加了一组自动程序可用作自动程序消息一部分的预定义卡片，从而扩展了卡片规范。 Teams使用 Bot Framework 支持自动程序，但它支持这些卡的一组略有不同。 有关 Bot Framework 中的卡片的常规信息，请参阅向邮件 [添加富卡片附件](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)。 这些卡片在 *卡片中称为* Teams。

聊天机器人Teams任何类型的卡片：简单、连接器或自适应。 Teams中自动程序支持的Teams[卡参考中详细说明](~/task-modules-and-cards/cards/cards-reference.md)。  

## <a name="cards-in-messaging-extensions"></a>邮件扩展中的卡片

[邮件扩展还可以](~/messaging-extensions/what-are-messaging-extensions.md) 返回卡片。 邮件扩展可以使用任何类型的卡片：简单、连接器或自适应。 这些卡片位于"Teams[参考"中](~/task-modules-and-cards/cards/cards-reference.md)。

## <a name="card-reference"></a>卡片参考

所有由 Teams 使用的卡都列在Teams[卡参考中](~/task-modules-and-cards/cards/cards-reference.md)。 本参考还介绍了自动程序框架卡和自动程序中的Teams。
