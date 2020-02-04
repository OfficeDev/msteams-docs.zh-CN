---
title: Bot 邮件格式
description: 描述 bot 邮件格式的详细信息
keywords: 团队方案频道对话 bot 邮件
ms.date: 05/20/2019
ms.openlocfilehash: eb0d0303d2b414ff84beab73055be5f057fff11c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673477"
---
# <a name="message-formatting-for-bots"></a>Bot 的邮件格式

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

您可以设置可选[`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message)属性以控制邮件的文本内容的呈现方式。

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
* 富卡片仅支持 text 属性中的格式设置，而不支持标题或副标题属性中的格式
* 丰富卡片不支持 Markdown 或表格格式

## <a name="cross-platform-support"></a>跨平台支持

若要确保您的格式在 Microsoft 团队支持的所有平台上都有效，请注意，目前不支持在所有平台上使用某些样式。

| Style                     | 纯文本邮件 | 丰富卡片（仅限 XML） |
| ---                       | :---: | :---: |
| bold                      | ✔ | ✖ |
| italic                    | ✔ | ✔ |
| 标头（级别&ndash;1 3） | ✖ | ✔ |
| 删除             | ✖ | ✔ |
| 水平标尺           | ✖ | ✖ |
| 无序列表            | ✖ | ✔ |
| 排序列表              | ✖ | ✔ |
| 预设格式文本         | ✔ | ✔ |
| blockquote                | ✔ | ✔ |
| 超链接                 | ✔ | ✔ |
| 图像链接                | ✔ | ✖ |

## <a name="support-by-individual-platform"></a>由单个平台支持

对文本格式的支持因邮件类型和平台而异。

### <a name="text-only-messages"></a>纯文本邮件

| Style                     | 桌面 | iOS | Android |
| ---                       | :---: | :---: | :---: |
| bold                      | ✔ | ✔ | ✔ |
| italic                    | ✔ | ✔ | ✔ |
| 标头（级别&ndash;1 3） | ✖ | ✖ | ✖ |
| 删除             | ✔ | ✔ | ✖ |
| 水平标尺           | ✖ | ✖ | ✖ |
| 无序列表            | ✔ | ✖ | ✖ |
| 排序列表              | ✔ | ✖ | ✖ |
| 预设格式文本         | ✔ | ✔ | ✔ |
| blockquote                | ✔ | ✔ | ✔ |
| 超链接                 | ✔ | ✔ | ✔ |
| 图像链接                | ✔ | ✔ | ✔ |

### <a name="cards"></a>圣诞卡

请参阅[卡片格式](~/task-modules-and-cards/cards/cards-format.md)以获得卡片支持。
