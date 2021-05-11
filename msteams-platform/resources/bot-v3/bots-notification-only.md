---
title: 仅限通知的机器人
description: 描述什么是仅通知聊天机器人Microsoft Teams
keywords: teams 自动程序通知
ms.topic: conceptual
localization_priority: Normal
ms.date: 01/29/2020
ms.openlocfilehash: 42a0b9acecbc1821ea492cb6c850c7a9b11bbbfe
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019760"
---
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="d5b84-104">仅通知聊天机器人Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d5b84-104">Notification-only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="d5b84-105">如果你的自动程序的唯一用途是向用户发送通知，并且不是对话的，可以在应用清单 `isNotificationOnly` 中启用字段。</span><span class="sxs-lookup"><span data-stu-id="d5b84-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="d5b84-106">这将生成以下更改：</span><span class="sxs-lookup"><span data-stu-id="d5b84-106">This produces the following changes:</span></span>

* <span data-ttu-id="d5b84-107">用户无法向仅通知机器人发送消息。</span><span class="sxs-lookup"><span data-stu-id="d5b84-107">Users cannot message your notification-only bot.</span></span>
* <span data-ttu-id="d5b84-108">用户无法@mention自动程序。</span><span class="sxs-lookup"><span data-stu-id="d5b84-108">Users cannot @mention the bot.</span></span>

> [!NOTE]
> <span data-ttu-id="d5b84-109">仅机器人应用将在两种情况下均在个人应用托盘中显示：或 `isNotificationOnly: true` `isNotificationOnly: false` 。</span><span class="sxs-lookup"><span data-stu-id="d5b84-109">The bot-only apps will surface in the personal app tray in both cases: `isNotificationOnly: true` or `isNotificationOnly: false`.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="d5b84-110">应用部件清单</span><span class="sxs-lookup"><span data-stu-id="d5b84-110">App manifest</span></span>

<span data-ttu-id="d5b84-111">若要启用此功能，请设置为 `isNotificationOnly` `true` 。</span><span class="sxs-lookup"><span data-stu-id="d5b84-111">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="d5b84-112">请注意，的值 `isNotificationOnly` 是布尔值，而不是字符串。</span><span class="sxs-lookup"><span data-stu-id="d5b84-112">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="d5b84-113">最佳做法和限制</span><span class="sxs-lookup"><span data-stu-id="d5b84-113">Best practices and limitations</span></span>

* <span data-ttu-id="d5b84-114">仅通知机器人使用主动消息与用户通信。</span><span class="sxs-lookup"><span data-stu-id="d5b84-114">Notification-only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="d5b84-115">有关详细信息 [，请参阅自动程序](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) 主动消息传递。</span><span class="sxs-lookup"><span data-stu-id="d5b84-115">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more details.</span></span>
