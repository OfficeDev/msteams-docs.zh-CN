---
title: 在机器人中添加卡片操作
description: 介绍 Microsoft Teams 中的卡片操作以及如何在机器人中使用它们
ms.localizationpriority: medium
ms.topic: conceptual
keywords: Teams, 机器人卡片操作
ms.openlocfilehash: 305706f3dfad820584f7a95e231870d258caa8ed
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756483"
---
# <a name="card-actions"></a>卡片操作

Teams 中机器人和消息扩展使用的卡片支持以下活动 [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) 类型：

> [!NOTE]
> 从连接器使用时，`CardAction` 操作与 Office 365 连接器卡片的 `potentialActions` 不同。

| 类型 | Action |
| --- | --- |
| `openUrl` | 在默认浏览器中打开 URL。 |
| `messageBack` | 从选择按钮或点击卡片的用户向机器人发送消息和有效负载。 向聊天流发送单独的消息。 |
| `imBack`| 从选择按钮或点击卡片的用户向机器人发送消息。 从用户发送到机器人的这一消息对所有对话参与者可见。 |
| `invoke` | 从选择按钮或点击卡片的用户向机器人发送消息和有效负载。 此消息不可见。 |
| `signin` | 启动 OAuth 流，允许机器人连接安全服务。 |

> [!NOTE]
>
>* Teams 不支持上表中未列出的 `CardAction` 类型。
>* Teams 不支持 `potentialActions` 属性。
>* 卡片操作不同于 Bot Framework 或 Azure 机器人服务中[建议的操作](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true)。 Microsoft Teams 不支持建议的操作。 如果希望按钮显示在 Teams 机器人消息上，请使用卡片。
>* 如果将卡片操作用作消息扩展的一部分，则在卡片提交到频道之前，操作将不起作用。 当卡片位于“撰写消息”框中时，操作将不起作用。

## <a name="action-type-openurl"></a>操作类型 openUrl

`openUrl` 操作类型指定要在默认浏览器中启动的 URL。

> [!NOTE]
> 机器人不会收到任何关于所选按钮的通知。

通过 `openUrl`，你可以创建具有以下属性的操作：

| 属性 | 说明 |
| --- | --- |
| `title` | 显示为按钮标签。 |
| `value` | 此字段必须包含完整且格式正确的 URL。 |

# <a name="json"></a>[JSON](#tab/json)

以下代码显示 JSON 中的 `openUrl` 操作类型的示例：

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

# <a name="c"></a>[C#](#tab/csharp)

以下代码显示 C# 中的 `openUrl` 操作类型的示例：

