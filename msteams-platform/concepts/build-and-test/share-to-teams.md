---
title: 创建“共享到 Teams”按钮
description: 了解如何使用代码示例Teams网站预览中的"共享到嵌入"按钮
ms.topic: reference
ms.localizationpriority: medium
keywords: 共享Teams共享到Teams
ms.openlocfilehash: 0f9425ae28312aeb9700d260d9ac2cf208351d4c
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889284"
---
# <a name="create-share-to-teams-button"></a>创建“共享到 Teams”按钮

第三方网站可以使用启动器脚本将"共享到Teams按钮嵌入到其网页上。 选择后，它将在弹出窗口中Teams"共享到共享"体验。 这允许你直接将链接共享给任何人员或Microsoft Teams频道，而无需切换上下文。 本文档指导您如何为网站创建和嵌入"共享到 Teams"按钮、制作网站预览以及扩展"共享到Teams 教育版"。

> [!NOTE]
> * 仅支持桌面版 Edge 和 Chrome。
> * 不支持使用免费增值帐户或来宾帐户。  

下图显示了"共享到Teams"弹出体验：

!["共享到Teams"弹出窗口](~/assets/images/share-to-teams-popup.png)

## <a name="embed-a-share-to-teams-button"></a>嵌入"共享到Teams按钮

1. 在 `launcher.js` 网页上添加脚本。

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. 在网页上添加一个 HTML 元素，该元素具有 `teams-share-button` 类属性和要共享属性 `data-href` 中的链接。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    完成此操作后，Microsoft Teams图标将添加到您的网站。 下图显示了"共享到Teams图标：

    ![共享到Teams图标](~/assets/icons/share-to-teams-icon.png)

1. 或者，如果您希望"共享对象"按钮具有不同的图标大小Teams，请使用 `data-icon-px-size` 属性。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```
1. 如果共享链接需要用户身份验证，并且要共享的链接中的 URL 预览在 Teams 中无法很好地呈现，则可以通过添加设置为 的属性来禁用 URL `data-preview` 预览 `false` 。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. 如果页面动态呈现内容，可以使用 方法强制共享在管道中的适当 `shareToMicrosoftTeams.renderButtons()` 位置呈现。

## <a name="craft-your-website-preview"></a>制作网站预览

将网站共享到Teams时，插入选定频道的卡片将包含网站的预览。 您可以通过确保将适当的元数据添加到要共享的网站（如 URL）来控制此预览 `data-href` 的行为。  

**显示预览**

* 必须包含缩略图 **图像，或** 标题 **和说明****。** 为了获得最佳结果，请全部包含这三者。
* 共享 URL 不需要身份验证。 如果要求进行身份验证，可以共享它，但不创建预览。

下表概述了必要的标记：

|值|Meta 标记| 打开Graph|
|----|----|----|
|Title|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|说明|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|缩略图图像| 无。 |`<meta property="og:image" content="http://example.com/image.jpg">`|

可以使用 HTML 默认版本或 Open Graph版本。

## <a name="share-to-teams-for-education"></a>共享到Teams 教育版

对于使用"共享到Teams"按钮的教师，还有一个附加选项 `Create an Assignment` 。 这使您能够基于共享链接在所选团队中快速创建工作分配。 下图显示了适用于教育的Teams共享： 

![共享到Teams弹出式教育](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>完整launcher.js定义

| 属性 | HTML 属性 | 类型 | 默认值 | 说明 |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | 不适用 | 要共享的内容的 href。 |
| preview | `data-preview` | boolean (字符串类型)  | `true` | 是否显示要共享的内容的预览。 |
| iconPxSize | `data-icon-px-size` | 数字 (字符串形式)  | `32` | 要呈现的"共享到Teams按钮的大小（以像素为单位）。 |
| msgText | `data-msg-text` | string | 不适用 | 要插入到邮件撰写框中的链接之前的默认文本。 最大字符数为 200。 |
| assignInstr | `data-assign-instr` | string | 不适用 | 要插入到工作分配"说明"字段中的默认文本。 最大字符数为 200。 |
| assignTitle | `data-assign-title` | string | 不适用 | 要插入到工作分配"标题"字段中的默认文本。 最大字符数为 50。 |

### <a name="methods"></a>方法

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (可选) ： `{ elements?: HTMLElement[] }`

目前，所有共享按钮都呈现在页面上。 如果随 `options` 元素列表一起提供可选对象，则这些元素将呈现到共享按钮中。

### <a name="set-default-form-values"></a>设置默认表单值

可以选择在"共享"表单上为以下字段设置Teams值：

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
