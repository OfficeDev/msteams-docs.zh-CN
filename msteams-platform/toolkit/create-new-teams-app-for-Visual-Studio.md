---
title: 在 Visual Studio 中创建新的 Teams 应用
author: surbhigupta
description: 在本模块中，了解如何使用 Teams Toolkit for Visual Studio 创建新的 Teams 应用
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 07/29/2022
ms.openlocfilehash: 12f0b74726aed8cdca50d9f5c078acd0f22cbeaa
ms.sourcegitcommit: 65ae3ccc2312ddc6cdaa05096e30bdf9dca10c3f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027434"
---
# <a name="create-new-teams-app-in-visual-studio"></a>在 Visual Studio 中创建新的 Teams 应用

Teams 工具包在 Visual Studio 中提供 Microsoft Teams 应用模板以创建 Teams 应用。  可以在创建新项目时搜索并选择所需的 Teams 应用模板。 可以使用 Teams 应用模板进行创建。

* Tab 应用
* 命令机器人
* 通知机器人
* 消息扩展

## <a name="prerequisites"></a>先决条件

| &nbsp; | 安装 | 用于使用... |
| --- | --- | --- |
| &nbsp; | **Required** | &nbsp; |
| &nbsp; | Visual Studio 版本 17.3 | 可以安装 Visual Studio 的企业版，并安装“ASP.NET”工作负荷和 Microsoft Teams 开发工具。 |
| &nbsp; | Teams 工具包 | 一个 Visual Studio 扩展，用于为应用创建项目基架。 使用最新版本。 |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | 通过聊天、会议、通话等应用与每一位同事进行协作的 Microsoft Teams - 一个地方完成所有操作。 |
 | &nbsp; | [准备 Microsoft 365 租户](../concepts/build-and-test/prepare-your-o365-tenant.md) | 对具有相应安装应用权限的 Teams 帐户的访问权限。 |

1. 启动 Visual Studio 时，从 **“开始”** 部分选择 **“创建新项目**”。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project1.png" alt-text="从入门开始创建新项目":::

   还可以直接从应用程序创建新项目。

1. 选择 **“文件”** 菜单。
1. 选择  **“新建**”。
1. 选择 **“项目**”。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project2.png" alt-text="从文件菜单创建新项目":::

1. 在列表中搜索 Microsoft **Teams** 应用。
1. 选择 **Microsoft Teams 应用**。
1. 选择“**下一步**”。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app.png" alt-text="搜索并选择 Microsoft Teams 应用":::

1. 选择 **项目名称** 并输入项目名称。
1. 选择“**创建**”。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-project-name.png" alt-text="为应用程序命名":::

1. 选择要创建的 **Teams 应用类型** 。
1. 选择“**创建**”。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-type.png" alt-text="选择 Teams 应用类型":::

## <a name="teams-app-templates-in-teams-toolkit-for-visual-studio"></a>Teams Toolkit for Visual Studio 中的 Teams 应用模板

可以看到 Teams 工具包中已为各种 Teams 应用类型填充了 Teams 应用模板。 下表列出了所有可用的模板：

|Teams 应用模板  |说明  |
|---------|---------|
|通知机器人     |通知机器人应用可以向 Teams 客户端发送通知，可以通过多种方式触发通知。 例如，按 HTTP 请求或按时间触发通知。 还可以根据业务方案选择触发的通知。         |
|命令机器人     |用户可以键入命令以使用命令机器人应用与机器人交互。         |
|Tab     |Tab 应用在 Teams 中显示网页，并使用 Teams 帐户启用单一登录。         |
|消息扩展     |消息扩展应用实现简单的功能，例如创建自适应卡片、搜索 Nugget 包、展开“dev.botframework.com”域的链接。         |

> [!NOTE]
>创建项目后，Teams 工具包会自动打开“入门”。 现在可以在“入门”中查看说明，并查看 Teams 工具包中的不同功能。

## <a name="see-also"></a>另请参阅

* [使用 Visual Studio 预配云资源](provision-cloud-resources.md)
* [使用 Visual Studio 将 Teams 应用部署到云](deploy-teams-app.md)
