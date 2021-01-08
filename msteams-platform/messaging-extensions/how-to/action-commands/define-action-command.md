---
title: 定义邮件扩展操作命令
author: clearab
description: 邮件扩展操作命令概述
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: be2135477c4234187f374aef215f90e8329fb74e
ms.sourcegitcommit: 5739245903278d521ec920427248b6b48676e637
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/07/2021
ms.locfileid: "49778399"
---
# <a name="define-messaging-extension-action-commands"></a>定义邮件扩展操作命令

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

使用操作命令 (，你可以向用户显示名为 Teams) 中任务模块的模式弹出窗口，以收集或显示信息，然后处理他们的交互并将信息发送回 Teams。 在创建命令之前，你需要决定：

1. 可以从何处触发操作命令？
1. 如何创建任务模块？
1. 最终的邮件或卡片是从自动程序发送到频道，还是将邮件或卡片插入撰写邮件区域供用户提交？

## <a name="choose-action-command-invoke-locations"></a>选择操作命令调用位置

首先需要确定操作命令的触发位置，具体 (调用命令) 位置。  通过指定 `context` 应用清单中的命令，可以从以下一个或多个位置调用命令：

* 撰写邮件区域底部的按钮。
* By @mentioning your app in the command box. 注意：如果从命令框调用消息扩展，则不能使用直接插入到对话中的自动程序消息进行响应。
* 直接通过 ... 从现有邮件发送...消息上的溢出菜单。 注意：对自动程序的初始调用将包括一个 JSON 对象，该对象包含从其中调用它的消息，你可以先处理该对象，然后再向它们显示任务模块。

## <a name="choose-how-to-build-your-task-module"></a>选择如何生成任务模块

除了选择命令的调用位置之外，还必须选择如何在任务模块中为用户填充表单。 有三个选项用于创建在任务模块内呈现的表单：

* **参数的静态列表** - 这是最简单的选项。 可以在 Teams 客户端将 (的应用清单) 输入字段定义参数列表。 不能使用此选项控制格式。
* **自适应卡片** - 你可以选择使用自适应卡片，它可更好地控制 UI，但仍限制你使用可用的控件和格式设置选项。
* **嵌入式 Web 视图** - 如果需要完全控制 UI 和控件，可以选择在任务模块中嵌入自定义 Web 视图。

如果选择使用静态参数列表创建任务模块，则当用户提交任务模块时，将首次调用邮件扩展。 使用嵌入式 Web 视图或自适应卡片时，邮件扩展将需要处理来自用户的初始调用事件、创建任务模块，然后返回给客户端。

## <a name="choose-how-the-final-message-will-be-sent"></a>选择最终邮件的发送

在大多数情况下，您的操作命令将导致在撰写邮件框中插入卡片。 然后，你的用户可以决定将其发送到频道或聊天。 在这种情况下，消息来自用户，你的自动程序将无法进一步编辑或更新卡片。

如果消息扩展从撰写框或直接从消息中触发，则 Web 服务可以直接将最终响应插入频道或聊天中。 在这种情况下，自适应卡片来自自动程序，自动程序将能够更新它，并且机器人还可以根据需要回复对话线程。 你将需要使用相同的 ID 和定义适当的范围将对象添加到 `bot` 应用清单。

## <a name="add-the-command-to-your-app-manifest"></a>将命令添加到应用清单

现在，你已决定用户如何与操作命令交互，是时候将其添加到应用清单了。 为此，你需要将新对象添加到应用清单 `composeExtension` JSON 的顶层。 可以在 App Studio 的帮助下完成操作，也可以手动完成。

### <a name="create-a-command-using-app-studio"></a>使用 App Studio 创建命令

