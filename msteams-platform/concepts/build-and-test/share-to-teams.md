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
# <a name="create-a-share-to-teams-button-for-your-website"></a><span data-ttu-id="3ec0f-104">为网站创建“共享到 Teams”按钮</span><span class="sxs-lookup"><span data-stu-id="3ec0f-104">Create a Share-to-Teams button for your website</span></span>

>[!NOTE]
> * <span data-ttu-id="3ec0f-105">仅支持桌面版 Edge 和 Chrome。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-105">Only the desktop versions of Edge and Chrome are supported.</span></span>
> * <span data-ttu-id="3ec0f-106">不支持使用免费增值帐户或来宾帐户。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-106">Use of Freemium or guest accounts is not supported.</span></span>

<span data-ttu-id="3ec0f-107">第三方网站可以使用启动器脚本在其网页上嵌入"共享到 Teams"按钮，这将在单击时在弹出窗口中启动"共享到 Teams"体验。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-107">Third-party websites can use the launcher script to embed Share to Teams buttons on their webpages which will launch the Share to Teams experience in a popup window when clicked.</span></span> <span data-ttu-id="3ec0f-108">这将允许你直接将链接共享给任何人或 Microsoft Teams 频道，而无需切换上下文。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-108">This will allow you to share a link directly to any person or Microsoft Teams channel without switching context.</span></span>

![共享到 Teams 弹出窗口](~/assets/images/share-to-teams-popup.png)

## <a name="how-to-embed-a-share-to-teams-button"></a><span data-ttu-id="3ec0f-110">如何嵌入"共享到 Teams"按钮</span><span class="sxs-lookup"><span data-stu-id="3ec0f-110">How to embed a Share to Teams button</span></span>

<span data-ttu-id="3ec0f-111">首先，您需要在网页上 `launcher.js` 添加脚本。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-111">First, you'll need to add the `launcher.js` script on your webpage.</span></span>

```html
<script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
```

<span data-ttu-id="3ec0f-112">接下来，在网页上添加一个 HTML 元素，该元素包含类属性和在属性 `teams-share-button` 中共享 `data-href` 的链接。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-112">Next, add an HTML element on your webpage with the `teams-share-button` class attribute and the link to share in the `data-href` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>">
</div>
```

<span data-ttu-id="3ec0f-113">这会将 Microsoft Teams 图标添加到你的网站。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-113">This will add the Microsoft Teams icon to your website.</span></span>

![共享到 Teams 图标](~/assets/icons/share-to-teams-icon.png)

<span data-ttu-id="3ec0f-115">（可选）如果需要"共享到 Teams"按钮的不同图标大小，请使用 `data-icon-px-size` 该属性。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-115">Optionally, if you want a different icon size for the Share to Teams button, use the `data-icon-px-size` attribute.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-icon-px-size="64">
</div>
```

<span data-ttu-id="3ec0f-116">如果你知道要共享的链接中的 URL 预览不会在 Teams (例如，链接需要用户身份验证) 可以通过将属性集添加到禁用 URL 预览 `data-preview` `false` 。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-116">If you know that the URL preview from your link to be shared won't render well in Teams (for example the link would require user authentication) you can disable the URL preview by adding the `data-preview` attribute set to `false`.</span></span>

```html
<div
  class="teams-share-button"
  data-href="https://<link-to-be-shared>"
  data-preview="false">
</div>
```

<span data-ttu-id="3ec0f-117">如果页面动态呈现内容，可以使用该方法强制"共享"按钮在管道 `shareToMicrosoftTeams.renderButtons()` 中的适当位置呈现。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-117">If your page dynamically renders content, you can use the the `shareToMicrosoftTeams.renderButtons()` method to force the **Share** button to render at the appropriate place in the pipeline.</span></span>

## <a name="crafting-your-website-preview"></a><span data-ttu-id="3ec0f-118">精心制作网站预览</span><span class="sxs-lookup"><span data-stu-id="3ec0f-118">Crafting your website preview</span></span>

<span data-ttu-id="3ec0f-119">将你的网站共享到 Teams 时，插入到所选频道的卡片将包含你的网站的预览。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-119">When your website is shared to Teams, the card that is inserted into the selected channel will contain a preview of your website.</span></span> <span data-ttu-id="3ec0f-120">您可以通过确保向要共享的网站添加适当的元数据（通过 URL `data-href` (）来控制) 。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-120">You can control the behavior of this preview by ensuring the appropriate meta-data is added to the website being shared (the `data-href` URL).</span></span> <span data-ttu-id="3ec0f-121">下表概述了必要的标记。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-121">The table below outlines the necessary tags.</span></span> <span data-ttu-id="3ec0f-122">可以使用 html 默认版本或 Open Graph 版本。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-122">You can use either the html default versions, or the Open Graph version.</span></span>

<span data-ttu-id="3ec0f-123">若要显示预览，必须：</span><span class="sxs-lookup"><span data-stu-id="3ec0f-123">In order for the preview to be displayed you must:</span></span>

