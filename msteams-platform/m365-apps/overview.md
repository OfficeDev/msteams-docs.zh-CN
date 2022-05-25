---
title: 跨 Microsoft 365 扩展 Teams 应用（预览版）
description: 将 Teams 应用体验扩展到 Microsoft 365 其他使用率较高的领域
ms.date: 05/24/2022
ms.topic: overview
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 9cc0d88d5f992aa596509a6206a26baa413bdcf1
ms.sourcegitcommit: c197fe4c721822b6195dfc5c7d8e9ccd47f142fe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2022
ms.locfileid: "65668142"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>跨 Microsoft 365 扩展 Teams 应用

使用最新版本[的 Microsoft Teams JavaScript 客户端 SDK](../tabs/how-to/using-teams-client-sdk.md) (版本 2.0.0) 、[Teams应用清单](../resources/schema/manifest-schema.md) (版本 1.13) 和[Teams Toolkit](../toolkit/visual-studio-code-overview.md)，可以生成和更新Teams应用以在其他高使用率Microsoft 365 产品并将其发布到 Microsoft 商业市场 ([Microsoft AppSource](https://appsource.microsoft.com/)) 。

跨Microsoft 365扩展Teams应用提供了一种简化的方式，可将跨平台应用交付给扩展的用户受众：从单个代码库中，可以创建为Teams、Outlook和Office环境量身定制的应用体验。 最终用户无需离开其工作的上下文即可使用你的应用，管理员将受益于合并管理和部署工作流。

Teams应用平台继续发展并全面扩展到Microsoft 365生态系统。 以下是应用程序主机) Microsoft 365 (Teams、Outlook和Office Teams应用平台元素的当前支持：

|          | 应用清单元素 | Teams支持 |Outlook* 支持 | Office* 支持 | 注释 |
|--|--|--|--|--|--|
| [**选项卡**](../tabs/what-are-tabs.md) (个人范围)     |`staticTabs`  | Web、桌面、移动 | Web (目标发布) 、桌面 (Beta 通道)  | Web (目标发布) | Microsoft 365尚不支持通道和组范围。 请参阅 [笔记](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook)。
| [**消息扩展**](../messaging-extensions/what-are-messaging-extensions.md) (基于搜索的) | `composeExtensions` | Web、桌面、移动| Web (目标发布) 、桌面 (Beta 通道) | |Microsoft 365尚不支持基于操作的操作。 请参阅 [笔记](extend-m365-teams-message-extension.md#preview-your-message-extension-in-outlook)。 |
| [**Graph连接器**](/microsoftsearch/connectors-overview)| `graphConnector` | Web、桌面、移动| Web、桌面 | Web| 请参阅 [笔记](#graph-connectors)
| [**Office加载项**](/office/dev/add-ins/develop/json-manifest-overview) (预览)  | `extensions` | | Web、桌面  | | 仅在 [devPreview](../resources/schema/manifest-schema-dev-preview.md) 清单版本中可用。 请参阅 [笔记](#office-add-ins-preview)。|

\*[Microsoft 365定向发布](/microsoft-365/admin/manage/release-options-in-office-365)选项和[Microsoft 365 应用版更新通道](/deployoffice/change-update-channels)注册需要管理员选择加入整个组织或所选用户。

有关Teams应用清单和 SDK 版本控制指南的指南，以及有关跨Microsoft 365当前Teams平台功能支持的更多详细信息，请参阅 [Teams JavaScript 客户端 SDK 概述](../tabs/how-to/using-teams-client-sdk.md)。

> [!NOTE]
> 我们欢迎你的反馈和问题报告，你展开Teams应用以在Microsoft 365生态系统中运行！ 请使用常规[Microsoft Teams开发人员社区频道](/microsoftteams/platform/feedback)发送反馈。

## <a name="personal-tabs-and-messaging-extensions-in-outlook-and-office"></a>Outlook和Office中的个人选项卡和消息传递扩展

通过将 Web 应用扩展为同时在Outlook和Office中运行的Teams个人选项卡应用程序，在用户的工作上下文中访问用户。

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="在 Outlook、Office 和 Teams 中运行的个人选项卡":::

你还可以将基于搜索的Teams消息扩展扩展到Outlook 网页版和Windows桌面，使客户能够通过Outlook的撰写消息区域搜索和共享结果，以及Microsoft Teams客户端。

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="在 Outlook 和 Teams 中运行的消息扩展":::

使用最新的[Teams应用清单](../resources/schema/manifest-schema.md)和 [Teams JavaScript 客户端 SDK](../tabs/how-to/using-teams-client-sdk.md) 生成应用可为你提供一个合并的开发过程。 通过为客户提供简化的部署、安装和管理体验，可以扩展应用的潜在覆盖面和使用范围。

## <a name="use-teams-app-manifest-across-microsoft-365"></a>跨Microsoft 365使用Teams应用清单

为了简化和简化Microsoft 365开发人员生态系统，我们将继续使用以下内容将Teams应用清单扩展到其他Microsoft 365领域。

### <a name="graph-connectors"></a>Graph连接器

使用 Microsoft Graph 连接器，组织可以为第三方数据编制索引，使其显示为Microsoft 搜索结果，从而扩展Teams应用中可搜索的内容源的类型。
有关详细信息，请[参阅 Microsoft Graph 连接器Microsoft 搜索概述](/microsoftsearch/connectors-overview)。

若要开始使用Teams应用中的图形连接器，请查看[Teams Toolkit Graph连接器示例](https://aka.ms/teamsfx-graph-connector-sample)并[Microsoft Teams开发人员预览清单架构](../resources/schema/manifest-schema-dev-preview.md)参考。

### <a name="office-add-ins-preview"></a>Office加载项 (预览) 

现在可以在Microsoft Teams应用清单的[开发人员预览版](../resources/schema/manifest-schema-dev-preview.md)中定义和部署Office加载项。 目前，此预览版仅限于Outlook订阅Office上为Windows运行的加载项。

有关详细信息，请参阅[Office加载项 (预览) Teams清单](/office/dev/add-ins/develop/json-manifest-overview)。

## <a name="microsoft-appsource-submission"></a>Microsoft AppSource 提交

在 [Microsoft AppSource](https://appsource.microsoft.com/) 应用商店中加入越来越多的生产Teams应用，并扩展了对Outlook和Office预览版 (目标发布) 受众的支持。 [为Outlook和Office启用的Teams应用的应用提交过程](../concepts/deploy-and-publish/appsource/publish.md)与传统Teams应用的提交过程相同;唯一的区别是在应用包中使用Teams应用清单[版本 1.13](../tabs/how-to/using-teams-client-sdk.md)，这引入了对跨应用运行的Teams应用的支持Microsoft 365。

发布为已启用Microsoft 365 Teams应用后，除了Teams应用商店之外，你的应用将从Outlook和Office 应用存储中发现为可安装的应用。 在Outlook和Office中运行时，应用使用在Teams中授予的相同权限。 Teams管理员可以管理对组织中用户[跨Microsoft 365 Teams应用的访问权限](/MicrosoftTeams/manage-third-party-teams-apps)。

有关详细信息，请参阅[发布Microsoft 365 Teams应用](publish.md)。

## <a name="next-step"></a>后续步骤

设置开发环境以生成用于Microsoft 365的Teams应用：

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)
