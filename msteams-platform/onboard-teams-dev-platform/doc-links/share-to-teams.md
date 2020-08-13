---
title: 向网站添加 "共享到团队" 按钮
description: 如何将共享添加到你的网站上的工作组嵌入式按钮
keywords: 共享团队共享与团队共享
ms.openlocfilehash: 0ebd47af068bf523f27c19241b85d2137af3ada6
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651894"
---
# <a name="adding-a-share-to-teams-button-to-your-website"></a>向网站添加 "共享到团队" 按钮

>[!NOTE]
> * 仅支持桌面版本的 Edge 和 Chrome。
> * 不支持使用 Freemium 或来宾帐户。

第三方网站可以使用启动器脚本在其网页上嵌入 "团队" 按钮共享，在单击时，将启动共享，以在弹出窗口中体验到团队的体验。 这将允许您在不切换上下文的情况下直接与任何人或 Microsoft 团队频道共享链接。

![共享到团队弹出菜单](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a>如何向团队按钮中嵌入共享

首先，你需要 `launcher.js` 在你的网页上添加脚本。

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

接下来，使用 `teams-share-button` class 属性和要在属性中共享的链接，在您的网页上添加一个 HTML 元素 `data-href` 。

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

这将向您的网站添加 Microsoft 团队图标。

!["共享到团队" 图标](~/assets/icons/share-to-teams-icon.png)

（可选）如果您希望 "共享到团队" 按钮的图标大小不同，请使用 `data-icon-px-size` 属性。

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

如果您知道要共享的链接中的 URL 预览，团队中将不会很好地呈现 (例如，此链接需要用户身份验证) 您可以通过将该 `data-preview` 属性设置为来禁用 URL 预览 `false` 。

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

如果您的页面动态呈现内容，则可以使用此 `shareToMicrosoftTeams.renderButtons()` 方法强制在管道中的适当位置呈现 "**共享**" 按钮。

## <a name="crafting-your-website-preview"></a>编制网站预览

当您的网站与团队共享时，插入到选定频道的卡片将包含您的网站的预览。 您可以通过确保将适当的元数据添加到正在 (URL) 共享的网站来控制此预览的行为 `data-href` 。 下表概述了必要的标记。 您可以使用 html 默认版本或打开的图形版本。

为了显示预览，必须执行以下操作：

* 包含缩略图图像，或同时包含标题和说明 (以获得最佳结果，请包含所有三个) 。
* 共享的 URL 不需要身份验证。 如果仍可以共享，则不会创建预览。

|值|Meta 标记| 打开图形|
|----|----|----|
|标题|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|说明|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|缩略图图像| 无 |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a>共享到教育版团队

对于使用 "共享到团队" 按钮的教师，你将向你提供其他选项 `Create an Assignment` 。 这使您可以基于共享链接快速创建所选团队中的工作分配。

![共享到团队弹出菜单](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>完整 launcher.js 定义

| 属性 | HTML 属性 | 类型 | 默认值 | 说明 |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | 不适用 | 要共享的内容的 href。 |
| preview | `data-preview` | 字符串形式的布尔值 ()  | `true` | 是否显示要共享的内容的预览。 |
| iconPxSize | `data-icon-px-size` |  (字符串形式的数字)  | `32` | 要呈现的 "要呈现的团队共享" 按钮的大小（以像素为单位）。 |
| msgText | `data-msg-text` | string | 不适用 | 在邮件撰写框中的链接前插入的默认文本 (200 个字符的限制)  |
| assignInstr | `data-assign-instr` | string | 不适用 | 要插入到 "说明" 字段中的默认文本 (200 字符的限制)  |
| assignTitle | `data-assign-title` | string | 不适用 | 要插入到工作分配 "标题" 域中的默认文本 (50 个字符的限制)  |

### <a name="methods"></a>方法

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (可选) ：`{ elements?: HTMLElement[] }`

呈现当前页面上的所有共享按钮。 如果一个可选 `options` 对象与一个元素列表一起提供，则这些元素将呈现在 "共享" 按钮中。

### <a name="setting-default-form-values"></a>设置默认的窗体值

（可选）您可以选择将 "共享到团队" 窗体上以下字段的默认值设置为：

* 说出有关此 (的事项 `msgText`) 
*  () 的分配说明 `assignInstr`
* 工作分配标题 (`assignTitle`) 

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
