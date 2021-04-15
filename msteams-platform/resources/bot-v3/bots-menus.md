---
title: 添加自动程序菜单
description: 介绍如何在 Microsoft Teams 中为机器人创建菜单
keywords: teams 自动程序菜单创建
ms.topic: how-to
ms.date: 05/20/2019
ms.openlocfilehash: 3623d85c1531b9942633af940c5e41ac1c574441
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696141"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a><span data-ttu-id="b2684-104">在 Microsoft Teams 中添加自动程序菜单</span><span class="sxs-lookup"><span data-stu-id="b2684-104">Add a bot menu in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="b2684-105">为了帮助发现和帮助用户了解机器人的功能，你现在可以添加每当用户与机器人交互时都会显示的菜单。</span><span class="sxs-lookup"><span data-stu-id="b2684-105">To aid discovery and to help educate users about your bot’s functionality, you can now add menus that surface whenever the user interacts with your bot.</span></span> <span data-ttu-id="b2684-106">菜单将显示命令文本，并提供帮助文本，如使用示例或命令用途的说明。</span><span class="sxs-lookup"><span data-stu-id="b2684-106">The menu will show the command text and also provide help text, such as a usage example or description of the command’s purpose.</span></span>

![自动程序菜单的屏幕截图](~/assets/images/bots/bot-menus-bot-menu-sample.png)

<span data-ttu-id="b2684-108">当用户选择菜单项时，命令字符串将插入到文本框中，帮助用户完成自动程序消息。</span><span class="sxs-lookup"><span data-stu-id="b2684-108">When a user selects a menu item, the command string is inserted into the text box to aid in user completion of the bot message.</span></span>

## <a name="bot-menu-support-on-teams-mobile-app"></a><span data-ttu-id="b2684-109">Teams 移动应用上的自动程序菜单支持</span><span class="sxs-lookup"><span data-stu-id="b2684-109">Bot menu support on Teams mobile app</span></span>
> [!NOTE] 
> <span data-ttu-id="b2684-110">自动程序菜单不显示在移动设备上</span><span class="sxs-lookup"><span data-stu-id="b2684-110">Bot menus are not displayed on mobile devices</span></span>

## <a name="app-manifest"></a><span data-ttu-id="b2684-111">应用清单</span><span class="sxs-lookup"><span data-stu-id="b2684-111">App manifest</span></span>

<span data-ttu-id="b2684-112">若要创建自动程序菜单，请向应用清单的自动程序 [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) 部分下添加新对象。</span><span class="sxs-lookup"><span data-stu-id="b2684-112">To create a bot menu, add a new [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) object to your app manifest under the bot section.</span></span> <span data-ttu-id="b2684-113">对于自动程序支持的每个范围，可以使用单独的命令声明单个菜单 `personal` (，) 每个菜单最多支持 `groupChat` `team` 10 个命令。</span><span class="sxs-lookup"><span data-stu-id="b2684-113">You can declare individual menus with separate commands for each scope your bot supports (`personal`, `groupChat` or `team`) Each menu supports up to 10 commands.</span></span>

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a><span data-ttu-id="b2684-114">清单摘录 - 两个作用域的单个菜单</span><span class="sxs-lookup"><span data-stu-id="b2684-114">Manifest excerpt - single menu for both scopes</span></span>

```json
{
  ⋮
  "bots":[
    {
      "botId":"[Microsoft App ID for your bot]",
      "scopes": [
        "personal",
        "team"
      ],
      "commandLists":[
        {
          "scopes":[
            "team",
            "personal"
          ],
          "commands":[
            {
              "title":"Help",
              "description":"Displays this help message"
            },
            {
              "title":"Search Flights",
              "description":"Search flights from Seattle to Phoenix May 2-5 departing after 3pm"
            },
            {
              "title":"Search Hotels",
              "description":"Search hotels in Portland tonight"
            },
            {
              "title":"Best Time to Fly",
              "description":"Best time to fly to London for a 5 day trip this summer"
            }
          ]
        }
      ]
    }
  ],
  ...
}
```

### <a name="manifest-excerpt---separate-menu-per-scope"></a><span data-ttu-id="b2684-115">清单摘录 - 每个作用域的单独菜单</span><span class="sxs-lookup"><span data-stu-id="b2684-115">Manifest excerpt - separate menu per scope</span></span>

```json
{
  ...
  "bots":[
    {
      "botId":"[Microsoft app ID for your bot]",
      "scopes": [
        "groupChat",
        "team"
      ],
      "commandLists":[
        {
          "scopes":[
            "team"
          ],
          "commands":[
            {
            "title":"help",
            "description":"Displays this help message for channels"
            }
          ]
        },
        {
          "scopes":[
            "groupChat"
          ],
          "commands":[
            {
            "title":"help",
            "description":"Displays this help message for group chat"
            }
          ]
        }
      ]
    }
  ],
  ...
}
```

## <a name="best-practices"></a><span data-ttu-id="b2684-116">最佳做法</span><span class="sxs-lookup"><span data-stu-id="b2684-116">Best practices</span></span>

* <span data-ttu-id="b2684-117">保持简单：自动程序菜单旨在显示自动程序的关键功能。</span><span class="sxs-lookup"><span data-stu-id="b2684-117">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="b2684-118">保持简短：菜单选项不应是超长且复杂的自然语言语句-它们应该是简单的命令。</span><span class="sxs-lookup"><span data-stu-id="b2684-118">Keep it short: Menu options shouldn’t be extremely long and complex natural language statements - they should be simple commands.</span></span>
* <span data-ttu-id="b2684-119">始终可用：自动程序菜单操作/命令应始终可进行通话，无论机器人位于对话或对话的状态如何。</span><span class="sxs-lookup"><span data-stu-id="b2684-119">Always available: Bot menu actions/commands should be always invokable, regardless of the state of the conversation or the dialog the bot is in.</span></span>
