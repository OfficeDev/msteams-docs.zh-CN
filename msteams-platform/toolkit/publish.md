---
title: 使用 Teams 工具包发布 Teams 应用
author: zyxiaoyuer
description: 在本模块中，了解如何使用 Teams 工具包发布 Teams 应用并发布到单个范围或旁加载权限
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 6188072b2d4ca73aae4e7ea91715869d968a9b9c
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616718"
---
# <a name="publish-teams-apps-using-teams-toolkit"></a>使用 Teams 工具包发布 Teams 应用

创建应用后，可以将应用分发到不同的范围，例如个人、团队、组织或任何人员。 分布取决于多种因素，例如需求、业务和技术要求，以及应用的目标。 分发到不同范围可能需要不同的审核流程。 一般而言，范围越大，应用就越需要针对安全性和合规性问题进行审核。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/publish-flow.png" alt-text="发布流":::

本部分将介绍以下内容：

* [发布到个人范围或旁加载权限](#publish-to-individual-scope-or-sideload-permission)
* [发布到组织](#publish-to-your-organization)
* [发布到 Microsoft Teams 应用商店](#publish-to-microsoft-teams-store)

## <a name="prerequisites"></a>先决条件

* 请确保创建[应用包](~/concepts/build-and-test/apps-package.md)，并[验证其](https://dev.teams.microsoft.com/appvalidation.html)是否存在错误。
* 在 Teams 中 [启用自定义应用上传](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。
* 确保应用正在运行并可使用 HTTPs 进行访问。
* 确保遵循了将应用发布到 Microsoft Teams 应用商店以发布应用的一组准则。

## <a name="publish-to-individual-scope-or-sideload-permission"></a>发布到个人范围或旁加载权限

可以通过将 *.zip 文件中的 [应用包](../concepts/build-and-test/apps-package.md) 直接上传到团队或个人上下文，将自定义应用添加到 Teams。 通过上传应用包添加自定义应用称为旁加载。 它允许你在 Teams 中上传时测试应用。 可在以下方案中生成和测试应用：

* 在本地测试并调试应用。
* 为自己生成应用，例如自动执行工作流。
* 为一小部分用户(例如工作组)生成应用。

可以生成仅供内部使用的应用，并将其与团队共享，无需将其提交到 Teams 应用商店的 Teams 应用目录中。 有关详细信息，请参阅 [Teams 中的上传应用](../concepts/deploy-and-publish/apps-upload.md)。

### <a name="to-build-your-app-to-zip-app-package-file"></a>生成应用以压缩应用包文件

在生成应用包之前，需要先运行 `Provision in the cloud` 。 以下步骤可帮助你生成应用包。

* 选择 **“部署**”下的 **Zip Teams 元数据包**。<br>
    生成的应用包将位于 `{your project folder}/build/appPackage/appPackage.{env}.zip` 中。

### <a name="to-upload-app-package"></a>上传应用包

执行以下步骤以上传应用包:

1. 在 Teams 客户端中，选择“ **应用** > **管理应用** > **”上传应用**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/publish1.png" alt-text="发布应用":::

   **将显示“上传应用** ”窗口。

2. 选择“**上传自定义应用**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/upload.png" alt-text="上传应用":::

   现在，应用已旁加载到 Teams 客户端，你可以添加和查看它。

## <a name="publish-to-your-organization"></a>发布到组织

当应用准备好在生产环境中使用时，可以使用从图形 API调用的 Teams 应用提交 API 提交应用。 Teams 应用提交 API 是一个集成开发环境， (IDE) ，例如使用 Teams 工具包安装的 Microsoft Visual Studio Code。 以下步骤可帮助你将应用发布到组织：

* [从 Teams 工具包发布](#publish-from-teams-toolkit)
* [批准管理员中心](#approve-on-admin-center)

### <a name="publish-from-teams-toolkit"></a>从 Teams 工具包发布

以下步骤可帮助你从 Teams 工具包发布应用：

1. 可以通过以下方式之一发布 Teams 应用：
     * 在 Teams 工具包的树视图中选择 **“发布到****部署** 下的 Teams”。
     * 输入触发器 Teams：从命令面板 **发布到 Teams** 。

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-publish.png" alt-text="选择“发布”":::

2 为 **组织选择“安装**”。

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/installforyourorganization.png" alt-text="为组织安装":::

  现在，应用已成功发布到管理门户，你将看到以下通知：

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/confirm-publish.png" alt-text="确认发布":::

  现在，该应用在 Microsoft Teams 管理中心的 **管理应用** 上可用，你和管理员可以在此处查看和批准它。

  > [!NOTE]
  > 应用尚未发布到组织的应用商店。 该步骤会将应用提交到 Microsoft Teams 管理中心，你可以在其中批准该应用，从而发布到组织的应用商店。

### <a name="approve-on-admin-center"></a>批准管理员中心

基于 Teams 应用提交 API 构建Visual Studio Code Teams 工具包，它允许你在 Teams 上自动执行自定义应用的提交到审批过程。

  > [!NOTE]
  > 确保 VS Code 中有 Teams 应用项目。 作为管理员，可以在 [Microsoft Teams 管理中心](https://admin.teams.microsoft.com/policies/manage-apps) 的 **管理应用** 中查看并管理组织的所有 Teams 应用。 可以在管理中心执行以下活动：
  >
  > * 请参阅应用的组织级别状态和属性。
  > * 批准或将新的自定义应用上传到组织的应用商店。
  > * 阻止或允许组织级别的应用。
  > * 将应用添加到 Teams。
  > * 购买第三方应用的服务。
  > * 查看应用请求的权限。
  > * 向应用授予管理员许可。
  > * [管理组织范围的应用设置](https://admin.teams.microsoft.com/policies/manage-apps)。

以下步骤可帮助你从管理员中心批准：

1. 选择 **“转到管理门户**”。

1. :::image type="icon" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/Showall.PNG":::选择 Teams **应用****管理应用** > >图标。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manage-apps.png" alt-text="选择“管理应用”":::

   可以查看组织的所有 Teams 应用。

   在页面顶部的“挂起审批”小组件中，可以了解提交自定义应用以供审批的时间。 在表中，新提交的应用会自动发布已提交和阻止的应用的状态。 可以按降序对发布状态列进行排序以查找应用。

   “:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/admin-approval-for-teams-app-1.png" alt-text="审批":::”

1. 选择应用名称以转到应用详细信息页。 在“ **关于”** 选项卡上，可以查看有关应用的详细信息，包括说明、状态和应用 ID。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/about-submitted-app-1.png" alt-text="已提交的应用":::

1. 选择状态下拉列表，然后从 **“提交** ”更改为 **“发布**”。

   发布应用后，发布状态会更改为“已发布”，且状态会自动更改为“已允许”。

   有关详细信息，请参阅[“发布到组织](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2Fmicrosoftteams%2Fplatform%2Fbreadcrumb%2Ftoc.json)”

## <a name="publish-to-microsoft-teams-store"></a>发布到 Microsoft Teams 应用商店

你可以将应用直接分发到 Microsoft Teams 内的应用商店，可以覆盖全球数百万用户。 如果在应用商店你的应用得到特别推荐，则可以立即联系潜在客户。 发布到 Teams 应用商店的应用也会自动在 Microsoft AppSource 上列出，后者是 Microsoft 365 应用和解决方案的官方市场。

有关详细信息，请参阅 [将应用发布到 Microsoft Teams 应用商店](../concepts/deploy-and-publish/appsource/publish.md#publish-your-app-to-the-microsoft-teams-store)。

## <a name="see-also"></a>另请参阅

* [分发 Microsoft Teams 应用](../concepts/deploy-and-publish/apps-publish-overview.md)
* [创建 Teams 应用包](../concepts/build-and-test/apps-package.md)
* [准备 Microsoft 365 租户](../concepts/build-and-test/prepare-your-o365-tenant.md)
* [将应用发布到 Microsoft Teams 商店](../concepts/deploy-and-publish/appsource/publish.md)
* [在 Teams 中上传应用](../concepts/deploy-and-publish/apps-upload.md)
* [在 Microsoft Teams 管理中心管理 Teams 应用](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2Fmicrosoftteams%2Fplatform%2Fbreadcrumb%2Ftoc.json)
