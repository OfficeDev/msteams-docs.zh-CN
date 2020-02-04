---
title: 创建邮件扩展
author: clearab
description: 如何为 Microsoft 团队应用程序创建邮件扩展插件。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 5d70ee361bdf32024f3cbdb56505a8aa410e7db0
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673496"
---
# <a name="create-a-messaging-extension-in-microsoft-teams"></a>在 Microsoft 团队中创建邮件扩展插件

在较高级别，需要完成以下步骤以创建邮件扩展。

1. 准备开发环境
2. 创建和部署 web 服务（在开发时使用隧道服务（如 ngrok）在本地运行它）
3. 使用 Bot 框架注册 web 服务
4. 创建应用程序包
5. 将你的包上传到 Microsoft 团队

可以按照任何顺序，创建 web 服务，创建应用程序包，并将您的 web 服务注册到 Bot 框架。 由于这三个部分如此 intertwined，无论你在哪种顺序中执行此操作，都需要返回以更新其他内容。 您的注册需要来自已部署的 web 服务的消息终结点，并且您的 web 服务需要从您的注册创建的 Id 和密码。 您的应用程序清单还需要该 Id 才能将团队连接到您的 web 服务。

在构建邮件扩展时，您将在更改应用程序清单和向 web 服务部署代码之间进行定期移动。 在使用应用程序清单时，请记住，可以手动操作 JSON 文件，也可以通过应用程序 Studio 进行更改。 无论哪种方式，在对清单进行更改时，都需要重新部署（上载）团队中的应用程序，但在将更改部署到 web 服务时，无需执行此操作。

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>创建 web 服务

您的邮件扩展的核心是您的 web 服务。 它将定义单个路由，通常`/api/messages`是接收上的所有请求。 如果你从头开始，你有几个选项可供选择。

