---
title: 跨 Microsoft 365 扩展 Teams 应用（预览版）
description: 将 Teams 应用体验扩展到 Microsoft 365 其他使用率较高的领域
ms.date: 02/11/2022
ms.topic: overview
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 66ba17a638fc57b47febef34bea769e39cdea7e3
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111946"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>跨 Microsoft 365 扩展 Teams 应用

> [!NOTE]
> 此早期开发人员预览版旨在为 Teams 开发人员提供尝试新功能的机会，并就将 Teams 开发人员平台扩展到 Microsoft 365 生态系统的其他使用率较高的领域[提供反馈](/microsoftteams/platform/feedback)。

可以通过更新代码以使用新的 [Microsoft Teams JavaScript 客户端 SDK v2 预览版](using-teams-client-sdk-preview.md)和 Microsoft Teams [开发人员预览版清单](../resources/schema/manifest-schema-dev-preview.md)来测试 Microsoft Office 和 Outlook 中运行的 Teams 应用。

使用此预览版，可以：

- 将现有 Teams [个人选项卡](/microsoftteams/platform/tabs/how-to/create-personal-tab)扩展到桌面版和网页版 Outlook 以及 Office 网页版 (office.com)。
- 将现有 Teams [基于搜索的消息扩展](/microsoftteams/platform/messaging-extensions/how-to/search-commands/define-search-command)扩展到桌面版和网页版 Outlook。

有关反馈和问题，请继续使用相关 [Microsoft Teams 开发人员社区频道](/microsoftteams/platform/feedback)。

## <a name="teams-personal-tabs-in-office-and-outlook"></a>Office 和 Outlook 中的 Teams 个人选项卡

借助此预览版可以扩展 Teams 个人选项卡应用程序，以便在 Windows 桌面版和网页版 Outlook 以及 Office 网页版中运行。

旁加载到 Teams 后，个人选项卡将显示为 Outlook 和 Office 中已安装的应用之一。

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="在 Outlook、Office 和 Teams 中运行的个人选项卡":::

## <a name="teams-message-extensions-in-outlook"></a>Outlook 中的 Teams 消息扩展

借助此预览版可以将基于搜索的 Teams 消息扩展扩展到网页版和 Windows 桌面版 Outlook，使客户能够通过 Outlook 的撰写消息区域（以及 Microsoft Teams 客户端）搜索和共享结果。

旁加载到 Teams 后，邮件扩展将显示为 Outlook 撰写消息区域中已安装的应用之一。

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="在 Outlook 和 Teams 中运行的消息扩展":::

## <a name="next-steps"></a>后续步骤

设置开发环境以跨 Microsoft 365 扩展 Teams 应用：

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)
