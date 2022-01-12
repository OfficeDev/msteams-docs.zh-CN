---
title: 部署到云
author: MuyangAmigo
description: 部署到云
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 0eeda4842ad3f0443d46b5075b1520b0042130ec
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768376"
---
# <a name="deploy-to-the-cloud"></a>部署到云

Teams Toolkit帮助你将应用程序中的前端和后端代码部署或上载到 Azure 中预配的云资源。

* 选项卡（如前端应用程序）部署到 Azure 存储，并针对静态 Web 托管或 sharepoint 网站进行配置。
* 后端 API 将部署到 Azure 函数。
* 自动程序或消息传递扩展将部署到 Azure 应用服务。

## <a name="prerequisite"></a>先决条件

* [安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

> [!NOTE]
> * 确保你已Teams VS 代码打开的应用项目。
> * 在将项目代码部署到云之前， [预配云资源](provision.md)。

## <a name="deploy-teams-apps-using-teams-toolkit"></a>使用Teams部署 Teams Toolkit

入门指南可帮助你使用 Teams Toolkit。 可以使用以下方法部署Teams应用：
* [将应用部署到 Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [将应用部署到SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>有关应用Teams的详细信息

| Teams应用工作负载 | 源代码 | 生成项目| 目标资源 |
|-------------|----------|---------------|---------------|
|带选项卡React </br> 前端工作负载| `yourProjectFolder/tabs`| `tabs/build` |Azure 存储 |
|带选项卡SharePoint </br> 前端工作负载 | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint应用程序目录 |
|Azure 函数上的 API </br> 后端工作负载 | `yourProjectFolder/api`| 不适用 |Azure 函数 |
|机器人和消息传递扩展 </br> 后端工作负载 | `yourProjectFolder/bot` | 不适用 | Azure 应用服务 |

> [!NOTE]
> 当你在项目中包括 Azure API 管理资源并触发部署时。 你可以将 Azure 函数中的 API 发布到 Azure API 管理服务。

## <a name="see-also"></a>另请参阅

* [添加更多云资源](add-resource.md)
* [添加更多Teams应用功能](add-capability.md)
* [使用 CI/CD 管道部署项目代码](use-CICD-template.md)
* [管理多个环境](TeamsFx-multi-env.md)
* [与其他开发人员协作处理Teams项目](TeamsFx-collaboration.md)
