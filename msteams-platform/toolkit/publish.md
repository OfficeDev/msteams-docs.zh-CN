---
title: 使用 Teams 工具包发布 Teams 应用
author: zyxiaoyuer
description: 在本模块中，了解如何使用 Teams 工具包发布 Teams 应用并发布到单个范围或旁加载权限
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 6c0f296549dc325548314e74f1f3ca7017b7aef0
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2022
ms.locfileid: "66485354"
---
# <a name="publish-teams-apps-using-teams-toolkit"></a>使用 Teams 工具包发布 Teams 应用

创建应用后，可以将应用分发到不同的范围，例如个人、团队、组织或任何人员。 分发取决于多种因素，包括需求、业务和技术要求以及应用的目标。 分发到不同范围可能需要不同的审核流程。 一般而言，范围越大，应用就越需要针对安全性和合规性问题进行审核。

## <a name="prerequisite"></a>先决条件

* [安装 Teams 工具包](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) 版本 v3.0.0+。

> [!TIP]
> 确保 VS Code 中有 Teams 应用项目。

## <a name="publish-to-individual-scope-or-sideload-permission"></a>发布到个人范围或旁加载权限

用户可以将 *.zip 文件中的应用包直接上传到团队或个人上下文，从而将自定义应用添加到 Teams。 上传应用包以添加自定义应用称为旁加载，且允许在应用准备好广泛分发之前，在开发时测试应用，如以下场景中所述:

* 在本地测试并调试应用。
* 为自己生成应用，例如自动执行工作流。
* 为一小部分用户(例如工作组)生成应用。

可以生成仅供内部使用的应用，并将其与团队共享，无需将其提交到 Teams 应用商店的 Teams 应用目录中。

**要将应用生成为 *.zip应用包文件**

可以从 Teams 工具包树视图中的“**部署**”选择“`Zip Teams metadata package`”，从而生成应用包。 需要先运行 `Provision in the cloud`。 生成的应用包将位于 `{your project folder}/build/appPackage/appPackage.{env}.zip` 中。

执行以下步骤以上传应用包:

1. 在 Teams 客户端中，在左栏中选择“**应用**”。
2. 选择“**管理应用**”。
3. 选择 **发布应用**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pub.png" alt-text="发布":::

4. 选择“**上传自定义应用**”:

   “:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/uplo.png" alt-text="上传":::”

## <a name="publish-to-your-organization"></a>发布到组织

当应用准备好用于生产时，可以使用 Teams 应用提交 API 提交应用。该 API 从 Graph API 调用，为集成开发环境(IDE)，例如随 Teams 工具包一同安装的 Microsoft Visual Studio 代码。 可以从 Teams 工具包树视图中的“**部署**”选择“**发布到 Teams**”，或从命令面板触发“**Teams: 发布到 Teams**”。 然后，选择“**为组织安装**”:

![为组织安装](./images/installforyourorganization.png)

应用在 Microsoft Teams 管理中心的 **管理应用** 中提供，你和管理员可以在其中审核并批准应用。

作为管理员，可以在 [Microsoft Teams 管理中心](https://admin.teams.microsoft.com/policies/manage-apps) 的 **管理应用** 中查看并管理组织的所有 Teams 应用。 可以查看应用的组织级别状态和属性、批准新的自定义应用或将其上传到组织的应用商店、在组织级别阻止或允许应用、将应用添加到团队、购买第三方应用的服务、查看应用请求的权限、向应用授予管理员同意以及 [管理组织范围内的应用设置](https://admin.teams.microsoft.com/policies/manage-apps)。

基于 Teams 应用提交 API 构建的适用于 Visual Studio Code 的 Teams 工具包，它允许在 Teams 上自动执行自定义应用的提交到审批流程。

> [!NOTE]
> 应用尚未发布到组织的应用商店。 该步骤会将应用提交到 Microsoft Teams 管理中心，你可以在其中批准该应用，从而发布到组织的应用商店。

## <a name="admin-approval-for-teams-apps"></a>Teams 应用的管理员审批

然后，Teams 租户的管理员可以转到 Microsoft Teams 管理中心的“**管理应用**”，在左侧导航栏中，转到“Teams 应用”>“管理应用”。 可以查看组织的所有 Teams 应用。 在页面顶部的“挂起审批”小组件中，可以了解提交自定义应用以供审批的时间。
在该表中，新提交的应用会自动发布已提交和已阻止的应用的状态。 可以按降序对发布状态列进行排序，从而查找应用:

 “:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/admin-approval-for-teams-app-1.png" alt-text="审批":::”

选择应用名称以转到应用详细信息页。 在“关于”选项卡上，可以查看有关应用的详细信息，包括描述、状态和应用 ID:

 :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/about-submitted-app-1.png" alt-text="已提交的应用":::

执行以下步骤以发布应用:

1. 在 Microsoft Teams 管理中心的左侧导航栏中，转到 “Teams 应用”>“**管理应用**”。
2. 选择应用名称以转到应用详细信息页面，然后在状态框中，选择“**发布**”。
发布应用后，发布状态会更改为“已发布”，且状态会自动更改为“已允许”。

## <a name="publish-to-microsoft-store"></a>发布到 Microsoft store

你可以将应用直接分发到 Microsoft Teams 内的应用商店，可以覆盖全球数百万用户。 如果在应用商店你的应用得到特别推荐，则可以立即联系潜在客户。 发布到 Teams 应用商店的应用也会自动在 Microsoft AppSource 上列出，后者是 Microsoft 365 应用和解决方案的官方市场。

有关详细信息，请参阅 (将 [应用发布到 Microsoft Teams 应用商店](../concepts/deploy-and-publish/appsource/publish.md#publish-your-app-to-the-microsoft-teams-store)) 。

## <a name="see-also"></a>另请参阅

* [管理多个环境](TeamsFx-multi-env.md)
* [在 Teams 项目中与其他开发人员协作](TeamsFx-collaboration.md)
