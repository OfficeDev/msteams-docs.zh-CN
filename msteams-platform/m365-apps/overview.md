---
title: 跨 Microsoft 365 扩展 Teams 应用（预览版）
description: 了解如何将 Teams 应用扩展到在 Teams、Outlook 和 Office 中作为应用程序主机) 运行的 Microsoft 365 (。
ms.date: 10/10/2022
ms.topic: Conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 91586eefe21836118ed2f0a0071070ac2034bf76
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789875"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>跨 Microsoft 365 扩展 Teams 应用

使用最新版本的 [Microsoft Teams JavaScript 客户端 SDK](../tabs/how-to/using-teams-client-sdk.md) (2.0.0 及更高版本) 、 [Teams 应用清单](../resources/schema/manifest-schema.md) (版本 1.13 及更高版本) 和 [Teams 工具包](../toolkit/visual-studio-code-overview.md)，你可以生成和更新 Teams 应用以在其他高使用率的 Microsoft 365 产品中运行，并将其发布到 Microsoft 商业市场 ([Microsoft AppSource](https://appsource.microsoft.com/)) 或组织的专用应用商店。

跨 Microsoft 365 扩展 Teams 应用提供了一种简化的方式来向扩展的用户受众提供跨平台应用：从单个代码库，你可以创建针对 Teams、Outlook 和 Office 环境定制的应用体验。 最终用户无需离开其工作的上下文来使用你的应用，管理员将从整合的管理和部署工作流中受益。

Teams 应用平台将继续发展并全面扩展到 Microsoft 365 生态系统。 以下是 Microsoft 365 (Teams、Outlook 和 Office 中作为应用程序主机的 Teams 应用平台元素的当前支持) ：

| Teams 应用功能| 应用清单元素 | Teams 支持 |Outlook* 支持 | Office* 支持 | 备注 |
|--|--|--|--|--|--|
| [**选项卡**](../tabs/what-are-tabs.md) 个人范围    |`staticTabs`  | Web、桌面、移动 | Web (定向发布) 、桌面 (Beta 频道)  | Web (定向发布) 、桌面 (Beta 频道) 、移动版 (Android) | Microsoft 365 尚不支持频道和组范围。 请参阅 [备注](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook)。
| 基于搜索 [**的消息扩展**](../messaging-extensions/what-are-messaging-extensions.md)| `composeExtensions` | Web、桌面、移动| Web (定向发布) 、桌面 (Beta 频道) | - |Microsoft 365 尚不支持基于操作。 请参阅 [备注](extend-m365-teams-message-extension.md#troubleshooting)。 |
| 链接展开 | `composeExtensions.messageHandlers` | Web、桌面 | Web (定向发布) 、桌面 (Beta 频道)  | - | 查看 [备注](extend-m365-teams-message-extension.md#link-unfurling) |
| [**Office 外接程序**](/office/dev/add-ins/develop/json-manifest-overview) (预览版)  | `extensions` | - | Web、桌面 | - | 仅在 [devPreview](../resources/schema/manifest-schema-dev-preview.md) 清单版本中可用。 请参阅 [备注](#office-add-ins-preview)。|

\*[Microsoft 365 定向发布](/microsoft-365/admin/manage/release-options-in-office-365)选项和[Microsoft 365 应用版更新通道](/deployoffice/change-update-channels)注册需要整个组织或所选用户的管理员选择加入。 更新通道特定于设备，仅适用于 Windows 上运行的 Office 安装。

有关 Teams 应用清单和 SDK 版本控制指南的指导，以及有关 Microsoft 365 中当前 Teams 平台功能支持的更多详细信息，请参阅 [Teams JavaScript 客户端 SDK 概述](../tabs/how-to/using-teams-client-sdk.md)。

> [!NOTE]
> 欢迎你在扩展 Teams 应用以在 Microsoft 365 生态系统中运行时提供反馈和问题报告！ 请使用常规 [Microsoft Teams 开发人员社区频道](/microsoftteams/platform/feedback) 发送反馈。

## <a name="personal-tabs-and-messaging-extensions-in-outlook-and-office"></a>Outlook 和 Office 中的个人选项卡和消息扩展

通过将 Web 应用扩展为同时在 Outlook 和 Office 中运行的 [Teams 个人选项卡](extend-m365-teams-personal-tab.md) 应用程序，直接在工作上下文中吸引用户。

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="屏幕截图是显示 Outlook、Office 和 Teams 中运行的“个人”选项卡的示例。":::

在移动设备上，可以测试和调试在 [适用于 Android 的 Office 应用](extend-m365-teams-personal-tab.md#office-app-for-android)上运行的 Teams 个人选项卡。

:::image type="content" source="images/office-mobile-personal-tab.png" alt-text="屏幕截图是显示 Office 中运行的个人选项卡的示例。":::

除了 Microsoft Teams 客户端之外，还可以将基于搜索的 [Teams 邮件扩展](extend-m365-teams-message-extension.md)扩展到Outlook 网页版和 Windows 桌面，使客户能够通过 Outlook 的撰写邮件区域搜索和共享结果。

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="屏幕截图是显示 Outlook 和 Teams 中运行的邮件扩展的示例。":::

[链接展开](extend-m365-teams-message-extension.md#link-unfurling)  在 Outlook Web 和 Windows 环境中的工作方式与在 Microsoft Teams 中的工作方式相同，与使用 Teams 应用清单版本 1.13 或更高版本相比，没有任何进一步的工作。

:::image type="content" source="images/outlook-teams-link-unfurling.png" alt-text="屏幕截图是一个示例，显示了在 Outlook 和 Teams 中运行的链接展开。":::

使用最新的 [Teams 应用清单](../resources/schema/manifest-schema.md) 和 [Teams JavaScript 客户端 SDK](../tabs/how-to/using-teams-client-sdk.md) 生成应用，使最新的合并 Microsoft 365 应用开发过程受益。 然后，为客户提供简化的部署、安装和管理体验，以扩大应用的范围和使用情况。

## <a name="use-teams-app-manifest-across-microsoft-365"></a>跨 Microsoft 365 使用 Teams 应用清单

为了简化和简化 Microsoft 365 开发人员生态系统，我们将继续将 Teams 应用清单扩展到 Microsoft 365 的其他领域，并提供以下内容。

### <a name="office-add-ins-preview"></a>Office 外接程序 (预览版) 

现在可以在 Microsoft Teams 应用清单的 [开发人员预览版](../resources/schema/manifest-schema-dev-preview.md) 中定义和部署 Office 外接程序。 目前，此预览版仅限于在订阅 Office for Windows 上运行的 Outlook 加载项。

有关详细信息，请参阅 [Office 加载项的 Teams 清单（预览版）](/office/dev/add-ins/develop/json-manifest-overview)。

## <a name="microsoft-commercial-marketplace-submission"></a>Microsoft 商业市场提交

加入 [Microsoft 商业市场中](https://appsource.microsoft.com/) 越来越多的生产 Teams 应用 (Microsoft AppSource) 商店，并扩展了对 Outlook 和 Office 预览版的支持， (定向发布) 受众。 [为 Outlook 和 Office 启用的 Teams 应用的应用提交过程](../concepts/deploy-and-publish/appsource/publish.md)与传统 Teams 应用相同。 唯一的区别在于，你将在应用包中使用 Teams 应用清单 [版本 1.13](../tabs/how-to/using-teams-client-sdk.md) ，它引入了对跨 Microsoft 365 运行的 Teams 应用的支持。

应用发布为已启用 Microsoft 365 的 Teams 应用后，除了 Teams 应用商店外，你的应用还可以在 Outlook 和 Office 应用商店中发现为可安装的应用。 在 Outlook 和 Office 中运行时，你的应用使用 Teams 中授予的相同权限。 Teams 管理员可以管理组织中用户 [跨 Microsoft 365 对 Teams 应用的访问权限](/MicrosoftTeams/manage-third-party-teams-apps) 。

有关详细信息，请参阅 [发布适用于 Microsoft 365 的 Teams 应用](publish.md)。

## <a name="next-step"></a>后续步骤

设置开发环境以生成适用于 Microsoft 365 的 Teams 应用：

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)
