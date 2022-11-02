---
title: 定义消息扩展操作命令
author: surbhigupta
description: 了解如何在 Microsoft Teams 中使用应用清单示例定义消息传递扩展操作命令。 示例 (.NET，Node.js) 如何定义操作命令、创建任务模块和响应任务模块提交操作。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: b4d40e3a3ba4f684a0b34fcebab21f988d79de87
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820092"
---
# <a name="define-message-extension-action-commands"></a>定义消息扩展操作命令

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> 启动邮件操作时，附件详细信息不会作为调用活动的 `turncontext` 一部分发送。

使用操作命令，可以在 Teams 中向用户显示称为任务模块的模式弹出窗口。 任务模块收集或显示信息、处理交互并将信息发送回 Teams。 本文档指导你如何选择操作命令调用位置、创建任务模块、发送最终消息或卡片、使用 App Studio 创建操作命令或手动创建操作命令。

在创建操作命令之前，必须确定以下因素：

1. [可以从何处触发操作命令？](#select-action-command-invoke-locations)
1. [如何创建任务模块？](#select-how-to-create-your-task-module)
1. [最终消息或卡片是从机器人发送到频道，还是将消息或卡片插入撰写消息区域供用户提交？](#select-how-the-final-message-is-sent)

请参阅以下视频，了解如何定义消息扩展操作命令：
<br>

> [!VIDEO <https://www.microsoft.com/en-us/videoplayer/embed/RE4OANG>]
<br>

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

:::image type="content" source="~/assets/images/messaging-extension-invoke-locations.png" alt-text="操作命令调用位置":::

## <a name="select-how-to-create-your-task-module"></a>选择如何创建任务模块

除了选择命令调用位置外，还必须选择如何在任务模块中为用户填充表单。 可以使用以下三个选项来创建在任务模块内呈现的表单：

* **参数的静态列表**：这是最简单的方法。 可以在 Teams 客户端呈现的应用清单中定义参数列表，但在这种情况下无法控制格式设置。
* **自适应卡片**：可以选择使用自适应卡片，它可以更好地控制 UI，但仍会限制可用控件和格式设置选项。
* **嵌入式 Web 视图**：可以选择在任务模块中嵌入自定义 Web 视图，以完全控制 UI 和控件。

如果选择创建具有静态参数列表的任务模块，并且当用户提交任务模块时，将调用消息扩展。 使用嵌入式 Web 视图或自适应卡片时，消息扩展必须处理来自用户的初始调用事件、创建任务模块并将其返回到客户端。

## <a name="select-how-the-final-message-is-sent"></a>选择最终消息的发送方式

大多数情况下，操作命令会导致卡片插入撰写消息框中。 用户可以将其发送到频道或聊天。 在这种情况下，消息来自用户，机器人无法进一步编辑或更新卡片。

如果从撰写框或直接从消息调用消息扩展，则 Web 服务可以直接将最终响应插入频道或聊天中。 在这种情况下，自适应卡片来自机器人，机器人会更新它，并根据需要回复对话线程。 必须使用相同的 ID 将 `bot` 对象添加到应用清单并定义适当的范围。

## <a name="add-the-action-command-to-your-app-manifest"></a>将操作命令添加到应用清单

To add the action command to the app manifest, you must add a new `composeExtension` object to the top level of the app manifest JSON. You can use one of the following ways to do so:

* [使用开发人员门户创建操作命令](#create-an-action-command-using-developer-portal)
* [手动创建操作命令](#create-an-action-command-manually)

### <a name="create-an-action-command-using-developer-portal"></a>使用开发人员门户创建操作命令

可以使用 **开发人员门户** 创建操作命令。

> [!NOTE]
> 创建操作命令的先决条件是已创建消息扩展。 有关如何创建消息扩展的信息，请参阅[创建消息扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。

若要创建操作命令，请执行以下操作：

1. 从 Microsoft Teams 客户端打开 **开发人员门户** ，然后选择“ **应用** ”选项卡。如果已在 **开发人员门户中** 创建了应用包，请从列表中选择。 如果尚未创建应用包，请导入现有应用包。
1. 导入应用包后，选择“**应用功能**”下的“**消息扩展**”。
1. 若要创建消息扩展，需要 Microsoft 注册的机器人。 可以使用现有机器人，也可以创建新的机器人。 选择“ **创建新机器人** ”选项，为新机器人命名，然后选择“ **创建**”。

   :::image type="content" source="../../../assets/images/tdp/bot-page.png" alt-text="屏幕截图显示如何在开发人员门户中创建机器人。":::

1. 若要使用现有机器人，请选择“ **选择现有机器人** ”，并从下拉列表中选择现有机器人，或者选择“ **输入机器人 ID** ”（如果已创建机器人 ID）。

1. 选择机器人的范围并 **保存**。

1. 在 **“命令** ”部分选择“添加 **命令** ”，以包含决定消息扩展行为的命令。

   :::image type="content" source="../../../assets/images/tdp/add-a-command.PNG" alt-text="屏幕截图显示如何添加命令来定义消息扩展的行为。":::

1. 选择“ **操作** ”，然后选择“参数类型”。

1. 输入 **“命令 ID****”、“命令标题**”和 **“命令说明**”。

1. 输入所有参数，并从下拉列表中选择输入类型。

   :::image type="content" source="../../../assets/images/tdp/add-a-command-parameter.PNG" alt-text="屏幕截图显示如何添加参数来定义消息扩展命令。":::

1. 选择 **“预览链接**”下的“**添加域**”。

1. 输入有效域，然后选择“ **添加**”。

   :::image type="content" source="../../../assets/images/tdp/add-domain.PNG" alt-text="屏幕截图显示如何将有效的域添加到链接展开的消息扩展。":::

1. 选择“**保存**”。

   :::image type="content" source="../../../assets/images/tdp/add-a-command-save.PNG" alt-text="屏幕截图显示如何保存消息扩展的所有设置和参数。":::

**添加其他参数**

1. 在“命令”部分下选择“省略号”，然后选择“ **编辑参数**”。

   :::image type="content" source="../../../assets/images/tdp/edit-parameters.PNG" alt-text="屏幕截图显示如何为消息扩展添加其他参数。":::

1. 选择“ **添加参数”** 并输入所有参数。

   :::image type="content" source="../../../assets/images/tdp/add-parameter.PNG" alt-text="屏幕截图显示如何为消息扩展添加其他参数。"lightbox="../../../assets/images/tdp/add-a-parameters.PNG":::

### <a name="create-an-action-command-manually"></a>手动创建操作命令

若要手动将基于操作的消息扩展命令添加到应用清单，必须将以下参数添加到 `composeExtension.commands` 对象数组：

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `id` | 此属性是分配给此命令的唯一 ID。 用户请求包含此 ID。 | 是 | 1.0 |
| `title` | 此属性是命令名称。 此值显示在 UI 中。 | 是 | 1.0 |
| `type` | 此属性必须是 `action`。 | 否 | 1.4 |
| `fetchTask` | 对于任务模块的自适应卡片或嵌入式 Web 视图，此属性设置为 `true`；对于静态参数列表或通过 `taskInfo` 加载 Web 视图时，此属性设置为 `false`。 | 否 | 1.4 |
| `context` | 此属性是一个可选值数组，用于定义从何处调用消息扩展。 可取值包括 `message`、`compose` 或 `commandBox`。 默认值为 `["compose", "commandBox"]`。 | 否 | 1.5 |

如果使用参数的静态列表，还必须添加以下参数：

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `parameters` | This property describes the static list of parameters for the command. Only use when `fetchTask` is `false`. | 否 | 1.0 |
| `parameter.name` | 此属性描述参数的名称。 这会在用户请求中发送到服务。 | 是 | 1.0 |
| `parameter.description` | This property describes the parameter’s purposes or example of the value that should be provided. This value appears in the UI. | 是 | 1.0 |
| `parameter.title` | 此属性是一个简短的用户友好参数标题或标签。 | 是 | 1.0 |
| `parameter.inputType` | 此属性设置为所需的输入类型。 可能的值包括 `text`、`textarea`、`number`、`date`、`time`、`toggle`。 默认值设置为 `text`。 | 否 | 1.4 |

如果使用嵌入式 Web 视图，可以选择添加 `taskInfo` 对象来提取 Web 视图，而无需直接调用机器人。 如果选择此选项，则行为类似于使用静态参数列表。 在此情况下，与机器人的第一次交互是[响应任务模块提交操作](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)。 如果使用 `taskInfo` 对象，则必须将 `fetchTask` 参数设置为 `false`。

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
|`taskInfo`|指定使用消息扩展命令时要预加载的任务模块。 | 否 | 1.4 |
|`taskInfo.title`|初始任务模块标题。 |否 | 1.4 |
|`taskInfo.width`|任务模块宽度，以像素为单位的数字或默认布局，如 `large`、`medium` 或 `small`。 |否 | 1.4 |
|`taskInfo.height`|任务模块高度，以像素为单位的数字或默认布局，如 `large`、`medium` 或 `small`。|否 | 1.4 |
|`taskInfo.url`|初始 Web 视图 URL。|否 | 1.4 |

#### <a name="app-manifest-example"></a>应用清单示例

本部分不是完整清单的示例。 有关完整的应用清单架构，请参阅 [应用清单架构](~/resources/schema/manifest-schema.md)。 下面是定义两个 `composeExtensions` 操作命令的对象的示例：

```json
...
"composeExtensions": [
  {
    "botId": "c8fa3cf6-b1f0-4ba8-a5bf-a241bc29adf3",
    "commands": [
      {
        "id": "To do",
        "type": "action",
        "title": "Create To do",
        "description": "Create a To do",
        "initialRun": true,
        "fetchTask": false,
        "context": [
          "commandBox",
          "compose"
        ],
        "parameters": [
          {
            "name": "Name",
            "title": "Title",
            "description": "To do Title",
            "inputType": "text"
          },
          {
            "name": "Description",
            "title": "Description",
            "description": "Description of the task",
            "inputType": "textarea"
          },
          {
            "name": "Date",
            "title": "Date",
            "description": "Due date for the task",
            "inputType": "date"
          }
        ]
      }
    ],
    "canUpdateConfiguration": true,
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "yourapp.onmicrosoft.com"
          ]
        }
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

如果使用自适应卡片或没有 `taskInfo` 对象的嵌入式 Web 视图，则下一步是：

> [!div class="nextstepaction"]
> [使用任务模块创建和响应](~/messaging-extensions/how-to/action-commands/create-task-module.md)

如果将参数或嵌入的 Web 视图与 对象一 `taskInfo` 起使用，下一步是：

> [!div class="nextstepaction"]
> [响应任务模块提交](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

## <a name="see-also"></a>另请参阅

* [卡片](../../../task-modules-and-cards/what-are-cards.md)
* [任务模块](../../../task-modules-and-cards/what-are-task-modules.md)
* [Teams 的应用清单架构](../../../resources/schema/manifest-schema.md)
* [Teams 开发人员门户](../../../concepts/build-and-test/teams-developer-portal.md)
* [消息扩展](../../what-are-messaging-extensions.md)
