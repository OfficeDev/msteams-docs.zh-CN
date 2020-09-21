---
title: 创建适合 Teams 的机器人
author: heath-hamilton
description: 了解如何在您的首个 Microsoft 团队应用程序中构建机器人。
ms.author: lajanuar
ms.date: 08/31/2020
ms.topic: tutorial
ms.openlocfilehash: f1307bcc7bb864ddfa97b9297f34fa4f7d5fcb0d
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964672"
---
# <a name="create-a-bot-for-teams"></a>创建适合 Teams 的机器人

您将在本教程中构建基本 *机器人* 应用程序。 Bot 充当团队用户与 web 服务之间的媒介。 用户可以与机器人聊天以快速获取信息或启动服务执行的工作流和任务。

## <a name="your-assignment"></a>您的分配

你的工作区已使用 [选项卡](../build-your-first-app/add-personal-tab.md) 在团队中呈现重要的联系人信息。 例如，同事可以快速访问技术支持电话号码。 而不是打电话，如果用户可以使用 chatbot 联系技术支持，该怎么办？ 你的老板要求你查看如何快速启动并在团队中运行基本的会话机器人。

## <a name="what-youll-learn"></a>你将了解的内容

> [!div class="checklist"]
>
> * 使用 Microsoft 团队工具包为 Visual Studio Code 创建一个应用程序项目和机器人
> * 确定应用程序清单属性和与 bot 相关的一些基架
> * 在本地托管 bot
> * 为团队配置机器人
> * 旁加载和测试团队中的 bot

## <a name="before-you-begin"></a>准备工作

