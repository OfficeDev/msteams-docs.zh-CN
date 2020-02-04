---
title: 为你的 bot 创建命令菜单
author: clearab
description: 如何为 Microsoft 团队 bot 创建命令菜单
ms.topic: overview, command menu
ms.author: anclear
ms.openlocfilehash: 81efb94fc882aa4653ab162863d5d973aeae87b9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673135"
---
# <a name="bot-command-menus"></a>Bot 命令菜单

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> 移动客户端上不会显示 Bot 菜单。

通过为你的 bot 添加命令菜单，你可以定义你的 bot 可以始终响应的一组核心命令。 当用户正在使用你的 bot 时，会向用户显示撰写邮件区域上方的命令列表。 从列表中选择一个命令会将命令字符串插入到撰写消息框中，所有用户都需要选择 "**发送**"。

![Bot 命令菜单](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a>为你的 bot 创建命令菜单

命令菜单在应用部件清单（manifest）中定义。 您可以使用应用程序 Studio 来帮助您创建它们，也可以手动添加它们。

### <a name="creating-a-command-menu-for-your-bot-using-app-studio"></a>使用应用程序 Studio 为你的机器人创建命令菜单

此处的说明假定您将编辑现有的应用程序清单。 无论是创建新的清单还是编辑现有的清单，添加命令菜单的步骤都是相同的。

1. 打开应用程序 Studio .。。左侧导航轨上的 "溢出" 菜单。 如果你没有可用的应用程序，可以下载。 有关使用应用程序 Studio 的详细信息，请参阅[安装应用程序 studio](https://aka.ms/teams-app-studio#installing-app-studio) 。

    ![应用程序工作室](./conversations/media/AppStudio.png)

2. 在应用程序 Studio 中，选择 "**清单编辑器**" 选项卡。

3. 在 "**功能**" 部分的 "清单编辑器" 视图的左列中，选择 " **bot**"。

4. 在清单编辑器视图的右列中的 "**命令**" 部分，选择 "**添加**" 按钮。

    ![应用程序 Studio 命令菜单添加按钮](./conversations/media/AppStudio-CommandMenu-Add.png)

5. 将显示**新的命令**屏幕。 输入要显示为菜单命令的**命令文本**，以及要在菜单中的命令文本正下方显示的 "**帮助" 文本**。 这应该是命令用途的简短说明。

6. 接下来，选择要在其中显示此命令菜单的范围，然后选择 "**保存**" 按钮。

    ![应用程序 Studio 命令菜单添加按钮](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="creating-a-command-menu-for-your-bot-by-editing-manifestjson"></a>通过编辑 Manifest 创建用于你的 bot 的命令菜单**json**

创建命令菜单的另一种有效方法是在开发 bot 源代码时直接在清单文件中创建它。 使用此方法时，请记住以下几点：

1. 每个菜单最长可支持10个命令。

2. 可以创建将在所有范围中运行的单个命令菜单。

3. 您可以为每个作用域创建不同的命令菜单

#### <a name="manifest-example---single-menu-for-both-scopes"></a>清单示例-两个范围的单个菜单

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

#### <a name="manifest-example---menu-for-each-scope"></a>清单示例-每个范围的菜单

```json
{
  ...
  "bots":[
    {
      "botId":"<Microsoft app ID for your bot>",
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

## <a name="handling-menu-commands-in-your-bot-code"></a>处理机器人代码中的菜单命令

组或通道中的 bot 仅在邮件中提及（"@botname"）时响应。 因此，在组或频道作用域中，由 bot 接收的每封邮件将在返回的邮件文本中包含其自己的名称。 您需要确保在处理返回的命令之前，您的邮件分析处理程序。

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

您可以使用 Microsoft Bot 框架（名为`Activity` `RemoveRecipientMention`的类的方法）提供的静态方法分析邮件文本的** \@提及**部分。

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node.js](#tab/javascript)

您可以使用 Microsoft Bot 框架（名为`TurnContext` `removeMentionText`的类的方法）提供的静态方法分析邮件文本的** \@提及**部分。

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="pythontabpython"></a>[Python](#tab/python)


您可以使用 Microsoft Bot **** 框架（名为`TurnContext` `remove_recipient_mention`的类的方法）提供的静态方法分析邮件文本的 @Mention 部分。

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

## <a name="command-menu-best-practices"></a>命令菜单最佳做法

* **保持简单**： bot 菜单旨在提供你的 bot 的主要功能。
* **保持简短**：菜单选项不应是超长且复杂的自然语言语句—它们应为简单命令。
* **将其 invokable**：自动程序菜单操作/命令应始终可用，而不考虑会话的状态或机器人所在的对话框。
