---
title: 为机器人创建命令菜单
author: surbhigupta
description: 在本模块中，了解如何使用代码示例为 Microsoft Teams 机器人创建和处理命令菜单。
ms.topic: how-to
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: e14afc31839368c7826a6ee15a6f779b5f6f47b1
ms.sourcegitcommit: 69a45722c5c09477bbff3ba1520e6c81d2d2d997
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/11/2022
ms.locfileid: "67312301"
---
# <a name="create-a-commands-menu"></a>创建命令菜单

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

若要定义机器人可以响应的一组核心命令，可以添加一个命令菜单，其中包含用于机器人的命令下拉列表。 在用户与机器人对话时，命令列表将显示在用户的撰写消息区域中。 从列表中选择一个命令，将命令字符串插入撰写消息框，然后选择“**发送**”。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="conversations/Media/bot-menu-sample.png" alt-text="Bot-command-menu":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="conversations/Media/mobile-bot-menu-sample.png" alt-text="Mobile-bot-command-menu":::

* * *

## <a name="create-a-command-menu-for-your-bot"></a>为机器人创建命令菜单

在应用清单中定义命令菜单。 可以使用 **开发人员门户** 创建它们，也可以在应用清单中手动添加它们。

### <a name="create-a-command-menu-for-your-bot-using-developer-portal"></a>使用开发人员门户为机器人创建命令菜单

为机器人创建命令菜单的先决条件是必须编辑现有应用清单。 无论是创建新清单还是编辑现有清单，添加命令菜单的步骤都是相同的。

使用开发人员门户为机器人创建命令菜单：

1. 打开 Teams，然后从左窗格中选择“**应用**”。 在 **“应用”** 页中，搜索 **开发人员门户**，然后选择 **“打开**”。

   :::image type="content" source="../../assets/images/tdp/add-dev-portal.png" alt-text="屏幕截图显示了如何在 Teams 客户端中添加开发人员门户。":::
  
1. 在 **开发人员门户** 中，选择 **“应用** ”选项卡。如果没有现有应用包，可以创建或导入现有应用。 有关详细信息，请参阅 [Teams 开发人员门户](../../concepts/build-and-test/teams-developer-portal.md)。

1. 选择 **“应用”** 选项卡，从左窗格中选择 **“应用”功能** ，然后选择 **“机器人**”。

1. 在 **“命令**”部分下选择 **“添加命令**”。

   :::image type="content" source="../../assets/images/tdp/add-a-bot-command.png" alt-text="屏幕截图显示了如何在开发人员门户中为机器人添加命令。":::

1. 输入显示为机器人命令菜单的 **命令** 。

1. 输入菜单中命令文本下显示的 **说明** 。 **说明** 必须是命令用途的简要说明。

1. 选中“ **范围** ”复选框，然后选择 **“添加**”。
   这定义了命令菜单必须显示的位置。

   :::image type="content" source="../../assets/images/tdp/bot-command.png" alt-text="屏幕截图显示了如何为机器人添加命令、说明和作用域。":::

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>通过编辑 Manifest.json 为机器人创建命令菜单

创建命令菜单的另一种方法是在开发机器人源代码时直接在清单文件中创建。若要使用此方法，请遵循以下几点:

* 每个菜单最多支持 10 个命令。
* 创建一个在所有范围内生效的单个命令菜单。
* 为每个范围创建另一个命令菜单。

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a>适用于两个范围的单个菜单的清单示例

适用于两个范围的单个菜单的清单示例代码如下所示：

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

#### <a name="manifest-example-for-the-menu-for-each-scope"></a>适用于每个范围的菜单的清单示例

适用于每个范围的菜单的清单示例代码如下所示：

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

在处理来自用户的任何消息时，必须在机器人代码中处理菜单命令。 可以通过分析消息文本的“**\@提及**”部分来在机器人代码中处理菜单命令。

## <a name="handle-menu-commands-in-your-bot-code"></a>在机器人代码中处理菜单命令

组或通道中的机器人仅在消息提到 `@botname` 它们时才会响应。 机器人在组或频道范围内收到的每条消息的消息文本中都包含其名称。 在处理要返回的命令之前，消息分析必须处理机器人收到的含有其名称的消息。

> [!NOTE]
> 为了在代码中处理这些命令，命令将作为常规消息发送到机器人。 你必须像处理来自用户的任何其他消息那样处理这些命令。 代码中的命令会将预配置的文本插入文本框中。 然后，用户必须像发送任何其他消息一样发送该文本。

# <a name="c"></a>[C#](#tab/dotnet)

可以使用 Microsoft Bot Framework 提供的一个静态方法分析消息文本的“**\@提及**”部分。 该方法是 `Activity` 类方法，名为 `RemoveRecipientMention`。

用于分析消息文本的“**\@提及**”部分的 C# 代码如下所示：

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

可以使用 Bot Framework 提供的一个静态方法分析消息文本的“**\@提及**”部分。 该方法是 `TurnContext` 类方法，名为 `removeMentionText`。

用于分析消息文本的“**\@提及**”部分的 JavaScript 代码如下所示：

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[Python](#tab/python)

可以使用“聊天机器人框架”提供的一个静态方法分析消息文本的 **@提及** 部分。它是名为 `remove_recipient_mention` 的 `TurnContext` 类方法。

用于分析消息文本的“**\@提及**”部分的 Python 代码如下所示：

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

若要使机器人代码顺利运行，必须遵循一些最佳做法。

## <a name="command-menu-best-practices"></a>命令菜单最佳做法

下面是命令菜单最佳做法：

* 保持简单：机器人菜单旨在呈现机器人的关键功能。
* 保持简短: 菜单选项不能冗长，不能是复杂的自然语言语句。它们必须是简单的命令。
* 始终可调用：无论机器人所在的聊天或对话的状态如何，机器人菜单操作或命令必须始终可用。

> [!NOTE]
> 如果从清单中删除任何命令，则必须重新部署应用以实现更改。 一般情况下，对清单所做的任何更改都需要重新部署应用。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [频道和群组对话](~/bots/how-to/conversations/channel-and-group-conversations.md)
