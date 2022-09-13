---
author: heath-hamilton
description: 了解将现有 Web 应用与 Microsoft Teams 集成的最佳做法或注意事项。 它提供有关应用与 Teams 的 API 要求、身份验证和深度链接的信息。
ms.author: surbhigupta
ms.date: 08/26/2020
ms.localizationpriority: medium
ms.topic: conceptual
title: Teams 集成注意事项
ms.openlocfilehash: 994747586610ac9301e1cc1a6d752ad77816af97
ms.sourcegitcommit: 937ea793889fc1efa9ec6a52374d5098be1117e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2022
ms.locfileid: "67653166"
---
# <a name="considerations-for-teams-integration"></a>Teams 集成注意事项

通过将 Web 应用与 Teams 正确集成，可以使 Web 应用适合 Teams 的社交和协作功能。
  
可与 Teams 集成的不同类型的应用如下所示：

* **独立应用**：独立应用是单页或大而复杂的应用。 用户可以在 Teams 中使用它的某些方面。
* **协作应用**：为 Teams 固有的社交和协作功能构建的现成应用。
* **SharePoint**：要在 Teams 中显示的 SharePoint 页面。

可以映射并遵循适用于集成方案的相应准则。
本文档概述了 Teams 功能、文件和数据存储的 SharePoint 要求、API 要求、身份验证以及应用与 Teams 的深层链接。

## <a name="get-to-know-teams-platform-capabilities"></a>了解 Teams 平台功能

***集成方案**：独立应用、协作应用、SharePoint*

Teams 应用必须包含必需和预期的协作功能。 若要处理应用集成，请务必熟悉 Teams 开发术语。

