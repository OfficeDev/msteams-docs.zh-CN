---
title: 使用开发人员门户管理应用
description: 了解如何使用开发人员门户 for Microsoft Teams 配置、分发和管理Microsoft Teams。
keywords: 开发人员门户团队入门
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 52a6f925caa8296908febdb2b963edcf2de2eba3
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2022
ms.locfileid: "63399322"
---
# <a name="manage-your-apps-with-the-developer-portal-for-microsoft-teams"></a>使用 Microsoft Teams 开发人员门户管理应用

开发人员<a href="https://dev.teams.microsoft.com" target="_blank">门户Teams</a>应用程序是配置、分发和管理 Microsoft Teams 应用程序的主要工具。 通过开发人员门户，你可以与应用上的同事协作、设置运行时环境等。

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="显示开发人员门户主页的屏幕截图Teams。":::

> [!NOTE]
> 目前，开发人员门户不适用于 政府社区云 (GCC) 、GCC-High 或国防部 (DOD) 租户。

## <a name="register-an-app"></a>注册应用

开发人员门户提供了几种注册应用Teams方法：

* 注册全新的应用
* 导入现有应用包

> [!NOTE]
> 如果使用 Microsoft Teams Toolkit [for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) 创建应用，可以在开发人员门户中管理该应用。

## <a name="set-up-an-environment"></a>设置环境

你可以配置环境和全局变量，以帮助将应用从本地运行时转换到生产环境。 全局变量在所有环境中使用。

若要设置环境：

1. 在开发人员门户中，选择你正在处理的应用。
2. 转到" **环境"** 页，然后选择 **"+ 添加环境"**。
3. 选择 **" + 添加变量** "，为环境创建配置变量。

若要使用变量：

使用变量名称而不是硬编码值来设置应用配置。

1. 在 `{{` 开发人员门户的任何字段中输入。 将显示一个下拉列表，包含为所选环境创建的所有变量以及全局变量。  
1. 在下载应用包 (例如，准备好发布到 Teams 应用商店) 时，请选择想要使用的环境。 应用配置根据环境自动更新。

## <a name="identify-app-owners"></a>确定应用所有者

每个应用都包括 **一个所有者** 页面，可在其中与组织中的同事共享应用注册。 **参与者** 角色具有与所有者 **角色相同的权限** ，但删除应用的能力除外。

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a>配置应用的功能和其他重要元数据

一Teams应用是 Web 应用。 像所有 Web 应用一样，其源代码通常在 IDE 或代码编辑器中开发，并托管在云中的 (Azure) 。

若要在应用程序中安装和呈现Teams，必须包括一组可识别Teams配置。 这通常通过创建应用清单（一个包含显示应用内容Teams元数据的 JSON 文件）完成。 开发人员门户将此过程抽象化，并包括新功能和工具，以帮助你取得更多成功。

## <a name="test-your-app-directly-in-teams"></a>直接在应用中测试Teams

开发人员门户提供用于测试和调试应用的选项：

* 在 **"概述**"页上，你可以看到应用配置是否针对应用商店Teams验证的快照。
* "**在Teams** 中预览"按钮允许你在 Teams 客户端中快速启动应用进行调试。

## <a name="distribute-your-app"></a>分发应用

从开发人员门户中 **，使用"** 分发"按钮下载应用包、发布到组织或发布到 Teams 应用商店。

有关详细信息，请参阅分发[你的Teams应用](~/concepts/deploy-and-publish/apps-publish-overview.md)。

## <a name="analyze-your-apps-usage"></a>分析应用的使用情况

在 **"概述** "页上，你可以看到应用的活动用户总数。 这些指标可用于通过开发人员门户发布到 Teams 商店或组织的应用程序目录的应用，并且范围为应用程序 ID。

| 跃点数 | 定义 |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| *每月 R30* | 默认使用率指标。 它显示了在 UTC 时间滚动 30 天窗口内使用你的应用的唯一活动用户数。 |
| *每天* | 显示以 UTC 格式在给定日期使用应用的唯一活动用户数。 |

显示过去七天、30 天和 60 天的每月使用情况和每日使用情况。 您应在 24-48 小时内看到给定一天的使用情况。 新应用的使用情况最多可能需要 3-5 天才能显示。

## <a name="use-tools-to-create-app-features"></a>使用工具创建应用功能

开发人员门户还包括可帮助你构建应用或应用Teams功能的工具。 其中一些工具包括：

* **Scene studio**：为 [会议设计自定义](~/apps-in-teams-meetings/teams-together-mode.md)一Teams场景。
* **自适应卡片编辑器**：创建和预览要包括在应用的自适应卡片。
* **Microsoft 标识平台管理**：使用 Azure Active Directory 注册应用，以帮助用户登录并提供对 API 的访问权限。

## <a name="see-also"></a>另请参阅

[将 SaaS 产品与Microsoft Teams一起](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
