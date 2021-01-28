---
title: 创建“共享到Teams”按钮
description: 如何在网站上添加"共享到 Teams"嵌入按钮
ms.topic: reference
keywords: 共享 Teams 共享到 Teams
ms.openlocfilehash: 46091c957137cc871095ca6a57c0d61fa79d9458
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014332"
---
# <a name="create-a-share-to-teams-button-for-your-website"></a>为网站创建“共享到 Teams”按钮

>[!NOTE]
> * 仅支持桌面版 Edge 和 Chrome。
> * 不支持使用免费增值帐户或来宾帐户。

第三方网站可以使用启动器脚本在其网页上嵌入"共享到 Teams"按钮，这将在单击时在弹出窗口中启动"共享到 Teams"体验。 这将允许你直接将链接共享给任何人或 Microsoft Teams 频道，而无需切换上下文。

![共享到 Teams 弹出窗口](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a>如何嵌入"共享到 Teams"按钮

首先，您需要在网页上 `launcher.js` 添加脚本。

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

接下来，在网页上添加一个 HTML 元素，该元素包含类属性和在属性 `teams-share-button` 中共享 `data-href` 的链接。

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

这会将 Microsoft Teams 图标添加到你的网站。

![共享到 Teams 图标](~/assets/icons/share-to-teams-icon.png)

（可选）如果需要"共享到 Teams"按钮的不同图标大小，请使用 `data-icon-px-size` 该属性。

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

如果你知道要共享的链接中的 URL 预览不会在 Teams (例如，链接需要用户身份验证) 可以通过将属性集添加到禁用 URL 预览 `data-preview` `false` 。

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

如果页面动态呈现内容，可以使用该方法强制"共享"按钮在管道 `shareToMicrosoftTeams.renderButtons()` 中的适当位置呈现。

## <a name="crafting-your-website-preview"></a>精心制作网站预览

将你的网站共享到 Teams 时，插入到所选频道的卡片将包含你的网站的预览。 您可以通过确保向要共享的网站添加适当的元数据（通过 URL `data-href` (）来控制) 。 下表概述了必要的标记。 可以使用 html 默认版本或 Open Graph 版本。

若要显示预览，必须：

* 包括缩略图图像，或同时包含标题和说明 (，以获得最佳效果，请包含所有三) 。
* 要共享的 URL 不能要求身份验证。 如果是这样，你仍可以共享它，但无法创建预览。

|值|Meta 标记| Open Graph|
|----|----|----|
|标题|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|说明|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|缩略图图像| 无 |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a>共享到 Teams 教育

对于使用"共享到 Teams"按钮的教师，你将获得一个附加选项 `Create an Assignment` 。 这使您能够基于共享链接在所选团队中快速创建工作分配。

![共享到 Teams 弹出窗口](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>完整launcher.js定义

| 属性 | HTML 属性 | 类型 | 默认值 | 说明 |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | 不适用 | 要共享的内容的 href。 |
| preview | `data-preview` | boolean (作为字符串)  | `true` | 是否显示要共享的内容的预览。 |
| iconPxSize | `data-icon-px-size` | number (作为字符串)  | `32` | 要呈现的"共享到 Teams"按钮的大小（以像素为单位）。 |
| msgText | `data-msg-text` | string | 不适用 | 在邮件撰写框中的链接之前插入的默认文本 (200 个字符)  |
| assignInstr | `data-assign-instr` | string | 不适用 | 要插入到工作分配"说明"字段中的默认文本 (200 个字符)  |
| assignTitle | `data-assign-title` | string | 不适用 | 要插入到工作分配"标题"字段中的默认文本 (50 个字符)  |

### <a name="methods"></a>方法

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (可选) ： `{ elements?: HTMLElement[] }`

呈现页面上当前的所有共享按钮。 如果随元素列表一起提供可选对象，则 `options` 这些元素将呈现到共享按钮中。

### <a name="setting-default-form-values"></a>设置默认表单值

（可选）你可以选择在"共享到 Teams"表单上设置以下字段的默认值：

* 说出有关此 `msgText` () 
* 工作分配 `assignInstr` () 
* 工作分配 `assignTitle` () 

#### <a name="example-default-form-values"></a>示例：默认表单值

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```
