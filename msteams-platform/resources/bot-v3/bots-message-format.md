---
title: 机器人消息格式
description: 在本模块中，了解机器人消息格式设置的详细信息
ms.topic: reference
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: 9e331a17940ee482a0c2adcb81b57a17823ab668
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2022
ms.locfileid: "66190166"
---
# <a name="message-formatting-for-bots"></a>机器人的消息格式

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

可以设置可选 [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) 属性来控制消息文本内容的呈现方式。

Microsoft Teams 支持以下格式设置选项：

| TextFormat 值 | 说明 |
| --- | --- |
| 纯文本 | 文本应被视为原始文本，无需应用任何格式。 |
| markdown | 文本应被视为 Markdown 格式，并根据需要在通道上呈现;请参阅 [支持样式的格式化文本内容](#formatting-text-content) 。 |
| xml | 文本是简单的 XML 标记;请参阅 [支持样式的格式化文本内容](#formatting-text-content) 。 |

## <a name="formatting-text-content"></a>设置文本内容格式

Teams支持 Markdown 和 XML (HTML) 格式设置标记的子集。

目前，以下限制适用：

* 仅文本消息不支持表格格式。
* 丰富卡片仅支持在文本属性中进行格式设置，不支持在标题或副标题属性中进行格式设置。
* 富卡不支持 Markdown 或表格格式。

## <a name="cross-platform-support"></a>跨平台支持

若要确保格式设置适用于Teams支持的所有平台，请注意，某些样式当前不支持所有平台。

| 样式                     | 仅文本邮件 | 仅)  (XML 的丰富卡片 |
| ---                       | :---: | :---: |
| bold                      | ✔️️ | ❌ |
| italic                    | ✔️ | ✔️ |
| 标头 (级别 1&ndash;3)  | ❌ | ✔️ |
| strikethrough             | ❌ | ✔️ |
| 水平规则           | ❌ | ❌ |
| 未排序列表            | ❌ | ✔️ |
| 已排序列表              | ❌ | ✔️ |
| 预格式化文本         | ✔️ | ✔️ |
| blockquote                | ✔️ | ✔️ |
| 超链接                 | ✔️ | ✔️ |
| 图像链接                | ✔️ | ❌ |

## <a name="support-by-individual-platform"></a>单个平台的支持

对文本格式的支持因消息类型和平台而异。

### <a name="text-only-messages"></a>仅文本邮件

| 样式                     | 桌面 | iOS | Android |
| ---                       | :---: | :---: | :---: |
| bold                      | ✔️ | ✔️ | ✔️ |
| italic                    | ✔️ | ✔️ | ✔️ |
| 标头 (级别 1&ndash;3)  | ❌ | ❌ | ❌ |
| strikethrough             | ✔️ | ✔️ | ❌ |
| 水平规则           | ❌ | ❌ | ❌ |
| 未排序列表            | ✔️ | ❌ | ❌ |
| 已排序列表              | ✔️ | ❌ | ❌ |
| 预格式化文本         | ✔️ | ✔️ | ✔️ |
| blockquote                | ✔️ | ✔️ | ✔️ |
| 超链接                 | ✔️ | ✔️ | ✔️ |
| 图像链接                | ✔️ | ✔️ | ✔️ |

### <a name="cards"></a>卡片

有关详细信息，请参阅 [卡片格式设置](~/task-modules-and-cards/cards/cards-format.md) 以获取卡片中的支持。
