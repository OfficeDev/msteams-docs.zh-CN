---
title: 帮助规划 Teams 应用开发的问题
author: heath-hamilton
description: 规划应用、了解用户及其需求、应用解决的问题、用户身份验证及其载入体验时需要考虑的问题。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: surbhigupta
ms.openlocfilehash: 01dfa683150070a2508173fb55991388ad877517
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123109"
---
# <a name="teams-app-planning-checklist"></a>Teams 应用规划清单

应用的生命周期从规划应用扩展到最终部署应用等。 计划应用需要的不仅仅是了解用户和要求。 根据应用需求，还可以考虑规划将来的更新。

让我们来实际了解如何规划应用的生命周期。

## <a name="relevant-questions"></a>相关问题

下面是规划应用时需要考虑的问题清单。 使用它作为指南，以确保你的规划涵盖应用开发的重要详细信息。

<br>
<br>
<details>
<summary>了解你的用户</summary>

| # | 考虑… |
| --- | --- |
| 1 | 用户是否主要是移动客户端上的一线工作人员? |
| 2 | 是否希望许多来宾用户需要访问你的应用? |
| 3 | 他们是使用团队和频道，还是主要使用群组聊天? |
| 4 | 主要用户在技术上有多成熟? |
| 5 | 需要全面的载入体验，还是需要一些指导性的建议? |

</details>
<br>
<details>
<summary>了解问题</summary>

| # | 考虑… |
|--- | --- |
| 1 | 用户使用的当前状态系统的优缺点是什么? |
| 2 | 用户要解决所面临的哪些问题? |
| 3 | 用户在当前工作方式中喜欢和热爱哪些特点或功能? |

</details>
<br>
<details>
<summary>了解应用的限制</summary>

| # | 考虑… |
| --- | --- |
| 1 | 当前应用在后端集成方面有哪些挑战? |
| 2 | 谁拥有后端数据 - 内部或第三方? |
| 3 | 是否有影响应用运行的防火墙? |
| 4 | 是否有 API 来访问应用运行所需的数据? |

</details>
<br>
<details>
<summary>提供身份验证</summary>

| # | 考虑…|
|--- | --- |
| 1 | 用户是否会根据其角色访问不同的数据视图? |
| 2 | 是否涉及 PII? |
| 3 | 交互是否也基于用户角色? |
| 4 | 外部用户是否将访问该应用? |

</details>
<br>
<details>
<summary>计划载入体验</summary>

| # | 考虑… |
| --- | --- |
| 1 | 当用户首次在频道中配置选项卡时会发生什么情况? |
| 2 | 如果使用消息扩展共享卡片，是否有必要向了解详细信息页面添加一个小链接，以帮助向用户介绍你的应用还可以执行哪些操作？ |
| 3 | 你是否希望大多数人已经对你的应用有了一些了解，或者已经在其他情况下使用过你的服务? |
| 4 | 他们是否在事先不知情的情况下进入你的应用? |

</details>
<br>
<details>
<summary>个人范围应用</summary>

| # | 考虑… |
| --- | --- |
| 1 | 出于隐私或其他原因，是否需要与应用进行一对一交互? 例如，检查剩余余额或其他私有信息。 |
| 2 | 可能没有任何共同 Teams 的用户之间是否会进行协作? 例如，查找公司中即将发生的组织范围活动。 |
| 3 | 是否存在需要在整个 Teams 应用体验中向用户发送的任何个性化通知或消息？ |

</details>
<br>
<details>
<summary>共享范围应用</summary>

| # | 考虑… |
| --- | --- |
| 1 | 应用在选项卡或机器人中提供的信息是否与团队中的大多数成员相关且有用？例如 Scrum 应用。 |
| 2 | 应用的上下文能否根据其添加到的团队而改变? 例如，Planner 的任务在不同的团队中是不同的。 |
| 3 | 角色中需要协作的所有成员是否都属于单个团队？例如，处理票证的代理。 |

</details>
<br>
<details>
<summary>选择生成环境</summary>

建议: 可帮助根据应用需求选择正确环境的选项。
</details>
<br>
<details>
<summary>测试应用的计划</summary>

建议: 有助于确定应用最佳测试环境的选项。
</details>
<br>
<details>
<summary>应用分发的计划</summary>

建议: 有助于确定最佳分发模型的选项。

</details>

## <a name="plan-for-hosting-your-teams-app"></a>托管 Teams 应用的计划

Teams 不托管你的应用。 当用户在 Teams 中安装你的应用时，他们安装的应用包仅包含配置文件 (也称为应用清单) 以及应用的图标。 应用的逻辑和数据存储托管在其他地方，如开发期间的本地主机和 Azure Web 服务。 Teams 通过 HTTPS 访问这些资源。

:::image type="content" source="../../assets/images/teams-app-host.png" alt-text="显示 Teams 应用的应用托管插图" border="true":::

## <a name="plan-beyond-app-building"></a>应用生成之外的计划

- **决定会在 Teams 中出现的内容**: 无论是新应用还是现有应用，请检查是否需要 Teams 客户端中的整个应用。 如果仅集成应用的一部分，请专注于共享、协作、启动和监视工作流。

- **计划载入体验**: 在考虑关键用户时创建载入体验。 在一对一聊天中安装聊天机器人时，如何引入在包含一千人的频道中安装的聊天机器人的方式会有所不同。

- **计划未来**: 确定用户在当前解决方案中首选的新功能。 任何新功能都可能会影响应用设计和体系结构。
