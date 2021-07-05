---
title: 为自动程序创建命令菜单
author: surbhigupta
description: 如何为自动程序创建Microsoft Teams菜单
ms.topic: how-to
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 4ee8c48b2f3b10c8924b0e81dae0a0c1f6014414
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254312"
---
# <a name="bot-command-menus"></a>自动程序命令菜单

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

若要定义自动程序可以响应的核心命令集，你可以添加一个命令菜单以及自动程序命令的下拉列表。 当用户与自动程序对话时，将在撰写邮件区域中显示命令列表。 Select a command from the list to insert the command string into the compose message box and select **Send**.

# <a name="desktop"></a>[桌面设备](#tab/desktop)

![自动程序命令菜单](./conversations/media/bot-menu-sample.png)

# <a name="mobile"></a>[移动设备](#tab/mobile)

![移动机器人命令菜单](./conversations/media/mobile-bot-menu-sample.png)

* * *

## <a name="create-a-command-menu-for-your-bot"></a>为自动程序创建命令菜单

命令菜单在应用清单中定义。 可以使用 App **Studio 创建** 它们，或在应用清单中手动添加它们。

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a>使用 App Studio 为机器人创建命令菜单

为自动程序创建命令菜单的先决条件是必须编辑现有应用清单。 无论是创建新清单还是编辑现有清单，添加命令菜单的步骤都是相同的。

**使用 App Studio 为机器人创建命令菜单**

1. 打开 **Teams，然后** 从左窗格中选择"应用"。 在"**应用"** 页中，搜索 **App Studio，** 然后选择"打开 **"。** 
   > [!NOTE]
   > 如果你没有 **App Studio，** 可以下载它。 有关详细信息，请参阅安装[App Studio。](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio)

    ![应用程序 Studio](./conversations/media/AppStudio.png)

2. 在 **App Studio** 中，选择 **"清单编辑器"** 选项卡。如果你没有现有应用包，可以创建或导入现有应用。 有关详细信息，请参阅 [更新应用包](~/get-started/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package)。

3. 在清单编辑器的左侧 **窗格中的**"功能"部分，选择"**自动程序"。**

4. 在清单编辑器的右侧 **窗格中的**"命令"部分 **，选择**"添加 **"。** 将显示 **"新建命令** "屏幕。

    ![App Studio 命令菜单添加按钮](./conversations/media/AppStudio-CommandMenu-Add.png)

5. 输入 **命令文本** ，该文本必须显示为自动程序的命令菜单。

6. 输入 **必须在菜单中** 的命令文本下显示的帮助文本。 **帮助文本** 必须是命令用途的简要说明。

7. 选中"**范围**"复选框以选择此命令菜单必须显示在何处，然后选择"保存 **"。**

    ![App Studio 新命令菜单按钮](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>通过编辑"打开"菜单为自动程序Manifest.js菜单

创建命令菜单的另一种方式是在开发自动程序源代码时直接在清单文件中创建它。 若要使用此方法，请遵循以下几点：

* 每个菜单最多支持 10 个命令。
* 创建在所有范围内工作的单个命令菜单。
* 为每个范围创建不同的命令菜单。

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a>两个作用域的单个菜单的清单示例

两个作用域的单个菜单的清单示例代码如下所示：

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

#### <a name="manifest-example-for-the-menu-for-each-scope"></a>每个范围的菜单的清单示例

每个范围的菜单的清单示例代码如下所示：

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

处理来自用户的任何消息时，必须在自动程序代码中处理菜单命令。 可以通过解析邮件文本的"提及"部分来处理自动程序 **\@ 代码中** 的菜单命令。

## <a name="handle-menu-commands-in-your-bot-code"></a>处理自动程序代码中的菜单命令

组或频道中的机器人仅在消息中提到时 `@botname` 进行响应。 自动程序在组或频道范围中收到的每封邮件在返回的消息文本中包含其名称。 在处理返回的命令之前，邮件分析必须处理自动程序使用其名称接收的消息。

> [!NOTE]
> 若要在代码中处理命令，它们作为常规消息发送到自动程序。 必须像处理用户发送的其他任何邮件一样处理邮件。 代码中的命令在文本框中插入预配置的文本。 然后，用户必须像发送任何其他邮件一样发送该文本。

# <a name="c"></a>[C#](#tab/dotnet)

可以使用邮件文本的 **\@ "提及**"部分分析邮件文本的静态Microsoft Bot Framework。 它是名为 的 `Activity` 类的一个方法 `RemoveRecipientMention` 。

用于C#"提及"部分的代码如下所示： **\@**

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

可以使用自动程序框架提供的静态 **\@** 方法分析邮件文本的"提及"部分。 它是名为 的 `TurnContext` 类的一个方法 `removeMentionText` 。

用于解析邮件文本的 **\@ "** 提及"部分的 JavaScript 代码如下所示：

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[Python](#tab/python)

可以使用 Bot Framework **@Mention** 静态方法解析邮件文本的 @Mention 部分。 它是名为 的 `TurnContext` 类的一个方法 `remove_recipient_mention` 。

用于分析邮件文本的 **\@ "提及**"部分的 Python 代码如下所示：

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

若要使自动程序代码顺利运行，必须遵循一些最佳做法。

## <a name="command-menu-best-practices"></a>命令菜单最佳实践

以下是命令菜单最佳实践：

* 保持简单：自动程序菜单旨在显示自动程序的关键功能。
* 保持简短：菜单选项不能长，不能是复杂的自然语言语句。 它们必须是简单的命令。
* 保持它可以进行通话：自动程序菜单操作或命令必须始终可用，无论对话的状态或聊天机器人位于哪个对话中。

> [!NOTE]
> 如果从清单中删除任何命令，则必须重新部署应用来实现更改。 通常，对清单的任何更改都需要重新部署应用。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [频道和群组对话](~/bots/how-to/conversations/channel-and-group-conversations.md)
