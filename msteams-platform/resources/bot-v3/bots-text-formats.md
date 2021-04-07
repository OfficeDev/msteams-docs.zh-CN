---
title: 对话中支持的文本格式
description: 介绍自动程序对话中的文本格式支持
keywords: 机器人对话消息传送
ms.date: 03/29/2018
ms.openlocfilehash: 3ef51a7f6e4e923d83ab746a2dfa1f22464efb93
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596264"
---
# <a name="formatting-bot-messages"></a>设置机器人消息的格式

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

可以设置可选 [`TextFormat`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) 属性来控制邮件文本内容的呈现方式。

Microsoft Teams 支持以下格式选项：

| TextFormat 值 | Description |
| --- | --- |
| plain | 文本应视为原始文本，而未应用任何格式 |
| markdown | 文本应视为 Markdown 格式，并在适当时呈现在频道上;请参阅 [格式化支持样式](#formatting-text-content) 的文本内容 |
| xml | 文本是简单的 XML 标记;请参阅 [格式化支持样式](#formatting-text-content) 的文本内容 |

## <a name="formatting-text-content"></a>设置文本内容的格式

Microsoft Teams 支持 Markdown 和 XML 代码的一 (HTML) 格式标记。

目前，存在以下限制：

* 纯文本邮件不支持表格式设置

有关卡片格式的信息，请参阅 Teams [卡片参考](~/task-modules-and-cards/cards/cards-reference.md)。

### <a name="cross-platform-support"></a>跨平台支持

若要确保你的格式可以在 Microsoft Teams 支持的所有平台上运行，请注意某些样式当前并非在所有平台上都受支持。

| 样式                     | 纯文本邮件 | 卡片 (XML)  |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| 页眉 (级别 1 &ndash; 3)  | ✖                  | ✔                |
| strikethrough             | ✖                  | ✔                |
| 水平规则           | ✖                  | ✖                |
| 无序列表            | ✖                  | ✔                |
| 排序列表              | ✖                  | ✔                |
| 预设格式的文本         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| 超链接                 | ✔                  | ✔                |
| 图像链接                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>单个平台支持

对文本格式的支持因邮件类型和平台而异。

#### <a name="text-only-messages"></a>纯文本邮件

| 样式                     | 桌面 | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| 页眉 (级别 1 &ndash; 3)  | ✖       | ✖   | ✖       |
| strikethrough             | ✔       | ✔   | ✖       |
| 水平规则           | ✖       | ✖   | ✖       |
| 无序列表            | ✔       | ✖   | ✖       |
| 排序列表              | ✔       | ✖   | ✖       |
| 预设格式的文本         | ✔       | ✔   | ✔       |
| blockquote                | ✔       | ✔   | ✔       |
| 超链接                 | ✔       | ✔   | ✔       |
| 图像链接                | ✔       | ✔   | ✔       |

### <a name="examples-of-text-formatting"></a>文本格式示例

| 样式 | 示例 | Markdown | XML (HTML)  |
| --- | --- | --- | --- |
| bold | **text** | `**text**` | `<strong>text</strong>` |
| italic | *text* | `*text*` | `<em>text</em>` |
| 页眉 (级别 1 &ndash; 3)  | **Text** | `### Text` | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| 无序列表 | <ul><li>text</li><li>text</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| 排序列表 | <ol><li>text</li><li>text</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| 预设格式的文本 | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| 超链接 | [必应](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| 图像链接 | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |
