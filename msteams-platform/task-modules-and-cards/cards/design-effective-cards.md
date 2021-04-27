---
title: 为应用设计自适应卡片
description: 了解如何为 Teams 设计自适应卡片并获取 Microsoft Teams UI 工具包。
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 67a2882a0a687d5ccb48759419ecefcdf9396fc3
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020280"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>为 Microsoft Teams 应用设计自适应卡片

自适应卡片包含卡片元素和可选操作集的免费格式正文。 自适应卡片是内容可操作的代码段，可以通过机器人或消息传递扩展添加到对话中。 这些卡片使用文本、图形和按钮，向受众提供丰富的通信。

自适应卡片框架适用于许多 Microsoft 产品，包括 Teams。 可以通过机器人或消息扩展向用户发送内部邮件卡片。 存在此情况时，用户可以对卡片采取操作。

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="示例显示自适应卡片。" border="false":::

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

可以在 Microsoft Teams UI 工具包中查找有关 Teams 中自适应卡片的更全面的设计指南，包括可根据需要获取和修改的元素。 UI 工具包还涵盖了主题设置、辅助功能和响应式大小调整等重要主题。

> [!div class="nextstepaction"]
> [获取 Microsoft Teams UI Kit （用户）](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>自适应卡片设计器

还可以直接在浏览器中开始设计自适应卡片。

> [!div class="nextstepaction"]
> [试用自适应卡片设计器](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>自适应卡片的类型

### <a name="hero"></a>主图

我们最大的卡片。 用于共享文章或场景，其中图像可以描述大部分情景。

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="示例显示自适应卡片。" border="false":::

### <a name="thumbnail"></a>缩略图

用于发送简单的可操作邮件。

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="自适应卡片的示例。" border="false":::

### <a name="list"></a>列表

在您希望用户从列表中选取项目，但项目不需要太多解释的情况下使用。

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="自适应卡片示例。" border="false":::

### <a name="digest"></a>Digest

用于新闻摘要和向上舍入帖子。 注意：我们建议使用单个更新或新闻项的缩略图卡片。

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="插图显示自适应卡片。" border="false":::

### <a name="media"></a>媒体

在你想要组合文本和媒体（如音频或视频）时使用。

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="插图显示自适应卡片。" border="false":::

### <a name="people"></a>人员

最适用于有效传达任务涉及人员。

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="自适应卡片的图示。" border="false":::

### <a name="request-ticket"></a>请求票证

用于从用户处获取快速输入，以自动创建任务或票证。

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="自适应卡片的图示。" border="false":::

### <a name="imageset"></a>ImageSet

用于发送多个图像缩略图。

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="自适应卡片示例。" border="false":::

### <a name="actionset"></a>ActionSet

当你希望用户选择一个按钮，然后从同一卡片收集添加的用户输入时，使用 。

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="示例显示自适应卡片。" border="false":::

### <a name="choiceset"></a>ChoiceSet

用于收集用户的多个输入。

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="示例显示自适应卡片。" border="false":::

## <a name="anatomy"></a>解剖

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="显示自适应卡片的 UI 分析的图示。" border="false":::

自适应卡片具有很多灵活性。 但是，我们强烈建议至少将以下组件包括在每张卡片中：

|计数器|说明|
|----------|-----------|
|A|**标头**：使标题简洁明了，但具有描述性。|
|B|**正文** 副本：用于传达太长或不够重要以包括在标头中的详细信息。|
|C|**主要操作**：最佳做法包括 1-3 个主要操作。 最多允许六个。|

## <a name="best-practices"></a>最佳做法

### <a name="primary-and-secondary-actions"></a>主要操作和辅助操作

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="显示自适应卡片最佳实践的示例。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>操作：最多使用六个主要操作

自适应卡片可以支持六个主要操作，但大多数卡片不需要这一点。 操作应简洁明了。 "少"表示"更多"。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="示例展示了自适应卡片最佳实践。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>请勿：使用超过 6 个主要操作

自适应卡片应显示快速且可操作的内容。 操作太多可能会使用户感到不知所措。

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>频率

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="显示自适应卡片最佳实践的图示。" border="false":::

#### <a name="do-be-concise"></a>应做：简洁

向对话中发送多个卡片很容易，但在卡片滚动到视图外后，它们变得不太有用。 尝试将自己限制为基本功能。 在用户对"噪音"所感知的容忍度较低的频道中尤其如此。
