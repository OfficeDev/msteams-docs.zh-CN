---
title: 定义消息扩展搜索命令
author: surbhigupta
description: 在本模块中，了解 Teams 应用的消息扩展搜索命令，通过应用清单和手动创建搜索命令。
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 5cddfcc5f4fd3088e72538c6243b5f4fbf19767c
ms.sourcegitcommit: 217025a61ed9c3b76b507fe95563142abc6d0318
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2022
ms.locfileid: "67363471"
---
# <a name="define-message-extension-search-commands"></a>定义消息扩展搜索命令

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

消息扩展搜索命令允许用户搜索外部系统，并将搜索结果插入卡片形式的邮件中。 本文档介绍如何选择搜索命令调用位置，以及如何将搜索命令添加到应用清单。

> [!NOTE]
> 结果卡大小限制为 28 KB。 如果卡片的大小超过 28 KB，则不会发送该卡。

请参阅以下视频，了解如何定义消息扩展搜索命令：
<br>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4OIvK]
<br>

## <a name="select-search-command-invoke-locations"></a>选择搜索命令调用位置

搜索命令从以下任意一个或两个位置调用：

* 撰写消息区域：撰写消息区域底部的按钮。
* 命令框：命令框中的@mentioning。

  从撰写消息区域调用搜索命令时，用户会将结果发送到会话。 从命令框调用该卡时，用户会与生成的卡进行交互，或将其复制到其他位置使用。

下图显示了搜索命令的调用位置：

:::image type="content" source="~/assets/images/messaging-extension/search-command-invoke-locations.png" alt-text="搜索命令调用位置":::

## <a name="add-the-search-command-to-your-app-manifest"></a>将搜索命令添加到应用清单

若要将搜索命令添加到应用清单，必须将新 `composeExtension` 对象添加到应用清单 JSON 的顶层。 可以借助开发人员门户或手动添加搜索命令。

### <a name="create-a-search-command-using-developer-portal"></a>使用开发人员门户创建搜索命令

创建搜索命令的先决条件是必须已创建消息扩展名。 有关如何创建消息扩展的信息，请参阅[创建消息扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。

**创建操作命令**

1. 从 Microsoft Teams 客户 **端打开开发人员门户** ，然后选择“ **应用** ”选项卡。如果已在 **开发人员门户** 中创建应用包，请从列表中选择。 如果尚未创建应用包，请导入现有包。
1. 导入应用包后，选择 **“应用功能**”下 **的消息扩展**。
1. 若要创建消息扩展，需要 Microsoft 注册的机器人。 可以使用现有机器人，也可以创建新的机器人。 选择 **“新建机器人** ”选项，为新机器人命名，然后选择 **“创建**”。

   :::image type="content" source="../../../assets/images/tdp/bot-page.png" alt-text="屏幕截图显示如何在开发人员门户中创建机器人。":::

1. 若要使用现有机器人，请 **选择现有机器人** ，然后从下拉列表中选择现有机器人，或者选择 **“输入机器人 ID** ”（如果已创建机器人 ID）。

1. 选择消息传递扩展的范围，然后选择 **“保存**”。

1. 在 **“命令**”部分中选择 **“添加命令**”以包含命令，这些命令决定消息扩展的行为。
下图显示了如何为消息扩展添加命令：

   :::image type="content" source="../../../assets/images/tdp/add-a-command.PNG" alt-text="屏幕截图显示了如何添加命令来定义消息扩展的行为。":::

1. 选择 **“搜索** ”并输入 **命令 ID**、 **命令标题** 和 **命令说明**。

1. 输入所有参数，然后从下拉列表中选择输入类型。

   :::image type="content" source="../../../assets/images/tdp/add-a-command-parameter.PNG" alt-text="屏幕截图显示了如何添加参数以定义消息扩展的命令。":::

1. 选择 **“预览”链接** 下 **的“添加域**”。

1. 输入有效域，然后选择 **“添加**”。

   :::image type="content" source="../../../assets/images/tdp/add-domain.PNG" alt-text="屏幕截图显示了如何将有效的域添加到消息传递扩展，以便展开链接。":::

1. 选择“**保存**”。

   :::image type="content" source="../../../assets/images/tdp/add-a-command-save.PNG" alt-text="屏幕截图显示了如何保存消息扩展的所有设置和参数。":::

**添加其他参数**

1. 在命令节下选择省略号，然后选择 **“编辑”参数**。

   :::image type="content" source="../../../assets/images/tdp/edit-parameters.PNG" alt-text="屏幕截图显示了如何为消息扩展添加其他参数。":::

1. 选择 **“添加参数** ”并输入所有参数。

   :::image type="content" source="../../../assets/images/tdp/add-parameter.PNG" alt-text="屏幕截图显示了如何为消息扩展添加其他参数。"lightbox="../../../assets/images/tdp/add-a-parameters.PNG":::

### <a name="create-a-search-command-manually"></a>手动创建搜索命令

若要手动将消息扩展搜索命令添加到应用清单，必须将以下参数添加到 `composeExtension.commands` 对象数组：

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `id` | 此属性是分配给搜索命令的唯一 ID。 用户请求包含此 ID。 | 是 | 1.0 |
| `title` | 此属性是命令名称。 此值显示在 UI)  (用户界面中。 | 是 | 1.0 |
| `description` | 此属性是一个帮助文本，指示此命令的作用。 此值显示在 UI 中。 | 是 | 1.0 |
| `type` | 此属性必须为 `query`. | 否 | 1.4 |
|`initialRun` | 如果此属性设置为 **true**，则指示用户在 UI 中选择此命令后应立即执行此命令。 | 否 | 1.0 |
| `context` | 此属性是一个可选值数组，用于定义搜索操作可用的上下文。 可取值包括 `message`、`compose` 或 `commandBox`。 默认值为 `["compose", "commandBox"]`。 | 否 | 1.5 |

必须添加搜索参数的详细信息，该参数定义 Teams 客户端中用户可见的文本。

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `parameters` | 此属性定义命令的参数静态列表。 | 否 | 1.0 |
| `parameter.name` | 此属性描述参数的名称。 这会在用户请求中发送到服务。 | 是 | 1.0 |
| `parameter.description` | 此属性描述参数的用途或必须提供的值的示例。 此值显示在 UI 中。 | 是 | 1.0 |
| `parameter.title` | 此属性是一个简短的用户友好参数标题或标签。 | 是 | 1.0 |
| `parameter.inputType` | 此属性设置为所需的输入类型。 可能的值包括`text`， `textarea`， `number`， `date`， `time`。 `toggle` 默认设置为 `text`. | 否 | 1.4 |
| `parameters.value` | 参数的初始值。 当前不支持该值 | 否 | 1.5 |

#### <a name="example"></a>示例

以下部分是定义搜索命令的对象的简单应用清单的 `composeExtensions` 示例：

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
