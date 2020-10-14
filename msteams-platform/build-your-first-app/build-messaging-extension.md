---
title: 入门-构建消息扩展
author: heath-hamilton
description: 使用 Microsoft 团队工具包快速创建 Microsoft 团队消息扩展。
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: b19856eacee866ebbc89f21ac12575f1392918b3
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452832"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a>为 Microsoft 团队构建消息扩展

有两种类型的团队 *邮件扩展*： [搜索命令](../messaging-extensions/how-to/search-commands/define-search-command.md) 和 [动作命令](../messaging-extensions/how-to/action-commands/define-action-command.md)。

在本课中，您将创建一个 *搜索命令* (也称为 " *基于搜索的邮件扩展* ") ，这是查找外部内容并在团队中共享它的快捷方式。 用户可以从 " [团队撰写" 或 "命令" 框](../messaging-extensions/what-are-messaging-extensions.md)中访问搜索命令。

## <a name="your-assignment"></a>您的分配

您的组织的技术支持人员通过团队与用户通信，但票证驻留在单独的系统中。 这意味着支持人员必须在应用程序之间持续来回切换。 您将通过为工作组创建简单的基于搜索的邮件扩展功能，来研究如何减少这种更多的上下文切换。

## <a name="what-youll-learn"></a>你将了解的内容

> [!div class="checklist"]
>
> * 使用 Microsoft 团队工具包为 Visual Studio Code 创建应用程序项目和邮件扩展 bot
> * 标识应用程序清单属性和一些与邮件扩展相关的基架
> * 在本地托管应用程序
> * 为邮件扩展配置 bot
> * 旁加载和测试团队中的邮件扩展

## <a name="before-you-begin"></a>准备工作