* 使用我们的[快速入门](#learn-more)教程之一，它将指导您完成 web 服务的创建。
* 选择要从其开始的[Bot 框架示例存储库](https://github.com/Microsoft/BotBuilder-Samples)中提供的邮件扩展示例之一。
* 如果您使用的是 JavaScript，请使用[Microsoft 团队的 Yeoman 生成器](https://github.com/OfficeDev/generator-teams)搭建团队应用程序（包括 web 服务）。
* 从头开始创建 web 服务。 您可以选择为您的语言添加 Bot 框架 SDK，也可以直接使用 JSON 有效负载。

## <a name="register-your-web-service-with-the-bot-framework"></a>使用 Bot 框架注册 web 服务

邮件扩展利用 Bot 框架的邮件架构和安全通信协议;如果尚未安装，则需要在 Bot 框架上注册 web 服务。 Microsoft 应用程序 Id （我们将把它作为你在团队内部的 Bot Id，以从其他应用 Id 中识别它），并在你的邮件扩展中使用你的收银机框架注册的消息终结点，以接收和响应必需的uests. 如果使用的是现有注册，请确保[启用 Microsoft 团队频道](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0)。

如果您关注其中一个快速入门或从一个可用示例开始，则将通过注册 web 服务来指导您。 如果要手动注册服务，有三个选项可执行此操作。 如果你选择不使用 Azure 订阅进行注册，将无法利用 Bot 框架提供的简化 OAuth 身份验证流。 创建后，你将能够将注册迁移到 Azure。

* 如果你有 Azure 订阅（或想要创建一个新订阅），你可以使用 Azure 门户手动注册 web 服务。 创建 "Bot 通道注册" 资源。 您可以选择免费定价层，因为来自 Microsoft 团队的邮件不会将每个月的允许总邮件数计到每个月。
* 如果您不想使用 Azure 订阅，则可以使用[旧版注册门户](https://dev.botframework.com/bots/new)。
* 应用程序 Studio 还可以帮助你注册 web 服务（bot）。 通过应用程序 Studio 注册的 Web 服务未在 Azure 中注册。 您可以使用[旧版门户](https://dev.botframework.com/bots)查看、管理和迁移您的注册。

## <a name="create-your-app-manifest"></a>创建您的应用程序清单

您可以使用应用程序 Studio 来帮助您创建应用程序清单，也可以手动创建应用程序清单。

### <a name="create-your-app-manifest-using-app-studio"></a>使用应用程序 Studio 创建应用程序清单

您可以使用 Microsoft 团队客户端中的应用程序 Studio 应用来帮助创建应用程序清单。

1. 在团队客户端中，从左侧导航栏上**的 "...** " 溢出菜单中打开应用程序 Studio。 如果尚未安装，可以通过搜索来执行此操作。
2. 在 "**清单编辑器**" 选项卡上，选择 "**新建应用程序**" （或者，如果要向现有应用程序中添加邮件扩展，则可以导入应用程序包）
3. 添加应用程序详细信息（有关每个字段的完整说明，请参阅[清单架构定义](~/resources/schema/manifest-schema.md)）。
4. 在 "**邮件扩展**" 选项卡上，单击 "**设置**" 按钮。
5. 您可以创建新的 web 服务（机器人）以供您的邮件扩展使用，或者，如果您已经注册了一个，请在此处选择/添加一个。
6. 如有必要，请将你的 bot 终结点地址更新为指向你的 bot。 其外观应类似于`https://someplace.com/api/messages`。
7. "**命令**" 部分的 "**添加**" 按钮将指导您将命令添加到邮件扩展。 有关添加命令的详细信息，请参阅 "[了解更多](#learn-more)" 部分。 请记住，您最长可为邮件扩展定义10个命令。
8. 通过 "**邮件处理程序**" 部分，您可以添加将在其中触发消息的域。 有关详细信息，请参阅[link unfurling](~/messaging-extensions/how-to/link-unfurling.md) 。

在 "**完成 => 测试和分布**" 选项卡上，您可以**下载**应用程序包（包括您的应用程序清单和应用程序图标），也可以**安装**程序包。

### <a name="create-your-app-manifest-manually"></a>手动创建应用程序清单

与 bot 和选项卡一样，您可以更新应用程序[清单](~/resources/schema/manifest-schema.md#composeextensions)以包含邮件扩展属性。 这些属性控制您的邮件扩展在 Microsoft 团队客户端中的显示和行为。 从清单的1.0 版开始，支持邮件扩展。

#### <a name="declare-your-messaging-extension"></a>声明消息扩展

若要添加消息扩展，请在应用程序清单中将新的顶级 JSON 结构包含在`composeExtensions`属性中。 您可以为您的应用程序创建一个单一的邮件扩展，最长可包含10个命令。

> [!NOTE]
> 清单将邮件传递扩展作为`composeExtensions`引用。 这是为了保持向后兼容性。

扩展定义是一个具有以下结构的对象：

| 属性名称 | 用途 | 是否必需？ |
|---|---|---|
| `botId` | 与 Bot 框架一起注册的 bot 的唯一 Microsoft 应用 ID。 通常应与整个团队应用程序的 ID 相同。 | 是 |
| `canUpdateConfiguration` | 启用 "**设置**" 菜单项。 | 否 |
| `commands` | 此消息扩展支持的命令数组。 限制为10个命令。 | 是 |

#### <a name="define-your-commands"></a>定义命令

您的邮件扩展应声明一个或多个命令，这些命令定义用户可以触发邮件扩展的位置和交互的类型。 有关消息扩展命令的详细信息，请参阅[了解详细](#learn-more)信息。

#### <a name="simple-manifest-example"></a>简单清单示例

下面的示例是包含搜索命令的应用程序清单中的一个简单的消息扩展对象。 这不是整个应用程序清单文件，只是特定于邮件扩展的部件。 有关完整示例，请参阅[应用部件清单](~/resources/schema/manifest-schema.md)（manifest）架构。

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

## <a name="add-your-invoke-message-handlers"></a>添加调用消息处理程序

当用户触发邮件扩展时，您需要处理初始调用邮件，收集用户的某些信息，然后处理该信息并做出相应的响应。 若要执行此操作，首先需要决定要向邮件扩展中添加的命令类型，并[添加操作命令](~/messaging-extensions/how-to/action-commands/define-action-command.md)或[添加搜索命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)。

## <a name="next-steps"></a>后续步骤

* [创建操作命令](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [创建搜索命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [链接 unfurling](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a>了解更多

在快速入门中试用：

* 适用于 C 的快速入门#
  * [带有基于操作的命令的消息扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [包含基于搜索的命令的邮件扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* 适用于 JavaScript 的快速入门
  * [带有基于操作的命令的消息扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [包含基于搜索的命令的邮件扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

了解有关邮件扩展的详细信息概念：

* [了解团队应用程序功能？](~/concepts/extensibility-points.md)
* [什么是邮件扩展？](~/messaging-extensions/what-are-messaging-extensions.md)
