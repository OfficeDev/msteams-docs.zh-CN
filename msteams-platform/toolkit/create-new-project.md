---
title: 使用 Teams 工具包创建新的 Teams 应用
author: zyxiaoyuer
description: 在本模块中，了解如何使用 Teams 工具包创建新的 Teams 应用，以及如何使用视图示例创建新的 Teams 应用
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: 1737c55598d5963a77317a0b37869275f96a902d
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503751"
---
# <a name="create-a-new-teams-app-using-teams-toolkit"></a>使用 Teams 工具包创建新的 Teams 应用 

若要使用 Teams 工具包创建新的 Teams 应用，可以从以下选项中进行选择：

* [新建 Teams 应用](create-new-project.md#create-a-new-teams-app)
* [查看示例](create-new-project.md#create-a-new-teams-app-using-view-samples)

## <a name="create-a-new-teams-app"></a>新建 Teams 应用

1. 打开 Visual Studio Code。
1. 在 Visual Studio Code 边栏中选择 Teams 工具包 :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG" border="true"::: 图标。
1. 选择 **创建新的 Teams 应用**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar.png" alt-text="Teams 工具包边栏":::

1. 可以选择“**创建新的 Teams 应用**”或“**从示例开始**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/select-create-app.png" alt-text="创建应用":::

1. 如果选择“**新建 Teams 应用**”，则以下图像将显示三个类别的模板：基于方案的 Teams 应用、基本 Teams 应用和 Microsoft 365 中的扩展 Teams 应用：

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams-capabilities.png" alt-text="Teams 应用的功能":::

1. 选择至少一个选项以开始创建 Teams 应用。

## <a name="create-a-new-teams-app-using-view-samples"></a>使用视图示例创建新的 Teams 应用

可以浏览“**查看示例**”并选择现有示例来创建新应用。 所选示例可能已有一些功能，例如，具有 Azure 后端的待办事项列表或与 Microsoft Graph Toolkit 的集成。

 1. 从 Microsoft Visual Studio Code 打开 **Teams Toolkit**。
 1. 在 Treeview 中选择“**开发**”部分。
 1. 选择 **查看示例**。 

    :::image type="content" source="../assets/images/teams-toolkit-v2/view-samples.png" alt-text="查看示例":::

    示例库如下图所示：

    :::image type="content" source="../assets/images/teams-toolkit-v2/sample-gallery.png" alt-text="示例库":::

  可按以下方式浏览示例库：

  1. 选择一个示例以浏览详细信息。
  1. 在每个示例的信息页面中选择“**创建**”以下载它。 
  1. 通过按照下载示例后自动打开的说明进行操作，在本地或远程运行应用以在 Teams Web 客户端中预览。
  1. 如果不希望下载示例，则可以选择“**在 GitHub 上查看**”，以在 GitHub 示例存储库中打开示例并浏览源代码。

## <a name="step-by-step-guides-using-teams-toolkit"></a>使用 Teams 工具包的分步指南

* [使用 Blazor 构建 Teams 应用](../sbs-gs-blazorupdate.yml)
* [通过 JavaScript 使用 React 构建 Teams 应用](../sbs-gs-javascript.yml)
* [使用 SPFx 构建 Teams 应用](../sbs-gs-spfx.yml)
* [使用 C# 或 .NET 构建 Teams 应用](../sbs-gs-csharp.yml)
* [向 Teams 发送通知](../sbs-gs-notificationbot.yml)
* [生成命令机器人](../sbs-gs-commandbot.yml)

## <a name="see-also"></a>另请参阅

* [预配云资源](provision.md)
* [将 Teams 应用部署到云](deploy.md)
* [发布 Teams 应用](../concepts/deploy-and-publish/appsource/publish.md)
* [管理多个环境](TeamsFx-multi-env.md)
* [在 Teams 项目中与其他开发人员协作](TeamsFx-collaboration.md)
