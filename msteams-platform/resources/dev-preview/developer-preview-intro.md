---
title: 开发者预览版
description: 介绍公共服务开发者预览版中的Microsoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: teams 预览开发人员功能
ms.openlocfilehash: 1dc719ae9ead4ef7c7519925b79ca62859ada903
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345556"
---
# <a name="public-developer-preview-for-microsoft-teams"></a>公共开发人员预览版Microsoft Teams

>[!NOTE]
>预览版中包含的功能可能不完整，在公开发布之前可能会发生更改。 它们仅供测试和探索使用。 它们不应在生产应用程序中使用。

开发者预览版开发人员的公共计划，可提前访问 Microsoft Teams 中未Microsoft Teams。 这允许你浏览和测试即将推出的功能，以潜在地包含在Microsoft Teams应用中。 我们还欢迎 [提供有关开发人员](~/feedback.md) 预览版中任何功能的反馈。 开发人员预览Microsoft Teams客户端启用，因此无需担心影响整个组织。

## <a name="developer-preview-app-manifest"></a>开发人员预览应用清单

开发人员预览版中启用的许多功能都需要更改应用清单 JSON 文件。 为此，将需要使用开发人员预览清单架构 如果[](~/resources/schema/manifest-schema-dev-preview.md)使用此架构，你将不能使用[App Studio](~/concepts/build-and-test/app-studio-overview.md)进行这些更改，也不能使用它上载应用进行测试。 若要上传应用，你需要单击应用栏上的 `More apps` 图标，然后选择 `Upload a custom app link` 。 使用此方法，你只能上传应用包的压缩版本。

你可能会发现使用 App Studio 创建应用包的非开发人员预览部分非常有用，然后导出该包并手动编辑文件以添加想要使用的 `manifest.json` 开发人员预览功能。 将开发人员预览功能添加到文件后，将无法将程序包重新导入 `manifest.json` App Studio。

## <a name="enable-developer-preview"></a>启用开发人员预览

基于每个客户端启用开发人员预览，但启用开发人员预览的选项在组织级别控制。 若要启用为个人启用开发人员预览的选项，必须确保他们能够上传自定义应用。 有关 [其他信息，](~/concepts/build-and-test/prepare-your-o365-tenant.md) 请参阅设置租户。

使用包含开发人员预览功能的应用可能会导致未启用开发人员预览的客户端发生意外行为。 如果未看到开发人员预览条目，最可能的原因是您的组织未配置应用上载。

### <a name="on-a-desktop-or-web-client"></a>在桌面或 Web 客户端上

若要在桌面或 Web 客户端上启用公共开发人员预览，需要执行以下操作：

1. 在租户的管理控制台中启用应用上传，如下 [所述](~/concepts/build-and-test/prepare-your-o365-tenant.md)。
1. 单击你的配置文件 (右上角或左下角的 Teams，) 显示Teams菜单。
1. 选择"关于→开发人员预览"。
1. 选择 **切换到开发人员预览**。

### <a name="on-a-mobile-client"></a>在移动客户端上

若要在移动客户端上启用公共开发人员预览版，需要执行以下操作：

1. 在租户的管理控制台中启用应用上传，如下 [所述](~/concepts/build-and-test/prepare-your-o365-tenant.md)。
1. 打开左上方的汉堡包菜单，然后选择 **"设置"。**
1. 选择 **"关于"。**
1. 单击"开发人员预览"切换。

## <a name="disable-developer-preview"></a>禁用开发人员预览

使用"关于开发人员预览→"下的同一菜单项，然后单击它将其关闭。



