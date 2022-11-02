---
title: 创建内容页
author: surbhigupta
description: 了解 Teams 客户端中的网页，属于个人、频道或组自定义选项卡。创建内容页并将其作为 Web 视图嵌入到任务模块中。
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 4074b3bb4499cca2453a9d928a83b1cd04f5c064
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820162"
---
# <a name="create-a-content-page"></a>创建内容页

内容页是在 Teams 客户端中呈现的网页，它是以下内容的一部分：

* 个人范围的自定义选项卡：在这种情况下，内容页是用户遇到的第一页。
* 频道或群组自定义选项卡：在用户固定并在适当的上下文中配置选项卡后，显示内容页。
* [任务模块](~/task-modules-and-cards/what-are-task-modules.md)：可以创建内容页并将其作为 Web 视图嵌入到任务模块中。 页面呈现在模式弹出窗口内。

本文专门介绍如何将内容页用作选项卡;但是，无论内容页如何呈现给用户，此处的大多数指南都适用。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="tab-content-and-design-guidelines"></a>选项卡内容和设计指南

选项卡的总体目标是提供对具有实际价值和明显用途的有意义且引人入胜的内容的访问权限。

你需要专注于使选项卡设计简洁、导航直观和内容沉浸式。有关详细信息，请参阅 [选项卡设计指南](~/tabs/design/tabs.md) 和 [Microsoft Teams 应用商店验证指南](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)。

## <a name="integrate-your-code-with-teams"></a>将代码与 Teams 集成

若要在 Teams 中显示页面，必须包含 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)，并在页面加载后包含对 `app.initialize()` 的调用。

> [!NOTE]
> 由于缓存，任何内容或 UI 更改都需要近 24-48 小时才能反映在选项卡应用中。

以下代码提供了页面和 Teams 客户端如何通信的示例：

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src="https://res.cdn.office.net/teams-js/2.2.0/js/MicrosoftTeams.min.js" 
      integrity="sha384yBjE++eHeBPzIg+IKl9OHFqMbSdrzY2S/LW3qeitc5vqXewEYRWegByWzBN/chRh" 
      crossorigin="anonymous" >
    </script>
...
</head>
<body>
...
    <script>
    microsoftTeams.app.initialize();
    </script>
...
</body>
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

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

***

## <a name="access-additional-content"></a>访问其他内容

可以通过使用 SDK 与 Teams 交互、创建深层链接、使用任务模块以及验证 URL 域是否包含在 `validDomains` 数组中来访问其他内容。

### <a name="use-the-sdk-to-interact-with-teams"></a>使用 SDK 与 Teams 交互

[Teams 客户端 JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) 提供了更多在开发内容页面时很有用的函数。

### <a name="deep-links"></a>深度链接

可以在 Teams 中创建实体的深层链接。 它们用于创建导航到选项卡中的内容和信息的链接。有关详细信息，请参阅 [在 Teams 中创建指向内容和功能的深层链接](~/concepts/build-and-test/deep-links.md)。

### <a name="task-modules"></a>任务模块

任务模块是可从选项卡触发的模式弹出体验。在内容页中，使用任务模块演示表单以收集其他信息、在列表中显示项的详细信息或向用户提供其他信息。 任务模块本身可以是其他内容页，也可以是完全使用自适应卡片创建的。 有关详细信息，请参阅[在选项卡中使用任务模块](~/task-modules-and-cards/task-modules/task-modules-tabs.md)。

### <a name="valid-domains"></a>有效域

确保选项卡中使用的所有 URL 域都包含在[清单](~/concepts/build-and-test/apps-package.md)的 `validDomains` 数组中。 有关详细信息，请参阅清单架构参考中的 [validDomains](~/resources/schema/manifest-schema.md#validdomains)。

> [!NOTE]
> 选项卡的核心功能存在于 Teams 内，而不是 Teams 外部。

## <a name="show-a-native-loading-indicator"></a>显示本机加载指示器

从[清单架构 v1.7](../../../resources/schema/manifest-schema.md) 开始，可以提供[本机加载指示器](../../../resources/schema/manifest-schema.md#showloadingindicator)。 例如，[选项卡内容页](#integrate-your-code-with-teams)、[配置页](configuration-page.md)、[删除页](removal-page.md)以及[选项卡中的任务模块](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)。

> [!NOTE]
>
> 移动客户端上的行为无法通过本机加载指示器属性进行配置。 移动客户端默认在内容页和基于 iframe 的任务模块中显示此指示器。 移动设备上的此指示器将在发出内容提取请求时显示，并在请求完成后立即关闭。

如果在应用清单中指示 `showLoadingIndicator : true`，则所有选项卡配置、内容、删除页和所有基于 iframe 的任务模块都必须遵循以下步骤：

若要显示加载指示器，请执行以下操作：

1. 将 `"showLoadingIndicator": true` 添加到清单。
1. 调用 `app.initialize();`。
1. 作为 **必需** 步骤，调用 `app.notifySuccess()` 以通知 Teams 应用已成功加载。 然后，Teams 会隐藏加载指示器（如果适用）。 如果在 `notifySuccess`  30 秒内未调用 ，Teams 会假定你的应用超时，并显示一个错误屏幕，其中包含重试选项。
1. **（可选）** 如果已准备好打印到屏幕并希望延迟加载应用程序的其余内容，可以通过调用 `app.notifyAppLoaded();`来手动隐藏加载指示器。
1. 如果应用程序未加载，可以调用 `app.notifyFailure({reason: app.FailedReason.Timeout, message: "failure message"});` 以告知 Teams 有关失败的信息，并选择性地提供失败消息。 `notifyFailure` 不显示自定义消息。 将向用户显示错误屏幕。 以下代码显示了定义应用程序加载失败的可能原因的枚举：

    ```typescript
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建配置页](~/tabs/how-to/create-tab-pages/configuration-page.md)

## <a name="see-also"></a>另请参阅

* [Teams 的生成选项卡](../../what-are-tabs.md)
* [创建个人选项卡](../create-personal-tab.md)
* [创建频道选项卡或组选项卡](../create-channel-group-tab.md)
* [Teams 的应用清单架构](../../../resources/schema/manifest-schema.md)
* [适用于 Microsoft Teams 选项卡的 DevTools](~/tabs/how-to/developer-tools.md)
