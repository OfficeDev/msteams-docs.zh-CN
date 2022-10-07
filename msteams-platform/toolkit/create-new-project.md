---
title: 新建 Teams 应用
author: zyxiaoyuer
description: 在本模块中，了解如何使用 Teams 工具包创建新的 Teams 应用
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 8ed7d882ba7d58862539e77bfc8b6ea5277a3729
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499242"
---
# <a name="create-a-new-teams-project"></a>创建新的 Teams 项目

本部分介绍如何使用 Visual Studio Code 和 Visual Studio 创建新的 Teams 项目。

::: zone pivot="visual-studio-code"

## <a name="create-a-new-teams-project-for-visual-studio-code"></a>为Visual Studio Code创建新的 Teams 项目

可以通过在 Teams 工具包中选择 **“创建新的 Teams 应用** ”来生成新的 Teams 项目。 可以在 Teams 工具包中创建以下类型的应用：

| 应用类型 | 定义 |
| --- | --- |
| 基本 Teams 应用 | 基本 Teams 应用是选项卡、机器人或消息扩展应用，可以根据需要创建和自定义该应用。 |
| 基于方案的 Teams 应用 | 基于方案的 Teams 应用是通知机器人、命令机器人、已启用 SSO 的选项卡或 SPFx 选项卡应用，适用于一个特定方案。 例如，通知机器人仅适用于发送通知而不用于聊天。 |

## <a name="create-a-new-teams-app"></a>新建 Teams 应用

创建新 Teams 应用的步骤与所有类型的应用（SPFx 和通知机器人除外）类似。 以下步骤可帮助你构建新的 Tab 应用：

**创建应用**

1. 打开 Visual Studio Code。

1. 选择左侧导航栏中的 Teams 工具包 :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: 图标。

1. 选择 **创建新的 Teams 应用**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/create-project.png" alt-text="Teams 工具包边栏中&quot;创建新项目&quot;链接的位置。":::

1. 确保 **选项卡** 已选中为应用功能。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-capabilities-tabapp.png" alt-text="选择应用功能":::

1. 选择 **JavaScript** 作为编程语言。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-language-tab.png" alt-text="显示如何选择编程语言的屏幕截图。":::

1. 选择 **默认文件夹** 以将项目根文件夹存储在默认位置。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-default-location.png" alt-text="选择默认位置":::

   以下步骤指导你更改默认位置：

      1. 选择 **“浏览**”。

          :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-browse.png" alt-text="选择浏览以进行存储":::

      1. 选择项目工作区的位置。

      1. 选择 **“选择文件夹**”。

          :::image type="content" source="../assets/images/teams-toolkit-v2/select-folder.png" alt-text="用于存储的 select-folder":::

1. 输入 `helloworld` 为应用程序名称。 确保仅使用字母数字字符。 选择“**Enter**”。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/enter-name-tab1.png" alt-text="显示在何处输入应用名称的屏幕截图。":::

1. 默认情况下，项目将在 10 秒内在新窗口中打开。 如果要在当前窗口中打开，请 **在当前窗口中选择“打开**”。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/new-window-notification.png" alt-text="新窗口通知":::

   Teams 选项卡应用在几秒钟内创建。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/tap-app-created1.png" alt-text="显示已创建应用的屏幕截图。":::

### <a name="directory-structure-for-different-app-types"></a>不同应用类型的目录结构

Teams 工具包提供用于生成应用的所有组件。 创建项目后，可以在 **资源管理器** 下查看项目文件夹和文件。

<br>
<details>
<summary><b>基本 Teams 应用的目录结构</b></summary>

你有三种不同类型的基本 Teams 应用，目录结构看起来与所有类型的应用类似。 以下示例演示基本的 Teams 选项卡应用目录结构：

| 文件夹名 | 目录 |
| --- | --- |
| `.fx/configs` | 用户可以为 Teams 应用自定义的配置文件。 |
| - `.fx/configs/config.<envName>.json` | 每个环境的配置文件。 |
| - `.fx/configs/azure.parameters.<envName>.json` | 适用于每个环境的 Azure BICEP 预配的参数文件。 |
| - `.fx/configs/projectSettings.json` | 适用于所有环境的全局项目设置。 |
| `tabs` | 运行时所需的 Tab 功能代码，例如隐私通知、使用条款和配置选项卡。 |
| - `tabs/src/index.jsx` | 前端应用的入口点，其中主应用组件随之呈现 `ReactDOM.render()` |
| - `tabs/src/components/App.jsx` | 用于处理应用中的 URL 路由的代码。 它调用了 [JavaScript 客户端 SDK](../tabs/how-to/using-teams-client-sdk.md) 应用和团队之间建立通信。 |
| - `tabs/src/components/Tab.jsx` | 用于实现应用 UI 的代码。 |
| - `tabs/src/components/TabConfig.jsx` | 用于实现配置应用的 UI 的代码。 |
| `templates/appPackage` | 应用清单模板文件和应用图标：color.png和outline.png。 |
| - `templates/appPackage/manifest.template.json` | 用于在本地或远程环境中运行应用的应用清单。  |
| `templates/azure` | BICEP 模板文件 |

