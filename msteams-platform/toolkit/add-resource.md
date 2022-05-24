---
title: 将资源添加到Teams应用
author: MuyangAmigo
description: 介绍添加 Teams 工具包的资源
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: f3b96b60447596eae8c1cdf37f4b38f6653c444b
ms.sourcegitcommit: 74623035d7c18194e339f566c820e0653bc3d8b6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2022
ms.locfileid: "65656647"
---
# <a name="add-cloud-resources-to-teams-app"></a>将云资源添加到 Teams 应用

TeamsFx 有助于预配应用程序托管的云资源。 可以选择性地添加符合开发需求的云资源。

## <a name="advantages"></a>优点

以下列表提供了在 TeamsFx 中添加更多云资源的优点：

* 提供便利
* 使用Teams Toolkit自动生成所有配置文件并连接到Teams应用

## <a name="limitation"></a>限制

如果已创建基于SPFx选项卡项目，则无法添加 Azure 云资源。

## <a name="add-cloud-resources"></a>添加云资源

**可以通过以下方法添加云资源：**

* 在Visual Studio Code中使用Teams Toolkit添加云资源
* 使用命令面板添加云资源

  > [!NOTE]
  > 在Teams应用中成功添加资源后，需要为每个环境进行预配。
  
* **在Visual Studio Code中使用Teams Toolkit添加云资源：**

   1. 打开 **Visual Studio Code**。
   1. 从左侧面板中选择 **Teams Toolkit**。
   1. 选择 **“开发**”下 **的“添加功能**”。

        :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/select-feature-updated.png" alt-text="添加功能" border="true":::

* **若要使用命令面板添加云资源，请执行以下操作：**

   1. 打开 **命令面板**。
   1. 输入 **Teams：添加功能**。
   1. 按 Enter 键。

        :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/Teams-add-features.png" alt-text="云" border="true":::

   1. 在弹出窗口中，选择要在项目中添加的云资源。

        :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/cloud/updated-final-cloud.png" alt-text="最后" border="true":::

## <a name="add-cloud-resources-using-teamsfx-cli"></a>使用 TeamsFx CLI 添加云资源

* 将目录更改为 **项目目录**。
* 下表列出了功能和所需的命令：

  |云资源|命令|
  |---------------|----------|
  | Azure 函数|`teamsfx add azure-function`|
  | Azure SQL 数据库|`teamsfx add azure-sql`|
  | Azure API 管理|`teamsfx add azure-apim`|
  | Azure Key Vault|`teamsfx add azure-keyvault`|

## <a name="types-of-cloud-resources"></a>云资源的类型

在以下方案中，TeamsFx 与 Azure 服务集成：

- [Azure 函数](/azure/azure-functions/functions-overview)：可满足随选要求的无服务器解决方案，例如为 Teams 应用程序后端创建 Web API。
- [Azure SQL 数据库](/azure/azure-sql/database/sql-database-paas-overview)：平台即服务 (PaaS) 数据库引擎，可用作 Teams 应用程序数据存储。
- [Azure API 管理](deploy.md)：API 网关可用于管理为Teams应用程序创建的 API，并将其发布到其他应用程序（如 Power 应用）上使用。
- [Azure 密钥保管库](/azure/key-vault/general/overview)：保护云应用和服务所使用的密钥和其他密码。

## <a name="add-cloud-resources"></a>添加云资源

在项目中添加资源后，将显示以下更改：

- 添加到 azure.parameter 的新参数。{env}.json，用于提供所需的预配信息。
- 新内容包含在 ARM 模板下 `templates/azure`，但添加 Azure 资源的文件夹中 `templates/azure/teamsfx` 除外。
- `templates/azure/teamsfx` 文件夹下的文件将重新生成，以确保 TeamsFx 所需的配置对于添加的 Azure 资源是最新的。
- `.fx/projectSettings.json` 已更新以跟踪项目中的可用资源。

在项目中添加资源后，将显示以下其他更改：

|资源|更改|说明|
|---------------|---------------|-----------------------------|
|Azure 函数|Azure 函数模板代码将添加到路径为 `yourProjectFolder/api` 的子文件夹中</br></br>`launch.json` 和 `task.json` 已在 `.visual studio code` 文件夹下更新。| 在项目中包含 Hello World HTTP 触发器模板。</br></br> 包含要在本地调试应用程序时执行 Visual Studio Code 所需的脚本。|
|Azure API 管理|添加到路径为 `yourProjectFolder/openapi` 的子文件夹中的已打开的 API 规范文件|发布后定义 API，它是 API 规范文件。|

## <a name="see-also"></a>另请参阅

* [预配云资源](provision.md)
* [新建 Teams 应用](create-new-project.md)
* [向Teams应用添加功能](add-capability.md)
* [部署到云](deploy.md)