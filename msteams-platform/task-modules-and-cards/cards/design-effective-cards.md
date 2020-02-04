---
title: 设计有效的卡片
description: 介绍创建卡片的设计准则
keywords: 团队设计准则参考框架卡适应性轻型
ms.openlocfilehash: 33ee0b59a3a5a1490d6e2106f8532094ed852598
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673436"
---
# <a name="designing-effective-cards"></a>设计有效的卡片

卡片是可通过 bot、连接器或应用添加到对话中的可操作内容片段。 通过使用文本、图形和按钮，卡片可以与访问群体进行通信。

我们的卡片框架消除了设计全功能 UX 的负担。 我们开发了几种标准卡类型，每种类型都适合于受支持的平台。 这意味着完全负责布局，并且无需跨平台开发不同的卡迭代。 相反，你可以将精力集中在你的内容上拨。

---

## <a name="guidelines"></a>准则

可将卡片视为对用户问题或设置的响应。 卡片可以响应直接问题（例如，"我有多少个打开的 bug？"）或一个条件（如 "每日上午9点发送我打开的 bug 的列表"）。

> [!TIP]
> 使用我们的标准卡类型之一意味着你将了解所有响应将在每个受支持的平台上进行良好呈现。

卡片可以包含以下任何元素：<br />

[!include[Card anatomy](~/includes/design/card-image-anatomy.html)]

1. **信封文本**：最适用于聊天消息。 例如，如果你想让 bot 说： "我找到了我找到的内容了！" 或 "用于您的1:00 新闻摘要的时间"，该邮件最好显示在信封文本中。

   信封文本是一种很好的方法来向服务中注入一些个性，只需记住保持相对简短。

2. **标题**：您的标题将始终为卡片中的最大文本。 它还充当 "挂钩"，因此请尽量缩短标题，使其易于浏览。

3. **副标题**：最适合用于特性、taglines 或辅助指令。 此组件显示在标题的正下方。

4. **图像**：图像根据其容器进行缩放。 这些英雄卡片的最大宽度为420px，缩略图的最大宽度为100px，列表视图仅允许在桌面模式下进行32。

5. **文本**：最适合用于卡片正文中的纯文本。 您的最大长度取决于所选的卡片类型。

6. **按钮**：最适合用于打开网页、选项卡或其他聊天内容。 确保将按钮文本保持简短和点。

   每个卡片最多可以包含6个按钮，但我们建议在此处 "更小的" 理念。

7. **点击区域**：这是卡片的可单击区域。 大多数用户都希望自动单击图像，因此请尝试并手工创建文本，以便他们知道应该点击或单击的位置。

> [!TIP]
> 无需在您创建的每个卡片中包含每个元素。 让你的内容为你的元素做决定。

---

## <a name="types-of-cards"></a>卡片类型

### <a name="hero"></a>主图

我们最大的卡片。 最适合用于您的图像告诉大多数情景的文章、详细说明或场景。

[!include[Card anatomy](~/includes/design/card-image-hero.html)]

### <a name="thumbnail"></a>缩略图

简单明了。 这些卡片是简短答案的理想选择，或者，如果您希望一次返回几张卡片，以便用户可以从一组选项中进行选择。 我们认为，这是一个很好的深度链接到另一个选项卡或 web 服务的方法。

[!include[Card anatomy](~/includes/design/card-image-thumbnail.html)]

### <a name="sign-in"></a>登录

某些服务要求用户独立于我们的身份验证进行登录。 在这种情况下，您将在用户可以连接到您的服务之前提供一个登录卡。

[!include[Card anatomy](~/includes/design/card-image-signin.html)]

> [!TIP]
> 限制其他登录卡的出现次数，因为它们会给新用户带来明显的速度增加。

---

## <a name="card-collections"></a>卡片集合

当您希望一次显示多个内容或以快速连续显示多个内容时，我们还提供了最适合使用的标准卡片类型。 为此，我们提供了一个轮播、摘要、列表以及我们称之为 "气泡合并" 的内容。

### <a name="carousel"></a>旋转式传送

最适合用于文章、购物和通过卡片浏览。

[!include[Card anatomy](~/includes/design/card-image-carousel.html)]

> [!TIP]
> 轮播将成为最大卡片的最大高度。 我们建议在中使用相同的卡片类型和内容字段。

### <a name="digest"></a>Digest

最适合用于新闻、摘要以及您希望用户一次查看多张卡片的情况。 建议使用摘要的缩略图卡片。

[!include[Card anatomy](~/includes/design/card-image-digest.html)]

### <a name="lists"></a>列表

列表是在 "选择其中一个" 方案中呈现一组可浏览对象的绝佳方式。 最适用于不需要大量说明的项目的列表。

[!include[Card anatomy](~/includes/design/card-image-list.html)]

### <a name="bubble-merge"></a>气泡合并

可通过快速连续发送一个英雄和几个缩略图来实现一些有趣的效果。 当您希望为主结果提供服务但包含更多相关的项目时，建议采用这种方法。

[!include[Card anatomy](~/includes/design/card-image-bubble-merge.html)]

---

## <a name="best-practices"></a>最佳做法

### <a name="keep-the-noise-down"></a>将噪音降低

可以轻松地将多个卡片发送到对话中，但一旦卡片从视图中滚出，它们就会变得不太有用。 尝试将自己限制为重点。 在用户对其感觉为 "干扰" 的程度较差的频道中，尤其如此。

### <a name="test-on-mobile"></a>在移动设备上测试

移动环境具有空间和带宽限制，因此请注意在列表和 carousels 中包含过多的图像和大型数据集。 此外，标题宽度和文本长度将在移动时截断，因此，另一件事就是要保持关注。

### <a name="check-your-graphics"></a>检查图形

将缩放图形，因此请务必在所有平台上进行预览。

### <a name="avoid-including-text-in-a-graphic"></a>避免在图形中包含文本

用户需要阅读的任何内容都应包含在文本字段中。 动态缩放图像后，添加到图形中的任何文本都可能变得无法理解。

### <a name="use-mentions-if-you-want-the-attention-of-specific-users"></a>如果您希望特定用户注意，请使用提及

> [!NOTE]
> 在[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中，目前仅支持对卡片中提及支持。

提及是在团队或群聊天中通知特定用户的一种极好的方法。 您可以在类似、分配给用户的任务或向 teammate 提供荣誉的方案中包括提及的卡片。 了解如何在[卡片格式页](~/task-modules-and-cards/cards/cards-format.md)的卡片中添加提及。 
