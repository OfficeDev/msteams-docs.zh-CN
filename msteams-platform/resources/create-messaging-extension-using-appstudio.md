---
title: 使用 App Studio 创建消息传递
author: surbhigupta
description: 了解如何使用 App Studio 创建Microsoft Teams消息传递扩展。
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 09bc7a7884f69c7c3ac4c8e195e5ac6d14d20990
ms.sourcegitcommit: 12510f34b00bfdd0b0e92d35c8dbe6ea1f6f0be2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2022
ms.locfileid: "66032779"
---
# <a name="create-a-messaging-extension-using-app-studio"></a>使用 App Studio 创建消息传递

> [!TIP]
> 寻找更快入门的方法？ 使用Microsoft Teams Toolkit创建[消息传递扩展](../build-your-first-app/build-messaging-extension.md)。

在高级别上，需要完成以下步骤来创建消息传递扩展。

1. 准备开发环境
2. 在开发时创建和部署 Web 服务 (使用 ngrok 等隧道服务在本地运行它) 
3. 使用 Bot Framework 注册你的 Web 服务
4. 创建应用包
5. 将你的程序包上传到 Microsoft Teams

可以按任何顺序创建 Web 服务、创建应用包以及向 Bot Framework 注册 Web 服务。 因为这三个部分是如此交织在一起，无论你按哪个顺序执行这些操作，都需要返回以更新其他部分。 注册需要已部署 Web 服务的消息传送终结点，并且 Web 服务需要从注册中创建的 ID 和密码。 应用清单还需要该 ID 才能将Teams连接到 Web 服务。

在生成消息传递扩展时，你将定期在更改应用清单和将代码部署到 Web 服务之间移动。 使用应用清单时，请确保可以手动修改 JSON 文件或通过 App Studio 进行更改。 无论哪种方式，在更改清单时，都需要重新部署 () 应用上传Teams，但在将更改部署到 Web 服务时无需执行此操作。

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>创建 Web 服务

消息传递扩展的核心是 Web 服务。 它将定义单个路由，通常 `/api/messages`用于接收所有请求。 如果你是从头开始的，你有一些选项可供选择。

