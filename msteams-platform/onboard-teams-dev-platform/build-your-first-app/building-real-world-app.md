---
title: 开始构建你的第一个团队应用
author: heath-hamilton
ms.author: lajanuar
description: 构建您的首个 Microsoft 团队应用程序的概述和先决条件
ms.openlocfilehash: 9392096a285a43d3a1f8bed5020e3464da0f7f18
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964665"
---
# <a name="get-started-building-your-first-teams-app"></a>开始构建你的第一个团队应用

在 " **构建您的首个应用** 课程" 中，您将创建基本的团队应用程序。 每个教程演示如何构建一个简单、真实的团队应用程序，同时向您介绍了常见工具、基本概念以及一些更高级的功能。

## <a name="what-youll-learn"></a>你将了解的内容

下面介绍了学习课程后您知道的内容。

> [!div class="checklist"]
  >
  > * **使用团队工具包快速启动和运行**： Visual Studio 代码的 Microsoft 团队工具包负责创建您的应用程序项目和基架，以便您可以在几分钟内运行应用程序。
  > * **使用清单定义您的应用**程序：应用程序清单是指您在其中指定团队应用程序使用的功能和服务的位置。
  > * **确定您的应用程序访问群体的范围**：构建一个工作组应用程序以供个人使用、协作或同时使用这两者。
  > * **获取框架经验**：自定义您的应用程序 (例如，更改其配色方案以匹配团队主题) 与团队 JavaScript SDK 中的 "帮助"。 此外，了解用于创建和管理 bot 的常用工具。
  > * **在您的应用程序上展开**：在整个课程中，您将找到可能对 (（如身份验证和设计指南) ）感兴趣的相关主题。

## <a name="teams-app-fundamentals"></a>团队应用程序基础

在开始教程之前，您应该了解以下有关为团队生成应用程序的信息。

### <a name="apps-can-have-multiple-capabilities"></a>应用可以有多种功能

团队应用程序由一个或多个 [平台功能](../capabilities-overview.md)组成。 您可以使用大量的团队特定 [UI 组件和约定](../doc-links/teams-ui-conventions.md)（如卡片和任务模块）来显示这些功能。

### <a name="teams-doesnt-host-your-app"></a>团队不会托管您的应用程序

团队应用程序包含三个重要部分：

* 对应用程序加电的逻辑、数据存储和 API 调用。 这些服务不是由团队托管的，并且必须可通过 HTTPS 访问。
* 团队客户端 (web、桌面或移动) 上的用户使用您的应用程序。
* 您的应用程序包，可用于在团队中安装应用程序。 它包含应用程序元数据以及指向托管服务的指针。

## <a name="get-prerequisites"></a>获取先决条件

验证您是否具有用于生成团队应用程序的正确帐户，并安装一些建议的开发工具。

### <a name="set-up-your-development-account"></a>设置你的开发帐户

您需要一个允许自定义应用程序旁加载的团队帐户。  (你的帐户可能已提供此。 ) 

1. 如果您有团队帐户，请验证您是否可以在团队中旁加载应用程序：
    1. 在 "团队客户端" 中，选择 " **应用**"。
    1. 查找用于 **上传自定义应用程序**的选项。

    :::image type="content" source="../doc-links/images/upload-custom-app-closeup.png" alt-text="旁加载选项视图":::

<!-- markdownlint-disable MD033 -->
<details>

<summary>如果您看不到旁加载选项或没有团队帐户，<b>请选择此处</b>。</summary>

你可以通过加入 Microsoft 365 开发人员计划获取免费的团队测试帐户，以允许应用旁加载。  (注册过程大约需要两分钟时间。 ) 

1. 转到 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program)。
1. 选择 " **立即加入** "，然后按照屏幕上的说明操作。
1. 进入 "欢迎" 屏幕时，选择 " **设置 E5 订阅**"。
1. 设置管理员帐户。 完成后，您应该会看到类似这样的屏幕。
:::image type="content" source="../doc-links/images/dev-program-subscription.png" alt-text="开发计划订阅视图":::
1. 使用刚刚设置的管理员帐户登录到团队。
1. 验证您是否现在已 **上载自定义应用程序** 选项。

</details>

### <a name="install-your-development-tools"></a>安装开发工具

您可以使用您的首选工具构建团队应用程序，但这些课程展示了如何快速开始使用 Microsoft 团队工具包获取 Visual Studio Code。

团队仅通过 HTTPS 连接显示应用内容。 由于您将在本地托管第一个应用程序，因此您将了解如何使用 ngrok 在团队和您的应用程序之间 [设置安全隧道](../doc-links/debug.md#locally-hosted) 。

1. 安装 [Node.js](https://nodejs.org/en/)。
1. 安装最新版本的 [Visual Studio Code](https://code.visualstudio.com/download)。  (早期版本可能在工具包中不起作用。 ) 
1. 在 Visual Studio Code 中， **Extensions**选择 :::image type="icon" source="../doc-links/images/vs-code-extensions.png"::: 左侧活动栏上的 "扩展"，然后安装**Microsoft 团队工具包**。
    :::image type="content" source="../doc-links/images/vsc-install-toolkit.png" alt-text="安装工具包视图":::
1. 安装 [ngrok](https://ngrok.com/download)。

## <a name="next-step"></a>后续步骤

设置帐户和环境后，即可开始构建。

> [!div class="nextstepaction"]
> [生成并运行您的第一个应用程序](../build-your-first-app/build-and-run.md)
