---
title: 仅限通知的机器人
description: 在本模块中，了解Microsoft Teams、应用清单及其最佳做法和限制中的仅限通知的机器人
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 01/29/2020
ms.openlocfilehash: 547ef73cfd036efe566afe15e4f50701a275c2cd
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144297"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Microsoft Teams 中仅限通知的机器人

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

如果机器人的唯一用途是向用户传递通知，而不是聊天，则可以在应用清单中启用该 `isNotificationOnly` 字段。 这会产生以下变化：

* 用户无法向仅通知机器人发送消息。
* 用户无法@mention机器人。

> [!NOTE]
> 在以下两种情况下，仅限机器人的应用会显示在个人应用托盘中：`isNotificationOnly: true` 或 `isNotificationOnly: false`。

## <a name="app-manifest"></a>应用部件清单

若要启用此功能，请将 `isNotificationOnly` 设置为 `true`。

> [!NOTE]
> `isNotificationOnly` 的值是布尔值，而不是字符串。

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

* 仅限通知的机器人使用主动消息传送与用户通信。 有关详细信息，请参阅[机器人的主动消息传送](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。
