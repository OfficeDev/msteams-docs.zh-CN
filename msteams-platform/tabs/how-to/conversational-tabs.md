---
title: 创建对话选项卡
author: surbhigupta
description: 了解如何在 Microsoft Teams 中创建对话选项卡以开始、继续、增强和关闭对话。
ms.topic: conceptual
ms.author: lomeybur
ms.localizationpriority: high
ms.openlocfilehash: fa54221a413b19704d80ec62feb1cf068e42d1a0
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820120"
---
# <a name="create-conversational-tabs"></a>创建对话选项卡

对话子实体提供了一种允许用户在选项卡中就子实体进行对话的方法。例如特定任务、患者和销售机会，而不是讨论整个选项卡（也称为实体）。 传统频道或可配置选项卡允许用户就选项卡进行对话，但用户需要更专注的对话。 如果内容太多而无法集中讨论，或者内容随时间而更改，则可能会产生更集中的对话的要求，从而使对话与显示的内容无关。 对话子实体为动态选项卡提供了更集中的聊天体验。

对话子实体仅在通道中受支持。 可以从个人或静态选项卡使用它们，在已固定到频道的选项卡中创建或继续对话。 如果要为用户提供一个位置，以便查看和访问跨多个通道发生的对话，则静态选项卡非常有用。

## <a name="prerequisites"></a>先决条件

若要支持对话子实体，选项卡 Web 应用程序必须能够在后端数据库中存储子实体↔会话之间的映射。 `conversationId`提供了 ，但你必须存储它`conversationId`并将其返回到 Teams，以便用户继续对话。

## <a name="start-a-new-conversation"></a>开始新对话

若要开始新的对话，请使用 `openConversation()` 函数。 开始和继续对话均由此方法处理。 从用户的角度来看，函数的输入会根据要采取的操作而更改，这会打开屏幕右侧的对话面板，以启动对话或继续对话。

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation** 采用以下输入在频道中启动对话：

* **subEntityId**：特定子实体的 ID。 例如，task-123。
* **entityId**：创建选项卡实例时的 ID。 ID 对于回引用同一选项卡实例非常重要。
* **channelId**：选项卡实例所在的通道。
   > [!NOTE]
   > **channelId 对于通道** 选项卡是可选的。 但是，如果要使跨通道和静态选项卡的实现保持一致，则建议这样做。
* **title**：在聊天面板中向用户显示的游戏。

还可以从 [`app.getContext()`](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-getcontext&preserve-view=true) TeamsJS v1) `microsoftTeams.getContext()` 中的 API (检索其中大多数值。 有关详细信息，请参阅 [PageInfo 接口](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-pageinfo&preserve-view=true)

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

下图显示了对话面板：

:::image type="content" source="../../assets/images/tabs/conversational-subentities/start-conversation.png" alt-text="开始对话":::

如果用户启动会话，请务必侦听该事件的回调以检索和保存 **conversationId**：

```javascript
⁠microsoftTeams.conversations.openConversation({
    ...,
    onStartConversation: (conversationResponse) => {
        ⁠// console.log(conversationResponse)
    },
});
```

对象 `conversationResponse` 包含与已启动的会话相关的信息。 建议保存此响应对象的所有属性以供以后使用。

## <a name="continue-a-conversation"></a>继续对话

会话开始后，后续调用 `openConversation()` 要求提供与 [开始新对话](#start-a-new-conversation)相同的输入，但还包括 **conversationId**。 此时会为视图中具有相应对话的用户打开对话面板。 用户可以实时查看新消息或传入消息。

下图显示了具有相应对话的会话面板：

:::image type="content" source="../../assets/images/tabs/conversational-subentities/continue-conversation.png" alt-text="继续对话":::

## <a name="enhance-a-conversation"></a>增强对话

选项卡必须包含 [指向子实体的深层链接](~/concepts/build-and-test/deep-links.md)，这一点很重要。 例如，用户从频道对话中选择选项卡 chiclet 深层链接。 预期行为是接收深层链接，打开该子实体，然后打开该子实体的对话面板。

若要支持个人或静态选项卡中的对话子实体，无需在实现中更改任何内容。 我们仅支持从已固定的频道选项卡开始或继续对话。 通过支持静态选项卡，你可以为用户提供一个位置，以便与所有子实体交互。 在频道中最初创建选项卡时，请务必保存 `subEntityId`、 `entityId`和 `channelId` ，以在静态选项卡中打开对话视图时具有正确的属性。

## <a name="close-a-conversation"></a>关闭对话

可以通过调用 `closeConversation()` 函数手动关闭对话视图。

```javascript
microsoftTeams.conversations.closeConversation();
```

当用户在对话视图中选择 **“关闭 (X)** ”时，还可以侦听事件。

```javascript
⁠microsoftTeams.conversations.openConversation({
    ...,
    onCloseConversation: (conversationResponse) => {
        ⁠// console.log(conversationResponse)
    },
});
```

## <a name="code-sample"></a>代码示例

| 示例名称 | Description | C# |Node.js|
|-------------|-------------|------|----|
|“创建对话”选项卡| 用于演示“创建对话”选项卡的 Microsoft Teams 选项卡示例应用。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/nodejs) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [选项卡边距更改](~/resources/removing-tab-margins.md)

## <a name="see-also"></a>另请参阅

* [Teams 的生成选项卡](../what-are-tabs.md)
* [创建个人选项卡](create-personal-tab.md)
* [创建频道选项卡或组选项卡](create-channel-group-tab.md)
* [具有自适应卡片的生成选项卡](build-adaptive-card-tabs.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)