> [!NOTE]
> 如果有机器人或消息扩展应用，则将相关文件夹添加到目录结构。

若要详细了解不同类型的基本 Teams 应用的目录结构，请参阅下表：

| 应用类型 | 链接 |
| --- | --- |
| 对于选项卡应用 | [使用 JavaScript 生成第一个选项卡应用](../sbs-gs-javascript.yml) |
| 对于机器人应用 | [使用 JavaScript 生成第一个机器人应用](../sbs-gs-bot.yml) |
| 对于消息扩展应用 | [使用 JavaScript 生成第一个消息传递扩展应用](../sbs-gs-msgext.yml) |

</details>
<br>
<details>
<summary><b>基于方案的 Teams 应用的目录结构</b></summary>

你有四种不同类型的基于方案的 Teams 应用，目录结构看起来与所有类型的应用类似。 以下示例演示基于方案的通知机器人 Teams 应用目录结构：

新的项目文件夹包含以下内容：

| 文件夹名 | 目录 |
| --- | --- |
| `.fx` | 项目级别设置、配置和环境信息 |
| `.vscode` | 本地调试的 VS 代码文件 |
| `bot` | 机器人源代码 |
| `templates` | Teams 应用清单和相应 Azure 资源的模板 |

**机器人** 文件夹中的核心通知实现及其包含：

| 文件名 | 目录 |
| --- | --- |
| `src/adaptiveCards/` | 自适应卡片的模板  |
| `src/internal/` | 为通知功能生成的初始化代码 |
| `src/index.*s` | 用于处理机器人消息和发送通知的入口点 |
| `.gitignore` | 要从机器人项目中排除本地文件的文件 |
| `package.json` | 机器人项目的 npm 包文件 |

> [!NOTE]
> 如果有命令机器人、启用 SSO 的选项卡或 SPFx 选项卡应用，则将相关文件夹添加到目录结构中。

若要详细了解不同类型的基于方案的 Teams 应用的目录结构，请参阅下表：

| 应用类型 | 链接 |
| --- | --- |
| 对于通知机器人应用 | [向 Teams 发送通知](../sbs-gs-notificationbot.yml) |
| 对于命令机器人应用 | [生成命令机器人](../sbs-gs-commandbot.yml) |
| 对于 SPFx 选项卡应用 | [使用 SPFx 构建 Teams 应用](../sbs-gs-spfx.yml) |

</details>
<br>
<details>
<summary><b>多功能应用的目录结构</b></summary>

可以使用添加功能将更多功能添加到现有 Teams 应用。 例如，如果将机器人应用添加到现有选项卡应用，Teams 工具包会添加包含相关文件和代码的机器人文件夹。

下图显示了 Tab 应用的目录结构：

   :::image type="content" source="../assets/images/teams-toolkit-v2/tabapp-directory.png" alt-text="Tab 应用目录结构":::

下图显示了具有机器人功能的 Tab 应用的目录结构：

   :::image type="content" source="../assets/images/teams-toolkit-v2/tab-app-with-bot-app.png" alt-text="具有机器人应用目录结构的 Tab 应用":::

</details>

::: zone-end

::: zone pivot="visual-studio"

## <a name="create-new-teams-app-in-visual-studio"></a>在 Visual Studio 中创建新的 Teams 应用

Teams 工具包在 Visual Studio 中提供 Microsoft Teams 应用模板以创建 Teams 应用。  可以在创建新项目时搜索并选择所需的 Teams 应用模板。 可以使用 Teams 应用模板来创建：

* Tab 应用
* 命令机器人
* 通知机器人
* 消息扩展应用

## <a name="prerequisites"></a>先决条件

| &nbsp; | 安装 | 用于使用... |
| --- | --- | --- |
| &nbsp; | **Required** | &nbsp; |
| &nbsp; | Visual Studio 版本 17.3 | 可以安装 Visual Studio 的企业版，并安装“ASP.NET”工作负荷和 Microsoft Teams 开发工具。 |
| &nbsp; | Teams 工具包 | 一个 Visual Studio 扩展，用于为应用创建项目基架。 使用最新版本。 |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | 通过聊天、会议、通话等应用与每一位同事进行协作的 Microsoft Teams - 一个地方完成所有操作。 |
 | &nbsp; | [准备 Microsoft 365 租户](../concepts/build-and-test/prepare-your-o365-tenant.md) | 对具有相应安装应用权限的 Teams 帐户的访问权限。 |

