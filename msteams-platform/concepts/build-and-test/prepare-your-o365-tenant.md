---
title: 准备 Microsoft 365 租户
description: 如何开始使用Teams Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: 配置Microsoft 365租户Teams上载
ms.openlocfilehash: 45d6dfb57fd2faa5bb303aac1dff86be142d0dc2
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019942"
---
# <a name="prepare-your-microsoft-365-tenant"></a>准备 Microsoft 365 租户

Microsoft 365订阅者可以使用以下Microsoft Teams之一开发适用于用户的应用程序：

* 基本
* 标准
* EnterpriseE1、E3 和 E5
* Developer
* 教育版、教育增强版和教育版 E5

> [!NOTE]
> * 有关订阅Microsoft 365，请参阅[计划](https://products.office.com/business/compare-more-office-365-for-business-plans)。
> * Teams停用之前订阅 E4 的客户也[可用](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)。

## <a name="create-your-development-environment"></a>创建开发环境

如果你没有帐户，Microsoft 365注册开发人员计划Microsoft 365[订阅](https://developer.microsoft.com/microsoft-365/dev-program)。 订阅将免费 90 天，并持续续订，只要将订阅用于开发活动。 如果你有一个Visual Studio Enterprise或Professional订阅，这两个计划均包括免费Microsoft 365[开发人员订阅](https://aka.ms/MyVisualStudioBenefits)。 只要你的订阅处于活动状态，Visual Studio就有效。 有关详细信息，请参阅[设置开发人员Microsoft 365订阅](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。

## <a name="enable-teams-for-your-organization"></a>为Teams启用管理

Enable Teams for your organization and for more information， see [enabling Teams for your organization](/microsoftteams/enable-features-office-365).

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>启用自定义Teams应用并启用自定义应用上传

**为开发人员租户启用自定义应用上传或旁加载**

1. 使用管理员[Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)登录管理中心。

2. 选择 **"显示所有**  >  **Teams"。**

    ![管理中心菜单](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > 可能需要 24 小时才能显示 **Teams选项。** 可以将[自定义应用上传到Teams环境中](/microsoftteams/upload-custom-apps#validate)进行测试和验证。

3. 导航到 **Teams**  >  **应用设置策略**  >  **全局 。**

   ![打开旁加载视图](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. 将 **Upload应用切换到****"打开"** 位置。

5. 选择“**保存**”。 测试租户可以允许自定义应用旁加载。

    > [!Note]
    > 旁加载可能需要 24 小时才能处于活动状态。 临时，可以使用 **upload for \<your tenant>** 测试应用。 若要上传.zip包文件，请参阅上传 [自定义应用](/microsoftteams/upload-custom-apps#upload)。

    ![Upload应用视图](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

有关这些设置如何交互的完整信息，请参阅管理[](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings)Teams 中的自定义应用策略和设置[Teams。](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"] 
> [选择测试设置](~/concepts/build-and-test/debug.md)

