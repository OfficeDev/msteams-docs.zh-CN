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
# <a name="adding-a-share-to-teams-button-to-your-website"></a><span data-ttu-id="e2d12-104">向网站添加 "共享到团队" 按钮</span><span class="sxs-lookup"><span data-stu-id="e2d12-104">Adding a Share to Teams button to your website</span></span>

>[!NOTE]
> * <span data-ttu-id="e2d12-105">仅支持桌面版本的 Edge 和 Chrome。</span><span class="sxs-lookup"><span data-stu-id="e2d12-105">Only the desktop versions of Edge and Chrome are supported.</span></span>
> * <span data-ttu-id="e2d12-106">不支持使用 Freemium 或来宾帐户。</span><span class="sxs-lookup"><span data-stu-id="e2d12-106">Use of Freemium or guest accounts is not supported.</span></span>

<span data-ttu-id="e2d12-107">第三方网站可以使用启动器脚本在其网页上嵌入 "团队" 按钮共享，在单击时，将启动共享，以在弹出窗口中体验到团队的体验。</span><span class="sxs-lookup"><span data-stu-id="e2d12-107">Third-party websites can use the launcher script to embed Share to Teams buttons on their webpages which will launch the Share to Teams experience in a popup window when clicked.</span></span> <span data-ttu-id="e2d12-108">这将允许您在不切换上下文的情况下直接与任何人或 Microsoft 团队频道共享链接。</span><span class="sxs-lookup"><span data-stu-id="e2d12-108">This will allow you to share a link directly to any person or Microsoft Teams channel without switching context.</span></span>

