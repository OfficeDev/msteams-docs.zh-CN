---
title: 准备帐户以生成 Teams 应用
author: zyxiaoyuer
description: 在本模块中，了解如何准备帐户以使用 Microsoft 365 帐户和开发人员计划生成 Teams 应用。 用于托管后端资源的 Azure 帐户
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: f359488788c31941ea90bedb02c710c28fb98366
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142211"
---
# <a name="prepare-accounts-to-build-teams-apps"></a>准备帐户以生成 Teams 应用

若要创建和上传 Teams 应用，需要准备以下帐户:

* [具有有效订阅的 Microsoft 365 帐户](accounts.md#microsoft-365-account)
* [在 Azure 上托管后端资源的 Azure 帐户](accounts.md#azure-account-to-host-backend-resources)

## <a name="microsoft-365-account"></a>Microsoft 365 账户

若要创建 Microsoft 365 帐户，请注册 Microsoft 365 开发人员计划订阅。 订阅免费使用 90 天，只要将订阅用于开发活动，就可以继续续订。

如果你有 Visual Studio Enterprise 或 Professional 订阅，则这两个计划都包含免费 Microsoft 365 [开发人员订阅](https://aka.ms/MyVisualStudioBenefits)。 只要你的 Visual Studio 订阅处于活动状态，它就处于活动状态。 有关详细信息，请参阅 [Microsoft 365 开发人员订阅](https://developer.microsoft.com/microsoft-365/dev-program)。

### <a name="microsoft-365-developer-program"></a>Microsoft 365 开发人员计划

若要获取免费的 Teams 开发人员帐户，请加入 Microsoft 365 开发人员计划，并按照步骤操作:

1. 转到 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program)。
2. 选择“**立即加入**”。
3. 选择“**设置 E5 订阅**”。
4. 设置管理员帐户。

   订阅完成后，可以看到以下图像:

    :::image type="content" source="./images/m365-developer-program.png" alt-text="显示 Microsoft 365 计划的图表":::

### <a name="microsoft-365-developer-account-types"></a>Microsoft 365 开发人员帐户类型

可以使用以下帐户类型之一注册开发人员计划:

* **Microsoft 帐户供个人使用**

    该帐户提供对 Microsoft 产品和云服务 (如 Outlook、Messenger、OneDrive、MSN、Xbox Live 或 Microsoft 365) 的访问权限。 可以注册 Outlook.com 邮箱来创建 Microsoft 帐户，该Microsoft 帐户可用于访问与消费者相关的 Microsoft 云服务或 Azure。

* **Microsoft 商业版工作帐户**

     此帐户提供对所有小型、中型和企业业务级别 Microsoft 云服务的访问，如 Azure、Microsoft Intune 或 Microsoft 365。 作为组织注册此类服务时，会在 Azure AD 中自动预配一个基于云的目录，来表示你的组织。

* **Visual Studio 用户 ID**

    Visual Studio Professional 或企业订阅的用户 ID 可用于加入 Visual Studio 库中的开发人员计划，以作为 Visual Studio 订阅者获得全部权益。

## <a name="azure-account-to-host-backend-resources"></a>用于托管后端资源的 Azure 帐户

如果现有应用程序托管在其他云提供商上，并且想要在 Teams 平台上集成现有应用程序，则 Azure 帐户是可选的。

**Visual Studio ID**

若要托管与应用程序相关的资源或访问 Azure 中的资源，可以在开始之前[创建免费帐户](https://azure.microsoft.com/free/)。 或者，可以选择使用另一个云提供程序托管后端资源，或者选择在自己的服务器上进行 (如果这些资源可从公共域中使用)。

## <a name="upload-custom-app"></a>上传自定义应用

> [!IMPORTANT]
> 创建应用后，必须在 Teams 中加载应用，但无需分发它。此过程称为 **旁加载**。

   可以使用 Visual Studio Code 或 Teams 客户端验证是否启用了旁加载权限。

* **使用 Visual Studio Code 验证旁加载权限**

    1. 打开 **Visual Studio Code**。
    2. 从左侧面板中选择 **Teams Toolkit**。 如果看不到该选项，请确保已安装 Teams 工具包扩展。
    3. 选择“**账户**”并登录到你的 Microsoft 365 帐户。
    4. 检查是否可以查看选项“**已启用旁加载**”，如下图所示：

       :::image type="content" source="../assets/images/teams-toolkit-v2/sideloading.png" alt-text="启用旁加载" border="true":::

* **使用 Teams 客户端验证旁加载权限**

    1. 打开 **Microsoft Teams**。
    2. 在左侧面板中选择“**应用**”。
    3. 选择“**发布应用**”。

       :::image type="content" source="../assets/images/teams-toolkit-v2/publish2.png" alt-text="发布应用" border="true":::

    4. 检查是否可以看到选项“**上传自定义应用**”，如下图所示：

       :::image type="content" source="../assets/images/teams-toolkit-v2/upload2.png" alt-text="上传自定义应用" border="true":::

        如果无法查看 **上传自定义应用** 的选项，那么则表明你没有进行旁加载所需的权限。

        * 对于租户管理员，请在 Teams 管理中心为租户或组织启用旁加载设置。
        * 如果你不是租户管理员，则需要联系租户管理员以启用旁加载。

* **使用管理中心上传自定义应用**

  > [!IMPORTANT]
  > 若要为开发人员租户启用自定义应用上传或旁加载，你必须是租户的管理员。

  执行以下步骤上传自定义应用:

  1. 请使用管理员帐户登录到 [Microsoft 365 管理中心](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)。

  2. 选择 **显示全部** > **Teams**。

     :::image type="content" source="../assets/images/teams-toolkit-v2/5.png" alt-text="显示全部" border="true":::

     > [!Note]
     > 可能 **至多 24 小时** 后 **Teams** 选项才会出现。 可以[将自定义应用上传到 Teams 环境](/microsoftteams/upload-custom-apps)进行测试和验证。

  3. 导航到 **Teams 应用** > **设置策略**。

     :::image type="content" source="../assets/images/teams-toolkit-v2/3.png" alt-text="设置策略":::

  4. 将“**上传自定义应用**”切换到“**开**”位置。

     :::image type="content" source="../assets/images/teams-toolkit-v2/4.png" alt-text="切换":::

  5. 选择 **保存**。

     > [!Note]
     > 旁加载最长可能需要 24 小时才能生效。 在此期间，可以使用“**为租户上传**”来测试应用。 若要上传应用的 .zip 包文件，请参阅“[上传自定义应用](/microsoftteams/teams-app-setup-policies)”。

有关详细信息，请参阅[在 Teams 中管理自定义应用策略和设置](/microsoftteams/teams-custom-app-policies-and-settings)和[在 Teams 中管理应用设置策略](/microsoftteams/teams-app-setup-policies)。

## <a name="see-also"></a>另请参阅

* [使用 Teams 工具包创建新的 Teams 应用](create-new-project.md)
* [预配云资源](provision.md)
* [将 Teams 应用部署到云](deploy.md)
* [发布 Teams 应用](../concepts/deploy-and-publish/appsource/publish.md)
* [管理多个环境](TeamsFx-multi-env.md)
