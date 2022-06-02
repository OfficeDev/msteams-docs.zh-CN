---
title: 入门 - 概述
description: 借助此学习路径，开始 Microsoft Teams 开发人员文档入门，其中介绍了常用工具、基本概念和高级功能。
ms.localizationpriority: high
ms.topic: reference
ms.openlocfilehash: a2dc779e24828ce73f9a93498bdcceecbdfe582b
ms.sourcegitcommit: b7b41ec2a1f022eb15a1980d1b31d22df1170913
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/01/2022
ms.locfileid: "65795152"
---
# <a name="get-started"></a>入门

欢迎访问“入门”，了解如何为 Microsoft Teams 构建和部署自定义应用！

演练构建基本、实际 Teams 应用的步骤。 “入门”还介绍了常用工具、基本概念以及更高级的功能。

下面概述了你将学习的内容：

- 快速启动并运行 Microsoft Teams 工具包（Visual Studio Code 的扩展程序）。
- 体验工具包和 SDK。
- 配置和构建不同类型的 Teams 应用。

让我们快速浏览一下可供选择的构建环境选项，以及构建和部署 Teams 应用的路线图。

:::image type="content" source="../assets/images/get-started/gs-build-options.png" alt-text="显示构建和部署 Teams 应用的基本步骤的插图":::

## <a name="app-capabilities-and-development-tools"></a>应用功能和开发工具

根据你希望应用具备的功能，选择适当的开发工具集。

| 应用功能 | 用户交互 | 推荐的工具 | SDK | 技术堆栈/语言 |
|--------|-------------|--------|--------|--------|
| 选项卡 | 全屏嵌入式 Web 体验。 | 带有 Teams 工具包扩展的 Microsoft Visual Studio Code，或 [TeamsFx CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md)（如果你更喜欢使用 CLI） | 用于核心库的 [TeamsFx SDK](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) 和用于 UI 功能的 [Teams 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) | Web 技术一般为 HTML、CSS 和 JavaScript（包括 React）。 |
| 机器人 | 与成员交谈的聊天机器人。 | 带有 Teams 工具包扩展的 Visual Studio Code，或 [TeamsFx CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [TeamsFx SDK](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) 和 [Bot Framework SDK](https://dev.botframework.com/) | Node.js、C#、Java 和 Python。 |
| 消息扩展 | 用于将外部内容插入对话或对邮件采取措施的快捷方式。 | 带有 Teams 工具包扩展的 Visual Studio Code，或 [TeamsFx CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) | [TeamsFx SDK](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) 和 [Bot Framework SDK](https://dev.botframework.com/) | Node.js、C#、Java 和 Python。 |

*不限于使用这些特定堆栈！*

如果你已经熟悉 Yeoman 工作流程，则可能更愿意使用 [YoTeams Yeoman Generator](https://github.com/pnp/generator-teams/blob/master/docs/docs/tutorials/build-your-first-microsoft-teams-app.md) 来构建应用。

> [!WARNING]
> 如果你一直使用 App Studio，我们建议你尝试使用开发人员门户来配置、分发和管理 Teams 应用。<br> App Studio 将于 2022 年 6 月 30 日弃用。

## <a name="build-your-first-teams-app"></a>构建首个 Teams 应用

现在，让我们来构建你的首个 Teams 应用。 但首先，请选择语言（框架）并准备开发环境。

> [!div class="nextstepaction"]
> [通过 JavaScript 使用 React 构建 Teams 选项卡应用](../sbs-gs-javascript.yml)
> [!div class="nextstepaction"]
> [通过 JavaScript 使用 React 构建 Teams 机器人应用](../sbs-gs-bot.yml)
> [!div class="nextstepaction"]
> [通过 JavaScript 使用 React 构建 Teams 消息扩展应用](../sbs-gs-msgext.yml)
> [!div class="nextstepaction"]
> [使用 Blazor 构建 Teams 应用](../sbs-gs-blazorupdate.yml)
> [!div class="nextstepaction"]
> [使用 SPFx 构建 Teams 应用](../sbs-gs-spfx.yml)
> [!div class="nextstepaction"]
> [使用 C# 或 .NET 构建 Teams 应用](../sbs-gs-csharp.yml)
> [!div class="nextstepaction"]
> [使用 Node.js 构建 Teams 应用](../sbs-gs-nodejs.yml)
> [!div class="nextstepaction"]
> [使用 JavaScript 生成通知机器人](../sbs-gs-notificationbot.yml)
> [!div class="nextstepaction"]
> [使用 JavaScript 生成命令机器人](../sbs-gs-commandbot.yml)
> [!div class="nextstepaction"]

## <a name="see-also"></a>另请参阅

* [Microsoft Teams 示例](https://github.com/OfficeDev/Microsoft-Teams-Samples#microsoft-teams-samples)
* [Git 和 GitHub 资源](/contribute/additional-resources)