![共享到团队弹出菜单](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a><span data-ttu-id="e2d12-110">如何向团队按钮中嵌入共享</span><span class="sxs-lookup"><span data-stu-id="e2d12-110">How to embed a Share to Teams button</span></span>

<span data-ttu-id="e2d12-111">首先，你需要 `launcher.js` 在你的网页上添加脚本。</span><span class="sxs-lookup"><span data-stu-id="e2d12-111">First, you'll need to add the `launcher.js` script on your webpage.</span></span>

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

<span data-ttu-id="e2d12-112">接下来，使用 `teams-share-button` class 属性和要在属性中共享的链接，在您的网页上添加一个 HTML 元素 `data-href` 。</span><span class="sxs-lookup"><span data-stu-id="e2d12-112">Next, add an HTML element on your webpage with the `teams-share-button` class attribute and the link to share in the `data-href` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

<span data-ttu-id="e2d12-113">这将向您的网站添加 Microsoft 团队图标。</span><span class="sxs-lookup"><span data-stu-id="e2d12-113">This will add the Microsoft Teams icon to your website.</span></span>

!["共享到团队" 图标](~/assets/icons/share-to-teams-icon.png)

<span data-ttu-id="e2d12-115">（可选）如果您希望 "共享到团队" 按钮的图标大小不同，请使用 `data-icon-px-size` 属性。</span><span class="sxs-lookup"><span data-stu-id="e2d12-115">Optionally, if you want a different icon size for the Share to Teams button, use the `data-icon-px-size` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

<span data-ttu-id="e2d12-116">如果您知道要共享的链接中的 URL 预览，团队中将不会很好地呈现 (例如，此链接需要用户身份验证) 您可以通过将该 `data-preview` 属性设置为来禁用 URL 预览 `false` 。</span><span class="sxs-lookup"><span data-stu-id="e2d12-116">If you know that the URL preview from your link to be shared won't render well in Teams (for example the link would require user authentication) you can disable the URL preview by adding the `data-preview` attribute set to `false`.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

<span data-ttu-id="e2d12-117">如果您的页面动态呈现内容，则可以使用此 `shareToMicrosoftTeams.renderButtons()` 方法强制在管道中的适当位置呈现 "**共享**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="e2d12-117">If your page dynamically renders content, you can use the the `shareToMicrosoftTeams.renderButtons()` method to force the **Share** button to render at the appropriate place in the pipeline.</span></span>

## <a name="crafting-your-website-preview"></a><span data-ttu-id="e2d12-118">编制网站预览</span><span class="sxs-lookup"><span data-stu-id="e2d12-118">Crafting your website preview</span></span>

<span data-ttu-id="e2d12-119">当您的网站与团队共享时，插入到选定频道的卡片将包含您的网站的预览。</span><span class="sxs-lookup"><span data-stu-id="e2d12-119">When your website is shared to Teams, the card that is inserted into the selected channel will contain a preview of your website.</span></span> <span data-ttu-id="e2d12-120">您可以通过确保将适当的元数据添加到正在 (URL) 共享的网站来控制此预览的行为 `data-href` 。</span><span class="sxs-lookup"><span data-stu-id="e2d12-120">You can control the behavior of this preview by ensuring the appropriate meta-data is added to the website being shared (the `data-href` URL).</span></span> <span data-ttu-id="e2d12-121">下表概述了必要的标记。</span><span class="sxs-lookup"><span data-stu-id="e2d12-121">The table below outlines the necessary tags.</span></span> <span data-ttu-id="e2d12-122">您可以使用 html 默认版本或打开的图形版本。</span><span class="sxs-lookup"><span data-stu-id="e2d12-122">You can use either the html default versions, or the Open Graph version.</span></span>

<span data-ttu-id="e2d12-123">为了显示预览，必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="e2d12-123">In order for the preview to be displayed you must:</span></span>

* <span data-ttu-id="e2d12-124">包含缩略图图像，或同时包含标题和说明 (以获得最佳结果，请包含所有三个) 。</span><span class="sxs-lookup"><span data-stu-id="e2d12-124">Include either a Thumbnail image, or both a Title and Description (for best results, include all three).</span></span>
* <span data-ttu-id="e2d12-125">共享的 URL 不需要身份验证。</span><span class="sxs-lookup"><span data-stu-id="e2d12-125">The URL being shared cannot require authentication.</span></span> <span data-ttu-id="e2d12-126">如果仍可以共享，则不会创建预览。</span><span class="sxs-lookup"><span data-stu-id="e2d12-126">If it does you can still share it, but the preview will not be created.</span></span>

|<span data-ttu-id="e2d12-127">值</span><span class="sxs-lookup"><span data-stu-id="e2d12-127">Value</span></span>|<span data-ttu-id="e2d12-128">Meta 标记</span><span class="sxs-lookup"><span data-stu-id="e2d12-128">Meta tag</span></span>| <span data-ttu-id="e2d12-129">打开图形</span><span class="sxs-lookup"><span data-stu-id="e2d12-129">Open Graph</span></span>|
|----|----|----|
|<span data-ttu-id="e2d12-130">标题</span><span class="sxs-lookup"><span data-stu-id="e2d12-130">Title</span></span>|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|<span data-ttu-id="e2d12-131">说明</span><span class="sxs-lookup"><span data-stu-id="e2d12-131">Description</span></span>|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|<span data-ttu-id="e2d12-132">缩略图图像</span><span class="sxs-lookup"><span data-stu-id="e2d12-132">Thumbnail Image</span></span>| <span data-ttu-id="e2d12-133">无</span><span class="sxs-lookup"><span data-stu-id="e2d12-133">none</span></span> |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a><span data-ttu-id="e2d12-134">共享到教育版团队</span><span class="sxs-lookup"><span data-stu-id="e2d12-134">Share to Teams for Education</span></span>

<span data-ttu-id="e2d12-135">对于使用 "共享到团队" 按钮的教师，你将向你提供其他选项 `Create an Assignment` 。</span><span class="sxs-lookup"><span data-stu-id="e2d12-135">For teachers using the Share to Teams button you'll be given an additional option to `Create an Assignment`.</span></span> <span data-ttu-id="e2d12-136">这使您可以基于共享链接快速创建所选团队中的工作分配。</span><span class="sxs-lookup"><span data-stu-id="e2d12-136">This enables you to quickly create an assignment in the chosen Team based on the shared link.</span></span>

![共享到团队弹出菜单](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a><span data-ttu-id="e2d12-138">完整 launcher.js 定义</span><span class="sxs-lookup"><span data-stu-id="e2d12-138">Full launcher.js definition</span></span>

| <span data-ttu-id="e2d12-139">属性</span><span class="sxs-lookup"><span data-stu-id="e2d12-139">Property</span></span> | <span data-ttu-id="e2d12-140">HTML 属性</span><span class="sxs-lookup"><span data-stu-id="e2d12-140">HTML attribute</span></span> | <span data-ttu-id="e2d12-141">类型</span><span class="sxs-lookup"><span data-stu-id="e2d12-141">Type</span></span> | <span data-ttu-id="e2d12-142">默认值</span><span class="sxs-lookup"><span data-stu-id="e2d12-142">Default</span></span> | <span data-ttu-id="e2d12-143">说明</span><span class="sxs-lookup"><span data-stu-id="e2d12-143">Description</span></span> |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| <span data-ttu-id="e2d12-144">href</span><span class="sxs-lookup"><span data-stu-id="e2d12-144">href</span></span> | `data-href` | <span data-ttu-id="e2d12-145">string</span><span class="sxs-lookup"><span data-stu-id="e2d12-145">string</span></span> | <span data-ttu-id="e2d12-146">不适用</span><span class="sxs-lookup"><span data-stu-id="e2d12-146">n/a</span></span> | <span data-ttu-id="e2d12-147">要共享的内容的 href。</span><span class="sxs-lookup"><span data-stu-id="e2d12-147">The href of the content to share.</span></span> |
| <span data-ttu-id="e2d12-148">preview</span><span class="sxs-lookup"><span data-stu-id="e2d12-148">preview</span></span> | `data-preview` | <span data-ttu-id="e2d12-149">字符串形式的布尔值 () </span><span class="sxs-lookup"><span data-stu-id="e2d12-149">boolean (as a string)</span></span> | `true` | <span data-ttu-id="e2d12-150">是否显示要共享的内容的预览。</span><span class="sxs-lookup"><span data-stu-id="e2d12-150">Whether or not to show a preview of the content to share.</span></span> |
| <span data-ttu-id="e2d12-151">iconPxSize</span><span class="sxs-lookup"><span data-stu-id="e2d12-151">iconPxSize</span></span> | `data-icon-px-size` | <span data-ttu-id="e2d12-152"> (字符串形式的数字) </span><span class="sxs-lookup"><span data-stu-id="e2d12-152">number (as a string)</span></span> | `32` | <span data-ttu-id="e2d12-153">要呈现的 "要呈现的团队共享" 按钮的大小（以像素为单位）。</span><span class="sxs-lookup"><span data-stu-id="e2d12-153">The size in pixels of the Share-to-Teams button to render.</span></span> |
| <span data-ttu-id="e2d12-154">msgText</span><span class="sxs-lookup"><span data-stu-id="e2d12-154">msgText</span></span> | `data-msg-text` | <span data-ttu-id="e2d12-155">string</span><span class="sxs-lookup"><span data-stu-id="e2d12-155">string</span></span> | <span data-ttu-id="e2d12-156">不适用</span><span class="sxs-lookup"><span data-stu-id="e2d12-156">n/a</span></span> | <span data-ttu-id="e2d12-157">在邮件撰写框中的链接前插入的默认文本 (200 个字符的限制) </span><span class="sxs-lookup"><span data-stu-id="e2d12-157">Default Text to be inserted before the link in the message compose box (200 character limit)</span></span> |
| <span data-ttu-id="e2d12-158">assignInstr</span><span class="sxs-lookup"><span data-stu-id="e2d12-158">assignInstr</span></span> | `data-assign-instr` | <span data-ttu-id="e2d12-159">string</span><span class="sxs-lookup"><span data-stu-id="e2d12-159">string</span></span> | <span data-ttu-id="e2d12-160">不适用</span><span class="sxs-lookup"><span data-stu-id="e2d12-160">n/a</span></span> | <span data-ttu-id="e2d12-161">要插入到 "说明" 字段中的默认文本 (200 字符的限制) </span><span class="sxs-lookup"><span data-stu-id="e2d12-161">Default Text to be inserted in the assignments "Instructions" field (200 character limit)</span></span> |
| <span data-ttu-id="e2d12-162">assignTitle</span><span class="sxs-lookup"><span data-stu-id="e2d12-162">assignTitle</span></span> | `data-assign-title` | <span data-ttu-id="e2d12-163">string</span><span class="sxs-lookup"><span data-stu-id="e2d12-163">string</span></span> | <span data-ttu-id="e2d12-164">不适用</span><span class="sxs-lookup"><span data-stu-id="e2d12-164">n/a</span></span> | <span data-ttu-id="e2d12-165">要插入到工作分配 "标题" 域中的默认文本 (50 个字符的限制) </span><span class="sxs-lookup"><span data-stu-id="e2d12-165">Default Text to be inserted in the assignments "Title" field (50 character limit)</span></span> |

### <a name="methods"></a><span data-ttu-id="e2d12-166">方法</span><span class="sxs-lookup"><span data-stu-id="e2d12-166">Methods</span></span>

**`shareToMicrosoftTeams.renderButtons(options)`**

<span data-ttu-id="e2d12-167">`options` (可选) ：`{ elements?: HTMLElement[] }`</span><span class="sxs-lookup"><span data-stu-id="e2d12-167">`options` (optional): `{ elements?: HTMLElement[] }`</span></span>

<span data-ttu-id="e2d12-168">呈现当前页面上的所有共享按钮。</span><span class="sxs-lookup"><span data-stu-id="e2d12-168">Renders all share buttons currently on the page.</span></span> <span data-ttu-id="e2d12-169">如果一个可选 `options` 对象与一个元素列表一起提供，则这些元素将呈现在 "共享" 按钮中。</span><span class="sxs-lookup"><span data-stu-id="e2d12-169">If an optional `options` object is supplied with a list of elements, those elements will be rendered into share buttons.</span></span>

### <a name="setting-default-form-values"></a><span data-ttu-id="e2d12-170">设置默认的窗体值</span><span class="sxs-lookup"><span data-stu-id="e2d12-170">Setting default form values</span></span>

<span data-ttu-id="e2d12-171">（可选）您可以选择将 "共享到团队" 窗体上以下字段的默认值设置为：</span><span class="sxs-lookup"><span data-stu-id="e2d12-171">Optionally, you can choose to set default values for the following fields on the Share to Teams form:</span></span>

* <span data-ttu-id="e2d12-172">说出有关此 (的事项 `msgText`) </span><span class="sxs-lookup"><span data-stu-id="e2d12-172">Say something about this (`msgText`)</span></span>
* <span data-ttu-id="e2d12-173"> () 的分配说明 `assignInstr`</span><span class="sxs-lookup"><span data-stu-id="e2d12-173">Assignment Instructions (`assignInstr`)</span></span>
* <span data-ttu-id="e2d12-174">工作分配标题 (`assignTitle`) </span><span class="sxs-lookup"><span data-stu-id="e2d12-174">Assignment Title (`assignTitle`)</span></span>

#### <a name="example-default-form-values"></a><span data-ttu-id="e2d12-175">示例：默认表单值</span><span class="sxs-lookup"><span data-stu-id="e2d12-175">Example: Default form values</span></span>

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```
