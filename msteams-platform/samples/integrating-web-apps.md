---
author: heath-hamilton
description: 将现有 Web 应用与Microsoft Teams集成的最佳做法或注意事项
ms.author: surbhigupta
ms.date: 08/26/2020
ms.localizationpriority: medium
ms.topic: conceptual
title: Teams集成的注意事项
ms.openlocfilehash: bbd5b046d7b1afca5cc3fa5c8afb21a3698f43eb
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104348"
---
# <a name="considerations-for-teams-integration"></a>Teams集成的注意事项

通过将 Web 应用与Teams正确集成，可以使 Web 应用适合Teams的社交和协作功能。
  
可以与Teams集成的不同类型的应用如下所示：

* **独立应用**：独立应用是单页或大而复杂的应用。 用户可以在 Teams 中使用它的某些方面。
* **协作应用**：已为Teams固有的社交和协作功能构建的应用。
* **SharePoint**：要在Teams中显示的SharePoint页。

可以映射并遵循适用于集成方案的相应准则。
本文档概述了Teams功能、文件和数据存储的共享点要求、API 要求、身份验证以及应用与Teams的深度链接。

## <a name="get-to-know-teams-platform-capabilities"></a>了解Teams平台功能

***集成方案**：独立应用、协作应用、SharePoint*

Teams应用必须包含必需和预期的协作功能。 若要处理应用集成，请务必熟悉Teams开发术语。

