---
title: 使用开发人员门户管理应用
description: 在本模块中，了解如何使用开发人员门户为Microsoft Teams配置、分发和管理应用。
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 948f22cf8f55a33e2d5b24b875678039fd101fc2
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142365"
---
# <a name="manage-your-teams-apps-using-developer-portal"></a>使用开发人员门户管理Teams应用

<a href="https://dev.teams.microsoft.com" target="_blank">Teams 开发人员门户</a>是配置、分发和管理 Microsoft Teams 应用的主要工具。 借助开发人员门户，你可以在应用上与同事协作、设置运行时环境等。

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="显示 Teams 开发人员门户主页的屏幕截图。":::

> [!NOTE]
>
> * 目前，开发人员门户不适用于政府社区云 (GCC)、GCC High 或国防部 (DOD) 租户。
> * 但是，可以使用常规租户在开发人员门户中构建应用、下载应用，并使用 [Microsoft Graph](/graph/api/teamsapp-publish?view=graph-rest-1.0&tabs=http&preserve-view=true) 将应用上传到国家云。 有关详细信息，请参阅[国家云部署](/graph/deployments)。

## <a name="register-an-app"></a>注册应用

开发人员门户提供了几种方法来注册 Teams 应用：

* 注册全新的应用。
* 导入现有应用包。

> [!NOTE]
> 如果使用[适用于 Visual Studio Code 的 Microsoft Teams 工具包](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)创建应用，则可以在开发人员门户中管理该应用。

## <a name="set-up-an-environment"></a>设置环境

你可以配置环境和全局变量，以帮助将应用从本地运行时过渡到生产环境。 全局变量将用于所有环境。

若要设置环境，请执行以下操作：

1. 在开发人员门户中，选择正在开发的应用。
2. 转到“**环境**”页面，然后选择“**+ 添加环境**”。
3. 选择“**+ 添加变量**”以为环境创建配置变量。

若要使用变量，请执行以下操作：

使用变量名称而不是硬编码值来设置应用配置。

1. 在开发人员门户的任何字段中输入 `{{`。 此时会显示一个下拉列表，其中包含为所选环境创建的所有变量以及全局变量。  
1. 例如，在下载应用包之前（例如，在准备发布到 Teams 应用商店时），请选择要使用的环境。 你的应用配置会根据环境自动更新。

## <a name="identify-app-owners"></a>标识应用所有者

每个应用都包含“**所有者**”页面，可从中与组织内的同事共享应用注册。**参与者角色** 具有与 **所有者** 角色相同的权限，但删除应用的功能除外。

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a>配置应用的功能和其他重要元数据

Teams 应用是一款 Web 应用。 与所有 Web 应用一样，其源代码通常在 IDE 或代码编辑器中开发，并托管在云中的某个位置（如 Azure）。

若要在 Teams 中安装和呈现应用，必须包含一组可由 Teams 识别的配置。 通常，这是通过制作应用清单来完成的，该清单是一个 JSON 文件，其中包含 Teams 显示应用内容所需的所有元数据。 开发人员门户可将此过程抽象化，并包含新的功能和工具来帮助你取得更大的成功。

## <a name="test-your-app-directly-in-teams"></a>直接在 Teams 中测试应用

开发人员门户提供用于测试和调试应用的选项：

* 在“**概述**”页面上，你可以看到应用配置是否针对 Teams 应用商店测试用例进行验证的快照。
* 通过“**在 Teams 中预览**”按钮，你可以在 Teams 客户端中快速启动应用以进行调试。

## <a name="distribute-your-app"></a>分发应用

在开发人员门户中，可使用“**分发**”按钮下载应用包、发布到组织或发布到 Teams 应用商店。

有关详细信息，请参阅[分发 Teams 应用](~/concepts/deploy-and-publish/apps-publish-overview.md)。

## <a name="analyze-your-apps-usage"></a>分析应用的使用情况

在Teams开发人员门户的 **“概述**”页上，可以看到应用的活动用户总数。

> [!NOTE]
> 使用情况分析目前仅适用于通过 **开发人员门户** 发布到组织的新自定义应用，用于Teams (以前的 App Studio) 或在 2022 年 4 月之后导入开发 **人员门户** 以供Teams。 **合作伙伴中心** 提供了发布到Teams存储区的所有应用的使用情况分析，以获取有关 [应用使用情况报告Teams](/office/dev/store/teams-apps-usage)详细信息。

| 跃点数 | 定义 |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| *每月 R30* | 默认使用指标。 它显示在 UTC 的滚动 30 天窗口内使用应用的唯一活动用户计数。 |
| *每天* | 它显示在 UTC 中给定日期使用应用的唯一活动用户计数。 |

给定一天的应用使用情况反映在 24 到 48 小时内，新应用的使用情况数据最多可能需要 3 到 5 天才能反映在图表中。

可以从 **“分析** ”页面查看应用的使用情况和其他见解。 若要访问页面，请执行以下操作：

