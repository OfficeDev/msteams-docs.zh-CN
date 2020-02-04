---
title: 运行和调试应用程序
description: 介绍运行和调试 Microsoft 团队应用程序所需的步骤
keywords: 团队运行调试应用程序
ms.topic: conceptual
ms.openlocfilehash: f7f49038617e0a6b8729df7fa53b97b63b3b3158
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673361"
---
# <a name="run-and-debug-your-microsoft-teams-app"></a>运行并调试 Microsoft 团队应用程序

Microsoft 团队应用可以包含一个或多个功能，以及运行甚至承载它们的方法可能会有所不同。 在进行调试时，通常有以下几种运行 Microsoft 团队应用程序的方法：

* **仅本地**&emsp;的 bot 可以在 bot 模拟器中测试您的体验。 对于其他内容，您可以在浏览器中本地运行，并通过`http://localhost`获取地址内容。
* **本地托管，在团队**&emsp;中这涉及使用隧道软件在本地运行，并创建要[上载](~/concepts/deploy-and-publish/apps-upload.md)到团队中[的包](~/concepts/build-and-test/apps-package.md)。 这使您可以轻松地在团队客户端中运行和调试应用程序。
* **云托管，在团队中**这真正模拟（或）对团队应用程序的生产级支持。 它涉及将您的解决方案上传到您的外部可访问服务器或云提供商（当然，我们建议 Azure）并[创建一个](~/concepts/build-and-test/apps-package.md)要[上载](~/concepts/deploy-and-publish/apps-upload.md)到团队中的包。

对于纯粹的本地或本地团队测试，可以从自己的计算机运行体验。 这使您可以在 IDE 中实际编译和运行，并充分利用断点和步骤调试等技术。 对于生产扩展调试和测试，我们建议您遵循自己的公司指南，以确保您能够通过您自己的过程来支持测试、暂存和部署。

通常，我们建议使用多个清单和包来维护生产和开发服务之间的分离。 例如，您可以选择注册单独的开发和生产 bot 并创建适当的程序包以将它们上载到测试环境中。 此外，我们还建议您在提交应用程序以供在我们的应用商店中发布或向客户分发之前，上载和测试生产包。

## <a name="purely-local"></a>纯本地

> [!NOTE]
> 以这种方式运行并不允许您访问团队应用功能或特定于团队的 bot 功能，如名单呼叫和其他特定于频道的功能。 此外，在 Microsoft 团队中运行时，您可能无法使用的 Bot 模拟器中的 Bot 框架允许某些功能。

你的 bot 可以在 Bot 模拟器中运行。 这使您可以测试 bot 的一些核心逻辑，查看邮件的粗略布局，并执行简单的测试。 步骤如下：

* 在本地运行代码
* 启动机器人仿真程序并设置 URL：
  * Node.js：`http://localhost:3978/api/messages`
  * .NET/C #：`http://localhost:3979/api/messages`
* 将 Microsoft 应用 ID 和 Microsoft 应用密码保留为空，以匹配默认环境变量。

## <a name="locally-hosted"></a>本地托管

由于 Microsoft 团队是完全基于云的产品，因此它要求其访问的所有服务都可公开使用 HTTPS 终结点。 因此，若要使您的应用程序能够在团队中工作，您需要将代码发布到您选择的云，或使我们的本地运行的实例可在外部访问。 可以使用隧道软件执行后一操作。

虽然您可以使用任何选择的工具，但我们使用并建议[ngrok](https://ngrok.com/download)，这将为您在计算机上本地打开的端口创建外部可寻址的 URL。 若要设置 ngrok 以准备在本地运行 Microsoft 团队应用程序，请执行以下操作：

* 在终端应用程序中，请转到安装了 ngrok 的目录。 您可能需要将其添加为 path 变量以避免这一步。
* 例如`ngrok http 3978 --host-header=localhost:3978`，运行，或根据需要替换端口号。

这将启动 ngrok 以侦听您指定的端口。 在 return 中，它为您提供一个外部可寻址的 URL，只要 ngrok 正在运行，它就会有效。

> [!NOTE]
> 如果您停止并重新启动 ngrok，则 URL 会发生更改。

若要在项目中使用 ngrok，并根据所使用的功能，必须将代码、configuration 和/或 .manifest 文件中的所有 URL 引用替换为使用此 URL 终结点。

例如，对于在 Microsoft Bot 框架中注册的 bot，请将 bot 的消息终结点更新为使用此新的 ngrok 终结点。 例如，`https://2d1224fb.ngrok.io/api/messages`。 您可以通过在 Bot 框架门户的 "测试聊天" 窗口中测试 bot 响应来验证 ngrok 是否正常工作。 （同样，与模拟器一样，此测试不允许您访问特定于团队的功能。）

> [!NOTE]
> 若要更新 bot 的消息终结点，必须使用 Bot 框架。 单击 bot[框架中的 bot 列表中的你的](https://dev.botframework.com/bots)机器人。 无需将你的 bot 迁移到 Microsoft Azure。 您还可以通过[应用程序 Studio](~/concepts/build-and-test/app-studio-overview.md)更新邮件终结点。

## <a name="cloud-hosted"></a>云托管

您可以使用任何外部可寻址服务来托管开发和生产代码及其 HTTPS 终结点。 您的功能不会预期驻留在同一服务上。 我们确实需要从 Microsoft 团队应用程序中访问的所有域都列在清单[`validDomains`](~/resources/schema/manifest-schema.md#validdomains) json 文件的对象中。

> [!NOTE]
> 为了确保安全环境，请明确了解您引用的确切域和子域，并且这些域必须在您的控制中。 例如， `*.azurewebsites.net`不建议这样做，但`contoso.azurewebsites.net`也不建议这样做。

## <a name="loading-and-running"></a>加载和运行

通常，若要在 Microsoft 团队中加载和运行你的体验，你需要创建一个包并使用以下指南将其上载到团队中：

* [为 Microsoft 团队应用程序创建包](~/concepts/build-and-test/apps-package.md)
* [在 Microsoft 团队中上传你的应用](~/concepts/deploy-and-publish/apps-upload.md)
