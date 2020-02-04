---
title: "\"共享到团队\" 嵌入按钮"
description: 如何将共享添加到你的网站上的工作组嵌入式按钮
keywords: 共享团队共享与团队共享
ms.openlocfilehash: 219724e6ef3448db8a5b1fc70a519803255ffee6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673343"
---
# <a name="creating-a-share-to-teams-embedded-button"></a>创建到工作组的共享按钮嵌入按钮

>[!NOTE]
> * 仅支持桌面版本的 Edge 和 Chrome。
> * 不支持使用 Freemium 或来宾帐户。

第三方网站可以使用启动器脚本在其网页上嵌入 "团队" 按钮共享，在单击时，将启动共享，以在弹出窗口中体验到团队的体验。 这将允许您在不切换上下文的情况下直接与任何人或 Microsoft 团队频道共享链接。

![共享到团队弹出菜单](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a>如何向团队按钮中嵌入共享

首先，你需要在你的网页`launcher.js`上添加脚本。

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

接下来，使用`teams-share-button` class 属性和要在`data-href`属性中共享的链接，在您的网页上添加一个 HTML 元素。

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

这将向您的网站添加 Microsoft 团队图标。

!["共享到团队" 图标](~/assets/icons/share-to-teams-icon.png)

（可选）如果您希望 "共享到团队" 按钮的图标大小不同，请`data-icon-px-size`使用属性。

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

如果您知道要共享的链接中的 URL 预览，团队中的呈现效果不好（例如，链接需要用户身份验证）您可以通过将`data-preview`属性设置为来`false`禁用 url 预览。

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

如果您的页面动态呈现内容，则可以使用此`shareToMicrosoftTeams.renderButtons()`方法强制在管道中的适当位置呈现 "**共享**" 按钮。

## <a name="crafting-your-website-preview"></a>编制网站预览

当您的网站与团队共享时，插入到选定频道的卡片将包含您的网站的预览。 您可以通过确保将适当的元数据添加到正在共享的网站（ `data-href` URL）来控制此预览的行为。 下表概述了必要的标记。 您可以使用 html 默认版本或打开的图形版本。

为了显示预览，必须执行以下操作：

* 包含缩略图图像，或同时包含标题和说明（若要获得最佳结果，请包含这三个图像）。
* 共享的 URL 不需要身份验证。 如果仍可以共享，则不会创建预览。

|值|Meta 标记| 打开图形|
|----|----|----|
|标题|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|说明|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|缩略图图像| 无 |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a>共享到教育版团队

对于使用 "共享到团队" 按钮的教师，你将向`Create an Assignment`你提供其他选项。 这使您可以基于共享链接快速创建所选团队中的工作分配。

![共享到团队弹出菜单](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>完整的启动程序 .js 定义

| 属性 | HTML 属性 | 类型 | 默认值 | 说明 |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | 无 | 要共享的内容的 href。 |
| preview | `data-preview` | boolean （以字符串形式） | `true` | 是否显示要共享的内容的预览。 |
| iconPxSize | `data-icon-px-size` | 数字（以字符串形式） | `32` | 要呈现的 "要呈现的团队共享" 按钮的大小（以像素为单位）。 |
| msgText | `data-msg-text` | string | 无 | 在邮件撰写框中的链接前插入的默认文本（200字符限制） |
| assignInstr | `data-assign-instr` | string | 无 | 要插入到工作分配的 "说明" 字段中的默认文本（200字符数限制） |
| assignTitle | `data-assign-title` | string | 无 | 要插入到工作分配 "标题" 字段中的默认文本（50字符数限制） |

### <a name="methods"></a>方法

**`shareToMicrosoftTeams.renderButtons(options)`**

`options`（可选）：`{ elements?: HTMLElement[] }`

呈现当前页面上的所有共享按钮。 如果一个可选`options`对象与一个元素列表一起提供，则这些元素将呈现在 "共享" 按钮中。

### <a name="setting-default-form-values"></a>设置默认的窗体值

（可选）您可以选择将 "共享到团队" 窗体上以下字段的默认值设置为：

* 说出有关此的`msgText`内容（）
* 赋值说明（`assignInstr`）
* 工作分配标题`assignTitle`（）

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
