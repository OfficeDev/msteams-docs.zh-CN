---
title: 开发人员预览版
description: 介绍 Microsoft 团队的公共开发人员预览版中的功能
keywords: 团队预览开发人员功能
ms.openlocfilehash: a09e715e4e2d4aba72726cc96c4d248c550a3ab1
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673288"
---
# <a name="public-developer-preview-for-microsoft-teams"></a>Microsoft 团队的公共开发人员预览版

>[!NOTE]
>预览中包含的功能可能不完整，并且可能会在公开发布之前获得更改。 仅提供它们用于测试和研究目的。 不应在生产应用程序中使用它们。

开发人员预览版是为开发人员提供对 Microsoft 团队中的 unreleased 功能的早期访问的公共计划。 这使您可以探索和测试即将推出的功能，以便在 Microsoft 团队应用中可能包含这些功能。 我们还欢迎对开发人员预览版中的任何功能提供[反馈](~/feedback.md)。 根据 Microsoft 团队客户端启用开发人员预览，因此无需担心会影响整个组织。

## <a name="developer-preview-app-manifest"></a>开发人员预览版应用程序清单

在开发人员预览中启用的许多功能都需要对应用程序清单 JSON 文件进行变更。 若要执行此操作，您需要使用[开发人员预览版清单架构](~/resources/schema/manifest-schema-dev-preview.md)。如果使用此架构，将无法使用[应用程序 Studio](~/concepts/build-and-test/app-studio-overview.md)进行这些更改，也不能使用它上传您的应用程序进行测试。 若要上传您的应用程序，您`More apps`需要单击应用栏上的图标，然后`Upload a custom app link`选择。 使用此方法，您只能上载应用程序包的压缩版本。

您可能会发现，使用应用程序 Studio 创建应用程序包的非开发人员预览部分会非常有用，然后导出该程序包并手动编辑该`manifest.json`文件，以添加您想要使用的开发人员预览功能。 将开发人员预览功能添加到`manifest.json`文件后，将无法将包重新导入到应用程序 Studio 中。

## <a name="enable-developer-preview"></a>启用开发人员预览

以每个客户端为基础启用开发人员预览，但在组织级别控制启用开发人员预览的选项。 若要启用选项以启用个人的开发人员预览版，必须确保能够上载自定义应用程序。 有关详细信息，请参阅[设置你的租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

使用包含开发人员预览功能的应用可能会导致未启用开发人员预览的客户端出现意外行为。 如果看不到 "开发人员预览" 条目，最可能的原因是您的组织未配置为应用上载。

### <a name="on-a-desktop-or-web-client"></a>在桌面或 web 客户端上

若要在桌面或 web 客户端上启用公共开发人员预览，您需要执行以下操作：

1. 在租户的管理员控制台中启用上传应用程序[，如下所述。](~/concepts/build-and-test/prepare-your-o365-tenant.md)
1. 单击您的配置文件（位于团队界面的右上角或左下方）以显示 "团队" 菜单。
1. 选择 "关于→开发人员预览"。
1. 选择 "**切换到开发人员预览**"。

### <a name="on-a-mobile-client"></a>在移动客户端上

若要在移动客户端上启用公共开发人员预览，您需要执行以下操作：

1. 在租户的管理员控制台中启用上传应用程序[，如下所述。](~/concepts/build-and-test/prepare-your-o365-tenant.md)
1. 打开左上角的 "汉堡" 菜单，然后选择 "**设置**"。
1. 选择 "**关于**"。
1. 单击 "开发人员预览" 切换。

## <a name="disable-developer-preview"></a>禁用开发人员预览

使用 "关于→开发人员预览" 下的相同菜单项，并单击它以将其关闭。

## <a name="features-available-in-developer-preview"></a>在开发人员预览版中可用的功能

有关当前在开发者预览版中启用的功能的完整列表，请参阅：[公共开发人员预览版中的功能](../../resources/dev-preview/developer-preview-features.md)。
