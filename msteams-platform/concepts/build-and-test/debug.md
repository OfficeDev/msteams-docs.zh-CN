---
title: 选择用于测试和调试应用的设置
description: 介绍在本地和云托管Microsoft Teams测试和调试应用的选项。
keywords: 团队运行调试应用本地云托管主机
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: eddcd41a7bebae183df079bc5dfe67deed65056e
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355704"
---
# <a name="choose-a-setup-to-test-and-debug-your-microsoft-teams-app"></a>选择用于测试和调试应用Microsoft Teams设置

Microsoft Teams应用包含一个或多个功能，并且运行甚至托管它们的方式是不同的。 对于调试，请使用以下方法之一：

* **纯本地**：对于自动程序，你可以测试在自动程序Emulator。 对于其他内容，可以在浏览器中本地运行，并通过 地址内容 `http://localhost`。
* **本地托管在 Teams**：这包括在隧道软件中本地运行应用，并创建要上传到 Teams。[](~/concepts/build-and-test/apps-package.md) [](~/concepts/deploy-and-publish/apps-upload.md) 这让你可以轻松地在客户端中运行和调试Teams应用。
* **云托管在Teams**：这真正模拟了对云应用的生产Teams支持。 它涉及将解决方案上载到您所选择的可从外部访问的服务器或云提供商，以及创建要[](~/concepts/build-and-test/apps-package.md)上传到 Teams。[](~/concepts/deploy-and-publish/apps-upload.md)

从你自己的计算机运行体验，以完全在本地或本地Teams测试。 通过执行此操作，可以在集成开发环境中编译和运行，并充分利用技术（如断点和步骤调试）。

> [!NOTE]
> 对于生产规模调试和测试，我们建议您遵循自己的公司准则，以确保能够通过自己的流程支持测试、暂存和部署。

使用多个清单和程序包保持生产和开发服务之间的分隔。 例如，你可以选择注册单独的开发和生产机器人，并创建相应的程序包以在测试环境中上载它们。 我们还建议你在提交应用以在我们的应用商店中发布或向客户分发之前上载和测试你的生产包。

## <a name="purely-local"></a>纯本地

> [!NOTE]
> 在本地运行自动程序不会授予你访问Teams或特定于Teams自动程序功能（如名单呼叫和其他特定于频道的功能）的访问权限。 此外，Bot 框架中的 Bot 框架还允许某些Emulator在自动程序运行时可能无法Microsoft Teams。

自动程序可以在自动程序Emulator。 这使你能够测试机器人的一些核心逻辑、查看消息的粗略布局和执行简单测试。 步骤如下：

1. 在本地运行代码。
2. 启动自动程序Emulator并设置 URL：
   * Node.js： `http://localhost:3978/api/messages`
   * .NET/C#： `http://localhost:3979/api/messages`
3. 将 Microsoft 应用 ID 和 Microsoft 应用密码留空，以匹配默认环境变量。

## <a name="locally-hosted"></a>本地托管

Microsoft Teams完全基于云的产品，它要求它访问的所有服务都使用 HTTPS 终结点公开提供。 因此，若要使应用在 Teams 中运行，你需要将代码发布到你选择的云，或使本地运行的实例可从外部访问。 我们可以使用隧道软件执行后者。

尽管可以使用你选择的任何工具，但我们使用并推荐 [ngrok](https://ngrok.com/download)，这将为计算机上本地打开的端口创建一个外部可地址 URL。

若要设置 ngrok 以准备在本地执行 Microsoft Teams 应用，请按照以下步骤操作：

1. 转到在终端应用程序中ngrok.exe的目录。 您可能需要将其添加为路径变量以避免此步骤。
2. 运行 ，例如 ， `ngrok http 3978 --host-header=localhost:3978`或根据需要替换端口号。
   这会启动 ngrok 以列出你指定的端口。 作为返回，它为你提供一个外部可地址 URL，只要 ngrok 正在运行，该 URL 就有效。

> [!NOTE]
> 如果停止并重新启动 ngrok，URL 将发生更改。

若要根据你使用的功能在项目中使用 ngrok，必须替换代码、配置和 manifest.json 文件的所有 URL 引用，以使用此 URL 终结点。

对于在 Microsoft Bot Framework 中注册的聊天机器人，更新机器人的消息终结点以使用此新的 ngrok 终结点。 例如，`https://2d1224fb.ngrok.io/api/messages`。 可以通过在 Bot Framework 门户的"测试"聊天窗口中测试自动程序响应来验证 ngrok 是否正常工作。 同样，与仿真器一样，此测试不允许你Teams特定功能。

> [!NOTE]
> 若要更新机器人的消息终结点，必须使用 Bot 框架。 在 Bot [Framework 中的自动程序列表中选择自动程序](https://dev.botframework.com/bots)。 无需将机器人迁移到Microsoft Azure。 您还可以通过 [App Studio](~/concepts/build-and-test/app-studio-overview.md) 更新消息终结点。

## <a name="cloud-hosted"></a>云托管

可以使用任何外部可地址服务来托管开发和生产代码及其 HTTPS 终结点。 无法预期你的功能驻留在同一个服务上。 我们要求从文件对象Microsoft Teams应用程序访问[`validDomains`](~/resources/schema/manifest-schema.md#validdomains)所有`manifest.json`域。

> [!NOTE]
> 若要确保安全环境，请明确引用的确切域和子域，这些域必须在你的控制中。 例如， `*.azurewebsites.net` 不建议使用 ，但 `contoso.azurewebsites.net` 建议这样做。

## <a name="load-and-run-your-experience"></a>加载并运行体验

若要在应用程序内加载Microsoft Teams体验，你需要创建一个程序包并将其上传到Teams。 有关详细信息，请参阅：

* [为应用创建Microsoft Teams包](~/concepts/build-and-test/apps-package.md)。
* [Upload应用中Microsoft Teams](~/concepts/deploy-and-publish/apps-upload.md)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [向环境中添加测试数据](~/concepts/build-and-test/test-data.md)

## <a name="see-also"></a>另请参阅

[在本地测试和调试机器人](../../bots/how-to/debug/locally-with-an-ide.md#test-and-debug-your-bot-locally)
