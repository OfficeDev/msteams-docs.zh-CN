---
title: 创建对话选项卡
author: surbhigupta
description: 为频道选项卡创建对话子企业聊天
keywords: Teams 选项卡频道可配置
ms.topic: conceptual
ms.author: lomeybur
ms.localizationpriority: none
ms.openlocfilehash: 7426ca8d994a9009b05e5a3eece05d4938f07f80
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720370"
---
# <a name="create-conversational-tabs"></a>创建对话选项卡

对话子项提供了一种允许用户在选项卡中就子用户的对话的方法。例如特定任务、患者和销售机会，而不是讨论整个选项卡（也称为实体）。 传统的频道或可配置的选项卡允许用户就选项卡进行对话，但用户需要更集中的对话。 如果内容太多，无法进行集中讨论，或者内容随着时间的推移而发生更改，使对话与显示的内容无关，则可能出现更集中的对话的要求。 对话子项为动态选项卡提供了更加集中的对话体验。

对话子项仅在频道中受支持。 它们可用于从个人选项卡或静态选项卡创建或继续已固定到频道的选项卡中的对话。 如果要为用户提供一个位置来查看和访问跨多个渠道发生的对话，静态选项卡非常有用。

## <a name="prerequisites"></a>先决条件

若要支持对话子项，您的选项卡 Web 应用程序必须能够在后端数据库中存储子↔会话之间的映射。 `conversationId`提供了 ，但您必须存储此内容，Teams `conversationId` 以便用户继续对话。

## <a name="start-a-new-conversation"></a>启动新对话

若要启动新对话，请使用 `openConversation()` 函数。 启动和继续对话都由此方法处理。 从用户的角度来看，根据要执行哪些操作，函数输入会发生变化，这将在屏幕右侧打开对话面板，以启动对话或继续对话。

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation** 采用以下输入在频道中启动对话：

* **subEntityId**：特定子项的 ID。 例如，task-123。
* **entityId**：选项卡实例创建时其 ID。 ID 必须引用回同一个选项卡实例。
* **channelId：** 选项卡实例所在的通道。
   > [!NOTE]
   > **channelId** 对于频道选项卡是可选的。 但是，如果你想要保持通道和静态选项卡的实现相同，则建议这样做。
* **title**：在聊天面板中向用户显示的标题。

大部分这些值也可从 `getContext` API 中检索。

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

下图显示了对话面板：

![对话子实体 - 开始对话](~/assets/images/tabs/conversational-subentities/start-conversation.png)

如果用户启动对话，则侦听该事件的回调以检索和保存 **conversationId 很重要**：

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

`conversationResponse`对象包含与已启动的对话有关的信息。 建议您保存此响应对象的所有属性，供以后使用。

## <a name="continue-a-conversation"></a>继续对话

开始对话后，后续调用要求，同时提供与开始新对话中相同的输入，但 `openConversation()` 还包括 [](#start-a-new-conversation) **conversationId**。 将在视图中为具有相应对话的用户打开对话面板。 用户可以实时查看新邮件或传入邮件。

下图显示了包含相应对话的对话面板：

![对话子实体 - 继续对话](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a>增强对话

你的选项卡包含指向你的 [次项的深层链接，这一点很重要](~/concepts/build-and-test/deep-links.md)。 例如，用户从频道对话中选择 Tab 键深度链接。 预期行为是接收深层链接，打开该子级，然后打开该子级的对话面板。

若要支持"个人"或"静态"选项卡中的对话子项，则不必在实现中更改任何内容。 我们仅支持从已固定的频道选项卡开始或继续对话。 通过支持静态选项卡，您可以为用户提供一个位置来与您的所有子项进行交互。 在静态选项卡中打开对话视图时，保存 、 和 选项卡最初在频道中创建时，必须拥有 `subEntityId` `entityId` `channelId` 正确的属性。

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

## <a name="code-sample"></a>代码示例

| 示例名称 | 说明 | C# |Node.js|
|-------------|-------------|------|----|
|创建"对话"选项卡| Microsoft Teams创建对话选项卡的选项卡示例应用。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/nodejs) |

## <a name="see-also"></a>另请参阅

* [Teams选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)
* [具有自适应卡片的生成选项卡](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="next-step"></a>下一步

> [!div class="nextstepaction"]
> [选项卡边距更改](~/resources/removing-tab-margins.md)
