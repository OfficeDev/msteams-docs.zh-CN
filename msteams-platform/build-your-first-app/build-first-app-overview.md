---
title: 入门 - 生成首个应用概述和先决条件
author: girliemac
description: 了解如何开始使用应用Microsoft Teams和设置环境。
ms.author: timura
ms.date: 03/18/2021
ms.topic: quickstart
ms.openlocfilehash: dae942be9383ef1e0a931d238e6148651f334ef5
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565877"
---
# <a name="get-started-with-microsoft-teams-app-development"></a>开始Microsoft Teams开发

生成一个简单的应用，了解Teams应用的基础知识。 一旦看到"Hello， World！"，请尝试阅读任何其他入门文章，详细了解常见工具、基本概念和高级功能。



## <a name="what-youll-learn"></a>您将了解哪些功能

* 快速启动并运行 Teams Toolkit 扩展Visual Studio Code扩展。 
* 使用 App Studio 配置应用。
* 熟悉开发人员Teams SDK。
* 请考虑Teams概念，如身份验证和设计最佳做法。

可以使用你选择Teams技术（例如，使用 CLI (命令行界面）生成) 。 但是，这些文章可帮助你开始使用以下推荐的工具和技术：

* Teams Toolkit，Visual Studio Code扩展
* React.js选项卡
* Node.js聊天机器人和消息扩展的扩展


## <a name="teams-app-fundamentals"></a>Teams应用基础

你可以为你自己Teams组织中的人员或世界各地人构建自定义应用。 在开始之前，你应该了解以下有关应用开发Teams概念：

### <a name="common-app-use-cases"></a>常见应用用例

自定义应用可以使用的Teams一些典型方案包括：

* 在客户端中嵌入基于 Web 的内容，如 Web 应用或Teams部分。
* 在另一个系统中快速查找信息，并添加到Teams对话。
* 直接从对话中的内容触发工作流和进程。

### <a name="app-capabilities-and-tools"></a>应用功能和工具

应用由一个或多个Teams和用户交互点。 你的开发工具集将因所需的功能而异。

| **应用功能**| **交互点** | **推荐的工具** | **SDK** | **技术堆栈** |
|--------|--------|--------|--------|--------|
| 选项卡 | 用户可在个人上下文和共享上下文中与嵌入的 Web 内容进行交互的空间。 | VS Code扩展Teams Toolkit Yeoman 生成器 | 团队 JavaScript 客户端 SDK | 常规 Web 技术 (HTML、CSS 和 JavaScript) 或 React.js |
| 机器人 | 在个人上下文和共享上下文中与用户交互的聊天机器人。 | VS Code扩展Teams Toolkit Yeoman 生成器 | Bot Framework SDK | Node.js、C# 或 Python | 
| 消息扩展 | 插入应用内容或处理消息而不离开对话的快捷方式。 | VS Code扩展Teams Toolkit Yeoman 生成器 | Bot Framework SDK | Node.js、C# 或 Python |

### <a name="teams-doesnt-host-your-app"></a>Teams不托管应用

当用户在 Teams 中安装你的应用时，他们只会安装一个包含配置文件 (也称为应用清单) 和应用的图标的应用包。 应用的逻辑和数据存储托管在其他地方，如开发期间 Azure Web 服务或 localhost。 Teams HTTPS 访问这些资源。

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="插图显示应用Teams指向云服务器中的应用逻辑。":::

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [生成并运行你的第一个Teams应用](../build-your-first-app/build-and-run.md)
