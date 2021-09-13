---
title: 生产准备就绪的排班连接器
description: 员工管理 针对员工的轮班Teams
ms.topic: reference
author: surbhigupta
ms.date: 03/09/2020
ms.localizationpriority: medium
keywords: Microsoft Teams连接器 kronos
ms.author: lajanuar
ms.openlocfilehash: f734bc4491826f5afee4147b55fdbc10b69fd433
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155341"
---
# <a name="production-ready-shifts-connectors"></a>生产准备就绪的排班连接器  

TeamsShifts 员工 (WFM) 连接器是生产就绪型、开放源代码和社区驱动的集成，对一线工作人员非常有用。 它们通过 Shift 为一线员工的数字转换提供了无缝体验Teams流程。 

每个连接器都提供有关部署和集成到组织的详细指导。 完整的源代码可在GitHub中提供。 您可以详细浏览或分叉，并自定义以满足您的特定需求。   

本文档概述了 Teams Shifts WFM 连接器、Kronos 到 Teams Shifts 连接器和 JDA 到 Teams Shifts 连接器的主要优势。

## <a name="key-benefits-of-teams-shifts-wfm-connectors"></a>Shifts WFM Teams的主要好处

下面是 Shifts WFM Teams的主要好处：

* **即插即用体验：** 所有 Shifts WFM 连接器都ARM Azure 部署脚本，这些脚本允许你在 Microsoft Azure 中托管Microsoft Azure。 部署应用不需要编码。

* **生产就绪代码：** 所有 Shifts 连接器都符合建议的安全性和基础结构最佳做法，并检查所有社区提交的更改以确保持续一致性。

* **可自定义和可扩展：**  尽管所有 Shifts WFM 连接器都已准备好部署以立即使用，但整个代码库和部署脚本随时可用。 你可以轻松自定义或扩展它们，以满足你的独特需求。

* **详细的文档&支持：**  所有 Shifts WFM 连接器都附带了有关解决方案体系结构、部署和配置步骤的端到端文档。 连接器存储库受到监视，以便可以通过存储库的"问题跟踪器"报告遇到GitHub问题。

* **无缝集成：** WFM 解决方案与 Teams Shifts 之间的集成允许一线工作人员使用 Teams Shifts 应用查看或管理其日程安排和班次时间，并使用 Teams 中提供的所有其他丰富协作功能，而无需将上下文切换到其他应用。  

**在"打开"视图中打开Teams** 

以下图像Teams班次视图： 

![打开Teams](../assets/images/teams-open-shifts-view.png)

## <a name="kronos-to-teams-shifts-connector"></a>Kronos 到 Teams Shifts 连接器

借助开放源代码，你可以将 Kronos 员工中心版本 8.1 及以上版本与 Teams 班次（如桌面或移动 Teams 应用）集成，用于以下一线员工和经理方案：

* 查看日程安排。

* 发布和请求打开的班次。

* 交换班次。

* 请求请假。

* 提供班次。

有关部署 Kronos-to-Teams Shifts 连接器[GitHub。](https://aka.ms/KronosShiftsConnector)

## <a name="jda-to-teams-shifts-connector"></a>JDA 到 Teams Shifts 连接器

借助开放源代码，你可以将 JDA（如 BlueYonder 版本 17.2 及以上）与 Teams Shift（如桌面或移动 Teams 应用）集成，用于以下一线工作人员和经理方案：

* 在 JDA 中发布班次和计划组，并查看Teams。

* 启用丰富的计划方案，包括请求转换交换和请假。

* 使用适用于班次的[Microsoft Graph API 设置用户可用性](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true)。

有关贡献和建议的更多信息，请参阅在[GitHub 上获取](https://aka.ms/JDAShiftsConnector)。</br></br>

## <a name="see-also"></a>另请参阅

[集成 web 应用](~/samples/integrate-web-apps-overview.md)
