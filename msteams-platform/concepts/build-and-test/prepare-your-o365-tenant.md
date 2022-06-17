---
title: 准备 Microsoft 365 租户
description: 在本模块中，了解如何开始使用Microsoft 365中的Teams并创建开发环境
ms.topic: how-to
ms.localizationpriority: medium
ms.openlocfilehash: 241040767c610692873e5a68bd215849a8cd26a0
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144388"
---
# <a name="prepare-your-microsoft-365-tenant"></a>准备 Microsoft 365 租户

Microsoft 365 订阅者可以使用以下计划之一为 Microsoft Teams 开发应用：

* 基本
* 标准
* 企业版 E1、E3 和 E5
* 开发人员版
* 教育版、教育增强版和教育版 E5

> [!NOTE]
>
> * 有关 Microsoft 365 订阅的详细信息，请参阅[计划](https://products.office.com/business/compare-more-office-365-for-business-plans)。
> * Teams 在 E4 计划[停用](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)之前也对其订阅客户可用。

## <a name="create-your-development-environment"></a>创建开发环境

如果没有 Microsoft 365 账户，则必须注册 [ Microsoft 365 开发人员计划 ](https://developer.microsoft.com/microsoft-365/dev-program) 订阅。 订阅可以免费使用 90 天，并且只要将订阅用于开发活动，就可以继续续订。 如果你有 Visual Studio Enterprise 或 Professional 订阅，则这两个计划都包含免费 Microsoft 365 [开发人员订阅](https://aka.ms/MyVisualStudioBenefits)。 只要你的 Visual Studio 订阅处于活动状态，它就处于活动状态。 有关详细信息，请参阅[设置 Microsoft 365 开发人员订阅](/office/developer-program/office-365-developer-program-get-started)。

## <a name="enable-teams-for-your-organization"></a>为组织启用 Teams

为组织启用 Teams，有关详细信息，请参阅[为组织启用 Teams](/microsoftteams/enable-features-office-365)。

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>启用自定义 Teams 应用并启用自定义应用上传

若要为开发人员租户启用自定义应用上传或旁加载，请执行以下操作：

1. 请使用管理员帐户登录到“[Microsoft 365 管理中心](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)”。

2. 选择 **显示全部** > **Teams**。

    ![管理中心菜单](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > 可能至多 24 小时后 **Teams** 选项才会出现。 在此期间可以[将自定义应用上传到 Teams 环境](/microsoftteams/upload-custom-apps#validate)进行测试和验证。

3. 导航到“**Teams 应用**” > “**设置策略**” > “**全局**”。

   ![打开旁加载视图](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. 将“**上传自定义应用**”切换到“**开**”位置。

5. 选择“保存”。 测试租户可以允许自定义应用旁加载。

    > [!Note]
    > 旁加载最长可能需要 24 小时才能生效。 在此期间，可以使用“**上传\<your tenant>**”来测试应用。 若要上传应用的 .zip 包文件，请参阅“[上传自定义应用](/microsoftteams/upload-custom-apps#upload)”。

    ![上传应用视图](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

有关这些设置如何交互的完整信息，请参阅[管理 Teams 中的自定义应用策略和设置](/microsoftteams/teams-custom-app-policies-and-settings)，以及[管理 Teams 中的应用设置策略](/microsoftteams/teams-app-setup-policies)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [选择测试设置](~/concepts/build-and-test/debug.md)

## <a name="see-also"></a>另请参阅

[将测试数据添加到 Microsoft 365 测试租户](~/concepts/build-and-test/test-data.md)
