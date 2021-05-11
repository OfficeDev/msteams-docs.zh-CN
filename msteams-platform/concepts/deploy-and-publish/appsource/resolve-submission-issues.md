---
title: 解决应用商店提交问题
description: 了解如何排查并更正你的应用商店Microsoft Teams问题。
ms.topic: how-to
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 847534c68d013566e4bfbe0e5a1bbbe92e36e63e
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101883"
---
# <a name="resolve-issues-if-your-microsoft-teams-store-submission-fails"></a>解决应用商店提交Microsoft Teams时的问题

发布到应用商店Microsoft Teams应用必须满足Teams[验证](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)准则和商业市场[策略](https://docs.microsoft.com/legal/marketplace/certification-policies)。

如果你的应用商店提交失败，Microsoft 将提供一个验证验证服务，以帮助使你的应用合规并发布。

## <a name="get-help-directly-from-microsoft"></a>直接从 Microsoft 获取帮助

Microsoft 提供的验证服务可帮助开发人员将应用发布到应用商店Teams商店。 作为此服务的一部分，Microsoft 会验证你的应用是否正常工作，是否包含所有适当的元数据，并为用户提供价值。

如果应用提交失败，Microsoft 在提交后 24 小时内会向您发送评价报告和建议。

## <a name="resolve-issues-and-resubmit-your-app"></a>解决问题并重新提交应用

必须先修复 Microsoft 验证团队报告的所有问题，然后才能在合作伙伴中心重新提交应用。 Microsoft 报告包含以下信息：

* 针对 [每个问题](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) 的相应验证准则
* 有关如何重现每个问题的说明
* 推荐公开提供的开发人员文档解决每个问题

解决问题并重新提交应用的过程通常如下所示：

1. 解决报告中的所有问题。
1. 你可以将以下内容发送到 Microsoft 验证团队<a href="mailto:teamsubm@microsoft.com">，teamsubm@microsoft.com：</a>
   * 更新的应用包
   * 如果你未在原始提交 (，则应用测试说明) ：
      * 至少两个帐户的凭据 (一个管理员和非管理员帐户) 
      * 配置应用并测试其功能的说明
      * 显示应用程序中使用的应用Teams
1. Microsoft 验证团队会全面测试更新后的应用。
1. 执行下列操作之一：
   * 如果你的应用没有问题，请重新提交合作伙伴中心上的应用。
   * 如果问题未解决或 Microsoft 发现新问题，您将收到另一个有关要修复问题的报告。 解决这些问题，并将应用的更新版本发送到 teamsubm@microsoft.com <a href="mailto:teamsubm@microsoft.com">。</a>

> [!CAUTION]
> 若要避免多个提交失败，请不要在 Microsoft 验证团队批准你的应用之前，在合作伙伴中心重新提交你的应用。

## <a name="faq"></a>常见问题

在解决应用提交问题时，获取一些常见问题的解答。

<br>

<details>

<summary><b>发布我的应用程序需要多久？</b></summary>

如果你的应用商店提交没有问题，你的应用将在 1-2 个工作日内发布。 如果应用失败，Microsoft 团队会提供修复问题的建议。 一旦进行这些修复，然后向该团队重新发送更新后的应用，如果应用已准备好发布或仍然需要更多工作，将在 24 小时内收到通知。

<br>

</details>

<details>

<summary><b>如何提高我的应用通过提交的可能性？</b></summary>

执行以下操作可能会导致成功提交：

1. 根据应用设计Teams[开发应用](~/concepts/design/design-teams-app-overview.md)。
1. 确保你的应用遵守应用商店验证[Teams](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) [Microsoft 商业市场认证策略](https://docs.microsoft.com/legal/marketplace/certification-policies)。
1. 使用应用验证Microsoft Teams[测试应用包](https://dev.teams.microsoft.com/appvalidation.html)。
1. [准备你的Teams提交](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)。

<br>

</details>

<details>

<summary><b>我的应用已进行 beta 测试。我能否提交我的应用以节省发布过程的时间？</b></summary>

错误。 Microsoft 仅验证生产就绪型应用。

<br>

</details>

<details>

<summary><b>在合作伙伴中心 teamsubm@microsoft.com 提交我的应用之前，我可能需要联系客户吗？</b></summary>

错误。 在合作伙伴中心首次提交应用之前，Microsoft 不会开始验证你的应用。

<br>

</details>

<details>

<summary><b>我收到了一封来自合作伙伴中心的电子邮件，指出我的应用已批准发布。为什么我的应用不在应用商店Teams？</b></summary>

应用获得批准后，发布通常需要 1-2 个工作日，具体取决于应用的功能。如果你的应用在两个工作日后尚未发布 <a href="mailto:teamsubm@microsoft.com">，请联系</a>teamsubm@microsoft.com。

<br>

</details>
