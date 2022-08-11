---
title: Visual Studio 的 Teams 工具包概述
author: surbhigupta
description: 在本模块中，了解适用于 Visual Studio 的 Teams 工具包概述
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
ms.openlocfilehash: 0f51d2c44eef3ec09d48581a797c63d501be8644
ms.sourcegitcommit: f192d7685ee3ddf4a55dc9787d56744403c3f8f9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/10/2022
ms.locfileid: "67302449"
---
# <a name="teams-toolkit-overview-for-visual-studio"></a>Visual Studio 的 Teams 工具包概述

适用于 Visual Studio 的 Teams 工具包可帮助你创建、调试和部署 Microsoft Teams 应用。 适用于 Visual Studio 的 Teams 工具包是 Visual Studio 2022 版本 17.3 中的正式版。 使用 Teams 工具包进行应用开发具有以下优点：

* 集成标识
* 对云存储的访问权限
* 来自 Microsoft Graph 的数据
* 采用零配置方法的 Azure 和 Microsoft 365 服务

对于 Teams 应用开发，还可以使用 [CLI 工具](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md)，类似于包含 Toolkit `teamsfx`的适用于 Microsoft Visual Studio 的 Teams 工具包代码。

Teams 工具包将生成 Teams 应用所需的所有工具放在一个位置。

> [!NOTE]
> Teams 工具包在其他版本中不可用。

## <a name="user-journey-of-teams-toolkit"></a>Teams 工具包的用户旅程

Teams 工具包可自动执行手动工作，并提供 Teams 和 Azure 资源的极佳集成。 下图显示了用户旅程：

:::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-user-journey.png" alt-text="Teams 工具包用户旅程":::

此旅程的主要里程碑包括：

1. 可以首先创建新项目或尝试生成示例 Teams 应用。
1. 然后，可以根据需要编辑代码或清单文件。
1. 若要生成和调试 Teams 应用，可以使用 Microsoft 365 帐户。
1. 若要预配应用并将其部署到云，可以使用 Azure 帐户。
1. 你最终可以将应用发布到 Teams。

## <a name="install-teams-toolkit-for-visual-studio"></a>安装 Visual Studio 的 Teams 工具包

可以从 [Visual Studio 下载页下载最新的 Visual Studio 安装](https://visualstudio.microsoft.com/vs/preview/)程序。

> [!NOTE]
> 安装 Visual Studio 之前，需要先安装 Visual Studio 安装程序。

打开 Visual Studio 安装程序后，在弹出的工作负荷窗口中。

1. 选择 **ASP.NET 和 Web 开发** 工作负载的框。
1. 在安装详细信息面板中选择 **“Microsoft Teams 开发工具** ”框。
1. 选择“安装”。

   :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-install1.png" alt-text="Visual studio-installation":::

1. 选择 **“启动** ”以打开 Visual Studio。

    :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-launch.png" alt-text="启动 visual Studio":::

   > [!IMPORTANT]
   > 建议下载 Visual Studio 2022 版本 17.3.0，因为适用于 Visual Studio 的 Teams 工具包在此版本中为 GA。 本文适用于 Visual Studio 2022 版本 17.3.0。 Teams 工具包版本 17.3.* 或更高版本。

## <a name="take-a-tour-of-teams-toolkit"></a>了解 Teams 工具包

安装 Teams 工具包后，可以简要了解 Teams 工具包的不同菜单选项：

1. 选择 **“项目**”。
1. 选择 **Teams 工具包**。
1. 现在可以访问 **Teams 工具包菜单** 选项。

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu.png" alt-text="Teams 工具包操作菜单":::

   还可以从解决方案资源管理器访问 Teams 工具包菜单。

4. 右键单击 **你的项目**。
5. 选择 **Teams 工具包** > **Teams 工具包菜单** 选项。

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu1.png" alt-text="Project 中的 Teams 工具包操作":::

   > [!NOTE]
   > 在此方案中，项目名称为 **MyTeamsApp1**。

可以在适用于 Visual Studio 的 Teams 工具包上执行以下函数：

|功能  |说明  |
|---------|---------|
|创建 Teams 项目     |在 Visual Studio 中使用 Teams 模板创建 Teams 项目         |
|准备 Teams 应用依赖项     |执行本地调试之前，它可帮助你设置本地调试依赖项并在 Teams 平台中注册 Teams 应用。 需要 Microsoft 365 帐户。 有关详细信息，请参阅 [使用 Visual Studio 在本地调试 Teams 应用](debug-teams-app-visual-studio.md)         |
|打开清单文件     |若要打开 Teams 清单文件，可以将鼠标悬停在参数上以预览值。 有关详细信息，请参阅 [使用 Visual Studio 编辑 Teams 应用清单](VS-TeamsFx-preview-and-customize-app-manifest.md)         |
|Teams 开发人员门户中的更新清单     |更新清单文件时，只能将清单文件重新部署到 Azure，而无需再次部署整个项目。 使用此命令将更改更新为远程。 有关详细信息，请参阅 [使用 Visual Studio 编辑 Teams 应用清单](VS-TeamsFx-preview-and-customize-app-manifest.md)       |
|预配到云     |此选项可帮助你创建托管 Teams 应用的 Azure 资源。 有关详细信息，请参阅 [使用 Visual Studio 预配云资源](provision-cloud-resources.md)        |
|部署到云     |此选项可帮助你将代码复制到“预配到云”时创建的 Azure 资源。 有关详细信息，请参阅 [使用 Visual Studio 将 Teams 应用部署到云](deploy-teams-app.md)        |
|Teams 中的预览版     |此选项启动 Teams Web 客户端，并允许你在其浏览器中预览 Teams 应用。         |
|Zip 应用包     |此选项在项目下的文件夹中 `Build` 生成 Teams 应用包。 可以将包上传到 Teams 客户端并运行 Teams 应用。         |

与 Teams Toolkit for Visual Studio Code 相比，Visual Studio 的 Teams 工具包尚不支持以下操作，但计划在未来的产品路线图中执行这些操作。

* 将其他 Teams 功能添加到 Teams 应用。
* 将更多 Azure 资源添加到 Teams 应用
* 向 Teams 应用添加单一登录。
* 将 API 连接添加到 Teams 应用。
* 自定义 Azure AD 清单。
* 添加 CI/CD 管道。
* 管理多个云环境。
* 协作处理 Teams 项目。
* 发布 Teams 应用。

### <a name="teamsfx-net-sdk-reference-docs"></a>TeamsFx .NET SDK 参考文档

* [Microsoft.Extensions.DependencyInjection 命名空间](/../dotnet/api/Microsoft.Extensions.DependencyInjection)
* [Microsoft.TeamsFx 命名空间](/../dotnet/api/Microsoft.TeamsFx)
* [Microsoft.TeamsFx.Configuration 命名空间](/../dotnet/api/Microsoft.TeamsFx.Configuration)
* [Microsoft.TeamsFx.Conversation 命名空间](/../dotnet/api/Microsoft.TeamsFx.Conversation)
* [Microsoft.TeamsFx.Helper 命名空间](/../dotnet/api/Microsoft.TeamsFx.Helper)

## <a name="see-also"></a>另请参阅

* [在 Visual Studio 中创建新的 Teams 应用](create-new-teams-app-for-Visual-Studio.md)
* [使用 Visual Studio 预配云资源](provision-cloud-resources.md)
* [使用 Visual Studio 将 Teams 应用部署到云](deploy-teams-app.md)