```csharp
var button = new CardAction()
{
    Type = ActionTypes.OpenUrl,
    Title = "Tabs in Teams",
    Value = "https://docs.microsoft.com/en-us/microsoftteams/platform/"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

以下代码显示 JavaScript 中的 `openUrl` 操作类型的示例：

```javascript
CardFactory.actions([
{
    type: 'openUrl',
    title: 'Tabs in Teams',
    value: 'https://docs.microsoft.com/en-us/microsoftteams/platform/'
}])
```

---

## <a name="action-type-messageback"></a>操作类型 messageBack

通过 `messageBack`，你可以创建具有以下属性的完全自定义操作：

| 属性 | 说明 |
| --- | --- |
| `title` | 显示为按钮标签。 |
| `displayText` | 可选。 执行操作时由用户在聊天流中使用。 此文本不会发送到机器人。 |
| `value` | 执行操作时发送到机器人。 可以对操作的上下文进行编码，例如唯一标识符或 JSON 对象。 |
| `text` | 执行操作时发送到机器人。 使用此属性可简化机器人开发。 代码可以检查单个顶级属性以调度机器人逻辑。 |

代码无法通过不使用`displayText`而在历史记录中保留可见用户消息的灵活性`messageBack`。

# <a name="json"></a>[JSON](#tab/json)

以下代码显示 JSON 中的 `messageBack` 操作类型的示例：

```json
{
  "buttons": [
    {
    "type": "messageBack",
    "title": "My MessageBack button",
    "displayText": "I clicked this button",
    "text": "User just clicked the MessageBack button",
    "value": "{\"property\": \"propertyValue\" }"
    }
  ]
}
```

`value` 属性可以是序列化的 JSON 字符串或 JSON 对象。

# <a name="c"></a>[C#](#tab/csharp)

以下代码显示 C# 中的 `messageBack` 操作类型的示例：

```csharp
var button = new CardAction()
{
    Type = ActionTypes.MessageBack,
    Title = "My MessageBack button",
    DisplayText = "I clicked this button",
    Text = "User just clicked the MessageBack button",
    Value = "{\"property\": \"propertyValue\" }"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

以下代码显示 JavaScript 中的 `messageBack` 操作类型的示例：

```javascript
CardFactory.actions([
{
    type: 'messageBack',
    title: "My MessageBack button",
    displayText: "I clicked this button",
    text: "User just clicked the MessageBack button",
    value: {property: "propertyValue" }
}])
```

---

### <a name="inbound-message-example"></a>入站消息示例

`replyToId` 包含卡片操作来自的消息的 ID。 如果要更新消息，请使用它。

以下代码显示入站消息的示例：

```json
{
   "text":"User just clicked the MessageBack button",
   "value":{
      "property":"propertyValue"
   },
   "type":"message",
   "timestamp":"2017-06-22T22:38:47.407Z",
   "id":"f:5261769396935243054",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:102jd210jd010icsoaeclaejcoa9ue09u",
      "name":"John Smith"
   },
   "conversation":{
      "id":"19:malejcou081i20ojmlcau0@thread.skype;messageid=1498171086622"
   },
   "recipient":{
      "id":"28:76096e45-119f-4736-859c-6dfff54395f7",
      "name":"MyBot"
   },
   "entities":[
      {
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo" 
      }
   ],
   "channelData":{
      "channel":{
         "id":"19:malejcou081i20ojmlcau0@thread.skype"
      },
      "team":{
         "id":"19:12d021jdoijsaeoaue0u@thread.skype"
      },
      "tenant":{
         "id":"bec8e231-67ad-484e-87f4-3e5438390a77"
      }
   },
        "replyToId": "1575667808184",
}
```

## <a name="action-type-imback"></a>操作类型 imBack

`imBack` 操作会触发向机器人返回消息，就像用户在正常聊天消息中键入一样。 频道中的用户和所有其他用户都可以看到按钮响应。

通过 `imBack`，你可以创建具有以下属性的操作：

| 属性 | 说明 |
| --- | --- |
| `title` | 显示为按钮标签。 |
| `value` | 此字段必须包含聊天中使用的文本字符串，因此会发送回机器人。 这是在机器人中处理以执行所需逻辑的消息文本。 |

> [!NOTE]
> `value` 字段是一个简单的字符串。 不支持格式化或隐藏字符。

# <a name="json"></a>[JSON](#tab/json)

以下代码显示 JSON 中的 `imBack` 操作类型的示例：

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

# <a name="c"></a>[C#](#tab/csharp)

以下代码显示 C# 中的 `imBack` 操作类型的示例：

```csharp
var button = new CardAction()
{
    Type = ActionTypes.ImBack,
    Title = "More",
    Value = "Show me more"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

以下代码显示 JavaScript 中的 `imBack` 操作类型的示例：

```javascript
CardFactory.actions([
{
    type: "imBack",
    title: "More",
    value: "Show me more"
}])
```

---

## <a name="action-type-invoke"></a>操作类型 invoke

`invoke` 操作用于调用[任务模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)。

`invoke` 操作包含三个属性，即 `type`、`title` 和 `value`。

通过 `invoke`，你可以创建具有以下属性的操作：

| 属性 | 说明 |
| --- | --- |
| `title` | 显示为按钮标签。 |
| `value` | 此属性可以包含字符串、字符串化 JSON 对象或 JSON 对象。 |

# <a name="json"></a>[JSON](#tab/json)

以下代码显示 JSON 中的 `invoke` 操作类型的示例：

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

当用户选择该按钮时，机器人会收到包含一些其他信息的 `value` 对象。

> [!NOTE]
> 活动类型是 `invoke`，而不是 `activity.Type == "invoke"` 的 `message`。

# <a name="c"></a>[C#](#tab/csharp)

以下代码显示 C# 中的 `invoke` 操作类型的示例：

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

以下代码显示 Node.js 中的 `invoke` 操作类型的示例：

```javascript
CardFactory.actions([
{
    type: "invoke",
    title: "Option 1",
    value: {
        option: "opt1"
    }
}])
```

---

### <a name="example-of-incoming-invoke-message"></a>传入调用消息的示例

顶级 `replyToId` 属性包含卡片操作来自的消息的 ID。 如果要更新消息，请使用它。

以下代码显示传入调用消息的示例：

```json
{
    "type": "invoke",
    "value": {
        "option": "opt1"
    },
    "timestamp": "2017-02-10T04:11:19.614Z",
    "localTimestamp": "2017-02-09T21:11:19.614-07:00",
    "id": "f:6894910862892785420",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1Eniglq0-uVL83xNB9GU6w_G5a4SZF0gcJLprZzhtEbel21G_5h-
    NgoprRw45mP0AXUIZVeqrsIHSYV4ntgfVJQ",
        "name": "John Doe"
    },
    "conversation": {
        "id": "19:97b1ec61-45bf-453c-9059-6e8984e0cef4_8d88f59b-ae61-4300-bec0-caace7d28446@unq.gbl.spaces"
    },
    "recipient": {
        "id": "28:8d88f59b-ae61-4300-bec0-caace7d28446",
        "name": "MyBot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Web",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "channel": {
            "id": "19:dc5ba12695be4eb7bf457cad6b4709eb@thread.skype"
        },
        "team": {
            "id": "19:712c61d0ef384e5fa681ba90ca943398@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```

## <a name="action-type-signin"></a>操作类型 signin

`signin` 操作类型启动允许机器人与安全服务连接的 OAuth 流。 有关详细信息，请参阅[机器人中的身份验证流](~/bots/how-to/authentication/auth-flow-bot.md)。

Teams 还支持仅由自适应卡片使用的[自适应卡片操作](#adaptive-cards-actions)。

# <a name="json"></a>[JSON](#tab/json)

以下代码显示 JSON 中的 `signin` 操作类型的示例：

```json
{
"type": "signin",
"title": "Click me for signin",
"value": "https://signin.com"
}
```

# <a name="c"></a>[C#](#tab/csharp)

以下代码显示 C# 中的 `signin` 操作类型的示例：

```csharp
var button = new CardAction()
{
    Type = ActionTypes.Signin,
    Title = "Click me for signin",
    Value = "https://signin.com"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

以下代码显示 JavaScript 中的 `signin` 操作类型的示例：

```javascript
CardFactory.actions([
{
    type: "signin",
    title: "Click me for signin",
    value: "https://signin.com"
}])
```

---

## <a name="adaptive-cards-actions"></a>自适应卡片操作

自适应卡片支持四种操作类型：

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action.ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [Action.Execute](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

你还可以修改自适应卡片 `Action.Submit` 有效负载，以支持在 `Action.Submit` 的 `data` 对象中使用 `msteams` 属性的现有 Bot Framework 操作。 下一部分提供有关如何将现有 Bot Framework 操作与自适应卡片配合使用的详细信息。

> [!NOTE]
> 使用 Bot Framework 操作将 `msteams` 添加到数据不适用于自适应卡片任务模块。

### <a name="adaptive-cards-with-messageback-action"></a>包含 messageBack 操作的自适应卡片

若要在自适应卡片中包含 `messageBack` 操作，请在 `msteams` 对象中包含以下详细信息：

> [!NOTE]
> 如果需要，可以在 `data` 对象中包含其他隐藏属性。

| 属性 | 说明 |
| --- | --- |
| `type` | 设置为 `messageBack`。 |
| `displayText` | 可选。 执行操作时由用户在聊天流中使用。 此文本不会发送到机器人。 |
| `value` | 执行操作时发送到机器人。 可以对操作的上下文进行编码，例如唯一标识符或 JSON 对象。 |
| `text` | 执行操作时发送到机器人。 使用此属性可简化机器人开发。 代码可以检查单个顶级属性以调度机器人逻辑。 |

以下代码显示包含 `messageBack` 操作的自适应卡片的示例：

```json
{
  "type": "Action.Submit",
  "title": "Click me for messageBack",
  "data": {
    "msteams": {
        "type": "messageBack",
        "displayText": "I clicked this button",
        "text": "text to bots",
        "value": "{\"bfKey\": \"bfVal\", \"conflictKey\": \"from value\"}"
    }
  }
}
```

### <a name="adaptive-cards-with-imback-action"></a>包含 imBack 操作的自适应卡片

若要在自适应卡片中包含 `imBack` 操作，请在 `msteams` 对象中包含以下详细信息：

> [!NOTE]
> 如果需要，可以在 `data` 对象中包含其他隐藏属性。

| 属性 | 说明 |
| --- | --- |
| `type` | 设置为 `imBack`。 |
| `value` | 需要在聊天中回显的字符串。 |

以下代码显示包含 `imBack` 操作的自适应卡片的示例：

```json
{
  "type": "Action.Submit",
  "title": "Click me for imBack",
  "data": {
    "msteams": {
        "type": "imBack",
        "value": "Text to reply in chat"
    }
  }
}
```

### <a name="adaptive-cards-with-signin-action"></a>包含 signin 操作的自适应卡片

若要在自适应卡片中包含 `signin` 操作，请在 `msteams` 对象中包含以下详细信息：

> [!NOTE]
> 如果需要，可以在 `data` 对象中包含其他隐藏属性。

| 属性 | 说明 |
| --- | --- |
| `type` | 设置为 `signin`。 |
| `value` | 设置为要重定向到的 URL。  |

以下代码显示包含 `signin` 操作的自适应卡片的示例：

```json
{
  "type": "Action.Submit",
  "title": "Click me for signin",
  "data": {
    "msteams": {
        "type": "signin",
        "value": "https://signin.com"
    }
  }
}
```

### <a name="adaptive-cards-with-invoke-action"></a>包含 invoke 操作的自适应卡片

若要在自适应卡片中包含 `invoke` 操作，请在 `msteams` 对象中包含以下详细信息：

> [!NOTE]
> 如果需要，可以在 `data` 对象中包含其他隐藏属性。

| 属性 | 说明 |
| --- | --- |
| `type` | 设置为 `task/fetch`。 |
| `data` | 设置值。  |

以下代码显示包含 `invoke` 操作的自适应卡片的示例：

```json
{
  "type": "Action.Submit",
  "title": "submit",
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

以下代码显示包含 `invoke` 操作和其他有效负载数据的自适应卡片的示例：

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    },
    "Value1": "some value"
  }
}
```

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [自适应卡的通用操作](../cards/Universal-actions-for-adaptive-cards/Overview.md)

## <a name="see-also"></a>另请参阅

* [卡参考](./cards-reference.md)
* [使用机器人的任务模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* [机器人中的自适应卡片](../../bots/how-to/conversations/conversation-messages.md#adaptive-cards)
* [自适应卡的通用操作](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md)
* [表单完成反馈](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