## <a name="create-a-new-teams-app"></a>新建 Teams 应用

创建新 Teams 应用的步骤与除通知机器人以外的所有类型的应用类似。 以下步骤可帮助你创建新的 Tab 应用：

1. 打开 Visual Studio。
1. 使用以下两个选项之一创建新项目。

     :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project1_1.png" alt-text="使用入门代码创建新项目":::

    * 在“**入门”** 下选择 **“创建新项目**”可帮助你选择具有代码基架的项目模板。
    * 选择 **“不使用代码继续** ”以创建没有代码基架的项目，然后在 Visual Studio 中选择 **“文件** > **新建** > **项目** ”。

        :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project2_1.png" alt-text="从文件菜单创建新项目":::

   将显示 **“创建新项目** ”窗口。  

1. 在搜索框中输入团队，然后从列表中选择 **Microsoft Teams 应用** ，然后选择 **“下一步**”。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/visual-studio.png" alt-text="搜索并选择 Microsoft Teams 应用":::

   将显示 **“配置新项目** ”窗口。

     :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-project-name_1.png" alt-text="为应用程序命名":::

    1. 为项目输入合适的名称。

         > [!NOTE]
         > 你输入的项目名称也会自动填充在 **解决方案名称** 中。 如果需要，可以更改解决方案名称，而不会影响项目名称。

    1. 选择要在其中创建项目工作区的文件夹路径。
    1. 如果需要，请输入其他解决方案名称。
    1. 如果需要，请检查将项目和解决方案保存在同一文件夹中的选项。 对于本教程，不需要此选项。
    1. 选择“**创建**”。

   将显示 **“创建新的 Teams 应用程序** ”窗口。

1. 在本教程中，选择 **Tab** 以创建新的团队应用程序并选择 **“创建**”。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-type_3.png" alt-text="选择 Teams 应用类型":::

   > [!NOTE]
   > 你可以为项目选择所需的 Teams 应用类型。

   随 **即** 会显示“**欢迎使用 Teams 工具包**”窗口的入门。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-getting-started-page.png" alt-text="选择入门团队工具包":::

### <a name="directory-structure"></a>目录结构

Teams 工具包提供用于生成应用的所有组件。 创建项目后，可以在资源管理器下查看项目文件夹和文件。

* **基本 Teams 应用的目录结构**

  :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project-solution-explorer_1.png" alt-text="选择解决方案资源管理器团队工具包的选项卡":::

* **基于方案的 Teams 应用的目录结构**

  :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project-solution-explorer.png" alt-text="选择解决方案资源管理器团队工具包":::

## <a name="teams-app-templates-in-teams-toolkit-for-visual-studio"></a>Teams Toolkit for Visual Studio 中的 Teams 应用模板

可以看到 Teams 工具包中已为各种 Teams 应用类型填充了 Teams 应用模板。 下表列出了所有可用的模板：

|Teams 应用模板  |说明  |
|---------|---------|
|通知机器人     |通知机器人应用可以向 Teams 客户端发送通知，可以通过多种方式触发通知。 例如，按 HTTP 请求或按时间触发通知。 还可以根据业务方案选择触发的通知。         |
|命令机器人     |用户可以键入命令以使用命令机器人应用与机器人交互。         |
|Tab     |Tab 应用在 Teams 中显示网页，并使用 Teams 帐户启用单一登录。         |
|消息扩展     |消息扩展应用实现简单的功能，例如创建自适应卡片、搜索 Nugget 包、展开“dev.botframework.com”域的链接。         |

> [!NOTE]
> 创建项目后，Teams 工具包会自动打开 **“入门”** 窗口。 现在可以在 **“入门** ”窗口中查看说明，并查看 Teams 工具包中的不同功能。

::: zone-end

## <a name="see-also"></a>另请参阅

* [使用 Blazor 构建 Teams 应用](../sbs-gs-blazorupdate.yml)
* [使用 C# 或 .NET 构建 Teams 应用](../sbs-gs-csharp.yml)
* [所有类型的环境和创建 Teams 应用的先决条件](tools-prerequisites.md)
* [准备使用 Microsoft Teams 工具包生成应用](build-environments.md)
* [使用 Visual Studio 预配云资源](provision-cloud-resources.md)
* [使用 Visual Studio 将 Teams 应用部署到云](deploy-teams-app.md)
