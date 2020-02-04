---
title: 创建内容页
author: laujan
description: ''
keywords: 团队选项卡组频道配置静态
ms.topic: conceptual
ms.author: v-laujan
ms.openlocfilehash: ac85e000c9bdaebf28cb33143a7c82a348d3771e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673246"
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

若要在团队中显示您的页面，您必须包含[Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) ，并在`microsoftTeams.initialize()`页面加载后包含一个调用。 这就是页面和团队客户端的通信方式：

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

[团队客户端 JAVASCRIPT SDK](~/tabs/how-to/using-teams-client-sdk.md)提供了许多其他功能，在开发人员的内容页时，您可能会发现有用的功能。

### <a name="deep-links"></a>Deep links

您可以创建指向团队中的实体的深层链接。 通常，这些用于创建导航到您的选项卡中的内容和信息的链接。请参阅[创建指向 Microsoft 团队中的内容和功能的深层链接](~/concepts/build-and-test/deep-links.md)。

### <a name="task-modules"></a>任务模块

任务模块是可以从选项卡触发的模式弹出窗口的体验。通常在内容页中，您不希望通过多个页面导航您的用户。 相反，您将使用任务模块显示用于收集其他信息的表单，并显示列表中项目的详细信息，或任何其他需要向用户提供其他信息的时间。 任务模块本身可以是其他内容页，也可以完全使用自适应卡片创建。 有关完整信息，请参阅[在选项卡中使用任务模块](~/task-modules-and-cards/task-modules/task-modules-tabs.md)。

### <a name="valid-domains"></a>有效的域

确保您的选项卡中使用的所有 URL 域都包含在`validDomains` [清单](~/concepts/build-and-test/apps-package.md)中的阵列中。 有关详细信息，请参阅清单架构参考中的[validDomains](~/resources/schema/manifest-schema.md#validdomains) 。 但是，请注意，您的选项卡的核心功能在团队中，而不是在团队外部。
