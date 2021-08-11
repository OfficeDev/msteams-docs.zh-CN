---
title: 应用代码示例
description: 适用于开发人员平台的示例应用程序Microsoft Teams和说明
localization_priority: Normal
ms.topic: reference
keywords: Microsoft Teams开发人员示例
ms.openlocfilehash: 05884025f91377764d65242d501314c3798d3a73a430e103de885692c1e2ee63
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2021
ms.locfileid: "57709586"
---
# <a name="overview"></a>概述

本教程介绍如何使用 React、Blazor、SPFx、C# 或 .NET、Node.js 和 Yeoman 生成器创建应用。 你还将了解如何创建你的第一个机器人和消息传递扩展。 本教程将指导你完成选项卡、聊天机器人、消息传递扩展、Webhook 和连接器以及 Graph API 的多个代码示例，帮助你自定义和配置应用。 此外，还可以参阅 Microsoft Learn 部分，通过创建自定义应用Teams开发人员平台功能。  

## <a name="getting-started-with-microsoft-learn"></a>Microsoft Learn 入门

| **功能**| **学习模块**|
|--------|-------------|
| 选项卡 — 嵌入式 Web 体验  |  [为 Microsoft Teams 创建嵌入式 Web 体验（选项卡）](/learn/modules/embedded-web-experiences/) |
| Webhook 和连接器  |  [使用 Webhook 和 Office 365 连接器将 Web 服务连接到 Microsoft Teams](/learn/modules/msteams-webhooks-connectors/) |
|消息扩展  | [通过消息传递扩展在 Microsoft Teams 中进行以任务为导向的交互](/learn/modules/msteams-messaging-extensions/)  |
| 任务模块 |  [使用任务Microsoft Teams中收集输入](/learn/modules/msteams-task-modules/) |
| 对话机器人  | [为 Microsoft Teams 创建交互式对话机器人](/learn/modules/msteams-conversation-bots/)  |

## <a name="build-your-first-microsoft-teams-app-overview"></a>生成首个Microsoft Teams应用概述

在 **入门课程** 中，你将了解如何创建基本Teams应用。 每个教程将介绍如何生成简单的实际 Teams 应用，同时向用户介绍通用工具、基本概念和更高级的功能。

### <a name="teams-app-fundamentals"></a>Teams应用基础

开发人员[Teams允许你](../overview.md)生成自定义应用。 自定义 Microsoft Teams 应用可以帮助解决以下常见情况：

* 在 Teams 客户端中直接嵌入网站或 Web 应用。
* 帮助用户快速查找另一个系统中的信息，将结果添加到 Teams。
* 触发基于 Teams 中对话的工作流和流程，保留对话上下文。

在开始教程之前，你应了解以下内容，以生成适用于Teams。

### <a name="app-capabilities"></a>应用功能

A Teams app is made up of one or more [platform capabilities](../concepts/capabilities-overview.md) and [user interaction points](../concepts/extensibility-points.md).

根据应用所需的功能，你将需要相应的开发工具集。

|应用功能|用户交互|推荐的工具|SDK |技术堆栈| |--------|-------------||--------||--------||--------| |选项卡|全屏嵌入式 Web 体验。 |VS Code扩展Teams Toolkit或 YoTeams (Yeoman Generator) |[Teams客户端 SDK](/javascript/api/overview/msteams-client) |通常，HTML、CSS 和 JavaScript | |自动程序|与成员对话的聊天机器人。 |VS Code扩展Teams Toolkit或 YoTeams (Yeoman Generator) |[Bot Framework SDK](https://dev.botframework.com/) |Node.js、C# 或 Python | |邮件扩展|用于将外部内容插入对话或对邮件采取措施的快捷方式。 |VS Code扩展Teams Toolkit或 YoTeams (Yeoman Generator) |[Bot Framework SDK](https://dev.botframework.com/) |Node.js、C# 或 Python |

入门部分将介绍推荐的工具集和常用技术，例如 Visual Studio Code 和 Teams 扩展、React.js（适用于选项卡）和 Node.js（适用于机器人和消息传递扩展，尽管不限于使用这些特定 *堆栈）。*

如果你更喜欢使用命令行界面和 CLI (CLI) ，请参阅使用[Yeoman](../get-started/get-started-yeoman.md)Microsoft Teams创建你的第一个 Microsoft Teams 应用。

### <a name="teams-does-not-host-your-app"></a>Teams托管你的应用

你将仅将包含配置文件（称为清单和应用图标）的应用包安装到Teams客户端。 其余的应用逻辑和数据存储托管在其他地方，如 Azure Web 服务。 在开发过程中，云或 localhost 中的应用通过 HTTPS Teams访问。

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="插图显示应用Teams指向云服务器中的应用逻辑。":::

## <a name="see-also"></a>另请参阅

* [使用应用程序创建React](first-app-react.md)
* [使用 Blazor 创建应用](first-app-blazor.md)
* [使用应用程序创建SPFx](first-app-spfx.md)
* [使用或 C# .NET 创建应用](get-started-dotnet-app-studio.md)
* [使用Node.js创建应用](get-started-nodejs-app-studio.md)
* [使用 Yeoman 生成器创建应用](get-started-yeoman.md)
* [创建对话机器人应用](first-app-bot.md)
* [创建邮件扩展](first-message-extension.md)
* [代码示例](https://github.com/OfficeDev/Microsoft-Teams-Samples)