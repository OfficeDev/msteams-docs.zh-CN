---
title: 使用开发人员门户管理应用
description: 了解如何使用开发人员门户管理Microsoft Teams。
keywords: 开发人员门户团队入门
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 41aade2eaedee2095e60288a7e4021897bb1a3fa
ms.sourcegitcommit: ece03efbb0e9d1fea5bd01c9c05a2bc232c1a1c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2021
ms.locfileid: "60378910"
---
# <a name="manage-your-apps-with-the-developer-portal-for-microsoft-teams"></a>使用开发人员门户管理应用Microsoft Teams

开发人员<a href="https://dev.teams.microsoft.com" target="_blank">门户Teams</a>是配置、分发和管理应用的主要Microsoft Teams工具。 通过开发人员门户，你可以与应用上的同事协作、设置运行时环境等。

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="显示开发人员门户主页的屏幕截图Teams。":::

## <a name="register-an-app"></a>注册应用

可以通过以下Teams在开发人员门户中注册你的应用程序：

* 注册新应用
* 导入现有应用包

> [!NOTE]
> 如果使用 Microsoft Teams Toolkit [for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)创建应用，可以在开发人员门户中管理该应用。

## <a name="set-up-an-environment"></a>设置环境

你可以配置环境和全局变量，以帮助将应用从本地运行时转换到生产环境。 全局变量在所有环境中使用。

**配置环境**

1. 在开发人员门户中，选择你正在处理的应用。
2. 转到"**环境"，** 然后选择 **"+ 添加环境"。**
3. 选择 **" + 添加变量** "，为环境创建配置变量。

**使用变量**

使用变量名称而不是硬编码值来设置应用配置。

1. 在 `{{` 开发人员门户的任何字段中输入。 将显示一个下拉列表，包含为所选环境创建的所有变量以及全局变量。  
1. 在下载应用包 (例如，准备好发布到 Teams 应用商店) 时，请选择想要使用的环境。 应用配置根据环境自动更新。 

## <a name="identify-app-owners"></a>确定应用所有者

每个应用 **都包括所有者**，可在其中与组织同事共享应用注册。 **参与者** 角色具有与所有者 **角色相同的权限**，但删除应用的能力除外。

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a>配置应用的功能和其他重要元数据

一Teams应用是 Web 应用。 像所有 Web 应用一样，其源代码通常在 IDE 或代码编辑器中开发，并托管在云中的 (Azure) 。

若要在应用程序中安装和呈现Teams，必须包括一组可识别Teams配置。 这通常通过创建应用清单（一个 JSON 文件）完成，其中包含显示应用Teams所需的所有元数据。 开发人员门户将此过程抽象化，并包括新功能和工具，以帮助你取得更多成功。

### <a name="basic-app-configuration"></a>基本应用配置 

**基本应用信息：** 用户在应用详细信息页面上看到Teams，例如应用 ID、应用名称、说明、开发人员信息、版本、应用 URL 和 Microsoft 合作伙伴网络 ID。

**品牌打造：** 应用需要 PNG 格式的颜色和大纲图标。 若要在应用商店中Teams应用，图标必须满足特定大小要求。

**功能** Teams可以包含在应用中的一些功能。 你可以添加一个或多个功能，具体取决于应用的用例。

**权限：** 指定在使用你的应用时用户必须同意哪些内容。

**单一登录：** 将应用配置为使用 SSO (单一登录) 。

**域：** 列出应用需要导航到的所有域。 使用通配符包括多个子域。 例如，`*.example.com`。

### <a name="advanced-app-configuration"></a>高级应用配置

**应用内容：** 为应用配置可选功能，如加载指示器和全屏模式。

**应用自定义：** 选择管理员Teams应用自定义的属性。

**第一方设置：** 超出公共功能的第一方应用程序的功能。

### <a name="distribute-your-app"></a>分发应用

**应用包：** 应用包介绍了应用配置、功能、必需资源以及其他重要属性。 例如，清单架构。

**航班：** 控制获取应用更新的人。 例如，你可以向 Microsoft 员工发布更新，以在将 Bug 发布给公众之前识别和修复 Bug。

**通过 Microsoft (发布到) ：** 使应用可供组织人员使用。 IT 管理员批准后，你的应用将在"专为Teams构建的应用>下特别推荐。

**发布到Teams应用商店：** 应用验证工具在查看你的应用时，根据 Microsoft 使用的测试用例检查你的应用包。 解决错误或警告，在提交之前阅读检查表。

## <a name="test-your-app-directly-in-teams"></a>直接在应用中测试Teams

开发人员门户提供用于测试和调试应用的选项：

* 在 **"** 概述"中，你可以看到应用配置是否针对应用商店Teams验证的快照。
* **在 Teams** 预览允许你在 Teams 客户端中快速启动应用进行调试。

## <a name="distribute-your-app"></a>分发应用

从开发人员门户中，使用 **分发下载** 应用包、发布到组织或发布到 Teams 应用商店。

有关详细信息，请参阅分发[你的Teams应用](~/concepts/deploy-and-publish/apps-publish-overview.md)。

## <a name="analyze-your-apps-usage"></a>分析应用的使用情况

在 **"** 概述"中，你可以看到你的应用的活动用户总数。 这些指标可用于通过开发人员门户发布到Teams应用商店或组织的应用程序目录，并且范围为应用 ID。

| 跃点数 | 定义 |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| *每月 R30* | 默认使用率指标。 它显示唯一活动用户数，这些用户已在此滚动 30 天窗口（采用 UTC）内使用过你的应用。 |
| *每天* | 显示唯一活动用户数，这些用户已使用采用 UTC 的给定日期的应用。 |

显示过去七天、30 天和 60 天的每月使用情况和每日使用情况。 您应在 24-48 小时内看到给定一天的使用情况。 新应用的使用情况最多可能需要 3-5 天才能显示。

## <a name="use-tools-to-create-app-features"></a>使用工具创建应用功能

开发人员门户还包括可帮助你构建应用应用Teams功能的工具。 其中一些工具包括：

* **Scene studio：** 为 [会议设计自定义](~/apps-in-teams-meetings/teams-together-mode.md)一Teams场景。
* **自适应卡片编辑器**：创建和预览要包括在应用的自适应卡片。
* **Microsoft 标识平台管理**：使用 Azure Active Directory (Azure AD) 注册应用，以帮助用户登录并提供 API 访问权限。

## <a name="see-also"></a>另请参阅

[将 SaaS 产品/服务与Microsoft Teams一起](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
