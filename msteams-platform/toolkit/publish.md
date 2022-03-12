---
title: 使用 Teams 工具包发布 Teams 应用
author: zyxiaoyuer
description: 发布Teams应用程序
ms.author: yanjiang
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: c705e9fe724a21d5159092f813157cee78d6dbe9
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453591"
---
# <a name="publish-teams-apps-using-teams-toolkit"></a>使用 Teams 工具包发布 Teams 应用

创建应用后，你可以将应用分发到不同的作用域，例如个人、团队、组织或任何人。 分布取决于多个因素，包括需求、业务和技术要求以及应用的目标。 分发到不同范围可能需要不同的审阅过程。 通常，范围越大，应用需要经过的针对安全性和合规性问题审查的就更多。

## <a name="prerequisite"></a>先决条件

* [安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

> [!TIP]
> 确保你拥有Teams VS 代码中的应用项目。

## <a name="publish-to-individual-scope-or-sideload-permission"></a>发布到单个范围或旁加载权限

用户可以将自定义应用Teams *.zip文件直接上载到团队或个人上下文中。。 通过上传应用包添加自定义应用称为旁加载，允许你在应用准备好广泛分发之前，在开发期间测试应用，如以下方案所述：

* 在本地测试和调试应用。
* 自己生成应用，例如自动化工作流。
* 为一小组用户（如工作组）生成应用。

你可以构建一个仅供内部使用的应用程序，并与你的团队共享它，而无需Teams应用程序目录中的 Teams 应用程序目录。

**生成应用以.zip *应用包文件**

可以通过从树视图的部署中选择来`Zip Teams metadata package`生成应用Teams Toolkit。 需要先 `Provision in the cloud` 运行。 生成的应用包将位于 中 `{your project folder}/build/appPackage/appPackage.{env}.zip`。

执行以下步骤以上传应用包：

1. 在 Teams 客户端 **中，选择** 左侧栏中的"应用"。
2. 选择 **"管理应用"**。
3. 选择 **"发布应用"**

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pub.png" alt-text="发布":::

4. 选择 **Upload自定义应用：**

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/uplo.png" alt-text="upload":::

## <a name="publish-to-your-organization"></a>发布到组织

当应用准备好在生产中使用时，可以使用 Teams 应用提交 API 提交应用，该 API 从 Graph API（集成开发环境 (IDE) 如 Microsoft Visual Studio Code 与 Teams 工具包一起安装）。 You can either select **Publish to Teams** from **DEPLOYMENT** in TreeView of Teams Toolkit， or trigger **Teams： Publish to Teams** from command palette. 然后选择 **"为组织安装"**：

![为组织安装](./images/installforyourorganization.png)

该应用可在管理中心的管理 **Microsoft Teams** 中提供，你和管理员可在其中查看和批准它。

作为管理员，**在** Microsoft Teams 管理中心中 [](https://admin.teams.microsoft.com/policies/manage-apps)管理应用是查看和管理组织Teams应用的地方。 可以查看应用程序的组织级别状态和属性、批准新的自定义应用或将其上载到组织的应用商店、在组织级别阻止或允许应用、将应用添加到团队、购买第三方应用的服务、查看应用请求的权限、向应用授予管理员同意以及管理 [组织](https://admin.teams.microsoft.com/policies/manage-apps)范围的应用设置。

Teams基于 Teams 应用提交 API 构建的 Visual Studio Code 工具包，它允许自动执行 Teams 上自定义应用的提交到审批过程。

> [!NOTE]
> 该应用尚未发布到组织的应用商店。 该步骤将应用提交到Microsoft Teams管理中心，你可以在这里批准它以发布到组织的应用商店。

## <a name="admin-approval-for-teams-apps"></a>管理员对应用Teams审批

然后，Teams租户的管理员可以转到 Microsoft Teams 管理中心中的管理应用，在左侧导航栏中，转到Teams应用>管理应用。 可以查看组织的所有Teams应用程序。 在页面顶部的"待审批"小部件中，你可以了解何时提交自定义应用进行审批。
在表中，新提交的应用自动发布已提交和已阻止应用的状态。 你可以按降序对发布状态列进行排序以查找应用：

 :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/admin-approval-for-teams-app-1.png" alt-text="审批":::

选择应用名称以转到应用详细信息页面。 On the About tab， you can view details about the app， including description， status， and app ID：

 :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/about-submitted-app-1.png" alt-text="已提交应用":::

执行以下步骤以发布应用：

1. 在管理中心左侧导航Microsoft Teams，转到Teams管理>**应用"**。
2. 选择要转到应用详细信息页面的应用名称，然后在状态框中选择"发布 **"**。
发布应用后，发布状态将更改为已发布，状态将自动更改为允许。

## <a name="publish-to-microsoft-store"></a>发布到 Microsoft Store

你可以将应用直接分发到 Microsoft Teams 内的应用商店，可以覆盖全球数百万用户。 如果在应用商店你的应用得到特别推荐，则可以立即联系潜在客户。 发布到应用商店的应用Teams Microsoft AppSource 自动列出，Microsoft AppSource 是应用和解决方案Microsoft 365官方市场。

有关详细信息，请参阅[发布到 microsoft Teams Store]([Publish your app to the Microsoft Teams store](../concepts/deploy-and-publish/appsource/publish.md#publish-your-app-to-the-microsoft-teams-store))

## <a name="see-also"></a>另请参阅

* [管理多个环境](TeamsFx-multi-env.md)
* [与其他开发人员协作处理Teams项目](TeamsFx-collaboration.md)
