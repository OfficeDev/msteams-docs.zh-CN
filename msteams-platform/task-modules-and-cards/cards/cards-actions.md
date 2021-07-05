---
title: 在自动程序中添加卡片操作
description: 描述自动Microsoft Teams中的卡片操作以及如何在机器人中使用它们
localization_priority: Normal
ms.topic: conceptual
keywords: teams 机器人卡片操作
ms.openlocfilehash: 4af152f6179785687d4fd7371d202c56e1aee170
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254200"
---
# <a name="card-actions"></a>卡片操作

聊天机器人和邮件扩展中使用的Teams支持以下活动 [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) 类型：

> [!NOTE]
> 操作 `CardAction` 不同于从 `potentialActions` 连接器Office 365连接器卡的操作。

| 类型 | Action |
| --- | --- |
| `openUrl` | 在默认浏览器中打开 URL。 |
| `messageBack` | 从选择按钮或点击卡片的用户向机器人发送消息和有效负载。 向聊天流发送单独的消息。 |
| `imBack`| 从选择按钮或点击该卡的用户向机器人发送消息。 所有对话参与者都可以看到从用户到机器人的消息。 |
| `invoke` | 从选择按钮或点击卡片的用户向机器人发送消息和有效负载。 此消息不可见。 |
| `signin` | 启动 OAuth 流，允许机器人与安全服务连接。 |

> [!NOTE]
>* Teams不支持 `CardAction` 上表中未列出的类型。
>* Teams不支持 `potentialActions` 属性。
>* 卡片操作不同于 Bot [](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) Framework 或 Azure Bot 服务中的建议操作。 建议的操作在活动Microsoft Teams。 如果希望按钮显示在自动程序Teams，请使用卡片。
>* 如果使用卡片操作作为邮件扩展的一部分，则这些操作在将卡片提交到频道之前不起作用。 当卡片位于撰写消息框中时，操作不起作用。

## <a name="action-type-openurl"></a>操作类型 openUrl

`openUrl` action 类型指定在默认浏览器中启动的 URL。

> [!NOTE]
> 自动程序不会收到有关已选择哪个按钮的任何通知。

使用 `openUrl` ，可以创建具有以下属性的操作：

| 属性 | 说明 |
| --- | --- |
| `title` | 显示为按钮标签。 |
| `value` | 此字段必须包含格式正确的完整 URL。 |

# <a name="json"></a>[JSON](#tab/json)

以下代码显示了 `openUrl` JSON 中的操作类型示例：

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

# <a name="c"></a>[C#](#tab/csharp)

以下代码显示了一个操作 `openUrl` 类型示例C#：

