---
title: 应用商店提交清单
description: 将 Microsoft Teams 应用发布到 AppSource 之前使用的清单
ms.topic: reference
localization_priority: Normal
keywords: Teams 发布应用商店 Office 发布清单提交 Teams 应用应用资源验证
ms.openlocfilehash: 1e7698e143d313ce46b834eada608571e3280b8a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020784"
---
# <a name="prepare-for-appsource-submission"></a>准备 AppSource 提交  

若要在 AppSource 上列出，应用必须完成审批流程。 这是 Microsoft Teams 组提供的一项免费服务，可验证你的应用是否按所述运行，包含所有适当的元数据，并提供对最终用户有价值的内容。 为了帮助你快速获得批准，请确保你的应用满足以下要求和指南：

* **分发方法：** 确保你的应用适用于在应用商店平台上发布。 还有其他 [一些选项](../../overview.md) 可用于分发应用，而无需发布到 AppSource。
* **验证策略：** 你的应用必须在提交之前通过所有 [当前的 AppSource](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams) 验证策略。 
  > [!NOTE] 
  > Appsource 验证策略可能会更改。
* **移动就绪情况：** 你的应用必须具有移动响应能力。 如果你的应用包含选项卡，它们必须遵循移动设计指南[](~/tabs/design/tabs-mobile.md)，并且你的应用必须符合 iOS 和[](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment)Android (上的不) 。
* **自行测试应用：** 使用清单验证工具 [测试应用](#teams-app-validation-tool)。
* **应用详细信息页面：** 你的应用必须与应用详细信息  [页面清单一致](detail-page-checklist.md)。
* **提示和经常失败的情况：** 请额外注意列出的 [提示和经常失败的情况](frequently-failed-cases.md)  ，以改进应用提交和审批时间。
* **应用清单：** 根据应用清单清单 [检查应用清单](app-manifest-checklist.md)。
* **测试和调试：** 确保你已 [完全测试和调试你的应用](../../../build-and-test/debug.md)。
* **测试说明：** 包括 [测试说明进行验证](#test-notes-for-validation)
* **隐私策略：** 确保 [你的隐私策略、使用条款和支持 URL 遵循](#privacy-policy-terms-of-use-and-support-urls) 我们的指南。

完成上述所有要求后，通过合作伙伴中心将程序包 [提交](/office/dev/store/use-partner-center-to-submit-to-appsource)到 AppSource。

## <a name="teams-app-validation-tool"></a>Teams 应用验证工具

应用验证工具由应用 [验证器和](#teams-app-validator) 初步 [清单组成](#preliminary-checklist)。 该工具复制 [AppSource](/office/dev/store/submit-to-appsource-via-partner-center) 用于评估应用提交的相同测试用例。 因此，在将解决方案提交到 AppSource 进行审批之前，必须通过所有测试用例至关重要。该工具可在 Teams 平台内的多个区域找到：

> [!div class="checklist"]
>
> * [**应用验证程序主页**](https://dev.teams.microsoft.com/appvalidation.html)
> * [**Teams Visual Studio Code 工具包**](/toolkit/visual-studio-code-overview.md)
> * [**应用程序 Studio**](../../../build-and-test/app-studio-overview.md)

### <a name="teams-app-validator"></a>Teams 应用验证程序

" **验证** "页允许你在提交到 AppSource 之前检查应用包。 只需上传应用包，验证工具将针对所有与清单相关的测试用例检查应用。 对于每个失败的测试，该说明都提供了一个文档链接，帮助您修复错误。

![验证工具](../../../../assets/images/validation-tool/validator.png)

### <a name="preliminary-checklist"></a>初步清单

对于难以自动化的测试方案，初步清单显示七个最常见的失败测试用例。

![初步清单](../../../../assets/images/validation-tool/preliminary-checklist.png)

## <a name="privacy-policy-terms-of-use-and-support-urls"></a>隐私策略、使用条款和支持 URL

### <a name="privacy-policy"></a>隐私策略

隐私策略指南：

> [!div class="checklist"]
>
> * 隐私策略可以特定于你的应用和/或所有服务的整体策略。
> * 如果使用通用隐私策略，则必须引用"服务"、"应用程序"和"平台"，以包括 Teams 应用和网站。
> * 它必须包括如何处理用户数据存储、用户数据保留、删除和安全控制。
> * 它必须包含您的联系信息。
> * 它不应包含断开的链接、beta URL 或暂存 URL。

### <a name="terms-of-use"></a>使用条款

使用条款声明应特定于应用和/或外接程序产品/服务。

### <a name="support-urls"></a>支持 URL

支持 URL 不应要求身份验证或登录凭据来就应用的任何问题联系你。

## <a name="test-notes-for-validation"></a>用于验证的测试说明

请包含以下内容：

* 必须提供至少两个登录凭据，一个管理员和非管理员。

* 出于验证目的，你提供的帐户应具有足够的预填充数据。

* 对于企业应用、需要订阅的应用或具有 Office 365 租户/域依赖项的应用，必须在未为应用预配置的同一域中提供第三个帐户，以便我们可以验证首次运行的用户体验。

* 如果你的应用具有高级/升级功能，则必须提供具有必要访问权限的帐户来测试该体验。

* 你可以选择将测试备注上载到 SharePoint。 如果是这样，请提供文件的公共链接。

* **测试帐户**。 如果你的应用仅允许来自后端的许可帐户或安全列表，则测试帐户是必需的。 此外，如果应用中允许团队/群聊范围，则同一租户中需要两个测试帐户来验证团队协作方案。

* **集成步骤**。 如果需要租户管理员预配置才能使用应用，请包含步骤和/或提供配置的管理员和非管理员帐户进行验证。 注意：你可以注册 [Office 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program) 订阅。 它 *是免费的* 90 天，并且将持续续订，只要你使用它进行开发活动。

* **有关 Teams 中的** 应用功能的注意事项：详细介绍 Teams 中应用提供的所有功能以及测试每个功能的步骤。

* **显示应用功能的视频 (可选**) ：你可以提供产品的视频录制，以便我们完全了解应用的功能。
