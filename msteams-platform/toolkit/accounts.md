---
title: 准备帐户以生成Teams应用程序
author: zyxiaoyuer
description: 准备帐户以生成Teams应用程序
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 9dbfa97b892f2234b53eb42b5d5764b8f6fd6e93
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452569"
---
# <a name="prepare-accounts-to-build-teams-apps"></a>准备帐户以生成Teams应用程序

若要开发Teams应用，至少需要一Microsoft 365有效订阅的帐户。 如果你想要在 Azure 上托管后端资源，则需要 Azure 帐户。 如果你的现有应用程序托管在其他云提供商上，并且你想要将现有应用程序集成到其他平台，则 Azure 帐户Teams可选。

## <a name="microsoft-365-account"></a>Microsoft 365 账户

如果你没有具有具有有效订阅Microsoft 365帐户，则可以通过加入开发人员计划Microsoft 365[帐户](https://developer.microsoft.com/microsoft-365/dev-program)。 开发人员Microsoft 365计划包括一Microsoft 365 E5开发人员订阅，可用于创建自己的沙盒和独立于生产环境开发解决方案。

## <a name="azure-account"></a>Azure 帐户

如果你想要在 Azure 中托管应用相关资源或访问资源，则必须具有 Azure 订阅。 可以在 [开始之前创建一](https://azure.microsoft.com/free/) 个免费帐户。

## <a name="join-microsoft-365-developer-program"></a>加入Microsoft 365开发人员计划

如果你没有帐户，则必须Microsoft 365开发人员计划订阅Microsoft 365[注册](https://developer.microsoft.com/microsoft-365/dev-program)。 订阅将免费 90 天，并持续续订，只要将订阅用于开发活动。 如果你有一个 Visual Studio Enterprise 或 Professional 订阅，则这两个计划均Microsoft 365[开发人员订阅](https://aka.ms/MyVisualStudioBenefits)。 只要你的订阅处于活动状态，Visual Studio就处于活动状态。 有关详细信息，请参阅[设置开发人员Microsoft 365订阅](https://developer.microsoft.com/microsoft-365/dev-program)。

1. 转到开发人员[Microsoft 365计划](https://developer.microsoft.com/microsoft-365/dev-program)。
2. 选择 **"立即加入"**。
3. 选择 **"设置 E5 订阅"**。
4. 设置管理员帐户。 完成后，应看到以下屏幕：

:::image type="content" source="./images/m365-developer-program.png" alt-text="显示 Microsoft 365 程序的关系图":::

## <a name="accounts-for-microsoft-365-developer-program"></a>开发人员计划Microsoft 365帐户

你可以使用以下帐户类型之一注册开发人员计划：

* **Microsoft 个人使用帐户**

  提供对面向消费者的所有 Microsoft 产品和云服务的访问，如 Outlook、Messenger、OneDrive、MSN、Xbox Live 或 Microsoft 365。 注册一个 Outlook.com 邮箱将自动创建一个 Microsoft 帐户。 创建 Microsoft 帐户后，可以用于访问消费者相关的 Microsoft 云服务或 Azure。

* **业务工作帐户**

  提供对所有小型、中型和企业业务级别 Microsoft 云服务（如 Azure、Microsoft Intune 或 Microsoft 365） 的访问权限。 当你作为组织注册这些服务之一时，基于云的目录将自动预配在Microsoft Azure Active Directory (Azure AD) 以代表你的组织。

* **Visual Studio ID**

  你可以为 Visual Studio Professional 或 Enterprise 订阅创建 - 我们建议使用此选项加入 Visual Studio 库中的开发人员计划，以作为 Visual Studio 订阅者获得全部权益。

## <a name="teams-customer-app-upload-or-sideload-permission"></a>Teams客户应用上传或旁加载权限

> [!IMPORTANT]
> 在开发期间，你必须在应用程序内加载Teams而不分发它。 这称为 **旁加载**。

以下列表提供了检查是否启用了旁加载应用权限的步骤。 两种不同的方式如下所示：

* **使用 Microsoft Visual studio 代码**

    1. 打开 **Visual Studio Code**。
    1. Select **Teams Toolkit** from left panel.
    1. 选择 **帐户** 并登录到你的Microsoft 365帐户。
    1. 检查是否可以看到"旁 **加载已启用"** 选项，如图所示：

       :::image type="content" source="../assets/images/teams-toolkit-v2/sideloading.png" alt-text="启用旁加载":::

* **使用Teams帐户**

    1. 打开 **Microsoft Teams**。
    2. 在 **左侧栏中** 选择"应用"。
    3. 选择 **"发布应用"**。

       :::image type="content" source="../assets/images/teams-toolkit-v2/publish.png" alt-text="发布应用":::

    4. 检查你是否可以看到自定义 **Upload选项，** 如图所示：

       :::image type="content" source="../assets/images/teams-toolkit-v2/upload.png" alt-text="Upload自定义应用":::

如果看不到自定义Upload选项，这表示你没有旁加载权限。 如果没有旁加载权限，将无法执行任何本地或远程调试。 因此，在针对你的应用执行任何调试之前，获取帐户的旁加载权限Teams非常重要。 如果你是租户管理员，你可以打开租户或组织的旁加载设置。 如果你不是管理员，请联系租户管理员获得权限。

## <a name="enable-custom-app-uploading-for-your-organization"></a>为组织启用自定义应用上传

> [!IMPORTANT]
> 若要为开发人员租户启用自定义应用上传或旁加载，你必须是租户的管理员。

1. 登录以[Microsoft 365 管理中心](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)管理员凭据登录。

2. 选择 **"全部显示Teams** > "。

   :::image type="content" source="../assets/images/teams-toolkit-v2/5.png" alt-text="全部显示":::

> [!NOTE]
> 可能需要 **24 小时才能显示****Teams选项。** 可以将[自定义应用上传到Teams环境中](/microsoftteams/upload-custom-apps)进行测试和验证。

3. 导航到 **Teams** **appsSetup** >  **PoliciesGlobal** > 。

   :::image type="content" source="../assets/images/teams-toolkit-v2/3.png" alt-text="set ies":::

4. 将Upload应用切换至 **"打开"** 位置。

   :::image type="content" source="../assets/images/teams-toolkit-v2/4.png" alt-text="切换":::

5. 选择“**保存**”。

> [!Note]
> 旁加载可能需要 24 小时才能处于活动状态。 在此期间，可以使用租户 **的上传功能** 测试应用。 若要上传.zip包文件，请参阅上传 [自定义应用](/microsoftteams/teams-app-setup-policies)。

有关详细信息，请参阅在应用中[管理自定义应用策略和](/microsoftteams/teams-custom-app-policies-and-settings)Teams在应用中管理应用[Teams。](/microsoftteams/teams-app-setup-policies)

## <a name="see-also"></a>另请参阅

* [新建Teams项目](create-new-project.md)
* [预配云资源](provision.md)