```csharp
var button = new CardAction()
{
    Type = ActionTypes.OpenUrl,
    Title = "Tabs in Teams",
    Value = "https://docs.microsoft.com/en-us/microsoftteams/platform/"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

以下代码显示了 `openUrl` JavaScript 中的操作类型示例：

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

使用 `messageBack` ，可以创建具有以下属性的完全自定义操作：

| 属性 | 说明 |
| --- | --- |
| `title` | 显示为按钮标签。 |
| `displayText` | 可选。 操作执行时由聊天流中的用户使用。 此文本不会发送到自动程序。 |
| `value` | 操作执行时发送到自动程序。 你可以为操作（如唯一标识符或 JSON 对象）对上下文进行编码。 |
| `text` | 操作执行时发送到自动程序。 使用此属性可简化机器人开发。 代码可以检查单个顶级属性以调度自动程序逻辑。 |

灵活性意味着代码无法直接使用 在历史记录中留下可见的 `messageBack` 用户消息 `displayText` 。

# <a name="json"></a>[JSON](#tab/json)

以下代码显示了 `messageBack` JSON 中的操作类型示例：

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

该属性 `value` 可以是序列化的 JSON 字符串或 JSON 对象。

# <a name="c"></a>[C#](#tab/csharp)

以下代码显示了一个操作 `messageBack` 类型示例C#：

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

以下代码显示了 `messageBack` JavaScript 中的操作类型示例：

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

### <a name="inbound-message-example"></a>入站邮件示例

`replyToId` 包含卡片操作所来自的邮件的 ID。 如果要更新邮件，请使用它。

以下代码显示了入站邮件的示例：

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

该操作会触发向自动程序发送的返回消息，就像用户在普通聊天消息中 `imBack` 键入一样。 你的用户和频道中的所有其他用户可以看到按钮响应。

使用 `imBack` ，可以创建具有以下属性的操作：

| 属性 | 说明 |
| --- | --- |
| `title` | 显示为按钮标签。 |
| `value` | 此字段必须包含聊天中使用的文本字符串，因此发送回聊天机器人。 这是在自动程序中执行所需逻辑时处理的消息文本。 |

> [!NOTE]
> 字段 `value` 是一个简单字符串。 不支持设置格式或隐藏字符。

# <a name="json"></a>[JSON](#tab/json)

以下代码显示了 `imBack` JSON 中的操作类型示例：

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

# <a name="c"></a>[C#](#tab/csharp)

以下代码显示了一个操作 `imBack` 类型示例C#：

```csharp
var button = new CardAction()
{
    Type = ActionTypes.ImBack,
    Title = "More",
    Value = "Show me more"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

以下代码显示了 `imBack` JavaScript 中的操作类型示例：

```javascript
CardFactory.actions([
{
    type: "imBack",
    title: "More",
    value: "Show me more"
}])
```

---

## <a name="action-type-invoke"></a>操作类型调用

`invoke`操作用于调用任务[模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)。

操作 `invoke` 包含三个属性： `type` 、 `title` 和 `value` 。

使用 `invoke` ，可以创建具有以下属性的操作：

| 属性 | 说明 |
| --- | --- |
| `title` | 显示为按钮标签。 |
| `value` | 此属性可以包含字符串、字符串化 JSON 对象或 JSON 对象。 |

# <a name="json"></a>[JSON](#tab/json)

以下代码显示了 `invoke` JSON 中的操作类型示例：

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

当用户选择该按钮时，机器人会收到 `value` 包含其他一些信息的对象。

> [!NOTE]
> 活动类型不是 。 `invoke` `message` `activity.Type == "invoke"`

# <a name="c"></a>[C#](#tab/csharp)

以下代码显示了一个操作 `invoke` 类型示例C#：

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

以下代码显示了一个 `invoke` 操作类型示例Node.js：

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

顶级属性包含卡片 `replyToId` 操作所来自的邮件的 ID。 如果要更新邮件，请使用它。

以下代码显示了传入调用消息的示例：

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

## <a name="action-type-signin"></a>操作类型登录

`signin` 操作类型启动 OAuth 流，该流允许机器人与安全服务连接。 有关详细信息，请参阅自动 [程序中的身份验证流](~/bots/how-to/authentication/auth-flow-bot.md)。

Teams还支持[仅](#adaptive-cards-actions)由自适应卡片使用的自适应卡片操作。

# <a name="json"></a>[JSON](#tab/json)

以下代码显示了 `signin` JSON 中的操作类型示例：

```json
{
"type": "signin",
"title": "Click me for signin",
"value": "https://signin.com"
}
```

# <a name="c"></a>[C#](#tab/csharp)

以下代码显示了一个操作 `signin` 类型示例C#：

```csharp
var button = new CardAction()
{
    Type = ActionTypes.Signin,
    Title = "Click me for signin",
    Value = "https://signin.com"
};
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

以下代码显示了 `signin` JavaScript 中的操作类型示例：

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

还可以修改自适应卡片有效负载，以支持使用 对象中的 属性执行现有 `Action.Submit` Bot Framework `msteams` `data` 操作 `Action.Submit` 。 下一部分详细介绍了如何将现有 Bot Framework 操作与自适应卡片一同使用。

> [!NOTE]
> 使用 `msteams` Bot Framework 操作向数据添加操作不能用于自适应卡片任务模块。

### <a name="adaptive-cards-with-messageback-action"></a>具有 messageBack 操作自适应卡片

若要在 `messageBack` 自适应卡片中包括操作，请包含对象中的以下 `msteams` 详细信息：

> [!NOTE]
> 如果需要，可以在对象中包括其他 `data` 隐藏属性。

| 属性 | 说明 |
| --- | --- |
| `type` | 设置为 `messageBack` 。 |
| `displayText` | 可选。 操作执行时由聊天流中的用户使用。 此文本不会发送到自动程序。 |
| `value` | 操作执行时发送到自动程序。 你可以为操作（如唯一标识符或 JSON 对象）对上下文进行编码。 |
| `text` | 操作执行时发送到自动程序。 使用此属性可简化机器人开发。 代码可以检查单个顶级属性以调度自动程序逻辑。 |

以下代码显示了操作自适应卡片 `messageBack` 的示例：

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

### <a name="adaptive-cards-with-imback-action"></a>使用 imBack 操作自适应卡片

若要在 `imBack` 自适应卡片中包括操作，请包含 对象中的以下 `msteams` 详细信息：

> [!NOTE]
> 如果需要，可以在对象中包括其他 `data` 隐藏属性。

| 属性 | 说明 |
| --- | --- |
| `type` | 设置为 `imBack` 。 |
| `value` | 需要在聊天中回显的字符串。 |

以下代码显示了操作自适应卡片 `imBack` 的示例：

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

### <a name="adaptive-cards-with-signin-action"></a>带登录操作自适应卡片

若要在 `signin` 自适应卡片中包括操作，请包含对象中的以下 `msteams` 详细信息：

> [!NOTE]
> 如果需要，可以在对象中包括其他 `data` 隐藏属性。

| 属性 | 说明 |
| --- | --- |
| `type` | 设置为 `signin` 。 |
| `value` | 设置为要重定向的 URL。  |

以下代码显示了操作自适应卡片 `signin` 的示例：

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

### <a name="adaptive-cards-with-invoke-action"></a>具有调用操作的自适应卡片

若要在 `invoke` 自适应卡片中包括操作，请包含 对象中的以下 `msteams` 详细信息：

> [!NOTE]
> 如果需要，可以在对象中包括其他 `data` 隐藏属性。

| 属性 | 说明 |
| --- | --- |
| `type` | 设置为 `task/fetch` 。 |
| `data` | 设置值。  |

以下代码显示了操作自适应卡片 `invoke` 的示例：

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

以下代码显示了具有其他有效负载数据的自适应卡片 `invoke` 示例：

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

## <a name="see-also"></a>另请参阅

[卡参考](./cards-reference.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [自适应卡的通用操作](../cards/Universal-actions-for-adaptive-cards/Overview.md)
