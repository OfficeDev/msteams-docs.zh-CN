---
title: 创建适合团队的机器人
author: clearab
description: '了解如何创建 Teams 机器人 '
ms.topic: conceptual
localization_priority: Priority
ms.author: anclear
ms.openlocfilehash: 86ef162ceee07b1f66992d6943b22336d717c9f7
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452797"
---
# <a name="create-a-bot-for-microsoft-teams"></a>为 Microsoft Teams 创建自动程序

> [!TIP]
> 正在寻求更快的入门方式？ 使用 Microsoft Teams 工具包创建[机器人](../../build-your-first-app/build-bot.md)。

需要完成以下步骤才能创建对话自动程序：

1. 准备开发环境。
1. 创建 Web 服务。
1. 使用 Microsoft Bot Framework 将你的 Web 服务注册为自动程序。
1. 创建应用程序清单和应用程序包。
1. 将程序包上传到 Microsoft Teams。

可使用 Bot Framework 按照任何顺序创建 Web 服务、注册 Web 服务和创建应用程序包：但是，由于这三个部分交织在一起，因此无论按什么顺序执行操作，都需要返回以更新其他部分。 注册需要来自部署的 Web 服务的消息传递终结点，并且 Web 服务需要从注册中创建的 ID 和密码。 应用程序清单还需要注册 ID 才能将 Teams 连接到 Web 服务。

构建自动程序时，你将定期在更改应用程序清单与将代码部署到 Web 服务之间切换。 使用应用程序清单时，请记住，你可以手动操作 JSON 文件，也可以通过 App Studio 进行更改。 无论采用哪种方法，当你对清单进行更改时，都需要在 Teams 中重新部署（上传）你的应用；但是，在将更改部署到 Web 服务时无需这样做。

有关 Bot Framework 的其他信息，请参阅 [Bot Framework 文档](/azure/bot-service/)。

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>创建 Web 服务

自动程序的核心是 Web 服务。 它将定义用于接收所有请求的路由，通常为 `/api/messages`。 若要开始，可选择以下选项之一：