* <span data-ttu-id="3ec0f-124">包括缩略图图像，或同时包含标题和说明 (，以获得最佳效果，请包含所有三) 。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-124">Include either a Thumbnail image, or both a Title and Description (for best results, include all three).</span></span>
* <span data-ttu-id="3ec0f-125">要共享的 URL 不能要求身份验证。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-125">The URL being shared cannot require authentication.</span></span> <span data-ttu-id="3ec0f-126">如果是这样，你仍可以共享它，但无法创建预览。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-126">If it does you can still share it, but the preview will not be created.</span></span>

|<span data-ttu-id="3ec0f-127">值</span><span class="sxs-lookup"><span data-stu-id="3ec0f-127">Value</span></span>|<span data-ttu-id="3ec0f-128">Meta 标记</span><span class="sxs-lookup"><span data-stu-id="3ec0f-128">Meta tag</span></span>| <span data-ttu-id="3ec0f-129">Open Graph</span><span class="sxs-lookup"><span data-stu-id="3ec0f-129">Open Graph</span></span>|
|----|----|----|
|<span data-ttu-id="3ec0f-130">标题</span><span class="sxs-lookup"><span data-stu-id="3ec0f-130">Title</span></span>|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|<span data-ttu-id="3ec0f-131">说明</span><span class="sxs-lookup"><span data-stu-id="3ec0f-131">Description</span></span>|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|<span data-ttu-id="3ec0f-132">缩略图图像</span><span class="sxs-lookup"><span data-stu-id="3ec0f-132">Thumbnail Image</span></span>| <span data-ttu-id="3ec0f-133">无</span><span class="sxs-lookup"><span data-stu-id="3ec0f-133">none</span></span> |`<meta property="og:image" content="http://example.com/image.jpg">`|

## <a name="share-to-teams-for-education"></a><span data-ttu-id="3ec0f-134">共享到 Teams 教育</span><span class="sxs-lookup"><span data-stu-id="3ec0f-134">Share to Teams for Education</span></span>

<span data-ttu-id="3ec0f-135">对于使用"共享到 Teams"按钮的教师，你将获得一个附加选项 `Create an Assignment` 。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-135">For teachers using the Share to Teams button you'll be given an additional option to `Create an Assignment`.</span></span> <span data-ttu-id="3ec0f-136">这使您能够基于共享链接在所选团队中快速创建工作分配。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-136">This enables you to quickly create an assignment in the chosen Team based on the shared link.</span></span>

