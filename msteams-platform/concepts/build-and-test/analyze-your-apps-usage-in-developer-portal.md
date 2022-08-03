---
title: 在开发人员门户中分析应用的使用情况
description: 在本模块中，了解如何在开发人员门户中分析应用的使用情况
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 43758fdebd1f2e76318880a51d9173469b0ed604
ms.sourcegitcommit: 990a36fb774e614146444d4adaa2c9bcdb835998
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2022
ms.locfileid: "67232378"
---
# <a name="analyze-your-apps-usage-in-developer-portal"></a>在开发人员门户中分析应用的使用情况

在 Teams 开发人员门户的 **“概述** ”页上，可以看到应用的活动用户总数。

> [!NOTE]
> 使用情况分析目前仅适用于通过 Teams **开发人员门户** 发布到组织的新自定义应用，或在 2022 年 4 月之后导入到 Teams **开发人员门户** 中。 **合作伙伴中心** 提供发布到 Teams 应用商店的所有应用的使用情况分析，了解 [Teams 应用使用情况报告](/office/dev/store/teams-apps-usage)的详细信息。

| 跃点数 | 定义 |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| *每月 R30* | 默认使用指标。 它显示在 UTC 的滚动 30 天窗口内使用应用的唯一活动用户计数。 |
| *每天* | 它显示在 UTC 中给定日期使用应用的唯一活动用户计数。 |

给定一天的应用使用情况反映在 24 到 48 小时内，新应用的使用情况数据最多可能需要 3 到 5 天才能反映在图表中。

可以从 **“分析** ”页面查看应用的使用情况和其他见解。 若要访问页面，请执行以下操作：

1. 转到 **[Teams 开发人员门户](https://dev.teams.microsoft.com)**。
1. 从左窗格中选择“**应用**”。
1. 从“应用”页中选择所需的 **应用** 。
1. 在 **“概述**”下选择 **“分析**”，或在 **“活动用户” (预览)** 卡下选择 **“查看详细信息**”。

 :::image type="content" source="../../assets/images/tdp/dev-app-portal.png" alt-text="屏幕截图显示开发人员门户中应用的分析页面。"lightbox="../../assets/images/tdp/dev-app-portal.png":::

在此页面上浏览各个指标时，可以使用 **“筛选器”** 按钮从以下筛选器选项分析应用的使用情况：

* 聚合类型：此筛选器允许按不同用户的计数或不同租户或客户的计数对以下指标进行分组。
* 平台
* 操作系统
* 领域

 :::image type="content" source="../../assets/images/tdp/dev-analytics-filter.png" alt-text="屏幕截图显示开发人员门户中的分析页面筛选器。":::

选择所需的筛选器后，可以浏览以下单个小组件：

* [按时间段的使用情况](#usage-by-time-period)
* [按平台和 OS 的使用情况](#usage-by-platform-and-os)
* [按保留状态的使用情况](#usage-by-retention-state)
* [使用强度](#usage-intensity)

## <a name="usage-by-time-period"></a>按时间段的使用情况

按 **时间段的使用** 情况图表显示跨不同时间段打开和使用应用的活动用户或租户数。

 :::image type="content" source="../../assets/images/tdp/usage-by-time-period.png" alt-text="屏幕截图显示已发布应用的时间周期图表的使用情况。":::

| 跃点数 | 定义 |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| 每月 R30 | 每个数据点表示给定的 R30 (滚动 30 天) 周期。 |
| 每月 R28 | 每个数据点表示给定的 R28 (滚动 28 天) 周期。 |
| 每周 R7| 每个数据点表示给定的 R7 (滚动 7 天) 周期。 |
| 每天 | 每个数据点表示给定的 R1 (滚动 1 天) 周期。 |

## <a name="usage-by-platform-and-os"></a>按平台和 OS 的使用情况

“ **按平台和操作系统** 使用情况”图表显示应用在各种终结点（例如 **Windows**、 **Mac**、 **iOS**、 **Android** 和 **Web**）的活动使用情况。 同一用户或租户可以在多个终结点上使用应用。 每个数据点表示给定的 R30 (滚动 30 天) 周期。

 :::image type="content" source="../../assets/images/tdp/usage-by-platform-OS.png" alt-text="屏幕截图显示已发布的应用的平台和 OS 图表的使用情况。":::

## <a name="usage-by-retention-state"></a>按保留状态的使用情况

通过 **保留状态** 图的使用情况，可以跟踪应用随时间推移的四个关键保留或变动指标。

:::image type="content" source="../../assets/images/tdp/usage-by-retention-state.png" alt-text="屏幕截图显示已发布的应用的保留状态图表的使用情况。":::

| 跃点数 | 定义 |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| 新用户或租户 | 新手且未使用应用的活动用户或租户。 |
| 返回用户或租户 | 在给定 R30 期间使用应用的活动用户或租户 (滚动 30 天) 时间段和紧接之前的 R30 时间段。 |
| 复活的用户或租户 | 以前使用过你的应用一次或多次但未在前面的 R30 时间段内使用你的应用的活动用户或租户。 |
| 已失效的用户或租户 | 活动用户或租户在给定的 R30 时间段内未出现，但在前面的 R30 时间段内出现。 |

## <a name="usage-intensity"></a>使用强度

**使用强度** 图表显示应用的主要使用强度指标。

 :::image type="content" source="../../assets/images/tdp/usage-intensity.png" alt-text="屏幕截图显示已发布的应用的使用强度图表。":::

| 跃点数 | 定义 |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| 每月使用的中值天数 | 在上一个 R30 (滚动 30 天) 时间段内打开应用的天数中位数。 |
| 5 天以上使用率的百分比 | 在过去 R30 时间段内打开或使用应用超过五天的活动用户的百分比。 |
| DAU/MAU | 每天使用应用的唯一用户或租户的平均数之比除以所选 R30 时间段的每月活动用户。 |

## <a name="app-dashboard"></a>应用仪表板

“ **我的应用”仪表板** 表显示前四个类别下每个指标的最新 R30 (滚动 30 天) 数据，以及“月月更改”。 使用左上角的时间选取器并选择所需的日期，可以查看过去 75 天和月末 R30 数据的每日 R30 数据，最长时间为 12 个月。

可以选择每个 **指标名称** ，查看随时间推移的趋势。

 :::image type="content" source="../../assets/images/tdp/app-dashboard.png" alt-text="屏幕截图显示已发布的应用的应用仪表板图表。":::

## <a name="see-also"></a>另请参阅

[Microsoft Teams 应用随附 SaaS 产品/服务](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
