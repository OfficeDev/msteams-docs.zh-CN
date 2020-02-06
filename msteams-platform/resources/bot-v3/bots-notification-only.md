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
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="d4e85-104">Microsoft 团队中仅通知的 bot</span><span class="sxs-lookup"><span data-stu-id="d4e85-104">Notification-only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="d4e85-105">如果你的 bot 的唯一用途是将通知传递给用户，而不是会话，则可以`isNotificationOnly`在应用程序清单中启用该字段。</span><span class="sxs-lookup"><span data-stu-id="d4e85-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="d4e85-106">这将产生以下更改：</span><span class="sxs-lookup"><span data-stu-id="d4e85-106">This produces the following changes:</span></span>

* <span data-ttu-id="d4e85-107">用户无法发送仅限通知的 bot。</span><span class="sxs-lookup"><span data-stu-id="d4e85-107">Users cannot message your notification-only bot.</span></span>
* <span data-ttu-id="d4e85-108">用户不能 @mention 机器人。</span><span class="sxs-lookup"><span data-stu-id="d4e85-108">Users cannot @mention the bot.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="d4e85-109">应用程序清单</span><span class="sxs-lookup"><span data-stu-id="d4e85-109">App manifest</span></span>

<span data-ttu-id="d4e85-110">若要启用此设置`isNotificationOnly` ， `true`请将设置为。</span><span class="sxs-lookup"><span data-stu-id="d4e85-110">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="d4e85-111">请注意，的值`isNotificationOnly`是布尔值，而不是字符串。</span><span class="sxs-lookup"><span data-stu-id="d4e85-111">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="d4e85-112">最佳实践和限制</span><span class="sxs-lookup"><span data-stu-id="d4e85-112">Best practices and limitations</span></span>

* <span data-ttu-id="d4e85-113">仅通知 bot 使用主动消息传递与用户的通信。</span><span class="sxs-lookup"><span data-stu-id="d4e85-113">Notification-only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="d4e85-114">有关详细信息，请参阅[用于 bot 的主动消息](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。</span><span class="sxs-lookup"><span data-stu-id="d4e85-114">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more details.</span></span>
