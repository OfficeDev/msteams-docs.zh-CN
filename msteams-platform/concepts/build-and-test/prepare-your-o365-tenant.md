---
title: 准备 Microsoft 365 租户
description: 如何在 Microsoft 365 中开始使用 Teams
ms.topic: how-to
keywords: 配置 Microsoft 365 租户 Teams 上传
ms.openlocfilehash: 50765271b93edd380d1c23672289b618baf1d346
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093941"
---
# <a name="prepare-your-microsoft-365-tenant"></a>准备 Microsoft 365 租户

如果你是 Microsoft 365 订阅者，可以使用以下计划之一为 Microsoft Teams 开发 [应用](https://products.office.com/business/compare-more-office-365-for-business-plans)：

* 基本
* 标准
* 企业版 E1、E3 和 E5
* 开发人员版
* 教育版、教育增强版和教育版 E5

Microsoft Teams 还将提供给在停用 E4 之前订阅 E4 [的客户](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)。

## <a name="just-need-a-development-environment"></a>只需要开发环境？

如果当前没有 Microsoft 365 帐户，可以注册 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program) 订阅。 它 *90* 天免费，并且将持续续订，只要使用它进行开发活动。 如果你有企业Visual Studio专业版订阅，这两个计划都包括免费的 Microsoft 365 开发人员[](https://aka.ms/MyVisualStudioBenefits)订阅，在订阅的生命周期内Visual Studio订阅。 *请参阅*[设置 Microsoft 365 开发人员订阅](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。

## <a name="enable-microsoft-teams-for-your-organization"></a>为组织启用 Microsoft Teams 

如果尚未为组织启用 Microsoft Teams，你将需要首先执行这一操作。 请看一下我们为组织 [启用 Teams 的详细指南](/microsoftteams/enable-features-office-365)。

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>启用自定义 Teams 应用并启用自定义应用上传

为开发人员租户启用自定义应用旁加载，如下所示：

1. 使用管理员 [凭据登录到 Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) 管理中心。 

2. 选择 **"显示所有**  -->  **团队"。** 

![管理中心菜单的图像](~/assets/images/prepare-test-tenant/admin-center.png)

> [!Note] 
> "Teams"选项最多可能需要 24 小时才能显示。 在此期间，你可以将 [自定义应用上载到 Teams 环境](/microsoftteams/upload-custom-apps#validate) 以进行测试和验证。

3. 导航到 **Teams 应用**  -->  **设置策略**  -->  **全局 (组织范围内的默认)**  

![打开旁加载视图](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. 将 **自定义应用切换** 至 **打开** 位置。

5. 选择 **"保存** "保存更改。

就是这么简单。 你的测试租户现在将允许自定义应用旁加载。

> [!Note] 
> 启用旁加载最多可能需要 24 小时。 在此期间，可以使用 **上传来 \<your tenant>** 测试你的应用。

![updload 应用视图](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

有关这些设置如何交互的完整信息，请参阅：在[Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings)中管理自定义应用策略和设置，以及[管理 Microsoft Teams 中的应用设置策略](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)。
