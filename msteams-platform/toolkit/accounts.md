---
title: 准备帐户以生成Teams应用程序
author: zyxiaoyuer
description: 准备帐户以生成Teams应用程序
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 6a215922ff4b89c4afdce187be9b03479e6a54e6
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227966"
---
# <a name="prepare-accounts-to-build-teams-apps"></a>准备帐户以生成Teams应用程序

若要开发Teams应用，至少Microsoft 365一个具有有效订阅的帐户。 如果你想要在 Azure 上托管后端资源，还需要 Azure 帐户。 如果你的现有应用程序托管在其他云提供商上，并且你想要将现有应用程序集成到其他平台，则 Azure 帐户Teams可选。

## <a name="microsoft-365-account"></a>Microsoft 365 帐户

如果你没有具有具有有效订阅Microsoft 365帐户，可以通过加入开发人员计划创建一Microsoft 365[帐户](https://developer.microsoft.com/microsoft-365/dev-program)。 Microsoft 365 开发人员计划包括 Microsoft 365 E5 开发人员订阅，可用于创建自己的沙盒并开发独立于生产环境的解决方案。

## <a name="azure-account"></a>Azure 帐户

如果你想要在 **Azure** 中托管应用相关资源或访问资源，则必须拥有 Azure 订阅。 可以在 [开始之前创建一](https://azure.microsoft.com/free/) 个免费帐户。

## <a name="join-microsoft-365-developer-program"></a>加入Microsoft 365开发人员计划 

如果你没有帐户，则必须Microsoft 365开发人员计划订阅Microsoft 365[注册](https://developer.microsoft.com/microsoft-365/dev-program)。 订阅将免费 90 天，并持续续订，只要将订阅用于开发活动。 如果你有一个 Visual Studio Enterprise 或 Professional 订阅，这两个计划均包括免费Microsoft 365[开发人员订阅](https://aka.ms/MyVisualStudioBenefits)。 只要你的订阅处于活动状态，Visual Studio就处于活动状态。 有关详细信息，请参阅[设置开发人员Microsoft 365订阅](https://developer.microsoft.com/microsoft-365/dev-program)。

1. 转到开发人员[Microsoft 365计划](https://developer.microsoft.com/microsoft-365/dev-program)。
2. 选择 **立即加入** 并按照屏幕上的说明进行操作。
3. 在欢迎屏幕中，选择 **"设置 E5 订阅"。**
4. 设置管理员帐户。 完成后，应看到以下屏幕：

:::image type="content" source="./images/m365-developer-program.png" alt-text="显示 Microsoft m365 程序的关系图":::

## <a name="accounts-for-microsoft-365-developer-program"></a>Microsoft 365计划帐户

你可以使用以下帐户类型之一注册开发人员计划：

- **Microsoft 帐户** 

您可以创建供个人使用 - 提供对面向消费者的所有 Microsoft 产品和云服务（如 Outlook、Messenger、OneDrive、MSN、Xbox Live 或 Microsoft 365）的访问权限。 注册一个 Outlook.com 邮箱将自动创建一个 Microsoft 帐户。 创建 Microsoft 帐户后，可以用于访问消费者相关的 Microsoft 云服务或 Azure。

- **工作帐户**

 管理员可以发出业务使用问题 - 提供对所有小型、中型和企业业务级别 Microsoft 云服务（如 Azure、Microsoft Intune 或 Microsoft 365）的访问权限。 作为组织注册此类服务时，会在 Azure Active Directory 中自动预配一个基于云的目录，来表示你的组织。

- **Visual Studio ID**

你可以为 Visual Studio Professional 或 Enterprise 订阅创建 - 我们建议使用此选项加入 Visual Studio 库中的开发人员计划，以作为 Visual Studio 订阅者获得全部权益。

## <a name="teams-customer-app-uploading-sideloading-permission-check"></a>Teams客户应用 (旁加载权限) 检查

> [!IMPORTANT]
> 在开发期间，你必须在应用中加载Teams而不分发它。 这称为 **旁加载**。

检查你是否拥有一个 Teams 帐户的方法之一，验证你能否在Teams：

1. 在 Teams客户端 **中，选择** 左侧栏中的"应用"。
2. 选择 **"管理应用"。**
3. 检查你是否可以看到自定义Upload **选项，** 如图所示：

:::image type="content" source="./images/sideload-check.png" alt-text="显示上载自定义应用的关系图":::

如果你看不到Upload自定义 **应用** 选项，这表示你没有旁加载权限。 如果没有旁加载权限，将无法执行任何本地/远程调试。 因此，在针对你的应用执行任何调试之前，获取帐户的旁加载权限Teams非常重要。 如果你是租户的管理员，你可以打开租户/组织的旁加载设置，而如果你不是管理员，请联系你的租户管理员获得权限。

## <a name="enable-custom-app-uploading-sideloading--for-your-organization"></a>为组织启用 (应用) 旁加载

> [!IMPORTANT]
> 若要为开发人员租户启用自定义应用上传或旁加载，你必须是租户的管理员。

1. 登录以[Microsoft 365 管理中心](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)管理员凭据登录。

2. 选择 **"显示所有**  >  **Teams"。**

:::image type="content" source="./images/admin-center-teams.png" alt-text="显示管理Teams的关系图":::

> [!NOTE]
> 可能需要 **24 小时才能显示****Teams选项。** 可以将[自定义应用上传到Teams环境中](/microsoftteams/upload-custom-apps)进行测试和验证。

3. 导航到 **Teams**  >  **应用设置策略**  >  **全局 。**

:::image type="content" source="./images/teams-setup-policy.png" alt-text="显示用户设置策略的Teams":::

4. 将Upload应用切换到 **打开** 位置。

:::image type="content" source="./images/turn-on-sideload.png" alt-text="显示打开旁加载的图表":::

5. 选择“**保存**”。 测试租户可以允许自定义应用旁加载。

:::image type="content" source="./images/save-sideload.png" alt-text="显示保存选项的图表":::

> [!Note]
> 旁加载可能需要 24 小时才能处于活动状态。 在此期间，可以使用 **[上传你的租户]** 测试你的应用。 若要上传.zip包文件，请参阅上传 [自定义应用](/microsoftteams/teams-app-setup-policies)。

有关详细信息，请参阅在应用中管理[自定义应用策略和](/microsoftteams/teams-custom-app-policies-and-settings)Teams在应用中管理[应用](/microsoftteams/teams-app-setup-policies)Teams。

## <a name="see-also"></a>另请参阅

> [!div class="nextstepaction"]
> [新建Teams项目](create-new-project.md)

> [!div class="nextstepaction"]
> [预配云资源](provision.md)
