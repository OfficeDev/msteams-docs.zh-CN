---
title: 开始构建第一个团队应用
author: heath-hamilton
description: 构建首个 Microsoft 团队应用程序的概述和先决条件
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: quickstart
ms.openlocfilehash: 14776b147309877212f710677ae5941238cf5c0d
ms.sourcegitcommit: 560bf433129c16888135879e2703dbdeb38ec99f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "48397692"
---
# <a name="build-your-first-teams-app-overview"></a>构建你的第一个团队应用概述

在 " **构建您的首个应用** 课程" 中，您将创建基本的团队应用程序。 每个教程演示如何构建一个简单的真实团队应用程序，同时向您介绍了常见工具、基本概念以及更高级的功能。

## <a name="what-youll-learn"></a>你将了解的内容

下面介绍了学习课程后您知道的内容。

> [!div class="checklist"]
  >
  > * **使用团队工具包快速启动和运行**： Visual Studio 代码的 Microsoft 团队工具包负责创建您的应用程序项目和基架，以便您可以在几分钟内运行应用程序。
  > * **使用清单定义您的应用**程序：应用程序清单是指您在其中指定团队应用程序使用的功能和服务的位置。
  > * **确定您的应用程序访问群体的范围**：构建一个工作组应用程序以供个人使用、协作或同时使用这两者。
  > * **获取团队框架的经验**：自定义应用 (例如，将其配色方案更改为与 "团队" 主题) 与团队 JavaScript SDK 中的 "帮助" 相匹配。 此外，了解用于创建和管理 bot 的常用工具。
  > * **在您的应用程序上展开**：在整个课程中，您将找到可能对 (（如身份验证和设计指南) ）感兴趣的相关主题。

## <a name="teams-app-fundamentals"></a>团队应用程序基础

在开始教程之前，您应该了解以下有关为团队生成应用程序的信息。

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a>应用可以具有多个功能和入口点

团队应用程序由一个或多个 [平台功能](../concepts/capabilities-overview.md) 和 [入口点](../concepts/extensibility-points.md)组成。 您可以使用大量的团队特定 [UI 组件和约定](../concepts/extensibility-points.md#ui-components)（如卡片和任务模块）呈现应用程序。

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

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="图显示了在团队中可以上载自定义应用程序的位置。&quot;:::

<!-- markdownlint-disable MD033 -->
<details>

<summary>如果您看不到旁加载选项或没有团队帐户，<b>请选择此处</b>。</summary>

你可以通过加入 Microsoft 365 开发人员计划获取免费的团队测试帐户，以允许应用旁加载。  (注册过程大约需要两分钟时间。 ) 

1. 转到 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program)。
1. 选择 &quot; **立即加入** &quot;，然后按照屏幕上的说明操作。
1. 进入 &quot;欢迎&quot; 屏幕时，选择 " **设置 E5 订阅**"。
1. 设置管理员帐户。 完成后，您应该会看到类似这样的屏幕。
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="图显示了在团队中可以上载自定义应用程序的位置。&quot;:::

<!-- markdownlint-disable MD033 -->
<details>

<summary>如果您看不到旁加载选项或没有团队帐户，<b>请选择此处</b>。</summary>

你可以通过加入 Microsoft 365 开发人员计划获取免费的团队测试帐户，以允许应用旁加载。  (注册过程大约需要两分钟时间。 ) 

1. 转到 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program)。
1. 选择 &quot; **立即加入** &quot;，然后按照屏幕上的说明操作。
1. 进入 &quot;欢迎&quot; 屏幕时，选择 ":::
1. 使用刚刚设置的管理员帐户登录到团队。
1. 验证您是否现在已 **上载自定义应用程序** 选项。

</details>

### <a name="install-your-development-tools"></a>安装开发工具

您可以使用您的首选工具构建团队应用程序，但这些课程展示了如何快速开始使用 Microsoft 团队工具包获取 Visual Studio Code。

团队仅通过 HTTPS 连接显示应用内容。 由于您将在本地托管您的第一个应用程序以节省时间，因此您将了解如何使用 ngrok 在团队和您的应用程序之间 [设置安全隧道](../concepts/build-and-test/debug.md#locally-hosted) 。  (生产级团队应用程序托管在云中。 ) 

1. 安装 [Node.js](https://nodejs.org/en/)。
1. 安装 [ngrok](https://ngrok.com/download)。
1. 安装最新版本的 [Visual Studio Code](https://code.visualstudio.com/download)。  (早期版本可能在工具包中不起作用。 ) 
1. 在 Visual Studio Code 中， **Extensions**选择 :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: 左侧活动栏上的 "扩展"，然后安装**Microsoft 团队工具包**。

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="图显示了在团队中可以上载自定义应用程序的位置。&quot;:::

<!-- markdownlint-disable MD033 -->
<details>

<summary>如果您看不到旁加载选项或没有团队帐户，<b>请选择此处</b>。</summary>

你可以通过加入 Microsoft 365 开发人员计划获取免费的团队测试帐户，以允许应用旁加载。  (注册过程大约需要两分钟时间。 ) 

1. 转到 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program)。
1. 选择 &quot; **立即加入** &quot;，然后按照屏幕上的说明操作。
1. 进入 &quot;欢迎&quot; 屏幕时，选择 ":::

## <a name="about-the-tutorials"></a>关于教程

你可以从任意团队开始 **构建你的第一个应用** 课程。 如果你不确定首先要转到的位置，请遵循初级友好路径，并构建一个 "Hello，World！" 应用程序.

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="图显示了在团队中可以上载自定义应用程序的位置。&quot;:::

<!-- markdownlint-disable MD033 -->
<details>

<summary>如果您看不到旁加载选项或没有团队帐户，<b>请选择此处</b>。</summary>

你可以通过加入 Microsoft 365 开发人员计划获取免费的团队测试帐户，以允许应用旁加载。  (注册过程大约需要两分钟时间。 ) 

1. 转到 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program)。
1. 选择 &quot; **立即加入** &quot;，然后按照屏幕上的说明操作。
1. 进入 &quot;欢迎&quot; 屏幕时，选择 " border="false":::

## <a name="next-step"></a>后续步骤

设置帐户和环境后，即可开始构建。

### <a name="beginner-friendly-tutorial"></a>初级友好教程

> [!div class="nextstepaction"]
> [构建 "Hello，World！" 应用程序](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a>其他教程

> [!div class="nextstepaction"]
> [创建机器人](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [创建邮件扩展](../build-your-first-app/build-messaging-extension.md)
