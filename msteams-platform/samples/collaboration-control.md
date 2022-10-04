---
title: 协作控件
author: surbhigupta
description: 在本模块中，了解协作控制如何允许制造商生成与 Microsoft 365 服务（如 Planner、Bookings 和 Outlook）集成的应用。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: fa0cb45921820a61fbfd7112a50f28eb9230fb4b
ms.sourcegitcommit: f2ac771cbd608e872604e9ac8ffec2d08f55ee1a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2022
ms.locfileid: "68373022"
---
# <a name="collaboration-controls"></a>协作控件

协作控制允许应用 Microsoft 365 和 Microsoft Teams 进行审批、文件、会议、备注和任务，以便围绕业务流程实现上下文协作。 使用这些控件可以生成可在 Teams 中显示的自定义协作体验。 组成协作控件的解决方案允许制造商以低代码方式生成与 Microsoft 365 服务（如 Planner、Bookings、Outlook 和 SharePoint）集成的应用程序。

这些控件使你能够通过构建业务线应用和工作来简化用户的工作流协作，而无需使用以下内容将上下文从应用切换到应用

* 审批
* 文件
* 会议
* 备注
* 任务

> [!NOTE]
> 目前，协作控件仅在 [公共开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中可用。

下面是协作控件的一些关键功能：

* **Microsoft Planner任务：** 创建任务并将其分配给记录成员，以便他们可以在 Microsoft Teams 中查看模型驱动应用和任务应用中的任务的合并列表。

* **Dataverse 任务：** 创建可分配给组织外部用户的任务。

* **Dataverse 备注：** 创建分配给应用中的记录的笔记。

* **Outlook 会议：** 安排与客户和内部员工的会议，并使用选择一个按钮与其他人无缝连接到 Microsoft Teams。

* **SharePoint 文件：** 与记录的成员共享文件，以便可以在 SharePoint 支持的集中位置搜索、引用和编辑相关项目。

* **批准：** 简化团队中的请求。

> [!NOTE]
> 通过配置和使用前面提到的各种 Microsoft 365 协作控件功能，你将授予用户数据通过图形 API并接受 [Microsoft API 使用条款的权限](/legal/microsoft-apis/terms-of-use?context=graph%2Fcontext)。 有关详细信息，请参阅 [Microsoft Graph](/graph/overview)。

## <a name="how-collaboration-controls-works"></a>协作控件的工作原理

这些控件在可部署到 Microsoft Teams 的 Power Apps 模型驱动应用程序 (MDA) 中运行。 MDA 在 Microsoft Dataverse 上运行，可与自定义数据模型集成。 这些控件与 Microsoft Graph for Planner 任务、Outlook 和 Teams 日历以及 SharePoint 文件集成。 协作控件不会直接与外部源（例如记录系统或门户）集成。

* 可以通过标准 OData API 从外部源将数据添加到 Dataverse。

* 可以通过标准 OData API 从 Dataverse 读取数据，并将其提交到外部源，例如记录系统或门户。

:::image type="content" source="~/assets/images/collaboration-control/consumption-mda.png" alt-text="协作生命周期":::
