---
title: 仅通知 bot
description: 描述 Microsoft 团队中仅有通知的 bot
keywords: 团队 bot 通知
ms.date: 05/20/2019
ms.openlocfilehash: 37652bc2d6171191c81be4e5a2875f47c79574f9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673032"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>仅通知 Microsoft 团队中的 bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

如果你的 bot 的唯一用途是将通知传递给用户，而不是会话，则可以`isNotificationOnly`在应用程序清单中启用该字段。 这将产生以下更改：

* 用户无法将仅通知 bot 发送给您。
* 用户不能 @mention 机器人。

## <a name="app-manifest"></a>应用程序清单

若要启用此设置`isNotificationOnly` ， `true`请将设置为。

> [!NOTE]
> 请注意，的值`isNotificationOnly`是布尔值，而不是字符串。

```json
{
  ⋮
  "bots":[
    {
      "botId":"[Microsoft App ID for your bot]",
      "isNotificationOnly": true,
      "scopes": [
        "personal",
        "team"
      ],
    }
  ],
  ...
}
```

## <a name="best-practices-and-limitations"></a>最佳实践和限制

* 您不能仅`personal`创建作用域通知 bot，因为用户无法在个人聊天中发送仅通知 bot。 这意味着，您无法收到可`conversationUpdate`提供用于发送通知的必要详细信息的事件。 仅当支持该`team`作用域并将其添加到团队中时，仅通知 bot 才能正常工作。 在 "团队设置" 中，你的 bot 将有权访问将通知发送到频道或私下给用户所需的信息。
* 仅通知 bot 使用主动消息与用户通信。 有关详细信息，请参阅[用于 bot 的主动消息](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。
