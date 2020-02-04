---
title: 在 bot 中添加卡片操作
description: 介绍 Microsoft 团队中的卡片操作以及如何在你的 bot 中使用它们
keywords: 团队 bot 卡片操作
ms.openlocfilehash: e0b050cde9adf5bd811d5d95ce1c6f1bf60546a1
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673201"
---
# <a name="card-actions"></a>卡片操作

由团队中的 bot 和邮件分机使用的卡片支持以下活动[`CardAction`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)（）类型。 请注意，从连接器使用`potentialActions`时，这些操作与 Office 365 连接器卡有所不同。

| 类型 | Action |
| --- | --- |
| `openUrl` | 在默认浏览器中打开 URL。 |
| `messageBack` | 将邮件和有效负载发送到 bot （从单击按钮或点击卡片的用户），并将单独的邮件发送到聊天流。 |
| `imBack`| 将邮件发送到自动程序（从单击按钮的用户或通过点击卡片）。 此邮件（从用户到 bot）对所有对话参与者均可见。 |
| `invoke` | 将邮件和有效负载发送到机器人（从单击按钮的用户或通过点击卡片）。 此消息不可见。 |
| `signin` | 启动 OAuth 流，允许 bot 与安全服务连接。 |

> [!NOTE]
>* 团队不支持`CardAction`上表中未列出的类型。
>* 团队不支持该`potentialActions`属性。
>* 卡片操作与 Bot 框架/Azure Bot 服务中的[建议操作](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button)不同。 Microsoft 团队不支持建议的操作：如果希望按钮显示在 "团队" bot 邮件中，请使用卡片。
>* 如果使用的是作为邮件扩展一部分的卡片操作，则在将该卡片提交到频道之前，操作将不起作用（当卡片在撰写消息框中时，这些操作将不起作用）。

团队还支持[自适应卡片操作](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)，仅供自适应卡片使用。 这些操作在本参考结束时在各自的部分中列出。

## <a name="openurl"></a>openUrl

此操作类型指定要在默认浏览器中启动的 URL。 请注意，你的 bot 不会收到单击了哪个按钮的任何通知。

`value`字段必须包含完整且格式正确的 URL。

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a>messageBack

使用`messageBack`，您可以创建具有以下属性的完全自定义操作：

| 属性 | 说明 |
| --- | --- |
| `title` | 显示为按钮标签。 |
| `displayText` | 可选。 在执行操作时，用户在聊天流中回显。 此文本*不*会发送到你的机器人。 |
| `value` | 在执行操作时发送到你的 bot。 您可以对操作的上下文进行编码，例如唯一标识符或 JSON 对象。 |
| `text` | 在执行操作时发送到你的 bot。 使用此属性可简化 bot 的开发：您的代码可以检查单个顶级属性以调度 bot 逻辑。 |

这`messageBack`意味着您的代码可以选择不使用`displayText`，而只是在历史记录中留下可见的用户消息。

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

该`value`属性可以是序列化的 json 字符串，也可以是 json 对象。

### <a name="inbound-message-example"></a>入站邮件示例

`replyToId`包含卡操作来自的邮件的 ID。 如果要更新邮件，请使用此方法。

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

此操作会触发到你的 bot 的返回邮件，就像用户在正常聊天消息中键入它一样。 如果你的用户和所有其他用户在频道中，将会看到按钮响应。

该`value`字段应包含聊天中的文本字符串回显，从而发回机器人。 这是将在你的 bot 中处理的邮件文本，以执行所需的逻辑。 注意：此字段是一个简单的字符串，不支持格式化或隐藏字符。

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a>调

该`invoke`操作用于调用[任务模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)。

`invoke`操作包含三个属性： `type`、 `title`和`value`。 `value`属性可以包含字符串、字符串化 JSON 对象或 json 对象。

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

当用户单击此按钮时，你的 bot 将接收`value`具有一些其他信息的对象。 请注意，活动类型将为`invoke`而不是`message` （`activity.Type == "invoke"`）。

### <a name="example-invoke-button-definition-net"></a>示例： Invoke button definition （.NET）

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a>示例：传入的 invoke 消息

顶级`replyToId`属性包含卡片操作来自的邮件的 ID。 如果要更新邮件，请使用此方法。

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

## <a name="signin"></a>登录

启动 OAuth 流，使 bot 能够与安全服务连接，如下文更详细地介绍： [bot 中的身份验证流](~/bots/how-to/authentication/auth-flow-bot.md)。

## <a name="adaptive-cards-actions"></a>自适应卡片操作

自适应卡片支持三种操作类型：

* [操作。 OpenUrl](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [Action.Submit](http://adaptivecards.io/explorer/Action.Submit.html)
* [操作。 ShowCard](http://adaptivecards.io/explorer/Action.ShowCard.html)

除了上面提到的操作之外， `Action.Submit`还可以使用`msteams` `data`对象中的属性修改自适应卡有效负载，以支持现有机器人框架操作。 `Action.Submit` 以下各节详细介绍了如何将现有的 Bot 框架操作用于自适应卡片。

### <a name="adaptive-cards-with-messageback-action"></a>具有 messageBack 操作的自适应卡片

若要包含`messageBack`自适应卡片的操作，请在`msteams`对象中包含以下详细信息。 请注意，如果需要，可以在`data`对象中包含其他隐藏属性。

| 属性 | 说明 |
| --- | --- |
| `type` | 设置为`messageBack` |
| `displayText` | 可选。 在执行操作时，用户在聊天流中回显。 此文本*不*会发送到你的机器人。 |
| `value` | 在执行操作时发送到你的 bot。 您可以对操作的上下文进行编码，例如唯一标识符或 JSON 对象。 |
| `text` | 在执行操作时发送到你的 bot。 使用此属性可简化 bot 的开发：您的代码可以检查单个顶级属性以调度 bot 逻辑。 |

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

### <a name="adaptive-cards-with-imback-action"></a>具有 imBack 操作的自适应卡片

若要包含`imBack`自适应卡片的操作，请在`msteams`对象中包含以下详细信息。 请注意，如果需要，可以在`data`对象中包含其他隐藏属性。

| 属性 | 说明 |
| --- | --- |
| `type` | 设置为`imBack` |
| `value` | 需要在聊天中回送的字符串 |

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

### <a name="adaptive-cards-with-signin-action"></a>具有登录操作的自适应卡片

若要包含`signin`自适应卡片的操作，请在`msteams`对象中包含以下详细信息。 请注意，如果需要，可以在`data`对象中包含其他隐藏属性。

| 属性 | 说明 |
| --- | --- |
| `type` | 设置为`signin` |
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
