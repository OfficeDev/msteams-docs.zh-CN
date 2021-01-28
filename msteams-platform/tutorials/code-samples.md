---
title: 应用代码示例
description: Microsoft Teams 开发人员平台的示例应用程序的链接和说明
ms.topic: reference
keywords: Microsoft Teams 开发人员示例
ms.openlocfilehash: f51ffb22a5e6b3b757d1971422adf955d95fb223
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014108"
---
# <a name="tutorials-and-code-samples-for-the-microsoft-teams-developer-platform"></a>Microsoft Teams 开发人员平台的教程和代码示例

你将在此处找到教程和代码示例列表，这些教程和代码示例演示如何通过创建自定义应用来扩展 Teams 开发人员平台功能。

## <a name="getting-started-with-microsoft-learn"></a>Microsoft Learn 入门

| 功能| 学习模块|
|--------|-------------|
| 选项卡 — 嵌入式 Web 体验  |  [使用 Microsoft Teams 选项卡创建嵌入式 Web 体验](https://docs.microsoft.com/learn/modules/embedded-web-experiences/) |
| Webhook 和连接器  |  [使用 Webhook 和 Office 365 连接器将 Web 服务连接到 Microsoft Teams](https://docs.microsoft.com/learn/modules/msteams-webhooks-connectors/) |
|消息扩展  | [Microsoft Teams 中面向任务的交互与消息传递扩展](https://docs.microsoft.com/learn/modules/msteams-messaging-extensions/)  |
| 任务模块 |  [使用任务模块收集 Microsoft Teams 中的输入](https://docs.microsoft.com/learn/modules/msteams-task-modules/) |
| 对话机器人  | [为 Microsoft Teams 创建交互式对话机器人](https://docs.microsoft.com/learn/modules/msteams-conversation-bots/)  |

## <a name="getting-started-with-code-samples"></a>代码示例入门

若要从 GitHub 下载示例：

1. 选择下面列出的项目之一，在 GitHub 中打开该项目。
2. 选择 **"克隆"或"下载** "按钮并复制 URL
3. 在要安装示例项目的父目录中打开命令提示符
4. 运行 `git clone <pasted url>`

### <a name="for-netc-samples"></a>对于 .NET/C# 示例

我们的每个 .NET 示例包括一Visual Studio解决方案文件，该文件可以完全生成解决方案，包括还原 NuGet 包。

### <a name="for-nodejs-samples"></a>有关Node.js示例

我们提供了一packages.js文件，其中列出了示例的所有必需包。 只需 `npm install` 从项目目录中的命令行Node.js安装所需的包。 现在可以在代码代码中打开项目Visual Studio开始试验。

### <a name="for-other-samples"></a>对于其他示例

与始终一样，项目的自述文件应包含有关特定示例的特定需求详细信息。

## <a name="bots-using-the-v4-sdk"></a>自动程序 (v4 SDK) 

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

>[!TIP]
>访问 [Bot Framework 示例存储库](https://github.com/Microsoft/BotBuilder-Samples) ，查看针对 C#、JavaScript、TypeScript 和 Python 的 Microsoft Bot Framework v4 SDK 任务重点示例。

## <a name="messaging-extensions-using-the-v4-sdk"></a>使用 v4 SDK (消息扩展) 

| 示例 | 说明 | .NET Core | JavaScript | Python|
|--------|------------- |---|---|----|
| 邮件扩展 - 搜索 | 接受搜索请求并返回结果的消息扩展。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |
| 邮件扩展 - 操作 | 接受参数并返回卡片的邮件扩展。 此外，如何接收作为邮件扩展中的参数的转发邮件。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| 邮件扩展 - 身份验证和配置 | 具有配置页面、接受搜索请求和在用户登录后返回结果的邮件扩展。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) |
| 邮件扩展 - 操作预览 | 演示如何为消息传递扩展创建预览和编辑流。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/53.teams-messaging-extensions-action-preview) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/53.teams-messaging-extensions-action-preview) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/53.teams-messaging-extensions-action-preview) |
| 链接展开 | 执行链接取消链接的消息扩展。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/55.teams-link-unfurling) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/55.teams-link-unfurling) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/55.teams-link-unfurling) |


## <a name="outgoing-webhooks"></a>传出 Webhook

| 示例 | 说明
|--------|-------------
| [用于 C#/.NET 的传出 Webhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook) | 说明如何使用 C#/.NET 为 Microsoft Teams 创建传出 **Webhook。**
| [传出 Webhook for Node.js](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs) | 说明如何使用大约 50行代码为 Microsoft Teams 创建Node.js Webhook。

## <a name="connectors"></a>连接器

| 示例 | 说明
|--------|-------------
| [示例连接器Node.js](https://github.com/OfficeDev/microsoft-teams-sample-connector-nodejs) | 此示例以 Node.js 为例，展示了如何使用 GitHub 生成 Microsoft Teams 连接器，以生成连接器通知。
| [C#/.NET 的示例连接器](https://github.com/OfficeDev/microsoft-teams-sample-connector-csharp) | 此示例用 C# 编写，展示如何使用示例任务列表应用作为生成连接器通知的示例来构建 Microsoft Teams 连接器。 此示例还演示如何在连接器配置页中实现登录功能。 

## <a name="graph-api"></a>图形 API

| 示例 | 说明
|--------|-------------
| [Microsoft Graph API 示例](https://github.com/OfficeDev/microsoft-teams-sample-graph) | 这些示例演示如何使用 Microsoft Graph API 调用执行任务，例如从在 Microsoft Teams 外部运行的 Web 服务查询团队和频道。

### <a name="bot-framework-sdk-v3-samples"></a>Bot Framework SDK v3 示例

| 示例 | 说明 |
|--------|------------- |
| [适用于 C#/.NET 的示例自动程序](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/CSharp/Samples/Microsoft.Bot.Connector.Teams.SampleBot) | Bot Framework v3 示例|
| [自动程序示例Node.js](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams/tree/master/Node/samples) | Bot Framework v3 示例 |
