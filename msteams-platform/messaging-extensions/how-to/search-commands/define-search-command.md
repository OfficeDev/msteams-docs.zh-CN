---
title: 定义邮件扩展搜索命令
author: clearab
description: 为 Microsoft 团队应用程序定义邮件扩展搜索命令。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: b6837fb8a131d8ce3e2bbd0c51c2861dbffda2bc
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673305"
---
# <a name="define-messaging-extension-search-commands"></a>定义邮件扩展搜索命令

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

邮件扩展搜索命令允许您的用户搜索外部系统，并将该搜索的结果插入卡片形式的邮件中。

## <a name="choose-messaging-extension-invoke-locations"></a>选择消息扩展调用位置

您需要确定的第一件事是可以从其触发搜索命令（或更具体地说，*调用*）。 您可以从以下一个或两个位置调用您的搜索命令：

* 撰写邮件区域底部的按钮
* 通过在命令框中 @mentioning

从撰写邮件区域调用时，您的用户将可以选择将结果发送到对话。 在命令框中调用用户时，用户可以与生成的卡片进行交互，或将其复制以供其他地方使用。

## <a name="add-the-command-to-your-app-manifest"></a>将命令添加到应用程序清单

现在，您已经决定了用户将如何与您的搜索命令进行交互，现在可以将其添加到您的应用程序清单中了。 若要执行此操作，请将`composeExtension`新对象添加到应用程序清单 JSON 的最高级别。 您可以使用应用程序 Studio 的帮助或手动执行此操作。

### <a name="create-a-command-using-app-studio"></a>使用应用程序 Studio 创建命令

以下步骤假定您已经[创建了邮件扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。

1. 在 Microsoft 团队客户端中，打开**应用程序 Studio**并选择 "**清单编辑器**" 选项卡。
2. 如果您已经在应用程序 Studio 中创建了应用程序包，请从列表中选择它。 如果不是，则可以导入现有的应用程序包。
3. 单击 "命令" 部分的 "**添加**" 按钮。
4. 选择 "**允许用户查询服务以获取信息" 并将其插入到邮件中**。
5. 添加**命令 Id**和**标题**。
6. 选择要从中触发搜索命令的位置。 选择**邮件**当前不会改变搜索命令的行为。
7. 添加搜索参数。
8. 单击"保存"。

### <a name="manually-create-a-command"></a>手动创建命令

若要将邮件扩展搜索命令手动添加到应用程序清单中，需要将以下参数添加到您`composeExtension.commands`的对象数组中。

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `id` | 您分配给此命令的唯一 ID。 用户请求将包括此 ID。 | 是 | 1.0 |
| `title` | 命令名称。 此值显示在 UI 中。 | 是 | 1.0 |
| `description` | 指示此命令执行的操作的帮助文本。 此值显示在 UI 中。 | 是 | 1.0 |
| `type` | 必须是 `query` | 否 | 1.4 |
|`initialRun` | 如果设置为**true**，则指示应在用户在 UI 中选择此命令后立即执行此命令。 | 否 | 1.0 |
| `context` | 用于定义搜索操作在中可用的上下文的值的可选数组。 可能的值`message`为`compose`、或`commandBox`。 默认值为 `["compose", "commandBox"]`。 | 否 | 1.5 |

您还需要添加搜索参数的详细信息，该详细信息将定义在团队客户端中用户可见的文本。

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `parameters` | 命令的参数的静态列表。 | 否 | 1.0 |
| `parameter.name` | 参数的名称。 此项将发送到用户请求中的服务。 | 是 | 1.0 |
| `parameter.description` | 描述了此参数的用途或应提供的值的示例。 此值显示在 UI 中。 | 是 | 1.0 |
| `parameter.title` | 短用户友好参数标题或标签。 | 是 | 1.0 |
| `parameter.inputType` | 设置为所需的输入类型。 可能的值`text`包括`textarea`、 `number`、 `date`、 `time`、 `toggle`、。 默认值设置为`text` | 否 | 1.4 |

#### <a name="app-manifest-example"></a>应用部件清单示例

下面是定义搜索命令的`composeExtensions`对象的一个示例。 这不是完整清单的完整清单示例，请参阅：[应用程序清单架构](~/resources/schema/manifest-schema.md)。

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

现在您已经添加了搜索命令，您需要[处理搜索请求](~/messaging-extensions/how-to/search-commands/respond-to-search.md)。

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]