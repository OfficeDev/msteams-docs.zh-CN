---
title: Microsoft 团队代码示例
description: Microsoft 团队开发人员平台的示例应用程序的链接和说明
keywords: Microsoft 团队开发人员示例
ms.openlocfilehash: 955588608fde694b163104d0a9e9e94289719003
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "44801112"
---
# <a name="tutorials-and-code-samples-for-the-microsoft-teams-developer-platform"></a>Microsoft 团队开发人员平台的教程和代码示例

在这里，你将看到教程和代码示例的列表，这些示例演示如何通过创建自定义应用程序来扩展团队开发人员平台功能。

## <a name="getting-started-with-microsoft-learn"></a>Microsoft 学习入门

| 功能| 了解模块|
|--------|-------------|
| 选项卡—嵌入式 web 体验  |  [使用 Microsoft 团队的选项卡创建嵌入的 web 体验](https://docs.microsoft.com/learn/modules/embedded-web-experiences/) |
| Webhook 和连接器  |  [使用 webhook 和 Office 365 连接器将 web 服务连接到 Microsoft 团队](https://docs.microsoft.com/learn/modules/msteams-webhooks-connectors/) |
|消息传递扩展  | [Microsoft 团队中具有邮件扩展功能的面向任务的交互](https://docs.microsoft.com/learn/modules/msteams-messaging-extensions/)  |
| 任务模块 |  [使用任务模块在 Microsoft 团队中收集输入](https://docs.microsoft.com/learn/modules/msteams-task-modules/) |
| 对话 bot  | [为 Microsoft 团队创建交互式对话 bot](https://docs.microsoft.com/learn/modules/msteams-conversation-bots/)  |

## <a name="getting-started-with-code-samples"></a>代码示例入门

从 GitHub 下载我们的示例：

1. 选择下面列出的其中一个项目，并在 GitHub 中打开该项目。
2. 选择 "**克隆" 或 "下载**" 按钮并复制 URL
3. 在要将示例项目安装到的父目录中打开一个命令提示符
4. 以`git clone <pasted url>`

### <a name="for-netc-samples"></a>For .NET/c # 示例

我们的每个 .NET 示例都包含一个直观的 Visual Studio 解决方案文件，该文件可以完全生成解决方案，包括还原 NuGet 包。

### <a name="for-nodejs-samples"></a>对于 Node.js 示例

我们提供了一个文件 packages.js，其中列出了一个示例所需的所有程序包。 只需 `npm install` 从 Node.js 项目目录中的命令行运行即可安装所需的程序包。 您现在可以在 Visual Studio Code 中打开项目并开始实验。

### <a name="for-other-samples"></a>有关其他示例

与往常一样，项目的自述文件应包含有关特定示例的特定需求的详细信息。

## <a name="bots-using-the-v4-sdk"></a>Bot （使用 v4 SDK）

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

>[!TIP]
>访问[Bot 框架示例存储库](https://github.com/Microsoft/BotBuilder-Samples)，以查看 Microsoft Bot FRAMEWORK v4 SDK 以任务为中心的针对 c #、JavaScript、TypeScript 和 Python 的示例。

## <a name="messaging-extensions-using-the-v4-sdk"></a>邮件扩展（使用 v4 SDK）

| 示例 | 说明 | .NET Core | JavaScript | Python|
|--------|------------- |---|---|----|
| 搜索命令 | 使用搜索命令的简单消息扩展 | [查看](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)| [查看](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|[查看](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/50.teams-messaging-extension-search)|
| 操作命令 | 带有操作命令的简单消息扩展。 插入到撰写邮件区域的响应。 | [查看](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[查看](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)|[查看](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/51.teams-messaging-extensions-action)|
| 带机器人响应的操作命令 | 带有操作命令的消息扩展。 由 bot 插入对话中的响应。 | [查看](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/53.teams-messaging-extensions-action-preview)|[查看](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/53.teams-messaging-extensions-action-preview)|[查看](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/53.teams-messaging-extensions-action-preview)|
| 搜索命令 | 带有搜索命令和身份验证和配置的消息扩展 | [查看](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)| [查看](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)|[查看](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/52.teams-messaging-extensions-search-auth-config)|

## <a name="outgoing-webhooks"></a>传出 Webhook

| 示例 | 说明
|--------|-------------
| [C # 的传出 Webhook/.NET](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook) | 说明如何在 c #/.NET. 中为 Microsoft 团队创建**传出 Webhook**
| [Node.js的传出 Webhook](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs) | 说明如何在 ~ 50 Node.js 代码行中为 Microsoft 团队创建简单的**传出 Webhook** 。

## <a name="connectors"></a>连接器

| 示例 | 说明
|--------|-------------
| [Node.js的示例连接器](https://github.com/OfficeDev/microsoft-teams-sample-connector-nodejs) | 本示例在 Node.js 中编写，展示了如何使用 GitHub 为 Microsoft 团队构建连接器，作为生成连接器通知的示例。
| [C #/.NET 的示例连接器](https://github.com/OfficeDev/microsoft-teams-sample-connector-csharp) | 此示例以 c # 编写，展示了如何使用示例任务列表应用程序为 Microsoft 团队构建连接器，作为生成连接器通知的示例。

## <a name="graph-api"></a>Graph API

| 示例 | 说明
|--------|-------------
| [Microsoft Graph API 示例](https://github.com/OfficeDev/microsoft-teams-sample-graph) | 这些示例演示如何使用 Microsoft Graph API 调用执行任务，例如，通过在 Microsoft 团队外部运行的 web 服务查询团队和频道。

### <a name="bot-framework-sdk-v3-samples"></a>Bot 框架 SDK v3 示例

| 示例 | 说明 |
|--------|------------- |
| [C #/.NET 的示例 bot](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/CSharp/Samples/Microsoft.Bot.Connector.Teams.SampleBot) | Bot 框架 v3 示例|
| [Node.js的示例 bot](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/Node/samples) | Bot 框架 v3 示例 |
