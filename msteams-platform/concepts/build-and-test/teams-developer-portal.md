---
title: 使用开发人员门户管理应用
description: 了解如何使用 Microsoft Teams 开发人员门户配置、分发和管理你的应用。
keywords: 开始使用, 开发人员门户, Teams
ms.localizationpriority: high
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: f55ecd7e44760a353a6058e004ea3cf6cdb769b2
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111792"
---
# <a name="manage-your-apps-with-the-developer-portal-for-microsoft-teams"></a>使用 Microsoft Teams 开发人员门户管理应用

<a href="https://dev.teams.microsoft.com" target="_blank">Teams 开发人员门户</a>是配置、分发和管理 Microsoft Teams 应用的主要工具。 借助开发人员门户，你可以在应用上与同事协作、设置运行时环境等。

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="显示 Teams 开发人员门户主页的屏幕截图。":::

> [!NOTE]
>
> * 目前，开发人员门户不适用于政府社区云 (GCC)、GCC High 或国防部 (DOD) 租户。
> * 但是，可以使用常规租户在开发人员门户中构建应用、下载应用，并使用 [Microsoft Graph](/graph/api/teamsapp-publish?view=graph-rest-1.0&tabs=http&preserve-view=true) 将应用上传到国家云。 有关详细信息，请参阅[国家云部署](/graph/deployments)。

## <a name="register-an-app"></a>注册应用

开发人员门户提供了几种方法来注册 Teams 应用：

* 注册全新的应用
* 导入现有的应用包

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

## <a name="use-tools-to-create-app-features"></a>使用工具创建应用功能

开发人员门户还包括各种工具来帮助你构建 Teams 应用的一些关键功能。 其中的一些工具包括：

* **场景工作室**：为 Teams 会议设计 [自定义的同框场景模式场景](~/apps-in-teams-meetings/teams-together-mode.md)。
* **自适应卡片编辑器**：创建和预览自适应卡片以包含在你的应用中。
* **Microsoft 身份平台管理**：向 Azure Active Directory 注册应用，以帮助用户登录并提供对 API 的访问权限。

## <a name="see-also"></a>另请参阅

[Microsoft Teams 应用随附 SaaS 产品/服务](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
