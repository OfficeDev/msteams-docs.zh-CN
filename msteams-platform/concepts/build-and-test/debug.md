---
title: 选择用于测试和调试应用的安装程序
description: 介绍用于测试和调试 Microsoft Teams 应用的选项
keywords: teams 运行调试应用
ms.topic: conceptual
ms.openlocfilehash: ea851a0d3ecf3ec87093bcc095050190a282c25e
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797797"
---
# <a name="choosing-a-setup-to-test-and-debug-your-microsoft-teams-app"></a>选择用于测试和调试 Microsoft Teams 应用的安装程序

Microsoft Teams 应用可以包含一个或多个功能，运行甚至托管这些功能的方式可能有所不同。 通常，对于调试，我们具有以下运行 Microsoft Teams 应用的方法：

* **纯本地** &emsp;对于机器人，可以在自动程序仿真器中测试你的体验。 对于其他内容，可以在浏览器中本地运行，并通过地址内容 `http://localhost` 运行。
* **本地托管，在 Teams 中** &emsp;这包括使用隧道软件在本地运行，并 [创建要](~/concepts/build-and-test/apps-package.md)上传到 Teams [的](~/concepts/deploy-and-publish/apps-upload.md)程序包。 这样，你可以轻松地在 Teams 客户端中运行和调试应用。
* **Teams 中的云托管** 这确实模拟 (或) Teams 应用的生产级支持。 它涉及将解决方案上载到可从外部访问的服务器或首选云提供商 (我们建议使用 Azure，当然，) 创建要上传到 Teams 的程序包。 [](~/concepts/build-and-test/apps-package.md) [](~/concepts/deploy-and-publish/apps-upload.md)

对于纯本地或本地 Teams 测试，你可以从自己的计算机运行体验。 这样，您实际上可以在 IDE 中编译和运行，并充分利用断点和步骤调试等技术。 对于生产规模调试和测试，建议您遵循自己的公司准则，以确保能够通过自己的流程支持测试、暂存和部署。

通常，我们建议使用多个清单和包，以允许您保持生产和开发服务之间的分离。 例如，你可以选择注册单独的开发和生产机器人，并创建适当的程序包以在测试环境中上载它们。 我们还建议你在提交应用以在我们的应用商店中发布或分发给客户之前上载和测试你的生产包。

## <a name="purely-local"></a>纯本地

> [!NOTE]
> 通过这种方法运行，你无法访问 Teams 应用功能或特定于 Teams 的自动程序功能，如名单呼叫和其他特定于频道的功能。 此外，自动程序仿真器中的自动程序框架可能允许某些功能，这些功能在 Microsoft Teams 中运行时可能无法正常工作。

机器人可以在自动程序仿真器中运行。 这使你能够测试机器人的一些核心逻辑，查看消息的粗略布局，并执行简单的测试。 步骤如下：

* 在本地运行代码
* 启动自动程序仿真器并设置 URL：
  * Node.js： `http://localhost:3978/api/messages`
  * .NET/C#： `http://localhost:3979/api/messages`
* 将 Microsoft 应用 ID 和 Microsoft 应用密码留空，以匹配默认环境变量。

## <a name="locally-hosted"></a>本地托管

由于 Microsoft Teams 是完全基于云的产品，因此它要求它访问的所有服务都使用 HTTPS 终结点公开提供。 因此，若要使你的应用在 Teams 中运行，你需要将代码发布到你选择的云，或使本地运行的实例可从外部访问。 我们可以使用隧道软件执行后者。

尽管可以使用任何选择的工具，但我们使用并推荐 [ngrok，](https://ngrok.com/download)这将为计算机上本地打开的端口创建外部可地址 URL。 若要设置 ngrok 以准备在本地运行 Microsoft Teams 应用：

* 在终端应用程序中，转到已安装ngrok.exe目录。 您可能需要添加它作为路径变量以避免此步骤。
* 例如，运行 `ngrok http 3978 --host-header=localhost:3978` 或根据需要替换端口号。

这将启动 ngrok 以侦听您指定的端口。 作为返回，它为你提供一个外部可地址 URL，只要 ngrok 正在运行，该 URL 就有效。

> [!NOTE]
> 如果停止并重新启动 ngrok，URL 将发生更改。

若要在项目中使用 ngrok，并且根据你使用的功能，必须替换文件的代码、配置和/或 manifest.js的所有 URL 引用，以使用此 URL 终结点。

例如，对于在 Microsoft Bot Framework 中注册的机器人，更新机器人的消息终结点以使用此新的 ngrok 终结点。 例如，`https://2d1224fb.ngrok.io/api/messages`。 可以通过在 Bot Framework 门户的"测试聊天"窗口中测试机器人响应来验证 ngrok 是否正常工作。  (，就像仿真器一样，此测试不允许你访问特定于 Teams 的功能。) 

> [!NOTE]
> 若要更新自动程序的消息终结点，必须使用 Bot 框架。 在 Bot Framework 中 [单击自动程序列表中的自动程序](https://dev.botframework.com/bots)。 无需将机器人迁移到 Microsoft Azure。 还可以通过 App Studio 更新消息 [终结点](~/concepts/build-and-test/app-studio-overview.md)。

## <a name="cloud-hosted"></a>云托管

可以使用任何外部可地址服务托管您的开发和生产代码及其 HTTPS 终结点。 您的功能不会驻留在同一个服务中。 我们要求从 Microsoft Teams 应用访问的所有域都列在文件上manifest.js[`validDomains`](~/resources/schema/manifest-schema.md#validdomains) 对象中。

> [!NOTE]
> 若要确保安全环境，请明确引用的确切域和子域，并且这些域必须在你的控制中。 例如， `*.azurewebsites.net` 不建议这样做，但 `contoso.azurewebsites.net` 建议这样做。

## <a name="loading-and-running"></a>加载并运行

通常，若要在 Microsoft Teams 中加载和运行体验，你需要按照以下指南创建一个程序包并将其上传到 Teams：

* [为 Microsoft Teams 应用创建程序包](~/concepts/build-and-test/apps-package.md)
* [在 Microsoft Teams 中上传应用](~/concepts/deploy-and-publish/apps-upload.md)
