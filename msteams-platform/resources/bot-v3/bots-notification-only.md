---
title: 仅限通知的机器人
description: 介绍 Microsoft Teams 中什么是仅通知聊天机器人
keywords: teams 自动程序通知
ms.topic: conceptual
ms.date: 01/29/2020
ms.openlocfilehash: 39ba25893623d6b963b44363b8458db6def58b60
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696071"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Microsoft Teams 中的仅通知机器人

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

如果你的自动程序的唯一用途是向用户发送通知，并且不是对话的，可以在应用清单 `isNotificationOnly` 中启用字段。 这将生成以下更改：

* 用户无法向仅通知机器人发送消息。
* 用户无法@mention自动程序。

> [!NOTE]
> 仅机器人应用将在两种情况下均在个人应用托盘中显示：或 `isNotificationOnly: true` `isNotificationOnly: false` 。

## <a name="app-manifest"></a>应用清单

若要启用此功能，请设置为 `isNotificationOnly` `true` 。

> [!NOTE]
> 请注意，的值 `isNotificationOnly` 是布尔值，而不是字符串。

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

* 仅通知机器人使用主动消息与用户通信。 有关详细信息 [，请参阅自动程序](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) 主动消息传递。
