---
title: 简介卡片
description: 描述卡片及其在 bot、连接器和邮件扩展中的使用方式
keywords: 连接器 bot 卡片消息传送
ms.openlocfilehash: 6d850f83183f12fa0c228a7a89b23e58f523e15b
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651654"
---
# <a name="cards"></a>卡

*卡片*是用户界面 (UI) 容器，用于简短的或相关的信息片段。 卡片可以具有多个属性和附件。 卡片可以包含可触发 [卡片操作](~/task-modules-and-cards/cards/cards-actions.md)的按钮。

## <a name="adaptive-cards"></a>自适应卡片

[自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card) 是 Microsoft 产品中卡片的一种新的矢量积规范，包括 Bot、Cortana、Outlook 和 Windows。 它们是新团队开发的推荐的卡片类型。 有关自适应卡片团队的一般信息，请参阅 [自适应卡片概述](/adaptive-cards)。 您可以使用自适应卡片随时随地使用现有的英雄卡片、Office365 卡片和缩略图卡。

除了自适应卡片之外，团队还支持其他两种类型的卡：

* 连接器卡，用作 Office 365 连接器的一部分。
* 来自 bot 框架的简单卡片，如缩略图和英雄卡片。

这些卡类型在 [团队卡片参考](~/task-modules-and-cards/cards/cards-reference.md)中的说明更完整。

团队在三个不同的位置使用卡片：

* 连接器
* 机器人
* 消息传递扩展

## <a name="adaptive-cards-and-incoming-webhooks"></a>自适应卡片和传入 webhook

> [!NOTE]
> 在作为 [公共开发者预览版计划](../resources/dev-preview/developer-preview-intro.md)的一部分的传入 webhook 中支持自适应卡片。 公共预览适用于早期访问和反馈。 尽管发布是稳定的，并且已进行了大量测试，但它并不适合在生产环境中使用。
>
> 在开发人员预览中，完全支持除之外的所有本机自适应卡架构元素 `Action.Submit` 。✔
>
> ✔支持的操作为 [**OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html)、 [**ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)和 [**action.togglevisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)。

## <a name="cards-in-connectors"></a>连接器中的卡片

卡片最初定义为 Outlook 和 Office 365 的一部分，并用作 Office 365 连接器的一部分。 与许多 Office 365 应用程序一样，团队支持连接器。 可以在 [Microsoft 团队的 Office 365 连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)中了解有关连接器的详细信息，并在可 [操作邮件卡参考](/outlook/actionable-messages/card-reference)中查找连接器中的卡的规范。

## <a name="cards-in-bots"></a>Bot 中的卡片

Microsoft Bot 框架通过添加一组预定义卡片来扩展智能卡规范，bot 可以将这些卡片用作 bot 邮件的一部分。 团队使用 Bot 框架支持 bot，但它支持的这些卡片集略有不同。 可以在 [将丰富的卡片附件添加到邮件](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)中找到机器人框架中卡片的常规信息。 这些卡片在团队中称为 *简单卡片* 。

团队中的 bot 可以使用任何类型的卡片：简单、连接器或自适应。 团队中的 bot 支持的卡片在 [团队卡片参考](~/task-modules-and-cards/cards/cards-reference.md)中详细介绍。  

## <a name="cards-in-messaging-extensions"></a>邮件分机中的卡片

[邮件扩展](~/messaging-extensions/what-are-messaging-extensions.md) 还可以返回一个卡片。 邮件扩展可以使用任何类型的卡片：简单、连接器或自适应。 这些卡片位于 " [团队卡片参考](~/task-modules-and-cards/cards/cards-reference.md)" 中。

## <a name="card-reference"></a>卡片参考

团队使用的所有卡片都列在 " [团队卡片" 参考](~/task-modules-and-cards/cards/cards-reference.md)中。 本参考还介绍了在团队中的 Bot 框架卡片和智能卡之间的区别。