* 使用我们的 [快速入](#learn-more) 门教程之一，指导你完成 Web 服务的创建。
* 从 [Bot Framework 示例存储库](https://github.com/Microsoft/BotBuilder-Samples) 中选择可用的消息传递扩展示例之一。
* 如果使用的是 JavaScript，请使用[用于Microsoft Teams的 Yeoman 生成器](https://github.com/OfficeDev/generator-teams)来搭建Teams应用的基架，包括 Web 服务。
* 从头开始创建 Web 服务。 可选择添加面向你的语言的 Bot Framework SDK，也可以直接使用 JSON 有效负载。

## <a name="register-your-web-service-with-the-bot-framework"></a>使用 Bot Framework 注册你的 Web 服务

消息传递扩展利用 Bot Framework 的消息传送架构和安全通信协议;如果还没有 Web 服务，则需要在 Bot Framework 上注册 Web 服务。 Microsoft 应用 ID (我们将此 ID 引用为来自Teams内部的机器人 ID，以便从其他应用 ID 中标识它，你可能正在处理) ，并且在 Bot Framework 中注册的消息终结点将用于消息传递扩展来接收和响应请求。 如果使用的是现有注册，请确保[启用Microsoft Teams通道](/azure/bot-service/bot-service-manage-channels?preserve-view=true&view=azure-bot-service-4.0)。

如果遵循其中一个快速入门，或者从其中一个可用示例开始，将引导你注册 Web 服务。 如果要手动注册服务，则有三个选项可执行此操作。 如果选择注册而不使用 Azure 订阅，则无法利用 Bot Framework 提供的简化的 OAuth 身份验证流。 创建后，你将能够将注册迁移到 Azure。

* 如果有 Azure 订阅 (或想要创建新的) ，则可以使用Microsoft Azure门户手动注册 Web 服务。 创建“机器人通道注册”资源。 可以选择免费定价层，因为来自Microsoft Teams的消息不计入每月允许的消息总数。
* 如果不想使用 Azure 订阅，可以使用 [旧版注册门户](https://dev.botframework.com/bots/new)。
* App Studio 还可以帮助你注册 web 服务 (机器人) 。 通过 App Studio 注册的 Web 服务不会在 Azure 中注册。 可以使用 [旧门户](https://dev.botframework.com/bots) 查看、管理和迁移注册。

## <a name="create-your-app-manifest"></a>创建应用清单

你可以使用 App Studio 帮助创建应用程序清单，也可以手动创建。

### <a name="create-your-app-manifest-using-app-studio"></a>使用 App Studio 创建应用清单

可以从Microsoft Teams客户端中使用 App Studio 应用来帮助创建应用清单。

1. 在 Teams 客户端中，从左侧导航栏上的“**…**”溢出菜单中打开 App Studio。 如果尚未安装，可以通过搜索来执行此操作。
2. 在 **“清单编辑器** ”选项卡上选择 **“创建新应用** (，或者如果要将消息传递扩展添加到现有应用，则可以导入应用包) 
3. 添加应用详细信息（有关每个字段的完整说明，请参阅[清单架构定义](~/resources/schema/manifest-schema.md)）。
4. 在 **“消息传递扩展”** 选项卡上，选择 **“设置”** 按钮。
5. 可以创建新的 Web 服务 (机器人) 供消息传递扩展使用，或者如果你已在此处注册了一个选择/添加它。
6. 如有必要，请更新自动程序终结点地址以指向你的自动程序。 它应该类似于 `https://someplace.com/api/messages`。
7. “**命令**”部分中的 **“添加**”按钮将指导你向消息传递扩展添加命令。 有关添加命令的详细信息，请参阅 [“了解详细](#learn-more) 信息”部分。 请记住，最多可以为消息传递扩展定义 10 个命令。
8. **通过“消息处理程序**”部分，可以添加消息传送将触发的域。 有关详细信息，请参阅 [链接展开](~/messaging-extensions/how-to/link-unfurling.md) 。

从 **“完成” =>“测试”和“分发** ”选项卡中，可以 **下载** 应用包 (包括应用清单以及应用图标) 或 **安装** 包。

### <a name="create-your-app-manifest-manually"></a>手动创建应用清单

与机器人和选项卡一样，更新应用的 [应用清单](~/resources/schema/manifest-schema.md#composeextensions) 以包含消息传递扩展属性。 这些属性控制消息传递扩展在Microsoft Teams客户端中的显示和行为方式。 从清单的 v1.0 开始支持消息传递扩展。

#### <a name="declare-your-messaging-extension"></a>声明消息传递扩展插件

若要添加消息传递扩展，请在应用清单中包含一个新的顶级 JSON 结构和属性 `composeExtensions` 。 为应用创建单个消息传递扩展，最多包含 10 个命令。

> [!NOTE]
> 清单将消息传递扩展称为 `composeExtensions`。 这是为了保持向后兼容性。

扩展定义是具有以下结构的对象：

| 属性名称 | 用途 | 是否必需？ |
|---|---|---|
| `botId` | 使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。 这通常应与整体Teams应用的 ID 相同。 | 是 |
| `canUpdateConfiguration` | 启用 **设置** 菜单项。 | 否 |
| `commands` | 此消息传递扩展支持的命令数组。 你只能使用 10 个命令。 | 是 |

#### <a name="define-your-commands"></a>定义命令

消息传递扩展应该声明一个或多个命令，用于定义用户可以触发消息传递扩展的位置以及交互的类型。 有关消息传递扩展命令的详细信息，请参阅 [详细](#learn-more) 信息。

#### <a name="simple-manifest-example"></a>简单清单示例

下面的示例是应用清单中包含搜索命令的简单消息传递扩展对象。 这不是整个应用程序清单文件，只是特定于消息传递扩展的部分。 有关完整示例，请参阅 [应用清单架构](~/resources/schema/manifest-schema.md) 。

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

当用户触发消息传递扩展时，需要处理初始调用消息，从用户收集一些信息，然后处理该信息并做出适当的响应。 为此，首先需要确定要添加到消息传递扩展的命令类型，并 [添加操作命令](~/messaging-extensions/how-to/action-commands/define-action-command.md) 或 [添加搜索命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)。

## <a name="messaging-extensions-in-teams-meetings"></a>Teams会议中的消息传递扩展插件

> [!NOTE]
> 如果会议或群聊已联合名册中的用户，Teams禁止所有用户（包括组织者）访问消息扩展。

会议开始后，Teams参与者可以在实时呼叫期间直接与消息传递扩展进行交互。 生成会议内消息传递扩展时，请考虑以下事项：

1. **Location**。 可以在会议聊天中从撰写消息区域、命令框或@mentioned调用消息扩展。

1. **元数据**。 调用消息传递扩展插件时，它可以标识用户和租户来自 `userId` 和 `tenantId`。 可在 `channelData` 对象中找到 `meetingId`。 你的应用可以使用 `userId` API 请求和 `GetParticipant` `meetingId` API 请求来检索用户角色。

1. **命令类型**。 如果消息扩展使用 [基于操作的命令](../messaging-extensions/what-are-messaging-extensions.md#action-commands)，则应遵循选项卡 [单一登录](../tabs/how-to/authentication/tab-sso-overview.md) 身份验证。

1. **用户体验**。 消息传递扩展的外观和行为应与会议外部相同。

## <a name="next-steps"></a>后续步骤

* [创建操作命令](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [创建搜索命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [链接展开](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a>了解详细信息

在快速入门中试用：

* C 快速入门#
  * [使用基于操作的命令进行消息传递扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [使用基于搜索的命令进行消息传递扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* JavaScript 快速入门
  * [使用基于操作的命令进行消息传递扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [使用基于搜索的命令进行消息传递扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

详细了解Teams开发概念：

* [了解Teams应用功能](../concepts/capabilities-overview.md)
* [什么是消息扩展？](../messaging-extensions/what-are-messaging-extensions.md)
