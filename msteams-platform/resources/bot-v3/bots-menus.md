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
# <a name="add-a-bot-menu-in-microsoft-teams"></a>在 Microsoft 团队中添加机器人菜单

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

若要协助发现并帮助用户了解你的 bot 的功能，你现在可以在用户与你的 bot 交互时添加表面的菜单。 菜单将显示命令文本，还提供帮助文本，例如命令用途的用法示例或说明。

![机器人菜单的屏幕截图](~/assets/images/bots/bot-menus-bot-menu-sample.png)

当用户选择菜单项时，命令字符串将插入到文本框中，以帮助用户完成 bot 消息。

## <a name="bot-menu-support-on-teams-mobile-app"></a>机器人菜单对工作组移动应用程序的支持
> [!NOTE] 
> 移动设备上不显示 Bot 菜单

## <a name="app-manifest"></a>应用程序清单

若要创建 bot 菜单，请将新[`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists)对象添加到应用程序清单中的 bot 部分下。 您可以使用单独的命令为你的 bot 支持的每个作用`personal`域`groupChat`声明`team`单个菜单（或）每个菜单最多支持10个命令。

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a>清单节选-两个范围的单个菜单

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a>清单节选-每个范围一个单独的菜单

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

* 保持简单： bot 菜单旨在提供你的 bot 的主要功能。
* 保持简短：菜单选项不应是超长且复杂的自然语言语句-它们应为简单命令。
* 始终可用：自动程序菜单操作/命令应始终 invokable，而不考虑会话状态或机器人所在的对话框。