如果还没有，请确保 [了解并安装团队开发先决条件](build-first-app-overview.md#get-prerequisites)。

## <a name="1-create-your-app-project"></a>1. 创建您的应用程序项目

Microsoft 团队工具包可帮助您为邮件扩展设置以下组件：

* 与邮件扩展相关的**应用程序清单和基架**
* 自动注册到 Microsoft Azure Bot 服务的邮件扩展的**Bot**

> [!TIP]
> 如果之前尚未创建团队应用程序项目，您可能会发现，请按照 [以下说明](../build-your-first-app/build-and-run.md) 更详细地说明项目。

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队**"， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **创建新的团队应用**"。
1. 为你的团队应用输入名称。  (这是您的应用程序的默认名称，也是本地计算机上的应用程序项目目录的名称。 ) 
1. 在 " **添加功能** " 屏幕上，依次选择 " **消息扩展** " 和 " **下一步**"
1. 在 " **配置消息扩展** " 屏幕上，执行以下操作：
    1. 为邮件扩展类型选择 " **基于搜索** 的选项"。
    1. 选择 " **创建新的 Bot** 并 **登录** " 以使用 Microsoft 365 开发帐户登录。
    1. 将你的 bot ID 和密码存储 (稍后需要一些) 。
    1.  (可选) 输入你的 bot 的自定义名称，然后选择 " **创建**"。  (这不是已指定的团队应用程序的名称。 ) 
    1. 现在，为 "链接 unfurling" 选择 " **否** " 选项。</br>
:::image type="content" source="../assets/images/build-your-first-app/choose-me-search.png" alt-text="演示如何在团队工具包中登录到 Microsoft 365 帐户，以创建用于邮件扩展的新 bot。&quot;:::
1. 选择屏幕底部的 &quot; **完成** " 以配置项目。

## <a name="2-identify-relevant-app-project-components"></a>2. 确定相关的应用程序项目组件

大多数应用程序清单和基架是在使用团队工具包创建项目时自动设置的。

### <a name="app-manifest"></a>应用程序清单

应用程序清单中的以下代码片段 (`manifest.json` 项目目录中的文件 `.publish`) 显示与邮件扩展相关的属性和默认值。

```JSON
"composeExtensions": [
    {
        "botId": "{botId0}",
        "canUpdateConfiguration": true,
        "commands": [
            {
                "id": "searchQuery",
                "context": [
                    "compose",
                    "commandBox"
                ],
                "description": "Test command to run query",
                "title": "Search",
                "type": "query",
                "parameters": [
                    {
                        "name": "searchQuery",
                        "title": "Search Query",
                        "description": "Your search query",
                        "inputType": "text"
                    }
                ]
            }
        ]
    }
],
```

让我们了解工具包为你创建的一些属性。  (查看受支持属性的完整列表 [`composeExtensions`](../resources/schema/manifest-schema.md#composeextensions) 。 ) 

* `botId`：你创建的你的项目设置的 bot 的 ID。  (存储在中 `{botId0}` ，则可以在中查找实际的 ID `Development.env` 。 ) 
* `commands`：邮件扩展的可用命令。 该工具包为您提供了搜索命令的基架。
* `context`：用户可以在其中调用邮件扩展。 在这种情况下，可以从 "团队撰写" 或 "命令" 框启动邮件扩展。
* `description`： UI 帮助文本，用于指示命令的用途或用法。
* `parameters`：包含所有参数一个命令接受 (必须至少有一个，并且最多可以有五个) 。
* `parameters.description`： UI 帮助文本，用于描述参数的用途或示例输入。

### <a name="app-scaffolding"></a>应用程序基架

应用程序基架包含一个 `.env` 文件，该文件位于项目的根目录中，用于存储邮件扩展机器人的 ID 和密码。

此外，在根目录中，还有一个 `botActivityHandler.js` 用于处理邮件扩展 (或技术方面的文件， [邮件扩展程序的 Bot](#4-configure-the-bot-for-your-messaging-extension)) 响应团队中的搜索查询。

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. 设置应用程序的安全隧道

出于测试目的，让我们在本地 web 服务器上托管您的邮件扩展 (端口 3978) 。

1. 在终端中，运行 `ngrok http -host-header=rewrite 3978` 。
1. 在输出中复制 HTTPS URL，因为团队需要 HTTPS 连接。
1. 在 `.publish` 目录中，打开 `Development.env` 。
1. 将 `baseUrl0` 值替换为复制的 URL。  (例如，改 `baseUrl0=http://localhost:3000` 为 `baseUrl0=https://85528b2b3ca5.ngrok.io` 。 ) 

您的应用程序清单指向你承载邮件扩展使用的 bot 的位置。

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. 配置邮件扩展的 bot

邮件扩展依靠 bot 来发送和处理从团队到托管服务的用户请求。

自动程序必须在 Azure Bot 服务中注册，这是在使用团队工具包设置应用程序时完成的。

### <a name="specify-your-bot-id-and-password"></a>指定你的 bot ID 和密码

在使用 Azure Bot 服务注册你的 bot 时，系统会为你的团队应用必须知道的 ID 和密码分配你的 bot。

1. 查找在工具包设置过程中存储的 bot ID 和密码。
1. 在您的根目录中，打开该 `.env` 文件。
1. 分别将机器人 ID 和密码分别设置为 `BotId` 和 `BotPassword` 属性。

### <a name="add-the-bot-endpoint-address"></a>添加 bot 终结点地址

您必须指定用于接收和处理邮件扩展中的搜索查询的 bot 终结点 URL。 通常，URL 如下所示 `https://HOST_URL/api/messages` 。 您可以在团队工具包中快速配置此设置。

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队**"， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **打开 Microsoft 团队工具包**"。
1. 转到 **Bot 管理 > 现有的 bot 注册** ，并选择在安装过程中创建的 bot。
1. 在 " **机器人终结点地址** " 字段中，输入您在其中承载机器人的本地 web 服务器 (`baseUrl10` 值) 并追加 `/api/messages` 到它。

你的 bot 将能够处理你的邮件扩展中的查询。

## <a name="5-run-your-app"></a>5. 运行您的应用程序

您已经设置了一个 URL 来托管您的邮件扩展并将其配置为处理搜索。 现在就可以启动并运行您的应用程序了。

1. 在终端中，转到您的应用程序项目的根目录并运行该目录 `npm install` 。
1. 运行 `npm start` 。

如果成功，你会看到类似于以下的消息，指示你的邮件扩展服务正在侦听以下内容中的活动 `localhost` ：

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>6. 旁加载您的邮件扩展在团队中

在邮件扩展运行的情况下，可以将其安装在团队中。

> [!TIP]
> 如果您在之前未旁加载团队应用程序并遇到问题，请按照这些 [说明](../build-your-first-app/build-and-run.md#5-sideload-your-app-in-teams)进行操作。

1. 使用允许应用旁加载的帐户登录到团队客户端。
1. 选择 " **应用**"，然后选择 " **上载自定义应用**"。
1. 转到您的应用程序项目 `.publish` 文件夹，然后选择 `Development.zip` 。
1. 在 "安装模式" 中，选择 " **添加** " 以安装您的应用程序。

## <a name="7-test-your-messaging-extension"></a>7. 测试邮件扩展

了解邮件扩展在团队聊天中的工作方式。

1. 启动新聊天。 在 "撰写" 框中，选择 " **更多** :::image type="icon" source="../assets/icons/teams-client-more.png"::: "，然后选择您刚刚旁加载的邮件扩展应用程序。<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-access.png" alt-text="演示如何在团队工具包中登录到 Microsoft 365 帐户，以创建用于邮件扩展的新 bot。&quot;:::
1. 选择屏幕底部的 &quot; **完成** " ) 。 如果你的应用程序正常运行，你将看到示例搜索结果 (你可以在以后添加自己的) 。<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="演示如何在团队工具包中登录到 Microsoft 365 帐户，以创建用于邮件扩展的新 bot。&quot;:::
1. 选择屏幕底部的 &quot; **完成** ":::

## <a name="well-done"></a>干的好

恭喜你！ 您有一个基本的工作组邮件扩展，它设置为在撰写或命令框中搜索外部内容。

## <a name="next-steps"></a>后续步骤

请参阅以下页面以继续操作并生成功能齐全的邮件扩展：

1. 定义与您的服务相关的[搜索命令](../messaging-extensions/how-to/search-commands/define-search-command.md)。
1. 将您的服务配置为 [响应用户的搜索](../messaging-extensions/how-to/search-commands/respond-to-search.md)。

## <a name="troubleshooting"></a>疑难解答

如果你在完成本教程时遇到问题，以下信息可能会有所帮助。

### <a name="toolkit-setup-fails"></a>工具包安装程序失败

使用 "团队" 工具包设置应用程序项目时，在选择 " **创建新的 Bot** " 选项并使用 Microsoft 365 开发帐户登录后，将会收到错误消息。

这可能是身份验证问题。 按照以下步骤完成对项目的设置。

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队**"， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **注销**"。
1. 通过使用相同帐户登录并创建新的 bot，再次执行安装过程。

### <a name="bot-isnt-connected-to-teams"></a>机器人未连接到团队

如果您安装了应用程序但不能正常运行，请确保消息扩展的 bot 已 [连接到 Azure Bot 服务的团队 *频道*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。

请务必了解，这与团队中的频道不相同。 在这种情况下，通道是 Azure Bot 服务将你的 Bot 连接到团队或其他 [受支持的 Microsoft 或第三方通信应用程序](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)的方式。

## <a name="learn-more"></a>了解详细信息

* [包含链接 unfurling 功能](../messaging-extensions/how-to/link-unfurling.md)
* [添加身份验证](../messaging-extensions/how-to/add-authentication.md)
* [创建基于操作的消息扩展](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft Bot 框架](https://dev.botframework.com/)
