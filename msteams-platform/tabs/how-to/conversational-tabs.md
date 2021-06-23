---
title: 创建对话选项卡
author: surbhigupta
description: 为频道选项卡创建对话子实体聊天
keywords: Teams 选项卡频道可配置
ms.topic: conceptual
ms.author: lomeybur
ms.openlocfilehash: 343cbe26ded2792489640ae3d86ec94c7c6db72b
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069232"
---
# <a name="create-conversational-tabs"></a>创建对话选项卡

会话子实体提供了一种方法，允许用户就选项卡中的子实体（如特定任务、患者和销售机会）展开对话，而不是讨论整个选项卡（也称为实体）。 传统的频道或可配置的选项卡允许用户就选项卡进行对话，但用户可能需要更集中的对话。 如果太多内容无法集中讨论或内容随着时间的推移而发生更改，则可能出现更集中的对话的要求，使对话与显示的内容无关。 对话子实体为动态选项卡提供了更加集中的对话体验。

对话子实体仅在频道中受支持。 但是，它们可用于从个人选项卡或静态选项卡创建或继续已固定到频道的选项卡中的对话。 如果你想要为用户提供一个位置来查看和访问跨多个渠道发生的对话，静态选项卡将非常有用。

## <a name="prerequisites"></a>先决条件

为了支持对话子实体，您的选项卡 Web 应用程序必须能够在后端数据库中存储子实体与↔之间的映射。 我们将为您提供 ，但您有责任存储此内容，Teams以便用户 `conversationId` `conversationId` 继续对话。

## <a name="start-a-new-conversation"></a>启动新对话

若要启动新对话，请使用 `openConversation()` 函数。 启动和继续对话都由此方法处理，但是，对函数的输入将根据您要执行的操作而更改。 从用户的角度来看，这将在屏幕右侧打开对话面板，以启动对话或继续对话。

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation** 采用以下输入在频道中启动对话：

* **subEntityId**：这是特定子实体的 ID。 例如，task-123。
* **entityId**：这是选项卡实例创建时 ID。 ID 必须引用回同一个选项卡实例。
* **channelId：** 这是选项卡实例所在的通道。
   > [!NOTE]
   > **channelId** 对于频道选项卡是可选的。 但是，如果你想要保持通道和静态选项卡的实现相同，则建议这样做。
* **title**：这是在聊天面板中向用户显示的标题。

大部分这些值也可从 `getContext` API 中检索。

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

这将打开对话面板。

![Conversationl 子实体 - 开始对话](~/assets/images/tabs/conversational-subentities/start-conversation.png)

如果用户启动对话，则侦听该事件的回调以检索和保存 **conversationId 很重要**：

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

`conversationReponse`对象包含与刚刚开始的对话有关的信息。 我们建议您保存此响应对象的所有属性，以便稍后重复使用。

## <a name="continue-a-conversation"></a>继续对话

开始对话后，后续调用要求你提供与启动新频道选项卡对话中相同的输入，但 `openConversation()` 还包括 **conversationId** [](#Starting a new channel tab conversation)。 将在视图中为具有相应对话的用户打开对话面板。 用户能够实时查看新邮件或传入邮件。

![Conversationl 子实体 - 继续对话](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a>增强对话

最后，你的选项卡使用到子实体的深层链接 [，这一点很重要](~/concepts/build-and-test/deep-links.md)。 例如，用户单击频道对话中的选项卡链接深度链接。 预期行为是接收深度链接，打开该子实体，然后打开该特定子实体的对话面板。

若要从个人选项卡或静态选项卡支持对话子实体，则不需要更改有关实现的任何内容。 我们仅支持从已固定的频道选项卡开始或继续对话。 通过支持静态选项卡，您可以为用户提供一个位置来与您的所有子实体进行交互。 但是，在最初在频道中创建选项卡时，保存 、和 非常重要，这样，在静态选项卡中打开对话视图时，您才能拥有 `subEntityId` `entityId` `channelId` 正确的属性。

## <a name="close-a-conversation"></a>关闭对话

可以通过调用 函数手动关闭对话 `closeConversation()` 视图。

```javascript
microsoftTeams.conversations.closeConversation();
```

还可以在对话视图被用户关闭时侦听事件。

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```
