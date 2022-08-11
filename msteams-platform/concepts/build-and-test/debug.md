---
title: 选择用于测试和调试应用的设置
description: 在本模块中，了解在本地和云托管环境中测试和调试 Microsoft Teams 应用的选项。
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: 5f2a53db5540656d3fd62047ed0fef9256ba62d6
ms.sourcegitcommit: 69a45722c5c09477bbff3ba1520e6c81d2d2d997
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/11/2022
ms.locfileid: "67312189"
---
# <a name="choose-a-test-setup-and-debug-your-teams-app"></a>选择测试设置并调试 Teams 应用

Microsoft Teams 应用包含一个或多个功能，而运行甚至托管它们的方法都不同。对于调试，请使用以下方法之一：

* **纯本地**：对于机器人，可以在机器人仿真器中测试体验。 对于其他内容，可在浏览器中本地运行，并通过 `http://localhost` 处理内容。
* **在 Teams 中进行本地托管**：这涉及在隧道软件中本地运行应用并 [创建包](~/concepts/build-and-test/apps-package.md)以 [上传](~/concepts/deploy-and-publish/apps-upload.md)到 Teams。 这允许你在 Teams 客户端中轻松运行和调试应用。
* **在 Teams 中进行云托管**：这真正模拟了对 Teams 应用的生产级别支持。 这涉及将解决方案上传到可从外部访问的服务器或云服务提供商，并[创建包](~/concepts/build-and-test/apps-package.md)以[上传](~/concepts/deploy-and-publish/apps-upload.md)到 Teams。

从自己的计算机运行体验，以进行纯本地或本地 Teams 测试。 通过执行此操作，可以在集成开发环境中编译和运行，并充分利用断点和步骤调试等技术。

> [!NOTE]
> 对于生产规模调试和测试，建议遵循你所在公司的指导方针，以确保能够通过自己的流程支持测试、暂存和部署。

使用多个清单和包，使生产服务和开发服务保持分离。 例如，可以选择注册单独的开发和生产机器人，并创建相应的包以在测试环境中上传它们。 我们还建议，在提交应用以在应用商店中发布或分发给客户之前，上传并测试生产包。

## <a name="purely-local"></a>纯本地

> [!NOTE]
> 在本地运行机器人无法访问 Teams 应用功能或特定于 Teams 的机器人功能，例如名单调用和其他特定于频道的功能。 此外，机器人模拟器中的 Bot Framework 允许某些功能在 Teams 中运行时可能无法正常工作。

可以在机器人仿真器中运行机器人。 这使你能够测试机器人的一些核心逻辑，查看消息的粗略布局，并执行简单测试。 操作步骤如下所示：

1. 在本地运行代码。
2. 启动机器人仿真器并设置 URL：
   * Node.js: `http://localhost:3978/api/messages`
   * .NET/C#： `http://localhost:3979/api/messages`
3. 将 Microsoft 应用 ID 和 Microsoft 应用密码留空，以匹配默认环境变量。

## <a name="locally-hosted"></a>本地托管

Teams 是一种完全基于云的产品，它要求其访问的所有服务都可使用 HTTPS 终结点公开提供。 因此，若要使应用在 Teams 中工作，需要将代码发布到所选云中，或使本地运行的实例可从外部访问。 我们可以使用隧道软件来实现后者。

尽管可以使用所选任何工具，但我们建议使用 [ngrok](https://ngrok.com/download)，它可为在计算机上本地打开的端口创建外部可寻址 URL。

若要设置 ngrok 以准备在本地执行 Teams 应用，请执行以下步骤：

1. 转到在终端应用程序中安装的 ngrok.exe 的目录。 你可能希望将其添加为路径变量以避免此步骤。
2. 例如，运行 `ngrok http 3978 --host-header=localhost:3978` 或根据需要替换端口号。
   这会启动 ngrok 以在指定的端口上列出。 作为回报，它为你提供了一个外部可寻址的 URL，只要 ngrok 正在运行，该 URL 就有效。

> [!NOTE]
> 如果停止并重新启动 ngrok，URL 会更改。

若要根据所使用的功能在项目中使用 ngrok，必须替换代码、配置和 manifest.json 文件中的所有 URL 引用才能使用此 URL 终结点。

对于在 Microsoft Bot Framework 中注册的机器人，请更新机器人的消息传递终结点以使用此新的 ngrok 终结点。 例如，`https://2d1224fb.ngrok.io/api/messages`。 可以通过在 Bot Framework 门户的“测试聊天”窗口中测试机器人响应来验证 ngrok 是否正常工作。 同样，与模拟器一样，此测试不允许你访问 Teams 特定的功能。

> [!NOTE]
> 若要更新机器人的消息传递终结点，必须使用 Bot Framework。 在 [Bot Framework 的机器人列表](https://dev.botframework.com/bots)中选择机器人。 无需将机器人迁移到 Microsoft Azure。 还可以通过 [Teams 开发人员门户](~/concepts/build-and-test/teams-developer-portal.md)更新消息传送终结点。

## <a name="cloud-hosted"></a>云托管

可以使用任何可外部寻址的服务来托管开发和生产代码及其 HTTPS 终结点。 不期望你的功能驻留在同一服务上。 我们需要从文件中的对象`manifest.json`中[`validDomains`](~/resources/schema/manifest-schema.md#validdomains)列出的 Teams 应用访问所有域。

> [!NOTE]
> 若要确保环境安全，请明确说明所引用的确切域和子域，并且这些域必须由你控制。例如，不建议使用 `*.azurewebsites.net`，但建议使用 `contoso.azurewebsites.net`。

## <a name="load-and-run-your-experience"></a>加载和运行体验

若要在 Teams 中加载和运行体验，需要创建包并将其上传到 Teams。 有关详细信息，请参阅：

* [为 Microsoft Teams 应用创建包](~/concepts/build-and-test/apps-package.md)。
* [在 Microsoft Teams 中上传应用](~/concepts/deploy-and-publish/apps-upload.md)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [向环境中添加测试数据](~/concepts/build-and-test/test-data.md)

## <a name="see-also"></a>另请参阅

[使用 IDE 在本地测试和调试机器人](../../bots/how-to/debug/locally-with-an-ide.md#test-and-debug-your-bot-locally-with-ide)

[适用于 Microsoft Teams 选项卡的 DevTools](../../tabs/how-to/developer-tools.md)
