---
title: 设置你的智能机器人邮件格式
author: surbhigupta
description: 了解如何设置机器人消息的格式和样式，例如删除线、有序列表和无序列表、超链接或图像链接。 了解跨平台支持。
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: b0db9f9d9e55dc3f11474dac4b8c6563caf5fd1b
ms.sourcegitcommit: bb15ce26cd65bec90991b703069424ab4b4e1a61
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2022
ms.locfileid: "68772298"
---
# <a name="format-your-bot-messages"></a>设置你的智能机器人邮件格式

邮件格式设置可以使机器人邮件发挥出最佳效果。 可以设置机器人消息的格式，以将富卡作为附件包含交互式元素，例如按钮、文本、图像等。

> [!NOTE]
> 机器人消息大小限制为 40 KB。 如果机器人消息大小限制超过 40 KB，机器人会收到状态 `413` 代码 (`RequestEntityTooLarge`) ，其中包含错误代码 `MessageSizeTooBig`。 机器人消息大小限制包括编码为 UTF-16 的整个消息有效负载，不包括 Base64 编码的图像。

## <a name="format-text-content"></a>设置文本内容格式

若要设置机器人邮件的格式，可以设置可选 [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) 属性以控制机器人邮件文本内容的呈现方式。

Microsoft Teams 支持以下格式设置选项：

| `TextFormat` 值 | 说明 |
| --- | --- |
| 纯文本 | 文本必须被视为原始文本，不应用任何格式。|
| markdown | 文本必须被视为 markdown 格式，并以适当格式在频道中呈现。 |
| xml | 文本是简单的 XML 标记。 |

Teams 支持一部分 markdown 和 XML 或 HTML 格式标记。

目前，以下限制适用于格式设置：

* 纯文本消息不支持表格格式设置。
* 丰富卡片仅支持在文本属性中进行格式设置，不支持在标题或副标题属性中进行格式设置。
* 富卡不支持 Markdown 或表格格式。

设置文本内容格式后，请确保你的格式设置适用于 Teams 支持的所有平台。

## <a name="cross-platform-support"></a>跨平台支持

目前，某些样式未在所有平台上受支持。 下表提供了样式列表，其中列出了哪种样式在仅文本的邮件和丰富卡片中受支持：

| 样式                     | 仅文本邮件 | 丰富卡片 - 仅 XML |
| ---                       | :---: | :---: |
| 粗体                      | ✔️️ | ❌ |
| 斜体                    | ✔️ | ✔️ |
| 标头 (级别 1&ndash;3) | ❌ | ✔️ |
| 删除线             | ❌ | ✔️ |
| 水平规则           | ❌ | ❌ |
| 未排序列表            | ❌ | ✔️ |
| 已排序列表              | ❌ | ✔️ |
| 预设格式的文本         | ✔️ | ✔️ |
| Blockquote                | ✔️ | ✔️ |
| Hyperlink                 | ✔️ | ✔️ |
| 图像链接                | ❌ | ❌ |

检查跨平台支持后，请确保单个平台的支持也可用。

## <a name="support-by-individual-platform"></a>单个平台的支持

对文本格式设置的支持因消息和平台的类型而异。

### <a name="text-only-messages"></a>仅文本邮件

下表提供了样式列表，其中列出哪些样式在桌面、iOS 和 Android 上受支持：

| 样式                     | 桌面 | iOS | Android |
| ---                       | :---: | :---: | :---: |
| 粗体                      | ✔️ | ✔️ | ✔️ |
| 斜体                    | ✔️ | ✔️ | ✔️ |
| 标头 (级别 1&ndash;3) | ❌ | ❌ | ❌ |
| 删除线             | ✔️ | ✔️ | ❌ |
| 水平规则           | ❌ | ❌ | ❌ |
| 未排序列表            | ✔️ | ❌ | ❌ |
| 已排序列表              | ✔️ | ❌ | ❌ |
| 预设格式的文本         | ✔️ | ✔️ | ✔️ |
| Blockquote                | ✔️ | ✔️ | ✔️ |
| Hyperlink                 | ✔️ | ✔️ | ✔️ |
| 图像链接                | ❌ | ❌ | ❌ |

### <a name="cards"></a>卡片

有关卡片支持，请参阅[卡片格式设置](~/task-modules-and-cards/cards/cards-format.md)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [更新和删除机器人消息](~/bots/how-to/update-and-delete-bot-messages.md)
