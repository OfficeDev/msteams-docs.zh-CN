---
title: 定义消息扩展操作命令
author: surbhigupta
description: 消息传递扩展操作命令及应用清单示例概述
ms.localizationpriority: high
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: ef9f1c45ec3b2d1df4bf5449885263034f19fde7
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111680"
---
# <a name="define-message-extension-action-commands"></a>定义消息扩展操作命令

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

利用操作命令可向用户呈现在 Teams 中称为任务模块的模式弹出窗口。 任务模块收集或显示信息、处理交互并将信息发送回 Teams。 本文档指导你如何选择操作命令调用位置、创建任务模块、发送最终消息或卡片、使用 App Studio 创建操作命令或手动创建操作命令。

在创建操作命令之前，必须确定以下因素：

1. [可以从何处触发操作命令？](#select-action-command-invoke-locations)
1. [如何创建任务模块？](#select-how-to-create-your-task-module)
1. [最终消息或卡片是从机器人发送到频道，还是将消息或卡片插入撰写消息区域供用户提交？](#select-how-the-final-message-is-sent)

## <a name="select-action-command-invoke-locations"></a>选择操作命令调用位置

首先，必须确定调用操作命令的位置。 通过在应用清单中指定 `context`，可以从以下一个或多个位置调用命令：

* 撰写消息区域：撰写消息区域底部的按钮。

    命令上下文 = compose

* 命令框：通过在命令框中@提及应用。

    命令上下文 = commandBox

   > [!NOTE]
   > 如果从命令框调用消息扩展，则无法使用直接插入到对话中的机器人消息进行响应。

* 消息：通过消息上的 `...` 溢出菜单直接从现有消息进行。

    命令上下文 = message

    > [!NOTE]
    > 对机器人的初始调用包括一个 JSON 对象，其中包含从中调用它的消息。 可以在将消息与任务模块一起呈现之前对其进行处理。

下图显示了调用操作命令的位置：

![操作命令调用位置](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="select-how-to-create-your-task-module"></a>选择如何创建任务模块

除了选择命令调用位置外，还必须选择如何在任务模块中为用户填充表单。 可以使用以下三个选项来创建在任务模块内呈现的表单：

* **参数的静态列表**：这是最简单的方法。 可以在应用清单中定义 Teams 客户端呈现的参数列表，但在这种情况下无法控制格式。
* **自适应卡片**：可以选择使用自适应卡片，它可以更好地控制 UI，但仍会限制可用控件和格式设置选项。
* **嵌入式 Web 视图**：可以选择在任务模块中嵌入自定义 Web 视图，以完全控制 UI 和控件。

如果选择创建具有静态参数列表的任务模块，并且当用户提交任务模块时，将调用消息扩展。 使用嵌入式 Web 视图或自适应卡片时，消息扩展必须处理来自用户的初始调用事件、创建任务模块并将其返回到客户端。

## <a name="select-how-the-final-message-is-sent"></a>选择最终消息的发送方式

大多数情况下，操作命令会导致卡片插入撰写消息框中。 用户可以将其发送到频道或聊天。 在这种情况下，消息来自用户，机器人无法进一步编辑或更新卡片。

如果从撰写框或直接从消息调用消息扩展，则 Web 服务可以直接将最终响应插入频道或聊天中。 在这种情况下，自适应卡片来自机器人，机器人会更新它，并根据需要回复对话线程。 必须使用相同的 ID 将 `bot` 对象添加到应用清单并定义适当的范围。

## <a name="add-the-action-command-to-your-app-manifest"></a>将操作命令添加到应用清单

若要将操作命令添加到应用清单，必须将新的 `composeExtension` 对象添加到应用清单 JSON 的顶层。 可以使用以下方法之一来执行此操作：

* [使用 App Studio 创建操作命令](#create-an-action-command-using-app-studio)
* [手动创建操作命令](#create-an-action-command-manually)

### <a name="create-an-action-command-using-app-studio"></a>使用 App Studio 创建操作命令

可以使用 **App Studio** 或 **开发人员门户** 创建操作命令。

> [!NOTE]
> App Studio 即将弃用。 使用新的[开发人员门户](https://dev.teams.microsoft.com/)配置、分发和管理 Teams 应用。

# <a name="app-studio"></a>[应用程序 Studio](#tab/AS)

> [!NOTE]
> 创建操作命令的先决条件是已创建消息扩展。 有关如何创建消息扩展的信息，请参阅[创建消息扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。

**创建操作命令**

1. 从 Microsoft Teams 客户端打开 **App Studio**，然后选择“**清单编辑器**”选项卡。
1. 如果已在 **App Studio** 中创建应用包，请从列表中选择它。 如果尚未创建应用包，请导入现有包。
1. 导入应用包后，选择“**功能**”下的“**消息扩展**”。 将显示一个弹出窗口来设置消息扩展。
1. 在窗口中选择“**设置**”，以在应用体验中包含消息扩展。 下图显示了消息扩展设置窗口：

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. 若要创建消息扩展，需要 Microsoft 注册的机器人。 可以使用现有机器人，也可以创建新的机器人。 选择“**创建新的机器人**”选项，为新机器人命名，然后选择“**创建**”。 下图显示了如何为消息扩展创建机器人：

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. 在消息扩展页面的 **“命令”部分** 中选择“**添加**”，以包含决定消息扩展行为的命令。
下图显示了如何为消息扩展添加命令：

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>

1. 选择“**允许用户在 Teams 内触发外部服务中的操作**”。 下图显示了操作命令选择：

    <img src="~/assets/images/messaging-extension/action-command-selection.png" alt="action command selection" width="500"/>

1. 若要使用一组静态参数来创建任务模块，请选择“**为命令定义一组静态参数**”。

    下图显示了操作命令静态参数选择：

   <img src="~/assets/images/messaging-extension/action-command-static-parameter-selection.png" alt="action command static parameter selection" width="500"/>

    下图显示了静态参数设置示例：

   <img src="~/assets/images/messaging-extension/setting-up-of-static-parameter.png" alt="action command static parameter set-up" width="500"/>

    下图显示了静态参数测试示例：

   <img src="~/assets/images/messaging-extension/static-parameter-testing.png" alt="action command static parameter testing" width="500"/>

1. 若要使用动态参数，请选择“**从机器人提取一组动态参数**”。 下图显示了操作命令参数选择：

    <img src="~/assets/images/messaging-extension/action-command-dynamic-parameter-selection.png" alt="action command dynamic parameter selection" width="500"/>

1. 添加 **命令 ID** 和 **标题**。
1. 选择要从中调用操作命令的位置。 下图显示了操作命令调用位置：

    <img src="~/assets/images/messaging-extension/action-command-invoke-location.png" alt="action command invoke location" width="500"/>

1. 选择“保存”。
1. 若要添加更多参数，请选择“**参数**”部分中的“**添加**”按钮。

### <a name="create-an-action-command-manually"></a>手动创建操作命令

若要手动将基于操作的消息扩展命令添加到应用清单，必须将以下参数添加到 `composeExtension.commands` 对象数组：

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `id` | 此属性是分配给此命令的唯一 ID。 用户请求包含此 ID。 | 是 | 1.0 |
| `title` | 此属性是命令名称。 此值显示在 UI 中。 | 是 | 1.0 |
| `type` | 此属性必须是 `action`。 | 否 | 1.4 |
| `fetchTask` | 对于任务模块的自适应卡片或嵌入式 Web 视图，此属性设置为 `true`；对于静态参数列表或通过 `taskInfo` 加载 Web 视图时，此属性设置为 `false`。 | 否 | 1.4 |
| `context` | 此属性是一个可选值数组，用于定义从何处调用消息扩展。 可取值包括 `message`、`compose` 或 `commandBox`。 默认值为 `["compose", "commandBox"]`。 | 否 | 1.5 |

如果使用的是静态参数列表，还必须添加以下参数：

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `parameters` | 此属性描述命令的静态参数列表。 仅当 `fetchTask` 为 `false` 时使用。 | 否 | 1.0 |
| `parameter.name` | 此属性描述参数的名称。 这会在用户请求中发送到服务。 | 是 | 1.0 |
| `parameter.description` | 此属性描述参数的用途或应提供的值示例。 此值显示在 UI 中。 | 是 | 1.0 |
| `parameter.title` | 此属性是一个简短的用户友好参数标题或标签。 | 是 | 1.0 |
| `parameter.inputType` | 此属性设置为所需的输入类型。 可能的值包括 `text`、`textarea`、`number`、`date`、`time`、`toggle`。 默认值设置为 `text`。 | 否 | 1.4 |

如果使用的是嵌入式 Web 视图，可以选择添加 `taskInfo` 对象以提取 Web 视图，而无需直接调用机器人。 如果选择此选项，则行为类似于使用静态参数列表。 在此情况下，与机器人的第一次交互是[响应任务模块提交操作](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)。 如果使用的是 `taskInfo` 对象，则必须将 `fetchTask` 参数设置为 `false`。

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
|`taskInfo`|指定使用消息扩展命令时要预加载的任务模块。 | 否 | 1.4 |
|`taskInfo.title`|初始任务模块标题。 |否 | 1.4 |
|`taskInfo.width`|任务模块宽度，以像素为单位的数字或默认布局，如 `large`、`medium` 或 `small`。 |否 | 1.4 |
|`taskInfo.height`|任务模块高度，以像素为单位的数字或默认布局，如 `large`、`medium` 或 `small`。|否 | 1.4 |
|`taskInfo.url`|初始 Web 视图 URL。|否 | 1.4 |

#### <a name="app-manifest-example"></a>应用清单示例

以下部分是定义两个操作命令的 `composeExtensions` 对象示例。 它不是完整的清单示例。 有关完整的应用清单架构，请参阅[应用清单架构](~/resources/schema/manifest-schema.md)：

```json
...
"composeExtensions": [
  {
    "botId": "12a3c29f-1fc5-4d97-a142-12bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "addTodo",
        "description": "Create a To Do item",
        "title": "Create To Do",
        "type": "action",
        "context": ["commandBox", "message", "compose"],
        "fetchTask": true,
        "parameters": [
          {
            "name": "Name",
            "description": "To Do Title",
            "title": "Title",
            "inputType": "text"
          },
          {
            "name": "Description",
            "description": "Description of the task",
            "title": "Description",
            "inputType": "textarea"
          },
          {
            "name": "Date",
            "description": "Due date for the task",
            "title": "Date",
            "inputType": "date"
          }
        ]
      },
      {
        "id": "reassignTodo",
        "description": "Reassign a todo item",
        "title": "Reassign a todo item",
        "type": "action",
        "fetchTask": true,
      }
    ]
  }
]
...
```

## <a name="code-sample"></a>代码示例

| 示例名称           | 说明 | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Teams 消息扩展操作| 介绍如何定义操作命令、创建任务模块和响应任务模块提交操作。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |

## <a name="step-by-step-guide"></a>分步指南

按照[分步指南](../../../sbs-meetingextension-action.yml)生成基于 Teams 操作的消息扩展。

## <a name="next-step"></a>后续步骤

如果在不使用 `taskInfo` 对象的情况下使用自适应卡片或嵌入式 Web 视图，下一步是：

> [!div class="nextstepaction"]
> [使用任务模块创建和响应](~/messaging-extensions/how-to/action-commands/create-task-module.md)

如果将参数或嵌入式 Web 视图与 `taskInfo` 对象配合使用，下一步是：

> [!div class="nextstepaction"]
> [响应任务模块提交](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
