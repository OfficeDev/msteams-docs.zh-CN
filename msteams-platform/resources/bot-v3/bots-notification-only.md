---
title: 仅限通知的机器人
description: 描述什么是仅通知聊天机器人Microsoft Teams
keywords: teams 自动程序通知
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 01/29/2020
ms.openlocfilehash: d3ee5343ea159950859237f2a488557d9063eb6e
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355725"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>仅通知聊天机器人Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

如果你的自动程序的唯一用途是向 `isNotificationOnly` 用户发送通知，并且不是对话的，可以在应用清单中启用字段。 这将生成以下更改：

* 用户无法向仅通知机器人发送消息。
* 用户无法@mention自动程序。

> [!NOTE]
> 仅机器人应用将在两种情况下均在个人应用托盘中显示： `isNotificationOnly: true` 或 `isNotificationOnly: false`。

## <a name="app-manifest"></a>应用部件清单

若要启用此功能，请设置为 `isNotificationOnly` `true`。

> [!NOTE]
> 的值为 `isNotificationOnly` Boolean，而不是字符串。

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
