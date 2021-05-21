---
title: 仅限通知的机器人
description: 描述什么是仅通知聊天机器人Microsoft Teams
keywords: teams 自动程序通知
ms.topic: conceptual
localization_priority: Normal
ms.date: 01/29/2020
ms.openlocfilehash: 3de462f73733f5f7cf223444ffe6deeb53faaaaa
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566759"
---
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="1877a-104">仅通知聊天机器人Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1877a-104">Notification-only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="1877a-105">如果你的自动程序的唯一用途是向用户发送通知，并且不是对话的，可以在应用清单 `isNotificationOnly` 中启用字段。</span><span class="sxs-lookup"><span data-stu-id="1877a-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="1877a-106">这将生成以下更改：</span><span class="sxs-lookup"><span data-stu-id="1877a-106">This produces the following changes:</span></span>

* <span data-ttu-id="1877a-107">用户无法向仅通知机器人发送消息。</span><span class="sxs-lookup"><span data-stu-id="1877a-107">Users cannot message your notification-only bot.</span></span>
* <span data-ttu-id="1877a-108">用户无法@mention自动程序。</span><span class="sxs-lookup"><span data-stu-id="1877a-108">Users cannot @mention the bot.</span></span>

> [!NOTE]
> <span data-ttu-id="1877a-109">仅机器人应用将在两种情况下均在个人应用托盘中显示：或 `isNotificationOnly: true` `isNotificationOnly: false` 。</span><span class="sxs-lookup"><span data-stu-id="1877a-109">The bot-only apps will surface in the personal app tray in both cases: `isNotificationOnly: true` or `isNotificationOnly: false`.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="1877a-110">应用部件清单</span><span class="sxs-lookup"><span data-stu-id="1877a-110">App manifest</span></span>

<span data-ttu-id="1877a-111">若要启用此功能，请设置为 `isNotificationOnly` `true` 。</span><span class="sxs-lookup"><span data-stu-id="1877a-111">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="1877a-112">请注意，的值 `isNotificationOnly` 是布尔值，而不是字符串。</span><span class="sxs-lookup"><span data-stu-id="1877a-112">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="1877a-113">最佳做法和限制</span><span class="sxs-lookup"><span data-stu-id="1877a-113">Best practices and limitations</span></span>

* <span data-ttu-id="1877a-114">仅通知机器人使用主动消息与用户通信。</span><span class="sxs-lookup"><span data-stu-id="1877a-114">Notification-only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="1877a-115">有关详细信息，请参阅 [自动程序主动消息传递](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。</span><span class="sxs-lookup"><span data-stu-id="1877a-115">For more information, see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>
