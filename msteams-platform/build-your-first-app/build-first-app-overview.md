---
title: 入门 - 生成首个应用概述和先决条件
author: girliemac
description: 了解如何开始使用 Microsoft Teams 应用开发和设置环境。
ms.author: timura
ms.date: 03/18/2021
ms.topic: quickstart
ms.openlocfilehash: 3bc99c535ea659f046b65dc26d9a60de0dd49cab
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068563"
---
# <a name="get-started-with-microsoft-teams-app-development"></a>Microsoft Teams 应用开发入门

生成一个简单的应用，了解 Teams 应用开发的基本知识。 一旦看到"Hello， World！"，请尝试阅读任何其他入门文章，详细了解常见工具、基本概念和高级功能。



## <a name="what-youll-learn"></a>您将了解哪些功能

* 快速启动并运行 Teams Toolkit（Visual Studio代码扩展） 
* 使用 App Studio 配置应用 
* 熟悉 Teams 开发人员工具和 SDK
* 考虑重要的 Teams 应用概念，例如身份验证和设计最佳做法

可以使用你选择的任何技术生成 Teams 应用，例如，使用 CLI (命令行) 。 但是，这些文章可帮助你开始使用以下推荐的工具和技术：

* Teams Toolkit，Visual Studio代码扩展
* React.js选项卡
* Node.js聊天机器人和消息扩展的扩展


## <a name="teams-app-fundamentals"></a>Teams 应用基础

你可以为自己、组织中的人员或世界各地用户生成自定义 Teams 应用。 在开始之前，你应该了解以下有关 Teams 应用开发的基本概念：

### <a name="common-app-use-cases"></a>常见应用用例

自定义 Teams 应用可帮助的一些典型方案包括：

* 在 Teams 客户端中嵌入基于 Web 的内容，如 Web 应用或网站的一部分
* 在另一个系统中快速查找信息并添加到 Teams 对话 
* 直接从对话中的内容触发工作流和进程 

### <a name="app-capabilities-and-tools"></a>应用功能和工具

应用由一个或多个 Teams 功能和用户交互点决定。 你的开发工具集将因所需的功能而异。

| **应用功能**| **交互点** | **推荐的工具** | **SDK** | **技术堆栈** |
|--------|--------|--------|--------|--------|
| 选项卡 | 用户可在个人上下文和共享上下文中与嵌入的 Web 内容交互的空间 | 使用 Teams 扩展或 Yeoman Toolkit VS 代码 | 团队 JavaScript 客户端 SDK | 常规 Web 技术 (HTML、CSS 和 JavaScript) 或 React.js |
| 机器人 | 在个人上下文和共享上下文中与用户交互的聊天机器人 | 使用 Teams 扩展或 Yeoman Toolkit VS 代码 | Bot Franework SDK | Node.js、C# 或 Python | 
| 消息扩展 | 插入应用内容或处理邮件而不离开对话的快捷方式 | 使用 Teams 扩展或 Yeoman Toolkit VS 代码 | Bot Framework SDK | Node.js、C# 或 Python |

### <a name="teams-doesnt-host-your-app"></a>Teams 不托管你的应用

当用户在 Teams 中安装你的应用时，他们仅安装包含配置文件 (也称为应用清单) 应用图标的应用包。 应用的逻辑和数据存储托管在其他地方，如开发期间 Azure Web 服务或 localhost。 Teams 通过 HTTPS 访问这些资源。

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="插图显示 Teams 上的应用指向云服务器中的应用逻辑。":::

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [生成并运行你的第一个 Teams 应用](../build-your-first-app/build-and-run.md)
