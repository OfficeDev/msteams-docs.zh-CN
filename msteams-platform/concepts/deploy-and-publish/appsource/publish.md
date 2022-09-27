---
title: 概述–将应用发布到 Microsoft Teams 商店
description: 了解将应用提交到合作伙伴中心并将其发布到 Microsoft Teams 应用商店（和 AppSource）的过程。
ms.topic: overview
author: heath-hamilton
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: f8891edb11134570a79c5483eea722a44ad48b91
ms.sourcegitcommit: 377a4b712b50a211851aeecc1029414939945390
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2022
ms.locfileid: "68044649"
---
# <a name="publish-your-app-to-the-microsoft-teams-store"></a>将应用发布到 Microsoft Teams 商店

你可以将应用直接分发到 Microsoft Teams 内的应用商店，可以覆盖全球数百万用户。 如果在应用商店你的应用得到特别推荐，则可以立即联系潜在客户。

发布到 Teams 应用商店的应用也会自动在 [Microsoft 商业商城](https://appsource.microsoft.com)上列出，此商城是 Microsoft 365 应用和解决方案的官方市场。

## <a name="understand-the-publishing-process"></a>了解发布过程

如果你认为应用已准备就绪，可以开始在 Teams 应用商店准备上架流程。

> [!TIP]
> 严格遵循预提交步骤可以提高 Microsoft 批准应用发布的可能性。

:::row:::
   :::column span="":::

   :::column-end:::
   :::column span="3":::
      :::image type="content" source="../../../assets/images/submission/teams-app-store-publish-process.png" alt-text="Teams 应用商店发布过程" lightbox="../../../assets/images/submission/teams-app-store-publish-process.png":::
   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

1. [查看 Teams 应用商店验证准则](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) 以确保应用符合 Teams 应用和应用商店标准。

1. [创建合作伙伴中心开发人员帐户](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)。

1. [准备应用商店提交](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)，其中包括运行自动测试、编译测试备注、创建应用商店一览，以及其他有助于加快审阅过程的重要任务。

1. [通过合作伙伴中心](/office/dev/store/add-in-submission-guide) 提交应用。

1. 如果提交失败，请直接与 Microsoft 联系，[解决问题，然后重新提交应用](~/concepts/deploy-and-publish/appsource/resolve-submission-issues.md)。

## <a name="what-to-expect-after-you-submit-your-app"></a>提交应用后会发生什么？

* **深层功能和体验测试**

  验证程序会全面审查你的应用，以确保符合 [Microsoft 商业市场认证政策](/legal/marketplace/certification-policies)。
  重点介绍深度功能和用户体验测试、可用性检查、元数据检查。 跨桌面、Web 和移动客户端执行应用验证。 我们努力在提交后的 24 个工作日内为你提供详细的测试报告。

* **通过引导式服务发布应用**

  如果应用未发现任何问题，我们会批准应用并发布到 Teams 应用商店。 另一方面，如果存在问题，则你会收到来自合作伙伴中心的自动验证报告，其中将包含失败的详细信息。 为了帮助你将应用成功发布到 Teams 应用商店，并指导你完成此过程，验证团队将通过我们的引导式服务[teamsubm@microsoft.com](mailto:teamsubm@microsoft.com)向你发送一封个性化的电子邮件，其中包括以下信息：

  * 所有问题的摘要

  * 策略链接和分类失败或问题的详细信息：

    * 强制修复：必须在应用批准之前修复问题。

    * 建议修复：可以在应用审批后修复问题，因为此类问题是帮助你改善应用体验的建议。

    * 阻止性问题：此类问题会阻止验证团队进一步测试你的应用功能，必须解决问题才能继续验证。

    * 查询：查询可以共享，以获取与应用相关的具体问题的答案。

  * 通过书面说明或视频格式重新创建问题的步骤。

  * 修复报告问题的建议与，其中包含指导文件的链接。

  查看问题列表后，修复所有报告的问题并通过电子邮件共享更新的应用包，以便验证团队重新全面验证你的应用。 如果有任何与报告问题相关的查询，请联系 [teamsubm@microsoft.com](mailto:teamsubm@microsoft.com)的验证团队。

  如果应用中发现剩余问题或回归问题，验证团队将与你共享更新的验证报告。 如果你的应用有阻止程序，则在解决阻止程序后验证应用时，可能会出现新问题报告。 有时，验证团队还会关注部署修复程序后，应用中的回归问题。 需要一些重新提交以关闭包含 Bug 应用的所有问题，并批准将其发布到 Teams 应用商店。

  关闭所有报告的问题，在合作伙伴中心进行最终提交后，验证团队将批准并发布你的应用。 允许应用程序在 Teams 商店中至少有一个工作日可用。

* **分析应用使用情况**

  批准并发布应用后，可以在合作伙伴中心中的 [Teams 应用使用情况报告](/office/dev/store/teams-apps-usage)中跟踪应用使用情况。 指标包括每月、每日、每周活动用户，以及可跟踪改动率和使用频率的保留期和强度图表。

  新发布的应用的数据大约需要一周时间才会显示在报表中。

## <a name="tips-for-rapid-approval-to-publish-your-app"></a>快速批准发布应用的提示

* **设计阶段**

  在 [应用生命周期的](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) 早期阶段查看应用商店验证指南 (设计阶段) 以确保生成符合应用商店要求的应用。 如果你按照这些指南生成应用，那你就不必由于不遵守应用商店策略而多花费工夫。

* **在应用提交之前**

  1. [提前创建合作伙伴](prepare/create-partner-center-dev-account.md) 中心帐户。 如果你遇到[合作伙伴中心帐户](prepare/create-partner-center-dev-account.md)的任何难题，请创建[支持票证](/azure/marketplace/partner-center-portal/support)。

  1. 再次查看[应用商店验证](prepare/teams-store-validation-guidelines.md)指南，以确保你的应用符合应用商店要求。 温习指南有助于减少应用中观察到的问题数量，从而减少批准应用所需的时间。

  1. 测试和重新测试你的应用：

     1. 使用 Teams [开发人员门户](https://dev.teams.microsoft.com/home) 验证应用包，以确定并修复全部应用包错误。

        :::image type="content" source="../../../assets/images/submission/teams-validation-developer-portal.png" alt-text="开发人员门户中的 Teams 商店应用验证" lightbox="../../../assets/images/submission/teams-validation-developer-portal.png":::

     1. 在提交应用之前，自行全面测试你的应用，以确保它符合应用商店策略。 在 Teams 中旁加载应用，并测试应用的端到端用户流。 确保功能按预期工作，链接不会中断，用户体验不会受阻，并且会明确突出显示任何限制。

     1. 跨桌面、Web 和移动客户端测试应用。 确保应用在不同外形类型中具有响应能力。
  
  1. 提交应用之前，请完成 [发布者验证](/azure/active-directory/develop/publisher-verification-overview)。 如果遇到任何问题，可以创建 [支持票证](/azure/marketplace/partner-center-portal/support) 进行解决。

  1. 准备应用提交时，请[按照清单操作](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/submission-checklist) ，并将以下详细信息作为提交包的一部分包括在内：

        1. 完全验证应用包。

        1. 工作管理员和非管理员用户凭据，用于测试应用功能 (如果你的应用提供高级订阅模型) 。

        1. 详细说明应用功能和受支持方案的测试说明。

        1. 如果应用需要更多配置来访问应用功能，请设置说明。 或者，如果应用需要复杂的配置，还可以提供 [预配的演示租户](/office/developer-program/microsoft-365-developer-program-get-started) 管理员访问权限，以便验证程序可以跳过配置步骤。

        1. 演示应用的关键用户流的视频链接。 强烈推荐。

* **应用提交后**

  * 查看验证报告后，使用与验证报告相关的任何查询回复电子邮件线程，或者需要任何额外的支持来解决报告的问题。

  * 确保有足够带宽供开发人员解决报告的任何问题，直到应用获得批准。

  * 在共享应用包进行下一步测试之前，请确保已[解决引导式服务[teamsubm@microsoft.com](mailto:teamsubm@microsoft.com)向你报告的所有问题](/microsoftteams/platform/concepts/deploy-and-publish/appsource/resolve-submission-issues)。 这有助于减少验证应用所需的迭代次数，从而缩短批准应用所花时间。
  
  * 避免在验证过程中进行可能会导致出现新问题的应用功能更改，否则有可能会增加批准应用所需的时间。

## <a name="additional-tips-for-rapid-approval-to-publish-your-app-linked-to-a-saas-offer"></a>快速批准发布链接到 SaaS 产品/服务的应用的其他提示

* **设计阶段**

  在应用生命周期早期（设计阶段）检查[特定于与链接的 SaaS 产品/服务一起发布的应用的存储验证准则](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#apps-linked-to-saas-offer)，以确保在构建应用时遵守应用商店的要求，以及[适用于链接了 SaaS 产品/服务的 Teams 应用的 Microsoft 商业市场策略](/legal/marketplace/certification-policies#11405-teams-app-linked-to-software-as-a-service-saas-offers)。 如果你按照这些指南生成应用，那你就不必由于不遵守应用商店策略而多花费工夫。

* **在应用提交之前**

  1. 当你在为应用提交作准备时，请确保：

      1. 你的应用链接到了 AppSource 上的已上线（已发布）的 SaaS 产品/服务，至少有一个计划包含定价信息。

      1. 在应用清单文件中以 `publisherId.offerId` 格式正确提及了 `subscriptionOffer` 详细信息。

      1. 必须确保链接的 SaaS 产品/服务旨在支持 [SaaS 定价模型](/azure/marketplace/create-new-saas-offer-plans)上分配的许可证。

      1. 包括测试说明或设置说明，或演示视频的链接，其中详细介绍了应用功能和支持的场景以及任何其他信息，以便我们的测试人员能够轻松了解你的 SaaS 门户工作流。

  1. 在提交链接到 SaaS 产品/服务的应用进行验证之前，必须对端到端购买和许可证管理工作流进行彻底的[自我测试](~/concepts/deploy-and-publish/appsource/prepare/test-preview-for-monetized-apps.md)，确保以下内容：

     1. 管理员和非管理员用户都可以下单并确认购买订阅。 购买者可以通过在 Microsoft 管理中心中选择 **立即设置** 导航到 SaaS 应用程序登陆页面。 测试并确保购买者可以在 SaaS 应用程序上激活和配置其订阅。 SaaS 应用程序上的消息应提供足够和明了的信息，让购买者能够充分了解。

     1. Microsoft 管理中心的 **管理订阅** 部分显示你的测试用户所带来的订阅的正确详细信息。 订阅状态、许可证数和其他详细信息必须准确。

     1. 购买和删除许可证工作流都能按预期方式工作。 确保购买者可以增加 Microsoft 管理中心的许可证数量。 确保 SaaS 应用程序上的许可证计数和分配能够反映各自的许可证和正确的被分配者。 此外，请确保 SaaS 应用程序提供了从用户处获取许可证的方法。 删除许可证后，请确保 SaaS 应用程序上的剩余分配和计数保持不变，让正确的详细信息反映在 Microsoft 管理中心中。

     1. 订阅取消可按预期工作。 购买者可以取消订阅。 取消后，检查正确的订阅状态是否反映在 Microsoft 管理中心和 SaaS 应用程序中。 验证在成功取消后购买者是否会失去对订阅的访问权限。

     1. 重新购买订阅的体验是无缝的。 取消活动订阅后，进行全面测试以确保购买者可以重新购买该订阅。

     1. 购买者可以更改其订阅的计划。 修改计划后，用户可以使用升级或降级的计划功能。

     1. SaaS 应用程序包含许可证管理功能。 购买者必须能够向用户分配、修改、重新分配可用的许可证。 检查购买者是否可以添加或删除用户来管理许可证。
  
  1. 必须测试并确保最低和批量许可证购买流按预期工作。
  
  1. 必须确保分配有许可证的用户有权使用计划列表中所述的他们所购买的正确的计划功能。

## <a name="see-also"></a>另请参阅

* [发布到 Microsoft 365 应用商店](/office/dev/store/)
* [上传 Teams 应用](~/concepts/deploy-and-publish/apps-upload.md)
* [将 Teams 应用发布到组织](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
* [为用户规划载入体验](../../design/planning-checklist.md#plan-beyond-app-building)
* [在移动设备上分发选项卡应用](../../../tabs/design/tabs-mobile.md#distribution)
* [针对盈利应用的测试预览](prepare/Test-preview-for-monetized-apps.md)
* [Microsoft Teams 应用商店排名参数](post-publish/teams-store-ranking-parameters.md)
