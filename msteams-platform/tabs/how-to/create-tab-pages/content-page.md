---
title: 创建内容页
author: laujan
description: 如何创建内容页
keywords: 团队选项卡组频道配置静态
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: ad1e1a015526fd723670ea7eda735ebf88f85bf8
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552533"
---
# <a name="create-a-content-page-for-your-tab"></a>创建选项卡的内容页

内容页面是在团队客户端中呈现的网页。 通常情况下，它们是以下部分：

* 个人作用域的自定义选项卡-在此实例中，内容页面是用户遇到的第一页。
* 通道/组自定义选项卡-用户固定并在适当的上下文中配置选项卡后，将显示内容页。
* [任务模块](~/task-modules-and-cards/what-are-task-modules.md)-您可以创建内容页并将其作为 web 视图嵌入任务模块中。 页面将在模式弹出窗口中呈现。

本文特定于将内容页用作选项卡;但是，无论内容页面是如何呈现给最终用户的，此处的大部分指南都适用。

## <a name="tab-content-and-style-guidelines"></a>选项卡内容和样式准则

您的选项卡的总体目标应是提供对具有实际价值和明显用途的有意义和吸引人的内容的访问。 这并不意味着您应放弃令人满意的样式，但您应通过使您的选项卡设计整洁、导航直观和内容沉浸在最大限度地减少杂乱的注意力。 使用选项卡和[Microsoft 团队应用程序审批过程指南](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)查看[内容和对话](~/tabs/design/tabs.md)

## <a name="integrate-your-code-with-teams"></a>将您的代码与团队集成

若要在团队中显示您的页面，您必须包含 [Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latestadd &preserve-view=true) ，并在 `microsoftTeams.initialize()` 页面加载后包含一个调用。 这就是页面和团队客户端的通信方式：

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
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

## <a name="accessing-additional-content"></a>访问其他内容

### <a name="using-the-sdk-to-interact-with-teams"></a>使用 SDK 与团队进行交互

[团队客户端 JAVASCRIPT SDK](~/tabs/how-to/using-teams-client-sdk.md)提供了许多其他功能，在开发内容页时可能会非常有用。

### <a name="deep-links"></a>深度链接

您可以创建指向团队中的实体的深层链接。 通常，这些用于创建导航到您的选项卡中的内容和信息的链接。请参阅 [创建指向 Microsoft 团队中的内容和功能的深层链接](~/concepts/build-and-test/deep-links.md)。

### <a name="task-modules"></a>任务模块

任务模块是可以从选项卡触发的模式弹出窗口的体验。通常在内容页中，您不希望通过多个页面导航您的用户。 相反，您将使用任务模块显示用于收集其他信息的表单，并显示列表中项目的详细信息，或任何其他需要向用户提供其他信息的时间。 任务模块本身可以是其他内容页，也可以完全使用自适应卡片创建。 有关完整信息，请参阅 [在选项卡中使用任务模块](~/task-modules-and-cards/task-modules/task-modules-tabs.md) 。

### <a name="valid-domains"></a>有效的域

确保您的选项卡中使用的所有 URL 域都包含在 `validDomains` [清单](~/concepts/build-and-test/apps-package.md)中的阵列中。 有关详细信息，请参阅清单架构参考中的 [validDomains](~/resources/schema/manifest-schema.md#validdomains) 。 但是，请注意，您的选项卡的核心功能在团队中，而不是在团队外部。

## <a name="show-a-native-loading-indicator"></a>显示本机加载指示器

从 [清单架构](../../../resources/schema/manifest-schema.md)v1.1，您可以在团队中加载 web 内容的任何位置提供 [本机加载指示器](../../../resources/schema/manifest-schema.md#showloadingindicator) ，例如， [选项卡内容页](#integrate-your-code-with-teams)、 [配置页](configuration-page.md)、 [删除页](removal-page.md) 和 [选项卡中的任务模块](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)。

> [!NOTE]
> 1. 本地加载指示器在移动设备上尚不受支持。
> 2. 如果  `"showLoadingIndicator : true`  在应用程序清单中指明，则所有选项卡配置、内容和删除页以及所有基于 iframe 的任务模块必须遵循以下强制协议：


1. 若要显示加载指示器，请将添加 `"showLoadingIndicator": true` 到你的清单中。 
2. 请记住调用 `microsoftTeams.initialize();` 。
3. **可选**。 如果您已准备好打印到屏幕，并希望延迟加载应用程序内容的其余部分，则可以通过调用来手动隐藏加载指示器 `microsoftTeams.appInitialization.notifyAppLoaded();`
4. **强制性**。 最后，调用 `microsoftTeams.appInitialization.notifySuccess()` 以通知团队您的应用程序已成功加载。 如果适用，团队将隐藏加载指示器。 如果  `notifySuccess`  在30秒内未调用，则系统将假定您的应用程序超时，并将出现一个带有重试选项的错误屏幕。
5. 如果您的应用程序无法加载，则可以通过调用 `microsoftTeams.appInitialization.notifyFailure(reason);` 来让团队知道出现了错误。 随后将向用户显示一个错误屏幕：

```typescript
``
/* List of failure reasons */
export const enum FailedReason {
    AuthFailed = "AuthFailed",
    Timeout = "Timeout",
    Other = "Other"
}
```
>
