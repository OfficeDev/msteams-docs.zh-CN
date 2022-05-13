---
title: 卡片
description: 介绍卡片及其在机器人、连接器和消息扩展中的使用方式
ms.localizationpriority: high
keywords: 连接器机器人卡片消息传递
ms.topic: overview
ms.openlocfilehash: 23ac23928a1fa1a31e41bd5b553612bf02c23728
ms.sourcegitcommit: 05285653b2548e0b39e788cd07d414ac87ba3eaf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2022
ms.locfileid: "65191255"
---
# <a name="cards"></a>卡片

卡片是装载简短信息或相关信息的用户界面 (UI) 容器。 卡片可以有多个属性和附件，可以包含按钮，可触发 [卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。 使用卡片，可以将信息组织到组中，让用户有机会与信息的特定部分进行交互。

Teams 机器人支持以下类型的卡片：

* 自适应卡片
* 主图卡片
* 列表卡
* Office 365 连接器卡
* 收据卡
* 登录卡
* 缩略图卡片
* 卡片集合

可以使用 Markdown 或 HTML 向卡片添加格式文本格式，具体取决于卡片类型。 Microsoft Teams 中机器人和消息扩展使用的卡片，添加和响应这些卡片操作、`openUrl`、`messageBack`、`imBack`、`invoke` 和 `signin`。

Teams 在三个不同的位置使用卡片：

* 连接器
* 机器人
* 消息扩展

## <a name="cards-in-connectors"></a>连接器中的卡

卡片最初定义为 Outlook 和 Office 365 的一部分，现在用作 Office 365 连接器的一部分。 与许多 Office 365 应用程序一样，Teams 支持连接器。 有关详细信息，请参阅[创建 Office 365 连接器](../webhooks-and-connectors/how-to/connectors-creating.md)。 可以在 [ 可操作邮件卡参考 ](/outlook/actionable-messages/card-reference) 中找到连接器中的卡片规范。

## <a name="cards-in-bots"></a>机器人中的卡片

Microsoft Bot Framework 通过添加一组预定义卡来扩展卡规范，机器人可以将其用作机器人消息的一部分。 Teams 支持使用 Bot Framework 的机器人，但它支持一组不同的卡片。 有关Bot Framework 中卡的常规信息，请参阅 [将富卡附件添加到邮件](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)。 这些卡在 Teams 中称为简单卡片。

Teams 中的机器人可以使用简单卡片、连接器卡或自适应卡片。 [类型卡](~/task-modules-and-cards/cards/cards-reference.md) 提供有关卡的信息，由 Teams 中的机器人支持。

## <a name="cards-in-message-extensions"></a>消息扩展中的卡片

[消息扩展](~/messaging-extensions/what-are-messaging-extensions.md) 还可以返回卡片。 消息扩展可以使用简单卡片、连接器卡或自适应卡片。 这些卡片位于 [类型卡中](~/task-modules-and-cards/cards/cards-reference.md)。

## <a name="types-of-cards"></a>卡片类型

Teams 使用的所有卡都列在[类型卡中](~/task-modules-and-cards/cards/cards-reference.md)。 本参考还介绍了 Teams 中Bot Framework卡和卡片之间的差异。

## <a name="adaptive-cards"></a>自适应卡

[自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)是一种跨产品的规范，可应用于包括机器人、Cortana、Outlook 和 Windows 在内的各种 Microsoft 产品。 它是新 Teams 开发推荐使用的卡片类型。 有关自适应卡片团队的常规信息，请参阅 [自适应卡片概述](/adaptive-cards)。 可在使用现有主图卡、Office 365 卡和缩略图卡的任何位置使用自适应卡片。

除了自适应卡片，Teams 支持两种其他类型的卡片：

* 连接器卡片：用作 Office 365 连接器的一部分。
* 简单卡片：从 Bot Framework 使用，例如缩略图和主图卡片。

### <a name="people-picker-in-adaptive-cards"></a>自适应卡片中的人员选取器

[人员选取器](cards/people-picker.md#people-picker-in-adaptive-cards) 添加为自适应卡片中的输入控件，可以搜索和选择人员。 可以在聊天、频道、任务模块和选项卡中使用。 移动和桌面客户端支持人员选取器，提供了内联键入体验。

### <a name="type-ahead-search-in-adaptive-cards"></a>在自适应卡片中键入提前搜索  

在自适应卡片中添加为输入控件的提前键入搜索，以便从动态加载的数据集中实现 [动态搜索](~/task-modules-and-cards/cards/dynamic-search.md) 体验。 它还允许用户在具有有限数量的选择的列表内执行提前键入静态搜索。 移动和桌面客户端支持提前键入动态搜索体验。

### <a name="adaptive-cards-and-incoming-webhooks"></a>自适应卡片和传入 Webhook

> [!NOTE]
>
> * 完全支持所有本机自适应卡片架构元素（`Action.Submit`除外）。
> * 受支持的操作包括 [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html)、[**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)、[**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)和 [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)。

借助传入 Webhook 自适应卡片，可以使用自适应卡片的丰富灵活功能。 它使用 Teams 中的传入 Webhook 从其 Web 服务发送数据。

## <a name="support-for-azure-ad-object-id-and-upn-in-user-mention"></a>在用户提及中支持 Azure AD 对象 ID 和 UPN

具有自适应卡片机器人支持用户提及 ID，例如 Microsoft Azure Active Directory (Azure AD) 对象 ID 和用户主体名称 (UPN)，以及现有 ID。 传入 Webhook 开始支持使用 AAD 对象 ID 和 UPN 在自适应卡片中提及用户。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [卡片类型](~/task-modules-and-cards/cards/cards-reference.md)

## <a name="see-also"></a>另请参阅

* [在 Teams 中格式卡片](~/task-modules-and-cards/cards/cards-format.md)
* [设计自适应卡片](~/task-modules-and-cards/cards/design-effective-cards.md)
* [机器人中的自适应卡片](../bots/how-to/conversations/conversation-messages.md#adaptive-cards)
