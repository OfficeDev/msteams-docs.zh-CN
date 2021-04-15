---
title: 使用 App Studio 创建消息传递
author: clearab
description: 了解如何使用 App Studio 创建 Microsoft Teams 消息传递扩展。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 25086d959004046e8227de46b31d840c0b3fd228
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51697224"
---
# <a name="create-a-messaging-extension-using-app-studio"></a>使用 App Studio 创建消息传递

> [!TIP]
> 寻找更快速入门的方法？ 使用 Microsoft Teams [策略](../build-your-first-app/build-messaging-extension.md) 创建消息传递Toolkit。

在高级别上，您需要完成以下步骤以创建邮件扩展。

1. 准备开发环境
2. 在开发时创建和部署 (服务使用隧道服务（如 ngrok）在本地运行) 
3. 使用 Bot Framework 注册你的 Web 服务
4. 创建应用包
5. 将你的程序包上传到 Microsoft Teams

创建 Web 服务、创建应用包以及使用 Bot Framework 注册 Web 服务可以按任意顺序完成。 由于这三个部分相互关联，因此无论按哪种顺序执行它们，都需要返回以更新其他部分。 注册需要来自部署的 Web 服务的消息终结点，并且 Web 服务需要通过注册创建的 ID 和密码。 你的应用清单还需要该 ID 以将 Teams 连接到 Web 服务。

