---
title: 为机器人创建命令菜单
author: surbhigupta
description: 了解如何使用代码示例为Microsoft Teams机器人创建命令菜单。
ms.topic: how-to
ms.localizationpriority: medium
ms.author: anclear
keywords: 命令菜单撰写消息对话@mention
ms.openlocfilehash: 6f4b9cdac76fc9beb42a39dde3b320036ea580b5
ms.sourcegitcommit: e40383d9081bf117030f7e6270140e6b94214e8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65102544"
---
# <a name="bot-command-menus"></a>机器人命令菜单

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

若要定义机器人可以响应的一组核心命令，可以添加一个命令菜单，其中包含机器人的命令下拉列表。 在与机器人对话时，命令列表将显示给撰写消息区域中的用户。 从列表中选择一个命令，将命令字符串插入撰写消息框，然后选择 **“发送**”。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

![机器人命令菜单](./conversations/media/bot-menu-sample.png)

# <a name="mobile"></a>[移动设备](#tab/mobile)

![移动机器人命令菜单](./conversations/media/mobile-bot-menu-sample.png)

* * *

## <a name="create-a-command-menu-for-your-bot"></a>为机器人创建命令菜单

命令菜单在应用清单中定义。 可以使用 **App Studio** 创建它们，也可以在应用清单中手动添加它们。

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a>使用 App Studio 为机器人创建命令菜单

为机器人创建命令菜单的先决条件是必须编辑现有应用清单。 无论是创建新清单还是编辑现有清单，添加命令菜单的步骤都是相同的。

**使用 App Studio 为机器人创建命令菜单**

1. 打开Teams，然后从左窗格中选择 **“应用**”。 在 **“应用”** 页中，搜索 **App Studio**，然后选择 **“打开**”。
   > [!NOTE]
   > 如果没有 **App Studio**，可以下载它。 有关详细信息，请参阅 [安装 App Studio](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio)。

    :::image type="content" source="/media/AppStudio.png" alt-text="安装应用工作室"lightbox="media/AppStudio.png"border="true":::

2. 在 **App Studio** 中，选择 **“清单编辑器** ”选项卡。如果没有现有应用包，可以创建或导入现有应用。 有关详细信息，请参阅 [更新应用包](~/get-started/deploy-csharp-app-studio.md)。

3. 在 **清单编辑器** 的左窗格和“ **功能** ”部分中，选择 **“机器人**”。

4. 在 **清单编辑器** 的右窗格和 **“命令”** 部分中，选择 **“添加**”。 将显示 **“新建命令** ”屏幕。

    :::image type="content" source="/media/AppStudio-CommandMenu-Add.png" alt-text="选择应用包"lightbox="/media/AppStudio-CommandMenu-Add.png"border="true":::

5. 输入必须显示为机器人命令菜单的 **命令文本** 。

6. 输入“ **帮助”文本** ，该文本必须显示在菜单中的命令文本下。 **帮助文本** 必须是命令用途的简要说明。

7. 选择 **“范围** ”复选框以选择此命令菜单必须显示的位置，然后选择 **“保存**”。

:::image type="content" source="/media/AppStudio-NewCommandMenu.png" alt-text="“App Studio 新建命令”菜单按钮"lightbox="/media/AppStudio-NewCommandMenu.png"border="true":::

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>通过编辑 Manifest.json 为机器人创建命令菜单

创建命令菜单的另一种方法是在开发机器人源代码时直接在清单文件中创建它。 若要使用此方法，请遵循以下几点：

* 每个菜单最多支持 10 个命令。
* 创建在所有范围内工作的单个命令菜单。
* 为每个范围创建不同的命令菜单。

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a>两个范围的单个菜单的清单示例

这两个作用域的单个菜单的清单示例代码如下所示：

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

在处理来自用户的任何消息时，必须在机器人代码中处理菜单命令。 可以通过分析消息文本的“提及”部分来处理机器人代码中的菜单命令。**\@**

## <a name="handle-menu-commands-in-your-bot-code"></a>处理机器人代码中的菜单命令

组或通道中的机器人仅在消息中提到 `@botname` 它们时才会响应。 机器人在组或通道范围内收到的每条消息在消息文本中都包含其名称。 在处理要返回的命令之前，消息分析必须处理机器人收到的消息及其名称。

> [!NOTE]
> 若要处理代码中的命令，它们将作为常规消息发送到机器人。 你必须处理它们，因为您将处理来自用户的任何其他消息。 代码中的命令将预配置的文本插入文本框中。 然后，用户必须像发送任何其他消息一样发送该文本。

# <a name="c"></a>[C#](#tab/dotnet)

可以使用随Microsoft Bot Framework提供的静态方法分析 **\@** 消息文本的“提及”部分。 它是命名`RemoveRecipientMention`类的方法`Activity`。

用于分析消息文本的 **\@“提及** ”部分的 C# 代码如下所示：

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

可以使用 Bot Framework 提供的静态方法分析 **\@** 消息文本的“提及”部分。 它是命名`removeMentionText`类的方法`TurnContext`。

用于分析消息文本的 **\@“提及** ”部分的 JavaScript 代码如下所示：

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[Python](#tab/python)

可以使用 Bot Framework 提供的静态方法分析消息文本的 **@Mention** 部分。 它是命名`remove_recipient_mention`类的方法`TurnContext`。

用于分析消息文本的 **\@“提及** ”部分的 Python 代码如下所示：

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

若要使机器人代码顺利运行，必须遵循一些最佳做法。

## <a name="command-menu-best-practices"></a>命令菜单最佳做法

下面是命令菜单最佳做法：

* 保持简单：机器人菜单旨在显示机器人的关键功能。
* 保持简短：菜单选项不能长，不能是复杂的自然语言语句。 它们必须是简单的命令。
* 使其可调用：机器人菜单操作或命令必须始终可用，而不考虑聊天状态或机器人所在的对话框。

> [!NOTE]
> 如果从清单中删除任何命令，则必须重新部署应用以实现更改。 一般情况下，对清单所做的任何更改都需要重新部署应用。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [频道和群组对话](~/bots/how-to/conversations/channel-and-group-conversations.md)