* 从采用 [C#/dotnet](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot) 或 [JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) 编写的 Teams 对话自动程序示例开始。
* 如果你使用的是 JavaScript，请使用[适用于 Microsoft Teams 的 Yeoman 生成器](https://github.com/OfficeDev/generator-teams)来搭建 Teams 应用，包括你的 Web 服务。 当构建包含多个对话自动程序的 Teams 应用时，它尤其有用。
* 从头开始创建 Web 服务。 可选择添加面向你的语言的 Bot Framework SDK，也可以直接使用 JSON 有效负载。

## <a name="register-your-web-service-with-the-bot-framework"></a>使用 Bot Framework 注册你的 Web 服务

> [!IMPORTANT]
> 注册 Web 服务时，请确保将**显示名称**设置为与应用程序清单中的**简短名称**相同的名称。 通过直接上传或利用组织的应用程序目录分发应用程序时，由自动程序发送到对话的消息将使用注册的**显示名称**，而不是应用程序的**简短名称**。

通过使用 Bot Framework 来注册 Web 服务，可在 Teams 客户端与 Web 服务之间建立安全的通信通道。 Teams 客户端与 Web 服务永远不会直接通信。 相反，消息通过 Bot Framework Service 进行路由（Microsoft Teams 使用此服务的单独实例，它符合 Office 365 标准）。

使用 Bot Framework 注册 Web 服务时，有两个选项可供选择。 可以使用 [App Studio](#using-app-studio) 或[旧门户](#in-the-legacy-portal)来注册你的自动程序，而无需使用 Azure 订阅。 或者，如果你已拥有 Azure 订阅（或者不介意创建一个），则可以使用 [Azure 门户](#with-an-azure-subscription)来注册 Web 服务。

### <a name="without-an-azure-subscription"></a>无 Azure 订阅

如果你不想在 Azure 中创建自动程序注册，则**必须**使用此链接 - https://dev.botframework.com/bots/new 或 App Studio。 如果单击 Bot Framework 门户中的“*创建自动程序*”按钮，将在 Microsoft Azure 中创建自动程序注册，并且需要提供 Azure 订阅。 若要在创建后管理注册或将其迁移到 Azure 订阅，请转到：https://dev.botframework.com/bots。

当你编辑未在 Azure 中注册的现有 Bot Framework 注册的属性时，你将看到“迁移状态”列和蓝色“迁移”按钮，该按钮会将你带到 Microsoft Azure 门户。 除非你希望这样做，否则不要选择“迁移”按钮。 相反，请选择自动程序的**名称**，然后可以编辑其属性：

   ![编辑自动程序属性](~/assets/images/bots/bf-migrate-bot-to-azure.png)

**必须**在 Azure 中注册自动程序（通过在 Azure 门户中创建或通过迁移）的应用场景：

* 你希望使用 Bot Framework 的 [OAuthPrompt](./authentication/auth-flow-bot.md) 进行身份验证。
* 你希望启用其他频道，例如网上聊天、Direct Line 或 Skype。

#### <a name="using-app-studio"></a>使用 App Studio

*App Studio* 是一种 Teams 应用程序，可帮助你构建 Teams 应用，包括将 Web 服务注册为自动程序、创建应用清单和应用包，以及更新设置和配置。 它还包含 React 控件库和卡的可配置示例。 请参阅[开始使用 Teams App Studio](../../concepts/build-and-test/app-studio-overview.md)。

请记住，如果使用 App Studio 注册你的 Web 服务，则需要转到 https://dev.botframework.com/bots 以管理你的注册。

#### <a name="in-the-legacy-portal"></a>在旧门户中

使用此链接创建自动程序注册：https://dev.botframework.com/bots/new。 **创建自动程序后，请确保从特色频道列表中将 Microsoft Teams 添加为频道。** 如果你已经创建应用程序包/清单，请随意重复使用你生成的任何 Microsoft 应用 ID。

   ![Bot Framework 注册页面](~/assets/images/bots/bfregister.png)

### <a name="with-an-azure-subscription"></a>拥有 Azure 订阅

你还可以通过在 Azure 门户中创建“自动程序频道注册”资源来注册 Web 服务。

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

[Bot Framework 门户](https://dev.botframework.com)已针对在 Microsoft Azure 中注册自动程序进行了优化。 以下是几个注意事项：

* 在 Azure 中注册的自动程序的 Microsoft Teams 频道是**免费**的。 通过 Teams 渠道发送的消息将不会计入自动程序使用的消息中。
* 如果你使用 Microsoft Azure 注册自动程序，则无需在 Microsoft Azure 上*托管*自动程序代码。
* 如果你使用 Microsoft Azure 门户注册自动程序，则必须拥有 Microsoft Azure 帐户。 你可以[免费创建一个](https://azure.microsoft.com/free/)。 若要在创建 Azure 帐户时验证你的身份，必须提供信用卡，但不会收费；在 Microsoft Teams 中创建和使用自动程序始终是免费的。

## <a name="create-your-app-manifest-and-package"></a>创建应用程序清单和程序包

[应用程序清单](~/resources/schema/manifest-schema.md)定义了应用程序的元数据、应用程序正在使用的扩展点以及指向这些扩展点连接到的 Web 服务的指针。 你可以使用 App Studio 帮助创建应用程序清单，也可以手动创建。

### <a name="add-using-app-studio"></a>使用 App Studio 添加

1. 在 Teams 客户端中，从左侧导航栏上的“**…**”溢出菜单中打开 App Studio。 如果尚未安装 App Studio，则可以通过搜索它来执行此操作。
2. 在“**清单编辑器**”选项卡上，选择“**创建新应用**”（或者，如果要将自动程序添加到现有应用中，则可以导入应用程序包）
3. 添加应用详细信息（有关每个字段的完整说明，请参阅[清单架构定义](~/resources/schema/manifest-schema.md)）。
4. 在“**自动程序**”选项卡上，选择“**设置**”按钮。
5. 你可以创建新的 Web 服务注册（**新自动程序**），或者如果已经注册了一个，请选择**现有自动程序**。
6. 选择自动程序所需的功能和作用域。
7. 如有必要，请更新自动程序终结点地址以指向你的自动程序。 它应该类似于 `https://someplace.com/api/messages`。
8. （可选）添加[自动程序命令](~/bots/how-to/create-a-bot-commands-menu.md)。
9. （可选）你可以从“**测试和分发**”选项卡下载完整的应用程序包。

### <a name="create-it-manually"></a>手动创建

与消息传递扩展和选项卡一样，你可以更新[应用程序清单](~/resources/schema/manifest-schema.md)以定义你的自动程序。 使用 `bots` 属性在你的应用程序清单中添加新的顶级 JSON 结构。

|姓名| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|字符串|64 个字符|✔|使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。 它可能与整个应用 ID 相同。|
|`needsChannelSelector`|布尔值|||描述自动程序是否利用用户提示将自动程序添加到特定频道。 默认值：`false`。|
|`isNotificationOnly`|布尔值|||指示自动程序是否为单向、仅通知的自动程序，而不是对话自动程序。 默认值：`false`。|
|`supportsFiles`|布尔值|||指示自动程序是否支持在个人聊天中上传/下载文件。 默认值：`false`。|
|`scopes`|枚举数组|3|✔|指定自动程序是在 `team` 内的频道上下文中提供体验、在群组聊天 (`groupchat`) 中提供体验，还是仅在单个用户 (`personal`) 范围内提供体验。 这些选项不具排他性。|

（可选）你可以定义由自动程序向用户推荐的一个或多个命令列表。 对象是一个数组（最多 2 个元素），所有元素的类型均为 `object`。 你必须为自动程序支持的每个作用域定义一个单独的命令列表。 有关详细信息，*请参阅*[自动程序菜单](./create-a-bot-commands-menu.md)。

|姓名| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`items.scopes`|枚举数组|3|✔|指定命令列表有效的作用域。 选项包括 `team`、`personal` 和 `groupchat`。|
|`items.commands`|对象数组|10|✔|自动程序支持的命令数组：<br>`title`：自动程序命令名称（字符串，32）<br>`description`：命令语法及其参数的简单描述或示例（字符串，128）|

#### <a name="simple-manifest-example"></a>简单清单示例

下面的示例是一个简单的自动程序对象，其中定义了两个命令列表。 这不是整个应用程序清单文件，只是特定于消息传递扩展的部分。

```json
...
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "scopes": [ "team", "personal", "groupchat" ],
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [ "team", "groupchat" ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command N",
              "description": "Description of Command N"
            }
          ]
        },
        {
          "scopes": [ "personal", "groupchat" ],
          "commands": [
            {
              "title": "Personal command 1",
              "description": "Description of Personal command 1"
            },
            {
              "title": "Personal command N",
              "description": "Description of Personal command N"
            }
          ]
        }
      ]
    }
  ],
...
```

#### <a name="create-your-app-package-manually"></a>手动创建应用程序包

若要创建应用程序包，你需要将应用程序清单和（可选）应用程序图标添加到 .zip 存档文件中。 有关完整详细信息，请参阅[创建应用程序包](~/concepts/build-and-test/apps-package.md)。 请确保 .zip 存档文件仅包含必需的文件，并且内部没有其他文件夹结构。

## <a name="upload-your-package-to-microsoft-teams"></a>将你的程序包上传到 Microsoft Teams

> [!NOTE]
> 要成功上传你的自动程序，你的租户管理员必须首先[允许在 Teams 中上传](/microsoftteams/manage-apps#manage-org-wide-app-settings)第三方或自定义应用。

如果你一直在使用 App Studio，则可以从**清单编辑器**的“**测试和分发**”选项卡中安装应用。 或者，你也可以通过以下方法安装应用程序包，即单击左侧导航栏中的 `...` 溢出菜单，单击“**更多应用**”，然后单击“**上载自定义应用**”链接。 你还可以将应用程序清单或应用程序包导入到 App Studio 中，以在上传之前进行其他更新。

## <a name="bots-in-teams-meetings"></a>Teams 会议的自动程序

Teams 支持在会议期间进行自动程序调用。 当你的自动程序收到调用消息时，它可以识别来自 `userId` 和 `tenantId` 的用户和租户。 可在 `channelData` 对象中找到 `meetingId`。 你的自动程序可以对 `GetParticipant` API 请求使用 `userId` 和 `meetingId` 来检索用户角色。

## <a name="next-steps"></a>后续步骤

* [自动程序对话基础知识](./conversations/conversation-basics.md)
* [订阅对话事件](./conversations/subscribe-to-conversation-events.md)