生成邮件扩展时，你将定期在更改应用清单和将代码部署到 Web 服务之间移动。 使用应用清单时，请记住，你可以手动操作 JSON 文件，或者通过 App Studio 进行更改。 无论采用哪种方式，在更改清单时) 在 Teams 中重新部署 (上传应用，但在将更改部署到 Web 服务时无需这样做。

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>创建 Web 服务

邮件扩展的核心是 Web 服务。 它将定义一个路由（通常为 `/api/messages` ）以接收所有请求。 如果你从头开始，你可以从几个选项中进行选择。

* 使用我们的快速 [入门](#learn-more) 教程之一指导你创建 Web 服务。
* 从 Bot [Framework](https://github.com/Microsoft/BotBuilder-Samples) 示例存储库中选择一个消息扩展示例。
* 如果你使用的是 JavaScript，请使用 Microsoft Teams 的 [Yeoman](https://github.com/OfficeDev/generator-teams) 生成器为 Teams 应用（包括 Web 服务）搭建基架。
* 从头开始创建 Web 服务。 可选择添加面向你的语言的 Bot Framework SDK，也可以直接使用 JSON 有效负载。

## <a name="register-your-web-service-with-the-bot-framework"></a>使用 Bot Framework 注册你的 Web 服务

邮件扩展利用 Bot Framework 的消息架构和安全通信协议;如果还没有，则需要在 Bot Framework 上注册 Web 服务。 Microsoft 应用 ID (我们将它作为来自 Teams 内部的自动程序 ID 进行引用，以便从你可能正在处理) 的其他应用 ID 中标识它，在 Bot Framework 中注册的消息终结点将在你的消息传递扩展中用于接收和响应请求。 如果你使用的是现有注册，请确保启用 Microsoft Teams [频道](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true)。

如果你遵循其中一个快速入门或从其中一个可用示例开始，将指导你完成注册 Web 服务。 如果要手动注册服务，有三个选项可进行注册。 如果选择注册而不使用 Azure 订阅，将无法利用 Bot Framework 提供的简化 OAuth 身份验证流。 创建后，你将能够将注册迁移到 Azure。

* 如果你有 Azure 订阅 (或想要创建新的 Azure) ，可以使用 Azure 门户手动注册 Web 服务。 创建"Bot Channels Registration"资源。 你可以选择免费定价层，因为来自 Microsoft Teams 的消息不计入每月允许的消息总数。
* 如果你不希望使用 Azure 订阅，可以使用旧版 [注册门户](https://dev.botframework.com/bots/new)。
* App Studio 还可以帮助你注册 Web 服务 (自动) 。 通过 App Studio 注册的 Web 服务未在 Azure 中注册。 可以使用旧 [门户查看](https://dev.botframework.com/bots) 、管理和迁移注册。

## <a name="create-your-app-manifest"></a>创建应用清单

你可以使用 App Studio 帮助创建应用程序清单，也可以手动创建。

### <a name="create-your-app-manifest-using-app-studio"></a>使用 App Studio 创建应用清单

可以在 Microsoft Teams 客户端内使用 App Studio 应用来帮助创建应用清单。

1. 在 Teams 客户端中，从左侧导航栏上的“**…**”溢出菜单中打开 App Studio。 如果尚未安装，则可以通过搜索来这样做。
2. 在清单 **编辑器** 选项卡上 **，选择** 创建新应用 (或者如果你要向现有应用添加消息传递扩展，你可以将应用包) 
3. 添加应用详细信息（有关每个字段的完整说明，请参阅[清单架构定义](~/resources/schema/manifest-schema.md)）。
4. 在" **消息扩展"** 选项卡上，单击" **设置"** 按钮。
5. 你可以创建新的 Web 服务 (自动) 供邮件扩展使用，或者如果你已注册一个，请在此处选择/添加它。
6. 如有必要，请更新自动程序终结点地址以指向你的自动程序。 它应该类似于 `https://someplace.com/api/messages`。
7. "**命令****"部分中的**"添加"按钮将指导你向邮件扩展添加命令。 有关添加 [命令详细信息](#learn-more) 的链接，请参阅了解详细信息部分。 请记住，您可以为邮件扩展定义最多 10 个命令。
8. " **消息处理程序"** 部分允许您添加邮件将触发的域。 有关详细信息 [，请参阅链接](~/messaging-extensions/how-to/link-unfurling.md) 取消链接。

从"**完成 =**> 测试并分发"选项卡中，你可以下载应用包 (其中包含应用清单以及应用图标) 或安装程序包。 

### <a name="create-your-app-manifest-manually"></a>手动创建应用清单

与机器人和选项卡一样，更新 [应用](~/resources/schema/manifest-schema.md#composeextensions) 的应用清单以包含消息传递扩展属性。 这些属性控制邮件扩展在 Microsoft Teams 客户端中的显示和行为方式。 从清单的 v1.0 开始，支持消息传递扩展。

#### <a name="declare-your-messaging-extension"></a>声明邮件扩展

若要添加消息传递扩展，请通过 属性在应用清单中添加一个新的顶级 JSON `composeExtensions` 结构。 使用最多 10 个命令为应用创建单个消息传递扩展。

> [!NOTE]
> 清单将消息传递扩展引用为 `composeExtensions` 。 这是为了维护向后兼容性。

扩展定义是具有以下结构的对象：

| 属性名称 | 用途 | 是否必需？ |
|---|---|---|
| `botId` | 使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。 这通常应该与整个 Teams 应用的 ID 相同。 | 是 |
| `canUpdateConfiguration` | 启用 **"设置"** 菜单项。 | 否 |
| `commands` | 此邮件扩展支持的命令数组。 只能使用 10 个命令。 | 是 |

#### <a name="define-your-commands"></a>定义命令

邮件扩展应声明一个或多个命令，这些命令定义用户可以在何处触发邮件扩展以及交互类型。 有关 [邮件](#learn-more) 扩展命令详细信息，请参阅了解详细信息。

#### <a name="simple-manifest-example"></a>简单清单示例

以下示例是应用清单中具有搜索命令的简单消息传递扩展对象。 这不是整个应用程序清单文件，只是特定于消息传递扩展的部分。 有关 [完整示例，](~/resources/schema/manifest-schema.md) 请参阅应用清单架构。

```json
...
"composeExtensions": [
  {
    "botId": "abcd1234-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "searchCmd",
        "description": "Search you ToDo's",
        "title": "Search",
        "initialRun": true,
        "parameters": [
          {
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }
        ]
      }
    ]
  }
]
...
```

#### <a name="complete-app-manifest-example"></a>完整的应用清单示例

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
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
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

## <a name="add-your-invoke-message-handlers"></a>添加调用消息处理程序

当用户触发消息扩展时，你需要处理初始调用消息，从用户收集一些信息，然后处理该信息并做出相应的响应。 为此，首先需要确定要添加到邮件扩展中的命令类型，并添加操作[命令或](~/messaging-extensions/how-to/action-commands/define-action-command.md)[添加搜索命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)。

## <a name="messaging-extensions-in-teams-meetings"></a>Teams 会议中的消息扩展

> [!NOTE]
> 如果会议或群聊在名单中有联盟用户，则 Teams 将禁止所有用户（包括组织者）访问消息传递扩展。

会议开始后，Teams 参与者可以在实时呼叫期间直接与消息扩展进行交互。 生成会议内消息传递扩展时，请考虑以下事项：

1. **Location**。 可以从会议聊天中的撰写消息区域、命令框或消息@mentioned消息扩展。

1. **元数据**。 调用消息扩展时，它可以从 和 标识用户和 `userId` 租户 `tenantId` 。 可在 `channelData` 对象中找到 `meetingId`。 你的应用可以使用 和 `userId` `meetingId`  的 API `GetParticipant` 请求检索用户角色。

1. **命令类型**。 如果邮件扩展使用 [基于操作的命令](../messaging-extensions/what-are-messaging-extensions.md#action-commands)，它应遵循选项卡 [单一登录](../tabs/how-to/authentication/auth-aad-sso.md) 身份验证。

1. **用户体验**。 消息扩展的外观和行为应该与在会议外相同。

## <a name="next-steps"></a>后续步骤

* [创建操作命令](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [创建搜索命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [链接展开](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a>了解详细信息

在快速入门中试用：

* C 快速入门#
  * [使用基于操作的命令的邮件扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [使用基于搜索的命令的邮件扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* JavaScript 快速入门
  * [使用基于操作的命令的邮件扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [使用基于搜索的命令的邮件扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

详细了解 Teams 开发概念：

* [了解 Teams 应用功能](../concepts/capabilities-overview.md)
* [什么是消息扩展？](../messaging-extensions/what-are-messaging-extensions.md)
