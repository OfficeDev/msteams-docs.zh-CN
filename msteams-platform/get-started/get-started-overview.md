---
title: 入门 - 概述
description: 开发人员文档入门Microsoft Teams概述
ms.localizationpriority: medium
ms.topic: reference
keywords: Microsoft Teams开发人员示例
ms.openlocfilehash: 9ab8014ad528aff9cfb0f4e271332981af3a8f29
ms.sourcegitcommit: 8935f54330c5685ff091f01e2b18c70502428054
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/28/2021
ms.locfileid: "61619800"
---
# <a name="get-started"></a>开始行动

欢迎使用开始构建和部署自定义应用Microsoft Teams！

演练构建基本的实际 Teams 应用的步骤。 入门还介绍了常用工具、基本概念以及更高级的功能。

以下是您将了解的一些概念：

- 快速启动并运行 Microsoft Teams Toolkit (扩展Visual Studio Code) 。
- 获取有关 Toolkit SDK 的体验。
- 配置和生成不同类型的 Teams 应用。

让我们快速浏览一下可以选择的生成环境选项，以及构建和部署应用Teams路线图。

:::image type="content" source="../assets/images/get-started/gs-build-options.png" alt-text="显示生成和部署应用程序的基本步骤的Teams示意图":::

## <a name="app-capabilities-and-development-tools"></a>应用功能和开发工具

根据应用需要的功能，选择相应的开发工具集。

| 应用功能 | 用户交互 | 推荐的工具 | SDK | 技术堆栈/语言 |
|--------|-------------|--------|--------|--------|
| 选项卡 | 全屏嵌入式 Web 体验。 | VS Code使用Teams Toolkit或[TeamsFx CLI（](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md)如果你更喜欢使用 CLI） | [适用于核心](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true)库的 TeamsFx [SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) Teams UI 功能的客户端 SDK | Web 技术通常包括 HTML、CSS 和 JavaScript (。React) 。 |
| 机器人 | 与成员对话的聊天机器人。 | VS Code扩展Teams Toolkit [TeamsFx CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [TeamsFx SDK](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) 和 [Bot Framework SDK](https://dev.botframework.com/) | Node.js、C#、Java 和 Python。 |
| 消息传递扩展 | 用于将外部内容插入对话或对邮件采取措施的快捷方式。 | VS Code扩展Teams Toolkit [TeamsFx CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [TeamsFx SDK](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) 和 [Bot Framework SDK](https://dev.botframework.com/) | Node.js、C#、Java 和 Python。 |

*不限于使用这些特定堆栈！*

如果你已熟悉 Yeoman 工作流，你可能更喜欢使用 [YoTeams Yeoman 生成器](https://github.com/pnp/generator-teams/blob/master/docs/docs/tutorials/build-your-first-microsoft-teams-app.md) 生成应用。

> [!NOTE]
> 如果你一直使用 App Studio，我们建议你尝试开发人员门户来配置、分发和管理你的Teams应用。


## <a name="build-your-first-teams-app"></a>生成首个Teams应用

现在，让我们生成你的第一个Teams应用。 但首先，选择语言 (框架) 准备开发环境。

> [!div class="nextstepaction"]
> [使用 Teams JavaScript 生成 React](../sbs-gs-javascript.yml)

> [!div class="nextstepaction"]
> [使用Teams生成SPFx](../sbs-gs-spfx.yml)

> [!div class="nextstepaction"]
> [使用 Teams 或 .NET C#应用](../sbs-gs-csharp.yml)

> [!div class="nextstepaction"]
> [使用Teams生成Node.js](../sbs-gs-nodejs.yml)

## <a name="see-also"></a>另请参阅

* [Microsoft Teams示例](https://github.com/OfficeDev/Microsoft-Teams-Samples#microsoft-teams-samples)
* [Git 和 GitHub 资源](/contribute/additional-resources)
