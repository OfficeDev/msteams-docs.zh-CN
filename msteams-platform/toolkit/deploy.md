---
title: 部署到云
author: MuyangAmigo
description: 在本模块中，了解如何使用 Teams 工具包将应用部署到云、Azure 或 SharePoint 以及部署 Teams 应用
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 17d4d1d80f9ffd634e2fdae815b8504bb6c0ca99
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833133"
---
# <a name="deploy-teams-app-to-the-cloud"></a>将 Teams 应用部署到云

Teams 工具包可帮助你将应用程序中的前端和后端代码部署或上传到 Azure 中预配的云资源。

::: zone pivot="visual-studio-code"

## <a name="deploy-teams-app-to-the-cloud-using-visual-studio-code"></a>使用 Visual Studio Code 将 Teams 应用部署到云

可以将以下内容部署到云：

* 选项卡（如前端应用程序）将部署到 Azure 存储，并配置为静态 Web 托管或 sharepoint 网站。
* 后端 API 部署到Azure Functions。
* 机器人或消息扩展部署到Azure 应用服务。

  > [!NOTE]
  > 在将应用代码部署到 Azure 云之前，需要成功完成 [云资源的预配](provision.md)。

## <a name="deploy-teams-apps-using-teams-toolkit"></a>使用 Teams 工具包部署 Teams 应用

入门指南可帮助你使用 Teams 工具包进行部署。 可以使用以下命令部署 Teams 应用：

* [将应用部署到 Azure。](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [将应用部署到 SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>有关 Teams 应用工作负载的详细信息

| Teams 应用工作负载 | 源代码 | 生成项目| 目标资源 |
|-------------|----------|---------------|---------------|
|带 React 的选项卡 </br> 前端工作负载| `yourProjectFolder/tabs`| `tabs/build` |Azure 存储 |
|带有 SharePoint 的选项卡 </br> 前端工作负载 | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint 应用目录 |
|Azure Functions上的 API </br> 后端工作负载 | `yourProjectFolder/api`| 不适用 |Azure Functions |
|机器人和邮件扩展 </br> 后端工作负载 | `yourProjectFolder/bot` | 不适用 | Azure 应用服务 |

> [!NOTE]
> 在项目中包含 Azure API 管理资源并触发部署时，可以在 Azure Functions 中将 API 发布到 Azure API 管理服务。

::: zone-end

::: zone pivot="visual-studio"

## <a name="deploy-teams-app-to-the-cloud-using-visual-studio"></a>使用 Visual Studio 将 Teams 应用部署到云

可以在 Visual Studio 中部署以下应用：

* 选项卡应用（如前端应用程序）将部署到 Azure 存储，该存储针对静态 Web 托管进行了配置。
* 可以将具有Azure Functions触发器的通知机器人应用部署到Azure Functions。
* 可以将机器人应用或消息扩展部署到 Azure 应用 服务。

部署后，可以在 Teams 客户端或 Web 浏览器中预览应用，然后再开始使用。

## <a name="deploy-teams-app-using-teams-toolkit"></a>使用 Teams 工具包部署 Teams 应用

1. 打开 Visual Studio。
1. 选择“ **创建新项目** ”或从列表中打开现有项目。
1. 右键单击项目 **“MyTeamsApp1** > **Teams Toolkit** > **部署到云”。**

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-cloud.png" alt-text="部署到云":::

   > [!NOTE]
   > 在此方案中，项目名称为 MyTeamsApp1。

1. 在确认对话框中选择“ **部署** ”。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-confirmation.png" alt-text="“部署到云”确认对话框":::

   部署过程完成后，可以看到一个弹出窗口，其中包含已成功部署的确认信息。 还可以在输出窗口中检查状态。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/VS-deploy-popup.png" alt-text="“部署到云”弹出窗口":::

### <a name="preview-your-app"></a>预览应用

若要预览应用，首先需要创建 Zip 应用包并旁加载到 Teams 客户端。

1. 选择 **“项目** > **Teams 工具包** > **Zip 应用包**”。
1. 选择“ **本地** ”或 **“适用于 Azure** ”选项以生成 Teams 应用包。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-ZipApp-package1.png" alt-text="生成团队应用包":::

**在 Teams 客户端中预览应用**

1. 选择“ **Teams 中的项目** > **Teams 工具包** > **预览**”。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams2.png" alt-text="在 Teams 客户端中预览 Teams 应用":::

   现在，你的应用已旁加载到 Teams 中。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/sideload-teams.png" alt-text="在 Teams 客户端中旁加载 Teams 应用":::

预览应用的另一种方法：

1. 在“**解决方案资源管理器**”下右键单击项目 **“MyTeamsApp1**”。
1. 选择 Teams **中的 Teams** **工具包** > 预览版，在 Web 浏览器中启动 Teams 应用。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams.png" alt-text="在 Web 浏览器中预览 Teams 应用":::

   > [!NOTE]
   > “项目”菜单中提供了相同的菜单选项。

   现在，你的应用已旁加载到 Teams 中。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/sideload-teams.png" alt-text="在 Teams 客户端中旁加载 Teams 应用":::

::: zone-end

## <a name="see-also"></a>另请参阅

* [创建和部署 Azure 云服务](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [创建多功能 Teams 应用](add-capability.md)
* [将云资源添加到 Microsoft Teams 应用](add-resource.md)
* [在 Visual Studio 中创建新的 Teams 应用](create-new-project.md#create-new-teams-app-in-visual-studio)
* [使用 Visual Studio 预配云资源](provision-cloud-resources.md)
* [使用 Visual Studio 编辑 Teams 应用清单](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [使用 Visual Studio 在本地调试 Teams 应用](debug-local.md#debug-your-teams-app-locally-using-visual-studio)
