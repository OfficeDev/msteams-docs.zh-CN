---
title: 对话中支持的文本格式
description: 在本模块中，了解机器人对话中的文本格式设置支持，并在Microsoft Teams中设置文本内容的格式
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 03/29/2018
ms.openlocfilehash: 0aea1472a323c0161567c4661c02956568cb2187
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189734"
---
# <a name="formatting-bot-messages"></a>设置机器人消息的格式

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
* 仅文本邮件不支持表格格式设置。

有关卡片格式化的信息，[请参阅Teams卡片参考](~/task-modules-and-cards/cards/cards-reference.md)。

### <a name="cross-platform-support"></a>跨平台支持

若要确保格式设置适用于Teams支持的所有平台，请注意，某些样式当前不支持所有平台。

| 样式                     | 仅文本邮件 | 仅)  (XML 的卡片 |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| 标头 (级别 1&ndash;3)  | ✖                  | ✔                |
| strikethrough             | ✖                  | ✔                |
| 水平规则           | ✖                  | ✖                |
| 未排序列表            | ✖                  | ✔                |
| 已排序列表              | ✖                  | ✔                |
| 预格式化文本         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| 超链接                 | ✔                  | ✔                |
| 图像链接                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>单个平台的支持

对文本格式的支持因消息类型和平台而异。

#### <a name="text-only-messages"></a>仅文本邮件

| 样式                     | 桌面 | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| 标头 (级别 1&ndash;3)  | ✖       | ✖   | ✖       |
| strikethrough             | ✔       | ✔   | ✖       |
| 水平规则           | ✖       | ✖   | ✖       |
| 未排序列表            | ✔       | ✖   | ✖       |
| 已排序列表              | ✔       | ✖   | ✖       |
| 预格式化文本         | ✔       | ✔   | ✔       |
| blockquote                | ✔       | ✔   | ✔       |
| 超链接                 | ✔       | ✔   | ✔       |
| 图像链接                | ✔       | ✔   | ✔       |

### <a name="examples-of-text-formatting"></a>文本格式的示例

| 样式 | 示例 | Markdown | XML (HTML)  |
| --- | --- | --- | --- |
| bold | **text** | `**text**` | `<strong>text</strong>` |
| italic | *text* | `*text*` | `<em>text</em>` |
| 标头 (级别 1&ndash;3)  | **Text** | `### Text` | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| 未排序列表 | <ul><li>text</li><li>text</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| 已排序列表 | <ol><li>text</li><li>text</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| 预格式化文本 | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| 超链接 | [必应](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| 图像链接 | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |
