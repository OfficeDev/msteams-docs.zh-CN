---
title: 自动程序消息格式
description: 介绍自动程序消息格式的详细信息
keywords: teams 方案频道对话机器人消息
ms.topic: reference
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: e737cd42d2aa00e3e4f302b4917fef67adaa5645
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155843"
---
# <a name="message-formatting-for-bots"></a>自动程序的邮件格式

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

可以设置可选 [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) 属性来控制邮件文本内容的呈现方式。

Microsoft Teams支持以下格式选项：

| TextFormat 值 | 说明 |
| --- | --- |
| plain | 文本应视为原始文本，而未应用任何格式。 |
| markdown | 文本应视为 Markdown 格式，并在适当时呈现在频道上;请参阅 [格式化支持样式](#formatting-text-content) 的文本内容。 |
| xml | 文本是简单的 XML 标记;请参阅 [格式化支持样式](#formatting-text-content) 的文本内容。 |

## <a name="formatting-text-content"></a>设置文本内容的格式

Microsoft Teams一部分 Markdown 和 XML (HTML) 格式标记。

目前，存在以下限制：

* 纯文本邮件不支持表格格式。
* 格式卡片仅支持文本属性中的格式设置，不支持标题或副标题属性中的格式设置。
* 富卡片不支持 Markdown 或表格格式。

## <a name="cross-platform-support"></a>跨平台支持

为了确保格式设置在所有受 Microsoft Teams支持的平台中运行，请注意某些样式当前并非在所有平台上都受支持。

| 样式                     | 纯文本邮件 | 富卡 (XML)  |
| ---                       | :---: | :---: |
| bold                      | ✔ | ✖ |
| italic                    | ✔ | ✔ |
| 页眉 (级别 1 &ndash; 3)  | ✖ | ✔ |
| strikethrough             | ✖ | ✔ |
| 水平规则           | ✖ | ✖ |
| 无序列表            | ✖ | ✔ |
| 排序列表              | ✖ | ✔ |
| 预设格式的文本         | ✔ | ✔ |
| blockquote                | ✔ | ✔ |
| 超链接                 | ✔ | ✔ |
| 图像链接                | ✔ | ✖ |

## <a name="support-by-individual-platform"></a>单个平台支持

对文本格式的支持因邮件类型和平台而异。

### <a name="text-only-messages"></a>纯文本邮件

| 样式                     | 桌面 | iOS | Android |
| ---                       | :---: | :---: | :---: |
| bold                      | ✔ | ✔ | ✔ |
| italic                    | ✔ | ✔ | ✔ |
| 页眉 (级别 1 &ndash; 3)  | ✖ | ✖ | ✖ |
| strikethrough             | ✔ | ✔ | ✖ |
| 水平规则           | ✖ | ✖ | ✖ |
| 无序列表            | ✔ | ✖ | ✖ |
| 排序列表              | ✔ | ✖ | ✖ |
| 预设格式的文本         | ✔ | ✔ | ✔ |
| blockquote                | ✔ | ✔ | ✔ |
| 超链接                 | ✔ | ✔ | ✔ |
| 图像链接                | ✔ | ✔ | ✔ |

### <a name="cards"></a>卡片

有关详细信息，请参阅 [卡片格式，](~/task-modules-and-cards/cards/cards-format.md) 获取卡片支持。
