---
title: 解决应用商店提交问题
description: 本文介绍如何排查和纠正Microsoft Teams存储提交问题。
ms.topic: how-to
author: heath-hamilton
ms.author: surbhigupta
ms.localizationpriority: medium
ms.openlocfilehash: 51427f2023ba566391a3d0b544d74e5658464a7c
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123207"
---
# <a name="resolve-issues-if-your-microsoft-teams-store-submission-fails"></a>解决 Microsoft Teams 应用商店提交失败时出现的问题

发布到Microsoft Teams应用商店的应用必须符合[Teams应用商店验证准则](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)和[商业市场策略](/legal/marketplace/certification-policies)。

如果应用商店提交失败，Microsoft 将提供礼宾验证服务，以帮助使应用符合并发布。

## <a name="get-help-directly-from-microsoft"></a>直接从 Microsoft 获取帮助

Microsoft 提供的礼宾验证服务可帮助开发人员将其应用发布到Teams存储。 作为此服务的一部分，Microsoft 将验证应用是否按所述工作，包含所有适当的元数据，并为用户提供值。

如果应用提交失败，Microsoft 会在提交后 24 小时内向你发送包含建议的评审报告。

## <a name="resolve-issues-and-resubmit-your-app"></a>解决问题并重新提交应用

在合作伙伴中心重新提交应用之前，必须解决 Microsoft 礼宾验证团队报告的所有问题。 Microsoft 报表包含以下信息：

* 每个问题的相应 [验证指南](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) 。
* 有关如何重现每个问题的说明。
* 推荐根据公开可用的开发人员文档解决每个问题。

解决问题和重新提交应用的过程通常如下所示：

1. 可以修复报表中的所有问题。
1. teamsubm@microsoft.com 向 Microsoft 礼宾验证团队发送以下 <a href="mailto:teamsubm@microsoft.com">内容</a>：
   * 更新后的应用包
   * 如果未在原始提交中包含这些说明，请测试应用的备注：
      * 至少两个帐户的凭据 (一个管理员和一个非管理员) 。
      * 有关配置应用并测试其功能的说明。
      * 显示Teams中使用的应用的视频。
1. Microsoft 礼宾验证团队会对更新后的应用进行全面测试。
1. 执行下列操作之一：
   * 如果应用没有问题，请在合作伙伴中心重新提交应用。
   * 如果问题未解决或 Microsoft 发现新问题，则会收到另一份有关要修复的问题的报告。 解决这些问题，并将应用的更新版本发送到 <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>。

> [!CAUTION]
> 若要避免多次提交失败，请在 Microsoft 礼宾验证团队批准应用之前，不要在合作伙伴中心重新提交应用。

## <a name="faq"></a>常见问题

解决应用提交问题时，获取一些常见问题的解答。

<br>

<details>

<summary><b>发布我的应用需要多长时间？</b></summary>

如果应用商店提交没有问题，应用将在 1-2 个工作日内发布。 如果应用失败，Microsoft 的一个团队会为你提供解决问题的建议。 完成这些修补程序并将更新后的应用重新发送到该团队后，如果应用已准备好发布或仍需要更多工作，将在 24 小时内收到通知。

<br>

</details>

<details>

<summary><b>如何实现增加应用通过提交的可能性？</b></summary>

执行以下操作可能会成功提交：

1. 根据[Teams设计准则开发](~/concepts/design/design-teams-app-overview.md)应用。
1. 确保应用遵守[Teams应用商店验证准则](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)和 [Microsoft 商业市场认证策略](/legal/marketplace/certification-policies)。
1. 使用[Microsoft Teams应用验证工具测试应用](https://dev.teams.microsoft.com/appvalidation.html)包。
1. [准备Teams存储提交](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)。

<br>

</details>

<details>

<summary><b>我的应用正在测试 beta。是否可以提交应用以节省发布过程的时间？</b></summary>

否。 Microsoft 仅验证生产就绪应用。

<br>

</details>

<details>

<summary><b>在合作伙伴中心首次提交应用之前，是否可以联系 teamsubm@microsoft.com 电子邮件？</b></summary>

否。 在合作伙伴中心首次提交应用之前，Microsoft 不会开始验证应用。

<br>

</details>

<details>

<summary><b>我收到一封来自合作伙伴中心的电子邮件，说我的应用已获准发布。为什么我的应用不在Teams存储中？</b></summary>

应用获得批准后，发布通常需要 1-2 个工作日，具体取决于应用的功能。如果应用在两个工作日后未发布，请联系 <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>。

<br>

</details>