1. 转到 **[开发人员门户进行Teams](https://dev.teams.microsoft.com)**。
1. 从左窗格中选择“**应用**”。
1. 从“应用”页中选择所需的 **应用** 。
1. 在 **“概述**”下选择 **“分析**”，或在 **“活动用户” (预览)** 卡下选择 **“查看详细信息**”。

 :::image type="content" source="../../assets/images/tdp/dev-app-portal.PNG" alt-text="dev-Portal-analytics"lightbox="../../assets/images/tdp/dev-app-portal.PNG":::

在此页面上浏览各个指标时，可以使用 **“筛选器”** 按钮从以下筛选器选项分析应用的使用情况：

* 聚合类型：此筛选器允许按不同用户的计数或不同租户或客户的计数对以下指标进行分组。
* 平台
* 操作系统
* 领域

 :::image type="content" source="../../assets/images/tdp/dev-analytics-filter.PNG" alt-text="筛选":::

选择所需的筛选器后，可以浏览以下单个小组件：

* [按时间段的使用情况](#usage-by-time-period)
* [按平台和 OS 的使用情况](#usage-by-platform-and-os)
* [按保留状态的使用情况](#usage-by-retention-state)
* [使用强度](#usage-intensity)

### <a name="usage-by-time-period"></a>按时间段的使用情况

按 **时间段的使用** 情况图表显示跨不同时间段打开和使用应用的活动用户或租户数。

 :::image type="content" source="../../assets/images/tdp/usage-by-time-period.png" alt-text="句号":::

| 跃点数 | 定义 |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| 每月 R30 | 每个数据点表示给定的 R30 (滚动 30 天) 周期。 |
| 每月 R28 | 每个数据点表示给定的 R28 (滚动 28 天) 周期。 |
| 每周 R7| 每个数据点表示给定的 R7 (滚动 7 天) 周期。 |
| 每天 | 每个数据点表示给定的 R1 (滚动 1 天) 周期。 |

### <a name="usage-by-platform-and-os"></a>按平台和 OS 的使用情况

“**按平台和操作系统** 使用情况”图表显示应用在各种终结点（如 **Windows**、**Mac**、**iOS**、**Android** 和 **Web**）中的活动使用情况。 同一用户或租户可以在多个终结点上使用应用。 每个数据点表示给定的 R30 (滚动 30 天) 周期。

 :::image type="content" source="../../assets/images/tdp/usage-by-platform-OS.png" alt-text="平台":::

### <a name="usage-by-retention-state"></a>按保留状态的使用情况

通过 **保留状态** 图的使用情况，可以跟踪应用随时间推移的四个关键保留或变动指标。

:::image type="content" source="../../assets/images/tdp/usage-by-retention-state.png" alt-text="保留":::

| 跃点数 | 定义 |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| 新用户或租户 | 新手且未使用应用的活动用户或租户。 |
| 返回用户或租户 | 在给定 R30 期间使用应用的活动用户或租户 (滚动 30 天) 时间段和紧接之前的 R30 时间段。 |
| 复活的用户或租户 | 以前使用过你的应用一次或多次但未在前面的 R30 时间段内使用你的应用的活动用户或租户。 |
| 已失效的用户或租户 | 活动用户或租户在给定的 R30 时间段内未出现，但在前面的 R30 时间段内出现。 |

### <a name="usage-intensity"></a>使用强度

**使用强度** 图表显示应用的主要使用强度指标。

 :::image type="content" source="../../assets/images/tdp/usage-intensity.png" alt-text="强度":::

| 跃点数 | 定义 |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| 每月使用的中值天数 | 在上一个 R30 (滚动 30 天) 时间段内打开应用的天数中位数。 |
| 5 天以上使用率的百分比 | 在过去 R30 时间段内打开或使用应用超过五天的活动用户的百分比。 |
| DAU/MAU | 每天使用应用的唯一用户或租户的平均数之比除以所选 R30 时间段的每月活动用户。 |

### <a name="app-dashboard"></a>应用仪表板

“ **我的应用”仪表板** 表显示前四个类别下每个指标的最新 R30 (滚动 30 天) 数据，以及“月月更改”。 使用左上角的时间选取器并选择所需的日期，可以查看过去 75 天和月末 R30 数据的每日 R30 数据，最长时间为 12 个月。

可以选择每个 **指标名称** ，查看随时间推移的趋势。

 :::image type="content" source="../../assets/images/tdp/app-dashboard.png" alt-text="应用程序":::

## <a name="use-tools-to-create-app-features"></a>使用工具创建应用功能

开发人员门户还包括各种工具来帮助你构建 Teams 应用的一些关键功能。 其中的一些工具包括：

* **场景工作室**：为 Teams 会议设计 [自定义的同框场景模式场景](~/apps-in-teams-meetings/teams-together-mode.md)。
* **自适应卡片编辑器**：创建和预览自适应卡片以包含在你的应用中。
* **Microsoft 身份平台管理**：向 Azure Active Directory 注册应用，以帮助用户登录并提供对 API 的访问权限。

## <a name="see-also"></a>另请参阅

[Microsoft Teams 应用随附 SaaS 产品/服务](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
