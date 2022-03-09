---
title: 定义消息传递扩展操作命令
author: surbhigupta
description: 包含应用清单示例的邮件扩展操作命令概述
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 938e37fac8cd27257e378fa1177916462b331023
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2022
ms.locfileid: "63399266"
---
# <a name="define-messaging-extension-action-commands"></a>定义消息传递扩展操作命令

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

操作命令允许你向用户显示名为任务模块的模式弹出框Teams。 任务模块收集或显示信息、处理交互并将信息发送回Teams。 本文档指导您如何选择操作命令调用位置、创建任务模块、发送最终消息或卡片、使用 app studio 创建操作命令或手动创建它。

在创建操作命令之前，必须确定以下因素：

1. [可以从何处触发操作命令？](#select-action-command-invoke-locations)
1. [如何创建任务模块？](#select-how-to-create-your-task-module)
1. [最终的邮件或卡片是从自动程序发送到频道，还是将邮件或卡片插入撰写邮件区域供用户提交？](#select-how-the-final-message-is-sent)

## <a name="select-action-command-invoke-locations"></a>选择操作命令调用位置

首先，必须决定必须调用操作命令的位置。 通过指定 `context` 应用清单中的 ，可以从以下一个或多个位置调用命令：

* 撰写邮件区域：撰写邮件区域底部的按钮。

    命令上下文 = 撰写

* 命令框：@mentioning命令框中显示你的应用。

    命令上下文 = commandBox

   > [!NOTE]
   > 如果从命令框调用消息传递扩展，则不能使用直接插入对话的自动程序消息进行响应。

* 消息：直接通过邮件上的溢出 `...` 菜单从现有邮件发送。

    命令上下文 = 消息

    > [!NOTE]
    > 对自动程序的初始调用包括一个 JSON 对象，其中包含从其中调用它的消息。 可以在向邮件显示任务模块之前处理邮件。

下图显示了调用 action 命令的位置：

![操作命令调用位置](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="select-how-to-create-your-task-module"></a>选择如何创建任务模块

除了选择命令的调用位置之外，还必须选择如何为用户填充任务模块中的窗体。 有以下三个选项用于创建在任务模块内呈现的窗体：

* **参数的静态列表**：这是最简单的方法。 可以在客户端呈现的应用清单中定义Teams列表，但在这种情况下无法控制格式。
* **自适应卡片**：可以选择使用自适应卡片，该卡片可以更好地控制 UI，但仍限制可用控件和格式设置选项。
* **嵌入式 Web** 视图：可以选择在任务模块中嵌入自定义 Web 视图，以便完全控制 UI 和控件。

如果您选择创建包含参数静态列表的任务模块，并且当用户提交任务模块时，将调用消息扩展。 使用嵌入式 Web 视图或自适应卡片时，邮件扩展必须处理来自用户的初始调用事件、创建任务模块，并返回到客户端。

## <a name="select-how-the-final-message-is-sent"></a>选择最终邮件的发送

在大多数情况下，操作命令会导致在撰写消息框中插入一个卡片。 用户可以将其发送到频道或聊天。 在这种情况下，邮件来自用户，机器人无法进一步编辑或更新卡片。

如果消息扩展从撰写框或直接通过消息调用，则 Web 服务可以直接将最终响应插入频道或聊天中。 在这种情况下，自适应卡片来自机器人，机器人会更新它，并根据需要回复到对话线程。 你必须使用相同的 `bot` ID 并定义适当的作用域将对象添加到应用清单。

## <a name="add-the-action-command-to-your-app-manifest"></a>将操作命令添加到应用清单

若要将操作命令添加到应用清单 `composeExtension` ，必须将新对象添加到应用清单 JSON 的顶层。 为此，可以使用下列方法之一：

* [使用 App Studio 创建操作命令](#create-an-action-command-using-app-studio)
* [手动创建操作命令](#create-an-action-command-manually)

### <a name="create-an-action-command-using-app-studio"></a>使用 App Studio 创建操作命令

可以使用 App **Studio 或开发人员** 门户创建 **操作命令**。

> [!NOTE]
> App Studio 即将被弃用。 使用新的开发人员门户配置Teams、分发和管理[应用](https://dev.teams.microsoft.com/)。

# <a name="app-studio"></a>[应用程序 Studio](#tab/AS)

> [!NOTE]
> 创建操作命令的先决条件是，已创建邮件扩展。 若要了解如何创建邮件扩展，请参阅 [创建邮件扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。

**创建操作命令**

1. 从 **客户端打开 App Studio** Microsoft Teams选择"**清单编辑器"** 选项卡。
1. 如果你已在 **App Studio** 中创建应用包，请从列表中选择它。 如果尚未创建应用包，请导入现有应用包。
1. 导入应用包后，选择" **功能"下的** "消息 **扩展"**。 你获得一个弹出窗口来设置邮件扩展。
1. 选择 **窗口中** 的"设置"，将消息传递扩展包括在你的应用体验中。 下图显示了消息扩展设置窗口：

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. 若要创建消息扩展，你需要一个 Microsoft 注册的自动程序。 可以使用现有自动程序或创建新的自动程序。 选择 **"创建新自动程序** "选项，为新的自动程序命名，然后选择"创建 **"**。 下图显示了邮件扩展的自动程序创建：

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. **选择"** 邮件扩展 **"** 页的"命令"部分中的"添加"，以包含决定邮件扩展行为的命令。
下图显示了邮件扩展的命令添加：

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>

1. 选择 **"允许用户在外部服务内触发Teams"**。 下图显示了操作命令选择：

    <img src="~/assets/images/messaging-extension/action-command-selection.png" alt="action command selection" width="500"/>

1. 若要使用一组静态参数来创建任务模块，请选择"为命令定义一组 **静态参数"**。

    下图显示了操作命令静态参数选择：

   <img src="~/assets/images/messaging-extension/action-command-static-parameter-selection.png" alt="action command static parameter selection" width="500"/>

    下图显示了一个静态参数设置示例：

   <img src="~/assets/images/messaging-extension/setting-up-of-static-parameter.png" alt="action command static parameter set-up" width="500"/>

    下图显示了静态参数测试示例：

   <img src="~/assets/images/messaging-extension/static-parameter-testing.png" alt="action command static parameter testing" width="500"/>

1. 若要使用动态参数，请选择" **从自动程序提取动态参数集"**。 下图显示了操作命令参数选择：

    <img src="~/assets/images/messaging-extension/action-command-dynamic-parameter-selection.png" alt="action command dynamic parameter selection" width="500"/>

1. 添加命令 **ID** 和 **标题**。
1. 选择要调用操作命令的位置。 下图显示了操作命令调用位置：

    <img src="~/assets/images/messaging-extension/action-command-invoke-location.png" alt="action command invoke location" width="500"/>

1. 选择“保存”。
1. 若要添加更多参数，请选择" **参数"部分** 中的" **添加"** 按钮。

### <a name="create-an-action-command-manually"></a>手动创建操作命令

若要手动将基于操作的消息扩展命令添加到应用 `composeExtension.commands` 清单，必须将以下参数添加到对象数组：

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `id` | 此属性是分配给此命令的唯一 ID。 用户请求包括此 ID。 | 是 | 1.0 |
| `title` | 此属性是命令名称。 此值显示在 UI 中。 | 是 | 1.0 |
| `type` | 此属性必须为 `action`。 | 否 | 1.4 |
| `fetchTask` | 对于任务模块 `true` 的自适应卡片或嵌入式 Web`false` 视图，以及参数的静态列表或加载 Web 视图时，此属性设置为 `taskInfo`。 | 否 | 1.4 |
| `context` | 此属性是一个可选的值数组，用于定义从何处调用消息传递扩展。 可取值包括 `message`、`compose` 或 `commandBox`。 默认值为 `["compose", "commandBox"]`。 | 否 | 1.5 |

如果使用参数的静态列表，则还必须添加以下参数：

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `parameters` | 此属性描述命令的参数静态列表。 仅在 为 时 `fetchTask` 使用 `false`。 | 否 | 1.0 |
| `parameter.name` | 此属性描述参数的名称。 这将在用户请求中发送到你的服务。 | 是 | 1.0 |
| `parameter.description` | 此属性描述参数的用途或应提供的值示例。 此值显示在 UI 中。 | 是 | 1.0 |
| `parameter.title` | 此属性是一个简短的用户友好参数标题或标签。 | 是 | 1.0 |
| `parameter.inputType` | 此属性设置为所需的输入类型。 可能的值包括 、`textarea`、`text`、`number``date`、`time`、。 `toggle` 默认值设置为 `text`。 | 否 | 1.4 |

如果你使用的是嵌入式 Web 视图 `taskInfo` ，可以选择添加 对象来获取 Web 视图，而无需直接调用机器人。 如果选择此选项，则其行为类似于使用静态参数列表的行为。 因此，与机器人的第一次 [交互是响应任务模块提交操作](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)。 如果使用对象， `taskInfo` 则必须将 参数 `fetchTask` 设置为 `false`。

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
|`taskInfo`|指定在使用消息传递扩展命令时要预加载的任务模块。 | 否 | 1.4 |
|`taskInfo.title`|初始任务模块标题。 |否 | 1.4 |
|`taskInfo.width`|任务模块宽度，以像素为单位的一个数字或默认布局（如 `large``medium`、 或 `small`）。 |否 | 1.4 |
|`taskInfo.height`|任务模块高度，以像素为单位或 `large`默认布局（如 、 `medium`或 `small`）。|否 | 1.4 |
|`taskInfo.url`|初始 Web 视图 URL。|否 | 1.4 |

#### <a name="app-manifest-example"></a>应用清单示例

下一节是定义两个操作 `composeExtensions` 命令的对象的示例。 这不是完整清单的示例。 有关完整的应用清单架构，请参阅 [应用清单架构](~/resources/schema/manifest-schema.md)：

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
|Teams邮件扩展操作| 介绍如何定义操作命令、创建任务模块和响应任务模块提交操作。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |

## <a name="step-by-step-guide"></a>分步指南

按照[分步指南构建](../../../sbs-meetingextension-action.yml)基于Teams操作的邮件扩展。

## <a name="next-step"></a>后续步骤

如果你使用的是自适应卡片或没有对象的嵌入 Web `taskInfo` 视图，下一步是：

> [!div class="nextstepaction"]
> [使用任务模块创建和响应](~/messaging-extensions/how-to/action-commands/create-task-module.md)

如果要将参数或嵌入的 Web 视图 `taskInfo` 与对象一同使用，下一步是：

> [!div class="nextstepaction"]
> [响应任务模块提交](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
