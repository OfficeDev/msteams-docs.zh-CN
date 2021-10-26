---
title: 设置你的智能机器人邮件格式
author: surbhigupta
description: 向自动程序消息添加丰富的格式
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 7a8bcc272163a14836fb4b7324cd7ba617bb5409
ms.sourcegitcommit: 781e7b82240075e9d1f55e97f3f1dcbba82a5e4d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2021
ms.locfileid: "60566223"
---
# <a name="format-your-bot-messages"></a>设置你的智能机器人邮件格式

邮件格式使您能够在自动程序消息中获得最佳效果。 你可以设置自动程序消息的格式，以包含包含交互式元素（如按钮、文本、图像、音频、视频等）的附件的富卡片。

## <a name="format-text-content"></a>设置文本内容的格式

若要设置自动程序消息的格式，可以设置可选属性 [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) 以控制自动程序消息的文本内容的呈现方式。

Microsoft Teams支持以下格式选项：

| `TextFormat` value | 说明 |
| --- | --- |
| plain | 必须将文本视为原始文本，不应用任何格式。|
| markdown | 文本必须视为 markdown 格式，并在适当时呈现在频道上。 |
| xml | 文本是简单的 XML 标记。 |

Teams markdown 和 XML 或 HTML 格式标记的子集。

目前，以下限制适用于格式设置：

* 纯文本邮件不支持表格格式。
* 格式卡片仅支持文本属性中的格式设置，不支持标题或副标题属性中的格式设置。
* 富卡片不支持 markdown 或表格格式。

设置文本内容的格式后，请确保您的格式设置适用于所有受 Microsoft Teams。

## <a name="cross-platform-support"></a>跨平台支持

某些样式当前并非在所有平台上都受支持。 下表提供了一个样式列表，其中哪些样式在纯文本邮件和富卡片中受支持：

| 样式                     | 纯文本邮件 | 富卡片 - 仅 XML |
| ---                       | :---: | :---: |
| 粗体                      | ✔ | ✖ |
| 斜体                    | ✔ | ✔ |
| 标题 (级别 1 &ndash; 3)  | ✖ | ✔ |
| 删除线             | ✖ | ✔ |
| 水平规则           | ✖ | ✖ |
| 未排序列表            | ✖ | ✔ |
| 已排序列表              | ✖ | ✔ |
| 预设格式的文本         | ✔ | ✔ |
| Blockquote                | ✔ | ✔ |
| 超链接                 | ✔ | ✔ |
| 图像链接                | ✔ | ✖ |

检查跨平台支持后，请确保各个平台也提供支持。

## <a name="support-by-individual-platform"></a>单个平台支持

对文本格式的支持因邮件类型和平台而异。

### <a name="text-only-messages"></a>纯文本邮件

下表提供了桌面、iOS 和 Android 上支持的样式列表：

| 样式                     | 桌面 | iOS | Android |
| ---                       | :---: | :---: | :---: |
| 粗体                      | ✔ | ✔ | ✔ |
| 斜体                    | ✔ | ✔ | ✔ |
| 标题 (级别 1 &ndash; 3)  | ✖ | ✖ | ✖ |
| 删除线             | ✔ | ✔ | ✖ |
| 水平规则           | ✖ | ✖ | ✖ |
| 未排序列表            | ✔ | ✖ | ✖ |
| 已排序列表              | ✔ | ✖ | ✖ |
| 预设格式的文本         | ✔ | ✔ | ✔ |
| Blockquote                | ✔ | ✔ | ✔ |
| 超链接                 | ✔ | ✔ | ✔ |
| 图像链接                | ✔ | ✔ | ✔ |

### <a name="cards"></a>卡片

有关卡支持，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [更新和删除机器人消息](~/bots/how-to/update-and-delete-bot-messages.md)
