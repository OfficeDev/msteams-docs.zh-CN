---
title: 部署到云
author: MuyangAmigo
description: 在本模块中，了解如何使用 Teams 工具包将应用部署到云、Azure 或 SharePoint 并部署 Teams 应用
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 9ad2c9d16901990344ca521599b94b84b0e76217
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616924"
---
# <a name="deploy-teams-app-to-the-cloud"></a>将 Teams 应用部署到云

Teams 工具包可帮助你将应用程序中的前端和后端代码部署或上传到 Azure 中预配的云资源。 可以将以下内容部署到云：

* 选项卡（例如前端应用程序）将部署到 Azure 存储，并配置为静态 Web 托管或 SharePoint 网站。
* 后端 API 将部署到 Azure 函数。
* 机器人或邮件扩展将部署到 Azure 应用服务。

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
|Azure 函数上的 API </br> 后端工作负载 | `yourProjectFolder/api`| 不适用 |Azure 函数 |
|机器人和邮件扩展 </br> 后端工作负载 | `yourProjectFolder/bot` | 不适用 | Azure 应用服务 |

> [!NOTE]
> 在项目中包括 Azure API 管理资源并触发部署时，可以在 Azure 函数中将 API 发布到 Azure API 管理服务。

## <a name="see-also"></a>另请参阅

* [创建和部署 Azure 云服务](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [创建多功能 Teams 应用](add-capability.md)
* [将云资源添加到 Microsoft Teams 应用](add-resource.md)
