---
title: 从 Web 应用共享到Teams
description: 了解如何使用代码示例，通过网站预览将"共享"添加到网站上Teams嵌入按钮
ms.topic: reference
ms.localizationpriority: medium
keywords: 共享Teams共享以Teams
ms.openlocfilehash: ac08d3c697bc5f02eb8527d2239afe022cb421af
ms.sourcegitcommit: f892125106adb6731a20127f15d6e92f279127c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2022
ms.locfileid: "64685660"
---
# <a name="share-to-teams-from-web-apps"></a>从 Web 应用共享到Teams

第三方网站可以使用启动器脚本将"共享"嵌入到其网页上Teams按钮。 选择时，它将启动"共享"，以在弹出窗口中Teams体验。 这样便可以直接共享指向任何人或Microsoft Teams通道的链接，而无需切换上下文。 本文档介绍如何为网站创建和嵌入"共享到Teams"按钮、制作网站预览版，以及如何将"共享"扩展到Teams 教育版。

> [!NOTE]
>
> * 仅支持 MicrosoftEdge&nbsp; 和 Google Chrome 的桌面版本。
> * 不支持使用 Freemium 或来宾帐户。  

下图显示"共享"以Teams弹出窗口体验：

:::image type="content" source="../../assets/images/share-to-teams-popup.png" alt-text="共享到Teams弹出窗口":::

## <a name="embed-a-share-to-teams-button"></a>"将共享嵌入到Teams"按钮

1. 在 `launcher.js` 网页上添加脚本。

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. 在网页上添加 HTML 元素， `teams-share-button` 其中包含类属性和要在属性中共享的 `data-href` 链接。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    完成此操作后，Microsoft Teams图标将添加到网站。 下图显示了"共享到Teams"图标：

    !["共享到Teams"图标](~/assets/icons/share-to-teams-icon.png)

1. 或者，如果希望"共享到Teams"按钮具有不同的图标大小，请使用该`data-icon-px-size`属性。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```

1. 如果共享链接需要用户身份验证，并且要共享的链接中的 URL 预览在Teams中呈现不良好，则可以通过将属性集添加`data-preview`到`false`该属性来禁用 URL 预览。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. 如果页面动态呈现内容，则可以使用 `shareToMicrosoftTeams.renderButtons()` 该方法强制 **Share** 在管道中的适当位置呈现。

## <a name="craft-your-website-preview"></a>创建网站预览

将网站共享到Teams时，插入到所选频道中的卡片包含网站预览。 可以通过确保将适当的元数据添加到要共享的网站（如 `data-href` URL）来控制此预览版的行为。  

若要显示预览版，请执行以下操作：

* 必须包括 **缩略图图像** 或 **标题** 和 **说明**。 为了获得最佳结果，请包括所有三个。
* 共享 URL 不需要身份验证。 如果需要身份验证，可以共享它，但未创建预览版。

下表概述了必要的标记：

|值|Meta 标记| 打开Graph|
|----|----|----|
|标题|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|说明|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|缩略图图像| 没有。 |`<meta property="og:image" content="http://example.com/image.jpg">`|

可以使用 HTML 默认版本或 Open Graph 版本。

## <a name="share-to-teams-for-education"></a>共享到Teams 教育版

对于使用"共享"按钮Teams教师，还有一个附加选项。`Create an Assignment` 这使你能够基于共享链接在所选团队中快速创建分配。 下图显示了用于教育的"共享到Teams"：

:::image type="content" source="../../assets/images/share-to-teams-popup-edu.png" alt-text="共享到Teams弹出式教育":::

## <a name="full-launcherjs-definition"></a>完整launcher.js定义

| 属性 | HTML 属性 | 类型 | 默认值 | 说明 |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | 不适用 | 要共享的内容的 href。 |
| preview | `data-preview` | 布尔 (作为字符串)  | `true` | 是否显示要共享的内容的预览。 |
| iconPxSize | `data-icon-px-size` | 数字 (为字符串)  | `32` | 要呈现的"共享到Teams"按钮的大小（以像素为单位）。 |
| msgText | `data-msg-text` | string | 不适用 | 要在邮件撰写框中的链接之前插入的默认文本。 最大字符数为 200。 |
| assignInstr | `data-assign-instr` | string | 不适用 | 要插入作业"说明"字段中的默认文本。 最大字符数为 200。 |
| assignTitle | `data-assign-title` | string | 不适用 | 要插入作业"标题"字段中的默认文本。 最大字符数为 50。 |

### <a name="methods"></a>Methods

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (可选) ： `{ elements?: HTMLElement[] }`

目前，所有共享按钮都呈现在页面上。 如果向可选 `options` 对象提供元素列表，则这些元素将呈现为共享按钮。

### <a name="set-default-form-values"></a>设置默认表单值

可以选择将"共享"上的以下字段的默认值设置为Teams窗体：

* 对此说些什么： `msgText`
* 分配说明： `assignInstr`
* 分配标题： `assignTitle`

#### <a name="example"></a>示例

 以下示例中给出了默认表单值：

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

* [集成 web 应用](~/samples/integrate-web-apps-overview.md)
* [从个人应用或选项卡共享到Teams](share-to-teams-from-personal-app-or-tab.md)
