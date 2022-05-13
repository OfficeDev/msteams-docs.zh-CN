---
title: 将资源添加到 Teams 应用
author: MuyangAmigo
description: 介绍添加 Teams 工具包的资源
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 50cd3de693f70fd0c8414408bd6f4e6d3332d544
ms.sourcegitcommit: 430bf416bb8d1b74f926c8b5d5ffd3dbb0782286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2022
ms.locfileid: "65297203"
---
# <a name="add-cloud-resources-to-your-teams-app"></a>将云资源添加到 Teams 应用

TeamsFx 有助于为应用程序托管预配云资源。 还可以选择性地添加满足开发需求的云资源。

## <a name="prerequisite"></a>先决条件

[安装 Teams 工具包](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

> [!TIP]
> 请确保 Visual Studio Code 中有 Teams 应用项目。

## <a name="add-cloud-resources-using-teams-toolkit"></a>使用 Teams 工具包添加云资源

> [!IMPORTANT]
> 添加资源后，需要预配每个环境。

1. 打开 **Microsoft Visual Studio Code**。
1. 从左窗格中选择“**Teams 工具包**”。
1. 在 Teams 工具包边栏面板中，选择“**添加云资源**”：

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add cloudresources.png" alt-text="添加资源":::

   你还可以打开命令面板并输入 **Teams: Add cloud resources**：

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addcloud.png" alt-text="添加云资源":::

1. 从弹出窗口中，选择要添加到 Teams 应用项目的云资源：

     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addresources.png" alt-text="添加":::

1. 选择“确定”。

所选资源已成功添加到你的项目中。

## <a name="add-cloud-resources-using-teamsfx-cli-in-command-window"></a>在命令窗口中使用 TeamsFx CLI 添加云资源

1. 将目录更改为 **项目目录**。
1. 执行以下命令，以在项目中添加其他资源：

|云资源|命令|
|---------------|----------|
| Azure 函数|`teamsfx resource add azure-function --function-name your-func-name`|
| Azure SQL 数据库|`teamsfx resource add --function-name your-func-name`|
| Azure API 管理|`teamsfx resource add azure-apim`|
| Azure Key Vault|`teamsfx resource add azure-keyvault`|

## <a name="types-of-cloud-resources"></a>云资源的类型

TeamsFx 与 Azure 服务集成，适用于以下方案：

- [Azure 函数](/azure/azure-functions/functions-overview)：可满足随选要求的无服务器解决方案，例如为 Teams 应用程序后端创建 Web API。
- [Azure SQL 数据库](/azure/azure-sql/database/sql-database-paas-overview)：平台即服务 (PaaS) 数据库引擎，可用作 Teams 应用程序数据存储。
- [Azure API 管理](deploy.md)：一种 API 网关，可用于管理为 Teams 应用程序创建的 API，并进行发布以在其他应用程序（例如 Power 应用）上使用。
- [Azure 密钥保管库](/azure/key-vault/general/overview)：保护云应用和服务所使用的密钥和其他密码。

## <a name="add-cloud-resources"></a>添加云资源

添加任何资源后，项目中的更改如下所示：

- 可将新参数添加到 azure.parameter.{env}.json，以提供所需的预配信息。
- 除 `templates/azure/teamsfx` 文件夹下的文件外，新内容将追加到 `templates/azure` 文件夹下的 ARM 模板中，以创建添加的 Azure 资源。
- `templates/azure/teamsfx` 文件夹下的文件将重新生成，以确保 TeamsFx 所需的配置对于添加的 Azure 资源是最新的。
- `.fx/projectSettings.json` 已更新以跟踪项目中存在的资源。

添加资源后，项目中的其他更改如下所示:

|资源|更改|说明|
|---------------|---------------|-----------------------------|
|Azure 函数|Azure 函数模板代码将添加到路径为 `yourProjectFolder/api` 的子文件夹中</br></br>`launch.json` 和 `task.json` 已在 `.visual studio code` 文件夹下更新。| 在项目中包含 Hello World HTTP 触发器模板。</br></br> 包含要在本地调试应用程序时执行 Visual Studio Code 所需的脚本。|
|Azure API 管理|添加到路径为 `yourProjectFolder/openapi` 的子文件夹中的已打开的 API 规范文件|发布后定义 API，它是 API 规范文件。|

## <a name="limitation"></a>限制

如果已创建基于 SPFx 的选项卡项目，则无法添加资源。

## <a name="see-also"></a>另请参阅

[预配云资源](provision.md)
