---
author: heath-hamilton
description: 将现有 Web 应用与 Microsoft Teams 集成的最佳方案
ms.author: v-heha
ms.date: 08/26/2020
ms.topic: conceptual
title: 将 Web 应用与 Microsoft Teams 集成
ms.openlocfilehash: 4671d2277d5eb7c035421c51b1714eccaac06a31
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696484"
---
# <a name="integrate-web-apps-with-teams"></a>将 Web 应用与 Teams 集成

你是否具有你认为适合 Teams 社交和协作功能的 Web 应用？ 这些指南可帮助你了解如何集成以下类型的应用：

* **独立应用**：可以是单页应用或希望用户使用 Teams 中某些方面的大型复杂应用。
* **协作应用**：为 Teams 固有的社交和协作功能构建的应用。
* **SharePoint：** 想要在 Teams 中显示 SharePoint 页面。

对于每个指南，你可以查看它是否适用于你的集成方案。

## <a name="get-to-know-teams-platform-capabilities"></a>了解 Teams 平台功能

***集成方案：** 独立应用程序、协作应用程序、SharePoint*

Teams 应用可以包含用户在协作时需要和可能期望的功能，但你可能不熟悉 Teams 开发术语。

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

将现有应用程序的所有功能集成到 Teams 中通常会导致强制的或不自然的用户体验，尤其是在大型应用中。 请考虑从影响最大的功能和与 Teams 更自然地集成的功能开始。 请记住，你始终可以允许用户启动主应用并访问其完整功能集。

在开始任何技术工作之前，请对 Teams 应用进行一些规划：

1. [将应用的用例映射到 Teams 平台功能](../concepts/design/map-use-cases.md)。
1. [确定应用的入口点](../concepts/extensibility-points.md)。 它是用于个人用途、协作还是同时用于两者？

## <a name="understand-sharepoint-requirements-and-options"></a>了解 SharePoint 要求和选项

***集成方案**： SharePoint*

可以将现有 [SharePoint 页面集成为](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) Teams 选项卡。请记住以下事项：

* 它必须 *是新式* SharePoint Online 页面
* 只有个人选项卡 (无法将页面集成为频道选项卡) 

或者，可以使用 [SharePoint](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction)框架生成 Teams 选项卡。

## <a name="aim-towards-multi-tenancy"></a>旨在实现多租户

***集成方案：** 独立应用程序、协作应用程序、SharePoint*

如果你的应用由多个组织使用，请考虑多租户托管，这将提高产品可扩展性并极大地简化分发。

## <a name="review-your-apis"></a>查看 API

***集成方案**：独立应用、协作应用*

与 Teams 集成时，请勿假定应用的现有 API 和数据结构完全支持该应用。 你可能需要使用有关 Teams 的上下文信息来扩充[](../concepts/authentication/configure-identity-provider.md)这些信息，以用于标识映射、[深层链接支持](../concepts/build-and-test/deep-links.md)以及合并[Microsoft Graph。](https://docs.microsoft.com/graph/teams-concept-overview)

详细了解如何获取 Teams 选项卡或[自动程序](../tabs/how-to/access-teams-context.md)[的上下文](../bots/how-to/get-teams-context.md)。

## <a name="understand-authentication-options"></a>了解身份验证选项

***集成方案：** 独立应用程序、协作应用程序、SharePoint*

Azure Active Directory (AD) 是 Teams 的标识提供程序。 如果你的应用使用不同的标识提供程序，你必须执行标识映射练习或与 Azure AD 联合。

Teams 具有适用于第三方应用的 Azure AD 的单一登录 (SSO) 机制，以及使用 OAuth 和开放 ID Connect (OIDC) 等标准将身份验证流到其他标识提供商的指南。

对于 SharePoint 页面，如果你希望 SSO 适用于另一个应用程序页面，则只能使用 SSO，并且不能添加其他 Azure AD ID (因为 ID 是 SharePoint 应用程序) 。

详细了解 Teams [中的身份验证](../concepts/authentication/authentication.md)。

## <a name="follow-teams-design-guidelines"></a>遵循 Teams 设计指南

***集成方案**：独立应用、协作应用*

通常，你的应用在 Teams 中应该感觉自然。 你可能认为将现有应用内容迁移到 Teams 选项卡就足够了，但我们强烈建议你的应用遵循 [Teams 设计指南](../concepts/design/understand-use-cases.md)。 另请参阅 [：Fluent Design System](https://fluentsite.z22.web.core.windows.net/)。

## <a name="maximize-deep-linking"></a>最大化深层链接

***集成方案：** 独立应用程序、协作应用程序、SharePoint*

Teams 中几乎所有内容都可以直接链接到深层 [链接](../concepts/build-and-test/deep-links.md)。 你的应用应最大限度地利用这些信息，包括链接到特定消息和选项卡内容以及从这些邮件和选项卡内容进行链接。 深度链接可以真正将应用的多个部分连接在一起，以获得更本机的 Teams 体验。

## <a name="be-smart-when-messaging-users"></a>在消息传递用户时要智能

***集成方案：** 独立应用程序、协作应用程序、SharePoint*

考虑 Teams 应用现在和长期可能发送的消息类型。 如果你认为你的应用将拥有多线程对话，机器人可能会提供比[webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)更大的灵活性。 [](../bots/what-are-bots.md)

自动程序还允许你向单个 *用户* 或频道发送主动消息。 这些是外部事件触发的未经提示的消息，而不是发送给自动程序的消息。  (例如，自动程序可以在安装后或新用户加入频道时发送欢迎消息) 

发送主动邮件需要特定于 Teams 的标识符 ，可以通过提取名单或[](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)用户配置文件数据、订阅对话事件，或者[](../bots/how-to/conversations/subscribe-to-conversation-events.md)使用 Microsoft Graph 来[捕获此信息](https://docs.microsoft.com/graph/teams-proactive-messaging)。

请注意不要向邮件过多的用户发送过多邮件。 如果 Teams 功能支持此功能，请考虑让用户为你的应用配置通知设置 (例如，"不要向我发送不拒绝的消息"。) 。

## <a name="use-sharepoint-for-file-and-data-storage"></a>将 SharePoint 用于文件和数据存储

***集成方案：** 独立应用程序、协作应用程序、SharePoint 页面*

创建团队时，还会设置 [SharePoint](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) 网站集以支持该团队的文件和数据存储。 如果应用与文件交互，应用可以并且应该利用此功能。 您还可以使用网站集在 SharePoint 列表和 Excel 中存储原始数据。