以下步骤假定你已 [创建邮件扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。

1. 从 Microsoft Teams 客户端中，打开 **App Studio** 并选择清单 **编辑器** 选项卡。
2. 如果你已在 App Studio 中创建应用包，请从列表中选择它。 如果没有，你可以导入现有应用包。
3. 单击 **"命令** "部分中的"添加"按钮。
4. 选择 **"允许用户在 Teams 内触发外部服务中的操作"。**
5. 如果要使用一组静态参数来创建任务模块，请选择该选项。 否则，请选择 **从自动程序获取一组动态参数**。
6. 添加命令 **ID** 和 **标题**。
7. 选择要从何处触发操作命令。
8. 如果对任务模块使用参数，请添加第一个参数。
9. 单击"保存"。
10. 如果需要添加更多参数，请单击"参数"部分中的"添加"按钮以添加它们。

### <a name="manually-create-a-command"></a>手动创建命令

若要将基于操作的消息扩展命令手动添加到应用清单，你需要将以下参数添加到对象 `composeExtension.commands` 数组。

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `id` | 分配给此命令的唯一 ID。 用户请求将包含此 ID。 | 是 | 1.0 |
| `title` | 命令名称。 此值显示在 UI 中。 | 是 | 1.0 |
| `type` | 必须是 `action` | 否 | 1.4 |
| `fetchTask` | `true`对于任务模块的自适应卡片或嵌入式 Web 视图，对于静态参数列表，或者当通过 `false``taskInfo` | 否 | 1.4 |
| `context` | 用于定义可以从何处调用邮件扩展的值的可选数组。 可能的值是 `message` ， `compose` 或 `commandBox` 。 默认值为 `["compose", "commandBox"]`。 | 否 | 1.5 |

如果使用静态参数列表，则也会添加它们。

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `parameters` | 命令的参数静态列表。 仅在为时 `fetchTask` 使用 `false` | 否 | 1.0 |
| `parameter.name` | 参数的名称。 这将在用户请求中发送到你的服务。 | 是 | 1.0 |
| `parameter.description` | 描述此参数的目的或应提供的值示例。 此值显示在 UI 中。 | 是 | 1.0 |
| `parameter.title` | 简短的用户友好参数标题或标签。 | 是 | 1.0 |
| `parameter.inputType` | 设置为所需的输入类型。 可能的值包括 `text` `textarea` ， ， `number` `date` `time` `toggle` 。 默认值设置为 `text` | 否 | 1.4 |

如果使用的是嵌入式 Web 视图，可以选择添加对象以提取 Web 视图，而无需 `taskInfo` 直接调用机器人。 如果选择使用此选项，则此行为类似于使用静态参数列表，这是因为与机器人的第一次交互将响应任务 [模块提交操作](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)。 如果使用的是对象 `taskInfo` ，请确保还要将参数 `fetchTask` 设置为 `false` 。

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
|`taskInfo`|指定使用消息传递扩展命令时要预加载的任务模块| 否 | 1.4 |
|`taskInfo.title`|初始任务模块标题|否 | 1.4 |
|`taskInfo.width`|任务模块宽度 - 一个数字（以像素为单位）或默认布局，如"large"、"medium"或"small"|否 | 1.4 |
|`taskInfo.height`|任务模块高度 - 一个数字（以像素为单位）或默认布局，如"large"、"medium"或"small"|否 | 1.4 |
|`taskInfo.url`|初始 Web 视图 URL|否 | 1.4 |

#### <a name="app-manifest-example"></a>应用清单示例

下面是定义两个操作 `composeExtensions` 命令的对象示例。 这不是完整清单的示例，有关完整应用清单架构，请参阅： [应用清单架构](~/resources/schema/manifest-schema.md)。

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

## <a name="next-steps"></a>后续步骤

如果你使用的是自适应卡片或没有对象的嵌入 Web 视图， `taskInfo` 你将希望：

* [使用任务模块创建和响应](~/messaging-extensions/how-to/action-commands/create-task-module.md)

如果将参数或嵌入的 Web 视图与对象一同使用，下一步是 `taskInfo` ：

* [响应任务模块提交](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
