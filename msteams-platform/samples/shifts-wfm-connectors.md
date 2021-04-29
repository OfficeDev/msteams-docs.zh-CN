---
title: 生产准备就绪的排班连接器
description: 适用于 Teams 的员工管理班次连接器
ms.topic: reference
author: laujan
ms.date: 03/09/2020
localization_priority: Normal
keywords: Microsoft Teams 连接器 kronos
ms.author: lajanuar
ms.openlocfilehash: 459797dd3f8425223c0dcbedc335955bf106ae37
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075736"
---
# <a name="production-ready-shifts-connectors"></a>生产准备就绪的排班连接器  

Teams Shifts 员工 (WFM) 连接器是生产就绪型、开放源代码和社区驱动的集成，对一线工作人员非常有用。 它们通过 Teams 班次为一线员工的数字转换提供了无缝体验和快速流程。 

每个连接器都提供有关部署和集成到组织的详细指导。 GitHub 存储库中提供了完整的源代码。 您可以详细浏览或分叉，并自定义以满足您的特定需求。   

本文档概述了 Teams Shifts WFM 连接器、Kronos 到 Teams Shifts 连接器和 JDA 到 Teams Shifts 连接器的关键优势。

## <a name="key-benefits-of-teams-shifts-wfm-connectors"></a>Teams Shifts WFM 连接器的主要好处

以下是 Teams Shifts WFM 连接器的主要优势：

* **即插即用体验：** 所有 Shifts WFM 连接器均ARM Azure 部署脚本，这些脚本允许你在 Microsoft Azure 中托管所有必要的服务。 部署应用不需要编码。

* **生产就绪代码：** 所有 Shifts 连接器都符合建议的安全性和基础结构最佳做法，并检查所有社区提交的更改以确保持续一致性。

* **可自定义和可扩展：**  尽管所有 Shifts WFM 连接器都已准备好部署以立即使用，但整个代码库和部署脚本随时可用。 你可以轻松自定义或扩展它们，以满足你的独特需求。

* **详细的文档&支持：**  所有 Shifts WFM 连接器都附带了有关解决方案体系结构、部署和配置步骤的端到端文档。 连接器存储库受到监视，以便可以通过存储库的 GitHub 问题跟踪器报告遇到的所有问题、挑战或困难。

* **无缝集成：** WFM 解决方案与 Teams Shifts 之间的集成使一线工作人员可以使用 Teams Shifts 应用查看或管理其日程安排和班次时间，并使用它的移动设备或桌面版中提供的所有其他丰富的协作功能，而无需将上下文切换到其他应用。  

**Teams 中的"打开班次"视图** 

下图显示了 Teams 中的班次视图： 

![Teams 中的开放班次](../assets/images/teams-open-shifts-view.png)

## <a name="kronos-to-teams-shifts-connector"></a>Kronos 到 Teams Shifts 连接器

借助开放源代码，你可以将 Kronos 员工中心版本 8.1 及以上版本与 Teams 班次（如桌面或移动 Teams 应用）集成，用于以下一线员工和经理方案：

* 查看日程安排。

* 发布和请求打开的班次。

* 交换班次。

* 请求请假。

* 提供班次。

有关部署 Kronos 到 Teams Shifts 连接器详细信息，请参阅 [在 GitHub 上获取它](https://aka.ms/KronosShiftsConnector)。

## <a name="jda-to-teams-shifts-connector"></a>JDA 到 Teams Shifts 连接器

借助开放源代码，可以将 JDA（如 BlueYonder 版本 17.2 及以上）与 Teams Shift（如桌面或移动 Teams 应用）集成，以用于以下一线员工和经理方案：

* 在 JDA 中发布班次和计划组，在 Teams 中查看它们。

* 启用丰富的计划方案，包括请求转换交换和请假。

* 使用适用于 Shifts [的 Microsoft Graph API 设置用户可用性](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true)。

有关参与和建议的信息，请参阅[在 GitHub 上获取。](https://aka.ms/JDAShiftsConnector)</br></br>

## <a name="see-also"></a>另请参阅

[集成 web 应用](~/samples/integrate-web-apps-overview.md)