|常见应用功能   |Teams 平台功能   |
|----------|-----------|
|内嵌网页、主页或 Web 视图  |[选项卡](../tabs/what-are-tabs.md)  |
|共享快捷方式和扩展  |[消息扩展](../messaging-extensions/what-are-messaging-extensions.md)  |
|操作快捷方式和扩展  |[消息扩展](../messaging-extensions/what-are-messaging-extensions.md)  |
|聊天机器人 |[机器人](../bots/what-are-bots.md) |
|频道通知  |[机器人](../bots/what-are-bots.md)<br/>[传入 Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Office 365 连接器](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|消息外部服务  |[机器人](../bots/what-are-bots.md)<br/>[传出 Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|模式  |[任务模块](../task-modules-and-cards/what-are-task-modules.md)  |
|内容丰富的卡片  |[自适应卡](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>确定功能子集

***集成方案**：独立应用*

将现有应用程序的所有功能集成到 Teams 通常会导致生硬或突兀的用户体验，尤其是大型应用。 要先从最具影响力的功能和与 Teams 集成更自然的功能开始。 你可以允许用户启动主应用并访问其完整功能集。

以下是将应用与 Teams 集成的先决条件。

1. [将应用用例映射到 Teams 平台功能](../concepts/design/map-use-cases.md)。
1. [确定应用的入口点](../concepts/extensibility-points.md)。 是供个人使用、协作还是二者兼顾？

## <a name="understand-sharepoint-requirements-and-options"></a>了解 SharePoint 要求和选项

***集成方案**：SharePoint*

若要将现有 [SharePoint 页面](/sharepoint/dev/general-development/overview-of-the-sharepoint-page-model)集成为 Teams 选项卡，必须考虑以下事项：

* 它必须是 *新式* SharePoint Online 页面。
* 仅支持个人选项卡。 无法将页面集成为频道选项卡。

或者，可以[使用 SharePoint 框架](/sharepoint/dev/spfx/integrate-with-teams-introduction)生成 Teams 选项卡。

## <a name="aim-towards-multitenancy"></a>面向多组织

***集成方案**：独立应用、协作应用、SharePoint*

如果应用由多个组织使用，请考虑多组织托管。 这会使产品可缩放并简化分发。

## <a name="review-your-apis"></a>审查 API

***集成方案**：独立应用、协作应用*

与 Teams 集成时，应用的 API 和数据结构必须支持应用。 若要扩展支持，必须使用有关 Teams 的上下文信息来增强 API 和数据结构，用于[标识映射](../concepts/authentication/authentication.md)、[深层链接支持](../concepts/build-and-test/deep-links.md)以及[整合 Microsoft Graph](/graph/teams-concept-overview)。

了解如何获取 Teams [选项卡](../tabs/how-to/access-teams-context.md)或[机器人](../bots/how-to/get-teams-context.md)的上下文。

## <a name="understand-authentication-options"></a>了解身份验证选项

***集成方案**：独立应用、协作应用、SharePoint*

Azure Active Directory 是 Teams 的提供程序。 如果你的应用使用不同的身份提供程序，则必须执行标识映射或与 Microsoft Azure Active Directory (Azure AD) 整合。

Teams 具有面向第三方应用的 Azure AD 单一登录 (SSO) 机制。 它还提供有关使用 OAuth 和 Open ID 连接（即 OIDC）等标准、针对其他身份提供程序的身份验证流的指南。

> [!IMPORTANT]
> 目前，第三方应用在政府社区云 (GCC) 中可用，但不适用于 GCC-High 和国防部 (DOD)。 GCC 默认关闭第三方应用。 若要为 GCC 启用第三方应用，请参阅[管理应用权限策略](/microsoftteams/teams-app-permission-policies)和[管理应用](/microsoftteams/manage-apps)。

对于 SharePoint 页面，如果希望 SSO 适用于另一个应用，则只能使用 SSO，并且不能添加其他 Azure AD ID，因为 ID 是 SharePoint 应用。

详细了解 [Teams 中的身份验证](../concepts/authentication/authentication.md)。

## <a name="follow-teams-design-guidelines"></a>遵循 Teams 机器人设计准则

***集成方案**：独立应用、协作应用*

请确保遵循 [Teams 设计准则](../concepts/design/understand-use-cases.md)，以便应用原生支持 Teams。 无法将现有应用内容迁移到 Teams 选项卡。有关应用设计的详细信息，请[参阅Fluent Design System](https://fluentsite.z22.web.core.windows.net/)。

## <a name="maximize-deep-linking"></a>最大程度地运用深层链接

***集成方案**：独立应用、协作应用、SharePoint*

你可以创建 Teams 中的信息和功能的链接。 使用[深层链接](../concepts/build-and-test/deep-links.md)将应用与 Teams 链接在一起，因为这些链接将应用的多个部分绑定在一起，以获得更原生的 Teams 体验。

## <a name="be-smart-when-messaging-users"></a>向用户智能发送消息

***集成方案**：独立应用、协作应用、SharePoint*

在 Teams 应用中使用[机器人](../bots/what-are-bots.md)进行多线程会话，因为这比 [Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md) 更具灵活性。

机器人还允许向单个用户或频道发送 **主动消息**。 主动消息是由外部事件（而非发送给机器人的消息）触发的无提示消息。 例如，机器人在安装或新用户加入通道时发送欢迎消息。

发送主动消息需要特定于 Teams 的标识符。 可以通过[提取名单或用户配置数据](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)、[订阅聊天事件](../bots/how-to/conversations/subscribe-to-conversation-events.md)或使用 [Microsoft Graph](/microsoftteams/platform/graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages?context=graph/context#proactive-messaging-in-teams) 来获取该信息。

不要向消息过多的用户发送垃圾邮件。 如果 Teams 功能支持，用户可以为应用配置通知设置。
通知消息示例如下：**请勿向我发送无提示消息**。

## <a name="use-sharepoint-for-file-and-data-storage"></a>使用 SharePoint 进行文件和数据存储

***集成方案：** 独立应用、协作应用、SharePoint 页面*

创建团队时，还会预配 [SharePoint 网站集](/microsoftteams/sharepoint-onedrive-interact)，以支持该团队的文件和数据存储。 如果应用与文件交互，则应用必须利用此功能。 使用该网站集将原始数据存储在 SharePoint 列表和 Microsoft Excel 中。

## <a name="see-also"></a>另请参阅

* [集成 web 应用](~/samples/integrate-web-apps-overview.md)
* [适用于 Microsoft Teams 的低代码和无代码解决方案](~/samples/teams-low-code-solutions.md)
* [从 Web 应用共享到 Teams](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [SameSite Cookie 属性](~/resources/samesite-cookie-update.md)
* [集成 Power Virtual Agents 聊天机器人](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
