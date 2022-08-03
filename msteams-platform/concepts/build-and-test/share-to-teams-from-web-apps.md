---
title: 从 Web 应用共享到 Teams
description: 使用代码示例，了解如何通过网站预览将“共享到 Teams”嵌入式按钮添加到网站上。
ms.topic: reference
ms.localizationpriority: medium
ms.openlocfilehash: 1d7b9b6ae80b224e67f24a589fae5e6af7e7f839
ms.sourcegitcommit: 990a36fb774e614146444d4adaa2c9bcdb835998
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2022
ms.locfileid: "67232335"
---
# <a name="share-to-teams-from-web-apps"></a>从 Web 应用共享到 Teams

第三方网站可使用启动器脚本将“共享到 Teams”按钮添加到其网页上。 选择“共享到 Teams”按钮时，它会在弹出窗口中启动“共享到 Teams”体验。 这使你无需切换上下文，即可将链接直接共享给任何人或任何 Microsoft Teams 频道。

下图显示“共享到 Teams”预览体验的弹出窗口：

:::image type="content" source="~/assets/images/share-to-teams-popup.png" alt-text="“共享到 Teams”弹出窗口":::

> [!NOTE]
>
> * 仅支持桌面版的 Microsoft&nbsp;Edge 和 Google Chrome。
> * 不支持使用免费增值或来宾帐户。

还可以为 Web 应用、个人应用或选项卡中托管的“共享到 Teams”按钮共享的链接添加链接展开。有关详细信息，请参阅 [链接展开](~/messaging-extensions/how-to/link-unfurling.md)。

下图显示通过“共享到 Teams”按钮展开体验的链接：

:::image type="content" source="~/assets/images/share-to-teams-link-unfurling.png" alt-text="“共享到 Teams”链接展开":::

本文介绍如何为网站创建和嵌入“共享到 Teams”按钮、制作网站预览版，以及如何将“共享”扩展到Teams 教育版。

请参阅以下视频，了解如何嵌入“共享到 Teams”按钮：
<br>
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4vhWH]
<br>

## <a name="embed-a-share-to-teams-button"></a>嵌入“共享到 Teams”按钮

1. 在网页上添加 `launcher.js` 脚本。

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. 使用 `teams-share-button` 类属性和“在 `data-href` 属性中共享”链接在网页上添加 HTML 元素。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    完成此操作后，Teams 图标将添加到您的网站。 下图显示了“共享到 Teams”图标：

    :::image type="content" source="~/assets/icons/share-to-teams-icon.png" alt-text="“共享到 Teams”图标":::

1. 或者，如果希望“共享到 Teams”按钮的图标大小不同，请使用该 `data-icon-px-size` 属性。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```

1. 如果共享链接需要用户身份验证，并且要共享的链接中的 URL 预览在 Teams 中呈现不正常，则可以通过将属性设置添加 `data-preview` 到 `false`来禁用 URL 预览。

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. 若要在撰写框中显示所选消息，可在属性中 `data-msg-text` 定义文本。

     ```html
     <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-msg-text="<default-message-to-be-populated-in-compose-box>"
      data-preview="false">
      </div>
     ```

1. 如果页面动态呈现内容，可使用 `shareToMicrosoftTeams.renderButtons()` 方法来强制 **Share** 在管道中的适当位置呈现。

## <a name="craft-your-website-preview"></a>创建网站预览

将网站共享到 Teams 时，插入到所选频道中的卡片包含网站预览。 可通过确保将适当的元数据添加到要共享的网站（如 `data-href` URL）来控制此预览的行为。  

若要显示预览：

* 必须包含 **缩略图**，或同时包含 **标题** 和 **说明**。 为获得最佳结果，请包括全部三项。
* 共享 URL 不需要身份验证。 如果需要身份验证，可以共享，但未创建预览版。

下表概述了必要的标记：

|值|Meta 标记| Open Graph|
|----|----|----|
|标题|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|说明|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|缩略图| 无。 |`<meta property="og:image" content="http://example.com/image.jpg">`|

可使用 HTML 默认版本或 Open Graph 版本。

## <a name="share-to-teams-for-education"></a>“共享到 Teams”教育版

对于使用“共享到 Teams”按钮的教师，还有一个附加选项 `Create an Assignment` ，可让你基于共享链接在所选团队中快速创建作业。 下图显示了“共享到 Teams”教育版：

:::image type="content" source="../../assets/images/share-to-teams-popup-edu.png" alt-text="共享到 Teams 弹出式教育":::

## <a name="full-launcherjs-definition"></a>完整 launcher.js 定义

| 属性 | HTML 属性 | 类型 | 默认值 | 说明 |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | 不适用 | 要共享的内容的 href。 |
| preview | `data-preview` | Boolean（作为字符串） | `true` | 是否显示要共享的内容的预览。 |
| iconPxSize | `data-icon-px-size` | number（作为字符串） | `32` | 要呈现的“共享到 Teams”按钮的大小（以像素为单位）。 |
| msgText | `data-msg-text` | string | 不适用 | 要在消息撰写框中的链接前面插入的默认文本。 最大字符数为 200。 |
| assignInstr | `data-assign-instr` | string | 不适用 | 要在分配“说明”字段中插入的默认文本。 最大字符数为 200。 |
| assignTitle | `data-assign-title` | string | 不适用 | 要在分配“标题”字段中插入的默认文本。 最大字符数为 50。 |

### <a name="methods"></a>方法

**`shareToMicrosoftTeams.renderButtons(options)`**

`options`（可选）：`{ elements?: HTMLElement[] }`

目前，所有共享按钮都呈现在页面上。 如果向可选 `options` 对象提供一系列元素，这些元素将呈现为共享按钮。

### <a name="set-default-form-values"></a>设置默认表单值

可选择将“共享到 Teams”表单上的以下字段设置为默认值：

* 提供描述：`msgText`
* 分配说明：`assignInstr`
* 分配标题：`assignTitle`

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
* [从个人应用或选项卡共享到 Teams](share-to-teams-from-personal-app-or-tab.md)
