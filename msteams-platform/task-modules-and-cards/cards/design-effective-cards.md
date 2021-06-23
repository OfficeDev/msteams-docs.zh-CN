---
title: 为你的应用设计自适应卡
description: 了解如何设计 Microsoft Teams 自适应卡并获取 Microsoft Teams UI Kit。
localization_priority: Priority
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8e56928da44e22006feb59715c8bdbf821ec4c42
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037654"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>为 Microsoft Teams 应用设计自适应卡

自适应卡片包含卡片元素的自由格式正文和一系列可选操作。 自适应卡片是可操作的内容片段，可通过机器人或消息传递扩展添加到对话。 这些卡片使用文本、图形和按钮为受众提供丰富的通信体验。

自适应卡框架用于许多 Microsoft 产品，包括 Microsoft Teams。 可以通过机器人或消息传递扩展向用户发送消息内的卡片。 用户还可以在卡片上执行操作（如果存在）。

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="自适应卡概述示例。" border="false":::

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

可在 Microsoft Teams UI Kit 中查看更全面的 Microsoft Teams 自适应卡设计指南，包括可根据需要获取和修改的元素。 UI 配套伯还涵盖主题、辅助功能和响应式大小等重要主题。

> [!div class="nextstepaction"]
> [获取 Microsoft Teams UI Kit（用户）](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>自适应卡设计器

还可以直接在浏览器中开始设计自适应卡。

> [!div class="nextstepaction"]
> [适用自适应卡设计器](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>自适应卡类型

### <a name="hero"></a>主图

我们最大的卡片。 用于共享文章或应用场景，用一张图像讲述故事主体。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="示例：自适应卡主图卡。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="示例：移动设备上的自适应卡主图卡。" border="false":::

---

### <a name="thumbnail"></a>缩略图

用于发送简单的可操作消息。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="示例：自适应卡缩略图卡。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="示例：移动设备上的自适应卡缩略图卡。" border="false":::

---

### <a name="list"></a>列表

当你希望用户从列表中选中一项，但项不需要大量解释时使用。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="示例：自适应卡列表卡。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="示例：移动设备上的自适应卡列表卡。" border="false":::

---
Use for news digests and round-up posts. Note: We recommend the thumbnail card for a single update or news item.
':::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Example shows an Adaptive Card digest card." border="false"::': null
':::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="Example shows an Adaptive Card digest card on mobile." border="false"::': null
---

### <a name="media"></a>媒体

在想要结合文本和媒体（如音频或视频）时使用。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="示例：自适应卡媒体卡。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="示例：移动设备上的自适应卡媒体卡。" border="false":::

---

### <a name="people"></a>人员

最适合用于有效传达任务相关人员。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="示例：自适应卡人员卡。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="示例：移动设备上的自适应卡人员卡。" border="false":::

---

### <a name="request-ticket"></a>请求票证

用于从用户获取快速输入以自动创建任务或票证。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="示例：自适应卡请求票证卡。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="示例：移动设备上的自适应卡请求票证卡。" border="false":::

---

### <a name="image-set"></a>图像集

用于发送多个图像缩略图。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="示例：自适应卡图像集卡。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="示例：移动设备上的自适应卡图像集卡。" border="false":::

---

### <a name="action-set"></a>操作集

当希望用户选择按钮，然后从同一张卡中收集添加用户输入时使用。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="示例：自适应卡操作集卡。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="示例：移动设备上的自适应卡操作集卡。" border="false":::

---

### <a name="choice-set"></a>选择集

用于从一个用户收集多个输入。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="示例：自适应卡选择集卡。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="示例：移动设备上的自适应卡选择集卡。" border="false":::

---

## <a name="anatomy"></a>解剖

自适应卡片具有极强的灵活性。 但作为最低要求，我们强烈建议在每张卡片中包含以下组件。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="示例：自适应卡片解剖。" border="false":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="示例：移动设备上的自适应卡片解剖。" border="false":::

---

|计数器|说明|
|----------|-----------|
|A|**标题**：让标题清晰简洁。|
|B|**正文文案**：传达过长或不够重要，不足以放在标题中的内容。|
|C|**主要操作**：作为最佳做法，包括 1-3 个主要操作。 可最多有 6 个。|

## <a name="best-practices"></a>最佳实践

使用上述建议打造优质应用体验。

### <a name="primary-and-secondary-actions"></a>主要和次要操作

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="有关如何在自适应卡上仅包含一小组操作的最佳实践。" border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>建议：最多使用六个主要操作

虽然自适应卡可以支持六个主要操作，但大多数卡并不需要这么多。 操作应做到清晰、简洁且直接。 操作越少，效率越高。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="有关如何避免在自适应卡上添加过多操作，而让用户感到不知所措的最佳实践。" border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>不建议：使用超过六个主要操作

自适应卡应提供快速、可操作的内容。 操作过多可能会使用户不知所措。

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>频率

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="有关自适应卡频率的最佳实践。" border="false":::

#### <a name="do-be-concise"></a>建议：做到简洁

将多个卡片发送到对话很容易，但一旦卡片滚动出视图，就会变得没那么有用。 尝试限制自己只传达必要内容。 在用户对自己认为是“干扰”的内容，容忍度更低的频道中尤其应注意这一点。
