---
title: 部署到云
author: MuyangAmigo
description: 将应用部署到云、Azure 或SharePoint
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 1d0ade9abed4be212abfb96068626172c4f0f03e
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104145"
---
# <a name="deploy-to-the-cloud"></a>部署到云

Teams Toolkit可帮助你将应用程序中的前端和后端代码部署或上传到 Azure 中预配的云资源。

* 选项卡（例如前端应用程序）部署到 Azure 存储，并配置为静态 Web 托管或 sharepoint 站点。
* 后端 API 部署到 Azure 函数。
* 机器人或消息扩展部署到 Azure 应用服务。

## <a name="prerequisite"></a>先决条件

* [安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

> [!NOTE]
>
> * 确保已在 VS 代码中打开Teams应用项目。
> * 在将项目代码部署到云之前， [请预配云资源](provision.md)。

## <a name="deploy-teams-apps-using-teams-toolkit"></a>使用Teams Toolkit部署Teams应用

入门指南可帮助你使用Teams Toolkit进行部署。 可以使用以下命令部署Teams应用：

* [将应用部署到 Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [将应用部署到SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>有关Teams应用工作负荷的详细信息

| Teams应用工作负载 | 源代码 | 生成项目| 目标资源 |
|-------------|----------|---------------|---------------|
|带有React的选项卡 </br> 前端工作负荷| `yourProjectFolder/tabs`| `tabs/build` |Azure 存储 |
|带有SharePoint的选项卡 </br> 前端工作负荷 | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint应用目录 |
|Azure 函数上的 API </br> 后端工作负载 | `yourProjectFolder/api`| 不适用 |Azure 函数 |
|机器人和消息扩展 </br> 后端工作负载 | `yourProjectFolder/bot` | 不适用 | Azure 应用服务 |

> [!NOTE]
> 在项目中包括 Azure API 管理资源并触发部署时。 可以在 Azure 函数中将 API 发布到 Azure API 管理服务。

## <a name="see-also"></a>另请参阅

* [添加更多云资源](add-resource.md)
* [创建和部署 Azure 云服务](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [添加更多Teams应用功能](add-capability.md)
* [使用 CI/CD 管道部署项目代码](use-CICD-template.md)
* [管理多个环境](TeamsFx-multi-env.md)
* [在 Teams 项目中与其他开发人员协作](TeamsFx-collaboration.md)
