---
title: 在自动程序中添加卡片操作
description: 介绍 Microsoft Teams 中的卡片操作以及如何在机器人中使用它们
ms.topic: conceptual
keywords: teams 机器人卡片操作
ms.openlocfilehash: f02e195f619fdfa2ebbc4b2ef00669a1cb5b38f6
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696022"
---
# <a name="card-actions"></a>卡片操作

Teams 中的机器人和消息传递扩展使用的卡片支持以下 () [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) 类型。 请注意，在使用连接器时， `potentialActions` 这些操作不同于 Office 365 连接器卡。

| 类型 | Action |
| --- | --- |
| `openUrl` | 在默认浏览器中打开 URL。 |
| `messageBack` | 从单击按钮或点击卡片 (用户向聊天机器人发送消息和负载) 并将单独的消息发送到聊天流。 |
| `imBack`| 从单击该按钮 (点击卡片的用户向自动程序发送) 。 此消息 (对话参与者) 自动程序"消息。 |
| `invoke` | 从单击按钮或点击卡片 (用户向自动程序发送一条消息和负载) 。 此消息不可见。 |
| `signin` | 启动 OAuth 流，允许机器人与安全服务连接。 |

> [!NOTE]
>* Teams 不支持 `CardAction` 上表中未列出的类型。
>* Teams 不支持 `potentialActions` 属性。
>* 卡片操作不同于 Bot [](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) Framework/Azure Bot Service 中的建议操作。 建议的操作在 Microsoft Teams 中不受支持：如果你希望按钮出现在 Teams 自动程序消息中，请使用卡片。
>* 如果你使用卡片操作作为邮件扩展的一部分，那么在将卡片提交到频道之前，这些操作将不起作用 (当卡片位于撰写消息框中时) 。

Teams 还 [支持自适应卡片操作](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)，这些操作仅由自适应卡片使用。 这些操作将在此参考末尾的其自己的部分中列出。

## <a name="openurl"></a>openUrl

此操作类型指定在默认浏览器中启动的 URL。 请注意，自动程序不会收到有关单击哪个按钮的任何通知。

字段 `value` 必须包含格式正确的完整 URL。

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a>messageBack

使用 `messageBack` ，可以创建具有以下属性的完全自定义操作：

| 属性 | 说明 |
| --- | --- |
| `title` | 显示为按钮标签。 |
| `displayText` | 可选。 用户执行该操作时回显到聊天流中。 此文本 *不会* 发送到自动程序。 |
| `value` | 操作执行时发送到自动程序。 你可以为操作（如唯一标识符或 JSON 对象）对上下文进行编码。 |
| `text` | 操作执行时发送到自动程序。 使用此属性可简化机器人开发：代码可以检查单个顶级属性以调度自动程序逻辑。 |

灵活性意味着代码只需使用 ，就可以选择不在历史记录中留下 `messageBack` 可见的用户消息 `displayText` 。

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

### <a name="inbound-message-example"></a>入站邮件示例

`replyToId` 包含卡片操作所来自的邮件的 ID。 如果要更新邮件，请使用它。

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

## <a name="imback"></a>imBack

此操作会触发向自动程序发送的返回消息，就像用户在普通聊天消息中键入一样。 你的用户和所有其他用户在频道中都将看到该按钮响应。

字段 `value` 应包含聊天中回显的文本字符串，因此发送回聊天机器人。 这是将在自动程序中处理的消息文本，以执行所需的逻辑。 注意：此字段是一个简单的字符串 - 不支持格式设置或隐藏字符。

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a>invoke

`invoke`操作用于调用任务[模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)。

操作 `invoke` 包含三个属性 `type` ：、 `title` 和 `value` 。 该属性 `value` 可以包含字符串、字符串化 JSON 对象或 JSON 对象。

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

当用户单击该按钮时，机器人将收到 `value` 包含其他一些信息的对象。 请注意，活动类型将 `invoke` 改为 (`message` `activity.Type == "invoke"`) 。

### <a name="example-invoke-button-definition-net"></a>示例：调用按钮定义 (.NET) 

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a>示例：传入调用消息

顶级属性包含卡片 `replyToId` 操作所来自的邮件的 ID。 如果要更新邮件，请使用它。

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

## <a name="signin"></a>signin

启动 OAuth 流，允许机器人与安全服务连接，如以下更加详细地介绍：自动 [程序中的身份验证流](~/bots/how-to/authentication/auth-flow-bot.md)。

## <a name="adaptive-cards-actions"></a>自适应卡片操作

自适应卡片支持三种操作类型：

* [Action.OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [Action.ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)

除了上述操作之外，还可以修改自适应卡片有效负载，以支持使用 对象中的 属性执行现有 `Action.Submit` Bot Framework `msteams` `data` 操作 `Action.Submit` 。 以下各节详细介绍了如何将现有 Bot Framework 操作与自适应卡片一同使用。

> [!NOTE]
> 使用 Bot Framework 操作向数据 `msteams` 添加内容不能用于自适应卡片任务模块。

### <a name="adaptive-cards-with-messageback-action"></a>具有 messageBack 操作自适应卡片

若要在 `messageBack` 自适应卡片中包括操作，请包含 对象中的以下 `msteams` 详细信息。 请注意，如果需要，可以在 对象中包括其他 `data` 隐藏属性。

| 属性 | 说明 |
| --- | --- |
| `type` | 设置为 `messageBack` |
| `displayText` | 可选。 用户执行该操作时回显到聊天流中。 此文本 *不会* 发送到自动程序。 |
| `value` | 操作执行时发送到自动程序。 你可以为操作（如唯一标识符或 JSON 对象）对上下文进行编码。 |
| `text` | 操作执行时发送到自动程序。 使用此属性可简化机器人开发：代码可以检查单个顶级属性以调度自动程序逻辑。 |

#### <a name="example"></a>示例

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

若要在 `imBack` 自适应卡片中包括操作，请包含 对象中的以下 `msteams` 详细信息。 请注意，如果需要，可以在 对象中包括其他 `data` 隐藏属性。

| 属性 | 说明 |
| --- | --- |
| `type` | 设置为 `imBack` |
| `value` | 需要在聊天中回显的字符串 |

#### <a name="example"></a>示例

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

若要在 `signin` 自适应卡片中包括操作，请包含 对象中的以下 `msteams` 详细信息。 请注意，如果需要，可以在 对象中包括其他 `data` 隐藏属性。

| 属性 | 说明 |
| --- | --- |
| `type` | 设置为 `signin` |
| `value` | 设置为要重定向到的 URL  |

#### <a name="example"></a>示例

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
 
若要在 `invoke` 自适应卡片中包括操作，请包含 对象中的以下 `msteams` 详细信息。 请注意，如果需要，可以在 对象中包括其他 `data` 隐藏属性。

| 属性 | 说明 |
| --- | --- |
| `type` | 设置为 `task/fetch` |
| `data` | 设置值  |

#### <a name="example"></a>示例

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

#### <a name="example-2-with-additional-payload-data"></a>示例 2 (附加有效负载数据) 

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
