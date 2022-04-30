---
title: 应用设计过程
author: heath-hamilton
description: 大致了解如何以及何时可以使用 Microsoft 工具和资源设计出有效的 Microsoft Teams 应用。
ms.localizationpriority: high
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: b59c2c09240478899ff66e6554719f0f46bc791c
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111267"
---
# <a name="design-process-for-microsoft-teams-apps"></a>Microsoft Teams 应用的设计过程

有多个工具和资源用于设计 Microsoft Teams 应用。 以下步骤介绍在设计过程中何时以及如何使用这些内容。 （某些步骤可能在技术上超出了设计过程，但包含在其他上下文中。）

:::image type="content" source="~/assets/images/design-guidelines/teams-app-design-process.png" alt-text="显示 Teams 应用设计过程示例的示意图。" border="false":::

## <a name="plan-your-app"></a>计划应用

设计高质量的 Teams 应用需要了解你希望应用执行的操作以及你认为用户会如何使用它。 但是，在开始设计之前，请回答以下问题：

* 你的用户是谁？
* 他们有什么问题？
* 你的应用如何解决他们的问题？
* 应用的使用频率是多少？
* 有多少人会使用你的应用？
* 你的应用可以提供什么样的投资回报？

有关详细信息，请参阅 [ 了解应用的用例 ](~/concepts/design/understand-use-cases.md)，并将 [ 用例映射到 Teams ](~/concepts/design/map-use-cases.md)。

## <a name="get-teams-design-tools"></a>获取 Teams 设计工具

Microsoft 提供了一些工具用来简化 Teams 应用的设计。 强烈建议至少使用 Microsoft Teams UI 工具包。

### <a name="get-the-microsoft-teams-ui-kit"></a>获取 Microsoft Teams UI 工具包

Microsoft Teams UI 工具包可以帮助在最短的时间内开发出有效的 Teams 应用。 UI 工具包包含你在这些文档中看到的与 Teams 应用设计相关的所有内容，包括大量的示例和变体。

UI 工具包还具有可以根据需要复制和修改的预建模板和组件，因此你可以花更多的时间来设计最佳用户体验，而不必担心按钮的外观。

> [!TIP]
> **UI 工具包是否适合我？** 如果你参与创建 Teams 应用，是的，适合。 了解如何制作 Teams 应用不仅对设计者有帮助，而且对产品经理、使用 IDE 的开发人员以及使用低代码工具（如 Microsoft Power Platform）的开发者也有帮助。

1. 转到 [ Microsoft Teams UI 工具包 Figma 页面 ](https://www.figma.com/community/file/916836509871353159)。
1. 选择“**重复**”，打开 UI 工具包。 （可能需要先创建 Figma 帐户。）

### <a name="try-the-sample-app"></a>试用示例应用

可以上传示例应用，了解应用在 Teams 客户端中的外观和行为。

> [!div class="nextstepaction"]
> [ 获取示例应用 (GitHub) ](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="learn-teams-design-system"></a>了解 Teams 设计系统

深入了解或至少熟悉 [ Teams 应用设计的基础知识 ](design-teams-app-fundamentals.md)，包括布局、配色方案等。

## <a name="choose-app-capabilities"></a>选择应用功能

在规划阶段之后，可以确定哪些 Teams 功能适合应用的用例。 例如，如果要主动通知用户，机器人可能是合适的功能。

UI 工具包具有预建的设计，展示用户通常如何添加、设置、使用和管理每个功能。 作为快速参考，此信息也在这些文档中，但使用 UI 工具包，可以将这些设计中的任何一种复制并粘贴到应用的设计中。

1. 在 UI 工具包的左侧导航栏中，转到“**应用功能**”并选择所需的应用功能。
1. 从该页面复制所需的内容来设计应用。<br />
   例如，如果应用支持使用单一登录进行身份验证，请复制并粘贴设计来处理这种情况。

## <a name="design-your-ux-flow"></a>设计 UX 流程

有了基本的应用设计后，可以通过从 UI 工具包复制 Teams UI 模板和基本组件来根据需要进行修改和优化。

### <a name="design-with-ui-templates"></a>使用 UI 模板进行设计

UI 模板是复杂的高保真设计，适用于常见的 Teams 用例和工作流。 建议使用这些模板来简化和加快设计过程，而不是从基本组件开始。

1. 在 UI 工具包的左侧导航栏中，转到“**UI 模板**”。
1. 复制对应用设计有意义的模板。<br />
   例如，如果要设计一款个人应用，可能需要使用“仪表板”模板。

### <a name="design-with-basic-ui-components"></a>使用基本 UI 组件进行设计

根据 Fluent UI，这些是创建熟悉的 Teams 界面的核心元素。 如果 UI 模板缺少所需的内容或只想从头开始设计应用，请使用这些组件。

1. 在 UI 工具包的左侧导航栏中，转到“**基本 UI 组件**”。
1. 复制应用设计所需的组件（例如按钮或开关）。

## <a name="implement-your-design"></a>实施设计

设计完成后，即可开始构建。 以下工具可以帮助简化应用的前端开发。

### <a name="build-with-ui-templates"></a>使用 UI 模板进行构建

如果在设计中使用了 UI 模板，则可以使用 Microsoft Teams UI 库来实现这些模板（基于 Fluent UI 的 React 组件库）。

目前，并非 UI 工具包中列出的所有模板都可以在库中使用。

> [!div class="nextstepaction"]
> [ 获取库 (GitHub) ](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="build-with-basic-ui-components"></a>使用基本 UI 组件进行构建

与设计阶段不同，如果 UI 模板缺少所需的内容，或者只想从头开始构建应用，则可以在应用项目中使用这些 Fluent UI 组件。 

（注意：如果发现缺少某些内容或对模板有想法，请考虑参与 Teams UI 库存储库。）

> [!div class="nextstepaction"]
> [ 获取库 (Fluent UI) ](https://fluentsite.z22.web.core.windows.net/)

## <a name="review-design-resources"></a>查看设计资源

无论是刚开始使用应用还是已经接近生产就绪的应用，建议定期查看以下资源：

* **Microsoft Teams 应用商店验证准则**：提供所有 Teams 应用应努力制定的标准，而不仅仅是应用商店中列出的应用。 有关详细信息，请参阅 [ 指南 ](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)。
* **设计最佳做法**：这些文档和 UI 工具包提供了设计高质量应用的最佳做法。 例如，请参阅 [ 设计机器人的最佳做法 ](~/bots/design/bots.md#best-practices)。

## <a name="see-also"></a>另请参阅

[ 设计活动源通知 ](~/concepts/design/activity-feed-notifications.md)
