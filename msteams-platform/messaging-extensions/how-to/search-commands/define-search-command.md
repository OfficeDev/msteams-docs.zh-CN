---
title: 定义消息传递扩展搜索命令
author: clearab
description: 为 Microsoft Teams 应用定义消息传递扩展搜索命令。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 19f1fdf7bd4efdbb0de11d1abad341ec24bc27bd
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696787"
---
# <a name="define-messaging-extension-search-commands"></a>定义消息传递扩展搜索命令

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

邮件扩展搜索命令允许用户搜索外部系统，并将该搜索的结果插入卡片形式的邮件中。 本文档指导您如何选择搜索命令调用位置，以及将搜索命令添加到应用清单。

> [!NOTE]
> 结果卡大小限制为 28 KB。 如果卡的大小超过 28 KB，则不发送该卡。

## <a name="select-search-command-invoke-locations"></a>选择搜索命令调用位置

从以下任一位置或两个位置调用搜索命令：

* 撰写邮件区域：撰写邮件区域底部的按钮。
* 命令框：@mentioning命令框中显示。

从撰写邮件区域调用搜索命令时，用户将结果发送到对话。 从命令框调用它时，用户与生成的卡片交互，或复制该卡片以在其他地方使用。

下图显示了搜索命令的调用位置：

![搜索命令调用位置](~/assets/images/messaging-extension/search-command-invoke-locations.png)

## <a name="add-the-search-command-to-your-app-manifest"></a>将搜索命令添加到应用清单

若要将搜索命令添加到应用清单，必须将新对象添加到应用清单 `composeExtension` JSON 的顶层。 可以在 App Studio 的帮助下或手动添加搜索命令。

### <a name="create-a-search-command-using-app-studio"></a>使用 App Studio 创建搜索命令

创建搜索命令的先决条件是，必须已创建邮件扩展。 若要了解如何创建邮件扩展，请参阅创建 [邮件扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。

**创建搜索命令**

1. 从 Microsoft Teams 客户端打开 **App Studio，** 然后选择清单 **编辑器** 选项卡。
1.  如果你已在 **App Studio** 中创建应用包，请从列表中选择。 如果尚未创建应用包，请导入现有应用包。
1. 导入应用包后，选择 **功能下的** 消息传递 **扩展**。 你获得一个弹出窗口来设置邮件扩展。
1. 选择 **窗口中** 的"设置"，将消息传递扩展包括在你的应用体验中。 下图显示了邮件扩展设置页面： 

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. 若要创建消息扩展，你需要一个 Microsoft 注册的自动程序。 可以使用现有自动程序或创建新的自动程序。 选择 **"创建新自动程序**"选项，为新的自动程序命名，然后选择"创建 **"。** 下图显示了邮件扩展的自动程序创建：

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. 选择 **"** 邮件扩展 **"** 页的"命令"部分中的"添加"，以包含决定邮件扩展行为的命令。   
下图显示了邮件扩展的命令添加：

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>
1. 选择 **"允许用户查询服务信息"，并将其插入到消息中**。 下图显示了搜索命令参数选择：

    <img src="~/assets/images/messaging-extension/search-command-parameter-selection.png" alt="search command parameter selection" width="500"/>

1. 添加命令 **ID** 和 **标题**。
1. 选择必须调用搜索命令的位置。 选择 **邮件** 当前不会更改搜索命令的行为。 下图显示了搜索命令调用位置：

    <img src="~/assets/images/messaging-extension/search-command-invoke-location-selection.png" alt="search command invoke location selection]" width="500"/>

1. 添加搜索参数，然后选择"保存 **"。**

### <a name="create-a-search-command-manually"></a>手动创建搜索命令 

若要将邮件扩展搜索命令手动添加到应用清单，必须将以下参数添加到 `composeExtension.commands` 对象数组：

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `id` | 此属性是分配给搜索命令的唯一 ID。 用户请求包括此 ID。 | 是 | 1.0 |
| `title` | 此属性是命令名称。 此值显示在用户界面用户界面 (UI) 。 | 是 | 1.0 |
| `description` | 此属性是一个帮助文本，用于指示此命令执行哪些操作。 此值显示在 UI 中。 | 是 | 1.0 |
| `type` | 此属性必须为 `query` 。 | 否 | 1.4 |
|`initialRun` | 如果此属性设置为 **true**，则指示用户一旦在 UI 中选择此命令，就应执行此命令。 | 否 | 1.0 |
| `context` | 此属性是一个可选的值数组，用于定义搜索操作可用的上下文。 可取值包括 `message`、`compose` 或 `commandBox`。 默认值为 `["compose", "commandBox"]` 。 | 否 | 1.5 |

必须添加搜索参数的详细信息，该参数定义在 Teams 客户端中对用户可见的文本。

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `parameters` | 此属性定义命令的参数静态列表。 | 否 | 1.0 |
| `parameter.name` | 此属性描述参数的名称。 这将在用户请求中发送到你的服务。 | 是 | 1.0 |
| `parameter.description` | 此属性描述参数的用途或必须提供的值示例。 此值显示在 UI 中。 | 是 | 1.0 |
| `parameter.title` | 此属性是一个简短的用户友好参数标题或标签。 | 是 | 1.0 |
| `parameter.inputType` | 此属性设置为所需输入的类型。 可能的值包括 `text` `textarea` `number` 、、、、、。 `date` `time` `toggle` 默认值设置为 `text` 。 | 否 | 1.4 |

#### <a name="example"></a>示例

以下部分是定义搜索命令的对象的简单应用 `composeExtensions` 清单的示例： 

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
|Teams 消息传递扩展操作| 介绍如何定义操作命令、创建任务模块和响应任务模块提交操作。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Teams 消息传递扩展搜索   |  介绍如何定义搜索命令并响应搜索。        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [响应搜索命令](~/messaging-extensions/how-to/search-commands/respond-to-search.md)。

