---
title: 入门 - 生成你的第一个应用概述和先决条件
author: heath-hamilton
description: 了解如何开始 Microsoft Teams 应用开发和设置环境。
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 4288efdbfada5f1a51fa1d4aeccdd6cdf9c64382
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797895"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a>生成首个 Microsoft Teams 应用概述

在 **入门课程** 中，你将了解如何创建基本的 Teams 应用。 每个教程将介绍如何生成简单的实际 Teams 应用，同时向用户介绍通用工具、基本概念和更高级的功能。

## <a name="what-youll-learn"></a>您将了解哪些知识

下面将了解在学习课程后将了解哪些内容。

> [!div class="checklist"]
  >
  > * 使用 Teams Toolkit 快速启动并 **运行**：Microsoft Teams Toolkit for Visual Studio Code 负责创建应用项目和基架，以便你可以几分钟内拥有正在运行的应用。
  > * **使用 App Studio 配置应用**：指定 Teams 应用使用的功能和服务。
  > * **确定应用受众的范围**：生成用于个人使用和/或协作的 Teams 应用。
> * **获取 Teams 工具和 SDK** 体验：使用 Teams JavaScript 客户端 SDK 帮助自定义应用。 例如，更改应用的配色方案以匹配 Teams 主题。 此外，了解用于创建和管理机器人的常用工具。
  > * **在应用中展开**：在整个课程过程中，你将找到你可能感兴趣的相关主题，例如 (身份验证和设计) 。

## <a name="teams-app-fundamentals"></a>Teams 应用基础

在开始教程之前，你应了解以下有关生成 Teams 应用的信息。

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a>应用可以有多个功能和入口点

Teams 应用由一个或多个平台[功能 (用户](../concepts/capabilities-overview.md)如何使用应用) 以及 (使用应用应用的入口点) 。 [](../concepts/extensibility-points.md)

### <a name="teams-doesnt-host-your-app"></a>Teams 不托管你的应用

Teams 应用包括以下重要部分：

* 支持你的应用的逻辑、数据存储和 API 调用。 这些服务不是由 Teams 托管的，必须通过 HTTPS 访问。
* Teams 客户端 (Web、桌面或) ，用户可使用你的应用。
* 应用 ID，允许你使用 App Studio 配置应用。

## <a name="get-prerequisites"></a>获取先决条件

验证你拥有用于生成 Teams 应用和安装一些推荐的开发工具的合适帐户。

### <a name="set-up-your-development-account"></a>设置开发帐户

你需要允许自定义应用旁加载的 Teams 帐户。  (您的帐户可能已经提供此功能。) 

1. 如果你有 Teams 帐户，请验证你能否在 Teams 中旁加载应用：
    1. 在 Teams 客户端中，选择 **"应用"。**
    1. 查找用于上载 **自定义应用的选项**。

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="插图显示可以在 Teams 中在哪里上载自定义应用。":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><b>如果你</b> 看不到旁加载选项或没有 Teams 帐户，请在此处选择。</summary>

通过加入 Microsoft 365 开发人员计划，你可以获取允许应用旁加载的免费 Teams 测试帐户。  (注册过程大约需要两分钟。) 

1. 转到 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program)。
1. 选择 **"立即加入** "并按照屏幕上的说明操作。
1. 当你进入欢迎屏幕时，选择 **"设置 E5 订阅"。**
1. 设置管理员帐户。 完成后，你应该会看到如下所示的屏幕。
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="注册 Microsoft 365 开发人员计划后看到的示例。":::
1. 使用刚设置的管理员帐户登录到 Teams。
1. 验证你现在是否具有" **上载自定义应用"** 选项。

</details>

> [!Note]
> 如果仍无法旁加载应用，请参阅启用自定义 [Teams 应用并启用自定义应用上传](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。

### <a name="install-your-development-tools"></a>安装开发工具

可以使用首选工具生成 Teams 应用，但以下课程将展示如何快速开始使用 Microsoft Teams Toolkit for Visual Studio Code。

Teams 仅通过 HTTPS 连接显示应用内容。 若要在本地调试某些类型的应用（如机器人），你将了解如何使用 [ngrok](../concepts/build-and-test/debug.md#locally-hosted) 在 Teams 和应用之间设置安全隧道。  (Teams 生产应用托管在云中。) 

1. 安装 [Node.js](https://nodejs.org/en/)。
1. 如果计划构建自动程序或消息扩展，请安装[ngrok。](https://ngrok.com/download)
1. 安装最新版本的 [Visual Studio 代码](https://code.visualstudio.com/download)。  (早期版本可能无法使用 toolkit.) 
1. 在Visual Studio代码中，选择左侧活动栏上的"扩展"，然后 :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: 安装 Microsoft Teams **Toolkit。**

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="插图显示可在 Visual Studio Code 中安装 Microsoft Teams Toolkit扩展。":::

## <a name="about-the-tutorials"></a>关于教程

你可以从任何 Teams 入门课程 **开始** 。 如果你不确定首先从何处开始，请遵循初学者友好路径并构建一个"Hello， World！" 应用。

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="显示 Teams&quot;入门&quot;课程的学习路径的技能树。" border="false":::

## <a name="next-step"></a>后续步骤

设置帐户和环境后，就可以开始构建。

### <a name="beginner-friendly-tutorial"></a>初学者友好教程

> [!div class="nextstepaction"]
> [生成"Hello， World！"应用](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a>其他教程

> [!div class="nextstepaction"]
> [创建机器人](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [创建邮件扩展](../build-your-first-app/build-messaging-extension.md)
