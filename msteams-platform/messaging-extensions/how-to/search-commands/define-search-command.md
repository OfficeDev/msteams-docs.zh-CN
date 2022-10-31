---
title: 定义邮件扩展搜索命令
author: surbhigupta
description: 了解 Teams 应用的消息扩展搜索命令，通过应用清单和手动创建搜索命令。
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: c126d6436c5fb091804c92caeb2876c09392bd9b
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791830"
---
# <a name="define-message-extension-search-commands"></a>定义邮件扩展搜索命令

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

消息扩展搜索命令允许用户搜索外部系统，并将该搜索结果以卡片的形式插入邮件中。 本文档指导你如何选择搜索命令调用位置，以及如何将搜索命令添加到应用清单。

> [!NOTE]
> 结果卡大小限制为 28 KB。 如果卡的大小超过 28 KB，则不会发送该卡。

请参阅以下视频，了解如何定义消息扩展搜索命令：
<br>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4OIvK]
<br>

## <a name="select-search-command-invoke-locations"></a>选择搜索命令调用位置

从以下任一位置或两个位置调用搜索命令：

* 撰写消息区域：撰写消息区域底部的按钮。
* 命令框：在命令框中@mentioning。

从撰写消息区域调用搜索命令时，用户会将结果发送到对话。 从命令框中调用该卡时，用户与生成的卡片交互，或将其复制到其他位置。

下图显示了搜索命令的调用位置：

:::image type="content" source="~/assets/images/messaging-extension/search-command-invoke-locations.png" alt-text="屏幕截图显示了 Teams 频道中搜索命令的调用位置。":::

## <a name="add-the-search-command-to-your-app-manifest"></a>将搜索命令添加到应用清单

若要将搜索命令添加到应用清单，必须将新 `composeExtension` 对象添加到应用清单 JSON 的顶层。 可以通过开发人员门户或手动添加搜索命令。

### <a name="create-a-search-command-using-developer-portal"></a>使用开发人员门户创建搜索命令

创建搜索命令的先决条件是必须已创建消息扩展。 有关如何创建消息扩展的信息，请参阅[创建消息扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。

**创建操作命令**

1. 从 Microsoft Teams 客户端打开 **开发人员门户** ，然后选择“ **应用** ”选项卡。如果已在 **开发人员门户中** 创建了应用包，请从列表中选择。 如果尚未创建应用包，请导入现有应用包。
1. 导入应用包后，选择“**应用功能**”下的“**消息扩展**”。
1. 若要创建消息扩展，需要 Microsoft 注册的机器人。 可以使用现有机器人，也可以创建新的机器人。 选择“ **创建新机器人** ”选项，为新机器人命名，然后选择“ **创建**”。

   :::image type="content" source="../../../assets/images/tdp/bot-page.png" alt-text="屏幕截图显示用于在 Teams 开发人员门户中为应用配置机器人的选项。":::

1. 若要使用现有机器人，请选择“ **选择现有机器人** ”，然后从下拉列表中选择现有机器人，或者选择“ **输入机器人 ID** ”（如果已创建机器人 ID）。

1. 选择消息传递扩展的范围，然后选择“ **保存**”。

1. 在“**命令**”部分选择“**添加命令**”，以包括决定消息扩展行为的命令。
下图显示了如何为消息扩展添加命令：

   :::image type="content" source="../../../assets/images/tdp/add-a-command.PNG" alt-text="屏幕截图显示如何在 Teams 开发人员门户中添加命令以定义消息扩展的行为。":::

1. 选择“**搜索**”，然后输入 **“命令 ID****”、“命令标题****”和“命令说明**”。

1. 输入所有参数，并从下拉列表中选择输入类型。

   :::image type="content" source="../../../assets/images/tdp/add-a-command-parameter.PNG" alt-text="屏幕截图显示如何添加参数以在 Teams 开发人员门户中为消息扩展定义命令。":::

1. 选择 **“预览链接**”下的“**添加域**”。

1. 输入有效域，然后选择“ **添加**”。

   :::image type="content" source="../../../assets/images/tdp/add-domain.PNG" alt-text="屏幕截图显示如何将有效的域添加到消息扩展以展开链接。":::

1. 选择“**保存**”。

   :::image type="content" source="../../../assets/images/tdp/add-a-command-save.PNG" alt-text="屏幕截图显示如何保存消息扩展的所有设置和参数。":::

**添加其他参数**

1. 在“命令”部分下选择“省略号”，然后选择“ **编辑参数**”。

   :::image type="content" source="../../../assets/images/tdp/edit-parameters.PNG" alt-text="屏幕截图显示如何编辑消息扩展的参数。":::

1. 选择“ **添加参数”** 并输入所有参数。

   :::image type="content" source="../../../assets/images/tdp/add-parameter.PNG" alt-text="屏幕截图显示如何为消息扩展添加其他参数。"lightbox="../../../assets/images/tdp/add-a-parameters.PNG":::

### <a name="create-a-search-command-manually"></a>手动创建搜索命令

若要将消息扩展搜索命令手动添加到应用清单，必须将以下参数添加到 `composeExtension.commands` 对象数组：

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `id` | 此属性是分配给搜索命令的唯一 ID。 用户请求包含此 ID。 | 是 | 1.0 |
| `title` | 此属性是命令名称。 此值显示在用户界面 (UI) 中。 | 是 | 1.0 |
| `description` | 此属性是一个帮助文本，指示此命令的作用。 此值显示在 UI 中。 | 是 | 1.0 |
| `type` | 此属性必须是 `query`。 | 否 | 1.4 |
|`initialRun` | 如果此属性设置为 **true**，则表示应在用户在 UI 中选择此命令后立即执行此命令。 | 否 | 1.0 |
| `context` | 此属性是一个可选的值数组，用于定义搜索操作可用的上下文。 可取值包括 `message`、`compose` 或 `commandBox`。 默认值为 `["compose", "commandBox"]`。 | 否 | 1.5 |

必须添加搜索参数的详细信息，该参数定义在 Teams 客户端中对用户可见的文本。

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `parameters` | 此属性定义命令的参数的静态列表。 | 否 | 1.0 |
| `parameter.name` | 此属性描述参数的名称。 在 `parameter.name` 用户请求中将 发送到服务。 | 是 | 1.0 |
| `parameter.description` | 此属性描述参数的用途或必须提供的值的示例。 此值显示在 UI 中。 | 是 | 1.0 |
| `parameter.title` | 此属性是一个简短的用户友好参数标题或标签。 | 是 | 1.0 |
| `parameter.inputType` | 此属性设置为所需的输入类型。 可能的值包括 `text`、、`textarea`、`number``date`、`time`、`toggle`。 默认值设置为 `text`。 | 否 | 1.4 |
| `parameters.value` | 参数的初始值。 目前不支持该值 | 否 | 1.5 |

#### <a name="example"></a>示例

以下部分是定义搜索命令的 `composeExtensions` 对象的简单应用清单示例：

```json
{
...
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
...
}

```

有关完整的应用清单，请参阅 [应用清单架构](~/resources/schema/manifest-schema.md)。

## <a name="code-sample"></a>代码示例

| 示例名称           | 说明 | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Teams 消息扩展搜索   |  介绍如何定义搜索命令和响应搜索。        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="step-by-step-guide"></a>分步指南

按照 [分步指南](../../../sbs-messagingextension-searchcommand.yml) 生成基于搜索的消息扩展。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [响应搜索命令](~/messaging-extensions/how-to/search-commands/respond-to-search.md)。
