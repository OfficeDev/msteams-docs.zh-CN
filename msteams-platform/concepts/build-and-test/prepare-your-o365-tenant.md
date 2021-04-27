---
title: 准备 Microsoft 365 租户
description: 如何在 Microsoft 365 中开始使用 Teams
ms.topic: how-to
localization_priority: Normal
keywords: 配置 Microsoft 365 租户 Teams 上传
ms.openlocfilehash: 45d6dfb57fd2faa5bb303aac1dff86be142d0dc2
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019942"
---
# <a name="prepare-your-microsoft-365-tenant"></a>准备 Microsoft 365 租户

Microsoft 365 订阅者可以使用以下计划之一为 Microsoft Teams 开发应用：

* 基本
* 标准
* 企业版 E1、E3 和 E5
* Developer
* 教育版、教育增强版和教育版 E5

> [!NOTE]
> * 有关 Microsoft 365 订阅详细信息，请参阅 [计划](https://products.office.com/business/compare-more-office-365-for-business-plans)。
> * Teams 还可供在停用之前订阅 E4 [的客户使用](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)。

## <a name="create-your-development-environment"></a>创建开发环境

如果你没有 Microsoft 365 帐户，则必须注册 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program) 订阅。 订阅将免费 90 天，并持续续订，只要将订阅用于开发活动。 如果你有企业版Visual Studio专业版订阅，这两个计划都包括免费的 Microsoft 365 [开发人员订阅](https://aka.ms/MyVisualStudioBenefits)。 只要你的订阅处于活动状态，Visual Studio就处于活动状态。 有关详细信息，请参阅设置 [Microsoft 365 开发人员订阅](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。

## <a name="enable-teams-for-your-organization"></a>为组织启用 Teams

为组织启用 Teams，有关详细信息，请参阅[为组织启用 Teams。](/microsoftteams/enable-features-office-365)

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>启用自定义 Teams 应用并启用自定义应用上传

**为开发人员租户启用自定义应用上传或旁加载**

1. 使用管理员凭据登录 [Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) 管理中心。

2. 选择 **"显示所有**  >  **团队"。**

    ![管理中心菜单](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > 可能需要 24 小时才能 **显示 Teams** 选项。 可以将 [自定义应用上传到 Teams 环境](/microsoftteams/upload-custom-apps#validate) ，以在当时进行测试和验证。

3. 导航到 **Teams 应用**  >  **设置策略**  >  **全局**。

   ![打开旁加载视图](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. 将 **"上传自定义应用"** 切换至 **"打开"** 位置。

5. 选择“**保存**”。 测试租户可以允许自定义应用旁加载。

    > [!Note]
    > 旁加载可能需要 24 小时才能处于活动状态。 临时，可以使用 **upload for \<your tenant>** 测试应用。 若要上传应用的 .zip 包文件，请参阅 [上传自定义应用](/microsoftteams/upload-custom-apps#upload)。

    ![上传应用视图](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

有关这些设置如何交互的完整信息，请参阅在 [Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) 中管理自定义应用策略和设置，以及管理 [Teams 中的应用设置策略](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"] 
> [选择测试设置](~/concepts/build-and-test/debug.md)

