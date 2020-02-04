---
title: Microsoft 团队代码示例
description: Microsoft 团队开发人员平台的示例应用程序的链接和说明
keywords: Microsoft 团队开发人员示例
ms.openlocfilehash: eb7794e788f8eb39102ac874748e23d8621f281e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41672980"
---
# <a name="code-samples-for-the-microsoft-teams-developer-platform"></a>Microsoft 团队开发人员平台的代码示例

在这里，你将看到一个代码示例列表，这些示例演示 Microsoft 团队开发平台的各种功能，以及如何构建应用程序以利用这些功能。

## <a name="getting-samples"></a>获取示例

从 GitHub 下载我们的示例：

1. 选择下面列出的其中一个项目，并在 GitHub 中打开该项目。
2. 选择 "**克隆" 或 "下载**" 按钮并复制 URL
3. 在要将示例项目安装到的父目录中打开一个命令提示符
4. 以`git clone <pasted url>`

### <a name="for-netc-samples"></a>For .NET/c # 示例

我们的每个 .NET 示例都包含一个直观的 Visual Studio 解决方案文件，该文件可以完全生成解决方案，包括还原 NuGet 包。

### <a name="for-nodejs-samples"></a>对于 node.js 示例

我们提供了一个程序包. json 文件，其中列出了一个示例所需的所有程序包。 只需`npm install`从 node.js 项目目录中的命令行运行即可安装所需的程序包。 您现在可以在 Visual Studio Code 中打开项目并开始实验。

### <a name="for-other-samples"></a>有关其他示例

与往常一样，项目的自述文件应包含有关特定示例的特定需求的详细信息。

## <a name="get-started"></a>入门

| 示例 | 说明|
|--------|-------------|
| [使用 node.js 的 Microsoft 团队中的 Hello World](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) | 向你`Node.js`介绍基本应用程序功能的示例团队应用。|
| [Microsoft 团队中使用 c # .NET 的 Hello World 版](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) | 向你`C# .NET`介绍基本应用程序功能的示例团队应用。|
| [开始使用团队的 Yeoman 生成器](~/tutorials/get-started-yeoman.md) | 使用 Microsoft 团队的 Yeoman 生成器从头开始创建团队应用程序。 |

## <a name="bots-using-the-v4-sdk"></a>Bot （使用 v4 SDK）

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="messaging-extensions-using-the-v4-sdk"></a>邮件扩展（使用 v4 SDK）

| 示例 | 说明 | .NET Core | JavaScript |
|--------|------------- |---|---|
| 搜索命令 | 使用搜索命令的简单消息扩展 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|
| 操作命令 | 带有操作命令的简单消息扩展。 插入到撰写邮件区域的响应。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)|
| 带机器人响应的操作命令 | 带有操作命令的消息扩展。 由 bot 插入对话中的响应。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/53.teams-messaging-extensions-action-preview)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/53.teams-messaging-extensions-action-preview)|
| 搜索命令 | 带有搜索命令和身份验证和配置的消息扩展 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)|

## <a name="outgoing-webhooks"></a>传出 Webhook

| 示例 | 说明
|--------|-------------
| [C # 的传出 Webhook/.NET](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook) | 说明如何在 c #/.NET. 中为 Microsoft 团队创建**传出 Webhook**
| [Node.js 的传出 Webhook](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs) | 说明如何在 ~ 50 行的 node.js 代码中为 Microsoft 团队创建简单的**传出 Webhook** 。

## <a name="connectors"></a>连接器

| 示例 | 说明
|--------|-------------
| [Node.js 的示例连接器](https://github.com/OfficeDev/microsoft-teams-sample-connector-nodejs) | 此示例在 node.js 中编写，展示了如何使用 GitHub 为 Microsoft 团队构建连接器，作为生成连接器通知的示例。
| [C #/.NET 的示例连接器](https://github.com/OfficeDev/microsoft-teams-sample-connector-csharp) | 此示例以 c # 编写，展示了如何使用示例任务列表应用程序为 Microsoft 团队构建连接器，作为生成连接器通知的示例。

## <a name="graph-api"></a>Graph API

| 示例 | 说明
|--------|-------------
| [Microsoft Graph API 示例](https://github.com/OfficeDev/microsoft-teams-sample-graph) | 这些示例演示如何使用 Microsoft Graph API 调用执行任务，例如，通过在 Microsoft 团队外部运行的 web 服务查询团队和频道。

## <a name="others"></a>其他

| 代码 | 说明 |
|------|------------- |
| [Node.js 中的完整示例](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) | 本示例演示如何使用 Microsoft 团队平台的所有功能。 注意：此示例使用 Bot 框架 v3 SDK。|
| [C #/.NET 中的完整示例](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) | 本示例演示如何使用 Microsoft 团队平台的所有功能。 注意：此示例使用 Bot 框架 v3 SDK。 |
| [C #/.NET 中的业务线应用程序](https://github.com/OfficeDev/msteams-sample-line-of-business-apps-csharp) | 此存储库包含多个示例业务线应用程序，可用于灵感，也可用作要在其上生成的模板。 注意：这些示例使用的是 Bot 框架 v3 SDK。|
| ["待办" 列表示例选项卡应用程序](https://github.com/OfficeDev/microsoft-teams-sample-todo) | 此 node.js 示例展示了将现有 web 应用转换为选项卡的难易程度。 |
| [Orky](https://github.com/OfficeDev/Orky) | 您可以使用 Orky 在 Microsoft 团队中注册自己的本地 bot，并从任意位置执行脚本！ |
| [内部版本2017天气](https://github.com/OfficeDev/microsoft-teams-build2017-weather) | 过期. //Build 2017 会话的源代码，以将 "天气" 选项卡添加到之前在会话中生成的框架应用程序中。 |

### <a name="bot-framework-sdk-v3-samples"></a>Bot 框架 SDK v3 示例

| 示例 | 说明 |
|--------|------------- |
| [C #/.NET 的示例 bot](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/CSharp/Samples/Microsoft.Bot.Connector.Teams.SampleBot) | Bot 框架 v3 示例|
| [Node.js 的示例 bot](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/Node/samples) | Bot 框架 v3 示例 |
