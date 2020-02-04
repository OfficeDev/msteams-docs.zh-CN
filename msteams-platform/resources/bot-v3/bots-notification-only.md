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
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="f94aa-104">仅通知 Microsoft 团队中的 bot</span><span class="sxs-lookup"><span data-stu-id="f94aa-104">Notification only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="f94aa-105">如果你的 bot 的唯一用途是将通知传递给用户，而不是会话，则可以`isNotificationOnly`在应用程序清单中启用该字段。</span><span class="sxs-lookup"><span data-stu-id="f94aa-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="f94aa-106">这将产生以下更改：</span><span class="sxs-lookup"><span data-stu-id="f94aa-106">This produces the following changes:</span></span>

* <span data-ttu-id="f94aa-107">用户无法将仅通知 bot 发送给您。</span><span class="sxs-lookup"><span data-stu-id="f94aa-107">Users cannot message your notification only bot.</span></span>
* <span data-ttu-id="f94aa-108">用户不能 @mention 机器人。</span><span class="sxs-lookup"><span data-stu-id="f94aa-108">Users cannot @mention the bot.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="f94aa-109">应用程序清单</span><span class="sxs-lookup"><span data-stu-id="f94aa-109">App manifest</span></span>

<span data-ttu-id="f94aa-110">若要启用此设置`isNotificationOnly` ， `true`请将设置为。</span><span class="sxs-lookup"><span data-stu-id="f94aa-110">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="f94aa-111">请注意，的值`isNotificationOnly`是布尔值，而不是字符串。</span><span class="sxs-lookup"><span data-stu-id="f94aa-111">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="f94aa-112">最佳实践和限制</span><span class="sxs-lookup"><span data-stu-id="f94aa-112">Best practices and limitations</span></span>

* <span data-ttu-id="f94aa-113">您不能仅`personal`创建作用域通知 bot，因为用户无法在个人聊天中发送仅通知 bot。</span><span class="sxs-lookup"><span data-stu-id="f94aa-113">You cannot create a `personal` scoped notification only bot, as the user cannot message your notification only bot in a personal chat.</span></span> <span data-ttu-id="f94aa-114">这意味着，您无法收到可`conversationUpdate`提供用于发送通知的必要详细信息的事件。</span><span class="sxs-lookup"><span data-stu-id="f94aa-114">This means that you can't receive a `conversationUpdate` event that would provide you with the necessary details to send a notification.</span></span> <span data-ttu-id="f94aa-115">仅当支持该`team`作用域并将其添加到团队中时，仅通知 bot 才能正常工作。</span><span class="sxs-lookup"><span data-stu-id="f94aa-115">Your notification only bot will only function correctly if it supports the `team` scope and is added to a team.</span></span> <span data-ttu-id="f94aa-116">在 "团队设置" 中，你的 bot 将有权访问将通知发送到频道或私下给用户所需的信息。</span><span class="sxs-lookup"><span data-stu-id="f94aa-116">In the team setting, your bot will have access to the necessary information to either send a notification to a channel or privately to a user.</span></span>
* <span data-ttu-id="f94aa-117">仅通知 bot 使用主动消息与用户通信。</span><span class="sxs-lookup"><span data-stu-id="f94aa-117">Notification only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="f94aa-118">有关详细信息，请参阅[用于 bot 的主动消息](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。</span><span class="sxs-lookup"><span data-stu-id="f94aa-118">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more details.</span></span>
