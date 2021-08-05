---
title: 创建内容页
author: surbhigupta
description: 如何创建内容页
keywords: teams 选项卡组通道可配置静态
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 6d1a0f6dd3593209f94966140ea94b33ac0c8d10
ms.sourcegitcommit: ec79bbbc3a8daa1ad96de809fc6d17367e8f0c6b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2021
ms.locfileid: "53726871"
---
# <a name="create-a-content-page-for-your-tab"></a>为选项卡创建内容页

内容页是在客户端中呈现Teams网页。 这些是以下部分：

* 个人范围的自定义选项卡：在这种情况下，内容页是用户遇到的第一个页面。
* 频道或组自定义选项卡：内容页在用户固定并配置相应上下文中的选项卡后显示。
* 任务 [模块](~/task-modules-and-cards/what-are-task-modules.md)：可以创建内容页，并将其作为 Web 视图嵌入任务模块中。 页面在模式弹出窗口内呈现。

本文专门介绍将内容页用作选项卡;但是，无论内容页如何呈现给用户，此处的大部分指南都适用。

## <a name="tab-content-and-design-guidelines"></a>选项卡内容和设计指南

选项卡的总体目标是提供对具有实用价值且明确用途的有意义且吸引人的内容的访问。 您必须专注于使选项卡设计干净、导航直观且内容沉浸式。

有关详细信息，请参阅选项卡[设计指南和](~/tabs/design/tabs.md)Microsoft Teams[应用商店验证指南](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)。

## <a name="integrate-your-code-with-teams"></a>将代码与Teams

若要在页面中显示Teams，必须包含[Microsoft Teams JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)客户端 SDK，并包括加载 `microsoftTeams.initialize()` 页面后对 的调用。 

以下代码提供了页面和客户端之间如何Teams的示例：

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://statics.teams.cdn.office.net/sdk/v1.10.0/js/MicrosoftTeams.min.js'></script>
...
</head>

<body>
...
    <script>
    microsoftTeams.initialize();
    </script>
...
</body>
```

## <a name="access-additional-content"></a>访问其他内容

您可以通过使用 SDK 与 Teams交互、创建深层链接、使用任务模块并验证 URL 域是否包含在数组中来访问 `validDomains` 其他内容。

### <a name="use-the-sdk-to-interact-with-teams"></a>使用 SDK 与 Teams

客户端[Teams JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md)提供了许多其他函数，您可以在开发内容页时发现这些函数很有用。

### <a name="deep-links"></a>深度链接

可以创建指向网站中的实体的深层Teams。 这些链接用于创建导航到选项卡中的内容和信息的链接。有关详细信息，请参阅 create [deep links to content and features in Teams](~/concepts/build-and-test/deep-links.md)。

### <a name="task-modules"></a>任务模块

任务模块是一种模式弹出体验，可以从选项卡触发。在内容页中，可以使用任务模块来显示表单，以收集其他信息、显示列表中项目的详细信息或向用户显示其他信息。 任务模块本身可以是其他内容页，或者完全使用自适应卡片创建。 有关详细信息，请参阅在 [选项卡中使用任务模块](~/task-modules-and-cards/task-modules/task-modules-tabs.md)。

### <a name="valid-domains"></a>有效域

确保选项卡中使用的所有 URL 域都包含在清单 `validDomains` 的 [数组中](~/concepts/build-and-test/apps-package.md)。 有关详细信息，请参阅清单架构参考中的[validDomains。](~/resources/schema/manifest-schema.md#validdomains)

> [!NOTE]
> 选项卡的核心功能存在于Teams中，而不是位于Teams。

## <a name="show-a-native-loading-indicator"></a>显示本机加载指示器

从清单 [架构 v1.7](../../../resources/schema/manifest-schema.md)开始，你可以提供 [本机加载指示器](../../../resources/schema/manifest-schema.md#showloadingindicator)。 例如， [选项卡内容页](#integrate-your-code-with-teams)、 [配置页](configuration-page.md)、 [删除页](removal-page.md)和 [选项卡中的任务模块](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)。

> [!NOTE]
> * 无法通过本机加载指示器属性配置移动客户端上的行为。 默认情况下，移动客户端在内容页和基于 iframe 的任务模块中显示此指示器。 当提出提取内容的请求时，会显示移动设备上的此指示器，请求完成后立即消除。

如果你在应用清单中指示，则所有选项卡配置、内容和删除页面以及所有基于 `showLoadingIndicator : true`  iframe 的任务模块都必须执行以下步骤：

**显示加载指示器**

1. 添加到 `"showLoadingIndicator": true` 清单。
1. 调用 `microsoftTeams.initialize();`。
1. 作为 **强制性步骤**，调用 以Teams `microsoftTeams.appInitialization.notifySuccess()` 应用已成功加载。 Teams，则隐藏加载指示器（如果适用）。 如果未在 30 秒内调用，则假定你的应用已退出，并且将显示一个显示 `notifySuccess`  重试选项的错误屏幕。
1. **（可选**）如果你已准备好打印到屏幕，并且希望延迟加载应用程序内容的其余部分，可以通过调用 手动隐藏加载指示器 `microsoftTeams.appInitialization.notifyAppLoaded();` 。
1. 如果应用程序无法加载，可以调用 以Teams `microsoftTeams.appInitialization.notifyFailure(reason);` 出现错误。 向用户显示一个错误屏幕。 以下代码提供了应用程序失败原因的示例：

    ```typescript
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```

## <a name="see-also"></a>另请参阅

* [Teams选项卡](~/tabs/what-are-tabs.md)
* [创建个人选项卡](~/tabs/how-to/create-personal-tab.md)
* [创建频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md)
* [创建内容页](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="next-step"></a>下一步

> [!div class="nextstepaction"]
> [创建配置页](~/tabs/how-to/create-tab-pages/configuration-page.md)
