---
title: 将资源添加到Teams应用中
author: MuyangAmigo
description: 描述添加资源Teams Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
---

# <a name="add-cloud-resources-to-your-teams-app"></a>将云资源添加到Teams应用

TeamsFx 有助于为应用程序托管设置云资源。 还可以选择添加满足开发需求的云资源。

## <a name="prerequisite"></a>先决条件

[安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

> [!TIP]
> 确保已Teams应用程序项目Visual Studio Code。

## <a name="add-cloud-resources-using-teams-toolkit"></a>使用云解决方案添加Teams Toolkit

> [!IMPORTANT]
> 添加资源后，需要预配每个环境。

1. 打开 **Microsoft Visual Studio代码**。
1. 从 **Teams Toolkit** 窗格中选择"设置"。
1. 在"Teams Toolkit栏面板中，选择"**添加云资源"**：

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add cloudresources.png" alt-text="添加资源":::

   还可以打开命令调色板并输入以下Teams **：添加云资源**：

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addcloud.png" alt-text="添加云资源":::

1. 从弹出窗口中，选择要添加到应用项目中的Teams资源：

     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/addresources.png" alt-text="add":::

1. 选择“确定”。

所选资源成功添加到项目中。

## <a name="add-cloud-resources-using-teamsfx-cli-in-command-window"></a>在命令窗口中使用 TeamsFx CLI 添加云资源

1. 将目录更改为 **项目目录**。
1. 执行以下命令以在项目中添加不同的资源：

|云资源|命令|
|---------------|----------|
| Azure 函数|`teamsfx resource add azure-function --function-name your-func-name`|
| Azure SQL 数据库|`teamsfx resource add --function-name your-func-name`|
| Azure API 管理|`teamsfx resource add azure-apim`|
| Azure Key Vault|`teamsfx resource add azure-keyvault`|

## <a name="types-of-cloud-resources"></a>云资源类型

针对以下方案，TeamsFx 与 Azure 服务集成：

- [Azure 函数](/azure/azure-functions/functions-overview)：一个无服务器解决方案，可满足你的需求，例如为应用程序后端创建Teams API。
- [Azure SQL](/azure/azure-sql/database/sql-database-paas-overview) 数据库：一个平台即服务 (PaaS) 数据库引擎充当Teams应用程序数据存储。
- [Azure API 管理](/azure/azure-sql/database/sql-database-paas-overview)：一个 API 网关，可用于管理为 Teams 应用程序创建的 API，并发布它们以在其他应用程序（如 Power 应用）上使用。
- [Azure 密钥保管](/azure/key-vault/general/overview)库：保护加密密钥和云应用和服务使用的其他密钥。

## <a name="add-cloud-resources"></a>添加云资源

添加任何资源后，项目中的更改如下所示：

- 新参数可以添加到 azure.parameter。{env}.json，用于提供预配的必需信息。
- 新内容将追加到ARM `templates/azure` 文件夹下的模板（ `templates/azure/teamsfx` 文件夹下的文件除外）以创建添加的 Azure 资源。
- 将重新生成文件夹 `templates/azure/teamsfx` 下的文件，以确保添加的 Azure 资源所需的 TeamsFx 配置是最新的。
- `.fx/projectSettings.json` 已更新，以跟踪项目中提供的资源。

添加资源后，项目的其他更改如下所示：

|资源|更改|说明|
|---------------|---------------|-----------------------------|
|Azure 函数|Azure 函数模板代码将添加到具有路径的子文件夹 `yourProjectFolder/api`</br></br>`launch.json` 并 `task.json` 更新文件夹 `.visual studio code` 下。| 将 hello world http 触发器模板包括在项目中。</br></br> 包括所需的脚本Visual Studio Code在本地调试应用程序时要执行的代码。|
|Azure API 管理|将打开的 API 规范文件添加到具有路径的子文件夹 `yourProjectFolder/openapi`|在发布后定义 API，它是 API 规范文件 。|

## <a name="limitation"></a>限制

如果已创建基于选项卡项目SPFx无法添加资源。

## <a name="see-also"></a>另请参阅

[预配云资源](provision.md)
