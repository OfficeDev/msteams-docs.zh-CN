---
title: 定义邮件扩展操作命令
author: clearab
description: Microsoft 团队平台上的邮件扩展概述
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 89cf92260418701ef4809f5a13750b991b9f7acb
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279684"
---
# <a name="define-messaging-extension-action-commands"></a>定义邮件扩展操作命令

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

操作命令使您可以向用户显示在团队) 中称为任务模块的模式弹出窗口 (，以收集或显示信息，然后处理他们的交互并将信息发送回团队。 在创建您的命令之前，您需要确定：

1. 从哪里可以触发操作命令？
1. 将如何创建任务模块？
1. 是否将最终邮件或卡片从 bot 发送到频道，或者是否将邮件或智能卡插入到撰写邮件区域中以供用户提交？

## <a name="choose-action-command-invoke-locations"></a>选择操作命令调用位置

您需要确定的第一件事是可以触发操作命令 (或更具体地是) *调用* 。 通过 `context` 在应用程序清单中指定，可以从以下一个或多个位置调用命令：

* "撰写邮件" 区域底部的按钮。
* 通过在命令框中 @mentioning 您的应用程序。 注意：如果您的邮件扩展是从命令框中调用的，则不能使用直接插入到对话中的 bot 消息进行响应。
* 直接从现有邮件，通过 .。。邮件上的溢出菜单。 注意：对你的 bot 的初始调用将包含一个 JSON 对象，其中包含从中调用该对象的邮件，您可以在将其处理到任务模块之前对其进行处理。

## <a name="choose-how-to-build-your-task-module"></a>选择如何生成任务模块

除了可以选择从中调用命令的位置之外，还必须选择如何在任务模块中为您的用户填充窗体。 有三个选项可用于创建在任务模块中呈现的表单：

* **参数的静态列表** -这是最简单的选项。 可以在团队客户端将呈现的应用程序清单中)  (输入字段定义参数列表。 您无法使用此选项控制格式设置。
* **自适应卡片** -您可以选择使用自适应卡片，它可以更好地控制 UI，但仍会限制可用控件和格式选项。
* **嵌入的 web 视图** -如果需要对 UI 和控件进行完全控制，则可以选择在任务模块中嵌入自定义 web 视图。

如果选择使用静态的参数列表创建任务模块，则当用户提交任务模块时，对邮件扩展的第一次调用。 使用嵌入的 web 视图或自适应卡片时，邮件扩展将需要处理用户的初始调用事件，创建任务模块，并将其返回到客户端。

## <a name="choose-how-the-final-message-will-be-sent"></a>选择最终邮件的发送方式

在大多数情况下，您的操作命令将导致卡片插入 "撰写" 消息框中。 然后，你的用户可以决定将其发送到频道或聊天。 在这种情况下，该消息来自用户，并且你的 bot 将无法进一步编辑或更新此卡。

如果您的邮件扩展是通过撰写框或直接从邮件中触发的，则您的 web 服务可以直接在频道或聊天中插入最终响应。 在这种情况下，自适应卡片来自机器人，bot 将能够更新它，并且 bot 也可以在需要时回复到会话线程。 您需要 `bot` 使用相同的 Id 将对象添加到应用程序清单，并定义相应的作用域。

## <a name="add-the-command-to-your-app-manifest"></a>将命令添加到应用程序清单

现在，您已经决定了用户将如何与您的操作命令进行交互，现在是将其添加到应用程序清单中的时候了。 若要执行此操作，请将新 `composeExtension` 对象添加到应用程序清单 JSON 的最高级别。 您可以使用应用程序 Studio 的帮助或手动执行此操作。

### <a name="create-a-command-using-app-studio"></a>使用应用程序 Studio 创建命令

以下步骤假定您已经 [创建了邮件扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。

1. 在 Microsoft 团队客户端中，打开 **应用程序 Studio** 并选择 " **清单编辑器** " 选项卡。
2. 如果您已经在应用程序 Studio 中创建了应用程序包，请从列表中选择它。 如果不是，则可以导入现有的应用程序包。
3. 单击 "命令" 部分的 " **添加** " 按钮。
4. 选择 **"允许用户在团队内部触发外部服务中的操作"**。
5. 如果要使用一组静态参数来创建任务模块，请选择该选项。 否则，请选择 **从你的 bot 中提取一组动态参数**。
6. 添加 **命令 Id** 和 **标题**。
7. 选择要触发操作命令触发的位置。
8. 如果您使用的是任务模块的参数，请添加第一个。
9. 单击"保存"。
10. 如果需要添加更多参数，请单击 "**参数**" 部分中的 "**添加**" 按钮以添加它们。

### <a name="manually-create-a-command"></a>手动创建命令

若要将基于操作的消息扩展命令手动添加到应用程序清单中，需要将以下参数添加到您 `composeExtension.commands` 的对象数组中。

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `id` | 您分配给此命令的唯一 ID。 用户请求将包括此 ID。 | 是 | 1.0 |
| `title` | 命令名称。 此值显示在 UI 中。 | 是 | 1.0 |
| `type` | 必须是 `action` | 否 | 1.4 |
| `fetchTask` | `true` 对于任务模块的自适应卡片或嵌入的 web 视图， `false` 对于参数的静态列表或在加载 web 视图时 `taskInfo` | 否 | 1.4 |
| `context` | 值的可选数组，用于定义可以从中调用邮件扩展的位置。 可能的值为 `message` 、 `compose` 或 `commandBox` 。 默认值为 `["compose", "commandBox"]`。 | 否 | 1.5 |

如果使用的是静态参数列表，则也将添加它们。

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `parameters` | 命令的参数的静态列表。 仅 `fetchTask` 在何时使用 `false` | 否 | 1.0 |
| `parameter.name` | 参数的名称。 此项将发送到用户请求中的服务。 | 是 | 1.0 |
| `parameter.description` | 描述了此参数的用途或应提供的值的示例。 此值显示在 UI 中。 | 是 | 1.0 |
| `parameter.title` | 短用户友好参数标题或标签。 | 是 | 1.0 |
| `parameter.inputType` | 设置为所需的输入类型。 可能的值包括 `text` 、、、、 `textarea` `number` `date` `time` 、 `toggle` 。 默认值设置为 `text` | 否 | 1.4 |

如果使用的是嵌入的 web 视图，则可以选择添加 `taskInfo` 对象以获取您的 web 视图，而无需直接调用你的 bot。 如果选择使用此选项，则行为类似于在中使用静态参数列表，因为与你的 bot 的第一次交互将 [响应任务模块提交操作](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)。 如果使用的是 `taskInfo` 对象，请确保同时将 `fetchTask` 参数设置为 `false` 。

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
|`taskInfo`|指定在使用消息扩展命令时要预加载的任务模块| 否 | 1.4 |
|`taskInfo.title`|初始任务模块标题|否 | 1.4 |
|`taskInfo.width`|任务模块宽度-以像素为单位的数字或默认布局，如 "大"、"中" 或 "small"|否 | 1.4 |
|`taskInfo.height`|任务模块高度-以像素为单位的数字或默认布局，如 "大"、"中" 或 "small"|否 | 1.4 |
|`taskInfo.url`|初始 web 视图 URL|否 | 1.4 |

#### <a name="app-manifest-example"></a>应用部件清单示例

下面是 `composeExtensions` 定义两个动作命令的对象的一个示例。 这不是完整清单的完整清单示例，请参阅： [应用程序清单架构](~/resources/schema/manifest-schema.md)。

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
        "fetchTask": false,
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

如果您使用的是自适应卡片或不带对象的嵌入式 web 视图 `taskInfo` ，则需要执行以下操作：

* [使用任务模块创建和响应](~/messaging-extensions/how-to/action-commands/create-task-module.md)

如果使用的是带对象的参数或嵌入的 web 视图 `taskInfo` ，则下一步是：

* [响应任务模块提交](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
