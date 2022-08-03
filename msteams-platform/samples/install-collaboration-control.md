---
title: 安装协作控件
author: surbhigupta
description: 在本模块中，了解如何使用电源应用和Microsoft 365 E3安装协作控件，以及如何安装协作控制解决方案。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: aa4259855ba0c95906d7196ffd83c093bea89ea9
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2022
ms.locfileid: "67178842"
---
# <a name="install-collaboration-controls"></a>安装协作控件

> [!NOTE]
> 目前，协作控件仅在 [公共开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中可用。

本文介绍如何安装协作控件。 使用协作控件生成和部署Collaboration Manager应用程序需要以下各项：

* **电源应用**：使用协作控件生成和运行模型驱动应用程序。
* **M365 E3 或更高版本**：将自定义应用程序部署到 Microsoft Teams 并将任务存储在 Planner、SharePoint 中的文件和 Outlook 中的会议中。

若要将组件安装到 Power Platform 环境中，需要以下角色：

* 系统自定义器
* 环境创建者

有关角色特权的详细信息，请参阅在[环境中配置用户安全](/power-platform/admin/database-security#predefined-security-roles)性

## <a name="install-the-collaboration-controls-solutions"></a>安装协作控制解决方案

你将通过专用链接将协作控件安装到 dataverse 环境中。 此链接不得与组织内部或外部的任何其他人员共享。

只有在收到链接并将协作控件安装到 dataverse 环境中后，才能在自己的模型驱动应用中配置和使用组件。

协作控制包括以下解决方案：

|**设置解决方案** | **用途** |
|---|---|
| 协作控制设置 | 保留支持协作控件的设置基础结构 |
| 协作控制设置对象 | 提供协作控件使用的预定义设置值。|

|**协作解决方案** | **用途** |
|---|---|
| 协作控制任务  | 包括任务 PCF (Power Apps 组件框架) 控制。 |
| 协作控制事件 | 包括 Outlook 和 Teams 会议和预订约会的事件 PCF 控件。 |
| 协作控制说明 | 包括备注 PCF 控件，该控件在 Dataverse 中存储笔记。 |
| 协作控制文件 | 包括用于访问 SharePoint 上文件的文件 PCF 控件。 |
| 协作控制核心 |包括自定义协作 API、用于事件、文件和任务控件的协作数据模型和虚拟表。 |
| 协作控制审批 | 包括新的审批 PCF 控件。 |
| 协作控制连接器 | 包括新的协作 Power Automate 连接器 |

> [!NOTE]
> 如果环境中安装了现有版本的控件，则可能需要创建新的环境并完成新安装才能成功升级到最新版本。

安装前，必须位于 Power Platform 环境或管理员租户中。 你将需要一个包含数据库的 dataverse 环境。 如果没有，则需要 [创建一个新](/power-platform/admin/create-environment) 安装来继续安装。

若要安装解决方案，请先浏览到 [Microsoft AppSource]，然后完成以下步骤：

1. 选择 **“立即获取”** 按钮。

   :::image type="content" source="../assets/images/collaboration-control/preview-form.png" alt-text="预览窗体 "border="true":::

1. 使用帐户登录，填写窗体，然后选择 **“继续**”。

   :::image type="content" source="../assets/images/collaboration-control/overview.png" alt-text="概述协作控制" border="true":::

   :::image type="content" source="../assets/images/collaboration-control/collaboration-controls-preview.png" alt-text="协作控制预览" border="true":::

1. 你将定向到 Power Platform 管理员中心。 从下拉菜单中选择一个环境并同意条款和策略语句。

   > [!TIP]
   > 如果在选择环境时看到权限错误，请尝试在环境下拉菜单外部进行选择，看看这是否解决了此问题。

   :::image type="content" source="../assets/images/collaboration-control/install-environment.png" alt-text="安装协作控制环境" border="true":::

1. 选择 **“安装**”，安装可能需要大约 15 分钟才能完成。

1. 如果已注册 Power Apps 预览版，[https://make.preview.powerapps.com/](https://make.preview.powerapps.com/)则也支持转到[https://make.powerapps.com/](https://make.powerapps.com/)。

1. 确保你所处的环境中安装了控件，因为可以查看环境，并在 Power Apps 门户右上角根据需要对其进行更改。

1. 选择 **“解决方案”** 选项卡可查看已在正确环境中安装的所有解决方案。

   :::image type="content" source="../assets/images/collaboration-control/solutions.png" alt-text="解决方案协作控制" border= "true":::

> [!NOTE]
> 协作控件是预览版，元素可能会随时间而变化，可能会发生重大更改。 生产环境中不支持协作控件。

将所有协作解决方案成功安装到环境中后，你将能够生成一个新的模型驱动应用，该应用可以利用协作控制功能。
