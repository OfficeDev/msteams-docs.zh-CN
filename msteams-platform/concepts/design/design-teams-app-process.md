---
title: 应用设计过程
author: heath-hamilton
description: 了解如何使用 Microsoft 工具和资源设计有效的应用，以及Microsoft Teams概念。
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 225859da18cb50741ab49c68d89bc318c6c9034c
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994208"
---
# <a name="design-process-for-microsoft-teams-apps"></a>应用程序的设计Microsoft Teams过程

有多种工具和资源可用于设计Microsoft Teams应用。 以下步骤介绍了在设计过程中可能何时以及如何使用这些元素。  (一些步骤可能在设计过程之外，但包含在其他上下文中。) 

:::image type="content" source="~/assets/images/design-guidelines/teams-app-design-process.png" alt-text="显示应用设计Teams示例的关系图。" border="false":::

## <a name="plan-your-app"></a>规划应用

设计高质量的Teams需要了解希望应用执行哪些操作，以及你认为用户会如何使用它。 但在开始设计之前，请回答以下问题：

* 你的用户是谁？
* 他们有什么问题？
* 你的应用如何解决他们的问题？
* 你的应用将多久使用一次？
* 有多少人将使用你的应用？
* 你的应用可以提供哪种类型的投资回报？

有关详细信息，请参阅[了解应用的用例，以及](~/concepts/design/understand-use-cases.md)将用例映射到[Teams。](~/concepts/design/map-use-cases.md)

## <a name="get-teams-design-tools"></a>获取Teams设计工具

Microsoft 提供了工具，可更轻松地设计Teams应用。 我们强烈建议至少使用 Microsoft Teams UI 工具包。

### <a name="get-the-microsoft-teams-ui-kit"></a>获取 Microsoft Teams UI 工具包

Microsoft Teams UI 工具包可以帮助你在最短时间内Teams开发有效的应用。 UI 工具包包含你在这些与应用设计相关的文档Teams，包括大量示例和变体。

UI 工具包还具有预建的模板和组件，你可以根据需要复制和修改这些模板和组件，以便你可以花费更多时间来设计最佳用户体验，而不是担心按钮的外观。

> [!TIP]
> **UI 工具包是否适合我？** 如果你对创建应用有Teams，可以。 了解如何制作 Teams 应用不仅对设计人员、产品经理、使用 ID 的开发人员以及使用低代码工具（如 Microsoft Power Platform) ）构建的 (也很有帮助。

1. 转到["Microsoft Teams UI 工具包""图块"页面](https://www.figma.com/community/file/916836509871353159)。
1. 选择 **"复制** "以打开 UI 工具包。  (可能需要先创建一个图块帐户。) 

### <a name="try-the-sample-app"></a>试用示例应用

你可以上载示例应用，以查看应用在客户端中的外观Teams行为。

> [!div class="nextstepaction"]
> [获取示例应用 (GitHub) ](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="learn-teams-design-system"></a>了解Teams设计系统

深入了解或至少熟悉应用设计[Teams，](design-teams-app-fundamentals.md)包括布局、配色方案等。

## <a name="choose-app-capabilities"></a>选择应用功能

在规划阶段后，你可以确定哪些Teams适合应用的用例。 例如，如果你想要主动通知用户，则自动程序可能是正确的功能。

UI 工具包预先构建了设计，可展示用户通常如何添加、设置、使用和管理每个功能。 为了快速参考，此信息也位于这些文档内，但借助 UI 工具包，你可以将其中任何设计复制并粘贴到应用设计中。

1. 在 UI 工具包的左侧导航中，转到应用 **功能** ，然后选择你需要的应用功能。
1. 从该页面复制所需的内容以设计应用。<br />
   例如，如果你的应用支持使用单一登录进行身份验证，请复制并粘贴用于处理该确切方案的设计。

## <a name="design-your-ux-flow"></a>设计用户体验流

拥有基本应用设计后，你可以根据需要修改和优化它，Teams UI 模板和基本组件。

### <a name="design-with-ui-templates"></a>使用 UI 模板进行设计

UI 模板是复杂的高保真设计，适用于Teams用例和工作流。 我们建议您使用这些模板来简化和加快设计过程，而不是从底部开始使用基本组件。

1. 在 UI 工具包的左侧导航中，转到 **"UI 模板"。**
1. 复制对你的应用设计有意义的模板。<br />
   例如，如果你正在设计个人应用，你可能想要使用仪表板模板。

### <a name="design-with-basic-ui-components"></a>使用基本 UI 组件进行设计

根据Fluent UI，这些是用于创建熟悉的用户界面Teams元素。 如果 UI 模板缺少你需要的内容，或者你只想从头开始设计应用，请使用这些组件。

1. 在 UI 工具包的左侧导航中，转到 **基本 UI 组件**。
1. 复制应用设计方案所需的组件 (例如按钮或切换) 。

## <a name="implement-your-design"></a>实现你的设计

设计已完成，你已准备好开始构建。 以下工具有助于简化应用的前端开发。

### <a name="build-with-ui-templates"></a>使用 UI 模板生成

如果在设计中使用了 UI 模板，可以使用 Microsoft Teams UI 库 (一个 React 组件库来实现这些模板，Fluent UI) 。

目前，并非 UI 工具包中列出的所有模板在库中都可用。

> [!div class="nextstepaction"]
> [获取库 (GitHub) ](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="build-with-basic-ui-components"></a>使用基本 UI 组件生成

与设计阶段不同，如果 UI 模板缺少你所需的内容，或者你只想从头开始构建应用，你可以在你的应用项目中Fluent UI 组件。 

 (注意：如果你注意到缺少某些内容或对模板有一些想法，请考虑为Teams UI 库存储库) 

> [!div class="nextstepaction"]
> [获取 UI (Fluent库) ](https://fluentsite.z22.web.core.windows.net/)

## <a name="review-design-resources"></a>查看设计资源

无论你是刚开始使用应用还是接近生产就绪型应用，我们建议你定期查看以下资源：

* **Microsoft Teams：** 提供所有应用都应Teams的标准，而不只是应用商店中列出的应用。 有关详细信息，请参阅 [指南](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)。
* **设计最佳做法**：这些文档和 UI 工具包提供了设计高质量应用的最佳方案。 例如，请参阅 [设计机器人的最佳实践](~/bots/design/bots.md#best-practices)。

