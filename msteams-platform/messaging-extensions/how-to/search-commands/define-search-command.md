---
title: 定义消息扩展搜索命令
author: surbhigupta
description: 在本模块中，了解 Teams 应用的消息扩展搜索命令，通过应用清单和手动创建搜索命令。
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: c131a511c5c16eac4bf57093bbbeed9bd4172e97
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503940"
---
# <a name="define-message-extension-search-commands"></a>定义消息扩展搜索命令

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

消息扩展搜索命令允许用户搜索外部系统，并将搜索结果插入卡片形式的邮件中。 本文档介绍如何选择搜索命令调用位置，以及如何将搜索命令添加到应用清单。

> [!NOTE]
> 结果卡大小限制为 28 KB。 如果卡片的大小超过 28 KB，则不会发送该卡。

请参阅以下视频，了解如何定义消息扩展搜索命令：
<br>

> [!VIDEO <https://www.microsoft.com/en-us/videoplayer/embed/RE4OIvK>]
<br>

## <a name="select-search-command-invoke-locations"></a>选择搜索命令调用位置

搜索命令从以下任意一个或两个位置调用：

* 撰写消息区域：撰写消息区域底部的按钮。
* 命令框：命令框中的@mentioning。

  从撰写消息区域调用搜索命令时，用户会将结果发送到会话。 从命令框调用该卡时，用户会与生成的卡进行交互，或将其复制到其他位置使用。

下图显示了搜索命令的调用位置：

:::image type="content" source="~/assets/images/messaging-extension/search-command-invoke-locations.png" alt-text="搜索命令调用位置":::

## <a name="add-the-search-command-to-your-app-manifest"></a>将搜索命令添加到应用清单

若要将搜索命令添加到应用清单，必须将新 `composeExtension` 对象添加到应用清单 JSON 的顶层。 可以在 App Studio 的帮助下或手动添加搜索命令。

### <a name="create-a-search-command-using-app-studio"></a>使用 App Studio 创建搜索命令

创建搜索命令的先决条件是必须已创建消息扩展名。 有关如何创建消息扩展的信息，请参阅[创建消息扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。

若要创建搜索命令，请执行以下操作：

1. 从 Microsoft Teams 客户端打开 “**App Studio**”，并选择“**清单编辑器**”选项卡。
1. 如果已在 **App Studio** 中创建应用包，请从列表中选择。 如果尚未创建应用包，请导入现有包。
1. 导入应用包后，选择“**功能**”下 **的消息扩展**。 将显示一个弹出窗口来设置消息扩展。
1. 在窗口中选择“**设置**”，以在应用体验中包含消息扩展。 下图显示消息扩展设置页：

    :::image type="content" source="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt-text="消息传递扩展设置":::

1. 若要创建消息扩展，需要 Microsoft 注册的机器人。 可以使用现有机器人，也可以创建新的机器人。 选择“**创建新的机器人**”选项，为新机器人命名，然后选择“**创建**”。 下图显示了如何为消息扩展创建机器人：

    :::image type="content" source="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt-text="为消息传递扩展创建机器人":::

1. 若要使用现有机器人，请选择“**使用现有机器人**”，然后选择“**从现有机器人之一选择**”，以从下拉列表中选择现有机器人，提供“**机器人名称**”，如果已创建机器人 ID，请选择“**保存**”或选择“**连接到不同的机器人 ID**”，提供“**机器人名称**”并选择“**保存**”。

    :::image type="content" source="~/assets/images/messaging-extension/use-existing-bot.png" alt-text="将现有机器人用于消息传递扩展":::

1. 选择“在消息扩展页的 **命令”部分** 中 **添加**“以包含命令，这些命令决定消息扩展的行为。
下图显示了如何为消息扩展添加命令：

    :::image type="content" source="~/assets/images/messaging-extension/include-command.png" alt-text="包含命令":::

1. 选择 **“允许用户查询服务信息并将其插入到邮件中**”。 下图显示了搜索命令参数选择：

    :::image type="content" source="~/assets/images/messaging-extension/search-command-parameter-selection.png" alt-text="搜索命令参数选择":::

1. 添加 **命令 ID** 和 **标题**。
1. 选择必须从中调用搜索命令的位置。 下图显示了搜索命令调用位置：

    :::image type="content" source="~/assets/images/messaging-extension/search-command-invoke-location-selection.png" alt-text="搜索命令调用位置选择":::

1. 添加搜索参数并选择 **“保存**”。

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
