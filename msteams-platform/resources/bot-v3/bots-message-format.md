---
title: 自动程序消息格式
description: 介绍自动程序消息格式的详细信息
keywords: teams 方案频道对话机器人消息
ms.topic: reference
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: 06037bd3fb23ace11eea763747dc64d763ac3c42
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020644"
---
# <a name="message-formatting-for-bots"></a>自动程序的邮件格式

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

可以设置可选 [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) 属性来控制邮件文本内容的呈现方式。

Microsoft Teams支持以下格式选项：

| TextFormat 值 | 说明 |
| --- | --- |
| plain | 文本应视为原始文本，而未应用任何格式 |
| markdown | 文本应视为 Markdown 格式，并在适当时呈现在频道上;请参阅 [格式化支持样式](#formatting-text-content) 的文本内容 |
| xml | 文本是简单的 XML 标记;请参阅 [格式化支持样式](#formatting-text-content) 的文本内容 |

## <a name="formatting-text-content"></a>设置文本内容的格式

Microsoft Teams一部分 Markdown 和 XML (HTML) 格式标记。

目前，存在以下限制：

* 纯文本邮件不支持表格式设置
* 格式卡片仅支持文本属性中的格式设置，不支持标题或副标题属性中的格式设置
* 富卡不支持 Markdown 或表格格式

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

### <a name="cards"></a>卡

有关 [卡片支持，](~/task-modules-and-cards/cards/cards-format.md) 请参阅卡片格式。
