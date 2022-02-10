---
title: 创建“共享到 Teams”按钮
description: 了解如何使用代码示例Teams网站预览中添加"共享到"嵌入按钮
ms.topic: reference
ms.localizationpriority: medium
keywords: 共享Teams共享到Teams
ms.openlocfilehash: a2c94ad690864b6af89005af4f96866f1ebda0b6
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518490"
---
# <a name="create-share-to-teams-button"></a>创建“共享到 Teams”按钮

第三方网站可以使用启动器脚本将"共享到Teams按钮嵌入到其网页上。 选择后，它将在弹出窗口中Teams"共享到用户"体验。 这允许你直接将链接共享给任何人员或Microsoft Teams频道，而无需切换上下文。 本文档指导您如何为网站创建和嵌入"共享到 Teams"按钮、制作网站预览以及扩展"共享到Teams 教育版"。

> [!NOTE]
> * 仅支持 MicrosoftEdge&nbsp; 和 Google Chrome 的桌面版本。
> * 不支持使用免费增值帐户或来宾帐户。  

下图显示了"共享到Teams"弹出体验：

!["共享到Teams"弹出窗口](~/assets/images/share-to-teams-popup.png)

## <a name="embed-a-share-to-teams-button"></a>嵌入"共享到Teams"按钮

1. 在网页上 `launcher.js` 添加脚本。

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. 在网页上添加一个 HTML 元素，该 `teams-share-button` 元素具有类属性和要共享属性 `data-href` 中的链接。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    完成此操作后，Microsoft Teams图标将添加到您的网站。 下图显示了"共享到Teams图标：

    ![共享到Teams图标](~/assets/icons/share-to-teams-icon.png)

1. 或者，如果希望"共享对象"按钮具有不同的图标大小Teams，请使用 `data-icon-px-size` 属性。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```
1. 如果共享链接需要用户身份验证，并且要共享的链接中的 URL 预览在 Teams 中无法很好地呈现，则可以通过添加 设置为 的属性来禁用 URL `data-preview` 预览`false`。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. 如果页面动态呈现内容 `shareToMicrosoftTeams.renderButtons()` ，可以使用 方法强制 **共享** 在管道中的适当位置呈现。

## <a name="craft-your-website-preview"></a>制作网站预览

将网站共享到Teams时，插入选定频道的卡片将包含网站的预览。 您可以通过确保将适当的 `data-href` 元数据添加到要共享的网站（如 URL）来控制此预览的行为。  

**显示预览**

* 必须包含缩略图 **图像，** 或同时包含 **标题和****说明**。 为了获得最佳结果，请全部包含这三者。
* 共享 URL 不需要身份验证。 如果要求进行身份验证，可以共享它，但不创建预览。

下表概述了必要的标记：

|值|Meta 标记| 打开Graph|
|----|----|----|
|Title|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|说明|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|缩略图图像| 无。 |`<meta property="og:image" content="http://example.com/image.jpg">`|

可以使用 HTML 默认版本或 Open Graph版本。

## <a name="share-to-teams-for-education"></a>共享到Teams 教育版

对于使用"共享到Teams"按钮的教师，还有一个附加选项。`Create an Assignment` 这使您能够基于共享链接在所选团队中快速创建工作分配。 下图显示了适用于教育的Teams共享： 

![共享到Teams弹出式教育](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>完整launcher.js定义

| 属性 | HTML 属性 | 类型 | 默认值 | 说明 |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | 字符串 | 不适用 | 要共享的内容的 href。 |
| preview | `data-preview` | boolean (字符串类型)  | `true` | 是否显示要共享的内容的预览。 |
| iconPxSize | `data-icon-px-size` | number (作为字符串)  | `32` | 要呈现的"共享到Teams按钮的大小（以像素为单位）。 |
| msgText | `data-msg-text` | 字符串 | 不适用 | 要插入到邮件撰写框中的链接之前的默认文本。 最大字符数为 200。 |
| assignInstr | `data-assign-instr` | 字符串 | 不适用 | 要插入到工作分配"说明"字段中的默认文本。 最大字符数为 200。 |
| assignTitle | `data-assign-title` | string | 不适用 | 要插入到工作分配"标题"字段中的默认文本。 最大字符数为 50。 |

### <a name="methods"></a>Methods

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (可选) ： `{ elements?: HTMLElement[] }`

目前，所有共享按钮都呈现在页面上。 如果随 `options` 元素列表一起提供可选对象，则这些元素将呈现到共享按钮中。

### <a name="set-default-form-values"></a>设置默认表单值

可以选择在"共享"表单上设置以下字段的Teams值：

* 对此说一些： `msgText`
* 工作分配说明： `assignInstr`
* 工作分配标题： `assignTitle`

#### <a name="example"></a>示例

 下面的示例中给出默认表单值：

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```

## <a name="see-also"></a>另请参阅

[集成 web 应用](~/samples/integrate-web-apps-overview.md)
