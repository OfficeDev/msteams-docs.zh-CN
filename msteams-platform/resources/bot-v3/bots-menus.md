---
title: 添加机器人菜单
description: 在本模块中，了解如何在Microsoft Teams中添加机器人菜单，并在Microsoft Teams中为机器人创建菜单
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: ed65699b930d3e5334dd7fbb03da18a1482d6e5d
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143380"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a>在Microsoft Teams中添加机器人菜单

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

为了帮助发现并帮助用户了解机器人的功能，现在可以在用户与机器人交互时添加显示的菜单。 菜单将显示命令文本，并提供帮助文本，例如使用示例或命令用途说明。

![机器人菜单的屏幕截图](~/assets/images/bots/bot-menus-bot-menu-sample.png)

当用户选择菜单项时，命令字符串将插入文本框，以帮助用户完成机器人消息。

## <a name="bot-menu-support-on-teams-mobile-app"></a>Teams移动应用上的机器人菜单支持

> [!NOTE]
> 机器人菜单不会显示在移动设备上。

## <a name="app-manifest"></a>应用部件清单

若要创建机器人菜单，请将新 [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) 对象添加到机器人部分下的应用清单。 可以为机器人支持 (`personal`的每个范围声明具有单独命令的单个菜单， `groupChat`或者 `team`) 每个菜单最多支持 10 个命令。

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a>清单摘录 - 每个范围的单独菜单

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

## <a name="best-practices"></a>最佳实践

* 保持简单：机器人菜单旨在呈现机器人的关键功能。
* 保持简短：菜单选项不应是非常长和复杂的自然语言语句 - 它们应该是简单的命令。
* 始终可用：机器人菜单操作/命令应始终可调用，而不考虑聊天状态或机器人所在的对话框。
