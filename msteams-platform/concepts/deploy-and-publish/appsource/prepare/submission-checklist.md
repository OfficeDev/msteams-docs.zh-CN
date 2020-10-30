---
title: 提交内容清单
description: 将 Microsoft 团队应用程序发布到 AppSource 之前要使用的清单
keywords: 团队发布 microsoft store office 发布清单提交团队应用 appsource 验证
ms.openlocfilehash: 1b25a449901c303269334e5cea6de46fa3b6f6e5
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796300"
---
# <a name="prepare-for-appsource-submission"></a>准备 AppSource 提交  

若要在 AppSource 上列出，您的应用程序必须经过审批过程。 这是 Microsoft 团队组提供的一项免费服务，它验证您的应用程序按所述方式工作，包含所有适当的元数据，并提供对最终用户有价值的内容。 为了帮助你获得快速批准，请确保你的应用满足以下要求和指南：

* **分发方法：** 请确保您的应用程序适用于商店平台上的出版物。 在不发布到 AppSource 的情况下，分发应用程序的 [其他选项](../../overview.md) 。
* **验证策略：** 您的应用程序必须在提交前传递所有当前的 [AppSource 验证策略](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams) 。 请注意，这些策略可能会发生更改。 
* * * 使用 [清单验证工具](#teams-app-validation-tool) 自我测试您的应用程序。
* **应用程序详细信息页面：** 您的应用程序必须与  [应用程序详细信息页检查表](detail-page-checklist.md)相一致。
* **提示和频繁失败的情况：** 请特别注意列出的 [提示和频繁失败的情况](frequently-failed-cases.md)  ，以改进应用提交和审批时间。
* **应用程序清单：** 检查应用部件清单（manifest）清单 [中的应用](app-manifest-checklist.md)清单。
* **测试和调试：** 确保已对应用程序进行了充分 [测试和调试](../../../build-and-test/debug.md)。
* **测试备注：** 包含 [用于验证的测试说明](#test-notes-for-validation)
* **隐私策略：** 确保你的 [隐私策略、使用条款和支持 url](#privacy-policy-terms-of-use-and-support-urls) 遵循我们的准则。

完成上述所有要求后，通过 [合作伙伴中心](/office/dev/store/use-partner-center-to-submit-to-appsource)将您的包提交到 AppSource。

## <a name="teams-app-validation-tool"></a>团队应用程序验证工具

应用程序验证工具由 [应用程序验证程序](#teams-app-validator) 和 [初步检查表](#preliminary-checklist)组成。 该工具将复制 [AppSource](/office/dev/store/submit-to-appsource-via-partner-center) 使用的相同测试用例来评估应用程序提交。 因此，在将解决方案提交到 AppSource 以供审批之前，将其传递给所有测试用例是至关重要的。可以在团队平台内的多个区域中找到该工具：

> [!div class="checklist"]
>
> * [**应用程序验证程序主页**](https://dev.teams.microsoft.com/appvalidation.html)
> * [**团队 Visual Studio Code 工具包**](/toolkit/visual-studio-code-overview.md)
> * [**应用程序工作室**](/concepts/build-and-test/app-studio-overview.md)

### <a name="teams-app-validator"></a>团队应用程序验证程序

通过 " **验证** " 页，您可以在提交到 AppSource 之前检查应用程序包。 只需上传应用程序包，验证工具便会针对所有与清单相关的测试用例检查您的应用程序。 对于每个失败的测试，说明提供的文档链接可帮助您修复错误。

![验证工具](../../../../assets/images/validation-tool/validator.png)

### <a name="preliminary-checklist"></a>初步清单

对于难以自动化的测试方案，初步清单将显示七个最常用的失败测试事例。

![初步清单](../../../../assets/images/validation-tool/preliminary-checklist.png)

## <a name="privacy-policy-terms-of-use-and-support-urls"></a>隐私策略、使用条款和支持 Url

### <a name="privacy-policy"></a>隐私策略

隐私策略指南：

> [!div class="checklist"]
>
> * 隐私策略可特定于您的应用程序和/或所有服务的整体策略。
> * 如果使用通用隐私策略，则必须引用 "服务"、"应用程序" 和 "平台" 以包含团队应用和您的网站。
> * 它必须包括处理用户数据存储、用户数据保留、删除和安全控件的方式。
> * 它必须包含您的联系信息。
> * 它不应包含损坏的链接、beta Url 或暂存 Url。

### <a name="terms-of-use"></a>使用条款

使用条款声明应是特定的，并适用于您的应用和/或外接程序产品。

### <a name="support-urls"></a>支持 Url

您的支持 Url 不应要求身份验证或登录凭据，以便与您联系，以解决应用程序中的任何问题。

## <a name="test-notes-for-validation"></a>验证的测试说明

请包含以下内容：

* 您必须至少提供两个登录凭据：一个管理员和一个非管理员。

* 出于验证目的，你提供的帐户应具有足够的预填充数据。

* 对于企业应用程序、需要订阅的应用程序或存在 Office 365 租户/域依赖项的应用程序，您必须在未为您的应用程序预配置的同一域中提供第三个帐户，以便我们可以验证首次运行的用户体验。

* 如果您的应用程序具有高级/升级功能，则必须提供具有必要访问权限的帐户来测试该体验。

* 您可以选择将测试笔记上传到 SharePoint。 如果是这样，请提供指向该文件的公用链接。

* **测试帐户** 。 如果您的应用程序仅允许来自后端的授权帐户或 safelisting，则需要测试帐户。 此外，如果您的应用程序中允许有团队/组聊天作用域，则必须在同一租户中有两个测试帐户来验证工作组协作方案。

* **集成步骤** 。 如果需要由租户管理员进行预配置以使用应用，请包括步骤和/或提供配置的管理员和非管理员帐户进行验证。 注意：你可以注册 [Office 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program) 订阅。 它在90天内 *免费* 使用，并且将持续更新，只要你将其用于开发活动即可。

* **有关团队中应用程序功能的说明** ：详细介绍了应用程序在团队中提供的所有功能，以及用于测试每项功能的步骤。

* **显示应用程序功能 (可选) 的视频** ：您可以为我们提供产品的视频录制，以充分了解应用程序的功能。