|常见应用功能   |Teams平台功能   |
|----------|-----------|
|嵌入网页、主页或 Webview  |[选项卡](../tabs/what-are-tabs.md)  |
|共享快捷方式和扩展  |[消息扩展](../messaging-extensions/what-are-messaging-extensions.md)  |
|操作快捷方式和扩展  |[消息扩展](../messaging-extensions/what-are-messaging-extensions.md)  |
|Chatbots |[机器人](../bots/what-are-bots.md) |
|通道通知  |[机器人](../bots/what-are-bots.md)<br/>[传入 Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Office 365 连接器](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|消息外部服务  |[机器人](../bots/what-are-bots.md)<br/>[传出 Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|模式  |[任务模块](../task-modules-and-cards/what-are-task-modules.md)  |
|内容丰富的卡片  |[自适应卡](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>确定功能的子集

***集成方案**：独立应用*

将现有应用程序的所有功能集成到Teams通常会导致强制用户体验或非自然用户体验，尤其是在大型应用中。 从最具影响力的功能和更自然地与Teams集成的功能开始。 你可以允许用户启动主应用并访问其完整功能集。

以下是将应用与Teams集成的先决条件。

1. [将应用的用例映射到Teams平台功能](../concepts/design/map-use-cases.md)。
1. [确定应用的入口点](../concepts/extensibility-points.md)。 是用于个人用途、协作还是用于两者？

## <a name="understand-sharepoint-requirements-and-options"></a>了解SharePoint要求和选项

***集成方案**：SharePoint*

若要将现有[SharePoint页](/sharepoint/dev/general-development/overview-of-the-sharepoint-page-model)集成为Teams选项卡，必须考虑以下事项：

* 它必须是新 *式* SharePoint联机页面。
* 仅支持个人选项卡。 无法将页面集成为频道选项卡。

或者，可以使用SharePoint 框架生成[Teams](/sharepoint/dev/spfx/integrate-with-teams-introduction)选项卡。

## <a name="aim-towards-multitenancy"></a>面向多租户

***集成方案**：独立应用、协作应用、SharePoint*

如果应用被多个组织使用，请考虑多租户托管。 它使产品可缩放并简化分发。

## <a name="review-your-apis"></a>查看 API

***集成方案**：独立应用、协作应用*

与Teams集成时，应用的 API 和数据结构必须支持应用。 若要扩展支持，必须使用有关[标识映射](../concepts/authentication/configure-identity-provider.md)Teams、[深层链接支持](../concepts/build-and-test/deep-links.md)以及[合并 Microsoft Graph](/graph/teams-concept-overview) 的上下文信息来增强 API 和数据结构。

了解如何获取Teams[选项卡](../tabs/how-to/access-teams-context.md)或[机器人](../bots/how-to/get-teams-context.md)的上下文。

## <a name="understand-authentication-options"></a>了解身份验证选项

***集成方案**：独立应用、协作应用、SharePoint*

Azure Active Directory是Teams的标识提供者。 如果应用使用不同的标识提供者，则必须执行标识映射练习或与Microsoft Azure Active Directory (Azure AD) 结合。

Teams具有单一登录 (SSO) 机制，其中包含第三方应用的Azure AD。 它还提供有关使用 OAuth 和 Open ID 连接（称为 OIDC）等标准流向其他标识提供者的身份验证指南。

> [!IMPORTANT]
> 目前，第三方应用在政府社区云 (GCC) 中可用，但不适用于GCC-High和国防部 (国防部) 。 默认情况下，第三方应用将关闭GCC。 若要为GCC启用第三方应用，请参阅[管理应用权限策略](/microsoftteams/teams-app-permission-policies)[和管理应用](/microsoftteams/manage-apps)。

对于SharePoint页，如果希望 SSO 适用于其他应用，则只能使用 SSO，并且无法添加其他Azure AD ID，因为 ID 是SharePoint应用。

详细了解[Teams中的身份验证](../concepts/authentication/authentication.md)。

## <a name="follow-teams-design-guidelines"></a>遵循Teams设计准则

***集成方案**：独立应用、协作应用*

请确保遵循[Teams设计准则](../concepts/design/understand-use-cases.md)，使应用能够原生地Teams。 无法将现有应用内容迁移到Teams选项卡。有关应用设计的详细信息，请[参阅Fluent Design System](https://fluentsite.z22.web.core.windows.net/)。

## <a name="maximize-deep-linking"></a>最大化深度链接

***集成方案**：独立应用、协作应用、SharePoint*

你可以创建 Teams 中的信息和功能的链接。 使用[深层链接](../concepts/build-and-test/deep-links.md)将应用与Teams链接在一起，以获得更本机的Teams体验。

## <a name="be-smart-when-messaging-users"></a>消息传递用户时要智能

***集成方案**：独立应用、协作应用、SharePoint*

在Teams应用中使用[机器人](../bots/what-are-bots.md)进行多线程会话，因为它比 [Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md) 更具灵活性。

机器人还允许向单个用户或频道发送 **主动消息** 。 主动消息是由外部事件触发的无提示消息，而不是发送给机器人的消息。 例如，机器人在安装或新用户加入通道时发送欢迎消息。

发送主动消息需要Teams特定的标识符。 可以通过[提取名册或用户配置文件数据](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)、[订阅聊天事件](../bots/how-to/conversations/subscribe-to-conversation-events.md)或使用 [Microsoft Graph](/microsoftteams/platform/graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages?context=graph/context#proactive-messaging-in-teams) 来捕获信息。

不要向消息过多的用户发送垃圾邮件。 如果Teams功能支持，用户可以为应用配置通知设置。
下面是通知消息的示例： **请勿向我发送不受提示的消息**。

## <a name="use-sharepoint-for-file-and-data-storage"></a>将SharePoint用于文件和数据存储

***集成方案：** 独立应用、协作应用、SharePoint页*

创建团队时，还会预配[SharePoint网站集](/microsoftteams/sharepoint-onedrive-interact)，以支持该团队的文件和数据存储。 如果应用与文件交互，则应用必须利用此功能。 使用网站集将原始数据存储在SharePoint列表和Microsoft Excel中。

## <a name="see-also"></a>另请参阅

* [集成 web 应用](~/samples/integrate-web-apps-overview.md)
* [用于Microsoft Teams的低代码和无代码解决方案](~/samples/teams-low-code-solutions.md)
* [从 Web 应用共享到 Teams](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [SameSite Cookie 属性](~/resources/samesite-cookie-update.md)
* [集成Power Virtual Agents聊天机器人](~/bots/how-to/add-power-virtual-agents-bot-to-teams.md)
