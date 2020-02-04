---
title: 对话中支持的文本格式
description: 描述 bot 对话中的文本格式支持
keywords: bot 对话消息
ms.date: 03/29/2018
ms.openlocfilehash: cc6cba697a1f6907bfb13b94740e7bf9e92596da
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673026"
---
# <a name="formatting-bot-messages"></a>格式化 bot 邮件

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

您可以设置可选[`TextFormat`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message)属性以控制邮件的文本内容的呈现方式。

Microsoft 团队支持以下格式设置选项：

| TextFormat 值 | 说明 |
| --- | --- |
| 文本 | 应将文本视为原始文本，而不会应用任何格式设置 |
| markdown | 应根据需要将文本视为 Markdown 格式并在通道上呈现。有关支持的样式，请参阅[格式化文本内容](#formatting-text-content) |
| xml | 文本是简单的 XML 标记;有关支持的样式，请参阅[格式化文本内容](#formatting-text-content) |

## <a name="formatting-text-content"></a>设置文本内容的格式

Microsoft 团队支持 Markdown 和 XML （HTML）格式设置标记的子集。

目前，以下限制适用：

* 纯文本邮件不支持表格格式

有关卡片中的格式设置的信息，请参阅[团队卡片参考](~/task-modules-and-cards/cards/cards-reference.md)。

### <a name="cross-platform-support"></a>跨平台支持

若要确保您的格式在 Microsoft 团队支持的所有平台上都有效，请注意，目前不支持在所有平台上使用某些样式。

| Style                     | 纯文本邮件 | 卡片（仅限 XML） |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| 标头（级别&ndash;1 3） | ✖                  | ✔                |
| 删除             | ✖                  | ✔                |
| 水平标尺           | ✖                  | ✖                |
| 无序列表            | ✖                  | ✔                |
| 排序列表              | ✖                  | ✔                |
| 预设格式文本         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| 超链接                 | ✔                  | ✔                |
| 图像链接                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>由单个平台支持

对文本格式的支持因邮件类型和平台而异。

#### <a name="text-only-messages"></a>纯文本邮件

| Style                     | 桌面 | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| 标头（级别&ndash;1 3） | ✖       | ✖   | ✖       |
| 删除             | ✔       | ✔   | ✖       |
| 水平标尺           | ✖       | ✖   | ✖       |
| 无序列表            | ✔       | ✖   | ✖       |
| 排序列表              | ✔       | ✖   | ✖       |
| 预设格式文本         | ✔       | ✔   | ✔       |
| blockquote                | ✔       | ✔   | ✔       |
| 超链接                 | ✔       | ✔   | ✔       |
| 图像链接                | ✔       | ✔   | ✔       |

### <a name="examples-of-text-formatting"></a>文本格式的示例

| Style | 示例 | Markdown | XML （HTML） |
| --- | --- | --- | --- |
| bold | **text** | `**text**` | `<strong>text</strong>` |
| italic | *text* | `*text*` | `<em>text</em>` |
| 标头（级别&ndash;1 3） | **Text** | `### Text` | `<h3>Text</h3>` |
| 删除 | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| 无序列表 | <ul><li>text</li><li>text</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| 排序列表 | <ol><li>text</li><li>text</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| 预设格式文本 | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| 超链接 | [必应](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| 图像链接 | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |
