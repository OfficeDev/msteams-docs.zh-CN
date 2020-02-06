---
title: 仅通知 bot
description: 介绍 Microsoft 团队中的仅通知 bot
keywords: 团队 bot 通知
ms.date: 01/29/2020
ms.openlocfilehash: d312f9cd4558d35fc2492b5cf0b4f77b65660833
ms.sourcegitcommit: 44ac886c0ca34a16222d3991a61606f8483b8481
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2020
ms.locfileid: "41783904"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Microsoft 团队中仅通知的 bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

如果你的 bot 的唯一用途是将通知传递给用户，而不是会话，则可以`isNotificationOnly`在应用程序清单中启用该字段。 这将产生以下更改：

* 用户无法发送仅限通知的 bot。
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

* 仅通知 bot 使用主动消息传递与用户的通信。 有关详细信息，请参阅[用于 bot 的主动消息](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。
