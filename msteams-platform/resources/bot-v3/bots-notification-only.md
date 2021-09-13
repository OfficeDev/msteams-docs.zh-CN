---
title: 仅限通知的机器人
description: 描述什么是仅通知聊天机器人Microsoft Teams
keywords: teams 自动程序通知
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 01/29/2020
ms.openlocfilehash: 71dbc07445a57194e90ba3985c3aff1e2d4f2cdf
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155289"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>仅通知聊天机器人Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

如果你的自动程序的唯一用途是向用户发送通知，并且不是对话的，可以在应用清单中启用 `isNotificationOnly` 字段。 这将生成以下更改：

* 用户无法向仅通知机器人发送消息。
* 用户无法@mention自动程序。

> [!NOTE]
> 仅机器人应用将在两种情况下均在个人应用托盘中显示：或 `isNotificationOnly: true` `isNotificationOnly: false` 。

## <a name="app-manifest"></a>应用部件清单

若要启用此功能，请设置为 `isNotificationOnly` `true` 。

> [!NOTE]
> 请注意，的值是 `isNotificationOnly` 布尔值，而不是字符串。

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

## <a name="best-practices-and-limitations"></a>最佳做法和限制

* 仅通知机器人使用主动消息与用户通信。 有关详细信息，请参阅 [自动程序主动消息传递](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。