如果尚未安装，请设置你的 Microsoft 365 开发 [帐户](building-real-world-app.md#set-up-your-development-account) 和 [团队应用工具](building-real-world-app.md#install-your-development-tools)。

## <a name="create-your-app-project-and-bot"></a>创建您的应用程序项目和机器人

Microsoft 团队工具包可帮助您为您的应用程序设置以下组件：

* **App 项目**：包括与 bot 相关的应用程序清单和基架
* **Bot**：配置新的 Bot 并使用 Microsoft Azure Bot 服务注册它

> [!TIP]
> 如果之前尚未创建团队应用程序项目，您可能会发现，请按照 [以下说明](../build-your-first-app/build-and-run.md) 更详细地说明项目。

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队**"， :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: 然后选择 " **创建新的团队应用**"。
1. 为你的团队应用输入名称。  (这是您的应用程序的默认名称，也是本地计算机上的应用程序项目目录的名称。 ) 
1. 在 " **添加功能** " 屏幕上，依次选择 **Bot** 和 " **下一步**"。
1. 选择 " **创建新的 Bot** 并 **登录** " 以使用 Microsoft 365 开发帐户登录。<br/>
:::image type="content" source="../doc-links/images/vsc-create-bot.png" alt-text="该图显示了如何在团队工具包中登录到 Microsoft 365 帐户以创建新的 bot。":::
1.  (可选) 输入你的 bot 的自定义名称，然后选择 " **创建**"。  (记住，这是你的 bot 的名称，而不是你已指定的团队应用程序的名称。 ) 
1. 选择屏幕底部的 " **完成** " 以配置项目。

## <a name="identify-relevant-app-project-components"></a>确定相关的应用程序项目组件

大多数应用程序清单和基架是在使用团队工具包创建项目时自动设置的。 我们来看看构建机器人的主要组件。

### <a name="app-manifest"></a>应用程序清单

应用程序清单中的以下代码片段 (`manifest.json` 项目目录中的文件 `.publish`) 显示与 bot 相关的属性和默认值。

```JSON
    "bots": [
        {
            "botId": "{botId0}",
            "scopes": [
                "personal",
                "groupchat",
                "team"
            ],
            "supportsFiles": false,
            "isNotificationOnly": false,
            "commandLists": [
                {
                    "scopes": [
                        "personal",
                        "groupchat",
                        "team"
                    ],
                    "commands": [
                        {
                            "title": "Hello",
                            "description": "Sends a hello message and @mention the sender"
                        }
                    ]
                }
            ]
        }
    ],
```

现在，让我们将重点放在以下必需属性上。  (查看受支持属性的完整列表 [`bots`](../../resources/schema/manifest-schema.md#bots) 。 ) 

* `botId`：你创建的你的项目设置的 bot 的 ID。  (存储在中 `{botId0}` ，则可以在中查找实际的 ID `Development.env` 。 ) 
* `scopes`：指定你的 bot 在 `personal` 、 `groupchat` 或 `team` (（即通道) 上下文中是否可用。
* `commands`：用户可以发送到你的 bot 的可用命令。
* `title`：用户在团队客户端中看到的 bot 命令名称。
* `description`：用于帮助用户了解 bot 命令执行的操作的语法和参数的简短说明或示例。

### <a name="app-scaffolding"></a>应用程序基架

应用程序基架提供一个 `botActivityHandler.js` 文件，该文件位于项目的根目录中，用于处理你的 bot 如何处理团队中的活动 (例如，bot 如何对特定邮件（如 "Hello" ) ）进行响应。

## <a name="set-up-a-secure-tunnel-to-your-app"></a>设置到您的应用程序的安全隧道

出于测试目的，让你将你的 bot 托管在本地 web 服务器上 (端口 3978) 。

1. 在终端中，运行 `ngrok http -host-header=rewrite 3978` 。
1. 在输出中复制 HTTPS URL，因为团队需要 HTTPS 连接。
1. 在 `.publish` 目录中，打开 `Development.env` 。
1. 将 `baseUrl0` 值替换为复制的 URL。  (例如，改 `baseUrl0=http://localhost:3000` 为 `baseUrl0=https://85528b2b3ca5.ngrok.io` 。 ) 

你的应用程序清单指向你承载机器人的位置。

## <a name="configuring-your-bot"></a>配置你的 bot

若要在团队中使用 bot，必须将其注册到 Azure Bot 服务。 幸运的是，当您使用团队工具包设置应用程序时，将自动完成此操作。

### <a name="add-the-bot-endpoint-address"></a>添加 bot 终结点地址

您必须指定接收和处理用户邮件的终结点 URL (例如，发送到 bot 的请求) 。 通常，URL 如下所示 `https://HOST_URL/api/messages` 。 您可以在团队工具包中快速配置此设置。

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队**"， :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: 然后选择 " **打开 Microsoft 团队工具包**"。
1. 转到 **Bot 管理 > 现有的 bot 注册** ，并选择在安装过程中创建的 bot。
1. 在 " **机器人终结点地址** " 字段中，输入承载机器人的本地 web 服务器，并 `/api/messages` 向其追加。

    :::image type="content" source="../doc-links/images/bot-config-endpoint-url.png" alt-text="图中显示可在团队工具包中配置 bot 终结点 URL 的位置。":::

你的 bot 将能够响应团队中的邮件。

## <a name="run-your-app"></a>运行应用程序

您已经设置了承载你的 bot 并将其配置为处理邮件的 URL。 现在是将你的 bot 准备好并运行了。

1. 在终端中，转到您的应用程序项目的根目录并运行该目录 `npm install` 。
1. 运行 `npm start` 。

如果成功，你会看到类似如下的消息，指示你的 bot 正在侦听你的活动 `localhost` ：

`Bot/ME service listening at http://localhost:3978`

## <a name="sideload-your-bot-in-teams"></a>在团队中旁加载你的机器人

在运行机器人的情况下，可以将其安装在团队中。

> [!TIP]
> 如果您在之前未旁加载团队应用程序并遇到问题，请按照这些 [说明](../build-your-first-app/build-and-run.md#sideload-your-app-in-teams)进行操作。

1. 使用允许应用旁加载的帐户登录到团队客户端。
1. 选择 " **应用**"，然后选择 " **上载自定义应用**"。
1. 转到您的应用程序项目 `.publish` 文件夹，然后选择 `Development.zip` 。
1. 在 "安装模式" 中，选择 " **添加** " 以安装您的应用程序。

## <a name="test-your-bot"></a>测试你的 bot

现在，为有趣部分：让我们在一对一聊天中说出 "Hello" 到你的机器人。

1. 在团队中，选择左侧的 " **更多**" :::image type="icon" source="../doc-links/images/teams-client-more.png"::: 。
1. 找到并选择您刚刚旁加载的 bot。<br/>
   :::image type="content" source="../doc-links/images/bot-teams-access.png" alt-text="图示显示在团队中访问机器人的位置。":::
1. 在 "撰写" 框中，发送一 `Hello` 封邮件。

你的 bot 将回复如下邮件等内容。

:::image type="content" source="../doc-links/images/contoso-chatbot.png" alt-text="显示用户将 "Hello" 发送到团队 bot 并获取响应的屏幕截图。":::

> [!NOTE]
> 如果在测试你的 bot 后进行代码更改（例如，更新），则 `botActivityHandler.js` 必须再次运行应用以查看团队中反映的更改。

## <a name="well-done"></a>干的好

恭喜你！ 您有一个基本的团队 bot，可以与用户一次或在组设置 (频道和聊天) 通信。

## <a name="troubleshooting"></a>故障排除

如果你在完成本教程时遇到问题，以下信息可能会有所帮助。

### <a name="toolkit-setup-fails"></a>工具包安装程序失败

使用 "团队" 工具包设置应用程序项目时，在选择 " **创建新的 Bot** " 选项并使用 Microsoft 365 开发帐户登录后，将会收到错误消息。

这可能是身份验证问题。 按照以下步骤完成对项目的设置。

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队**"， :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: 然后选择 " **注销**"。
1. 通过使用相同帐户登录并创建新的 bot，再次执行安装过程。

### <a name="bot-isnt-connected-to-teams"></a>机器人未连接到团队

如果您安装了应用程序，但机器人无法正常运行，请确保将 bot [连接到 Azure Bot 服务的团队 *频道*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。

请务必了解，这与团队中的频道不相同。 在这种情况下，通道是 Azure Bot 服务将你的 Bot 连接到团队或其他 [受支持的 Microsoft 或第三方通信应用程序](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)的方式。

## <a name="learn-more"></a>了解详细信息

* [请参阅其他团队 bot 可以使用 (GitHub 中的一个示例) ](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [自动程序对话基础知识](../../bots/how-to/conversations/conversation-basics.md)
* [团队中的 Bot 身份验证](../../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot 框架](https://dev.botframework.com/)