![共享到 Teams 弹出窗口](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a><span data-ttu-id="3ec0f-138">完整launcher.js定义</span><span class="sxs-lookup"><span data-stu-id="3ec0f-138">Full launcher.js definition</span></span>

| <span data-ttu-id="3ec0f-139">属性</span><span class="sxs-lookup"><span data-stu-id="3ec0f-139">Property</span></span> | <span data-ttu-id="3ec0f-140">HTML 属性</span><span class="sxs-lookup"><span data-stu-id="3ec0f-140">HTML attribute</span></span> | <span data-ttu-id="3ec0f-141">类型</span><span class="sxs-lookup"><span data-stu-id="3ec0f-141">Type</span></span> | <span data-ttu-id="3ec0f-142">默认值</span><span class="sxs-lookup"><span data-stu-id="3ec0f-142">Default</span></span> | <span data-ttu-id="3ec0f-143">说明</span><span class="sxs-lookup"><span data-stu-id="3ec0f-143">Description</span></span> |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| <span data-ttu-id="3ec0f-144">href</span><span class="sxs-lookup"><span data-stu-id="3ec0f-144">href</span></span> | `data-href` | <span data-ttu-id="3ec0f-145">string</span><span class="sxs-lookup"><span data-stu-id="3ec0f-145">string</span></span> | <span data-ttu-id="3ec0f-146">不适用</span><span class="sxs-lookup"><span data-stu-id="3ec0f-146">n/a</span></span> | <span data-ttu-id="3ec0f-147">要共享的内容的 href。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-147">The href of the content to share.</span></span> |
| <span data-ttu-id="3ec0f-148">preview</span><span class="sxs-lookup"><span data-stu-id="3ec0f-148">preview</span></span> | `data-preview` | <span data-ttu-id="3ec0f-149">boolean (作为字符串) </span><span class="sxs-lookup"><span data-stu-id="3ec0f-149">boolean (as a string)</span></span> | `true` | <span data-ttu-id="3ec0f-150">是否显示要共享的内容的预览。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-150">Whether or not to show a preview of the content to share.</span></span> |
| <span data-ttu-id="3ec0f-151">iconPxSize</span><span class="sxs-lookup"><span data-stu-id="3ec0f-151">iconPxSize</span></span> | `data-icon-px-size` | <span data-ttu-id="3ec0f-152">number (作为字符串) </span><span class="sxs-lookup"><span data-stu-id="3ec0f-152">number (as a string)</span></span> | `32` | <span data-ttu-id="3ec0f-153">要呈现的"共享到 Teams"按钮的大小（以像素为单位）。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-153">The size in pixels of the Share-to-Teams button to render.</span></span> |
| <span data-ttu-id="3ec0f-154">msgText</span><span class="sxs-lookup"><span data-stu-id="3ec0f-154">msgText</span></span> | `data-msg-text` | <span data-ttu-id="3ec0f-155">string</span><span class="sxs-lookup"><span data-stu-id="3ec0f-155">string</span></span> | <span data-ttu-id="3ec0f-156">不适用</span><span class="sxs-lookup"><span data-stu-id="3ec0f-156">n/a</span></span> | <span data-ttu-id="3ec0f-157">在邮件撰写框中的链接之前插入的默认文本 (200 个字符) </span><span class="sxs-lookup"><span data-stu-id="3ec0f-157">Default Text to be inserted before the link in the message compose box (200 character limit)</span></span> |
| <span data-ttu-id="3ec0f-158">assignInstr</span><span class="sxs-lookup"><span data-stu-id="3ec0f-158">assignInstr</span></span> | `data-assign-instr` | <span data-ttu-id="3ec0f-159">string</span><span class="sxs-lookup"><span data-stu-id="3ec0f-159">string</span></span> | <span data-ttu-id="3ec0f-160">不适用</span><span class="sxs-lookup"><span data-stu-id="3ec0f-160">n/a</span></span> | <span data-ttu-id="3ec0f-161">要插入到工作分配"说明"字段中的默认文本 (200 个字符) </span><span class="sxs-lookup"><span data-stu-id="3ec0f-161">Default Text to be inserted in the assignments "Instructions" field (200 character limit)</span></span> |
| <span data-ttu-id="3ec0f-162">assignTitle</span><span class="sxs-lookup"><span data-stu-id="3ec0f-162">assignTitle</span></span> | `data-assign-title` | <span data-ttu-id="3ec0f-163">string</span><span class="sxs-lookup"><span data-stu-id="3ec0f-163">string</span></span> | <span data-ttu-id="3ec0f-164">不适用</span><span class="sxs-lookup"><span data-stu-id="3ec0f-164">n/a</span></span> | <span data-ttu-id="3ec0f-165">要插入到工作分配"标题"字段中的默认文本 (50 个字符) </span><span class="sxs-lookup"><span data-stu-id="3ec0f-165">Default Text to be inserted in the assignments "Title" field (50 character limit)</span></span> |

### <a name="methods"></a><span data-ttu-id="3ec0f-166">方法</span><span class="sxs-lookup"><span data-stu-id="3ec0f-166">Methods</span></span>

**`shareToMicrosoftTeams.renderButtons(options)`**

<span data-ttu-id="3ec0f-167">`options` (可选) ： `{ elements?: HTMLElement[] }`</span><span class="sxs-lookup"><span data-stu-id="3ec0f-167">`options` (optional): `{ elements?: HTMLElement[] }`</span></span>

<span data-ttu-id="3ec0f-168">呈现页面上当前的所有共享按钮。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-168">Renders all share buttons currently on the page.</span></span> <span data-ttu-id="3ec0f-169">如果随元素列表一起提供可选对象，则 `options` 这些元素将呈现到共享按钮中。</span><span class="sxs-lookup"><span data-stu-id="3ec0f-169">If an optional `options` object is supplied with a list of elements, those elements will be rendered into share buttons.</span></span>

### <a name="setting-default-form-values"></a><span data-ttu-id="3ec0f-170">设置默认表单值</span><span class="sxs-lookup"><span data-stu-id="3ec0f-170">Setting default form values</span></span>

<span data-ttu-id="3ec0f-171">（可选）你可以选择在"共享到 Teams"表单上设置以下字段的默认值：</span><span class="sxs-lookup"><span data-stu-id="3ec0f-171">Optionally, you can choose to set default values for the following fields on the Share to Teams form:</span></span>

* <span data-ttu-id="3ec0f-172">说出有关此 `msgText` () </span><span class="sxs-lookup"><span data-stu-id="3ec0f-172">Say something about this (`msgText`)</span></span>
* <span data-ttu-id="3ec0f-173">工作分配 `assignInstr` () </span><span class="sxs-lookup"><span data-stu-id="3ec0f-173">Assignment Instructions (`assignInstr`)</span></span>
* <span data-ttu-id="3ec0f-174">工作分配 `assignTitle` () </span><span class="sxs-lookup"><span data-stu-id="3ec0f-174">Assignment Title (`assignTitle`)</span></span>

#### <a name="example-default-form-values"></a><span data-ttu-id="3ec0f-175">示例：默认表单值</span><span class="sxs-lookup"><span data-stu-id="3ec0f-175">Example: Default form values</span></span>

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```
