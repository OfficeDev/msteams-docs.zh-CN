---
title: 部署到云
author: MuyangAmigo
description: 部署到云
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 3f7dc4b320bccfa8a6017f87045b27a37d8199f7
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227681"
---
# <a name="deploy-to-the-cloud"></a>部署到云

Teams Toolkit帮助你将应用程序中的前端和后端代码部署或上载到 Azure 中预配的云资源。

* 选项卡（如前端应用程序）部署到 Azure 存储，并配置为静态 Web 托管或SharePoint网站。
* 后端 API 将部署到 Azure 函数。
* 自动程序或消息传递扩展将部署到 Azure 应用服务。

## <a name="prerequisite"></a>先决条件

* [安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

> [!TIP]
> 你应该已经拥有一个Teams VS 代码打开的应用项目。

> [!NOTE]
> 在将项目代码部署到云之前，请首先 [执行预配云](provision.md) 资源步骤。


## <a name="deploy-teams-apps-using-teams-toolkit"></a>使用Teams部署 Teams Toolkit

在入门教程中，提供如何使用 Teams Toolkit 的分步指南。 可以使用以下方法部署Teams应用程序：

* [将应用部署到 Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [将应用部署到SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workloads"></a>有关Teams工作负载的详细信息

| Teams应用工作负载| 源代码 | 生成Artifacts| 目标资源 |
|-------------|----------|---------------|---------------|
|带选项卡React </br> 前端工作负载| `yourProjectFolder/tabs`| `tabs/build` |Azure 存储 |
|带选项卡SharePoint </br> 前端工作负载 | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint应用程序目录 |
|Azure 函数上的 API </br> 后端工作负载 | `yourProjectFolder/api`| 不适用 |Azure Functions |
|机器人和消息传递扩展 </br> 后端工作负载 | `yourProjectFolder/bot` | 不适用 | Azure 应用服务 |

> [!NOTE]
> 当你在项目中包括 Azure API 管理资源并触发部署时。 可以在 Azure 函数中将 API 发布到 Azure API 管理服务。

## <a name="see-also"></a>另请参阅

> [!div class="nextstepaction"]
> [添加更多云资源](add-resource.md)

> [!div class="nextstepaction"]
> [添加更多Teams应用功能](add-capability.md)

> [!div class="nextstepaction"]
> [使用 CI/CD 管道部署项目代码](use-CICD-template.md)

> [!div class="nextstepaction"]
> [管理多个环境](TeamsFx-multi-env.md)

> [!div class="nextstepaction"]
> [与其他开发人员协作处理Teams项目](TeamsFx-collaboration.md)
