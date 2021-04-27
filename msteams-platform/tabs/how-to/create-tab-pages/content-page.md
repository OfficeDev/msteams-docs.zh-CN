---
title: 创建内容页
author: laujan
description: 如何创建内容页
keywords: teams 选项卡组通道可配置静态
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 9dc6c73d877d9355c5d4a9653e0d8ed669fb347e
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020378"
---
# <a name="create-a-content-page-for-your-tab"></a>为选项卡创建内容页

内容页是在 Teams 客户端中呈现的网页。 通常，这些是以下部分：

* 个人范围的自定义选项卡 - 在此实例中，内容页是用户遇到的第一个页面。
* 频道/组自定义选项卡 - 在用户固定并配置相应上下文中的选项卡后，将显示内容页。
* 任务 [模块](~/task-modules-and-cards/what-are-task-modules.md) - 可以创建内容页并将其作为 Web 视图嵌入任务模块中。 页面将在模式弹出窗口内呈现。

本文专门介绍将内容页用作选项卡;但是，无论内容页如何呈现给最终用户，此处的大部分指南都适用。

## <a name="tab-content-and-style-guidelines"></a>选项卡内容和样式指南

您的选项卡的总体目标应该是提供对具有实用价值且明确用途的有意义且吸引人的内容的访问。 这并不意味着你应该放弃一种令人愉悦的样式，但应专注于通过使选项卡设计干净、导航直观和内容沉浸式来最大程度地减少混乱。 请参阅 [内容和对话，全部使用](~/tabs/design/tabs.md) 选项卡和 Microsoft [Teams 应用审批流程指南](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)

## <a name="integrate-your-code-with-teams"></a>将代码与 Teams 集成

若要在 Teams 中显示页面，必须包含 [Microsoft Teams JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) 客户端 SDK，并包括加载页面 `microsoftTeams.initialize()` 后对 的调用。 这就是页面和 Teams 客户端进行通信的方式：

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

### <a name="using-the-sdk-to-interact-with-teams"></a>使用 SDK 与 Teams 交互

[Teams 客户端 JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md)提供了许多其他功能，你可能会发现在开发内容页时很有用。

### <a name="deep-links"></a>深度链接

可以在 Teams 中创建指向实体的深层链接。 通常，它们用于创建导航到选项卡中的内容和信息的链接。请参阅 [在 Microsoft Teams 中创建内容和功能的深层链接](~/concepts/build-and-test/deep-links.md)。

### <a name="task-modules"></a>任务模块

任务模块是一种模式弹出式体验，可以从选项卡触发。通常，在内容页中，您不希望在多个页面中导航用户。 相反，您将使用任务模块来显示表单，以收集其他信息、显示列表中某个项目的详细信息，或在需要向用户显示其他信息时显示任何其他时间。 任务模块本身可以是其他内容页，或者完全使用自适应卡片创建。 有关 [完整信息，请参阅在选项卡中](~/task-modules-and-cards/task-modules/task-modules-tabs.md) 使用任务模块。

### <a name="valid-domains"></a>有效域

确保选项卡中使用的所有 URL 域都包含在清单 `validDomains` 的数组 [中](~/concepts/build-and-test/apps-package.md)。 有关详细信息，请参阅清单架构参考中的[validDomains。](~/resources/schema/manifest-schema.md#validdomains) 但是，请注意，选项卡的核心功能存在于 Teams 中，而不是 Teams 之外。

## <a name="reorder-static-personal-tabs"></a>对静态个人选项卡重新排序

从清单版本 1.7 开始，开发人员可以重新排列其个人应用的所有选项卡。 特别是，开发人员可以移动自动程序聊天选项卡，该选项卡始终默认位于个人应用选项卡标题中的任意位置。 我们已声明两个保留选项卡 entityId 关键字、*对话和**关于*。

如果你创建具有个人范围的自动程序，它将默认显示在个人应用的第一个选项卡位置。 如果你希望将其移动到另一个位置，则必须使用保留的关键字对话 将静态选项卡对象添加到 *清单* 中。 对话 *选项卡* 显示在 Web 或桌面上，根据你在数组中添加对话选项卡 `staticTabs` 的什么位置。 

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

## <a name="show-a-native-loading-indicator"></a>显示本机加载指示器

从[清单架构 v1.7](../../../resources/schema/manifest-schema.md)开始，可以在[](../../../resources/schema/manifest-schema.md#showloadingindicator)Teams 中加载 Web 内容（例如选项卡内容页、配置页、删除页和选项卡中[](configuration-page.md)的任务模块）[](removal-page.md)提供本机加载[指示器](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)。 [](#integrate-your-code-with-teams)

> [!NOTE]
> 1. 无法通过此清单属性配置移动客户端上的行为。 默认情况下，移动客户端在内容页和基于 iframe 的任务模块中显示本机加载指示器。 当提出提取内容的请求时，会显示移动设备上的此指示器，请求完成后立即消除。
> 2. 如果你在应用清单中指示，则所有选项卡配置、内容和删除页面以及所有基于 iframe 的任务模块必须遵循以下  `"showLoadingIndicator : true`  强制协议：


1. 若要显示加载指示器，请 `"showLoadingIndicator": true` 添加到清单中。 
2. 请记住调用 `microsoftTeams.initialize();` 。
3. **可选。** 如果已准备好打印到屏幕，并且希望延迟加载应用程序内容的其余部分，可以通过调用 手动隐藏加载指示器 `microsoftTeams.appInitialization.notifyAppLoaded();`
4. **强制 。** 最后， `microsoftTeams.appInitialization.notifySuccess()` 致电通知 Teams 你的应用已成功加载。 团队随后将隐藏加载指示器（如果适用）。 如果未在 30 秒钟内调用，则假定你的应用已退出，并且将显示一个显示重试选项  `notifySuccess`  的错误屏幕。
5. 如果你的应用程序无法加载，你可以致电让 `microsoftTeams.appInitialization.notifyFailure(reason);` Teams 知道出现错误。 然后，会向用户显示一个错误屏幕：

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
