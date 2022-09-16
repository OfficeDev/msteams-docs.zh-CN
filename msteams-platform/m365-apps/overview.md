---
title: 跨 Microsoft 365 扩展 Teams 应用（预览版）
description: 本文介绍如何生成、更新和扩展 Teams 应用体验，以及如何创建跨 Microsoft 365 的其他高使用区域使用的应用。
ms.date: 05/24/2022
ms.topic: Conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: fec2a91d250044e638783ecb25175771a60f3cdd
ms.sourcegitcommit: de7496f9586316bed12d115cd3e4c18ba0854d4f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2022
ms.locfileid: "67781071"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>跨 Microsoft 365 扩展 Teams 应用

随着最新版本的 [Microsoft Teams JavaScript 客户端 SDK](../tabs/how-to/using-teams-client-sdk.md) (版本 2.0.0 及更高版本) ， [Teams 应用清单](../resources/schema/manifest-schema.md) (版本 1.13 及更高版本) 和 [Teams 工具包](../toolkit/visual-studio-code-overview.md)，你可以生成和更新 Teams 应用以在其他高使用率的 Microsoft 365 产品中运行，并将其发布到 Microsoft 商业市场 ([Microsoft 商业市场](https://appsource.microsoft.com/)) 。

跨 Microsoft 365 扩展 Teams 应用提供了一种简化的方式，可将跨平台应用交付给扩展的用户受众：从单个代码库中，可以创建为 Teams、Outlook 和 Office 环境定制的应用体验。 最终用户无需离开其工作的上下文即可使用你的应用，管理员将受益于合并管理和部署工作流。

Teams 应用平台继续发展并全面扩展到 Microsoft 365 生态系统。 以下是 Microsoft 365 (Teams、Outlook 和 Office 作为应用程序主机的 Teams 应用平台元素的当前支持) ：

|          | 应用清单元素 | Teams 支持 |Outlook* 支持 | Office* 支持 | 备注 |
|--|--|--|--|--|--|
| [**选项卡**](../tabs/what-are-tabs.md) (个人范围)     |`staticTabs`  | Web、桌面、移动 | Web (目标发布) 、桌面 (Beta 通道)  | Web (目标发布) 、桌面 (Beta 通道) | Microsoft 365 尚不支持频道和组范围。 请参阅 [笔记](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook)。
| [**消息扩展**](../messaging-extensions/what-are-messaging-extensions.md) (基于搜索的) | `composeExtensions` | Web、桌面、移动| Web (目标发布) 、桌面 (Beta 通道) | - |Microsoft 365 尚不支持基于操作的操作。 请参阅 [笔记](extend-m365-teams-message-extension.md#preview-your-message-extension-in-outlook)。 |
| [**Office 加载项**](/office/dev/add-ins/develop/json-manifest-overview) (预览)  | `extensions` | - | Web、桌面 | - | 仅在 [devPreview](../resources/schema/manifest-schema-dev-preview.md) 清单版本中可用。 请参阅 [笔记](#office-add-ins-preview)。|

\*[Microsoft 365 目标发布](/microsoft-365/admin/manage/release-options-in-office-365)选项和[Microsoft 365 应用版更新通道](/deployoffice/change-update-channels)注册要求整个组织或所选用户的管理员选择加入。 更新通道是特定于设备的，仅适用于在 Windows 上运行的 Office 的安装。

有关 Teams 应用清单和 SDK 版本控制指南的指导，以及有关 Microsoft 365 中当前 Teams 平台功能支持的更多详细信息，请参阅 [Teams JavaScript 客户端 SDK 概述](../tabs/how-to/using-teams-client-sdk.md)。

> [!NOTE]
> 我们欢迎你的反馈和问题报告，因为你展开 Teams 应用以跨 Microsoft 365 生态系统运行！ 请使用常规 [的 Microsoft Teams 开发人员社区频道](/microsoftteams/platform/feedback) 发送反馈。

## <a name="personal-tabs-and-messaging-extensions-in-outlook-and-office"></a>Outlook 和 Office 中的个人选项卡和消息传递扩展

通过将 Web 应用扩展为同样在 Outlook 和 Office 中运行的 Teams 个人选项卡应用程序，在用户的工作上下文中访问用户。

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="屏幕截图是显示 Outlook、Office 和 Teams 中运行的个人选项卡的示例。":::

还可以将基于搜索的 Teams 消息扩展扩展到Outlook 网页版和 Windows 桌面，使客户能够通过 Outlook 的撰写消息区域（除了 Microsoft Teams 客户端）搜索和共享结果。

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="屏幕截图是显示 Outlook 和 Teams 中运行的消息扩展的示例。":::

使用最新的 [Teams 应用清单](../resources/schema/manifest-schema.md) 和 [Teams JavaScript 客户端 SDK](../tabs/how-to/using-teams-client-sdk.md) 生成应用可为你提供一个合并的开发过程。 通过为客户提供简化的部署、安装和管理体验，可以扩展应用的潜在覆盖面和使用范围。

## <a name="use-teams-app-manifest-across-microsoft-365"></a>跨 Microsoft 365 使用 Teams 应用清单

为了简化和简化 Microsoft 365 开发人员生态系统，我们将继续使用以下内容将 Teams 应用清单扩展到 Microsoft 365 的其他领域。

### <a name="office-add-ins-preview"></a>Office 加载项 (预览) 

现在可以在 Microsoft Teams 应用清单的 [开发人员预览版](../resources/schema/manifest-schema-dev-preview.md) 中定义和部署 Office 加载项。 目前，此预览版仅限于在订阅 Office for Windows 上运行的 Outlook 加载项。

有关详细信息，请参阅 [Office 加载项的 Teams 清单（预览版）](/office/dev/add-ins/develop/json-manifest-overview)。

## <a name="microsoft-commercial-marketplace-submission"></a>Microsoft 商业市场提交

将越来越多的生产 Teams 应用加入 [Microsoft 商业市场](https://appsource.microsoft.com/) (Microsoft AppSource) 应用商店，并扩展了对 Outlook 和 Office 预览版 (目标发布) 受众的支持。 [为 Outlook 和 Office 启用的 Teams 应用的应用提交过程](../concepts/deploy-and-publish/appsource/publish.md)与传统 Teams 应用相同。 唯一的区别是，你将在应用包中使用 Teams 应用清单 [版本 1.13](../tabs/how-to/using-teams-client-sdk.md) ，这引入了对跨 Microsoft 365 运行的 Teams 应用的支持。

发布为已启用 Microsoft 365 的 Teams 应用后，除了 Teams 应用商店之外，你的应用将作为可安装的应用从 Outlook 和 Office 应用商店中发现。 在 Outlook 和 Office 中运行时，应用使用 Teams 中授予的相同权限。 对于组织中的用户，Teams 管理员可以 [管理对 Microsoft 365 中 Teams 应用的访问权限](/MicrosoftTeams/manage-third-party-teams-apps) 。

有关详细信息，请参阅 [Microsoft 365 的发布 Teams 应用](publish.md)。

## <a name="next-step"></a>后续步骤

设置开发环境以生成适用于 Microsoft 365 的 Teams 应用：

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)
