---
title: 添加机器人菜单
description: 介绍如何为 Microsoft 团队中的 bot 创建菜单
keywords: 团队 bot 菜单创建
ms.date: 05/20/2019
ms.openlocfilehash: 36a224dc21cccc5fcd1047e45e3d749e7ca19ea7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673033"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a><span data-ttu-id="0e6fd-104">在 Microsoft 团队中添加机器人菜单</span><span class="sxs-lookup"><span data-stu-id="0e6fd-104">Add a bot menu in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="0e6fd-105">若要协助发现并帮助用户了解你的 bot 的功能，你现在可以在用户与你的 bot 交互时添加表面的菜单。</span><span class="sxs-lookup"><span data-stu-id="0e6fd-105">To aid discovery and to help educate users about your bot’s functionality, you can now add menus that surface whenever the user interacts with your bot.</span></span> <span data-ttu-id="0e6fd-106">菜单将显示命令文本，还提供帮助文本，例如命令用途的用法示例或说明。</span><span class="sxs-lookup"><span data-stu-id="0e6fd-106">The menu will show the command text and also provide help text, such as a usage example or description of the command’s purpose.</span></span>

![机器人菜单的屏幕截图](~/assets/images/bots/bot-menus-bot-menu-sample.png)

<span data-ttu-id="0e6fd-108">当用户选择菜单项时，命令字符串将插入到文本框中，以帮助用户完成 bot 消息。</span><span class="sxs-lookup"><span data-stu-id="0e6fd-108">When a user selects a menu item, the command string is inserted into the text box to aid in user completion of the bot message.</span></span>

## <a name="bot-menu-support-on-teams-mobile-app"></a><span data-ttu-id="0e6fd-109">机器人菜单对工作组移动应用程序的支持</span><span class="sxs-lookup"><span data-stu-id="0e6fd-109">Bot menu support on Teams mobile app</span></span>
> [!NOTE] 
> <span data-ttu-id="0e6fd-110">移动设备上不显示 Bot 菜单</span><span class="sxs-lookup"><span data-stu-id="0e6fd-110">Bot menus are not displayed on mobile devices</span></span>

## <a name="app-manifest"></a><span data-ttu-id="0e6fd-111">应用程序清单</span><span class="sxs-lookup"><span data-stu-id="0e6fd-111">App manifest</span></span>

<span data-ttu-id="0e6fd-112">若要创建 bot 菜单，请将新[`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists)对象添加到应用程序清单中的 bot 部分下。</span><span class="sxs-lookup"><span data-stu-id="0e6fd-112">To create a bot menu, add a new [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) object to your app manifest under the bot section.</span></span> <span data-ttu-id="0e6fd-113">您可以使用单独的命令为你的 bot 支持的每个作用`personal`域`groupChat`声明`team`单个菜单（或）每个菜单最多支持10个命令。</span><span class="sxs-lookup"><span data-stu-id="0e6fd-113">You can declare individual menus with separate commands for each scope your bot supports (`personal`, `groupChat` or `team`) Each menu supports up to 10 commands.</span></span>

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a><span data-ttu-id="0e6fd-114">清单节选-两个范围的单个菜单</span><span class="sxs-lookup"><span data-stu-id="0e6fd-114">Manifest excerpt - single menu for both scopes</span></span>

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a><span data-ttu-id="0e6fd-115">清单节选-每个范围一个单独的菜单</span><span class="sxs-lookup"><span data-stu-id="0e6fd-115">Manifest excerpt - separate menu per scope</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="0e6fd-116">最佳做法</span><span class="sxs-lookup"><span data-stu-id="0e6fd-116">Best practices</span></span>

* <span data-ttu-id="0e6fd-117">保持简单： bot 菜单旨在提供你的 bot 的主要功能。</span><span class="sxs-lookup"><span data-stu-id="0e6fd-117">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="0e6fd-118">保持简短：菜单选项不应是超长且复杂的自然语言语句-它们应为简单命令。</span><span class="sxs-lookup"><span data-stu-id="0e6fd-118">Keep it short: Menu options shouldn’t be extremely long and complex natural language statements - they should be simple commands.</span></span>
* <span data-ttu-id="0e6fd-119">始终可用：自动程序菜单操作/命令应始终 invokable，而不考虑会话状态或机器人所在的对话框。</span><span class="sxs-lookup"><span data-stu-id="0e6fd-119">Always available: Bot menu actions/commands should be always invokable, regardless of the state of the conversation or the dialog the bot is in.</span></span>
