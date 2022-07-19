---
title: 创建对话选项卡
author: surbhigupta
description: 在本模块中，了解如何为频道选项卡创建聊天子实体聊天，以使用代码示例管理对话
ms.topic: conceptual
ms.author: lomeybur
ms.localizationpriority: medium
ms.openlocfilehash: f039c8cb03aa874993f64d32030eb226c59a707d
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2022
ms.locfileid: "66841980"
---
# <a name="create-conversational-tabs"></a>创建对话选项卡

对话子实体提供了一种方法，允许用户在选项卡中进行有关子实体的对话。例如特定的任务、患者和销售机会，而不是讨论整个选项卡（也称为实体）。 传统的频道或可配置选项卡允许用户进行有关选项卡的对话，但用户需要更集中的对话。 如果内容过多而无法进行集中讨论，或者由于内容随时间推移而更改，使对话与所显示的内容无关，则可能会产生对更集中对话的要求。 会话子实体为动态选项卡提供更集中的会话体验。

对话子实体仅在通道中受支持。 可以从个人或静态选项卡使用它们在已固定到频道的选项卡中创建或继续对话。 如果要为用户提供一个位置来查看和访问跨多个通道发生的对话，静态选项卡非常有用。

## <a name="prerequisites"></a>先决条件

若要支持会话子实体，Tab Web 应用程序必须能够在后端数据库中的子实体↔对话之间存储映射。 提供 `conversationId` 此功能，但必须将其存储 `conversationId` 并返回到 Teams，以便用户继续对话。

## <a name="start-a-new-conversation"></a>开始新对话

若要启动新对话，请使用该 `openConversation()` 函数。 启动和继续会话均由此方法处理。 对函数的输入根据要执行的操作而更改，从用户的角度来看，这会打开屏幕右侧的对话面板，以启动对话或继续聊天。

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**openConversation** 采用以下输入在频道中启动对话：

* **subEntityId**：特定子实体的 ID。 例如，task-123。
* **entityId**：创建选项卡实例时的 ID。 返回到同一个选项卡实例时，ID 非常重要。
* **channelId**：选项卡实例所在的通道。
   > [!NOTE]
   > **channelId** 是频道选项卡的可选选项。 但是，如果要在通道和静态选项卡之间保持相同的实现，则建议执行此操作。
* **title**：在聊天面板中向用户显示的标题。

还可以从 [`app.getContext()`](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-getcontext&preserve-view=true) TeamsJS v1) 中的 API (`microsoftTeams.getContext()` 检索其中的大部分值。 有关详细信息，请参阅 [PageInfo 接口](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-pageinfo&preserve-view=true)

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

下图显示了对话面板：

:::image type="content" source="../../assets/images/tabs/conversational-subentities/start-conversation.png" alt-text="开始对话":::

如果用户启动对话，请务必侦听该事件的回调以检索并保存 **conversationId**：

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

该 `conversationResponse` 对象包含与已启动的对话相关的信息。 建议保存此响应对象的所有属性供以后使用。

## <a name="continue-a-conversation"></a>继续对话

会话启动后，需要后续调用 `openConversation()` ，同时提供与 [开始新会话](#start-a-new-conversation)时相同的输入，但也包括 **conversationId**。 会话面板将打开，供查看相应对话的用户使用。 用户可以实时查看新消息或传入消息。

下图显示了具有相应对话的对话面板：

:::image type="content" source="../../assets/images/tabs/conversational-subentities/continue-conversation.png" alt-text="继续对话":::

## <a name="enhance-a-conversation"></a>增强对话

选项卡包含 [到子实体的深层链接](~/concepts/build-and-test/deep-links.md)非常重要。 例如，用户从频道对话中选择选项卡小鸡的深层链接。 预期行为是接收深层链接，打开该子实体，然后打开该子实体的对话面板。

若要从个人或静态选项卡支持对话子实体，无需更改实现中的任何内容。 我们仅支持从已固定的频道选项卡开始或继续对话。 支持静态选项卡可为用户提供单个位置，以便与所有子实体进行交互。 在静态选项卡中打开对话视图时，`entityId``channelId`务必保存`subEntityId`选项卡，并在最初在通道中创建选项卡时具有正确的属性。

## <a name="close-a-conversation"></a>关闭对话

可以通过调用 `closeConversation()` 函数手动关闭对话视图。

```javascript
microsoftTeams.conversations.closeConversation();
```

当用户关闭对话视图时，还可以侦听事件。

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```

## <a name="code-sample"></a>代码示例

| 示例名称 | Description | C# |Node.js|
|-------------|-------------|------|----|
|“创建对话”选项卡| 用于演示“创建对话”选项卡的 Microsoft Teams 选项卡示例应用。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/nodejs) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [选项卡边距更改](~/resources/removing-tab-margins.md)

## <a name="see-also"></a>另请参阅

* [Teams 选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [移动设备上的选项卡](~/tabs/design/tabs-mobile.md)
* [具有自适应卡片的生成选项卡](~/tabs/how-to/build-adaptive-card-tabs.md)
