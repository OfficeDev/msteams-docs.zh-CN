---
title: 为 Microsoft 团队构建应用程序
author: clearab
description: 了解为 Microsoft 团队构建应用程序的典型过程。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 7c748829c481373dd7dfa011bfba4e7de3aba1bb
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673337"
---
# <a name="building-an-app-for-microsoft-teams"></a>为 Microsoft 团队构建应用程序

创建和分发在 Microsoft 团队平台上构建的应用程序涉及到确定要生成的内容、生成 web 服务、创建应用程序包以及将该包分发给目标最终用户。 由组织的管理员决定谁可以访问和安装您的应用程序，并将由您的用户在任何特定的上下文中安装您的应用程序。

## <a name="design-a-great-app"></a>设计出色的应用程序

为 Microsoft 团队创建成功应用程序的最重要步骤是选择适当的组合扩展性点和要利用的 UI 元素。 有时，这是一种非常简单的决策，但对于更复杂的应用程序，您应花大量时间来了解您尝试使用应用程序所做的问题，并将您的解决方案映射到用户可以在 Microsoft 中与您的应用程序交互的各种方式。团队客户端。 不要低估上下文和范围的重要性！ 在一对一聊天中运行良好的会话自动程序在群聊天或频道对话过程中可能不起作用。

1. 首先，[了解团队客户端扩展性点和](~/concepts/extensibility-points.md)可用于您的应用程序的 UI 元素。

2. 接下来，请务必[了解你的用例](~/concepts/design/understand-use-cases.md)。

3. 最后，将[用例映射到团队平台功能](~/concepts/design/map-use-cases.md)。

在决定了应用程序将利用哪些扩展性点和功能后，您将需要考虑这些交互中的每一项。 根据应用程序的设计，您可能需要查看以下内容：

* [设计极好的选项卡](~/tabs/design/tabs.md)
* [设计有用的对话 bot](~/bots/design/bots.md)

## <a name="prepare-your-environment"></a>准备环境

