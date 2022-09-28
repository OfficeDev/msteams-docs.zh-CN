---
title: 适用于 Microsoft Teams 的公共开发人员预览版
description: 开发人员预览 (Beta) 是一个公共计划，用于探索和测试即将推出的功能，以便可能包含在 Microsoft Teams 应用中。
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: dd0583f453e93a0127bf4cbcc29a6a56dec6655a
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100285"
---
# <a name="public-developer-preview-for-teams"></a>Teams 公共开发人员预览版

>[!NOTE]
>预览版中包含的功能可能不完整，并且在公开发布之前可能会发生更改。 它们仅用于测试和探索目的。 不应在生产应用程序中使用它们。

开发人员预览版是面向开发人员的公共计划，可提供对 Microsoft Teams 中未发布功能的早期访问权限。 这使你能够探索和测试即将推出的功能，以便可能包含在 Teams 应用中。 欢迎你对开发者预览版中的任何功能提供 [反馈](~/feedback.md)。 每个 Microsoft Teams 客户端都已启用开发者预览版，因此你不必担心会影响整个组织。

## <a name="developer-preview-app-manifest"></a>开发人员预览版应用清单

开发人员预览版中启用的许多功能都需要更改应用清单 JSON 文件。 为此，需要使用 [开发人员预览清单架构](~/resources/schema/manifest-schema-dev-preview.md)。 如果使用此架构，将无法使用 [Teams 开发人员门户](~/concepts/build-and-test/teams-developer-portal.md) 做出这些更改，也无法将其用于上传应用来进行测试。 若要上传应用，需要选择应用栏上的 `More apps` 图标，然后选择 `Upload a custom app link`。 使用此方法，只能上传应用包的压缩版本。

你可能会发现使用 Teams 开发人员门户 创建应用包的非开发人员预览部分，然后导出该包并手动编辑 `manifest.json` 文件来添加要使用的开发人员预览功能是很有用的。 将开发人员预览功能添加到 `manifest.json` 文件后，将无法将包重新导入 Teams 开发人员门户。

## <a name="enable-developer-preview"></a>启用开发人员预览版

开发人员预览按客户端基础启用，但开启开发人员预览的选项是在组织层面控制的。 若要启用为个人开启开发人员预览的选项，必须确保他们能够上传自定义应用。 有关其他信息，请参阅 [设置租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

使用包含开发人员预览功能的应用可能导致未启用开发人员预览的客户端出现意外行为。 如果看不到开发人员预览的条目，最可能的原因是未配置组织以进行应用上传。

### <a name="on-a-desktop-or-web-client"></a>在桌面或 Web 客户端上

如果要在桌面或 Web 客户端上启用公共开发人员预览，请执行以下操作：

1. 为开发人员租户启用自定义应用上传或旁加载。 有关详细信息，请参阅 [启用自定义 Teams 应用](../../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。
1. 选择用户配置文件旁边的省略号（“...”）菜单以显示 Teams 菜单。
1. 选择“**关于**” > “**开发人员预览**”。
1. 选择“**切换到开发人员预览版**”。

### <a name="on-a-mobile-client"></a>在移动客户端上

要在移动客户端上启用公共开发人员预览，请执行以下操作：

1. 为开发人员租户启用应用上传或旁加载。 有关详细信息，请参阅 [启用自定义 Teams 应用](../../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。
1. 打开左上角的汉堡菜单，然后选择 **设置**。
1. 选择“**关于**”。
1. 打开“**开发人员预览**”切换开关。

## <a name="disable-developer-preview"></a>禁用开发人员预览

使用“关于”→“开发人员预览”下的相同菜单项，并选择它以将其关闭。

## <a name="see-also"></a>另请参阅

[测试和调试 Microsoft Teams 应用](~/concepts/build-and-test/debug.md)
