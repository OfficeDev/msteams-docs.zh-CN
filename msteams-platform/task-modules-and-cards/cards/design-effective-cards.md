---
title: 为你的应用程序设计自适应卡片
description: 了解如何为团队设计自适应卡片和获取 Microsoft 团队 UI 工具包。
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: bd48846284620415cc8cadabc59f2ab7b61d5189
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604505"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>为 Microsoft 团队应用程序设计自适应卡片

自适应卡片包含卡片元素的任意多边形和可选的一组操作。 自适应卡片是可通过 bot 或邮件扩展添加到对话中的可操作内容片段。 通过使用文本、图形和按钮，这些卡片可为你的受众提供丰富的通信。

自适应卡片框架跨许多 Microsoft 产品（包括团队）使用。 您可以通过 bot 或邮件分机向用户发送邮件内部的卡片。 如果有，用户可以对卡片采取操作。

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="示例显示了一个自适应卡片。" border="false":::

## <a name="microsoft-teams-ui-kit"></a>Microsoft 团队 UI 工具包

您可以在 Microsoft 团队 UI 工具包中找到有关团队中的自适应卡片的更全面的设计指南，包括可以在需要时获取和修改的元素。 UI 工具包还介绍了一些基本主题，如主题、辅助功能和响应大小调整。

> [!div class="nextstepaction"]
> [ (Figma) 获取 Microsoft 团队 UI 工具包 ](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>自适应卡片设计器

此外，还可以在浏览器中直接开始设计自适应卡片。

> [!div class="nextstepaction"]
> [尝试自适应卡片设计器](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>自适应卡片的类型

### <a name="hero"></a>主图

我们最大的卡片。 用于共享在其中显示大部分文章的文章或场景。

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="thumbnail"></a>缩略图

用于发送简单的可操作邮件。

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="list"></a>列表

在希望用户从列表中选取项目的情况下使用，但这些项目不需要很多说明。

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="digest"></a>Digest

用于新闻摘要和向上舍入文章。 注意：我们建议单个更新或新闻项目的缩略图卡。

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="media"></a>媒体

当您想要组合文本和媒体（如音频或视频）时使用。

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="people"></a>人员

最适用于有效传达任务所涉及的人员的情况。

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="request-ticket"></a>请求票证

用于获取来自用户的快速输入，以自动创建任务或票证。

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="imageset"></a>ImageSet

使用发送多个图像缩略图。

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="actionset"></a>ActionSet

在您希望用户选择按钮时使用，然后从同一卡片收集添加用户输入。

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

### <a name="choiceset"></a>ChoiceSet

使用收集用户的多个输入。

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="示例显示了一个自适应卡片。" border="false":::

## <a name="anatomy"></a>解析

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="显示自适应卡片的 UI 剖析的图示。" border="false":::

自适应卡片具有很大的灵活性。 但至少我们建议在每个卡片中包括以下组件：

|计数器|描述|
|----------|-----------|
|A|**标头**：使标头清晰明了，但却是描述性的。|
|B|**正文副本**：用于传递的详细信息太长或不够重要，无法包含在标头中。|
|C|**主要操作**：最佳实践包括1-3 主要操作。 最多允许6个。|

## <a name="best-practices"></a>最佳做法

### <a name="primary-and-secondary-actions"></a>主要操作和次要操作

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="显示自适应卡片最佳实践的示例。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>操作：使用最大6个主要操作

自适应卡可支持六个主要操作，而大多数卡片不需要。 操作应清晰、简明且直接向前。 越少越好。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="显示自适应卡片最佳实践的示例。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>请勿：使用6个以上的主要操作

自适应卡片应提供快速的可操作内容。 操作过多可能会严重影响用户。

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>频率

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="显示自适应卡片最佳实践的示例。" border="false":::

#### <a name="do-be-concise"></a>Do：简单明了

可以轻松地将多个卡片发送到对话中，但一旦卡片从视图中滚出，它们就会变得不太有用。 尝试将自己限制为重点。 在用户对其感觉为 "干扰" 的程度较差的频道中，尤其如此。