您需要确保您有一个可在其中上传和测试团队应用程序的环境。 如果您还没有已启用团队的 O365 订阅，并且可以将应用上传到它，则可以[注册 O365 开发人员计划](https://dev.office.com/devprogram)，从而为开发目的提供访问免费 Office 365 订阅的功能。

有关详细信息，请参阅[准备您的 O365 环境](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

## <a name="build-and-test-your-app"></a>生成和测试应用程序

生成和测试适用于 Microsoft 团队的应用程序与生成任何其他 web 应用程序没有什么不同。 主要区别在于，需要在应用程序包中使用应用程序清单将团队客户端连接到 web 服务。 每当您对应用程序清单进行更改时，您都需要重新上载应用程序包，并通过重新安装在团队中更新您的应用程序。 但是，在对 web 服务进行更改时，不需要在团队客户端中重新安装您的应用程序。

最初创建您的应用程序时，您将定期更新 web 服务和应用程序包，通常是在团队客户端中重新上载并多次安装应用程序（尤其是在初始安装应用程序期间）。 但是，由于你构建的稳定，更改应用清单的需求将会降低，并且你将主要对 web 服务进行更改。

### <a name="build-your-web-services"></a>生成 web 服务

一旦您决定了用户如何与您的应用程序进行交互，它就会生成 web 服务以对其进行电源的时间。 根据您创建的内容，团队将提供各种 Sdk、模板、代码示例和生成器来帮助您入门，其中包括：

* 用于[邮件扩展](~/messaging-extensions/what-are-messaging-extensions.md)和[对话 Bot](~/bots/what-are-bots.md)的 Bot 框架 SDK
* 用于[选项卡](~/tabs/what-are-tabs.md)和其他内容页的团队 JavaScript 客户端 SDK
* 用于在 node.js 中构建应用程序的[Yeoman 生成器](~/tutorials/get-started-yeoman.md)
* **预览**用于 web 内容页的一组开放源代码控件-[熟知 UI](https://microsoft.github.io/fluent-ui-react/)
* 现成的可供生产[应用程序模板](~/samples/app-templates.md)
* 帮助您入门的各种[示例](~/samples/code-samples.md)

请记住，您需要以一种方式承载 web 服务，从而使它们以公共方式通过 internet 访问（通常在云服务提供商（如 Azure）中），并通过 HTTPS 提供您的内容。

### <a name="create-your-app-package"></a>创建应用程序包

您还需要创建一个可在 Microsoft 团队中分发和安装的应用程序包。 应用程序包包含两个图标和一个 JSON 清单文件，其中描述了您的应用程序的元数据、您的应用程序正在使用的扩展点以及指向这些扩展点的服务的指针。

在创建应用程序包时，可以选择手动创建，也可以使用应用程序工作室（即团队内的应用程序）来帮助您创建团队应用程序（我们知道，非常多元）。 应用程序 Studio 将指导您创建您的应用程序清单，并可帮助您在 Bot 框架中注册你的 bot。 它还包含卡片设计器，可帮助您以可视化方式创建卡片和卡片操作，并将示例发送给团队中的自己。

## <a name="distributing-your-app"></a>分发应用程序

您有三个选项可用于[分发 Microsoft 团队应用程序](~/concepts/deploy-and-publish/apps-publish.md)，具体取决于您的目标访问群体。

* **直接共享您的应用程序包。** 您可以选择直接向用户共享您的应用程序包。 如果您的应用程序面向受限制的访问群体（只是几个团队或个人），以及在开发和测试应用过程中，这一点尤其有用。
  
* **将应用程序发布到组织应用程序目录。** 如果您的应用程序适用于特定组织（或者，如果您已经自定义了您的应用程序以满足组织的特定需求），租户管理员可将您的应用程序上传到组织的应用程序目录。 这使组织中的任何人都可以安装（但不会自动安装它）您的应用程序。
  
* **将应用程序发布到公用应用商店。** 如果您的应用程序适用于所有团队用户，则可以在公共应用商店中提交您的应用程序以供发布。 您需要执行严格的审阅过程，因此请确保您已将您的 t 与 t 相带点。

分发您的应用程序时，您需要考虑的不仅仅是您所需的访问群体，而是要与之共享您的应用程序的组织中的 IT 策略。 每个组织都可以完全控制如何确定要将哪些应用程序上载到其组织应用程序目录，以及哪些应用程序可从应用商店进行安装。

### <a name="the-app-you-create-versus-the-app-your-users-install"></a>您创建的应用程序与您的用户安装的应用程序

您的应用程序可以利用团队客户端中的多个扩展性点，并在各种范围内工作。 分发给用户的应用程序包将全部定义为单个实体。 但是，由于 Microsoft 团队中的所有应用安装都是*特定于上下文*的，因此并非始终为所有用户安装整个应用程序。

例如，假设您的应用程序包含一个在个人对话和团队对话中工作的对话机器人，以及一个个人选项卡和一个频道选项卡。安装应用程序后，它将安装在特定的上下文中-如果用户在团队中安装了应用程序，则无需安装应用程序的个人部分。 首先，这可能有点令人困惑，只需记住永远不要指望应用程序的所有部分都将在任何给定的上下文中安装和配置。

## <a name="get-started-quickly"></a>快速入门

想要快速开始？ 查看我们的入门教程之一，或查看针对特定平台功能（可在文档的每个功能部分中找到）的快速入门教程。

入门教程：

* [在 C 中构建 bot 和选项卡应用#](~/tutorials/get-started-dotnet-app-studio.md)
* [构建 JavaScript/node.js 中的 bot 和选项卡应用程序](~/tutorials/get-started-nodejs-app-studio.md)
* [使用 Yeoman 生成器创建应用程序](~/tutorials/get-started-yeoman.md)
