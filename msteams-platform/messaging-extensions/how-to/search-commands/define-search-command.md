---
title: 定义邮件扩展搜索命令
author: clearab
description: 为 Microsoft Teams 应用定义邮件扩展搜索命令。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 18bac3049fec8fead168c12f2832bfbbb72cf609
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449267"
---
# <a name="define-messaging-extension-search-commands"></a>定义邮件扩展搜索命令

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

邮件扩展搜索命令允许用户搜索外部系统，并将该搜索的结果插入卡片形式的邮件中。

> [!NOTE]
> 结果卡片大小限制为 28 KB。 如果卡的大小超过 28 KB，则不发送该卡。 

## <a name="choose-messaging-extension-invoke-locations"></a>选择消息扩展调用位置

需要确定的第一件事是，在何处触发搜索命令 (具体调用搜索) 位置。  可以从以下一个或两个位置调用搜索命令：

* 撰写邮件区域底部的按钮
* 在@mentioning框中显示

从撰写邮件区域调用时，用户可选择将结果发送到对话。 从命令框调用时，用户可以与生成的卡片进行交互，或复制它以在其他地方使用。

## <a name="add-the-command-to-your-app-manifest"></a>将命令添加到应用清单

现在，你已决定用户如何与搜索命令交互，是时候将其添加到应用清单了。 为此，你将向应用清单 JSON 的顶层添加新 `composeExtension` 对象。 可以在 App Studio 的帮助下或手动执行。

### <a name="create-a-command-using-app-studio"></a>使用 App Studio 创建命令

创建搜索命令的先决条件是您必须已创建邮件扩展。 若要了解如何创建邮件扩展，请参阅 [创建邮件扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。

**创建搜索命令**

1. 在 Microsoft Teams 客户端中，打开 **App Studio，** 然后选择清单 **编辑器** 选项卡。
1. 如果你已在 **App Studio** 中创建应用包，请从列表中选择它。 如果尚未创建应用包，请导入现有应用包。
1. 导入应用包后，在 **"功能"下选择**"消息扩展 **"。**
1. 选择 **"** 消息扩展 **"页** 中的"在命令"部分添加。
1. Choose **Allow users to query your service for information and insert that into a message.**
1. 添加命令 **ID** 和 **标题**。
1. 选择必须触发搜索命令的位置。 选择 **邮件** 当前不会更改搜索命令的行为。
1. 添加搜索参数，然后选择"**保存"。**
 
### <a name="manually-create-a-command"></a>手动创建命令

若要将邮件扩展搜索命令手动添加到应用清单，需要将以下参数添加到 `composeExtension.commands` 对象数组。

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `id` | 分配给此命令的唯一 ID。 用户请求将包含此 ID。 | 是 | 1.0 |
| `title` | 命令名称。 此值显示在 UI 中。 | 是 | 1.0 |
| `description` | 指示此命令执行哪些操作的帮助文本。 此值显示在 UI 中。 | 是 | 1.0 |
| `type` | 必须是 `query` | 否 | 1.4 |
|`initialRun` | 如果设置为 **true，** 则指示在用户选择 UI 中的此命令后，应尽快执行此命令。 | 否 | 1.0 |
| `context` | 用于定义搜索操作可用的上下文的可选值数组。 可能的值是 `message` ， `compose` 或 `commandBox` 。 默认值为“`["compose", "commandBox"]`”。 | 否 | 1.5 |

你还需要添加搜索参数的详细信息，这将定义在 Teams 客户端中对用户可见的文本。

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `parameters` | 命令的参数静态列表。 | 否 | 1.0 |
| `parameter.name` | 参数的名称。 这将在用户请求中发送到你的服务。 | 是 | 1.0 |
| `parameter.description` | 描述此参数的用途或应提供的值示例。 此值显示在 UI 中。 | 是 | 1.0 |
| `parameter.title` | 简短的用户友好参数标题或标签。 | 是 | 1.0 |
| `parameter.inputType` | 设置为所需的输入类型。 可能的值包括 `text` ， ， ， ， `textarea` `number` `date` `time` `toggle` 。 默认值设置为 `text` | 否 | 1.4 |

#### <a name="app-manifest-example"></a>应用清单示例

下面是定义搜索 `composeExtensions` 命令的对象的示例。 这不是完整清单的示例，有关完整应用清单架构，请参阅： [应用清单架构](~/resources/schema/manifest-schema.md)。

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

## <a name="next-steps"></a>后续步骤

现在，你已添加搜索命令，你将需要 [处理搜索请求](~/messaging-extensions/how-to/search-commands/respond-to-search.md)。

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
