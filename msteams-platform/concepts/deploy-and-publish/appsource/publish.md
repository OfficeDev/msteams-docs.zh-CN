---
title: 概述 - Teams应用商店发布过程
description: 介绍将应用提交到合作伙伴中心并发布到 Microsoft Teams 应用商店和 AppSource (的过程) 。
ms.topic: overview
author: heath-hamilton
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: eaebde76a3d1f387ba16c9fdc77670144d22fa61
ms.sourcegitcommit: 40aade608ee21f5d7d813bd145bef5736dc647f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/17/2022
ms.locfileid: "62881649"
---
# <a name="publish-your-app-to-the-microsoft-teams-store"></a>将应用发布到 Microsoft Teams 应用商店

你可以将应用直接分发到 Microsoft Teams 内的应用商店，并覆盖全球数百万用户。 如果你的应用也在应用商店中特别推荐，你可以立即联系潜在客户。

发布到应用商店Teams应用也会自动在 [Microsoft AppSource](https://appsource.microsoft.com) 上列出，Microsoft AppSource 是 Microsoft 365应用和解决方案的官方市场。

## <a name="understand-the-publishing-process"></a>了解发布过程

当你感觉你的应用已做好生产准备时，你可以开始在应用商店中列出Teams过程。

> [!TIP]
> 严格遵循提交前步骤可能会增加 Microsoft 批准你的应用进行发布的可能性。

:::row:::
   :::column span="":::
      
   :::column-end:::
   :::column span="3":::
      :::image type="content" source="../../../assets/images/submission/teams-app-store-publish-process.png" alt-text="Teams应用商店发布过程" lightbox="../../../assets/images/submission/teams-app-store-publish-process.png":::
   :::column-end:::
   :::column span="":::
      
   :::column-end:::
:::row-end:::

1. [查看Teams应用商店验证指南](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)，确保你的应用符合Teams和应用商店标准。

1. [创建合作伙伴中心开发人员帐户](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)。

1. [准备应用商店提交，](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)其中包括运行自动测试、编译测试备注、创建应用商店一览，以及其他有助于加快审阅过程的重要任务。

1. [通过合作伙伴中心](/office/dev/store/add-in-submission-guide) 提交应用。

1. 如果提交失败，请直接与 Microsoft 合作以解决问题并重新 [提交应用](~/concepts/deploy-and-publish/appsource/resolve-submission-issues.md)。

## <a name="what-to-expect-after-you-submit-your-app"></a>提交应用后有什么预期？

* **深度功能和体验测试**

  验证程序会全面检查你的应用，以确保符合 [Microsoft 商业](/legal/marketplace/certification-policies) 市场认证策略，并重点关注深入的功能和用户体验测试、可用性检查和元数据检查。 跨桌面、Web 和移动客户端执行应用验证。

* **通过引导式服务发布应用**

  如果你的应用没有观察到任何问题，你的应用将被批准并发布到Teams应用商店。 如果存在问题，你将从合作伙伴中心收到包含失败详细信息的自动验证报告。 为了帮助你成功将应用发布到 Teams 应用商店并指导你完成此过程，验证团队会从我们的销售服务中心向您发送一封 teamsubm@microsoft.com 个性化电子邮件，[其中包括](mailto:teamsubm@microsoft.com)以下信息：

   * 所有问题的摘要

   * 策略链接和分类失败或问题的详细信息： 

     * 强制修复：必须在应用批准之前修复这些问题。

     * 建议修复：可以在应用审批后修复这些问题，因为建议改进应用体验。

     * 阻止程序：这些问题会阻止验证团队进一步测试你的应用功能，必须解决它们，验证方能继续。

     * 查询：可以共享这些查询，获取与你的应用相关的特定问题的答案。

   * 通过书面说明或视频格式重新创建问题的步骤。

   * 推荐指南文档的链接修复报告的问题。
 
  查看问题列表后，修复所有报告的问题并通过电子邮件共享更新的应用包，以便验证团队重新全面验证你的应用。 如果有任何与报告的问题相关的查询，请与验证团队联系，[teamsubm@microsoft.com。](mailto:teamsubm@microsoft.com)

  如果应用中发现的问题剩余或回归问题，验证团队将与你共享更新的验证报告。 如果你的应用有阻止程序，你可能会看到在阻止程序解决后验证应用时报告的新问题。 有时，验证团队还注意到在部署修复程序后，应用中的回归问题。 需要一些重新提交以关闭包含 Bug 的应用的所有问题，并批准将其发布到 Teams 应用商店。

  关闭所有报告的问题，在合作伙伴中心进行最终提交后，验证团队将批准并发布你的应用。 允许应用在应用商店中至少提供一Teams日。

## <a name="tips-for-rapid-approval-to-publish-your-app"></a>使用技巧以快速审批发布应用

* **在设计阶段**

  在 [应用生命周期的](prepare/teams-store-validation-guidelines.md) 早期阶段查看应用商店验证指南 (设计阶段) 以确保生成符合应用商店要求的应用。 如果你按照这些指南生成应用，这将防止由于不遵守应用商店策略而出现任何返工。

* **在应用提交之前**

  1. [提前创建合作伙伴](prepare/create-partner-center-dev-account.md) 中心帐户。 如果你遇到合作伙伴中心帐户的任何 [难题，](prepare/create-partner-center-dev-account.md)请创建支持 [票证](/azure/marketplace/partner-center-portal/support)。

  1. 再次 [查看应用商店验证](prepare/teams-store-validation-guidelines.md) 指南，以确保你的应用符合应用商店要求。 这有助于减少在应用中观察到的问题数量，进而减少批准应用所花时间。

  1. 测试和重新测试你的应用：

     1. 使用开发人员门户验证Teams[包，](https://dev.teams.microsoft.com/home)以确定并修复任何程序包错误。

        :::image type="content" source="../../../assets/images/submission/teams-validation-developer-portal.png" alt-text="存储验证":::
 
     1. 在提交应用之前全面自我测试你的应用，以确保它符合应用商店策略。 在应用中旁加载Teams并测试应用的端到端用户流。 确保功能按预期工作，链接不会中断，用户体验不会受阻，并且会明确突出显示任何限制。

     1. 跨桌面、Web 和移动客户端测试应用。 确保应用在不同外形类型中具有响应能力。

  1. 提交 [应用前](/azure/active-directory/develop/publisher-verification-overview) 完成发布者验证。 如果遇到任何问题，可以创建支持 [票证](/azure/marketplace/partner-center-portal/support) 来解决问题。

  1. 准备应用提交时，请按照清单 [操作](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/submission-checklist) ，并包含以下详细信息作为提交程序包的一部分：

      1. 彻底验证了应用包。

      1. 工作管理员和非管理员用户凭据，用于测试应用 (应用是否提供高级订阅模型) 。

      1. 详细说明应用功能和受支持的方案的测试说明。

      1. 如果应用需要其他配置来访问应用功能，则安装说明。 或者，如果你的应用需要复杂的配置，还可以提供预配的演示租户和[](/office/developer-program/microsoft-365-developer-program-get-started)管理员访问权限，以便我们的验证程序可以跳过配置步骤。

      1. 链接到应用的演示视频录制关键用户流。 强烈建议这样做。

* **应用提交后**

  * 查看验证报告后，使用与验证报告相关的任何查询回复电子邮件线程，或者如果您需要任何其他支持来解决报告的问题。

  * 确保有足够的开发人员带宽来解决报告的任何问题，直到应用获得批准。

  * 在共享应用包以[](/microsoftteams/platform/concepts/deploy-and-publish/appsource/resolve-submission-issues)进一步测试之前，teamsubm@microsoft.com 服务报告的所有[](mailto:teamsubm@microsoft.com)问题。 这有助于减少验证应用所需的迭代次数，从而缩短批准应用所花时间。
  
  * 避免在验证过程中更改应用功能。 这可能会导致发现新问题并增加批准应用所花的时间。

## <a name="see-also"></a>另请参阅

* [发布到Microsoft 365应用商店](/office/dev/store/)
* [Upload你的Teams应用](~/concepts/deploy-and-publish/apps-upload.md)
* [将Teams应用程序发布到组织](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
* [为用户规划载入体验](../../design/understand-use-cases.md#plan-the-onboarding-experience)
* [在移动设备上分发选项卡应用](../../../tabs/design/tabs-mobile.md#distribution)
* [针对盈利应用的测试预览](prepare/Test-preview-for-monetized-apps.md)
