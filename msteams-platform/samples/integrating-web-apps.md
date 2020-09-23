---
author: heath-hamilton
description: 将现有 web 应用与 Microsoft 团队集成的最佳实践
ms.author: v-heha
ms.date: 08/26/2020
ms.topic: conceptual
title: 将 web 应用与 Microsoft 团队集成
ms.openlocfilehash: e7d4f74526f7a71fe33d5a70d9ed60be960adefc
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210160"
---
# <a name="integrate-web-apps-with-teams"></a>将 web 应用与团队集成

您是否有您认为可自然符合团队社会和协作功能的 web 应用程序？ 这些指南可帮助您了解如何集成以下类型的应用程序：

* **独立应用程序**：可以是单页应用或大型、复杂的应用程序，您希望用户使用团队中的某些方面。
* **协作应用**程序：已为团队固有的社会和协作功能构建的应用程序。
* **Sharepoint**：要在团队中呈现的 sharepoint 页面。

对于每个准则，您都可以查看它是否适用于您的集成方案。

## <a name="get-to-know-teams-platform-capabilities"></a>了解团队平台功能

***集成方案**：独立应用程序、协作应用程序、SharePoint *

您的团队应用程序可以包括用户所需的功能，并且可能会在协作时预期的功能，但您可能不熟悉团队开发术语。

|常见应用程序功能   |团队平台功能   |
|----------|-----------|
|嵌入的网页、主页或 web 视图  |[选项卡](../tabs/what-are-tabs.md)  |
|共享快捷方式和扩展  |[消息扩展](../messaging-extensions/what-are-messaging-extensions.md)  |
|操作快捷方式和扩展  |[消息扩展](../messaging-extensions/what-are-messaging-extensions.md)  |
|Chatbots  |[机器人](../bots/what-are-bots.md) |
|频道通知  |[机器人](../bots/what-are-bots.md)<br/>[传入 webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[Office 365 连接器](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|邮件外部服务  |[机器人](../bots/what-are-bots.md)<br/>[传出 webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|模式  |[任务模块](../task-modules-and-cards/what-are-task-modules.md)  |
|内容丰富的卡片  |[自适应卡片](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a>确定功能的子集

***集成方案**：独立应用程序 *

将现有应用程序的所有功能集成到团队中通常会导致强制或 unnatural 的用户体验，尤其是在大型应用程序中。 考虑从最 impactful 的功能开始，这些功能将更自然地与团队集成。 请记住，始终允许用户启动主要应用程序，并访问其完整的功能集。

在开始任何技术工作之前，请为你的团队应用程序做一些规划：

1. 将[应用程序的用例映射到团队平台功能](../concepts/design/map-use-cases.md)。
1. [确定您的应用程序的入口点](../concepts/extensibility-points.md)。 是用于个人用途、协作还是同时使用这两者？

## <a name="understand-sharepoint-requirements-and-options"></a>了解 SharePoint 要求和选项

***集成方案**： SharePoint *

您可以将现有 [SharePoint 页面](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) 集成为 "团队" 选项卡。请记住以下几点：

* 它必须是 *新式* SharePoint Online 页面
* 仅支持个人选项卡 (无法将您的页面集成为通道选项卡) 

或者，您可以 [使用 SharePoint 框架](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction)生成 "团队" 选项卡。

## <a name="aim-towards-multi-tenancy"></a>朝着多租户为目的

***集成方案**：独立应用程序、协作应用程序、SharePoint *

如果你的应用程序由多个组织使用，请考虑多租户托管，这将使你的产品可扩展并大大简化分发。

## <a name="review-your-apis"></a>查看你的 Api

***集成方案**：独立应用程序、协作应用程序 *

不要假设您的应用程序的现有 Api 和数据结构在与团队集成时完全支持该应用程序。 您可能需要扩充这些信息，其中包含有关 [标识映射](../concepts/authentication/configure-identity-provider.md)、 [深度链接支持](../concepts/build-and-test/deep-links.md)和 [包含 Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview)的团队的上下文信息。

了解有关获取 ["团队" 选项卡](../tabs/how-to/access-teams-context.md) 或 [bot](../bots/how-to/get-teams-context.md)的上下文的详细信息。

## <a name="understand-authentication-options"></a>了解身份验证选项

***集成方案**：独立应用程序、协作应用程序、SharePoint *

Azure Active Directory (AD) 是团队的标识提供者。 如果您的应用程序使用不同的标识提供程序，则必须执行 identity mapping 练习或与 Azure AD 联盟。

团队具有单一登录 (SSO) 机制，其中包含适用于第三方应用程序的 Azure AD，以及使用诸如 OAuth 和 Open ID Connect (OIDC) 的其他标识提供程序进行身份验证流的指南。

对于 SharePoint 页面，如果您希望 SSO 在另一个应用程序中运行，则只能使用 SSO，并且无法添加其他 Azure AD ID，因为 ID 是 SharePoint 应用) 的 (。

了解有关 [团队中的身份验证的](../concepts/authentication/authentication.md)详细信息。

## <a name="follow-teams-design-guidelines"></a>关注团队设计准则

***集成方案**：独立应用程序、协作应用程序 *

通常情况下，您的应用程序应在团队中感觉自然。 您可能会认为将现有应用程序内容迁移到 "团队" 选项卡是足够的，但强烈建议您的应用遵循 [团队设计准则](../concepts/design/understand-use-cases.md)。 另请参阅： [熟知设计系统](https://fluentsite.z22.web.core.windows.net/)。

## <a name="maximize-deep-linking"></a>最大化深度链接

***集成方案**：独立应用程序、协作应用程序、SharePoint *

团队中的几乎所有内容都可以直接链接到 [深层链接](../concepts/build-and-test/deep-links.md)。 您的应用程序应最大限度地利用这些内容，包括与特定邮件和选项卡内容的链接。 Deep links 可以真正将应用程序的多个部分结合在一起，以实现更多的本机团队体验。

## <a name="be-smart-when-messaging-users"></a>在邮件用户进行智能化时进行智能化

***集成方案**：独立应用程序、协作应用程序、SharePoint *

考虑团队应用程序现在可以发送的消息类型以及长期。 如果您认为您的应用程序将有多线程对话，则 [bot](../bots/what-are-bots.md) 可能会比 [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)提供更大的灵活性。

您还可以通过 bot 向单个用户或频道发送 *主动消息* 。 这些是由外部事件触发的自发邮件，而不是发送到 bot 的邮件。  (例如，你的 bot 可以在安装时发送欢迎消息，或者新用户加入频道。 )  

发送前瞻性邮件需要特定于团队的标识符-您可以通过 [提取名单或用户配置文件数据](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile)、 [订阅会话事件](../bots/how-to/conversations/subscribe-to-conversation-events.md)或使用 [Microsoft Graph](https://docs.microsoft.com/graph/teams-proactive-messaging)来捕获此信息。

注意不到邮件过多的垃圾邮件用户。 如果团队功能支持，请考虑让用户为您的应用程序配置通知设置 (例如，"不向我发送自发消息。") 。

## <a name="use-sharepoint-for-file-and-data-storage"></a>将 SharePoint 用于文件和数据存储

***集成方案：** 独立应用程序、协作应用程序、SharePoint 页面*

创建团队时，也会将 [SharePoint 网站集](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) 配置为支持该团队的文件和数据存储。 如果您的应用程序与文件交互，则可以并应使用此功能。 您还可以使用网站集将原始数据存储在 SharePoint 列表和 Excel 中。
