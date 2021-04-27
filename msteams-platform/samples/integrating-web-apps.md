---
author: heath-hamilton
description: 将现有 Web 应用与 Microsoft Teams 集成的最佳方案
ms.author: v-heha
ms.date: 08/26/2020
localization_priority: Normal
ms.topic: conceptual
title: Web 应用
ms.openlocfilehash: 1f46c4a8b9457a00b5000e81c280759f584a50d2
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020420"
---
# <a name="web-apps"></a>Web 应用 

通过将 Web 应用与 Teams 正确集成，你可以使 Web 应用适合 Teams 的社交和协作功能。
  
可以与 Teams 集成的不同应用类型如下所示：
* **独立应用**：独立应用是单页应用或大型复杂应用。 用户可以在 Teams 中使用它的某些方面。
* **协作应用**：为 Teams 固有的社交和协作功能构建的应用。
* **SharePoint：** 想要在 Teams 中显示 SharePoint 页面。

你可以映射并按照适用于集成方案的适当准则执行。
本文档概述了 Teams 功能、文件和数据存储的共享点要求、API 要求、应用的身份验证和 Teams 的深层链接。
 
## <a name="get-to-know-teams-platform-capabilities"></a>了解 Teams 平台功能

***集成方案：** 独立应用程序、协作应用程序、SharePoint*

Teams 应用必须包含必需和预期的协作功能。 若要使用应用集成，必须熟悉 Teams 开发术语。

|常见应用功能   |Teams 平台功能   |
|----------|-----------|
|嵌入式网页、主页或 Webview  |[选项卡](../tabs/what-are-tabs.md)  |
|共享快捷方式和扩展  |[消息扩展](../messaging-extensions/what-are-messaging-extensions.md)  |
|操作快捷方式和扩展  |[消息扩展](../messaging-extensions/what-are-messaging-extensions.md)  |
|Chatbots  |[机器人](../bots/what-are-bots.md) |
|频道通知  |[机器人](../bots/what-are-bots.md)<br/>[传入 Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Office 365 连接器](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|邮件外部服务  |[机器人](../bots/what-are-bots.md)<br/>[传出 webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|Modals  |[任务模块](../task-modules-and-cards/what-are-task-modules.md)  |
|内容丰富的卡片  |[自适应卡](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>确定功能的子集

***集成方案**：独立应用*

将现有应用程序的所有功能集成到 Teams 中通常会导致强制的或不自然的用户体验，尤其是在大型应用中。 从影响最大的功能和与 Teams 更自然地集成的功能开始。 你可以允许用户启动主应用并访问其完整功能集。

**将应用与 Teams 集成的先决条件** 以下是将应用与 Teams 集成的先决条件。 

1. [将应用的用例映射到 Teams 平台功能](../concepts/design/map-use-cases.md)。
1. [确定应用的入口点](../concepts/extensibility-points.md)。 它是用于个人用途、协作还是同时用于两者？

## <a name="understand-sharepoint-requirements-and-options"></a>了解 SharePoint 要求和选项

***集成方案**： SharePoint*

若要将现有 [SharePoint 页面集成](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) 为"Teams"选项卡，必须考虑以下事项：

* 它必须 *是新式* SharePoint Online 页面。
* 仅支持个人选项卡。 无法将页面作为通道选项卡进行集成。

或者，可以使用 [SharePoint](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction)框架生成 Teams 选项卡。

## <a name="aim-towards-multi-tenancy"></a>旨在实现多租户

***集成方案：** 独立应用程序、协作应用程序、SharePoint*

如果你的应用由多个组织使用，请考虑多租户托管，它使产品可扩展并大大简化分发。

## <a name="review-your-apis"></a>查看 API

***集成方案**：独立应用、协作应用*

与 Teams 集成时，你必须使应用的现有 API 和数据结构支持该应用。 若要扩展支持，必须使用有关 Teams 的上下文信息扩充 API 和数据结构，以用于[](../concepts/authentication/configure-identity-provider.md)标识映射、[](../concepts/build-and-test/deep-links.md)深层链接支持以及合并[Microsoft Graph。](https://docs.microsoft.com/graph/teams-concept-overview)

详细了解如何获取 Teams 选项卡或[自动程序](../tabs/how-to/access-teams-context.md)[的上下文](../bots/how-to/get-teams-context.md)。

## <a name="understand-authentication-options"></a>了解身份验证选项

***集成方案：** 独立应用程序、协作应用程序、SharePoint*

Azure Active Directory (AD) 是 Teams 的标识提供程序。 如果你的应用使用不同的标识提供程序，则必须执行标识映射练习或与 Azure AD 结合使用。

Teams 具有单一登录 (SSO) Azure AD 的第三方应用机制。 它还提供了使用 OAuth 和 Open ID Connect（称为 OIDC）等标准向其他标识提供商进行身份验证的指南。

对于 SharePoint 页面，如果你希望 SSO 适用于另一个应用程序，则只能使用 SSO，并且不能添加其他 Azure AD ID，因为 ID 是 SharePoint 应用程序。

详细了解 Teams [中的身份验证](../concepts/authentication/authentication.md)。

## <a name="follow-teams-design-guidelines"></a>遵循 Teams 设计指南

***集成方案**：独立应用、协作应用*

确保遵循 [Teams 设计指南](../concepts/design/understand-use-cases.md) ，使你的应用成为 Teams 本机应用。 无法将现有应用内容迁移到 Teams 选项卡。有关应用设计详细信息，请参阅[Fluent Design System。](https://fluentsite.z22.web.core.windows.net/)

## <a name="maximize-deep-linking"></a>最大化深层链接

***集成方案：** 独立应用程序、协作应用程序、SharePoint*

可以在 Teams 内创建指向信息和功能的链接。 使用 [深层链接](../concepts/build-and-test/deep-links.md) 将你的应用与 Teams 链接，因为它们将应用的多个部分关联在一起，获得更本机的 Teams 体验。

## <a name="be-smart-when-messaging-users"></a>在消息传递用户时要智能

***集成方案：** 独立应用程序、协作应用程序、SharePoint*

在 [Teams](../bots/what-are-bots.md) 应用中使用自动程序进行多线程对话，因为它提供比 [Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)更大的灵活性。

自动程序还允许你向单个 **用户** 或频道发送主动消息。 主动邮件是由外部事件触发的未经提示的消息，而不是发送给自动程序的消息。 例如，自动程序在安装或新用户加入频道时发送欢迎消息。 

发送主动邮件需要特定于 Teams 的标识符。 您可以通过提取[名单或用户配置文件](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)数据、订阅对话事件，或者使用[](../bots/how-to/conversations/subscribe-to-conversation-events.md)Microsoft Graph 来[捕获信息](https://docs.microsoft.com/graph/teams-proactive-messaging)。

不要向具有过多邮件的用户发送垃圾邮件。 如果 Teams 功能支持此功能，用户可以为你的应用配置通知设置。   
下面是一条通知邮件的示例： **不要向我发送不通知的邮件**。

## <a name="use-sharepoint-for-file-and-data-storage"></a>将 SharePoint 用于文件和数据存储

***集成方案：** 独立应用程序、协作应用程序、SharePoint 页面*

创建团队时，还会设置 [SharePoint](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) 网站集以支持该团队的文件和数据存储。 如果应用与文件交互，则必须利用此功能。 使用网站集在 SharePoint 列表和 Excel 中存储原始数据。

## <a name="see-also"></a>另请参阅

> [!div class="nextstepaction"]
> [集成 web 应用](~/samples/integrate-web-apps-overview.md)
