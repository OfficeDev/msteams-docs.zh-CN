---
title: 添加自动程序菜单
description: 介绍如何为聊天机器人创建Microsoft Teams
keywords: teams 自动程序菜单创建
ms.topic: how-to
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: da6f36e1b7071b92f6411ab7d2afdccb795946b7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566766"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a>在"聊天机器人"菜单中添加Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

为了帮助发现和帮助用户了解机器人的功能，你现在可以添加每当用户与机器人交互时都会显示的菜单。 菜单将显示命令文本，并提供帮助文本，如使用示例或命令用途的说明。

![自动程序菜单的屏幕截图](~/assets/images/bots/bot-menus-bot-menu-sample.png)

当用户选择菜单项时，命令字符串将插入到文本框中，帮助用户完成自动程序消息。

## <a name="bot-menu-support-on-teams-mobile-app"></a>移动应用上的自动Teams支持
> [!NOTE] 
> 自动程序菜单不会显示在移动设备上。

## <a name="app-manifest"></a>应用部件清单

若要创建自动程序菜单，请向应用清单的自动程序 [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) 部分下添加新对象。 对于自动程序支持的每个范围，可以使用单独的命令声明单个菜单 (、 或) 每个菜单最多支持 `personal` `groupChat` `team` 10 个命令。

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a>清单摘录 - 两个作用域的单个菜单

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a>清单摘录 - 每个作用域的单独菜单

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

## <a name="best-practices"></a>最佳做法

* 保持简单：自动程序菜单旨在显示自动程序的关键功能。
* 保持简短：菜单选项不应是超长且复杂的自然语言语句-它们应该是简单的命令。
* 始终可用：自动程序菜单操作/命令应始终可进行通话，无论机器人位于对话或对话的状态如何。
